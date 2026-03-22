---
title: '[알고리즘 및 자료구조] 3. 완전 탐색과 백트래킹'
date: '2026-03-22'
tags:
  - 완전탐색
  - Brute Force
  - 백트래킹
thumbnail: /assets/img/9/image1.png
---
__이글은 개인적인 공부를 위해 작성한 글이며 피드백주시면 수정하도록하겠습니다.(출처 : 인프런 10주완성 C++ 코딩테스트)

## 완전탐색

**완전탐색이란?**

<img src="/assets/img/9/image1.png"
     alt="이미지"
     style="
       max-width: 60%;
       height: auto;
       display: block;
       margin: 20px auto;
       border-radius: 8px;
       box-shadow: 0 4px 12px rgba(0,0,0,0.15);
     ">

브루트포스(Brute Force)라고도 불리는 완전탐색은 말 그대로 모든 경우의 수를 탐색하는 알고리즘이다.

보통 시간복잡도가 1억 이하일 때 완전탐색을 사용가능하고, for/while 반복문을 통해서 구현할 수 있으며, 재귀를 통해서도 완전 탐색을 구현할 수 있다.

물론 때에 따라서는 다른 자료 구조를 사용해서 시간복잡도를 대폭 줄일 수 있다.(당연하게도,,,)

구현할 때, 반복문으로 구현이 가능하다면 재귀보단 반복문으로 구현하는 것이 코스트적인 면에서 봤을 때 이득이다. 

왜냐하면 재귀는 호출할 때마다 코스트가 생기기때문이다.

완전 탐색은 어떠한 코딩테스트를 풀든, 맨 처음에 생각할 수 있는 방법으로 일단은 무식하게 풀어보는 방법이라고 할 수 있다.

하지만, 왠만한 문제는 시간복잡도가 매우 크게 나와 다른 알고리즘이나 자료구조를 사용해야 풀리는 경우가 많을 것이다.


## 백트래킹(Backtracking)

백트래킹은 완전 탐색의 일종으로, 모든 해를 찾는 과정에서 불필요한 탐색을 줄여주는 방법이다.

여기서 사용되는 방식으로 **가지치기** 라는 것이 있는데 가지치기는 목표 해에 도달할 가능성이 없다고 판단되면 더 이상 그 경로를 탐색하지 않고 되돌아가는 방식으로 백트래킹에서 사용된다.

백트래킹은 아래의 코드와 같이 주로 재귀를 통해서 구현된다.


```cpp
void go(int idx){
	if(v.size() == 3){
		print();
		return;
	}
	for(int there : adj[idx]){
		if(visited[there]) continue;
		visited[there] = 1;
		v.push_back(there);
		
		go(there);
		
		visited[there] = 0; // 원상 복구
		v.pop_back(); // 원상 복구
	}
}
```

이 코드를 보면 기저조건인 v의 크기가 3일때 함수를 호춣하고 함수를 나가도록 되있고,

```visited[there] = 1 ``` 을 하고 재귀 함수를 호출한 뒤 ```visited[there] = 0``` 을 해서 원래 방문했던 곳을 안 방문한 것으로 처리하여 여러 경우의 수를 생각하게 할 수 있다.

백트래킹은 DFS 및 BFS로 모두 구현이 가능하나 대부분은 DFS를 사용하여 구현한다.

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
  const images = Array.from(document.querySelectorAll("img[src^='/assets/img/8/']"));
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
