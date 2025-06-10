테라폼 환경설정

테라폼 exe을 다운받은후 원하는 폴더에 저장.

시스템환경변수 path 편집.


![1](https://github.com/user-attachments/assets/169acf44-d6cc-41e6-b4a2-2ed3e3923d5e)

Terraform.exe을 원하는 폴더에 구성했는데 이 경로를 가져옵니다. 

![2](https://github.com/user-attachments/assets/ee24295f-8e91-4b90-b654-4a6c18e3047b)

잘 적용되었나 확인. 

![3](https://github.com/user-attachments/assets/ff46f341-17fe-45a6-8c15-7bc023cfd412)

aws cli설치

![4](https://github.com/user-attachments/assets/9c810b96-1911-4f6f-bfc1-377188899f6d)

설치후 aws —version을 통해 확인



IAM IDENTITY CENTER
활성화후

![5](https://github.com/user-attachments/assets/f4fce594-bd18-482f-87cc-151f3920e2d1)

사용자 생성에 들어가서

![6](https://github.com/user-attachments/assets/c400581d-4f2a-40b2-8dca-9a5bf298a3c5)

사용자 설정후 생성.



![7](https://github.com/user-attachments/assets/e6c02683-bbe6-44a7-b9ea-ff2b54cc34f8)

user1에 대한 mfa등록후 로그인까지하면 이런창이 뜹니다.
이제 권한을 줘봅니다. 권한세트에 들어가서 권한을 만듭니다.


![8](https://github.com/user-attachments/assets/66a17da2-804f-436e-8093-5885e42d1192)

어드민권한세트를 주었고 세션기간은 12시간을 주었다.(이때 사용자 설정 시간을 부여해도 최대시간이 12시간이다.)


![9](https://github.com/user-attachments/assets/235562c4-e51c-4d7f-9eca-483dd5a46521)

그룹생성후 aws계정에서 조금전에 만든 사용자인 ggoggoya계정에 권한을 부여한다.

![10](https://github.com/user-attachments/assets/143d9e2e-c535-4b3a-84c8-d2571d1411ec)

부여가 끝난 모습.


이제 user1로 로그인을 해보면 아까와는 다르게 권한이 생긴 모습을 확인할수 있다.

![11](https://github.com/user-attachments/assets/798cea43-981a-499a-bd26-78012b84adbd)

이제 여기서 액세스키를 부여받고 콘솔홈으로 들어갈수있다.

![12](https://github.com/user-attachments/assets/fd28407d-cc8c-4b15-9e85-48058c152d48)

들어간모습.

이제  계정이 잘 만들어졌고 권한까지주어 로그인확인까지 끝냈으니 aws cli로 로그인을 해보자.


![13](https://github.com/user-attachments/assets/57fa7d7e-15cc-4cab-9a61-75cca10a912a)

- session name: 여러 SSO 세션을 구분하기 위한 이름이다. (~/.aws/config에서 사용됨)
- start URL:IAM Identity Center메인 페이지에 AWS 액세스 포털 URL이다.

세션이름은 편하게 my-sso라고 이름을 주었고

스타트 url 같은경우엔 아까 로그인할때 썼던 액세스 포탈 url을 사용하면된다.

지역은 서울이니  ap-northeast-2를 넣어주었다.

![14](https://github.com/user-attachments/assets/85ad74f8-f7c0-4072-9a92-8e0797b104cb)

그러면 보기와같이 액세스 허용창이 뜬다.

![15](https://github.com/user-attachments/assets/448d45e7-f3b4-467d-9998-b3fb402f8f5a)


액세스를 허용하고 다시한번 설정을 입력해준다.

나는 서울지역 그리고 json 프로필이름은 마이프로필으로 했다.

aws sts get-caller-identity --profile my-profile 그렇다면 이런 결과를 얻는데.

여러 프로필이 있고 매 번 프로필을 지정하려면 번거로우니 config 파일을 열어 프로파일 이름을 default로 변경하면 기본값이 된다.

![16](https://github.com/user-attachments/assets/5b9aa012-d2af-4d8c-b4d3-98665faf813d)

그러면 방금만든 마이프로필이 나온다,

다음처럼 default profile 설정이 가능하며, profile 이름도 식별이 편한 이름으로 고쳐두어도 된다.


![17](https://github.com/user-attachments/assets/29507a61-0369-4bc8-beb8-e6afb118d11c)


프로필 아래로 새로 디폴트칸을 만들어 프로필 정보를 정보를 입력해준다.

[default]
sso_session = sso
sso_account_id = 123154806408
sso_role_name = AdministratorAccess
region = ap-northeast-2
output = json

설정이 완료되면 AWS CLI를 통해 인증이 제대로 되었는지 확인하기 위해 **AWS 계정 정보**를 조회해봅니다. 계정 정보가 출력되면 설정이 올바르게 완료된 것입니다.

aws sts get-caller-identity
![18](https://github.com/user-attachments/assets/18676836-5f63-46e7-a191-0adfc5289d23)

이렇게 설정이 끝나면 따로 프로필이름을 넣지 않고도 aws sso login 만으로도 로그인이 가능하다.

이제 테라폼으로 다시 넘어가서 테라폼을 과제를 수행할 폴더를 만들어주자

![19](https://github.com/user-attachments/assets/a16e2c17-ac00-402e-9c7a-c08af2e340a2)

간단히 terraform-aws라는 폴더를 만들어주었다.









