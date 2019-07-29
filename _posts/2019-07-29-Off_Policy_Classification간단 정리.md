---
layout: post
title: Off Policy Classifcation를 소개하는 페이지의 내용 분석
date: 2019-07-29
comments: true
external-url: https://ai.googleblog.com/2019/06/off-policy-classification-new.html
categories: Review
---

> Off Policy Classification?

>> In contrast, fully off-policy RL is a variant in which an agent learns entirely from older data, which is appealing because it enables model iteration without requiring a physical robot. With fully off-policy RL, one can train several models on the same fixed dataset collected by previous agents, then select the best one. However, fully off-policy RL comes with a catch: while training can occur without a real robot, evaluation of the models cannot.

fully off-policy RL은 과거의 history르 가지고 언제든지 재학습을 통해서 가장 좋은 것을 선택할 수 있는 장점이 있지만, 실세계와는 다르게 모델의 평가는 할 수 없는 단점이 있다 함.

>> Furthermore, ground-truth evaluation with a physical robot is too inefficient to test promising approaches that require evaluating a large number of models, such as automated architecture search with AutoML. 

더욱이, ground-truth evaluation은 너무 비효율적이라는 문제가 있다고 함

>> Though the OPE framework shows promise, it assumes one has an off-policy evaluation method that accurately ranks performance from old data. However, agents that collected past experience may act very differently from newer learned agents, which makes it hard to get good estimates of performance. 

off-policy evaluation (OPE)와 연관관계가 있어지만, 과거의 에이전트의 행동이 새로운 에이전트의 행동과 전혀 다를 가능성이 있으므로, 과거의 에이전트들을 가지고 만든 평가 모델은 문제가 있을 수 있다고 함.

>> In “Off-Policy Evaluation via Off-Policy Classification”, we propose a new off-policy evaluation method, called off-policy classification (OPC), that evaluates the performance of agents from past data by treating evaluation as a classification problem, in which actions are labeled as either potentially leading to success or guaranteed to result in failure. Our method works for image (camera) inputs, and doesn’t require reweighting data with importance sampling or using accurate models of the target environment, two approaches commonly used in prior work. We show that OPC scales to larger tasks, including a vision-based robotic grasping task in the real world.

여기서는 Off-policy classification(OPC)라는 것을 제안함. action에 대해서 성공 또는 실패를 라벨링하고, 이를 이용하여 에이전트의 성능을 평가하는 분류 모델을 만듦, 

>> OPC relies on two assumptions: 1) that the final task has deterministic dynamics, i.e. no randomness is involved in how states change, and 2) that the agent either succeeds or fails at the end of each trial.

OPC는 다음의 두가지 가정을 가지고 있다. 1. final task는 deterministic dynamics이다.(randomness가 상태 변화에 영향을 미치지 못한다.) 2. 성공 또는 실패가 있다.

>> Because each trial will either succeed or fail in a deterministic way, we can assign binary classification labels to each action.  We say an action is effective if it could lead to success, and is catastrophic if it is guaranteed to lead to failure.

action이 성공적인 결과를 이끌면, *effective*, 그렇지 않다면, *catastrophic*으로

>> In our paper, we prove that the performance of an agent is measured by how often its chosen action is an effective action, which depends on how well the Q-function correctly classifies actions as effective vs. catastrophic. This classification accuracy acts as an off-policy evaluation score.

이 논문에서는 만들어진 액션으로 에이전트의 성능을 평가하고, 이게 얼마나 좋은 측정량인지 증명할 것이다.

>> However, the labeling of data from previous trials is only partial. For example, if a previous trial was a failure, we do not get negative labels because we do not know which action was the catastrophic one. To overcome this, we leverage techniques from semi-supervised learning, positive-unlabeled learning in particular, to get an estimate of classification accuracy from partially labeled data. This accuracy is the OPC score.

