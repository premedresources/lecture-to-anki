---
name: lecture-to-anki
description: "Convert a professor's lecture slide deck (PDF) + your Notion AI-generated lecture notes (text) into a complete, high-quality Anki deck — two tab-separated import files (cloze and Q&A) — using Wozniak's 20 Rules and your established card conventions. Use this skill whenever you upload a lecture PDF and provides notes and wants Anki cards produced. Also triggers for: 'make cards from this deck', 'card this lecture', 'process this PDF + notes into Anki'. This skill produces superior output by cross-referencing both sources simultaneously."
---

# Lecture-to-Anki Skill

Converts a professor's slide deck PDF and your Notion lecture notes into two Anki import files. This skill is the primary card-generation workflow for your pre-med courses.

**This skill always reads these reference files before writing any cards:**
- `references/20-rules.md` — Wozniak's rules, annotated for pre-med. Non-negotiable quality standard.
- `references/card-patterns.md` — Cloze and Q&A templates, file formats, anti-patterns, worked examples.
- `references/source-processing.md` — How to read and reconcile the two input sources.

---

## Inputs

This skill requires exactly two inputs per session:

1. **Professor's slide deck** — uploaded as a PDF. This is the primary content source. It reflects exactly what was presented in lecture and what diagrams/visuals exist. It may be sparse, use bullet lists, and lack explanatory context.

2. **your Notion lecture notes** — provided as pasted text. These are AI-generated summaries of the same lecture, often more verbose and organized. They contain:
   - Exam-flagged content (explicit "must know" and "do NOT need to know" markers)
   - Definitions with context
   - Process/mechanism descriptions
   - Vocabulary with explanations
   - Scope guidance (what depth is expected)

**Do not proceed if either input is missing.** If only one is provided, ask for the other before doing anything else. Both are required — neither alone is sufficient.

---

## Step 0: Read Reference Files

Before doing anything else, read all three reference files:
- `references/20-rules.md`
- `references/card-patterns.md`
- `references/source-processing.md`

Do not skip this step even if you have seen these files before. They are the quality specification for every card produced.

---

## Step 1: Parse the Notes — Extract Scope and Priority Signals

Read your notes in full before touching the PDF. Extract and internally record:

### 1a. Exam scope markers
Scan for any language indicating:
- **Must know / exam-flagged** — these topics get full card coverage
- **Do NOT need to know** — these topics are explicitly excluded; do not generate any cards for them, even if the slides cover them in detail
- **Know generally / no detail needed** — card the concept only at the surface level (one card max)

These scope markers are the single most important signal in the notes. They represent what the professor explicitly told students. Respect them absolutely.

### 1b. Structural organization
Identify the major topic sections in the notes. These become the tag hierarchy for the output files.

### 1c. Definitions inventory
List every defined term. Note which ones have mechanistic explanations vs. which are purely vocabulary.

### 1d. Processes and mechanisms inventory
List every named process or multi-step mechanism. These are high-priority card candidates.

### 1e. Contrast pairs
Identify any concepts presented as opposites or comparisons (e.g., sympathetic vs. parasympathetic, primary vs. secondary response, afferent vs. efferent). Each contrast pair gets a dedicated contrast card.

### 1f. Lists and enumerations in the notes
Flag any lists. Do not card them as lists — plan to decompose each item into an individual card.

---

## Step 2: Parse the PDF — Extract Content and Visual Structure

Read the slide deck PDF with these goals:

### 2a. Content inventory
What topics are actually on the slides? Note slide-by-slide what is covered. This is the ground truth of what was actually shown in lecture.

### 2b. Visual and diagram content
Identify slides that contain:
- Labeled anatomical diagrams
- Flow charts or process diagrams
- Tables comparing concepts
- Images with structural labels

**Flag all diagram slides.** These cannot be fully captured by text cards. Note them in the output summary as candidates for image occlusion processing. Do not attempt to recreate visual spatial relationships in text cards — text cards for diagram content should test function and label meaning, not spatial arrangement.

### 2c. Slide density and emphasis
Note which topics the professor spent the most slides on — this is a proxy for exam weight. More slides = more card coverage warranted.

### 2d. Exact phrasing
Where the professor uses specific terminology or definitions on slides, prefer that exact phrasing in card answers. This matches what will appear on exams.

---

## Step 3: Cross-Reference and Reconcile

Now hold both sources simultaneously and reconcile them:

### 3a. Scope filtering
For every topic on the slides, check against the notes' scope markers:
- If notes say "do NOT need to know" → skip, regardless of slide detail
- If notes say "know generally" → one surface-level card max
- If notes say "must know" or it's exam-flagged → full coverage

### 3b. Depth calibration
The notes often contain more explanatory depth than the slides. Use the notes to understand *why* something works the way it does. Use that understanding to write mechanistically grounded cards — even when the slide only has a bullet point.

### 3c. Gap detection
Sometimes slides cover content the notes don't mention, or vice versa. Handle as follows:
- **On slides but not in notes:** Card it if it fits the course level and seems clearly exam-relevant. Tag it `[not in notes]` in the output summary.
- **In notes but not on slides:** Card it — the notes may be capturing verbal lecture content not on the slides.
- **Contradictions between sources:** Flag it. Do not card contradictory content. Note it at the end of output as `[FLAGGED - contradiction: <brief description>]`.

---

## Step 4: Plan the Card Set

Before writing a single card, produce an internal plan (do not output this to the user — use it to guide writing):

For each major topic section:
- How many cloze cards are warranted?
- How many Q&A cards?
- Which contrast pairs need dedicated contrast cards?
- Which items are list-type and need decomposition?
- Which mechanisms need step-by-step cloze sequences?
- What is explicitly excluded?

Apply Wozniak's Rule 20 (Prioritize) here: not every fact deserves a card. High-yield = mentioned in notes as exam-flagged, covered on multiple slides, or fundamental to understanding other concepts. Low-yield = appears once with no elaboration and no exam flag.

---

## Step 5: Write the Cards

### Card composition order (always follow this sequence):
1. **Contrast cards first** — these anchor discrimination between easily confused concepts
2. **Mechanism and process cards** — step-by-step cloze sequences for multi-step processes
3. **Structure-function cards** — for anatomical structures: location + function, not just name
4. **Definition cloze cards** — vocabulary with mechanistic grounding
5. **Factual detail cards** — specific values, classifications, only if exam-flagged

### Cloze card rules:
- One deletion per card in almost all cases
- Use c1, c2, c3 within a SINGLE card only when blanks are genuinely interdependent (e.g., a paired contrast where knowing one implies the other should be visible as context)
- The blank must require actual retrieval — not pattern-matchable from surrounding text
- Include a [domain tag] at the end of every cloze card text for context
- Keep surrounding context short — it is a cue, not a lecture

### Q&A card rules:
- Question must be answerable cold — no assumed context
- Answer is 1–3 lines max; longer means the card is too broad
- Answers explain WHY where possible, not just WHAT
- Mechanism answers include the causal chain, not just the outcome
- Contrast answers always name both sides

### Anti-patterns — never produce these:
- A card whose answer is a list of 3+ items → decompose into one card per item
- A card testing the same fact as another card with different wording → deduplicate ruthlessly
- A cloze where the blank is trivially inferable → rewrite or cut
- A Q&A where the question contains the answer → rewrite
- A card for out-of-scope content → cut
- A card with an answer longer than 3 lines → split
- A card that names a structure without testing its function → add function
- A single cloze card that bundles multiple functions of one structure into multiple blanks → decompose. Example: the medulla oblongata controls 7 unconscious functions — that is 7 separate cards, each testing one function with the structure named in context, NOT one card with 7 blanks. Same rule applies to the thalamus, hypothalamus, temporal lobe, and any other multi-function structure.
- A mnemonic card that lists all items as a single answer → decompose into one card per item, each grounded in a physiological consequence. Example: the sympathetic "4 E's" should produce 4 cards, each connecting one E to the physiological state it describes, not one card with all four as the answer.

### Interference handling:
Whenever two concepts in the deck are likely to be confused with each other (e.g., pons vs. medulla oblongata functions, afferent vs. efferent, somatic vs. autonomic), create an explicit contrast Q&A card in addition to the individual cards for each concept.

**Contrast cards must isolate a specific dimension of difference — not describe both concepts independently.** "How does X differ from Y?" is too broad and produces stapled definitions, not real contrast. Always specify the dimension: "How does X differ from Y in [neurotransmitter / mechanism / what it controls / relationship to consciousness]?" One contrast card per meaningful dimension. See card-patterns.md for the full rules, worked bad example, and worked good examples.

For anatomical structures with high interference risk — structures that are spatially adjacent, functionally similar, or frequently confused — also generate **reverse-direction cards**. A reverse card tests the same fact from the opposite angle:
- Forward: "What does the thalamus do?" → relay center for sensory tracts
- Reverse: "Which structure serves as the relay center for sensory tracts from the spinal cord to the cerebrum?" → thalamus

This forces discrimination between similar structures (thalamus vs. hypothalamus, pons vs. medulla, hippocampus vs. amygdala) rather than just recall of a single structure's function in isolation. Generate reverse cards for any structure where a student could plausibly confuse it with an adjacent one.

---

## Step 6: Format and Output

### File 1: `[CourseName]-[Topic]-cloze.txt`
- Format: tab-separated, two columns: `Text[TAB]Tags`
- Tags use `::` hierarchy matching your existing deck conventions
- Example tag: `Bio1::NervousSystem`, `Bio1::Immunology`
- One cloze deletion per card (c1) in most cases
- Include [domain tag] at end of card text

### File 2: `[CourseName]-[Topic]-qa.txt`
- Format: tab-separated, three columns: `Front[TAB]Back[TAB]Tags`
- Same tag convention
- Answers: 1–3 lines, mechanistically grounded

### File 3: `[CourseName]-[Topic]-diagrams.pdf`
- A filtered copy of the professor's slide deck containing **only** the diagram slides flagged for image occlusion
- Extract flagged pages from the original PDF using pypdf or pikepdf
- This file is dropped directly for image occlusion card generation — no other processing needed
- If no diagram slides were flagged, skip this file and note it in the summary

### Naming convention examples:
- `BioI-NervousSystem-cloze.txt` / `BioI-NervousSystem-qa.txt` / `BioI-NervousSystem-diagrams.pdf`
- `BioI-Immunology-cloze.txt` / `BioI-Immunology-qa.txt` / `BioI-Immunology-diagrams.pdf`
- `Psych1-Memory-cloze.txt` / `Psych1-Memory-qa.txt`

---

## Step 7: Output Summary

After producing both files, output a plain-text summary (not a file) containing:

1. **Card counts** — total cloze cards, total Q&A cards
2. **Topics covered** — major sections cardd and approximate card count per section
3. **Excluded content** — what was skipped and why (out of scope, diagram-only, flagged)
4. **Diagram slides flagged** — slide numbers or topics flagged for image occlusion
5. **Contradictions flagged** — any content where slides and notes disagreed
6. **Interference zones** — concept pairs that are likely to cause confusion during review; recommend monitoring these during early review sessions
7. **Content in slides but not in notes** — anything cardd that wasn't in your notes (so you can verify it's worth keeping)

---

## Quality Checklist (run before finalizing output)

Before writing the files, scan all generated cards against this checklist:

- [ ] No card answers a list question with a list answer
- [ ] No multi-function structure (medulla, thalamus, hypothalamus, temporal lobe, etc.) has its functions bundled into one multi-blank card — each function gets its own card
- [ ] No mnemonic (4 E's, 3 D's, etc.) is carded as a single list — each item gets its own card grounded in a consequence
- [ ] No two cards test the same underlying fact
- [ ] Every anatomical structure card tests function, not just name
- [ ] Every contrast pair has a dedicated contrast card
- [ ] High-interference structure pairs have reverse-direction cards
- [ ] Ordered sequences (evolutionary progression, process steps) have at least one card testing order/sequence, not just individual item lookup
- [ ] Every out-of-scope topic is excluded
- [ ] Every cloze blank requires genuine retrieval
- [ ] Every Q&A answer is ≤3 lines
- [ ] Every mechanism card tests causal reasoning, not rote sequence
- [ ] Diagram slides have been extracted into a diagrams PDF
- [ ] Tags are consistent and follow `Course::Topic` format

---

## What This Skill Does NOT Do

- **Image occlusion card generation** — spatial label relationships on diagrams cannot be captured in text cards. Diagram slides are extracted into a filtered diagrams PDF for image occlusion.
- **First-pass teaching** — this skill produces retention cards, not learning material. The student should have attended lecture or read the notes before importing the deck.
- **Card all content** — this skill curates. If a fact is low-yield, out of scope, or untestable in isolation, it is excluded. The goal is a tight, high-signal deck, not an exhaustive one.
