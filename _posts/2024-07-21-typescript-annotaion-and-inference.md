---
layout: post
title: Typescript 2편 타입 정의와 추론
author: K
date: 2024-07-21 03:31:00 +09:00
categories: [Typescript]
tags: [Typescript]
render_with_liquid: false
comments: true
image: 
    path: /blog/typescript.webp
    alt: Typescript
---


# Typescript 2편 타입 정의와 추론

![Typescript](blog/typescript.webp)

---

## Type Annotations (타입 정의)

타입 어노테이션은 변수가 참조하는 값의 타입이 무엇인지, 타입스크립트가 알 수 있도록,

"우리가" 작성할 코드이다.


### Example #1 

```typescript
interface Todo {
    id: number;
    title: string;
    createdAt: Date;
}

const todoItem: Todo = {
    id: 1,
    title: 'todo-title',
    createdAt: new Date()
}

console.log(todoItem);
```

todoItem의 타입. 즉 `interface Todo`가 "우리가" 작성한 Type Annotation 이다.

---


## Type Inference (타입 추론)

타입 추론은 타입스크립트가 말 그대로 타입을 자동으로 추론 하는것을 말한다.

```typescript
let text = "string";
let number = 0;
let bool = false;
```

`text`는 들어간 value를 확인하고 자동으로 string 타입으로 추론한다.

`number` 또한 value를 확인하고 자동으로 number 타입으로 추론한다.


### ❗ 알아야 할 부분

```typescript
let fruit;
fruit = "과일"; //  ⚠️ any type
```

값을 할당하고 초기화 하는 과정을 위 코드처럼 나누게 되면,

Type Annotation이 any 타입으로 바뀌게 된다.

---

## Usage with Functions

함수에서도 마찬가지로 타입 어노테이션을 아래와 같이 작성 할 수 있다.

```typescript
// ✅ GOOD CASE 
const plus = (x: number, y: number): number => {
    return x + y;
}
```

함수에 들어오는 `인자에 대한 타입`을 정의 해주고, `콜론(:) 뒤에는 반환값에 대한 타입`을 정의 해주면 된다.

추가로 `함수의 반환값에 한해서는 타입 추론이 작동` 한다.

```typescript
// ❗️ Bad Case But working.
const plus = (x: number, y: number) => {
	return x + y;
}
```
이렇게 작성해도 문제는 없지만, 작은 실수로 인해 타입 추론이 망가지는 케이스가 있기 때문에,

반환 값에도 타입을 정의 해주는 것 을 권장한다.

```typescript
//❗️타입추론을 사용했으나, return을 쓰지않아 자동으로 void로 추론함
const exampleCase = (x: number, y: number) => {
	x * y;
}
```


## Conclusion

항상 타입추론을 활용 하다가, 직접 타입 정의를 해야 할때는 다음과 같다.

1. 함수가 any타입을 반환 할때,
2. 변수를 선언한 후 다른줄에서 초기화 할때
3. 변수에 여러 타입이 들어올 가능성이 있을때


