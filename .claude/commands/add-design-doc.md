# Add Design Doc - Usage: /add-design-doc [taskID] <title> (例: PROJ-123 新機能の設計)

`design-docs/` 配下に新しい Design Doc ファイルを作成する。

## 引数

`$ARGUMENTS` の形式: `[taskID] <title>`

例:
- `PROJ-123 新機能の設計`
- `認証リファクタリング`

## 実行手順

1. `$ARGUMENTS` を解析する。最初のトークンがチケットIDの形式（英字・ハイフン・数字）なら `taskID` とし、残りを `title` とする。そうでなければ全体を `title` とする

2. ディレクトリ名を決定する:
   - 形式: `design-docs/YYYY-MM-DD-<taskID>-<slug>/README.md`。`taskID` がなければ `design-docs/YYYY-MM-DD-<slug>/README.md`
   - 日付は今日の日付（`currentDate` を参照）
   - slug は title のスペースをハイフンに置換した英語表記（日本語の場合は適切に英訳）
   - 同名のディレクトリが既にあれば作成せず、その旨を伝えて終了する

3. `design-docs/_template/README.md` のテンプレートを読み込み、見出しの `<title>` を `title` の値に置換する
   - それ以外の記入案内（`<!-- -->` のコメントや `<...>` のプレースホルダー）は作者が書き換えるため、そのまま残す

4. `design-docs/<dir>/README.md` に書き出す

5. 作成したファイルパスを表示して完了を伝える
