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
Based on these stored samples, the learner (which is basically a deep neural network), during inference, learns a mapping from $$x \rightarrow y$$ where $$(x,y) \in D_t$$. The inference is given by $$y^ argmax **p \circ m**$$ where **p** is the softmax probability  and **m** is a user defined mask (especially for defining tasks in task incremental learning case).
