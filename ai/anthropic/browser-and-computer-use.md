# Browser Use and Computer Use

Date added: 2026-05-01
Source: Anthropic course notes / Gabe learning backlog
Status: try in future

## Why this matters
These are practical AI workflow capabilities worth testing later because they may reduce manual research and app-hopping friction.

## Browser use
Claude in Chrome can:
- navigate websites
- interact with pages
- pull findings directly into the task it is working on

Useful examples:
- check competitor pricing across many websites
- gather data from pages that do not have an API
- compare product pages, documentation, pricing, changelogs, reviews, or market pages

Potential Gabe use cases:
- competitor research for niche app ideas
- App Store / website comparison research
- pricing-page audits
- documentation gathering for app architecture decisions
- market research where APIs are not available

## Computer use
When Claude does not have a connector or plugin, it can navigate the computer directly:
- click
- type
- open apps
- interact with UI like a human would

Claude priority order:
1. connectors first
2. Chrome/browser use
3. direct screen/computer interaction

The idea is to pick the fastest, most reliable, least fragile method first.

Safety/permissions notes:
- Permission prompt appears before Claude accesses each app.
- Blocklists can keep sensitive apps/sites off-limits.
- Computer use is research preview on Pro/Max plans.
- macOS only for now; Windows planned later.

## Things to test later
- Can browser use reliably gather competitor pricing for app ideas?
- Can it compare App Store/web copy across competitors without hallucinating?
- Can it collect structured data from non-API pages into a table?
- Can computer use safely handle repetitive UI tasks that lack CLI/API access?
- Where does it fail compared with direct connectors/API/CLI automation?

## Eval criteria
When trying these, score:
- accuracy of gathered info
- citation/source quality
- time saved
- friction/permission overhead
- risk/privacy comfort
- whether it beats existing CLI/API workflows

## Rule of thumb
Use direct APIs/connectors/CLI tools when available. Use browser use for web pages without APIs. Use computer use only when no reliable connector/browser/API route exists.
