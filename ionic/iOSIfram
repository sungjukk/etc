## iOS에서 iFrame
### input, textarea에서 focus문제
* input, textarea에서 글 작성 중 다른 곳 터치 후 input창에 글이 안써지는 경우
* iframe안에 페이지에 계속 포커스를 유지하도록 추가
```javascript
$(document).ready(function() {
	$("input").on("keydown", function () {
		window.focus();
		$(this).focus();
	});
	$("textarea").on("keydown", function () {
		window.focus();
		$(this).focus();
	});
});
```
