---
description: Post a Hello World greeting as a GitHub issue
on:
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [repos, issues]
safe-outputs:
  mentions: false
  allowed-github-references: []
  create-issue:
    title-prefix: "Hello World: "
    labels: [hello-world, automated]
    close-older-issues: true
    expires: 7d
model: gpt-4.1-mini
engine:
  id: copilot
  version: latest
---

# Hello World

Post a short **Hello World** greeting for `${{ github.repository }}` as a GitHub issue.

## Task

1. Create a single issue via `create-issue` with:
   - Title starting with the configured prefix (include a short timestamp or run id for uniqueness if helpful)
   - Body that clearly says hello world to this repository
2. Keep the body meaningful (at least a short greeting and context); do not use placeholder-only text.

### Suggested body

```markdown
### Greeting

Hello World from the `hello-world` agentic workflow.

> [!NOTE]
> Triggered via `workflow_dispatch` on `${{ github.repository }}`.
```

## Safe Outputs

- Use `create-issue` for the greeting.
- Call `noop` with a short explanation only if creating the issue is not possible.