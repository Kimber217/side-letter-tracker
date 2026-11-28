# Issue tracker: GitHub

Issues and specs for this repo live as GitHub issues. Use the `gh` CLI for all operations.

## Conventions

Use `gh api` (GitHub's REST API) for every operation. In Claude Code cloud sessions GitHub's GraphQL API is blocked, so `gh issue create`, `gh issue list`, `gh issue view` and `gh issue edit` fail with "GitHub GraphQL is not available from Claude Code sessions". `{owner}/{repo}` is filled in by `gh` from `git remote -v` when run inside the clone.

- **Create an issue**: `gh api repos/{owner}/{repo}/issues -f title='...' -f body="$(cat body.md)" -f 'labels[]=needs-triage'`. Write multi-line bodies to a file first.
- **Read an issue**: `gh api repos/{owner}/{repo}/issues/<number> --jq '.title, .state, ([.labels[].name] | join(", ")), .body'`, then comments with `gh api repos/{owner}/{repo}/issues/<number>/comments --jq '.[] | "--- \(.user.login): \(.body)"'`.
- **List issues**: `gh api 'repos/{owner}/{repo}/issues?state=open&per_page=100' --paginate --jq '[.[] | select(.pull_request | not) | {number, title, body, labels: [.labels[].name]}]'`. Add `&labels=<name>` to filter.
- **List children**: the open issues whose `## Parent` section names `<number>`, each with its count of open blockers: `gh api 'repos/{owner}/{repo}/issues?state=open&per_page=100' --paginate --jq '.[] | select(.body // "" | test("## Parent\\s+#<number>\\b")) | "\(.number) blocked_by=\(.issue_dependencies_summary.blocked_by) \(.title)"'`, plus any sub-issues (`gh api repos/{owner}/{repo}/issues/<number>/sub_issues --paginate --jq '.[] | select(.state == "open") | "\(.number) blocked_by=\(.issue_dependencies_summary.blocked_by) \(.title)"'`).
- **Comment on an issue**: `gh api repos/{owner}/{repo}/issues/<number>/comments -f body='...'`
- **Apply / remove labels**: `gh api repos/{owner}/{repo}/issues/<number>/labels -f 'labels[]=<name>'` to add; `gh api --method DELETE repos/{owner}/{repo}/issues/<number>/labels/<name>` to remove.
- **Create a missing label**: `gh api repos/{owner}/{repo}/labels -f name='<name>'` (a 422 "already_exists" reply means it is there).
- **Close**: comment first, then `gh api --method PATCH repos/{owner}/{repo}/issues/<number> -f state=closed`.

## Pull requests as a triage surface

**PRs as a request surface: no.** _(Set to `yes` if this repo treats external PRs as feature requests; `/triage` reads this flag.)_

When set to `yes`, PRs run through the same labels and states as issues, using the `gh pr` equivalents:

- **Read a PR**: `gh pr view <number> --json title,state,body,comments --jq '.title, .state, .body, (.comments[] | "--- \(.author.login): \(.body)")'` and `gh pr diff <number>` for the diff.
- **List external PRs for triage**: `gh pr list` has no author association field, so use the REST API: `gh api 'repos/{owner}/{repo}/pulls?state=open' --paginate --jq '[.[] | select(.author_association | IN("CONTRIBUTOR", "FIRST_TIME_CONTRIBUTOR", "NONE")) | {number, title, body, author: .user.login, labels: [.labels[].name]}]'`. This drops `OWNER`/`MEMBER`/`COLLABORATOR`. Read each PR's comments with `gh pr view`.
- **Comment / label / close**: `gh pr comment`, `gh pr close`, and `gh pr edit` with `--add-label` or `--remove-label`.

GitHub shares one number space across issues and PRs, so a bare `#42` may be either: resolve it in one call with `gh api 'repos/{owner}/{repo}/issues/42' --jq 'if .pull_request then "pr" else "issue" end'`, which answers for both kinds.

## When a skill says "publish to the issue tracker"

Create a GitHub issue.

## When a skill says "fetch the issue"

Run the **Read an issue** command above.

## Wayfinding operations

Used by `/wayfinder`; `/to-tickets` uses **Blocking** too. The **map** is a single issue with **child** issues as tickets.

- **Map**: a single issue labelled `wayfinder:map`, holding the Destination / Notes / Decisions so far / Added so far / Not yet specified / Out of scope body. the **Create an issue** call with `-f 'labels[]=wayfinder:map'`.
- **Child ticket**: an issue linked to the map as a GitHub sub-issue (`gh api` on the sub-issues endpoint). Where sub-issues aren't enabled, add the child to a task list in the map body and put `Part of #<map>` at the top of the child body. Labels: `wayfinder:<type>` (`research`/`prototype`/`grilling`/`task`). Once claimed, the ticket is assigned to the driving dev.
- **Blocking**: GitHub's **native issue dependencies**, the canonical, UI-visible representation. Add an edge with `gh api --method POST repos/<owner>/<repo>/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`, where `<blocker-db-id>` is the blocker's numeric **database id** (`gh api repos/<owner>/<repo>/issues/<n> --jq .id`, _not_ the `#number` or `node_id`). GitHub reports `issue_dependencies_summary.blocked_by` (open blockers only, the live gate). Where dependencies aren't available, fall back to a `Blocked by: #<n>, #<n>` line at the top of the child body. A ticket is unblocked when every blocker is closed.
- **Frontier query**: list the map's children with `gh api repos/<owner>/<repo>/issues/<map>/sub_issues --paginate` (or read the map's task list where sub-issues aren't enabled). Keep the open ones (`state == "open"`), drop any with an open blocker (`issue_dependencies_summary.blocked_by > 0`, or an open issue in the `Blocked by` line) or an assignee; first in map order wins.
- **Claim**: `gh api repos/{owner}/{repo}/issues/<n>/assignees -f 'assignees[]=<your login>'`, the session's first write.
- **Resolve**: comment with the answer, then close (see **Comment** and **Close** above), then append a context pointer (gist + link) to the map's Decisions-so-far.
