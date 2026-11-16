# 貢献のしかた

## 原文と翻訳

`ja` ブランチが原文です。`main` ブランチは英訳で、`ja` の変更を追って更新します。文章の変更は `ja` へ、英訳の修正は `main` へ Pull Request を送ってください。

## 変更の流れ

1. 変更したい内容を Issue に書く。規約（AGENTS.md、REVIEW.md）やテンプレートの変更は、どの場面で困ったかを添えてください。
2. ブランチを切って変更し、Pull Request を送る。
3. CI（[kit.yml](.github/workflows/kit.yml)）が、Kit から新しいリポジトリを作って `doc:new` と `kit:update` が動くことを確かめます。

## 文章

- 規約は「禁止」より「何をするか」で書く。1文に1つの内容。
- 日本語の文章は `npx textlint <file>` で検査できます。
- 図は `assets/*.excalidraw` を編集し、`npx @excalidraw/cli render assets/<name>.excalidraw --out assets/<name>.svg` で書き出します。

## 互換性

`kit:update` は Kit が持つファイルを上書きします。利用者が触るのは `local/` と `design-docs/` の設計書だけなので、それ以外のファイル名や場所を変えるときは、Release ノートに移行手順を書いてください。
