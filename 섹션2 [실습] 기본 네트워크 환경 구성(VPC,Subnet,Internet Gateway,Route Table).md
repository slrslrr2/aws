# 섹션2 [실습] 기본 네트워크 환경 구성(VPC,Subnet,Internet Gateway,Route Table)

<br>

<img width="922" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/eebe0bfc-8f19-4eee-bbde-4ebe45d5dc39">


### 1. VPC 생성하고, DNS hostname 활성화

<html>
<body>
<!--StartFragment-->


<!-- notionvc: 18340e09-21a9-407c-b52d-0ca0421046f9 --><!--EndFragment-->
</body>
</html>

<img width="570" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/7a21ac66-fec6-43ec-9c4d-9465a84e487e">


DNS HostName을 활성화 한다.

- DNS 호스트 이름을 사용하면 인스턴스의 퍼블릭 IP 주소를 기억하지 않고도 쉽게 액세스할 수 있습니다.
- 인스턴스의 퍼블릭 IP 주소가 변경되더라도, 퍼블릭 DNS 호스트 이름은 일반적으로 변경되지 않습니다.


# 섹션2 [실습] 기본 네트워크 환경 구성(VPC,Subnet,Internet Gateway,Route Table)

<br>

<img width="922" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/eebe0bfc-8f19-4eee-bbde-4ebe45d5dc39">


### 1. VPC 생성하고, DNS hostname 활성화


<img width="570" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/7a21ac66-fec6-43ec-9c4d-9465a84e487e">


DNS HostName을 활성화 한다.

- DNS 호스트 이름을 사용하면 인스턴스의 퍼블릭 IP 주소를 기억하지 않고도 쉽게 액세스할 수 있습니다.
- 인스턴스의 퍼블릭 IP 주소가 변경되더라도, 퍼블릭 DNS 호스트 이름은 일반적으로 변경되지 않습니다.

<br>

### 2. 서브넷 생성


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

<img width="754" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/e863fadd-88b0-4f44-96e2-35bc43107249">
<br><br>
<img width="762" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/973bb9ef-22e5-431f-87b9-dc782abe9fb6">
<br><br>
<img width="745" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/5f1e80e4-7221-482c-a22c-74f8822fbfd1">
<br><br>
<img width="748" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/12ac870d-4361-42f6-b007-2d7ea3437b44">
<br><br>
<img width="735" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/3811ea0d-28ce-46b1-961a-e1d974c3ecb6">
<br><br>
<img width="733" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/5392f220-2d91-486d-ba77-6c453bf5d85c">
<br><br>
<img width="730" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/5dec34bb-0580-46fe-8f10-d2c424c273c2">


<br>

-----

<br>

### 3. Internet Gateway

<img width="826" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/6697dc19-6742-4783-9df6-8efbb2c99cd7">

인터넷게이트웨이가 어떤 VPC의 Gateway로 할 것인지 Attach(연결) 한다.

<img width="782" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/0095da7b-b0bb-40e5-8398-394f06070b08">

