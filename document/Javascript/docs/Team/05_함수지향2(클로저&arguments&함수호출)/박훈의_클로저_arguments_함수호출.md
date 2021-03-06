#함수지향

* **함수지향**
    - 클로저
    - arguments
    - 함수의 호출

##함수지향


###클로저(Closuer)
자바스크립트에서는 함수가 자신을 생성한 함수, 즉 자신을 내포하는 함수의 문맥(context)에 접근할 수 있다. 이것을 클로저라 부른다.
*(참고로 클로저라는 개념은 자바스크립트 이 외에 다른 언어에서도 사용된다.)*
>오늘날 대부분의 언어에서는 변수를 가능한 늦게, 즉 처음 사용하기 바로 전에 선언해서 사용할 것을 권한다. 하지만 자바스크립트에서는 블록 유효범위를 지원하지 않기 때문에 권장하는 방법이 아니라고 한다. 대신에 자바스크립트에서는 함수에서 사용하는 모든 변수를 함수 첫 부분에서 선언하는 것이 더 나은 방법이라고 한다.

###코드 예제 1

```javascript
<script>
	function init() {
	  var name = "Mozilla";
	  function displayName() {
	    alert(name);
	  }
	  displayName();
	}
	init();
</script>
```
>init() 함수는 name 이라는 지역변수를 만들고 displayName() 이라는 함수를 정의한다. displayName() 은 내부함수라고 불리는데 이는 함수 init() 안에 정의되었고 init() 함수 안에서만 사용할 수 있기 때문이다. displayName() 함수는 지역변수를 가지지 않지만 외부에서 정의된 name변수를 사용하고 있다.
코드를 한번 실행해보라. 잘 동작할 것이다. 이 예제는 함수 스코핑(functional scoping) 을 보여주기 위해 소개했다. 자바스크립트에서 중첩된 함수는 그 함수 외부에서 정의된 변수를 사용할 수 있다. 

###코드 예제 2

```javascript
<script>
	function makeFunc() {
	  var name = "Mozilla";
	  function displayName() {
	    alert(name);
	  }
	  return displayName;
	}
	
	var myFunc = makeFunc();
	myFunc();
</script>
```
>이 예제를 실행해 보면 위의 예제 init() 함수와 동일한 결과를 보이는걸 알 수 있다(알람창에 "Mozilla" 문자열이 보일 것이다). 위 예제와 다른 점은 외부함수의 리턴 값이 내부함수 displayName() 라는 것이다. <br>이 코드가 문제없이 실행되는 것은 직관적이지 않다. 일반적으로 함수안에 정의된 지역변수는 함수가 종료되기 전까지만 존재한다. makeFunc() 함수가 종료될 때 이 함수 내부에 정의된 지역변수는 없어지는게 상식적이다. 이 코드가 문제없이 동작하는 걸 보면 다른 일이 일어나고 있는 것 같다!<br>이 퍼즐에 대한 해답은  myFunc 함수가 클로져(closure) 를 갖는다는 것이다. 클로져는 두 개의 것으로 이루어진 특별한 오브젝트이다. 첫 번째는 함수이고 두 번째는 그 함수가 만들어진 환경이다. 그 함수가 만들어진 환경은 함수가 만들어질 때 사용할 수 있었던 변수들로 이루어진다. 이 경우에 myFunc 는 displayName 함수와 "Mozilla" 문자열을 포함하는 클로져이다.

<br>
----

###arguments
현재 실행 중인 함수 및 이 함수를 호출한 함수에 대한 인수를 나타내는 개체입니다. <br>arguments 개체는 명시적으로 만들 수 없습니다. arguments 개체는 함수가 실행을 시작할 때만 사용할 수 있습니다.함수의 arguments 개체는 배열이 아니지만 배열 요소에 액세스하는 방식과 동일하게 각각의 인수에 액세스할 수 있습니다. n 인덱스는 실제로 arguments 개체의 0n 속성 중 하나에 대한 참조입니다.

### 코드 예제

```javascript
<script>
	function ArgTest(a, b)
	{
	   var s = "";
	
	   s += "Expected Arguments: " + ArgTest.length;
	   s += "<br />";
	   s += "Passed Arguments: " + arguments.length;
	   s += "<br />";
	
	   s += "The individual arguments are: "
	   for (n = 0; n < arguments.length; n++)
	   {
	      s += ArgTest.arguments[n];
	      s += " ";
	   }
	
	   document.write(s);
	}
	
	ArgTest(1, 2, "hello", new Date())
	
	// Output:
	// Expected Arguments: 2
	// Passed Arguments: 4
	// The individual arguments are: 1 2 hello Tues Jan 8 08:27:09 PST 20xx
</script>
```

----
###함수의 호출
객체에 속성이 있고 속성안에 함수가 들어있다면 그것을 메소드 라고 한다.<br/>


* **함수 호출 패턴 4가지**
    1. 메소드 호출 패턴
    2. 함수 호출 패턴
    3. 생성자 호출 패턴
    4. apply 호출 패턴
    
#### 1. 메소드 호출 패턴
>함수를 객체의 속성(Property)에 저장하는 경우 이 함수를 메소드라고 부른다. 그리고 객체의 메소드를 호출할 때, this는 메소드를 속성(Property)으로 포함하고 있는 객체에 바인딩 된다. 

####코드 예제

```javascript
<script>
	var myObject = {
	  value : 0,
	  increment: function(inc) {
	    this.valiue += typeof inc === 'number' ? inc : 1;
	  }
	};
	
	myObject.increment();
	console.log(myObject.value); // 1
	
	myObject.increment(2);
	console.log(myObject.valiue); // 3
</script>
```
    
#### 2. 함수 호출 패턴
>함수가 객체의 속성이 아닌 경우에는 함수로서 호출한다. 함수를 이패턴으로 호출할 때 this는 전역객체에 바인딩 된다. _(브라우저에서는 window == this 가 되기 때문에 자바스크립트 함수에서 this를 잘못 사용하면 애러 발생.)_ 

####코드 예제

```javascript
<script>
	function add(a, b) { return a + b; }
	
	var sum = add(3, 4)
</script>
```

    
#### 3. 생성자 호출 패턴
>함수를 new 라는 전치연산자와 함께 호출하는 것을 말한다. 생성자 호출 패턴을 사용하는 경우 호출한 함수의 prototype 속성의 값에 연결되는 (숨겨진) 링크를 갖는 객체가 생성되고, 이 새로운 객체는 this에 바인딩된다. _(이해하기 어렵고 책에서는 해당 패턴은 권장하지 않는다고 나와있다고 합니다.)_

####코드 예제

```javascript
<script>
	var Quo = function(string) {
	  this.status = string;
	};
	
	Quo.prototype.getStatus = function() {
	  return this.status;
	}
	
	var myQuo = new Quo("confused");
	console.log(myQuo.getStatus()); //confused
</script>
```

    
#### 4. apply 호출 패턴 
>자바스크립트의 함수객체(Function)는 apply 메소드를 갖는데 해당 메소드를 사용하는 것을 말한다. 
참고로 자바스크립트는 함수형 객체지향 언어??? 이기 때문에 함수는 메소드를 가질 수 있다. (메소드 정의 1.메소드 호출 패턴 참고)
apply 메소드는 this의 값을 선택할 수 있도록 해주며, 두개의 매개변수를 갖는다. 첫 번째는 this에 바인딩 될 값이며, 두 번째는 매개변수들의 배열이다. 

####코드 예제

```javascript
<script>
	function add(a, b) {
	  this['sum'] = a+b;
	  return this.sum;
	}
	
	var array = [3, 4];
	var context = {};
	add.apply(context , array);
	
	console.log(window.sum) // undefined
	console.log(context.sum) // 7
	
	add(1, 1);
	console.log(window.sum) // 2
</script>
```



##참고

- [딤딤이의 블로그 - http://dimdim.tistory.com/category/Javascript](http://dimdim.tistory.com/category/Javascript)
<br>
- [MDN(클로저) - https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures)
- [MSDN(arguments) - https://msdn.microsoft.com/ko-kr/library/87dw3w1k(v=vs.94).aspx](https://msdn.microsoft.com/ko-kr/library/87dw3w1k(v=vs.94).aspx) 