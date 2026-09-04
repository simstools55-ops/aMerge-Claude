# aMerge Claude Deployment Test

Target: Package 1.1.2 / Shared 3.3.0

確認項目:
1. VERSION が 1.1.2 である。
2. SHARED_VERSION が 3.3.0 である。
3. Project Instructions が aMerge 1.1.2 として読み込まれる。
4. MERGE_REQUIRED では aMerge 自身が統合後完成原稿を生成する。
5. `payload.merged_article.content_markdown` に完成原稿全文が格納される。
6. Redirect / noindex / delete を自動実行しない。
7. Publication Assessment が PUBLIC_OK / PUBLIC_OK_WITH_FIXES / HOLD_FOR_VERIFICATION のいずれかになる。
