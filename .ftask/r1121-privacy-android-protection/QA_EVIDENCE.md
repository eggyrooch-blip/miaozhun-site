# QA_EVIDENCE

## 1 (pre-ship, local file)
- action: grep -c 人物保护 privacy-android.html; grep -c 手动补遮; grep -c 'Android 系统云备份'; grep -c eggyrooch@gmail.com
- expected: each ≥1
- actual: 1 / 1 / 1 / 3
## 2 (live, before ship)
- action: curl live page grep 人物保护
- expected: 0 (old version live)
- actual: 0
- post-ship live curl is recorded in REPORT.md
