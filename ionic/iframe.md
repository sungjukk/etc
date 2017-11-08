## iOS에서 iframe 적용 시 width값이 정상적으로 적용되지 않는 경우
### iframe에 속성 적용하면됨
* `scrolling = no`
* `width : 1px`
* `min-width : 100%` 적용
```html
<iframe scrolling="no" style="width:1px; min-width:100%; height:100%"></iframe>
```
