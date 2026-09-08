# The Goldilocks zone

[Regularisation variants](regularization-variants.md) ← previous card, next → [The role of gradient noise (gradient noise / full-batch training)](gradient-noise.md)

[Concept card index](index.md), category: [4. Training and optimisation factors](index.md#cat-4)\
→ Next category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)\
← Previous category: [Modular arithmetic](modular-arithmetic.md)

## Definition

**The Goldilocks zone** is a narrow, "just right" region of a network's parameters (the metaphor comes from the tale of Goldilocks, who picks the porridge neither too hot nor too cold) inside which — and only inside which — the network attains generalisation. The notion was introduced by Liu et al. (2022) in application to [grokking](grokking.md): meaningful representation learning happens only in a "Goldilocks zone" lying between the regimes of [memorisation](memorization-phase.md) and "confusion" \[[1.1](#ref-1-1)\]. In Omnigrok the zone is formalised in weight space — as a narrow band (a spherical shell) of weight norm around a critical value, where generalisation is better than outside it \[[1.2](#ref-1-2)\].

![The phase diagram of the four training phases (comprehension, grokking, memorization, confusion): meaningful learning lives in a narrow zone (fig. 8 of Liu et al.)](assets/goldilocks-phase-diagram.png)

## Elaboration

The Goldilocks zone appeared in Liu et al.'s "[effective theory](effective-theory-statistical-mechanics.md) of representation learning": the authors distinguish four phases of training — comprehension, grokking, memorization and confusion — and show that meaningful representation learning goes on only in the intermediate "Goldilocks zone", between excessive memorisation and outright confusion \[[1.1](#ref-1-1)\]. In Omnigrok the same idea is carried into weight space: generalising solutions lie on a thin spherical shell — a narrow band of weight norm around a critical value — and grokking is explained by the network, under a large initialisation, first falling quickly into an overfitted solution of large norm outside the shell, after which [weight decay](weight-decay.md) (the regularisation penalising a large weight norm) slowly draws the weight vector radially into the zone, where generalisation switches on \[[1.2](#ref-1-2)\]. In this picture the control parameter is the weight norm, and the [phase transition](phase-transition.md) itself is the crossing of the zone's boundary. The idea is taken up and extended: Kumar et al. carry the "Goldilocks zone" over to the axis of training-set size (generalisation is possible but not immediate) and tie it to the passage from the "lazy" regime (near-kernel, with almost no [feature learning](feature-emergence-feature-learning.md)) to the "rich" one (active feature learning) \[[3.1](#ref-3-1)\]. A number of works, however, contest the rigidity of the picture: the requirement of a spherical shell in particular is called too strong, with a more complicated geometry of weight space conjectured \[[2.1](#ref-2-1)\], while others show that grokking happens outside the typical zone too, which makes the Euclidean (L2) weight norm an unreliable indicator of generalisation \[[2.2](#ref-2-2)\].

The shape of the curves by which the zone is recognised is called by Omnigrok the **LU mechanism**: as the weight norm changes, the training and the test loss trace the letters L and U.

## Alternative definitions and nuances

### A. The zone of representation learning (between memorisation and confusion)

Liu et al.'s original reading: the parameter defining the zone is the degree or quality of the learned representations, and the whole space of the network's behaviours is divided into four phases (comprehension, grokking, memorization, confusion). The Goldilocks zone is the middle corridor between two failures: excessive memorisation (the representations are under-learned, there is no generalisation) and "confusion" (the representations are destroyed). Useful representation learning goes on only inside that corridor \[[1.1](#ref-1-1)\].

### B. The weight-norm shell (Omnigrok)

Liu et al.'s reading in Omnigrok: the control parameter is the scalar weight norm; generalising solutions lie on a thin spherical shell (a narrow band of weight norm around a critical value). A large initialisation throws the network outside the shell into an overfitted solution, and weight decay then slowly draws it radially into the zone — which is what accounts for the delay in grokking \[[1.2](#ref-1-2)\]. The key difference from reading A: the zone is set by a directly measurable and controllable quantity (the weight norm) rather than by an abstract quality of representations — so one can enter the zone artificially, for instance by projecting the weights onto a sphere of the required radius.

### Contested

Miller et al.: the shell mechanism is plausible, but the requirement of a spherical zone in particular is "too stringent"; the real geometry of weight space appears to be more complicated than a spherical shell \[[2.1](#ref-2-1)\]. Notsawo et al.: grokking is observed even outside the typical Goldilocks zone, which makes the Euclidean (L2) weight norm an unreliable indicator of generalisation; other measures are proposed instead — activation sparsity and weight entropy \[[2.2](#ref-2-2)\].

### In support

Kumar et al. extend the "Goldilocks zone" from the axis of weight norm to that of training-set size: a "just right" amount of data is needed — enough for generalisation to be possible, but not immediate (in the limit of infinite data there is no grokking); being in such a zone is necessary but not sufficient for grokking to be observed \[[3.1](#ref-3-1)\]. They tie the same happy medium to the difficulty of the task in the sense of [NTK](neural-tangent-kernel-ntk.md) alignment (the agreement of the task with the network's tangent kernel) \[[3.1](#ref-3-1)\].

## References

###### ref-1-1
**\[1.1\]** 2205.10343 — Liu et al., "Towards Understanding Grokking: An Effective
Theory of Representation Learning". [`"representation learning to occur only in a “Goldilocks zone” (including comprehension and grokking) between memorization and confusion"`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p1-2).\
Also: [`"Both comprehension and grokking are able to generalize (in the “Goldilocks zone”)"`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p7-2).

###### ref-1-2
**\[1.2\]** 2210.01117 — Liu et al., "Omnigrok: Grokking Beyond Algorithmic Data". [`"There is a spherical shell in the weight space (the "Goldilocks" zone), where generalization is better than outside this zone"`](../papers/2210.01117.omnigrok-grokking-beyond-algorithmic-data/original/2210.01117.omnigrok-grokking-beyond-algorithmic-data.md#p2-3).\
Also: [`"CE produces a broader “Goldilocks zone" (the weight range where generalization happens) than MSE"`](../papers/2210.01117.omnigrok-grokking-beyond-algorithmic-data/original/2210.01117.omnigrok-grokking-beyond-algorithmic-data.md#p15-8).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2310.17247 — Miller, O'Neill, Bui 2024, "Grokking Beyond Neural Networks: An Empirical Exploration with Model Complexity". Contests: the requirement of a spherical zone in particular is too stringent, and in the Gaussian-process experiment no such geometry is observed. [`"the requirement of a spherical Goldilocks zone seems too stringent"`](../papers/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity.card.md#p3-1).\
Also (the empirical check): [`"we did not see a clear example of the spherical geometry mentioned in the Goldilocks zone theory of (Liu et al.(2023 a))"`](../papers/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity.card.md#p8-1).

###### ref-2-2
**\[2.2\]** 2506.05718 — Notsawo et al., "Grokking Beyond the Euclidean Norm of Model Parameters". Contests: grokking happens outside the zone as well, so the weight norm is unreliable. [`"it occurs even outside the typical “goldilocks zone”"`](../papers/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters/original/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters.md#p16-2).

###### ref-2-3
**\[2.3\]** 2311.18817 — Lyu et al., "Dichotomy of Early and Late Phase Implicit Biases Can Provably Induce Grokking". Contests: for homogeneous networks the norm does not bound expressivity, so a narrow zone in norm itself calls for an explanation rather than serving as one. Nuance: what is contested is the explanation, not the observation — the empirical recipe "large initialisation plus small non-zero weight decay" is taken from Liu et al. 2023 wholesale and is the starting point of the whole work. [`"it is impossible to explain the effect of norm just from the expressive power, since all classifiers that can be represented with a certain norm can also be represented by all other norms"`](../papers/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking/original/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking.md#p4-2).\
Also: [`"Fort and Scherlis 2019; Liu et al. 2023 did not provide much explanation on why such a narrow Goldilocks zone could exist in the first place"`](../papers/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking/original/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking.md#p4-2).


###### ref-2-4
**\[2.4\]** 2405.12755 — Golechha 2024, "Progress Measures for Grokking on Real-world Tasks". Contests: grokking is induced, with the weight norm steadily rising (roughly 100 → 400), by adding to the loss a term $-\delta\sum_{w\in\theta}|w|^{2}$ with $\delta=2e-10$, whence the conclusion that the phenomenon happens far outside the zone. Nuance: the zone itself is not measured — neither the critical norm $w_{c}$ nor the landscape of the reduced test loss over the norm, the only things by which Liu et al. define the zone, is constructed for this setting; what is shown is that the norm grows, not that it is outside the zone. The paper's own figure 1, in the unmodified setting, shows the norm falling simultaneously with generalisation — that is, confirming the target — and this is not reflected in the conclusions. [`"we refute this claim by showing that grokking can occur way outside this ”goldilocks zone”"`](../papers/2405.12755.progress-measures-for-grokking-on-real-world-tasks/original/2405.12755.progress-measures-for-grokking-on-real-world-tasks.md#p2-4).\
Also (the claim among the contributions): [`"generalization can occur way outside the “goldilocks zone” of low weight norm"`](../papers/2405.12755.progress-measures-for-grokking-on-real-world-tasks/original/2405.12755.progress-measures-for-grokking-on-real-world-tasks.md#p1-8).

###### ref-2-5
**\[2.5\]** 2505.11411 — Zhang, Shang, Yang, Zhang, "Is Grokking a Computational Glass Relaxation?". Contests the account of grokking through the evolution of the norm towards the Goldilocks zone alone: the toy optimiser WanD generalises with a norm growing to about 175 and with no constraints whatever. What matters is that both sides of the dispute are reproduced in a single work — hard rescaling to a norm of 30 does indeed nearly remove grokking. Nuance: the counterexample is narrowed by the authors themselves — the network's output is not scaled, and the Omnigrok tasks are not reproduced. [`"This provides strictly-defined counterexamples to theory attributing grokking solely to weight norm evolution towards the Goldilocks zone liu2022omnigrok"`](../papers/2505.11411.is-grokking-a-computational-glass-relaxation/original/2505.11411.is-grokking-a-computational-glass-relaxation.md#p1-2).\
Also (the opponent's recipe confirmed): [`"The training results, presented in Appendix Figure 6, show that grokking can be greatly eliminated under this condition."`](../papers/2505.11411.is-grokking-a-computational-glass-relaxation/original/2505.11411.is-grokking-a-computational-glass-relaxation.md#p7-1)\
Also (how the counterexample is narrowed): [`"but in a more strictly-defined context as we do not scale NN’s output, which could be taken as effectively changing the weight norm"`](../papers/2505.11411.is-grokking-a-computational-glass-relaxation/original/2505.11411.is-grokking-a-computational-glass-relaxation.md#p8-3).

###### ref-2-6
**\[2.6\]** 2606.13753 — Truong et al. 2026, "The Weight Norm Sets the Grokking Timescale: A Causal Delay Law". Demands a restatement of the weight-space derivation of the notion: the narrow band of norm in which grokking is observed turns out to be an attracting equilibrium of weight decay rather than a condition for generalisation — with the norm clamped, the network groks both above and below it, only more slowly or more quickly. The concentration of the value itself is not contested but tightened: the spread reported by Manir & Rupa ($14.5$%, one seed per setting) is reduced to $1\text{–}2$% by conditioning on the task and $\lambda$. Nuance: under LayerNorm the concentration of the total norm disappears altogether (spread $0.15\text{–}0.17$) and returns only in the unembedding, so the "zone" in its weight-space derivation is tied to settings where the norm sets the scale of the function. [`"not a value grokking requires, which is why grokking is observed above and below it"`](../papers/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law.card.md#p11-5).\
Also (what was tightened): [`"Our observational findings (§4) corroborate this rate-vs-threshold dissociation and tighten the concentration to CV $1$–$2\%$ by conditioning on task and $\lambda$"`](../papers/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law.card.md#p2-3).
### In support

###### ref-3-1
**\[3.1\]** 2310.06110 — Kumar et al., "Grokking as the Transition from Lazy to Rich". Nuance: a "Goldilocks zone" exists along the axis of data size as well. [`"being in the “goldilocks zone for data set size” is necessary but not sufficient to see grokking"`](../papers/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics/original/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics.md#p16-7).\
Also: [`"with grokking in a goldilocks somewhere in the middle, when the task is hard (in an NTK alignment sense)"`](../papers/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics/original/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics.md#p25-1).


###### ref-3-2
**\[3.2\]** 2603.25009 — Manir, Rupa, "A Systematic Empirical Study of Grokking…". [`"exhibiting a narrow “Goldilocks” regime in which grokking occurs, while too little or too much prevents generalization"`](../papers/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization.card.md#p1-3).\
Also (the width of the zone): [`"a factor-of-two step beyond the optimum collapses training entirely"`](../papers/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization.card.md#p10-2).
###### ref-3-3
**\[3.3\]** 2308.09543 — Hu, Chen, Saphra & Cho, "Delays, Detours, and Forks in the Road: Latent State Models of Training Dynamics". Nuance: an independent agreement from an unsupervised map of training: the "just right" fall of the norm is read through the Goldilocks-zone hypothesis. [`"the weight norm is slow to reach a shell of particular $L_{2}$ norm in weight space, previously called the “Goldilocks zone” (Fort & Scherlis 2018)"`](../papers/2308.09543.delays-detours-and-forks-in-the-road-latent-state-models-of-training-dynamics/original/2308.09543.delays-detours-and-forks-in-the-road-latent-state-models-of-training-dynamics.md#p12-3).

###### ref-3-4
**\[3.4\]** 2605.15787 — Hidajat, Stoll, An 2026, "Grokking as Structural Inference: Transformers Need Bayesian Lottery Tickets". The Goldilocks zone enters the theorem wholesale as a norm condition $\mathcal{N}$ ($\Vert\theta_{\text{MLP}}\Vert_{F}\in[r_{\min},r_{\max}]$), but is declared necessary and not sufficient: in a factorial experiment, norm fitting (projecting the MLP weights onto the hypersphere $r_{\max}$ at every step) with adversarial attention leaves the accuracy at chance, while oracle attention without norm control gives only partial generalisation. Nuance: the necessity of $\mathcal{N}$ is derived by the phrase "standard generalisation bounds prescribe", with references to Liu and Notsawo — that is a citation, not a derivation; the whole theory is derived for linear ReLU attention and "extended" to softmax by a hypothesis called "observationally complete" on the strength of curves agreeing. [`"Perfect generalization appears only when capacity control and structural routing are present together."`](../papers/2605.15787.grokking-as-structural-inference-transformers-need-bayesian-lottery-tickets/2605.15787.grokking-as-structural-inference-transformers-need-bayesian-lottery-tickets.card.md#p8-2).

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2309.02390 — Varma et al., "Explaining Grokking Through Circuit Efficiency". [`"it takes longer for regularisation to reduce parameter norm to the “Goldilocks zone” where generalisation occurs"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p10-6).

**\[4.2\]** 2405.19454 — Fan, Pascanu, Jaggi 2024, "Deep Grokking: Would Deep Neural Networks Generalize Better?". [`"the model needs to *grok* slowly into the *Goldilocks zone* (Fort & Scherlis, 2018) for generalization"`](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#p6-2).

**\[4.3\]** 2501.04697 — Prieto et al., "Grokking at the Edge of Numerical Stability". [`"weight norms need to be in a narrow range or “Goldilocks Zone” for generalization"`](../papers/2501.04697.grokking-at-the-edge-of-numerical-stability/2501.04697.grokking-at-the-edge-of-numerical-stability.card.md#p1-5).

**\[4.4\]** 2504.13292 — Xu et al., "Let Me Grok For You: Accelerating Grokking". [`"grokking through the concept of a “Goldilocks zone”, a spherical shell of weights"`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p3-1).

**\[4.5\]** 2510.04930 — Saheb Pasand et al., "Egalitarian Gradient Descent: A Simple Approach to Accelerated Grokking". [`"emerges in a specific zone for the weights of a network called the ”Goldilocks Zone”"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p4-1).

**\[4.6\]** 2511.04760 — Singh et al., "When Data Falls Short: Grokking Below the Critical Threshold". [`"slow formation of useful representations within a “Goldilocks zone” between memorization and confusion [16]"`](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p2-3).

**\[4.7\]** 2603.15492 — Acharya et al., "Grokking as a Variance-Limited Phase Transition". [`"Liu et al. [2] identified a "Goldilocks zone" of initialization and data size"`](../papers/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold/original/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold.md#p2-2).

**\[4.8\]** 2604.13123 — Truong et al., "Spectral Entropy Collapse as a Phase Transition in Delayed Generalisation". [`"Liu et al. (2022) described a “Goldilocks zone” of weight norms in which generalisation emerges"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p3-1).

**\[4.9\]** 2305.18741 — Murty et al. 2023, "Grokking of Hierarchical Structure in Vanilla Transformers". The notion is mentioned only in a survey of quantities tied to grokking; no zone is sought in the work and no boundaries in weight norm are drawn, while the whole subsequent analysis consists in the fact that the weight norm grows monotonically and is no good for telling successful architectures apart. [`"Liu et al. 2022 identify a “goldilocks zone” in weight norm space where grokking occurs"`](../papers/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers/original/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers.md#p4-1).

**\[4.10\]** 2507.20057 — Lyle et al., "What Can Grokking Teach Us About Learning Under Nonstationarity?". A mention only: the "Goldilocks zone" is cited as Liu et al. 2022b's position in the dispute over the causal arrow between norm and generalisation. The work neither seeks nor measures this zone, but its own argument shifts the sought "just right" quantity from the parameter norm to the ratio of the step norm to the parameter norm — which it does not call a "zone". [`"Liu et al. 2022b characterize grokking as the convergence of the parameter norm towards a “goldilocks zone” (Fort & Scherlis 2019) which allows for generalization"`](../papers/2507.20057.what-can-grokking-teach-us-about-learning-under-nonstationarity/original/2507.20057.what-can-grokking-teach-us-about-learning-under-nonstationarity.md#p3-2).
