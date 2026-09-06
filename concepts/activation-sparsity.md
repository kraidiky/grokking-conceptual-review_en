# Sparsity (activation and structural sparsity)

[sparse-solutions-hidden-progress](sparse-solutions-hidden-progress.md) ← previous card, next → [execution-manifold](execution-manifold.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**Sparsity** in the [grokking](grokking.md) corpus is a common name for three different observations: sparsity in the Fourier domain (few frequencies carry the computation), sparsity of structure (few weights or neurons take part in the answer) and sparsity of response (few activations are non-zero on an input). Their connection is the content of the notion: *"Nanda et al. (2023) observe sparsity in the Fourier domain after grokking, whereas we have found it in the conventional network structure as well"* \[[1.1](#ref-1-1)\].

Hence the working hypothesis of this line, stated so as to be testable: *"Grokked tickets are sparser subnetworks compared to the base model, and this higher degree of sparsity leads to the reduction in delayed generalization"* \[[1.2](#ref-1-2)\].

## Elaboration

**Sparsity as a consequence rather than a cause.** The hypothesis is tested honestly: models are built with the same sparsity as the grokked ticket, and one checks whether they speed generalisation up on their own \[[1.2](#ref-1-2)\]. Such a control separates "sparsity accompanies" from "sparsity causes" — a distinction that most mentions do not draw.

The mechanism by which sparsity arises is called, in the corpus, **selective norm growth**.

**Where it comes from.** The mechanism is called selective norm growth: not all weights grow alike, and part of the subnetwork stands out against the rest \[[3.1](#ref-3-1)\]. This ties sparsity to the line of the [weight norm](weight-decay.md) and explains why [weight decay](weight-decay.md) and sparsity are mentioned together as candidate explanations of the delay \[[3.2](#ref-3-2)\].

**Sparsity of response.** The third reading is about activations: generalising networks answer with fewer neurons, and a measure of "effective sparsity" is introduced to account for grokking \[[3.3](#ref-3-3)\]. This is the form closest to [polysemanticity](polysemanticity-superposition.md): the sparser the response, the more meaningful a neuron-by-neuron reading becomes.

**What is missing.** In the corpus sparsity is cited more often than it is measured over time: there are few sparsity curves standing next to accuracy curves, and it is exactly those that would separate it from [hidden progress](sparse-solutions-hidden-progress.md) as a measure in its own right.

## Alternative definitions and nuances

### A. Sparsity in the basis of the task

Few frequencies carry the computation — a form available wherever the algorithm is known \[[1.1](#ref-1-1)\]. The distinguishing feature is that the basis is set by the task rather than by the network, so the measure is comparable across models; the limitation is that outside modular arithmetic there is no such basis.

### B. Structural sparsity of a subnetwork

Few weights suffice for the solution; checked by pruning and lottery tickets \[[1.2](#ref-1-2)\], \[[3.1](#ref-3-1)\]. The source of the difference is the subject matter: not the response but the connectivity; the consequence is that sparsity is measurable without data, from the network alone.

### C. Sparsity of response

Few activations are non-zero on a typical input \[[3.3](#ref-3-3)\]. The distinguishing feature is the dependence on the data distribution: the quantity is defined relative to a sample, and a change in it may reflect a shift of the data rather than a rearrangement of the network.

## References

###### ref-1-1
**\[1.1\]** 2303.11873 — Merrill et al., "A Tale of Two Circuits: Grokking as Competition of Sparse and Dense Subnetworks". [`"Nanda et al. (2023) observe sparsity in the Fourier domain after grokking, whereas we have found it in the conventional network structure as well."`](../papers/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks/original/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks.md#p3-4).

###### ref-1-2
**\[1.2\]** 2310.19470 — Minegishi et al., "Bridging Lottery Ticket and Grokking: Understanding Grokking from Inner Structure of Networks". [`"**Hypothesis 2 (Sparsity):** *Grokked tickets are sparser subnetworks compared to the base model, and this higher degree of sparsity leads to the reduction in delayed generalization.*"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p7-3).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2303.11873 — Merrill et al., "A Tale of Two Circuits: Grokking as Competition of Sparse and Dense Subnetworks". Nuance: sparsity is derived from selective norm growth rather than postulated. [`"Motivated by the discovery of this sparse subnetwork, we now turn our attention to understanding why this subnetwork emerges and its structure."`](../papers/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks/original/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks.md#p3-4).

###### ref-3-2
**\[3.2\]** 2310.19470 — Minegishi et al., "Bridging Lottery Ticket and Grokking: Understanding Grokking from Inner Structure of Networks". Nuance: sparsity and the weight norm go through the corpus as a pair, two candidate explanations of the delay. [`"While factors such as weight norms and sparsity have been proposed to expla"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p1-2).

###### ref-3-3
**\[3.3\]** 2405.12755 — Golechha, "Progress Measures for Grokking on Real-world Tasks". Nuance: the third form is sparsity of response, for which a measure of effective sparsity is introduced. [`"Li et al. 2022 find sparse MLP layers in networks that generalize well"`](../papers/2405.12755.progress-measures-for-grokking-on-real-world-tasks/original/2405.12755.progress-measures-for-grokking-on-real-world-tasks.md#p3-6).
