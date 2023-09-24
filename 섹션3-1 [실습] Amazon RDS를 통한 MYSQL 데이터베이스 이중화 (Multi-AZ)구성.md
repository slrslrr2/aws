# 섹션3-1 [실습] Amazon RDS를 통한 MYSQL 데이터베이스 이중화 (Multi-AZ)구성

<br>

```
1. RDS용 Security group 생성
2. Subnet group 생성( RDS 위치 )
3. 복수의 가용영역에 MySQL DB생성
    1. Multi-AZ Deployment
    2. DB Engine, DB Instance
    3. Storage
    4. Availability Durability
    5. Connectivity
    6. Authentication
    7. Backup 등
4. DB 정보 확인
```
<img width="630" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/b3e904e0-a6a8-4652-bec4-4243fc8a4e43">

<br>

----
<br>

## 1. Security Group을 생성한다.

인바운드의 경우 MYSQL/Autora 를 선택한다.

<img width="1055" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/36051cb9-5863-461d-a23f-a581c2eb6b24">

인바운드 규칙의 경우, Source는 **10.1.0.0/16 으로 설정하여, 해당 VPC에 모두 허용**한다.


<img width="1043" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/fb1de782-60d2-41e6-88d5-ff61061f6f99">

<br>
<br>

## 2. 서브넷 그룹을 생성한다.

<img width="632" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/6283fee3-8b5b-4969-b1cd-f363385e6c8a">

서브넷 그룹의 경우 private-a2, c2를 선택하여 RDS만들것을 염두한다.
<img width="672" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/0edf7670-b393-490d-a50c-4190dcaa8d50">

<br>

---
<br>

## 3. RDS 생성
<img width="620" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/7d057ac0-9894-4647-bce6-548aaca070a0">

<br>
[다중 AZ DB인스턴스] 선택 시, 
해당 가용영역중 하나에는 Master, 다른 하나에는 Standby가 생성됩니다.

<img width="611" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/2baecab3-7849-47dc-89ef-aedad528a2c0">
<br>

db.t2.micro는 subnet영역 2곳 이상인경우 요금이 부과됩니다.

<img width="612" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/f59d238d-e48b-4dbd-bb68-6f9930c32510">
<br>
[Storage autoscaling]은 RDS 저장공간이 부족할 경우 자동으로 저장공간을 확장하는 기능입니다.
<img width="611" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/e26073ae-2ac5-4345-80ad-9600ff19d787">
<br><img width="610" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/04add12d-2a21-4f75-8b41-a3ee216797b7">
<br><img width="615" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/52d5eaf2-f451-4a32-bec3-b99527fa7535">
<br><img width="612" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/10b721ad-0e34-481a-91dd-c83d270d58f2">
<br><img width="614" alt="9" src="https://github.com/slrslrr2/aws/assets/58017318/4b714224-5fc0-4ddb-acd1-474b7f4cc2e5">
<br><img width="614" alt="10" src="https://github.com/slrslrr2/aws/assets/58017318/20b612f7-0b42-40df-8c6a-eabd6bb1f9a0">
<br><img width="612" alt="11" src="https://github.com/slrslrr2/aws/assets/58017318/38574d19-a4a9-4377-a775-0bad11276507">


DB정보를 세부적으로 확인하면 아래와 같다.
Connectivity & security에서 Endpoind를 통해 DB를 Access할 수 있다.
또한, Networking에 Availavility Zone에하단에는 Master DB가 설정됨을 확인할 수 있다.
<img width="1035" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/15addab0-d346-4e90-bead-ecbf6561d616">

또한 네트워크 인터페이스를 확인해보면 2가지 생성을 확인할 수 있다.
<img width="1542" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/905729f1-0083-404a-a14f-7509ada5bb6f">
