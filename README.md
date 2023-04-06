# 플러그인 설치

- Korean Language Pack
- Indent_RainBow
- Auto Rename Tag
- CSS Peek
- HTML to CSS autocompletion
- HTML CSS Support
- Live Server
- ESLint
- Prettier

# Vue란 무엇인가?

## 바닐라 자바스크립과의 차이점

```html
<body>
  <div id="app">
    <button type="button" v-on:click="counter++">Counter: {{counter}}</button>
  </div>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          counter: 0,
        };
      },
    });
    app.mount("#app");
  </script>
</body>
```

- 선언적 렌더링 : Vue는 템플릿 구문{{데이터}}을 활용하여 데이터를 선언적으로 출력(렌더링)할 수 있도록 함
- 반응성 : Vue는 Javascript 상태 변경을 자동으로 추적하고 변경이 발생하면 DOM을 효율적으로 업데이트함.

# Vue 핵심 기능

## 바인딩(v-bind)

```html
<body>
  <div id="app">
    <input type="text" v-bind:placeholder="message" />
  </div>
  <script>
    const Counter = {
      data() {
        return {
          message: "텍스트를 입력해주세요",
        };
      },
    };
    Vue.createApp(Counter).mount("#app");
  </script>
</body>
```

- v-bind 속성은 데이터(상태) 속성에 바인딩할 때 사용하는 특수 속성.
- 바인딩된 DOM의 placeholder 속성은 Vue 인스턴스의 message 속성으로 **최신 상태**를 유지.(반응형 동작)
- 이렇게 v- 접두어가 붙은 속성을 **디렉티브**라고 함.

## 이벤트 핸들링(v-on)

- 사용자가 앱과 상호작용할 수 있게 v-on 디렉티브를 사용하여 Vue 인스턴스의 메소드를 호출하는 이벤트 리스너를 추가 가능.

```html
<p>{{message}}</p>
<button type="button" v-on:click="reverseMessage">reverseMessage</button>
```

```javascript
method: {
    reverseMessage(){
        this.message = this.message.split('').reverse().join('');
    }
}
```

## 양방향 바인딩(v-model)

- Vue는 양식(input, select 등)의 입력과 앱의 상태(data)를 **양방향으로 바인딩하는 v-model 디렉티브**를 제공함.
- 위의 v-bind는 단방향 주의 (vue->html)

```html
<p>{{bindingMessage}}</p>
<input type="text" v-model="bindingMessage" />
```

## 조건문

- 엘리먼트 표시 여부는 v-if 특수 속성(디렉티브)로 제어 가능.

```html
<p v-if="visible">보이나요?</p>
<button type="button" v-on:click="visible = true">visible</button>
```

```javascript
data(){
    return{
        visible: false,
    };
},
```

## 반복문

```html
<ul>
  <li v-for="item in items">{{item}}</li>
</ul>
```

```javascript
data(){
    return {
        items:["사과", "포도", "딸기"]
    };
},
```

# 컴포넌트 이해하기

- 자바스크립트를 재사용 가능하게 분리한 파일을 **모듈**이라고 함
- UI(html, css, js)를 재사용 가능하게 분리한 파일을 **컴포넌트**라고 함.

## 컴포넌트 만드는 순서

- 컴포넌트 정의 -> 컴포넌트 등록(지역등록, 전역등록) -> 컴포넌트 사용

## 컴포넌트 정의 2가지 방법

- 문자열 템플릿
- Single File Component(SFC)

### 문자열 템플릿

```javascript
// BookComponent.js 파일
exprot default{
    data(){
        return {
            subtitle: '도서명'
        }
    },
    template:`
        <!-- HTML -->
        <!-- HTML -->
    `
}
```

### Single File Component(SFC)

- 자바스크립트로 복잡한 프로젝트를 개발한다면 다음과 같은 어려움이 존재.
- 문자열 템플릿은 가독성이 떨어지고 예쁘지 않음.
- .js는 HTML과 JavaScript는 모듈화 할 수 있지만 CSS는 빠져 있음!!
- 이 문제를 해결하기 위해 Vue.js는 Vite같은 빌드 도구를 활용하여 .vue확장자를 가진 Single File Component(SFC)를 사용함.
- SFC는 template, script, style 크게 세가지로 구성되어 있음.

```html
<template></template>
```

# 프로젝트 구성

- 경로 별칭 설정

```javascript
alias: {
      "@": fileURLToPath(new URL("./src", import.meta.url)),
    },
```

## public 디렉토리

- 파비콘과 같은 정적인 리소스 파일

## src/assets

- 빌드도구에 영향을 받는 이미지나 css와 같은 정적인 자산을 놓는 위치

## App.vue

- 루트 컴포넌트.

## main.js

- createApp(Ap p.mount(#app));
- -> 실제 뷰 인스턴스를 생성하는 메서드
- 파라미터로 App.vue가 들어가게 됨 //루트컴포넌트

# 뷰 스타일 가이드

## 4가지.

### 필수 규칙

- 컴포넌트 이름을 사용할 때 합성어 사용
- Prop 정의 시 배열이 아닌 객체로 정의

## eslint

- eslintrc.cjs

```javascript
"rules":{
  "no-console":process.env.NODE_ENV === "production" ? "error" : "off",
  // eslint와 prettier 충돌 피하기
  "prettier/prettier":["error", {
    singleQuote: true,
    semi: true,
    useTabs: true,
    tabWidth: 2,
    trailingComma: 'all',
    printWidth: 80,
    bracketSpacing: true,
    arrowParens: 'avoid'
  }]
}
```

- settings.json에서 설정

```
"eslint.validate": [
  "editor.defaultFormatter"
  ]
```

- 설정(컨트롤쉼표)에서 format on save 꺼야 충돌 안남.

# 옵션 API vs 컴포지션 API 
## 컴포지션 API
- 컴포지션 API는 옵션(data, methods, ...)을 선언하는 대신 가져온 함수(ref, onMounted, ...)을 사용하여 Vue컴포넌트를 작성할 수 있는 API 세트
- 옵션 API는 동일한 논리적 관심사를 같는 코드임에도 불구하고 분산되어(옵션별로작성하기때문) 있음 ! - Mixins방식
- 컴포지션 API는 동일한 논리적 관심사를 그루핑하여 작성할 수 있음
- -> 코드로 추출하여 쉽게 재활용 가능 -> 이러한 코드를 컴포저블 함수(Composable)이라고 함.
## 2가지 제한사항 해결
- 1. hook을 사용하여 관련 코드 조각을 함께 그룹화 함.
- 2. Composables을 사용하면 애플리케이션 전체에서 코드를 매우 쉽게 재사용할 수 있음.

## 컴포지션 API와 옵션 API의 관계
- 컴포지션 API은 대부분의 옵션API을 대체하나
- 필요한 경우 몇가지 옵션API를 사용해야할 수도 있음.
- 함께 사용도 가능.

# 컴포지션 API (Composition API)
- 컴포지션 API는 옵션(data, methos,,,)을 선언하는 대신 가져온 함수 (ref, onMounted, ...)를 사용하여 Vue 컴포넌트를 작성할 수 있는 API 세트.
## 컴포지션 API 크게 3가지 종류
### 반응형 API (Reactivity API)
- 예를 들어 ref(), reactive()와 같은 API를 사용하여 reactive state(반응 상태), computed state(계산된 상태), watcher(감시자)와 같은 것들을 만들 수 있음. 

### 라이프 사이클 훅(Lifecycle Hooks)
- 예를들어 onMounted(), onUnmounted()와 같은 API를 사용하여 프로그래밍 방식으로 컴포넌트 라이프 사이클에 접근 가능.
- 라이프 사이클 특정 시점에 이러한 함수로 코드를 삽입 가능.

### 종속성 주입(Dependency Injection)
- 예를들어 provide()와 inject()는 Reactivity API를 사용하는 동안 Vue의 의존성 주입 시스템을 활용할 수 있게 해줌.

## 반응형 API (Reactivity API)
- 반응형 API는 말 그대로 **반응하는 데이터**와 관련된 API 세트.
- 예를 들어 ref(), isRef()
- 예시
``` javascript
export default{
  const reactiveMessage = ref('Hello Reactive Message'); 
  const addReactiveMessage= () =>{ //실행되면 '!'가 추가됨
    reactiveMessage.value = reactiveMessage.value + '!';
  };

  const nomalMessage = 'Hello Normal Message'; 
  const addNormalMessage= () =>{ // 실행되어도 '!'가 추가 안됨
    nomalMessage.value = nomalMessage.value + '!';
  };
  return{
    reactiveMessage,
    normalMessage,
    addReactiveMessage,
    nomalMessage
  }
}

``` 

## 라이프 사이클 훅(Lifecycle Hooks)
- 라이프 사이클 : Vue 인스턴스나 컴포넌트가 생성될 때, 미리 사전에 정의된 몇 단계의 과정을 거치게 되는데, 이를 라이프사이클이라 합니다.
- 1. 생성(create), 2.부착(mount), 3.업데이트(update), 4.없어짐(destory) 의 과정.


# setup()
- 셋업 함수(hook)
- Composition API 사용을 위한 진입점 역할을 함.
- setup()은 컴포넌트 인스턴스가 생성되기 전에 실행 됨. 
## setup() 기본 사용 방법
- 반응형 API를 사용하여 반응형 상태를 선언하고 setup()에서 객체를 반환하여 <template> 노출할 수 있음.
- 반환된 객체의 속성은 구성 요소 인스턴스에서도 사용할 수 있음 (다른 옵션이 사용되는 경우)

## setup()의 첫번째 매개변수 - props
- setup()의 첫 번째 매개변수는 props. props는 반응형 객체.
- props 객체를 구조 분해 할당을 하면 반응성을 잃게 됨. 따라서 항상 props.xxx 형식으로 props에 액세스하는 것이 좋다.
```
toRef, toRefs
```
- props의 반응성을 유지하면서 구조 분해 할당을 해야한다면 (예: 외부 함수에 prop을 전달해야 하는 경우) toRef(), 및 toRef() 유틸리티 API를 사용하여 이를 수행할 수 있음. 

## setup()의 두번째 매개변수 - context
- setup() 두번째 매개변수는 context(컨텍스트) 객체. 컨텍스트 객체는 setup 함수 내에서 유용하게 사용할 수 있는 속성을 갖고 있음.

# 템플릿 문법
## 텍스트 보간법
- 데이터 바인딩의 가장 기본형태는 {{data}}(이중 중괄호, 콧수염 괄호)를 사용하는 것.
- 이중 중괄호를 사용하면 해당 문법은 컴포넌트 인스턴스의 **message** 값으로 대체 됨.
- 이중 중괄호 안에서 자바스크립트 문법 사용 가능 ! 
- message 속성이 변경될 때마다 갱신(반응)됨.
- v-once 디렉티브를 사용하여 데이터가 변경되어도 갱신(반응)되지 않는 **일회성 보간**을 수행할 수 있음. 
- cf) 디렉티브 : v-... 프리픽스가 붙은 특수한 속성. 엘리먼트나 컴포넌트에게 특정 작업을 지시함. 
- 이중 중괄호는 데이터를 HTML이 아닌 일반 텍스트로 해석. 실제 HTML을 출력하려면 v-html 디렉티브를 사용. (xss 취약점 주의 !)

## 속성 바인딩 (v-bind)
- 이중 중괄호는 HTML 속성에 사용할 수 없음. 대신 **v-bind 디렉티브를 사용.
```
<div v-bind:title="dynamicTitle">마우스를 올려보세요.</div>
```
- Boolean 속성은 속성 존재 자체가 참 또는 거짓을 의미하는 속성
```
<input type="text" v-bind:disabled="isInputDisabled" />
```
- v-bind는 **단축**으로 사용가능 =>':'
- **여러 속성을 객체 하나로 바인딩** 가능 
```vue
<template>
	<div>
		<h2>보간법</h2>
		<p>{{ message }}</p>
		<!--변경 안됨-->
		<p v-once>{{ message }}</p>
		<button v-on:click="message = message + '!'">Click</button>
		<hr />
		<h2>HTML</h2>
		<p>{{ rawHtml }}</p>
		<p v-html="rawHtml"></p>
		<hr />
		<h2>속성 바인딩</h2>
		<div v-bind:title="dynamicTitle">마우스를 올려보세요</div>
		<input type="text" value="홍길동" v-bind:disabled="isInputDisabled" />
		<!--다중속성바인딩-->
		<input v-bind="attrs" />
		<h2>javascript</h2>
		<!--이중중괄호 안에서 자바스크립트 문법 사용 가능!-->
		{{ message.split('').reverse().join('') }}
	</div>
</template>

<script>
import { ref } from 'vue';
export default {
	setup() {
		const message = ref('안녕하세요!');
		const rawHtml = ref('<strong>안녕하세요</strong>');
		const dynamicTitle = ref('안녕하세요!!!!');
		const isInputDisabled = ref(true);
		const attrs = ref({
			type: 'password',
			value: '12345678',
			disabled: false,
		});
		return {
			message,
			rawHtml,
			dynamicTitle,
			isInputDisabled,
			attrs,
		};
	},
};
</script>

<style lang="scss" scoped></style>
```

# 반응형 기초
## 반응형 상태 선언하기
- javascript 객체에서 반응형 상태를 생성하기 위해서는 reactive() 함수를 사용할 수 있습니다.
```javascript
import {reactive} from 'vue'
//반응형 상태
const state = reactive({count: 0 })
```
- 컴포넌트 <template>에서 반응형 객체를 사용하려면 setup()함수에서 선언하고 리턴해야함.
- -> 반환된 상태는 반응형 객체. 반응형 변환은 "깊음"
- -> 컴포넌트의 data()에서 객체를 반환할 때, 이것은 내부적으로 reactive()에 의해 반응형으로 만들어짐.

## reactive()
- 객체나 배열같은 레퍼런스(참조) 타입을 반응형 객체로 만들 수 있음.
``` javascript
<template>
	<div>
		<button v-on:click="increment">Click{{ state.count }}</button>
		<button v-on:click="increment">Deep Click{{ state.deep.count }}</button>
	</div>
</template>

<script>
import { reactive } from 'vue';

export default {
	//옵션s API에서는 반응형 객체를 생성할 때, data 옵션의 객체를 리턴해서 선언했었음. -> 반환된 객체는 내부적으로 reactive()에 감싸져 나온 것
	// data() {
	// 	return {};
	// },
	setup() {
		const state = reactive({
			count: 0,
			deep: {
				count: 0,
			},
		});
		const increment = () => {
			state.count++;
			state.deep.count++;
		};
		return { state, increment };
	},
};
</script>
<style lang="scss" scoped></style>
```

## ref()로 원시값 반응형 데이터 생성하기 
- reactive()는 객체타입만 동작 => ref()원시형 타입을 반응형으로 만들기 (number,string,boolean)
- ref()는 변이가능한(mutable)객체를 반환. 이 객체 안에는 value라는 하나의 속성만 포함.
- value값은 ref()메서드에서 매개변수로 받은 값을 갖고 있음. 이 객체는 내부의 value값에 대한 반응형 참조(reference)역할을 함.
``` vue
import {ref} from 'vue'
const count = ref()
console.log(count.value)
count.value++
console.log(count.value)
```

```vue
<template>
	<div>
		<p>{{ message }}</p>
		<button v-on:click="addMessage">add click</button>
	</div>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
	setup() {
		// 느낌표가 추가되지 않고 있음!!
		//reactive함수는 객체나 배열같이 레퍼런스 타입의 반응형 상태 객체를 선언하는 함수이므로 -> 약속된 속성을 선언하고 그 안에 선언하기 (value속성)
		// let message = reactive('Hello Vue!');
		// const addMessage = () => { <-- 작동 x
		// 	message = message + '!';
		// };
		//let message = reactive({ value: 'Hello Vue!' }); // 템플릿에서{{message.value}}로 받기

		let message = ref('Hello Vue!');
		const addMessage = () => {
			message.value = message.value + '!'; // value 붙여서 사용 !
		};
		return { message, addMessage };
	},
};
</script>

<style lang="scss" scoped></style>
```

## 반응형 객체의 ref 언래핑(Unwarpping)
- ref가 반응형 객체의 속성으로 접근할 때, 자동적으로 내부 값으로 벗겨내서, 일반적인 속성과 마찬가지로 동작. 이때 반응형은 연결되어 있음
```javascript
const count = ref(0)
const state = reactive({count}) //reactive({count:count}) 인 상황 (키와 값이 같으면 단축가능)
count.value++
console.log(count.value)//1
console.log(state.count)//1  <-- state.count.value가 아님 !
```

## 배열 및 컬렉션의 참조 언래핑(Unwarpping)
- 반응형 객체와 달리 ref가 반응형 배열 또는 Map과 같은 기본 컬렉션 타입의 요소로 접근될 때 수행되는 래핑 해제가 없음.
```javascript
const books = reactive([ref('Vue 3 Guide')])
console.log(books[0].value) //value 속성 필요 !
const map = reactive(new Map([['count', ref(0)]]))
console.log(map.get('count').value) //value 속성 필요 !
```

## 반응형 상태 구조분해 할당하기
- 큰 반응형 객체의 몇몇 속성을 사용하길 원할 때, 원하는 속성을 얻기 위해 ES6 구조 분해 할당을 사용하는 것은 매우 일반적.
```javascript
import {reactive} from 'vue'

const book = reactive({
  author: 'Vue Team',
  year: '2020',
  title: 'Vue 3 Guide',
  description: '당신은 이 책을 지금 바로 읽습니다.',
  price: '무료'
});

//let { author, title } = book; // 구조분해할당으로 반응형을 읽게됨
//let { author, title } = toRefs(book); // 반응형 전체 그대로 유지
let { author } = toRef(book, 'author'); // 원하는 속성반 반응형 유지
```
- 하지만 위해서  author, title속성은 **구조분해할당하여 반응형을 잃게됨**
- 이런 경우 반응형 객체를 일련의 ref들로 변환해야함. 이러한 ref들은 소스 객체에 대한 반응형 연결을 유지.
- => toRefs, toRef를 사용하면 반응형 객체의 속성과 동기화가 됨. 그래서 원본 속성을 변경하면 ref객체가 업데이트 되고 그 반대의 경우도 마찬가지입니다.

## readonly를 이용하여 반응형 객체의 변경 방지 
- 반응형 객체에 대해 변화를 막고 싶을 때
- 예를 들어 Provide/Inject로 주입된 반응형 객체를 갖고 있을 때, 우리는 그것이 주입된 곳에서는 해당 객체가 변이되는 걸 막고자 함. 이렇게 하려면 원래 객체에 대한 읽기 전용 프록시를 생성.
``` javascript
import {reactive, readonly} from 'vue'
const original = reactive({count:0})
const copy = readonly(original)
// 원본이 변이되면 복사본에 의존하는 watch도 트리거 될 것임.
original.count++
// 복사본을 변이하려고 하면 경고와 함께 실패
copy.count++ //warning
```

```javascript
const original = reactive({
			count: 0,
		});
		const copy = readonly(original);
		original.count++;
		copy.count++;
		
		console.log(original); // 1
		console.log(copy); // 1 original.count++에만 적용
```

## Reactivity Transform(아직 실험단계)
- ref와 함께 .value를 사용해야 하는 것은 javascript 언의 제약으로 인한 단점. 그러나 compile-time transforms을 사용하면 적절한 위치에 .value를 자동으로 추가하여 인체 공학을 개선할 수 있음.
- Vue는 다음과 같이 이전 "counter" 예제를 작성할 수 있는 compile-time transforms를 제공.
``` javascript
let count = $ref(0);
function increment(){
  // .value 필요 없음
  count++;
}
```

# Computed Properties
- 템플릿 표현식 내 코드가 길어질 경우 가독성이 떨어짐.
- 이럴 때 사용하는 것이 계산된 속성(Computed Properties)
``` javascript 
const hasLecture = computed(()=>{ //일반 함수로 사용 시 렌더링 시마다 다시 계산
  return teacher.lectures.length > 0 ? 'Yes' : 'No' 
})
```
- Computed는 기본적으로 getter 전용. 계산된 속성에 새 값을 할당하려고 하면 런타임 경고가 표시됨.
- 새로운 계산된 속성이 필요한 경우에 getter와 setter을 정의하여 속성을 만들 수 있음.

```javascript
const firstName = ref('홍');
const lastName = ref('길동');
const fullName = coumputed({
  get(){
    return firstName.value + ' ' + lastName.value;
  },
  set(newValue){
    [fistName.value, lastName.value] = newValue.split(' '); //구조분해할당 -> 반응형데이터의 값이 바뀐 것이기 때문에 -> 출력시 바뀐값으로 get()
  }
  fullName.value = '안녕 하세요';
  return {
    firstName, lastName, fullName,
  }
});
```

# 클래스와 Style 바인딩
## HTML 클래스 바인딩
### 객체 바인딩
- 클래스를 동적으로 바인딩하기 위해선 :class(v-bind:class)를 사용할 수 있음.
```vue
<div class="text" :class="active: istActive, 'text-danger': hasError"> </div>
```
- 위 예시처럼 v-bind:class 디렉티브는 일반 class 속성과 공존가능. 객체를 반환하는 computed에 바인딩 가능
```vue
<div class="text" :class="classObject"></div>
const classObject = computed(()=>{
  return {
    active: isActive.value && !hasError.value,
    'text-danger': !isActive.value && hasError.value,
  };
});
```
- 예시
``` vue
<template>
	<div>
		<!-- <div :class="{ active: true, 'text-danger': hasError }">텍스트입니다.</div> -->
		<div :class="classObject">텍스트입니다.</div>
		<!-- 하이픈이 들어간 경우에 ''로 묶어줌 -->
		<button v-on:click="toggle">toggle</button>
		<button v-on:click="hasError = !hasError">toggle</button>
	</div>
</template>

<script>
import { computed, reactive, ref } from 'vue';
export default {
	setup() {
		const isActive = ref(true);
		const hasError = ref(false);
		// const classObject = reactive({  //엑티브되는 상태가 여러개라면 -> computed가 유용
		// 	active: true,
		// 	'text-danger': true,
		// });

		const classObject = computed(() => {
			return {
				active: true && true,
				'text-danger': true && true,
			};
		});

		const toggle = () => {
			isActive.value = !isActive.value;
		};
		return { isActive, hasError, toggle, classObject };
	},
};
</script>
<style lang="scss" scoped></style>
```

## 스타일 바인딩
```vue
<template>
	<div>
		<div :style="styleObject">
			Lorem ipsum, dolor sit amet consectetur adipisicing elit. Numquam,
			voluptates animi recusandae illo officiis quis beatae ad ea doloribus est
			odit incidunt rerum itaque nulla blanditiis aliquam consequuntur saepe
			assumenda.
		</div>
		<button v-on:click="fontSize++">+</button>
		<button v-on:click="fontSize--">-</button>
	</div>
</template>

<script>
import { computed, reactive, ref } from 'vue';
export default {
	setup() {
		// const styleObject = reactive({
		// 	color: 'red',
		// 	fontSize: '13px',
		// });
		const fontSize = ref(13);
		const styleObject = computed(() => {
			return { 
				color: 'red',
				fontSize: fontSize.value + 'px',
			};
		});
		return { styleObject, fontSize };
	},
};
</script>

<style lang="scss" scoped></style>
```


# 조건부 렌더링(v-if, v-show)
## v-if
- v-if 디렉티브는 조건부로 블록을 렌더링할 때 사용. 
- v-else 디렉티브는 v-if가 거짓 일때 렌터링하는 블록
- v-else-if는 v-if에 대한 else if 블록
```
<h1 v-if="visible">Hello Vue3!</h1>
```
## <template v-if="">
- 여러개의 HTML 요소를 v-if 디렉티브로 연결하고 싶다면 <template를 사용>
## v-show
- 스타일의 display 속성을 변경 (v-if는 렌더링 조차 안됨)

## v-if VS v-show
- v-if는 실제로 렌더링 됨. 전환할 때 블록 내부의 컴포넌트들이 제거되고 다시 생성되기 때문.
- 또한 v-if는 게으름. 초기 렌더링 시, 조건이 거짓이면 아무작업도 하지 않음. 조건부 블록은 조건이 처음으로 참이 될때까지 렌더링하지 않음. 
- 이에 비해 v-show는 훨씬 간단. 초기조건과 관계없이 항상 렌더링. 조건에 따라 css display 속성 전환
- 일반적으로 v-if는 전환비용이 높고, v-show는 초기 렌더링 비용이 높음.
- 자주 전환해야한다면 v-show. 런타임 시 조건이 변경되지 않는다면 v-if.

```vue
<template>
	<div>
		<h2 v-if="visible">Hello Vue 3</h2>
		<h2 v-else>fals 입니다!</h2>
		<button v-on:click="visible = !visible">toggle</button>
		<hr />
		<button v-on:click="type = 'A'">A</button>
		<button v-on:click="type = 'B'">B</button>
		<button v-on:click="type = 'C'">C</button>
		<button v-on:click="type = 'D'">D</button>
		<h2 v-if="type === 'A'">A입니다.</h2>
		<h2 v-else-if="type === 'B'">B입니다.</h2>
		<h2 v-else-if="type === 'C'">C입니다.</h2>
		<h2 v-else>A, B, C가 아닙니다.</h2>
		<hr />
		<template v-if="visible">
			<h1>Title</h1>
			<p>Paragrah 1</p>
			<p>Paragrah 2</p>
		</template>
		<hr />
		<h1 v-show="ok">Title 입니다.</h1>
		<button v-on:click="ok = !ok">show toggle</button>
	</div>
</template>

<script>
import { ref } from 'vue';
export default {
	setup() {
		const visible = ref(false);
		const type = ref('A');
		const ok = ref(true);
		return { visible, type, ok };
	},
};
</script>

<style lang="scss" scoped></style>
```

# 목록 렌더링 (v-for)
- v-for 디렉티브를 사용하여 배열인 목록을 렌더링할 수 있음.
- v-for="item in items" 문법을 사용해서 배열에서 항목을 순차적으로 할당합니다.
- v-for="(item, index) in items" 문법을 사용해서 배열 인덱스를 가져올 수 있음.
- 항목을 나열할때, 각 :key 속성에는 고유한 값을 지정해야함. 

``` vue
<template>
	<div>
		<ul>
			<template v-for="(item, index) in items" :key="item.id">
				<!-- computed도 사용 가능 (아래) -->
				<!-- <li v-if="item.id % 2 === 0"> -->
				<li>ID: {{ item.id }}, 인덱스:{{ index }}, {{ item.message }}</li>
			</template>
		</ul>
	</div>
</template>

<script>
import { computed, reactive } from 'vue';
export default {
	setup() {
		const items = reactive([
			{ id: 1, message: 'Java' },
			{ id: 2, message: 'HTML' },
			{ id: 3, message: 'CSS' },
			{ id: 4, message: 'JavaScript' },
		]);

		const eventItems = computed(() => items.filter(item => item.id % 2 === 0));
		return { items, eventItems };
	},
};
</script>

<style lang="scss" scoped></style>
```
## v-for객체
- v-for를 사용하여 객체의 속성을 반복할 수도 있음.
``` vue 
const myObject = reactive({
	title: '제목입니다.',
	author: '홍길동',
	publishedAt: '2016-04-10.',
});

<li v-for="(value, key, index) in myObject" :key="key">
	{{key}} - {{value}}, {{index}}
</li>
```

# 디렉티브(directives)
- 디렉티브(지시)는 v- 접두사가 있는 특수 속성. 
- 기능상에서 중요한 역할인 컴포넌트(또는 DOM요소)에게 "~~하게 작동하라"고 지시를 해주는 지시문임.
- 여러 내장 디렉티브
```
v-text
v-html
v-show
v-fi
v-else
v-else-if
v-for
v-on(@)
v-bind(:)
v-model
v-slot(#)
v-pre
v-once
v-cloak
v-memo
``` 

## v-text
- 엘리먼트의 textContent를 업데이트함. textContent의 일부를 업데이트해야하는 경우 머스태시 보간법을 사용
```vue
<span v-text="msg"></span> <!-- HTML아님 주의-->
<!-- 같은 방법 -->
<span>{{msg}}</span>
```

## v-cloak
- 연결된 컴포넌트 인스턴스가 컴파일을 완료할 때까지만 엘리먼트에 남아 있음.
```html
<style>
	[v-cloak]{
		display:none
	}
</style>
<template>
	<div>
		<p v-cloak>{{message}} </p> // 뷰 컴파일이 완료되기 전까지 {{message}}가 출력되는 것을 v-cloak과 css 설정으로 숨김 !
	</div>
</template>

<script>
import { ref } from 'vue';
export default {
	setup() {
		const message = '안녕하세요'

		return {message};
	},
};
</script>
```

## v-once 
- 엘리먼트와 컴포넌트를 한번만 렌더링함. 이후에 재렌더링 할 때 엘리먼트/컴포넌트 및 모든 하위 엘리먼트는 정적 컨텐츠로 처리되고 건너뜀. 업데이트 성능을 최적화 하는데 사용 가능. 

```vue
<!-- 단일 엘리먼트-->
<span v-once> This will never change: {{msg}}</span>
<!-- 엘리먼트가 자식 엘리먼트를 가진 경우-->
<div v-once>
	<h1> comment</h1>
	<p>{{msg}}</p>
</div>
<!-- 컴포넌트 -->
<my-component v-once :comment="msg"></my-component>
<!-- 'v-for' 디렉티브 -->
<ul>
	<li v-for="i in list" v-once>{{i}}</li>
</ul>
```

## v-memo
```vue
<div v-memo="[valueA, valueB]"></div>
```
- v-memo 디렉티브가 속성으로 배열을 갖을 때 -> 배열 안에 반응형 데이터가 업데이트 됐을때만 렌더링 일어남.
```vue
<template>
	<div>
		<div v-memo="[subscribers]">
			<!--subscribers가 변경되면 그 시점에서 변경되어져왔던 모든 변수도 한번에같이 변함..-->
			<p>subscribers:{{ subscribers }}</p>
			<p>views:{{ views }}</p>
			<p>likes:{{ likes }}</p>
		</div>
		<button @click="subscribers++">Subs++</button>
		<button @click="views++">Views++</button>
		<button @click="likes++">Likes++</button>
	</div>
</template>

<script>
import { ref } from 'vue';
export default {
	setup() {
		const subscribers = ref(4000);
		const views = ref(400);
		const likes = ref(20);
		return { subscribers, views, likes };
	},
};
</script>

<style lang="scss" scoped></style>
```

## 디렉티브 구성
### 디렉티브(directives) 
- v- 접두사가 있는 특수 속성으로 디렉티브의 값이 변경될 때 특정 효과를 반응적으로 DOM에 적용하는 것을 말함.
### 전달인자 (Argument) 
- 일부 디렉티브 디렉티브명 뒤에 콜런으로 표기되는 전달인자를 가질 수 있음 예를들어, v-bind 디렉티브는 반응적으로 HTML 전달인자를 동적으로 삽입할 수 있음.
- 동적 전달인자 : 대괄호를 사용하여 전달인자를 동적으로 삽입할 수 있음. 
- ex) <a v-bind:[attrbuteName]="url"> ... </a>
### 수식어 
- 수식어는 점(.)으로 표시되는 특수 접미사로 디렉티브가 특별한 방식으로 바인딩 되어야함을 나타탬
```
  1     2      3        4  
v-on:submit.prevent="onSubmit"
1. 디렉티브명
2. 전달인자
3. 수식어
4. 값.
```

# 이벤트 처리(v-on(@))
- 이벤트 처리는 v-on 디렉티브로 사용할 수 있음. 그리고 v-on 이벤트는 자주 사용하기 때문에 @ 단축표현으로 많이 사용됨.

## 이벤트 객체 접근
```vue
<template>
	<div>
		<button @click="printEventInfo('Hello Vue3', $event)">
			inline evnet handler
		</button>
		<hr />
		<input type="text" @keyup="onKeyUpHandler" />
	</div>
</template>

<script>
export default {
	setup() {
		const printEventInfo = (message, event) => {
			console.log('message: ', message);
			console.log('event.taget: ', event.target);
			console.log('event.taget.tagName: ', event.target.tagName);
		};
		const onKeyUpHandler = event => {
			console.log('event.key: ', event.key);
		};
		return { printEventInfo, onKeyUpHandler };
	},
};
</script>

<style lang="scss" scoped></style>
```

## 이벤트 수식어
- 이벤트를 조작할 때 이벤트 내부에서 event.prevnetDefault() 또는 event.stopPropagation()메서드를 호출할 수 있음.
- 메소드에서 이러한 메소드의 호출은 어렵지 않지만 **메소드 안에서 비즈니스 외의 이러한 코드는 비효율적**임.
- 이러한 문제를 해결하기 위해서 v-on이벤트에 다양한 이벤트 수식어를 제공함
- 여러개의 수식어 연결 사용 가능  ex) @click.prvent.stop
```
.stop = e.stopPropagation()
.prenvet = e.preventDefautlt()
.capture = 캡쳐모드 사용할 때 이벤트 리스너를 사용 가능
.self = 오로지 자기 자신만 호출할 수 있음. 즉, 타깃 요소가 self일 때 발동
.once = 해당 이벤트는 한 번만 실행 됨.
.passive = 일반적으로 모바일 장치의 성능을 개선하기 위해 터치 이벤트 리스너와 함께 사용됨. ex) @scroll.passive="onScroll"
```

```vue
<template>
	<div>
		<div id="modifiers">
			<!-- 이벤트 캡쳐를 사용하여 해당 엘리먼트 먼저 작동 -->
			<!-- 현재 상황에서는 div -> span -> p 순으로 이벤트 전파!!! -->
			<div @click.capture="clickDiv">
				DIV 영역
				<!-- 이벤트 전파에 의해서 작동 안되고 자기 자신의 이벤트에 의해서만 발동!! -->>
				<p @click.self="clickP">
					P 영역
					<span @click.stop="clickSpan"> SPAN 영역 </span>
					<a href="" @click.prevent.stop="clickA">a 영역</a>
				</p>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	setup() {
		const clickDiv = () => {
			console.log('clickDiv');
		};
		const clickP = () => {
			console.log('clickP');
		};
		const clickSpan = () => {
			console.log('clickSpan');
		};
		const clickA = () => {
			console.log('clickSpan');
		};
		return { clickDiv, clickP, clickSpan, clickA };
	},
};
</script>

<style lang="scss" scoped>
#modifiers div,
#modifiers p,
#modifiers span {
	padding: 40px;
}
#modifiers div {
	background-color: #ccc;
}
#modifiers p {
	background-color: #999;
}
#modifiers span {
	background-color: #666;
	display: block;
}
</style>
```

### 키 수식어
- 키이벤트 수신 수식어
```
.enter
.tab
.delete
.esc
.space
.up
.down
.left
.right
```

## 시스템 키수식어
- 다음수식어를 사용해 해당 수식어 키가 눌러진 경우에만 마우스 또는 키보드 이벤트 리스너를 트리거할 수 있음.
```
.ctrl
.alt
.shift
.meta(맥은커맨드키. 윈도우는윈도우키)
```
```vue
<!-- 알트 + 엔터 -->
<input @keyup.alt.enter="clear"/>
<!-- 컨트롤 + 엔터 -->
<input @keyup.ctrl.enter="send"/>
<!-- 컨트롤 + 클릭 -->
<div @click.ctrl="doSomething">Do sometihg</div>
```

# 양방향 바인딩
- 홈 입력 양식과 반응형 상태를 동기화 할 수 있는 양방향 바인딩
- v-bind(:)는 단방향 바인딩
- v-bind은 입력요소의 상태와 자바스크립트 상태를 동기화 해야하는 경우가 많음
```html
<input :value="text" @input="event => text = event.target.value" />
```
- value를 바인딩 하고, @input이벤트로 자바스크립트 text변수를 변경하는 것은 번거롭다. 

- 위의 단방향 바인딩을 양방향 바인딩으로
```html
<input v-model="text" />
```
## v-model => html요소 별 속성, 이벤트
### input type="text" & textarea
- input type="text" 와 textarea는 value 속성과 input 이벤트를 사용함.

### checkbox & radio
- checkbox & radio 버튼은 checked 속성과 change 이벤트를 사용

### select 
- select 태그는 value 속성과 change 이벤트를 사용.

```vue
<template>
	<div>
		<h2>input Value</h2>
		<!-- 단방향 바인딩 예시 -->
		<!-- <input
			type="text"
			:value="inputValue"
			@input="event => (inputValue = event.target.value)"
		/> -->
		<!-- 양방향 바인딩 -->
		<input type="text" v-model="inputValue" />
		<div>{{ inputValue }}</div>

		<h2>textarea value</h2>
		<textarea v-model="textareaValue"></textarea>
		<div>{{ textareaValue }}</div>

		<h2>checkbox value</h2>
		<label for="checkbox">{{ checkboxValue }}</label>
		<!-- 단방향 바인딩 예시 -->
		<!-- <input
			type="checkbox"
			id="checkbox"
			:checked="checkboxValue"
			@change="event => (checkboxValue = event.target.checked)"
		/> -->
		<!-- 양방향 바인딩 -->
		<input
			type="checkbox"
			id="checkbox"
			v-model="checkboxValue"
			true-value="YES"
			false-value="NO"
		/>

		<h2>checkbox values</h2>
		<label>
			<input type="checkbox" value="html" v-model="checkboxValues" />
			HTML
		</label>
		<label>
			<input type="checkbox" value="CSS" v-model="checkboxValues" />
			CSS
		</label>
		<label>
			<input type="checkbox" value="javascript" v-model="checkboxValues" />
			javascript
		</label>

		<h2>radio value</h2>
		<label>
			<!-- <input
				type="radio"
				name="type"
				value="O"
				:checked="radioValue === 'O'"
				@change="event => (radioValue = event.target.value)"
			/>0형</label -->
			<input type="radio" name="type" value="O" v-model="radioValue" /> O형
		</label>
		<label>
			<!-- <input
				type="radio"
				name="type"
				value="A"
				:checked="radioValue === 'A'"
				@change="event => (radioValue = event.target.value)"
			/>A형</label\> -->
			<input type="radio" name="type" value="A" v-model="radioValue" /> A형
		</label>
		<div>{{ radioValue }}</div>

		<h2>select value</h2>
		<!-- <select
			:value="selectValue"
			@change="
				event => {
					selectValue = event.target.value;
				}
			"
		> -->
		<select v-model="selectValue">
			<option value="html">HTML 수업</option>
			<option value="css">CSS 수업</option>
			<option value="javascript">JavaScript 수업</option>
		</select>
		<div>{{ selectValue }}</div>
	</div>
</template>

<script>
import { ref } from 'vue';
export default {
	setup() {
		const inputValue = ref('');
		const textAreaValue = ref('');
		const checkboxValue = ref('YES');
		const checkboxValues = ref([]); // 초기값 빈배열(체크하면 채워짐)
		const radioValue = ref('O');
		const selectValue = ref('html');
		return {
			inputValue,
			textAreaValue,
			checkboxValue,
			checkboxValues,
			radioValue,
			selectValue,
		};
	},
};
</script>

<style lang="scss" scoped></style>
```


## v-model 수식어(modifiers)
```
.lazy
.number
.trim
```

### .lazy
- 기본적으로, v-model은 각 input 이벤트 후 입력과 데이터를 동기화함.(단, 앞에서 설명한 IME 구성은 제외)
- lazy수식어를 추가하여 change 이벤트 이후에 동기화 할 수 있음.
```vue
<input v-model.lazy = "text"/>
```

### .number
- 사용자 입력이 자동으로 number 타입으로 형변환되기를 원하면, .number 수식어를 추가.
```vue
<input v-mode.number="text"/>
```
### .trim
- 사용자가 입력한 내용에서 자동으로 앞 뒤 공백을 제거하는 트림.
```vue
<input v-model.trim="text"/>
```

# Watch, WatchEffect (반응형 API)
- 반응형 상태가 변경 되었을때 감지하여 다른 작업(api call)을 수행해야하는 경우가 있음.
- Composition API의 watch()를 사용하여 반응형 상태가 변경될 때마다 특정 작업을 수행할 수 있음.
```javascript
const message = ref('Hello World');

// message 데이터 변경에
watch(message, (newValue, oldValue) =>{
	console.log('newValue: , newValue);
	console.log('oldValue: , oldValue);
	// 어떠한 작업을 수행하는 "감시자" 역할.
});
```

## deep option
- **반응형 객체**를 직접 watch()하면 암시적으로 **깊은 감시자**가 생성됨. 
- 즉, 속성 뿐만아니라, 모든 중첩된 속성에도 트리거 됨.
```javascript
const person = reactive({
	name: '홍길동',
	age: 30,
	hobby: '운동',
	obj:{
		count: 0,
	}
});
watch(person, (newValue)=>{
	console.log('newValue: ', newValue);
});
```

```vue
<template>
	<div></div>
</template>

<script>
import { reactive, ref, watch } from 'vue';
export default {
	setup() {
		const x = ref(0);
		const y = ref(0);

		const obj = reactive({
			count: 0,
		});

		//watch()에 첫번쨰 매개변수로 getter함수 정의하여 넣어줌으로써 두수의 합을 감지할 수 있음.
		watch(
			() => x.value + y.value,
			(sum, oldValue) => {
				console.log(sum);
				console.log(oldValue);
			},
		);

		watch([x, y], (newX, newY) => {
			console.log(newX, newY);
		});

		watch(obj, (newValue, oldValue) => {
			console.log('newValue: ', newValue);
			console.log('newValue: ', oldValue); // obj가 변경되어도 같은 참조를하기 때문에 값이 동일함
		});

		// 특정 오브젝트의 속성으로 바로 접근하지 못함(반응형데이터가 아니기 때문에) -> 게터 함수 필요
		watch(obj.count, (newValue, oldValue) => {
			//작동X
			console.log('newValue: ', newValue);
			console.log('newValue: ', oldValue);
		});

		//특정 오브젝트의 속성에 바로접근하기 위해 게터함수 사용
		watch(
			() => obj.count,
			(newValue, oldValue) => {
				console.log('newValue: ', newValue);
				console.log('newValue: ', oldValue);
			},
		);

		// 깊은 감시자 예시
		const person = reactive({
			name: '홍길동',
			age: 30,
			hobby: '운동',
			obj: {
				count: 0,
			},
		});
		watch(person, newValue => {
			console.log('newValue: ', newValue);
		});

		watch(
			() => person.obj, // obj 자체가 변경되면 감지, obj의 값만 변경되면 감지X
			newValue => {
				console.log('newValue: ', newValue);
			},
		);

		return { x, y, obj, person };
	},
};
</script>

<style lang="scss" scoped></style>

```

## immediate 즉시실행
- watch()같은 콜백함수가 최초로 즉시 실행되기 원할 때 
- immediate 옵션을 사용하여 최초으ㅔ 즉시 실행할 수 있음.
```javascript
const message = ref('Hello World!');

const reverseMessage = ref('');
watch(
	message,
	(newValue) => {
		reverseMessage.value=newValue.split('').reverse().join('');
	},
	{
		immediate : true,
	}
);
```

## Computed VS Watch 
- computed와 watch 둘 다 비슷한 역할을 하고 있음.
- computed
```javascript
const reverseMessage = computed(()=>
	message.value.split('').reverse().join('')
);
```
- watch
```javascript
watch(message,
(newValue) => {
	reverseMessage.value = newValue.split('').reverse().join('');
});
```

### Computed vs Watch 사용 방식 차이
#### computed
- Vue의 인스턴스의 상태(ref, reactive변수)의 종속관계를 자동으로 세팅하고자 할 때는 computed로 구현하는 것이 좋음.
- 위의 예시처럼 reverseMessage는 message 값에 따라 결정되어지는 종속관계에 있음. 이 종속관계 코드가 복잡해지면 watch로 구현할 경우 더 복잡해지거나 중복계산 또는 오류를 발생시킬 수 있다.
#### watch
- Vue 인스턴스의 상태(ref, reactive변수)의 변경 시점에 특정 액션(call api, push route등)을 취하고자할 때 적합.
- 대게의 경우 computed로 구현한 것이라면 watch가 아니라 computed로 구현하는 게 대부분 옳다. 

## WatchEffect 
- WatchEffect는 콜백 함수 안의 반응성 데이터의 변화가 감지되면 자동으로 반응하여 실행함
- watch와 다르게 watchEffecsms 최초한번 즉시 실행함.
```javascript
watchEffect(async() => {
	const {data} = await axios.get(`https://reqres.in/api/users?page=${page.value}`);
	items.value = data.data;
});
```

## watch vs watchEffect
- watch와 watchEffect는 둘다 관련 작업(api call, push route 등)을 반응적으로 수행할 수 있게 해줌. 하지만 주요 차이점은 관련된 반응형 데이터를 추적하는 방식.
### watch
- watch는 명시적으로 관찰된 소스만 추적. 콜백 내에서 액세스한 항목은 추적x.  
- 한 콜백 소스가 실제로 변경된 경우에만 트리거됨. 
- watch 종속성 추적을 부작용과 분리하려 콜백이 실행되어야 하는 시기를 보다 정확하게 제어함. 
### watchEffect
- 반면 watchEffect는 종속성 추척과 부작용을 한 단계로 결합.
- 동기 실행 중에 액세스 되는 모든 반응 속성을 자동으로 추적.
- 더 간결한 코드, 그러나 반응성 종속성을 덜 명시적으로 만듬. 
```vue
<template>
	<div>
		<form action="">
			<input v-model.lazy="title" type="text" placeholder="Title" />
			<textarea v-model.lazy="contents" placeholder="Contents"></textarea>
			<button>저장</button>
		</form>
	</div>
</template>

<script>
import { ref, watchEffect } from 'vue';
export default {
	setup() {
		const title = ref('');
		const contents = ref('');

		const save = (title, contents) => {
			console.log(`저장되었습니다. title:${title}, contents:${contents}`);
		};

		watchEffect(() => {
			console.log(title.value);
			console.log(contents.value);
			save(title.value, contents.value);
		});
		return { title, contents };
	},
};
</script>

<style lang="scss" scoped></style>
```


# 컴포넌트 심화
## 컴포넌트 코드 컨벤션
- Vue에서 컴포넌트는 파스칼 케이스를 추천
### 베이스 컴포넌트 이름
- 애플리케이션 고유의 스타일과 규칠을 적용하는 베이스컴포넌트는 모두 같은 측정 접두사로 시작
```
components/
	|-BaseButton.vue
	|-BaseTable.vue
	|-BaseIcon.vue
```
### 싱글 인스턴스 컴포넌트
- 하나의 활성 인스턴스만 갖는 컴포넌트는 하나만 있을 수 있음을 표시하도록 The로 시작
- (페이지당 한 번만 사용 - 단일 페이지에서만 사용된다는 뜻은 아님)
```
components/
	|-TheHeading.vue
	|-TheSidebar.vue
```

## 컴포넌트 등록
- Vue 컴포넌트는 <template>안에서 발견 되었을 때 Vue가 구현위치를 알 수 있도록 "등록"해야함. 컴포넌트 등록 방법은 전역 등록, 지역 등록 두가지가 있음.

### 전역 등록
- 우리는 app.component()메서드를 사용하여 현재 Vue 애플리케이션에서 전역적으로 사용할 수 있도록 할 수 있음.

```javascript
//main.js
import {createApp} from 'vue';
import App from './App.vue';
import GlobaComponent from './components/GlobalComponent.vue';

const app = createApp(App)
app.component('GlobalComponent', GlobalComponent)
app.mount('#app');
```
- app.component()메서드는 다음과 가팅 연결(메서드 체인)될 수 있음.
```javascript
app.component('ComponentA', ComponentA)
	.component('ComponentB', ComponentB)
	.component('ComponentC', ComponentC)
```
- 전역 등록된 컴포넌트는 애플리케이션 어떤 곳에서든 사용 가능.
- 그러나 웹팩과 같은 빌드시스템을 사용하는 경우 컴포넌트를 전역 등록하는 것은 컴포넌트를 사용하지 않더라도 계속해서 최종 빌드에 해당 컴포넌트가 포함되는 것을 의미.
- 전역 등록을 계속하게 되면 애플리케이션의 컴포넌트 간 종속관계를 확인하기 힘듬.

### 지역 등록
- 지역 등록된 컴포넌트는 현재 컴포넌트 영역 안에서만 사용할 수 있음.
- Vue 컴포넌트 인스턴스의 components옵션을 사용해서 등록할 수도있음.
``` javascript
// ParentComponent.vue 파일
import ChildComponent from './ChildComponent.vue'

export default {
	components:{
		ChildComponent
	},
	setup(){
		//...
	}
}
```

# 싱글 파일 컴포넌트
- 싱글 파일 컴포넌트(SFC)의 스펙과 다양한 기능들 
## 언어 블록
### <template>
- 각 *.vue 파일은한 번에 하나의 top-level <template>블록을 포함할 수 있음.
- 콘텐츠는 추출되어 @vue/compiler-dom으로 전달되고, JavaScript 렌더 기능으로 사전 컴파일되고, render 옵션으로 내보내어 컴포넌트에 첨부됨.
### <script>
- 각 *.vue 파일은 한번에 최대 하나의 <script>블록을 포함할 수 있음 (<script setup> 제외)
- 스크립트는 ES 모듈로 실행됨.
- default export는 일반 객체 또는 defineComponent의 반환값으로 Vue 컴포넌트 옵션 객체여야함.
### <script setup>
- 각 *.vue 파일은 한 번에 최대 하나의 <script setup> 블록을 포함할 수 있음.(normal<script>)제외
- <script setup>은 사전에 처리되어 컴포넌트의 setup()함수로 사용됨. 
- 즉, 컴포넌트의 각 인스턴스에 대해 실행됨. 
- <script setup>의 최상위 바인딩은 템플릿에 자동 노출됨.
### <style>
- 단일 *.vue파일에는 여러 <style>태그가 포함될 수 있음.
- <style>태그는 현재 컴포넌트에 스타일을 캡슐화하는데 도움이 되도록 scoped 또는 module 속성을 가질 수 있음. 캡슐화 모드가 다른 여러 <style>태그를 동일한 구성 요소에서 혼합할 수 있음
## 전처리기
- <script>의 lang 속성을 사용하여 전처리기 선언
```vue
<script lang="ts">
</script>
```

## Src 가져오기
- .vue 컴포넌트를 여러 파일로 분할하려는 경우 src 속성을 사용하여 language block 에 대한 외부 파일을 가져올 수 있음.
```javascript
<tempate src="./template.html"></template>
<style src="./style.css"></style>
<script src="./script.js"></script>
```

## CSS 기능
### Scoped CSS
- <style>태그에 scoped속성이 있는 경우 해당 CSS는 현재 컴포넌트의 요소에만 적용됨.
```javascript
<template>
	<p class = "greeting">greeting</p>
</template>
<style scoped>
.greeting{
	color: red;
	font-weight: bold;
}
</style>
```
- 원리는 PostCSS 사용하여 아래와 같이 변환됨
```javascript
<template>
	<p class = "greeting" data-v-7ba5>greeting</p>
</template>
<style scoped>
.greeting[data-v-7ba5]{
	color: red;
	font-weight: bold;
}
</style>
```

## CSS 모듈
- <style module>은 CSS 모듈로 컴파일되고, CSS 클래스를 $style 객체의 속성을 노출함.
- 아래에서 style이 $style이라는 객체가 됨 -> :class로 속성 바인딩 시킴.
```javscript
<template>
	<p :class="$style.red"> This should be red</p>
</template>

<style module>
.red{
	color: red;
}
</style>
```
- 결과 클래스는 충돌을 피하기 위해 해시되어 CSS 범위를 현재 컴포넌트만 지정하는 것과 동일한 효과를 얻음.
### Custom Inject Name
- 모듈 속성에 값을 제공하여 주입된 클래스 객체의 속성 키를 변경할 수 있음.
```
<template>
	<p :class="classes.red"> This should be red</p>
</template>

<style module="classes">
.red{
	color: red;
}
</style>
```

### v-bind() in CSS
- SFC <style> 태그는 v-bind CSS 기능을 사용하여 CSS 값을 동적 구성 요소 상태에 연결하는 것을 지원함.
```vue
<template>
	<div class ="text">hello</div>
</template>

<script>
export default{
	data(){
		return{
			color:'red'
		}
	}
}
</script>

<style>
.text{
	color:v-bind(color);
}
</style>
```

# Props
- 부모 컴포넌트 => (데이터) => 자식 컴포넌트 
- 부모 컴포넌트에서 자식 컴포넌트로 데이터를 보내는 방식을 Props라고 함.
- 자식 컴포넌트에서 props옵션을 선언하고, 부모 컴포넌트에서 props 바인딩하여 채워넣는다 !!!
## Props 컨벤션
- 자식컴포넌트에서 선언할때는 카멜 케이스
- 부모컴포넌트에서 값을 사용할 때는 케밥케이스

## Props 개념
- Props는 컴포넌트에 등록할 수 있는 **사용자 정의 속성**

## Props 선언
- Vue 컴포넌트에는 **명시적으로 props 선언이 필요**함.
- 왜냐하면 컴포넌트에 전달된 외부 props가 fallthrough 속성으로 처리되어야함을 알 수 있음
- cf)fallthrough 속성 : props 또는 emits에 명시적으로 선언되지 않은 속성 또는 이벤트

## props 문자열 배열 선언
- 컴포넌트에 props 옵션을 사용하여 선언할 수 있음.
```javascript
export default{
	props:['title'],
	setup(props){
		console.log(props.title)
	}
}
```


## props 객체 문법 선언
```javascript
export default{
	props:{
		title: String,
		likes: Number
	},
	setup(props){
		console.log(props.title)
		console.log(props.likes)
	}
}
```
- props 선언 시 key는 속성명, value는 속성 타입.
### props 객체 값 객체에서 사용 가능 속성들
- type : 모든 기본 생성자 또는 모든 사용자 정의 타입.
- default : 속성값이 비어있거나 undefined를 전달받은 경우 기본값을 선언할 수 있음. 그리고 type 속성 값이 객체 또는 배열 타입인 경우 기본값을 팩토리 함수를 사용하여 반환. 
- required : 속성이 필수값이라면 true로 해서 설정할 수 있음.
- validator : 속성값의 유효성 검사가 필요할 때 사용할 수 있음.
- 컴포넌트 사용시 type, required, validator에 명시된 사항 위반할때 개발모드에서 콘솔 경고 발생

## Props 사용
- 선언된 props를 <template>에서 바로 사용가능.
```javascript
<template>
	<p>{{title}}</p>
</template>
```

 - setup()함수의 첫번째 매개변수로 props 객체를 받아사용가능.
 ```
 export default{
	 setup(props){
		 return{};
	 },
 };
 ``` 

 - 컴포넌트 인스턴스(this)의 $props객체로 접근 가능 (Options API)

 ## 객체를 사용하여 다중 속성 전달 
 객체의 모든 속성을 props로 전달하려는 경우 v-bind에 전달인자 없이 사용할 수 있음.
 ```vue
// 객체를 사용한 다중 속성 전달 (전달인자 없음)
<BlogPost v-bind="post"/>
<BlogPost :id="post.id" :title="post.title"/>
 ```

 ## **단반향 데이터 흐름**(중요)
- 모든 props는 상위 속성과 -> 하위 속성 간에 단방향 바인딩으로 형성되어 있음.
- 만약 상위 속성이 업데이트되면 -> 하위 속성도 업데이트 되지만 그 반대는 아님.
- 이러한 성질은 하위 속성 변경 실수로 상위 속성을 변경하여 앱의 데이터 흐름을 이해하기 어렵게 만드는 것을 방지.
- 또한 상위 컴포넌트가 업데이트 될 때마다 하위 컴포넌트의 모든 props는 최신 상태도 초기화 됨. 그렇기 때문에 자식 컴포넌트 내부에서 props를 변경하지 않아야함.
```vue
export default{
	props:['title'],
	setup(props){
		// 자식컴포넌트 내부에서 props변경하면 안됨!
		props.title = 'chagned title';
	}
}
```
- 일반적으로 props를 하위 컴포넌트에서 변경하고 싶은 두 가지 경우.
- 
- 1. prop은 초기값을 전달하는데 사용됨. 자식 컴포넌트에서 속성 값을 로컬 데이터 속성으로 사용하고자 할 때. 이 경우 prop을 초기값으로 사용하는 로컬 변수를 선언하는 것이 좋다.
```javascript

```
- 2. 자식 컴포넌트에서 부모 컴포넌트로 이벤트를 올려서 변경... setup() 두번째 파라미터 context.emit() 사용


## 객체 / 배열 Props 업데이트
- 객체나 배열 같은 레퍼런스(참조)타입을 속성으로 전달 시 주의사항
- 자식Comp에서 Props변경 하면 안되나, 자바스크립트 속성상 레퍼런스 타입의 속성은 변경할 수 있다.


## Boolean Casting
- Boolean 타입의 Props는 특별한 캐스팅 규칙이 있음.
```javascript
<!-- 자식 컴포넌트에서 Props 선언 -->
export default{
	props:{
		disabled: Boolean
	}
}
```

```vue
<!-- 부모 컴포넌트 --> 
<!-- :disabled="true" 전달하는 것과 동일. -->
<MyComponent disabled />
<!-- :disabled="false" 전달하는 것과 동일. -->
<MyComponent />
```


## props 예시
- 자식 컴포넌트에서 props옵션을 선언하고, 부모 컴포넌트에서 props 바인딩하여 채워넣는다 !!!
- 자식 컴포넌트 AppCard.vue
```vue
<template>
	<div class="card">
		<div class="card-body">
			<!-- type: new, notice -->
			<span class="badge bg-secondary">{{ typeName }}</span>
			<h5 class="card-title red mt-2">{{ title }}</h5>
			<p class="card-text">
				{{ contents }}
			</p>
			<!-- props->setup에서 computed로 처리하여 한줄로 변경 가능 -->
			<!-- <a v-if="isLike" href="#" class="btn btn-danger">좋아요</a>
			<a v-else href="#" class="btn btn-outline-danger">좋아요</a> -->
			<a href="#" class="btn" :class="isLikeClass">좋아요</a>
			<br />
			<!-- 부모에서 받음-->
			{{ obj }}
		</div>
	</div>
</template>

<script>
import { computed } from 'vue';
export default {
	props: {
		type: {
			type: String,
			default: 'news',
			validator: value => {
				//유효성 검사 !
				return ['news', 'notice'].includes(value);
			},
		},
		title: {
			type: String,
			required: true,
		},
		contents: {
			type: String,
			required: true,
		},
		isLike: {
			type: Boolean,
			default: false,
		},
		obj: {
			type: Object,
			default: () => ({}),
		},
	},
	emits: ['toggleLike'],
	setup(props, context) {
		console.log('props.title: ', props.title);
		const isLikeClass = computed(() =>
			props.isLike ? 'btn-danger' : 'btn-outline-danger',
		);
		const typeName = computed(() =>
			props.type === 'news' ? '뉴스' : '공지사항',
		);
		const toggleLike = () => {
			//props.isLike = !pros.isLike; 자식컴포넌트에서 props 변경불가
			// 이벤트를 부모 컴포넌트로 올리기
			context.emit('toggleLike');

			//자바스크립트 특성상 obj속성 변경 가능
			props.obj.title = '김길동'; // 가능하지만 사용하면 안됨 (부모컴포넌트 속성은 이벤트를 올려서 수정해야함 !)
		};
		return { isLikeClass, typeName, toggleLike };
	},
};
</script>

<styles></styles>
```

- 부모 컴포넌트 TheView.vue
```vue
<template>
	<main>
		<div class="container py-4">
			<div class="row g-3">
				<div v-for="post in posts" :key="post.id" class="col col-4">
					<AppCard
						:title="post.title"
						:contents="post.contents"
						:type="post.type"
						:is-like="post.isLike"
						@toggle-like="post.isLike = !post.isLike"
						:obj="obj"
					></AppCard>
					<!-- 자식컴포넌트에서 context.emit()으로 보낸 이벤트 받기-->
				</div>
			</div>
		</div>
	</main>
</template>

<script>
import AppCard from '@/components/AppCard.vue';
import { reactive } from 'vue';
export default {
	components: {
		AppCard,
	},
	setup() {
		const post = reactive({
			title: '제목2',
			contents: '내용2',
		});
		const posts = reactive([
			{ id: 1, title: '제목1', contents: '내용1', isLike: true, type: 'news' },
			{ id: 2, title: '제목2', contents: '내용2', isLike: true, type: 'news' },
			{ id: 3, title: '제목3', contents: '내용3', isLike: true, type: 'news' },
			{
				id: 4,
				title: '제목4',
				contents: '내용4',
				isLike: false,
				type: 'notice',
			},
			{
				id: 5,
				title: '제목5',
				contents: '내용5',
				isLike: false,
				type: 'notice',
			},
		]);
		// 단방향 바인딩 꺠는 예시.
		const obj = reactive({
			title: '제목2',
			contents: '내용2',
		});

		return { post, posts, obj };
	},
};
</script>

<style lang="scss" scoped></style>

```
# Events
- 자식 컴포넌트에서 부모 컴포넌트로 데이터를 전달 또는 트리거의 목적으로 이벤트를 내보내는 것을 말함. 
- 이벤트는 컴포넌트의 emit 메서드를 통하여 발생시킬 수 있음.
- 부모 컴포넌트 <= 데이터 전달 또는 트리거 <= 자식 컴포넌트

## 이벤트 주의사항
- **이벤트는 선언하는 것이 좋음**
- 컴포넌트의 문서화를 더 잘하기 위해서. 
- NonProps(fallthrough속성)에서 제외하기 위해서
- -> 선언을 하지 않으면 우리가 추가한 이벤트가 NonProps 속성에 추가 됨.
- 자식 컴포넌트 MyButton.vue
```vue
<template>
	<div class="p-3 bg-danger">
		<button class="btn btn-primary" type="button" @click="handler">
			My Buttons
		</button>
	</div>
</template>

<script>
export default {
	setup(props, { emit }) {
		// 이벤트 emit 옵션으로 선언하지 않은 상태
		// NonProps 속성상 정의되지 않은 Prop이나 이벤트는 루트엘리먼트에 상속됨
		const handler = () => {
			emit('SayHello');
		};
		return { handler };
	},
};
</script>

<style lang="scss" scoped></style>
```
- 부모 컴포넌트 MyButtonParent.vue
``` vue
<template>
	<div>
		<!-- 자식 컴포넌트에서 emit 객체로 SayHello이벤트를 등록해두지 않았기 떄문에. emit()으로 받은 이벤트가 다시 자식으로 상속됨!!! -->
		<MyButton @say-hello="sayHello"></MyButton>
	</div>
</template>

<script>
import MyButton from '@/components/MyButton.vue';
export default {
	components: { MyButton },
	setup() {
		const sayHello = () => {
			alert('say hello !');
		};
		return { sayHello };
	},
};
</script>

<style lang="scss" scoped></style>
```

## 이벤트 발생 및 수신
- 컴포넌트의 <template> 블록 안에서 내장 함수 $emit()을 사용하여 직접 커스텀한 이벤트를 내보낼 수 있음.
- 또는 setup()의 두번째 파라미터인 context객체의 emit() 사용가능.
```vue
<template>
	<button @click="$emit('someEvent')">버튼</button>
</template>
```
- 그러면 부모 컴포넌트에서 v-on(또는 @)을 사용하여 이벤트를 수신할 수 있음.
<MyComponent @some-event="callFunction">
- .once 수식어는 컴포넌트 커스텀 이벤트에서도 지원됨
```vue
<MyComponent @some-event.once="callFunction"/>
```

## 이벤트 선언하기 
- Vue3에서는 emits 옵션을 사용하여 이벤트를 선언할 수 있음.
- 2가지 선언 방법 : 1. 문자열 배열 선언, 2. 객체 문법 선언

### 객체 문법으로 선언 이벤트
- 객체 문법으로 선언할 경우 validation 로직을 추가할 수 있음.
- 만약 validation이 없다면 null로 설정.

```javascript
export default{
	emits:{
		//유효성 검사가 없는 이벤트 선언
		someEvent: null,
		// 유혀성 검사가 있는 이벤트 선언
		someSubmit:(result) =>{
			if(email && password){
				return true
			}else{
				console.warn('result 값이 비어 있습니다!')
				return false
			}
		}
	},
	setup(props, context){
		context.emit('someEvent', 'Hello World!')
	}
}
```

## 사용자 정의 v-model 만들기
- 컴포넌트를 만든 후 해당 컴포넌트에 사용자 정의 v-model을 적용하려면 @update:modelValue 이벤트를 사용하여 v-model을 만들 수 있음.
- 자식컴포넌트 LabelInput.vue
```vue
<template>
	<label>
		{{ label }}
		<intput
			:value="modelValue"
			@input="event => $emit('update:modelValue', event.target.value)"
			type="text"
		/>
	</label>
</template>

<script>
export default {
	props: ['modelValue', 'label'], // props, emit 생성하여 부모컴포넌트에서 사용자 정의 v-model 사용 가능해짐
	emit: ['update:modelValue'],
	setup() {
		return {};
	},
};
</script>

<style lang="scss" scoped></style>
```
- 부모 컴포넌트 TheView.vue
```vue
<template>
<!-- <LabelInput :model-value="username" @update:model-value="value=>(username=value)"></LabelInput>-->
	<LabelInput v-model="username" label="이름"></LabelInput>
</template>
<script>
import LabelInput from '@/components/LabelInput.vue';
import { reactive, ref } from 'vue';
export default {
	components: {
		LabelInput,
	},
	setup() {
		const username = ref('');
		return { username };
	}
}

</script>
```

## Computed 이용하기
- 컴포넌트 안에서 computed를 사용하여 v-model을 구현할 수 있음. 
- computed는 읽기 전용이지만, getter,setter 정의하면 쓰기도 가능한 점을 이용 !
```vue
<template>
	<label>
		{{ label }}
		<!-- <intput
			:value="modelValue"
			@input="event => $emit('update:modelValue', event.target.value)"
			type="text"
		/> -->
		<input v-model="value" type="text" />
	</label>
</template>

<script>
import { computed } from 'vue';
export default {
	props: ['modelValue', 'label'], // props, emit 생성하여 부모컴포넌트에서 사용자 정의 v-model 사용 가능해짐
	emit: ['update:modelValue'],
	setup(props, { emit }) {
		const value = computed({
			get() {
				return props.modelValue;
			},
			set(value) {
				emit('update:modelValue', value);
			},
		});
		return { value };
	},
};
</script>

<style lang="scss" scoped></style>
```

## v-model 전달인자
- 기본적으로 v-model은 컴포넌트에서 modelValue props와 update:modelValue 이벤트로 사용. 하지만 전달인자(Arguments)를 사용하여 이러한 이름을 수정할 수 있음.
```javascript
//부모컴포넌트
<!--<BookComponent v-model="bookTitle"> 기존 코드-->
<BookComponent v-model:title="bookTitle">
```

- 이 경우 자식 컴포넌트에서는 :title을 속성으로 정의하고 update:title로 이벤트를 내보내야함.

```vue
<template>
	<article>
		<strong>책 이름</strong>:
		<input
		type="text"
		:value="title"
		@input="$emit('update:title', $event.target.value)"
		/>
	</article>
</template>
<script>
export default{
	props: ['title'],
	emits:['update:title'],
};
</script>
```

## 다중 v-model 바인딩
- v-model 전달인자를 사용하여 컴포넌트에 여러 v-model을 바인딩할 수 있음

```javascript
<BookComponent
	v-model:title="bookTitle"
	v-model:author="bookAuthor"
/>
```

```vue
<template>
	<article>
		<strong>책 이름</strong>:
		<input
		type="text"
		:value="title"
		@input="$emit('update:title', $event.target.value)"
		/>
		<br/>
		<!-- 다른 표현 방식 -->
		<strong>저자</strong>:
		<input
		type="text"
		model-value="author"
		@update:model-value="value => $emit('update:author', value)"
		>
	</article>
</template>
<script>
export default{
	props: ['title', 'author'],
	emits:['update:title', 'update:author'],
};
</script>
```

# Non-Prop 속성(fallthrough 속성)
- Non-Prop 속성은 props 또는 event에 명시적으로 선언되지 않은 속성 또는 이벤트.
- class, style, id와 같은 것이 있음.

## 속성 상속
- 컴포넌트가 단일 루트 요소로 구성되어 있으면 fallthrough 속성은 루트 요소의 속성에 자동으로 추가됨.
- 자식 컴포넌트 MyButton.vue 
```javascript
<template>
	<button>click me</button>
</template>
```
- 부모 컴포넌트 
```javascript
<MyButton class="large">
```
- 최종 렌더링 된 DOM (속성 상속함)
```
<button class="large">click me</button>
```

## class, style 속성 병합, 다른 속성(id속성)은 덮어씌워짐
- class와 sylte이 아닌 속성들 (ex-id 속성)은 덮어씌워진다. 
- 만약 자식 컴포넌트 루트 요소에 이미 class와 style 속성이 정의되어 있으면, 부모로 받은 class와 style 속성과 병합함.
```javascript
// 자식 컴포넌트
<button class="btn">click me</button>
```
```javascript
// 속성 병합된 자식 컴포넌트
<button class="btn larget">click me</button>
```

## v-on 이벤트 리스너 상속
- v-on 이벤트 리스너도 동일하게 상속됨.
```
<MyButton @click="onClick"/>
```
- @click 리스너는 <MyButton>의 컴포넌트 루트요소인 <button>요소에 추가됨.
- 만약 <button> 요소에 이미 바인딩된 이벤트가 있다면 이벤트가 추가되어 두 리스너 모두 트리거 됨.

## 속성 상속 비활성하
- 컴포넌트가 자동으로 Non-Prop 속성을 상속하지 않도록 하려면 컴포넌트의 inheritAttrs: false 옵션을 설정할 수 있음.
```vue
<template>
	<button class="btn" data-link="hello">click me</button>
</template>
<script>
export default{
	inheritAttrs: false,
};
</script>
```
- 컴포넌트에 Non-Prop 속성을 비활성화 하는 일반적인 경우는 자식 컴포넌트의 루트요소 이외에 다른 요소에 Non-Prop 속성을 적용하고 싶을 때.
- ex)
```javascript
// 자식컴포넌트의 루트요소가 div라서 상속 비활성
<template>
// 비활성하지 않으면 div가 상속 받는다 -> 하지만 div의 자식태그인 button도 상속 x -> 내장 객체인 $attrs사용(v-bind)
	<div> 
		<button v-bind="$attrs">my button</button>
	</div>
</template>
<script>
	export default{
		inheritAttrs: false,
		setup(props, context){
			context.attrs;
			return {};
		}
	}
</script>
```

- 그리고 적용해야하는 요소에 <template> 에서 Non-Prop 속성에 접근할 수 있는 내장 객체 $attrs로 직접 접근 가능.
```javascript
<template>
	<p>fallthrough 속성 : {{$attrs}}</p>
</template>
```
- $attrs 객체는 컴포넌트에 선언되지 않은 모든 속성 props, emits (예 : class, style, v-on등)을 포함.
- 참고사항
- props와 달리 Non-Prop 속성은 Javascript에서 원래 대소문자를 유지하므로 foo-bar와 같은 속성은 $attrs['foo-bar']로 접근해야함.
- @click과 같은 v-on 리스너는 $attrs.onClick과 같이 함수로 접근. 

## Fragments
- Vue3에서 컴포넌트는 다중 루트 노드 컴포넌트인 fragments를 공식 지원
### Vue2 문법
- Vue2에서는 다중 루트 컴포넌트가 지원되지 않았고, 사용자가 실수로 다중 루트 컴포넌트를 만들었을 경우 경고메시지를 내보냈었음.
- 이 오류를 해결하기 위해 많은 컴포넌트가 단일 <div>로 감싸게 됐었음.
```html
<template>
	<div>
		<header></header>
		<main></main>
		<footer></footer>
	</div>
</template>
```
### Vue3 문법
- Vue3에서 컴포넌트는 다중 루트 노드를 가질 수 있음. 하지만, 개발자가 속성을 배포(상속)해야하는 위치를 명시적으로 정의해야함.
```vue
<template>
	<header></header>
	<main v-bind="$attrs"></main>
	<footer></footer>
</template>
```

# Slots
- slot을 사용하여 컴포넌트에 컨텐츠 전달 가능. 
- 컨텐츠는 태그 사이에 들어가는 값 -> <tag> contents </tag>
- \<slot\> 요소는 **부모 컴포넌트에서 제공하는 콘텐츠**를 나타내는 슬롯 콘텐츠. 슬롯은 텍스트 뿐만아니라 HTML요소, 컴포넌트 등 다양한 모든 콘텐츠가 될 수 있음.
- 예시)  FancyButton.vue 자식 컴포넌트.
```vue
<template>
	<button class="fancy-btn">
		<slot></slot>>
	</button>
</template>
```
- 부모 컴포넌트
```vue
<FancyButton>
	<span style="color: red"> Click me </span>
	<i>!</i>
</FancyButton>
```

## Fallbock Content
- 상위 컴포넌트에서 슬롯 콘텐츠가 제공되지 않을 때 슬롯에 대한 폴백(기본 콘텐츠)을 지정할 수 있음.
- 예시)  FancyButton.vue 자식 컴포넌트.
```javascript
<template>
	<button class="btn">
		<slot>Default Click !</slot>
	</button>
</teplate>
```
## Named Slots
- \<slot\> 요소에 이름을 부여하는 여러개의 \<slot\>을 정의할 수 있음.
```vue
<!-- BaseCard.vue -->
<template>
	<article>
		<div>
			<slot name="header"></slot>
		</div>
		<div>
			<slot></slot>
		</div>
		<div>
			<slot name="footer"></slot>
		</div>
	</article>
</template>
```

- <slot>에 name 속성을 부여하여 특정 슬롯 콘텐츠가 렌더링 되어야할 위치를 설정할 수 있음
- name이 없는 <slot>의 이름은 암시적으로 default임.
```vue
<!-- 부모 컴포넌트 -->
<template>
	<BaseCard>
		<template v-slot:header>제목</template>
		<!-- <template v-slot:default>안녕하세요</template> -->
		<!-- default슬롯은 암시적으로 그냥 사용 가능 -->
		안녕하세요
		<!-- 단축표현 # -->
		<template #footer>푸터</template> 
	</BaseCard>
</template>
```

## slot 전달인자 동적으로 변경 가능

``` vue
<!-- 부모 컴포넌트 -->
<template>
	<BaseCard>
		<!-- #[]안에 동적인 변수 전달 -->
		<template #[slotArgs]>제목</template>
	</BaseCard>
</template>

<script>
// ...
setup(){
	const slotArgs = ref('header');
	return {slotArgs};
}
</script>
```

## Render Scope
- 슬롯 콘텐츠는 상위 컴포넌트에 정의되어 있으므로 상위 컴포넌트의 데이터 영역에 접근은 가능하지만 하위 컴포넌트의 영역에는 접근할 수 없음.

### Scoped Slots
- Render Scope에서 업급했던 것처럼 슬롯 콘텐츠는 자식 컴포넌트의 데이터에 접근할 수 없음.
- 하지만 슬롯 콘텐츠에서 상위 컴포넌트와 하위 컴포넌트 데이터를 모두 사용할 수 있다면 개발할 때 유용
- 이러한 방법으로 자식 컴포넌트에서 \<slot\> 요소를 사용할 때 props전달하는 것처럼 속성을 슬롯 콘텐츠에 전달할 수 있음. 
- 자식 컴포넌트
```vue
<template>
	<slot></slot>
</template>

<script>
import {ref} from 'vue';
export default{
	setup(){
		const childMessage = ref('자식 메시지');
		return {childMessage};
	}
}
</script>
```

- 부모 컴포넌트
```vue
<template #default>
	{{message}} {{childMessage}} // 현재 자식 컴포넌트의 변수 접근x
</template>
<script>
import {ref} from 'vue';
export default{
	setup(){
		const message = ref('부모 메시지');
		return {message};
	}
}
</script>
```
- Scoped Slots 사용하여 Props 전달하는 것처럼 상위 컴포넌트로 전달 가능 !
- Scoped Slots 적용 자식 컴포넌트
```vue
<template>
	<slot :child-message="childMessage"></slot>
</template>

<script>
import {ref} from 'vue';
export default{
	setup(){
		const childMessage = ref('자식 메시지');
		return {childMessage};
	}
}
</script>
```
- Scoped Slots 받는 부모 컴포넌트
```vue
<template #default="obj"> // 객체에 담겨서 옴
<!-- <template #default="{childMessage}"> --> 구조분해할당도 가능 !!!
	{{message}} {{obj.childMessage}} // 현재 자식 컴포넌트의 변수 접근 가능 !!!
</template>
<script>
import {ref} from 'vue';
export default{
	setup(){
		const message = ref('부모 메시지');
		return {message};
	}
}
</script>
```


## $slots 내장 객체와 context.slots을 활용한 computed 처리
- 부모컴포컨트에서 slots 값 내려주지 않으면 출력 안하기
- $slots 내장객체 이용하여 부모로부터 받은 값이 없으면 출력안하기 조건문 작성 가능
- 자식 컴포넌트
```vue
<template>
	<article>
		<!--  부모에서 header slots 값을 주지 않으면 출력x-->
		<div v-if="$slots.header"> 
			<slot name="header"></slot>
		</div>
		<div>
			<slot></slot>
		</div>
		<!--  부모에서 footer slots 값을 주지 않으면 출력x-->
		<div v-if = "hasFooter">
			<slot name="footer"></slot>
		</div>
	</article>
</template>
<script>
export default{
	//setup(props, context){
	setup(props, {slots}){
		// setup함수 context 객체에서 slots 접근 가능 -> computed 활용 가능

		const hasFooter = computed(()=>  !!slots.footer	) //느낌표 두개 자바스크립트 문법..?
		
		return {hasFooter};
	}
}
</script>
```

# Provide / Inject (Prop Drilling 해결)
- 부모 컴포넌트 -> Props / 데이터 전달 -> 자식 컴포넌트
- 부모 컴포넌트와 자식컴포넌트 사이에 많은 중간 컴포넌트들이 끼어 있다면 ? -> 두 컴포넌트 사이에 모든 컴포넌트들에 Props 전달해야하므로 굉장히 번거로움
- 중간에 있는 컴포넌트들은 단순히 하위 컴포넌트에 Props를 전달하기 위해 Props를 선언하고 사용해야함. -> 이를 Prop Drilling이라 함(단순 Props 전달의 목적)
- =>> 이 Prop Drilling 을 해결하기 위한 것이 "Provide / Inject"

## Provide
- 하위 컴포넌트 항목에 데이터를 제공하여면 provider 역할을 하는 상위 컴포넌트 setup()함수 내부에서 provide()함수를 사용하여 데이터를 제공
```javascript
import { provide} from 'vue';
export default{
	setup(){
		provide('message', 'hello!');
	},
};
```
- provide() 함수는 두 개의 파라미터를 받음
- 첫번째 파라미터는 주입 키 : 문자열 또는 Symbol이 될 수 있음. 주입 키는 하위 컴포넌트에서 주입된 값을 조회하는 데 사용됨.
- 두번째 파라미터는 제공된 값: 값은 refs와 같은 반응성 데이터를 포함하여 모든 유형이 될 수 있음.
- 부모 컴포넌트 provide 예시
```javascript
import {provide, ref} from 'vue';
export default{
	setup(){
		const message = 'Hello World!';
		provide('static-message', message);
		return {
			message,
		};
	},
}
```
- 자식 컴포넌트 inject 예시

```javascript
import {inject} from 'vue';
export default{
	setup(){
		const staticMessage = inject('static-message', 'defaultMessage'); // 두번째 파라미터에 디폴트 값지정(provide 값 없는 경우)
		return {
			staticMessage,
		};
	},
}
```

## Reactivity 
- Provide / Inject를 반응성 데이터로 제공할 때 가능한 모든 변경을 Provider 내부에서 하는 것이 좋음 -> 유지관리 용이
- 만약 injector 내부 컴포넌트에서 반응성 데이터를 변경해야하는 경우 데이터 변경을 제공하는 함수를 함께 제공하는 것이 좋다. 
```javascript
//Provider
const message = ref('Hello World!');
const updateMessage = () => { // 데이터 변경 함수 함꼐 제공
	message.value = 'world!';
}
provide('message', {message, updateMessage});
```
```javascript
//Injector
const{message, updateMessage} = inject('message');
```
- 주입된 컴포넌트에서 제공된 값을 변경할 수 없도록 하여면 readonly()함수 사용가능.
```vue
import {provide, readonly, ref} from 'vue';
provide('count', readonly(count));
```

## Symbol 키 사용
- 대규모 애플리케이션에서 다른 개발자와 함께 작업할 때 잠재적 충돌을 피하기 위해 Symbol 주입 키를 사용하는 것이 가장 좋음
```javascript
//key.js
export const myInjectionKey = Symbol()
```
```javascript
// in provider component
import {provide} from 'vue'
import {myInjectionKey} from './keys.js'
provide(myInjectionKey, {
	/* data to provide */
});
```
```javascript
import {inject} from 'vue'
import {myInjectionKey} from './keys.js'
const injected = inject(myInjectionKey)
```

## App-level Provide
- 컴포넌트에서 데이터를 제공하는 것 외에도 App-level에서 제공할 수도 있음.
```javascript
import {createApp} from 'vue';
import App from './App.vue';
const app = createApp(App);
app.provide('appMessage', 'Hello app message');
app.mount('#app');
```

### App-level에서의 Provide / Inject 사용 예
- App-level에서의 Provide는 앱에서 렌더링되는 모든 컴포넌트에서 사용가능. Plugin작성할때 유용
- Vue2에서 컴포넌트 인스턴스 객체를 추가할때 global property에 추가하여 this로 접근했으나, Vue3에서 Composition API Setup 함수에서는 컴포넌트 인스턴스에 this 접근할 수 없음.(this  생성 전 라이플 사이클이기 때문)
-  -> 이때 때신 Provide / Inject 사용 가능.

# Lifecycle Hooks
- 라이프사이클 훅은 각 라이프사이클단계에서 사용자가 프로그래밍 코드를 추가할 수 있는 함수를 말함.
- Creation(생성) -> Mounting(장착) -> Updating(변경) -> Destruction(소멸)

## 라이프사이클 순서
1. setup() <- Composition API
2. beforeCreate()
3. created()
4. beforeMount()
5. mounted()
6. beforeUpdate()
7. updated()
8. beforeUnmount()
9. unmounted()

### Compotision API에서 사용
- beforeCreate, created 를 제외하고(필요하지 않음) -> 두 훅에서 사용하고 싶었던 함수를 그냥 setup()내부에서 사용하면 됨.
- setup 내부에서 사용 가능 

### Creation
- 컴포넌트 초기화 단계이며 Creation Hooks 은 라이프 사이클 단계에서 가장 먼저 실행됨.
- 아직 컴포넌트가 DOM에 추가되기 전이므로 DOM에 접근할 수 없다.
- 서버렌더링에 지원되는 단계
- 클라이언트나 서버 렌더 단에서 처리해야할 일이 있으면 이 단계에서 진행

### beforeCreate
- 컴포넌트 인스턴스가 초기화 될 때 실행됨.
- data() 또는 computed와 같은 다른 옵션을 처리하기 전에 측시 호출됨.

### created
- 컴포넌트 인스턴스가 초기화를 완료한 후 호출 되는 훅

### setup
- Composition API의 setup() 혹은 Opions API 훅 보다 먼저 호출됨.
- beforeCreate와 created 라이프사이클 훅은 OptionsAPI에서 사용되는 라이프사이클 훅으로 Vue3 Composition API를 활용하여 개발을 진행할 때는 setup()함수로 대체할 수 있음.

### Mounting
- DOM에 컴포넌트를 삽입하는 단계. onBeforeMount와 onMounted가 있음
- 서버 렌더링에서 지원되지 않음
- 초기 렌더링 직전에 돔을 변경하고자 한다면 이 단계에서 활용할 수 있음.
#### onBeforeMount
- 컴포넌트가 마운트되기 직전에 호출됨
- 대부분의 경우 사용을 권장하지 않음
- -> onBeforeMount와 onMounted사이에서 자식 컴포넌트가 생성, onMounted까지 완료됨.
#### onMounted
- 컴포넌트가 마운트된 후에 호출 됨. DOM에 접근 가능.
- 모든 자식 컴포넌트가 마운트되었음을 의미.
- 자체 DOM 트리가 생성되어 상위 컴포넌트에 삽입되었음을 의미함.

### Updating
- 반응형 데이터가 변경되어 DOM에 업데이트 되려고 할 떄 호출
- 컴포넌트에서 사용되는 반응형 데이터가 변경되었거나 어떠한 이유로 **재렌더링**이 발생될 때 호출.
- 디버깅이나 프로파일링 등을 위해 컴포넌트 재렌더링 시점을 알고 싶을 때 사용.


#### onBeforeUpdate
- 반응형 상태변경으로 인해 컴포넌트가 DOM 트리를 업데이트하기 직전에 호출됨.
- 컴포넌트에서 사용되는 반응형 상태 값이 변해서, DOM에도 그 변화를 적용시켜야할 때가 있음.
- 이때, 변화 직전에 호출되는 것이 바로 onBeforeUpdate 훅. 

#### onUpdated
- 반응 상태 변경으로 인해 컴포넌트가 DOM 트리를 업데이트한 후에 호출됨.
- 상위 컴포넌트의 onUpdated 훅은 하위 컴포넌트의 훅 이후에 호출됨(Child-> Parent)
- 이 훅은 다른 상태변경으로 인해 발생할 수 있는 컴포넌트의 DOM 업데이트 후에 호출됨. 
- 특정 상태 변경 후에 업데이트된 DOM에 엑세스 해야하는 경우 대신 nextTick()을 사용 
- 경고) onUpdated훅에서 컴포넌트의 상태를 변경하면 무한 업데이트 루프가 발생할 수 있음.

### Destruction
- 해체(소멸)단계이며 onBeforeUnmount 와 onUnmounted가 있음. 

#### onBeforeUnmount
- 컴포넌트가 마운트 해제되기 직전에 호출됨

#### onUnmounted
- 컴포넌트가 마운트 해제된 후 호출됨.


# Template Refs
- 뷰에서 DOM에 직접 접근할떄 사용하는 템플릿 참조
- Vue의 선언적 렌더링 모델은 대부분의 직접적인 DOM의 작업을 대신 수행.
- 하지만 때론 기본 DOM요소에 직접 접근해야하는 경우가 있을 수 있음.
- -> 이때 ref 특수 속성을 사용해서 쉽게 접근 가능
```vue
<input type="text" ref="input"/>
```
- ref는 특수속성. 이 ref 특수 속성을 통해 마운트 된 DOM 요소 또는 자식 컴포넌트에 대한 참조를 얻을 수 있음 !

## Ref 접근하기 
- Composition API로 참조를 얻으려면 동일한 이름의 참조를 선언해야함
- 컴포넌트가 마운트 된 후에 접근 가능!!!
- <template> 안에서 input으로 Refs참조에 접근하려는 경우 렌더링 되기 전에는 참조가 null 일 수 있음
- <template> 안에서 $refs 내장 객체로 Refs 참조에 접근 가능

```vue
<template>
	<div>
		<!-- ref 속성 변수명 짓기 -->
		<input ref="input" type="text" />
		<p>{{ input }}</p>
		<!-- 이상태에서 새로고침하면 null-> v-if로 마운트된 후 출력 -->
		<p v-if="input">{{ input.value }}</p>
		<!-- $ref 내장객체 사용 가능 -->
		<p>{{ $refs.input.value }}, {{ $refs.input === input }}</p>
	</div>
</template>

<script>
import { onMounted, ref } from 'vue';
export default {
	setup() {
		// ref 속성 동일한 변수 짓기
		const input = ref(null);
		// 돔 요소에 대한 참조는 마운트 이후 가능 -> onMounted()에서 접근 가능

		onMounted(() => {
			input.value.value = 'Hello World!';
			console.log('onMounted: ', input.value);
		});

		return { input };
	},
};
</script>

<style lang="scss" scoped></style>
```

## v-for 내부 참조
- v-for 내부에서 ref가 사용될 때 ref는 마우트 후 요소 배열로 채워짐
```vue
<template>
	<ul>
		<!-- // 마운트 된 후 itemRefs 안에 돔 요소 채워짐 -->
		<li v-for="fruit in fruits" :key="fruit" ref="itemRefs">
			{{ fruit }}
		</li>
		<!-- 함수 바인딩도 가능 -->
		<li
			v-for="fruit in fruits"
			:key="fruit"
			ref="(el)=>itemRefs.push(el.textContent)"
		>
			{{ fruit }}
		</li>
	</ul>
</template>

<script>
import { onMounted, ref } from 'vue';
export default {
	setup() {
		const list = ref([1, 2, 3]);
		const fruits = ref(['사과', '딸기', '포도']);
		// 마운트 된 후 itemRefs 안에 돔 요소 채워짐
		const itemRefs = ref([]);

		onMounted(() => {
			itemRefs.value.forEach(item => console.log('item: ', item));
		});
		return {
			list,
			fruits,
			itemRefs,
		};
	},
};
</script>
<style lang="scss" scoped></style>
```


## 자식 컴포넌트로 접근하는 Refs
- ref를 자식 컴포넌트에도 사용 가능.
- ref로 자식 컴포넌트에 참조값을 얻게 되면 자식 컴포넌트의 모든 속성과 메서드에 대한 전체를 접근 가능
- 이러한 경우 부모/자식 간 의존도가 생기므로 반드시 필요한 경우만
- 일반적으로 ref보다 표준 props를 사용하며 부모/자식간 상호작용을 구현해야함 !

```vue
<!-- 부모 컴포넌트 -->
<template>
	<TemplateRefsChild ref="child"></TemplateRefsChild>
</template>
<script>
import TemplateRefsChild from './TemplateRefsChild.vue'
export default{
	component:{
		TemplateCHild,
	},
	setup(){
		onMounted(()=>{
			// 돔 요소에 대한 참조는 마운트 된 후
			console.log(child.value);
			child.value.sayHello();
		})
	}
}
</script>
```

## 부모 컴포넌트로 접근하는 $parent
```vue
<template>
	<div>{{$parent}}</div>
</template>
```

# \<script setup\>
- \<script setup\>은 Single-File Component내에서 Composotion API를 사용하기 위한 syntactic sugar(문법적 설탕)임
- cf)문법적 설탕 : 기능은 그대로인데 읽는 사람을 위해 직관적으로 쉽게 코드를 읽을 수 있게 만듬
- SFC와 Composition API를 사용하는 경우 \<script setup\>을 사용하는 것을 권장.
- 간결한 문법으로 상용구를 줄일 수 있음
- 타입스크립트를 사용한 props와 emits 선언 가능
- 런타임 성능의 향상 (템플릿이 setup 스크립트와 같은 scope에 있는 render함수로 컴파일 되므로 프록시가 필요 없음)
- 더 뛰어난 IDE 타입 추론 성능

```vue
<script setup>
import ChildComponent from '@components/ChildComponent.vue'; // component:{} 에 등록 필요 없어짐 !
//아래 코드가 필요 없어짐..!! => setup(), return{} 필요 없음. 
// export default{
// setup(){
// 		return {

// 		}
// 	}
// }
</script>
```

## defineProps() & defineEmits()
- .eslintrc.cjs에서 설정해야 사용가능 
```
env:{
	'vue/setup-compiler-macros':true, 
}
```
- defineProps() 와 defineEmits() APIs를 <script setup> 내에 선언하여 props와 emits를 사용할 수 있음
``` javascript
<script setup>
const props = defineProps({
	foo: String
})
const emit = defineEmits(['change', 'delete'])
</script>
```
- defineProps와 defineEmits는 <script setup> 내부에서만 사용할 수 있는 컴파일러 매크로. -> 그렇기 때문에 import 할 필요가 없으면 <script setup>이 처리될 때 컴파일 됨.
- defineProps는 props 옵션과 동일한 값을 허용. 그리고 defineEmits는 emits 옵션과 동일한 값 허용
- defineProps와 defineEmits에 전달받은 옵션을 기반으로 타입 추론을 제공
- defineProps와 defineEmits에 전달된 옵션은 setup()에서 모듈 영역으로 호이스팅됨. 따라서 옵션을 setup()영역에 선언된 지역변수를 참조할 수 없음. 하지만 import 된 옵션을 사용할 수 있음. import도 모듈영역으로 호이스팅되기 떄문.

## defineExpose()
- script setup을 사용하는 컴포넌트는 기본적으로 Templat Refs나 $parent 같이 컴포넌트간 통신이 닫혀 있으.ㅁ
- 명시적으로 노출하려면 defineExpose() 사용해야함.


## useSlots() & useAttrs()
- slots과 attrs는 <template> 내부에서 $slots와 $attrs로 직접 접근해서 사용. 
- script setup 내부에선s useSlots(), userAttrs() helper 메서드 사용 가능
```vue
const slots = userSlots();
const attrs = useAttrs();
```

## <script>와 <script setup> 함계 사용
- <script setup>에서 표현할 수 없는 inheritAttrs 옵션이나 Plugin을 통해 활성화된 Custom옵션을 사용하고자 할때 normal<script>을 함께 선언
- named export를 선언했을 때 (export const data)
- 한 번만 실행되어야 하는 로직이 있을 때
```vue
<script>
//일반 스크립트, 모듈 범위에서 한 번만 실행 -> 일반 스크립트는 한번만 실행됨
runSideEffectOnce()
//옵션 선언
export default{
	inheritAttrs: false, //NonProps 속성을 루트에 상속할 것인가?
	customOptions: {}
}
</script>
<script setup>
// 각 인스턴스 생성 시 setup() 범위에서 실행됨
</script>
```

## Top-level await
- <script setup> 내의 top-level에서 await를 사용할 수 있음. 이러한 코드는 async setup()이렇게 컴파일 됨 

# 동적 컴포넌트
- 컴포넌트를 동적으로 변경하고 싶을 때 v-bind:is 속성을 사용해서 변경할 수 있음. 동적 컴포넌트는 탭 인터페이스와 같이 컴포넌트 간에 동적으로 전환해야할 떄 유용
```vue
<component :is="currentTabComponet"></component>
```
- :is 속성에 전달된 값은 다음 중 하나를 포함할 수 있음.
- 등록된 컴포넌트의 문자열 이름 string
- 실제 가져온 컴포넌트 객체 object

```vue
<template>
	<button @click="changeCurrentComp(DynamicApple)">사과</button>
	<button @click="changeCurrentComp(DynamicBanana)">바나나</button>
	<hr/>
	<component :is="currentComp"/>
</template>

<script setup>
import DynamicApple from ''
import DynamicBanana from ''
//const currentComp = ref(DynamicApple);
// is 속성으로 컴포넌트를 넘길 때는 shallowRef 함수로 넘기는게 퍼포먼스 유리
const currentComp = shallowRef(DynamicApple); //속성에 대해서는 반응 x, 값 자체가 바뀌었을때만 반응 

const obj = shallowRef({name : 김길동});
obj.value = {}; //반응
obj.value.name = ""; //반응X
const changeCurrentComp = comp => (currentComp.value = comp);
</script>
```
