**Express** 사용시 **Http 헤더 설정**을 자동으로 바꾸어 **웹 취약성**으로부터 **서버**를 **보호**해주는 **보안 모듈**입니다.

사용 법
```javascript
import express from "express";
import helmet from "helmet";

const app = express();

//기본적인 보안만 설정 
app.use(helmet());

app.use(helmet.crossOriginResourcePolicy({ policy: "cross-origin" }));

// 특정 세부 기능 하나하나 설정할때 사용 app.use(helmet.contentSecurityPolicy()); 
app.use(helmet.crossOriginEmbedderPolicy()); app.use(helmet.crossOriginOpenerPolicy()); app.use(helmet.crossOriginResourcePolicy()); app.use(helmet.dnsPrefetchControl()); app.use(helmet.expectCt()); app.use(helmet.frameguard()); app.use(helmet.hidePoweredBy()); app.use(helmet.hsts()); app.use(helmet.ieNoOpen()); app.use(helmet.noSniff()); app.use(helmet.originAgentCluster()); app.use(helmet.permittedCrossDomainPolicies()); app.use(helmet.referrerPolicy()); app.use(helmet.xssFilter());

```


![[스크린샷 2023-03-08 오후 12.34.28.png]]