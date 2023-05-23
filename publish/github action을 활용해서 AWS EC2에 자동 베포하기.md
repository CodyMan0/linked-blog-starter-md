
불편했던 것: 백엔드 서버를 어찌 어찌 해서 구현했고 fileZilla 서버에 현재 로컬에 있는 node.js 서버를 복사해서 Aws EC2 instance에 붙혀넣어주어 구현을 했다. 여기서 문제는 그렇다면 매번 이런식으로 베포를 해야하는 걸까? 절대 아니지!! 우선 간단하게 github action으로 자동화해보려고 한다. 

내가 하려고 하는 것  **Github 프로젝트 코드를 AWS S3 에 업로드 한 후 AWS EC2 에서 끌어다 쓰는 것이 가장 핵심**이며 AWS CodeDeploy 는 그걸 보조해주는 역할을 담당합니다.

## 쉽게 ssh 접근하기

### 1. keypair가 있는 디렉토리에서 keypair 복사
```
$ cp my-key.pem ~/.ssh/
```

### 2. 키 페어 파일 권한 변경
```
$ chmod 600 my-key.pem
```

### ~/.ssh/config 파일 생성
```shell
// $ vi ~/.ssh/config

Host podo
User ubuntu
HostName 3.35.131.144
IdentityFile ~/.ssh/aws-ec2-keypair.pem
```

### 설정한 HOST로 접속
```
ssh podo
```


## 생각 
1. 복잡한 베포가 아니라 굳이 CodyDeploy 서비스를 사용할 필요가 있을까? 필요없다. 



## Github Secrets 설정

우선 CICD.yml에서 사용 할 수 있도록, aws에 접근 가능한 AWS-ACCESS-KEY와 SECRET-KEY를 Github에 설정해야 합니다.

엑세스 키 : AWS 홈페이지 -> 본인 이름 -> 자격 증명 -> 엑세스 키 만들기


![[Pasted image 20230520141836.png|500]]

## 2. EC2 설정 추가
인스턴스를 만든 상태에서 3가지를 추가할 예정입니다.
1. Tag를 추가하려고 합니다. CodyDeploy에서 어떤 인스턴스에 실행할지를 구분하는 값으로 사용될 예정입니다.
2. IAM 역할을 등록합니다. 왜? EC2 인스턴스에서 S3 에 올려놓은 파일에 접근할 수 있도록 권한을 추가해줘야 합니다.
3. EC2 서버에 CodyDeploy Agent를 설처합니다. 왜? 

### 2.1 Tag 추가 
태그 이름  : podo-ec2-tag
### IAM Role 설정
역할 이름 : podo-ec2-iam-role

### CodyDeploy Agent 설치
```shell
sudo apt update
sudo apt install ruby-full
sudo apt install wget
wget https://aws-codedeploy-ap-northeast-2.s3.ap-northeast-2.amazonaws.com/latest/install
$ chmod +x ./install
sudo ./install auto > /tmp/logfile 
sudo service codedeploy-agent status  
```

### AWS S3 생성
AWS S3는 이미지또는 zip파일을 저장하기 위한 스토리지 서비스인데, 현재 제 백엔드 서버에서는 public 하위에 이미지를 저장하고 있습니다. 그러다보니 EC2에서 베포된 서버를 통해 업로드된 이미지와 로컬에서 업로드된 이미지의 url 문제로 UI에 이미지가 표시되지 않는 문제가 발생했습니다. S3를 사용하여 로직을 수정하려고 합니다. 

버킷 이름 : podo-action-s3-bucket


### 4. CodeDeploy 생성
배포를 도와주는 CodeDeploy 생성 및 설정을 진행해봅니다.
역할 이름 : my-codedeploy-iam


### CodeDeploy 어플 계정 생성
이름 :podo-codedeploy-app


### CodeDeploy 배포 그룹 생성
베포 그룹 이름 : podo-codedeploy-group



## 5. Github Actions 에서 사용할 IAM 사용자 추가
사용자 이름 : my-github-actions-iam-user


## AppSpec 파일 작성
지금까지 한 건 EC2, 베포할 결과물 저장할 S3, 베포 도와줄 CodeDeploy  서비스를 만듬.

CodeDeploy에서 참조할 AppSpec 파일 작성. 이 문서를 통해서 어떤 파일을 EC2의 어떤 경로에 복사할지를 설정할 수 있고 베포 프로세스 이후에 수행할 스크립트를 지정해서 자동으로 서버를 띄울 수 있다. 


AppSpec 작성하기 전, 우선 백엔드 현재 로컬에 저장하는 코드를 수정해야할 것 같다. 
그럼 나는 S3를 베포할 결과물을 저장할때 그리고 정적인 이미지를 저장할때 사용한다. 

Q. github action으로 빌드된 S3 결과물을 EC2 인스턴스에 베포하는 이유가 뭐지? 그냥 github code로 올리면 안되나? 
A.
1. node.js 디팬던시 문제가 있을 수 있다. githuv actions를 사용하면 빌드 및 종속성 관리를 자동할 수 있다.
2. 확장성 : 원래 제가 하던 방식인 EC2에 직접 코드를 푸쉬했던 것 보다 훨씬 유연하게 관리할 수 있다. 다양한 베포 환경에 대응할 ㅅ ㅜ있다. 아아!! 테스트 환경, 스테이징 환경, 프로덕션 환경 등에 대해 다른 베포 절차를 정의할 수 있다.
3. 보안 : 제가 했던 방식인 코드를 바로 EC2에 푸쉬하는 것보다 보안적으로 안전하다. 



# 도움이 된 자료 
1. S3에 이미지 담기 이미지 :  https://myunji.tistory.com/386
2. 전반적인 베포 과정  : https://bcp0109.tistory.com/363