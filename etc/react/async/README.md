---
icon: '3'
---

# Async

## 1. Promise와 비동기 처리의 이해

**Promise란?**

* 비동기 작업의 완료 또는 실패를 나타내는 객체
* 세 가지 상태: Pending(대기), Fulfilled(이행), Rejected(거부)
* 콜백 지옥(Callback Hell)을 해결하기 위해 도입된 패턴

```javascript
// Promise 기본 구조
const promise = new Promise((resolve, reject) => {
    // 비동기 작업
    if (성공) {
        resolve(결과);
    } else {
        reject(에러);
    }
});
```

## 2. Callback Hell의 문제점

**Callback Hell이란?**

* 중첩된 콜백 함수들로 인해 코드가 피라미드 모양으로 깊어지는 현상
* 코드 가독성 저하, 디버깅 어려움, 유지보수 곤란

```javascript
// Callback Hell 예시
getData(function(a) {
    getMoreData(a, function(b) {
        getEvenMoreData(b, function(c) {
            getYetMoreData(c, function(d) {
                // 계속 중첩...
            });
        });
    });
});
```

## 3. Then 체이닝으로 해결

**`.then()` 메서드**

* Promise가 이행될 때 실행되는 메서드
* 체이닝을 통해 콜백 지옥 문제 해결
* 평면적이고 읽기 쉬운 코드 작성 가능

```javascript
// Then 체이닝 예시
axios.get('https://api.github.com/emojis')
    .then(response => {
        console.log('데이터 받음:', response.data);
        return response.data;
    })
    .then(data => {
        // 데이터 처리
        if (data[emojiname]) {
            setImageUrl(data[emojiname]);
        }
    })
    .catch(error => {
        console.error('에러 발생:', error);
    });
```

## 4. React에서의 비동기 처리 실습

**실습 프로젝트: GitHub 이모지 검색 앱**

**주요 컴포넌트 구조:**

* `App`: 상태 관리 (imageUrl)
* `SearchBox`: 사용자 입력 처리
* `ImageBox`: 이미지 표시
* `SearchEmoji`: API 호출 함수

**핵심 코드 패턴:**

```javascript
function SearchEmoji(emojiname, setImageUrl) {
    axios.get('https://api.github.com/emojis')
        .then(response => {
            const emojis = response.data;
            if (emojis[emojiname]) {
                setImageUrl(emojis[emojiname]);
            } else {
                setImageUrl('');
            }
        })
        .catch(error => {
            console.error('API 호출 실패:', error);
        });
}
```

## 5. 마주친 문제들과 해결 과정

**문제 1: API 응답 데이터 구조 이해**

* 초기 실수: `Object.keys(response.data)` 사용
* 해결: `response.data` 객체 직접 접근
* 학습: API 스키마 `{ "type": "object", "additionalProperties": { "type": "string" } }` 이해

**문제 2: React 상태 전달과 스코프**

* 초기 실수: 함수 간 상태 공유 문제
* 해결: Props를 통한 `setImageUrl` 함수 전달
* 학습: React의 단방향 데이터 흐름 이해

**문제 3: 비동기 함수의 반환값 처리**

* 초기 실수: `onClick={() => setImageUrl(SearchEmoji(emojiname))}`
* 문제점: Promise는 즉시 반환되지 않음
* 해결: 콜백 함수 내에서 상태 업데이트 직접 수행

**문제 4: API 요청 제한 (403 Forbidden)**

* 원인: GitHub API 시간당 60회 제한
* 해결: 더미 데이터로 대체하여 학습 진행
* 학습: API 사용 시 rate limiting 고려 필요성

#### 🔧 사용한 기술 스택

* **React**: 컴포넌트 기반 UI 구성
* **Axios**: HTTP 클라이언트 라이브러리
* **GitHub API**: 이모지 데이터 소스
* **useState**: React 상태 관리 Hook
* **useEffect**: 사이드 이펙트 처리 Hook

#### 💡 핵심 학습 포인트

#### 비동기 처리 패턴의 진화

1. **Callback** → 콜백 지옥 문제
2. **Promise + .then()** → 체이닝으로 가독성 개선
3. **async/await** → 동기식 코드처럼 작성 가능

#### React에서 비동기 처리 시 주의사항

* 컴포넌트 언마운트 후 상태 업데이트 방지
* 에러 처리를 통한 사용자 경험 향상
* API 호출 최적화 (중복 요청 방지, 캐싱 등)
