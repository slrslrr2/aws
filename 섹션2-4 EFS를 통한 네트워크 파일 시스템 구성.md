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







<br>
-----
<br>

## 3. public ec2에 EFS 관련 연결 Install

public ec2에 접속하여 df -h명령어를 통하여,

파일 시스템의 디스크 사용량을 표시해보자
   Mount on에서
   `"마운트(Mount)"란 컴퓨터에서 다른 디스크, 파티션 또는 네트워크 리소스를 특정 디렉토리에 연결`
<img width="813" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/73fd2378-a77d-40d0-86de-fcc1a339c469">

위 마운트 부분에서 efs가 아직 존재하지 않는다.

<br>

aws에서 제공하는 efs helper를 통해 ec2와 efs를 마운트해보자.

```
1. amazon-efs-utils 설치
[ec2-user@ip-10-0-1-77 ~]$ sudo -i
[root@ip-10-0-1-77 ~]# yum install amazon-efs-utils -y

2. efs를 마운트하기위한 마운트 포인트를 생성해보자
[root@ip-10-0-1-77 html]# pwd
/var/www/html
[root@ip-10-0-1-77 html]# mkdir efs #마운트 하기 위한 공간
[root@ip-10-0-1-77 html]# ls
efs  index.php

```

<br>
이제, efs를 attach(연결)해보자,
<img width="1247" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/97bafd6e-9373-41b1-9730-1c44081a5182">


```
sudo mount -t efs -o tls <EFS-DNS-or-IP>: <Mount-Point>
이 명령어는 sudo mount를 사용하여 마운트 작업을 수행하고, 
-t efs를 사용하여 파일 시스템 타입을 EFS로 지정하고, 
-o tls를 사용하여 전송 계층 보안(TLS)을 사용하여 암호화된 연결을 설정합니다. 

그리고 fs-059bb7082fd6dabb6:/를 마운트할 EFS 리소스의 DNS 이름 또는 IP 주소로 바꿔서 입력해야 합니다. 
efs 다음의 :는 마운트할 디렉토리를 지정하는 것으로, 해당 리소스를 루트로서 마운트할 것입니다.
```

```
sudo mount -t efs -o tls fs-059bb7082fd6dabb6:/ efs
```

<br>
<img width="540" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/03c47e5e-c5d2-4393-bc94-4ff92bc91eb4">


df -h를 통해 /var/www/html/efs 경로가 마운트됨을 확인할 수 있다

```
wget https://lab-s3-web-hosting-gbitkim.s3.amazonaws.com/car.jpg
wget https://lab-s3-web-hosting-gbitkim.s3.amazonaws.com/mycar.html
```

<img width="435" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/5ad4a635-3c8b-49e2-aa47-7342e35c7d0c">


그리고 Public EC2에 efs 파일이 붙었는지 확인한다.

<img width="662" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/5ad2d896-c7ec-4eef-b9fb-29cfb29a2419">


해당 efs의 경로에 생긴 파일은 해당 EFS와 연동된 EC2 폴더에 공유된다.


<br>
-----
<br>

## 4. Public EC2안에 EFS 마운드 작업한다.

```
1  cd /var/www/html/
2  mkdir efs
3  yum install amazon-efs-utils -y
4  sudo mount -t efs -o tls fs-059bb7082fd6dabb6:/ efs
```

가용영역 a에 있는 EC2에, 
공유된 efs파일들이 표시되어있는지 확인한다.

<img width="436" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/d9c05f76-b37b-4f5f-9ac0-a6fb4d3f8285">

가용영역 a에 있는 EC2에, 
공유된 efs파일들이 표시되어있는지 확인한다.

<img width="436" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/eeeaf59b-077f-4ec9-a92b-aac8e5b18fdc">

df -h 를 통해 efs가 마운팅됨을 확인한다
<img width="391" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/21d231ea-f4ff-4391-a326-703edbf5399f">


