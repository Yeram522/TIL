# lambda 함수와 리스트 정렬 (sort())

## &#x20;**1. `lambda` 함수란?**

`lambda` 함수는 **이름이 없는 간단한 함수**를 만드는 키워드이다. 주로 **한 줄로 끝나는 표현식 함수**를 만들 때 사용한다.

```python
lambda 매개변수: 표현식
```

예:

```python
lambda x: x + 10
```

***

## &#x20;**2. 리스트 정렬에서 `lambda` 활용**

`list.sort()` 또는 `sorted()` 함수에서 `key` 매개변수에 `lambda`를 사용하면, **정렬 기준을 직접 지정**할 수 있다.

```python
리스트.sort(key=lambda 요소: 정렬기준값)
```

***

## **3. 실습 예제**

**📌 예제 1: 튜플 리스트 정렬**

```python
items = [('apple', 3), ('banana', 1), ('cherry', 2)]
items.sort(key=lambda x: x[1])
# 결과: [('banana', 1), ('cherry', 2), ('apple', 3)]
```

**📌 예제 2: 딕셔너리 리스트 정렬**

```python
inventory = [
    {'item_name': 'healing_potion', 'price': 50},
    {'item_name': 'sword_of_legend', 'price': 10000},
    {'item_name': 'iron_shield', 'price': 1500},
    {'item_name': 'mana_potion', 'price': 40}
]

# 가격 기준 정렬
inventory.sort(key=lambda item: item['price'])
```

**📌 예제 3: 내림차순 정렬**

```python
inventory.sort(key=lambda item: item['price'], reverse=True)
```

**📌 예제 4: 정렬 기준이 여러 개인 경우**

```python
inventory.sort(key=lambda item: (item['price'], item['item_name']))
```

***

**💡 학습 요약**

* `lambda`는 간단한 함수를 inline으로 사용할 수 있어서 정렬 기준을 작성할 때 유용하다.
* `sort()`나 `sorted()` 함수의 `key` 매개변수에 `lambda`를 쓰면 리스트 요소를 원하는 기준대로 정렬할 수 있다.
* 정렬 기준이 단일 값이든 복합 값이든 `lambda`로 처리 가능하다.
* `reverse=True`를 사용하면 내림차순 정렬도 가능하다.

***
