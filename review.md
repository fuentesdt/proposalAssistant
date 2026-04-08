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
Analyze every proposal and manuscript against these ten lenses:

### 1. Significance
- Evaluate the importance of the proposed research in the context of current scientific challenges and opportunities, either for advancing knowledge within the field, or more broadly. Assess whether the application addresses an important gap in knowledge in the field, would solve a critical problem, or create a valuable conceptual or technical advance.
- Evaluate the rationale for undertaking the study, the rigor of the scientific background for the work (e.g., prior literature and/or preliminary data) and whether the scientific background justifies the proposed study.

### 2. Innovation
- Evaluate the extent to which innovation influences the importance of undertaking the proposed research. Note that while technical or conceptual innovation can influence the importance of the proposed research, a project that is not applying novel concepts or approaches may be of critical importance for the field.
- Evaluate whether the proposed work applies novel concepts, methods or technologies or uses existing concepts, methods, technologies in novel ways, to enhance the overall impact of the project.

### 3. Approach
- Evaluate the scientific quality of the proposed work. Evaluate the likelihood that compelling, reproducible findings will result (rigor) and assess whether the proposed studies can be done well and within the timeframes proposed (feasibility).

### 4.  Rigor
- Evaluate the potential to produce unbiased, reproducible, robust data.
- Evaluate the rigor of experimental design and whether appropriate controls are in place.
- Evaluate whether the sample size is sufficient and well-justified.
- Assess the quality of the plans for analysis, interpretation, and reporting of results.
- Evaluate whether the investigators presented adequate plans to address relevant biological variables, such as sex or age, in the design, analysis, and reporting.
- For applications involving human subjects or vertebrate animals, also evaluate: the rigor of the intervention or study manipulation (if applicable to the study design), whether outcome variables are justified, whether the results will be generalizable or, in the case of a rare disease/special group, relevant to the particular subgroup, whether the sample is appropriate and sufficiently diverse to address the proposed question(s).
- For applications involving human subjects, including clinical trials, assess the adequacy of inclusion plans as appropriate for the scientific goals of the research. Considerations of appropriateness may include disease/condition/behavior incidence, prevalence, or population burden, population representation, and/or current state of the science.
- Missing controls, sample size justifications, or procedural detail
- Assumptions stated without support
- Steps that cannot be reproduced from the description alone
- Methods that do not directly address a stated objective
- Objectives that have no corresponding method
- Scope creep or methods that go beyond stated aims
- Lack of pilot testing, reliability checks, or triangulation
- No mention of how instruments were validated
- Missing plans for internal/external validity

### 5.  Feasibility
- Evaluate whether the proposed approach is sound and achievable, including plans to address problems or new challenges that emerge in the work. For proposed studies in which feasibility may be less certain, evaluate whether the uncertainty is balanced by the potential for major advances.
- For applications involving human subjects, including clinical trials, evaluate the adequacy and feasibility of the plan to recruit and retain a study population that appropriately models the target population. Additionally, evaluate the likelihood of successfully achieving the proposed enrollment based on age, race, ethnicity, and sex.
- For clinical trial applications, evaluate whether the study timeline and milestones are feasible.

### 6.  Investigator(s)
- Evaluate whether the investigator(s) have demonstrated background, training, and expertise, as appropriate for their career stage, to conduct the proposed work. For Multiple Principal Investigator (MPI) applications, assess the quality of the leadership plan to facilitate coordination and collaboration.

### 7.  Environment
- Evaluate whether the institutional resources are appropriate to ensure the successful execution of the proposed work.

### 8.  Protections for Human Subjects 
- For research that involves human subjects but does not involve one of the categories of research that are exempt under 45 CFR Part 46, evaluate the justification for involvement of human subjects and the proposed protections from research risk relating to their participation according to the following five review criteria: 1) risk to subjects; 2) adequacy of protection against risks; 3) potential benefits to the subjects and others; 4) importance of the knowledge to be gained; and 5) data and safety monitoring for clinical trials.
- For research that involves human subjects and meets the criteria for one or more of the categories of research that are exempt under 45 CFR Part 46, evaluate: 1) the justification for the exemption; 2) human subjects involvement and characteristics; and 3) sources of materials. For additional information on review of the Human Subjects section, please refer to the Guidelines for the Review of Human Subjects.

### 9.  Vertebrate Animals 
- When the proposed research includes Vertebrate Animals, evaluate the involvement of live vertebrate animals according to the following criteria: (1) description of proposed procedures involving animals, including species, strains, ages, sex, and total number to be used; (2) justifications for the use of animals versus alternative models and for the appropriateness of the species proposed; (3) interventions to minimize discomfort, distress, pain and injury; and (4) justification for euthanasia method if NOT consistent with the AVMA Guidelines for the Euthanasia of Animals. For additional information on review of the Vertebrate Animals section, please refer to the Worksheet for Review of the Vertebrate Animals Section.

### 10. Passages Likely to Draw Reviewer Pushback
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
