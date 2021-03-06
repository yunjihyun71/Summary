![Object Model](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2229.png)

# BOM

> Browser Object Model

### window 객체

> 모든 객체가 소속된 객체(생략 가능). 창이나 프레임을 의미.

```javascript
window.alert(window.a);
alert(a);
```



### location 객체

> 문서의 주소와 관련된 정보

```javascript
// ex) http://opentutorials.org:80/module/1?id=1#bookmark
location.href; // 현재 문서의 전체 URL
location.protocol; // 프로토콜 -> http
location.host; // 호스트 주소(도메인) -> opentutorials.org
location.port; // 포트번호 -> 80
location.pathname; // 경로 -> /module/1
location.search; // 전달인자 -> ?id=1
location.hash; // 해쉬(페이지 내에서 특정 위치 저장) -> #bookmark
```

##### URL 변경(문서 이동)

```javascript
location.href = "https://www.naver.com";
location = "https://www.naver.com";
```

##### 새로고침

```javascript
location.reload();
```



### navigator 객체

> 브라우저와 관련된 정보

```javascript
navigator.appName; // 브라우저명(크롬, 파이어폭스 등은 Netscape라 나옴)
navigator.appVersion; // 브라우저, 운영체제 환경
navigator.userAgent; // 웹브라우저가 웹서버에 보내는 내용. appVersion과 비슷
navigator.platform; // 브라우저가 동작하고 있는 운영체제
```



### 커뮤니케이션

> 아래는 모두 window 객체 소속이다.

```javascript
// 경고창
alert();

// 확인창
confirm(); // 확인을 누르면 true, 취소를 누르면 false 반환

// 입력창
prompt(); // 확인을 누르면 입력한값 반환
```



### 창 제어

##### 새 창 생성

> window.open([URL], [target], [specs]);

```javascript
window.open("https://www.google.co.kr/", "_blank", "width=200, height=200, resizable=yes");
```

target

- 생략 : 새 탭에서
- _blank : 새 창에서
- _self : 현재 창에서
- _parent : 부모 frame에서
- 특정 name : 그 이름으로 새 탭을 연다. 다시 열어도 그 이름으로 된 탭에서만 열림.

specs : 새 창 모양

##### 페이지 삽입

```javascript
$("선택자").load(url, [data,] [function(response, status, xhr)])
```

data : 서버로 보낼 데이터
function : 콜백 함수
response : 서버로부터 받을 데이터
status : "success", "notmodified", "error", "timeout", or "parsererror") 
xhr : XMLHttpRequest 객체

##### 팝업 차단

> window.open() 함수가 버튼을 클릭 하는 등 사용자에 의해 실행되지 않고, script에 의해 자동 실행되는 경우 팝업 차단이 된다.



# DOM

> Document Object Model

![DOM Tree](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2234.png)

### 제어 대상 찾기

```javascript
document.getElementById(아이디); // 아이디로 객체를 찾아서 반환
document.getElementsByTagName(태그명); // NodeList(유사배열) 반환.
document.getElementsByClassName(클래스명);
// CSS 선택자 문법 사용
document.querySelector(선택자); // 첫 객체 하나만 반환(IE8 이상)
document.querySelectorAll(선택자); // 유사배열로 반환(IE9 이상)
```



### 속성과 프로퍼티

```javascript
// attribute 방식(속성)
target.setAttribute('class', 'important');

// property 방식(프로퍼티)
target.className = 'important';
```

속성과 프로퍼티는 속성의 이름과 값이 다른 경우도 있다.
jQuery는 이를 자동으로 고쳐준다.



### Node 객체

> 모든 DOM 객체는 Node 객체를 상속 받는다.

##### 관계

```javascript
.childNodes // 유사배열로 반환
.firstChild
.lastChild
.nextSibling // 다음 형제 노드
.previousSibling
.contains()
.hasChildNodes()
```

##### 노드의 종류

```
.nodeType // 노드 종류에 대한 번호
.nodeName // 태그명
```

##### 값

```javascript
.nodeValue
.textContent
```

##### 노드 추가/제거

```javascript
.appendChild(elem) // 마지막 자식으로 엘리먼트 추가
.removeChild(elem) // 부모 노드의 자식 중 엘리먼트 삭제
```

##### 텍스트

```javascript
.innerHTML // 노드 안의 텍스트노드 get, set
.outerHTML // 노드를 포함한 텍스트노드 get, set
.innerText // 노드 안의 문자열(HTML코드 제외) get, set
.outerText // 노드를 포함한 문자열(HTML코드 제외) get, set
```



### Element 객체

##### 식별자 

```javascript
.classList
.className
.id
.tagName
```

##### 조회

```javascript
.getElementsByClassName(name)
.getElementsByTagName(name)
.querySelector(선택자)
.querySelectorAll(선택자)
```

##### 속성

```javascript
.getAttribute(name)
.setAttribute(name, value)
.hasAttribute(name)
.removeAttribute(name)
```



### document 객체

> 현재 문서 자체를 의미

##### 노드 생성

```javascript
.createElement(태그명) // 해당 태그의 엘리먼트 노드 추가
.createTextNode(텍스트노드) // 텍스트 노드 추가
```

##### 문서 정보

```javascript
.title
.URL
.referrer
.lastModified
```



### Text 객체

> DOM에서는 줄바꿈이나 공백도 텍스트 노드이다!

##### 값

```javascript
.data // 텍스트 노드 get, set
.nodeValue // 위와 동일
```

##### 조작

```javascript
.appendData()
.deleteData()
.insertData()
.replaceData()
.subStringData()
```

##### 생성

```javascript
document.createTextNode(내용)
```



# 이벤트

### 용어

- 이벤트 : 클릭했을 때, 스크롤했을 때와 같은 사건
- event target : 이벤트가 일어날 객체
- event type : 이벤트의 종류
- event handler : 이벤트가 발생했을 때 동작하는 코드
- 이벤트 객체 : 이벤트 함수의 인자(매개변수)



### 등록 방법

##### inline 

> 태그의 속성으로 이벤트 지정

```html
<button id="target" onclick="alert('Hello')">
```

##### 프로퍼티 리스너

> 해당 객체의 프로퍼티로 이벤트 지정

```javascript
target.onclick = function() {
	alert('Hello');
}
```

##### 이벤트 리스너

> 하나의 이벤트 대상에 복수의 동일 이벤트 타입 리스너 등록 가능
>
> 복수의 엘리먼트에 하나의 리스터 등록 가능
>
> 권장(IE8이하는 attachEvent 사용)

```javascript
target.addEventListener("click", function() {
	alert("Hello");
});
```



### 기본 동작의 취소

> 기본 동작 : a태그의 클릭, form의 submit 클릭, input text의 키보드 입력과 같이 기본적으로 이벤트가 등록되어 있는 것

##### inline 

> 이벤트 핸들러의 리턴값이 false이면 기본 동작 취소

```html
<a href="" onclick="return false">
```

##### 프로퍼티

> 이벤트 핸들러의 리턴값이 false이면 기본 동작 취소

```javascript
target.onclick = function(event) {
	return false;
};
```

##### addEventListener

> event 객체의 preventDefault() 메소드를 실행하면 기본 동작 취소

```javascript
target.addEventListener('click', function(event) {
	event.preventDefault();
	// IE9 이하 버전에서는 event.returnValue = false;
});
```




### 이벤트 종류

##### 마우스

- click
- dblclick
- mousedown
- mouseup
- mousemove
- mouseover
- mouseout
- contextmenu : context 메뉴가 실행될 때(마우스 오른쪽 버튼)

> 마우스 포인터 위치

```javascript
event.clientX
event.clientY
```

> 마우스 키보드 조합

```javascript
event.shiftKey : shift키가 눌러져 있으면 true
event.altKey
event.ctrlKey
```

##### form

- submit : form의 정보를 서버로 전송하는 명령인 submit을 클릭했을 때
- change : form의 컨트롤 값이 변경 되었을 때 - input(text, radio, checkbox), textarea, select 태그
- focus : 포커스가 생겼을 때
- blur : 포커스가 사라졌을 때



# 타이머

```javascript
setInterval(함수, 시간(ms)); // 시간마다 함수 실행 -> Interval 객체 반환
clearInterval(Interval inter); // Interval 중지
setTimeout(함수, 시간(ms)); // 시간이 지난 후 함수 실행
```



# 네트워크

### JSON

> JavaScript Object Notation
>
> JavaScript에서 객체를 만들 때 사용하는 표현식
>
> 사람, 기계 모두 이해하기 쉽고 데이터 용량이 작아서 주로 사용

```javascript
JSON.parse(문자열) // 문자열을 JavaScript 객체로 반환
JSON.stringify(객체) // JavaScript 객체를 문자열로 반환
```



### Ajax

> Asynchronous JavaScript and XML
>
> 웹브라우저와 웹서버가 내부적으로 통신 -> 웹페이지의 리로딩 없이 서비스 사용 가능

##### GET 방식

```javascript
var xhr = new XMLHttpRequest(); // XMLHttpRequest 객체 생성
xhr.open('GET', './time.php'); // 접속. form의 method, action에 해당
xhr.onreadystatechange = function(){
	// .readyState === 4 : 통신 완료 상태
	// .status === 200 : 통신 성공 (404는 페이지를 못찾음)
	if(xhr.readyState === 4 && xhr.status === 200){
		// .responseText : 서버에서 전송한 데이터
		document.querySelector('#time').innerHTML = xhr.responseText;
	}
}
xhr.send(); 
```

##### POST 방식

```
var xhr = new XMLHttpRequest();
xhr.open('POST', './time2.php');
xhr.onreadystatechange = function(){
	document.querySelector('#time').innerHTML = xhr.responseText;
}
// 서버로 전송할 데이터 타입의 형식 지정 -> HTML의 form과 같은 형식으로 전송함
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
// 데이터 형식 만들기
var data = '';
data += 'timezone='+document.getElementById('timezone').value;
data += '&format='+document.getElementById('format').value;
// 전달
xhr.send(data);
```

jQuery를 사용하면 더 쉽게 Ajax 통신을 할 수 있다.(jQuery 문서 참조)



------

##### References

- 생활코딩 : https://opentutorials.org/course/1