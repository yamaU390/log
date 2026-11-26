# TASK_SPEC

- タスク名：ボード疎通確認（smoke test）
- 作成日：2026-11-26
- ジョブID：2026-11-26-board-smoke-test
- モデル：（Antigravity 側で選んだモデルを HANDOVER.md に記録すること）
- モード：board（ファイル経由のみ。agy 駆動ではない）

## 目的

ボード経路の Antigravity 側の往復が成立するかを確かめるための最小ジョブ。実案件ではない。

## 作業内容（Antigravity）

1. この TASK_SPEC.md を読む。
2. `work/hello.txt` に、読んだ日時と使用モデルを1〜2行で書く。
3. 必須出力3点を `antigravity/` に置く（差分が hello.txt だけなら DIFF.patch はその差分）。

## 変更対象（許可する範囲）

- 変更してよい場所：このジョブの `work/` と `antigravity/` のみ
- 変更してはいけないもの：このジョブの `muse/`、他のジョブ、このリポジトリの他の場所

## 制約

- 秘密情報（認証情報、.env 等）を読まない、書かない
- できなかったことは HANDOVER.md の「未解決の懸念」に残す

## 完了条件

- `work/hello.txt`、`antigravity/HANDOVER.md`、`antigravity/DIFF.patch`、`antigravity/TEST_LOG.md`（テストは「なし」でよいが、その場合は TEST_LOG.md にテストなしと明記）が置かれていること

## テストコマンド

- なし
