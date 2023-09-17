# 섹션2-7 Application Load Balancer를 통한 이중화 네트워크 구성(2)

<br>

WebServer를 public 영역에 두는것은 보안적인 측면에 위험할 수 있으니, Private EC2를 두고 이를 ALB를 통해  트래픽을 분산하고 제공하는 서비스를 만들겠습니다.

```
1. Target Group 생성
2. Application Load Balancer 구성
3. 웹 브라우저를 통한 Application Load Balancer 작동 테스트
```
<img width="1111" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/a233b58b-0146-4fdd-86b2-4607773e66a1">


<br>

---

<br>

## 1. Target Group 생성

<img width="652" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/4c9498a3-5910-4d66-ad10-4890dd7d68c7">

<img width="553" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/85bd9136-3b12-4549-841b-f5675d6be8fc">


<img width="550" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/ca2fa2db-3e86-497a-92f0-778b125af625">
<img width="552" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/7768f5bb-788b-43ca-9786-cbc4f82d299b">



<img width="1418" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/4510daa4-4db7-4572-bb6b-21b57556bb6b">

