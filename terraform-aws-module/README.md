terraform-aws-modules

AWS 인프라를 Terraform을 통해 자동화하고 관리하는 데 필요한 모듈들을 모아 놓은 오픈소스 프로젝트

이 프로젝트는 다양한 AWS 리소스를 효율적으로 배포하고 관리할 수 있도록 돕는 모듈들을 제공

표준화된 베스트 프랙티스를 따름

이를 통해 개발자와 운영자는 복잡한 AWS 인프라를 더 쉽게 구성하고 관리 가능

https://registry.terraform.io/namespaces/terraform-aws-modules

재사용 가능한 모듈
복잡한 인프라 구성을 코드 몇줄만으로 배포 가능.

ex)- vpc,ec2,s3,rds,lamda,등 aws에서 자주 사용하는 서비스를 쉽게 배포

시간절약,유지관리 용이,커뮤니티 지원등 장점이 많다!



주요 모듈 목록

1. EC2 Instance Module
- GitHub: https://github.com/terraform-aws-modules/terraform-aws-ec2-instance

2. S3 Bucket Module
    - GitHub: https://github.com/terraform-aws-modules/terraform-aws-s3-bucket

3. RDS (Relational Database Service) Module
    - GitHub: https://github.com/terraform-aws-modules/terraform-aws-rds
  
  다적으면 너무 많아져서 조금만 적겠다. 이런식으로 다양하게 모듈이 존재한다.



https://github.com/terraform-aws-modules/terraform-aws-vpc/blob/v5.13.0/examples/complete/main.tf

이 샘플 코드는 Terraform을 사용해 AWS에 VPC, 서브넷, NAT/VPN 게이트웨이, 보안 그룹, VPC 엔드포인트(S3, RDS 등)등을
모듈 기반으로 완전하게 자동 구축하는 인프라 예제이며 이것을 통해 간단하게 공부해볼것임.


각기능에 대해서 간단하게 주석을 달아주었음.

![image](https://github.com/user-attachments/assets/24b7d14c-82d1-418e-a86c-d9061c0e3150)

전체는 올려놓은 파일로 확인가능




![image](https://github.com/user-attachments/assets/69fd6f20-b146-4f8d-bab8-1c6227c76021)

version같은경우에는 꿀팁으로 ""안을 다지우고 컨트롤+스페이스바를 누르면 위와같이 최신버전 확인이 가능함.

terraform in-place update 와 replace
1. terraform plan으로 미리 변경사항을 확인!!
항상 테라폼 어플라이전에 플랜을 실행하여 어떤 리소스가 업데이트되고 리소스가 교체되는지 미리 확인.

2. 서비스 중단 고려
리소스 교체가 필요한 경우 서비스 중단이 발생가능. 그러므로 서비스 가용상에 대한 대책 마련 중요.

등등 고려해야할것이 많음.

작성중--













  
