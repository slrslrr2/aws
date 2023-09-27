<br>
# 섹션3-3 데이터베이스의 Read replica 생성 및 웹 서버 연결
<br><br>

1. 데이터베이스 Read Replica 생성
2. EC2-Read Replica DB 연결
3. 웹 브라우저를 통해 Read Replica DB 연결 테스트
4. 원본 DB 변경 후 웹브라우저를 통해 Read Replica 반영 테스트

<img width="625" alt="1" src="https://github.com/slrslrr2/aws/assets/58017318/d4011067-8fee-44ed-87d0-173a86b332a6">
<br>
<br>

## 1. Read Replica 생성하기
<img width="788" alt="2" src="https://github.com/slrslrr2/aws/assets/58017318/0ba3711e-7aac-4751-a191-c21612dd973f">
<br><br>
<img width="616" alt="3" src="https://github.com/slrslrr2/aws/assets/58017318/ef99fc41-ade5-474f-a0e8-69314c39cd83">
<br><br>
<img width="617" alt="4" src="https://github.com/slrslrr2/aws/assets/58017318/da126493-b754-43a4-9526-23047b2ad4e3">
<br><br>
<img width="616" alt="5" src="https://github.com/slrslrr2/aws/assets/58017318/6ee0e403-8857-4f96-8f65-9316bef8e1df">
<br><br>
<img width="618" alt="6" src="https://github.com/slrslrr2/aws/assets/58017318/1c4ab7f7-16e4-4d99-b935-d62069dbeadd">
<br><br>
<img width="614" alt="7" src="https://github.com/slrslrr2/aws/assets/58017318/cbb59fdc-6a74-4e27-8cca-ccdecfaddd75">
<br><br>
<img width="616" alt="8" src="https://github.com/slrslrr2/aws/assets/58017318/42f1dbfd-36f6-45a6-9942-2ef44c62944d">
<br><br>
<img width="1450" alt="9" src="https://github.com/slrslrr2/aws/assets/58017318/2e415626-f9b9-410e-bae7-39a5d61f98a5">
<br><br>
<br>

## 2. Master, ReadReplica 접속 및 연동 확인
<br><br>
1. Master에 DB INSERT 시 
<img width="572" alt="10" src="https://github.com/slrslrr2/aws/assets/58017318/3665329e-daa8-4cd6-82c4-555c6bb508b7">
<br><br>
2. Read Replica에도 표시됨을 알 수 있다.
<img width="335" alt="11" src="https://github.com/slrslrr2/aws/assets/58017318/78b40829-e0d7-4e9a-b5c3-aaba929c0a29">
<br><br>
3. Read Replica에 INSERT 를 시도할경우, 실행되지 않는다
<img width="801" alt="12" src="https://github.com/slrslrr2/aws/assets/58017318/cb116102-b45a-4353-9f8f-146f990db0c3">
<br><br>
결론적으로 Master와 Read Replica의 Data는 동기화되며, Read Replica에서 쓰기작업은 불가능하다.
