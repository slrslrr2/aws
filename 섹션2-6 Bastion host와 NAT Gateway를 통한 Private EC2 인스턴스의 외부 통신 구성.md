# 섹션2-6 Bastion host와 NAT Gateway를 통한 Private EC2 인스턴스의 외부 통신 구성

<br>
## Bastion host와 NAT Gateway를 통한 Private EC2 인스턴스의 외부 통신 구성

1. Private subnet에 EC2 생성
2. Public subnet의 EC2를 통해 Private subnet EC2 접속
    - key pair 생성
3. NAT Gateway 생성
4. Route table 설정
5. Private subnet의 EC2의 외부 통신 테스트

<img width="1116" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/e0b1719f-83d7-4259-ac23-a06017563d9e">
<br>

---

**Bastion Host**는 내부 네트워크로의 접근을 관리하기 위한 중간 단계 서버이다.
**NAT Gateway**는 **사설 네트워크에서 공용 네트워크로 나가는 트래픽**을 관리하는 역할을 수행합니다. 
이러한 AWS 리소스들은 보안 및 네트워크 구성을 강화하고 내부 리소스를 안전하게 보호하는 데 사용됩니다.


```
1. Bastion Host:
Bastion Host는 외부 네트워크에서 내부 네트워크로 접근하기 위한 중간 단계의 서버입니다. 
주로 보안상의 이유로 내부 네트워크에 직접 접근하는 것을 방지하기 위해 사용됩니다. 
개발자나 관리자가 내부 리소스에 접근해야 할 때, 
먼저 Bastion Host에 접속한 후 이를 통해 내부 서버로 접근할 수 있습니다. 
이를 통해 내부 네트워크의 보안을 강화할 수 있습니다.

2. NAT Gateway (Network Address Translation Gateway):
NAT Gateway는 사설 네트워크에서 공용 네트워크로 나가는 트래픽을 관리하는 AWS 리소스입니다. 
주로 인스턴스가 인터넷으로 나가는 데 사용되며, 
사설 IP 주소를 공용 IP 주소로 변환하여 인터넷 리소스에 접근할 수 있게 해줍니다. 
NAT Gateway는 보안 그룹 및 네트워크 ACL을 통해 허용된 트래픽만 허용하도록 구성할 수 있어 보안을 강화할 수 있습니다. 
주로 내부 리소스가 외부 서비스에 접근해야 하는 경우에 사용됩니다.
```

<br>

---
<br>

## 1. Private subnet에 EC2 생성

<img width="634" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/193f5cba-55ba-4d0d-a3c8-ee77c3b9d109">

<img width="632" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/08045f11-4989-49df-b295-ef92ac83d90a">


private ec2를 위한 키페어를 생성하겠습니다.




<img width="631" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/917df419-1166-499a-a5b4-5b29b3b4a1bc">
<img width="491" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/95c361a7-091a-4565-b27f-b280ce7368dd">



<img width="599" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/1d7d2aa1-1516-4e67-bdc3-8d80e0deea24">
<img width="606" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/3aec696a-0b4d-4759-b63f-481c03e42676">

<img width="630" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/264e06a0-75cd-4fea-945b-b7a7b0e45adf">
<img width="631" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/997a4ae6-7cab-4586-8d90-c4c9831578ba">
<img width="629" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/a2a60317-da78-4aaf-bb19-c05b8328a036">
<img width="626" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/31e7d0e9-ef94-4480-8eb7-78ee5f40dcc4">

<br>
private EC2 생성을 확인한다.
<img width="1540" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/29b9618d-a947-46a5-a9e3-45d206e89b5b">


<br>

---
<br>

## 2. Public subnet의 EC2를 통해 Private subnet EC2 접속(key pair 생성)

Public EC2에 접근한다.

```
geumbit@gimgeumbich-ui-MacBookPro pem % ssh -i ./ec2-public-seoul.pem ec2-user@3.37.35.84
Last login: Tue Aug 15 01:46:35 2023 from 222.109.121.90

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
16 package(s) needed for security, out of 26 available
Run "sudo yum update" to apply all updates.
[ec2-user@ip-10-0-1-77 ~]$ pwd
/home/ec2-user
```

<br>
private keypair시 생성한 ec2-private-seoul.pem 를 생성한다.

```
[ec2-user@ip-10-0-1-77 ~]$ vi ec2-private-seoul.pem
```

만약 pem의 권한이 너무 많으면 아래와 같이 뜬다

```
Permissions 0664 for './ec2-private-seoul.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "./ec2-private-seoul.pem": bad permissions
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```
<br>
때문에, 아래 명령어로 모드를 변경 후, 접속한다.

```
[ec2-user@ip-10-0-1-77 ~]$ chmod 400 ec2-private-seoul.pem
```

<br>

```
[ec2-user@ip-10-0-1-77 ~]$ ssh -i ./ec2-private-seoul.pem ec2-user@10.0.3.165
Last login: Mon Jul 31 09:03:29 2023 from 121.140.89.153

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
```
이렇게하면 public EC2를 통해 Private로 접속하였다.
