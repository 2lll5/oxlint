# Agent Instructions

## Overview

- This repository is home to the shareable Oxlint config.
- The config is split into multiple theme-based packages located under `packages/*`.
- This project is public and open source.

## Shorthand Commands

- Shorthand commands are high-level task macros that define complete, self-contained procedures.
- Always execute shorthand commands exactly as defined below.

### Dependencies

- Review all `package.json` files in the repository for missing, redundant, or misassigned dependencies.
    - Include `pnpm-workspace.yaml` in this review.
    - Report any installed `@types/*` packages that are not utilized.
    - Ensure all installed `@types/*` packages are always referenced in `compilerOptions.types` in the corresponding `tsconfig.json`.
- Ensure all `catalog:` dependencies are referenced by more than one package.
    - Account for `overrides` in `pnpm-workspace.yaml`.
    - Ensure public packages do not rely on `catalog:` dependencies for runtime packages.
- Perform this task without making edits.

### Inventory

- For all core `plugins` used in each config, ensure every supported Oxlint rule is explicitly configured (enabled or disabled).
    - List each missing rule on a separate line in a code block.
    - Exclude `nursery` rules from this audit.
    - For additional context, fetch the release notes from the provided URL. If no URL is provided, attempt to fetch the release notes for the installed Oxlint version from `https://github.com/oxc-project/oxc/releases`.
- Ensure each base config explicitly configures every core rule referenced by override configs within the same config package.
- Perform this task without making edits.

### Review

- Review the commit matching the provided hash.
    - If no hash is given, review the most recent commit on the current branch.
- Report any regressions the changes may introduce.
- Report any cases where new code reimplements behavior already available in the language, standard library, or existing shared utilities in this repository.
- Ensure all changes align with the latest version of `AGENTS.md`.
- Perform this task without making edits.

### Verify

- Re-read `AGENTS.md` and all reported files to confirm whether reported issues remain relevant.
    - Ensure that all findings align with the latest version of `AGENTS.md`.
- Mark resolved issues as addressed and exclude them from future reports.
- Highlight any issues that persist after the latest edits.

## Google Drive Build 交付規範（所有 Agent 必須遵守）
- 所有 Build 的正式目的地：Google Drive `AI Project/oxlint/`；資料夾名稱必須與 GitHub Repo 名稱一致（AI Project ID `1Yhfro6Ss5TSCXCVIZIHEu5h7V1gL8b27`）。不可將壓縮檔散放於 `AI Project/` 根目錄，也不可每次 Build 新建頂層版本資料夾。
- **最新版直接放專案資料夾根目錄**，但需確認完整且經實際測試：ZIP／EXE、SHA-256、完整分卷與必要安裝／還原腳本一併提供；多平台最新版可並存。上傳後讀回 parent／檔名／大小／checksum，缺 ZIP 或分片的不完整新版本不能覆蓋舊的完整版本。
- **只有重大功能、架構、相容性或美術改版才在專案內建立 `vX.Y.Z-說明/`**。一般舊版移入 `歷史封存/`，保留檔案不可直接刪除。
- 新功能與修正必須提交 GitHub。昂貴 Actions 建置以 `workflow_dispatch` 或 `release: published` 受控觸發，避免每次 push main 就 Build。完成時回報 Drive 專案資料夾、版本、檔案、校驗與測試情形。
**For Codex:** Latest complete tested builds at `AI Project/oxlint/`; archive routine old builds under `歷史封存/`; separate version folders only for significant milestones, never partial uploads.
