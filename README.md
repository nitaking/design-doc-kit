# design-doc-kit

Design Doc を書き、レビューするためのリポジトリの土台です。AIに作者の判断を代行させないことを前提にしています。

[English](https://github.com/nitaking/design-doc-kit/tree/main)

![AIに設計を任せる場合と、design-doc-kit を使う場合の比較](assets/overview.svg)

## なぜ作ったか

### Design Doc を Notion で管理していたとき

- Notion では描画されるのが Mermaid
  - 図の一部にコメントしにくい
- コメントした箇所に変更が入ると、コメントが吹き飛ぶ
- Mermaid 以外の図のレンダリングがしにくい
- バージョン管理がしにくい

Pull Request のように、提案とコメントと修正のやりとりがしたい。また、develop へのマージがしたい。

### 導入してみて

- submodule で適用すると、複数のリポジトリ間での AI Agent Coding が自走させやすくなった
- レビュー時にも、一貫性のある仕様、コンテキストをもたせた Agent の利用ができる
- 人からみても、設計の反映がさせやすくなった
- 特に in/out の明確な、DB や API の設計は効果的

### 導入後の不満

- AIと壁打ちしながらの設計の詰めがしやすくなった反面、AIが思考の先取りをしてしまうため、設計の深さが浅くなる点がリスクになった
- 設計の経験が少なかったり、経験があっても考える時間が取れないと、一度目にした案のバイアスから抜け出しにくい
- また、最も理解が求められる設計において、AIによる目が滑る出力テキストは、脳の理解を妨げる

### 動機

このような出来事があり、今回、「人間が思考に没頭できる」「AIは設計を行わない、伴走のみを行う」フォーマットを整備した。

AI向けの制約は [CLAUDE.md](CLAUDE.md)、レビューの観点は [REVIEW.md](REVIEW.md) にあります。

## 含まれるもの

```mermaid
flowchart LR
  author([作者])
  ai([AI])
  reviewer([レビュアー])

  subgraph kit["キットが持つ: upstream の merge で更新される"]
    claude["CLAUDE.md<br/>AIへの規約"]
    review["REVIEW.md<br/>レビュー観点"]
    template["design-docs/_template/<br/>テンプレート"]
    addon["addons/sudo-modeling/<br/>任意部品"]
    tasks["mise.toml<br/>タスク"]
    lint[".textlintrc.yml<br/>日本語の文章 lint"]
  end

  subgraph yours["各リポジトリが持つ"]
    local["local/<br/>固有の指示と観点"]
    docs["design-docs/YYYY-MM-DD-*/<br/>設計書"]
  end

  author -->|書く| docs
  reviewer -->|レビューする| docs
  ai -->|従う| claude
  reviewer -->|確認に使う| review
  template -->|コピーされる| docs
  tasks -->|doc:new, d2:png| docs
  lint -->|検査する| docs
  claude -->|取り込む| local
  review -->|リンクする| local
  addon -.->|有効にする| local
```

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

## リポジトリ固有の設定

このキットが持つファイルは編集せず、固有の内容は `local/` に書きます。こうしておくと、キットの更新を取り込むときに衝突しません。

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

- 設定ファイルとタスク定義: [MIT](LICENSE)
- 規約とテンプレートの文面（Markdown）: [CC BY 4.0](LICENSE-CC-BY-4.0)

