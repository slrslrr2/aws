# 섹션2 [실습] 기본 네트워크 환경 구성(VPC,Subnet,Internet Gateway,Route Table)

<br>

<img width="922" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/eebe0bfc-8f19-4eee-bbde-4ebe45d5dc39">


### 1. VPC 생성하고, DNS hostname 활성화

<html>
<body>
<!--StartFragment-->

Name | IPv4 CIDR
-- | --
public-subnet-a1 | 10.0.1.0/24
public-subnet-c1 | 10.0.2.0/24
private-subnet-a1 | 10.0.3.0/24
private-subnet-c1 | 10.0.4.0/24
private-subnet-a2 | 10.0.5.0/24
private-subnet-c2 | 10.0.6.0/24


<!-- notionvc: 18340e09-21a9-407c-b52d-0ca0421046f9 --><!--EndFragment-->
</body>
</html>

<img width="570" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/7a21ac66-fec6-43ec-9c4d-9465a84e487e">


DNS HostName을 활성화 한다.

- DNS 호스트 이름을 사용하면 인스턴스의 퍼블릭 IP 주소를 기억하지 않고도 쉽게 액세스할 수 있습니다.
- 인스턴스의 퍼블릭 IP 주소가 변경되더라도, 퍼블릭 DNS 호스트 이름은 일반적으로 변경되지 않습니다.


