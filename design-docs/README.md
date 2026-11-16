# Design Doc

## 作成手順

1. ひな形を生成する

    ```shell
    mise run doc:new <slug>
    # 例: mise run doc:new my-feature
    # → design-docs/YYYY-MM-DD-my-feature/README.md を作成
    ```

2. `README.md` を編集する
3. 説明を分けた方が読みやすい場合は、以下のテンプレートファイルを同ディレクトリへコピーして追加する
4. PR を作成してレビューを依頼する

> [!NOTE]
> Design Doc はストック情報です。フロー情報は Issue や PR コメントで管理しましょう。

## テンプレート構成

| ファイル | 内容 | 必須 |
|---|---|---|
| [`_template/README.md`](_template/README.md) | 背景と目的・設計・相談したいこと | 必須 |
| [`_template/design.md`](_template/design.md) | 設計の検討と判断 | 説明を分ける場合 |
| [`_template/operations.md`](_template/operations.md) | 変更の適用方法と失敗時の対応 | 説明を分ける場合 |
| [`_template/validation.md`](_template/validation.md) | 確かめたいことと検証方法 | 説明を分ける場合 |
| [`_template/addons/sudo-modeling/`](_template/addons/sudo-modeling/README.md) | DDDのための sudoモデリング | 任意部品 |

テンプレートの見出しや書式は固定ではありません。作者自身が現状の具体例と解決したい問題を説明し、設計対象に合う構成で検討を進めてください。

セルフレビューと他者レビューの確認観点は [REVIEW.md](../REVIEW.md) にまとめています。確認項目ごとの節を作る必要はありません。AIを使う場合の作業制約は [CLAUDE.md](../CLAUDE.md) を参照してください。

## Tips

D2 の図を掲載する際、元データへのリンクを `<figure>` で付けられます。

```markdown
<figure>
  <img src="./YYYY-MM-DD-slug/design.png" alt="Design">
  <figcaption>Source: <a href="https://...">figjam</a></figcaption>
</figure>
```
