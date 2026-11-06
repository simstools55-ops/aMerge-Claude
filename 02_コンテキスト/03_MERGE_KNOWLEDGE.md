# aMerge v2.0.2 — 03_MERGE_KNOWLEDGE.md

以下のSOURCE見出しは元資料の識別名です。ファイルシステム上のパスではありません。


---
## SOURCE: knowledge/CANNIBALIZATION_RULES.md

# Cannibalization Rules

同一語を含むだけではカニバリとしません。Query overlap、Intent overlap、Content overlap、Performance splitを総合評価します。

Confidence: CONFIRMED / LIKELY / POSSIBLE / UNLIKELY / NOT_CANNIBALIZATION


---
## SOURCE: knowledge/MERGE_WRITING_RULES.md

# Merge Writing Rules

## 原則

- Primary Articleを正本として編集する。ゼロから別記事へ作り替えない。
- Absorbed ArticleからはPreservation Mapで指定された固有価値を移植する。
- 同義の説明、重複FAQ、重複表は1つに統合する。
- Primary Articleの既存検索意図を壊さない。
- Query MappingでPrimaryへ集約すると決めた主要クエリを自然にカバーする。

## Preservation

無断削除禁止の例：
- 独自体験・検証
- 実測データ
- 比較表
- 広告・アフィリエイト導線
- 読者に有用な具体例
- Doctor/SBMが明示した保護対象

## 禁止

- Evidenceにない数値・体験・専門資格を創作しない
- blocked_scopeの内容を書き換えない
- Redirect/noindex/deleteを本文編集と同時に実行した扱いにしない
- Merge本文編集をWriterへ丸投げしない

## 完成原稿

原則として部分差分だけでなく、Primary Articleへそのまま反映できる統合後の完成本文を返す。元記事にHTML/広告コード等の保護要素があり、Markdown完全再現で失われる危険がある場合は、保護要素の位置を明示して維持する。


## JSON完全性
Human-readableで完成原稿を書いた場合、その全文を`payload.merged_article.content_markdown`にも格納する。プレースホルダー・参照文・省略記号で代替しない。SBM登録用JSONだけで統合後完成原稿を復元できることを合格条件とする。

## RC3 Publication Quality Gate

統合後完成原稿は、Preservationと重複整理が成功していても、そのまま公開可能とは限らない。最終返却前に以下を検査する。

### 1. Post-Merge Fact Check
- 統合によって新規追加・再構成した設定手順、数値、仕様、制度、料金、ポート番号、バージョン依存情報、製品挙動などは検証対象とする。
- SBM Package内Evidenceで裏付けられる場合はそのEvidenceを優先する。
- Packageだけでは現行性を確認できず、外部確認が必要な場合は可能なら一次情報・公式情報を確認する。
- 外部確認不能・Evidence不足の場合は、未確認事実を断定したまま`PUBLIC_OK`にしない。

### 2. Overclaim Guard
以下のような根拠を超える保証表現を禁止する。
- 「必ず成功する」「必ず解決できる」「必ず原因を特定できる」
- 「絶対に」「確実に」など、Evidenceが保証していない断定

必要なら「解決につながる可能性があります」「原因を切り分けやすくなります」等へ弱める。

### 3. Publication Readiness
完成原稿には次の公開判定を付ける。
- `PUBLIC_OK`：Fact Check済みで、公開阻害事項なし。
- `PUBLIC_OK_WITH_FIXES`：Merge自身が必要修正を完成原稿へ反映済み。修正後は公開可能。
- `HOLD_FOR_VERIFICATION`：重要な事実確認が残り、そのまま公開させてはいけない。

`publication_ready=true`は`PUBLIC_OK`または`PUBLIC_OK_WITH_FIXES`に限る。`HOLD_FOR_VERIFICATION`では必ずfalseとする。


---
## SOURCE: knowledge/PRESERVATION_RULES.md

# Preservation Rules

体験談、比較表、FAQ、画像、広告、アフィリエイトリンク、Winner Query対応部分、被リンク価値を保護します。


---
## SOURCE: knowledge/QUERY_MAPPING_RULES.md

# Query Mapping Rules

各クエリの現在URL、目標URL、処置、理由を記録します。


---
## SOURCE: knowledge/ROLLBACK_RULES.md

# Rollback Rules

統合前全文、メタ情報、URL、リンク、Redirect/noindex設定を保存し、自動Rollbackは行いません。



---
## v2.0.3 Reading Device Style Addendum
## 閲覧環境設定（Reading Device Style）
SBMから渡された `reading_device_style` を統合後完成原稿の文章表現に適用する。参照順は `payload.reading_device_style`、依頼文中の明示された同名設定、サイト設定の順とし、矛盾がある場合は勝手に推定せず確認事項として返す。
- `DESKTOP_FIRST`（バランス型）：自然な文長・段落、論理的な見出し、必要な表・箇条書きを維持する。
- `MOBILE_STORY`（スマホ重視型）：短く読みやすい文と段落、明確な結論先行、スマホで追いやすい箇条書きを用いる。ただし機械的な一文一段落化はしない。
- 未指定または未知の値：既存の統合執筆ルールを維持し、未知値は警告する。サイトや読者層から設定を推定しない。
- 読みやすさは編集上の補助条件であり、Doctor/SBMの統合判断、Primary選定、Query Mapping、allowed_scope/blocked_scope、Preservation Map、広告・内部リンク・体験・数値・表・HTML保護を上書きしない。
- 原文にない事実、体験、実測値を追加しない。統合に不要な段落や保護対象を閲覧スタイルだけを理由に書き換えない。
- Human-readable出力と `payload.merged_article.content_markdown` は完全一致させる。既存のJSON契約名・バージョンは変更しない。
- `payload.reading_device_style` が存在する場合は、結果の `payload.reading_device_style` に同じ値を任意の追加フィールドとして返す。未指定なら追加しない。これを理由に公開判定を緩めない。

## v2.0.4 閲覧スタイルの非干渉・公開完全性ゲート
- 閲覧スタイルは**文章表現のみ**に適用する。統合対象、採用/不採用の事実、根拠評価、SEO方針、Query Mapping、Preservation Map、見出しの意味、内部リンク、表の数値・採否、保護対象はスタイルに依存させない。
- スタイルを適用する前に「内容決定台帳」（採用・除外・保留と各根拠）を確定し、両スタイルで同一台帳を使う。根拠不足の推奨頻度や数値を、スタイルを理由に復活させない。スタイル別出力を比較するとき、内容差異があれば合格にしない。
- 根拠不足の定期実施推奨（例：Teamsキャッシュ削除を週1回、月1回など）は、一次情報または依頼Evidenceで裏付けられない限り本文に入れない。既存の根拠不足情報も無批判に移植しない。
- `<!-- PROTECTED -->` など保護対象の位置だけを示すマーカーは、元HTMLそのものではない。マーカーが本文に残る、保護リンクURLが欠落する、必要な元HTMLが復元できない場合は `publication_ready=false` とし、`publication_assessment.status=HOLD_FOR_VERIFICATION`、不足素材を明示する。実際のHTMLが完全に保持されている場合のみ公開可能と判定できる。
- `PUBLIC_OK_WITH_FIXES` は修正が**完成本文へ反映済み**のときだけ使う。ユーザーによるHTML復元など必須作業が残る場合は公開可能としない。
- 原稿と結果JSONの `content_markdown` の完全一致、JSONの構文、ID/契約名、スタイル値、保護要素、未検証claim、公開判定の整合を返却前に点検する。
