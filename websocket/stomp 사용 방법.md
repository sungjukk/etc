### STOMP
#### stomp 설정
* pom.xml에서 websocket 추가
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
* `WebSocketConfig.java` 파일 작성
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
