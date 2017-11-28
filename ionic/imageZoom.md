## Image zoom
### 이미지를 줌 하는 경우 끊키면서 줌이 되는 경우(android)
* 원인으로는 android에서 이미지를 처리할 때 하드웨어 가속을 하지 실행하기 때문
* css 속성 중 transform으로 하드웨어 가속도 처리 가능
```css
img {
  transform : scale3d(1,1,1);
}
```
