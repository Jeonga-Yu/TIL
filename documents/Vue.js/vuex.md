# Vuex
vue.js 애플리케이션에 대한 상태 관리 패턴 + 라이브러리이다. 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 한다.

### 간단한 저장소 예제

    const store = new Vuex.Store({
      state: {
        count: 0
      },
      mutations: {
        increment (state) {
          state.count++
        }
      }
    })

`store.commit 메소드`로 상태 변경을 트리거 할 수 있다.

    store.commit('increment')
    
    console.log(store.state.count) // -> 1

[참고](https://vuex.vuejs.org/kr/guide/)
