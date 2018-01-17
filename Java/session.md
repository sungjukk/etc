## 세션 중복 로그인 처리
### HttpSessionBindingListener
* 세션에 담기거나 제거될 때 실행되는 이벤트
* `request.getSession().setAttribute("member",obj)` 또는 `request.getSession().invalidate();` 이벤트 처리 시 실행됨
* HttpSessionBindingListener를 implements 해서 사용
* `valueBound` 메소드와 `valueUnbound` 메소드 호출
* `valueBound` : 세션에 담길 때 호출되는 메소드
* `valueUnbound` 세션이 지워질 때 발생되는 메소드
### 중복 로그인
1. 로그인 시 세션이 저장될 때 세션이 있는지 확인
2. 기존에 저장된 세션이 있다면 기존 세션 지워줌
3. 기존 세션 지운 후에 세션 저장
### 소스
* `SessionCheck.java`
```java
public class SessionCheck implements HttpSessionBindingListener {
	
	@Override
	public void valueBound(HttpSessionBindingEvent event) {
		// TODO Auto-generated method stub
		if (LoginPreventor.findByLoginId(event.getName())) {
			LoginPreventor.invalidateByLoginId(event.getName());
		}
		
		LoginPreventor.loginUsers.put(event.getName(), event.getSession());
		
	}

	@Override
	public void valueUnbound(HttpSessionBindingEvent event) {
		// TODO Auto-generated method stub
		LoginPreventor.loginUsers.remove(event.getName(), event.getSession());
	}
	
}
```
* `LoginPreventor.java`
```java
public class LoginPreventor {
	public static ConcurrentHashMap<String, HttpSession> loginUsers = new ConcurrentHashMap<String, HttpSession>();
	
	public static boolean findByLoginId(String loginId) {
		return loginUsers.containsKey(loginId);
	}
	
	public static void invalidateByLoginId(String loginId) {
		Enumeration<String> e = loginUsers.keys();
		
		while (e.hasMoreElements()) {
			String key = (String) e.nextElement();
			if (key.equals(loginId)) {
				loginUsers.get(key).invalidate();
			}
		}
	}
}
```
* `login.do` 로그인 체크 메서드
```java
public void login(HttpServletRequest request, HttpServletResponse response, ModelAndView mav) throws Exception {
  String memberId = "00001";
  // 로그인 로직 구현
  // 로그인 됐다고 가정
  request.getSession().setAttribute("member",memberId);
  SessionCheck listener = new SessionCheck();    // HttpSessionBindingListener를 상속 받은 클래스 호출
  request.getSession().setAttribute(memberId, listener); // 이렇게 해줘야 SessionCheck.valueBound() 메서드 실행 됨
}
```

* `logout.do` 로그아웃 매서드
```java
public void login(HttpServletRequest request, HttpServletResponse response, ModelAndView mav) throws Exception {
  request.getSession.invalidate(); // SessionCheck.valueUnbound() 매서드 실행
}
```
