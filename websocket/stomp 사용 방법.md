### STOMP
#### stomp 설정
1. pom.xml에서 websocket 추가
```xml
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-websocket</artifactId>
	<version>${org.springframework-version}</version>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-messaging</artifactId>
	<version>${org.springframework-version}</version>
</dependency>
```
2. `WebSocketConfig.java` 파일 작성
```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig extends AbstractWebSocketMessageBrokerConfigurer {

	@Override
	public void configureMessageBroker(MessageBrokerRegistry config) {
		config.enableSimpleBroker("/topic", "/groupChat");
		config.setApplicationDestinationPrefixes("/app");
		config.setUserDestinationPrefix("/user");
	}

	@Override
	public void registerStompEndpoints(StompEndpointRegistry registry) {
		logger.info("gs-websocket socket");
		registry.addEndpoint("/gs-websocket").setAllowedOrigins("*").withSockJS();
	}

}
```    
* `WebSocketConfig` 클래스는 Message broker에 대한 설정을 한다.
* `AbstractWebSocketMessageBrokerConfigurer` 추상클래스 상속
* `enableSimpleBroker()` 메소드는 해당 api를 구독하고 있는 클라이언트에게 메세지 전달
* `setUserDestinationPrefix()` 메소드는 서버에서 클라이언트로부터 메세지 받을 prefix 설정
* `registerStompEndpoints(StompEndpointRegistry registry)` 메소드는 클라이언트에서 websocket을 연결할 api 설정
* `addEndpoint("/gs-websocket")` 메소드를 통해 여러가지 end point 설정 가능
* 크로스 도메인 시 `setAllowedOrigins('*')` 설정 필수!!!!

3. `WebSocketController.java` 파일 작성
```java
@Controller
public class ChattingController {
	private static final Logger logger = LoggerFactory.getLogger(ChattingController.class);

	private SimpMessagingTemplate simpMessagingTemplate;

	@Autowired
	public ChattingController(SimpMessagingTemplate simpMessagingTemplate) {
		this.simpMessagingTemplate = simpMessagingTemplate;
	}

	@Autowired
	private ChattingService chatService;

	@MessageMapping("/groupChat")
	@SendTo("/groupChat/all")
	public HelloMessage greeting(HelloMessage message) throws Exception {
		return message;
	}

	@MessageMapping("/roomChat")
	public void sendMsg(Message message) {
		String msg = "{\"sendId\" : \"" + message.getId() + "\", \"content\" : \"" + message.getMessage() + "\"}";
		//System.out.println("message : " + message);
		this.simpMessagingTemplate.convertAndSend("/groupChat/room/" + message.getRoomName(), msg);
		//this.simpMessagingTemplate.convertAndSendToUser("asdf", "/groupChat/room/enter", "asdaf");
	}
}
```
* `@MessageMapping("/groupChat")` 어노테이션은 클라이언트에서 받아올 때 주소
* `@SendTo("/groupChat/all")` 어노테이션은 클라이언트로 보내는 주소
* `json` 형태로 리턴
*  `simpMessagingTemplate` 메서드로 특정 유저한테만 보내기도 가능

4. 클라이언트 코드 작성
* websocket을 하려는 페이지에 `sockjs.min.js`, `stomp.min.js` 추가
```html
<script src="/sockjs.min.js"></script>
<script src="/stomp.min.js"></script>
```
* 스크립트에 연결 추가
```javascript
function connect() {
	var socket = new SockJS('/gs-websocket');
	stompClient = Stomp.over(socket);
	stompClient.connect({}, function(frame) { // connect(id,pw,function(), error)
		console.log('Connected: ' + frame);
		stompClient.subscribe('/groupChat/all', function(greeting) { // subscribe(메세지 받는 주소, 함수)
			console.log(JSON.parse(greeting.body)); // body를 JSON형태로 변환
		});
	}, function(msg) {
		alert(msg); // 서버에서 연결이 끊어진 경우 실행되는 함수
	});
}

function send() {
	stompClient.send("/app/roomChat", {}, JSON.stringify({ //send('서버로 보내는 주소', 데이터(json))
		'id' : 'name',
		'message' : 'welcome'
	}));
}
```
