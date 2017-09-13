## ionic Push
### Android FCM 사용 방법
1.  [firebase](https://console.firebase.google.com/)에서 프로젝트 생성


2. 생성 후 `android 앱에 firebase 추가` 버튼 클릭


3. 패키지 이름은 config.xml에 있는 아이디 값과 동일하게


4. `google-services.json` 파일을 `프로젝트/platform/android/` 및 `프로젝트` 에 복사


5. 프로젝트에 `cordova plugin` 설치
```npm
cordova plugin add cordova-plugin-inappbrowser
cordova plugin add cordova-plugin-fcm
cordova plugin add cordova-plugin-velda-devicefeedback
```

6. html에서 token 값 정상적으로 받아오는지 확인
```javascript
document.addEventListener("deviceready", onDeviceReady, false);
function onDeviceReady() {
	alert(FCMPlugin)
	FCMPlugin.getToken(
	  function(token){
		console.log("token :"+ token)
		alert("token : "+ token);  // 토큰 값이 정상적으로 뜨면 성공
	  },
	  function(err){
		console.log('error retrieving token: ' + err);
	  }
	)

  FCMPlugin.onNotification(
	  function(data){
		if(data.wasTapped){
		  alert( JSON.stringify(data) );
		}else{
		  alert( JSON.stringify(data) );
		}
	  },
	  function(msg){
		alert('onNotification callback successfully registered: ' + msg) // 앱이 실행되고 있는 도중 푸시가 오면 실행되는 함수
		console.log('onNotification callback successfully registered: ' + msg);
	  },
	  function(err){
		console.log('Error registering onNotification callback: ' + err);
	  }
	);
}
```

7. [firebase](https://console.firebase.google.com/)에서 notification 메뉴 접속 후 메세지 보내기 클릭


8. 추가한 패키지에서 클릭 후 메세지 보내기


9. 푸시 서버는 추가하겠음
