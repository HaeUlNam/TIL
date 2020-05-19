### Intent란?

- Intent는 메서징 객체로서 다른 앱 구성 요소로부터 작업을 요청하는데 사용할 수 있습니다.
- Action과 Data라는 두 가지 요소를 가지고 전달하게 된다.
- 기본 3가지 사용 사례
  * Activity 시작: 새 Activity를 시작하려면 Intent를 startActivity로 전달. Activity 완료 후 결과를 수신하려면 startActivityForResult() 호출
  * Service 시작: Intent를 startService()에 전달 또는 bindService()에 전달
  * BroadCast 전달: 브로드캐스트는 모든 앱이 수신할 수 있는 메시지. 보통 시스템에서 다양한 브로드캐스트를 전달하는데, Intent를 sendBroadCast()에 전달하면 다른 앱에 브로드캐스트를 전달할 수 있습니다.

### 명시적 Intent vs 암시적 Intent

- 명시적 Intent: Intent에 클래스 객체나 컴포넌트 이름을 지정하여 호출할 대상을 확실히 알 수 있는 경우에 사용. 주로 Application 내부에서 사용
  * 특정 컴포넌트나 Activity가 명확하게 실행되어야할 경우에 사용
- 암시적 Intent: 특정 구성 요소의 이름을 대지는 않지만, 그 대신 수행할 일반적인 작업을 선언하여 다른 앱의 구성 요소가 이를 처리할 수 있도록 해줍니다.
```java
//Intent.ACTION_VIEW는 URI을 볼 수 있게 해주는데, http를 tracking하게 되면 브라우저를 띄우게 된다.
//따라서 현재 핸드폰에 깔려있는 브라우저 앱들 중에 하나를 띄우는 과정을 거친 후 실행.
//더 많은 Action들은 https://jwandroid.tistory.com/73 참고..
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://www.google.com/"));
startActivity(intent);
```

### Intent를 통한 Activity 실행 과정
![image](https://user-images.githubusercontent.com/26040955/82324318-69024000-9a14-11ea-863d-7d8e8c928559.png)

1. Activity A가 Intent를 생성해서 이를 Android System으로 전달
2. Android System이 모든 앱에서 해당 인텐트와 일치하는 인텐트 필터를 검색합니다.
3. 일치하는 항목을 찾으면 시스템이 해당 액티비티의 oncrate()메서드를 호출하여 이를 Intent에 전달하고 일치하는 액티비티를 시작.
  * 더 디테일한 생성과정은 ActivityManagerService -> Zygote Process -> Fork() -> Activity Thread(Main thread)를 그 위에 올리고 실행해서 component 동작.
 
### Intent Filter

- App의 Manifest 파일에 들어 있는 표현으로 해당 구성 요소가 수신하고자 하는 (암시적) 인텐트의 유형을 나타냅니다.
```xml
<!--아래처럼 하면 명시적 인텐트를 사용해서 Activity를 호출해야 한다.-->
<activity android:name=".DetailActivity"></activity>

<!-- 아래처럼 하면 명시적/암시적 인텐트 모두 사용 가능 -->
<activity android:name=".DetailActivity">
  <intent-filter>
     <action android:name="com.example.ACTION_VIEW"/>
     <category android:name="android.intent.category.DEFAULT"/>
  </intent-filter>
</activity>
```

### Pending Intent
- Intent를 가지고 있는 클래스로 가지고 있는 인텐트를 보류하고 특정 시점에 작업을 요청하도록 하는 특징을 가지고 있다.
- Notification을 통해 인텐트를 실행하도록 하거나 특정 시점에 AlarmManager를 이용하여 인텐트를 실행할 때 사용.
  * 참고: https://lesslate.github.io/android/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%ED%8E%9C%EB%94%A9-%EC%9D%B8%ED%85%90%ED%8A%B8(Pending-Intent)/

### 참고자료
- [Android 개발자 문서- 인텐트 및 인텐트 필터](https://developer.android.com/guide/components/intents-filters?hl=ko#java)
- 깡샘의 안드로이드 프로그래밍
- [XML 주석](http://tcpschool.com/xml/xml_basic_comments)
