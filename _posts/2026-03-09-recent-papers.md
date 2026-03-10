---
layout: post
title: Recent Interesting Papers
date: 2026-03-08 00:01:00
description: Discusses recently read papers in AI I found interesting
tags: AI
categories: AI and Science
---

# WiseFT: Robust fine-tuning of zero-shot models

Large pretrained models like CLIP give great zero shot performance, and even better finetuned performances on datasets. However, this leads to reduction in robustness to distribution shifts and catastrophic forgetting. WiseFT [^1] deals with this problem, by ensembling the weights of zero shot  model and finetuned model.
This could be used in continual learning.






[^1]: Wortsman, M., Ilharco, G., Kim, J.W., Li, M., Kornblith, S., Roelofs, R., Lopes, R.G., Hajishirzi, H., Farhadi, A., Namkoong, H. and Schmidt, L., 2022. Robust fine-tuning of zero-shot models. In Proceedings of the IEEE/CVF conference on computer vision and pattern recognition (pp. 7959-7971).

---

# Steering CLIP’s vision transformer with sparse autoencoders
CVPR Workshop on Mechanistic Interpratibility for Vision
Paper from MILA: Joseph, Suresh, Richards et al

Context: Foundation models often compress information about multiple different things to a single neuron weight, making these not very interpretable. In language models with transformers, sparse autoenoders have helped to make language models based on transformers interpretable, by learning using internal activations of transformer layers. Since only a few features are allowed to activate at once, it is forced to learn disentangled features making the vectors interpretable.

Now if we are able to understand which part of the ViT is responsible for classifying a particular task, we can make its learning rate higher when a similar kind of task appears, while keeping other parts less learnable (remember SLCA: Slow Learner with Classifier Alignment).

In [^2], they train SAEs on CLIP's Vision transformer.

[^2]: Joseph, S., Suresh, P., Goldfarb, E., Hufe, L., Gandelsman, Y., Graham, R., Bzdok, D., Samek, W. and Richards, B.A., 2025. Steering CLIP's vision transformer with sparse autoencoders. arXiv preprint arXiv:2504.08729.