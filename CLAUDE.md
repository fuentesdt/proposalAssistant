# Proposal Assistant

## Project Overview
- **Grant type**: [NIH R01 / NSF / DoD / etc.]
- **Submission deadline**: [Date]
- **Funding agency**: [Agency name]
- **Project title**: [Title]

<!-- The **directory map** lets Claude know exactly where to look for source material versus output files.-->
<!-- Separating **LaTeX as source of truth** from Word avoids conflicting edits across formats.-->
## Directory Structure
/project-root
├── CLAUDE.md
├── /references          # Research papers and literature
│   ├── /background
│   ├── /preliminary-data
│   └── /methods
└── /grant-documents     # Main grant files
    ├── /latex
    │   ├── specific_aims.tex
    │   ├── research_plan.tex
    │   └── bibliography.bib
    └── /word
        ├── specific_aims.docx
        ├── research_plan.docx
        └── letters_of_support.docx

## Reference Material (`/references`)
- Summarize or cite papers from this directory to support claims
- Prioritize papers in `/preliminary-data` when justifying feasibility
- Use `/methods` papers to support technical approach sections

## Grant Documents (`/grant-documents`)
- LaTeX files are the source of truth; Word versions are for collaborator review
- Maintain consistent terminology across all documents
- Page/word limits to enforce:
  - Specific Aims: 1 page
  - Research Strategy: 12 pages (R01) or [X pages]
  - [Add other section limits here]

## Writing Style & Tone
- Audience: [e.g., NIH study section, mixed MD/PhD reviewers]
- Tone: Confident, precise, and clinically grounded
- Avoid jargon not defined on first use
- Use active voice wherever possible
- Emphasize significance, innovation, and feasibility

## Grant Sections & Priorities
1. **Specific Aims**  hook reviewers; clearly state the gap, hypothesis, and aims
2. **Significance**  establish the problem's importance with cited statistics
3. **Innovation**  differentiate from existing work using `/references`
4. **Approach**  detail methods with fallback/alternative strategies
5. **Letters of Support**  tone should be personalized, not generic

<!-- The **key instructions block** acts as standing rules so you don't have to repeat yourself each session.-->
## Key Instructions for Claude
- When drafting, always ask: which aim does this support?
- Cross-reference `/references` papers before making unsupported claims
- Flag any section approaching its page limit
- Suggest citations from `/references` when strengthening weak claims
- When editing `.tex` files, preserve all existing LaTeX commands and formatting
- When editing `.docx` files, maintain heading styles and section numbering
- Never alter the Specific Aims without explicit instruction  it anchors the whole proposal

<!-- The **reviewer criteria section** keeps Claude aligned with how the proposal will actually be scored.-->
## Reviewer Criteria to Optimize For
- **Significance**: Is the problem important?
- **Investigators**: Is the team qualified?
- **Innovation**: Does it challenge existing paradigms?
- **Approach**: Is the plan rigorous and feasible?
- **Environment**: Are the resources adequate?

<!-- The **terminology table** prevents Claude from paraphrasing or misusing acronyms critical to grant reviewers.-->
## Terminology & Acronyms
| Term | Definition |
|------|------------|
| EDRN | Early Detection Research Network |
| PCDC | [Define here] |
| CPDPC | [Define here] |
| [Add more] | |

## Collaborating Institutions
- Mayo Clinic (PCDC site)  [PI name, role]
- Cedars Sinai (CPDPC site)  [PI name, role]
- [Other institutions]  [roles]

## Notes & Constraints
- Do not change Aim numbering without confirming with PI
- All statistical claims must trace back to a paper in `/references`
- Preliminary data figures are finalized  do not suggest redesigning them
