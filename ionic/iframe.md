## iOS에서 iframe 적용 시 width값이 정상적으로 적용되지 않는 경우
### iOS iframe
* iOS에서는 iframe 속성 중 width, height가 정상적으로 적용되지 않는다.
* iOS에서 크기를 다시 계산하기 때문에....???(인터넷에서 얼핏 봤음)
### iframe에 속성 적용하면됨
* `scrolling = no`
* `width : 1px`
* `min-width : 100%` 적용
```html
<iframe scrolling="no" style="width:1px; min-width:100%; height:100%"></iframe>
```
### iOS에서 iframe 적용 시 scroll이 생기지 않는 경우
### div안에 iframe를 감싸고 스크롤 생성
* `-webkit-overflow-scrolling = touch`
```html
<div id="wrap">
    <iframe id="inner" src="http://www.apple.com"></iframe>
</div>
```
```css
#wrap {
            width: 320px;
            height: 400px;
            position: relative;
            overflow-x: hidden;
            overflow-y: scroll;
            -webkit-overflow-scrolling: touch;
        }
#inner {
           width: 320px;
           height: 100%;
           /* Android 이중 스크롤 방지 */
           position:absolute; top:0; left:0;
        }
```
