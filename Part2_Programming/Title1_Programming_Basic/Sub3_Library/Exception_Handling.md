
### 개요

- 프로그래밍을 하다보면 수백, 수천만 가지의 이유로 코드에 에러가 발생하기도 한다.
- 단순히 코드 작성 중 실수일 수도 있지만
- 에러 발생 원인이 이것만 있는 것은 아니고
- 예상치 못한 사용자 입력, 서버 응답 이슈 등 에러가 발생하는 원인은 무궁무진하다.

- 그리고 이런 에러는 당연히 내 프로그램이나 웹 사이트를 서비스하는데
- 치명적인 이슈로써 작용을 한다.
- 다행히도 이런 문제를 사전에 방지할 수 있는 방법은 이미 존재하는데
- 예외 처리를 통해서 이를 미리 방지하는 것이 가능하다.

---

#### Exception Handling 예외 처리

- 예외 처리란 오류가 발생 시 해당 오류를 그대로 실행시키지 않고 <br/>
	오류에 대응하는 방법으로 처리하는 프로그래밍 기법이다.
- `JavaScript`에선 `try...catch` 문법을 사용해서 예외 처리를 한다.

``` js
try {
	//code
} catch (err){
	//Error Handling
}
```

- `try...catch`의 동작 알고리즘은 다음과 같다.

```
1. try {} 내부에 작성한 코드 실행
2. Error가 없는 경우, try 내부의 마지막 줄 코드까지 실행, catch 실행 X
3. Error가 있는 경우, try 내부의 코드 실행 중지, catch(err){} 넘어간다.
   여기서 매개변수 err은 에러 발생에 대한 설명이 담긴 Error 객체를 포함하고 있다.
```


``` js
//try...catch Exam

try {
	alert("try block Start");
	
	//IamErr; 정의되지 않은 변수
	
	alert("try block End");

	//코드에 Error가 없는 경우, try {} 코드 마지막 줄까지 실행
	//error가 없었기에 catch(err){} 실행되지 않는다.

	//코드 실행 중 Error 발생하면, try {} 실행 중지
	//catch(err){} 실행된다.
} catch(err){
	alert("에러가 발생했습니다.")
}
```

---

#### `throw`

- 사용자 정의 예외를 발생 시킬 수 있는 키워드
- `throw` 예외를 발생 시킬 때, 객체를 명시할 수 있는데 <br/>
	이러면 `catch` 블록에서 해당 객체의 속성을 참조할 수 있게 된다.

``` js
function UserException(message){
	this.massage = massage;
	this.name = "UserException";
}

function getMonthName(mo){
	mo = mo - 1; //월 숫자와 배열 index와 맞추기 위한 용도
	const Months = [
		"1월",
		"2월",
		"3월",
		"4월",
		"5월",
		"6월",
		"7월",
		"8월",
		"9월",
		"10월",
		"11월",
		"12월"
	];,

	if (Months[mo] !== undefined){
		return Months[mo];
	} else {
		throw new UserException("존재하지 않는 월 입니다.");
	}
}

try {
	var month = 15; //1년 12개월 중 15월은 없기 때문에 예외 발생
	var monthname = getMonthName(month);
} catch(err){
	var monthname = "unknown";
	console.log(err.massage, err.name); //오류 처리기에 예외 객체 전달
}
```

