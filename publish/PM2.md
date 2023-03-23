
nodejs의 프로세스 manager

1. sudo npm install pm2 -g
2. pm2 start index.js
3. ![[스크린샷 2023-03-04 오후 3.32.26.png]]
index.js를 프로세스로 만든 것 
4. pm2 start index.js --watch를 통해서 서버에서 수정이 될때 프로세스를 새로 할당해 반영해주는 역할 
5. pm2 log를 통해서 console.log()를 확인할 수 있다.
6. pm2-dev index.js를 통해서 watch와 log를 같이 볼 수 있다. 
7. pm2 index.js -i max 로 스레드의 갯수 만큼 프로세스가 생성
![[스크린샷 2023-03-04 오후 3.46.13.png]]