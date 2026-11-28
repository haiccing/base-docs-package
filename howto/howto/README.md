# howto

A how-to made runnable: its page and, beside it, its script, each line as typed after haicc with what it answers.

Pattern: howto

A how-to is a folder of its package's `howto/`, `<name>/`: its page,
`README.md`, what it does and why, and its script, `steps.haicc`, what
a run runs. The page's `## Steps` is filled from the script at info
extraction: what a reader sees is what is run. Its key is
`<org>/<package>/<name>`; the runner, `howto/run`, runs it where it is
installed (`base-package-howto`).

## Making it

In development, where the packages are built (`howto/`, "Written where"):

```sh
# the page: what it does, why; ## Steps a line pointing at the script
$EDITOR haiccing/<pkg>/howto/<name>/README.md
# the script: # step: <title> blocks, each line as typed after haicc,
# # expect: <fragment> under a line; # scene: first, what the steps need
$EDITOR haiccing/<pkg>/howto/<name>/steps.haicc
# its form, as the runner reads it: the code check
tools/bare tools/code-check.js
# in the sources, then run where it is installed (the steps below)
tools/bare tools/release.js
```

## Steps

The script, [steps.haicc](steps.haicc): each line as typed after `haicc`, what it answers under it; run with `howto/run`, shown here at info extraction.

## Notes

- **The form**, a line a command: `# step: <title>` opens a step; a
  line its position first (`.`, `host`, `host/peer-1`), then the
  command; `# expect: <fragment>` under it, in its answer (its output
  as `haicc --output` prints it, or `error: <message>`); `# scene:
  <title>`, once, before the steps; `# needs: docker` (or `network`),
  first. Other comments are the page's.
- **An expect that checks something**: a fragment of what the line is
  for (`"state":"started"`, `"deployed":"host"`), not one any answer
  holds. A line meant to fail says so, `# expect: error: <fragment>`.
- **Forward only**: `.` is where the runner is, the scene; a line
  reaches what is below it. A line of the terminal's own (`--raw`,
  `haicc output`, the boot itself) is none: such a how-to stays an `sh`
  procedure, and its page says so (no `steps.haicc`).
