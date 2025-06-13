
main.tf


![image](https://github.com/user-attachments/assets/e3dd7e77-359e-46ff-ac8d-587ef8e1b777)


파일에 AWS ec2인스턴스를 생성할 수 있는 Terraform 코드를 작성.

 us-east1-2 리전에 t2.micro 타입의 EC2 인스턴스를 생성하는 코드 작성.

 
![화면 캡처 2025-06-13 224156](https://github.com/user-attachments/assets/4d8ebaf4-4296-458c-8566-74c803089f9b)


![화면 캡처 2025-06-13 224303](https://github.com/user-attachments/assets/3fc5b8b6-4b43-4de4-a3a3-08b864e53290)


코드를 작성한 후 terraform plan 명령어를 통해 적용될 인프라 변경 사항을 미리 확인.

문제가 없다면 terraform apply 명령어를 실행하여 실제로 AWS에 인프라를 배포


![화면 캡처 2025-06-13 224535](https://github.com/user-attachments/assets/5de6ce30-4d92-4a97-93e7-e0b72419a104)

이렇게하면 ec2가 생성되었는데 직접 웹서비스에 들어가서 확인해보자.

![화면 캡처 2025-06-13 224734](https://github.com/user-attachments/assets/6b0f8566-3d21-4d9c-a73c-83034d089689)

잘 만들어진것을 확인.




애플리케이션 배포를 모두 확인헀다면 삭제한다.

terraform destroy를 사용.

![화면 캡처 2025-06-13 231721](https://github.com/user-attachments/assets/6e868606-e478-499e-9410-0c217be7c4b4)

![화면 캡처 2025-06-13 231821](https://github.com/user-attachments/assets/0844c5dd-2303-4d0d-99f2-dbce92de2861)





