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

### 8. redux-actions 라이브러리

#### 1.1 redux-actions란?

* **Redux 코드 간소화 라이브러리**: Action Creator와 Reducer 작성을 더 쉽고 간결하게 만들어주는 유틸리티
* **보일러플레이트 코드 감소**: 반복적인 switch문과 액션 생성자 코드를 줄여줌
* **일관된 코드 스타일**: 표준화된 방식으로 Redux 코드 작성 가능

#### 1.2 기존 방식 vs redux-actions 방식

**기존 방식의 문제점**

```javascript
// 많은 보일러플레이트 코드
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

const increment = (value) => ({
    type: INCREMENT,
    payload: { value }
});

function counterReducer(state = 0, action) {
    switch(action.type) {
        case INCREMENT:
            return state + action.payload.value;
        case DECREMENT:
            return state - action.payload.value;
        default:
            return state;
    }
}
```

**redux-actions 방식의 장점**

* 코드량 대폭 감소
* 오타 위험성 줄어듦
* 일관된 패턴으로 유지보수 용이

### 9. createAction 메소드

#### 2.1 createAction 기본 사용법

```javascript
import { createAction } from 'redux-actions';

// 기본 사용
const increment = createAction('INCREMENT');
const decrement = createAction('DECREMENT');

// 결과: increment() => { type: 'INCREMENT' }
// 결과: increment(5) => { type: 'INCREMENT', payload: 5 }
```

#### 2.2 createAction의 고급 기능

```javascript
// payload 변환 함수 사용
const addTodo = createAction('ADD_TODO', (text) => ({
    id: Date.now(),
    text,
    completed: false
}));

// meta 정보 추가
const fetchUser = createAction('FETCH_USER', 
    (userId) => ({ userId }),           // payload creator
    (userId) => ({ timestamp: Date.now() })  // meta creator
);
```

#### 2.3 createAction 활용 예제

```javascript
// 사용자 관리 액션들
const setUser = createAction('SET_USER');
const updateUser = createAction('UPDATE_USER', (id, updates) => ({ id, updates }));
const deleteUser = createAction('DELETE_USER');

// 폼 관리 액션들
const setFormField = createAction('SET_FORM_FIELD', (field, value) => ({ field, value }));
const resetForm = createAction('RESET_FORM');
const submitForm = createAction('SUBMIT_FORM');
```

### 10. createActions 메소드

#### 3.1 여러 액션을 한번에 생성

```javascript
import { createActions } from 'redux-actions';

// 여러 액션을 객체로 한번에 생성
const { increment, decrement, reset } = createActions({
    INCREMENT: (value = 1) => ({ value }),
    DECREMENT: (value = 1) => ({ value }),
    RESET: () => ({})
});

// 중첩된 액션 생성
const { todo: { add, toggle, remove } } = createActions({
    TODO: {
        ADD: (text) => ({ text }),
        TOGGLE: (id) => ({ id }),
        REMOVE: (id) => ({ id })
    }
});
```

#### 3.2 createActions의 실용적 활용

```javascript
// 사용자 관리 모듈
const userActions = createActions({
    FETCH_USERS_START: () => ({}),
    FETCH_USERS_SUCCESS: (users) => ({ users }),
    FETCH_USERS_ERROR: (error) => ({ error }),
    CREATE_USER: (userData) => userData,
    UPDATE_USER: (id, updates) => ({ id, updates }),
    DELETE_USER: (id) => ({ id })
});
```

### 11. handleActions 메소드

#### 4.1 handleActions 기본 개념

* **switch문 대체**: 기존의 긴 switch문을 객체 형태로 간소화
* **타입 안전성**: 액션 타입 오타 방지
* **가독성 향상**: 각 액션별 처리 로직이 명확히 분리

#### 4.2 기본 사용법

```javascript
import { handleActions } from 'redux-actions';

const counterReducer = handleActions({
    [increment]: (state, action) => state + action.payload.value,
    [decrement]: (state, action) => state - action.payload.value,
    [reset]: () => 0
}, 0); // 초기 상태
```

#### 4.3 복잡한 상태 관리 예제

```javascript
const todoReducer = handleActions({
    [addTodo]: (state, action) => ({
        ...state,
        todos: [...state.todos, {
            id: action.payload.id,
            text: action.payload.text,
            completed: false
        }]
    }),
    
    [toggleTodo]: (state, action) => ({
        ...state,
        todos: state.todos.map(todo =>
            todo.id === action.payload.id
                ? { ...todo, completed: !todo.completed }
                : todo
        )
    }),
    
    [removeTodo]: (state, action) => ({
        ...state,
        todos: state.todos.filter(todo => todo.id !== action.payload.id)
    })
}, {
    todos: [],
    filter: 'all'
});
```

### 12. Redux Middleware 개념

#### 5.1 Middleware란?

* **Action과 Reducer 사이의 중간 처리자**: Action이 dispatch되고 Reducer에 도달하기 전에 실행되는 함수
* **확장 포인트**: Redux의 기본 기능을 확장할 수 있는 공식적인 방법
* **체인 형태**: 여러 미들웨어를 연결하여 순차적으로 실행 가능

#### 5.2 Middleware의 동작 원리

```
Action Dispatch → Middleware 1 → Middleware 2 → ... → Reducer → State Update
```

#### 5.3 Middleware가 해결하는 문제들

* **로깅**: 모든 액션과 상태 변화 기록
* **비동기 처리**: API 호출 등 비동기 작업 관리
* **에러 처리**: 전역 에러 핸들링
* **라우팅**: 액션에 따른 페이지 이동
* **성능 모니터링**: 액션 처리 시간 측정

#### 5.4 Middleware 적용 방법

```javascript
import { createStore, applyMiddleware } from 'redux';

const store = createStore(
    rootReducer,
    applyMiddleware(middleware1, middleware2, middleware3)
);
```

### 13. redux-logger

#### 6.1 redux-logger의 역할

* **개발 도구**: 모든 액션과 상태 변화를 콘솔에 자동으로 로깅
* **디버깅 지원**: 액션 전후의 상태를 비교하여 디버깅 용이
* **개발 환경 전용**: 프로덕션에서는 제외하고 개발 시에만 사용

#### 6.2 redux-logger가 제공하는 정보

* **이전 상태 (prev state)**: 액션 실행 전의 상태
* **액션 정보 (action)**: 실행된 액션의 type과 payload
* **다음 상태 (next state)**: 액션 실행 후의 새로운 상태
* **시간 정보**: 액션 실행 시간과 소요 시간

#### 6.3 redux-logger 설정 및 활용

```javascript
import logger from 'redux-logger';

// 기본 사용
const store = createStore(
    rootReducer,
    applyMiddleware(logger)
);

// 커스텀 설정
const customLogger = createLogger({
    predicate: (getState, action) => action.type !== 'SOME_ACTION',
    collapsed: true,
    duration: true,
    diff: true
});
```

#### 6.4 로깅 정보 해석 방법

* 콘솔에서 펼쳐지는 로그의 구조 이해
* 상태 변화 추적을 통한 버그 발견
* 성능 이슈 파악 (duration 정보 활용)

### 14. redux-thunk (비동기 처리)

#### 7.1 redux-thunk의 필요성

* **기본 Redux의 한계**: 동기적 액션만 처리 가능
* **비동기 작업의 필요성**: API 호출, 타이머, 파일 읽기 등
* **Thunk 패턴**: 지연 실행이 가능한 함수를 반환하는 패턴

#### 7.2 redux-thunk 동작 원리

* 함수를 dispatch할 수 있게 해주는 미들웨어
* Thunk 함수는 `dispatch`와 `getState`를 인자로 받음
* 내부에서 여러 액션을 순차적으로 dispatch 가능

#### 7.3 비동기 액션의 일반적인 패턴

```javascript
// 3단계 패턴: START → SUCCESS/ERROR
const fetchUsersStart = createAction('FETCH_USERS_START');
const fetchUsersSuccess = createAction('FETCH_USERS_SUCCESS');
const fetchUsersError = createAction('FETCH_USERS_ERROR');

// Thunk 액션 크리에이터
const fetchUsers = () => async (dispatch, getState) => {
    dispatch(fetchUsersStart());
    
    try {
        const response = await api.getUsers();
        dispatch(fetchUsersSuccess(response.data));
    } catch (error) {
        dispatch(fetchUsersError(error.message));
    }
};
```

### 15. 실제 프로젝트에서의 활용

#### 8.1 redux-actions + middleware 조합 사용법

```javascript
// 액션 생성
const { fetchData, updateData, deleteData } = createActions({
    FETCH_DATA_START: () => ({}),
    FETCH_DATA_SUCCESS: (data) => ({ data }),
    FETCH_DATA_ERROR: (error) => ({ error }),
    UPDATE_DATA: (id, updates) => ({ id, updates }),
    DELETE_DATA: (id) => ({ id })
});

// 리듀서 생성
const dataReducer = handleActions({
    [fetchDataStart]: (state) => ({ ...state, loading: true }),
    [fetchDataSuccess]: (state, action) => ({
        ...state,
        loading: false,
        data: action.payload.data
    }),
    [fetchDataError]: (state, action) => ({
        ...state,
        loading: false,
        error: action.payload.error
    })
}, initialState);
```

#### 8.2 개발 환경 설정

```javascript
// 개발용 미들웨어 설정
const isDevelopment = process.env.NODE_ENV === 'development';

const middlewares = [thunk];
if (isDevelopment) {
    middlewares.push(logger);
}

const store = createStore(
    rootReducer,
    applyMiddleware(...middlewares)
);
```

