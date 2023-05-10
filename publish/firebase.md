리액트에서 firebase를 사용하여 로그인 youtube.com/watch?v=cZAnibwI9u8


1. npm install firebase
2. firebase 연결
```js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";

// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
	apiKey: "AIzaSyC1EKZVIQCTPVs96j4r3r6xyJtkpREdE2o",
	authDomain: "test-56693.firebaseapp.com",
	projectId: "test-56693",
	storageBucket: "test-56693.appspot.com",
	messagingSenderId: "384473862273",
	appId: "1:384473862273:web:6498473609cc0d7ed1bd80",
};
// Initialize Firebase
const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);

```


