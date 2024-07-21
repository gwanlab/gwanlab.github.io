---
layout: post
title: HTML Semantic Tag, 제대로 알고 사용하자
author: K
date: 2024-07-22 04:30:00 +09:00
categories: [html]
tags: [html, SemanticTag]
render_with_liquid: false
comments: true
image: 
    path: /blog/html.webp
    alt: html-image
---


# HTML Semantic Tag, 제대로 알고 사용하자

![html](blog/html.webp)

---

HTML의 Semantic Tag를 용도에 맞게 알고 사용 하면, SEO 개선과 접근성 향상 등의 효과가 있다.

## header

* 용도: 페이지나 섹션의 헤더를 나타낸다.

### Example

```html
<header>
	<h1>GOOD COMPANY</h1>
	<nav>
		<ul>
			<li><a href="#home">홈</a></li>
			<li><a href="#about">소개</a></li>
		</ul>
	</nav>
</header>
```

---

## nav

* 용도: 주요 네비게이션의 링크를 포함

### Example

```html
<nav>
	<ul>
		<li><a href="#services">서비스</a></li>
		<li><a href="#products">제품</a></li>
		<li><a href="#contact">연락처</a></li>
	</ul>
</nav>
```

---

## main

* 용도: 페이지의 주요 콘텐츠를 나타낸다.

### Example


```html
<main>
	<h1>Welcome!</h1>
	<p>저희 제품을 소개합니다.</p>
</main>
```

---

## article

* 용도: 독립적으로 구분되거나 재사용 가능한 콘텐츠를 나타낸다. 보통 블로그 글, 댓글 등으로 활용

### Example


```html
<article>
	<h1>공지사항 전달 드립니다</h1>
	<p>네 공지사항은 사실 없습니다.</p>
</article>
```

---

## section

* 용도: 문서의 일반적인 섹션을 나타낸다.
 
### Example

```html
<section>
	<h2>회사 소개</h2>
	<p>우리 회사는 좋은 회사입니다.</p>
</section>
```

---

## aside

* 용도: 주요 콘텐츠와 간접적으로 연관된 보조 콘텐츠를 나타낸다. (보통 사이드바.)

### Example

```html
<aside>
	<h3>관련 링크</h3>
	<ul>
		<li><a href="#news">최신 뉴스</a></li>
		<li><a href="#events">이벤트</a></li>
	</ul>
</aside>
```

---

## footer

* 용도: 페이지나 섹션의 푸터를 나타낸다.

### Example


```html
<footer>
	<p>&copy; 2024 elcode. all rights reserved.</p>
	<address>
		연락처: <a href="mailto:admin@elcode.co.kr">admin@elcode.co.kr</a>
	</address>
</footer>
```

---

## figure, figurecaption

* 용도: 이미지와 그 설명을 그룹화 하는 용도이다.

### Example

```html
<figure>
	<img src="/img/test-img.png" alt="신제품 이미지" />
	<figcaption>그림1: 엄청난 신제품 이미지</figcaption>
</figure>
```
---

## time

* 용도: 날짜나 시간을 나타낸다. 

### Example 

```html
<p>제품 출시일: <time datetime="2024-07-21">2024년 07월 21일</time></p>
```

---

## mark

* 용도: 텍스트를 강조 할 때 사용한다.

### Example

```html
<p>이번 주 <mark>특별 할인</mark> 상품을 확인해보세요.</p>
```

---

## detail, summary 

* 용도: 아코디언(열고 닫는 그 녀석)으로 상세정보를 제공하는데 쓰인다.

### Example 

```html
<details>
	<summary>제품 상세 정보</summary>
	<p>이 제품은 엄청납니다..</p>
</details>
```

---

## address

* 용도: 연락처 정보를 나타낸다.

### Example 

```html
<address>
	작성자: <a href="mailto:admin@elcode.co.kr">홍길동</a><br>
	사랑시 고백구 행복동 123
</address>
```

---

## Conclusion

* 시멘틱 태그를 적절히 사용하여 SEO 개선과 접근성을 향상 시켜보자.
* 시멘틱의 의미에 맞게 사용하고, `남용` 하지 말자.
* 모든 주요 섹션에는 적절한 제목 태그(h1~h6)를 할당하자.
* aria 속성을 활용하면 접근성을 더 향상 시킬 수 있다.

<br>  

#### 관련문서

[W3C-SCHOOLS-SEMANTIC-ELEMENTS](https://www.w3schools.com/html/html5_semantic_elements.asp)

[MDN-WEB-DOCS ARIA](https://developer.mozilla.org/ko/docs/Web/Accessibility/ARIA)