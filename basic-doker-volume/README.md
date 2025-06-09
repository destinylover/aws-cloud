
컨테이너가 종료되더라도 데이터를 보존할 수 있는 방법인 Docker Volume의 동작 원리와 효과를 확인하기 위한 간단 실습.

Docker Volume이란.
Docker Volume은 컨테이너 외부에 데이터를 저장하기 위한 메커니즘으로, 컨테이너가 재시작되거나 삭제되더라도 데이터가 유지되도록 합니다.
이는 애플리케이션의 상태, 로그, 데이터베이스 등 영속적인 데이터를 다룰 때 필수적으로 사용됩니다.

주요특징

컨테이너 수명과 무관하게 데이터 유지

Docker가 직접 볼륨을 관리하며, 호스트 파일 시스템과 분리

여러 컨테이너 간 데이터 공유 가능


1. 데이터유지성


![도커볼륨](https://github.com/user-attachments/assets/dbd6de89-be9c-4f8d-ba16-e24f4dcc1a8d)

컨테이너 외부에 데이터를 저장하는 공간. 컨테이너가 삭제되어도 데이터 유지
hello.txt가 재접속 후에도 존재함을 확인 → Docker Volume은 컨테이너와 별개로 데이터 보존 가능


2.데이터 공유

![화면 캡처 2025-06-10 020853](https://github.com/user-attachments/assets/7adfc63d-f0c5-4460-9de2-95cd19c762f7)

shared_volume이라는 Docker 볼륨을 /shared 경로에 마운트
shared_file.txt에 "shared data" 문자열 작성
정상적으로 cat 명령으로 내용 확인

![화면 캡처 2025-06-10 020919](https://github.com/user-attachments/assets/888f5e74-c98d-4c03-ac52-90aaf7f6f276)

다른 터미널에서 같은 볼륨을 동일 경로에 마운트
shared_file.txt를 확인하니 앞에서 작성한 "shared data" 그대로 존재

![화면 캡처 2025-06-10 020933](https://github.com/user-attachments/assets/541afd74-c4a9-4bcb-b1a5-e3eb355f299e)

busybox 컨테이너 2개가 실행 중 (각각 공유 볼륨을 마운트)
컨테이너는 서로 다르지만 같은 볼륨을 공유하며 실행 중


