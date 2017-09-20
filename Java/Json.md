## JAVA에서 JSON 사용
### JSONObject
* `pom.xml`에 JSON.simple 추가
```xml
<dependency>
	<groupId>com.googlecode.json-simple</groupId>
	<artifactId>json-simple</artifactId>
	<version>1.1</version>
</dependency>
```

* JSON 생성 및 추가 (엄청 간단...)
```JAVA
JSONObject obj = new JSONObject();
obj.put("name","xxx");
```

* JSON을 String 형태로
```JAVA
String name = obj.get("name");
String text = obj.toString();
```

* JSON 배열
```JAVA
JSONArray arrayObj = new JSONArray();
arrayObj.add("1");
arrayObj.add("2");
```
