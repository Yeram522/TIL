---
icon: '5'
---

# Redux

### 1. Redux 핵심 개념

#### Redux란?

* **상태관리 라이브러리**: 애플리케이션의 모든 상태를 하나의 저장소(store)에서 관리
* **예측 가능한 상태 관리**: 상태 변경을 예측 가능하게 만들어 디버깅과 테스트를 쉽게 함
* **단방향 데이터 흐름**: Action → Reducer → Store → View 순서로 데이터가 흐름

#### Redux의 3가지 원칙

1. **Single Source of Truth**: 앱의 모든 상태는 하나의 store에 저장
2. **State is Read-Only**: 상태를 변경하는 유일한 방법은 action을 dispatch하는 것
3. **Changes are Made with Pure Functions**: 상태 변경은 순수 함수인 reducer로만 가능

### 2. Redux 핵심 구성 요소

#### Store (저장소)

```javascript
const store = createStore(reducer);
```

* 앱의 전체 상태를 보관하는 객체
* `getState()`: 현재 상태 조회
* `dispatch(action)`: 액션을 발생시켜 상태 변경
* `subscribe(listener)`: 상태 변화 감지

#### Action (액션)

```javascript
{
    type: 'INCREMENT',        // 필수: 어떤 동작인지 설명
    payload: {               // 옵션: 추가 데이터
        incrementValue: 1
    }
}
```

* 상태 변경을 요청하는 객체
* `type`은 필수, `payload`는 선택사항

#### Reducer (리듀서)

```javascript
function reducer(state = initialState, action) {
    switch(action.type) {
        case 'INCREMENT':
            return state + action.payload.incrementValue;
        default:
            return state;
    }
}
```

* 현재 상태와 액션을 받아 새로운 상태를 반환하는 순수 함수
* **순수 함수**: 같은 입력에 대해 항상 같은 출력, 부작용 없음

### 3. 바닐라 Redux 예제

#### 기본 카운터 예제

```javascript
// 1. 리듀서 정의
function counter(state = 0, action) {
    switch(action.type) {
        case 'INCREMENT': return state + 1;
        case 'DECREMENT': return state - 1;
        default: return state;
    }
}

// 2. 스토어 생성
const store = createStore(counter);

// 3. 상태 변화 구독
store.subscribe(() => console.log(store.getState()));

// 4. 액션 발생
store.dispatch({type: 'INCREMENT'});  // 1
store.dispatch({type: 'INCREMENT'});  // 2
store.dispatch({type: 'DECREMENT'}); // 1
```

### 4. React-Redux 연동

#### Provider 컴포넌트

```javascript
<Provider store={store}>
    <App />
</Provider>
```

* Redux 스토어를 React 컴포넌트 트리에 제공
* 하위 컴포넌트들이 스토어에 접근할 수 있게 함

#### useSelector 훅

```javascript
const count = useSelector(state => state);
```

* 스토어의 상태를 조회하는 훅
* 상태가 변경되면 컴포넌트가 자동으로 리렌더링

#### useDispatch 훅

```javascript
const dispatch = useDispatch();
dispatch({ type: 'INCREMENT', payload: { incrementValue: 1 } });
```

* 액션을 발생시키는 훅
* 리듀서 함수를 호출하여 상태 변경

### 5. combineReducers를 이용한 복합 상태 관리

#### 여러 리듀서 결합

```javascript
const rootReducer = combineReducers({
    counter: counterReducer,
    user: userReducer,
    ui: uiReducer
});
```

#### 상태 구조

```javascript
// 결합된 상태 구조
{
    counter: { currentCount: 5 },
    user: { name: '', email: '', phone: '' },
    ui: { isActive: false }
}
```

#### 특정 상태 선택

```javascript
const count = useSelector(state => state.counter.currentCount);
const user = useSelector(state => state.user);
```

### 6. 실습 코드의 주요 오타 및 수정 사항

#### 발견된 오타들

1. `ReacRedux` → `ReactRedux`
2. `paylaod` → `payload`
3. `useselector` → `useSelector`
4. `togleActivation` → `toggleActivation`
5. Input 태그의 name 속성이 모두 "name"으로 동일
6. ReactDOM.render()에 컴포넌트 전달 누락

#### 수정된 완전한 예제

```javascript
// 올바른 구조분해할당
const {createStore, combineReducers} = Redux;
const {useSelector, useDispatch, Provider} = ReactRedux;

// 올바른 payload 사용
case 'INCREMENT':
    return {currentCount: state.currentCount + payload.incrementValue}

// 올바른 input 설정
<input type="text" name="email" value={email} onChange={onChangeHandler}/>
<input type="text" name="phone" value={phone} onChange={onChangeHandler}/>

// 올바른 렌더링
ReactDOM.createRoot(document.getElementById("root")).render(
    <Provider store={store}>
        <App />
    </Provider>
);
```

### 7. Ducks 패턴 (코드 조직화)

#### 개념

* 관련된 액션 타입, 액션 생성자, 리듀서를 하나의 파일에 모아두는 패턴
* 모듈별로 상태 관리 코드를 조직화

#### 구조

```javascript
// 액션 타입 (접두사로 모듈명 사용)
const INCREMENT = 'count/INCREMENT';
const DECREMENT = 'count/DECREMENT';

// 액션 생성자
const increase = () => ({ type: INCREMENT, payload: { incrementValue: 1 } });
const decrease = () => ({ type: DECREMENT, payload: { decrementValue: 1 } });

// 리듀서
function countReducer(state = initialState, action) {
    // 리듀서 로직
}
```

### 8. 학습 요점 정리

#### Redux 사용 시 주의사항

1. **불변성 유지**: 상태를 직접 수정하지 말고 새로운 객체/배열 반환
2. **순수 함수**: 리듀서는 부작용 없는 순수 함수여야 함
3. **액션 타입 상수화**: 오타 방지를 위해 액션 타입을 상수로 선언
4. **payload 네이밍**: 일관된 네이밍 규칙 사용

#### 디버깅 팁

1. Redux DevTools 확장 프로그램 사용
2. console.log로 상태 변화 추적
3. 액션과 리듀서의 타입 검사

#### 언제 Redux를 사용할까?

* 여러 컴포넌트가 동일한 상태를 공유해야 할 때
* 상태 변경 로직이 복잡할 때
* 상태 변경 히스토리를 추적해야 할 때
* 중대형 애플리케이션에서 상태 관리가 복잡할 때
