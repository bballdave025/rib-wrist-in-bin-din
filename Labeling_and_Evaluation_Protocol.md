NO GREAT FORMATTING, YET. THREE PARTS, NOW SEPARATED FROM EACH OTHER AND FROM THIS DESCRIPTION BY TRIPLE HYPHENS, WHICH WILL NEED TO BE WOVEN TOGETHER.

The second seems like it might be an incomplete copy/pasting of the first.

---

Labeling & Evaluation Protocol
Overview
This project involves detecting reused manuscript materials—particularly reuse in bindings—across large, heterogeneous digitized image corpora. Because the phenomena of interest include low-visibility signals, material ambiguity, and historically contingent interpretation, we adopt a labeling and evaluation protocol that explicitly separates:
Ground annotation constraints
Model decision behavior
Evaluation philosophy
This separation allows us to remain honest about uncertainty while still producing results that are comparable, reproducible, and useful to collaborators.
1. Ground Annotation Policy (Initial Dataset)
1.1 Forced-decision labeling
For the initial dataset (n ≈ 3,331 images), annotations were created under a forced-decision policy:
Each image was required to receive at least:
a binding reuse vs. non-binding reuse decision
No explicit “abstain” or “uncertain” class was available at annotation time
This constraint reflects the historical reality of early-stage dataset construction and mirrors common practice in computer vision benchmarks.
1.2 Consequence
As a result:
Some images now understood as ambiguous or borderline were necessarily assigned to:
fakeout, non-reuse, or related negative classes
These labels are not treated as errors, but as products of a limited label ontology
The dataset therefore encodes both signal and epistemic pressure.
2. Expanded Label Ontology (Post hoc)
As the project matured, additional semantic categories were recognized, including:
Ambiguous / hard-to-classify cases
Convincing fakeouts
Peripheral reuse outside the focal document
Low-pixel-footprint reuse
Rather than retroactively rewriting ground truth, we preserve original labels and introduce new decision states at the model and evaluation layers.
This preserves reproducibility while enabling more expressive reasoning.
3. Model Decision Behavior
3.1 Required decisions (training phase)
During training and baseline evaluation:
Models are required to make a binding reuse vs. non-binding reuse decision
This aligns with the original annotation constraints and supports direct comparison
3.2 Abstention capability (deployment & analysis phase)
Models may additionally output an abstention / uncertainty decision (e.g., suh = seems unclear or hard) when confidence falls below a calibrated threshold.
Important clarification:
Abstention is a decision policy, not a claim about ground truth
It represents epistemic uncertainty, not absence of signal
4. Evaluation Metrics
We report two complementary evaluation regimes, always together.
4.1 Forced-decision metrics (“hard” metrics)
Purpose:
Comparability with standard CV benchmarks
Historical consistency with initial annotations
Properties:
Abstentions are penalized as errors
Standard precision, recall, and accuracy are reported
This answers:
How well does the model perform if it must decide?
4.2 Abstention-aware metrics (“selective” metrics)
Purpose:
Responsible deployment
Expert time optimization
Trustworthy collaboration
Properties:
Abstentions are not treated as errors
We report:
Coverage (fraction of images classified)
Conditional precision/recall on classified images
Selective risk
This answers:
How well does the model perform when it chooses to speak only when confident?
5. Expert Review and Final Labels
Human experts are treated as collaborators, not oracles.
Experts may:
Express uncertainty
Disagree with prior labels
Request additional imaging or context
Expert uncertainty is preserved as metadata
However:
Final adjudicated labels (post-review) are forced decisions
This ensures downstream usability for training, comparison, and archival reference
6. Ontology Evolution as a Design Principle
Differences between early annotations and later interpretations are expected and documented.
We treat label evolution as:
Evidence of increasing domain understanding
A motivation for abstention-aware modeling
A justification for collaborative review
Rather than hiding ambiguity, the protocol makes it measurable, modelable, and useful.
Summary
This protocol balances:
Historical annotation constraints
Modern uncertainty-aware modeling
Scholarly expectations of interpretability and rigor
It is designed to support:
Machine learning research
Manuscript studies collaboration
Responsible large-scale discovery

---

Labeling & Evaluation Protocol
Overview
This project involves detecting reused manuscript materials—particularly reuse in bindings—across large, heterogeneous digitized image corpora. Because the phenomena of interest include low-visibility signals, material ambiguity, and historically contingent interpretation, we adopt a labeling and evaluation protocol that explicitly separates:
Ground annotation constraints
Model decision behavior
Evaluation philosophy
This separation allows us to remain honest about uncertainty while still producing results that are comparable, reproducible, and useful to collaborators.
1. Ground Annotation Policy (Initial Dataset)
1.1 Forced-decision labeling
For the initial dataset (n ≈ 3,331 images), annotations were created under a forced-decision policy:
Each image was required to receive at least:
a binding reuse vs. non-binding reuse decision
No explicit “abstain” or “uncertain” class was available at annotation time
This constraint reflects the historical reality of early-stage dataset construction and mirrors common practice in computer vision benchmarks.
1.2 Consequence
As a result:
Some images now understood as ambiguous or borderline were necessarily assigned to:
fakeout, non-reuse, or related negative classes
These labels are not treated as errors, but as products of a limited label ontology
The dataset therefore encodes both signal and epistemic pressure.
2. Expanded Label Ontology (Post hoc)
As the project matured, additional semantic categories were recognized, including:
Ambiguous / hard-to-classify cases
Convincing fakeouts
Peripheral reuse outside the focal document
Low-pixel-footprint reuse
Rather than retroactively rewriting ground truth, we preserve original labels and introduce new decision states at the model and evaluation layers.
This preserves reproducibility while enabling more expressive reasoning.
3. Model Decision Behavior
3.1 Required decisions (training phase)
During training and baseline evaluation:
Models are required to make a binding reuse vs. non-binding reuse decision
This aligns with the original annotation constraints and supports direct comparison
3.2 Abstention capability (deployment & analysis phase)
Models may additionally output an abstention / uncertainty decision (e.g., suh = seems unclear or hard) when confidence falls below a calibrated threshold.
Important clarification:
Abstention is a decision policy, not a claim about ground truth
It represents epistemic uncertainty, not absence of signal
4. Evaluation Metrics
We report two complementary evaluation regimes, always together.
4.1 Forced-decision metrics (“hard” metrics)
Purpose:
Comparability with standard CV benchmarks
Historical consistency with initial annotations
Properties:
Abstentions are penalized as errors
Standard precision, recall, and accuracy are reported
This answers:
How well does the model perform if it must decide?
4.2 Abstention-aware metrics (“selective” metrics)
Purpose:
Responsible deployment
Expert time optimization
Trustworthy collaboration
Properties:
Abstentions are not treated as errors
We report:
Coverage (fraction of images classified)
Conditional precision/recall on classified images
Selective risk
This answers:
How well does the model perform when it chooses to speak only when confident?
5. Expert Review and Final Labels
Human experts are treated as collaborators, not oracles.
Experts may:
Express uncertainty
Disagree with prior labels
Request additional imaging or context
Expert uncertainty is preserved as metadata
However:
Final adjudicated labels (post-review) are forced decisions
This ensures downstream usability for training, comparison, and archival reference
6. Ontology Evolution as a Design Principle
Differences between early annotations and later interpretations are expected and documented.
We treat label evolution as:
Evidence of increasing domain understanding
A motivation for abstention-aware modeling
A justification for collaborative review
Rather than hiding ambiguity, the protocol makes it measurable, modelable, and useful.


---


Labeling & Evaluation Protocol
1. Scope and Philosophy
This project distinguishes primary classification labels (which define ground truth) from diagnostic annotations (which record human perception, difficulty, or error risk). Only primary labels are intended for model training. Diagnostic annotations are intentionally sparse, non-exhaustive, and historical.
Uncertainty, ambiguity, and abstention are treated as model behaviors, not human-assigned ground-truth classes.
2. Primary Labels (Training Ground Truth)
Primary labels are encoded in filenames and are required for all images in the curated dataset.
These include, at minimum:
Reuse vs. non-reuse
Binding reuse vs. non-binding reuse
Specific reuse subclasses (e.g., outside cover reuse, etc.)
These labels are assumed to be forced-choice at the dataset level, even in cases where human certainty is low. This constraint exists to support supervised training and later expert refinement.
3. Diagnostic Annotations (Non-Exhaustive, Non-Training)
3.1 fko — Fakeout (Recall-Control Diagnostic)
fko marks human-observed false affordances: visual structures that strongly resemble reuse indicators but ultimately do not correspond to the target reuse feature.
Key properties of fko:
Not exhaustive: many fakeouts are intentionally left unlabeled
Not a class: models are not expected to learn fko as a discriminative category
Orthogonal to reuse: an image may be fko and contain valid reuse of a different type
Recall-control role: highlights where humans (and models) may over-detect reuse
fko exists to document where recall pressure is dangerous, not to define negative ground truth.
fko annotations are used for:
error analysis
calibration diagnostics
explaining abstention and review workflows
pedagogy and collaborator onboarding
They are never used as training labels.
3.2 suh — Deprecated Diagnostic (Forbidden Going Forward)
suh (“seems unclear / hard”) was introduced late in dataset curation as an informal diagnostic and was used inconsistently to mark:
human uncertainty
anticipated model difficulty
ambiguous visual evidence
lack of confidence in a forced decision
Because suh conflates multiple concepts and was never rigorously defined, it is deprecated.
suh will not be used in training, evaluation, or future annotation
suh will not be used to define abstention behavior
suh may be referenced only in documentation to explain dataset evolution
No relabeling is required or desired.
4. Abstention and Ambiguity
Abstention is treated as a model-level capability, not a human label.
Humans are required to make forced primary labels during dataset creation
Models may abstain based on calibrated uncertainty thresholds
Evaluation may include:
forced-decision metrics
abstention-aware metrics
cost-sensitive recall/precision tradeoffs
Diagnostic annotations (e.g., fko) may be used to analyze abstention behavior but never to define it.
5. Evaluation Philosophy
Evaluation explicitly separates:
Ground-truth correctness
Human perceptual traps
Model confidence and calibration
Operational cost of false negatives vs. false positives
Sparse diagnostics are a feature, not a flaw: they preserve the distinction between what is known, what is suspected, and what must be decided anyway.
Summary (one-sentence anchor)
This labeling scheme enforces decisive ground truth while preserving human uncertainty as diagnostic signal rather than semantic noise.
