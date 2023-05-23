공식문서 : https://reactnative.dev/
공부 출처 : https://nomadcoders.co/react-native-for-beginners/lobby
레포 : https://github.com/CodyMan0/knockknock/blob/master/.node-version

- 네이티브 앱 
아이폰 : Object-c , Swift
안드로이드 : Kotlin

단점 : 각각 운영체제에 맞게 개발을 해야하는 비효율이 생긴다.


- 하이브리드 앱
안드로이드 , 아이폰에서 사용할 수 있도록 

## 하이브리드 앱 개발 동작원리
React Native 코드 변환 :
아이폰에서 실행하면 Object-c or Swift로 변환해준다. 
안드로이드에서 실행하면 Java나 Kotlin으로 변환해준다.


## 장점 
1. 리액트 개발자가 쉽게 배울 수 있다. 
2. 아이폰 , 안드로이드에서 동시에 돌릴 수 있다.


## 단점
1. 리액트와 다르고 어느정도 공부를 해야한다.
2. 네이티브 앱보다 성능 이슈
3. 네이티브 앱의 기능을 전부 지원하지 않고 속도도 느리다. 
4. 개발사가 업데이트를 꾸준히 해줘야 한다. 


# 학습 
테스트를 위한 도구 : expo , watch man 
![[RN 구조.excalidraw.png]]

위에 보이는 모든 인프라스트럭쳐들이 JS가 운영체제와 통신을 할 수 있도록 만들어졌다. 

### 동작 원리 (중요)

RN의 중요한 부분은 인프라 부분! 
RN은 shell과 같고 [[OS Moc]]와 소통할 수 있다. 

[[리액트와 RN의 큰 구조.excalidraw]]
![[리액트와 RN의 큰 구조.excalidraw.png]]

#### STYLESHEET 동작 원리
```ts
const styles = StyleSheet.create({
	container : {
		flex : 1,
		backgroundColor : '#fff',
		alignItems : "center"
	}
	text : {
		fontSize :28,
	}
})
```

그냥 객체 혹은 inline-styling도 적용되지만 styleSheet.create는 객체를 생성하는데 사용하는 이유:
1. 타입스크립트와 같이 **자동 완성**을 제공해준다. 
2. 

### 통신은 어떻게 이루어지는거야? 
[[RN의 통신.excalidraw]]
![[RN의 통신.excalidraw.png|800]]

## 에러 
1. expo로 사용하는데 npm install이 안됨. ENOTE문제
-> sudo chown -R 501:20 "/Users/leejuyoung/.npm" 
.npm 경로에 있는 모든 파일 및 디렉토리 소유자와 그릅을 변경하는 명령어. 
-> "sudo"는 슈퍼 유저로 하라는 의미
=> "chown" 는 파일 또는 디렉토리의 소유자 그룹 변경
-> "R" 재귀적으로 모든 하위 변경
-> 소유자의 그룹을 501:20으로 변경하라는 의미! 



## 실제 구현하면서 다른 점 정리
1. 대부분의 CSS를 적용할 수 있지만 적용하지 못하는 Property가 있다.



## 중요한 point 
1. third party - library 
	1. react Native 
	2. Expo SDK
2. component
3. API 

# 웹과 차이
1. flexBox의 디폴트 값: 웹은 row, 앱은 column
2. 앱에서는 px 사용해서 만들지 않는다.




