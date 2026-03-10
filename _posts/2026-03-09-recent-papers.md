---
layout: post
title: Recent Interesting Papers
date: 2026-03-08 00:01:00
description: Discusses recently read papers in AI I found interesting
tags: AI
categories: AI, Science
---

# WiseFT: Robust fine-tuning of zero-shot models

Large pretrained models like CLIP give great zero shot performance, and even better finetuned performances on datasets. However, this leads to reduction in robustness to distribution shifts and catastrophic forgetting. WiseFT [^1] deals with this problem, by ensembling the weights of zero shot  model and finetuned model.
This could be used in continual learning.






[^1]: Wortsman, M., Ilharco, G., Kim, J.W., Li, M., Kornblith, S., Roelofs, R., Lopes, R.G., Hajishirzi, H., Farhadi, A., Namkoong, H. and Schmidt, L., 2022. Robust fine-tuning of zero-shot models. In Proceedings of the IEEE/CVF conference on computer vision and pattern recognition (pp. 7959-7971).

---

# Steering CLIP’s vision transformer with sparse autoencoders
CVPR Workshop on Mechanistic Interpratibility for Vision
Paper from MILA: Joseph, Suresh, Richards et al

Context: Foundation models often compress information about multiple different things to a single neuron weight (**polysemantic**), making these not very interpretable. In language models with transformers, sparse autoenoders (SAEs) have helped to make language models based on transformers interpretable, by learning using internal activations of transformer layers. Since only a few features are allowed to activate at once, it is forced to learn disentangled features making the vectors interpretable.

Now if we are able to understand which part of the ViT is responsible for classifying a particular task, we can make its learning rate higher when a similar kind of task appears, while keeping other parts less learnable (remember **SLCA**: Slow Learner with Classifier Alignment).


In the paper by Joseph et al [^2], authors train SAEs on CLIP's Vision transformer. They found that $$10-15\%$$ of neurons and features are steerable - which could be utilized. Another observation: The $$L_0$$ values of SAEs trained on spatial tokens are higher at center of image, with higher L0 values than the CLS token or the language model's SAEs. Thus, language and vision models could have different sparsity.

For an input activation $$x \in R^{d_{model}}$$ where $$R^{d_{model}}$$ is a set of feature vectors. SAE computes the following decomposition:
$$
\hat{x} + \epsilon (x) = \sum_{j=1}^{d_{SAE}} f_j (x) n_j + b + \epsilon (x)
$$

where $$n_j\in R^{d_{model}}$$ are normalized vectors and feature activations $$F_j(x)\in R$$ serves as sparse coefficients and $$b\in R^{d_{model}}$$
represents bias.

The papers `Interpreting CLIP with
sparse linear concept embeddings (spliCE).` and `eyond scalars: Concept-based
alignment analysis in vision transformers.`
 demonstrate CLIP's internal representations align naturally with human interpretable concepts.

Also SAEs are better than CBM since CBMs rely on LLM generated features, while SAEs are unsupervised based on model's internal representations.


### Models being trained:
CLIP ViT B/32 being used.
Vanilla SAE uses ReLU activation with sparsity induced by L1 reg and trained on Imagenet1K.

### How to Steer?
CLIP SAEs can be used to control feature activations: "manipulating SAE features to influence model outputs".

To measure steering effects, a feature f is selected, and its feature activation across all patches are replaced with steering strength s during forward pass.


*I didnt quite get how these features are obtained while unsupervised.*

What is SAE doing:
The base model's 768 dimension activation space is mapped to dictionary of $$768\times 64$$ features, with initial encoder weights set to transpose of decoder weights.

I didnt care about the evaluation metric here, so wont comment.









[^2]: Joseph, S., Suresh, P., Goldfarb, E., Hufe, L., Gandelsman, Y., Graham, R., Bzdok, D., Samek, W. and Richards, B.A., 2025. Steering CLIP's vision transformer with sparse autoencoders. arXiv preprint arXiv:2504.08729.

---

# Model Steering: Learning with a Reference Model Improves Generalization Bounds and Scaling Laws
 ICML 2025 Spotlight
 Authors: Wei, Lin, Yang et al





