# Job Skill Tag Audit

A reproducible audit of 50 fictional job descriptions and their model-generated skill tags.

## Results

- 200 predicted tags: 170 right (85.0%), 30 wrong (15.0%).
- 179 required skill mentions: 27 missed (15.1%).
- 14 of 50 descriptions have no wrong tag or missed required skill.

A tag is right when it is supported as a required or optional skill and maps to the supplied skill vocabulary. Only required skills count as misses. Clear aliases such as `Node` to `Node.js` and `Excel` to `Microsoft Excel` are normalized. See `writeup.md` for the rubric, failure patterns, and proposed fix.

## Files

- `audit.ipynb` - code to extract reference skills, normalize tags, score predictions, and export labels.
- `labels.csv` - per-description expected, right, wrong, and missed skills.
- `job-descriptions-tagged.csv` - supplied dataset.
- `skill-list.csv` - supplied skill vocabulary.
- `writeup.md` - audit method, results, failure analysis, fix, and tool-use note.
- `job_skill_audit_bundle.pdf` - paginated report with the full notebook, labels, vocabulary, and source descriptions.

## Run

Open `audit.ipynb` in Jupyter from this folder. It uses Python with pandas. The notebook writes `labels.csv` in the current folder.

## Tool use

AI assistance was used to draft the notebook code, rule-based labeling workflow, summary, and PDF. The final labels are generated from the stated rules and supplied descriptions; they are an auditable assessment, not independently established ground truth.
