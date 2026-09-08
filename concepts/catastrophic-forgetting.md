# Catastrophic forgetting

[Anti-grokking / generalisation collapse](anti-grokking.md) ← previous card, next → [Semi-grokking](semi-grokking.md)

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

**Catastrophic forgetting** is a network's abrupt loss of previously acquired knowledge when training continues on new data or on a changed distribution (the classical phenomenon, McCloskey & Cohen, 1989). In work on [grokking](grokking.md) it is used to account for the loss of an already reached generalising solution under further training \[[1.1](#ref-1-1)\].

## Elaboration

Varma et al. tie forgetting to grokking directly: [ungrokking](ungrokking.md) (the regression of a grokked network to poor test accuracy) is a **special case** of catastrophic forgetting, but with a qualification: ungrokking arises even when examples are merely removed from the training set, whereas classical forgetting usually involves *training on new* examples \[[1.1](#ref-1-1)\]. Prakash & Martin exhibit a concrete mechanism inside grokking: **[correlation traps](correlation-traps.md)** (anomalously large entries of the weight matrices) induce forgetting and accompany [anti-grokking](anti-grokking.md) \[[3.1](#ref-3-1)\]. Singh et al., in a continual-pretraining regime (a grokked model moves in sequence from one task to another), show that **knowledge distillation** (KD — training a model on another model's predictions) speeds generalisation up and **mitigates** forgetting \[[3.2](#ref-3-2)\].

## Alternative definitions and nuances

### A. Classical forgetting on a change of task (McCloskey & Cohen)

The canonical definition: a network fine-tuned on a new task or distribution abruptly loses its former skills \[[1.1](#ref-1-1)\]. The source of the difference: the driving factor is a **change of the training distribution**.

### B. Forgetting inside grokking (ungrokking as a special case)

In grokking, forgetting sets in even without a new task — when the dataset is reduced (ungrokking) or when spectral anomalies appear in the weights (correlation traps, anti-grokking) \[[1.1](#ref-1-1)\]\[[3.1](#ref-3-1)\]. The source of the difference: the loss of generalisation happens on the same task, for internal reasons of the dynamics.

### In support

- **Forgetting through correlation traps** \[[3.1](#ref-3-1)\]: spectral anomalies of the weight matrices induce catastrophic forgetting in the anti-grokking phase. The source of the difference: a concrete weight-level mechanism of forgetting inside grokking.
- **Mitigation by distillation** \[[3.2](#ref-3-2)\]: under continual pretraining of a grokked model, knowledge distillation weakens forgetting. The source of the difference: forgetting is treated as a removable defect of transfer.

## References

###### ref-1-1
**\[1.1\]** 2309.02390 — Varma et al., "Explaining grokking through circuit efficiency". [`"Ungrokking can be seen as a special case of catastrophic forgetting"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p6-6).\
Also (the difference): [`"ungrokking would arise even if we only remove examples from the training dataset, whereas catastrophic forgetting typically involves training on new examples as well"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p6-6).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2602.02859 — Prakash & Martin, "Late-Stage Generalization Collapse in Grokking: Detecting anti-grokking with WeightWatcher". Nuance: in grokking, forgetting is induced by correlation traps. [`"Correlation Traps can induce catastrophic forgetting and/or prototype memorization"`](../papers/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher/original/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher.md#p1-5).

###### ref-3-2
**\[3.2\]** 2511.04760 — Singh et al., "When Data Falls Short: Grokking Below the Critical Threshold". Nuance: knowledge distillation mitigates forgetting under continual pretraining of a grokked model. [`"KD both accelerates generalization and mitigates catastrophic forgetting, achieving strong performance"`](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p1-3).


### Stepping outside

###### ref-3-3
**\[3.3\]** 2507.20057 — Lyle et al., "What Can Grokking Teach Us About Learning Under Nonstationarity?". Brings a neighbouring phenomenon of continual learning into the corpus — *primacy bias*: the spoiling of generalisation on later tasks by earlier data; under the same name the authors subsume the "critical periods" of Achille et al. 2017. This is not forgetting: the network loses not what it learned but the ability to learn something new well. Nuance: a common mechanism with grokking is declared a conjecture — all that agrees is that one intervention helps in both settings, and no measure of feature learning is applied to both settings at once. [`"the *same fundamental process* by which a network replaces randomly initialized *memorizing* features with *generalizing* ones during grokking can be leveraged in continual learning problems to overwrite previously-learned features with new ones"`](../papers/2507.20057.what-can-grokking-teach-us-about-learning-under-nonstationarity/original/2507.20057.what-can-grokking-teach-us-about-learning-under-nonstationarity.md#p2-1).
###### ref-3-4
**\[3.4\]** 2606.26050 — Li, Sreedhar 2026, "Natural Ungrokking: Asymmetric Control of Which Rules Survive Pretraining". A counterexample to the usual frame: forgetting without a distribution shift, without removing data and without new data — a competing shallow prior (a corpus preference for *he*) displaces a rule within a single run on a stationary stream, while the construction stays solved; the contrastive margin crosses zero at the same 100-step checkpoint as the behavioural collapse, and the displacement reaches down into the representation — the decodability of the prompt's gender at the position of the prediction falls to chance ($0.56$) on the web data against a ceiling ($0.96$) on TinyStories, the margin being carried and lost by the contextual contribution while the direct embedding one stays pinned near zero. Nuance: the timing alignment — the central argument — rests on two seeds out of three (the third fails an instrumental guard); the deferred conflict slice of the focal family is 12 probes. [`"the displacement reaches down into the representation, upstream of the logits."`](../papers/2606.26050.natural-ungrokking-asymmetric-control-of-which-rules-survive-pretraining/original/2606.26050.natural-ungrokking-asymmetric-control-of-which-rules-survive-pretraining.md#p4-6).

###### ref-3-5
**\[3.5\]** 2607.29503 — Zhang, Chan, Shang, Zhang, Yang 2026, "The Grokked Illusion: True Equilibrium Mitigates Catastrophic Forgetting". A new experimental setting: a network that has already mastered $x+y\bmod 67$ to 100% test accuracy is additionally required to memorise **completely** 500 new noisy examples (a 99.8% training-accuracy threshold on the mixture), with the original data kept in training and fitted to 100%: the AdamW-trained network loses a quarter of its test accuracy (down to $75$% on random noise), the Wang–Landau equilibrium one holds at about $95$%, and the gap narrows along a ladder of structural closeness of the noise to the task (84% against >98% on $x^{2}+y\bmod 37$; 97% against ~100% on $x+y\bmod 37$). Nuance: the title itself is a stretch — what collapses is generalisation while the fit to the training data is preserved, not the memory of the sample (the authors stress this but do not change the term); one pretrained network of each kind is compared, and the ten seeds vary only the injection. [`"In stark contrast, the WLMD-equilibrium NN maintains approximately $95\%$ test accuracy on the original task after fully memorizing the random noise, demonstrating a substantial robustness advantage."`](../papers/2607.29503.the-grokked-illusion-true-equilibrium-mitigates-catastrophic-forgetting/original/2607.29503.the-grokked-illusion-true-equilibrium-mitigates-catastrophic-forgetting.md#p3-10).

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2601.09049 — He et al., "Is Grokking Worthwhile? Functional Analysis and Transferability of Generalization Circuits". [`"To prevent catastrophic forgetting of the original knowledge, we also retain a subset of 8,000 atomic facts"`](../papers/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers/original/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers.md#p4-3).

**\[4.2\]** 2512.03437 — Liang & Li, "Grokked Models are Better Unlearners". Nuance: flat minima cushion destructive forgetting, but a comparison with SAM shows that flatness alone is not enough. [`"confirming that flatter minima help buffer against catastrophic forgetting"`](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p19-3).

**\[4.3\]** 2308.15594 — Charton, "Learning the greatest common divisor: explaining transformer predictions". Nuance: catastrophic forgetting is named as what log-uniform sampling of the operands avoids — the distribution never changes during training, unlike in a curriculum. The paper has no experiment with a changing schedule and no measurement of forgetting. [`"This is related to curriculum learning, but avoids catastrophic forgetting, because the training distribution never changes."`](../papers/2308.15594.learning-the-greatest-common-divisor-explaining-transformer-predictions/original/2308.15594.learning-the-greatest-common-divisor-explaining-transformer-predictions.md#p9-8).
