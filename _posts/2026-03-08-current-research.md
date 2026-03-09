---
layout: post
title: What am I working on currently and other ideas
date: 2026-03-07 00:01:00
description: Brainstorming ideas and current projects
tags: Ideas, CL
categories: Continual-Learning
bibliography: march26-bib.bib
---


Currently, for my masters thesis, I have been working on continual learning using CLIP. In this regard, I have come across the XTAIL [^1] <d-cite key="xu2024advancing"></d-cite> (cross domain task agnostic incremental learning) benchmark, in which the CLIP model is adapted across multiple tasks, with each task being a different dataset and with different classes. The datasets span multiple domains like satellite image, natural domain, mnist, etc. The model is tested across all tasks, after training on each task, so both seen and unseen classes are tested.

Two successful methods in this benchmark are RAIL - which uses a frozen ZS CLIP model to predict, and if the prediction is within a seen class, the ViT output is additionally passed to a froze random projection matrix, followed by nearest class mean classification otherwise gives the ZS CLIP output. Thus, this has to store all the seen classes to be able to classify, and is almost like separate branches for seen and unseen classes - not really adapting CLIP.

Another method is LADA, which keeps ViT Frozen, PEFT trains the text encoder for a particular task, and stores the text vectors, and again during inference, uses ZS clip to predict if seen class, if seen it uses the text features which were stored of seen classes.

Again this is like a separate branch for classifying the same thing.

Ideally, in CLIP model any set of class names can be passed and the CLIP model is able to predict in that label space, here we are constraining CLIP to only be able to predict properly within the seen label space, otherwise a ZS CLIP output is given.



I want to suggest a way where the CLIP model can itself be adapted without needing to store classifiers - so we can pass any order of classes to text embedding and the model predicts it - and doesnt undergo catastrophic forgetting on seen classes.

---

What lacks in current AI models, especially generative models is a method of authentication. I will explain what I mean.
When one asks the model to generate a "forged" image, say superimposing a face on top of a celebrity at cannes - there should be an accurate method to allow for authentication - we should only allow the user to manipulate with his/her own face not with someone elses. This could take care of the problem in twitter where people ask grok to generate images of other people in questionable clothing or worse... and grok does it which is a serious ethical and privacy violation.


I haven't seen much research in this regard - there has been work done on unlearning particular entities that had been present in training data, but that is quite expensive and is done adaptively, not inherent to the model.

[^1]: Xu, Yicheng, Yuxin Chen, Jiahao Nie, Yusong Wang, Huiping Zhuang, and Manabu Okumura. "Advancing cross-domain discriminability in continual learning of vision-language models." Advances in Neural Information Processing Systems 37 (2024): 51552-51576.
