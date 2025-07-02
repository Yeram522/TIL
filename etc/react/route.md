---
icon: '4'
---

# Route

#### 1. Next.js App Router 개념

* **App Router**: Next.js 13+에서 도입된 새로운 라우팅 시스템
* **폴더 기반 라우팅**: 파일 시스템의 폴더 구조가 URL 경로와 직접 연결
* **page.js**: 각 경로의 UI를 정의하는 특별한 파일명

#### 2. 폴더 구조 기반 라우팅 시스템

**기본 라우팅 구조**

```
app/
├── page.js              # 루트 경로 (/)
├── menu/
│   ├── page.js          # /menu 경로
│   └── [menucode]/
│       └── page.js      # /menu/[동적값] 경로
└── components/
    ├── Header.jsx
    ├── Layout.jsx
    └── Navbar.jsx
```

**라우팅 규칙**

* **폴더명 = URL 경로**: `menu` 폴더 → `/menu` URL
* **page.js**: 해당 경로에서 렌더링될 React 컴포넌트
* **중첩 라우팅**: 폴더 안의 폴더로 하위 경로 생성

#### 3. 동적 라우팅 (Dynamic Routes)

**\[menucode] 폴더 구조**

* **대괄호 표기법**: `[매개변수명]` 형태로 동적 경로 생성
* **URL 매칭**: `/menu/1`, `/menu/pizza`, `/menu/abc` 모두 매칭
* **매개변수 접근**: `useParams()` Hook으로 값 추출

**실습 예시:**

```javascript
// app/menu/[menucode]/page.js
'use client';
import { useParams } from "next/navigation";

export default function MenuDetail() {
    const { menucode } = useParams();
    // menucode에는 URL의 동적 부분이 들어감
    
    return (
        <div>
            <h1>메뉴 코드: {menucode}</h1>
        </div>
    );
}
```

#### 4. 컴포넌트 분리와 재사용

**components 폴더 구조**

```
components/
├── Header.jsx    # 페이지 상단 헤더
├── Layout.jsx    # 전체 레이아웃 틀
└── Navbar.jsx    # 네비게이션 바
```

**각 컴포넌트의 역할**

* **Header.jsx**: 사이트 로고, 제목 등 상단 영역
* **Navbar.jsx**: 메뉴 링크, 네비게이션 요소
* **Layout.jsx**: Header, Navbar를 조합한 전체 레이아웃

#### 5. Layout 컴포넌트 패턴

**Layout.jsx 구현 예시**

```javascript
import Header from './Header';
import Navbar from './Navbar';

export default function Layout({ children }) {
    return (
        <div>
            <Header />
            <Navbar />
            <main>
                {children}
            </main>
        </div>
    );
}
```

**사용 방법**

```javascript
// app/menu/page.js
import Layout from '@/components/Layout';

export default function MenuPage() {
    return (
        <Layout>
            <h1>메뉴 페이지</h1>
            {/* 페이지별 고유 내용 */}
        </Layout>
    );
}
```

#### 6. Next.js vs 순수 React 차이점

**파일 기반 라우팅**

* **React**: React Router 라이브러리 필요
* **Next.js**: 폴더 구조만으로 자동 라우팅

**서버 사이드 렌더링 (SSR)**

* **React**: 클라이언트 사이드 렌더링 기본
* **Next.js**: 서버 사이드 렌더링 기본 지원

**'use client' 지시어**

* **목적**: 클라이언트 컴포넌트임을 명시
* **사용 시점**: useState, useEffect 등 브라우저 API 사용 시

#### 7. 실습한 주요 개념들

**절대 경로 import**

```javascript
import Layout from '@/components/Layout';
// @ 기호로 프로젝트 루트 경로 참조
```

**useParams() Hook**

```javascript
import { useParams } from "next/navigation";

const { menucode } = useParams();
// URL 매개변수 추출
```

**useRouter() Hook**

```javascript
import { useRouter } from "next/navigation";

const router = useRouter();
router.push('/menu/search'); // 프로그래밍 방식 네비게이션
```

#### 8. 컴포넌트 재사용의 장점

**개발 효율성**

* **한 번 작성, 여러 곳 사용**: Header, Navbar 등
* **일관된 UI**: 모든 페이지에서 동일한 레이아웃
* **유지보수 용이**: 컴포넌트 수정 시 전체 적용

**코드 구조화**

* **관심사 분리**: 레이아웃과 페이지 내용 분리
* **모듈화**: 각 컴포넌트의 독립적 관리
* **테스트 용이**: 개별 컴포넌트 단위 테스트

#### 9. 폴더 구조 설계 원칙

**App Router 베스트 프랙티스**

```
app/
├── globals.css          # 전역 스타일
├── layout.js           # 루트 레이아웃
├── page.js             # 홈페이지
├── menu/
│   ├── page.js         # 메뉴 목록
│   ├── search/
│   │   └── page.js     # 메뉴 검색
│   └── [menucode]/
│       └── page.js     # 메뉴 상세
└── components/
    └── [컴포넌트들]
```

**명명 규칙**

* **폴더명**: 소문자, 하이픈 사용 (`menu-list`)
* **동적 라우팅**: 대괄호 + 의미있는 이름 (`[menucode]`)
* **컴포넌트**: PascalCase (`Header.jsx`)

#### 10. 학습한 핵심 기술

**Next.js 특화 기능**

* **파일 기반 라우팅**: 폴더 = URL 경로
* **동적 라우팅**: `[param]` 문법
* **자동 코드 분할**: 페이지별 자동 최적화
* **내장 최적화**: 이미지, 폰트, 번들링 등

**React 기본 개념 응용**

* **컴포넌트 합성**: Layout + 페이지 컴포넌트
* **Props 전달**: children prop 활용
* **상태 관리**: useState로 페이지 상태 관리

#### 11. 다음 학습 과제

* **Middleware**: 라우팅 전 처리 로직
* **Loading UI**: loading.js 파일 활용
* **Error Boundary**: error.js 파일 활용
* **Static Generation**: 정적 사이트 생성
* **API Routes**: 백엔드 API 구축
