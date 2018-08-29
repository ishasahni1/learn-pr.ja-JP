Jim は、会社の Web インフラストラクチャで実行されている Azure 仮想マシンのセットを管理しています。このインフラストラクチャには、複数の Web サイトとさまざまなプラットフォームで実行されているデータベース サーバーが含まれます。 

Azure portal は使いやすいですが、さまざまなブレードを移動することにより、一部のタスクに余分な時間がかかっていることに Jim は気付いています。 

代替手段を検討しているときに、彼は Azure CLI ツールを見つけました。

Azure CLI を使用することで、Jim はスクリプトを記述して、サーバーの状態の確認、新しい構成の展開、ポートのオープン、または仮想マシンに接続して設定を変更できるようになりました。

もしかしたら、あなたも Jim のようにクラウド環境内のタスクを自動化するためのツールを探しているのではないでしょうか。 Azure CLI を使用して、Azure でホストされている仮想マシンを作成および管理する方法を説明します。 

## <a name="azure-cli"></a>Azure CLI

Azure CLI は、Azure リソースを管理するための、Microsoft のクロスプラットフォーム コマンド ライン ツールです。 このツールは、macOS、Linux、および Windows で使用できます。またはブラウザーで [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) を使用して使用できます。

> [!IMPORTANT]
> 現在使用できる Azure CLI ツールには、Azure CLI 1.0 と Azure CLI 2.0 の 2 つのバージョンがあります。 ここでは最新バージョンである Azure CLI 2.0 を使用します。1.0 用に記述されたレガシ スクリプトを実行している場合を除き、こちらを使用することをお勧めします。 Azure CLI 1.0 は、`azure` コマンドで始まり、Azure CLI 2.0 は、`az` コマンドで始まります。 

Azure CLI では、コマンドラインからまたはスクリプトで仮想マシンやディスクなどの Azure リソースを管理するのに役立ちます。 始めて、その機能を確認しましょう。

## <a name="learning-objectives"></a>学習の目的
> [!div class="checklist"]
> * CLI を使用して Azure 仮想マシンを作成する
> * CLI を使用して VM のサイズを変更する
> * コマンドラインから VM の管理とクエリを行う
> * VM にソフトウェアをインストールする