# Job skill tag audit

## Check and scope
I treated a skill named as a requirement, “must,” or routine daily-use item as required. Skills marked “plus,” “bonus,” or “nice to have” are optional: a matching model tag is correct, but omission is not counted as a miss. Generic “good communication” boilerplate is not a skill requirement. I normalized clear synonyms to the provided vocabulary (Node→Node.js, JS→JavaScript, Excel→Microsoft Excel, Postgres→PostgreSQL, ML→Machine Learning, and US/UK “Modeling/Modelling”). Tags outside the vocabulary or unsupported by the description are wrong. Repeated predictions are counted once as right and then as duplicate/wrong.

The reference labels are rule-based, human-reviewable judgments extracted from the supplied descriptions. This audit covers all 50 rows; it is not a sample. The rubric is conservative: generic “APIs” language alone does not imply REST APIs.

## Results (n=50)
- Predicted tags: **200**; judged right: **170** (85.0%); wrong: **30** (15.0%).
- Required skill mentions in the reference: **179**; missed required skills: **27** (15.1%).
- Descriptions with no wrong or missed-required labels: **14/50** (28.0%).

“Right-tag rate” uses predicted tags as the denominator. “Miss rate” uses required skill mentions as the denominator. Optional skills are excluded from the miss denominator. Full per-description judgments and expected skills are in `labels.csv`.

## Three failure patterns
1. **Unsupported extras / cross-role contamination.** Irrelevant labels can falsely route students to roles: e.g. JD001 adds Teamwork, JD004 adds SAP, and JD025 adds Leadership and Kubernetes without support in the description.
2. **Vocabulary drift and alias handling.** Some outputs use an unapproved or truncated name: JD023 emits “API” and generic “Communication” instead of the supported canonical labels, while JD045 emits “Social Media” and omits the full Social Media Marketing skill. Clear listed aliases were normalized; these labels do not have an approved mapping.
3. **Required-skill omissions.** Required items are sometimes absent even when the description names them: JD010 omits HR Operations and Interviewing, JD046 omits Design Systems and Figma, and JD049 omits Customer Support and Microsoft Excel. See `labels.csv` for all omitted skills per ID.

## First fix
Constrain model output to the supplied skill vocabulary, with a canonicalization layer for approved aliases, then require evidence spans for each emitted tag. For omissions, ask the model to check every “required/must/use every day” phrase against the final tags while keeping optional phrases separate. Evaluate the change on these 50 labeled descriptions and a held-out set: compare wrong-tag rate and required-skill miss rate, inspect each changed prediction, and ensure optional mentions do not inflate the miss score.

## Reproducibility
`audit.ipynb` performs extraction, alias normalization, scoring, and exports `labels.csv`. The supplied CSVs are included so the folder can be run independently.

## Tool use
AI assistance was used to draft the notebook code, rule-based labeling workflow, summary, and PDF. The final labels are generated from the stated rules and the supplied descriptions; they are an auditable assessment, not independently established ground truth.
