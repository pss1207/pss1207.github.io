---
title: Markov Decision Process and Bellman Equation
tags: [getting_started]
keywords: release notes, announcements, what's new, new features
last_updated: Oct 10, 2017
summary:
sidebar: mydoc_sidebar
permalink: mdp.html
folder: deep_learning
---

## Markov Decision Process (MDP)
Sequential decision making을 하기 위해 수학적으로 문제를 모델링하는 방법으로 agent 입장에서 문제를 이해하는 방식을 나타낸다. State, Action, Reward, Policy로 이루어진다.
State: Agent의 상황과 행동을 위한 현재의 정보를 나타낸다.
Action: Agent가 어떤 State에서 취할 수 있는 action으로 left, right, up, down과 같은 방향이 그 예가 될 수 있다.
Reward: Reinforcement Learning이라고 불리는 이유와 관계되는 핵심 요소로 Agent의 Action에 대한 평가를 나타낸다.
Policy: Agent가 Reward를 받기 위하여 어떠한 Action을 취해야 하는지를 결정한다.

## MDP의 구성 요소
### State
Agent의 상황을 나타내는 것으로 로봇의 경우 Sensor값이 된다. 모델을 만들때에는 학습을 하기 위해 충분한 정보가 있는지 체크하여야 한다.
### Action
State $${ S }_{ t }$$에서 가능한 행동
### Reward function
State $${ S }_{ t }=s$$에서 Action $${ A }_{ t }=a$$를 취했을 때 Agent가 받을 Reward<br>
$${ { R }_{ s }^{ a } }=E[{ R }_{ t+1 }|{ S }_{ t }=s,{ A }_{ t }=a]$$
### State Transition Probability
Agent가 Current State s에서 어떤 Action a를 취했을 때 Next State s'으로 갈 확률을 나타낸다.<br>
$${ { P }_{ ss' }^{ a } }=P[{ S }_{ t+1 }=s'|{ S }_{ t }=s,{ A }_{ t }=a]$$
### Discount Factor
나중에 받는 Reward에 대해서는 가치를 줄여주는 것으로 Current State와 가까운 Reward일수록 더 큰 가치를 준다. $$\gamma$$로 표시하며 0에서 1사이 값이 된다.
### Policy
각 State에서 Agent가 취할 Action으로 State가 input이 되고 Action이 output이 된다. output은 단일 action이 될 수도 있고 각 action들의 probability가 될 수도 있다. 학습을 통해 Optimum Policy를 찾는 것이 최종 목표이다. <br>
$${ \pi (a|s) }=P[{ A }_{ t }=a|{ S }_{ t }=s]$$
