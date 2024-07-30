---
layout: post
title: Typescript 4편 구조분해(Destructuring) 사용 하기
author: K
date: 2024-07-30 00:00:00 +09:00
categories: [Typescript]
tags: [Typescript]
render_with_liquid: false
comments: true
image: 
    path: /blog/typescript.webp
    alt: Typescript
---


# Typescript 4편 구조분해(Destructuring) 사용 하기

![Typescript](blog/typescript.webp)

---

## Functions

타입스크립트 환경의 함수에서 구조분해를 사용 해보자.

### Example #1 

```typescript
const post = {
  title: "post title",
  content: "lorem ipsum...",
  date: new Date(),
}

// 👌 post를 console.log로 출력하는 함수
// ❗구조분해(Destructuring)을 하지 않은 예시
const logPost = (post): void => {
  console.log(post.title); // post title
  console.log(post.content); //lorem ipsum...
}

logPost(post);
```

먼저 post를 로그로 출력해주는 함수는 
반환 된 값이 없을것 같아, return에 해당하는 부분을 void로  타입을 정의해 주었다.

그 후, `post.~~~` 형식으로 출력한 예시이다.

여기서 구조분해를 사용해보자.

### Example #2

```typescript
const post = {
  title: "post title",
  content: "lorem ipsum...",
  date: new Date(),
}

// ES2015
const logPost2 = ({
  title,
  content,
}: {
  title: string;
  content: string;
}): void => {
  console.log(title); // post title
  console.log(content); // lorem ipsum...
};

logPost2(post);
```

return하는게 없으니 return값에 대한 타입은 void로 정의 해주는 부분은 동일 하고,

title과 content만 구조분해로 데이터를 뽑아온다고 했을때,

중괄호로 묶어, post를 `{title, content}`로 구조 분해를 한 예시 이다.

---

## Objects 

객체 에서의 구조분해도 살펴보자. 결국에 위에서 설명한 함수와 사용 방법이 동일 하다.

### Example #1

```typescript
const post = {
  id: 1,
  title: "post title",
  content: "lorem ipsum...",
  date: new Date(),
  setContent(content: string): void {
    this.content = content;
  }
};

const {id, title, content, setContent}: {id: number, title: string, content: string, setContent(content: string): void} = post;

console.log(id); // 1
console.log(title); // post title
console.log(content); // lorem ipsum...

setContent.bind(post)("UPDATED CONTENT");
// ⚠️ 객체 내부 메서드를 구조분해 할 경우 this 바인딩이 깨지기 때문에 bind메서드를 사용 해주어야함

console.log(post.content); // UPDATED CONTENT
```
이 객체 에서는, 객체안에 메서드를 추가하였다.

`title`이나 `content`같은 녀석들은 함수와 똑같이 구조분해 하면 되지만, 

메서드 같은 경우는 구조 분해까지는 동일하지만, 사용 할때는 살짝 다르다.

구조분해 까지는 동일 하지만, 호출할때 this 바인딩이 깨지기 때문에, 

bind 메서드를 사용하여 `post`객체의 컨텍스트를 유지해야 한다.

---

## Conclusion 

* 한줄로 작성하면 복잡하지만, 여러줄로 나누어 생각하면 더 쉽게 읽고 쓸수 있다.

```typescript
const {
  id,
  title,
  content,
  setContent,
}: {
  id: number;
  title: string;
  content: string;
  setContent(content: string): void;
} = post;
```
* 객체 내부 메서드를 구조분해 하고 사용할 때는,  `bind` 메서드를 사용하여 객체의 컨텍스트를 유지해야 한다.


[Destructuring Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

[Function.prototype.bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)