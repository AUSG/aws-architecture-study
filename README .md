기간 : 2019년 2월 13일 ~ 2019년 2월 17일 

주제 : 서버리스 웹 애플리케이션 구축

난이도 : 하

============

이 자습서에서는 사용자가 Wild Ryde 플릿에서 유니콘 탑승을 요청할 수 있도록 간단한 서버리스 웹 애플리케이션을 생성합니다. 
이 애플리케이션은 사용자가 픽업할 위치를 나타내기 위해 HTML 기반 사용자 인터페이스를 제공하고, 
백엔드에서 RESTful 웹 서비스와 연결하여 요청을 제출하고 근처의 unicorn을 디스패치합니다. 
또한 이 애플리케이션은 사용자가 서비스에 등록하고 탑승 요청 전에 로그인하기 위한 시설을 제공합니다.

애플리케이션 아키텍처는 AWS Lambda, Amazon API Gateway, Amazon S3, Amazon DynamoDB, Amazon Cognito를 사용합니다.

![아키텍처] (https://d1.awsstatic.com/Test%20Images/Kate%20Test%20Images/Serverless_Web_App_LP_assets-02.400d3f961e8e12b2640cc15cddf83510b6ecfc18.png)

진행 순서 
  1) 아키텍처에 사용되는 서비스 개념 정리 (~2/13)
  2) 정적 웹 사이트 호스팅 (~2/14)
  3) 사용자 관리 (~2/15)
  4) 서비리스 백엔드 구축 (~2/16)
  5) RESTful API 배포 (~2/17) 
  
[프로젝트 출처](https://aws.amazon.com/ko/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/?trk=gs_card)
