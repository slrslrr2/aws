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

