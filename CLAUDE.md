# Side Letter Tracker

Side letter tracker for Harrow Ridge Infrastructure Fund I. The app is one file, `index.html`, published as the claude.ai artifact https://claude.ai/artifact/T1bDURhU4xaSCnNvsfZpt1.

## Agent skills

### Issue tracker

GitHub Issues on Kimber217/side-letter-tracker, through the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

The seven default labels: bug, enhancement, needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `GLOSSARY.md` at the root, and ADRs in `docs/adr/` once the first one is written. See `docs/agents/domain.md`.

### External peers

`auto`: picks the hardened Claude or Codex adapter from host metadata, with default models and high effort. See `docs/agents/cross-model.json`.
