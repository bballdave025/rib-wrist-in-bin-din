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
