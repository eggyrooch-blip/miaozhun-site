---
slug: r1121-privacy-android-protection
generated_at: 2026-11-21T11:36:15.887Z
spec_revision: 8fa0d3b4c3ce
surfaces: [api]
scenarios:
  - id: 1
    surface: api
    action: |
      curl 线上 URL → 200 且含关键句
    observed: |
      pre-ship: 本地文件含 人物保护/手动补遮/系统云备份 各1处，线上旧版 curl 200 但 人物保护=0（符合预期，新内容未发布）。
    rationale: GitHub Pages 内容只有 ship 后才变；上线后的 200 + 关键句 curl 读回在 REPORT.md 记录。
    verdict: inconclusive
---

# Simulation trace — r1121-privacy-android-protection

Agent: for each scenario set a `verdict` (pass / fail / inconclusive) plus ONE
piece of evidence — either a `ftask simulate <slug> --capture <id> -- <cmd>` run
(ftask records exit/stdout you can't fabricate; preferred) OR paste real output
into `observed` (web: an Interceptor screenshot path). expected/rationale are
optional context. A `--capture` wrapping a deterministic test suite is NOT
re-run — it records a reference to the TEST gate (add --force-capture if you
really need the frame). Save large artifacts (screenshots, network logs) to
`/Users/eggyrooch/code/miaozhun-site/.ftask/r1121-privacy-android-protection/sim_artifacts/`.

Verdict legend:
- `pass` — observed matches expected.
- `fail` — observed contradicts expected. **Blocks ship.**
- `inconclusive` — agent couldn't fully verify (missing env / external dep);
  rationale MUST explain why. Allowed through ship.
