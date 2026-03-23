---
title: '[디자인 패턴] 1. 싱글톤 패턴, 팩토리 패턴, 전략 패턴, 옵저버 패턴'
date: '2026-03-23'
tags:
  - 싱글톤 패턴
  - 팩토리 패턴
  - 전략 패턴
  - 옵저버 패턴
thumbnail: /assets/img/10/image1.png
---
__이글은 개인적인 공부를 위해 작성한 글이며 피드백주시면 수정하도록하겠습니다.(출처 : 면접을 위한 CS 전공지식 노트)

# 디자인 패턴

**디자인 패턴이란?**

프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계등을 이용하여 해결할 수 있도록 하나의 '규약' 형태로 만들어 놓은 것을 말한다.

<img src="/assets/img/10/image1.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

이처럼 디자인 패턴은 프로그램을 만들 때 여러 구조에서 사용된다.
여러가지의 디자인 패턴이 존재하며, 상황에 따라 다른 디자인 패턴이 사용되곤 한다.

하나씩 알아보자!! 😀

## 싱글톤 패턴

싱글톤 패턴은 프로그램을 설계할 때 자주 사용되는 디자인 패턴이다.

싱글톤 패턴이란.. 

**하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴** 

<img src="/assets/img/10/image2.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

하나의 인스턴스를 만들어 놓고, 해당 인스턴스를 다른 모듈들이 공유하며 사용할 수 있다

그래서 인스턴스를 하나만 만들기 때문에 인스턴스를 생성할 때의 비용이 줄어드는 장점이 있다.

다만, 그 인스턴스에만 의존성이 높아지는 단점이 생기고, TDD(Test Driven Development)을 할 때 문제가 생긴다.

왜냐하면 TDD를 할 때는 단위 테스트를 주로 하는데, 단위 테스트는 테스트가 서로 독립적이어야하며 테스트를 어떤 순서로든 실행할 수 있어야한다.

싱글톤 패턴은 미리 생성된 하나의 인스턴스를 기반으로 구현하는 패턴이기에 각 테스트마다 '독립적인' 인스턴스를 만들기가 어렵다.

그래서 이를 해결하기위해 하나의 해결책을 사용한다.

### 의존성 주입

그건 바로 의존성을 주입하는 것!

싱글톤 패턴은 모듈간의 결합을 강하게 만들 수 있기 때문에 의존성 주입을 통해 모듈 간의 결합을 조금 느슨하게 만들 수 있다.

여기서 의존성이 있다는 것은, A와 B가 의존성이 있다고 할 때, B가 변하면 A또한 변해야한다는 것이다.

그런데 의존성 주입을 메인 모듈이 직접 다른 하위 모듈에 의존성을 주기보다는 중간에 '의존성 주입자'가 의존성을 주입하여 메인 모듈이 **간접적**으로 의존성을 주입하는 방식을 사용한다.

의존성 주입의 장점으로는.. 

모듈들을 쉽게 교체가 가능하여 테스팅하기 쉽고 마이그레이션하기가 수월하다!

또한 모듈간의 관계들이 좀 더 명확해진다.

의존성 주입의 단점으로는 모듈이 더욱 분리되어 클래스 수가 늘어나 복잡성이 증가될 수 있고, 런타임 페널티가 생길 수도 있다.

의존성 주입을 할 때는 원칙이 존재하는데,

상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야하고, 둘다 추상화에 의존해야한다.

그리고 추상화는 세부 사항에 의존하지 말아야한다.


## 팩토리 패턴

<img src="/assets/img/10/image3.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

팩토리 패턴이란..?

**객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴**

이게 무슨 소리일까?

정의만 보면 좀 어렵다..😅

좀 더 풀어보면, 객체를 직접 생성하지 않고, 객체 생성을 하는 로직을 별도의 **공장**에 맡기는 패턴이다.

상속 관계에 있는 두 클래스인 부모 자식 관계에서, 상위 클래스인 부모가 중요한 뼈대를 정하고, 하위 클래스인 자식이 객체 생성에 관한 구체적인 내용을 결정한다.

예를 하나 들어보자

커피 공장이 하나있고, 여기 공장에서 라떼, 아메리카노, 우유 레시피를 가진 하위클래스가 있다. 즉, 상위 클래스인 커피 공장에서 하위 클래스인 저 셋의 레시피를 이용해 만드는 것이다.

팩토리 패턴은 객체 생성과 사용을 분리할 수 있고, 결합도가 감소하며 확장에 유리하다!

다만 클래스 및 구조가 늘어나서 복잡해지고, 새로운 타입 추가 시에 팩토리 수정이 필요하다.


## 전략 패턴

전략 패턴은 **알고리즘(행동 방식)을 각각 별도의 클래스로 분리하고, 실행 중에 필요한 알고리즘을 교체해서 사용할 수 있게 하는 패턴**이다. 

<img src="/assets/img/10/image4.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

무엇을 할지는 같지만, 어떻게 할지는 상황마다 다를 때 **어떻게**를 따로 빼서 교체 가능하게 만드는 것이라 할 수 있다.

전략 패턴은 런타임에도 행동 교체가 가능하고, 새 전략을 추가할 때 기존 코드를 수정하는 것을 최소화할 수 있다
그리고 테스트하기도 쉽다!

다만, 클래스 수가 많아지고 구조가 복잡해지는 문제는 어쩔 수 없다...(복잡한 건 해결 못하나..?😂)


## 옵저버 패턴

**옵저버 패턴은 말 그대로 주체가 어떤 객체의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 패턴**이다.

<img src="/assets/img/10/image5.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

대표적인 예로 X(트위터)가 있다.

어떤 한사람(주체)을 팔로우하면 본인(옵저버)은 팔로워가 된다. 그리고 그 팔로우한 대상(주체)이 글을 올리면 모든 팔로워들(옵저버들)에게 글을 올렸다는 알림이 가게된다.

옵저버 패턴은 주로 이벤트 기반 시스템에 사용하고, 추후 알아볼 MVC 패턴에도 사용된다.

보통 하나의 이벤트를 여러 객체가 **동시**에 반응해야할 때 사용하고, UI, 알림, 게임 이벤트, 상태 변화 전파에 이용한다.

옵저버 패턴의 장점으로는 결합이 느슨하고, 확장성이 좋다

즉, 주체와 옵저버 간 결합도를 낮추면서, 이벤트 기반 구조를 유연하게 설계할 수 있다.

단점으로는 옵저버가 많아지면 관리가 복잡해지고, 디버깅이 힘들어진다.



<!-- ================= Lightbox Modal ================= -->

<style>
#lightbox-modal {
  display: none;
  position: fixed;
  z-index: 9999;
  inset: 0;
  background: rgba(0, 0, 0, 0.85);
  justify-content: center;
  align-items: center;
}

#lightbox-modal img {
  max-width: 90%;
  max-height: 85%;
  width: auto;
  height: auto;
  object-fit: contain;
  border-radius: 12px;
  box-shadow: 0 10px 40px rgba(0,0,0,0.5);
}

.lightbox-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 40px;
  color: white;
  cursor: pointer;
  user-select: none;
  padding: 20px;
}

#prev-btn { left: 20px; }
#next-btn { right: 20px; }

#close-btn {
  position: absolute;
  top: 20px;
  right: 30px;
  font-size: 35px;
  color: white;
  cursor: pointer;
}
</style>

<div id="lightbox-modal">
  <span id="close-btn">&times;</span>
  <span id="prev-btn" class="lightbox-btn">&#10094;</span>
  <img id="lightbox-image">
  <span id="next-btn" class="lightbox-btn">&#10095;</span>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
  const images = Array.from(document.querySelectorAll("img[src^='/assets/img/10/']"));
  const modal = document.getElementById("lightbox-modal");
  const modalImg = document.getElementById("lightbox-image");
  const closeBtn = document.getElementById("close-btn");
  const prevBtn = document.getElementById("prev-btn");
  const nextBtn = document.getElementById("next-btn");

  let currentIndex = 0;

  function showImage(index) {
    currentIndex = index;
    modalImg.src = images[currentIndex].src;
    modal.style.display = "flex";
  }

  images.forEach((img, index) => {
    img.style.cursor = "zoom-in";
    img.addEventListener("click", function(e) {
      e.preventDefault();
      showImage(index);
    });
  });

  closeBtn.onclick = () => modal.style.display = "none";

  prevBtn.onclick = () => {
    currentIndex = (currentIndex - 1 + images.length) % images.length;
    showImage(currentIndex);
  };

  nextBtn.onclick = () => {
    currentIndex = (currentIndex + 1) % images.length;
    showImage(currentIndex);
  };

  modal.onclick = (e) => {
    if (e.target === modal) modal.style.display = "none";
  };
});
</script>

<!-- ================================================== -->
