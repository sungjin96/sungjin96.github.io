---
layout: post
title:  "애자일의 단일 책임 원칙 (SRP)"
date:   2021-08-07 20:58:36 +0530 
tags: 애자일 단일책임원칙 SRP
categories : [애자일]
---

애자일의 원칙중에 단일 책임 원칙에 대해서 기록할려고 한다.

단일 책임 원칙이란 한 클래스에서는 한 가지의 변경 이유만 가져야 한다. 밑에 예시코드를 살펴 보자.

```java
class Circle {
    private int radius;

    Circle(int radius) {
        this.radius = radius;
    }

    public void setRadius(int radius) {
        this.radius = radius;
    }

    public int getRadius() {
        return this.radius;
    }

    public void paint() {
        // paint code
    }

    public getRound() {
        // round code
    }

    public getArea() {
        // area code
    }
}
```

위 Circle 이라는 클래스는 원을 그리고 원의 둘레, 넓이를 계산하는 기능을 가지고 있는 간단한 클래스 이다.

이때, Circle 은 크게 두가지 책임을 가지고 있다고 생각할 수 있다. 첫번째 책임은 원을 그려주는 책임 두번째 책임은 둘레, 넓이를 계산하주는 책임을 가지고 있는 것이다.

만약 단일 책임 원칙 즉, SRP 를 지킨다면 다음 처럼 작성을 할 수 있을 것이다.

```java
interface Draw {
    public void paint();
}

interface Calculate {
    public getRound(int radius);

    public getArea(int radius);
}

class Circle {
    private Draw draw;
    private Calculate calculate;

    public void setCalculate(Calculate calculate) {
        this.calculate = calculate;
    }

    public void setDraw(Draw draw) {
        this.draw = draw;
    }

    public Draw getDraw() {
        return draw;
    }

    public Calculate getCalculate() {
        return calculate;
    }

    public void paint() {
        draw.paint();
    }
}
```

내가 잘 이해한 대로 코드를 작성하면 위 코드처럼 작성을 할 수 있을꺼 같다.

예시코드를 봤는데 굳이 저렇게 클래스를 안나누는게 java 파일도 작은데 할 필요가 있을까? 라고 생각이 들기도 한다. 그런데 갑자기 원 뿐만 아니라 직사각형, 다각형 등등이 추가가 된다고 했을때, 첫번째 예시
코드였으면 어떻게 됐을까!? 거기까지는 일반 코더들 처럼 그냥 복붙하고 코드 구현하면 되기는 할 것이다. 하지만 그렇게 도형들이 추가되고 추가되고 추가되서 100만개를(~~극단적이게..~~) 만들었는데 갑자기 화면
그리는것 뿐 아니라 지우는 기능이 추가가 됐다고 하면 100만개의 클래스에 추가를 해야할 것이다. 수정 하다보면 실수로 인한 예상치 못한 방식으로 잘못 동작할 수 도 있다.

하지만 만약 하나의 클래스에서 무조건 두개의 책임의 변경을 유발하게 된다면 이들을 불리할 필요가 없다. 분리하게 된다고 하면 불필요하게 복잡해지게 될 것이다.

## 이때, 책임이란 무엇일까?

위에서 계속 언급되는 책임이란 무엇일까? 클린 소프트웨어라는 책에서는 **변경을 위한 이유**로 정의한다고 나와 있다. 여기서 우리는 변경을 위한 이유가 무엇인지에 대해서 많은 고민이 필요하다고 생각한다. 사람들마다
생각이 다르고 그리고자 하는 그림이 다르기 때문이다. 물론 위에 예시처럼 단순한 경우라면 다르겠지만 만약 복잡한 클래스라면 의견이 다를 수 도 있기 때문이다.

내가 생각하는 변경을 위한 이유는 하나의 카테고리 라고 생각을 한다. 위 예시 코드를 보면 하나는 그리기라는 카테고리 다른 하나는 계산이라는 카테고리라고 생각 할 수 있다. 주문이라는 클래스가 있다고 생각하면 할인 계산, 주문 계산, 결제 수단 등등의
카테고리를 생각할 수 있을 것이다.

## 결론
내가 맞게 이해를 한 것인지는 나도 모르겠다. 하지만 스타트업에서 혼자 개발자로서 일을 하다보면 많은 어려움과 답답함이 존재한다. 기능 구현 자체는 어렵지 않지만 설계와 좋은 코드라는 주제에서는 많은 고민을 해왔다.
물론 위에 안좋은 예시처럼 무작정 코드를 한 클래스에 쭉 작성할 때도 있었지만 계속 바뀌는 기능과 추가되는 기능에 맞추어 수정할 때마다 과거의 나 자신을 욕하고는 헀다.
앞으로도 더 많은 고민을 하게 될 것이다. 

SRP는 가장 지키기 어려운 원칙이라고 생각한다. 개발을 진행하다 보면 어느 순간 한 클래스에 너무 많은 책임이 존재하게 되는 경우가 참 많았다. 하지만 가장 중요한 원칙이라고도 생각한다.


## 참고

- 클린 소프트웨어
