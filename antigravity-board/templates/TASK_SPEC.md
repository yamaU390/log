# TASK_SPEC

- タスク名：
- 作成日：
- ジョブID：（このフォルダ名）
- モデル：（Antigravity 側で選んだモデルを HANDOVER.md に記録すること）
- モード：board（ファイル経由のみ。agy 駆動ではない）

## 目的

（このタスクで達成したいことを、単一タスクとして完結する形で書く）

## 変更対象（許可する範囲）

- 変更してよい場所：このジョブの `work/` と `antigravity/` のみ
- 変更してはいけないもの：このジョブの `muse/`、他のジョブ、このリポジトリの他の場所

## 制約

- 外部通信、破壊的コマンド（削除・上書きの広範囲な実行）はしない
- 秘密情報（認証情報、.env 等）を読まない、書かない、ボードに置かない
- できなかったことは HANDOVER.md の「未解決の懸念」に残す

## 完了条件

- （受け入れテストや動作条件を、検証可能な形で書く）

## テストコマンド

- （Antigravity が実行し、TEST_LOG.md に残すコマンド。無ければ「なし」）

## 必須出力（Antigravity）

- `antigravity/HANDOVER.md`（`templates/HANDOVER.md` の型）
- `antigravity/DIFF.patch`（`git diff` の出力。変更が work/ 内で完結する場合はその旨を HANDOVER に書く）
- `antigravity/TEST_LOG.md`（実行したテストと結果）
