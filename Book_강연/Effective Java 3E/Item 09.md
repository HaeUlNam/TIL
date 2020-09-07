# try-finally보다는 try-with-resources를 사용하라
- 자바 라이브러리에는 close 메서드를 호출해 직접 닫아줘야 하는 자원이 많다.
  * InputStream, OutputStream, java.sql.Connection

## try-finally
- 전통적으로 자원이 제대로 닫힘을 보장하는 수단으로 try-finally가 쓰였다.
### 단점 1. 자원이 둘 이상이면 try-finally 방식은 너무 지저분하다.
```java
static void copy(String src, String dst) throws IOException {
  InputStream in = new FileInputStream(src);
  try{
     OutputStream out = new FileOutputStream(dst);
     try{
       byte[] buf = new byte[BUFFER_SIZE];
       int n;
       while ((n = in.read(buf)) >= 0)
          out.write(buf, 0, n);
     } finally {
       out.close();
     }
  } finally {
    in.close();
  }
}
```

### 단점 2. try block에서 예외 발생시 close가 제대로 되지 않는다.
- 이런 경우 첫번째 예외 때문에 두번째 예외인 close 예외가 가려지게 되서 실제 시스템에서의 디버깅이 어렵다. (Question) 왜 가려지는 건가?)
- 이렇게 숨겨진 예외들도 그냥 버려지지는 않고, 스택 추적 내역에 '숨겨졌다(suppressed)'는 꼬리표를 달고 출력된다. 또한, 자바 7에서 Throwable에 추가된 getSuppressed 메서드를 이용하면 프로그램 코드에서 
가져올 수도 있다.

## try-with-resources
- 이 구조를 사용하려면 해당 자원이 AutoCloseable 인터페이스를 구현해야 한다. 단순히 void를 반환하는 close 메서드 하나만 덩그러니 정의한 인터페이스이다.
  * 자바 라이브러리와 서드파티 라이브러리들의 수많은 클래스와 인터페이스가 이미 AutoCloseable을 구현하거나 확장해뒀다. 닫아야 하는 자원이 있다면 AutoCloseable을 구현하자.

```java
static String firstLineOfFile(String path) throws IOException {
  try (BufferedReader br = new BufferedReader(
          new FileReader(path)){
          return br.readLine();
  }
}
```

```java
static void copy(String src, String dst) throws IOException {
  try(InputStream in = new FileInputStream(src);
      OutputStream out = new FIleOutputStream(dst)) {
        byte[] buf = new byte[BUFFER_SIZE];
        int n;
        while ((n = in.read(buf)) >= 0)
          out.write(buf, 0, n);
      }
}
```

- try-with-resource와 함께 catch절을 써서 try문을 더 중첩하지 않고도 다수의 예외를 처리할 수 있다.
```java
static String firstLineOfFile(String path) throws IOException {
  try (BufferedReader br = new BufferedReader(
          new FileReader(path)){
          return br.readLine();
  } catch (IOException e) {
    return defaultVal;
  }
}
```
