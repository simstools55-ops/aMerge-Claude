# aMerge v2.0.2 — 06_MERGE_VALIDATION.md

以下のSOURCE見出しは元資料の識別名です。ファイルシステム上のパスではありません。


---
## SOURCE: validation/MERGE_VALIDATION.md

# Merge Validation

Identity / Evidence / Decision / Preservation / Safety / Rollbackを検証します。

## RC3 Publication Quality Validation

MERGE_REQUIREDでは以下を追加検証する。

- `publication_assessment.status`が存在する。
- `HOLD_FOR_VERIFICATION`なのに`publication_ready=true`になっていない。
- `verification_required`に重要項目がある場合、公開可能と断定していない。
- 完成原稿に根拠のない保証表現（例：「必ず解決」）を残さない。
- Fact Checkできなかった事実を「確認済み」と偽らない。


---
## SOURCE: validation/RC3_PUBLICATION_QUALITY_ACCEPTANCE.md

# RC3 Publication Quality Acceptance

MERGE_REQUIREDの最終回答で次を検査する。

1. 完成原稿全文がcontent_markdownに入っている。
2. 統合で追加・再構成したfact claimを確認した。
3. 根拠のない「必ず」「絶対」「確実」等を残していない。
4. publication_assessment.statusが存在する。
5. verification_requiredが残る場合はHOLD_FOR_VERIFICATIONかつpublication_ready=false。
6. PUBLIC_OK_WITH_FIXESなら修正済み本文をcontent_markdownへ反映済み。
7. Writer Referralで逃げない。


---
## SOURCE: validation/SAFETY_VALIDATION.md

# Safety Validation

自動削除・自動Redirect・自動noindexは禁止。Primary公開前に吸収記事を変更しません。



## RC2 Machine Result Gate（プロジェクト指示との整合）
- `MERGE_REQUIRED` の `payload.merged_article.content_markdown` には完成原稿全文を入れる。
- 「上記参照」「省略」等の参照文字列のみではSUCCESSを返さない。
- `payload.publication_assessment.status` が `HOLD_FOR_VERIFICATION` の場合は `payload.merged_article.publication_ready=false` とする。
- 公開判定は原稿の準備状況であり、Redirect/noindex/deleteの自動実行を意味しない。

## v2.0.4 閲覧スタイルの非干渉・公開完全性ゲート
- 閲覧スタイルは**文章表現のみ**に適用する。統合対象、採用/不採用の事実、根拠評価、SEO方針、Query Mapping、Preservation Map、見出しの意味、内部リンク、表の数値・採否、保護対象はスタイルに依存させない。
- スタイルを適用する前に「内容決定台帳」（採用・除外・保留と各根拠）を確定し、両スタイルで同一台帳を使う。根拠不足の推奨頻度や数値を、スタイルを理由に復活させない。スタイル別出力を比較するとき、内容差異があれば合格にしない。
- 根拠不足の定期実施推奨（例：Teamsキャッシュ削除を週1回、月1回など）は、一次情報または依頼Evidenceで裏付けられない限り本文に入れない。既存の根拠不足情報も無批判に移植しない。
- `<!-- PROTECTED -->` など保護対象の位置だけを示すマーカーは、元HTMLそのものではない。マーカーが本文に残る、保護リンクURLが欠落する、必要な元HTMLが復元できない場合は `publication_ready=false` とし、`publication_assessment.status=HOLD_FOR_VERIFICATION`、不足素材を明示する。実際のHTMLが完全に保持されている場合のみ公開可能と判定できる。
- `PUBLIC_OK_WITH_FIXES` は修正が**完成本文へ反映済み**のときだけ使う。ユーザーによるHTML復元など必須作業が残る場合は公開可能としない。
- 原稿と結果JSONの `content_markdown` の完全一致、JSONの構文、ID/契約名、スタイル値、保護要素、未検証claim、公開判定の整合を返却前に点検する。
