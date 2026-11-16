# design-doc-kit

Design Doc を書き、レビューするためのリポジトリの土台です。AIに作者の判断を代行させないことを前提にしています。

[English](https://github.com/nitaking/design-doc-kit/tree/main)

![AIが書く場合は全部が決まったように見え、AIが聞く場合は決めたことと未決が見分けられる](assets/overview.svg)

## なぜ作ったか

### Design Doc × Notion の問題

- Notion では描画されるのが Mermaid
  - 図の一部にコメントしにくい
- コメントした箇所に変更が入ると、コメントが吹き飛ぶ
- Mermaid 以外の図のレンダリングがしにくい
- バージョン管理がしにくい

Pull Request のように、提案とコメントと修正のやりとりがしたい。また、develop へのマージがしたい。

### Design Doc × Git で良くなったこと

- submodule で適用すると、複数のリポジトリ間での AI Agent Coding が自走させやすくなった
- レビュー時にも、一貫性のある仕様、コンテキストをもたせた Agent の利用ができる
- 人からみても、設計の反映がさせやすくなった
- 特に in/out の明確な、DB や API の設計は効果的

### AI Agent との設計の問題

- AIと壁打ちしながらの設計の詰めがしやすくなった反面、AIが思考の先取りをしてしまうため、設計の深さが浅くなる点がリスクになった
- 設計の経験が少なかったり、経験があっても考える時間が取れないと、一度目にした案のバイアスから抜け出しにくい
- また、最も理解が求められる設計において、AIによる目が滑る出力テキストは、脳の理解を妨げる

### この Kit で目指すこと

このような出来事があり、今回、「人間が思考に没頭できる」「AIは設計を行わない、伴走のみを行う」フォーマットを整備した。

AI向けの制約は [CLAUDE.md](CLAUDE.md)、レビューの観点は [REVIEW.md](REVIEW.md) にあります。

## 似たツールとの違い

この Kit は、AI に設計書を書かせるツールではありません。作者が書き、AI は質問とレビューだけを行うための土台です。

| | **design-doc-kit** | 仕様駆動開発 | 質問スキル | ADR ツール |
| --- | :---: | :---: | :---: | :---: |
| 設計書を書くのは | **作者** | AI | AI | 作者 |
| AI の役割 | 質問・整理・レビュー | 生成 | 質問 | なし |
| 不明な点の扱い | **未決として残す** | 推測で埋めて進む | 質問して決めてもらう | — |
| 提案と決定の区別 | ✅ | △ | — | — |
| レビュー観点の同梱 | ✅ | △ | — | — |
| 複数リポジトリで共有 | ✅ submodule | — | — | △ |
| ゴール | 人が考え、人がレビューする | エージェントに実装させる | 認識を揃える | 決定を記録・公開する |

- **仕様駆動開発**: [Spec Kit](https://github.com/github/spec-kit)、[OpenSpec](https://github.com/Fission-AI/OpenSpec)、[cc-sdd](https://github.com/gotalab/cc-sdd)、[Tsumiki](https://github.com/classmethod/tsumiki)。要件・設計・タスクを AI が生成し、人が承認します。不明な点は AI が推測で埋めます。たとえば Spec Kit の `/speckit.specify` は「文脈と業界標準から妥当な推測をする」「要確認の印は最大3つまで」と指示しています。Tsumiki は各項目に信頼性レベルを付けます（△）。
- **質問スキル**: [grill-me](https://github.com/mattpocock/skills)、[superpowers](https://github.com/obra/superpowers) の brainstorming。質問で作者の考えを引き出す点はこの Kit と同じで、併用できます。grill-me は各質問に推奨回答を付け、ファイルは残しません。brainstorming は最後に AI が設計書を書きます。
- **ADR ツール**: [MADR](https://github.com/adr/madr)、[adr-tools](https://github.com/npryce/adr-tools)、[Log4brains](https://github.com/thomvaill/log4brains)。人が書いた決定を記録し、公開します。AI の使い方は扱いません。Log4brains はモノレポ内の複数パッケージに対応します（△）。

## 含まれるもの

![Kit が持つファイルと、各リポジトリが持つファイル](assets/included.svg)

## 使い方

GitHub の「Use this template」からリポジトリを作ります。[mise](https://mise.jdx.dev/) が必要です。

```shell
mise install
pnpm install
mise run doc:new <slug>     # design-docs/YYYY-MM-DD-<slug>/README.md を作成
mise run textlint:diff      # 変更した Markdown を検査
mise run d2:png             # 変更した .d2 を PNG に変換
```

Design Doc の書き方は [design-docs/README.md](design-docs/README.md) を参照してください。

## 複数のリポジトリから参照する

Design Doc のリポジトリを、参照する側のリポジトリに submodule として追加します。

![仕様変更は Design Doc を更新し、submodule で各リポジトリに同期して、Agent などで半自動反映する](assets/submodule.svg)

```shell
# 参照する側のリポジトリで
git submodule add <Design Doc リポジトリの URL> shared-docs

# 設計の更新を取り込む
git submodule update --remote shared-docs
git add shared-docs
git commit -m "docs(shared-docs): update to latest"
```

## リポジトリ固有の設定

この Kit が持つファイルは編集せず、固有の内容は `local/` に書きます。こうしておくと、Kit の更新を取り込むときに衝突しません。

| 書く内容 | 場所 |
| --- | --- |
| AIへの固有の指示 | [local/CLAUDE.md](local/CLAUDE.md) |
| 固有のレビュー観点 | [local/REVIEW.md](local/REVIEW.md) |
| 自分たちの README | `.github/README.md` |

## 更新の取り込み

```shell
git remote add upstream https://github.com/nitaking/design-doc-kit.git   # 初回のみ
mise run kit:update        # upstream/ja を取り込む
```

## ライセンス

[MIT](LICENSE)

