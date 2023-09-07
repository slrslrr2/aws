# 섹션2-3 Custom AMI를 통한 Public EC2 인스턴스 생성

<br>


현재 상황<br>
<img width="939" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/8678a02a-4fee-4bf1-8e7f-cbe3c9532f4f">

<br><br>

적용예정<br>

<img width="942" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/6ccfe96e-8fa9-4153-98ab-fa85778fb756">

<br><br>

### 1. EC2의 이미지 스냅샷을 생성

첫번째로, 이전에 만들었던 인스턴스를 스냅샷을 찍어놓는다.

<img width="626" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/2c039d62-ce6b-41a8-aa5f-ee35d35219aa">
<img width="1112" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/11fb020b-389b-4b0f-a135-e8e45f13312c">

이미지 생성을 아래와같이 확인할 수 있다.

<img width="1525" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/a4b1d0f1-9fc2-40a6-90ad-a4f8f67ad35b">

이를 통해 인스턴스를 생성할 수 있다.

<br>

----
<br>

## 2.  이를 활용하여 EC2생성하기

<img width="637" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/a7c88842-093e-41a9-8f60-fb11651e24ff">
<img width="630" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/5fb241d1-8ea3-429c-8e74-2fe1451d0f7c">
<img width="634" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/5eace1de-327f-4d0b-930b-d2cc276d4eb4">
<img width="630" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/98915b9b-7778-4a44-bd0b-7db62430c50d">
<img width="627" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/c4fa0ed7-4301-47ee-b15a-33a1a60ec467">
<img width="630" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/8018247f-1dca-48db-afdd-f31a025f5a16">
<img width="634" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/11d6071c-85d4-4417-a011-53951cac9edb">

사용자 데이터의 경우, 이전 만들었던 EC2를 스냅샷찍어 AMI를 선택하였기에 
사용자 데이터를 입력 안해도 LAMP가 추가된다.

그럼 아래와 같이 인스턴스가 추가됨을 확인할 수 있다.

<img width="1501" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/fdf82fa0-33b7-4b6a-8d36-38b8b182f537">

<br>

----
<br>

## 3. Elastic IP를 할당하여 위 만들어진 EC2의 고정IP를 만들어준다.
<img width="658" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/71a539b4-8749-4c48-82c5-ed8a3f01b9ee">
<img width="659" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/d215fab1-4464-428c-8d1a-9cc3da5fe68b">

해당 인스턴스의 Elastic IP할당을 확인한다.

<br>
<img width="1536" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/10cdf331-e77b-48d4-9842-47934aac5622">

<br>
ssh 접속해본다.

```
ssh -i ./ec2-public-seoul.pem ec2-user@13.124.9.38
```

또한, AMI가 어디 인스턴스에 접속이 되어있는지 확인가능하다.



<img width="1726" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/c0ac5126-acf2-43ae-904e-f77129587f89">

