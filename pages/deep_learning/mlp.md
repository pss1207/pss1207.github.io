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


{% include links.html %}
