# proposal and manuscript Review Workflow

## Purpose
This project performs structured peer-review of proposals and manuscripts in .docx files.
For each file in /inbox, Claude produces a reviewed copy in /reviewed with:
- Word comments flagging each concern
- Track changes suggesting specific edits inline

---

## How to trigger a review
Say: "Review the proposal in /inbox" or "Review [filename].docx"

---

## Review Framework
Analyze every proposal and manuscript against these four lenses:

### 1. Methodology Gaps
- Missing controls, sample size justifications, or procedural detail
- Assumptions stated without support
- Steps that cannot be reproduced from the description alone

### 2. Objectives vs. Methods Misalignment
- Methods that do not directly address a stated objective
- Objectives that have no corresponding method
- Scope creep or methods that go beyond stated aims

### 3. Missing Validation Strategies
- Lack of pilot testing, reliability checks, or triangulation
- No mention of how instruments were validated
- Missing plans for internal/external validity

### 4. Passages Likely to Draw Reviewer Pushback
- Overclaiming causality from correlational data
- Vague quantifiers ("many", "most", "significant") without data
- Unsupported generalizations beyond the study population
- Logical jumps between evidence and conclusions

---

## Output Specification

For EACH concern found:

**Step 1 — Add a Word Comment** anchored to the relevant passage:
- Prefix with category tag: [METHODOLOGY GAP], [MISALIGNMENT],
  [VALIDATION], or [REVIEWER RISK]
- State the concern clearly in 1–3 sentences
- Suggest what is needed to address it

**Step 2 — Add a Track Change** at the same location:
- Insert a brief inline suggestion using tracked insertion
- If text should be removed, mark it as a tracked deletion
- Author name for all changes: "Claude"

---

## Technical Steps (follow in order)

1. Copy the source file from /inbox to /reviewed as
   [filename]_reviewed.docx — NEVER modify the original
2. Unpack: `python scripts/office/unpack.py`
3. Read document.xml to identify all flagged passages
4. For each concern:
   a. Run `python scripts/comment.py` to register the comment
   b. Add <w:commentRangeStart>, <w:commentRangeEnd>, and
      <w:commentReference> markers in document.xml
   c. Add <w:ins> or <w:del> tracked change at the same location
5. Pack: `python scripts/office/pack.py`
6. Validate the output opens correctly

---

## Quality Rules
- Every comment MUST have a paired track change — never one without
  the other
- Do not alter section headings or figures
- Preserve all existing formatting and styles
- If a passage triggers multiple categories, add one comment per
  category, each with its own track change
- Maximum 20 comments per document — prioritize highest-impact issues
