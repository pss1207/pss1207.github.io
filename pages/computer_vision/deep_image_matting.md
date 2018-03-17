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
image matting이란 이미지에서 foreground 영역을 얼마나 정확하게 분리하냐의 문제로 이미지 편집과 영화제작 분야에서 핵심 기술로 사용됩니다. 기존의 알고리즘들은 foreground와 background가 비슷한 경우 또는 복잡한 texture가 있을 때에는 부정확한 결과를 보였는데, 그 원인은 low-level의 feature만 사용하여 high-level의 context에 대한 정보가 부족하였기 때문입니다. 이러한 원인을 딥러닝 방식으로 풀어서 기존 알고리즘 대비 높은 정확도를 보입니다.



{% include links.html %}
