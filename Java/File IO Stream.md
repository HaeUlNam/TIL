### Java I/O Stream

- 데이터 source나 destination(파일이나 다른 프로그램)에 access해서 읽거나 쓰는 방법
- 데이터가 Program으로 흘러들어가는 파이프라인을 Stream이라고 한다.

### Byte Stream vs Character Stream
- Byte Stream : 8bit, InputStream/OutputStream classes
  * 이미지 나 미디어같은 binary data를 다룰 때 주로 사용
- Character Stream: 16bit unicode, Reader/Writer classes
  * text와 같은 character 데이터를 다룰 경우 사용

### Scanner vs BufferedReader

- 둘 다 Character stream을 이용하고 있으며, 위의 주 stream과는 달리 보조 스트림이라고 생각하면 된다.

```java
Scanner sc = new Scanner(System.in);
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
```

- Scanner의 버퍼 크기는 1024 chars, BufferReader의 버퍼 크기는 8192 chars이다.
  * 따라서, 대용량의 내용을 읽을 때는 BufferReader가 더 좋다.
  
- Scanner는 문자열을 구분하여 분석 가능, BufferReader는 문자열을 단순히 읽고 저장
  * scan.useDelimiter("/")와 같은 함수로 token을 할 수 있다.
  * BufferReader는 추가적으로 StringTokenizer 이용

- Scanner는 동기화가 되지 않고, BufferReader는 동기화가 된다.
  * Java는 보통 multithread를 사용하기에 BufferReader가 더 안전하게 사용 가능하다.

- Scanner는 data를 변환까지 하기에 더 느리고, BufferReader는 단순히 character stream만 읽기에 더 빠르다.


```java
// Initialize Scanner object 
Scanner scan = new Scanner("Anna Mills/Female/18"); 

// initialize the string delimiter 
scan.useDelimiter("/"); 

// Printing the tokenized Strings 
while(scan.hasNext()){ 
  System.out.println(scan.next()); 
} 

// closing the scanner stream 
scan.close();

//출처: https://mygumi.tistory.com/43 [마이구미의 HelloWorld]
```


### 참고자료
- 호주 현직 자바 개발자가 묻고 답하는 영어 기술면접 25
- [Ways to read input from console in Java](https://www.geeksforgeeks.org/ways-to-read-input-from-console-in-java/?ref=lbp)
- [[입출력] Scanner와 BufferedReader의 차이](https://m.blog.naver.com/PostView.nhn?blogId=occidere&logNo=220811824303&proxyReferer=https:%2F%2Fwww.google.com%2F)
- [Understanding Byte Streams and Character Streams in Java](https://www.developer.com/java/data/understanding-byte-streams-and-character-streams-in-java.html)
- [Java I/O 스트림](http://tcpschool.com/java/java_io_stream)
- [Difference between Scanner and BufferReader Class in Java](https://www.tutorialspoint.com/difference-between-scanner-and-bufferreader-class-in-java)
