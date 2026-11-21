# QA_EVIDENCE

## 1 (pre-ship, local file)
- action: grep -c 人物保护 privacy-android.html; grep -c 手动补遮; grep -c 'Android 系统云备份'; grep -c eggyrooch@gmail.com
- expected: each ≥1
- actual: 1 / 1 / 1 / 3  (re-run after fix below)
## 2 (live, before ship)
- action: curl live page grep 人物保护
- expected: 0 (old version live)
- actual: 0
- post-ship live curl is recorded in REPORT.md
## 3 (after review fix, local)
- action: grep nav links + EN section + deletion wording in privacy-android.html
- actual: nav links=href="privacy-android.html" href="privacy.html" href="support.html" href="terms.html"  | EN section=1 | 随项目一起删除 residual=0
- Android facts verified against git 93f7aa8 source (see REPORT.md): INTERNET removed in manifest, PickVisualMedia, MediaStore Movies/Miaozhun, no face detector, allowBackup unset, no in-app project delete UI
