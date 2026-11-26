# ボード運用手順（PROTOCOL）

正本の所在：このファイルがボード上の手順。キット側の背景・経緯は `~/workspace/external-llm/antigravity-delegation/BOARD.md`（Muse ローカル）。

## 置き場の決定（2026-11-26）

- 当初案は専用リポジトリの新規作成だったが、GitHub コネクタ（Muse GitHub App）からのリポジトリ作成は 403（Resource not accessible by integration）で実行できなかった。
- 既存4リポジトリのうち、実プロジェクトが入っている `ccfolia-mcp-api`／`game1022`／`.github-workflow` への相乗りは、試行フォルダ限定というキットの隔離原則と合わない。
- `log` はルートに README.md だけの実質空のリポジトリで、Muse コネクタの読み取りが実測済みだった。よって当面は `yamaU390/log` の `antigravity-board/` フォルダをボード置き場とする。ボードはこのフォルダ配下で自己完結しており、山村が専用リポジトリを作成した時はフォルダごと移行できる。

## 1ジョブの流れ

### 1. Muse がパケットを置く

- `jobs/<YYYY-MM-DD>-<slug>/` を作り、`muse/TASK_SPEC.md`（`templates/TASK_SPEC.md` の型）に仕様・スコープ・受け入れテスト・禁止事項を書く。対象コードが要る場合は、その置き場と取得方法を TASK_SPEC に明記する（ボードに置く場合は `work/` の初期状態として Muse が置くのではなく、Antigravity 側の初回作業として取得させるか、山村経由で置く。`work/` の書き手は Antigravity のみ、という分離を守るため）。
- `muse/STATUS.md` を `state: packet-placed` で作る。
- GitHub コネクタで push し、読み戻して置けたことを実測する。

### 2. 山村が Antigravity を起こす（節目・山村のみ）

- 山村が公式画面で Antigravity を開き、このリポジトリ（`yamaU390/log`）を clone／開かせる。
- Antigravity へ渡す指示は1文で足りる：「`antigravity-board/jobs/<job-id>/muse/TASK_SPEC.md` を読み、その仕様どおりに作業してください。成果物は同ジョブの `work/` と `antigravity/` にだけ書き、`muse/` は編集しないでください」
- Antigravity 側のアカウントは、山村本人がローカルで使う本人のアカウント（syuukatu390）。muse.mountain は関係ない（2026-11-20 の切り分け）。

### 3. Antigravity が結果を置く

- 実作業は `work/`。必須出力3点（差分・テストログ・HANDOVER.md）を `antigravity/` に置いて push する。
- できなかったことは HANDOVER.md の「未解決の懸念」に残す。HANDOVER.md が無いジョブは未完了。

### 4. Muse が読み戻して検証する

- GitHub コネクタで `antigravity/` の3点と `work/` の変更を読む。
- 機械検収：テストを Muse 側でも再実行し、差分を読み、スコープ逸脱（`muse/` の改変、`jobs/<job-id>/` 外の変更）がないか確認する。結果を `muse/VERIFY.md` に書く。
- 意味側の検証：仕様・差分・テスト結果を Carbon（Gemini Web、新規チャット）に渡して検証させ、Muse の見方と分けて VERIFY.md に残す（段取りの検証形どおり）。
- `muse/STATUS.md` を更新し（`verified`／`changes-requested`／`accepted`）、山村へ報告する。差し戻しは新しい TASK_SPEC 追記ではなく、STATUS.md の差し戻し欄＋必要なら次のジョブとして扱う。

## 計測（段取り Step 3 から引き継ぐ）

- Antigravity 側：実行前後の枠の減り（5時間枠％・週間枠％・プール別）、所要時間。Antigravity 側の数値は山村／Antigravity の申告でしか得られないため、HANDOVER.md に記録欄を置く。
- Muse 側：パケット作成＋検証の往復数とコンテキスト量の代理指標。
- 品質：検証で見つかった欠陥数、修正往復の回数、スコープ違反の有無。

## やらないこと

- `agy` の直接駆動・ラッピング、stream-json での子プロセス制御（§6）。
- Muse による Antigravity の操作・起動。
- 秘密情報（認証情報・.env 等）をボードに置くこと。ボードは公開リポジトリ配下にある前提で書く。
