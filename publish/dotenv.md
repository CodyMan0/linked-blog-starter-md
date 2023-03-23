사용 이유 

여러 운영체제 마다 환경 변수를 설정하는 방식이 다른데 dotenv 라이브러리를 통해 모든 운영체제에서 동일한 코드 로직으로 환경 변수를 설정할 수 있게 해준다. 

```
npm i dotenv
```

라이브러리를 설치한 후, .env에 외부로 노출되지 않아야하는 변수를 선언합니다. 

```
MONGO_URL ='mongodb+srv://id:password@mongodb.smguf3j.mongodb.net/?retryWrites=true&w=majority'

PORT=8000

JWT_SECRET = 'string'
```
