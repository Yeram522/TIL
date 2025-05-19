---
icon: gear
---

# setting

### 1. 새로운 계정 만들기

```sql
CREATE USER '<생성할아이디>'@'<호스트>'IENTIFIED BY'<생성할비밀번호>';
```

host = 접속할 수 있는 호스트 지정

`localhost` : 로컬 호스트에서만 접속 가능

`%` : 외부 접근 허용

```sql
CREATE USER 'test'@'localhost'IENTIFIED BY'1234';
CREATE USER 'test'@'%'IENTIFIED BY'1234';
```

#### 현재 존재하는 데이터 베이스 확인

```sql
SHOW databases;
```

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

#### mysql 데이터베이스로 계정 정보 확인

```sql
-- 데이터 베이스 선택 명령어
USE mysql;

-- 유저리스트 조회하기
SELECT * FROM USER;
```

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

### 2. 데이터베이스 생성 후 계정에 권한 부여

```sql
CREATE DATABASE menudb;
```

{% code title="test 데이터베이스에 대한 권한 부여" %}
```sql
GRANT ALL PRIVILEGES ON menudb.* TO 'ohgiraffers'@'%';
```
{% endcode %}

{% code title="ohgiraffers에 대한 권한 보" %}
```sql
SHOW GRANTS FOR 'ohgiraffers'@'%';
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>
