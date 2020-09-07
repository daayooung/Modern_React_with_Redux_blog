# Synchronous / Asynchronous action creator

### Synchronous action creator

- 즉시 사용할 수 있는 data로 action을 return한다.

### Asynchronous action creator

data를 준비하는 데 약간의 시간이 걸린다. -> middleware (redux-thunk)설치 필요

> [243강] Middlewares in redux

# redux Thunk

### Normal Rules

1. acton creator는 반드시 action object를 return한다.
2. action들은 반드시 type 속성을 가진다.
3. action들은 선택적으로 'payload'를 가진다.

### Rules with Redux Thunk

1. action creator는 action object를 return할 수도, function을 return할 수도 있다.
2. 만약 action object가 return되면, 반드시 type을 갖는다.
3. 만약 action object가 return되면, 선택적으로 'payload'를 가진다.
4. 만약 function을 return하면, dispatch와 함께 function이 호출된다.
5. request가 끝날 때까지 기다린다.
6. request가 완료되면, action을 수동적으로 dispatch한다.

# Rules of Reducers

1. 반드시 value를 return해야 한다. ('undefined' 제외)
2. 이전 state 및 action만 사용하여 앱 내부에서 사용할 'state'또는 data를 생성한다. (reducer는 pure하다).
3. 자신을 벗어난 것을 value로 return하면 안된다.

```
export default (state, action)=> {
<!-- bad -->
return document.querySelector('input')

<!-- bad -->
return axios.get('/post')

<!-- good -->
return state + action
}
```

4. 입력된 state argument를 변경하면 안된다.
   (하지만 입력된 state를 그대로 return하라는 뜻은 아니다. state를 변경없이 그대로 return하면 react는 변경된 것이 아무것도 없다 판단하여 rerender하지 않는다.)
