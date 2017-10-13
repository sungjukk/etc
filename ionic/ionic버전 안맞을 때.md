## Ionic node 버전이 맞지 않는 경우
### node 업데이트 후 build 에러
* build 할 때 이런 에러가 나는 경우
```
Error: Missing binding C:\ionicFCM\FCMApp\node_modules\node-sass\vendor\win32-x64-57\binding.node
Node Sass could not find a binding for your current environment: Windows 64-bit with Node.js 8.x

Found bindings for the following environments:
  - Windows 64-bit with Node.js 7.x

```
* 프로젝트에 노드 버전은 7.x인데 내 node는 8.x 이여서 버전이 맞지 않다.
```
npm rebuild node-sass --force
```
* 이 명령어로 `node-sass` 업데이트 후 빌드하면 정상적으로 빌드 된다!
