
시작에 앞서 테라폼에서의 프로바이더(provider)란?

terraform이 어떤 클라우드 서비스와 통신할지 지정해 주는 플러그인 역할이다.

각 프로바이더는 특정한 클라우드 서비스(azure , aws 등) 과 같은 서비스와 통신하고 리소스를 관리하는 역할을 담당.

aws 프로바이더를 사용해 ec2,vpc,s3등 다양한 서비스를 terraform코드로 정의하고 제어한다.

provider 설정

이 설정을 통해서 terraform은 aws서비스에 접근할수 있는 자격 정보와 리전(region)을 설정 할 수 있다.

예시
![image](https://github.com/user-attachments/assets/e6942ecb-6efd-4fe2-99f6-c941e9ce8fa8)

aws프로바이더를 사용하며 us-east-1 리전을 지정 그리고 내 프로필은 my-profile을 사용.


aws인증정보 설정.



provider를 사용할때는 자격증명(credentials)이 필요

하지만 이때 프로바이더안에 직접 하드코딩을 해버리면 보안상 좋지 않기떄문에 시스템환경

로컬에 구성하는것이 일반적.


1. 환경변수 설정 aws cli설정에서 사용하는 환경변를 통해 terraform이 인증 정보를 가져옴

![image](https://github.com/user-attachments/assets/dcca8e0f-b78b-4b81-8715-76a10e374bfe)


2. ~/.aws/credentials 파일. aws cli에서 사용하는 자격증명 파일을 통해 인증 정보를 가져옴.

 
3. ~/.aws/config(profile) 사용. 여러 자격증 관리하는 경우 특정 프로파일을 지정가능. (aws계정 여러개를 가지고있다면 추천)

![image](https://github.com/user-attachments/assets/e49256d9-f33c-4547-ae78-b5cf42ef7f6c)



aws provider의 버전관리.



terraform provider는 지속적으로 업데이트되므로 특정 버전을 사용하도록 설정

버전설정.

기존코드 유지목적 필요에 따라 특정 버전이상부터 지원하는 파라미터를 사용하기 위해 등등.


source: 프로바이더의 소스 주소를 지정. 대부분 hashicorp/aws로 설정됨.

version: 사용할 프로바이더 버전을 지정.

이때 버전 "~> 3.0"은 3.x버전을 사용한다는 뜻.

밑에는 설정

![image](https://github.com/user-attachments/assets/b5c069be-8d9e-4916-b3ae-df36f5ba840a)


예시

![image](https://github.com/user-attachments/assets/fafa3869-80dc-49ad-befb-2623e3ca6b61)





프로바이더 플러그인 캐시 설정.

terraform init명령은 플로그인을 작업 디렉토리의 하위 디렉토리에 다운.

각 작업 디렉토리가 독립적으로 유지되며 동일한 프로바이더를 사용하는 구성파일이 있을경우 각 구성마다 플러그인 복사본이 별도로 다운로드됨.

중복이된다 = 용량 문제발생.

프로바이더 플러그인은 수백 메가 바이트에 달할 수 있어 인터넷 속도가 느리거나 데이터가 제한되는 환경에선 좋지 않을수있음.


이문제 해결을 위해 terraform은 로컬 디렉토리를 공유 플러그인캐시로 사용할수있도록 옵션제공.
각 플러그인 바이너리를 한번만 다운하도록 설정.

![image](https://github.com/user-attachments/assets/a81e5800-4ee3-48b4-9355-a8bfb299cf47)


A  /500MB

B  /500MB   --->(링크느낌으로)     공유디렉토리 /500MB

C  /500MB


장점: 데이터를 효율적으로 쓸수있음.
단점: 다수의 프로젝트가 동시에 공유 파일을 어플라이했을때 동시에 실행 보장이 없음.


플러그인 캐시를 활성화하는 두가지 방법

방법1

cli 설정파일(%appdata%/terraform.rc)에서 plugin_cache_dir설정을 구성 필요.

캐시 디렉토리는 자동 생성되지 않으므로 직접 생성.

plugin_cache_dir = "c:/terraform-plugin-cache"

방법2
TF_PLUGIN_CACHE_DIR 환경 변수를 사용하여 특정 세션에서 캐시 디렉토리 활성화 , 덮어쓰는 방법.


방법2를 진행해 보았다.

먼저 E드라이브를 경로로 사용할거라 E드라이브에 mkdir E:\terraform-plugin-cache로 폴더를 만들어줌.
 
![image](https://github.com/user-attachments/assets/50ad84f0-22b9-415d-9b11-0996c871353d)

플러그인 캐시 디렉토리가 활성화된 이후 과정

terraform init 명령을 실행. 기존설치 방식을 사용하여 사용 가능한 플러그인의 메타데이터를 가져옴.

적합한 버전이 선택되면 캐시 디렉토리에 해당 플러그인이 있는지 확인.

플러그인이 이미 캐시에 있으면 이전에 다운로드한 복사본을 사용.

선택된 플러그인이 캐시에 없을경우 terraform은 먼저 캐시에 단로드한후 현재 작업 디렉토리에 복사.

가능한 경우 심볼릭 링크를 사용하여 여러 디렉토리에 동일한 플러그인 복사본을 저장하는것을 피함.

주의사항

terraform은 한번 캐시에 추가된 플러그인을 스스로 삭제 x

-시간이 지나면서 플러그인이 업데이트됨에 따라 캐시 디렉토리는 여러 사용하지 않는 버전을 포함하게 될수 있는데 이걸 수동삭제 해야함.

플러그인 캐시 디렉토리는 동시성에 안전하지 않을 수 있음
위에서 아까 말했듯이 여러 terraform init 호출이 동시에 실행되는 환경에서는 프로바이더 설치자의 동작이 정의되지 않음.

















