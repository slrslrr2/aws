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
