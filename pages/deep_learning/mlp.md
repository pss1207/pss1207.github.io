---
title: Deep Feedforward Networks
tags: [getting_started]
keywords: release notes, announcements, what's new, new features
last_updated: Oct 10, 2017
summary:
sidebar: mydoc_sidebar
permalink: mlp.html
folder: deep_learning
---


## Multilayer Perceptrons (MLPs)

### MLP란?
Deep Feedforward Networks 또는 Feedforward Neural Networks라고도 불리는 것으로 입력 x가 주어졌을 때 출력 y가 나올 수 있는 function f를 나타내는 모델로 $$y=(x;\theta)$$에서 $$\theta$$를 학습하여 best function을 찾는것이 목표이다.

### MLP의 구조
일반적으로 Neural Networks는 Chain Structure의 형태로 각 function들이 chain으로 연결되어 있다. 예를들면 $$f\left( x \right) =f^{ (3) }\left( f^{ (2) }\left( f^{ (1) }\left( x \right)  \right)  \right)$$에서 각 function $$f^{ (3) }\left( x \right)$$, $$f^{ (2) }\left( x \right)$$, $$f^{ (1) }\left( x \right)$$이 chain으로 연결되어 있으며 $$f^{ (1) }\left( x \right)$$은 1st layer, $$f^{ (2) }\left( x \right)$$는 2nd layer, 마지막 layer인 $$f^{ (3) }\left( x \right)$$은 output layer를 나타낸다. 이 layer의 개수가 모델의 depth와 관련이 있으며 Deep Learning은 이러한 depth로 부터 나온 개념이다.

### Hidden Layer
1st layer와 2nd layer를 hidden layer라고 부르는데 이는 모델을 학습할 때 training data에 input data와 output label에 대한 정보만 있고 각 hidden layer의 output에 대한 정보는 없기 때문이다. 각 hidden layer들은 vector로 나타내며 이 vector의 dimensionality가 모델의 width를 결정한다. vector의 각 unit은 이전 layer의 다른 unit들로부터 입력을 받아서 각 activation value를 계산한다.

### Nonlinear function
nonlinear model로 표현하기 위해 각 unit의 입력을 x가 아닌 $$\phi(x)$$라는 nonlinear transformation을 적용한다.

### Example: Learning XOR
XOR은 두개의 binary value인 x1과 x2에 대한 연산으로 두 값이 다를때에는 1을, 같을때에는 0을 return한다. $$y=f^{ * }(x)$$를 target function, $$y=f(x;\theta)$$를 학습할 모델이라고 하자. 학습 알고리즘은 parameter $$\theta$$를 변경하여 $$f$$를 $$f^{ * }$$와 가장 유사하도록 하는것이 목표이다.<br>
MSE function: $$J ( \theta ) = \frac { 1 }{ 4 } \sum_{ x \in X  }^{  }{ { (f^{ * } \left ( x \right) -f( x; \theta ) ) }^{ 2 } }$$
만약, $$f(x;\theta)$$가 linear model이라면 $$f(x;w,b)=x^{ T }w+b$$로 정의할 수 있다. x가 0, 1, 2, 3일 때 y는 0, 1, 1, 0이 되므로 linear model의 결과는 w=0, $$b=\frac{1}{2}$$가 될 것이다. 즉, linear model로는 XOR 문제를 풀 수 없다. linear model로 풀기 위해서는 다른 feature space를 사용하여야 한다.
앞의 모델에서 하나의 hidden layer가 더 있다고 가정하자. hidden layer에서는 $$h=f^{ (1) }(x;W,c)$$ 연산을 하고 그 결과가 output layer로 들어갈 것이다. 즉, $$y=f^{(2)}(h;w,b)$$가 된다.
전체 모델을 나타내면 $$f(x;W,c,w,b)=f^{(2)}(f^{(1)}(x))$$가 된다. 하지만 $$f^{(1)}$$이 linear이면 전체 모델도 linear model이 되어버린다. $$f(x)=w^{T}W^{T}x$$ <br>
그렇다면 $$h=g(W^{T}x+c)$$와 같이 nonlinear function을 써보자. 이때 $$g(z)=max\{0,z\}$$로 정의되는 ReLU function으로 정의하면 $$f(x;W,c,w,b)=w^{T}max\{0, W^{T}x+c\}+b$$가 된다. <br>
W, c, w를 다음과 같다고 가정하자.
$$W=\begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix},\quad c=\begin{bmatrix} 0 \\ -1 \end{bmatrix},\quad w=\begin{bmatrix} 1  \\ -2  \end{bmatrix}$$<br>
입력 X가 $$X=\begin{bmatrix} 0 & 0 \\ 0 & 1 \\ 1 & 0 \\ 1 & 1 \end{bmatrix}$$이면, XW는 다음과 같다. $$XW=\begin{bmatrix} 0 & 0 \\ 1 & 1 \\ 1 & 1 \\ 2 & 2 \end{bmatrix}$$<br>
여기에 c를 더하면 $$XW+c=\begin{bmatrix} 0 & -1 \\ 1 & 0 \\ 1 & 0 \\ 2 & 1 \end{bmatrix}$$이 된다. <br>
Nonlinear function인 ReLU를 적용하면 $$ReLU(XW+c)=\begin{bmatrix} 0 & 0 \\ 1 & 0 \\ 1 & 0 \\ 2 & 1 \end{bmatrix}$$가 되는데 2번째와 3번째 행이 동일해진것을 확인할 수 있다. 즉, 입력 X가 1(01) 또는 2(10)일 때의 ReLU출력이 동일해져서 output layer에서 linear model로 구분이 가능해진것이다.




{% include links.html %}
