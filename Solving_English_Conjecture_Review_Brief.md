# Solving English: a conjecture about complete lexical semantic representation

## Purpose of this brief

Evaluate the research idea below independently and critically. It is an ambitious conjecture, not an established result. The originator wants to understand its scientific coherence, novelty, significance, and tractability, and whether a position paper could motivate a collective research effort. They do not currently have the resources or expertise to solve the entire problem alone.

Please engage with the fundamental question about English itself. Do not automatically narrow it to a small embedding-rotation experiment or dismiss it by observing that sentences express meanings that individual words do not. The proposal explicitly distinguishes lexical meaning from contextual composition.

## 1. The central idea

English's vocabulary may possess a finite, discoverable semantic structure. A sufficiently expressive, appropriately organized embedding representation might capture all the accumulated lexical meanings within a specified vocabulary and historical scope.

The stronger conjecture is that complete representations would preserve the same underlying semantic structure: their independent semantic dimensionality would be fixed, even though their bases, coordinates, or implementation details could differ. Complete, nonredundant representations would therefore be isomorphic in an appropriately defined semantic sense.

If such a representation could be discovered and its completeness and equivalence characterized, it could become a shared semantic foundation. Future neural networks could begin with that foundation, freeze its lexical weights, and learn subsequent capabilities downstream. Systems requiring greater efficiency could use explicit lower-resolution approximations or projections.

The motivating headline is **“English is solvable in embedding space.”** A more precise scientific formulation is:

> Within a specified vocabulary and historical scope, English's accumulated lexical semantics admits a finite, semantically complete representation. Independent complete representations preserve a common structure, and this structure may be reusable as a fixed lexical foundation across learning systems.

The existence, dimensionality, equivalence, and downstream sufficiency parts of this statement require separate investigation.

## 2. What “solving English” means here

The target is the accumulated meaning associated with lexical items, not every possible sentence, contextual inference, future fact, or act of reasoning.

Consider “door.” Its uses supply information about barriers, passage, access, opening and closing, privacy, and figurative opportunity. Other words overlap with parts of this content: gate, window, lid, entrance, barrier. The proposal asks whether we can recover the full lexical content and discover the shared semantic distinctions organizing it across the vocabulary.

Historical contexts are evidence from which lexical meanings could be learned. They need not themselves be the objects stored in the final representation. Multiple senses must be preserved rather than averaged away, although the appropriate mechanism—one structured vector, sense-specific vectors, or another arrangement—is unresolved.

The originator's intuition is that a word has been used only finitely many times up to a given point in history. Its accumulated usages consequently supply a bounded body of semantic evidence. Extending this idea across the vocabulary motivates seeking a finite shared semantic structure.

This intuition does not itself prove that meanings have one uniquely correct decomposition, or that finite observations determine a complete account. Those are substantive questions for review.

Examples such as “the dog chased the cat” versus “the cat chased the dog” concern word order and composition. They do not directly refute the lexical conjecture, because those operations are explicitly placed downstream. However, explaining what lexical information those downstream operations require remains relevant.

## 3. Three distinct claims

### A. Finite semantic completeness

There exists a finite representation retaining every lexical semantic distinction in the declared scope, with those distinctions accessible through a specified class of semantic readouts or operations.

The representation must do more than assign unique numbers to words. Otherwise, arbitrary token identifiers plus a sufficiently powerful decoder would satisfy an unhelpfully weak definition.

### B. Common structure and isomorphism

Complete representations encode the same semantic structure, even if their coordinates differ. An appropriate invertible mapping preserves the specified semantic properties and relations.

This is not merely the theorem that vector spaces of equal dimension are linearly isomorphic. Nor is a bijection between vocabulary entries enough. Semantic structure must be defined and preserved.

Orthogonal equivalence, general linear equivalence, and nonlinear structural equivalence are different hypotheses. If completeness is defined as a faithful encoding of one already specified abstract structure, isomorphism may follow by construction; the scientific contribution would then be discovering and validating that structure, not proving a tautology.

### C. A reusable frozen lexical foundation

The discovered representation can be reused without lexical retraining across downstream models. Further learning can occur downstream without changing that foundation.

This does not assert that present embeddings contain future facts. It asserts that their lexical resources could remain sufficient for learning and expressing additional knowledge within the stated scope.

Complete lexical information does not automatically imply an optimal computational interface. Reuse, efficiency, and training benefits require their own evidence.

## 4. Dimensionality and interpretability

The relevant quantity is the number of independent semantic degrees of freedom, not the maximum number of columns allocated to a table. Redundant or empty columns can be added indefinitely.

An operational investigation could increase representation width while encouraging meaningful, distinct features, and measure which additional lexical distinctions become recoverable. The question is whether there is a stable point beyond which added capacity yields no additional semantic content.

The originator particularly values explicit semantic coordinates over opaque overlapping encodings. A representation that attains excellent task scores by packing distinctions into difficult-to-interpret combinations would not fully meet this goal. Interpretability is therefore part of the intended representation standard, not merely decoration added afterward.

Several notions must be separated:

- Matrix rank: independent linear variation among vocabulary vectors.
- Effective dimension: dimensions needed to preserve a chosen amount of measured structure.
- Number of interpretable features: may exceed rank if features have dependencies or nonlinear relationships.
- Semantic independence: the substantive linguistic notion the research must define.

A finite vocabulary of V entries always gives a V-by-d table rank at most V. That algebraic bound does not establish a meaningful dimensionality of English. Precision, permitted readouts, treatment of dependent features, and tolerated approximation also affect capacity claims.

“Complete finite representation” is preferable to “closed-form solution”: the latter normally suggests an explicit mathematical formula, which this proposal does not supply.

## 5. Why the idea could matter

### Scientific significance

The primary ambition is to discover something fundamental about English: the inventory and organization of lexical distinctions, how they overlap, which are independent, and whether different discovery processes recover equivalent structure.

If the recovered organization predicts independent human judgments or behavior, it could also inform cognitive science. Agreement among models alone would not demonstrate how humans represent meaning.

### Shared AI infrastructure

A validated semantic foundation could make lexical knowledge cumulative and inspectable. Researchers could demonstrate missing distinctions, test corrections, and compare models against a common reference. Downstream architecture experiments could share a controlled lexical starting point.

If completeness and reuse were convincingly established, parts of lexical representation research might become relatively settled engineering infrastructure. Other work could focus on extensions, compression, new vocabulary or senses, and downstream computation.

The originator considers efficiency projections a secondary consequence. The central goal is discovering the complete semantic structure, not merely finding a convenient smaller embedding width.

## 6. Strengths of the proposal

1. **It identifies a substantial scientific object.** Lexical semantic organization is worth studying independently of any particular model's benchmark performance.
2. **It separates representation from downstream use.** This could clarify whether a failure reflects missing lexical distinctions or ineffective computation over available distinctions.
3. **It supports cumulative research.** A shared semantic reference and explicit challenges could allow contributions from linguistics, representation learning, lexicography, and cognitive science.
4. **It connects several existing research traditions.** Finite semantic primitives, intrinsic dimensionality, interpretable axes, cross-model alignment, and frozen representations offer tools and precedents.
5. **It generates partial tests without requiring immediate completeness.** Researchers can study coverage, convergence, residual distinctions, dimensionality curves, and frozen transfer.
6. **It can produce value even if the strongest conjecture fails.** A broad, interpretable, reusable partial semantic resource could still be scientifically and practically useful.
7. **Modern models provide a discovery instrument.** Their representations can help aggregate semantic evidence across many usages. This makes investigation plausible; it does not establish that present technology can recover everything.

## 7. Weaknesses and serious challenges

### Completeness is difficult to define and certify

All tests sample distinctions. Passing them does not establish that none remain. A plateau could reflect limited evaluation, annotations, data, optimization, or representational choices. A credible program needs independent challenges and an explicit account of what a completeness claim would mean.

### Finite usage does not guarantee a canonical semantic inventory

Finite observations can support multiple explanations. Speakers may disagree about senses and connotations; meanings can vary across communities and periods. The project must decide whether to represent a shared core, the union of usages, or a structured distribution of variants.

### The boundary between lexical and encyclopedic knowledge is unresolved

For “door,” shape, function, social significance, and cultural convention can blur together. The conjecture needs a principled scope for lexical content without defining away difficult distinctions. This is a genuine scope question, not an objection based on sentence composition.

### Sense structure may not fit an ordinary static vector naturally

A word's senses are alternatives with internal relationships, not necessarily quantities to average. A complete representation might need structure richer than a conventional embedding row. Such a result could preserve the larger goal while changing its proposed implementation.

### A natural vector geometry is an additional hypothesis

Shared lexical structure might be better described by a graph, a family of relations, a structured code, or multiple interacting spaces. Even if all of it can be encoded numerically, that does not establish that one linear basis exposes it faithfully.

### Interpretability and independence may conflict

Human-readable concepts often overlap or entail one another. A minimal independent basis could be less interpretable than an overcomplete vocabulary of features. The proposal must distinguish a complete semantic structure from one preferred coordinate system.

### Isomorphism can be too weak or too strong

Arbitrary invertible mappings can hide rather than explain structure. Orthogonal or linear mappings may exclude equally faithful representations. The relevant invariants and allowed mappings must be specified before equivalence is informative.

### Frozen reuse does not follow from completeness

An information-complete representation can still be inconvenient for a particular architecture. A downstream system may expend substantial computation decoding it. Frozen embeddings are most persuasive if they preserve useful semantic accessibility, rather than merely forcing downstream layers to relearn lexical structure.

### A historical snapshot is not a permanent closure of English

New words and senses can arise. A complete snapshot could be versioned, but indefinite freezing requires assumptions about future expressivity and updating. This does not negate the snapshot research question.

### Novelty and industry impact remain uncertain

Major pieces have precedents. Combining them may yield a valuable agenda, but a targeted search has not established novelty. Industry adoption would require compelling experiments and useful artifacts, not only the size of the vision.

## 8. A possible research program

This is a menu of investigations, not a commitment that the originator should implement all of them.

1. **Define the target.** Specify lexical units, senses, historical scope, semantic observations, allowable readouts, and approximation criteria.
2. **Assemble independent semantic challenges.** Include properties, relations, similarity, categories, graded attributes, sense distinctions, and difficult near-misses. Separate optimization evidence from evaluation.
3. **Learn representations with increasing capacity.** Control data, objectives, precision, and optimization while examining width, organization, and interpretability.
4. **Study residuals.** Ask which distinctions remain unrepresented and whether new dimensions consistently capture them.
5. **Test independent convergence.** Compare structures learned from different sources and procedures using declared semantic invariants. Control similarity measures for nuisance effects.
6. **Test frozen reuse.** Train different downstream systems on the candidate foundation and compare against learned embeddings under matched budgets. Check whether useful lexical structure remains accessible.
7. **Invite adversarial semantic challenges.** Make proposed completeness or coverage claims easy for others to contest with genuine missing distinctions.

A strong intermediate finding would be reproducible semantic coverage and dimensionality across independent learning methods, plus useful frozen transfer. It would support the program without proving full completeness.

Evidence against a strong version could include persistent non-equivalent structures under well-specified criteria, continual discovery of consequential distinctions without convergence, or a need for richer sense organization than the proposed representation allows. Failures of one optimizer alone would be inconclusive.

## 9. Closest literature identified so far

These are leads from a targeted search, not an exhaustive review or a claim that every paper has been read in full.

| Work | Overlap | Important difference |
|---|---|---|
| [Universal Dimensions of Meaning Derived from Semantic Relations among Words and Senses — Samsonovich and Ascoli, 2014](https://doi.org/10.3390/computation2030061) | Explicitly considers finite universal semantic dimensions and their independent characterization. | Its weak semantic maps omit domain-specific meaning; not complete lexical semantics. |
| [Are All Good Word Vector Spaces Isomorphic? — Vulić, Ruder, and Søgaard, 2020](https://aclanthology.org/2020.emnlp-main.257/) | Investigates near-isomorphism and the importance of data and training. | Empirical cross-language alignment, not a theorem about all complete representations. |
| [Discovering Universal Geometry in Embeddings with ICA, 2023](https://aclanthology.org/2023.emnlp-main.283/) | Finds corresponding interpretable axes across models, languages, and modalities. | Does not establish completeness or final dimensionality. |
| [On the Dimensionality of Word Embedding — Yin and Shen, 2018](https://papers.nips.cc/paper_files/paper/2018/hash/b534ba68236ba543ae44b22bd110a1d6-Abstract.html) | Studies optimal dimensionality and bias–variance trade-offs. | Optimality for data and algorithms is not intrinsic completeness of English. |
| [The Platonic Representation Hypothesis, 2024](https://proceedings.mlr.press/v235/huh24a.html) | Proposes convergence toward shared underlying representations. | Broader than lexical semantics; does not establish a complete frozen table. |
| [Revisiting the Platonic Representation Hypothesis: An Aristotelian View, 2026](https://proceedings.mlr.press/v306/groger26a.html) | Examines whether apparent convergence survives measurement calibration. | Relevant methodological challenge, not a direct refutation of this conjecture. |
| [Towards Universal Semantics With Large Language Models, 2025](https://arxiv.org/abs/2505.11764) | Uses LLMs to generate explanations based on Natural Semantic Metalanguage primitives. | Structured verbal decomposition, not a finite vector basis. |

Natural Semantic Metalanguage is an especially important conceptual predecessor: it proposes elementary meanings from which complex word meanings can be described. The number of verbal primitives must not be equated with the number of embedding coordinates, since their combinations have structure.

The distinctive proposed synthesis is: discover a complete lexical semantic structure, characterize its equivalence across independently discovered solutions, and investigate it as a shared frozen foundation. Whether that synthesis is itself new needs further research.

## 10. The originator's practical goal

The originator may choose to formulate and communicate this agenda rather than personally solve it. A short, well-grounded position paper could clarify the conjecture, acknowledge precedents, identify decisive tests, and invite collaboration.

The goal is to discover fundamental truth about English, potentially with consequences for AI and human semantic understanding. It should not be reduced automatically to improving an existing model's task score or to justifying a previously chosen implementation project.

## 11. Requested independent assessment

Please address:

1. What is the strongest coherent and nontrivial formulation of this conjecture?
2. Which claims are plausible, which are unsupported, and which might be false or tautological?
3. What mathematical structure would make semantic completeness and isomorphism meaningful?
4. Is a unique intrinsic dimensionality defensible? Under which constraints?
5. What is the closest prior work, including work missing from this brief? Distinguish proposals from established results and verify citations.
6. What would be a decisive supporting result, and what would genuinely falsify the conjecture?
7. Can completeness be certified, or is the attainable goal progressively stronger empirical coverage?
8. Would the result justify a reusable frozen lexical foundation, or is that a separate conjecture requiring additional conditions?
9. What could an independent researcher contribute through a position paper or modest experiment without claiming to solve the whole problem?
10. Is this an important research agenda, a useful synthesis of existing work, a misleading framing, or some combination? Explain your judgment directly.

Please avoid both automatic encouragement and dismissal based on contextual composition that is outside the intended target. Preserve the ambition while scrutinizing the assumptions.
