# Solving English
## A proof-oriented agenda for complete, reusable lexical representations

**Research proposal · Version 2 · 2 November 2026**

## Summary

AI language models represent words using lists of numbers called embeddings. These representations help models recognize relationships among words and use them in sentences. But a useful representation is not necessarily a complete one: it may capture that a door permits passage while failing to preserve some of the word’s other senses, associations, or distinctions.

This proposal asks whether there is a finish line for this part of language learning. For a fixed collection of recorded language, can we construct a representation that preserves all the word meaning recoverable from that evidence? We call this ideal representation **E(C)**, where C is the evidence collection. The goal is exact completeness within that boundary, rather than merely strong performance on a handful of tests. Different numerical representations could preserve the same meaning equally well.

If complete—or sufficiently strong—lexical representations could be constructed and reused, they could become shared foundations for many AI models. A model could begin with an established representation of word meaning and learn how to use it in context. Potential benefits include lower training costs, shorter training times, and more controlled research experiments. More efficient inference could also follow if a better foundation permits a smaller downstream model. These possibilities are reasons to investigate the idea, not results already established.

The scientific ambition and the initial contribution have different scales. **The ambition is an industry-wide effort to discover complete lexical representations. Our contribution is to make that destination intelligible, formalize the questions, connect existing research, and provide an initial benchmark through which others can contribute evidence.** We do not propose to solve English or train a new large language model in this first project.

The work combines a proof-oriented framework with a small, reproducible evaluation suite for existing input embeddings. It distinguishes what can already be established mathematically from what remains a conjecture. The motivating possibility is that practically excellent approximations may be attainable well before exact completeness can be certified—and that pursuing this shared target could make lexical representation research more cumulative.

## 1. The target: accumulated lexical meaning

“Solving English” here means representing accumulated **lexical semantic content**: the senses, properties, relations, connotations, and usage restrictions associated with specified words or lexical units. It does not mean solving every possible sentence, future fact, or reasoning task.

For example, a representation of *bank* could preserve both its financial and geographical senses. Selecting the intended sense in a sentence remains a contextual operation. The boundary between lexical content, factual associations, and contextual interpretation requires explicit investigation; it cannot be settled by excluding difficult examples.

Two related conjectures motivate the project:

**Historical conjecture.** Up to a specified cutoff, a word has a finite history of actual usages. Its accumulated meaning is wholly determined by that history, including semantically relevant circumstances, and admits a finite complete representation. The claim that usage exhausts accumulated lexical meaning is a substantive premise. A finite number of occurrences does not alone establish a finite encoding of everything relevant about them.

**Recorded-evidence conjecture.** For a fixed finite collection of records $C$, all lexical semantic information recoverable under declared interpretation assumptions admits a finite complete representation with a useful, constrained means of access.

The recorded-evidence version is the initial formal target. It does not assume that recorded usages reveal everything in unrecorded history. Discovering another document changes $C$ and produces a new target version; it does not invalidate completeness relative to the original evidence. A date interval alone does not identify a corpus.

Exactness means **no loss of semantic distinctions within scope**. It need not mean certainty where evidence is ambiguous, nor exact reproduction of a preferred set of numerical coordinates. Interpretability, efficient construction, and downstream reuse are additional properties, not part of completeness by default.

## 2. Formal framework

### 2.1 Objects and notation

| Symbol | Meaning |
|---|---|
| $H$ | Complete historical usage record up to a cutoff, generally unavailable. |
| $C\in\mathcal C$ | A finite evidence collection in a declared class of admissible collections. |
| $V$ | The lexical inventory, with an explicit policy for senses and multiword expressions. |
| $B$ | Background interpretation assumptions, including conventions, inference rules, and any grounding assumptions. |
| $Q$ | The family of lexical questions or distinctions defining the semantic scope. |
| $S_B(C,q)$ | The answer supported by the evidence and assumptions for question $q$; it can preserve uncertainty or alternatives. |
| $E(C)$ | An ideal complete lexical representation. $E$ denotes the extraction map; its existence does not establish an executable algorithm. |
| $\widehat E(C)$ | A learned candidate approximation, pronounced “E hat.” |
| $T,U_T$ | A tokenizer and its decoder. Losslessness means $U_T(T(C))=C$. |
| $A,b$ | A learning procedure, including architecture and objective, and its resource budget. |
| $D\in\mathcal R$ | A readout and the permitted class of readouts. |
| $\mathcal K$ | Representation and access constraints: storage, width, numerical encoding, and readout complexity. |
| $\ell,\Delta_C$ | Discrepancy between answers and overall semantic error. |

A **readout** is the procedure used to extract an answer from a representation. Cosine similarity, projection onto a size direction, and a trained linear category classifier are different readouts. Their capabilities differ, so “information is present” must be accompanied by an account of how it is accessed.

A candidate is produced schematically by

$$
\widehat E_{T,A,b}(C)=A_b(T(C)).
$$

The subscripts can be omitted once the experimental conditions are clear. The notation $E(C)$ also suppresses dependence on $V,B,Q,\mathcal R,\mathcal K$; these choices must be declared. Neither $B$ nor the readout should conceal a corpus-specific database of answers. Dictionaries, annotations, and pretrained evaluators can contribute external information and must be identified as evidence, assumptions, or evaluation resources.

### 2.2 Completeness

A representation and readout are complete on the declared corpus class if

$$
\forall C\in\mathcal C,\ \forall q\in Q:\qquad
D(E(C),q)=S_B(C,q).
$$

**In words:** every lexical answer obtainable from the evidence under the declared assumptions is obtainable from the representation through the allowed readout.

The readout receives no separate access to $C$. A shared readout across a corpus class, together with limits on its parameters and computation, helps prevent the entire semantic resource from being hidden in the decoder. Uniformity alone is not sufficient; complexity must also be accounted for.

Raw corpus storage preserves information but is not the intended lexical foundation. Arbitrary word identifiers plus an unrestricted downstream answer database are similarly uninformative. The central research problem is to find constraints $\mathcal K$ that exclude those trivial solutions without assuming in advance a small dimension, linear geometry, or interpretable basis.

The query family must characterize the intended semantic scope rather than merely reproduce a convenient benchmark. Defining a defensible $Q$ and $S_B$ is a major open task, not something solved by introducing notation.

### 2.3 Error, approximation, and equivalence

For a candidate and declared readout, define

$$
\Delta_C(\widehat E(C),D)
=
\sup_{q\in Q}
\ell\bigl(D(\widehat E(C),q),S_B(C,q)\bigr),
$$

where $\ell$ is nonnegative and equals zero only when the semantic answers agree.

**In words:** compare the candidate’s answer with the evidence-supported answer for every question in scope, and take the worst-case discrepancy. The supremum is the least upper bound, including cases where no single question attains that bound. Zero error means every answer agrees, including any uncertainty the target itself preserves.

A finite benchmark tests only a subset of these questions. Average scores can conceal rare missing distinctions, and benchmark saturation is not a proof of completeness.

Arbitrarily good approximation and exact attainment are separate claims. Errors $1,1/2,1/3,\ldots$ approach zero but never reach it. Zero is their **infimum**, or greatest lower bound; there is no attained minimum. A fixed nonempty finite set of permitted representation/readout pairs does have a best member, but its error may remain positive.

We therefore distinguish the ideal target, the best achievable error under declared constraints, and the candidate actually learned. The best constrained solution may still have practical value even if it cannot reach exact completeness.

Two representation/readout pairs are semantically equivalent when they give the same answers throughout $Q$. Different coordinates need not imply different semantic content. Linear or orthogonal equivalence requires additional assumptions; it does not follow from equal performance or semantic agreement alone.

## 3. Supporting lemmas and their limits

These elementary results establish foundations. They are not presented as mathematical novelties or as a proof that English is solved.

### Lemma 1: finite evidence has a finite lossless encoding

If $C$ contains $N$ bits, those bits preserve its recorded information. If the answer function $S_B(C,q)$ is computable by a fixed finite program, the corpus and program provide a finite generative description of all its answers, even for an infinite query family.

**Proof sketch.** Store $C$ and execute the answer program on it and $q$.

**Significance.** Finiteness provides an information source with a finite description. It does not establish semantic organization, efficient extraction, or computability of arbitrary questions. Applying the argument to $H$ additionally requires a finite description of all semantically relevant circumstances.

### Lemma 2: lossless tokenization preserves the evidence target

If $U_T(T(C))=C$, then any map $F$ on the original evidence can operate on tokenized evidence through decoding:

$$
(F\circ U_T)(T(C))=F(C).
$$

**Proof sketch.** Substitute the lossless-decoding identity.

**Significance.** Lossless tokenizers preserve the same source information. They need not be equally easy for a fixed learner to use. The identity must include relevant boundaries and metadata; lossy normalization is outside the premise. Tokenizer optimization is not an initial project commitment.

### Lemma 3: a finite lexical answer matrix has an exact linear representation

For a finite inventory and $m$ numeric unary queries, let $M$ contain their answers, one word per row and one query per column. If $\operatorname{rank}(M)=r$, an exact factorization

$$
M=FW
$$

exists with $r$ embedding coordinates in $F$, and no exact linear factorization uses fewer.

**Proof sketch.** A rank factorization supplies the factors; conversely, a factorization with width $d$ has rank at most $d$.

**Corollary.** Two minimal rank-$r$ factorizations of the same matrix are related by an invertible change of coordinates:

$$
F_2=F_1R,\qquad W_2=R^{-1}W_1.
$$

Both embedding factors span the column space of $M$, so their bases differ by an invertible matrix. $R$ need not be orthogonal.

**Significance.** In a restricted setting, exact representation, minimum width, and equivalence can be proved. This does not show that a finite unary query matrix covers English, or that its rank is English’s intrinsic dimension. Rational answer matrices admit finite rational factorizations; arbitrary real factors and fixed-precision hardware must not be conflated.

### Lemma 4: reversible coordinates preserve recoverability when the readout compensates

For an invertible transformation $g$, define

$$
D_g(x,q)=D(g^{-1}(x),q).
$$

Then $D_g(g(E(C)),q)=D(E(C),q)$.

**Proof sketch.** The inverse cancels the transformation.

**Significance.** Coordinate changes need not change content. The claim holds only if the compensating readout is permitted. Restricted readouts can make some orientations more accessible than others. Interpretability and completeness remain separate.

### Lemma 5: indistinguishable evidence cannot select conflicting interpretations with certainty

If two admissible interpretations give identical available evidence but different required answers, a procedure using only that evidence cannot guarantee the correct selection in both cases.

**Proof sketch.** Its input is identical in the two cases. Randomization cannot give certainty for both conflicting answers either.

**Significance.** The target must preserve unresolved alternatives, justify additional assumptions, or incorporate additional evidence. Exact preservation of ambiguity is compatible with zero semantic loss.

### Lemma 6: partial tests cannot distinguish candidates that agree on those tests

If two admissible candidates agree on all tested queries but differ elsewhere, the test observations do not distinguish them.

**Proof sketch.** Their observed outputs are identical.

**Significance.** Passing a benchmark cannot establish unrestricted completeness without further structure. Proving that a finite **determining set** of questions fixes every answer in a wider family would be a substantive advance.

## 4. The open proof agenda

| Claim | What remains to establish |
|---|---|
| Semantic specification | A defensible account of lexical scope, evidence-relative answers, and ambiguity. |
| Constrained existence | A finite complete representation with meaningful storage and access constraints, beyond storing the evidence verbatim. |
| Extraction | An executable method for obtaining the representation; efficient construction is a further question. |
| Approximation | Conditions under which candidate errors can approach zero, distinguished from finite-time exact attainment. |
| Structural equivalence | Which semantic relations are preserved across complete solutions, and what additional assumptions imply stronger isomorphisms. |
| Certification | Whether determining sets, structural constraints, or other arguments can support completeness claims beyond sampled tests. |
| Efficient reuse | Whether strong lexical foundations help varied downstream models enough to justify their construction and integration costs. |

Three formal directions merit attention. **Semantic sufficiency** asks what representation preserves all answers relevant to the declared scope, connecting to sufficient statistics and information bottleneck work [1]. A probabilistic formulation requires a declared distribution rather than treating a single fixed corpus as a nontrivial random variable.

**Semantic equivalence classes** identify corpora that agree on all answers in $Q$. This defines an abstract target structure but does not supply an efficient or computable canonical encoding. Any equivalence obtained by definition must be distinguished from an empirical discovery of shared structure.

**Resource bounds** investigate storage, width, precision, and readout cost jointly. A sufficiently unrestricted matrix can encode other finite structures, so claims of matrix limitations require explicit constraints. If a gap is proved under those constraints, identifying what must change would itself be valuable research; no particular replacement representation is presumed superior.

Exact semantic agreement does not require exact numerical coordinates. Rounding matters if it destroys a needed distinction, but suitable separation or encoding may preserve all answers. We have no basis yet for declaring precision, dimensionality, or computational complexity the dominant obstacle.

The initial paper should provide clear conventional proofs. Formal verification is not a planned deliverable. A new nontrivial theorem would strengthen the work, but the agenda and benchmark should not depend on disguising elementary facts as novel results.

## 5. Prior research as parts of a shared agenda

| Research direction | Connection to the proposed target | What it does not establish |
|---|---|---|
| Distributional learning | Skip-gram factorization connects learned embeddings to explicit corpus statistics [2]. | Recovery of those statistics is not recovery of all lexical meaning. |
| Relevant-information preservation | Information bottleneck work formalizes retaining information about a specified target [1]. | It does not identify the complete lexical target for English. |
| Shared geometry | ICA findings and the Platonic Representation Hypothesis motivate investigating correspondence between learned spaces [3,4]. | Agreement can coexist with shared omissions. |
| Calibrated comparison | Work revisiting representation convergence identifies similarity-measure confounds and proposes calibration [5]. | Uncalibrated alignment is not evidence of semantic completeness. |
| Lexical evaluation | QVEC and QVEC-CCA evaluate correspondence with linguistic resources [6,7]. | Resource coverage is partial. |
| Contextual-to-static extraction | Context aggregation and distillation construct static lexical representations from contextual models [10,11]. | Successful distillation does not establish complete semantic recovery. |
| Earlier access to capabilities | Self-distillation and LayerSkip investigate transferring knowledge toward shallower computation or training useful early predictions [12,13]. | Earlier availability alone does not quantify semantic coverage or savings. |
| Interpretability | Rotation, axis labeling, and description evaluation such as FADE address how content is exposed and explained [8]. | Readable descriptions do not certify completeness. |

The grounding objection also matters. Bender and Koller distinguish **linguistic form**—the observable symbols and their patterns—from meaning involving their relationship to communicative intentions and the world [9]. Their argument challenges claims that text is self-interpreting. Our response must be to specify what evidence and background assumptions make semantic distinctions identifiable, not to assume the objection away or claim it rules out useful lexical structure.

The literature review must establish the proposal’s differences from semantic-primitives research, universal semantic-dimension proposals, sufficient representations, and existing embedding evaluation and reuse. The organizing framework is our proposed synthesis; it need not have been the original objective of the cited authors. Novelty remains to be established.

## 6. Initial empirical contribution: a shared lexical benchmark

The principal code contribution is a small, reproducible benchmark for **knowledge accessible in input embedding tables under declared readouts**. It should make missing distinctions visible and let researchers compare candidates systematically. It is evidence toward the agenda, not a numerical oracle for distance to the unknown ideal.

| Test family | Illustrative target | Initial evaluation approach |
|---|---|---|
| Similarity and relatedness | Cat–dog versus cup–coffee | Cosine comparisons against independent judgments; distinguish similarity from association. |
| Category intrusion | Dog, rabbit, horse, hammer | Identify an intruder, including difficult alternatives. |
| Category organization | Animals, tools, foods, vehicles | Clustering assessed with withheld labels. |
| Graded properties | Typical animal size | Predetermined projections compared with independent orderings. |
| Semantic attributes | Aquatic, manufactured, capable of flight | Small linear probes tested on unseen words. |
| Factual associations | Paris–France | Rank plausible alternatives without equating association with a specific relation. |
| Relation discrimination | Capital–country versus other city–country pairs | Constrained decoders with held-out entities. |
| Linguistic properties | Number, part of speech, sentiment | Separate linguistic categories and semantic targets in reporting. |
| Cross-language correspondence | A word and its translations | Retrieval with explicit token-form and vocabulary coverage. |

**Initial scope.** Implement a few families well—provisionally graded properties, category intrusion, and semantic attributes—and report baseline results for a small selection of existing input tables. The remaining families define an extension interface, not obligations for the first release. Reuse suitable existing datasets where their provenance, licensing, and evaluation design permit.

Declare the readout, supervision, splits, and preprocessing. Include matched random-vector and shuffled controls, plus nuisance baselines where spelling or frequency could explain results. Keep lexical families and token-form variants from leaking across train/test splits. Report coverage separately from performance conditional on coverage; a shared whole-word subset is an experimental simplification, not a claim that subword semantics are absent. Where learned probes are used, disclose their capacity and use multiple seeds.

External evaluation resources are operational checks of candidate representations; they are not automatically facts recoverable from a model’s documented $C$. Record known training provenance and avoid claiming equal-evidence comparisons when corpora differ or are unavailable. Both successes and failures need interpretation: a poor score can reflect the readout, missing evidence, or missing representation.

**Community contribution.** Publish versioned task definitions, baseline scripts, scoring conventions, and a process for proposing missing distinctions or challenging labels. Encourage routine reporting of input-embedding results alongside model evaluations. Maintain stable comparison sets while protecting or refreshing independent tests against benchmark overfitting. Contributions should improve coverage and diagnosis rather than chase an aggregate score mistaken for completeness.

Input tables are the initial scope. Models also have output/unembedding matrices, sometimes sharing weights with the input table. Their role should be acknowledged when interpreting results and future reuse, but a separate output-embedding evaluation program is not required here.

A compact worked example of the finite-matrix lemma can illustrate exact recovery and a candidate that passes partial tests while missing a distinction. It remains an explanatory supplement, not a new factorization method or a substitute for the benchmark.

## 7. Directions enabled by the framework

These are questions for later work and community participation, not a commitment to implement every experiment in the first project.

**A reusable foundation.** The clean starting point is to freeze a candidate $\widehat E(C)$ and train a fresh downstream model around it. An adapter could connect different embedding and model widths. Does this improve learning efficiency or quality compared with learning the lexical foundation jointly? Starting with previously trained downstream weights is a potential cost optimization, but introduces interface compatibility problems that are unnecessary for stating the conjecture. Future comparisons should account for foundation construction costs and appropriate learned and random baselines.

**Upstream compression.** We hypothesize that lexical semantic knowledge distributed across a model’s layers can be compressed into its embedding representation, concentrating that knowledge in a reusable lexical foundation. Here the proposed compression concerns the distributed representation of lexical meaning itself. Reduced downstream reconstruction, interference, or resource requirements are possible consequences. Establishing this hypothesis requires evidence that meaning has been consolidated, with appropriate accounting for storage and decoding; no compression ratio follows merely from counting layers.

This motivates an intended division of labor: upstream parameters hold reusable lexical semantic knowledge, while downstream components learn contextual interpretation, composition, reasoning, and additional knowledge. Downstream processing is not wholly “non-semantic,” and the best allocation remains an empirical question.

**Candidate construction.** A contextual model can be an instrument for recovering lexical structure, as demonstrated by contextual-to-static extraction and distillation [10,11]. The ideal need not be learned directly from simple co-occurrence statistics. A static representation must preserve alternative senses rather than blindly average away contextual differences; the preferred extraction objective remains open.

**Richer diagnostics.** Small nonlinear readouts or contextual evaluators could examine what limited computation can learn to use from frozen embeddings. They also learn from their supervision, so capacity and sample-efficiency comparisons matter. Optional layer-wise tests could examine where lexical capabilities become accessible, using contexts that do not supply the answer. Neither extension replaces the initial table-level suite or certifies completeness.

**Rotation and semantic labels.** Improving completeness and improving interpretability are independent endeavors. Alongside better $\widehat E(C)$, researchers can seek a rotation $\widehat R$ that improves semantic alignment under a declared labeling objective. There need not be a unique optimal orientation. A stable lexical foundation allows its orientation to be chosen before training a fresh downstream model, avoiding the specific problem of rotating inputs after downstream weights have learned a different interface. Freezing alone does not repair an already-trained model, and rotation cannot recover information absent from the original representation.

## 8. Benefits, uncertainties, and tests of the vision

A collective search for $E(C)$ could make lexical knowledge a shared, progressively validated research resource. Laboratories could contribute better candidates, independent tests, or results identifying constraints that prevent completeness. This would create a common destination while allowing different architectures and discovery methods.

If strong representations can be reused efficiently, concrete benefits could include lower accelerator costs and shorter training times, lower optimizer-memory requirements, and less researcher time spent rebuilding lexical foundations or disentangling embedding differences from downstream architecture effects. A common foundation could also help diagnose missing **lexical semantic knowledge** separately from failures to use it. Inference could become more efficient if that foundation permits a smaller or less computationally demanding downstream model.

These benefits do not require us to certify exact completeness before useful approximations are deployed. Conversely, completeness alone does not guarantee them: interface cost, construction expense, and downstream requirements matter. Freezing weights by itself does not reduce inference work.

Embedding importance may vary with model size. A modest descriptive analysis can report input-table parameters, $P_{\mathrm{embed}}=|V|d$, relative to total parameters for selected models, including weight tying. Parameter share is not FLOP share or a savings estimate. Practical effects on training and inference require downstream measurements beyond the initial benchmark.

The central weaknesses are unresolved semantic scope, potential triviality under unrestricted encodings, uncertainty about efficient extraction, and incomplete evaluation. Exactness may be unattainable under particular resource constraints; even then, characterizing the best constrained approximation or proving a gap could be valuable. We should identify limitations before proposing particular architectural remedies.

Finiteness does not prove learnability or tractability. Model agreement does not prove completeness. A failed optimizer or transfer experiment does not disprove the general conjecture. A meaningful negative result would establish a missing distinction or an impossibility under clearly stated assumptions. A meaningful positive result could establish a determining set, a nontrivial existence or equivalence result, or reproducible improvements in coverage and practical reuse.

Finally, preserving a corpus’s lexical content does not ensure factual correctness, fairness, or universal agreement. Evidence versions, provenance, community variation, and resource rights remain relevant to any shared foundation.

## 9. Focused deliverable and broader ambition

**The initial project will deliver:** a readable position and research proposal with a precise formal core; short proofs distinguishing established consequences from conjectures; a synthesis of related work; and an initial open benchmark with baseline results on selected input embeddings. The first formal milestone is a concrete, worked specification of semantic scope and readout constraints. The first empirical milestone is a small set of tests whose outputs can be independently reproduced and scrutinized.

It does not commit to a new large model, downstream retraining study, distillation algorithm, output-embedding suite, or formal-verification project. Those are opportunities for subsequent work, not prerequisites for the initial contribution.

**The broader ambition is to make complete lexical representation a shared scientific target.** Practically excellent approximations may be within reach even while exact certification remains difficult. Demonstrating that possibility, identifying its limits, and building reusable foundations would have consequences across AI research and deployment. This project aims to give that effort a clear question, a disciplined mathematical language, and an empirical starting point.

## Selected references

These references support specific connections and objections; they do not constitute an exhaustive novelty assessment.

1. Tishby, Pereira, and Bialek. **The Information Bottleneck Method** (1999; arXiv 2000). [Paper](https://arxiv.org/abs/physics/0004057).
2. Levy and Goldberg. **Neural Word Embedding as Implicit Matrix Factorization** (2014). [Paper](https://papers.neurips.cc/paper_files/paper/2014/hash/b78666971ceae55a8e87efb7cbfd9ad4-Abstract.html).
3. Yamagiwa, Oyama, and Shimodaira. **Discovering Universal Geometry in Embeddings with ICA** (2023). [Paper](https://aclanthology.org/2023.emnlp-main.283/).
4. Huh, Cheung, Wang, and Isola. **Position: The Platonic Representation Hypothesis** (2024). [Paper](https://proceedings.mlr.press/v235/huh24a.html).
5. Gröger, Wen, and Brbic. **Revisiting the Platonic Representation Hypothesis: An Aristotelian View** (2026). [Paper](https://proceedings.mlr.press/v306/groger26a.html).
6. Tsvetkov et al. **Evaluation of Word Vector Representations by Subspace Alignment** (2015). Project-source PDF, QVEC.
7. Tsvetkov, Faruqui, and Dyer. **Correlation-based Intrinsic Evaluation of Word Vector Representations** (2016). Project-source PDF, QVEC-CCA.
8. Puri et al. **FADE: Why Bad Descriptions Happen to Good Features** (2025). Project-source PDF.
9. Bender and Koller. **Climbing towards NLU: On Meaning, Form, and Understanding in the Age of Data** (2020). [Paper](https://aclanthology.org/2020.acl-main.463/).
10. Bommasani, Davis, and Cardie. **Interpreting Pretrained Contextualized Representations via Reductions to Static Embeddings** (2020). [Paper](https://aclanthology.org/2020.acl-main.431/).
11. Gupta and Jaggi. **Obtaining Better Static Word Embeddings Using Contextual Embedding Models** (2021). [Paper](https://aclanthology.org/2021.acl-long.408/).
12. Zhang et al. **Be Your Own Teacher: Improve the Performance of Convolutional Neural Networks via Self Distillation** (2019). [Paper](https://openaccess.thecvf.com/content_ICCV_2019/html/Zhang_Be_Your_Own_Teacher_Improve_the_Performance_of_Convolutional_Neural_ICCV_2019_paper.html).
13. Elhoushi et al. **LayerSkip: Enabling Early Exit Inference and Self-Speculative Decoding** (2024). [Paper](https://aclanthology.org/2024.acl-long.681/).
