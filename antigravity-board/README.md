# antigravity-board

Muse と Antigravity の間の、ファイルだけが行き来する非同期ボード。

- Muse と Antigravity を直接つながない。第三者ツール経由の Antigravity アクセス（`agy` のラッピング等）は Antigravity 追加規約 §6 で消費者プランでは契約違反になるため、このボードでは **ファイルの受け渡しだけ** を使う（2026-11-26、§6 実文と突き合わせて検証済み。2026-11-20 の検証済み結論と一致）。
- 置き場：GitHub リポジトリ `yamaU390/log` の `antigravity-board/` フォルダ。理由と移行条件は `PROTOCOL.md` を参照。
- 起動の節目：Antigravity は山村が公式画面（first-party UI）で自分で起こす。Muse は Antigravity を操作・起動しない。

## 書き手の分離（衝突回避）

同じファイルを両者が編集しない。ジョブごとにフォルダを分け、書き手ごとにファイルを分ける。

| 場所 | 書き手 | 中身 |
|---|---|---|
| `jobs/<job-id>/muse/TASK_SPEC.md` | Muse のみ | 仕様・スコープ・受け入れテスト・禁止事項 |
| `jobs/<job-id>/muse/STATUS.md` | Muse のみ | ジョブの状態（Muse が Antigravity 側の出力を読んで更新する） |
| `jobs/<job-id>/muse/VERIFY.md` | Muse のみ | Muse の機械検収＋ Carbon 検証の記録 |
| `jobs/<job-id>/work/` | Antigravity のみ | 実作業のコード（対象コードの置き場であり成果物） |
| `jobs/<job-id>/antigravity/HANDOVER.md` | Antigravity のみ | 変えたこと・判断したこと・未解決の懸念 |
| `jobs/<job-id>/antigravity/DIFF.patch` | Antigravity のみ | コード差分（`git diff` の出力） |
| `jobs/<job-id>/antigravity/TEST_LOG.md` | Antigravity のみ | 実行したテストと結果のログ |

- Antigravity は `muse/` のファイルを編集しない。Muse は `antigravity/` と `work/` のファイルを編集しない（読むだけ）。
- 状態の正本は `muse/STATUS.md`。Antigravity 側の進捗申告は `antigravity/HANDOVER.md` の有無と内容で伝える（状態ファイルを共同編集しない）。

## 必須出力（段取り Step 2 に対応）

ジョブは次の3点が揃うまで未完了として扱う。

1. コード差分（`antigravity/DIFF.patch`、または `work/` 内の変更そのもの）
2. テストログ（`antigravity/TEST_LOG.md`）
3. `antigravity/HANDOVER.md`

## 使い方

手順の正本は `PROTOCOL.md`。テンプレートは `templates/`。
