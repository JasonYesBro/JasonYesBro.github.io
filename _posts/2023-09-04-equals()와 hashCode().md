---
title: equals(), hashCode()는 왜 같이 재정의해야 할까?
author: snghyun
date: 2023-09-04 <!-- 커맨드 + h -->
categories: [Blogging, Java] <!-- 카테고리의 첫번째는 대문자로 시작 -->
tags: [객체비교] <!-- ,로 구분 -->
---

이클립스에서 equals()메서드를 overriding 자동완성기능을 사용하던 도중 equals()와 hashCode()는 같이재정의 하게끔 되어있는데 이유가 궁금하여 찾아보고 정리하게 되었다.

## equals()
```
객체안의 String값을 비교한다.
인자값은 null 값이 오면 안된다.
해당 객체의 문자들의 열거들이 같은지를 보여준다.
```


hashCode() 와 equals()를 함께 재정의하지 않으면 코드가 예상과 다르게 작동한다.
정확히 말해서 hash값을 사용하는 Collection(HashSet, HashMap, HashTable)객체를 사용할 때 문제가 발생한다.

### 왜 이런 문제가 발생하지?

hash값을 사용하는 Collection 은 객체가 논리적으로 같은지 비교할 때 아래와 같은 과정을 거친다.

1. hashCode() 리턴 값
	1. 다름 -> false -> 다른객체
2. 같음
	1. equals() 리턴값
		1. 다름 -> false -> 다른객체
3. 같음
	1. 동등한 객체
![image](https://github.com/JasonYesBro/JasonYesBro.github.io/assets/126242681/367cece7-4d29-4dcc-9da7-bf72ca006042)