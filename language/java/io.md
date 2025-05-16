---
icon: clock-twelve
---

# IO

## 1️⃣ File

{% code title="✅ 파일 인스턴스 생성" %}
```java
File file= new File("src/main/java/com/ohgiraffers/section01/file/test.txt");
```
{% endcode %}

```
try {
    /* 파일 생성 후 성공 실패 여부를 boolean으로 리턴한다. */
    boolean createSuccess = file.createNewFile();
    System.out.println("createSuccess = "+ createSuccess);
} catch (IOException e) {
    e.printStackTrace();
}
```

`createNewFile()` 메서드는 오류발생시Unhandled exception: java. io. IOException을 반환 하기 때문에, 예외처리를 해주어야 한다. -> 위에서는 try-catch 사용

{% code title="✅파일 클래스 여러 메서드" %}
```java
System.out.println("파일의 크기 : " + file.length() + "byte");
System.out.println("파일의 경로 : "  + file.getPath());
System.out.println("현재 파일의 상위 경로 : " + file.getParent());
System.out.println("파일의 절대 경러 : " + file.getAbsolutePath());
```
{% endcode %}

{% code title="✅ 파일 삭제" %}
```java
boolean deleteSuccess = file.delete();
```
{% endcode %}

## 2️⃣ Stream

### 입출력 스트림 개요

프로그래밍 할 때 많은 종류의 데이터를 다루는데, 데이터는 프로그램 내부에 있을 수도 있지만, 외부의 데이터를 가져와서 사용할 수도 있다. 또한 프로그램에서 생성한 데이터를 외부로 출력할 수 도 있다.

#### 외부데이터란?

프로그램 외부에 존재하는 모든 데이터를 의미.외부 데이터를 대상으로 작업할 때 가장 먼저 해야 할 일은 자바 프로그램과 외부 데이터를 연결하는 것이다.

#### 스트림(Stream)

이처럼 프로그램과 외부 데이터가 연결된 길을 스트림(stream)이라고 한다. 스트림은 단방향이기 때문에 데이터를 읽어오기 위한 길은 입력 스트림, 데이터를 출력하기 위한 길은 출력 스트림이라고 부른다.

### FileInputStream

데이터를 1바이트 단위로 데이터를 읽어오는 입력 스트림

{% code title="✅ 선언 및 초기화" %}
```java
FileInputStream fin = null;
```
{% endcode %}

{% code title="✅ 사용 예시" %}
```java
try {
    /*⭐존재하지 않는 파일 경로로 Stream을 생성하려 할 경우,
    * java.io.FileNotFoundException 런타임 에러가 발생한다.
    */
    fin = new FileInputStream("src/main/java/com/ohgiraffers/section02/stream/testInputStream.txt");

    int value;

    /* read() : 파일에 기록된 값을 순차적으로 읽어오고 더 이상 읽어올 데이터가 없는 경우 -1을 반환 */
    while((value = fin.read()) != -1){
        System.out.println(value);

        System.out.println((char)value);
    }

    System.out.println("파일의 길이 : " + new File("src/main/java/com/ohgiraffers/section02/stream/testInputStream.txt").length());

    /* ⭐ 1 byte씩 읽어와야 하는 경우도 존재하긴 하지만 대부분 경우 굉장히 비효율적이다.
     *  byte 배열을 이용해서 한 번에 데이터를 읽어오는 방법도 제공한다.
     *  파일의 길이 만큼의 byte 배열을 만든다. */

    int fileSize = (int) new File("src/main/java/com/ohgiraffers/section02/stream/testInputStream.txt").length();
    byte[] bar = new byte[fileSize];

    fin.read(bar);

} catch (FileNotFoundException e) {
    e.printStackTrace();
} catch(IOException e){
    e.printStackTrace();
} finally {
    // ⭐fin 인스턴스가 null이 아닌 경우 자원 반납을 해야 한다.
    if(fin != null){
        try {
            fin.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```
{% endcode %}

{% hint style="warning" %}
**자원 반납을 해야하는 경우**

1. 장기간 실행중인 프로그램에서 <mark style="color:red;">스트림을 닫지 않는 경우</mark> 다양한 리소스에서 **누수(leak)**&#xAC00; 발생한다.
2. 뒤에서 배우는 버퍼를 이용하는 경우 마지막에 **flush()**&#xB85C; <mark style="color:red;">버퍼에 있는 데이터를 강제로 전송</mark>해야 한다.\
   만약 _<mark style="color:red;">잔류 데이터가 남은 상황에서 추가로 스트림을 사용한다</mark>_&#xBA74; <mark style="background-color:yellow;">**데드락(deadlock)**</mark>상태가 된다.\
   판단하기 어렵고 의도하지 않는 상황에서도 이런 현상이 발생할 수 있기 때문에 마지막에는 flush()를 무조건 실행해주는 것이 좋다.\
   **close()** 메소드는 <mark style="color:red;background-color:yellow;">자원을 반납하며 flush()를 해 주기</mark> 때문에 close()만 제대로 해줘도 된다.\
   따라서 _<mark style="color:red;">close() 메소드는 외부 자원을 사용하는 경우 반드시 마지막에 호출</mark>_&#xD574;줘야 한다.
{% endhint %}

### FileReader

FileInputStream과 사용하는 방법은 거의 동일하다.\
단, byte 단위가 아닌 <mark style="background-color:yellow;">**character 단위**</mark>로 읽어오는 부분이 차이점이다.&#x20;따라서 _<mark style="color:orange;">글자 단위로 읽어오기 때문에 한글을 정상적으로 읽어올 수 있다.</mark>_

```java
FileReader fr = null;

try {
    fr = new FileReader("src/main/java/com/ohgiraffers/section02/stream/testReader.txt");

    int value;
    while((value = fr.read()) != -1){
        System.out.print((char)value);

    }
} catch (FileNotFoundException e) {{
    throw new RuntimeException(e);
}
}catch (IOException e){
    e.printStackTrace();
}finally {
    if(fr != null){
        try{
            fr.close();
        }catch (IOException e){
            throw new RuntimeException(e);
        }
    }
}
```

### FileOutputStream

프로그램의 <mark style="background-color:yellow;">**데이터를 파일로 내보내가 위한 용도**</mark>의 스트림이다.\
<mark style="background-color:yellow;">**1바이트 단위**</mark>로 데이터를 처리한다.

```java
FileOutputStream fout = null;

try {
    // 💡OutputStream의 경우 대상 파일이 존재하지 않으면 파일을 자동으로 생성해준다.
    fout = new FileOutputStream("src/main/java/com/ohgiraffers/section02/stream/testOutputStream.txt");

    fout.write(97);

    byte[] bar = new byte[] {98,99,10,101,102, 10};
    fout.write(bar);

    fout.write(bar, 1, 3);

} catch (FileNotFoundException e) {
    throw new RuntimeException(e);
}catch (IOException e){
    e.printStackTrace();
}finally {
    if(fout != null){
        try {
            fout.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

### FileWriter

프로그램의 <mark style="background-color:yellow;">**데이터를 파일로 내보내기 위한 용도**</mark>의 스트림이다.\
<mark style="background-color:yellow;">**글자 단위**</mark>로 데이터를 처리한다.

```java
FileWriter fw = null;

try {
    fw = new FileWriter("src/main/java/com/ohgiraffers/section02/stream/testWriter.txt");

    fw.write(97);

    fw.write('A');

    fw.write(new char[] {'a','p','p','l','e'});
    
    fw.write("우리나라 대한민국");

}catch (FileNotFoundException e){
    e.printStackTrace();
}
catch (IOException e) { // FileNotFoundException보다 IOException이 상위여서 나중에 작성!
    throw new RuntimeException(e);
}finally {
    if(fw != null){
        try {
            fw.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

## 3️⃣ FileStream

java.io 패키지의 입출력 스트림은 **기본 스트림**과 **필터 스트림**으로 분류할 수 있다.\
<mark style="background-color:green;">**기본 스트림**</mark>은 <mark style="color:green;">외부 데이터에 직접 연결</mark>되는 스트림이고\
<mark style="background-color:green;">**필터 스트림**</mark>은 외부 데이터에 직접 연결하는 것이 아니라 <mark style="color:green;">기본 스트림에 추가로 사용할 수 있는 스트림</mark>이다.\
<mark style="color:red;">주로 성능을 향상시키는 목적으로 사용</mark>되며 생성자를 보면 구분이 가능하다.\
생성자쪽에 <mark style="background-color:green;">매개변수로 다른 스트림을 이용하는 클래스는</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**필터스트림**</mark>이라고 볼 수 있다.

### 보조 스트림

#### BufferWriter

```java
BufferedWriter bw = null;

try {
    bw = new BufferedWriter(new FileWriter("src/main/java/com/ohgiraffers/section03/filterstream/testBuffered.txt"));

    bw.write("안녕하세요\n");
    bw.write("반갑습니다\n");

} catch (IOException e) {
    throw new RuntimeException(e);
} finally {
    if(bw != null){
        try {
            bw.close();
        }catch(IOException e){
            throw new RuntimeException(e);
        }
    }

}
```

#### BufferReader

버퍼에 미리 읽어온 후 한 줄 단위로 읽어들이는 기능을 제공하며 기본 스트림보다 성능을 개선시킨다.

```java
BufferedReader br = null;

try {
    br = new BufferedReader(new FileReader("src/main/java/com/ohgiraffers/section03/filterstream/testBuffered.txt"));
    String temp;
    while ((temp = br.readLine()) != null){
        System.out.println(temp);
    }


} catch (FileNotFoundException e) {
    throw new RuntimeException(e);
}catch (IOException e){
    throw  new RuntimeException(e);
}finally {
    if(br != null){
        try {
            br.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

### 형변환 보조스트림

기본 스트림이 byte 기반 스트림이고, 보조 스트림이 char 기반 스트림인 경우에 사용한다.

{% hint style="success" %}
**표준 스트림**

자바에서는 콘솔이나 키보드 같은 표준 입출력 장치로부터 데이터를 입출력 하기 위한 스트림을\
표준 스트림 형태로 제공하고 있다. System 클래스의 필드 in, out, err가 대상 데이터에 스트림을 의미한다.\
**System.in(InputStream)** : 콘솔로부터 데이터를 입력받는다.\
**System.out(PrintStream) : 콘솔로 데이터를 출력한다.**\
**System.err(PrintStream)** : 콘솔로 데이터를 출력한다.
{% endhint %}

<pre class="language-java"><code class="lang-java">/* System.in을 InputStreamReader로 변환하여 바이트기반 스트림을 문자 기반 스트림으로 변환 후
*  버퍼를 이용한 보조스트림과 연결해보자.
* */
<strong>BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
</strong>

try {
    System.out.print("문자열 입력 : ");
    String value = br.readLine();

    System.out.println("value = " + value);
} catch (IOException e) {
    throw new RuntimeException(e);
}finally {
    if(br != null){
        try {
            br.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}

BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

try {
    bw.write("java mysql jdbc");
} catch (IOException e) {
    throw new RuntimeException(e);
}finally {
    if(bw != null){
        try {
            bw.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
</code></pre>

### 데이터 입출력 보조 스트림

외부 데이터로부터 읽어오는 데이터를 바이트형, 정수, 문자, 문자열로만 읽어오면&#x20;여러 데이터 타입을 취급하는 경우 별도로 처리를 해주어야 한다.\
데이터 자료형 별로 처리하는 기능을 추가한 보조스트림을 제공하고 있다.

#### DataOutputStream

```java
DataOutputStream dout = null;

try {
    dout = new DataOutputStream(new FileOutputStream("src/main/java/com/ohgiraffers/section03/filterstream/score.txt"));
    
    dout.writeUTF("홍길동"); //String 형을 내보날땨는 writeUTF
    dout.writeInt(95);
    dout.writeChar('A');

} catch (FileNotFoundException e) {
    throw new RuntimeException(e);
}catch (IOException e){
    throw new RuntimeException(e);
}finally {
    if(dout != null){
        try {
            dout.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

#### DataInputStream

```java
DataInputStream din = null;

try {
    din = new DataInputStream(new FileInputStream("src/main/java/com/ohgiraffers/section03/filterstream/score.txt"));

    /* 파일에 기록한 순서대로 읽어들이지 않는 경우 에러 발생함.*/
    while(true){
        System.out.println(din.readUTF() + ", " + din.readInt()  + ", " + din.readChar() );
    }


} catch (FileNotFoundException e) {
    throw new RuntimeException(e);
}catch (EOFException e){
    System.out.println("파일 읽기 완료!");
}
catch (IOException e){
    throw new RuntimeException(e);
}
```

### 객체단위 입출력 보조 스트림

```java
MemberDTO[] outputMembers = {
        new MemberDTO("user01", "pass01", "홍길동", "hong@gmail.com", 25, '남', 1250.7),
        new MemberDTO("user02", "pass02", "유관순", "yoo@gmail.com", 25, '여', 1221.6),
        new MemberDTO("user03", "pass03", "이순신", "lee@gmail.com", 25, '남', 1234.7)};

ObjectOutputStream objOut = null;

try {
    objOut = new ObjectOutputStream
                (new BufferedOutputStream
                        (new FileOutputStream("src/main/java/com/ohgiraffers/section03/filterstream/testObjectStream.txt")));

    for(int i = 0 ; i < outputMembers.length; i++){
        objOut.writeObject(outputMembers[i]);
    }

} catch (IOException e) {
    throw new RuntimeException(e);
}finally {
    if(objOut != null){
        try {
            objOut.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

{% hint style="info" %}
직렬화?

자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부에서도 사용할 수 있도록&#x20;바이트(byte) 형태로 데이터를 변환하는 기술을 말한다.\
반대로 바이트로 변환된 데이터를 다시 객체로변환하는 기술을 역직렬화라고 한다.
{% endhint %}

```java
MemberDTO[] inputMembers = new MemberDTO[3];
ObjectInputStream objIn = null;

try {
    objIn = new ObjectInputStream(new BufferedInputStream(new FileInputStream("src/main/java/com/ohgiraffers/section03/filterstream/testObjectStream.txt")));

    while(true){
        System.out.println(objIn.readObject());
    }


}catch (ClassNotFoundException e){
    e.printStackTrace();
}
catch (EOFException e){
    System.out.println("끝!");
}
catch (IOException e) {
    throw new RuntimeException(e);
}finally {
    if(objIn != null){
        try {
            objIn.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```
