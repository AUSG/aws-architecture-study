# 1주차 AWS architecture 스터디

## S3에 업로드 된 이미지를 리사이징 하는 Lambda 함수 만들기

### 참고자료 : [AWS 자습서](https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/with-s3-example.html)

### 주의사항

~~~
    1. 버킷 이름을 '원본 이름'과 '원본 이름-reisized'로 만들 것
    2. 핸들러 정보를 [파일 이름].handler 로 수정
    3. 람다 함수 구성에서 S3 트리거 추가(이벤트 유형: ObjectCreated)
    4. 제한 시간 기본 3초로 되어있음 늘릴 것
    5. 배포 패키지 설정해주기(안해주면 no module error) - [AWS Lambda 배포 패키지](https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/lambda-python-how-to-create-deployment-package.html)
~~~