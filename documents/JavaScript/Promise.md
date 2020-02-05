## Promise

참고

[https://jeong-pro.tistory.com/128](https://jeong-pro.tistory.com/128)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)

'비동기에서 성공과 실패를 분리해서 메서드를 수행한다.'

Promise 생성

Promise 객체는 new 키워드와 생성자를 사용하여 만든다. 생성자는 매개변수로 "실행 함수"를 받는다. 이 함수는 매개 변수로 두 가지 함수를 가져야하는데 첫 번째 함수(resolve)는 비동기 작업이 성공적으로 완료되어 결과를 값으로 반환하면 호출되고 두 번째 함수(reject)는 작업이 실패하여 오류의 원인을 반환하면 호출된다. 두 번째 함수는 주로 오류 객체를 받는다.

    const promise1 = () => {
      return new Promise(function (resolve, reject) {
        // resolve(something) // fulfilled
        // reject('failure reason") // rejected
      })
    }