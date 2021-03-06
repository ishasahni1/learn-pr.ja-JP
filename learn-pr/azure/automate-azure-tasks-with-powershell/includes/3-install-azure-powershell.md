あなたが自動化ソリューションとして Azure PowerShell を選択したとします。 管理者は、Azure Cloud Shell ではなくローカルでスクリプトを実行しようとします。 チームは、Linux、macOS、および Windows を実行するマシンを使用しています。 これらのすべてのデバイスで Azure PowerShell が実行される必要があります。 

## <a name="what-must-be-installed"></a>何をインストールしなければならないでしょう。
次のユニットでは、実際のインストール手順について説明しますが、ここで Azure PowerShell を構成する 2 つのコンポーネントを見てみましょう。

- **ベース PowerShell 製品**: これには、Windows 上の PowerShell と、macOS および Linux 上の PowerShell Core という 2 つのバリエーションがあります。
- **Azure PowerShell モジュール**: PowerShell に Azure 固有のコマンドを追加するには、この追加のモジュールをインストールする必要があります。

> [!NOTE]
> PowerShell は Windows に含まれています (ただし、更新プログラムを適用できる場合があります)。 Linux および macOS では、PowerShell Core をインストールする必要があります。

ベース製品がインストールされたら、インストールに Azure PowerShell モジュールを追加します。

## <a name="how-to-install-powershell-core"></a>PowerShell Core をインストールする方法
Linux および macOS では、パッケージ マネージャーを使用して PowerShell Core をインストールします。 推奨されるパッケージ マネージャーは、OS とディストリビューションによって異なります。

> [!NOTE]
> PowerShell Core は Microsoft リポジトリ内で利用できるので、まずパッケージ マネージャーにそのリポジトリを追加する必要があります。

### <a name="linux"></a>Linux
Linux では、選択した Linux ディストリビューションに基づいてパッケージ マネージャーが変更されます。

| ディストリビューション  | パッケージ マネージャー |
|------------------|-----------------|
| Ubuntu、Debian   | `apt-get`       |
| Red Hat、CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
macOS では、`Homebrew` を使用して PowerShell Core をインストールします。

## <a name="how-to-install-azure-powershell"></a>Azure PowerShell をインストールする方法
PowerShell をインストールした後は、Azure PowerShell モジュールの推奨されるインストール方法として、PowerShell 内から `Install-Module` コマンドを使用します。 モジュールをインストールするには、昇格された特権が必要です。

- Windows では、PowerShell を管理者として実行する必要があります
- Linux および macOS では、`sudo` コマンドを使用して、昇格された特権を取得します

## <a name="summary"></a>まとめ
Windows では、PowerShell は組み込み済みですが、Azure PowerShell モジュールをインストールする必要があります。 Linux および macOS では、PowerShell Core と Azure PowerShell モジュールの両方をインストールする必要があります。 次のセクションでは、いくつかの一般的なプラットフォームでの詳細なインストール手順について説明します。