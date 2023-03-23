
1.  클래스 컴포넌트  
    
    
``` js
    // App.js 
    import React from 'react'; 
    class App extends React.Component {   
    render(){
        return <h1>This is Class Component!</h1>;  
        }
	} 
	export default App;
```

클래스 컴포넌트에서는 위와 같이 반드시 **render()** 메서드가 있어야 하고, 그 안에서 화면에 보여줄 **JSX(Javascript Syntax eXtension)** 를 반환합니다. state 및 lifecycle(라이프사이클) API를 통해 관련 기능을 사용할 수 있습니다. 


2. 함수 컴포넌트  
      
       
``` js
    // App.js 
    import React from 'react';
    const App = () => {
     return <h1>This is Function Component!</h1>; }; 
     
    export default App;
    
```
`
함수 컴포넌트는 render() 메서드 없이 JSX를 반환하는 방식으로, 클래스 컴포넌트에 비해서 훨씬 간단하고 ==단순하지만 state와 라이프사이클을 관리하지 못한다는 단점(함수형에도 단점이있었구나..)==으로 인해 잘 사용되지 않았습니다. ==하지만 React 16.8 버전에서 **Hook** 기능이 추가되면서 함수 컴포넌트에서도 state를 사용할 수 있게 되었고, 그 후부터 클래스 컴포넌트보다는 함수 컴포넌트가 더 많이 사용되기 시작했습니다.==  ==이것때문에 hook을 배우는거 였구나)== 


### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : 
