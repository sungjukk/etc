## pushServer
### FCM pushServer
* https://fcm.googleapis.com/fcm/send 에 데이터만 넣어서 보내주면 된다.
* `notification`, `data` 두가지 방식
* `notification`은 백그라운드에서 `onMessageReceived` 매서드 접근이 안된다.
* `data` 방식은 백그라운드에서 접근 가능

#### 코드
```java
public void sendPush() throws Exception {
    String apiKey = "firebase내 서버 키 값";
    URL url = new URL("https://fcm.googleapis.com/fcm/send");
    HttpsURLConnection conn = (HttpsURLConnection) url.openConnection();
    conn.setDoOutput(true);
    conn.setRequestMethod("POST");
    conn.setRequestProperty("Content-Type", "application/json");
    conn.setRequestProperty("Authorization", "key=" + apiKey);
    conn.setDoOutput(true);

    // 전체
    //String input = "{\"notification\" : {\"title\" : \"여기다 제목 넣기 \", \"body\" : \"여기다 내용 넣기\"}, \"to\":\"/topics/ALL\"}";
    // 단일
    //String input = "{\"notification\" : {\"title\" : \" 여기다 제목넣기 \", \"body\" : \"여기다 내용 넣기\"}, \"to\":\"받는 사람 토큰 값"}";
    JSONObject root = new JSONObject();
    JSONObject notification = new JSONObject();
    notification.put("body", "내용");
    notification.put("title", "타이틀");
    root.put(type, notification);
    //root.put("notification", notification);
    root.put("to", token);

    OutputStream os = conn.getOutputStream();
    // 인코딩 UTF-8 처리
    os.write(root.toString().getBytes("UTF-8"));
    os.flush();
    os.close();

    int responseCode = conn.getResponseCode();

    BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
    String inputLine;
    StringBuffer response = new StringBuffer();

    while ((inputLine = in.readLine()) != null) {
        response.append(inputLine);
    }
    in.close();
}
```
