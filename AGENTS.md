# Alan’s Videowright fork

Work on main. `origin` is approveplz/videowright and `upstream` is
scosman/videowright. Preserve upstream attribution and the existing local fixes.
Do not reset to upstream or publish personal lesson assets as part of a library
change. Explicitly select changed files when committing.

For lesson work, use the shared **videowright** skill and read
`docs/lesson-workflow.md`, `explainers/README.md`, and the lesson’s PLAN.md.
The shared skill owns teaching choices; packages/lib/skill supplies API details.
Use Claude for the teaching review. Existing briefs and authorization carry
forward. Ask only about consequential missing learning goals or background.

Keep lesson code in explainers. Change the library only for a demonstrated
shared requirement. Inspect current callers and local patterns first. Prefer a
small draft or representative scene before narration and full export. Record
measured resource use and distinguish tool estimates from billed cost.
