---
title: Linux への PowerShell Core のインストール
description: さまざまな Linux ディストリビューションへの PowerShell Core のインストールに関する情報
ms.date: 08/06/2018
ms.openlocfilehash: d60e1d5a89b6907b67c19b8cfcde969be156bd60
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851291"
---
# <a name="installing-powershell-core-on-linux"></a>Linux への PowerShell Core のインストール

[Ubuntu 14.04][u14]、[Ubuntu 16.04][u16]、[Ubuntu 18.10][u18]、[Debian 8][deb8]、[Debian 9][deb9]、[CentOS 7][cos]、[Red Hat Enterprise Linux (RHEL) 7][rhel7]、[OpenSUSE 42.3][opensuse]、[Fedora 27][fedora]、[Fedora 28][fedora]、[Arch Linux][arch] をサポートしています。

公式にサポートしていない Linux ディストリビューションの場合、[PowerShell Snap パッケージ][snap]を利用できます。
また、Linux [`tar.gz` アーカイブ][tar]で直接、PowerShell バイナリを展開できます。ただし、場合によっては、OS に基づいて依存関係を別の手順で設定する必要があります。

すべてのパッケージは GitHub [リリース][] ページにあります。
パッケージがインストールされたら、ターミナルから `pwsh` を実行します。

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u18]: #ubuntu-1810
[u18]: #ubuntu-1804
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-423
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a>プレビュー リリースのインストール

パッケージ リポジトリを介して、Linux 用の PowerShell Core Preview リリースをインストールすると、パッケージ名が `powershell` から `powershell-preview` に変わります。

直接ダウンロードによるインストールでは、ファイル名以外は変わりません。

さまざまなパッケージ マネージャーを使用して、安定したパッケージとプレビュー パッケージをインストールするためのコマンドを以下の表に示します。

|ディストリビューション|安定したコマンド | プレビュー コマンド |
|---------------|---------------|-----------------|
| Ubuntu、Debian |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| CentOS、RedHat |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| OpenSUSE |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| Fedora   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a>Ubuntu 14.04

### <a name="installation-via-package-repository---ubuntu-1404"></a>パッケージ リポジトリによるインストール - Ubuntu 14.04

Linux 向け PowerShell Core はパッケージ リポジトリに公開され、インストール (と更新) が簡単です。
この方法を使用することをお勧めします。

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

スーパーユーザーとして Microsoft リポジトリを登録します。
以降は、インストールの更新に `sudo apt-get upgrade powershell` を使用するだけで済みます。

### <a name="installation-via-direct-download---ubuntu-1404"></a>直接ダウンロードによるインストール - Ubuntu 14.04

Debian パッケージ `powershell_6.1.0-1.ubuntu.14.04_amd64.deb` を
[リリース][] ページから Ubuntu コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` コマンドは依存関係が満たされずに失敗します。
> 次のコマンド `apt-get install -f` でこれらの問題は解決され、PowerShell パッケージの構成が完了します。

### <a name="uninstallation---ubuntu-1404"></a>アンインストール - Ubuntu 14.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a>Ubuntu 16.04

### <a name="installation-via-package-repository---ubuntu-1604"></a>パッケージ リポジトリによるインストール - Ubuntu 16.04

Linux 向け PowerShell Core はパッケージ リポジトリに公開され、インストール (と更新) が簡単です。
この方法を使用することをお勧めします。

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

スーパーユーザーとして Microsoft リポジトリを一度登録すれば、その後は `sudo apt-get upgrade powershell` を使用する更新だけが必要になります。

### <a name="installation-via-direct-download---ubuntu-1604"></a>直接ダウンロードによるインストール - Ubuntu 16.04

Debian パッケージ `powershell_6.1.0-1.ubuntu.16.04_amd64.deb` を
[リリース][] ページから Ubuntu コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` コマンドは依存関係が満たされずに失敗します。
> 次のコマンド `apt-get install -f` でこれらの問題は解決され、PowerShell パッケージの構成が完了します。

### <a name="uninstallation---ubuntu-1604"></a>アンインストール - Ubuntu 16.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a>Ubuntu 18.04

> [!NOTE]
> Ubuntu 18.04 のサポートは `6.1.0-preview.2` 以降に追加されました。

### <a name="installation-via-package-repository---ubuntu-1804"></a>パッケージ リポジトリによるインストール - Ubuntu 18.04

Linux 向け PowerShell Core はパッケージ リポジトリに公開され、インストール (と更新) が簡単です。
この方法を使用することをお勧めします。

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

スーパーユーザーとして Microsoft リポジトリを一度登録すれば、その後は `sudo apt-get upgrade powershell` を使用する更新だけが必要になります。

### <a name="installation-via-direct-download---ubuntu-1804"></a>直接ダウンロードによるインストール - Ubuntu 18.04

Debian パッケージ `powershell_6.1.0-1.ubuntu.18.04_amd64.deb` を
[リリース][] ページから Ubuntu コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` コマンドは依存関係が満たされずに失敗します。
> 次のコマンド `apt-get install -f` でこれらの問題は解決され、PowerShell パッケージの構成が完了します。

### <a name="uninstallation---ubuntu-1804"></a>アンインストール - Ubuntu 18.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a>Ubuntu 18.10

> [!NOTE]
> Ubuntu 18.10 のサポートは `6.1.0-preview.3` 以降に追加されました。
> 18.10 はデイリー ビルドであるため、コミュニティのサポートのみです。

18.10 へのインストールは `snapd` を使用してサポートされます。 完全な手順については、「[Snap パッケージ][snap]」を参照してください。

## <a name="debian-8"></a>Debian 8

### <a name="installation-via-package-repository---debian-8"></a>パッケージ リポジトリによるインストール - Debian 8

Linux 向け PowerShell Core はパッケージ リポジトリに公開され、インストール (と更新) が簡単です。
この方法を使用することをお勧めします。

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

スーパーユーザーとして Microsoft リポジトリを一度登録すれば、その後は `sudo apt-get upgrade powershell` を使用する更新だけが必要になります。

### <a name="installation-via-direct-download---debian-8"></a>直接ダウンロードによるインストール - Debian 8

Debian パッケージ `powershell_6.1.0-1.debian.8_amd64.deb` を
[リリース][] ページから Debian コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo dpkg -i powershell_6.1.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` コマンドは依存関係が満たされずに失敗します。
> 次のコマンド `apt-get install -f` でこれらの問題は解決され、PowerShell パッケージの構成が完了します。

### <a name="uninstallation---debian-8"></a>アンインストール - Debian 8

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a>Debian 9

### <a name="installation-via-package-repository---debian-9"></a>パッケージ リポジトリによるインストール - Debian 9

Linux 向け PowerShell Core はパッケージ リポジトリに公開され、インストール (と更新) が簡単です。
この方法を使用することをお勧めします。

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl gnupg apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

スーパーユーザーとして Microsoft リポジトリを一度登録すれば、その後は `sudo apt-get upgrade powershell` を使用する更新だけが必要になります。

### <a name="installation-via-direct-download---debian-9"></a>直接ダウンロードによるインストール - Debian 9

Debian パッケージ `powershell_6.1.0-1.debian.9_amd64.deb` を
[リリース][] ページから Debian コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo dpkg -i powershell_6.1.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a>アンインストール - Debian 9

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a>CentOS 7

> [!NOTE]
> このパッケージは Oracle Linux 7 でも動作します。

### <a name="installation-via-package-repository-preferred---centos-7"></a>パッケージ リポジトリによるインストール (推奨) - CentOS 7

Linux 向け PowerShell Core は公式 Microsoft リポジトリに公開され、インストール (と更新) が簡単です。

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

スーパーユーザーとして Microsoft リポジトリを一度登録すれば、その後は `sudo yum update powershell` を使用する PowerShell の更新だけが必要になります。

### <a name="installation-via-direct-download---centos-7"></a>直接ダウンロードによるインストール - CentOS 7

[CentOS 7][] を使用して、RPM パッケージ `powershell-6.1.0-1.rhel.7.x86_64.rpm` を
[リリース][] ページから CentOS コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

ダウンロードという中間の手順なしでも RPM をインストールできます。

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a>アンインストール - CentOS 7

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a>Red Hat Enterprise Linux (RHEL) 7

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a>パッケージ リポジトリによるインストール (推奨) - Red Hat Enterprise Linux (RHEL) 7

Linux 向け PowerShell Core は公式 Microsoft リポジトリに公開され、インストール (と更新) が簡単です。

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

スーパーユーザーとして Microsoft リポジトリを一度登録すれば、その後は `sudo yum update powershell` を使用する PowerShell の更新だけが必要になります。

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a>直接ダウンロードによるインストール - Red Hat Enterprise Linux (RHEL) 7

RPM パッケージ `powershell-6.1.0-1.rhel.7.x86_64.rpm` を
[リリース][] ページから Red Hat Enterprise Linux コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

ダウンロードという中間の手順なしでも RPM をインストールできます。

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a>アンインストール - Red Hat Enterprise Linux (RHEL) 7

```sh
sudo yum remove powershell
```

## <a name="opensuse-423"></a>OpenSUSE 42.3

PowerShell Core をインストールすると、`zypper` から次のエラーが報告されることがあります。

```Output
Problem: nothing provides libcurl needed by powershell-6.1.0-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.1.0-1.rhel.7.x86_64
 Solution 2: break powershell-6.1.0-1.rhel.7.x86_64 by ignoring some of its dependencies
```

この場合、次のコマンドで `libcurl4` パッケージがインストール済みであることを確認して、互換性のある `libcurl` ライブラリが存在することを確認します。

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

次に、PowerShell パッケージをインストールするときに `break powershell-6.1.0-1.rhel.7.x86_64 by ignoring some of its dependencies` ソリューションを選択します。

### <a name="installation-via-package-repository-preferred---opensuse-423"></a>パッケージ リポジトリによるインストール (推奨) - OpenSUSE 42.3

Linux 向け PowerShell Core は公式 Microsoft リポジトリに公開され、インストール (と更新) が簡単です。

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Repository
zypper ar https://packages.microsoft.com/rhel/7/prod/

# Update the list of products
sudo zypper update

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-423"></a>直接ダウンロードによるインストール - OpenSUSE 42.3

[リリース][] ページから OpenSUSE コンピューターに RPM パッケージ `powershell-6.1.0-1.rhel.7.x86_64.rpm` をダウンロードします。

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

ダウンロードという中間の手順なしでも RPM をインストールできます。

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-423"></a>アンインストール - OpenSUSE 42.3

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a>Fedora

> [!NOTE]
> Fedora 28 は、PowerShell Core 6.1 以降でのみサポートされます。

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a>パッケージ リポジトリによるインストール (推奨) - Fedora 27、Fedora 28

Linux 向け PowerShell Core は公式 Microsoft リポジトリに公開され、インストール (と更新) が簡単です。

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install a system component
sudo dnf install compat-openssl10

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a>直接ダウンロードによるインストール - Fedora 27、Fedora 28

RPM パッケージ `powershell-6.1.0-1.rhel.7.x86_64.rpm` を
[リリース][] ページから Fedora コンピューターにダウンロードします。

次にターミナルで次を実行します。

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

ダウンロードという中間の手順なしでも RPM をインストールできます。

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a>アンインストール - Fedora 27、Fedora 28

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a>Arch Linux

> [!NOTE]
> Arch のサポートは試験段階です。

PowerShell は [Arch Linux][] User Repository (AUR) から入手できます。

* [タグが付けられた最新のリリース][arch-release]でコンパイルできます
* [最新のコミットからマスターに][arch-git]コンパイルできます
* [最新のリリース バイナリ][arch-bin]でインストールできます

AUR のパッケージはコミュニティにより保守管理されています。公式のサポートはありません。

AUR からパッケージをインストールする方法については、[Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) かコミュニティ [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile) をご覧ください。

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a>Snap パッケージ

### <a name="getting-snapd"></a>Snapd の取得

Snap を実行するには、`snapd` が必要です。
`snapd` がインストールされているかどうかを確認するには、[こちらの手順](https://docs.snapcraft.io/core/install)を使用してください。

### <a name="installation-via-snap"></a>Snap を使用したインストール

Linux 向け PowerShell Core は [Snap ストア](https://snapcraft.io/store)に公開されるため、インストール (と更新) が簡単です。
この方法を使用することをお勧めします。

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

Snap のインストールが自動的にアップグレードされた後も、`sudo snap refresh powershell-preview` を使用してアップグレードをトリガーすることができます。

### <a name="uninstallation"></a>アンインストール

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a>Kali

### <a name="installation"></a>インストール

```sh
# Download & Install prerequisites
wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu57_57.1-9_amd64.deb
dpkg -i libicu57_57.1-9_amd64.deb
apt-get update && apt-get install -y curl gnupg apt-transport-https

# Add Microsoft public repository key to APT
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

# Add Microsoft package repository to the source list
echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" | tee /etc/apt/sources.list.d/powershell.list

# Install PowerShell package
apt-get update && apt-get install -y powershell

# Start PowerShell
pwsh
```

### <a name="uninstallation---kali"></a>アンインストール - Kali

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a>Raspbian

> [!NOTE]
> Raspbian のサポートは試験段階です。

現在のところ、PowerShell は Raspbian Stretch でのみサポートされています。

また、Core CLR (と PowerShell Core) は Pi 2 および Pi 3 デバイス上でのみ動作します。これは、[Pi Zero](https://github.com/dotnet/coreclr/issues/10605) のような他のデバイスにはサポートされていないプロセッサが搭載されているためです。

[Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) をダウンロードし、[インストール手順](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)に従って Pi にインストールしてください。

### <a name="installation"></a>インストール

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.1.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

必要に応じて、"pwsh" バイナリへのパスを指定せずに、シンボリック リンクを作成して PowerShell を起動することができます

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a>アンインストール - Raspbian

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a>バイナリ アーカイブ

Linux プラットフォームで高度な展開シナリオを実行するために、PowerShell バイナリ `tar.gz` アーカイブが用意されています。

### <a name="dependencies"></a>依存関係

PowerShell はすべての Linux ディストリビューションに移植可能なバイナリをビルドします。
ただし、.NET Core ランタイムはディストリビューションごとに異なる依存関係を必要とします。PowerShell でも同じです。

次の表は、公式にサポートされている Linux ディストリビューションと .NET Core 2.0 の依存関係をまとめたものです。

| OS                 | 依存関係 |
| ------------------ | ------------ |
| Ubuntu 14.04       | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu52 |
| Ubuntu 16.04       | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu55 |
| Ubuntu 17.10       | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu57 |
| Ubuntu 18.04       | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu60 |
| Debian 8 (Jessie)  | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.0、libicu52 |
| Debian 9 (Stretch) | libc6、libgcc1、libgssapi-krb5-2、liblttng-ust0、libstdc++6、 <br> libcurl3、libunwind8、libuuid1、zlib1g、libssl1.0.2、libicu57 |
| CentOS 7 <br> Oracle Linux 7 <br> RHEL 7 <br> OpenSUSE OpenSUSE 42.3 | libunwind、libcurl、openssl-libs、libicu |
| Fedora 27 <br> Fedora 28 | libunwind、libcurl、openssl-libs、libicu、compat-openssl10 |

公式にサポートされていない Linux ディストリビューションで PowerShell バイナリを展開するには、別の手順で、ターゲット OS に必要な依存関係をインストールする必要があります。
たとえば、[Amazon Linux dockerfile][amazon-dockerfile] は依存関係を先にインストールし、それから Linux `tar.gz` アーカイブを抽出します。

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a>インストール - バイナリ アーカイブ

#### <a name="linux"></a>Linux

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.1.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.1.0

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.1.0/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a>バイナリ アーカイブのアンインストール

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a>パス

* `$PSHOME` は `/opt/microsoft/powershell/6.1.0/` です
* ユーザー プロファイルは `~/.config/powershell/profile.ps1` から読み込まれます
* 既定のプロファイルは `$PSHOME/profile.ps1` から読み込まれます
* ユーザー モジュールは `~/.local/share/powershell/Modules` から読み込まれます
* 共有モジュールは `/usr/local/share/powershell/Modules` から読み込まれます
* 既定のモジュールは `$PSHOME/Modules` から読み込まれます
* PSReadline 履歴は `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt` に記録されます

プロファイルは PowerShell のホスト別構成を順守します。そのため、既定のホスト固有プロファイルは同じ場所の `Microsoft.PowerShell_profile.ps1` にあります。

PowerShell は、Linux の [XDG ベース ディレクトリ仕様][xdg-bds]を尊重しています。

[リリース]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
