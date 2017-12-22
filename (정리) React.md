# (정리) React


## 특징

* Facebook 에서 프레임웍 개발

* React의 관심사 = DOM 업데이트 , 이벤트 응답  
-> ajax, 라우팅, 저장소, 데이터 구조 에는 관심이 없음

* 가상 DOM을 이용해서 DOM을 읽지 않고 갱신 함  
* 랜더링 함수가 핵심  
	현재 상태값 -> 가상 표현 객체 -> DOM 에 전달  
	
	현재의 가상표현 객체와 새로운 가상 표현 객체의 차이를 아주 효과적으로 비교하는 알고리즘을 가지고 있음  
	
	입력이나 외부의 변화에의해 상태의 번화가 있다는 사실을 React에게 알려 주기만 하면 됨  
	
* (주의/집중할 부분)  
	** 컴포넌트 라이프 사이클 -> 메모리 누수에 연관  
	** 데이터 흐름 : 컴포넌트 트리에 데이터 전달 , 어떤 데이터를 변경해도 안전한지   
	
	** 속성 (props), 상태(stats)의 명확한 구분  
	
* React의 이벤트 처리는 선언적이다.  
	
---- 

## 문법 TODO	
	
	
	
----

## 라이프 사이클   


### 초기화  

* getDefaultProps  
	: 인스턴스를 생성하는 시점에 딱 한번만 호출  

* getInitialState  
	: 인스턴스를 생성할 때마다 호출  
	: this.props 접근 가능  
	
* componentWillMount  
	: 최초 랜더링 직전에 호출   
	: 컴포넌트의 상태에 영향을 줄 수 있는 마지막 단계  
	
* render  
	: 가상DOM을 생성   
	: 필수 구현 메소드  
	: 제약조건  
		-- 접근할 수 있는 데이터는 this.props , this.stat 뿐이다  
		-- null, false, 어던 React 컴포넌트도 반환할 수 있다.  
		-- 단일 최상위 컴포넌트만 반환할 수 있다. 엘리먼트 배열은 반환할 수 없다.  
		-- 컴포넌트의 상태를 변경한거나 DOM을 수정할 수 없다.  
		
	: 반환된 가상DOM과 실제 DOM의 차이를 확인하여 반영된다.  
	:? -- this.setState 메소드가 호출 될 때 마다 render를 호출
			-> this.state 보다 this.setState메소드를 이용하는게 좋다.
	
		
* componentDidMount  
	: this.getDomNode()를 통해 실제 DOM에 접근 가능  
		:= 0.13 React.findDomNode(component)  
		
	-> 렌더링 결과물의 높이값 확인   
	-> 타이머를 이용한 조작  
	-> jQuery 플러그인 적용  
	-> ...  
	
### 실행시  

* componentWillReceiveProps  
	: 컴포넌트의 props가 바뀌면 componentWillReceiveProps 메소드가 호출됨  
	: 이때 새로운 props나 state 객체를 변경할 수 있음  
		??--> 새로운 componentWillReceiveProps 가 발생하는가?  
		
* shouldComponentUpdate
	: false 를 반환하면 자신이나 자식 컴포넌트를 랜더링 하지 않는다. ( 속도 향상 ) ( React가 render()를 호출하지 않는다. )
	: 렌더링 초기화시 , forceUpdate 사용 이후에는 호출되지 않는다.
	: PureRenderMixin 참고
	
* componentWillUpdate
	: componentWillMount와 비슷

* render  
	
* componentDidUpdate
	: componentDidMount와 비슷

### 분해 정리

* componentWillUnmount
	: 컴포넌트가 제거되기 직전에 호출
	
	
	
----

## 안티패턴?

### render 함수 안의 코드를 보고 state값이, 기반으로 하고 있는 props 값과 동기화 되어 있는지 알 수 있어야 한다. 
	: props에 가져온값을 계산한 결과를 state에 저장하지 않는다.
	: --> render 에서 값을 계산한다.
	: --> initial 시점에는 초기값을 셋팅하는 작업만을 수행한다.

	
----

## 데이터 흐름

### 데이터가 부모 컴포넌트에서 자식 컴포넌트로 흐르는 단방향 데이터 흐름을 지향한다. 

### 최상위 컴포넌트의 속성이 바뀌면 React는 변경사실을 컴포넌트 트리에 전달하고 해당 속성을 사용한 모든 컴포넌트를 다시 렌더링 한다.

### 컴포넌트의 내부 상태값은 컴포넌트 내부에서만 수정할 수 있다.

### 컴포넌트가 자신의 props를 변경해서는 안된다.
	: 컴포넌트 내에서 this.props 혹은 this.setProps를 호출해서 값을 직접 변경하지 않도록 한다.
	
### this.state를 직접 변경해서는 안된다.(?) -> this.setState를 사용한다.


----
## 이벤트 처리

### React는 이벤트 객체를 제공할 때 SyntheticEvent로 한번 랩핑을 해서 반환한다. 
	: 브라우저가 생성한 이벤트와 같은 형태의 작동방식을 제공
	: 크로스 브라우저 이슈에 대응
	: SyntheticEvent의 nativeEvent 프로퍼티를 이용해서 브라우저가 생성한 원래의 이벤트 객체에 접근할 수 있다.
	
----
## 컴포넌트 구성  

### React는 상속보다 구성을 선호한다.  
	:작고 간단한 컴포넌트와 데이터 객체를 조합해서 더 크고 복잡한 컴포넌트를 만드는 방식  
	-> 다른 프레임웍과 달리 상속하는 extendClass 메소드를 제공하지 않는다.  
	

	: 아래에서 위로 올라가면서 컴포넌트를 하나씩 조합.... 왜??  (?? 큰그림부터 그리는게 올바르지 않은가? )  
	
----
## DOM 조작

### 실제 DOM에 접근 
	: render 에서 ref = 유일한키 를 주게 되면 랜더링이 완료된 이후에 실제 DOM에 접근이 가능함
	: this.refs.유일한키.getDOMNode()
	: ES6에서는 getDOMNode() API를 제공하지 않고, 대신 React.findDomNode(component)를 이용해야 한다. 
	
	
	
	





## 참고

	
---- 
## 궁금한것




