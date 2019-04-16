## AWS를 이용해 Node API 백엔드 서버 만들기

### 소개

이번 문서는 Node API 서버를 클라우드에 띄워보고, API 서버이기 때문에 Swagger UI를 통해 요청과 응답에 대한 문서화를 진행할 것이다. 물론 개발에 대해서는 신경쓰지 않아도 된다! 고생은 이 글을 작성하는 내가 할테니 이 글을 읽는 당신은 그저 Swagger UI로 API 문서를 받아보면 되는 것이다(흡사 백엔드 개발자와 협업하는 프론트엔드 개발자).

### 준비물

- Node, Express 등 이번 프로젝트에서 사용되는 라이브러리 및 프레임워크 관련 지식
- 서버 관련 지식
- 클라우드 환경에서 나만의 API 서버를 구현하고 싶다는 열망
- git에 대한 이해도

### 들어가기 전에

- API 서버가 필요한 이유
- 우리가 사용할 도구(대표적인 것)들(node(typescript), express, swagger, nginx(optional), docker(optional) 등)
    - 위 도구들을 쓰는 이유
        - node, express: 서버 사이드 자바스크립트인 node와 node를 활용한 백엔드 프레임워크인 express를 사용하는 것이 바닐라 자바스크립트로 서버를 구현하는 것보다 상대적으로 높은 안정성과 높은 생산성을 유지할 수 있다.
        - swagger: Rest API의 처리 흐름을 가시적으로 볼 수 있고, 기존의 방식(postman 등)보다 상대적으로 높은 트러블 슈팅 프로세스를 유지할 수 있다. 하지만 그만큼 번거롭다.
        - nginx(optional): 안정적인 웹 서버를 위한 도구, 기존의 아파치와 비교해 상대적으로 높은 성능을 가지고 있다. 아파치는 요청당 쓰레드 할당하여 쓰레드를 많이 사용하는 구조 이고 nginx는 비동기이벤트 구조로 쓰레드를 적게 사용하는 구조를 지닌다.
        - docker(optional): 컨테이너 환경을 통해 실제 구동 환경과 개발 환경, 심지어 테스트 환경까지 거의 유사하게 구성하여 상대적으로 안정적이고 이슈 관리가 쉬운 환경 제공한다.

- 우리가 사용할 AWS 서비스(Lambda, CloudFront, S3)
    - 위 도구들을 쓰는 이유
        - Lambda: 컴퓨팅 파워를 위해 사용, EC2를 사용할 수도 있지만, 우리는 Docker를 사용할 예정이라 직접적으로 조작할 필요가 없음.
        - Cloud Front: 정적 파일 국제화(사실상 필요없지만 S3를 권장 옵션으로 사용하기 위함)
        - S3: 정적 데이터(파일, 이미지 등)을 저장하기 위한 storge
        - ECS: Docker의 이미지 배포(push) 및 배포한 이미지를 pull받아 사용하기 위해 사용

### 본문

우선 실습을 위한 node project를 만들어보자. 이번 실습의 뼈대는 [node backend boilerplate](https://github.com/rayjaywayjoe/rjwj.webback.boilerplate)를 사용한다. 이 뼈대는 필자가 미리 만들어뒀기 때문에 코드에 대한 별다른 작업없이 누구나 클라우드에 API 서버를 띄워보는 경험을 할 수 있다.

 ```
 git clone https://github.com/rayjaywayjoe/rjwj.webback.boilerplate.git
 ```

### 마지막으로

- 우리가 사용할 API 서버의 구조(아키텍처) -> 우선 만들어보고 구성해보기
