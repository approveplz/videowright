# Technical lesson workflow

The deliverable is a useful mental model. Visual polish helps the viewer follow
that model. Choose the learner’s goal before choosing an animation style.

## Brief and storyboard

The shared **videowright** skill owns questions to the user. For a developer who
wants general understanding, prioritize the mechanism and a transferable lesson.
A request to operate a deployment needs more operational detail.

Write a compact storyboard with the learning goal, running example, and each
beat’s question, narration, visible state, and causal change. Define unfamiliar
terms when they first matter. Preserve the same objects and names through setup,
failure, and correction. A picture should explain something the narration alone
would make harder to follow. Put peripheral facts in source notes.

Before speech generation, have Claude review the storyboard and a small selection
of representative images. Ask for concrete misunderstandings, omissions, and cuts.
Fix substantive findings. This is an internal teaching review, not an automatic
extra approval gate for the user. Preserve unresolved scientific or factual
uncertainty instead of converting a reviewer's confidence into evidence.

## Bounded Claude review on Dev Mac

Use the saved Claude subscription. Check `claude auth status` when authentication
is uncertain. Do not use `--bare`: current CLI help says it skips OAuth. Read
current help if these options change. The following leaves only file reading
available and excludes unrelated hooks, skills, connectors, and browser sessions.

Create a short request file naming only the brief, storyboard, and representative
frames. Bound the desired answer length and tell Claude whether it is reviewing
stills, a script, or continuous playback. Avoid sending both a source JSON file
and an identical script. Do not load an entire repository or conversation history
for a standalone editorial question.

```sh
mkdir -p .local/review
/usr/bin/time -l env -u ANTHROPIC_API_KEY -u ANTHROPIC_AUTH_TOKEN \
  -u ANTHROPIC_BASE_URL -u CLAUDE_CODE_USE_BEDROCK \
  -u CLAUDE_CODE_USE_VERTEX -u CLAUDE_CODE_USE_FOUNDRY -u CLAUDECODE \
  claude -p --safe-mode --effort medium --tools Read --allowedTools Read \
  --strict-mcp-config --mcp-config '{"mcpServers":{}}' --output-format json \
  < .local/review/request.txt > .local/review/result.json \
  2> .local/review/resources.txt
```

The JSON retains the session ID, answer, elapsed time, turns, token/cache usage,
and reported list-price equivalent. Subscription usage is not a separate charge
merely because the CLI reports `total_cost_usd`. Report unknown billing as unknown.
Use the returned session ID with `--resume` only for a closely related follow-up.
Do not repeatedly send the same artifacts. Keep the tool set stable for related
review follow-ups to preserve cached context. Start implementation from the
reviewed storyboard and concise findings, rather than carrying all review images
and history into a different tool set. Explicitly assign file ownership. Keep
review-only runs read-only. On resumed sessions, modelUsage and total_cost_usd
can be cumulative while usage describes the current invocation. Do not sum
cumulative totals.

## Prototype, narration, and export

Prototype the hardest mechanism first. A persistent data structure, pointer,
queue, request lane, or ownership boundary is often more useful than another
slide. Motion should show order, movement, lifetime, or a change in state.
Use a short prediction question and show its answer on the same model.

Use the existing shared hand-drawn Canvas skill for illustrated cutaways, and
Videowright segments for the composed lesson. Its direct Canvas export avoids
browser screenshots and draws at 12 frames per second, outputting 24. Read its
actual API and use its renderer rather than creating another rendering framework.
Text and essential diagram shapes must remain legible on a phone.

Generate narration after the teaching review. Reuse unchanged clips and timing.
Render draft frames before full export. Do not freeze frames while a diagram is
still changing. A static-frame optimization is valid only after proving the
animation has settled. Keep original narration and timing separate from artwork.

For the final export, inspect actual frames, transitions and narrated playback.
Verify audio, duration, decoding, subtitles, chapter navigation, and the published
link. Record wall time and peak memory for costly steps. State the machine,
resolution, duration, and method before comparing render performance. A successful
encode does not prove teaching quality, and a storyboard review does not prove
playback quality.
