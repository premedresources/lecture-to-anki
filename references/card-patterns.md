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
- Q: How does primary vs. secondary active transport differ in energy source?
- A: Primary uses ATP directly (e.g., Na+/K+ ATPase). Secondary couples to an existing ion gradient (e.g., SGLT1 uses Na+ gradient to co-transport glucose).

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
