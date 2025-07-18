# プロビジョニングしたリソースの削除

ハンズオンが終了し、不要となったリソースは確実に削除しましょう。Azure上に作成したリソースを放置すると予期せぬコストが発生する可能性があります。ここではAzure Developer CLIを使ったクリーンアップ手順を紹介します。

## リソースの削除手順

Azure Developer CLIでは、デプロイした環境を一括で削除するコマンドが用意されています。特に今回のようにリソースグループごと作成した場合、そのリソースグループと中の全リソースをまとめて消去できます。

- **削除コマンドの実行**: プロジェクトのディレクトリ（`postgres-agentic-shop`）内で、以下のコマンドを実行します。

```sh
azd down --purge
```

これにより、`azd up`で作成された全リソースが削除されます。`--purge`オプションを付けることで、Azure OpenAIのような「アカウント」リソースも含め完全に削除されます。通常の`azd down`ではリソースグループ内の削除のみですが、`--purge`を付けると例えばOpenAIリソースからモデルのデプロイ解除→リソース削除まで行われます。削除には数分かかることがありますが、完了すると「削除成功」のようなメッセージが表示されます。

- **削除結果の確認**: 念のためAzureポータルでリソースグループ一覧を確認し、該当のリソースグループが消えていることを確認してください。`azd`の環境もローカルに記録が残っていますが、再利用しない場合は `.azure` ディレクトリごと削除しておいて構いません。

- **代替手段**: Azure Developer CLIを使用しない場合、Azureポータルからリソースグループを手動で削除しても同様です。その場合、Azure OpenAIリソースのみリソースグループ外に存在する可能性がありますが、今回は同じRG内に作成されているはずなので、一括削除できる見込みです。ポータルでリソースグループを削除する際は、リソースグループ名の入力確認がありますので指示に従ってください。

> [!CAUTION] 警告
> 一度削除を行うと、データベース内のデータや接続情報、ログなど全て失われます。ハンズオン中に何か成果物（例: エクスポートした特徴データや分析結果）がある場合は事前にバックアップしておいてください。もっとも、本ハンズオンでは特に保持すべきデータはありませんので、そのまま削除して問題ありません。

以上で後片付けは完了です。Azure上に不要なリソースを残さない習慣は、コスト管理上とても重要ですので、ハンズオンの最後には必ずこの手順を実施するようにしましょう。

これで、GitHubリポジトリ postgres-agentic-shop を用いたAzure上でのAI統合アプリケーション開発ハンズオンの全工程が終了です。

お疲れ様でした！

今回学んだように、Azure Database for PostgreSQLにAI拡張や`pgvector`、Apache AGEを組み合わせることで、シンプルながら強力なAIアプリケーション基盤を構築できます。ぜひ現場のプロジェクトでも応用してみてください。各セクションで触れた技術要素について更に深掘りしたい場合、公式ドキュメントや関連ブログ記事なども参照すると理解が深まるでしょう。


[前へ](07-GraphRAG.md)
