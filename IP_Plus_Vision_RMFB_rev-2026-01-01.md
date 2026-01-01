# IP_Plus_Vision_RMFB_rev-2026-01-01

**Project:** RMFB — Reused Manuscript Fragments in Bindings  
**Author:** Dave Black (DWB, &nbsp;&nbsp;&nbsp;&nbsp; GitHub @bballdave025)  
**Status:** Working vision + technical direction (evolves)  
**Companion doc(s):** [`IP_Notes_-_RMFB_2025-12-29.md`](#) (snapshot log)  
**Repository note:** This document is intended to protect both the author and any current/future employers by clarifying provenance, scope, and public disclosure boundaries.

---

## 0. What this is (and what it is not)

This is a **vision-plus-technical direction** document for RMFB: a pipeline to discover, classify, and prioritize **information-bearing writing-surface traces** in digitized images of book bindings and related material contexts.

It is **not** a claim that the core ideas are unprecedented; it is a claim that the author has not yet located a project that combines these elements at the same scale and with this specific operational framing. If you have prior art, related work, or parallel efforts, please contact me—I will cite promptly and gratefully.

This document also aims to be **collaboration-friendly**: it identifies where domain experts (codicology, conservation, paleography, textual criticism, library science) are essential, and where machine learning can help without pretending to replace scholarship.

---

## 1. Why this exists now

A threshold has been crossed:

- **Digitization scale** (including large public repositories and institutional programs) has created an effectively “astronomical” image universe of bindings, covers, pastedowns, flyleaves, spine interiors, sewing structures, and repair traces.
- **Modern CV** has reached a point where high-recall triage and weak localization can be practical across messy, real-world imagery.
- **The bottleneck is no longer images.** The bottleneck is discovery, prioritization, and scholarly attention.

RMFB exists to turn that bottleneck into a pipeline.

---

## 2. The core intuition

When reused manuscript fragments appear in bindings (or associated structural contexts), they can be:

- **Textual witnesses** (variants, lost exemplars, transmission evidence)
- **Material history signals** (workshop practices, repair cultures, economic constraints)
- **Preservation opportunities** (preventive conservation, targeted documentation)
- **Discovery triggers** (the “one weird binding” that opens an entire cluster)

The difficulty is that signals range from:

- **high pixel footprint** (large, obvious, cover-level reuse), to
- **low pixel footprint** (tiny wraparound writing, partial strokes, faint offsets, sewing-structure glimpses, iron-gall ghosting, adhesive shadows).

A scalable approach must handle both extremes.

---

## 3. “Reuse” is not a binary — taxonomy as infrastructure

A key RMFB decision is to treat the task as more than “reuse vs. no reuse.”

Real images include:

- genuine reuse in bindings,
- reuse not in bindings (important but different),
- writing-like fakeouts,
- structural textures that mimic strokes,
- repairs, stitches, seams, and occlusions,
- ink phenomena (iron-gall, bleed-through, offsets),
- photographed artifacts that produce misleading cues (lighting, glare, compression).

Therefore RMFB uses a **taxonomy** designed for machine learning *and* scholarship:

1. It supports **multi-label reality** (an image can contain more than one phenomenon).
2. It explicitly reserves classes for **non-reuse** that are *convincing* (hard negatives).
3. It documents where the author is **not specialized enough** to safely over-subclassify, and collapses classes accordingly to preserve label integrity.

The taxonomy is a collaboration hook: experts can refine it; ML can operationalize it.

---

## 4. The “fakeout” strategy (high recall without drowning humans)

A central operational goal is:

- **Miss almost nothing** (high recall),
- while **not burying reviewers** in junk.

RMFB explicitly embraces *convincing fakeouts* as part of the design:

- Train models that treat “fakeouts” as a first-class negative category.
- Use **threshold games** (or abstention) to keep recall high while filtering obvious non-candidates.
- Accept that some fraction of “review queue” will be fakeouts—*but fakeouts with a purpose*: they keep the system honest, calibrated, and explainable.

This is not merely a metric hack; it is how you protect scarce expert attention.

---

## 5. Collaboration-first explainability

RMFB is designed to attract and support collaborators who already have deep expertise:

- codicologists,
- paleographers,
- textual critics,
- conservators,
- historians of the book,
- librarians and digitization program staff.

The pipeline should be **trust-building**:

- show *why* a candidate was flagged (saliency / weak localization),
- expose uncertainty (calibration + abstention),
- preserve provenance and metadata,
- produce reviewable outputs rather than opaque scores.

The implicit promise is: “Your expertise remains the gold standard; RMFB exists to bring you better candidates faster.”

---

## 6. Democratization: from archive intern to senior scholar

Not every institution has the same resources.

RMFB aims to create multiple “entry points”:

- **Phone camera / low compute**: a lightweight model that flags obvious candidates.
- **Laptop / modest GPU**: higher quality triage with explainability overlays.
- **Institutional compute**: ensembles, self-supervised pretraining, and deeper analysis.
- **Specialized lab access**: targeted MSI / MA-XRF for the best candidates.

This matters because the discovery surface is global, while resources are uneven.

---

## 7. Expensive-imaging targeting: MSI / MA-XRF as an outcome

Some of the highest-value cases will require more than RGB.

RMFB explicitly plans to nominate targets for:

- **MSI** (multispectral imaging) to recover faint writing, offsets, or undertext;
- **MA-XRF** (macro X-ray fluorescence scanning) to map element-rich inks/pigments even when visually obscured.

RMFB’s contribution is to make that targeting practical at scale: “Scan these 20, not these 2,000.”

---

## 8. Model roadmap (M0–M9)

This roadmap is intentionally modular. “Early wins” are prioritized, and later models can be added without breaking the pipeline.

### M0 — Dataset & provenance backbone
- Canonical ingestion of image + metadata.
- Immutable identifiers.
- Clear separation of: raw images, derived crops/tiles, labels, model outputs.
- Optional per-image attribution scaffold (institution, collection, link, rights notes).

### M1 — High-precision triage classifier with calibration + abstention
Goal: A first-pass gate that is *reliable*.

- Train a classifier to separate: “likely candidate / likely non-candidate,” plus key high-level categories.
- Add:
  - **calibration** (probabilities that mean something),
  - **abstention** (a “not sure” outcome for ambiguous cases),
  - a recall-oriented operating mode.

Deliverables:
- A ranked review queue.
- An “abstain queue” explicitly marked for human decision.
- Simple, interpretable metrics (recall-heavy plus reviewer burden estimates).

### M2 — Weakly supervised localization (where is the signal?)
Goal: Show *where* the model is looking.

- CAM / Grad-CAM style heatmaps as baseline.
- Upgrade to weak localization (e.g., class activation maps + postprocessing) to estimate “candidate regions.”
- Use those regions to enable *safe augmentation* and better cropping/tiling decisions.

### M3 — Tiling / stitching models for tiny writing (low pixel footprint)
Goal: Don’t lose the needle by scaling down the haystack.

- Patch-based inference over high-res imagery.
- Aggregate patch evidence back into an image-level decision.
- Preserve spatial info for reviewer overlays.

### M4 — Multi-resolution strategy (explicitly)
Goal: Handle both “big cover reuse” and “tiny wraparound traces.”

- Train/evaluate across resolutions.
- Consider architectures or training regimes that preserve small-feature sensitivity.

### M5 — Architecture sweep (pragmatic)
Goal: A credible comparison across a small, meaningful set.

Candidates (illustrative, not exhaustive):
- Strong CNN baselines (ResNet family; EfficientNetV2; ConvNeXt).
- One segmentation-capable model (e.g., U-Net variant) for region discovery.
- One detection-oriented model (YOLO-like) if localization stabilizes.
- A transformer-family model (ViT / DINO / MAE style) once the supervised pipeline is stable.

### M6 — “Hard negative” fakeout specialist
Goal: Reduce reviewer pain without sacrificing recall.

- Build a dedicated fakeout filter:
  - textures mimicking strokes,
  - sewing patterns,
  - shadows/creases,
  - printed modern text,
  - glare artifacts.
- Keep it intentionally conservative (it should avoid deleting true positives).

### M7 — Semi-supervised and self-supervised expansion (later phase)
Goal: Scale beyond labeled data with discipline.

- Use self-supervised pretraining to exploit large unlabeled corpora.
- Use semi-supervised methods to incorporate confident pseudo-labels.
- Guardrails: do not degrade interpretability; do not hide errors behind scale.

### M8 — Ensemble / voting (only if justified)
Goal: When diversity truly helps.

- Combine complementary models (e.g., high-res tiler + global classifier).
- Use ensemble only if it reduces false negatives *and* preserves reviewer usability.

### M9 — Targeting outputs for MSI / MA-XRF and scholar workflows
Goal: Convert model output into real scholarly and conservation actions.

- Candidate packs:
  - images,
  - overlays,
  - provenance,
  - uncertainty summary,
  - “why flagged” regions,
  - suggested next-step imaging modality.

---

## 9. Near-term deliverables (fast, collaborator-friendly)

1. A curated “review queue” demo (50–200 images) with:
   - heatmaps,
   - fakeout examples,
   - non-reuse examples,
   - a few “wow” candidates.

2. A short collaborator-facing PDF (or page) answering:
   - What is RMFB?
   - What will you get if you join?
   - What does RMFB need from you?

3. A clear protocol for:
   - label refinement,
   - provenance handling,
   - publication / attribution norms.

---

## 10. Rights, provenance, and institutional respect

RMFB is designed to respect:

- the source institutions’ rights and attribution expectations,
- the fact that digitization is expensive and often policy-bound,
- the ethical obligation to avoid “scrape-first, ask-later” behaviors.

The project’s license and public artifacts should be chosen to protect:
- institutions (FamilySearch, national libraries, university libraries, archives),
- collaborators,
- and downstream users who want to do the right thing.

A practical approach is:
- Keep raw images out of the repo unless explicitly allowed.
- Keep links, identifiers, and derived metadata in standardized form.
- Provide a reproducible “fetch/ingest” procedure that honors terms.

---

## 11. Closing note: why this feels like a calling

RMFB is not only a technical project. It is a bridge between:
- scale and care,
- automation and scholarship,
- discovery and preservation.

It is built to surface what might otherwise remain unseen—while keeping human meaning, context, and responsibility at the center.

---

*End of document (rev-2026-01-01).*
