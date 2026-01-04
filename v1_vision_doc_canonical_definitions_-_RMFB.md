# RMFB — Vision Canonical Definitions (v1)

**Status:** Frozen (v1)  
**Scope:** Reused Manuscript Fragments in Bindings (RMFB)  
**Purpose:** Provide stable, shared semantic anchors for labeling, evaluation, and vision-based discussion.

This document defines the canonical A–E image categories used across RMFB IP notes, vision documents, model design, and evaluation protocols.

---

## A. Obvious reuse (Ground-truth anchor)

**Definition:**  
Clear, unmistakable manuscript reuse visible at a glance.

**Purpose:**  
- Serves as ground truth
- Anchors model calibration and human trust
- Establishes uncontested positive examples

**Typical features:**  
- Large, legible text fragments  
- Clear rotation or truncation  
- Obvious parchment or paper reuse in bindings  
- No plausible alternative explanation

---

## B. Low-footprint reuse (Motivation + novelty)

**Definition:**  
Genuine manuscript reuse with a very small pixel footprint relative to the full image.

**Purpose:**  
- Central novelty driver of RMFB
- Justifies high-resolution inputs, tiling, and nonstandard CV models
- Demonstrates why naive downsampling fails

**Typical features:**  
- Wraparound text  
- Partial strokes or faint ink  
- Spine-adjacent or background fragments  
- Human-recognizable only at sufficient resolution

---

## C. Fakeout (Precision / cost control)

**Definition:**  
Patterns that resemble reuse but are not reuse.

**Purpose:**  
- Controls false positives
- Enables recall-heavy strategies without overwhelming reviewers
- Supports abstention and calibrated confidence

**Typical features:**  
- Iron-gall ink damage  
- Sewing shadows  
- Leather grain  
- Wormholes, abrasion, cracking, or staining

**Note:**  
Fakeouts are diagnostic artifacts, not a target class the model is expected to positively identify.

---

## D. Ambiguous (Collaboration + humility)

**Definition:**  
Cases where confident classification is not possible without additional expertise or context.

**Purpose:**  
- Signals epistemic humility
- Invites expert collaboration
- Justifies abstention rather than forced classification

**Typical features:**  
- Borderline marks  
- Competing explanations (wear vs ink)  
- Insufficient resolution or occlusion

---

## E. Peripheral reuse outside the focal document

**Definition:**  
Manuscript reuse present in the image but not part of the manuscript being filmed.

**Purpose:**  
- Demonstrates failure of whole-image reasoning
- Justifies localization, tiling, or multi-instance analysis
- Shows how both humans and models can miss relevant reuse

**Typical features:**  
- Background books on workbenches  
- Support volumes beneath stacks  
- Adjacent codices partially in frame  
- Reuse unrelated to the filmed record itself

---

## Meta-summary

> **A anchors certainty, B motivates the work, C controls cost, D invites collaboration, and E proves why localization matters.**

---

## Versioning notes (provisional, hence the stikethrough)

- This document represents **v1 frozen semantics**
- ~~Later refinements must reference this version explicitly~~
- ~~Changes should be additive, not redefinitional, to preserve interpretability across drafts~~
- - Remember that these five (maybe more, later) images are meant to enhance the RMFB `IP_Plus_Vision` document, not to be definitional for the RMFB (rib-wrist-in-bin-din) project.
