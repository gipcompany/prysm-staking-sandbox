# prysm-staking-sandbox

詳細は、以下のURLを参照してください。

https://docs.prylabs.network/docs/install/install-with-script#step-2-install-prysm

## 認証情報の作成

    ./prysm.sh beacon-chain generate-auth-secret

PrysmというEthereum 2.0クライアントのbeacon chainコンポーネントに対して、認証用のシークレットを生成する。
この情報は、jwt.hex というファイルに保存される。
これは、beacon chainノードが他のノードやクライアントと安全に通信するために必要な認証情報となる。

## geth のインストール

    brew install ethereum

## staking-deposit-cli のインストール

https://github.com/ethereum/staking-deposit-cli/releases

より環境毎のバイナリをダウンロードして、 staking-deposit-cli をインストールする。

## validator の作成

以下のコマンドは、Ethereum 2.0のステーキングに必要となるバリデータを作成するためのものである。
具体的には、`./bin/deposit`という実行ファイルを使用して、新しいニーモニックフレーズを生成し、そのフレーズを用いて1つのバリデータを作成する。
バリデータの数は`--num_validators=1`で指定されており、ニーモニックフレーズの言語は`--mnemonic_language=english`として英語が選ばれている。
また、`--chain=sepolia`により、セポリアテストネット用の設定が行われる。
但し、以下はmacOSの場合の例である。
Linuxの場合は、./bin 配下の別のバイナリを使用する。

    ./bin/deposit new-mnemonic --num_validators=1 --mnemonic_language=english --chain=sepolia

実行後、 ./validator_keys ディレクトリに *.json が作成される。


## validator アカウントのインポート

    ./prysm.sh validator accounts import --keys-dir=./validator_keys --sepolia

Prysmを使用して、バリデーターアカウントをインポートする。
これにより、 wallet path に指定されたディレクトリにあるバリデーターキーがインポートされる。


## validator wallet の作成

    ./prysm.sh validator wallet create --wallet-dir=./.my_wallet_dir

`Imported Wallet (Recommended)` と表示されるので、それを選択する。
password を入力すると、 wallet が作成される。



## Execution Client の起動

Geth（Go-Ethereum）を使用して、Sepoliaテストネットワーク上でノードを起動する。
Geth が Ethereum 2.0 ネットワークの Execution Layer として動作する。

    geth --sepolia --http --http.api=eth,net,engine,admin --authrpc.jwtsecret=./jwt.hex

## Consensus Client の起動

以下のコマンドにより、Consensus Layer への接続に成功し、Sepoliaテストネットワーク上で動作するbeacon chainノードが起動する。

    ./prysm.sh beacon-chain --accept-terms-of-use --execution-endpoint=http://localhost:8551 --sepolia --jwt-secret=./jwt.hex --checkpoint-sync-url=https://sepolia.beaconstate.info --genesis-beacon-api-url=https://sepolia.beaconstate.info

## validator の起動

    ./prysm.sh validator --sepolia  --wallet-dir=./.my_wallet_dir --wallet-password-file=./.wallet-password-file
