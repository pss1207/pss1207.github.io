---
title: Deep Image Matting
tags: [getting_started]
keywords: release notes, announcements, what's new, new features
last_updated: Oct 10, 2017
summary:
sidebar: mydoc_sidebar
permalink: deep_image_matting.html
folder: computer_vision
---



## Image Matting Problem
![Image of matting](https://pss1207.github.io/pages/computer_vision/deep_image_matting/knn.jpg) <br>
image matting이란 이미지에서 foreground 영역을 얼마나 정확하게 분리하냐의 문제로 이미지 편집과 영화제작 분야에서 핵심 기술로 사용됩니다. 기존의 알고리즘들은 foreground와 background가 비슷한 경우 또는 복잡한 texture가 있을 때에는 부정확한 결과를 보였는데, 그 원인은 low-level의 feature만 사용하여 high-level의 context에 대한 정보가 부족하였기 때문입니다. 본 논문은 이러한 원인을 딥러닝 방식으로 풀어서 기존 알고리즘 대비 높은 정확도를 보입니다. <br>>


## 기존 연구의 한계점
논문에서는 기존 연구들의 한계점 두가지를 제시합니다. 첫번째는 matting problem을 정의하는 matting equation 자체의 한계점이고, 두번째는 데이터셋 생성의 어려움입니다.<br>
### Matting Equation의 한계점
기존 연구들은 아래와 같은 matting equation을 푸는 방식으로 접근하였습니다.<br>
{ I }_{ i }={ \alpha  }_{ i }{ F }_{ i }+(1-{ \alpha  }_{ i }){ B }_{ i }\quad { \alpha  }_{ i }\in [0,1] <br>
위의 equation은 foreground와 background의 color distribution이 overlap되지 않다는 가정이 들어있어, distribution이 overlap될 경우에는 한계가 있습니다. 이 논문 이전의 deep learning approach들 조차도 color값에 기반하여 alpha를 찾는 문제였습니다.
![Image of matting](https://pss1207.github.io/pages/computer_vision/deep_image_matting/fig1.jpg) <br>
위 그림의 3번째 상단에 있는 이미지가 Closed-form 방법이라는 기존 방식으로 alpha값을 찾은 결과입니다. 그림을 보면 머리카락과 같은 high frequency 성분이 떡지는것을 볼 수 있는데 그 이유가 바로 background의 다리 기둥과 foreground의 머리카락이 비슷한 color distribution을 가지기 때문입니다.<br>
### 데이터셋 부족
matting의 경우 background에서 foreground를 떼어내는 문제이기 때문에 매우 정확하게 경계면을 찾아야 합니다. 즉, ground truth 이미지를 생성하는게 매우 어렵습니다. alphamatting.com에서 제공하는 데이터도 training set 27개와 test set 8개뿐이라 학습을 하기에는 매우 부족한 숫자입니다. 그리고 이 데이터들 조차도 비슷한 이미지들이라 한계가 있습니다.


{% include links.html %}
