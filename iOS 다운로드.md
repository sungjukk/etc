##ios ipa 파일 설치 링크 만들기
### 준비물
* dropbox 계정
* provisioning 파일
* app.ipa
### dropbox에 올리는 이유
* iOS는 설치 링크 등록 시 http는 허용하지 않기 때문....
* https만 허용함
### 설치 방법
1. ipa를 dropbox로 옮긴 후 dropbox에서 옮긴 ipa의 주소를 가져온다.
    `ex) https://www.dropbox.com/s/qoogb4qe2qgh9uk/NH_Moduda.ipa?dl=0`
2. 해당 주소를 다운로드 받을 수 있는 주소로 변환
    1. 뒤에 ?dl=0 제거
    2. 기존 주소를 https://dl.dropboxusercontent.com로 변경
    `ex) https://dl.dropboxusercontent.com/s/qoogb4qe2qgh9uk/NH_Moduda.ipa`
3. plist파일 생성(첨부파일)
    1. url 항목에 변경된 url입력
    2. bundle-identifier 입력 (ipa의 bundle Id와 일치해야함)
    3. bundle-version 및 title 입력
4. 생성한 plist파일을 dropbox로 옮긴 후 주소를 가져와서 다운 받을 수 있는 주소로 변환
    ex) https://dl.dropboxusercontent.com/s/0mgxlavme76hgfi/NH_Moduda.plist
5. 다운로드 페이지에 링크 추가
```html
<a href="itms-services://?action=download-manifest&url=https://dl.dropboxusercontent.com/s/0mgxlavme76hgfi/NH_Moduda.plist">다운로드</a>
```
### app.plist
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>items</key>
    <array>
      <dict>
        <key>assets</key>
        <array>
          <dict>
            <key>kind</key>
            <string>software-package</string>
            <key>url</key>
            <string>2번에서 변환된 주소</string>
      </dict>
     </array>   
     <key>metadata</key>
      <dict>
        <key>bundle-identifier</key>
        <string>bundleId 입력</string>
        <key>bundle-version</key>
        <string>앱버전</string>
        <key>kind</key>
        <string>software</string>
        <key>title</key>
        <string></string>
      </dict>
     </dict>
  </array>
</dict>
</plist>
```
