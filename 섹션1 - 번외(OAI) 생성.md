# OAI(Origin Access Identity)

OAI(Origin Access Identity)는 AWS CloudFront에서 사용되는 보안 기능으로,
원본 서버(S3)의 직접 노출을 방지하고, CloudFront 배포와 연결된 S3 버킷이나 커스텀 오리진(Origin)에 대한 접근을 해용해줌으로써 보안을 강화하여 클라이언트와의 상호작용을 안전하게 유지합니다.

 

진행순서는 아래와 같습니다.

1. S3 버킷을 생성합니다

2. CloudFront OAI 생성

3. CloudFront 배포 생성

4. S3 정책 확인

5. CloudFront를 통해 gonang.png 사진 확인

--- 

### 1. S3 버킷을 생성합니다
![0](https://github.com/slrslrr2/aws/assets/58017318/b98242e3-561b-4552-b49d-92e488043261)
![1](https://github.com/slrslrr2/aws/assets/58017318/c09ec6ce-1aba-4685-9801-4b5fd5f261de)

모든 퍼블릭 액세스를 차단함으로써, S3의 직접적인 차단을 할 수 있습니다.

<br>

###  2. CloudFront OAI 생성
S3의 직접적인 차단을 진행하였으니, OAI를 통하여 S3에 접근하여 S3의 파일을들 가져올 수 있도록 설정하겠습니다.


![2](https://github.com/slrslrr2/aws/assets/58017318/129a2782-be23-4b0d-8cc5-17d3a7365d33)

먼저 OAI를 생성하도록 하겠습니다.

![3](https://github.com/slrslrr2/aws/assets/58017318/0b266844-c3ec-4d7f-a20d-991b116c7a85)

이름을 입력한 후 [생성]버튼을 클릭합니다.
그럼 아래와같은 OAI가 생성됩니다.


![4](https://github.com/slrslrr2/aws/assets/58017318/768b51e3-3b78-4b7b-abb8-3e202112d9a5)



### 3. CloudFront 배포 생성




![5](https://github.com/slrslrr2/aws/assets/58017318/7d67b912-5b7e-4f87-bc10-e3008bf424d0)


![6](https://github.com/slrslrr2/aws/assets/58017318/58340fc9-134a-47d0-9a72-ae7f140dd79c)

1. 원본도메인: 첫번째에 생성한 도메인(S3)를 CloudFront와 연결합니다.
2. 이름: 원하는 CloudFront 명칭을 지정합니다.
3. 원본 액세스: OAI를 생성하였기에 [Legacy access identities]를 선택합니다. 이때, 원본 액세스ID에 연결해줍니다.
4. 버킷정책 업데이트 : 해당 내용을 선택함으로써 S3버킷정책이 자동으로 UPDATE 됩니다.


### 4. S3 정책 확인
![7](https://github.com/slrslrr2/aws/assets/58017318/0258bdfa-c448-428c-83a6-5c849f437b0e)

![8](https://github.com/slrslrr2/aws/assets/58017318/d31320da-6740-49b3-b1eb-a2bb9d5a8347)

S3정책에 CloudFront가 연결된 OAI 정책이 추가됨을 확인할 수 있습니다.

 

이제, S3에 파일을 하나 업로드 합니다. (저는 고양이를 좋아하기에 gonang.png를 업로드 하겠습니다)
![9](https://github.com/slrslrr2/aws/assets/58017318/ba956cb2-abac-491c-ab7b-8bead5bc99ef)


### 5. CloudFront를 통해 gonang.png 사진 확인

아래 주소를 통해 CloudFront 주소를 확인합니다.





![10](https://github.com/slrslrr2/aws/assets/58017318/09f91cc2-6e47-441b-b6d3-8cf4924f204b)
![11](https://github.com/slrslrr2/aws/assets/58017318/a3b41640-5d6c-43a0-a731-e84058a8f60f)


이렇게 S3를 생성하고 CloudFront및 OAI를 연결할 수 있었습니다.

---------------
이렇게 끝내긴 아쉬우니 IAM과 OAI를 간단하게 비교하도록 하겠습니다.

 

OAI(Origin Access Identity)와 IAM(Identity and Access Management)은 AWS의 서로 다른 보안 기능입니다.

OAI (Origin Access Identity):
- 용도: CloudFront에서 사용하는 기능으로, 클라이언트와 오리진 서버 간의 보안을 강화하기 위해 오리진에 대한 액세스를 제어합니다.
- 동작: OAI를 사용하면 CloudFront 배포와 연결된 오리진(S3)에 대한 직접 액세스를 방지하고, CloudFront에서만 오리진(S3)과 통신할 수 있도록 합니다.

IAM (Identity and Access Management):
- 용도: AWS 계정 전반에 걸쳐 서비스 및 리소스에 대한 액세스 권한을 관리하는 AWS의 전체적인 보안 서비스입니다.
- 동작: IAM은 AWS 계정 사용자, 그룹, 역할에 대한 권한을 관리하며, 서비스 간의 상호 작용 및 AWS 리소스에 대한 접근을 제어합니다.


간단히 말하면, OAI는 CloudFront에서 **오리진(S3)에 대한 특정한 접근을 제어**하는 데 사용되는 도구이며, IAM은 AWS 계정 내에서 **전반적인 리소스 및 서비스에 대한 액세스를 관리**하는 데 사용됩니다. **OAI는 주로 클라우드프론트 배포와 연관**되어 있으며, **IAM은 AWS 전체 서비스 및 리소스에 걸친 권한 관리**에 사용됩니다.


