---
title: '[디자인 패턴] 3. MVC, MVP, MVVM 패턴'
date: '2026-03-24'
tags:
  - MVC 패턴
  - MVP 패턴
  - MVVM 패턴
thumbnail: /assets/img/12/image1.png
---
__이글은 개인적인 공부를 위해 작성한 글이며 피드백주시면 수정하도록하겠습니다.(출처 : 면접을 위한 CS 전공지식 노트)
이미지 출처 : https://velog.io/@ilil1/안드로이드-MVVM-비교-MVP이란

----------------------------------------

MVC, MVP, MVVM 패턴은 UI(화면)와 비즈니스 로직(기능), 데이터 처리를 분리해서 관리하기 위한 패턴이다. 

지금부터 하나씩 알아보자!

<img src="/assets/img/12/image1.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

## MVC 패턴

**MVC 패턴**은 **Model, View, Controller**로 이루어진 디자인 패턴이다.

### 모델(Model)

**모델**은 데이터베이스, 상수, 변수 등을 의미한다.

예를 들어 사각형 모양의 박스안에 글자가 있다고 하자.

여기서 모델에 해당하는 것은 사각형 모양의 박스 위치 정보, 글자 내용, 글자의 위치, 글자의 포맷 등 관련된 정보를 모두 포함한다.

### 뷰(View)

**뷰**는 사용자 인터페이스에 해당하는 요소로 모델을 기반으로 사용자가 실제로 볼 수 있는 화면을 의미한다.

뷰는 모델이 가지는 정보들을 따로 저장하지 않고 오로지 화면에 표시되는 정보만 가지고 있다.

마약 뷰가 변경이 된다면 컨트롤러에게 전달하는 역할을 한다.

### 컨트롤러(Controller)

**컨트롤러**는 하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 하는 이벤트 등 메인 로직을 담당하는 요소이다.

모델과 뷰의 생명주기를 관리하며, 모델이나 뷰의 변경 통지를 받으면 이를 해석하여 각각의 구성요소에게 해당 내용을 알려준다.


MVC패턴을 사용하면 애플리케이션의 구성 요소를 세 가지 역할로 구분하여 개발 프로세스에서 각각의 구성요소에만 집중하여 개발이 가능하다.

따라서 재사용성과 확장성이 용이하다.

다만, 애플리케이션이 복잡해질수록 모델과 뷰의 관계가 복잡해진다.

스프링(Spring) 프레임워크는 대표적인 MVC 패턴을 이용한 프레임워크라고 할 수 있다.

한 줄로 요약하면, MVC 패턴은 컨트롤러가 입력을 받아 모델을 제어하고, 뷰를 갱신하는 구조를 가진다.


## MVP 패턴

**MVP 패턴**은 MVC 패턴에서 C가 프레젠터(P)로 변경된 패턴이다.

MVP 패턴은 MVC 패턴보다 더 강한 결합을 지닌 패턴이라고 할 수 있는데, 뷰가 오로지 프레젠터를 통해서만 동작하도록 한다.

뷰는 오직 UI 표시만 담당하고, 프레젠터가 대부분의 UI 로직을 처리한다.

MVC 패턴은 뷰도 어느정도 모델을 직접 참조할 수 있지만, MVP 패턴에서 뷰는 모델을 직접 알지 못하고 오로지 프레젠터를 통해서만 참조가 된다.

이로인해 뷰와 모델의 결합이 낮아지고 UI와 로직분리가 MVC 패턴보다 명확하다는 특징이 있다.


## MVVM 패턴

**MVVM 패턴**은 MVC 패턴에서 C가 뷰모델(VM)로 변경된 패턴이다.

여기서 뷰모델(View Model)은 뷰를 더 추상화한 계층이다.

MVVM 패턴은 **커맨드**와 **데이터 바인딩**을 가지는데, 이는 뷰와 뷰모델 사이의 양방향 데이터 바인딩을 지원한다.

커맨드는 여러가지 요소에 대한 처리를 하나의 액션으로 처리할 수 있게 하는 기법이고,

데이터 바인딩은 화면에 보이는 데이터와 웹브라우저의 메모리 데이터를 일치시키는 기법으로, 뷰모델을 변경하면 뷰가 변경되게 된다.(자동으로!)

MVVM 패턴은 UI를 별도의 코드 수정 없이 재사용 할수 있고, 단위 테스트에 유리하다는 특징을 가진다.



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
  const images = Array.from(document.querySelectorAll("img[src^='/assets/img/12/']"));
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
