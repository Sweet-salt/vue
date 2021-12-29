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
