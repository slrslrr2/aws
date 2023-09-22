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

