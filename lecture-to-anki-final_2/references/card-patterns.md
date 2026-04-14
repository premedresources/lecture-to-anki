# Card Design Patterns for Pre-Med Material

Concrete templates and anti-patterns for the two card types this skill generates: **Cloze** and **Q&A**. Read alongside 20-rules.md.

---

## Card Type 1: Cloze

### When to use
- Definitions: fill in the term or the defining property
- Mechanisms: one cloze per step, surrounding context intact
- Sequences: adjacent steps provide cues for the blanked one
- Relationships and named classifications

### Design rules
- **One deletion per card** in most cases. Multiple deletions (c1, c2) only when the blanks are so coupled that knowing one nearly implies the other — otherwise split.
- The blank should be the *meaningful* term, not a preposition or filler.
- Keep non-blanked context short: it's a cue, not a lecture.
- Add a [domain tag] at the end of every card.

### Anti-patterns
- Blanking an entire clause → split it
- Blanking something trivially inferable from surrounding text
- Blanking a word that appears verbatim elsewhere in the same sentence

### File format (Anki tab-separated import: Text TAB Tags)
```
The {{c1::sarcomere}} is the functional unit of a myofibril.	Biology::Muscle
ATP synthase uses a {{c1::proton gradient}} to drive phosphorylation of ADP.	Biochem::ETC
Apoptosis is a form of {{c1::programmed cell death}} that does NOT trigger inflammation.	CellBio
```

---

## Card Type 2: Q&A (Basic)

### When to use
- Mechanism questions: "What happens when X?" / "Why does Y occur?"
- Comparison/contrast: "How does X differ from Y?" — high-yield for combating interference
- Consequence/application: "What is the result of X deficiency?"
- Reasoning: "Why does X cause Y?"

### Design rules
- Question must be specific enough to have exactly one defensible answer.
- Answer is 1–3 lines max. Longer = the card is too broad, split it.
- Question must be self-contained — answerable cold without seeing source material.
- Don't embed the answer in the question ("Explain why ATP synthase uses a proton gradient to...").
- For mechanism cards, the answer explains the *why*, not just restates the *what*.

### High-value Q&A patterns that build understanding

**Consequence cards** (causal reasoning):
- Q: What happens to blood pH when the kidneys retain more bicarbonate?
- A: pH rises (metabolic alkalosis) — bicarbonate buffers excess H+.

**Contrast cards** (discrimination between similar concepts):

A contrast card must isolate a **specific dimension** on which two concepts meaningfully differ and make that dimension the frame of the question. It is NOT two definition cards stapled together.

**Bad contrast card:**
- Q: How does the thalamus differ from the hypothalamus in function?
- A: Thalamus: sensory relay station — routes signals from spinal cord to cerebrum; also handles pain, temperature, touch, emotions, arousal. Hypothalamus: homeostatic regulator — controls body temperature, sleep/wake, appetite, thirst, sexual arousal, and endocrine function via the pituitary.

This is two definitions side by side. The question is too broad ("in function") and the answer is too long. It trains the student to recite both descriptions, not to discriminate between them.

**Good contrast card — dimension-specific:**
- Q: How does the thalamus differ from the hypothalamus in their relationship to conscious awareness?
- A: Thalamus: gates what reaches conscious awareness — relays and filters sensory signals (pain, touch, temperature) on their way to the cerebrum. Hypothalamus: drives unconscious homeostatic responses — hunger, thirst, temperature regulation, sleep, endocrine output. Thalamus = toward consciousness; hypothalamus = toward the body.

**Rules for contrast cards:**
- The question must name a specific dimension: "in neurotransmitter used", "in their relationship to X", "in what they control", "in speed of response"
- "How does X differ from Y?" alone is too broad — always add the dimension
- The answer must explicitly name both sides and show how they diverge on that dimension
- One contrast card per meaningful dimension — if two structures differ in three ways, write three contrast cards, each isolating one
- The answer should end with a discriminating summary if possible: a short phrase that crystallizes the distinction ("Thalamus = toward consciousness; hypothalamus = toward the body")

**More good examples:**
- Q: How does the somatic nervous system differ from the autonomic in the type of movement controlled?
- A: Somatic: voluntary — controls skeletal muscle under conscious direction. Autonomic: involuntary — controls smooth muscle, cardiac muscle, and glands without conscious input.

- Q: How does memorization differ from skill learning in the cellular mechanism involved?
- A: Memorization: strengthens existing synaptic connections — fast but fragile. Skill learning: creates new neural connections via mechanisms similar to brain growth — slow but durable.

**Why cards** (mechanism over memorization):
- Q: Why does left heart failure cause pulmonary edema?
- A: Backed-up pressure in pulmonary veins raises capillary hydrostatic pressure, forcing fluid into alveolar space.

**Clinical transfer cards**:
- Q: A patient has low serum calcium. What would you expect to happen to PTH?
- A: PTH rises — hypocalcemia is the primary stimulus for PTH secretion by the parathyroid glands.

### File format (Anki tab-separated import: Front TAB Back TAB Tags)
```
What is the driving force for glomerular filtration?	Net filtration pressure = glomerular hydrostatic pressure minus (oncotic pressure + Bowman's capsule pressure).	Physiology::Renal
Why does the liver convert ammonia to urea?	Free ammonia is neurotoxic. Urea is non-toxic, water-soluble, and renally excreted.	Biochem::NitrogenMetabolism
How does apoptosis differ from necrosis in inflammatory response?	Apoptosis: no inflammation (contents packaged for phagocytosis). Necrosis: triggers inflammation (cell rupture releases contents).	CellBio
```

---

## Translating Common Pre-Med Content into Good Cards

### Definitions
BAD: Q: What is apoptosis? / A: Programmed cell death involving caspases, DNA fragmentation, membrane blebbing, and phagocytosis without inflammation.
— Four separate facts bundled. Split them.

BETTER:
- Cloze: Apoptosis is a form of {{c1::programmed cell death}} that does not trigger inflammation. [CellBio]
- Q&A: How does apoptosis differ from necrosis in terms of inflammatory response? / Apoptosis does not trigger inflammation — cell contents are packaged for phagocytosis. Necrosis does — cell rupture releases contents that activate immune response.

### Mechanisms (multi-step)
BAD: Q: Describe the complement cascade. / A: [6-line paragraph]
— Each step needs its own card.

BETTER (cloze sequence):
- C3 convertase cleaves {{c1::C3}} into C3a and C3b. [Immunology]
- C3b binds pathogens and acts as an {{c1::opsonin}}. [Immunology]
- The membrane attack complex (MAC) forms a {{c1::pore}} in the pathogen membrane. [Immunology]

### Lists and enumerations
BAD: Q: What are the fat-soluble vitamins? / A: A, D, E, K.
— List memorization that doesn't transfer.

BETTER: Convert each item into its own mechanistically grounded card:
- Q: Which fat-soluble vitamin is required for synthesis of clotting factors II, VII, IX, and X? / A: Vitamin K.
- Q: Deficiency of which fat-soluble vitamin causes night blindness? / A: Vitamin A — required for rhodopsin synthesis in rod cells.
- Use a mnemonic (ADEK) only as a redundancy card, not the primary encoding.

### Clinical consequences
Frame as: "Given normal physiology X, what breaks when X is disrupted?"
- Q: A patient is taking a loop diuretic. What electrolyte imbalance is most expected and why?
- A: Hypokalemia — loop diuretics block the Na+/K+/2Cl− cotransporter in the thick ascending limb, increasing K+ excretion in the collecting duct via aldosterone-driven exchange.
