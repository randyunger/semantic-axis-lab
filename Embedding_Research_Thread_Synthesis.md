# From embedding-table knowledge to the semantic structure of English

Research-thread synthesis · October 31, 2026

This document preserves the ideas, motivations, proposed experiments, literature leads, and unresolved questions developed in this conversation. It is a standalone planning note, not a revision of research proposal v3.2. Suggested experiments have not been performed merely because they appear here. The larger conjecture is not an established result.

## 1. The starting observation

Our first exploration of extracted LLM embeddings found that some analogies could be completed using the embedding table and vector arithmetic alone, without running the transformer blocks. We have been exploring tables from Pythia, Qwen, and SmolLM; this note does not imply that every listed experiment has been run on every model.

This is a meaningful first observation for our investigation: useful learned relationships are accessible directly in the table. It is not a novel discovery for the field, nor a measurement of all the knowledge stored there. It motivates a broader question: what kinds of knowledge are recoverable from this component, and how simply can we recover them?

The public analogy explorer should be retained. It offers an intuitive entry point into the research before introducing transformations, labels, or statistical evaluation.

## 2. Measuring knowledge in the table beyond analogies

The conversation identified a family of complementary tests. Together they could form a reproducible evaluation suite for extracted LLM input tables.

| Test family | Example | Table-only procedure | What to watch for |
|---|---|---|---|
| Similarity and relatedness | Cat–dog versus cup–coffee | Compare cosine similarities against independent judgments | Similarity and association are different targets. |
| Category membership and intrusion | Dog, rabbit, horse, hammer | Find the item least similar to the rest | Easy random intruders can exaggerate performance. |
| Category organization | Animals, tools, foods, vehicles | Cluster vectors, then evaluate against withheld category labels | Clustering can reflect spelling, frequency, or other nuisance properties. |
| Graded properties | Order mouse, rabbit, dog, horse, elephant by typical size | Project onto a direction such as large minus small | Check independent ground truth and sensitivity to anchor choices. |
| Semantic attributes | Aquatic, manufactured, sweet, capable of flight | Fit a small probe and evaluate on unseen words | A learned probe contributes a decoding rule. |
| Factual associations | Paris associated with France | Rank plausible candidate answers | Association alone does not establish the specific relation “capital of.” |
| Relation discrimination | Capital–country versus other city–country pairs | Train a constrained relation decoder on disjoint examples | Hold out entities and control memorization. |
| Linguistic properties | Part of speech, number, sentiment | Directions, clusters, or simple probes | Grammatical information should be distinguished from semantic properties. |
| Cross-language correspondence | Cat and its translations | Cross-language nearest-neighbor retrieval | Token availability and token-form differences affect coverage. |

A manageable demonstration proposed in the thread was animal-size ordering: normalize the direction large − small, project normalized animal vectors onto it, and compare the order with independent judgments. Fix the word list before inspecting results; repeat with alternative anchors such as big − little. This links recoverable world knowledge directly to semantic directions.

### What a score means

The suite measures **knowledge accessible under a specified readout**, not an absolute quantity of all knowledge in the table.

- Fixed arithmetic, similarity, and predetermined projections provide direct tests of existing geometry.
- Linear probes test whether distinctions generalize through a learned linear decoding rule.
- Powerful decoders can learn substantial new structure themselves, weakening attribution to the table.

Declare the permitted readout, training data, and evaluation splits. Include appropriate random-vector, shuffled-label, and nuisance-feature controls. Keep spelling/spacing/capitalization variants and related lexical families from creating trivial train–test leakage.

Report tokenizer coverage separately from conditional accuracy. A shared whole-word subset supports fairer geometric comparisons, but excludes potentially important parts of the vocabulary. Whole-word filtering remains a simplification, not proof that subword semantics are unimportant.

## 3. What interpretability tests should evaluate

The key distinction is between **recoverable knowledge** and **how transparently that knowledge is organized**.

An orthogonal rotation preserves pairwise dot products, norms, cosine similarities, distances, and ordinary analogy geometry, assuming consistent preprocessing. Geometry-based knowledge tests are therefore preservation checks for rotation, not measures of improved coordinate interpretability. For oblique transformations, these invariances no longer automatically hold.

| Interpretability test | Operational question | Application to rotation |
|---|---|---|
| Axis coherence / word intrusion | Can an independent evaluator identify a challenging intruder among high-scoring words? | Test each tail separately; avoid judging with the same geometry used to optimize. |
| Held-out label fidelity | Does an axis label predict how unseen words rank or score? | Freeze labels before final evaluation; include plausible near-misses. |
| Responsiveness | Do words genuinely expressing the labeled property receive expected scores? | Detect labels that explain only a few selected examples. |
| Purity | Are strongly scoring words actually explained by the label? | Detect unrelated meanings bundled on the same axis. |
| Coordinate-budget curves | How accurately can a property be read from 1, 2, 4, 8… coordinates versus the full space? | Test whether rotation concentrates accessible information. Select coordinates on training data only. |
| Coverage and redundancy | How many distinct properties are explained, and which domains are neglected? | Orthogonality does not itself prevent semantic duplication. |
| Weakest-axis evaluation | How well explained are the worst coordinates, not merely the average? | Retain minimum and bottom-fraction reporting central to our project. |
| Stability | Do meanings or subspaces recur across word samples, seeds, and initializations? | Compare matched axes or subspaces, accounting for sign and permutation. |

An axis that produces an appealing top-word list is not automatically understood. Its label should predict behavior on independently evaluated words. The negative end need not mean the opposite of the positive end.

FADE offers useful distinctions among explanation-quality criteria, but its original intervention-based faithfulness evaluation is not directly reproduced by a table-only test. DCI-style measures provide another conceptual framework for informativeness, concentration, and separation, but our semantic annotations do not constitute a complete inventory of ground-truth factors.

## 4. Specific implications for the rotational research project

### What is already present

The v3.2 proposal already includes coherence, label fidelity, responsiveness/purity, sparse-readout comparisons, weak-axis evaluation, independent evidence, redundancy analysis, and cross-model directions. The thread's contribution is partly to make these a more explicit evaluation program and connect them to a larger scientific motivation—not to imply they were all missing.

### Suggested additions or clarifications

1. **Make the public notebook tell a coherent story:** demonstrate accessible knowledge with the analogy explorer; add one independent property task; show what changes and what stays invariant after rotation.
2. **Separate preservation from improvement:** report geometry-based knowledge scores alongside coordinate interpretability scores. A successful orthogonal rotation should preserve the former while improving the latter.
3. **Prioritize a coordinate-budget curve:** for a labeled property, compare original, random, statistical, and semantically optimized bases using identical held-out words and readout budgets.
4. **Identify evaluation families explicitly:** conventional intrinsic embedding evaluation, semantic probing, dimension-selection probing, explanation evaluation, and disentanglement metrics.
5. **Add dimensionality-selection and isomorphism literature to the broader reading map.** These inform the longer-term question even when they do not change Milestone 1.
6. **Use cross-model agreement as a later scientific test:** ask whether independently learned spaces expose comparable semantic distinctions. Agreement with a source used for optimization is not independent confirmation.
7. **Retain uncertainty and negative results:** failure to label an axis might reflect limited labels, data, optimization, or non-linear organization; it does not by itself establish absent meaning or superposition.

### How rotation might become useful beyond analysis

One possible pathway is: extract lexical knowledge, organize it into interpretable coordinates, compare independently trained models, and investigate a shared reusable semantic representation.

For an existing model, an exact and consistently compensated change of basis preserves computation; it does not automatically improve predictions. Replacing only its embedding table is not generally function-preserving. For future models, organized coordinates might support sparse connections, explicit feature selection, frozen semantic inputs, and easier auditing. Those benefits require experiments.

The broader conjecture gives rotation an application pathway even without immediate accuracy gains. It does not prove those gains, and rotation cannot create knowledge absent from the extracted representation.

## 5. Potential new project: “Solving English”

### Working title

**The Finite Lexical Semantics Conjecture: Discovering the Structure and Dimensionality of English Meaning**

### Summary description

This project asks whether the accumulated lexical meanings of English admit a complete, finite, discoverable semantic representation. It would investigate the shared dimensions that distinguish and connect word meanings, whether independently obtained complete representations preserve the same underlying semantic structure, and whether such a representation could become a reusable foundation for language models. Neural networks would serve as instruments for discovering linguistic structure. The object of study would be English's lexical semantics itself, with applications to AI and possible connections to human semantic organization.

The motivating conjecture is that, within a specified vocabulary and historical scope, individual words carry a bounded inventory of accumulated semantic distinctions. Across the vocabulary, those distinctions overlap and may admit a finite system of independent semantic dimensions. A community could seek a complete representation, characterize its equivalence to other complete representations, and test whether it can be frozen while subsequent learning occurs downstream.

This is a proposed research program. Completeness, a fixed intrinsic dimensionality, isomorphism, and universal architectural usefulness remain unproven.

### The intended scope—and the misunderstanding to avoid

The question concerns the accumulated semantic content of lexical items, not the unbounded meanings generated by combining words into new sentences.

For example, “door” carries evidence about barriers, passage, access, privacy, opening and closing, and figurative opportunity. The aim is to recover and organize that lexical content, together with its distinctions and overlaps with gate, lid, window, and other words.

An example contrasting “the dog chased the cat” with “the cat chased the dog” does not address this conjecture: that contrast concerns composition and order, which the proposal already places downstream. Contexts can provide evidence for learning a word's senses without making sentence-level composition the target representation.

The hypothesis is not merely “make a particular LLM more interpretable.” It asks whether there is a discoverable structure of English meaning that models approximate. This larger scientific goal may motivate, redirect, or replace the current rotation project. It should not automatically be reduced to an extension of Milestone 1.

### Three linked hypotheses

| Hypothesis | Claim to investigate | What would be needed |
|---|---|---|
| Finite completeness | A finite semantic representation captures every lexical distinction within the declared scope. | An independent account of distinctions and a serious process for challenging completeness. |
| Equivalence of complete solutions | Complete representations preserve a common structure, up to an appropriate isomorphism. | Define the preserved properties and relations, then establish the relevant mapping. |
| Frozen-foundation sufficiency | A shared lexical representation can remain fixed while downstream systems acquire further capabilities. | Reuse experiments across independently designed and trained architectures. |

“All future knowledge is downstream” is best interpreted architecturally: subsequent learning could occur without altering the lexical foundation. It does not mean that a present-day table contains future facts.

### Dimensionality and semantic alignment

The desired quantity is the dimensionality of the independent semantic structure, not the largest number of columns we can allocate. Redundant coordinates and unused dimensions can be added indefinitely. Multiple bases could describe the same structure; if it is a vector space, those bases have equal dimension.

A central proposed experiment is to increase representational capacity while encouraging distinct interpretable features, then measure additional independently validated semantic distinctions. Investigate whether improvements level off and whether the same semantic organization reappears across sufficiently rich data sources and learning methods.

Adding columns through a linear expansion of an existing table cannot add independent information. A capacity study would need newly learned representations at different widths or an explicitly different representation scheme. Comparing unrelated pretrained models alone confounds dimensionality with their data, tokenizers, objectives, and architectures.

The user's motivation is to favor explicit semantic dimensions over opaque packing or superposition. That preference must become a stated constraint or objective: a knowledge score alone does not require the learner to expose its information intelligibly.

Lower-dimensional projections for efficiency are a secondary engineering consequence. They should not displace the main question of whether a complete reference structure can be discovered.

### What “isomorphic” must mean

A bijection between word identities is insufficient. The mapping must preserve the semantic properties, relations, sense distinctions, or other structure that defines the target. Linear equivalence, orthogonal equivalence, and more general structure-preserving equivalence are different hypotheses.

Even if the scope is finite, finiteness does not by itself identify a uniquely determined semantic geometry. We must define what counts as an independent distinction. For example, should “permits passage when opened” be an independent feature or a relationship among barrier, access, and openable? Addressing such questions is part of the scientific work.

“Complete finite representation” is the intended term. “Closed-form solution” would incorrectly suggest an explicit formula rather than a potentially extensive discovery process.

### Why the result would matter

- **Linguistics:** a systematic account of shared lexical structure, independent distinctions, and their organization.
- **Cognitive science:** hypotheses that can be compared with independent human judgments and behavior. Model convergence alone would not establish psychological truth.
- **AI infrastructure:** a shared semantic foundation whose omissions and distortions can be inspected and improved collectively.
- **Cumulative research:** teams could demonstrate missing distinctions or improve organization against a common reference.
- **Architecture research:** if frozen reuse succeeds, researchers could focus on downstream computation or choose explicit approximations of the common foundation.

## 6. What would support—or limit—the larger conjecture?

The most compelling evidence would combine semantic coverage, interpretable organization, cross-method convergence, and successful reuse. None alone establishes the whole claim.

A plateau in a benchmark could reflect the benchmark, corpus, annotation coverage, optimizer, or representation constraints rather than an intrinsic limit of English. The question is how to distinguish those explanations, not to treat their existence as a reason to abandon the ambition.

Useful research directions include independent challenges to a candidate representation, residual analysis for unexplained distinctions, replication across corpora and training objectives, alignment of independently learned structures, and frozen-foundation transfer experiments. These are future investigations, not a settled implementation plan.

Before expensive experiments, clarify:

1. What semantic structure is being preserved, and what constitutes completeness?
2. What could demonstrate discovery of that structure rather than one useful construction?
3. What could distinguish intrinsic semantic limits from limits of our instruments?
4. How should senses, lexical units, idioms, rare usages, and historical scope be defined?
5. What would falsify the strong conjecture while leaving a useful partial semantic reference?

## 7. Literature map and novelty assessment

These links were identified in the conversation. They form a targeted reading map, not an exhaustive novelty review. Some papers were checked through abstracts or selected passages rather than fully reviewed.

| Work | Relevance and limits |
|---|---|
| [SimLex-999 (2015)](https://aclanthology.org/J15-4004/) | Existing semantic-similarity evaluation; distinguishes similarity from association. |
| [Intrinsic Evaluation of Word Vectors Fails to Predict Extrinsic Performance (2016)](https://aclanthology.org/W16-2501/) | Cautions against assuming better intrinsic scores imply better downstream models. |
| [Rotated Word Vector Representations and their Interpretability (2017)](https://aclanthology.org/D17-1041/) | Direct rotation and interpretability precedent, already in the project. |
| [On the Dimensionality of Word Embedding (2018)](https://papers.nips.cc/paper_files/paper/2018/hash/b534ba68236ba543ae44b22bd110a1d6-Abstract.html) | Dimensionality selection and bias–variance trade-offs; not a final dimensionality of English. |
| [Intrinsic Probing through Dimension Selection (2020)](https://aclanthology.org/2020.emnlp-main.15/) | Directly studies concentrated versus dispersed linguistic information. [Code](https://github.com/rycolab/intrinsic-probing). |
| [DCI: A Framework for the Quantitative Evaluation of Disentangled Representations (2018)](https://www.pure.ed.ac.uk/ws/portalfiles/portal/57345826/iclr_final.pdf) | Separates informativeness, disentanglement, and completeness relative to known factors; our semantic factors are incomplete. |
| [Just Rank / EvalRank (2022)](https://aclanthology.org/2022.acl-long.419/) | Reconsiders intrinsic evaluation and its relationship to downstream usefulness. |
| [MTEB (2023)](https://aclanthology.org/2023.eacl-main.148/) | Broad embedding-system evaluation; not specifically isolation of an LLM input table. |
| [FADE (2025)](https://aclanthology.org/2025.findings-acl.881/) | Explanation-quality evaluation; already in the project. |
| [SAEBench (2025)](https://proceedings.mlr.press/v267/karvonen25a.html) | Precedent for a multidimensional benchmark of an interpretability component; not an input-table benchmark. |
| [Universal Dimensions of Meaning… — Samsonovich and Ascoli (2014)](https://doi.org/10.3390/computation2030061) | Explicitly investigates potentially finite universal semantic dimensions. Its weak semantic maps omit domain-specific meaning, so it does not establish complete lexical semantics. |
| [Are All Good Word Vector Spaces Isomorphic? — Vulić, Ruder, and Søgaard (2020)](https://aclanthology.org/2020.emnlp-main.257/) | Close precedent on near-isomorphism and the effects of training/data; not a proof of equivalence of complete solutions. |
| [Discovering Universal Geometry in Embeddings with ICA (2023)](https://aclanthology.org/2023.emnlp-main.283/) | Recurring interpretable axes across languages, algorithms, and modalities; already in the project. |
| [The Platonic Representation Hypothesis (2024)](https://proceedings.mlr.press/v235/huh24a.html) | Shared underlying representations as a convergence hypothesis; not a complete frozen lexical foundation. |
| [Revisiting the Platonic Representation Hypothesis: An Aristotelian View (2026)](https://proceedings.mlr.press/v306/groger26a.html) | Challenges some convergence measurements after calibration; relevant to evaluator design. |
| [Towards Universal Semantics With Large Language Models (2025)](https://arxiv.org/abs/2505.11764) | Automates explanations using Natural Semantic Metalanguage primitives. Structured verbal primitives are not themselves vector dimensions. |

Other existing project resources remain relevant: QVEC/QVEC-CCA for semantic evaluation and alignment; SemAxis, DensRay, POLAR, Word Equations, and BiImp for semantic directions; ConceptNet-based labeling; Automated Word Intruder Test; Axis Tour; CEDAR; and ROTATE.

**Novelty assessment:** finite semantic foundations, shared geometry, and approximate isomorphism all have substantial precedents. The particular synthesis of complete lexical semantics, well-defined equivalence, and a reusable frozen foundation may offer a useful research agenda, but novelty has not been established. No source reviewed here establishes the complete proposed result.

## 8. A realistic role for the originator

The user does not currently have the resources or expertise to discover a complete representation alone. A legitimate initial contribution is to formulate the conjecture clearly, connect the literature, explain the motivation, and identify experiments that others can undertake.

A suggested route is a three-to-five-page concept or position paper, followed by targeted feedback from authors of the closest work. Public notebooks can supply accessible demonstrations. A public essay can introduce the ambition, while a technical note states its assumptions and evidence requirements.

Relevant communities include the [Re-Align representational-alignment workshop](https://representational-alignment.github.io/2026/) and conference position-paper tracks such as [ICML's](https://icml.cc/Conferences/2026/CallForPositionPapers). The 2026 submission dates discussed in the thread had already passed; these are examples of communities and publication formats, not open submission promises.

Potential influence on frontier models would most plausibly follow expert engagement, experiments, collaborations, and evidence—not an expectation that an unsolicited suggestion immediately redirects a lab.

## 9. Decisions preserved for the next conversation

- Preserve the analogy explorer and broaden the evaluation perspective beyond analogies.
- Keep recoverable knowledge, coordinate interpretability, and downstream usefulness distinct.
- Consider a property task and coordinate-budget curve as concrete additions to rotation work.
- Read the 2014 finite-dimensions and 2020 isomorphism papers closely; add dimension-selection probing to the practical evaluation reading list.
- Treat “solving English” as a potentially independent scientific project, not merely a justification for continuing rotation.
- Allow a conceptual investigation to redirect or pause implementation; no final decision to abandon the rotation project was made.
- Preserve the ambition: discover fundamental lexical semantic structure and enable collective progress toward a complete reusable foundation.
- Preserve the epistemic status: that foundation's existence, fixed dimensionality, equivalence, and sufficiency remain hypotheses.

**Compact handoff:** We began by observing that some analogies are recoverable from extracted embeddings alone. This motivated a broader table-only knowledge benchmark and complementary tests of coordinate interpretability. Those ideas could strengthen the rotation project, especially through held-out label fidelity and coordinate-budget curves. The discussion then developed a larger conjecture: English's historically bounded lexical meanings may admit a complete finite semantic structure, equivalent across full representations and reusable as a frozen foundation. The user is interested in this as a fundamental question about English itself and may pursue its formulation and dissemination independently of rotation implementation. The next conversation should respect that larger goal while keeping hypotheses separate from established findings.
