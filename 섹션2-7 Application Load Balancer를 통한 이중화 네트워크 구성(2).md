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

<br>

-----

<br>

## 2. Application Load Balancer 구성

<img width="756" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/dbeb208c-eb6e-47c4-9f8b-c4eaf666d916">
<img width="743" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/24e0f2c1-b386-4616-a563-eb8c32e7f424">
ALB의 네트워크매핑의 경우, **public**을 선택해야한다

네트워크 인터페이스가 인터넷 게이트웨이를 통해 통신을 하게해야하기에 public을 선택해야한다.

<br>

<img width="745" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/9b828fc6-7476-4f9d-a66a-7e8613bfff67">
ALB의 Security Group을 생성한다.

<br><br>

<img width="1548" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/6828bd23-2d9f-43ce-a50c-f58c2134ffbf">
<img width="1546" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/1ce9ed31-19f1-4aec-904d-39fb6e506656">
<img width="879" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/c3656a51-fe80-4866-94aa-4c585414f863">
<img width="877" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/838d3a2e-a8b5-401a-8d3d-a30cb7e16915">
<img width="1512" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/7f7720e4-932d-4f01-93a3-2eb01a2c1c4c">
<img width="732" alt="9" src="https://github.com/slrslrr2/aws/assets/58017318/eef93b42-3941-4e10-b67d-c547d83dcd00">
<img width="755" alt="10" src="https://github.com/slrslrr2/aws/assets/58017318/10b8b66c-ae0c-4bc4-8f2e-08c1d4616aa7">

