# Claude Update Guide

## Target
aMerge Claude 1.1.2

1. Claude Project内の旧aMergeファイルを削除する。
2. `Claude-Upload/`の中身を、同梱の投入対象一覧・手順に従ってアップロードする。
3. Project Instructionsとして`CLAUDE_PROJECT_INSTRUCTIONS.md`を設定・確認する。
4. Identity確認でPackage=1.1.2, Shared=3.3.0を確認する。
5. 更新後は新しいチャットを開始する。
6. Acceptance TestではMERGE_REQUIRED案件に対し、aWriter Referralではなく`merged_article`と完成原稿が出ることを確認する。

## Important
- 旧版と新版のProject Knowledgeを混在させないでください。
- 更新途中の案件は、結果をSIMS Managerへ返して区切ってから更新してください。
- Shared baselineは3.3.0です。
