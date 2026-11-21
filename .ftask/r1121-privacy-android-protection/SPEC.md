# SPEC — r1121-privacy-android-protection
## Done — ONE measurable sentence
- /privacy-android(.html) 返回 200，正文含「人物保护」「手动补遮」「Android 系统云备份」，且每句与安卓 main 93f7aa8 的 manifest（无 INTERNET）和代码一致。
## What sunke wants (plain language)  [Objective]
- Play 上架用的安卓隐私页要和带人物保护的 main 一致，联系方式沿用 iOS 页。（派单 2，2026-11-21 回「做」）
## Out of scope (what we will NOT do)  [Scope]
- 不改 iOS 页、support/terms、不改运营者名（KitCarry vs KE SUN 待 sunke 定）、不动安卓仓。
## 我拍的数 (轮数/超时/并发/范围)
- 单文件 privacy-android.html，纯文案。
## 怎么做 — 根因 / 先红的测试 / 最小改动 / 删掉什么
- 根因: 已发布版本 11-18 写成 1.0.0 无人物保护；main 93f7aa8 已有人物保护/手动补遮，且 allowBackup 未关。
- 先红的测试: curl 线上页 grep「人物保护」→ 0 命中。
- 最小改动: 加人物保护/补遮数据条、云备份说明、更新日期 → 为了 Done。
- 删掉什么: 无
## How will I know it works
### Surface (pick one or more)
- [x] api — curl against real endpoint
### Visual target
- 无
### Acceptance scenarios (user does X → observe Y)
- curl 线上 URL → 200 且含关键句
### Regression guards (what must NOT break)
- 联系邮箱、nav 链接不变
### Targeted tests (repo-relative paths; one per bullet, or `full-suite`)
- full-suite
## Plan (ordered steps; tick progress)
- [x] 改页 - [ ] save/ship - [ ] curl 读回
## Dead ends (approach → why it failed; never retry)
- 无
