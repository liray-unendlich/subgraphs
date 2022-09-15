# Subgraphs

このレポジトリは標準化されたスキーマによって定義されるサブグラフを含んでいます。このサブグラフは、ブロックチェーンから直接データを抽出し、dAppや分析のために、意味のあるメトリックに変換するために使用されます。私たちの目標は、仮想通貨の世界のすべてのDeFiプロトコルのためのサブグラフを構築することです。

## コントリビュートガイド

- どのプロトコルのサブグラフを作成するかを決めます。
- このリポジトリをフォークします。
- フォルダ`subgraphs`の下に、作業したいプロトコルの名前でフォルダを追加します。
- ルートフォルダから対応するスキーマをコピーしてください。例えば、Yield aggregator を開発する場合、`schema-yield.graphql` を自分のフォルダにコピーして、`schema.graphql` にリネームしてください。`schema-common.graphql`はスキーマの設計やリファレンスとして使用するものであり、実装には決して使用しないことに注意してください。
- そのフォルダの中でサブグラフを構築する。[リファレンス・サブグラフ](./subgraphs/_reference_/)をリファレンスとして自由に使ってください。
- 完成したら、このレポにPR（プルリクエスト）を提出します。作業途中のPRの場合は、必ずドラフトとして提出してください。PRの説明には、あなたのデプロイメントへのリンクを含めてください。

## Recommended Development Workflow

- プロトコルを理解することから始めましょう。テストネットでプロトコルのUIを操作し、Etherscanで取引の詳細を確認し、発信される主要なイベントに注目することから始めるのが簡単でしょう。
- スマートコントラクトを調べます。データを取得する必要があるものを特定する。
  - 通常、各プロトコルには、他のコントラクトの追跡を担当するファクトリーコントラクトがあります（例：Uniswapのファクトリーコントラクト、Aaveのレンディングプールレジストリ、Yearnのレジストリなど）。
  - また、プールレベルの簿記とトランザクションを担当するプール/金庫契約もある（例：Uniswapのペア契約、Yearnの金庫契約、Aaveのレンディングプール契約）。
- スキーマを確認し、スマートコントラクトのイベント/コールから、どのデータが各エンティティのフィールドにマッピングされる必要があるか考えてください。
  - より粒度の細かいエンティティから始めて、集約されたデータまで構築するのが最も簡単です。
  - 例えば、通常はトランザクションや使用状況メトリクス用のマッピングを書き始めるのが簡単です。
- docs` フォルダにあるドキュメントに目を通してみてください。多くの疑問が解決されるはずです。
- マッピングを実装し、Hosted ServiceまたはThe Graph Studioを使ってデータをデプロイし、テストする。
- メトリクスの計算（例：収益、手数料、TVL）については、プロトコルのサブグラフフォルダにある `README.md` を参照してください。また、`docs/Schema.md`にスキーマの各フィールドがどのように定義されているか、より幅広い説明があります。もし何か不明な点があれば、遠慮なく私に連絡してください。
- サブグラフのデータを素早く視覚化するために、便利なデバッグ/検証用ダッシュボードを作成しました。これは、[subgraphs.xyz](https://subgraphs.xyz/)にデプロイされており、ソースコードは `dashboard` にありますので、ローカルで起動したい場合はそちらをご利用ください。
- 他のソースに対してサブグラフを検証し、これらのソースへの特定のリンクをREADMEに含めてください。以下は、一般的なソースです。
  - プロジェクトの公式アナリティクスダッシュボード
  - [DeFi Llama](https://defillama.com/) (TVL確認)
  - [Dune Analytics](https://dune.xyz/)
  - [TokenTerminal](https://www.tokenterminal.com/terminal)

> その他の寄稿ガイドラインは [Contributing.md](./docs/Contributing.md) を参照してください。

## Resources

### 入門ドキュメント

- GraphQLの基本: [https://graphql.org/learn/](https://graphql.org/learn/)
- GraphQLを使ったサブグラフのクエリ: https://thegraph.com/docs/en/developer/graphql-api/
- The Graphの入門: [https://thegraph.academy/developers/](https://thegraph.academy/developers/)
- サブグラフの定義: [https://thegraph.academy/developers/defining-a-subgraph/](https://thegraph.academy/developers/defining-a-subgraph/)
- サブグラフの作成: https://thegraph.com/docs/en/developer/create-subgraph-hosted/
- The Graph Studioを使ったサブグラフのデプロイメント: [https://thegraph.com/docs/en/studio/deploy-subgraph-studio/](https://thegraph.com/docs/en/studio/deploy-subgraph-studio/)

### 中級ドキュメント

- [AssemblyScript API](https://thegraph.com/docs/en/developer/assemblyscript-api/)
- [Matchstickを用いたユニットテスト](https://thegraph.com/docs/en/developer/matchstick/)
- [Sushiswap用のサブグラフを開発する](https://docs.simplefi.finance/subgraph-development-documentation/sushiswap-subgraph-development)
- [Loopringのサブグラフを開発する](https://www.youtube.com/watch?v=SNmzhwlQqgU)
  - テンプレート（動的データソース）の利用
  - プロキシのインデックス作成

### 上級ドキュメント

- 素晴らしいサブグラフを開発する (パートI): https://www.youtube.com/watch?v=4V2o5YJooOM
  - スキーマデザイン
  - エラーハンドリング
  - インターフェースとユニオンタイプ
- 素晴らしいサブグラフを開発する (パートII) https://www.youtube.com/watch?v=1-8AW-lVfrA
  - パフォーマンスへのtipと技術 (マッピング・クエリ面)
- [graph-nodeのドキュメント](https://github.com/graphprotocol/graph-node/tree/master/docs)

## Development Status

🔨 = In progress.
🛠 = Feature complete. Additional testing required.
✅ = Production-ready.
| Protocol | Status | Versions † | Deployments |
| ------- | :------: | --- | --- |
| **DEX AMM** | | |
| [Apeswap](https://apeswap.finance/) | ✅ | 1.3.0 / 1.1.6 / 1.0.0 | [![Apeswap BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/apeswap-bsc) [![Apeswap Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/apeswap-polygon) |
| [Balancer v2](https://balancer.fi/) | 🛠 | 1.3.0 / 1.1.3 / 1.0.0 | [![Balancer V2 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/balancer-v2-ethereum) [![Balancer V2 Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/balancer-v2-arbitrum) [![Balancer V2 Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/balancer-v2-polygon) |
| [Bancor v3](https://try.bancor.network/) | ✅ | 1.3.0 / 1.0.0 / 1.0.0 | [![Bancor V3 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/bancor-v3-ethereum) |
| [Beethoven X](https://beets.fi/) | 🛠 | 1.3.0 / 1.1.3 / 1.0.0 | [![Beethoven X Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/beethoven-x-fantom) [![Beethoven X Optimism](./docs/images/chains/optimism.png)](https://thegraph.com/hosted-service/subgraph/messari/beethoven-x-optimism) |
| [Curve](https://curve.fi/) | 🛠 | 1.2.1 / 1.0.0 / 1.0.0 | [![Curve Finance Gnosis](./docs/images/chains/xdai.png)](https://thegraph.com/hosted-service/subgraph/messari/curve-finance-gnosis) [![Curve Finance Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/curve-finance-polygon) [![Curve Finance Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/curve-finance-arbitrum) [![Curve Finance Optimism](./docs/images/chains/optimism.png)](https://thegraph.com/hosted-service/subgraph/messari/curve-finance-optimism) [![Curve Finance Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/curve-finance-fantom) [![Curve Finance Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/curve-finance-avalanche) [![Curve Finance Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/curve-finance-ethereum) |
| [Ellipsis Finance](https://ellipsis.finance/) | 🛠 | 1.2.1 / 1.0.0 / 1.0.0 | [![Ellipsis Finance BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/ellipsis-finance-bsc) |
| DODO v2 | 🔨 | | |
| [Honeyswap](https://honeyswap.org/) | 🛠 | 1.3.0 / 1.0.3 / 1.0.1 | [![Honeyswap Gnosis](./docs/images/chains/xdai.png)](https://thegraph.com/hosted-service/subgraph/messari/honeyswap-gnosis) |
| [MM Finance](https://mm.finance/) | 🛠 | 1.3.0 / 1.0.2 / 1.0.0 | [![MM Finance Cronos](./docs/images/chains/cronos.png)](https://graph.cronoslabs.com/subgraphs/name/messari/mm-finance) [![MM Finance Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/mm-finance-polygon) |
| [Platypus Finance](https://platypus.finance/) | ✅ | 1.3.0 / 1.3.0 / 1.0.0 | [![Platypus Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/platypus-finance-avalanche) |
| [Quickswap](https://quickswap.exchange/#/swap) | 🛠 | 1.3.0 / 1.0.3 / 1.0.0 | [![Quickswap Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/quickswap-polygon) |
| [Saddle Finance](https://saddle.finance/#/) | 🛠 | 1.3.0 / 1.1.0 / 1.0.0 | [![Saddle Finance Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/saddle-finance-ethereum) [![Saddle Finance Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/saddle-finance-arbitrum) [![Saddle Finance Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/saddle-finance-fantom) [![Saddle Finance Optimism](./docs/images/chains/optimism.png)](https://thegraph.com/hosted-service/subgraph/messari/saddle-finance-optimism) |
| [Solarbeam](https://solarbeam.io/) | 🛠 | 1.3.0 / 1.1.4 / 1.0.0 | [![Solarbeam Moonriver](./docs/images/chains/moonriver.png)](https://thegraph.com/hosted-service/subgraph/messari/solarbeam-moonriver) |
| [SpiritSwap](https://www.spiritswap.finance/) | 🛠 | 1.3.0 / 1.1.4 / 1.0.0 | [![SpiritSwap Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/spiritswap-fantom) |
| [SpookySwap](https://spooky.fi/) | 🛠 | 1.3.0 / 1.1.5 / 1.0.0 | [![SpookySwap Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/spookyswap-fantom) |
| [SushiSwap](https://www.sushi.com/) | ✅ | 1.3.0 / 1.1.8 / 1.0.0 | [![SushiSwap Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-ethereum) [![SushiSwap Celo](./docs/images/chains/celo.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-celo) [![SushiSwap Fuse](./docs/images/chains/fuse.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-fuse) [![SushiSwap Moonriver](./docs/images/chains/moonriver.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-moonriver) [![SushiSwap Moonbeam](./docs/images/chains/moonbeam.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-moonbeam) [![SushiSwap Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-avalanche) [![SushiSwap BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-bsc) [![SushiSwap Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-arbitrum) [![SushiSwap Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-fantom) [![SushiSwap Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-polygon) [![SushiSwap Gnosis](./docs/images/chains/xdai.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-gnosis) [![SushiSwap Harmony](./docs/images/chains/harmony.png)](https://thegraph.com/hosted-service/subgraph/messari/sushiswap-harmony) |
| [Trader Joe](https://traderjoexyz.com/home#/) | 🛠 | 1.3.0 / 1.1.6 / 1.0.0 | [![Trader Joe Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/trader-joe-avalanche) |
| [Ubeswap](https://ubeswap.org/) | 🛠 | 1.3.0 / 1.1.6 / 1.0.0 | [![Ubeswap Celo](./docs/images/chains/celo.png)](https://thegraph.com/hosted-service/subgraph/messari/ubeswap-celo) |
| [Uniswap v2](https://uniswap.org/) | 🛠 | 1.3.0 / 1.1.6 / 1.0.0 | [![Uniswap V2](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/uniswap-v2-ethereum) |
| [Uniswap v3](https://uniswap.org/) | 🛠 | 1.3.0 / 1.1.1 / 1.0.0 | [![Uniswap V3](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/uniswap-v3-ethereum) [![Uniswap V3 Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/uniswap-v3-polygon) [![Uniswap V3 Optimism](./docs/images/chains/optimism.png)](https://thegraph.com/hosted-service/subgraph/messari/uniswap-v3-optimism) [![Uniswap V3 Arbtitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/uniswap-v3-arbitrum) [![Uniswap V3 Celo](./docs/images/chains/celo.png)](https://thegraph.com/hosted-service/subgraph/messari/uniswap-v3-celo) |
| [Velodrome](https://velodrome.finance/) | 🔨 | | |
| [VVS Finance](https://vvs.finance/) | 🛠 | 1.3.0 / 1.1.7 / 1.0.0 | [![VVS Finance Cronos](./docs/images/chains/cronos.png)](https://graph.cronoslabs.com/subgraphs/name/messari/vvs-finance) |
| **Lending Protocols** | | |
| [Aave v2](https://aave.com/) | ✅ | 2.0.1 / 1.2.13 / 1.0.0 | [![Aave V2 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v2-ethereum) [![Aave V2 Ethereum ARC](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-arc-ethereum) [![Aave V2 Ethereum RWA](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-rwa-ethereum) [![Aave V2 Ethereum AMM](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-amm-ethereum) [![Aave V2 Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v2-avalanche) [![Aave V2 Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v2-polygon) |
| [Aave v3](https://aave.com/) | ✅ | 2.0.1 / 1.0.3 / 1.0.0 | [![Aave V3 Optimism](./docs/images/chains/optimism.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v3-optimism) [![Aave V3 Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v3-polygon) [![Aave V3 Harmony](./docs/images/chains/harmony.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v3-harmony) [![Aave V3 Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v3-fantom) [![Aave V3 Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v3-avalanche) [![Aave V3 Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/aave-v3-arbitrum) |
| [Aurigami](https://www.aurigami.finance/) | 🛠 | 2.0.1 / 1.1.3 / 1.0.0 | [![Aurigami Aurora](./docs/images/chains/aurora.png)](https://thegraph.com/hosted-service/subgraph/messari/aurigami-aurora) |
| [Alpaca Finance (Lend)](https://app.alpacafinance.org/lend) | 🔨 | | |
| [Bastion Protocol](https://bastionprotocol.com/) | 🛠 | 2.0.1 / 1.1.3 / 1.0.0 | [![Bastion Protocol Aurora](./docs/images/chains/aurora.png)](https://thegraph.com/hosted-service/subgraph/messari/bastion-protocol-aurora) |
| [Banker Joe](https://traderjoexyz.com/lending#/) | ✅ | 2.0.1 / 1.1.4 / 1.0.0 | [![Banker Joe Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/banker-joe-avalanche) |
| [BENQI](https://benqi.fi/) | ✅ | 2.0.1 / 1.1.3 / 1.0.0 | [![BENQI Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/benqi-avalanche) |
| [Compound](https://compound.finance/) | ✅ | 2.0.1 / 1.7.3 / 1.0.0 | [![Compund Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/compound-v2-ethereum) |
| [CREAM Finance](https://cream.finance/) | 🛠 | 2.0.1 / 1.1.4 / 1.0.0 | [![CREAM Finance Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/cream-finance-arbitrum) [![CREAM Finance Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/cream-finance-polygon) [![CREAM Finance BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/cream-finance-bsc) [![CREAM Finance Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/cream-finance-ethereum) |
| [dForce](https://dforce.network) | 🛠 | 2.0.1 / 1.1.3 / 1.0.0 | [![dforce Arbitrum](./docs/images/chains/arbitrum.png)]() [![dforce Avalanche](./docs/images/chains/avalanche.png)]() [![dforce BSC](./docs/images/chains/bsc.png)]() [![dforce Ethereum](./docs/images/chains/ethereum.png)]() [![dforce Optimism](./docs/images/chains/optimism.png)]() [![dforce Polygon](./docs/images/chains/matic.png)]() |
| [Euler Finance](https://www.euler.finance/) | ✅ | 1.3.0 / 1.1.1 / 1.0.0 | [![Euler Finance](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/euler-finance-ethereum) |
| [Geist Finance](https://geist.finance/markets) | ✅ | 2.0.1 / 1.0.9 / 1.0.0 | [![Geist Protocol](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/geist-fantom) |
| [Iron Bank](https://app.ib.xyz/) | ✅ | 2.0.1 / 1.1.1 / 1.0.0 | [![Iron Bank Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/iron-bank-fantom) [![Iron Bank Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/iron-bank-avalanche) [![Iron Bank Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/iron-bank-ethereum) |
| [Maple Finance](https://www.maple.finance/) | ✅ | 1.3.0 / 1.1.0 / 1.0.0 | [![Maple Finance Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/maple-finance-ethereum) |
| [Moonwell Finance](https://moonwell.fi/) | ✅ | 2.0.1 / 1.1.1 / 1.0.0 | [![Moonwell Moonriver](./docs/images/chains/moonriver.png)](https://thegraph.com/hosted-service/subgraph/messari/moonwell-moonriver) [![Moonwell Moonbeam](./docs/images/chains/moonbeam.png)](https://thegraph.com/hosted-service/subgraph/messari/moonwell-moonbeam) |
| Notional Finance | 🔨 | | |
| Radiant | 🔨 | | |
| [Rari Fuse](https://app.rari.capital/fuse) | 🛠 | 2.0.1 / 1.1.5 / 1.0.0 | [![Rari Fuse Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/rari-fuse-ethereum) [![Rari Fuse Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/rari-fuse-arbitrum) |
| [SCREAM](https://scream.sh/) | ✅ | 2.0.1 / 1.1.3 / 1.0.0 | [![SCREAM Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/scream-fantom) |
| TrueFi | 🔨 | | |
| [Tectonic](https://tectonic.finance/) | ✅ | 2.0.1 / 1.1.4 / 1.0.0 | [![Tectonic Cronos](./docs/images/chains/cronos.png)](https://graph.cronoslabs.com/subgraphs/name/messari/tectonic/graphql) |
| [Venus Protocol](https://venus.io/) | ✅ | 2.0.1 / 1.1.4 / 1.0.0 | [![Venus Protocol BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/venus-protocol-bsc) |
| [Yeti Finance](https://yeti.finance/) | 🔨 | | |
| **CDPs** | | |
| [Abracadabra](https://abracadabra.money/) | ✅ | 2.0.1 / 1.2.9 / 1.0.0 | [![Abracadabra Money](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/abracadabra-money-ethereum) [![Abracadabra Money](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/abracadabra-money-bsc) [![Abracadabra Money](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/abracadabra-money-arbitrum) [![Abracadabra Money](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/abracadabra-money-fantom) [![Abracadabra Money](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/abracadabra-money-avalanche) |
| [Inverse Finance](https://www.inverse.finance/) | ✅ | 1.3.0 / 1.2.2 / 1.0.0 | [![Inverse Finance Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/inverse-finance-ethereum) |
| [Liquity](https://www.liquity.org/) | ✅ | 2.0.1 / 1.2.0 / 1.0.1 | [![Liquity Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/liquity-ethereum) |
| [MakerDAO](https://makerdao.com/en/) | ✅ | 1.3.0 / 1.1.3 / 1.0.1 | [![MakerDAO Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/makerdao-ethereum) |
| [QiDAO](https://app.mai.finance/) | ✅ | 1.3.0 / 1.1.0 / 1.0.0 | [![QiDAO Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-arbitrum) [![QiDAO Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-avalanche) [![QiDAO BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-bsc) [![QiDAO Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-fantom) [![QiDAO Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-polygon) [![QiDAO Moonriver](./docs/images/chains/moonriver.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-moonriver) [![QiDAO Optimism](./docs/images/chains/optimism.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-optimism) [![QiDAO Gnosis](./docs/images/chains/xdai.png)](https://thegraph.com/hosted-service/subgraph/messari/qidao-gnosis) |
| Synthetix | 🔨 | | |
| [Vesta Finance](https://vestafinance.xyz/) | 🔨 | | |
| **Yield Aggregators** | | |
| Alchemix | 🔨 | | |
| Aura | 🔨 | | |
| [Arrakis Finance](https://www.arrakis.finance/) | ✅ | 1.3.0 / 1.0.1 / 1.0.0 | [![Arrakis Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/arrakis-finance-ethereum) |
| [BadgerDAO](https://badger.com/) | 🛠 | 1.3.0 / 1.0.0 / 1.0.0 | [![BadgerDAO Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/badgerdao-ethereum) | |
| [Beefy Finance](https://beefy.finance/) | 🛠 | 1.2.1 / 1.0.2 / 1.1.0 | [![Beefy Finance Harmony](./docs/images/chains/harmony.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-harmony) [![Beefy Finance Moonbeam](./docs/images/chains/moonbeam.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-moonbeam) [![Beefy Finance Celo](./docs/images/chains/celo.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-celo) [![Beefy Finance Aurora](./docs/images/chains/aurora.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-aurora) [![Beefy Finance Fuse](./docs/images/chains/fuse.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-fuse) [![Beefy Finance Moonriver](./docs/images/chains/moonriver.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-moonriver) [![Beefy Finance Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-arbitrum) [![Beefy Finance Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-avalanche) [![Beefy Finance Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-polygon) [![Beefy Finance BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-bsc) [![Beefy Finance Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/beefy-finance-fantom) |
| [Belt Finance](https://belt.fi/landing) | 🛠 | 1.3.0 / 1.1.0 / 1.0.0 | [![Belt BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/belt-finance-bsc) |
| [Convex Finance](https://www.convexfinance.com/) | ✅ | 1.3.0 / 1.2.0 / 1.0.0 | [![Convex Finance Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/convex-finance-ethereum) |
| [Gamma Strategies](https://www.gamma.xyz/) | ✅ | 1.3.0 / 1.1.2 / 1.0.0 | [![Gamma Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/gamma-ethereum) [![Gamma Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/gamma-polygon) |
| Harvest Finance | 🔨 | | |
| Liquid Driver | 🔨 | | |
| [Rari Vaults](https://rari.capital/) | ✅ | 1.3.0 / 1.4.2 / 1.0.0 | [![Rari Vaults Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/rari-vaults-ethereum) |
| [Stake DAO](https://stakedao.org/) | 🛠 | 1.3.0 / 1.3.0 / 1.0.0 | [![Stake DAO](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/stake-dao-ethereum) |
| [Tokemak](https://www.tokemak.xyz/) | 🛠 | 1.2.1 / 1.0.0 / 1.0.0 | [![Tokemak](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/tokemak-ethereum) |
| [Vesper Finance](https://vesper.finance/) | ✅ | 1.3.0 / 1.0.0 / 1.0.0 | [![Vesper Finance Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/vesper-ethereum) |
| Yield Yak | 🔨 | | |
| [Yearn v2](https://yearn.fi/) | 🛠 | 1.3.0 / 1.2.0 / 1.0.0 | [![Yearn V2 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/yearn-v2-ethereum) [![Yearn V2 Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/yearn-v2-arbitrum) [![Yearn V2 Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/yearn-v2-fantom) |
| **Others** | | |
| [Lido](https://lido.fi) | ✅ | 1.3.0 / 1.0.0 / 1.0.0 | [![Lido Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/lido-ethereum) |
| Rocket Pool | 🔨 | | |
| Tornado Cash | 🔨 | | |
| The Graph | 🔨 | | |
| **Governance** | | |
| Fei Governor | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![Fei Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/fei-governance) |
| ENS Governor | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ENS Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/ens-governance) |
| Hop Governor | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![Hop Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/hop-governance) |
| TrueFi Governor | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![TrueFi Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/truefi-governance) |
| Euler Governor | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![Euler Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/euler-governance) |
| Silo Governor | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![Silo Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/silo-governance) |
| Unlock Governor | 🔨 | 1.0.0 / 1.0.0 / 1.0.0 | [![Unlock Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/unlock-governance) |
| Angle Governor | 🔨 | 1.0.0 / 1.0.0 / 1.0.0 | [![Angle Governor](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/angle-governance) |
| Code4rena Governor | 🔨 | 1.0.0 / 1.0.0 / 1.0.0 | [![Code4rena Governor](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/code4rena-governance) |
| **Network Subgraph** | | |
| EVM | 🛠 | 1.1.1 / 1.1.2 / 1.0.0 | [![Network Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/network-ethereum) [![Network Arbitrum](./docs/images/chains/arbitrum.png)](https://thegraph.com/hosted-service/subgraph/messari/network-arbitrum) [![Network Aurora](./docs/images/chains/aurora.png)](https://thegraph.com/hosted-service/subgraph/messari/network-aurora) [![Network Avalanche](./docs/images/chains/avalanche.png)](https://thegraph.com/hosted-service/subgraph/messari/network-avalanche) [![Network Boba](./docs/images/chains/boba.png)](https://thegraph.com/hosted-service/subgraph/messari/network-boba) [![Network BSC](./docs/images/chains/bsc.png)](https://thegraph.com/hosted-service/subgraph/messari/network-bsc) [![Network Celo](./docs/images/chains/celo.png)](https://thegraph.com/hosted-service/subgraph/messari/network-celo) [![Network Clover](./docs/images/chains/clover.png)](https://thegraph.com/hosted-service/subgraph/messari/network-clover) [![Network Fantom](./docs/images/chains/fantom.png)](https://thegraph.com/hosted-service/subgraph/messari/network-fantom) [![Network Fuse](./docs/images/chains/fuse.png)](https://thegraph.com/hosted-service/subgraph/messari/network-fuse) [![Network Gnosis](./docs/images/chains/xdai.png)](https://thegraph.com/hosted-service/subgraph/messari/network-gnosis) [![Network Harmony](./docs/images/chains/harmony.png)](https://thegraph.com/hosted-service/subgraph/messari/network-harmony) [![Network Moonbeam](./docs/images/chains/moonbeam.png)](https://thegraph.com/hosted-service/subgraph/messari/network-moonbeam) [![Network Moonriver](./docs/images/chains/moonriver.png)](https://thegraph.com/hosted-service/subgraph/messari/network-moonriver) [![Network Optimism](./docs/images/chains/optimism.png)](https://thegraph.com/hosted-service/subgraph/messari/network-optimism) [![Network Polygon](./docs/images/chains/matic.png)](https://thegraph.com/hosted-service/subgraph/messari/network-polygon) [![Network Cronos](./docs/images/chains/cronos.png)](https://graph.cronoslabs.com/subgraphs/name/messari/network-cronos) |
| Cosmos | 🛠 | 1.1.1 / 1.1.2 / 1.0.0 | [![Network Cosmos](./docs/images/chains/cosmos.png)](https://thegraph.com/hosted-service/subgraph/messari/network-cosmos) [![Network Osmosis](./docs/images/chains/osmosis.png)](https://thegraph.com/hosted-service/subgraph/messari/network-osmosis) [![Network Juno](./docs/images/chains/juno.png)](https://thegraph.com/hosted-service/subgraph/messari/network-juno) |
| NEAR | 🛠 | 1.1.1 / 1.1.2 / 1.0.0 | [![Network Near](./docs/images/chains/near.png)](https://thegraph.com/hosted-service/subgraph/messari/network-near) |
| Arweave | 🛠 | 1.1.1 / 1.1.2 / 1.0.0 | [![Network Arweave](./docs/images/chains/arweave.png)](https://thegraph.com/hosted-service/subgraph/messari/network-arweave-mainnet) |
| **ERC20 Subgraphs** | | |
| ERC20 Tokens (2017) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC20 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc20-holders-2017) |
| ERC20 Tokens (2018) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC20 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc20-holders-2018) |
| ERC20 Tokens (2019) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC20 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc20-holders-2019) |
| ERC20 Tokens (2020) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC20 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc20-holders-2020) |
| ERC20 Tokens (2021) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC20 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc20-holders-2021) |
| ERC20 Tokens (2022) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC20 Ethereum](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc20-holders-2022) |
| **ERC721 Subgraphs** | | |
| ERC721 Holders | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC721 Holders](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc721-holders) |
| ERC721 Metadata | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![ERC721 Metadata](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/erc721-metadata) |
| **NFT Marketplace Subgraphs** | | |
| OpenSea v1 (Wyvern Exchange) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![OpenSea v1](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/opensea-v1-ethereum) |
| OpenSea v2 (Wyvern Exchange) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![OpenSea v2](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/opensea-v2-ethereum) |
| OpenSea (Seaport) | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![OpenSea Seaport](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/opensea-seaport-ethereum) |
| LooksRare | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![LooksRare](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/looksrare-ethereum) |
| Sudoswap | 🔨 | 1.0.0 / 1.0.0 / 1.0.0 | |
| X2Y2 | 🛠 | 1.0.0 / 1.0.0 / 1.0.0 | [![X2Y2](./docs/images/chains/ethereum.png)](https://thegraph.com/hosted-service/subgraph/messari/x2y2-ethereum) |

† Versions are schema version, subgraph version, methodology version respectively
