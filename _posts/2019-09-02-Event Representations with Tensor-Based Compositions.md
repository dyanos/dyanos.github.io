---
layout: post
title: Summary on "Event Representations with Tensor-Based Compositions"
date: 2019-09-02
comments: true
external-url: https://arxiv.org/abs/1711.07611
categories: Paper
---

# Event Representations with Tensor-Based Compositions

Source Code : https://github.com/stonybrooknlp/event-tensors

Paper : https://arxiv.org/abs/1711.07611



### Dataset

We use **the New York Times Gigaword Corpus** for training data.

Event triples are extracted using **the Open Information Extraction system Ollie** (Mausam et al. 2012).

https://github.com/knowitall/ollie



## Main

어떻게 Predicate와 Argument를 구할 것인가?? Embedding은...

![image-20190830182038655](images/image-20190830182038655.png)

Real??

Instead of additive models, we propose **tensor-based composition models**, <u>which combine the subject, predicate, and object to produce the final event representation</u>.



## Models: Tensor-based Event Composition

![image-20190830182602545](images/image-20190830182602545.png)

