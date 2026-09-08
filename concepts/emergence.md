# Emergence and emergent abilities

[The slingshot effect](slingshot.md) ← previous card, next → [Double descent](double-descent.md)

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

**Emergent abilities** are qualitatively new abilities of a model that appear abruptly (in a jump) when a critical threshold of **scale** is crossed (number of parameters, amount of data, compute) \[[1.1](#ref-1-1)\]\[[3.1](#ref-3-1)\]. In work on [grokking](grokking.md), emergence is studied as the same abrupt appearance of an ability, but governed by **training time** on small algorithmic tasks \[[1.2](#ref-1-2)\]\[[1.3](#ref-1-3)\].

## Elaboration

The term came from research on large language models: as **scale** grows (number of parameters, amount of data, compute), a new ability appears suddenly rather than smoothly \[[1.1](#ref-1-1)\]\[[3.1](#ref-3-1)\]. Grokking serves as a controlled "laboratory" model of the same phenomenon, but on small algorithmic tasks and without any growth of scale: grokking "resembles so-called emergent behavior in large language models" \[[1.3](#ref-1-3)\].

The mechanism connecting emergence with grokking is a **competition of two circuits** (two subnetworks within one model): a "memorising" one, which simply stores the training examples, and a "generalising" one, which implements the task's general algorithm. The visible jump in ability is the moment when the generalising circuit displaces the memorising one; the corpus examines this as [circuit efficiency](circuit-efficiency.md). The same frame unites grokking with [double descent](double-descent.md) (the non-monotone dependence of the test error on model or data size) and with emergent abilities \[[1.2](#ref-1-2)\]\[[1.5](#ref-1-5)\]\[[1.6](#ref-1-6)\].

Formally, emergence is described as a [phase transition](phase-transition.md). In the information-theoretic version its trigger is **feature synergy**: a formal quantity from the partial information decomposition — the share of information about the target that features carry only jointly and that none of them has on its own. Its synergistic contribution rises sharply at the point of transition \[[1.4](#ref-1-4)\].

The main dispute is **whether there is a genuine discontinuity here**: a true jump on the ability curve (rather than merely a steep but smooth rise) — or only its appearance. Some show that the sharpness is an **artefact of the metric**: a "mirage" arising from the hard thresholds by which "accuracy" is defined; on a smooth metric the transition smears out \[[2.1](#ref-2-1)\]. Others prove the transition to be **genuine**: it shows up synchronously in a set of **continuous [order parameters](order-parameter.md)**. An order parameter is a notion from statistical physics: a quantity that changes by a jump at the point of a phase transition; here it is an internal scalar metric of the model, independent of any accuracy threshold. A metric artefact could not produce their simultaneous discontinuity \[[3.1](#ref-3-1)\].

## Alternative definitions and nuances

### A. Emergent abilities at scale (scale-driven)

The canonical reading from the LLM literature (Wei et al.): a new ability appears **abruptly when a threshold of scale is crossed** — parameters, data or compute \[[1.1](#ref-1-1)\]\[[3.1](#ref-3-1)\]. The source of the difference: the driving parameter is **scale**, and the appearance is discontinuous (a step on the ability curve).

### B. Grokking as a time-driven analogue of emergence

Grokking (delayed generalisation on small tasks) is read as a **training-time-driven** version of emergence: the same sudden appearance of an ability, but without growth of scale; hence the unification of grokking, double descent and emergent abilities within a single circuit-competition frame \[[1.2](#ref-1-2)\]\[[1.3](#ref-1-3)\]\[[1.5](#ref-1-5)\]. The source of the difference: the driving parameter is **training time** rather than scale, and the phenomenon is studied mechanistically in toy models.

### C. Emergence as a structural event (a phase transition / a circuit)

A definition through a specific internal mechanism rather than through the shape of a curve: emergence = a **phase transition** brought about by synergistic interactions \[[1.4](#ref-1-4)\], or the **appearance of a generalising circuit** in the course of training \[[1.6](#ref-1-6)\]. The source of the difference: emergence is tied to a measurable structural event inside the network rather than to a jump of an external metric.

### Contested

- **Emergence as a metric artefact (a "mirage")** \[[2.1](#ref-2-1)\]: the sharpness of the accuracy curve arises only from the thresholds by which "accuracy" is defined; under a smooth metric the transition smears out. The source of the difference: emergence is not a property of the model but an artefact of the choice of metric.

### In support

- **Emergence as a genuine transition** \[[3.1](#ref-3-1)\]: its reality is proved by synchronous discontinuities of a set of **continuous** order parameters (independent of any accuracy threshold) — a direct refutation of the "emergence is a mirage" criticism. The source of the difference: co-located discontinuities of independent continuous probes, which a metric artefact would not produce.

## References

###### ref-1-1
**\[1.1\]** 2503.23298 — Wang et al., "Learning Towards Emergence: Paving the Way to Induce Emergence by Inhibiting Monosemantic Neurons on Pre-trained Models". [`"the phenomenon of a rapid performance increase once the model scale reaches a threshold"`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#p1-2).

###### ref-1-2
**\[1.2\]** 2402.15175 — Huang et al., "Unified View of Grokking, Double Descent and Emergent Abilities: A Perspective from Circuits Competition". [`"demonstrating how algorithm tasks can be turned into emergent abilities"`](../papers/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities/original/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities.md#p1-2).

###### ref-1-3
**\[1.3\]** 2303.11873 — Merrill et al., "A Tale of Two Circuits: Grokking as Competition of Sparse and Dense Subnetworks". [`"grokking resembles so-called emergent behavior in large language models"`](../papers/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks/original/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks.md#p1-4).

###### ref-1-4
**\[1.4\]** 2408.08944 — Clauw, Stramaglia, Marinazzo 2024, "Information-Theoretic Progress Measures reveal Grokking is an Emergent Phase Transition". [`"We attribute grokking to an emergent phase transition caused by the synergistic interactions between neurons as a whole"`](../papers/2408.08944.information-theoretic-progress-measures-reveal-grokking-is-an-emergent-phase-transition/original/2408.08944.information-theoretic-progress-measures-reveal-grokking-is-an-emergent-phase-transition.md#p1-2).

###### ref-1-5
**\[1.5\]** 2510.04930 — Saheb Pasand et al., "Egalitarian Gradient Descent". [`"grokking has been linked to phenomena such as double descent and emergent abilities"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p4-1).

###### ref-1-6
**\[1.6\]** 2601.09049 — He et al., "Is Grokking Worthwhile? Functional Analysis and Transferability of Generalization Circuits". [`"this transition is driven by the emergence of a **“Generalization Circuit”**"`](../papers/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers/original/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers.md#p1-7).

###### ref-1-7
**\[1.7\]** 2207.08799 — Barak et al., "Hidden Progress in Deep Learning: SGD Learns Parities Near the Computational Limit". Nuance: emergence is examined from the computational side — as a question about the success of gradient optimisation rather than about expressive capacity; transfer to real data is left open. [`"There is mounting evidence of *emergent phenomena* in the capabilities of deep learning methods as we scale up datasets, model sizes, and training times."`](../papers/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit.card.md#p1-2).\
Also: [`"the extent to which non-synthetic tasks (in, e.g., natural language processing and program synthesis) embed within them parity-like subtasks of exhaustive combinatorial search"`](../papers/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit.card.md#p11-1).

###### ref-1-8
**\[1.8\]** 2407.20199 — Mallinar et al., "Emergence in non-neural models: grokking modular arithmetic via average gradient outer product". Nuance: the emergence is attributed entirely to feature learning; along the compute axis the "mirage" of Schaeffer et al. is refuted, while along the data-size axis the authors themselves grant it. [`"we show that sharp emergence in modular arithmetic arises entirely from feature learning, independently of other aspects of modeling and training, and is not predicted by the standard measures of progress"`](../papers/2407.20199.emergence-in-non-neural-models-grokking-modular-arithmetic-via-average-gradient-outer-product/original/2407.20199.emergence-in-non-neural-models-grokking-modular-arithmetic-via-average-gradient-outer-product.md#p2-2).\
Also (the authors' concession): [`"unlike the emergence with respect to compute, emergence with respect to the training data size may be a “mirage” in the sense of [38]"`](../papers/2407.20199.emergence-in-non-neural-models-grokking-modular-arithmetic-via-average-gradient-outer-product/original/2407.20199.emergence-in-non-neural-models-grokking-modular-arithmetic-via-average-gradient-outer-product.md#p15-6)\
Also (on several skills): [`"it is possible that these skills are grokked at different rates"`](../papers/2407.20199.emergence-in-non-neural-models-grokking-modular-arithmetic-via-average-gradient-outer-product/original/2407.20199.emergence-in-non-neural-models-grokking-modular-arithmetic-via-average-gradient-outer-product.md#p10-1).
## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2310.06110 — Kumar et al., "Grokking as the Transition from Lazy to Rich". Contests the discontinuity of emergence: the sharpness is an artefact of the metric. [`"“Grokking” on the corresponding accuracy curves is thus a mirage arising from sweeping over thresholds"`](../papers/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics/original/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics.md#fig-18).

### In support

###### ref-3-1
**\[3.1\]** 2511.12768 — Hong et al., "Evidence of Phase Transitions in Small (Language) Models". Nuance: emergence is a genuine transition, proved by synchronous discontinuities of continuous order parameters (a refutation of the "mirage"). [`"new capabilities appear abruptly once models surpass critical thresholds of scale"`](../papers/2511.12768.evidence-of-phase-transitions-in-small-transformer-based-language-models/original/2511.12768.evidence-of-phase-transitions-in-small-transformer-based-language-models.md#p1-4).\
Also: [`"a genuine phase-transition-like reorganization rather than a gradual drift"`](../papers/2511.12768.evidence-of-phase-transitions-in-small-transformer-based-language-models/original/2511.12768.evidence-of-phase-transitions-in-small-transformer-based-language-models.md#p7-4).

###### ref-3-2
**\[3.2\]** 2308.15594 — Charton, "Learning the greatest common divisor: explaining transformer predictions". Nuance: a rare case where the content of the suddenly appearing ability is established by name (a divisibility test for a new prime) and without recourse to the weights; the control quantity is training time rather than scale — performance is the same from 300 thousand to 700 million parameters. The author does not use the word "emergent". [`"Experiments indicate that **transformers learn a sieve algorithm for computing GCD**."`](../papers/2308.15594.learning-the-greatest-common-divisor-explaining-transformer-predictions/original/2308.15594.learning-the-greatest-common-divisor-explaining-transformer-predictions.md#p9-4).\
Also: [`"trained model performance is stable over a wide range of model size (300 thousands to 700 millions parameters)"`](../papers/2308.15594.learning-the-greatest-common-divisor-explaining-transformer-predictions/original/2308.15594.learning-the-greatest-common-divisor-explaining-transformer-predictions.md#p13-1).

###### ref-3-3
**\[3.3\]** 2409.09281 — Lv et al., "Language Models “Grok” to Copy". Supports the time-driven reading: the jump in ability is obtained at a fixed 162M parameters, and the axis of the transition is the number of update steps and tokens seen. Nuance: the words "emergent" and "emergence" do not occur in the work, it measures no scaling thresholds, and the formulation itself is hedged ("we hypothesise"). [`"the grokked context copying doesn’t emerge until the optimization reaches a specific intensity"`](../papers/2409.09281.language-models-grok-to-copy/2409.09281.language-models-grok-to-copy.card.md#p3-4).

###### ref-3-4
**\[3.4\]** 2603.07323 — Truong, Truong, "Norm-Hierarchy Transitions in Representation Learning…". Nuance: an account through the training budget and the norm gap; the authors themselves call it a conjecture. [`"We stress that this is a theoretical conjecture generating testable predictions; empirical verification at scale is left to future work."`](../papers/2603.07323.norm-hierarchy-transitions-in-representation-learning-when-and-why-neural-networks-abandon-shortcuts/2603.07323.norm-hierarchy-transitions-in-representation-learning-when-and-why-neural-networks-abandon-shortcuts.card.md#p14-5).
###### ref-3-5
**\[3.5\]** 2310.17247 — Miller, O'Neill & Bui, "Grokking Beyond Neural Networks: An Empirical Exploration with Model Complexity". Nuance: a bridge from neural-network emergence to arbitrary learning systems: the phenomenon is reproduced in Gaussian processes, linear regression and a Bayesian network, and its only condition is declared to be that the search for a solution is governed by complexity and error. [`"grokking is not limited to neural networks but occurs in other settings such as Gaussian process (GP) classification, GP regression, linear regression and Bayesian neural networks"`](../papers/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity.card.md#p1-1).\
Also: [`"grokking may be possible in any model where solution search is guided by complexity and error"`](../papers/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity.card.md#p1-1).


###### ref-3-6
**\[3.6\]** 2307.09550 — Gokhale 2023, "The semantic landscape paradigm for neural networks". Emergence with scale is explained by percolation in $N$: growing the number of parameters widens the network's "vocabulary" (the model nodes), and a path to low-error models opens only at sufficiently large $N$; in the dispute over the "mirage of emergence" (Schaeffer et al.) a clear position is taken — emergence must mean the appearance of an *ability*, independently of loss metrics, and can be established only by a mechanistic analysis of the representations. Nuance: there is no experimental part at all — all four figures are schematics, and the abstract's "show" refers to reasoning rather than measurement. [`"The only real way to determine whether a new capability has emerged is to look under the hood and figure out what has changed in the network’s learned representations."`](../papers/2307.09550.the-semantic-landscape-paradigm-for-neural-networks/original/2307.09550.the-semantic-landscape-paradigm-for-neural-networks.md#p10-2).\
Also (the role of $N$): [`"Thus, the effect of increasing $N$ is to increase the number of nodes on the graph of heuristic models."`](../papers/2307.09550.the-semantic-landscape-paradigm-for-neural-networks/original/2307.09550.the-semantic-landscape-paradigm-for-neural-networks.md#p6-2).

###### ref-3-7
**\[3.7\]** 2509.21016 — Sun et al. 2025, "RL Grokking Recipe: How Does RL Unlock and Transfer New Algorithms in LLMs?". A contribution to the "sharpening or discovery" dispute about abilities under RLVR (Yue et al. and Wu et al. against ProRL): on a family where the reference model's pass@128 is zero, staged RL brings the full-pass rate to 100%, whence the conclusion that RL can discover strategies the base model did not execute. Nuance: the argument rests on an empirical pass@128 = 0 — 128 zero samples do not mean zero support of the distribution, and the dispute is precisely about the support; the authors themselves grant that in easy regimes RL only sharpens, and that the outcome depends on the reward, the data mixture and the difficulty; the corpus neighbour 2504.20571 (a delayed jump under RLVR on a single example, concluding that the ability is already in the base model) is not cited. [`"our staged RL training strategies enables the model to fully solve this family, achieving 100% full pass rate."`](../papers/2509.21016.rl-grokking-recipe-how-does-rl-unlock-and-transfer-new-algorithms-in-llms/2509.21016.rl-grokking-recipe-how-does-rl-unlock-and-transfer-new-algorithms-in-llms.card.md#p6-3).\
Also (the starting point): [`"where the reference model *Qwen3-4B-Instruct-2507* achieves **0% full pass rate at pass@128**"`](../papers/2509.21016.rl-grokking-recipe-how-does-rl-unlock-and-transfer-new-algorithms-in-llms/2509.21016.rl-grokking-recipe-how-does-rl-unlock-and-transfer-new-algorithms-in-llms.card.md#p6-3).
###### ref-3-8
**\[3.8\]** 2606.00230 — Muckatira, Shivagunde, Deshpande, Rumshisky 2026, "A Pre-Training Analogue of Grokking in Language Models: Tracing Delayed Grammatical Generalization". The "seen before unseen" delay is tied to the phenomenon (short for regular subject–verb agreement, longest for irregular participles and existential there) and reproduces at scales of 35M and 130M; and the smaller model reaches the validation threshold earlier than the larger one, which is explained by capacity at a fixed step budget (more tokens per weight — earlier extraction of what transfers) and offered as a conjecture. Nuance: "LLM pre-training" here means models of 35–130M weights and ~200M tokens of C4; all the delays observed amount to 1–9 checkpoints of 100 steps; and the sets on which proxy validation never reached 80% were filtered out before measurement. [`"The 35M model reaches the validation 80% threshold earlier than the 130M model on most datasets, despite being the smaller model."`](../papers/2606.00230.a-pre-training-analogue-of-grokking-in-language-models-tracing-delayed-grammatical-generalization/original/2606.00230.a-pre-training-analogue-of-grokking-in-language-models-tracing-delayed-grammatical-generalization.md#p12-1).

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2301.05217 — Nanda et al., "Progress Measures for Grokking via Mechanistic Interpretability". [`"Neural networks often exhibit emergent behavior, where qualitatively new capabilities arise from scaling up the amount of parameters, training data, or training steps"`](../papers/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability.card.md#p1-2).

**\[4.3\]** 2506.21551 — Li et al., "Grokking in LLM Pretraining?". [`"a mechanistic interpretation of its emergent generalization on downstream tasks"`](../papers/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test.card.md#p2-2).

**\[4.4\]** 2603.29262 — Zhang et al., "Grokking: From Abstraction to Intelligence". [`"Emergent capabilities (Elhady et al., 2025; Kaplan et al., 2020) in modern large language models"`](../papers/2603.29262.grokking-from-abstraction-to-intelligence/2603.29262.grokking-from-abstraction-to-intelligence.card.md#p1-3).\
Also (shedding bits): [`"The emergence of grokking is thus rigorously characterized as the system shedding algorithmic bits to transition from a complexity class of $\mathcal{O}(p^{2})$ to $\mathcal{O}(p)$."`](../papers/2603.29262.grokking-from-abstraction-to-intelligence/2603.29262.grokking-from-abstraction-to-intelligence.card.md#p8-1)

**\[4.5\]** 2306.17844 — Zhong et al. 2023, "The Clock and the Pizza". The notion is mentioned only in the related-work survey, together with a qualification about dependence on the choice of measure; the work does not apply the word "emergence" to its own transitions and does not vary model scale. [`"An ability is “emergent” if the performance on a subtask suddenly increases with growing model sizes, though such claims depend on the choice of metric [27]."`](../papers/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks/original/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks.md#p10-1).

**\[4.6\]** 2302.03025 — Chughtai et al., "A Toy Model of Universality: Reverse Engineering how Networks Learn Group Operations". Nuance: grokking is assigned to emergence by the authors' own word, and progress measures are presented as a device for understanding it; the work contains no experiments with model scale. [`"Grokking is a form of emergence, first reported by (Power et al. 2022)"`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p3-1).\
Also: [`"from mechanistic explanations as a methodology for understanding emergence"`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p6-10).

**\[4.7\]** 2305.18741 — Murty et al. 2023, "Grokking of Hierarchical Structure in Vanilla Transformers". The word "emergent" occurs only as a turn of phrase in retelling neighbouring work ("emergent linguistic structure", "emergent hierarchical structure in transformers"); the work does not apply it to its own findings, seeks no thresholds in scale, and its dependence on depth is not a threshold but an inverted U. [`"norm growth in transformers leads to attention saturation, an important property for emergent linguistic structure (Merrill et al. 2022)"`](../papers/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers/original/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers.md#p4-2).

**\[4.8\]** 2401.10463 — Zhu et al. 2024. Nuance: emergent abilities are mentioned once, in a list of discoveries about generalisation alongside scaling laws, double descent and grokking; there is no analysis of their own. [`"researchers have made a series of striking discoveries across generalization abilities, including neural scaling laws [4], double descent [11], grokking [15] and emergent abilities [23]"`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p1-3).

**\[4.9\]** 2406.06158 — Kunin et al., "Get rich quick: exact solutions reveal how unbalanced initializations promote rapid feature learning". Nuance: emergence appears in a single subordinate clause about grokking and with a reference to Nanda et al. 2023 — there is no definition, no measurement and no scaling in the work. [`"believed to be important towards understanding emergent phenomena [72]"`](../papers/2406.06158.get-rich-quick-exact-solutions-reveal-how-unbalanced-initializations-promote-rapid-feature-learning/2406.06158.get-rich-quick-exact-solutions-reveal-how-unbalanced-initializations-promote-rapid-feature-learning.card.md#p10-2).

**\[4.10\]** 2506.23286 — Jeffares & van der Schaar, "Not All Explanations for Deep Learning Phenomena Are Equally Valuable". Nuance: the work contains no analysis of emergence of its own and no measurements on language models. [`"this echos a similar point which has been made more generally on the so-called *emergent abilities* of large language models"`](../papers/2506.23286.not-all-explanations-for-deep-learning-phenomena-are-equally-valuable/original/2506.23286.not-all-explanations-for-deep-learning-phenomena-are-equally-valuable.md#p4-1).

**\[4.11\]** 2502.01774 — Carvalho et al. 2025, "Grokking Explained: A Statistical Phenomenon". [`"our observations of emergent behavior when training with very limited examples of a pattern that is nevertheless structured into classes and subclasses"`](../papers/2502.01774.grokking-explained-a-statistical-phenomenon/original/2502.01774.grokking-explained-a-statistical-phenomenon.md#p6-7).

**\[4.12\]** 2606.13753 — Truong et al. 2026, "The Weight Norm Sets the Grokking Timescale: A Causal Delay Law". Mentions emergence as a neighbouring family of sudden jumps and draws a lesson for itself from the dispute about discontinuous metrics: clearly defined control quantities and a finite-size analysis are needed. Nuance: its own transition measure nonetheless remains discontinuous (the first step at which validation accuracy is $\geq 0.9$), and it is defended not by continuity but by robustness — at thresholds of $0.8/0.9/0.95$ the measured norm changes by less than $2$%. [`"Emergent abilities [11] were argued by Schaeffer et al. 2023 to be partly an artifact of discontinuous metrics"`](../papers/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law.card.md#p4-2).


**\[4.13\]** 2402.09469 — Li, Liang, Shi, Song, Zhou, "Fourier Circuits in Neural Networks and Transformers: A Case Study of Modular Arithmetic with Multiple Inputs". [`"The phenomenon known as “grokking” was initially identified by [69] and is believed to be a way of studying the emerging abilities of LLM [99]"`](../papers/2402.09469.fourier-circuits-in-neural-networks-and-transformers-a-case-study-of-modular-arithmetic-with-multiple-inputs/original/2402.09469.fourier-circuits-in-neural-networks-and-transformers-a-case-study-of-modular-arithmetic-with-multiple-inputs.md#p6-2).

### External works

###### ref-5-1
**\[5.1\]** 2406.05335 — External work (demoted from the corpus): Nakaishi, Nishikawa, Hukushima 2024, "Phase transition in large language models and the criticality of natural languages". Nuance: the critical behaviour is not built into the architecture but arises during training, and two structures are acquired at different thresholds. [`"These results indicate that the model begins to acquire nontrivial structures of the natural language around $k_{c}\approx 10^{2}$, giving rise to a critical phase transition"`](../externals/2406.05335.phase-transition-in-large-language-models-and-the-criticality-of-natural-languages/original/2406.05335.phase-transition-in-large-language-models-and-the-criticality-of-natural-languages.md#p5-2).\
Also (the second threshold): [`"The difference between these two onsets suggests that the model acquires two distinct structures at different stages of training"`](../externals/2406.05335.phase-transition-in-large-language-models-and-the-criticality-of-natural-languages/original/2406.05335.phase-transition-in-large-language-models-and-the-criticality-of-natural-languages.md#p5-3).
```
concept:
  category: 1                    # 1. Phenomena
  papers_linked: 29             # distinct papers across the reference sections
  counted_at: 2026-08-27
```

###### ref-5-2
**\[5.2\]** 2408.12578 — An external work (excerpt): Lubana, Kawaguchi, Dick & Tanaka 2024, "A Percolation Model of Emergence: Analyzing Transformers Trained on a Formal Language". Gives the notion a working definition of three properties: a non-linear growth of the performance on a task, the simultaneity of such growth on several tasks, and the acquisition of a structure of the data-generating process. Nuance: the notion of structure is left deliberately informal, and the work has no checkable criterion of it. [`"In this sense, what is emergent is a structure, and what is observed is a change in the model’s capabilities."`](../externals/2408.12578.a-percolation-model-of-emergence-analyzing-transformers-trained-on-a-formal-language/2408.12578.a-percolation-model-of-emergence-analyzing-transformers-trained-on-a-formal-language.card.md#p4-4).
