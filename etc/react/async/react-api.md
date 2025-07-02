# React 컴포넌트 분리와 API 호출

#### 1. 컴포넌트 분리 (Component Separation)

* **개념**: 하나의 큰 기능을 작은 단위의 컴포넌트로 나누어 개발하는 방식
* **장점**:
  * 코드 재사용성 증가
  * 유지보수 용이
  * 가독성 향상
  * 각 컴포넌트의 역할이 명확해짐

**실습한 컴포넌트들:**

* `Title`: 제목을 표시하는 컴포넌트
* `PokemonList`: 포켓몬 목록을 관리하는 컴포넌트
* `Card`: 개별 포켓몬 정보를 표시하는 컴포넌트
* `App`: 전체 애플리케이션을 조합하는 최상위 컴포넌트

#### 2. Fetch API

* **개념**: 웹 브라우저에서 HTTP 요청을 보내기 위한 JavaScript API
* **특징**: Promise 기반으로 비동기 처리

**기본 사용법:**

```javascript
fetch('https://pokeapi.co/api/v2/pokemon')
  .then(response => response.json())
  .then(data => console.log(data));
```

**실습에서 사용한 API:**

* 포켓몬 목록: `https://pokeapi.co/api/v2/pokemon`
* 개별 포켓몬 정보: `https://pokeapi.co/api/v2/pokemon/{id}`
* 포켓몬 종족 정보: `https://pokeapi.co/api/v2/pokemon-species/{name}`

#### 3. React Hooks

**useState**

* **목적**: 컴포넌트의 상태를 관리
* **사용법**: `const [state, setState] = useState(초기값)`

**실습 예시:**

```javascript
const [pokemonList, setPokemonList] = useState([]);
const [pokemon, setPokemon] = useState({});
const [speciesInfo, setSpeciesInfo] = useState({});
```

**useEffect**

* **목적**: 컴포넌트의 생명주기에 따른 부수 효과 처리
* **사용 시점**: 컴포넌트가 마운트될 때, 업데이트될 때, 언마운트될 때

**실습 예시:**

```javascript
useEffect(() => {
    getPokemonList(setPokemonList);
}, []); // 빈 배열: 컴포넌트 마운트 시에만 실행
```

#### 4. 비동기 처리 (Async/Await)

* **개념**: Promise를 더 간단하게 처리할 수 있는 문법
* **장점**: 코드가 동기적으로 보여서 이해하기 쉬움

**실습 예시:**

```javascript
const loadData = async () => {
    await getPokemon(url, setPokemon);
    const result = await getPokemonKorSpecies(name);
    setSpeciesInfo(result);
}
```

#### 5. Props

* **개념**: 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 방법
* **특징**: 읽기 전용, 단방향 데이터 흐름

**실습 예시:**

```javascript
// 부모에서 자식으로 props 전달
<Card name={pokemon.name} url={pokemon.url} />

// 자식에서 props 받기
function Card({ name, url }) {
  // name과 url 사용
}
```

#### 6. 조건부 렌더링

* **개념**: 특정 조건에 따라 다른 UI를 표시하는 방법
* **방법**: 논리 연산자(&), 삼항 연산자(?:), 옵셔널 체이닝(?.) 사용

**실습 예시:**

```javascript
<img src={pokemon.sprites?.front_default} />
// sprites가 존재할 때만 front_default에 접근
```

#### 7. 배열 렌더링

* **방법**: map() 함수를 사용하여 배열의 각 요소를 컴포넌트로 변환

**실습 예시:**

```javascript
{pokemonList.map(pokemon => 
  <Card name={pokemon.name} url={pokemon.url} />
)}
```

#### 8. 학습한 주요 개념 정리

**컴포넌트 설계 원칙:**

* 단일 책임 원칙: 각 컴포넌트는 하나의 역할만 담당
* 재사용 가능성: 다른 곳에서도 사용할 수 있도록 설계
* 명확한 Props: 필요한 데이터만 전달

**API 호출 패턴:**

* useEffect에서 API 호출
* 로딩 상태 관리
* 에러 처리 고려

