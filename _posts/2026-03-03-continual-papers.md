---
layout: post
title: Continual Learning Papers
date: 2026-03-03 00:01:00
description: Discusses recently read continual learning papers
tags: CL
categories: Continual-Learning
---

# GDumb: A Simple Approach that Questions Our Progress in Continual Learning
Authors: Ameya Prabhu, Philip Torr, Puneet Dokania

Was published in ECCV 2020.

GDumb challenges the conitnual learning methods and research scenarios till then - claiming most of the assumptions and simplifications make the methods not practical.
They demonstrate this by proposing a simple method consisting of Greedy balancing sampler and a learner, which doesn't have any component which was made for continual learning, and is able to outperform continual learning methods.
From the paper:
Given a memory budget, say k samples, the sampler greedily stores samples from the data-stream (max k samples) with the constraint to asymptotically balance class distribution. It is greedy in the sense that whenever it encounters a new class, the sampler simply creates a new bucket for that class and starts removing samples from the old ones, in particular, from the one with a maximum number of samples. Any tie is broken randomly, and a sample is also removed randomly assuming that each sample is equally important. Note, this sampler does not rely on task boundaries or any information about the number of samples in each class.
Based on these stored samples, the learner (which is basically a deep neural network), during inference, learns a mapping from $$x \rightarrow y$$ where $$(x,y) \in D_t$$. The inference is given by $$\hat{y} argmax **p \circ m**$$ where **p** is the softmax probability  and **m** is a user defined mask (especially for defining tasks in task incremental learning case).

This was an important paper to understand if a CL model is doing good, because of the actual algorithm, or if it essentially stores the previous samples for classification.


# XTAIL: Advancing Cross domain Task agnostic Incremental Learning
Authors: Xu, Chen, Okumura, et al.

Was published in NeurIPS 2024.
This paper suggested extending the previously proposed Multidomain Task Incremental Learning benchmark to a more realistic task ID free class incremental learning scenario. Here, each task is a new dataset (with 10 total datasets of different domain - Aircraft, Caltech101, DTD, EuroSAT, Flowers, Food101, MNIST, Oxford Pets, Stanford Cars and Sun 397). So during task 3 for example, the model has already seen samples from tasks 1 and 2- aircraft and caltech, and optimizes on samples from 3 with or without replay. After each task training, the model is tested on all tasks from 1 to 10, so it is evaluated on both seen tasks (to gauge **backward forgetting**) and unseen (zero shot ) tasks (to gauge **forward forgetting**). Thus, all methods in this scenario is CLIP based.

The paper also suggested a method called RAIL - Regression Analytic Incremental Learner method which is actually an extension of the RANPAC method to CLIP for this task. 
In essence, the model uses a frozen  zero shot CLIP model to classify roughly whether the model predictions are within seen or unseen part. 
If it predicts within seen part, the image features obtained from CLIP ViT are further passed to an adapter, which in primal RAIL consists of projecting the features to a higher dimension using a frozen random matrix, and then using a MLP to classify. This gives good enough results, beating other common CL methods. 
