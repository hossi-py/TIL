# Vue 정리

[TOC]

## A. Vue의 기본 형태 (HTML)

```html
<body>
    <div id="app">
        {{ message }}
	</div>
    
    <script>
    	const app = new Vue ({
            el: '#app',
            data: {
                message: 'Hello World!',
                ]
            }
        })
    </script>
</body>

```

```markdown
Data와 DOM이 연결되었다.
```

`data`

- vue 앱의 상태 데이터를 정의하는 곳
- Vue template에서 보간법을 통해 접근할 수 있다.
- this 키워드를 통해 접근할 수 있다.





## B. Vue 구문

### 1) v-for

> 반복문 :key 속성을 반드시 정의해야 한다.



### 2) v-if / v-else-if / v-else

> 조건문 참이면 Yes / 거짓이면 No가 렌더링 된다.



### 3) v-bind: 혹은 :

> 전달인자 : HTML 속성을 갱신할 수 있다.
>
> Object 형태로 사용하면 value가 true인 key가 class 바인딩 값으로 할당된다.



### 4) v-on: 혹은 @

> DOM 이벤트를 수신한다. 전달인자는 이벤틀르 받을 이름이다.



### 5) v-model

> 양방향 바인딩을 할 수 있다.



### 6) v-text / v-html

> text : 내부 보간법 문법이 text로 컴파일된다.
>
> html : 다른 사용자 데이터를 절대 사용하면 안된다.



### 7) v-show

> v-if 와 비슷하지만 v-if는 조건에 따라 컴포넌트가 실제로 제거되고 생성되지만,
>
> v-show는 css의 display 속성만 변경된다.



### 8) filter

> 중괄호 보간법 or v-bind: 표현법을 이용할 때 사용 가능하다.



### 9) lodash

> 여러 표현법을 사용할 수 있다.

#### a) _.reverse()

#### b) _.sortBy()

#### c) _.range()

> 끝 숫자 - 1까지 포함된다. (기존 파이썬과 같음)

#### d) _.random()

> 끝 숫자까지 포함된다. (기존 파이썬과 다름)

#### e) _.sampleSize()

> 속해있는 배열 중 , 옆에 있는 숫자만큼 꺼낸다. 만약 우측이 크다면 모두 꺼낸다.



## C. Vue 함수표현

> methods를 이용하여 함수를 설정할 수 있다.

### 메뉴 랜덤 선택

```vue
<script>
	methods: {
        pickOneInLunchMenu: function () {
            const randomIndex = _.random(this.lunch.length - 1)
            this.selectedLunchMenu = this.lunch[randomIndex]
        }
    }
</script>
```



## D. .Vue 형태

```vue
<template>
	<div id="app">
        
    </div>
</template>

<script>
export default {
    name: 'App', (.vue 파일의 이름)
    components: {
        
    }

}

</script>
```



## Vuex

> Vue.js 애플리케이션에 대한 상태 관리 패턴 + 라이브러리
>
> store 옵션으로 모든 자식 컴포넌트에 저장소를 주입한다.
>
> this.$store. 으로 접근할 수 있다.



### 1) state

> 컴포넌트 간에 공유할 data 속성을 의미한다. data 변경이 일어나지 않음

### 2) getters

> 특정 state에 대해 어떠한 연산을 하고 그 결과를 뷰에 바인딩 할 수 있다.
>
> state의 변경 여부에 따라 getters는 재계산이 된다.

### 3) mutations

> 동기적 요청만 작성한다. state를 변경한다. 함수로 구현되며, 첫번째 인자로는 state를 받고 두번째 인자는 data를 받는다.
>
> store.commit

### 4) actions

> 비동기 작업이 가능하다. 첫번째 인자는 context를 받고 두번째 인자는 data를 받는다.
>
> mutations을 실행시킨다.
>
> store.dispatch



## HOMEWORK 정리

SPA : single page application / 모든 정적 리소스를 한번에 받고, 이후부터는 페이지 갱신에 필요한 데이터만 전달 받는다.



MVVM

M :  model : 데이터를 준비하고 그에 대한 이벤트를 보냄

V : view : 모델을 관찰하고 있다가, 이벤트가 전달되면 화면을 갱신한다.

VM :  view model : view와 model 사이에 매개체 역할



computed와 watch의 차이점

| computed                     | watch                                                        | 차이점                                                       |
| ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 함수의 반환값이 바인딩 된다. | 데이터를 감시하고, 데이터의 변화가 일어났을 때 실행되는 함수이다. | computed는 특정 데이터를 직접적으로 사용하여 다른 값을 만들 때 사용하고 watch는 특정 데이터의 변화 상황에 맞춰 다른 data를 바꿔야 할 때 사용 |



created Hook은 DOM이 그려지기 전에 실행된다.



NPM : node package manager



history mode  : 브라우저에서 지원하는 history api를 사용하면 주소의 이동 없이 URI만 바꿀 수 있다.



HTML에서 v-on:click 디렉티브 사용가능 / Component에서는 v-on:click.native 형태로 사용



props => 데이터를 상위에서 하위로 전달 / emit => 하위에서 상위로 이벤트 전달

(vuex 대신 사용하는 것이다.)





