---
icon: '2'
---

# Iteration

## 1. .map()

```javascript
 return (
                <>
                    <input type="text" value={inputValue} onChange={handleChange} placeholder="이름을 입력하세요"/>
                    <button onClick={handleAdd}>추가</button>

                    <ul>
                        {names.map(name => (
                            <li key={name.id} onDoubleClick={() =>handleRemove(name.id)}>{name.text}
                                <button onClick={() => handleRemove(name.id)}>삭제</button>
                            </li>
                        ))}
                    </ul>
                </>
            )
```

.map() 메서드를 통해서 배열 객체를 순회하며 tag를 생성할 수 있다.

map을 이용할 때는 반드시 key 값이 필요하다.



## 2. 배열.filter()

기존 배열에서 callback 함수를 각 요소마다 실행하고 true를 반환하는 요소들만으로\
다시 배열을 정의하여 반환하는 배열의 메소드이다.

```javascript
const updated = names.filter(name => name.id !== id);
```
