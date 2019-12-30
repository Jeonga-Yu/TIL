# ES6

> 책 빠른 모바일 앱 개발을 위한 React Native 정리

ES6는 ECMAScript 6의 줄임말이며 '하모니'로도 불리는 ECMAScript의 새로운 버전이다.

## 비구조화

비구조화 할당(Destructuring assignment)을 이용하면 간략한 표현식으로 객체에서 데이터를 편리하게 추출할 수 있다.

>ES5 호환코드
```
var myObj = {a: 1, b:2};
var a = myObj.a;
var b = myObj.b;
```

> 비구조화 할당 표현식
```
var {a, b} = {a:1, b:2};
```

이 표현식은 모듈을 불러오는 구문에서 많이 보인다.


> 비구조화 표현식 없이 View 컴포넌트 불러오기
```
var ReactNative = require('react-native');
var View = ReactNativ.View;
```

>비구조화 표현식을 이용하여 View 컴포넌트 불러오기
```
var { View } = require('react-native');
```

## 모듈 불러오기
컴포넌트나 다른 자바스크립트 모듈을 내보내고 불러올 때 CommonJS 모듈 문법을 주로 사용한다.
이 방식은 다른 모듈을 불러오기 위해 require를 사용하고, 파일의 내용을 다른 모듈에서 사용할 수 있게 하기 위해 module.exports에 값을 할당한다.
> CommonJS 문법을 이용한 모듈 내보내기와 불러오기
```
var OtherComponent = require('./other_component');
var MyComponent = React.createClass({
  . . . 
});
module.exports = MyComponent;
```

ES6 모듈 문법에서는 export와 import 명령어를 사용한다.

> ES6 모듈 문법을 이용한 모듈 내보내기와 불러오기
```
import OtherComponent from './other_component';
var Mycomponent = React.createClass({
  . . .
});
export default MyComponent;
```

## 함수 축약 표현식
>ES5 호환 자바스크립스 함수선언

```
render: function() {
  return <Text>Hi</Text>;
}
```

> 축약 표현식으로 함수선언

``` 
render() {
  return <Text>Hi</Text>;
}
```

## 두꺼운 화살표 함수
ES5 호환 자바스크립트에서는 함수가 실행되는 콘텍스트(context, 예를 들어 this 변수)를 명확히 하기 위해 
함수 실행 시 bind 명령을 이용하곤 한다.
콜백(callback)을 다룰 때 특히 많이 사용한다.

> ES5 호환 자바스크립트에서 수동으로 함수 바인딩하기
```
var callbackFunc = function(val) {
  console.log('Do something');
}.bind(this);
```

두꺼운 화살표 함수(Fat Arrow Function)는 자동으로 바인딩되기 때문에 따로 해줄 필요가 없다.

>바인딩을 위해 두꺼운 화살표 함수 사용하기
```
var callbackFunc = (val) => {
  console.log('Do something');
}
```

## 문자열 조립(템플릿 문자열)
>ES5 호환 자바스크립트에서 문자열 조립
```
var API_KEY = 'abcdefg';
var url = 'http://someapi.com/request&key=' + API_KEY;
```

ES6에서는 여러 줄에 걸친 문자열 조립을 지원하는 템플릿 문자열을 제공한다. 문자열을 백틱(backtick, `)으로 감싸면 __${}__ 문법을
이용하여 문자열 중간에 변수의 값을 넣을 수 있다.
>ES6의 문자열 조립
```
var API_KEY = 'abcdefg;
var url = `http://someapi.com/request&key=${API_KEY}`;
```

## 클래스
>ES6 클래스
```
class HelloMessage extends Component {
  render() {
    . . .
  }
}
```

- 생성자에서 초기화
클래스에는 생성자(constructor) 함수가 있다. state를 초기화하고자 할 때는 getInitalstate 대신에 생성자에서 직접 지정해야 한다.

## let과 const

함수 안에서만 유효한 변수를 선언할 때 var를 사용해왔다.
ES6에서는 변수의 유효 범위를 지정하는 let과 const가 추가되었다.

let은 블록 유효범위를 갖는 변수를 선언할 때 사용한다.
const는 상수를 선언할 때 사용하며 const로 지정한 변수는 초기화 이후에 값을 변경할 수 없다.
