## Cordova Camera
### Android
* `cordova-plugin-camera` 추가
```
cordova plugin add cordova-plugin-camera
```
* options 설정
```javascript
var options = {
    quality : 75,
    destinationType : Camera.DestinationType.DATA_URL,
    sourceType : Camera.PictureSourceType.CAMERA,
    allowEdit : true,
    encodingType : Camera.EncodingType.JPEG,
    targetWidth : 300,
    targetHeight : 300,
    popoverOptions : CameraPopoverOptions,
    saveToPhotoAlbum : false
}
```
* 카메라 실행
```javascript
navigator.camera.getPicture(function (imgData) {
	sendPhoto(imgData);
}, function (err) {
    alert(err);
  	}, options);
```

### Ios
* `cordova-plugin-camera` 추가
```
cordova plugin add cordova-plugin-camera --variable CAMERA_USAGE_DESCRIPTION="your usage message" --variable PHOTOLIBRARY_USAGE_DESCRIPTION="your usage message"
```

* 나머지는 안드랑 동일


### options
* quality : 품질 설정
* destinationType : 이미지 가져오는 방식???
	* `DATA_URL` : base64 형식
	* `FILE_URI` : 파일 url `content://media/external/images/media/2 for Android`
 	* `NATIVE_URI` : 실제 경로?? 맞나??
* sourceType : 카메라 실행
	* `PHOTOLIBRARY` : 기기에 있는 포토 라이브러리 실행
	* `CAMERA` : 카메라 실행
	* `SAVEDPHOTOALBUM` : 기기의 카메라 앨범만 실행
* encodingType : 인코딩 타입
	* `JPEG`, `PNG` 형식으로 가져올 수 있다.
* saveToPhotoAlbum : 카메라 찍은 후 자동 저장 여부
* 나머지 자세한 옵션은 [여기(npm)](https://www.npmjs.com/package/cordova-plugin-camera#module_Camera.DestinationType) 참고
