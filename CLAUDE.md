# Side Letter Tracker

Side letter tracker for Harrow Ridge Infrastructure Fund I. The app is one file, `index.html`, published as the claude.ai artifact https://claude.ai/artifact/T1bDURhU4xaSCnNvsfZpt1.

Start every session by reading `docs/HANDOFF.md`: it links the test copy, the user guide and the audit, and lists what to fix next and the rules for working on the trackers.

## Keep the user guide current

Every change that alters what a user sees or does (a button name, a step, a screen, a limit) gets a matching edit to the user guide, https://claude.ai/artifact/63d1xbTY7a1yV2KfHFuNJj, in the same piece of work. Check button names against `index.html` rather than writing them from memory. Remove a warning from the guide's "Limits and good habits" section when the bug behind it is fixed. Tell the user which guide sections changed.

## Agent skills

### Issue tracker

GitHub Issues on Kimber217/side-letter-tracker, through the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

The seven default labels: bug, enhancement, needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `GLOSSARY.md` at the root, and ADRs in `docs/adr/` once the first one is written. See `docs/agents/domain.md`.

### External peers

`auto`: picks the hardened Claude or Codex adapter from host metadata, with default models and high effort. See `docs/agents/cross-model.json`.
