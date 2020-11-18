# 서론

이메일 중복 체크하는 API를 아래와 같이 만들었다. EmailCheckRequest DTO는 email만 있는 DTO이다.
최근 무의식적으로 DTO를 생성하고 있는 것 같았다. Map을 사용할 수도 있는데 나만의 기준을 정하는 것이 필요하다고 생각하였다.

```java
public ApiResult<Boolean> checkEmail(@RequestBody EmailCheckRequest emailCheckRequest) {
...
```

# DTO, Map 장단점

## DTO

### 장점
* 명시적으로 표현 할 수 있다.

### 단점
클래스를 매번 만들어야 한다.
DTD에 대한 네이밍을 제대로 표현하기가 어려울(?) 때가 있다.

## Map

### 장점
* 추가적인 class가 필요없다.

### 단점
* 파악하기 어려울 수 있다.
* 직접 key 값을 다루어야 하기 때문에 휴먼 에러가 발생할 수 있다.

내가 생각하기에 데이터가 지금처럼 1개인 경우 Map을 사용하는 것이 낫다고 생각한다. 하지만 요청된 데이터가 많은 경우 Map을 사용한다면 파악하기도 여럽고, key를 직접 다루다 보면 실수할 여지가 있을 수 있다. 그래서 데이터가 적으면 Map을 사용하는 것이 낫고, 많다면 DTO를 사용하는 것이 맞지 않을까? 라는 생각을 한다.
