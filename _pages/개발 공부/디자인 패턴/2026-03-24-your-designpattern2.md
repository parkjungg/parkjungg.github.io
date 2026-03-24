---
title: '[디자인 패턴] 2. 프록시 패턴, 이터레이터 패턴, 노출모듈 패턴'
date: '2026-03-24'
tags:
  - 프록시 패턴
  - 이터레이터 패턴
  - 노출모듈 패턴
thumbnail: /assets/img/11/image1.png
---
__이글은 개인적인 공부를 위해 작성한 글이며 피드백주시면 수정하도록하겠습니다.(출처 : 면접을 위한 CS 전공지식 노트)
이미지 출처 : https://refactoring.guru/ko/design-patterns

----------------------------------------

##프록시 패턴

**프록시 패턴**이란?

<img src="/assets/img/11/image2.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

실제 객체에 직접 접근하지 않고, 그 앞에 대리인 객체(프록시)를 두어 접근을 제어하거나 추가 기능을 수행하도록 하는 패턴

클라이언트에서 바로 서버로 접근하는 것이 아닌, 프록시 서버로 먼저 간 후 실제 서버로 접근하는 것이다.

한번 우회한다고 생각하면 된다.

프록시 패턴은 보통 권한 확인, 보안, 데이터 검증, 캐싱, 로깅 등에 사용된다.

프록시 패턴이 사용되는 **프록시 서버**는 서버와 클라이언트 사이에서 클라이언트가 프록시 서버를 통해 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 시스템이나 응용프로그램을 말한다.

프록시 패턴은 보통 보안을 위해 사용하는 경우가 많다!

장점으론 접근 제어가 가능하고, 실제 객체에 직접 접근을 막고, 프록시를 통해서만 안전하게 접근이 가능해 보안적으로 좋다.

다만 구조가 복잡하고, 많이 쓰면 흐름 추적이 어렵다...


##이터레이터 패턴

<img src="/assets/img/11/image2.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

이터레이터 패턴은 말그대로 이터레이터(반복자)를 이용하여 컬렉션의 요소들에 접근하는 패턴이다.

여러가지 자료형의 구조와는 상관없이 이터레이터라는 하나의 인터페이스로 컬렉션의 요소에 접근할 수 있다.


##노출모듈 패턴

노출 모듈패턴은 즉시 실행되는 함수를 통해 private, public 같은 접근 제어자를 만드는 패턴이다.

여기서 즉시 실행 함수란, 함수를 정의하자마자 따로 호출하지 않아도 바로 호출되는 함수를 말한다.

라이브러리 내 전역 변수의 충돌을 방지하는 등에 사용되곤 한다.


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
  const images = Array.from(document.querySelectorAll("img[src^='/assets/img/11/']"));
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
