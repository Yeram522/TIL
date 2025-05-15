---
icon: clock-ten
---

# Collection

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

### LinkedList

ArrayList가 배열을 이용해서 발생할 수 있는 성능적인 단점을 보완하고자 고안되었다.\
내부는 이중 연결리스트로 구현되어 있다.



#### 단일 연결 리스트

저장한 요소가 순서를 유지하지 않고 저장되지만 이러한 요소들 사이를 링크로 연결하여 구성하며\
마치 연결된 리스트 형태인 것처럼 만든 자료구조

* 장점:  요소의 저장,삭제 시 다음 요소를 가리키는 참조 링크만 변경하면 되기 때문에 요소의 저장과 삭제가 빈번히 일어나는 경우 ArrayList보다 성능면에서 우수
* 단점: 다음 요소만 링크하기 때문에 이전 요소로 접근하기 어렵다. 이를 보완하고자 만든 것이 이중 연결 리스트!

#### 이중 연결 리스트

단일 연결 리스트는 다음 요소만 링크하는 반면 이중 연결 리스트는 이전 요소도 링크하여\
이전 요소로 접근하기 쉽게 고안된 자료구조이다.



LinkedList는 이중 연결리스트를 구현한 것.\
List 인터페이스를 상속 받았기 때문에, ArrayList와 사용하는 방법이 거의 유사하지만 내부적으로 요소를 저장하는 방법에는 차이가 있다.

{% code title="✅ 선언 및 인스턴스 생성" %}
```java
List<String> linkedList = new LinkedList<>();
```
{% endcode %}

{% code title="✅ 원소 삽입" %}
```java
linkedList.add("apple");
linkedList.add("banana");
linkedList.add("orange");
linkedList.add("mango");
linkedList.add("grape");
```
{% endcode %}

{% code title="✅ 원소 삭제" %}
```java
linkedList.remove(1);
```
{% endcode %}

{% code title="✅ 원소 값 변경" %}
```java
linkedList.set(0, "fineapple");
```
{% endcode %}

{% code title="✅ 리스트 순회" %}
```java
for(int i = 0; i < linkedList.size(); i++){
    System.out.println(i + " : "  + linkedList.get(i));
}
```
{% endcode %}

{% code title="✅ 리스트 출력" %}
```java
System.out.println(linkedList); 
```
{% endcode %}

{% code title="✅ 원소 모두 지우기" %}
```java
linkedList.clear();
```
{% endcode %}

{% code title="✅ 리스트가 비어있는지 확인" %}
```javascript
linkedList.isEmpty()
```
{% endcode %}

### Stack

Stack은 리스트 계열 클래스의 vector 클래스를 상속받아서 구현했다.

스택 메모리 구조는 선형 메모리 공간에 데이터를 저장하며,&#x20;후입선출(LIFO - Last Input First Out) 방식의 자료 구조라 불린다.

{% code title="✅ 선언 및 인스턴스 생성" %}
```java
Stack<Integer> integerStack = new Stack<>();
```
{% endcode %}

{% code title="✅ stack 원소 삽입" %}
```java
integerStack.push(1);
integerStack.push(2);
integerStack.push(3);
integerStack.push(4);
integerStack.push(5);
```
{% endcode %}

{% code title="✅ 요소 검색" %}
```java
integerStack.search(5);
```
{% endcode %}

`int search(Object o)` 는 Stack에서 주어진 객체(o)를 찾아서 그 위치를 반환한다.\
못 찾을 경우 -1을 반환한다.\


<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ top 요소 반환" %}
```java
integerStack.peek();
```
{% endcode %}

**peek() :** 해당 스택의 가장 마지막에 있는(상단에 있는) 요소 반환

{% code title="✅ top 요소 반환 후 제거" %}
```java
integerStack.pop();
```
{% endcode %}

**pop() :** 해당 스택의 가장 마지막에 있는(상단에 있는) 요소 반환 후 제거

‼️ 빈 스택에 pop하면 `EmptyStackException` 에러가 난다.

### Queue

선형 메모리 공간에 데이터를 저장하는&#x20;선입선출(FIFO - First Input First Out) 방식의 자료구조.

Queue 인터페이스를 상속받는 하위 인터페이스들은&#x20;Deque, BlockingQueue, BlockingDeque, TransferQueue등 다양하지만&#x20;대부분의 큐는 LinkedList를 이용한다.

{% code title="✅ 선언 및 인스턴스 생성" %}
```java
Queue<String> que = new LinkedList<>();
```
{% endcode %}

{% code title="✅ 데이터 삽입" %}
```java
que.offer("first");
que.offer("second");
que.offer("third");
que.offer("fourth");
que.offer("fifth");
```
{% endcode %}

{% code title="✅ front 요소 반환" %}
```java
que.peek()
```
{% endcode %}

**peek()** : 해당 큐의 가장 앞에 있는 요소(먼저 들어온 요소)를 반환한다.

{% code title="✅ front 요소 반환 후 제거" %}
```java
que.poll()
```
{% endcode %}

**poll() :** 해당 큐의 가장 앞에 있는 요소(먼저 들어온 요소)를 반환하고 제거한다.

## 2️⃣ Set

Set 인터페이스를 구현한 Set 클래스의 특징\
1\. 요소의 저장 순서를 유지하지 않는다.\
2\. 같은 요소의 중복 저장을 허용하지 않는다. (null값도 중복하지 않게 하나의 null만 저장한다.)

### HashSet 클래스

Set 컬렉션 클래스에서 가장 많이 사용되는 클래스 중 하나이다.\
해시 알고리즘을 사용하여 검색 속도가 빠르다는 장점을 가진다.

{% code title="✅ 정의 및 인스턴스 선언" %}
```java
HashSet<String> hset = new HashSet<>();

// HashSet은 Set 인터페이스를 구현하고 있다.
Set hset2 = new HashSet(); 
Collection hset3 = new HashSet<>();// Set 인터페이스는 Collection 인터페이스를 상속한다.
```
{% endcode %}

{% code title="✅ 데이터 삽입" %}
```java
hset.add("java");
hset.add("oracle");
hset.add("jdbc");
hset.add("html");
hset.add("css");
```
{% endcode %}

{% code title="✅ HashSet 크기" %}
```java
hset.size()
```
{% endcode %}

{% code title="✅데이터 검색" %}
```java
hset.contains("oracle")
```
{% endcode %}

💡HashSet은 저장된 객체를 하나씩 꺼내는 기능이 없다.&#x20;반복문을 이용해서 연속 처리하는 방법 2가지가 있다.

✅ 순회

#### 1. toArray() 배열로 바꾸고 반복문 사용

```java
Object[] arr = hset.toArray();
for(int i = 0; i < arr.length; i++){
    System.out.println(i + " : " + arr[i]);
}
```

#### 2. iterator()로 목록 만들어 연속 처리

```java
Iterator<String> iter = hset.iterator();

while(iter.hasNext()){
    System.out.println(iter.next());
}
```

{% code title="✅ 원소 모두 지우기" %}
```java
hset.clear();
```
{% endcode %}

{% code title="✅set이 비어있는지 확인" %}
```java
hset.isEmpty()
```
{% endcode %}

## 3️⃣ Map

### Map 인터페이스 특징

Collection인터페이스와는 다른 저장 방식을 가진다.\
**키(key)**&#xC640; **값(value)**&#xB97C; <mark style="background-color:blue;">하나의 쌍</mark>으로 저장하는 방식을 사용한다.

#### 키(key)란?

<mark style="color:red;">값(value)를 찾기 위한 역할</mark>을 하는 객체를 의미한다.\
1\. 요소의 <mark style="background-color:yellow;">저장 순서를 유지하지 않는다.</mark>\
2\. <mark style="color:red;background-color:yellow;">키는 중복을 허용하지않지만</mark>, 키가 다르면 <mark style="color:red;background-color:yellow;">중복되는 값은 저장 가능</mark>하다.\
\
HashMap, HashTable, TreeMap 등의 대표적인 클래스가 있다.\
HashMap이 가장 많이 사용된다.\
⭐ 해시 알고리즘을 사용하여 검색 속도가 매우 빠르다.

{% code title="✅ 선언 및 인스턴스 생성" %}
```java
HashMap hmap = new HashMap();
Map hmap2 = new HashMap<>();
```
{% endcode %}

{% code title="✅ 데이터 삽입" %}
```java
hmap.put("one", new Date());
hmap.put(12, "red apple");
hmap.put(33, 123);
```
{% endcode %}

{% code title="❌ 키는 중복으로 저장되지 않는다." %}
```java
hmap.put(12, "red apple"); // {12 : "red apple"}
hmap.put(12,"yellow banana"); // {11 : "yellow banana"} 최근 키로 override 된다( 덮어씀 )
```
{% endcode %}

{% code title="✅ value(값) 중복은 가능" %}
```java
hmap.put(9,"yellow banana"); // value 중복은 가능하다
```
{% endcode %}

{% code title="✅키에 대한 값 객체 가져오기 get()" %}
```
System.out.println("키 9에 대한 객체 : " + hmap.get(9));
```
{% endcode %}

{% code title="✅ 키 값으로 삭제하기" %}
```java
hmap.remove(9);
```
{% endcode %}

#### keySet( )

keySet()을 이용해서 키만 따로 set으로 만들고, iterator() 키에 대한 목록을 만들 수 있다.

```java
Iterator<String> keyIter = hmap2.keySet().iterator();

while(keyIter.hasNext()){
    String key= keyIter.next();
    String value = hmap2.get(key);
    System.out.println(key + " = " + value);
}
```

#### values()

저장된 value 객체들만 values()로 Collections으로 만들 수 있다.

```java
Collection<String> values = hmap2.values();
```

{% code title="IteIterator()로 목록 만들어서 처리" %}
```java
Iterator<String> valueIter = values.iterator();
while (valueIter.hasNext()){
    System.out.println(valueIter.next());
}
```
{% endcode %}

{% code title="배열로 만들어서 처리" %}
```java
Object[] valueArr = values.toArray();
for(int i = 0; i < valueArr.length; i++){
    System.out.println(i + " : " + valueArr[i]);
}
```
{% endcode %}

#### entrySet()

Map의 내부클래스인 EntrySet을 이용해서 순회를 할 수 있다.

```java
Set<Map.Entry<String,String>> set =  hmap2.entrySet();
// Entry :  키 객체와 값 객체를 쌍으로 묶은 것
Iterator<Map.Entry<String, String>> entryIter = set.iterator();
while(entryIter.hasNext()){
    Map.Entry<String, String> entry = entryIter.next();
    System.out.println(entry.getKey() + " : " + entry.getValue());
}
```

### 🤔 Properties란?

HashMap을 구현하여 사용 용법이 거의 유사하지만 **key**와 **value** 모두 문자열만 사용할 수 있는 자료구조이다.&#x20;설정 파일의 값을 읽어서 어플리케이션에 적용할 때 사용한다.

{% code title="✅ 선언 및 인스턴스 생성" %}
```java
Properties prop = new Properties();
```
{% endcode %}

{% code title="✅ 데이터 삽입" %}
```java
prop.setProperty("driver", "oracle.jdbc.driver.OracleDriver");
prop.setProperty("url", "jdbc:oracle:this:@127.0.0.1:1521:xe");
prop.setProperty("user", "student");
prop.setProperty("password", "student");
```
{% endcode %}

{% code title="✅ 파일 생성후 property에 저장하기" %}
```java
try{
    prop.store(new FileOutputStream("driver.dat"), "jdbc driver");
    prop.store(new FileWriter("driver.txt"), "jdbc driver");
    prop.storeToXML(new FileOutputStream("driver.xml"), "jdbc driver");

}catch (IOException e){
    throw  new RuntimeException(e);
}
```
{% endcode %}

{% code title="✅ 파일 불러와서 property에 저장하기." %}
```java
Properties prop2 = new Properties();

try {
    prop2.load(new FileInputStream("driver.dat"));
    prop2.load(new FileReader("driver.txt"));
    prop2.loadFromXML(new FileInputStream("driver.xml"));

    prop2.list(System.out);

    System.out.println(prop.getProperty("driver"));
    System.out.println(prop.getProperty("url"));
    System.out.println(prop.getProperty("user"));
    System.out.println(prop.getProperty("password"));
} catch (IOException e) {
    throw new RuntimeException(e);
}
```
{% endcode %}
