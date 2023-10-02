<br>
# 섹션3-4 Failover를 통한 데이터베이스 이중화 테스트
<br><br>

1. Master/Standby DB IP 정보 확인
2. Master DB Failover (Reboot with Failover)
3. Standby DB가 Master DB로 변경 확인
4. 웹 브라우저를 통해 DB 연결 테스트

<img width="625" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/e768c9ec-4c68-4cff-acf0-8f1a6953ba0f">

<br><br>

연결 & 보안에서 가용영역이 ap-northeast-2c로 되어있음으로써,
Master는 private-2c가용영역에 존재함을 알 수 있다.
<img width="781" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/57a1323f-4874-45a1-9e79-59d3b8548d57">
![3](https://github.com/slrslrr2/aws/assets/58017318/9c092519-e320-4a77-91ee-a7599879ec51)

<br><br>
`dig 엔드포인트` 명령어 입력 시 아래와 같이 표시된다.

`ANSWER SECTION` 부분에서 10.0.6.26으로 응답함으로써 
ptivate-subnet-c2의 IPv4 CIDR영역인 `10.0.6.0/24` 에 포함됨을 확인할 수 있다.

```
[root@ip-10-0-4-179 html]# dig lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com

; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.amzn2.13.1 <<>> lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 24453
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com. IN A

;; ANSWER SECTION:
lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com. 5 IN	A 10.0.6.26

;; Query time: 1 msec
;; SERVER: 10.0.0.2#53(10.0.0.2)
;; WHEN: 토  8월 19 02:47:08 UTC 2023
;; MSG SIZE  rcvd: 102
```

<br><br>
<img width="810" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/42dfc635-dcff-4d86-9392-c8f76e9cc0bb">
<br><br>
네트워크 인터페이스로도 ap-northeast-2c로 되어있는 상세 IP를 확인 가능하다.

<img width="824" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/5b4c9478-57b6-4eee-8270-23d342780928">


<br><br><br>
### 그렇다면, Failover 시 Master와 Standby가 변경되는지 확인해보자.
<img width="627" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/7d606d1f-9cb5-42ed-a247-264f75334000">

재부팅 후 ANSWER SECTION: 를 확인하여 10.0.5.95로 가용영역이 바뀜을확인할 수 있다.

```
[root@ip-10-0-4-179 html]# dig lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com

; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.amzn2.13.1 <<>> lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48316
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com. IN A

;; ANSWER SECTION:
lab-vpc-rds.co9k21vicozo.ap-northeast-2.rds.amazonaws.com. 5 IN	A 10.0.5.95

;; Query time: 2 msec
;; SERVER: 10.0.0.2#53(10.0.0.2)
;; WHEN: 토  8월 19 02:55:46 UTC 2023
;; MSG SIZE  rcvd: 102
```

<img width="813" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/de37a9ca-e1fd-4a05-89ea-5308f67e7980">
