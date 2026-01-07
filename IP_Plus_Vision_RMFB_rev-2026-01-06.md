# IP_Plus_Vision_RMFB_rev-2026-01-06

**Project:** RMFB — Reused Manuscript Fragments in Bindings  
**Author:** David Black (DWB, GitHub @bballdave025)  
**Status:** Working vision + technical direction (evolves)  
**Companion doc(s):** [`IP_Notes_-_RMFB_2025-12-29.md`](https://github.com/bballdave025/dwb-ip-notes/blob/main/IP_Notes_-_RMFB_2025-12-29.md)  
**Repository note:** This document clarifies provenance, scope, and public disclosure boundaries to protect both the author and any current or future employers.

---

## 0. What this is (and what it is not)

This is a **vision-plus-technical direction** document for RMFB: a pipeline to discover, classify, and prioritize **information-bearing writing-surface traces** in digitized images of book bindings and related material contexts.

It is **not** a claim that the core ideas are unprecedented; it is a claim that the author has not yet located a project that combines these elements at the same scale and with this specific operational framing. If you have prior art, related work, or parallel efforts, please contact me—I will cite promptly and gratefully.

This document is also **collaboration-friendly by design**: it identifies where domain experts (codicology, conservation, paleography, textual criticism, library science) are essential, and where machine learning can help without pretending to replace scholarship.

---

## 1. Why this exists now

A threshold has been crossed:

- **Digitization scale** has created an effectively astronomical universe of images containing bindings, covers, pastedowns, flyleaves, spine interiors, sewing structures, and repair traces.
- **Modern computer vision** is now capable of high-recall triage across messy, real-world imagery.
- **The bottleneck is no longer images.** The bottleneck is discovery, prioritization, and expert attention.

RMFB exists to turn that bottleneck into a pipeline.

---

## 2. The core intuition

When reused manuscript fragments appear in bindings (or associated structural contexts), they can be:

- textual witnesses (variants, lost exemplars, transmission evidence),
- material history signals (workshop practices, repair cultures, economics),
- preservation opportunities (targeted documentation or conservation),
- discovery triggers (the “one weird binding” that opens a cluster).

These signals span a wide range of visual scales—from large, obvious reuse to faint traces that approach the limits of recoverability under downsampling.

A scalable approach must handle both extremes.

---

## 3. “Reuse” is not a binary — taxonomy as infrastructure

Digitized bindings contain **multiple overlapping phenomena**, including:

- reuse where fragments predate the bound text,
- reuse that is *younger* than the bound text (rebinding, reinforcement, repair),
- structural interventions that mimic writing,
- non-textual marks resembling strokes,
- genuine writing outside the focal document.

For **project-vision purposes**, RMFB uses the following **A–H taxonomy** to motivate scope, model needs, and collaboration—not to prescribe final labeling granularity.

### Vision Taxonomy (A–H)

- **A — Obvious reuse (canonical anchor)**  
  Clear, high-footprint reuse serving as ground truth and onboarding exemplar.

- **B — Low-footprint reuse (motivating difficulty)**  
  Small, faint, or partial writing traces that are legible at full resolution but easily lost under downsampling.

- **D — Ambiguous (abstention-critical)**  
  Marks that plausibly indicate writing but may also be shadow, wear, or texture.

- **E — Peripheral reuse outside the focal document**  
  Reuse visible on work surfaces or adjacent objects captured incidentally.

- **F — Non-reuse with high collaborator value**  
  Information-rich images that are not reuse but attract scholarly expertise.

- **G — Structural intervention (e.g., stitching)**  
  Repairs or manufacture marks that resemble text-like patterns.

- **H — Motivating exemplar**  
  An image whose cultural and technical significance makes RMFB feel necessary.

*(Class C was intentionally deprecated to preserve label integrity.)*

---

## 4. Inline exemplars (editorial selection)

### Figure 1 — Canonical reuse (Class A)

![Canonical reuse: manuscript fragment reused as binding material, rotated and cut to size, clearly showing inverted text serving as a pastedown or flyleaf.](https://raw.githubusercontent.com/bballdave025/rib-wrist-in-bin-din/refs/heads/main/img/project_vision/BnF_-_Ms-Lat-17385_00003_mbr_fmr_scg.jpg)

**Alt text (29 words):**  
A manuscript fragment with legible medieval text is visibly cut, inverted, and reused as a pastedown or flyleaf inside a later binding, clearly demonstrating intentional material reuse.

---

### Figure 2 — Low-footprint reuse with zoom (Class B)

![Low-footprint reuse visible only at full resolution, with faint but separable letterforms embedded in binding material.](https://raw.githubusercontent.com/bballdave025/rib-wrist-in-bin-din/refs/heads/main/img/project_vision/FamilySearch_-_DGS004534287_00361.jpg)

**Alt text (33 words):**  
Faint, partial writing appears along a binding surface with a very small pixel footprint; individual letterforms are separable at full resolution but would be lost under typical downsampling.

This class motivates **Nyquist-aware design**: the information exists, but only if resolution and bit depth are preserved.

---

## 5. The “fakeout” strategy (high recall without drowning humans)

RMFB embraces convincing fakeouts as first-class citizens:

- Train explicit fakeout categories.
- Use calibrated thresholds and abstention.
- Preserve reviewer trust by showing *why* a candidate was flagged.

The goal is not perfection, but honesty about uncertainty.

---

## 6. Collaboration-first explainability

RMFB is built to **support**, not replace, domain expertise.

Models should:
- show candidate regions,
- expose uncertainty,
- preserve provenance,
- invite expert interpretation.

The promise is simple: *your expertise remains the gold standard*.

---

## 7. Democratization and scale

RMFB supports multiple entry points—from phone-scale triage to institutional compute—so discovery is not limited by resources.

---

## 8. Expensive-imaging targeting

RMFB nominates candidates for MSI and MA-XRF, enabling institutions to focus scarce imaging resources where they matter most.

---

## 9. Model roadmap (M0–M9)

*(Roadmap unchanged from prior version; see previous commit for full details.)*

---

## 10. Near-term deliverables

- A curated review queue with overlays and fakeouts.
- A collaborator-facing explainer.
- Clear protocols for refinement, attribution, and publication.

---

## 11. Rights, provenance, and respect

RMFB avoids “scrape-first” behavior and respects institutional constraints by default.

---

## 12. Appendix — exemplar gallery

### Appendix A — Ambiguous marks (Class D)

![Ambiguous marks requiring expert interpretation.](https://raw.githubusercontent.com/bballdave025/rib-wrist-in-bin-din/refs/heads/main/img/project_vision/France-BibMunMetz_-_Ms-12324_00246_fko_nbr.jpg)

**Alt text (34 words):**  
Dark, structured marks appear near decorative elements; some resemble cursive strokes while others may be shadow or wear, illustrating ambiguity that cannot be resolved confidently without expert review.

---

### Appendix B — Peripheral reuse context (Class E)

![Peripheral objects captured during digitization.](https://raw.githubusercontent.com/bballdave025/rib-wrist-in-bin-din/refs/heads/main/img/project_vision/FamilySearch_-_DGS004482113_00577.jpg)

**Alt text (30 words):**  
Stacks of books and other objects appear at the edge of a digitized image, revealing reused or annotated materials outside the focal document and motivating whole-image reasoning.

---

### Appendix C — Non-reuse collaborator bait (Class F)

![Information-rich non-reuse artifact.](https://raw.githubusercontent.com/bballdave025/rib-wrist-in-bin-din/refs/heads/main/img/project_vision/GentUnivBib_-_BHSL-HS-0076_00012_mmx_nbr.jpg)

**Alt text (27 words):**  
A non-reused manuscript feature with rich material detail, valuable for scholarly interpretation and collaboration despite not representing reuse.

---

### Appendix D — Structural intervention (Class G)

![Parchment stitching repair.](https://raw.githubusercontent.com/bballdave025/rib-wrist-in-bin-din/refs/heads/main/img/project_vision/FamilySearch_-_DGS008268002_00562_mmx_nbr.jpg)

**Alt text (32 words):**  
Stitching repairs close parchment damage using thread that is partially preserved or lost, producing linear patterns that can mimic writing but represent structural intervention.

---

### Appendix E — Motivating exemplar (Class H)

![Culturally significant reused text motivating RMFB.](https://raw.githubusercontent.com/bballdave025/rib-wrist-in-bin-din/refs/heads/main/img/project_vision/FamilySearch_-_DGS008225062_00218.jpg)

**Alt text (31 words):**  
A reused manuscript fragment of high cultural and historical significance, legible at full resolution, whose vulnerability and recoverability exemplify why systematic discovery is necessary.

---

## Closing note

RMFB exists to illuminate the **boundary between visually recoverable information and features that require direct physical inspection of the artifact**—and to make that boundary honest, collaborative, and actionable.

*End of document (rev-2026-01-06).*
