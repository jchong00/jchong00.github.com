---
layout: post
title: Java Concurrent Programming - Overview
subtitle: About Java Concurrent Programming, Overview page
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [java]
comments: true
---
# 경고
현재 이글은 블로그 이전을 위해서 작성되고 있습니다. 테스트용 문구이오는 해당 내용을 찾으로 오신 분들의 저자의 현재 HOME으로 가서 자료를 찾으시기 바랍니다.
# 프롤로그

<p style='text-align: justify;'>
프로그램밍이라는 것을 시작한 이래로 늘 무겁게 다가오는 주제가 Multi-Thread였다. 어떤 언어로 하던간에 어렵고 난해    했다. 그렇기에 늘 내가 알고 하고있구나 하는 느낌 보다는 어디서 주섬 주섬 주워온 코드로 현실에 Issue들을 해결하기급급 했다. 헌데 지금은 양상이 다르다. 서버 프로그램밍을 하고 있는 시점에 "아 됐어, 돌아가!" 그리고 다음진도를    빼기에는 너무 불안하다. 사실 이 글을 쓰기전에 atomicReference와 atomicStampedReference등의    자바 Class를 이용한 기술 단편을 정리해서 글을 작성 했는데 내가 이거 뭐 알고 쓰고 있는거야 하는 자책감에 차마    공개하지 못하고 모든 진도와 계획을 멈추고 책과 자료를 찾아 뒤졌다. 자료를 하루 이틀 찾다 보니 그간 내가 정말 개념 없이 volitile, atomic을 운운 했구나 하는 생각이 들었다. 약 일주일의 시간이 긴 터널 같이 느껴질 정도로 간만에 정말 열심히 공부 했다. 더 나가기 전에 이 글을 이해하려면 적어도 Thread가 뭔지는 알아야 한다. 그렇지 못한 독자가 있다면 잠시 다른 자료를 통해 개념이라도 이해 하고 다시 돌아오시기 바란다.
</p>
<p style='text-align: justify;'>
이번 글에서는 Multi-Thread와 이를 다루는 과정의 기초가 되는 가시성과 원자성을 정의해 보도록 하겠다. 사실 가시성과 원자성이라고 하는 단어는 문제를 해결하기 위한 원칙(?)이다. 바꿔 말해 Multi-Thread를 구성하다 보니 비 가시성 비 원자성 문제가 발생 했고 Muti-Thread를 문제 없이 사용하려면 가시성과 원자성을 확보해야 한다. 이렇게 정의 할 수 있다. 필자가 이야기 하는 "~해야 한다."가 비단 개발자의 노력만으로는 이루어 질수 없음을 먼저 밝혀둔다. (CPU, OS, JVM 등이 지원을 해야한다는 말이다.) 참 노파심에서 집고 넘어가는데 가시성과 원자성은 여러 Thread가 동시에 접근이 가능한 공유변수에 대한 이야기다. Thread을 많이 작성해봤지만 이런 내용는 금시초문이다 하는 분들은 아마도 각각의 Thread가 각각의 변수만을 다루는 격리된 설계상에서 구현된 프로그램이였을 것이라 상상해본다.
</p>


![repsimg_20190905](https://jchong00.github.io/img/multi-cpu-archi.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5MzkxODQ3OV19
-->
