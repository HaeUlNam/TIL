### java.lang.Object

- object 클래스는 모든 자바 클래스의 조상 클래스입니다.


### Clone() 메소드

- 해당 인스턴스를 복사하여 새로운 인스턴스를 생성해 반환합니다.
- 하지만 복사할 때 필드 값만 복사하기에 배열이나 인스턴스이면 제대로 복제할 수 없습니다. 복제하려는 class에서 clone() method안에서 배열이나 인스턴스는 따로 
clone을 호출해서 복제해주어야 한다. 그렇지 않으면, 주소값만 복사되어 완전히 복제되는 것이 아니다.

```java

import java.util.ArrayList;

public class DeepShallow implements Cloneable{
    private int a;
    private String aa;
    private ArrayList<String> list;

    public DeepShallow(int a, String aa){
        this.a = a;
        this.aa = aa;
        list = new ArrayList<>();
    }

    public void pushList(String city){
        list.add(city);
    }

    @Override
    protected Object clone(){

        try{
            DeepShallow tmp = (DeepShallow) super.clone(); //shallow copy
            //tmp.list = (ArrayList<String>) this.list.clone(); //deep copy
            return tmp;
        }
        catch(CloneNotSupportedException e){
            e.printStackTrace();
            return null;
        }

    }

    public ArrayList<String> getList() {
        return list;
    }

    public int getA() {
        return a;
    }

    public String getAa() {
        return aa;
    }
}

public class helloworld {
    public static void main(String[] arg) {
        DeepShallow d1 = new DeepShallow(10, "aaaa");
        d1.pushList("seoul");


        System.out.println(d1.getA() + d1.getAa() + d1.getList());

        DeepShallow d2 = (DeepShallow) d1.clone();
        d2.pushList("NewYork");

        System.out.println(d1.getA() + d1.getAa() + d1.getList());
        System.out.println(d2.getA() + d2.getAa() + d2.getList());
    }

}

```

- Shallow Copy: 위 예제를 보면 주석처리 되어 있는 코드를 풀지 않으면, 복제한 object에 Arraylist의 주소값이 넘어가기에 ArrayList에 변경됨에 따라 같이 변경된다.

<img width="253" alt="스크린샷 2020-05-11 오후 4 50 46" src="https://user-images.githubusercontent.com/26040955/81537058-9103fa80-93a7-11ea-9566-fe5699fb525c.png">

- Deep Copy: 주석을 풀게 되면, 주소값을 전달하는 것이 아니라 멤버변수에 새롭게 객체를 생성하기에 변경된다고 해도 d1과 d2은 서로 같이 바뀌지 않는다.

<img width="260" alt="스크린샷 2020-05-11 오후 4 52 59" src="https://user-images.githubusercontent.com/26040955/81537244-e04a2b00-93a7-11ea-8b7e-1bee8652c429.png">


### equals() vs ==
- 기본적으로 둘 다 primitive type은 값을 비교하고, referenced type은 주소값을 비교하게 된다.
  * String의 경우: equals는 안의 내용을 비교하고 ==는 주소값을 비교한다. 따라서, 아래의 경우 false, true순으로 출력이 되게 된다.

```java
String s1 = new String("HELLO");
String s2 = new String("HELLO");
System.out.println(s1 == s2);
System.out.println(s1.equals(s2));
```


### 참고자료
- [TCP School - Object 클래스](http://tcpschool.com/java/java_api_object)
- [Difference between == and .equals() method in Java](https://www.geeksforgeeks.org/difference-equals-method-java/)
