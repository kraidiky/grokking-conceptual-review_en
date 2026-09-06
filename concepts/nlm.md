# Naive Loss Minimization

[comprehension-confusion-phases](comprehension-confusion-phases.md) ← previous card, next → —

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

**Naive Loss Minimization (NLM)** is the component of the gradient that **does not change the model's predictions** but lowers the cross-entropy loss by simply **scaling the logits** (the pre-softmax outputs) upwards; past the point of overfitting the gradient goes almost entirely into this direction of uncontrolled logit growth. It was introduced by Prieto et al. (2025) as the cause of the postponement of generalisation in [grokking](grokking.md) and of [Softmax Collapse](softmax-collapse.md) \[[1.1](#ref-1-1)\].

![Trajectories of the model over the loss landscape: with no interventions the optimisation goes off into the direction of naive loss minimization — a growth of the logits with no change of the predictions (fig. 7 of Prieto et al.)](assets/nlm-trajectories.png)

## Elaboration

Why NLM arises at all: under a cross-entropy loss even an already correctly classified example keeps giving a non-zero gradient — it can be reduced almost indefinitely simply by **inflating the scale of the logits** (usually through a growth of the weight norms along the current direction), without changing which class is predicted \[[1.1](#ref-1-1)\]. Prieto et al. show that it is precisely NLM that is responsible for the **postponement of generalisation** and that in the limit it leads to Softmax Collapse; to confirm this they introduce the [optimizer](optimizer-adam-adamw-sgd.md) **[⊥Grad](orthogonal-gradient-perp-grad.md)**, which keeps only the part of the gradient orthogonal to the NLM direction — and it groks without an initial overfitting phase \[[1.1](#ref-1-1)\]. Yıldırım takes NLM as the cause of the logit growth and therefore bounds the norm of the output layer (a bounded output) \[[3.1](#ref-3-1)\].

## Alternative definitions and nuances

### A. NLM as a component of the gradient (by definition)

A definition through the geometry of training: a direction in the gradient that does not change the predictions but lowers the loss by scaling the logits \[[1.1](#ref-1-1)\]. The source of difference: the notion is set by the shape of the gradient.

### B. NLM as the cause of the collapse and of the postponement (by role)

A definition through the consequences: the uncontrolled growth of the logits postpones generalisation and in the limit causes Softmax Collapse; it is removed by deleting this component (⊥Grad) or by bounding the output \[[1.1](#ref-1-1)\]\[[3.1](#ref-3-1)\]. The source of difference: the emphasis is on the functional role rather than on the definition.

### In support

- **NLM as the justification of a bounded output** \[[3.1](#ref-3-1)\]: Yıldırım takes NLM as the cause of the logit growth and therefore bounds the norm of the output (unembedding) matrix so as not to let it come to Softmax Collapse. The source of difference: the same notion is applied as an argument for an architectural constraint.

## References

###### ref-1-1
**\[1.1\]** 2501.04697 — Prieto et al., "Grokking at the Edge of Numerical Stability". [`"overfitting and cross-entropy loss push the model in a direction of uncontrolled logit growth"`](../papers/2501.04697.grokking-at-the-edge-of-numerical-stability/2501.04697.grokking-at-the-edge-of-numerical-stability.card.md#p2-4).\
Also (its nature): [`"does not change the predictions of the model but decreases the loss by scaling the logits"`](../papers/2501.04697.grokking-at-the-edge-of-numerical-stability/2501.04697.grokking-at-the-edge-of-numerical-stability.card.md#p1-2).\
Also (its role): [`"we validate that NLM is responsible for delaying generalization (Fig. 1, a to b) and leading to SC"`](../papers/2501.04697.grokking-at-the-edge-of-numerical-stability/2501.04697.grokking-at-the-edge-of-numerical-stability.card.md#p2-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2603.05228 — Yıldırım, "The Geometric Inductive Bias of Grokking: Bypassing Phase Transitions via Architectural Topology". Nuance: NLM is taken as the cause of the logit growth and motivates a bounded output layer. [`"This behavior—known as Naïve Loss Minimization—leads to numerical instability and Softmax Collapse"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p6-5).
