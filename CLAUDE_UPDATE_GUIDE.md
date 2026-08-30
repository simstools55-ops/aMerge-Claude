# Claude Update Guide

## Target
aMerge Claude 1.1.0-RC1

1. Claude Project内の旧Mergeファイルを削除する。
2. `Claude-Upload/`の中身をすべてアップロードする。
3. Project Instructionsとして`CLAUDE_PROJECT_INSTRUCTIONS.md`を確認する。
4. Identity確認でPackage=1.1.0-RC1, Shared=3.3.0を確認する。
5. Acceptance TestではMERGE_REQUIRED案件に対し、Writer Referralではなく`merged_article`と完成原稿が出ることを確認する。
