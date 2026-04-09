# Source Processing Guide: Slides + Notes Reconciliation

This reference governs how to read, weight, and reconcile the two input sources for the lecture-to-anki skill. Read alongside 20-rules.md and card-patterns.md.

---

## The Two Sources and Their Roles

### Source 1: Professor's Slide Deck (PDF)
**Role:** Ground truth for lecture content and exam-testable material.
**Strengths:**
- Reflects exactly what was shown in class
- Professor's own phrasing — closer to how exam questions will be worded
- Visual and diagram content (irreplaceable)
- Slide emphasis (more slides on a topic = more weight)

**Weaknesses:**
- Often sparse — bullet points without explanation
- No scope guidance (doesn't tell you what's high vs. low yield)
- May include content mentioned in passing that isn't exam-relevant
- Diagrams and figures require image occlusion, not text cards

**How to read it:** Treat every slide as a data point. Note which topics get multiple slides vs. one bullet on a summary slide. Professor emphasis is signal.

---

### Source 2: Your Notion Lecture Notes (Text)
**Role:** Exam scope filter and depth calibrator.
**Strengths:**
- Contains explicit "must know" and "do NOT need to know" markers — treat these as professor directives
- More explanatory — connects facts to mechanisms
- Organized by concept rather than by slide, making relationships clearer
- Vocabulary section with context-rich definitions
- Process/mechanism sections ideal for step-by-step cloze sequences

**Weaknesses:**
- AI-generated — occasionally imprecise phrasing
- May not capture everything on slides (verbal lecture additions)
- Organization may not match slide order

**How to read it:** The notes are the exam scope map. Use them to filter the slides, not to replace them. When notes say "do NOT need to know," that is an absolute exclude signal, regardless of how much slide space the topic gets.

---

## Reading Priority Rules

### Rule P1: Scope exclusions from notes are absolute.
If the notes say "you do NOT need to know X," do not card X even if:
- X appears on multiple slides
- X has a detailed diagram
- X has vocabulary definitions in the notes
The exclusion overrides everything.

### Rule P2: Exam-flagged content from notes gets full coverage.
If the notes flag something as exam-relevant or "must know," card it thoroughly:
- Definition cloze
- Function/mechanism Q&A
- Contrast card if a comparable concept exists
- Step-by-step cloze if it's a process

### Rule P3: Slides provide phrasing; notes provide depth.
When writing card answers:
- Use the professor's phrasing from slides where it exists (closer to exam language)
- Use the notes' mechanistic explanations to make answers more than rote definitions
- Blend: professor phrasing + notes context = ideal card answer

Example:
- Slide says: "Medulla oblongata — controls heart rate, breathing"
- Notes say: "Controls unconscious activities: respiratory rate, heart rate, blood vessel constriction, swallowing, hiccuping, coughing, sneezing; nerve tracts cross left-right here; origin of most cranial nerves"
- Card answer: "Controls unconscious autonomic functions: HR, respiratory rate, BP (vessel constriction), swallowing, coughing, sneezing, hiccuping. Nerve tracts cross left-right. Origin of most cranial nerves." [NervousSystem::Brainstem]

### Rule P4: Content in notes but not on slides — card it.
The notes capture verbal lecture content not always on slides. If a concept is explained in the notes with enough detail to write a good card, card it. Tag it normally.

### Rule P5: Content on slides but not in notes — use judgment.
- If it fits the course level and is clearly conceptual → card it, flag in summary
- If it appears to be a diagram label or visual aid only → flag for image occlusion
- If it's a passing reference with no elaboration → exclude, flag in summary

### Rule P6: Contradictions between sources — flag and exclude.
If slides say X and notes say Y on the same factual point, do not card either version. Note the contradiction in the output summary so you can resolve it.

---

## Handling Diagram Slides

Diagram slides are slides where the primary content is a visual — a labeled anatomical figure, a flow chart, a cross-section, a pathway diagram.

**What to do:**
1. Note the slide number and topic
2. Extract any text labels that can be tested as function/definition cards
3. Do NOT attempt to recreate spatial relationships in text cards (e.g., don't make a card saying "structure X is located superior to structure Y" based on diagram position)
4. Flag the slide in the output summary as a image occlusion candidate

**What text cards are appropriate for diagram slides:**
- Function cards for each labeled structure (if notes confirm exam relevance)
- Definition cloze for any labeled terms
- NOT: position cards, arrangement cards, or "what is adjacent to X" cards

---

## Handling the Vocabulary/Definitions Section of Notes

Lecture notes typically include a dedicated definitions section. Process it as follows:

1. For each defined term, check if it's already covered by a mechanism/process card → if so, the definition card may be redundant; use judgment
2. If the definition adds context not in the mechanism card → write a cloze definition card
3. If the term is in the "do NOT need to know" exclusion zone → skip it even if it has a definition
4. If the definition is purely circular ("X is the process of doing X") → skip it
5. For multi-part definitions, apply Rule 4 (minimum information) → one cloze per meaningful fact in the definition

**Good definition → cloze example:**
- Definition: "Opsonization — marking of pathogens by antibodies for destruction by macrophages"
- Cloze: "Opsonization is the marking of pathogens by {{c1::antibodies}} to facilitate their destruction by macrophages. [Immunology]"
- NOT: "{{c1::Opsonization}} is the marking of pathogens by antibodies for destruction by macrophages." (blanking the term is fine only if the definition is being tested in reverse — but that's a separate card)

---

## Handling Process/Mechanism Sections of Notes

When the notes include a numbered process (e.g., "Vaccine function: 1. Vaccination acts as first exposure... 2. Body mounts primary response..."), convert it as follows:

1. Do NOT make one card for the whole process
2. Do NOT make a card that asks "list all steps of X"
3. DO make one cloze card per meaningful step, with surrounding steps as context cues
4. The blank in each step should be the most meaningful term — the one that, if forgotten, would break understanding of that step
5. If a step is purely transitional ("step 3 leads to step 4"), collapse it into an adjacent step's card

**Example — Reflex arc:**
Notes: "1. Sensory nerve detects stimulus → 2. Signal travels to spinal cord → 3. Spinal cord processes without brain → 4. Motor nerve sends signal to muscles → 5. Body responds reflexively"

Cards:
- "In a reflex arc, the signal is processed in the {{c1::spinal cord}} without traveling to the brain. [NervousSystem::SpinalCord]"
- "In a reflex arc, the {{c1::sensory (afferent)}} nerve carries the stimulus signal toward the spinal cord. [NervousSystem::SpinalCord]"
- "The reflex arc bypasses the brain to enable {{c1::faster}} response times for protective reflexes. [NervousSystem::SpinalCord]"

## Handling Ordered Sequences (Evolution, Developmental Progressions)

When the notes or slides present an ordered progression (e.g., evolutionary complexity from simple to complex organisms), do NOT card each item only as an isolated lookup. Also generate at least one card that tests the sequence itself — what comes before, what comes after.

**Example — Evolution of nervous systems:**
Bad approach: one card per organism testing only "what type of NS does X have"
Better approach: also include cards like:
- "In the evolutionary progression of nervous systems, {{c1::flatworms}} represent the first organisms with cephalization, coming after cnidarians and echinoderms." 
- "In nervous system evolution, which group comes after annelids and before mollusks? {{c1::Arthropods (insects)}}"

This ensures the student can reconstruct the sequence, not just look up individual entries.

---

## Handling Contrast Pairs

Whenever two concepts are presented as opposites or complements in either source, always generate:

1. Individual cards for each concept (definition/function)
2. One dedicated contrast Q&A card: "How does X differ from Y in [specific dimension]?"

**High-priority contrast pairs to always card:**
- Sympathetic vs. Parasympathetic (multiple dimensions: NT used, effects, "motto")
- Afferent vs. Efferent
- Somatic vs. Autonomic
- CNS vs. PNS
- Short-term vs. Long-term memory (location, mechanism, stability)
- Memorization vs. Skill learning (speed, mechanism, durability)
- Primary vs. Secondary immune response (if immunology content present)

For each contrast card, the answer must name both sides — not just describe one.

---

## Tag Conventions

Follow your Anki tag hierarchy:

- Top level = course: `Bio1`, `Psych1`, `Chem1`
- Second level = major topic: `NervousSystem`, `Immunology`, `CellBio`
- Third level (optional) = subtopic: `Brainstem`, `SpinalCord`, `LimbicSystem`, `ANS`

Examples:
- `Bio1::NervousSystem::Brainstem`
- `Bio1::NervousSystem::ANS`
- `Bio1::NervousSystem::Memory`
- `Bio1::Immunology`

Use the most specific tag that applies without over-tagging. Every card gets exactly one tag string.
