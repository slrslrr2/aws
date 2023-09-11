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



