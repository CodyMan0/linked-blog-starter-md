Elastic compute cloud
원격 제어를 이용해서 컴퓨터를 제공  

SSH키로 내 컴퓨터 터미널에서 가상 컴퓨터에 웹서버 깔기

### ssh로 연결
인스턴스 연결 누르면 SSH 클라이언트 메뉴를 누릅니다 

만들어놓은 키페어를 자신이 원하는 폴더에 넣어놓고 터미널로 키페어가 속한 폴더로 이동합니다

예시를 복사하여 붙혀넣기 합니다

그러면 에러 생김 
> waring: unprotexted private key file 

파일의 권한이 모두에게 허용되어있어 권한을 수정해야 접근할 수 있다는 뜻입니다. 
```
chomd 400 // 두번째 자리와 세번째 자리가 모두 0이어야한다. 
```




### AWS instance 
1. sudo apt update;
2. sudo apt install apache2
	-> EC2 컴퓨터의 ip로 사용자들은 접속할 수 있게 된다.


### 로컬로 해당 Instance에 접근하기
3. well-known port
  -   22 - SSH(Secure Shell)
        -   네트워크 프로토콜 중 하나로 안전하게 통신하기 위해 사용하는 프로토콜
        -   대표적으로 데이터 전송(git push)와 원격 제어(EC2 인스턴스 접속)에 사용
    -   80 - HTTP
    -   443 - HTTPS
![[스크린샷 2023-03-04 오후 3.00.46.png]]

### 리눅스에서 노드 앱 구동시키기 
[[PM2]]
1. sudo apt update
2. sudo apt install nodejs npm 
3. ==웹 서버를 저기에 옮기는것 -> 해야한다.==  
	1. github를 사용하자
	- [x] filezilla를 사용하자
		-> 1. filezilla 세팅해서 연결 후, server 파일 업로드
		2. npm i (모든 디팬던시 install)
		
1. sudo npm install --global pm2;
2. (sudo로 실행) sudo pm2 start (앱.js)
3. (컴퓨터가 꺼졌다가 켜졌을떄 자동 실행)sudo pm2 save, sudo pm2 startup
4. (일반 사용자로 80번 포트 사용하기 위해) 

#### IPtables (네트워크의 흐름 제어)
8. sudo iptables - A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8000;
9. [[linux]]의 ipTables는 ==휘발성== : 리눅스의 패킷 필터링(Packet Filtering) 도구로서 방화벽 구성이나 NAT(Network Address Translation)에 사용된다.
10. ipTables를 복원시켜주는 앱 -> iptables-persistent
11. sudo apt install iptables-persistent
12. cat /etc/iptables/rules.v4 안에 내용이 있다. 이 내용때문에 컴퓨터가 켜지면 해당 상태로 된다. 
13. sudo bash -c "iptables-save > /etc/iptables/rules.v4"; 를 통해  8번 상태를 rules.v4에 저장하여 카피한 것 
14. (일반 사용자 권한)



### 리눅스에서 mongoDB를 사용하는 법
내 우분투 버전 확인 : ubuntu-jammy-22.04-amd64-server-20230208
![[스크린샷 2023-03-05 오후 12.05.02.png]]
나는 22.04에 해당



1. 명령어를 입력해서 GPG키를 받아서 실행
```linux
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
```

ok가 보여지면 다음 단계로 넘어가자
첫번째 단계 설명: 몽고 디비의 키를 발행하여 몽고 디비에서 제공한 소프트웨어를 안전하게 사용하도록 키를 발행하는 것. 

2. 우분투 22.04 LTS 설치할 목록을 만들어야한다.

```
lsb_release -dc
```
를 통해 자신의 우분투의 버젼을 알 수 있따. 


```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```


cat 명령어를 통해서 저장이 됐는지 확인 할 수 있다. 
```
cat /etc/apt/sources.list.d/mongodb-org-6.0.list
```

3. 설치 프로그램 apt-get의 설치할 목록 최신화
```
sudo apt-get update
```


4. 프로그램 설치 과정
```
sudo apt-get install -y mongodb-org
```

4-1 지속적인 업그레이드로 인한 자동 업데이트를 막아주는 코드 (선택)

```
echo "mongodb-org hold" | sudo dpkg --set-selections

echo "mongodb-org-database hold" | sudo dpkg --set-selections

echo "mongodb-org-server hold" | sudo dpkg --set-selections

echo "mongodb-mongosh hold" | sudo dpkg --set-selections

echo "mongodb-org-mongos hold" | sudo dpkg --set-selections

echo "mongodb-org-tools hold" | sudo dpkg --set-selections
```


# 몽고 디비 시작하기 
```
sudo systemctl start mongod
```

잘 작동하는지 확인 
```
sudo systemctl status mongod
```

q버튼을 눌러서 종료 가능 

재부팅할때 자동으로 mongoDB 시작하도록 하려면 실행

```
sudo systemctl enable mongod
```

 몽고 DB 외부 접속 허용하기 /etc/mongod.conf 파일 수정하기 
 
```
sudo vi /etc/mongod.conf
```


```
127.0.0.1 -> 0.0.0.0
```


재시작

```
sudo systemctl restart mongod
```

서버 open된 상태 확인
```
sudo netstat -tnlp | grep mongo
```





# 포트가 안열리는 문제 

1. http://ip주소:8000을 하면 무한 로딩에 빠져 결국 html을 못 가져오는 상황이어서 apache 서버의 80번 포트가 열려있는지 확인하는 과정. 
2. 확인하려고 하는데 netstat가 없다고 한다.
```
sudo netstat -tulpn | grep apache2
```

net stat 설치 
```
sudo apt-get install net-tools
```

포트포워딩 문제인가? 싶어서 iptables 확인하는 도중 만난 에러

iptables v1.8.7 (nf_tables): unknown option "--dport"

생활 코딩 코드 다시 보기 
```
sudo iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8000;
```
사용자 요청이 80번 포트로 들어오면 8000번 포트로 리디렉트 시키는 코드 
-> 성공 

iptable 설정 저장했다가 컴퓨터 



# https , http

[[소셜 미디어 에러 노트]]
12. [mixed content] Mixed Content: The page at 'https://codyman0.github.io/podo/' was loaded over HTTPS, but requested an insecure resource 'http://3.36.123.70/auth/login'. This request has been blocked; the content must be served over HTTPS.

클라이언트 github page는 https , EC2의 서버는 http 프로토콜이어서 통신을 하지 못하는 상황이 발생 

## 인증서 설치

## 공부
### 용어 정리
HTTP : Hypertext Transfer Protocol -> HTML을 전송하기 위한 통신 규약 
HTTPS: Hypertext Transfer Protocol Secure
HTTPS와 SSL의 차이 : SSL이 HTTP보다 더 포괄적이고 HTTP가 SSL을 이용하게 되면 HTTPS 프로토콜이 된다.
SSL과 TLS : SSL은 네스케이프에서 발명되었는데 점점 사용되면서 표준화기구로 인해 TLS라는 이름으로 바뀐 것 뿐입니다.  


### SSL 인증서 동작 원리 
클라이언트와 서버간의 통신을 제 3자가 보증해주는 전자화된 문서! 
이점 
1. **통신 내용이 공격자에게 노출되는 것을 막는다**
	암호화가 필요하다.  
	key를 가지고 정보를 암호화하고 복호화할 수 있다.
	대칭키 : 클라이언트와 서버간에 가지고 있는 키가 동일한 방식
	-> 대칭키의 단점을 보완한 ==공개키==
	공개키는 키가 두개 (모두에게 공유된 공개키 , 개인키 )
	대칭키는 키가 한개
	비대칭키 원리 : 가지고 있는 공개키로 서버로 보내는 메세지를 암호화하여 서버로 보내면 됨. 
	-> 이로인해 키를 배달할때 탈취되는 문제를 해결 

공개키를 활용하여 인증 원리 
  

#### SSL 인증서의 역할
인증서 안에 공개키가 담겨있다!

#### SSL 인증서의 내용
1. 서비스의 정보 (인증서 발급한 CA, 서비스의 도메인)
2. 서버 측의 공개키 (공개키의 내용, 공개키의 암호화 방법)


#### CA를 브라우저는 알고 있다. 
CA는 root 인증 기관을 기본적으로 브라우저는 알고 있다.

#### SSL 인증서가 서비스를 보증하는 방법
1. 브라우저가 서버로 접속할떄 서버는 먼저 클라이언트에게 인증서를 제공
2. 브라우저는 인증서의 CA가 root 인증 기관 리스트에 있는지 확인한다. 포함되어있다면 
3. 공개키를 이용하여 인증서를 복호화한다. 


## 인증서 붙히는 가장 쉬운 방법 cloudFlare
cloudFlare가 대신하여 https를 제공하고 cloundflare에서 우리서버와 http로 동작하면서 중간에서 https 통신을 관리해준다. 


### **HSTS 우회**


[[도메인 구입 과정]]으로 인해서 podostore.store을 구입
[[AWS EC2와 도메인 연결 ]] -> http://www.podostore.store

https://www.youtube.com/watch?v=B__QpelmCMM (2분 1초 )

[[cloudFlare를 활용하여 웹서버 https로 바꾸는 과정 ]]



https://ap-northeast-2.console.aws.amazon.com/ec2/home?region=ap-northeast-2#InstanceDetails:instanceId=i-07a233024232d41a9

에러
-> cloudFlare를 사용하여 CDN 서버로 네임서버를 돌렸음에도 불구하고 적용이 안되는 상황 


몇 단계 더 추가 작업이 남아 있습니다.
참고자료 : https://blog.naver.com/websiteman
참고 : https://www.szkorean.net/2020/05/cloudflare-dns-lets-encrypt-v2-ui.html

cloudFlare에서 -> 페이지 규칙 설정 

![[스크린샷 2023-03-07 오후 4.59.04.png]]


성공
![[스크린샷 2023-03-07 오후 5.00.17.png]]
## 서버와 클라이언트 베포된 애들끼리 통신시키기 






로컬에서만 실행하지 않고 어디서든 서버 데이터를 받게 하고 싶은데??

**AWS Ec2** 

그럼 Ec2 컴퓨터가 꺼져도 어떻게 실행되게 하지?

**PM2**

그럼 어떻게 https 인증서를 붙히지?

**CloudFlare** 

사용하려면 도메인이 있어야한다

**가비아** 

로컬 파일이 바뀌면 자동으로 AWS EC2의 코드도 업데이트 될 수 있을까!? 











# 예산 설정 






### 참고 자료 
AWS 서버 접속 및 에러 해결 정리
https://soobakba.tistory.com/53