## iframe
### iframe에서 동영상 재생 시 전체 화면
* iframe에서 동영상을 재생 하면 전체 화면이 되지 않을 경우
* iframe 속성에서 ` allowfullscreen="true"`,`mozallowfullscreen="true"`,`webkitallowfullscreen="true"` 속성을 추가 시켜준다.
### iframe 안에서 부모창으로 데이터 전송
* `postMessage()`를 이용
* `postMessage(데이터,도메인)` 형식 데이터는 `json`도 지원
* data를 보낼 자식 창??
```javascript
var obj = {
   cameraEvent : event
}
window.parent.postMessage(obj,'*');
```

* data를 받을 부모 창
```javascript
window.addEventListener('message',receiveMessage, true);
function receiveMessage(event){
  alert(event);
}
```
### 부모창 > 자식창으로
* 부모창
```javascript
  var w = document.getElementsByTagName('iframe')[0]; //iframe 엘리먼트 정보 받아옴
  w.contentWindow.postMessage(data,'*');
```
* 자식창
```javascript
window.addEventListener('message',receiveMessage, true);
function receiveMessage(e) {
	alert(e.data);
}
```
