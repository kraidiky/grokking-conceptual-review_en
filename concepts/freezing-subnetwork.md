# Freezing a subnetwork / edge-popup

[StableMax / perp-Grad (numerical-stability fix)](numerical-stability-fix.md) ← previous card, next → [Spherical weight-norm constraint](spherical-weight-norm-constraint.md)

[Concept card index](index.md), category: [5. Interventions and methods](index.md#cat-5)\
→ Next category: [Progress measures](progress-measures.md)\
← Previous category: [Weight decay (L2 regularisation)](weight-decay.md)

## Definition

**Freezing a subnetwork / edge-popup** is a technique in which the weights of a network are fixed ("frozen") and not updated, while only the structure of the network is optimised: which connections (edges) to keep active and which to cut. Generalisation here is achieved not by changing the weights but by finding a good subnetwork inside an existing (randomly initialised or trained) one. The technique was brought into the context of [grokking](grokking.md) by Minegishi et al. through the edge-popup algorithm (Ramanujan et al., 2020), who showed that a memorising network can be turned into a generalising one by cutting connections alone, without a single weight update \[[1.1](#ref-1-1)\].

![The loss of the base model and of the "grokked ticket": the subnetwork found generalises without a delay (fig. 11 of Minegishi et al.)](assets/grokked-ticket-loss.png)

## Elaboration

Mechanically, edge-popup works like this: every weight is assigned a learnable score; the scores are updated by backpropagation, and on the forward pass the network uses only the edges with the highest scores (the top (1−k) at a pruning fraction k) — the weights themselves staying unchanged \[[1.1](#ref-1-1)\]. Such a subnetwork, giving good performance without any weight training, is called a "strong [lottery ticket](sparse-subnetwork-lottery-ticket.md)"; it is a strengthening of the lottery ticket hypothesis (Frankle & Carbin: a randomly initialised overparameterised network contains a sparse subnetwork trainable to good performance). The key thesis of Minegishi et al. is that the source of the accelerated generalisation is neither a lowering of the weight norm nor structural sparsity (the fraction of pruned connections) in themselves, but precisely the discovery of a "good structure": of three competing hypotheses (H1 — the weight norm, H2 — sparsity, H3 — structure), controlled experiments reject H1 and H2 and leave H3 \[[1.1](#ref-1-1)\]. The passage from the [memorisation phase](memorization-phase.md) to generalisation is, in this picture, synchronised not with a fall of the norm but with a rapid rearrangement of the subnetwork mask (measured by the Jaccard distance between masks at neighbouring checkpoints). The same methodological device — freeze the weights and optimise only a binary mask by structured pruning (cutting whole components: attention heads and MLP layers rather than individual weights) — is used by Bhaskar et al., but they carry it over to pretrained language models and contest the "competition of subnetworks" as an account of generalisation: instead of disjoint competing subnetworks they find a shared "heuristic core" (a set of attention heads present in all the subnetworks), and in their case the effective size (the size of the smallest subnetwork whose accuracy matches the full model's) grows under generalisation rather than falling as it does in grokking \[[2.1](#ref-2-1)\]. Freezing a subnetwork is thus both a generative instrument (inducing generalisation by cutting connections) and a diagnostic one (isolating and comparing subnetworks inside a fixed model); the interpretation of what exactly a "good subnetwork" explains remains disputed.

## Alternative definitions and nuances

### A. The generative reading: edge-popup finds a generalising subnetwork without changing the weights

A definition through the mechanism of inducing generalisation. The weights are frozen; only the mask is trained (through the edge-popup scores), and a memorising network passes into a generalising one without weight updates \[[1.1](#ref-1-1)\]. The distinguishing machinery: the [order parameter](order-parameter.md) here is the structural distance (the Jaccard distance) between subnetwork masks, not the weight norm; the cause of the acceleration is the discovery of a good structure, which is separated empirically from a lowering of the norm (H1) and from sparsity (H2) by controlled experiments. That is, freezing a subnetwork is read as a sufficient condition for generalisation: a structural search is enough, and weight updates are not required.

### B. The diagnostic reading: freezing the weights and structured pruning as an instrument for isolating subnetworks

A definition through analysis rather than induction. The model is frozen after fine-tuning and only a binary mask is optimised by structured pruning, in order to isolate different subnetworks that preserve the full model's behaviour and to compare their generalisation \[[2.1](#ref-2-1)\]. The difference from reading A: the aim is not to "switch on" generalisation by cutting connections but to decompose an already trained model and test the competing-subnetworks hypothesis; the freezing is needed for the subnetwork's faithfulness to the original model, and the source of difference between subnetworks is the random seed of the pruning.

### Contested

Bhaskar et al., applying the same freeze-and-prune to pretrained language models, contest the transfer of the "competing subnetworks" picture (on which generalisation is a switch from a dense memorising subnetwork to a sparse generalising one, with the effective size falling): instead of disjoint subnetworks they find a shared heuristic core of attention heads present in all subnetworks, including ones that do not generalise at all, and on the passage to generalisation the effective size does not fall but rises sharply \[[2.1](#ref-2-1)\]. That is, freezing a subnetwork transfers as a technique, but the conclusion "a good sparse subnetwork = generalisation" does not.

## References

###### ref-1-1
**\[1.1\]** 2310.19470 — Minegishi et al., "Bridging Lottery Ticket and
Grokking: Understanding Grokking from Inner Structure of Networks".
[`"pruning techniques like the edge-popup algorithm can identify these effective structures without modifying the weights"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p1-2).\
Also: [`"each weight is assigned a score, and these scores are updated through backpropagation"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p12-3); [`"generalization can be achieved solely through structural exploration without updating the weights"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p13-1); [`"rather to the discovery of good subnetworks"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p1-2).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2403.03942 — Bhaskar et al., "The Heuristic Core: Understanding Subnetwork Generalization in Pretrained Language Models". Contests: the transfer of "competing subnetworks" to pretrained language models — under generalisation the effective size grows rather than falls, and all the subnetworks share a common heuristic core. [`"We freeze the model after fine-tuning and only optimize the pruning masks to"`](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#p3-2).\
Also: [`"we use structured pruning"`](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#p1-6); [`"generalization in our case is accompanied by a sharp increase in effective size"`](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#p2-1); [`"generalization in simple algorithmic tasks"`](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#p1-2) (the very reading through competition of subnetworks that the work contests).

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2205.10343 — Liu et al., "Towards Understanding Grokking: An
Effective Theory of Representation Learning". [`"Some of the structure required for generalization exists before training hinting at a connection with the Lottery Ticket Hypothesis"`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p8-8).

**\[4.2\]** 2301.05217 — Nanda et al., "Progress Measures for Grokking via
Mechanistic Interpretability". [`"Returning to phase transitions, the lottery ticket-style explanation suggests that we might expect phase transitions as circuits form"`](../papers/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability.card.md#p35-3).



**\[4.3\]** 2402.16726 — Furuta et al., "Towards Empirical Interpretation of
Internal Circuits and Properties in Grokked Transformers on Modular Polynomials".
[`"The sparse lottery tickets in neural networks may also promote grokking (Minegishi et al., 2023)"`](../papers/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials/original/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials.md#p2-2).

**\[4.4\]** 2504.13292 — Xu et al., "Let Me Grok For You: Accelerating
Grokking". [`"Minegishi et al. (2024) demonstrated that the gap between memorization and generalization can be nearly eliminated if a lottery ticket, a set of sparse mask matrices, is applied to the model during training"`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p3-1).

**\[4.5\]** 2511.04760 — Singh et al., "When Data Falls Short: Grokking Below
the Critical Threshold". [`"lottery-ticket approaches [22], transferring embeddings from a weaker to a stronger"`](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p3-1).

**\[4.6\]** 2603.29262 — Zhang et al., "Grokking: From Abstraction to Intelligence". Nuance: the bypassing of forty intermediate layers is read as a selection for simplicity rather than as a by-product of a redundant architecture. [`"the model indeed effectively bypasses $\approx 40$ intermediate layers"`](../papers/2603.29262.grokking-from-abstraction-to-intelligence/2603.29262.grokking-from-abstraction-to-intelligence.card.md#p14-3)

**\[4.7\]** 2604.00316 — Tomàs, Mallinar, Belkin, "Breaking Data Symmetry is Needed For Generalization in Feature Learning Kernels". Nuance: an imposed initial feature matrix locks the model into a subgroup, and generalisation extends only to its orbit. [`"RFM is unable to *escape the symmetry*, and will only generalize to points within the orbit of that reflection"`](../papers/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels/original/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels.md#p7-4)

**\[4.8\]** 2503.23298 — Wang et al., "Learning Towards Emergence: Paving the Way to Induce Emergence by Inhibiting Monosemantic Neurons on Pre-trained Models". Nuance: the inhibition is applied only to the middle layers, judged to be the more polysemantic ones. [`"Besides, middle layers exhibit higher FKR, suggesting they are more polysemantic. This coincides with their role in abstraction and reasoning."`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#p15-1)

**\[4.9\]** 2405.16658 — Park, Kim, Kim, "Acceleration of Grokking in Learning Arithmetic Operations via Kolmogorov-Arnold Representation". Nuance: a freezing of a different kind from edge-popup — the trained weights of a whole module carried over from another task are fixed (the decoder block when transferring from operation to operation, the embedding layer when transferring to composition), and the rest is trained on. In the task with unknowns the freezing is partial: alongside the transferred embedding a new trainable layer is created for the new tokens. There is not a single "frozen versus trainable" comparison, so it is unknown how much of the acceleration is owed to the freezing and how much to the initialisation itself. [`"For learning a different commutative binary operation, the transferred decoder block is frozen, and only the embedding and classifier layer are learned."`](../papers/2405.16658.acceleration-of-grokking-in-learning-arithmetic-operations-via-kolmogorov-arnold-representation/2405.16658.acceleration-of-grokking-in-learning-arithmetic-operations-via-kolmogorov-arnold-representation.card.md#p15-2).\
Also: [`"it is not reasonable to freeze the entire embedding layer because these new tokens require their own representations"`](../papers/2405.16658.acceleration-of-grokking-in-learning-arithmetic-operations-via-kolmogorov-arnold-representation/2405.16658.acceleration-of-grokking-in-learning-arithmetic-operations-via-kolmogorov-arnold-representation.card.md#p16-3).
