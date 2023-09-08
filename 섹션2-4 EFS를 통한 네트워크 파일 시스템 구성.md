# 섹션2-4 EFS를 통한 네트워크 파일 시스템 구성

<br>

이전 상황
<br>

<img width="941" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/c4d646f2-240c-4caf-80bf-973a136574dc">
<br>

<br>
적용예정내용
<br>
<img width="943" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/0772ad06-d832-4957-b2e0-09b9a27d8659">

---

## 1. EFS에 필요한 Security Group생성

EC2와 EFS 사이의 트래픽의 Protocal, Port의 이동 허용에 대한 Security Group이 필요하다.

아래 보안그룹은 **EFS→Public EC2**로 인바운드 될 경우 사용된다.

<img width="1550" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/114ed2d4-a7ba-4a44-942e-7e4f20938c48">
<img width="1444" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/d4c71dff-180a-4be8-8703-14eaefbf7657">


<br>
-----
<br>

## 2. EFS를 생성
<img width="555" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/948fff45-74af-4a57-9f0e-d23b09688bbd">


스토리지 클래스 : 우리는 가용영역으로 EFS를 연결할것이므로 Standard 선택

<br>

<img width="559" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/1cd5b177-268c-402d-a037-7f9a8023fed4">
EFS에 생성된 파일들을 자동으로 Backup 여부

<br>
<img width="551" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/bb67c29f-280f-4059-b324-f2ab422f2667">

IA로 전환 : 일정 기간 접속하지 않은 파일의 경우 특정공간으로 이동하여 비용절감되도록 적용,
IA 외부로 전환 : 이후 이동된 파일을 다시 EFS경로로 원복하는데 사용

<br>

<img width="553" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/8c121d0d-dc47-42a4-9e52-51dc466f74e0">


<br>

<img width="550" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/e16b1c42-e7bf-4699-be37-b5f91ff8c961">
<img width="552" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/5c1606b6-e034-48dd-bc54-605e3d231e56">

<br>

<img width="1025" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/ea47c410-e83c-4531-be84-0e27aaefa019">
