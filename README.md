# first_vue

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


------------------------
this 를 사용할 때 arrow function을 사용하면 Vue를 가리키지 않음.
------------------------

## 보간법( Interpolation )
- 데이터 바인딩의 가장 기본 형태 {{}}(이중 중괄호 구문) 기법을 사용한 문자열 보간법. 
- Mustache태그는 해당 컴포넌트 인스턴스의 msg 속성 값으로 대체됨. msg속성이 변경될 때마다 갱신됨.

- v-once 디렉티브 -> 데이터가 변경되어도 갱신X 일회성 보간 수행시 사용


## computed
- computed는 캐싱이 되어있기 때문에 한번 연산된 것을 다시 사용 할 때에는 다시 연산하지 않는다.
- 데이터를 최적화 하는 용도로 사용한다.
- 반복사용에 부담이 적다.

## watch
- 감시하는 용도로 사용
- 작성법
``` 
watch: {
    함수() {
        console.log('함수:', this.함수)
    }
}
```


### v-if
- v-if를 사용할 때 따로 랜더링 되지 않게 만들기 위해서는 template를 사용하면 된다.
- 최상위 temlate에는 적용되지 않는다.

### v-show
- 엘리먼트를 조건에 따라 표시하기 위한 또 다른 방법
- 사용법은 거의 동일
```
<h1 v-show="ok">Hi!!</h1>
```
- 둘의 차이점은 v-show를 쓰는 엘리먼트의 경우, 항상 렌더링 되어 DOM(HTML)에 남아있다.
- v-show는 단순히 엘리먼트의 css display 속성만을 전환한다.


## v-if VS v-show
- v-if는 실제 조건부 렌더링 
- DOM자체를 생성 X
- v-if는 게으르다.
    - 조건이 거짓 -> 아무것도 안함.
    - 조건 참 -> 렌더링

- v-show는 항상 렌더링함.
    - 엘리먼트를 DOM에 우선 렌더링 후 조건에 따라 CSS display 속성을 전환함.

### 정리
- v-if -> 전환 비용이 높음 / v-show -> 초기 렌더링 비용 높음
- 자주 전환 -> v-show / 런타임 시 조건이 변경되지 않으면 -> v-if 


# 오류 발생
- v-for에 대한 연습도중 고유한 id값을 가져오기 위해 shortid를 사용 하려했으나 오류가 발생함
- 발생한 오류는 'shortid' is defined but never used  no-unused-vars
## 해결법
- 코드를 짜는 도중에 발생한 오류 그냥 숙련도 이슈 하지만 never used  no-unused-vars 오류 발생시 해결밥법을 구글에서 찾아봄 나중에 혹시나를 위해 적어둠 
``` 해결방법 - package.json에 eslintConfig를 추가
{
    "name": "your-app-name",
    "dependencies": { ... },
    "devDependencies": { ... },
    "eslintConfig": { // Add this <-----
        "root": true,
        "env": {
            "node": true
        },
        "extends": [
            "plugin:vue/essential",
            "eslint:recommended"
        ],
        "parserOptions": {
            "parser": "babel-eslint"
        },
        "rules": { // rules configuration here <-----
            "no-unused-vars": "off" 
        }
    }
}
```

- eslint 구성을 에 저장하기로 선택한 경우 키 .eslintrc.js를 추가하기만 하면 rules됩니다.
```
module.exports = {
    ...
    rules: {
        "no-unused-vars": "off"
    }
}
```
- 이거 오류에 대해 생각하느라 1시간을 써버림 코드를 짤 때에는 신중하게 한번더 생각하자.

# 오류발생2
- template 안에는 둘 이상의 루트 노드를 가질 수 없음

## 해결법
- div 태그로 전체 내용을 감싸기 


## 고유한 값이 필요할 때 만드는 법
```
npm i -D shortid
```
```
<template>
  <ul>
    <li
      v-for="x in newX"
      :key="x.id"
    >
      {{x.name}}-{{x.id}}
    </li>
  </ul>
</template>

<script>
  import shortid from 'shortid'
  export default{
    data(){
      return {
        arr: [ 'apple', 'banana', 'melon'],
        
    }
  },
  computed: {
    newX(){
      return this.arr.map(x =>
       ({id: shortid.generate(),
        name: x})
      )
    }
  }
}
</script>
```

#### v-if < display  <   visibility     <     opacity
     x      dom/cssom    dom/cssom/rendertree


## 컴포넌트
- 공통으로 사용하기 위해서 사용.
- 특별한 역할을 부여하기 위해 사용.

### 전역 컴포넌트
```
Vue.component('product-list', {
    template: '<button>이런식</button>',
    data(){
        return {
            //여기다 작성 
        }
    }
});
```
- 함수로 등록하는 이유는 private 하게 만들기 위해서임

### 이벤트 핸들링
- 메소드 체이닝 가능.
- once -> 한번만 실행
- passive -> 사용자의 경험을 향상시켜주고 싶을 때 사용

### 이벤트 버블링
- 이벤트가 상위요소로 타고 타고 올라가는 것.
- 방지법 : stopPropagation()

### 이벤트 캡처링
- capture 
- 버블링과 반대되는 개념

### 양방향 데이터 바인딩
```
<template>
  <div>
    <h1>{{ msg }}</h1>
    <input 
    type="text"
    v-model="msg"
    />
    <input type="checkbox"
    v-model="checked"
    >
  </div>
</template>

<script>
  
  export default{
    data() {
      return {
        msg: 'Hello World!',
        checked: false
      }
    }
}
</script>
```
- 주의사항
  - v-model 사용시에는 한글은 바로바로 적용이 안됨
  ```
  :value="msg"
  @input="msg = $event.target.value"
  ```
  - 이걸 대신 사용하자.

#### 컴포넌트 - 속성 상속
- template안에 루트 요소가 2개일 경우에는 클래스를 어떤 요소가 받게 될 지 알수가 없음 그래서 :class="$attrs.class" 이런식으로 클래스를 넣어줌


### 약어
- v-bind: => :
- v=on: => @
- v-slot: => #


### Ref
- 참조를 위해서 사용
- mounted(html에 연결된 직후)에 사용 가능함. 
- 클래스에 클래스이름적고 refs.classname으로 참조가 가능하다.
