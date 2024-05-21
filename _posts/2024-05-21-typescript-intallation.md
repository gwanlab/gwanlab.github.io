---
layout: post
title: React-Hook-Form에 Zod를 곁들여 유효성 검증하기
author: K
date: 2024-05-21 18:21:00 +09:00
categories: [Typescript]
tags: [Typescript]
render_with_liquid: false
comments: true
image: 
    path: /blog/typescript.webp
    alt: Typescript
---


# Typescript 1편 설치 및 환경설정

![Typescript](blog/typescript.webp)

---

## Introduction

타입스크립트 코드를 작성한다 라는 의미는 결과적으로 자바스크립트 코드를 작성하는 것 이다.

다만 타입스크립트에서는 타입 시스템을 다루기 위한 문법이 추가될 뿐이며,

타입 시스템은, 개발 할때의 오류를 잡아내기 위해 사용한다.

또한 실제로 실행할 때에는, 타입스크립트 파일이 먼저 컴파일되어 JS 코드로 변환되며, 변환된 JS파일이 실행된다.

브라우저에서 실행할 코드에는 아무런 영향을 주지않으며, 결국 브라우저는 자바스크립트를 읽는다.

타입스크립트는 작성하는 코드에 오류가 있는지 확인 해줄 뿐, 코드 성능 최적화 등의 효과가 있지는 않다.

---

## Installation


```terminal
npm install -g typescript ts-node
```

typescript와 ts-node를 글로벌 모듈로 설치한다.

ts-node는 명령어 하나로 ts 파일을 컴파일하고 실행하는데 사용하는 녀석이다.

설치가 완료되었다면,  터미널에서 아래 명령어를 입력 해보면 성공적으로 설치되었는지 알 수 있다.

```terminal
tsc --help
```


## Usage


```console
ts-node [file-name.ts]
```