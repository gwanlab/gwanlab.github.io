---
layout: post
title: React-Hook-Form에 Zod를 곁들여 유효성 검증하기
author: K
date: 2024-04-13 02:21:00 +09:00
categories: [React, React-Hook-Form, Zod]
tags: [React, Validation, Zod, React-Hook-Form]
render_with_liquid: false
comments: true
image: 
    path: /blog/react-hook-form-with-zod.png
    alt: React-Hook-Form with Zod
---

# React-Hook-Form에 Zod를 곁들여 유효성 검증하기

![React-Hook-Form-With-Zod](blog/react-hook-form-with-zod.png)


React-Hook-Form은 유효성 검사를 쉽게 사용할 수 있게 해주는 라이브러리이다.

이것만 사용해도 무난한 편이지만, Zod를 곁들이면 좀 더 강력하고 편하게 유효성 검증을 할 수 있는데 Zod는 어떤 역할을 할까?

---

## Installation

Zod는 타입스크립트 스키마 선언 및 스키마 유효성 검사 라이브러리이다.

설치 후 예제 코드와 함께 간단하게 사용방법을 알아보자.

```console
npx create-react-app hook-form-with-zod --template typescript
npm install react-hook-form @hookform/resolvers zod
npm start
```

create-react-app을 통해 새로운 프로젝트를 만들고, zod와 react-hook-form을 설치했다.

설치가 끝났다면 쓸모없는 파일들을 제거한다.

`src` 폴더안에 있는 `App.css` , `App.test.tsx`, `logo.svg`, `reportWebVitals.ts`, `setupTests.ts` 파일들을 제거 하였다.

---
## 폼 만들기

그후 `src` 폴더 안에 `Form.tsx` 컴포넌트를 만들어 준다.

아래 예제 코드는 layout과 스타일링만 작성했기에 tsx작성하기 귀찮은 사람은 아래 코드를 복붙해도 된다.

```tsx

// src/Form.tsx
import React from "react";

const Form = () => {
  return (
    <form className="space-y-3">
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="name"
        >
          이름
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="text"
          placeholder="이름을 입력하세요."
        />
      </div>
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="email"
        >
          이메일
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="email"
          placeholder="이메일을 입력하세요."
        />
      </div>
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="password"
        >
          비밀번호
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="password"
          placeholder="********"
        />
      </div>
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="cPassword"
        >
          비밀번호 확인
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="password"
          placeholder="********"
        />
      </div>
      <div>
        <input type="checkbox" id="terms" className="mr-2" />
        <label htmlFor="terms" className="text-sm font-bold text-gray-700">
          약관동의
        </label>
      </div>

      <div>
        <button className="w-full font-bold py-3 px-2 text-white bg-cyan-400 rounded-md ">
          Sign-Up
        </button>
      </div>
    </form>
  );
};

export default Form;
```

```tsx
// src/App.tsx
import React from "react";
import Form from "./Form";

function App() {
  return (
    <div className="max-w-lg mx-auto flex  mt-10 border py-5 px-10 flex-col ">
      <div>
        <h1 className="text-2xl font-bold mb-8 text-center">
          React-Hook-Form With Zod
        </h1>
      </div>
      <Form />
    </div>
  );
}

export default App;
```

![React-Hook-Form-With-Zod-Image-1](blog/react-hook-form-with-zod-img1.png)

---

## Zod Example #1

Zod의 장점은, 타입스크립트의 타입을 자동으로 추론하고, 그 타입을 추출할 수 있다는 점이다.

또한, 종속성이 없는 독립형 라이브러리라서 다른 라이브러리와 함께 사용하기 편리하며, 복잡한 데이터 구조를 쉽게 만들 수 있다.

```tsx
import {z} from "zod";
const schema = z.object({
    name: z.string(),
    password: z.string(),
    rank: z.number()
});

type ExampleSchema = z.infer<typeof schema>;
```


`z.infer<typeof schema>`를 사용하면 타입을 추출 할수 있다.

이재 `validationSchema`를 작성 해보자.

## validationSchema 작성하기

먼저 `src/Form.tsx` 에서 종속성을 `import` 해야한다.

```console
import { z } from "zod";
import { SubmitHandler, useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
```

```tsx
// src/Form.tsx
import { z } from "zod";
import { SubmitHandler, useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";

const validationSchema = z.object({
    name: z
        .string()
        .min(1, {message: "이름은 필수 입력 항목입니다."}),
    email: z
        .string()
        .min(1, {message: "이메일은 필수 입력 항목입니다."})
        .email({message: "유효한 이메일 주소를 입력하세요."}),
    password: z
        .string()
        .min(8, {message: "비밀번호는 최소 8자 이상이어야 합니다."}),
    confirmPassword: z
        .string()
        .min(8, {message: "비밀번호 확인은 필수 입력 항목입니다."}),
    terms: z.literal(true, {
        errorMap: () => ({message: "약관 동의는 필수 입니다."});
    })
}).refine((data) => data.password === data.confirmPassword, {
    path: ["confirmPassword"],
    message: "비밀번호가 일치하지 않습니다.",
})

type ValidationSchema = z.infer<typeof validationSchema>;

const Form2 = () => {
// ...
```

zod는 `z.object()` 메소드를 사용하여 스키마를 정의 한다.

`z.string().min(1, {message: "이름은 필수 입력 항목 입니다."})` 는 문자열이며 최소 길이가 1이어야 한다는 것을 의미한다.

이메일 또한, `z.email()`로 쉽게 유효성 검사를 할 수 있다.

약관동의 같은 경우는 `z.literal()`로 검사한다. 
`z.literal()`은  필드가 정확히 이 값이어야 한다는 의미이며(약관 동의의 경우 무조건 true여야 함), 
`errorMap`에 오류 메세지를 정의 할 수 있다.

대략적으로 이정도면 스키마 정의는 이해 됬으리라 본다. 

하지만 비밀번호와 비밀번호 확인이 동일한지 검사를 해야 하는데 
먼저 위에 이메일과 이름처럼 최소길이로 기본 유효성 검사를 수행한 후, 

`refine()` 메소드를 통해 커스텀 유효성 검사 로직을 수행할 수 있다.

마지막으로 `type ValidationSchema`에 타입을 추출하여 가져오게 된다.

```typescript
// 타입이 추출된 type ValidationSchema 
type ValidationSchema = {
    name: string; 
    email: string;
    password: string;
    confirmPassword: string;
    terms: true
}
```

---

## React-Hook-Form에 곁들여 사용하기 

```tsx
const Form = () => {
    const {register, handleSubmit, formState: {errors}} = useForm<ValidationSchema>({
        resolver: zodResolver(validationSchema),
    });
    const onSubmit: SubmitHandler<ValidationSchema> = (data) => console.log(data);
//...
```
React-Hook-Form의 `useForm` 훅을 정의할때, 위에서 추출한 `ValidationSchema` 타입을 사용하으며, resolver를 통해 zod와 연결한다.

```tsx
const Form = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<ValidationSchema>({
    resolver: zodResolver(validationSchema),
  });
  const onSubmit: SubmitHandler<ValidationSchema> = (data) => console.log(data);
  return (
    <form className="space-y-3" onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="name"
        >
          이름
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="text"
          placeholder="이름을 입력하세요."
          {...register("name")}
        />
        
      </div>
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="email"
        >
          이메일
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="email"
          placeholder="이메일을 입력하세요."
          {...register("email")}
        />
      </div>
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="password"
        >
          비밀번호
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="password"
          placeholder="********"
          {...register("password")}
        />
      </div>
      <div>
        <label
          className="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="cPassword"
        >
          비밀번호 확인
        </label>
        <input
          className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="password"
          placeholder="********"
          {...register("confirmPassword")}
        />
      </div>
      <div>
        <input
          type="checkbox"
          id="terms"
          className="mr-2"
          {...register("terms")}
        />
        <label htmlFor="terms" className="text-sm font-bold text-gray-700">
          약관동의
        </label>
      </div>

      <div>
        <button className="w-full font-bold py-3 px-2 text-white bg-cyan-400 rounded-md ">
          Sign-Up
        </button>
      </div>
    </form>
  );
};

export default Form;
```

`useForm()`에서 불러온 register함수를 input에 동일한 이름으로 넣어준다.
`name`, `email`, `password`, `confirmPassword`, `terms`

---

## 에러 핸들링 하기

마지막 마무리 단계이다. 
아까 zod에 정의한 에러 메세지를 react-hook-form의 `errors`를 사용하여 에러메시지를 핸들링 해주면 된다.

```tsx

//...
<input
    className="w-full px-3 py-2 text-sm leading-tight text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
    type="text"
    placeholder="이름을 입력하세요."
    {...register("name")}
/>
{errors.name && (
    <p className="text-xs italic text-red-500 mt-2">
    {errors.name.message}
    </p>
)}
//...
```

![React-Hook-Form-With-Zod-Image-2](blog/react-hook-form-with-zod-img2.png)

에러 핸들링까지 완료 된것을 볼 수 있다.


### Conclusion

이 글에서는 기본적인 폼 유효성 검증만 해보았다.

React-Hook-Form + Zod는 무적이다.

더 강력한 기능도 많으니, 관심이 있다면 공식문서를 살펴보도록 하자.

[React-Hook-Form-Docs 바로가기](https://www.react-hook-form.com/)
[Zod Docs 바로가기](https://zod.dev/)
