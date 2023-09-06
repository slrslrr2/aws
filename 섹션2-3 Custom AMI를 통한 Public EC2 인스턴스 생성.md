# 섹션2-3 Custom AMI를 통한 Public EC2 인스턴스 생성

<br>


현재 상황
<img width="939" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/8678a02a-4fee-4bf1-8e7f-cbe3c9532f4f">

<br><br>

적용예정

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
