# Arkiv — Reported Issues

This is the public queue for reporting issues, bugs, and ideas about [Arkiv](https://arkiv.network) — the Web3 database, powered by $GLM.

If you've hit a bug, run into unexpected behaviour, or have an idea you'd like the team to consider, this is the place.

## Reporting an issue

1. Head to **[New issue](https://github.com/Arkiv-Network/reported-issues/issues/new/choose)**.
2. Pick the form that matches what you want to report:
   - **Bug or network issue** — something is broken or behaving unexpectedly.
   - **Feature request or idea** — you'd like Arkiv to do something it doesn't yet.
3. Fill in the form. The more detail you give us up front, the faster we can help.

Before reporting, please:
- Check the [documentation](https://docs.arkiv.network) — your question may already be answered there.
- Search [existing issues](https://github.com/Arkiv-Network/reported-issues/issues?q=is%3Aissue) so we don't duplicate work.
- For general questions or quick chats, drop into the [Arkiv Discord](https://discord.gg/golem) first.

## What happens next

Every issue lands on the team's triage queue. A maintainer will:
- **Acknowledge** the report and apply the right labels.
- **Ask for more info** if the form didn't capture enough to act on.
- **Decide** whether it's a real bug, a usage question, a known limitation, or a feature we'll consider.
- **Route** the work. Arkiv is built across several repos (SDKs, node, docs, website, infra). When a report needs code changes, we open a linked issue in the right repo and mark this one as the parent. **Your issue here stays open as the public tracker** until the fix ships — so you only have to watch one place.
- **Close with a note** once the fix has landed and been released, linking the PR or release so you can see what changed.

We aim to get to new reports within a few working days. If something is urgent (e.g. the network is down for you), please flag that in the report and we'll prioritise.

> Maintainers: the internal triage flow lives in [`TRIAGE.md`](./TRIAGE.md).

## Security issues

**Do not open a public issue for security vulnerabilities.** Please report them privately through [GitHub Security Advisories](https://github.com/Arkiv-Network/reported-issues/security/advisories/new).

## A note on scope

This repository is for reports about Arkiv itself — the protocol, SDKs, tooling, docs, and website. For issues with applications built **on** Arkiv, please report them to the application's own team in the first instance.

---

_Arkiv is in active development. Honest reports — even rough ones — make the product better. Thanks for taking the time._
