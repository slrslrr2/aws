# 섹션2-2 [실습] Public EC2 인스턴스 생성 및 LAMP 웹서버 구성

<br>



<html>
<body>
<!--StartFragment--><p>현재상황)</p>
<p>VPC생성 및 SubNet, InternetGateway, RouteTable 생성</p>

Name | IPv4 CIDR | Route Table
-- | -- | --
public-subnet-a1 | 10.0.1.0/24 | public-subnet-rt
public-subnet-c1 | 10.0.2.0/24 | 위와 동일
private-subnet-a1 | 10.0.3.0/24 | private-subnet-a1-rt
private-subnet-c1 | 10.0.4.0/24 | private-subnet-c1-rt
private-subnet-a2 | 10.0.5.0/24 | private-subnet-a2-rt
private-subnet-c2 | 10.0.6.0/24 | private-subnet-c2-rt


<p>진행예정)</p>
<!-- notionvc: 243663b9-bf3b-4e76-af43-1195c8bf2a8d --><!--EndFragment-->
</body>
</html>










<img width="921" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/2f74bd10-a051-49b8-9e88-2d50d571b043">


### 1. 인스턴스를 생성해보자


<img width="801" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/2e270efa-4da2-4538-8523-605789d6cd3c">

AMI(Amazon Machine Image)는 
가상 머신(인스턴스)을 생성하는 데 사용되는 
       사전 구성된 운영 체제(예: Linux, Windows 등)와 해당 소프트웨어 구성을 포함하는 템플릿입니다.
        - 최근사용, 내가만든것(스냅샷), 외부공유, 외부 써드파티에서 만든 AMI등 선택 가능


<img width="789" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/0d4a0f94-8d45-4958-ac85-8dd45a2d1d4a">

인스턴스 유형의 경우, 인스턴스의 소프트웨어를 의미(CPU, Memory)


<img width="791" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/095e378c-1af5-4437-b21a-e1abdadf71ce">

t(유형)2(세대).micro(크기)

AWS에서 키페어(key pair)는 인스턴스에 안전하게 접속할 수 있도록 공개 키와 개인 키를 쌍으로 제공하는 보안 인증 방법이다.
     **- pem파일 :** 
        Linux 및 macOS와 같은 유닉스 기반 시스템에서 SSH(Secure Shell) 클라이언트를 통해 
        이 키페어를 사용하여 EC2 인스턴스에 접속할 수 있습니다.
     **- ppk파일 :** 
        Windows 사용자가 EC2 인스턴스에 접속할 때는 **`.ppk`** 확장자를 가진 개인 키를 사용하여 
        PuTTY 클라이언트를 통해 접속합니다.


<img width="608" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/11e7e0e3-469d-49b5-839d-712f8f0b9110">

네트워크설정 (VPC, 서브넷, 방화벽(인바운드 설정))

퍼블릭 IP 자동할당은 비활성화하고, 후에 Elastic IP를 통해 고정 IP할당한다.
⇒ 이렇게하면 Public IP가 고정된다.
보안그룹을 통해 인스턴스 레벨에서 통신타입과 포트, 프로토콜로 트래픽을 제어할 수 있다.

<br>



<img width="809" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/61e0cbbd-d8bb-4bd9-b501-0d6240224855">



<img width="788" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/274ddd9a-2187-444d-b472-7714c3d2bf06">

<br>

스토리지는 하드웨어(EBS)를 의미하며,
인스턴스와 Network로 연결되어있어 인스턴스 재시작이 가능하다.


<img width="813" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/92a6aafc-f5cb-41ef-a42e-cb08eeb3061a">


### 고급 세부 정보

<img width="150" alt="9" src="https://github.com/slrslrr2/aws/assets/58017318/23435155-35cc-4a6a-a7a4-0604bed5b36b">

위 선택을 해제하면 인스턴스는 온디맨드 방식으로 비용이 청구됩니다.
    스팟 인스턴스의 경우, 경매형식으로 용량을 제공해줍니다.


<img width="736" alt="10" src="https://github.com/slrslrr2/aws/assets/58017318/a4c830a0-e708-47b7-92a2-1506c6e1b12f">

<img width="742" alt="11" src="https://github.com/slrslrr2/aws/assets/58017318/7d38948e-7eae-40c3-8a7b-f4ec1f8e2212">

도메인 조인 디렉터리는 
    AWS Directory Service를 사용하여 인스턴스를 디렉터리에 연결하는 것으로, 
    사용자 관리 및 인증을 간편하게 하기 위한 기능입니다. 

반면에 IAM 인스턴스 프로파일은 
     IAM을 사용하여 인스턴스에 대한 권한을 관리하는 것으로, 
     안전하고 효율적인 인스턴스 권한 관리를 위한 메커니즘입니다.

<img width="425" alt="12" src="https://github.com/slrslrr2/aws/assets/58017318/4deae353-66bb-49c7-95b1-042ee53c0ddf">

인스턴스의 호스트 이름을 어떻게 설정할지 결정하는 것으로, 
   IP이름과 리소스이름 2가지로 식별 가능하다.

<img width="427" alt="13" src="https://github.com/slrslrr2/aws/assets/58017318/38afe349-e464-4b16-86cc-06341be578d9">

리소스 기반 IPv4(A 레코드) DNS 요청 활성화
   DNS는 인터넷에서 도메인 이름(예: [example.com](http://example.com/))을 
   IP 주소(예: 203.0.113.1)로 매핑하는 역할을 합니다. 
   A 레코드는 도메인 이름을 IPv4 주소로 매핑하는 레코드입니다. 
   예를 들어, [example.com](http://example.com/) 도메인의 A 레코드가 203.0.113.1로 설정되어 있다면, 
    이 도메인을 사용하는 모든 장치 및 서비스는 203.0.113.1 IP 주소로 연결됩니다.


<img width="424" alt="14" src="https://github.com/slrslrr2/aws/assets/58017318/54e79196-07b5-404d-ac88-0004bd4ed460">

메모리 오버플로우, 디스크 문제, 운영 체제 충돌 등으로 인해 
인스턴스가 정상적으로 작동하지 않는 경우 
"시스템 상태 확인에 실패"라고 판단하여 인스턴스 자동 복구 기능이 작동하도록 설정할 수 있습니다.


<img width="420" alt="15" src="https://github.com/slrslrr2/aws/assets/58017318/5a75d3c3-ac24-4aa5-8000-6fc891d1f569">


OS 수준에서 종료할 때의 인스턴스 동작입니다.
**중지**는 EC2 인스턴스를 일시적으로 중지하는 동작입니다.
    중지된 인스턴스는 그 상태를 유지하며, 사용 중인 Amazon EBS(Elastic Block Store) 볼륨의 데이터는 보존됩니다.
**종료**는 EC2 인스턴스를 영구적으로 중지하고 삭제하는 동작입니다.
인스턴스가 종료되면 해당 인스턴스와 연결된 Amazon EBS 볼륨의 데이터도 함께 삭제됩니다. 따라서 종료된 인스턴스의 데이터는 복구할 수 없습니다.



<img width="423" alt="16" src="https://github.com/slrslrr2/aws/assets/58017318/10412181-592e-411d-bf16-a9292db8a57d">

최대 절전 모드는 인스턴스를 중지하고 인스턴스의 RAM에 있는 내용을 루트 볼륨에 저장합니다. 시작 후에는 최대 절전 기능을 활성화할 수 없습니다.


<img width="420" alt="17" src="https://github.com/slrslrr2/aws/assets/58017318/d0e40cfa-28fb-4c46-92b9-075ef45c7106">

활성화된 경우, 종료 방지 기능을 사용하면 다음과 같은 상황에서 인스턴스를 종료할 수 없습니다:

- 콘솔을 통한 종료 시도
- AWS CLI(Command Line Interface)를 사용한 종료 시도
- AWS SDK 또는 API를 사용한 종료 시도

따라서 종료 방지 기능이 활성화되어 있으면 실수로 인스턴스를 종료하지 않도록 보호할 수 있습니다.

<img width="420" alt="18" src="https://github.com/slrslrr2/aws/assets/58017318/9fc92d83-c5ae-4668-a2f9-e7622fe20ced">

<img width="421" alt="19" src="https://github.com/slrslrr2/aws/assets/58017318/d85fa1b6-df52-41ce-b420-df4c2b5de099">

Amazon CloudWatch를 통해 인스턴스에 대한 측정치를 모니터링, 수집 및 분석할 수 있습니다. 활성화된 경우, 추가 요금이 적용됩니다. 값을 지정하지 않으면 원본 템플릿의 값이 계속 사용됩니다.


<img width="424" alt="20" src="https://github.com/slrslrr2/aws/assets/58017318/457a4ebd-adac-461d-863b-18b8c9ca1a75">

서버를 사용시 기존에는 기본만 사용하다가, 
트래픽이 높아지면 순간적으로 상위 인스턴스로 변경되며 요금부가되는데,
 현재는 개인프로젝트이므로 표준을 선택한다.



<img width="656" alt="21" src="https://github.com/slrslrr2/aws/assets/58017318/8dfcfb8f-f67b-4fac-8851-e2ab6ed65b24">

배치 그룹(Batch Group)은 EC2(Amazon Elastic Compute Cloud)에서 사용되는 용어로,
 특정 인스턴스 유형에 대한 클러스터 그룹을 의미합니다. 
배치 그룹을 사용하면 여러 EC2 인스턴스를 논리적으로 묶어서 
동일한 유형의 인스턴스를 함께 실행하거나 관리할 수 있습니다.

<img width="666" alt="22" src="https://github.com/slrslrr2/aws/assets/58017318/a98f5327-8120-487f-8145-f37c7610af7b">

용량 예약을 사용하여 인스턴스 용량을 미리 예약함으로써 가용성과 가격 절감을 동시에 이끌어낼 수 있습니다. 이를 통해 EC2 인스턴스를 효율적으로 운영하고 비용을 절감할 수 있습니다.


<img width="420" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/17da5aab-27a4-4753-b37f-438f4df67fb1">

전용 테넌시 인스턴스는 단일 테넌트의 전용 하드웨어에서 실행됩니다. 
호스트 테넌시 인스턴스는 전용 호스트에서 실행되며 추가요금이 발생합니다.





<img width="673" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/dc25f59a-553e-41c6-9cf1-32128d5dc068">
<img width="682" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/30f05025-de21-4b65-8d8a-e26341082c47">


인스턴스 생성 후, 해당 스크립트를 자동으로 실행해준다.




<img width="680" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/8c9d6591-da3e-4e4a-833c-091371456938">

```
■ LAMP 웹 서버 및 Application Load Balancer 구성 - EC2 Userdata 스크립트

#!/bin/bash
yum update -y
amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2 
yum install -y httpd mariadb-server
systemctl start httpd
systemctl enable httpd
usermod -a -G apache ec2-user
chown -R ec2-user:apache /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} \;
find /var/www -type f -exec chmod 0664 {} \;
```

```
#!/bin/bash
# 이 줄은 스크립트가 bash 쉘에서 실행됨을 나타냅니다.

yum update -y
# yum 명령어를 사용하여 시스템의 패키지들을 최신 버전으로 업데이트합니다.

amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
# Amazon Linux Extras를 사용하여 lamp-mariadb10.2-php7.2와 php7.2 패키지를 설치합니다.
# 이를 통해 LAMP (Linux, Apache, MySQL, PHP) 스택을 설치하고, MariaDB 10.2 버전과 PHP 7.2를 사용할 수 있도록 합니다.

yum install -y httpd mariadb-server
# yum 명령어를 사용하여 Apache 웹 서버와 MariaDB 데이터베이스 서버를 설치합니다.

systemctl start httpd
# Apache 웹 서버를 시작합니다.

systemctl enable httpd
# 시스템 부팅 시 자동으로 Apache 웹 서버가 시작되도록 설정합니다.

usermod -a -G apache ec2-user
# ec2-user를 apache 그룹에 추가합니다. 
# 이렇게 하면 ec2-user도 Apache 웹 서버에 접근할 수 있습니다.

chown -R ec2-user:apache /var/www
# /var/www 디렉토리 및 그 하위 파일과 디렉토리의 소유자를 ec2-user로, 그룹을 apache로 변경합니다.
# 이렇게 함으로써 Apache 웹 서버와 ec2-user가 /var/www 디렉토리 내의 파일들을 공유할 수 있습니다.

chmod 2775 /var/www
# /var/www 디렉토리에 setgid를 설정합니다. 
# 이로 인해 새로운 파일과 디렉토리는 자동으로 apache 그룹을 상속합니다.

find /var/www -type d -exec chmod 2775 {} \;
# /var/www 디렉토리 및 하위 디렉토리들에 대해 setgid를 설정합니다.
# 이렇게 함으로써 새로운 디렉토리들은 자동으로 apache 그룹을 상속하게 됩니다.

find /var/www -type f -exec chmod 0664 {} \;
# /var/www 디렉토리 및 하위 파일들에 대해 쓰기 권한이 없는 다른 사용자들도 읽기와 쓰기를 할 수 있도록 권한을 설정합니다.

```

<br>
---

<br>

## 연결이 되었음을 확인하고 ssh로 접속해보자

```
ssh -i ./ec2-public-seoul.pem ec2-user@3.37.35.84
```

<img width="211" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/af1a49e2-542e-409a-856b-7f34a0bc8725">

ec2-user로 접속 시 10.0.1.77(프라이빗 주소로) 접속됨을 확인할 수 있다.

<img width="421" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/6c36d59b-575b-4d53-a935-80e1dbd864f5">

index.php를 생성하여 아래 내용을 적어준다.

```
<?php include "dbinfo.inc"; ?>
<html>
<body>
<h1>Instance data</h1>
<?php

  echo "<table>";
  echo "<tr><th>Data</th><th>Value</th></tr>";

  $urlRoot="http://169.254.169.254/latest/meta-data/";

  echo "<tr><td>Instance ID</td><td><i>" . file_get_contents($urlRoot . 'instance-id') . "</i></td><tr>";
  echo "<tr><td>Private IP Address</td><td><i>" . file_get_contents($urlRoot . 'local-ipv4') . "</i></td><tr>";
  echo "<tr><td>Public IP Address</td><td><i>" . file_get_contents($urlRoot . 'public-ipv4') . "</i></td><tr>";
  echo "<tr><td>Availability Zone</td><td><i>" . file_get_contents($urlRoot . 'placement/availability-zone') . "</i></td><tr>";

  echo "</table>";

?>
<h1>RDS Practice</h1>
<?php

  /* Connect to MySQL and select the database. */
  $connection = mysqli_connect(DB_SERVER, DB_USERNAME, DB_PASSWORD);

  if (mysqli_connect_errno()) echo "Failed to connect to MySQL: " . mysqli_connect_error();

  $database = mysqli_select_db($connection, DB_DATABASE);

?>

<!-- Display table data. -->
<table border="1" cellpadding="2" cellspacing="2">
  <tr>
    <td>ID</td>
    <td>NAME</td>
    <td>ADDRESS</td>
  </tr>

<?php

$result = mysqli_query($connection, "SELECT * FROM SAMPLE");

while($query_data = mysqli_fetch_row($result)) {
  echo "<tr>";
  echo "<td>",$query_data[0], "</td>",
       "<td>",$query_data[1], "</td>",
       "<td>",$query_data[2], "</td>";
  echo "</tr>";
}
?>

</table>

<!-- Clean up. -->
<?php

  mysqli_free_result($result);
  mysqli_close($connection);

?>

</body>
</html>
```

<br>
<img width="742" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/2dd6e2cc-7d54-458f-8c64-5ceb5e10ea5d">


