# 섹션2-5 Application Load Balancer를 통한 이중화 네트워크 구성(1)

<br>

<img width="944" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/48f812eb-4235-46f0-9607-c7351bf7607c">

1. Target Group 생성

<br>

**ApplcationLoadBalancer**는 **트래픽을 받으면** **Target Group으로 전달**을 하게된다.
<img width="880" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/2aba2730-19da-4b9e-906b-c515a057e070">


```
TargetGroup을 통하여 밸런싱할 Instance를 지정합니다.
후에 로드 벨런서에서 '리스너'지정 후 '대상 그룹'을 등록하게됩니다.

'리스너' : Client와 ALB 사이 Port를 지정해줍니다.
     Protocol: Port: 
     이는 TargetGroup 소속된 EC2들이 설정된 'Protocol: Port'만 받는다는 것을 의미합니다. 
     즉, HTTP: 80으로 설정한다면 TargetGroup에 소속된 EC2 Instance들은 
     80 Port로 설정된 요청만을 받아들인다는 것 입니다.

'TargetGroup' : ALB에서 TargetGroup으로 요청이 들어올 때, 
     Protocol과 Port는 TargetGroup에서 지정한다.
     이는 TargetGroup 소속된 EC2들이 설정된 'Protocol: Port'만 받는다는 것을 의미합니다. 
     즉, HTTP: 80으로 설정한다면 TargetGroup에 소속된 EC2 Instance들은 
     80 Port로 설정된 요청만을 받아들인다는 것 입니다.
```

<br>


<img width="647" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/9b7ba109-3c87-4a7e-9508-9b7bb89f00c6">
<br>

ALB는 Health Check를 통해 EC2의 정상상태를 체크한다. HTTP프로토콜로 아래 경로로 체크한다.




<img width="646" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/21aadc38-78d8-4346-909d-1f376badb58f">
<img width="646" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/a6b14427-945c-4a5e-a001-79cd3ae012f2">


<img width="650" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/67fc8de2-7492-401d-bfb8-8bfde4405a1e">

Register targets는 트래픽을 받을 대상을 의미합니다.



<img width="989" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/96ed2c00-b676-47ff-8e78-0f95222a61c1">

<br><br>
이후 생성하게되면 아래와 같은 TargetGroup이 생성된다.

- HTTP, 80포트로 통신
- public EC2 2개를 연결해놓는다. => 이후 강좌에서 보안을 위해 private로 변경할것이다.
- healthCheck 설정 등 적용

<img width="1067" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/911295a0-739a-46f5-a8b7-52d40b46445b">


<br>

-----
<br>

## 2. ALB 생성한다.
<img width="816" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/9447e355-1acf-4bb7-bddf-cab031b5d5c2">
[Application Load Balancer] 선택

<br>

**Internet-facing** ALB는 인터넷에서 직접 접근할 수 있고, 외부 클라이언트들과 통신하는 데 사용된다.
**Internal** ALB는 VPC 내에서만 접근 가능하고, VPC 내의 내부 서비스들과 통신하는 데 사용됩니다.

<img width="880" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/7035f65d-bea5-4cec-9cbb-ecf24910c41b">

<br>
<img width="874" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/d68d8748-34e7-4bb5-84be-0b9f6eab4b32">

**Internet-facing** ALB는 인터넷에서 직접 접근할 수 있도록 설정해놓았기때문에,
외부 Internet통신이 가능한, Internet Gateway를 설정한 public 영역으로 지정해야한다.

<br>
Security Group

ALB는 Target이 되는 EC2를 위해 사용되므로 새로 생성한다.



<img width="1226" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/7a110b18-a97b-48f9-830c-5086cffc3050">
<img width="872" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/86a8555a-4be1-4ee3-8e6d-2dae3198cc24">

```
TargetGroup의 Protocol과 Port:
Protocol: TargetGroup에서 사용할 프로토콜을 지정합니다. 
일반적으로 HTTP, HTTPS, TCP 등의 프로토콜을 선택할 수 있습니다. 
이는 TargetGroup과 연결된 EC2 인스턴스 또는 다른 리소스와 통신할 때 사용되는 프로토콜입니다.
Port: TargetGroup과 연결된 리소스(예: EC2 인스턴스)가 사용하는 포트를 지정합니다. 
TargetGroup은 이 포트를 통해 연결된 리소스와 통신합니다. 

ALB의 Listeners and routing에서 Listener의 Protocol과 Port:
Protocol: Load Balancer의 프로토콜을 지정합니다. 
즉, 클라이언트(사용자)와 Load Balancer 간의 통신에 사용됩니다. 
주로 HTTP와 HTTPS를 선택할 수 있습니다. 
예를 들어, 웹 애플리케이션을 위한 ALB의 경우, HTTP 또는 HTTPS를 선택할 수 있습니다.
Port: Load Balancer에서 들어오는 연결을 수신하는 포트를 지정합니다. 
이 포트는 애플리케이션의 리스닝 포트와 일치해야 합니다. 
즉, 클라이언트가 Load Balancer에 접속할 때 사용하는 포트입니다.
이러한 설정은 Load Balancer가 들어오는 트래픽을 어떻게 처리할지 결정하는데 중요한 역할을 합니다. 예를 들어, HTTP로 설정된 TargetGroup과 Listener는 HTTP 요청을 처리할 수 있으며, 해당 요청을 HTTP 프로토콜을 사용하는 EC2 인스턴스의 80번 포트와 같은 타겟 포트로 전달합니다. 
이런 방식으로 Load Balancer는 클라이언트와 애플리케이션 사이의 트래픽 분산과 로드 밸런싱을 수행합니다.
```
<br>

외부요청(Client Request) → ALB

<img width="871" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/6f6bb004-ac34-4d3e-a3c0-18f4f96b73d6">
<img width="590" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/c7e0e636-6b4f-4cc3-ace1-dab4a796a991">


<br><br>

결과적으로 아래와 같은 ALB가 생성되었습니다.
- Basic configuration (Internet-facing)
- Security Groups => public EC2 2개 연결
- 리스너 : HTTP:80
- TargetGroup : HTTP:80
<img width="849" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/0736e222-1c4d-4c17-8b13-2ceccb00a146">

