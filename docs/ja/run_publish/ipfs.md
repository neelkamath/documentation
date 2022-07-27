# IPFSを使用してプロジェクトをホスティングする

このガイドでは、ローカルの SubQuery プロジェクトを [IPFS](https://ipfs.io/) に公開し、ホスティングインフラストラクチャにデプロイする方法について説明します。

Hosting a project in IPFS makes it available for all and reduces your reliance on centralised services like GitHub.

## 要件

- `@subql/cli` バージョン 0.21.0 以上。
- マニフェスト `specVersion` 0.2.0 以上。
- Get your [SUBQL_ACCESS_TOKEN](ipfs.md#prepare-your-subql-access-token) ready.
- デプロイを確実に成功させるために、`subql build` コマンドでプロジェクトをビルドし、公開する前にローカルでテストすることを強くお勧めします。

## SUBQL_ACCESS_TOKENを準備する

- ステップ 1: [SubQuery Projects](https://project.subquery.network/) に移動してログインします。
- Step 2: Click on your profile at the top right of the navigation menu, then click on **_Refresh Token_**.
- ステップ 3: 生成されたトークンをコピーします。
- ステップ 4: このトークンを使用するには:
  - オプション1:環境変数に SUBQL_ACCESS_TOKENを追加します。 `EXPORT SUBQL_ACCESS_TOKEN=<token>` (Windows) or `export SUBQL_ACCESS_TOKEN=<token>` (Mac/Linux)
  - オプション 2: 近日中に `subql/cli` が SUBQL_ACCESS_TOKEN をローカルに保存することをサポートする予定です。

## プロジェクトを公開する方法

We provide two methods to publish your project:

### Option 1

As you have `@subql/cli` already installed, you can run the following command, which will read the project and required information from its default manifest `project.yaml`:

```
// Publish it from your project's root directory
subql publish

// OR point to your project root
subql publish -f ~/my-project/
```

### Option 2

または、プロジェクトに複数のマニフェストファイルがあるとします。 たとえば、複数のネットワークをサポートしていますが、同じマッピングとビジネスロジックを共有し、以下のようにプロジェクト構造を持っています:

```
L projectRoot
 L src/
 L package.json
 L polkadot.yaml (Manifest for Polkadot network)
 L kusama.yaml   (Manifest for Kusama network)
 ...
```

選択したマニフェストファイルを使用してプロジェクトをいつでも公開できます

```
 # This will publish project support indexing Polkadot network
subql publish -f ~/my-projectRoot/polkadot.yaml
```

## 公開した後

プロジェクトを正常に公開した後 以下のログは、プロジェクトが IPFS クラスターで作成され、 `CID` (コンテンツ識別子) を返したことを示しています。

```
Building and packing code... done
Uploading SupQuery project to IPFS
SubQuery Project uploaded to IPFS: QmZ3q7YZSmhwBiot4PQCK3c7Z6HkteswN2Py58gkkZ8kNd  //CID
```

この `CID` に注意してください。 With this `CID`, you can view your published project as what we call it [IPFS Deployment](ipfs.md#ipfs-deployment).

With `@subql/cli` version 1.3.0 or above, when using `subql publish` it will store a copy of the project's `IPFS CID` in a file in your project directory, the naming of the file will be consistent with your project.yaml. For example, if your manfiest file is named `project.yaml`, the IPFS file will be named  `.project-cid`.

## IPFS Deployment

IPFS Deploymentは、分散ネットワーク上のSubQueryプロジェクトの独立したユニークな存在を表します。 そのため、プロジェクト内のコードに変更があると、そのユニーク性に影響が出ます。 ビジネスロジックを調整する必要がある場合、例えばマッピング機能を変更する場合は、プロジェクトを再発行する必要があり、 `CID` が変更されます。

For now, to view the project you have published, use a `REST` api tool such as [Postman](https://web.postman.co/), and use `POST` method with the following example URL to retrieve it:`https://ipfs.subquery.network/ipfs/api/v0/cat?arg=<YOUR_PROJECT_CID>`.

You should see the example project deployment as below.

このデプロイメントはマニフェストファイルによく似ています。 それらの記述フィールドを期待することができ、ネットワークとディクショナリーのエンドポイントは、プロジェクトの実行結果に直接影響しないため、削除されました。

ローカルプロジェクトで使用されたファイルは、IPFSにもパックされて公開されています。

```yaml
dataSources:
  - kind: substrate/Runtime
    mapping:
      file: ipfs://QmTTJKrMVzCZqmRCd5xKHbKymtQQnHZierBMHLtHHGyjLy
      handlers:
        - handler: handleBlock
          kind: substrate/BlockHandler
        - filter:
            method: Deposit
            module: balances
          handler: handleEvent
          kind: substrate/EventHandler
        - handler: handleCall
          kind: substrate/CallHandler
    startBlock: 8973820
network:
  genesisHash: "0x91b171bb158e2d3848fa23a9f1c25182fb8e20313b2c1eb49219da7a70ce90c3"
schema:
  file: ipfs://QmTP5BjtxETVqvU4MkRxmgf8NbceB17WtydS6oQeHBCyjz
specVersion: 0.2.0
```

## ホストされたサービスでSubQueryプロジェクトを実行する

### IPFS Deploymentでプロジェクトを作成する

You can follow the guide to [Publish your SubQuery project](../run_publish/publish.md) but where you set your deployment source you can select **IPFS**.

次に、本番用環境を選択し、IPFS Deploymentの CID（先頭の `ipfs://` を除く）をコピーして貼り付けます。

プレビューセクションにIPFS Deploymentが表示されます。 ネットワーク、ディクショナリのエンドポイントなどを選択できます。

ホストされたサービスにIPFSデプロイメントを正常にデプロイした後。 SubQueryエクスプローラで表示することができ、ローカルで行うようにクエリーサービスにアクセスできます。
