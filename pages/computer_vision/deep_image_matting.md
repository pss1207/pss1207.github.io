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

* 논문 링크: https://arxiv.org/abs/1703.03872

## Image Matting Problem
![Image of matting](https://pss1207.github.io/pages/computer_vision/deep_image_matting/knn.jpg) <br>
image matting이란 이미지에서 foreground 영역을 얼마나 정확하게 분리하냐의 문제로 이미지 편집과 영화제작 분야에서 핵심 기술로 사용됩니다. 기존의 알고리즘들은 foreground와 background가 비슷한 경우 또는 복잡한 texture가 있을 때에는 부정확한 결과를 보였는데, 그 원인은 low-level의 feature만 사용하여 high-level의 context에 대한 정보가 부족하였기 때문입니다. 본 논문은 이러한 원인을 딥러닝 방식으로 풀어서 기존 알고리즘 대비 높은 정확도를 보입니다. <br>


## 기존 연구의 한계점
논문에서는 기존 연구들의 한계점 두가지를 제시합니다. 첫번째는 matting problem을 정의하는 matting equation 자체의 한계점이고, 두번째는 데이터셋 생성의 어려움입니다.<br>
### Matting Equation의 한계점
기존 연구들은 아래와 같은 matting equation을 푸는 방식으로 접근하였습니다.<br>
$${ I }_{ i }={ \alpha  }_{ i }{ F }_{ i }+(1-{ \alpha  }_{ i }){ B }_{ i }\quad { \alpha  }_{ i }\in [0,1]$$ <br>
위의 equation은 foreground와 background의 color distribution이 overlap되지 않다는 가정이 들어있어, distribution이 overlap될 경우에는 한계가 있습니다. 이 논문 이전의 deep learning approach들 조차도 color값에 기반하여 alpha를 찾는 문제였습니다.
![Image of matting](https://pss1207.github.io/pages/computer_vision/deep_image_matting/fig1.png) <br>
위 그림의 3번째 상단에 있는 이미지가 Closed-form 방법이라는 기존 방식으로 alpha값을 찾은 결과입니다. 그림을 보면 머리카락과 같은 high frequency 성분이 떡지는것을 볼 수 있는데 그 이유가 바로 background의 다리 기둥과 foreground의 머리카락이 비슷한 color distribution을 가지기 때문입니다.<br>
### 데이터셋 부족
matting의 경우 background에서 foreground를 떼어내는 문제이기 때문에 매우 정확하게 경계면을 찾아야 합니다. 즉, ground truth 이미지를 생성하는게 매우 어렵습니다. alphamatting.com에서 제공하는 데이터도 training set 27개와 test set 8개뿐이라 학습을 하기에는 매우 부족한 숫자입니다. 그리고 이 데이터들 조차도 비슷한 이미지들이라 한계가 있습니다.<br>

## 제안된 방법
본 논문은 크게 5가지 특징으로 요약될 수 있습니다.
* 입력 이미지와 trimap(foreground, background, unknown의 세가지 영역으로 구분)으로부터 alpha matte를 deep learning approach를 통해 direct로 구현
* 머리카락이나 털과 같은 패턴이나 움직이는 물체의 경계면, 반투명한 물체들은 기존 방법들에서 쓰였던 low-level feature로는 학습이 되지 않지만 deep networks에서는 학습이 가능 - 즉, color information을 참고하기보다는 natural structure를 학습했다는 점에서 기존 기술들과 차별성을 보임.
* 네트워크의 구조는 encoder-decoder stage와 refinement stage 두 개의 stage로 구성
* background가 단순한 이미지에서 object를 완벽히 추출한 뒤 새로운 background 이미지에 합성하는 방식으로 데이터셋을 구축
* 위의 Figure 1의 두번째 열이 trimap을 나타내는데 하단의 케이스와 같이 대부분인 unknown 영역(회색)일 경우에도 기존 방법들과 비교했을 때 좋은 결과를 보임.

## 새로운 matting 데이터셋 구축
앞에서도 설명드린대로 기존의 alphamatting.com 데이터는 27개의 training set과 8개의 test set만 있어 데이터 수도 적을뿐만 아니라 비슷한 환경에서 생성된 이미지들이라 diversity 측면에서도 매우 부족합니다. <br>
이러한 이유로 본 논문에서는 소수의 foreground object들을 다수의 background 이미지에 합성하는 방식으로 데이터를 구축하였습니다.<br>
![Image of matting](https://pss1207.github.io/pages/computer_vision/deep_image_matting/fig2.png) <br>
위 그림 figure 2의 a와 같이 background가 단순한 이미지에서 object를 추출한 뒤 포토샵으로 정확한 alpha matte 이미지를 구하였습니다. 물론 기존의 alphamatting.com과 videomatting 데이터셋의 object들도 사용하였습니다. 이렇게하여 training set을 위한 foreground object 493개와 test set을 위한 foreground object 50개를 생성한 뒤, 이를 다른 background 이미지에 합성하여 training set 총 49,300개, test set 총 1000개의 이미지를 생성하였습니다. 또한 trimap의 unknown영역은 random하게 dilation을 적용하여 unknown영역의 넓이를 다양하게 하였습니다. <br>

## 네트워크 구조
![Image of matting](https://pss1207.github.io/pages/computer_vision/deep_image_matting/fig3.png) <br>
네트워크는 encoder-decoder stage, refinement stage로 두 개의 stage로 구성되어 있습니다.
### Matting Encoder-Decoder Stage
encoder-decoder 구조는 이미 image segmentation, boundary prediction, hole filling등 computer vision분야에서 많이 사용되어 온 구조입니다. 입력으로는 R, G, B 세 개의 channel을 가지는 이미지와 alpha값과 unknown 영역이 표시된 trimap 이렇게 4개의 channel로 들어갑니다. 앞단의 encoder network 부분에서는 convolutional neural layer와 max pooling layer를 통해 feature map을 계속 줄여나가고, decoder network는 역으로 unpooling layer를 통해 max pooling operation과 convolutional layer를 역으로 연산합니다. encoder는 총 14개의 convolutional layer와 5개의 max pooling layer로 구성되어 있으며, decoder는 encoder보다는 작은 6개의 convolutional layer와 5개의 unpooling layer, 그리고 마지막 alpha값을 계산하는 alpha prediction layer로 구성되어 있습니다. <br>
#### Loss function
loss function은 alpha-prediction loss와 compositional loss 두 개로 이루어져 있습니다.<br>
* alpha-prediction loss: trimap의 unknwon region에 대하여 alpha값이 계산되면 계산된 alpha인 predicted alpha와 ground truth alpha값의 차이를 구함. <br>
$${ L  }_{ \alpha  }^{ i }=\sqrt { { ({ \alpha  }_{ p }^{ i }-{ \alpha  }_{ g }^{ i }) }^{ 2 }+{ \epsilon  }^{ 2 } } ,\quad { \alpha  }_{ p }^{ i },{ \alpha  }_{ g }^{ i }\in [0,1]$$<br>
* compositional loss: predicted alpha값을 참고하여 합성된 predicted RGB 이미지와 ground truth RGB 이미지의 color값 차이
$${ L  }_{ c  }^{ i }=\sqrt { { ({ c  }_{ p }^{ i }-{ c }_{ g }^{ i }) }^{ 2 }+{ \epsilon  }^{ 2 } } ,\quad { \alpha  }_{ p }^{ i },{ \alpha  }_{ g }^{ i }\in [0,1]$$<br>
* overall loss
위 두가지 loss에 대한 weighted sum으로 overall loss를 계산하였습니다. <br>
$${ L }_{ overall }={ w }_{ l }\cdot { L }_{ \alpha  }+(1-{ w }_{ l })\cdot { L }_{ c }$$ <br>
#### Implementation
foreground가 493개만 있으므로 overfitting을 피하기 위하여 아래와 같은 전략으로 학습을 하였습니다.<br>
* 이미지를 320x320으로 random하게 crop한 이미지 생성
* 480x480 또는 640x640으로 crop한 뒤, 320x320으로 resize한 이미지 생성
* flipping한 이미지 생성
* trimap 생성시 ground truth alpha mattes로부터 random하게 dilation적용
* training epoch마다 입력 이미지를 random하게 재생성
encoder의 14개 convolutional layer는 VGG-16의 layer 사용하였으며 입력이 3채널이 아니라 R, G, B, trimap 4개의 채널이므로 나머지 한 개의 채널은 zero initialization을 적용하였습니다. 그리고 decoder쪽 parameter들은 Xavier random variables로 initialization하였습니다.<br>

### Matting Refinement Stage
![Image of matting](https://pss1207.github.io/pages/computer_vision/deep_image_matting/fig4.png) <br>
앞의 encoder-decoder stage 이후에 refinement stage가 들어간 이유는 encoder-decoder구조의 특성상 위 그림의 (b)와 같이 그 결과가 너무 smooth한 이미지를 생성해내기 때문입니다. 본 논문에서는 refinement stage를 추가하여 (c)와 같이 alpha matte를 더 정확하게 구하고 더욱 sharp한 edge를 구할 수 있었다고 설명하고 있습니다.
#### Network Structure
encoder-decoder stage의 입력이었던 image patch와 prediction된 alpha값을 concatenation하여 입력으로 넣어줍니다. 출력은 최종 alpha matte값으로 ground truth alpha값과의 차이로 loss를 구합니다. 총 4개의 convolutional layer로 구성된 fully convolutional network 구조이면서 최종 출력단에 encoder-decoder의 출력 alpha값을 더하여 Resnet과 같은 skip model을 적용하였습니다.
#### Implementation
training할때에는 먼저 refinement stage는 제외하고 encoder-decoder part만 training한 뒤, trining이 수렴하면 refinement part도 update하기 시작합니다. refinement part가 수렵하면 전체 network를 같이 fine-tune하는 방식으로 학습을 합니다. loss function의 경우 alpha값을 refinement하는것이 목적이므로 encoder-decoder stage와 다르게 alpha prediction loss만 사용합니다.


{% include links.html %}
