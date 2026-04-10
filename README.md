# lecture-to-anki

DISCLAIMER: I make no guarantees about accuracy, etc. You use this at your own risk.

## If this page is big scary and you've never been on Github before READ THIS: 
1. Go to claude.ai.
2. Make an account.
3. Pay for $20/month subscription.
4. Install Claude on the desktop of your computer. This won't work on your phone.
5. Log into Claude on your desktop.
6. Paste the following prompt into Claude: "Please install the lecture-to-anki skill from this GitHub repo: https://raw.githubusercontent.com/premedresources/lecture-to-anki/main/. Fetch SKILL.md, references/20-rules.md, references/card-patterns.md, and references/source-processing.md and write them to /mnt/skills/user/lecture-to-anki/ using your file tools."
7. Once that's done, you should be able to give it two files by dragging and dropping them to a new chat (or by hitting the + in the dialogue box) and asking it to please make you anki cards using the lecture-to-anki skill.
8. It should return three files - a file of QA (standard style) Anki cards, a file of Cloze style Anki cards, and a pdf of any diagrams in your lecture deck. The PDF of the diagrams is so you can make Image Occlusion cards of the diagrams, if you'd like.

A Claude skill that converts a professor's lecture slide deck (PDF) and your own lecture notes into a complete, high-quality Anki deck — automatically.

Built for pre-med students who want cards that reflect what their professor actually expects them to know.

---

## The Problem

AI flashcard generators only see your slide deck. Without additional context, they tend to:

- Generate duplicate cards testing the same fact in slightly different wording
- Bundle multiple facts into single cards with 4–6 blanks (which fail during review)
- Card low-yield or explicitly out-of-scope content because they have no way to know what the professor flagged
- Produce almost no Q&A cards — the kind that build actual reasoning, not just recall
- Miss the "why" behind every fact

## The Solution

This skill takes **two inputs simultaneously**:

1. **Your professor's slide deck** (PDF) — the ground truth of what was shown in lecture
2. **Your own lecture notes** (pasted text) — your exam scope map, with explicit "must know" and "do NOT need to know" markers

By cross-referencing both, the skill knows what to card, how deeply to card it, what to skip entirely, and how to write answers that explain *why* — not just *what*.

---

## What You Get

Three output files per lecture:

| File | Contents |
|---|---|
| `[Course]-[Topic]-cloze.txt` | Tab-separated cloze cards, ready to import into Anki |
| `[Course]-[Topic]-qa.txt` | Tab-separated Q&A cards, ready to import into Anki |
| `[Course]-[Topic]-diagrams.pdf` | Filtered PDF containing only diagram slides — for image occlusion in your tool of choice |

### Card quality principles (built in)
- One fact per card — no multi-blank list dumps
- Every anatomical structure card tests function, not just name
- Every contrast pair (e.g. sympathetic vs. parasympathetic) gets a dedicated contrast card
- High-interference structure pairs get reverse-direction cards
- Multi-function structures (medulla oblongata, thalamus, etc.) get one card per function
- Mnemonics get one card per item, each grounded in a physiological consequence
- Ordered sequences (evolutionary progressions, process steps) include sequence-order cards
- Out-of-scope content excluded based on your notes' explicit markers
- Answers explain *why* where possible, not just *what*

---

## How to Use

### Installation

Clone this repo into your Claude skills directory:

```bash
git clone https://github.com/YOUR_USERNAME/lecture-to-anki /mnt/skills/user/lecture-to-anki
```

Or unzip the release into `/mnt/skills/user/lecture-to-anki/`.

The skill will be picked up automatically by Claude when triggered.

### Running the skill

In a Claude session with computer use enabled:

1. Upload your professor's lecture PDF
2. Paste your lecture notes into the same message
3. Say something like: **"Make Anki cards from this deck and these notes"**

Claude will read the skill, cross-reference both sources, and produce all three output files.

### Importing into Anki

For the `.txt` files:
- Open Anki → File → Import
- Select the `.txt` file
- Set field separator to **Tab**
- Map fields to your note type (cloze or basic)
- Import

For image occlusion:
- Upload `[Course]-[Topic]-diagrams.pdf` to your image occlusion tool of choice
- Generate image occlusion cards there
- Export and import to Anki as normal

---

## File Structure

```
lecture-to-anki/
├── SKILL.md                          # Main skill — Claude reads this first
└── references/
    ├── 20-rules.md                   # Wozniak's 20 Rules of Knowledge Formulation, annotated for pre-med
    ├── card-patterns.md              # Cloze and Q&A templates, anti-patterns, file format spec
    └── source-processing.md         # How to reconcile slides vs. notes, handle diagrams, contrast pairs, sequences
```

---

## Note Type Recommendations

The skill produces standard tab-separated output compatible with any Anki note type. For best results:

- **Cloze file** → use Anki's built-in `Cloze` note type
- **Q&A file** → use Anki's built-in `Basic` note type
- Tags follow `Course::Topic::Subtopic` hierarchy (e.g. `Bio1::NervousSystem::Brainstem`)

---

## Limitations

- **Image occlusion** — spatial diagram cards cannot be generated as text cards. The diagrams PDF output is designed to make this step as easy as possible with any image occlusion tool.
- **Handwritten or scanned slides** — if the PDF is image-only with no extractable text, card quality will degrade. Clean slide decks with real text work best.
- **Notes quality** — the skill is only as good as your notes. Notes with explicit exam scope markers ("must know", "do NOT need to know") produce the best results. AI-generated notes from tools like Notion AI work well.

---

## Built On

- [Wozniak's 20 Rules of Knowledge Formulation](https://www.supermemo.com/en/blog/twenty-rules-of-formulating-knowledge) — the foundational principles behind every card decision
- [Anki](https://apps.ankiweb.net/) — spaced repetition flashcard system

---

## License

MIT — use it, modify it, share it.
