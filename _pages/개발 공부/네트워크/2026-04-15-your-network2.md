---
title: '[네트워크] 2. TCP/IP 4계층 모델(1)'
date: '2026-04-15'
tags:
  - 애플리케이션 계층
  - 전송 계층
  - TCP
  - UDP
thumbnail: /assets/img/15/image1.png
---
__이글은 개인적인 공부를 위해 작성한 글이며 피드백주시면 수정하도록하겠습니다.(출처 : 면접을 위한 CS 전공지식 노트)

이미지 출처 : https://velog.io/@sckwon770/1.2-TCPIP-4계층-모델, 개발자를 위한 컴퓨터공학 2: 혼자 공부하는 네트워크

----------------------------------------

TCP/IP 4계층 모델은 OSI 7계층과 달리 애플리케이션 계층, 전송 계층, 인터넷 계층, 링크 계층으로 나뉜다.

보통 네트워크의 계층을 설명하면 4계층 모델로 설명을 한다. 

그 이유는 OSI 7계층은 통신과정을 표준화하고 이해하기 위해 만든 이론적 모델이고, TCP/IP 4계층은 실제 인터넷에서 통신을 구현하기 위해 만들어진 실용적인 모델이다.

<img src="/assets/img/15/image1.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

그래서 주로 사용되는 TCP/IP 4계층 모델을 알아보자!!😀

## 애플리케이션 계층(Application Layer)

**애플리케이션 계층**은 웹 서비스 및 이메일등 서비스를 실질적으로 사람들에게 제공하는 층이다.

FTP, HTTP, SSH, SMTP, DNS 등이 이에 해당하는데.. 각 역할은 다음과 같다

**FTP** : 장치와 장치간의 파일을 전송하는데 사용되는 표준 통신 프로토콜
**SSH** : 보안되지 않은 네트워크에서 네트워크 서비스를 안전하게 운영하기 위한 암호화 네트워크 프로토콜
**HTTP** : 웹 사이트를 이용하는데 쓰는 프로토콜
**SMTP** : 전자 메일 전송을 위한 인터넷 표준 통신 프로토콜
**DNS** : 도메인 이름과 IP주소를 매핑해주는 서버

실제로 사용자가 직접 사용하는 서비스가 동작하는 계층으로 제일 체감이 많이 되는 계층이라 볼 수 있다!

## 전송 계층(Transport Layer)

**전송 계층**은 송신자와 수신자를 연결하는 통신 서비스이다.

애플리케이션 계층과 추후 알아볼 인터넷 계층 사이의 데이터가 전달될 때 중계 역할을 하며, 데이터를 정확하고 안정적으로 전달하는 계층이다.

대표적으로 **TCP, UDP**가 존재한다

### TCP

**TCP**는 패킷 사이의 순서를 보장하고 연결지향 프로토콜을 사용해서 연결을 하여 신뢰성을 구축해서 수신 여부를 확인하며 가상회선 패킷 교환 방식을 사용하는 프로토콜이다.

여기서 **가상회선 패킷 교환 방식**이란..

간단히 말해 모든 패킷을 전송하면 각 패킷에 존재했던 가상회선이 해제되고 패킷들은 전송된 **순서대로** 도착하는 방식이다.

TCP는 정확성이 중요할 때 사용하는데, 대표적으로 파일을 다운로드한다든가, 인터넷에서 결제를 할때 사용된다. 데이터가 하나라도 틀리면 문제가 되기 때문이다. 

#### TCP의 연결 및 해제 과정

TCP는 신뢰성 확보를 위해 UDP와 다르게 특별한 방식을 사용한다.

**3/4-way-handshake** 방식을 사용하여 연결 및 해제를 하는데.. 연결 먼저 알아보자

**TCP 연결 성립 과정**

<img src="/assets/img/15/image2.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

연결은 3-way-handshake 방식을 사용한다.

1. SYN 단계 : 클라이언트는 서버에 클라이언트의 ISN을 담아 SYN을 보냄
여기서 SYN은 첫 번째 패킷에 할당된 임의의 시퀀스 번호를 뜻하고, SYN은 연결 요청 플래그이다.

2. SYN + ACK 단계 : 서버는 클라이언트의 SYN을 수신하고 서버의 ISN을 보내며 승인번호로 클라이언트의 **ISN + 1**을 보냄

3. ACK 단계 : 클라이언트는 서버의 **ISN + 1**한 값인 승인 번호를 담아 ACK를 서버에 보냄

이렇게 3-way-handshake가 이뤄지고 신뢰성이 구축된 다음 데이터 전송이 시작된다.

**TCP 연결 해제 과정**

<img src="/assets/img/15/image3.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

연결 해제는 4-way-handshake 방식을 사용한다.

1. 클라이언트가 연결을 닫으려고 할때, FIN으로 설정된 세그먼트를 서버에 보냄

여기서 클라이언트는 FIN_WAIT_1 상태로 들어가고, 서버의 응답을 기다린다

2. 서버는 클라이언트로 ACK라는 승인 세그먼트를 보냄

서버는 CLOSE_WAIT 상태에 들어가며, 클라이언트는 세그먼트를 받으면 FIN_WAIT_2 상태에 들어간다.

3. 서버는 ACK를 보내고, 일정 시간 이후 클라이언트에 FIN이라는 세그먼트를 보냄

4. 클라이언트는 TIME_WAIT 상태가 되며, 다시 서버로 ACK를 보내서 서버는 CLOSED 상태가 됨

이렇게 클라이언트는 어느 정도의 시간을 대기한 후 연결이 닫히고, 클라이언트와 서버의 모든 자원의 연결이 해제된다.

근데, 여기서 특이한 점이 TIME_WAIT 상태가 있는 것인데, TIME_WAIT은 소켓이 소멸되지 않고 일정 시간 유지되는 상태를 말한다. 바로 연결이 해제되지 않고 이러는 이유로는, 지연 패킷이 발생할 경우를 대비하고 두 장치의 연결이 잘 닫혔는지 확인하기 위해 일정 시간 이후 연결을 닫는다!!


### UDP

**UDP**는 TCP와 달리 순서를 보장하지 않고 수신 여부를 확인하지 않으며 단순히 데이터만 주는 데이터그램 패킷 교환 방식을 사용하는 프로토콜이다.

**데이터그램 패킷 교환 방식**은 패킷이 독립적으로 이동하고, 최적의 경로를 선택하여 이동하는 것을 말하고, 하나의 메시지에서 분할된 분할된 여러 패킷은 서로 다른 경로로 전송될 수 있다.

즉, 패킷이 도착하는 순서가 다를 수 있다.(뒤죽박죽?)

UDP는 속도가 더 중요할 때 사용하는데, 라이브 서비스를 할때 주로 사용된다. 게임이나, 영상 스트리밍 등이 이에 해당한다.



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
  const images = Array.from(document.querySelectorAll("img[src^='/assets/img/15/']"));
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
