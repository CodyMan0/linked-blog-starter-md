-> OR 연산자로 계산할때 0은 falsy로 귀결돼 원하는 값을 얻지 못할때가 있다. 그럴떄 사용할 수 있는 것 **Null 병합 연산자**!!

```js
funtion incrementcreateElement(type,height,width) {
const element = document.createElement(type||'div');
element.style.height = String(hegiht ||10) + 'px';
element.style.width = String(width || 10) + 'px';

return element;
}
```

```js
//바꾼 코드 
funtion incrementcreateElement(type,height,width) {
const element = document.createElement(type ??'div');
element.style.height = String(hegiht ?? 10) + 'px';
element.style.width = String(width ?? 10) + 'px';

return element;
}
```
피연산자가 Null이거나 Undefined일때만 적용이된다. 

-> 부작용이 있을 수 있다. 아무때나 사용하는것이 아니라 NULL과 Undefined일때만 값을 얻고 싶을때 사용