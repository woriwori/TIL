javascript에서 값을 복사할때, =으로만 가능하지않다.

**원시 타입(primitive: Boolean, Null, Undefined, Number, String, Symbol)** 은 변수에 원시 데이터값이 저장되어,
= 을 할 경우 그 값이 복사된다. 

```javascript
let x = 1;
let y = x;
y = 2;
console.log(x); // 1 
```

**참조 타입(reference: object, array, function)** 은 데이터에 ㅔ대한 참조만 저장되어, =을 할 경우 참조가 복사된다.

```javascript
let x = {n: 1};
let y = x;
y.n = 2;
console.log(x.n); // 2
```

<br>

# Shallow Copy

depth1 까지의 object만 copy를 할 수 있는 방법이다.

- ES6의 Object.assign()

```javascript
let x = {n: 1};
let y = Object.assign({}, x);
y.n = 2;
console.log(x); // 1 
console.log(y); // 2 
```

- ES6의 Spread 문법

```javascript
let x = {n: 1};
let y = {...};
y.n = 2;
console.log(x); // 1 
console.log(y); // 2 
```

- Object.prototype.constructor 사용

```javascript
function copyObj(obj){
  if(!obj || typeof obj !== 'object') return obj;
  const copy = obj.constructor();
  for(let key in obj){
    if(obj.hasOwnProperty(key)) copy[key] = obj[key];
  }
  return copy;
}
let x = {n: 1};
let y = copyObj(x);
y.n = 2;
console.log(x); // 1 
console.log(y); // 2 
```

- library 사용 
   - underscore.js / lodash / ramda / jquery / Angular ...
   
# Deep Copy   

- JSON.stringfy 사용

```javascript
let x = {n: 1, m: {deep: 2}};
let y = JSON.parse(JSON.stringfy(x));
y.m.deep = 3;
console.log(x.m.deep); // 2
console.log(y.m.deep); // 3
```

- Object.prototype.constructor 사용

```javascript
function copyObj(obj){
  if(!obj || typeof obj !== 'object') return obj;
  const copy = obj.constructor();
  for(let key in obj){
    if(obj.hasOwnProperty(key)) copy[key] = obj[key];
  }
  return copy;
}
let x = {n: 1, m: {deep: 2}};
let y = copyObj(x);
y.m.deep = 3;
console.log(x.m.deep); // 2
console.log(y.m.deep); // 3
```
