# ➕ Collection

컬렉션 프레임워크는 데이터를 효율적으로 저장하는 **자료구조**와&#x20;데이터를 처리하는 **알고리즘**을 미리 구현해놓은 클래스이다.

Collection Framework는 크게 3가지 인터페이스 중 한 가지를 상속받아 구현해 놓았다.

1.  List 인터페이스

    •   **순서 있는** 데이터 집합으로 데이터의 **중복 저장을 허용**한다.

    •   <mark style="color:green;">vector, ArrayList, LinkedList, Stack, Queue</mark> 등이 있다.


2.  Set 인터페이스

    •  **순서가 없는** 데이터 집합으로 데이터의 **중복을 허용하지 않**는다.

    •  <mark style="color:green;">HashSet, TreeSet</mark> 등이 있다.


3.  Map 인터페이스

    •  **키와 값 한 쌍**으로 이루어지는 데이터 집합이다.    \
    •  key를 <mark style="background-color:yellow;">**Set 방식으로 관리**</mark>하기 때문에 데이터의 순서를 관리하지 않고 **중복된 key를 허용하지 않**는다.    \
    •  _<mark style="color:orange;">value는 중복된 값을 저장할 수 있다.</mark>_    \
    •  <mark style="color:green;">HashMap, TreeMap, HashTable, Properties</mark> 등이 있다.

## 1️⃣ List

### ArrayList

가장 많이 사용되는 컬렉션 클래스이다.\
내부적으로 **배열을 이용**하여 요소를 관리하며, <mark style="color:red;">인덱스를 이용해 배열 요소에 빠르게 접근</mark>할 수 있다.

\
ArrayList는 배열의 단점을 보완하기 위해 만들어졌다.\
배열은 크기를 변경할 수 없고, 요소의 추가, 삭제, 정렬 등이 복잡하다는 단점을 가지고 있다.

\
ArrayList는 저러한 배열의 단점을 보완하고자\
**크기 변경, 요소의 추가, 삭제, 정렬 기능**들을 미리 메소드로 구현해서 제공하고 있다.\
자동적으로 수행되는 것이지 _<mark style="color:red;">속도가 빨라지는 것이 아니다.</mark>_

```java
       ArrayList aList = new ArrayList();

        List list = new ArrayList();

        Collection clist = new ArrayList<>();

        aList.add("apple");
        aList.add(123);
        aList.add(45.34);
        aList.add(new Date());

        System.out.println(aList);
        System.out.println(aList.size());

        for(int i = 0; i < aList.size(); i++){
            System.out.println(i + " : "  + aList.get(i));
        }

        // 데이터의 중복 저장을 허용
        aList.add("apple");
        System.out.println(aList);

        aList.add(1, "banana");
        System.out.println(aList);

        // 값을 삭제할 때
        aList.remove(2);
        System.out.println(aList);

        // 값을 수정할 때
        aList.set(1, Boolean.valueOf(true));
        System.out.println(aList);

        List<String> stringList = new ArrayList<>();
        stringList.add("apple");
//        stringList.add(123);
        stringList.add("banana");
        stringList.add("orange");
        stringList.add("mango");

        System.out.println(stringList);
        // 오름차순 정렬
        Collections.sort(stringList);
        System.out.println(stringList);
```

### Iterator

Collection 인터페이스의 iterator() 메소드를 이용해서 인스턴스를 생성할 수 있다.\
컬렉션에서 값을 읽어오는 방식을 통일된 방식으로 제공하기 위해 사용한다.\
**반복자** 라고 불리우며, <mark style="background-color:green;">반복문을 이용해서 목록을 하나씩 꺼내는 방식으로 사용하기 위함</mark>이다.\
인덱스로 관리되는 컬렉션이 아닌 경우에는 반복문을 사용해서 요소에 하나씩 접근할 수 없기 때문에&#x20;<mark style="background-color:green;">인덱스를 사용하지 않고도 반복문을 사용하기 위한 목록을 만들어주는 역할</mark>이라고 보면 된다.\
`hasNext()` : 다음 요소를 가지고 있는 경우 true, 더 이상 요소가 없는 경우 false 반환\
`next()` : 다음 요소를 반환

{% code title="✅ 내림차순 정렬" %}
```markup
stringList = new LinkedList<>(stringList);
/*LinkedList 타입으로 현변환 한 후 descendingIterator() 메소드를 사용하면
* 내림차순 정렬된 Iterator 타입의 목록으로 반환을 해준다. */
Iterator<String> dIter = ((LinkedList<String>)stringList).descendingIterator();
```
{% endcode %}

```java
while (dIter.hasNext()){
    System.out.println(dIter.next());
}

List<String> descList = new ArrayList<>();
while (dIter.hasNext()){
    descList.add(dIter.next());
}
System.out.println(descList);
```

만약, ArrayList의 타입을 사용자 지정 클래스로 정해놓았다면 위에서 사용했던 `sort` 함수는 사용할 수 없다.

{% code title="❌ 사용자 지정 타입은 ArrayList의 sort함수 사용 불가능" %}
```java
List<BookDTO> bookList = new ArrayList<>();
        
bookList.add(new BookDTO(1, "홍길동전", "허균",50000));
bookList.add(new BookDTO(2, "목민심서", "정약용",30000));
bookList.add(new BookDTO(3, "동의보감", "허준",40000));
bookList.add(new BookDTO(4, "삼국사기", "김부식",46000));
bookList.add(new BookDTO(5, "삼국유사", "일연",58000));

Collections.sort(bookList);  //❌ 문법 에러
```
{% endcode %}

### Comparator

Comparator 인터페이스의 compare 함수는 `@Contract(pure=true)` 라고 되어있는데,\
이는 순수 가상 함수라는 뜻으로, 구현할 때 반드시 해당 함수를 오버라이딩 해야 한다는 의미이다.

```java
public class AscendingPrice implements Comparator<BookDTO> {

    @Override
    public int compare(BookDTO o1, BookDTO o2) {

        int result = 0;

        // 오름 차순이기 때문에 순서를 바꿔야 하는 경우는 양수를 반환하도록 한다.
        if(o1.getPrice() > o2.getPrice()){
            
            result =  1;

        }else if(o1.getPrice() < o2.getPrice()){            
            // 이미 오름차순 정렬 돼서 음수 반환
            result = -1;
        } else{
            // 두 값이 같을 경우
            result = 0;
        }

        return result;
    }
}
```

{% code title="✅ Comparator의 compare 오버라이딩" %}
```java
bookList.sort(new AscendingPrice());
```
{% endcode %}

{% code title="✅ 익명 클래스를 이용" %}
```java
bookList.sort(new Comparator<BookDTO>() { // 익명 클래스
    @Override
    public int compare(BookDTO o1, BookDTO o2) {

        // 순서를 바꾸는 경우 양수, 바꾸지 않는 경우에는 음수 반환
        return o1.getPrice() >= o2.getPrice() ? -1 : 1;
    }
});
```
{% endcode %}

{% code title="✅ string의 compareTo 함수를 이용한 정렬" %}
```java
bookList.sort((BookDTO b1, BookDTO b2) -> b2.getTitle().compareTo(b1.getTitle()));
```
{% endcode %}
