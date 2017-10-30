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
Sequential decision making을 하기 위해 수학적으로 문제를 모델링하는 방법으로 agent 입장에서 문제를 이해하는 방식을 나타낸다. State, Action, Reward, Policy로 이루어진다.<br>
State: Agent의 상황과 행동을 위한 현재의 정보를 나타낸다.<br>
Action: Agent가 어떤 State에서 취할 수 있는 action으로 left, right, up, down과 같은 방향이 그 예가 될 수 있다.<br>
Reward: Reinforcement Learning이라고 불리는 이유와 관계되는 핵심 요소로 Agent의 Action에 대한 평가를 나타낸다.<br>
Policy: Agent가 Reward를 받기 위하여 어떠한 Action을 취해야 하는지를 결정한다.<br>


## MDP의 구성 요소
### State
Agent의 상황을 나타내는 것으로 로봇의 경우 Sensor값이 된다.<br>
모델을 만들때에는 학습을 하기 위해 충분한 정보가 있는지 체크하여야 한다.<br>
### Action
State $${ S }_{ t }$$에서 가능한 행동<br>
### Reward function
State $${ S }_{ t }=s$$에서 Action $${ A }_{ t }=a$$를 취했을 때 Agent가 받을 Reward<br>
$${ { R }_{ s }^{ a } }=E[{ R }_{ t+1 }|{ S }_{ t }=s,{ A }_{ t }=a]$$<br>
### State Transition Probability
Agent가 Current State s에서 어떤 Action a를 취했을 때 Next State s'으로 갈 확률을 나타낸다.<br>
$${ { P }_{ ss' }^{ a } }=P[{ S }_{ t+1 }=s'|{ S }_{ t }=s,{ A }_{ t }=a]$$<br>
### Discount Factor
나중에 받는 Reward에 대해서는 가치를 줄여주는 것으로 Current State와 가까운 Reward일수록 더 큰 가치를 준다.<br>
$$\gamma$$로 표시하며 0에서 1사이 값이 된다.<br>
### Policy
각 State에서 Agent가 취할 Action으로 State가 input이 되고 Action이 output이 된다.<br>
output은 단일 action이 될 수도 있고 각 action들의 probability가 될 수도 있다.<br>
학습을 통해 Optimum Policy를 찾는 것이 최종 목표이다.<br>
$${ \pi (a|s) }=P[{ A }_{ t }=a|{ S }_{ t }=s]$$<br>

## Value Function
Agent는 Current State에서 앞으로 받을 Reward들을 고려하여 Action을 선택해야 Optimal Policy에 도달할 수 있다. 이 때 받을 Reward를 예상하는 함수가 Value Function이다.<br>
시간 t에서 단순히 앞으로의 Step들의 Reward를 더한다면 $${ G }_{ t }={ R }_{ t+1 }+{ R }_{ t+2 }+{ R }_{ t+3 }+...$$와 같이 될 것이다.<br>
이러한 방식의 문제점은 모든 Step에서의 Reward들에 대한 Weight가 같아서 Current State로 부터의 거리에 대한 정보를 반영할 수가 없다.<br>
만약, Discount Factor를 적용한다면 다음과 같은 형태가 될 것이다.<br>
$${ G }_{ t }={ R }_{ t+1 }+\gamma{ R }_{ t+2 }+{ \gamma }^{ 2 }{ R }_{ t+3 }+...$$<br>
Value Function은 시간 t에서 State가 s일 때의 Return값 $${ G }_{ t }$$에 대한 Expectation값으로 정의된다.<br>
$$v(s) = E[{G}_{t}|{S}_{t}=s]$$<br>
위 수식을 대입하면, $$v(s)=E[{ R }_{ t+1 }+\gamma{ R }_{ t+2 }+{ \gamma }^{ 2 }{ R }_{ t+3 }+...|{S}_{t}=s] = E[{ R }_{ t+1 }+\gamma({ R }_{ t+2 }+\gamma{ R }_{ t+3 }+...)|{S}_{t}=s] = E[{ R }_{ t+1 }+\gamma{G}_{t+1}|{S}_{t}=s]$$$${G}_{t+1}$$도 결국은 실제 Reward가 아닌 예상되는 값으로 Value Function으로 표현될 수 있다.<br>
즉, $$v(s)=E[{ R }_{ t+1 }+\gamma v({S}_{t+1})|{S}_{t}=s]$$ 로 표현된다.<br>

### Bellman Expectation Equation
Current State에서 Next State로 넘어갈 때에는 Policy에 따라 Action을 결정한다. 이 때, Policy에 의해 Value Function도 영향을 받는데 이렇게 Policy를 고려한 Value Function을 Bellman Expectation Equation이라고 한다.<br>
$${v}_{\pi}(s)={E}_{\pi}[{ R }_{ t+1 }+\gamma {v}_{\pi}({S}_{t+1})|{S}_{t}=s]$$<br>

### Q Function
Agent는 Value Function을 통해 각각의 Next State에 대한 Total Reward를 알 수 있다. 즉, Value Function은 입력이 State가 되고 출력이 Total Reward가 되는 함수이다.<br>
Q Function은 Next State의 Value Function이 아니라 Current State에서 각 Action에 대한 Value Function을 나타내는 것을 의미한다. 즉, State와 Action이라는 두개의 변수를 가진다.<br>
Value Function = Sum of (Policy x Q Function)으로 나타낸다.<br>
$${ v }_{ \pi  }(s)\quad =\quad \sum _{ a\in A }^{  }{ \pi (a|s){ q }_{ \pi  }(s,a) } $$<br>
Q Function의 Bellman Expectation Equation: $${q}_{\pi}(s,a)={E}_{\pi}[{ R }_{ t+1 }+\gamma {q}_{\pi}({S}_{t+1}, {A}_{t+1})|{S}_{t}=s, {A}_{t}=a]$$<br>
