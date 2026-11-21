---
recorded_at: 2026-11-21T11:36:01.828Z
by: gemini/gemini-4-neon-high
writer: claude
requested_model: gemini-4-neon-high
dispatch_ms: 144685
verdict: concerns
mode: full
finding_ids: privacy-android.html:person-protection:cloud-backup-contradiction#p1
simulation_verdict: n/a
direction_verdict: aligned
spec_hash: 8fa0d3b4c3ce
code_patch_id: 03994b6d2b84c6de25ae1b18d32fa98ecc03c89db1f801a277078682ab78560c
code_diff_hash: b584194fb199c75410cab9e182fd8bb9c95f07227d0c51f647d351335882aec3
head_sha: 7a4204f61cdb0ba344fa89be758fd0f42209763f
review_snapshot: 7a4204f61cdb0ba344fa89be758fd0f42209763f
confusion: |
  Whether Android main 93f7aa8 actually provides in-app deletion of individual projects: L25/L50 state that Person Protection and manual cover box data are "随项目一起删除" / "deleted with the project", whereas L33/L52 ("保留与删除" / "Retention and deletion") only describe clearing app data in system settings or uninstalling the app (unlike privacy.html L30 for iOS, which explicitly mentions deleting projects on the project page). Without access to the Android codebase, I could not verify which phrasing matches the Android UI, so I did not raise that discrepancy as a confirmed finding.
assumptions: |
  1. The Android repository (main 93f7aa8) is outside this worktree and could not be inspected; therefore all claims about the Android app's manifest and code (no INTERNET permission, allowBackup enabled, local person segmentation with no face recognition/templates, Person Protection modes/scopes/strength, manual cover box fields, Movies/Miaozhun output path, and absence of third-party SDKs) are accepted unverified.
  2. The newly added root .gitignore (8 lines ignoring .ftask runtime artifacts) is assumed to be intentional ftask harness scaffolding rather than out-of-scope drift, even though the SPEC scopes this task to single-file privacy-android.html.
  3. Live deployment routing (/privacy-android and /privacy-android.html returning HTTP 200) is not testable prior to ship and is assumed to be verified post-ship as noted in the SPEC plan.
notes: |
  [qa=thin] Finding: privacy-android.html:person-protection:cloud-backup-contradiction#p1
  - Problem: The diff introduces a direct factual self-contradiction between the new Person Protection copy and the new Android System Cloud Backup disclosure (and leaves Retention & Deletion inconsistent with the cloud backup disclosure). In privacy-android.html L25 (ZH) and L50 (EN), the page states that Person Protection settings and manual cover boxes are stored in project files in the app's private storage and unconditionally claims "它们不会离开你的手机" / "and never leave your phone". Immediately afterward in L30 (ZH) and L51 (EN), the page discloses that if Android system cloud backup is enabled, the system may back up app data including project files ("Android 系统云备份（如果你在手机上开启了该功能，系统可能备份 App 数据，包括项目文件）"). Likewise, L33 states "卸载 App 会删除全部项目数据" without qualifying that uninstalling only removes local device data and does not delete existing Android system cloud backups.
  - Root cause: The diff added the allowBackup / Android system cloud backup caveat in Saving and sharing (L30/L51), but drafted the Person Protection item (L25/L50) as if project files never leave the device under any circumstance, and did not reconcile the deletion statement in Retention and deletion (L33/L52). Because SPEC states allowBackup is not disabled and Done requires every sentence to match Android main 93f7aa8's manifest and code, the unconditional "never leave your phone" claim is inaccurate and risks Google Play privacy review / user-trust issues.
  - Concrete fix:
    1. In privacy-android.html L25, replace "它们不会离开你的手机。" with "本 App 不会将其上传或发送给任何服务器或第三方（系统云备份情况见下文「保存与分享」）。"
    2. In privacy-android.html L50, replace ", and never leave your phone." with ", and are never uploaded or sent by the app (see Saving and sharing regarding Android system cloud backup)."
    3. In privacy-android.html L33, qualify "卸载 App 会删除全部项目数据；" as "卸载 App 会删除设备本地的全部项目数据；" and include Android system cloud backup in the external-deletion sentence (e.g., "已保存到系统相册、已分享的视频，或已由 Android 系统云备份的数据，需要在相册、对应服务或系统/Google 备份设置中管理或删除。"), and apply the matching clarification in L52 ("Videos already saved to the gallery or shared, as well as any data backed up by Android system cloud backup, must be managed or deleted there.").

  Evidence audit:
  - SIM: n/a — pure static HTML copy edit with no executable code or simulation harness.
  - QA: thin — QA_EVIDENCE is hand-written/unverified with no recorded URL, only greps 3 Chinese strings + email on the local file (omitting nav-link regression check, English section check, and Android 93f7aa8 manifest/code verification evidence), and records only the pre-ship baseline curl (0 matches) while deferring post-ship HTTP 200 + content verification to REPORT.md.
  repro privacy-android.html:person-protection:cloud-backup-contradiction#p1 (steps): Open privacy-android.html (served at /privacy-android.html) as a user or Google Play reviewer on an Android device with Android System Cloud Backup enabled (the default behavior when android:allowBackup is not disabled). Compare L25/L50 with L30/L51 and L33/L52. Observed: L25 ('保存在 App 私有目录的项目文件中，随项目一起删除；它们不会离开你的手机') and L50 ('stored in the project in the app's private storage, are deleted with the project, and never leave your phone') unconditionally state that project-stored Person Protection and manual cover box data never leaves the phone, and L33 states '卸载 App 会删除全部项目数据', directly contradicting L30/L51 which state that Android system cloud backup may back up app data including project files. Expected: L25/L50 should state that the app itself never uploads or transmits these files (cross-referencing Android system cloud backup in Saving and sharing), and L33/L52 should clarify that uninstalling removes local device data while any Android system cloud backup must be managed in system/Google backup settings.
---
