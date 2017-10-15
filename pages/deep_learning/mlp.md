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
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

## Multilayer Perceptrons (MLPs)

Deep Feedforward Networks 또는 Feedforward Neural Networks라고도 불리는 것으로 입력 x가 주어졌을 때 출력 y가 나올 수 있는 function f를 나타내는 모델로 $$y=(x;\theta)$$에서 $$\theta$$를 학습하여 best function을 찾는것이 목표이다.

일반적으로 Neural Networks는 Chain Structure의 형태로 각 function들이 chain으로 연결되어 있다. 예를들면 $$f\left( x \right) =f^{ (3) }\left( f^{ (2) }\left( f^{ (1) }\left( x \right)  \right)  \right)$$에서 각 function $$f^{ (3) }\left( x \right)$$, $$f^{ (2) }\left( x \right)$$, $$f^{ (1) }\left( x \right)$$이 chain으로 연결되어 있으며 $$f^{ (1) }\left( x \right)$$은 first layer, $$f^{ (2) }\left( x \right)$$는 2nd layer, 마지막 layer인 $$f^{ (3) }\left( x \right)$$은 output layer를 나타낸다. 이 layer의 개수가 모델의 depth와 관련이 있으며 layer의 개수가 많은 구조를 Deep Learning이라고 한다.

{% include links.html %}
