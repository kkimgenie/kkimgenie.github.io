---
layout: post
title: "4. 아키텍처 설계"
tags: [cloud, pca, architecture]
comments: true
# hidden: true
---

4.1 기반 인프라 구축 설계
-----

##### 4.1.1 AWS VPC 설계
* VPC 구성
보안 VPC : 인바운드, 아웃바운드 통신에 대한 보안 통제
서비스(PRD) VPC : 샘플 서비스 제공, 서비스를 위한 API Gateway, VPC Link 구성
DevOps VPC : CI/CD 관련 서비스를 제공

q/ 왜 화살표 방향이 운영->보안, DevOps ->보안 인지?
q/ VPC Link?

##### 4.1.2 VPC별 Subnet 설계
* VPC Subnet 구성
COMM : ALB나 Endpoint 등의 자원 할당 (10.10.128.0/24)
AP : 컨테이너나 Cache, Queue 등 자원할 당 (10.10.129.0/24)
DB : (10.10.143.24)

* Subnetting : 서브넷을 쪼개는 것
  10.0.0.0/26   - A Class
  10.10.0.0/25  - B Class
  10.10.10.0/24 - C Class
  
  기본적으로 8bits로 쪼개며, 6개는 3-tier 리소스에 쓰고 나머지는 여유분으로 가진다

| VPC | 용도 | Subnet | CIDR | AZ |
|:----:|:----|:----|:----:|:----:|
| SEC-VPC | Public COMM | SEC-COMM-PUB-A | 10.10.128.0/27 | ap-northeast-2a |
| | | SEC-COMM-PUB-C | 10.10.128.32/27 | ap-northeast-2c |
| | Private COMM | SEC-COMM-PRI-A | 10.10.128.64/27 | ap-northeast-2a |
| | | SEC-COMM-PRI-C | 10.10.128.96/27 | ap-northeast-2c |
| | Private AP | SEC-AP-PRI-A | 10.10.128.128/27 | ap-northeast-2a |
| | | SEC-AP-PRI-C | 10.10.128.160/27 | ap-northeast-2c |
| PRD-VPC | Private COMM | PRD-COMM-PRI-A | 10.10.129.0/27 | ap-northeast-2a |
| | | PRD-COMM-PRI-C | 10.10.129.32/27 | ap-northeast-2c |
| | Private AP | PRD-AP-PRI-A | 10.10.130.0/23 | ap-northeast-2a |
| | | PRD-AP-PRI-C | 10.10.132.0/23 | ap-northeast-2c |
| | Private DB | PRD-COMM-DB-A | 10.10.129.64/27 | ap-northeast-2a |
| | | PRD-DB-PRI-C | 10.10.129.96/27 | ap-northeast-2c |
| DevOps-VPC | Private COMM | DEVOPS-COMM-PRI-A | 10.10.143.192/27 | ap-northeast-2a |
| | | DEVOPS-COMM-PRI-C | 10.10.143.224/27 | ap-northeast-2c |
| | Private AP | DEVOPS-AP-PRI-A | 10.10.143.128/27 | ap-northeast-2a |
| | | DEVOPS-AP-PRI-C | 10.10.143.160/27 | ap-northeast-2c |

q/ PRD-VPC에서 Private AP 영역 CIDR만 왜?  
a/ 그냥 다양하게 구성한걸까

##### 4.1.3 VPC 네트워크 상세 설계
###### 4.1.3.1 VPC간 네트워크 통신 분리방안 설계
###### 4.1.3.2 인터넷 구간 인바운드 통신 상세 설계
###### 4.1.3.3 인터넷 구간 아웃바운드 통신 상세 설계

##### 4.1.4 DNS 구성

##### 4.1.5 Overall VPC 및 네트워크 설계