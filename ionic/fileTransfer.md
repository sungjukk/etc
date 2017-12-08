## fileTransfer
### download
1. 객체 생성
```javascript
var fileTransfer = new FileTransfer();
```
2. `download(url,fileUrl,successFunction,errorFunction)` 매서드 실행
```javascript
var url = 'fileDownUrl';
var saveFilePath = 'cdvfile://localhost/persistent/test.jpg';
fileTransfer.download(encodeURI(url),saveFilePath,function(fileEntry) {
  alert(success);
}, function(err) {
  alert(err);
});
```
### upload
1. 객체 생성
```javascript
var fileTransfer = new FileTransfer();
```
2. `upload(filePath,serverUrl,successFunction,errorFunction,options)` 매서드 실행
```javascript
var filePath = 'filePath';  // 파일이 저장된 경로
var serverUrl = 'serverUrl'; // 서버에 저장할 경로
var options = new FileUploadOptions();
options.chunkedMode = true; // 이건 조금 확인 해봐야 함
options.fileKey = 'fileKey'; // 파일키
options.fileName = fileUrl.substr(fileUrl.lastIndexOf('/') + 1); //저장될 파일 이름
options.mimeType = mimeType; // mimeType 설정
var headers = {'headerParam' : 'headerValue'};
options.headers = headers; // 헤더 설정
fileTransfer.upload(filePath,serverUrl,function(result) {
  alert(success);
}, function (err) {
  alert(err);
}, options);
```
