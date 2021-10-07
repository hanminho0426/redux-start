## 리덕스의 액션이란?

- 액션은 사실 그냥 객체(object)이다.

- 두 가지 형태의 액션이 있다.

```js
-{ type: "TEST" } - // payload 없는 액션
  { type: "TEST", params: "hello" }; // payload 있는 액션
```

- type 만이 필수 프로퍼티이며, type은 문자열이다.

## 리덕스의 액션 생성자란?

- function 액션생성자 (...args) { return 액션; }
- 액션을 생성하는 함수를 "액션 생성자(Action Creator)"라고 한다.
- 함수를 통해 액션을 생성해서, 액션 객체를 리턴해준다.
- createTest('hello'); //{type: 'TEST', params:'hello'} 리턴

## 리덕스의 액션은 어떤 일을 하나?

- 액션 생성자를 통해 액션을 만들어낸다.
- 만들어낸 액션 객체를 리덕스 스토어에 보낸다.
- 리덕스 스토어가 액션 객체를 받으면 스토어의 상태 값이 변경된다.
- 변경된 상태 값에 의해 상태를 이용하고 있는 컴포넌트가 변경된다.
- 액션은 스토어에 보내는 일종의 인풋이라 생각할 수 있다.

## 액션을 준비하기 위해서는?

- 액션의 타입을 정의하여 변수로 빼는 단계

  - 강제는 아니다(그러므로 안해도 된다.)
  - 그냥 타입을 문자열로 넣기에는 실수를 유발할 가능성이 크다.
  - 미리 정의한 변수를 사용하면, 스펠링에 주의를 덜 기울여도 된다.

- 액션 객체를 만들어 내는 함수를 만드는 단계
  - 하나의 액션 객체를 만들기 위해 하나의 함수를 만들어낸다.
  - 액션의 타입은 미리 정의한 타입 변수로 부터 가져와서 사용한다.

## 리덕스의 리듀서란?

- 액션을 주면, 그 액션이 적용되어 달라진(안달라질수도...) 결과를 만들어준다.

- 그냥 함수다.
  - Pure Function / 항상 같은 인풋을 받으면 같은 인풋의 결과를 내는 함수 / 시간에 따라 달라지는 형태의 코드를 넣으면 안된다.
  - Immutable / 오리지널 스테이트와 바뀌어진 스테이트가 별도의 객체로 만들어져야 한다는 것
    - 왜?
      - 리듀서를 통해 스테이트가 달라졌음을 리덕스가 인지하는 방식(Immutable)

```js
//리덕스의 리듀서 방식
// 함수   이름   현재스테이트,  액션객체
function 리듀서(previousState, action) {
  // 새로운 스테이트 객체
  return newState;
}
```

- 액션을 받아서 스테이트를 리턴하는 구조
- 인자를 들어오는 previousState와 리터되는 newState는 다른 참조를 가지도록 해야한다.

## 스토어를 만드는 함수

```js
const store = createStore(리듀서);
```

- createStore<S>(
  reducer: Reducer<S>,
  preloadedState:S,
  enhancer?: StoreEnhancer<S>
  ): Store<S>;

## store

- store.getState();

- store.dispatch(액션);, store.dispatch(액션생성자());

- const unsubscribe = store.subscribe(() => {});

  - 리턴이 unsubscribe 라는 점!
  - unsubscribe(); 하면 제거

- store.replaceReducer(다른리듀서);
