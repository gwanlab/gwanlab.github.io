---
layout: post
title: Typescript 3편 void, never
author: K
date: 2024-07-22 00:00:00 +09:00
categories: [Typescript]
tags: [Typescript]
render_with_liquid: false
comments: true
image: 
    path: /blog/typescript.webp
    alt: Typescript
---


# Typescript 3편 void, never

![Typescript](blog/typescript.webp)

---

## Void

```typescript
const showMessage = (message: string) => {
    console.log(message);
}
```

위 코드의 경우 return되는 값이 없기 때문에, 타입 추론(Type Inference)에서  자동으로 `void` 타입으로 추론한다.

`void`는 아무것도 반환하지 않는 의미 이기도 한데,

정확히 말하면 void를 반환하는 함수는 `null` 혹은 `undefined`를 반환 할 수 있다.

함수의 반환값과 관련된 특수한 타입이 한가지 더 있는데 이것이 바로 `never`이다.


---

## Never

```typescript
const doSomething = (message: string): never => {
  throw new Error(message);
};

doSomething("hello");
```

단순하게 에러를 던지는 코드이다. 함수가 끝까지 실행되지 않고, 오류가 발생해 함수가 종료 되는데

이 경우 반환 타입을 `never`로 정의 할 수 있다.

(예시일뿐, 실제로 의도적으로 오류를 발생시키는 케이스는 없다고 생각하면 된다.)


```typescript
//❗Message를 받지못하면 에러를 발생시키고 그렇지 않으면 message를 Return
const doSomething = (message: string): never => {
	if(!message) throw new Error(message);
	return message;
}
```

위 코드의 케이스는 반환을 할 수도있고, 못할 수도 있기 때문에,
`never` 타입에는 적절하지 않다.

`never`는 함수가 null이든 undefined든 그 무엇도 반환하지 않을때 사용하면 된다.

---

## Conclusion

* void는 아무것도 반환하지 않는 의미이지만, 실제로 `null` 혹은 `undefined`를 반환 할 수 있다.
* never는 함수가 아무것도 반환하지 않는게 확실할때 사용 한다.