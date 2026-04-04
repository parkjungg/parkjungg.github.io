---
title: '[네트워크] 1. 네트워크의 기초'
date: '2026-04-04'
tags:
  - 네트워크
  - 네트워크 토폴로지
  - 병목 현상
  - 네트워크 성능 분석
thumbnail: /assets/img/14/image1.png
---
__이글은 개인적인 공부를 위해 작성한 글이며 피드백주시면 수정하도록하겠습니다.(출처 : 면접을 위한 CS 전공지식 노트)

----------------------------------------


## 네트워크의 기초

<img src="/assets/img/14/image1.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

**네트워크**란?

컴퓨터 등의 장치들이 통신 기술을 이용하여 구축하는 연결망을 지칭하는 용어를 말한다.

네트워크는 노드와 링크가 서로 연결되어 있으며, 리소스를 공유하는 집합이라고 볼 수 있다.

좋은 네트워크는 많은 **처리량**을 처리할 수 있으며, **지연시간**이 짧고 **장애빈도**가 적으며, **좋은 보안**을 갖춘 네트워크를 말한다.

네트워크를 구성할 때 항상 위에 사항들을 고려하며 구성해야 한다.

네트워크에는 여러가지 용어들이 존재하는 데 이를 먼저 간단히 알아보자!

**노드** : 서버, 라우터, 스위치 등의 네트워크 장비

**링크** : 유선 또는 무선의 연결

**처리량** : 링크 내에서 성공적으로 전달된 데이터 양을 말하며, 얼만큼의 트래픽을 처리했는지를 의미한다.
단위는 bps(bits per second)를 사용하고, 이는 초당 전송 또는 수신되는 비트 수를 말한다.
처리량은 트래픽, 네트워크 장치 간의 대역폭, 에러, 하드웨어 스펙에 영향을 받는다.

**대역폭** : 주어진 시간 동안 네트워크 연결을 통해 흐를 수 있는 최대 비트 수

**지연 시간** : 요청이 처리되는 시간, 즉 어떤 메시지가 두 장치 사이를 왕복하는 데 걸린 시간을 말한다.


## 네트워크 토폴로지

**네트워크 토폴로지**는 노드와 링크가 어떻게 배치되어있는지 나타내는 연결 형태를 말한다.

종류는 다음 이미지 처럼 5가지가 있다. 

<img src="/assets/img/14/image2.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

### 트리 토폴로지

위에 이미지처럼 트리 형식의 네트워크 구성으로 된 토폴로지이다.

트리 토폴로지는 노드의 추가 및 삭제가 쉽고, 특정 노드에 트래픽이 집중될 때 하위 노드에 영향을 끼칠 수 있다.

### 버스 토폴로지

**버스 토폴로지**는 중앙 통신 회선 하나에 여러 개의 노드가 연결되어 공유하는 네트워크이다.

보통 근거리 통신망(LAN)에서 사용되고, 설치 비용이 적으며 신뢰성이 우수하고 회선에 노드를 추가하거나 삭제하기 쉬운 장점이 있다.

단, **스푸핑**이 가능한 문제점이 존재한다.

여기서 **스푸핑**이란, LAN상에서 송신부의 패킷을 송신과 관련없는 다른 호스트에 가지 않도록 하는 스위칭 기능을 마비시키거나 속여서 특정 노드에 해당 패킷이 오도록 하는 것을 말한다. 

쉽게 말해, 패킷을 가로채서 내가 원하는 노드에 패킷을 보내도록 하는 것이다!

### 스타 토폴로지

**스타 토폴로지**는 중앙에 있는 노드에 모두 연결된 네트워크 구성이다.

이는 노드를 추가하거나 에러를 탐지하기 쉽고, 패킷의 충돌 발생 가능성이 적다.

또한, 장애 노드가 중앙 노드가 아니면, 다른 노드에 영향을 끼치는 것이 적은 장점이 있다.

다만, 중앙 노드에 장애가 발생하면 전체 네트워크를 사용할 수 없고 설치하는 데 비용이 비싸다는 단점이 존재한다😅

### 링형 토폴로지

**링형 토폴로지**는 각각의 노드가 양옆의 두 노드와 연결하여 전체적으로 고리처럼 하나의 연속된 길을 통해 통신하는 구성이다.

이는 노드 수가 증가되어도 네트워크 상의 손실이 거의 없고 충돌이 발생되는 가능성이 적으며 노드의 고장 발견을 쉽게 찾을 수 있다는 장점이 있다.

그러나 네트워크 구성 변경이 어렵고 회선에 장애가 발생하면 전체 네트워크에 영향을 끼친다.

### 메시 토폴로지

**메시 토폴로지** 그물망처럼 연결되어 있는 구성이다.

한 단말 장치에 장애가 발생하더라도 여러 개의 경로가 존재하기때문에 네트워크를 계속 사용할 수 있고, 트래픽 분산 처리가 가능하여 처리량을 올릴 수 있다.

하지만 노드의 추가가 어렵고 구축 비용과 운용하는 비용이 비싸다.



그럼 왜 네트워크 토폴로지가 중요하냐면.. 

바로 토폴로지를 확인하여 **병목 현상**을 해결할 수 있기 때문이다!!

여기서 **병목 현상**이란..

전체 시스템의 성능이나 용량이 하나의 구성요소로 인해 제한을 받는 현상을 말한다.

<img src="/assets/img/14/image3.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     "> 

위의 이미지처럼 아래가 막혀서 위에가 빠져나갈 수 없는 걸 생각하면 쉽다!!

그래서 토폴로지를 보면 트래픽이 집중되는 경로와 장애 지점을 유추할 수 있다.

이를 보고 대역폭 확장, 경로 분산, 구조 개선등과 같은 해결책을 적용할 수 있다.


## 네트워크의 분류

네트워크는 규모를 통해서 분류가 가능한데, LAN, MAN, WAN으로 나눌 수 있다.

1. **LAN(Local Area Network)** : 근거리 통신망, 같은 건물이나 캠퍼스와 같은 좁은 공간에서 주로 운영한다. 이는 전송 속도가 빠르고 혼잡하지 않다. 

2. **MAN(Metropolitian Area Network)** : 대도시 지역의 네트워크이며, 도시 같은 넓은 지역에서 운영하고, 전송 속도는 LAN보다는 느리다.

3. **WAN(Wide Area Network)** : 광역 네트워크이며, 국가 또는 대륙에서 운영한다. 전송 속도는 느리고, MAN보다 혼잡하다. 


## 네트워크 성능 분석 명령어

네트워크는 병목 현상이 흔하게 발생하는데, 병목 현상은 네트워크 대역폭, 네트워크 토폴로지, 서버 CPU 및 메모리 사용량, 비효율적인 네트워크 구성으로 인해 발생한다.

그래서 네트워크의 성능을 분석을 위해 몇 가지 명령어가 존재하는데, 이를 통해 현재 네트워크의 상태나 여러 정보들을 알 수 있다.

### ping(Packet INternet Groper)

**네트워크의 상태를 확인하려는 대상 노드를 향해 일정 크기의 패킷을 전송하는 명령어**

**ping**은 해당 노드의 패킷 수신 상태와 도달하기까지의 시간을 알 수 있다.

ICMP 프로토콜을 통해 동작하기 때문에 ICMP 프로토콜을 지원하지 않는 기기는 실행할 수 없으며, 네트워크 정책상 ICMP나 traceroute를 차단하는 대상은 ping 테스팅이 불가하다.

사용하는 방법은 ping [IP주소 또는 도메인 주소]로 실행하면 된다.

ex) ping www.naver.com

<img src="/assets/img/14/image4.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

### netstat

**접속되어 있는 서비스들의 네트워크 상태를 표시하는데 사용**

**netstat**를 사용하면 네트워크 접속 상태, 라우팅 테이블, 네트워크 프로토콜 등의 리스트를 보여준다.

또한, 서비스의 포트가 열려있는지 확인할 때 사용하기도 한다.


### nslookup

**DNS에 관련된 내용을 확인하기 위해 쓰는 명령어**

이는 특정 도메인에 매핑된 IP를 확인하기 위해 사용한다.


### tracert(traceroute)

**목적지 노드까지 네트워크 경로를 확인할 때 사용하는 명령어**

이는 목적지 노드까지 구간들 중 어느 구간에서 응답 시간이 느려지는 지 확인이 가능하다.


## 네트워크 프로토콜 표준화

**네트워크 프로토콜**은 다른 장치들끼리 데이터를 주고받기 위해 설정된 공통된 인터페이스를 말한다.

이는 개인이 정하는게 아니라 IEEE/IETF라는 표준화 단체가 정하고 이를 따른다.



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
  const images = Array.from(document.querySelectorAll("img[src^='/assets/img/14/']"));
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
