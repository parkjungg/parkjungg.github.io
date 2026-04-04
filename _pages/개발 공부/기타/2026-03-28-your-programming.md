---
title: '[프로그래밍 패러다임] 1. 객체지향 프로그래밍과 절차지향 프로그래밍'
date: '2026-03-28'
tags:
  - 객체지향 프로그래밍
  - SOLID 원칙
  - 절차지향 프로그래밍
thumbnail: /assets/img/13/image1.png
---
__이글은 개인적인 공부를 위해 작성한 글이며 피드백주시면 수정하도록하겠습니다.(출처 : 면접을 위한 CS 전공지식 노트)

이미지 출처 : https://www.freepik.com

----------------------------------------

## 프로그래밍 패러다임

<img src="/assets/img/13/image1.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

프로그래밍 패러다임은 프로그래머에게 프로그래밍의 관점을 갖게 해주는 역할을 하는 개발 방법론을 말한다.

대표적으로 객체지향, 절차지향 프로그래밍이 있다.

하나씩 알아보자!!😀


## 1. 객체지향 프로그래밍(Object Oriented Programming)

**객체지향 프로그래밍**이란?

객체들의 집합으로 프로그램의 상호작용을 표현하며 데이터를 객체로 취급하여 객체 내부에 선언된 메서드를 활용하는 방식을 말한다.

객체지향 프로그래밍은 설계에 많은 시간이 소요되며 처리 속도가 다른 프로그래밍 패러다임에 비해 상대적으로 느린 특징을 가지고 있다.

객체지향 프로그래밍은 4가지의 특징을 가진다.

1. 추상화 : 복잡한 시스템으로부터 핵심적인 개념 또는 기능을 간추려내는 것을 의미
2. 캡슐화 : 객체의 속성과 메서드를 하나로 묶고 일부를 외부에 감추어 은닉하는 것
3. 상속성 : 상위 클래스의 특성을 하위 클래스가 이어받아서 재사용하거나 추가 및 확장하는 것 → 코드의 재사용 측면과 유지보수성 측면 에서 매우 중요
4. 다형성 : 하나의 메서드나 클래스가 다양한 방법으로 동작하는 것
→ 오버로딩 : 같은 이름을 가진 메서드를 여러 개 두는 것(정적 다형성)
→ 오버라이딩 : 상위 클래스로부터 상속받은 메서드를 하위 클래스가 재정의하는 것(동적 다형성)


### SOLID 원칙

객체지향 프로그래밍을 설계할 때는 **SOLID** 원칙을 지켜야한다!!

이는 객체 지향 설계를 더 유연하고, 유지보수하기 쉽게 만들기 위한 5가지 원칙이다.

1. 단일 책임 원칙(SRP) : 모든 클래스는 각각 하나의 책임만을 가져야 하는 원칙 → A라는 로직이 있다면 어떠한 클래스는 A에 관한 클래스여야 하고 이를 수정한다고 했을 때도 A와 관련된 수정이어야 한다.

2. 개방-폐쇄원칙(OCP) : 유지보수 사항이 생긴다면 코드를 쉽게 확장할 수 있도록하고 수정할 때는 닫혀있어야 하는 원칙 → 기존의 코드는 잘 변경하지 않으면서도 확장은 쉽게 할 수 있어야한다.

3. 리스코프 치환원칙(LSP) : 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위타입의 인스턴스로 바꿀 수 있어야하는 것 → 부모 자식 관계에서 부모 객체에 자식 객체를 넣어도 시스템이 문제없이 돌아가게 만드는 것

4. 인터페이스 분리 원칙(ISP) : 하나의 일반적인 인터페이스보다 구체적인 여러 개의 인터페이스를 만들어야하는 원칙

5. 의존 역전 원칙(DIP) : 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변하기 쉬운 것의 변화에 영향받지 않게 하는 원칙 → 상위 계층은 하위 계층의 변화에 대한 구현으로부터 독립해야한다.

이렇게 5가지의 원칙을 지키면서 객체지향 프로그래밍을 설계해야한다😀


## 2. 절차지향 프로그래밍

절차지향 프로그래밍은 수행되어야 할 연속적인 계산 과정으로 이루어진다.

코드의 가독성이 좋고, 실행 속도가 객체 지향에 비해 빠르다.

단, 모듈화 하기 어렵고 유지 보수성이 떨어진다는 단점이 있다.

그래서 대부분 객체지향 프로그래밍을 하는 경우가 많다!

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
  const images = Array.from(document.querySelectorAll("img[src^='/assets/img/13/']"));
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
