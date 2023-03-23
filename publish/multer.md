 ```js
 const storage = multer.diskStorage({
	destination: function (req, file, cb) {
	cb(null, "public/assets");
	},
	filename: function (req, file, cb) {
	cb(null, file.originalname);
	},
});

const upload = multer({ storage });

//이 코드가 무슨 말이지? 
app.post("/auth/register", upload.single("picture"), register);
 ```

upload.single("picture")은 미들웨어 , register가 실행되기 전 upload.single("picture")이 먼저 실행된다. ![[스크린샷 2023-03-08 오전 11.59.56.png]]
미들웨어를 거쳐 회원가입이 일어나기 전에 아래의 프론트엔트와 같이 input field의 value가 picture로 되어있어 해당하는 이미지를 백앤드로 가지고 오는것. 

```js
<Dropzone
 acceptedFiles=".jpg,.jpeg,.png"
 multiple={false}
 onDrop={acceptedFiles =>
 setFieldValue('picture', acceptedFiles[0])
}

>
```


```js
 const storage = multer.diskStorage({
	destination: function (req, file, cb) {
	cb(null, "public/assets");
	},
	filename: function (req, file, cb) {
	cb(null, file.originalname);
	},
});
```
이게 무슨 코드지? 


  
