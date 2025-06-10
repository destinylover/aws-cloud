간단한 도커이용.

![docker](https://github.com/user-attachments/assets/6583c78c-2159-436a-a013-ea3bd1d152c6)

Dockerfile을 기반으로 Flask 애플리케이션 이미지를 생성

![화면 캡처 2025-06-10 005924](https://github.com/user-attachments/assets/99004f92-3718-44f0-95e6-0fe80d431ada)

생성된 이미지를 컨테이너로 실행하고, 외부 포트 매핑 설정

![화면 캡처 2025-06-10 010343](https://github.com/user-attachments/assets/b1a11b3f-fd7b-4d1d-9813-96c1fb0f6887)

Flask 코드

![화면 캡처 2025-06-10 010404](https://github.com/user-attachments/assets/7e42843a-5377-4fb7-af49-29ad87ba8688)

웹 브라우저를 통해 Flask 앱 접속 및 정상 동작 확인













간단한 DOCKER COMPOSE 사용

![화면 캡처 2025-06-10 233712](https://github.com/user-attachments/assets/e656642f-3c59-4716-8178-a2e5a67a2b93)

docker 컴포즈 yml파일이다.


실행해보자.

![화면 캡처 2025-06-10 233641](https://github.com/user-attachments/assets/242d4031-0814-466e-91fe-15022ab9a069)


![화면 캡처 2025-06-10 233625](https://github.com/user-attachments/assets/5475a1d9-2b1a-4318-9146-c4bb32e6f98a)

![화면 캡처 2025-06-10 233652](https://github.com/user-attachments/assets/76892127-3340-4e98-a2b4-0611f3835948)

사진과같이 잘접속까지 되는 모습.




Docker Compose를 사용해 Flask 앱과 MySQL을 연동하는 전형적인 2-tier 아키텍처 구현해보기.


![image](https://github.com/user-attachments/assets/b1b27ea0-07eb-4dc1-b1e5-211157d4eb09)

copose.yml파일

![image](https://github.com/user-attachments/assets/9c1439df-ab93-4ba9-a9f0-62dcb5505051)

빌드해보고 접속해보자.

![image](https://github.com/user-attachments/assets/cf3d8904-a2a8-4e87-afc1-cbd70a3c80df)

실행된것을 확인.

실습으로서 공부하게된것.
docker-compose.yml로 두 컨테이너(Flask+MySQL) 한 번에 띄우기
컨테이너 간 네트워크 연결 (app에서 db 호스트명으로 접근)
환경 변수로 설정 분리 (MYSQL_HOST=db)
볼륨으로 DB 데이터 유지 (db_data)






