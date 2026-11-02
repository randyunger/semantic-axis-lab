# Solving English
## Toward complete lexical representations of bounded linguistic evidence

**Research proposal · 2 November 2026 · Initial proof-oriented formulation**

### 1. Aim and central position

Can we finish representing the lexical semantic information available in a fixed body of language?

This project proposes **semantic completeness as an explicit target for lexical representation research**. For a bounded evidence collection \(C\), let \(E(C)\) denote an ideal representation preserving all of its recoverable lexical semantic content. Existing embeddings \(E'(C)\) are candidates to be evaluated against that target, rather than treated as complete because they perform well on selected tasks.

The intended endpoint is exact: **zero loss of the lexical semantic information available under the declared evidence and interpretation conditions**. Approximation describes candidate solutions and their progress toward the endpoint; it does not redefine the endpoint as “good enough.” Completeness need not imply a unique coordinate system, human-readable dimensions, or certainty about facts that the evidence leaves ambiguous.

The proposed paper would contribute a formal framework, elementary supporting and limiting results, a structured interpretation of prior work, and a reproducible demonstration. It would introduce a research agenda rather than announce that English has already been solved. Its potential novelty lies in the specific formulation and consequences of the target, not in the observations that language has statistical structure or that finite data admit finite encoding.

### 2. Two versions of the conjecture

**Historical version.** At a fixed cutoff, every prior spoken or written occurrence belongs to a finite usage history \(H\), whether recorded or not. The conjecture is that accumulated lexical meaning is wholly determined by this history, with relevant circumstances included, and admits a finite complete representation. This is a claim about language itself. The claim that usages exhaust accumulated meaning is a substantive premise; the finite number of occurrences alone does not establish it or establish a finite encoding of all their relevant circumstances.

**Recorded-evidence version.** Fix an actual collection \(C\) of records, including any declared metadata or grounding evidence. Investigate all lexical semantic content recoverable from that collection under explicit interpretation assumptions. This version does not require the surviving records to recover everything in \(H\). Missing historical meaning is outside this target; meaning recoverable from \(C\) but absent from a candidate embedding is a representation failure.

The paper should develop the recorded-evidence version first and retain the historical version as the broader conjecture. Dates alone do not identify \(C\): models can have different corpora from the same period. Discovering a document changes the evidence collection and creates a new target version; it does not invalidate completeness relative to the old version.

“Lexical” includes senses, properties, relations, connotations, and usage restrictions attached to the chosen lexical units. It does not mean every future sentence, every contextual inference, or all human knowledge. Determining that boundary is part of the research, especially for idioms, polysemy, and encyclopedic associations.

### 3. Proposed formal vocabulary

| Symbol | Proposed meaning |
|---|---|
| \(H\) | Complete usage history up to a declared cutoff; generally unavailable. |
| \(C\in\mathcal C\) | A finite evidence collection in a declared class of admissible collections. |
| \(V\) | Fixed lexical inventory: initially words, with an explicit policy for senses and multiword expressions. |
| \(B\) | Background interpretation assumptions: language conventions, grounding assumptions, and inference rules; fixed independently of a particular target corpus. |
| \(Q\) | Family of lexical semantic queries or distinctions that defines the target scope. |
| \(S_B(C,q)\) | The evidence-relative answer to query \(q\), potentially including alternatives, uncertainty, or community variation. |
| \(T,U_T\) | Tokenizer and its decoder; losslessness means \(U_T(T(C))=C\). |
| \(E\), \(Z_C=E(C)\) | Ideal semantic extraction map and its output. Existence as a mathematical map does not establish an executable extraction algorithm. |
| \(E'_{T,A,b}(C)\) | Candidate representation produced using tokenizer \(T\), learning procedure/architecture \(A\), and resource budget \(b\). The prime denotes a candidate, not a derivative. |
| \(\mathcal R,D\) | Permitted readout class and a particular shared readout \(D\in\mathcal R\). |
| \(\mathcal K\) | Representation and access constraints: shape, numerical encoding, storage, and readout cost. |
| \(\ell,\Delta\) | Answer discrepancy and aggregate semantic error. |

The shorthand \(E(C)\) suppresses dependence on \(V,B,Q,\mathcal R,\mathcal K\). Those choices must be published. A corpus by itself does not specify a unique theory of meaning. External dictionaries, human annotations, and pretrained evaluators can introduce additional information; their roles as evidence, interpretation assumptions, or evaluation resources must be distinguished.

#### Exact completeness

A candidate extractor and readout are complete on the declared corpus class when

\[
\forall C\in\mathcal C,\ \forall q\in Q:\qquad
D(E(C),q)=S_B(C,q).
\]

The readout is shared across the corpus class and receives no separate access to \(C\). Requiring the statement across a class prevents a decoder from simply hard-coding the answers for one chosen corpus. Its description length, learned parameters, and computation must still be accounted for: otherwise the entire semantic resource could be hidden in the decoder.

The real research target is a representation satisfying this equality **under meaningful constraints \(\mathcal K\)**. Storing the corpus verbatim is an existence witness but not the intended lexical foundation. Likewise, arbitrary word IDs plus an unrestricted semantic lookup hidden downstream are not an informative solution. The constraints should exclude these escapes without presupposing a small dimension, linearity, or interpretability.

#### Semantic error and equivalence

For a particular candidate \(Z'\) and declared readout \(D\), define

\[
\Delta_C(Z',D)=\sup_{q\in Q}
\ell\bigl(D(Z',q),S_B(C,q)\bigr),
\]

where \(\ell\geq0\), with zero only for equal semantic answers. Thus \(\Delta_C=0\) means no query in scope is answered incorrectly. Exact uncertainty sets can be equal even where no unique real-world answer is justified. Selecting a suitable discrepancy for structured answers remains open.

Finite benchmarks estimate restricted performance; they do not automatically evaluate this supremum. Average scores can hide missing rare distinctions. Also, \(\inf_D\Delta_C=0\) does not prove that any permitted decoder attains zero: exact existence and arbitrarily close approximation must remain distinct.

Two representation/readout pairs are semantically equivalent if they give the same answers throughout \(Q\). Equality of coordinates is unnecessary. Semantic equivalence alone implies neither an orthogonal transformation nor a linear one. Extra structure and minimality conditions are needed for stronger isomorphism claims.

### 4. Mathematical results already available

The following are elementary results with proof sketches, not claimed mathematical novelties. They establish a starting point and prevent stronger conclusions from being attributed to finiteness alone.

**Lemma 1 — Finite evidence admits a finite lossless representation.** If \(C\) contains \(N\) bits, storing those bits preserves all its recorded information. If \(S_B(C,q)\) is computed by a fixed finite program, the corpus and that program provide a finite generative description of every such answer, even if the query family is infinite.

*Proof.* Use the identity encoding and execute the program on the stored corpus and query. This does not prove compact lexical organization, efficient answers, decidability of arbitrary semantic questions, or a suitable embedding matrix. The historical version additionally requires a finite encoding of semantically relevant circumstances.

**Lemma 2 — Lossless tokenization leaves the ideal evidence target unchanged.** If \(U_T\circ T\) is the identity, any extraction map \(F\) on the original corpus can be expressed on tokenized evidence as \(F\circ U_T\).

*Proof.* \((F\circ U_T)(T(C))=F(C)\). This holds for every lossless tokenizer. Preserve document boundaries, metadata, and any other evidence included in \(C\); lossy normalization is outside the premise. The result establishes information equivalence, not equal learning efficiency or equal error at fixed model size. No word-preferential tokenizer is required by the existence argument.

**Lemma 3 — Finite semantic targets admit exact matrix representations.** Let a finite family of numeric lexical queries define a finite-valued matrix \(M\in\mathbb R^{|V|\times m}\), with \(M_{ij}\) the answer for word \(i\) and query \(j\). If \(\operatorname{rank}(M)=r\), an exact real-arithmetic linear factorization \(M=ZW\) exists with \(r\) embedding coordinates; no exact linear factorization uses fewer.

*Proof.* A rank factorization supplies \(Z,W\); conversely \(\operatorname{rank}(ZW)\leq d\) for an embedding width \(d\). If entries are rational, rational rank factors exist and have finite exact encodings, though bit lengths may be large. Fixed-precision floating-point exactness does not follow.

**Corollary — Minimal linear solutions have a conditional equivalence.** For two rank-\(r\) factorizations of the same \(M\), there is an invertible \(r\times r\) matrix \(R\) with \(Z_2=Z_1R\) and \(W_2=R^{-1}W_1\), because both embedding matrices span the column space of \(M\). Orthogonality requires further conditions.

This is an explicit example of an exact target, minimum width, and equivalence between solutions. It does **not** establish that a finite query matrix covers English, that its rank is an intrinsic dimensionality of English, or that matrix factorization is the correct general semantic model. Non-unary relations may require richer structures.

**Lemma 4 — Reversible reparameterization preserves recoverability when the readout can compensate.** For invertible \(g\), use \(D_g(z,q)=D(g^{-1}(z),q)\).

*Proof.* \(D_g(g(Z),q)=D(Z,q)\). This applies only when the compensating readout is allowed. A rotation can change accessibility under sparse or coordinate-limited readouts without changing unrestricted recoverability. Interpretability is therefore a separate objective, not a prerequisite for \(E(C)\).

**Lemma 5 — Observationally indistinguishable alternatives cannot be uniquely recovered.** If two admissible semantic interpretations yield identical available evidence but disagree on a target answer, no deterministic procedure using only that evidence can always select the correct interpretation; randomization cannot guarantee correctness for both either.

*Proof.* The procedure receives the same input in both cases. The corpus-relative target must retain the unresolved alternatives, justify an additional assumption, or incorporate additional evidence. This is a limit on unique inference, not a requirement to accept semantic loss.

**Lemma 6 — Partial tests alone cannot certify unrestricted completeness.** If the admissible candidate class contains two representations agreeing on every tested query but differing on an untested one, those tests cannot distinguish a complete candidate from the other.

*Proof.* The observed test outputs are identical. Certification requires exhaustive coverage, a proven determining set, or additional structural assumptions. A finite determining set for a wider query family would be an especially valuable research result.

**What follows now:** finite source encoding, tokenizer invariance, and exact solutions in a restricted matrix setting are established under their premises. Exact lexical extraction, useful bounds on its size, efficient discovery, and universal transfer are not established.

### 5. Main conjectures and proof agenda

The central question should remain ambitious while its components are investigated separately.

| Claim | Status and proposed investigation |
|---|---|
| **Semantic specification:** a defensible \(B,Q,S_B\) captures all lexical content in scope. | Open linguistic and formal problem. Avoid equating a convenient benchmark with the whole target. |
| **Constrained existence:** \(E(C)\) exists with finite storage and a useful shared readout under \(\mathcal K\). | Central conjecture beyond raw corpus storage. Explore structured sense representations as well as ordinary matrices. |
| **Exact extraction:** an executable procedure constructs such a representation. | Separate conjecture; mathematical existence need not imply computability or tractability. |
| **Approximation:** resource-indexed candidates can make semantic error arbitrarily small. | Specify a sequence and error notion. Convergence need not imply finite-time attainment of exact completeness. |
| **Structural equivalence:** complete, appropriately minimal solutions preserve common semantic structure. | Define the preserved relations before proposing linear or orthogonal equivalence. Some equivalence follows by construction and is not a discovery. |
| **Reusable foundation:** complete representations can support varied downstream models efficiently while frozen. | Architectural and empirical hypothesis; information sufficiency alone does not imply convenient computation. |

Three formalization directions deserve priority. First, investigate **semantic sufficiency**: a representation should preserve precisely the information needed for the declared semantic observations, with no corpus-specific semantic database hidden in the readout. This connects to sufficient statistics and information bottleneck theory [1], but a single fixed corpus cannot be treated as a nontrivial random variable without a declared statistical model.

Second, investigate **semantic equivalence classes**: define \(C_1\sim C_2\) when their semantic answers agree for every query. This supplies an abstract target structure. It does not by itself give a finite, computable canonical encoding or an efficient way to decide equivalence.

Third, investigate **determining sets and complexity**: can a bounded set of lexical distinctions determine all answers through fixed rules? What are the joint storage and computation requirements of the representation and readout? Width alone is inadequate because numerical precision and decoder capacity can conceal arbitrarily large resources.

### 6. Evidence and organization of prior research

The framework should organize contributions by what they establish, without retroactively attributing the \(E(C)\) goal to their authors.

| Research direction | Relevant evidence or precedent | Remaining gap |
|---|---|---|
| Distributional learning and factorization | Levy and Goldberg relate skip-gram with negative sampling to a shifted PMI word-context matrix [2]. | Recovering specified corpus statistics is not equivalent to recovering all lexical semantics. |
| Semantic sufficiency and compression | Information bottleneck theory formalizes preservation of information relevant to another variable [1]. | Which semantic targets are sufficient for lexical completeness, and how should they be specified? |
| Shared representation structure | ICA work reports corresponding semantic axes across embeddings [3]; the Platonic Representation Hypothesis proposes convergence toward shared representations [4]. | Agreement can coexist with shared omissions; neither establishes complete lexical content. |
| Tests of convergence | Gröger et al. identify scale-related confounds in similarity measures and propose null calibration [5]. | Apparent geometric convergence needs calibrated controls and semantic validation. |
| Lexical evaluation | QVEC and QVEC-CCA compare embeddings with linguistic feature resources [6,7]. | Resource coverage is partial; scores do not certify completeness. |
| Interpretability | Rotation, labeling, and feature-description evaluation, including FADE [8], address how representations are explained. | Description fidelity and semantic completeness are separate properties. |
| Grounding and meaning | Bender and Koller argue that linguistic form alone cannot establish meaning [9]. | The proposal must defend its evidence-relative semantic target and specify grounding assumptions, not treat text as self-interpreting. |

The existing project’s analogy and neighborhood explorations motivate investigating embedding content but are exploratory observations, not evidence of completeness or convergence to zero error. Likewise, information stored elsewhere in a language model cannot automatically be credited to its input embedding table.

The literature review must also examine prior semantic-primitives and universal semantic-dimension proposals, minimal sufficient representations, and frozen embedding transfer. No claim of first proposing finite meaning or shared representations is justified yet. The intended contribution is the precise target, distinctions, proof obligations, and experimentally useful consequences.

### 7. Paired implementation: a formal example and a transfer test

**Exact miniature example.** Provide a small executable reference implementation of Lemma 3. Generate a finite lexical query matrix with known rank, recover an exact factorization using rational arithmetic, and verify every declared answer. Construct an incomplete candidate that passes a selected benchmark but fails an omitted distinction; show an invertible coordinate change preserving every answer. If synthetic sentences generate the matrix, explicitly distinguish facts identifiable from those sentences from facts known only to the generator.

This illustrates exact completeness, conditional equivalence, and the limitations of partial evaluation. It proves nothing about full English and should not be presented as a novel factorization algorithm.

**Practical embedding-transfer experiment.** Test whether one model’s frozen embeddings can serve another through a small shared adapter. Begin with a compatible tokenizer or an explicitly declared shared lexical subset, avoiding a tokenizer study. Keep the recipient body and output head frozen during the primary adapter-only experiment; preserve the original output head separately if it was tied to the replaced input embeddings.

Compare the intact recipient, transferred frozen donor embeddings, frozen random embeddings, and donor embeddings with lexical row assignments shuffled. Match adapter capacity and training budget across replacement conditions; normalize or report scale differences. Train only on training data and evaluate held-out text, with coverage and frequency breakdowns. A held-out-word adapter test where feasible helps separate learned alignment from memorized lexical remapping. Later body unfreezing is a separate experiment with separate claims.

Report held-out loss, adaptation sample efficiency, trainable parameters, and compute. Random and shuffled controls test whether learned semantic organization helps beyond arbitrary identifiers or generic vector geometry. Multiple seeds and a fixed stopping rule are needed. Failure can reflect interface mismatch, so it does not refute \(E(C)\); successful transfer supports reuse, not completeness. Donor training evidence must be disclosed where known: transfer is not proof of equal-corpus information recovery.

These components form a credible initial package: a position paper with a precise formal core, executable proof examples, and a bounded practical test. A successful transfer result is desirable but not a prerequisite for honest reporting.

### 8. Strengths, weaknesses, and decisive open questions

**Strengths.** The proposal separates information available in evidence from information captured by a model. It gives exact completeness a clear conceptual role without requiring interpretability. It connects representation learning, evaluation, equivalence, and reuse through explicit proof obligations. Useful partial results include determining-set theorems, impossibility results, evidence of missing distinctions, and well-controlled transfer measurements.

**Weaknesses.** The semantic specification is not yet operational. An unrestricted encoding makes existence trivial; excessive restrictions can manufacture impossibility or a preferred dimensionality. Finite history does not alone establish grounding, learnability, or efficient computation. A representation may preserve uncertainty that cannot be collapsed into a single “correct meaning.” Ordinary static matrices may be inconvenient for senses and relations. Exactness can require more numerical precision than standard hardware affords. Novelty remains unestablished, and practical benefits may be small if lexical relearning is not a dominant training cost.

**Questions that determine viability:** Can a semantic observation family be justified independently of the models being evaluated? Can we identify a determining set broader than a hand-selected test suite? What restrictions keep meaning in the representation while allowing useful downstream reasoning? Which equivalences are substantive rather than definitional? What lower bounds rule out insufficient capacity? Can completeness ever be certified for the chosen scope, or can experiments only establish failures and increasing coverage?

Once constraints are fixed, a genuine counterexample could show that no permitted representation can preserve a required distinction, or that no permitted learner can identify the target from the evidence. One failed optimizer, a transfer failure, or lack of benchmark improvement would not establish those conclusions.

### 9. Implications if the target can be constructed

For past research, \(E(C)\) provides a common way to distinguish acquiring content, measuring coverage, studying equivalent structures, exposing interpretation, and demonstrating reuse. For future work, it encourages explicit evidence boundaries, challenges targeting omitted distinctions, independently calibrated evaluations, and joint accounting of representation size and readout complexity. Contributions could accumulate against a versioned semantic resource rather than only against end-to-end model scores.

For industry, a complete **and efficiently usable** representation could become a shared frozen lexical foundation. Potential benefits include less repeated acquisition of lexical knowledge, controlled comparisons of downstream architectures, clearer diagnosis of missing knowledge versus failed computation, and explicit compressed variants with characterized losses. These are conditional consequences, not established savings. Contextual interpretation, composition, reasoning, new knowledge, and model-specific adaptation remain substantial problems. Corpus bias is also preserved unless explicitly addressed; completeness is not correctness or fairness.

Finding \(E(C)\) would therefore settle a specified representation problem, not all embedding engineering or language modeling. The scale of its impact depends on construction cost, evidence rights and provenance, update mechanisms, interface efficiency, and cross-model transfer.

### 10. Initial deliverable and decision criterion

Produce a concise research paper and public code package containing: a defensible corpus-relative semantic target; the elementary lemmas and their limits; one substantive formal contribution beyond those elementary facts, if obtainable; the exact miniature example; and the controlled embedding-transfer experiment. Present the historical conjecture and industry consequences as motivation, with their additional assumptions explicit.

The first milestone is to settle a concrete candidate for \(B,Q,\mathcal R,\mathcal K\) and work through a complete example. Before claiming a new theorem or a new agenda, compare that formulation with the closest prior work. The project succeeds initially if it gives researchers a useful definition, result, or reproducible test they can build on—even while the existence and construction of a complete English lexical foundation remain open.

### Selected references

These references support specific connections and objections, not an exhaustive novelty assessment. The proposal was developed from the present discussion and relevant original project discussions; earlier “Solving English” briefs were not used as its drafting source.

1. Tishby, Pereira, and Bialek. **The Information Bottleneck Method** (1999; arXiv 2000). [Paper](https://arxiv.org/abs/physics/0004057).
2. Levy and Goldberg. **Neural Word Embedding as Implicit Matrix Factorization** (2014). [Paper](https://papers.neurips.cc/paper_files/paper/2014/hash/b78666971ceae55a8e87efb7cbfd9ad4-Abstract.html).
3. Yamagiwa, Oyama, and Shimodaira. **Discovering Universal Geometry in Embeddings with ICA** (2023). [Paper](https://aclanthology.org/2023.emnlp-main.283/).
4. Huh, Cheung, Wang, and Isola. **Position: The Platonic Representation Hypothesis** (2024). [Paper](https://proceedings.mlr.press/v235/huh24a.html).
5. Gröger, Wen, and Brbic. **Revisiting the Platonic Representation Hypothesis: An Aristotelian View** (2026). [Paper](https://proceedings.mlr.press/v306/groger26a.html).
6. Tsvetkov et al. **Evaluation of Word Vector Representations by Subspace Alignment** (2015). Project-source PDF, QVEC.
7. Tsvetkov, Faruqui, and Dyer. **Correlation-based Intrinsic Evaluation of Word Vector Representations** (2016). Project-source PDF, QVEC-CCA.
8. Puri et al. **FADE: Why Bad Descriptions Happen to Good Features** (2025). Project-source PDF.
9. Bender and Koller. **Climbing towards NLU: On Meaning, Form, and Understanding in the Age of Data** (2020). [Paper](https://aclanthology.org/2020.acl-main.463/).
