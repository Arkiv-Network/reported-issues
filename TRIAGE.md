# Triage — Reported Issues

Internal flow for maintainers handling reports filed in this repo. Reporter-facing summary lives in the [README](./README.md).

## The shape of the problem

`reported-issues` is the **front door** — a single public queue so users don't have to know which Arkiv repo their bug actually belongs in. The **fix** almost always lives in a different repo (`arkiv-sdk-js`, `arkiv-node`, `arkiv-starlight-docs`, `arkiv-website`, etc.).

We want both:
- The reporter to follow status in one place — the issue they filed.
- Engineering to track the work where the code is.

The pattern below gives us both without duplicating effort.

## Default flow: parent + sub-issue

For any report that needs a code change:

1. **Triage in `reported-issues`.** Confirm it's real, reproduce if you can, identify the target repo.
2. **Open the implementation issue in the target repo.** Sharper title if needed, technical detail in the body. Reference the parent with a line like:
   > Reported in Arkiv-Network/reported-issues#N.
3. **Link as a sub-issue.** On the `reported-issues` ticket, use **Add sub-issue → Add existing issue** and paste the URL of the implementation issue. GitHub sub-issues work cross-repo and surface the relationship in both UIs.
4. **Label the parent** `routed` so triage state is visible on the board without reading comments.
5. **PR closes the sub-issue.** In the implementation repo, the PR uses `Closes Arkiv-Network/<repo>#M`. The parent stays open.
6. **Close the parent once shipped.** When the fix has been released (not just merged), close the `reported-issues` ticket with a one-line comment:
   > Fixed in <PR link>, shipped in <version or date>.

   That comment is the changelog the reporter sees.

## When to deviate

**Transfer the issue** (`gh issue transfer Arkiv-Network/reported-issues <number> Arkiv-Network/<target-repo>`) — only when the report was clearly mis-filed and there's no value in a public reporter-facing tracker. Rare. Examples: an internal infra note, a security report that slipped past the advisory channel (handle privately, then transfer the public stub).

**Close as duplicate** — if it's a dup of an existing `reported-issues` ticket. Add `duplicate` label, link the original, close. Don't open a sub-issue.

**Close without routing** — known limitation, working as intended, or out of scope. Leave a short explanation. No sub-issue needed.

## Decision tree

```
Is it a real, actionable report?
├── No → close with explanation (or ask for more info first)
└── Yes
    ├── Already reported here? → close as duplicate, link original
    ├── Mis-filed, no public tracker value? → transfer to target repo
    └── Needs a code change → DEFAULT FLOW (parent + sub-issue + `routed` label)
```

## Labels we use for routing

- `routed` — implementation issue exists in a target repo; parent stays open as tracker.
- `duplicate` — closed in favour of an existing reported issue.
- `needs-info` — awaiting reporter response; auto-close after extended silence.
- `wontfix` / `known-limitation` — closed with explanation, no implementation work.

(Add others as needed; keep the set small.)

## Why this pattern

- **One watcher, one notification stream** for the reporter.
- **Native GitHub relationship** — sub-issues are first-class, not buried in comments, and the link survives repo reorgs.
- **No transfer surprises** — transferring breaks the reporter's URL and removes the public tracker. We avoid it unless the report doesn't belong in this repo at all.
- **Changelog falls out for free** — the closing comment on the parent is the user-facing release note for that report.

## Quick commands

```bash
# Switch to the right gh account before anything else
gh auth switch -u marcos-golem

# Open the implementation issue in the target repo
gh issue create --repo Arkiv-Network/<target-repo> \
  --title "<sharp technical title>" \
  --body "Reported in Arkiv-Network/reported-issues#<N>.\n\n<details>"

# Then link it as a sub-issue via the GitHub UI on the parent issue.
# (gh CLI doesn't yet have a first-class sub-issue subcommand; the GraphQL
# `addSubIssue` mutation works if you want to script it.)

# Label the parent
gh issue edit <N> --repo Arkiv-Network/reported-issues --add-label routed

# When shipped, close the parent with the release note
gh issue close <N> --repo Arkiv-Network/reported-issues \
  --comment "Fixed in <PR link>, shipped in <version/date>."
```
