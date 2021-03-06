---
title: OpenXR の概要
description: Windows Mixed Reality と HoloLens 2 ヘッドセットでポータブル OpenXR API 標準を使用する方法については、こちらをご覧ください。
author: thetuvix
ms.author: alexturn
ms.date: 2/28/2020
ms.topic: article
keywords: OpenXR、Khronos、BasicXRApp、Windows Mixed Reality OpenXR 開発者ツール、DirectX、ネイティブ、ネイティブアプリ、カスタムエンジン、ミドルウェア、作業の開始、101、プレビュー拡張機能、OpenXR ランタイムバージョン、システム状態
ms.openlocfilehash: e09ff2748921789d74bafdb321f19882336ea500
ms.sourcegitcommit: 3c32f45fd941767d408cccc5a76f1ff1cec763da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86879235"
---
# <a name="getting-started-with-openxr"></a>OpenXR の概要

デスクトップ上の HoloLens 2 または Windows Mixed Reality の OpenXR を使用して開発することができます。  ヘッドセットへのアクセス権がない場合は、代わりに HoloLens 2 エミュレーターまたは Windows Mixed Reality シミュレーターを使用できます。

## <a name="getting-started-with-openxr-for-hololens-2"></a>OpenXR for HoloLens 2 の概要

HoloLens 2 用の OpenXR アプリケーションの開発を開始するには:

1. HoloLens 2 をセットアップするか、「 [hololens 2 エミュレーターの最新バージョンをインストール](using-the-hololens-emulator.md)するには」の手順に従います。  デバイスが最近 OS を更新した場合、または最近のエミュレーターイメージを使用している場合は、既に OpenXR 1.0 を準備しておく必要があります。
1. すべての[拡張機能](openxr.md#roadmap)を備えた最新の OpenXR ランタイムがあることを確認するには、デバイスまたはエミュレーター内から**ストア**アプリを起動し、右上のメニューを開き、[**ダウンロードと更新**] をクリックし、[**更新プログラムの取得**] をクリックします。  これにより、HoloLens の OpenXR ランタイムが最新の状態に保たれます。  エミュレーターを使用している場合は、エミュレーターイメージを起動するたびにエミュレーターイメージがリセットされるため、最善の方法は、 [HoloLens 2 エミュレーターイメージの最新バージョン](using-the-hololens-emulator.md)があることを確認することだけです。

## <a name="getting-started-with-openxr-for-windows-mixed-reality-headsets"></a>OpenXR for Windows Mixed Reality ヘッドセットの概要

イマーシブ Windows Mixed Reality ヘッドセット用の OpenXR アプリケーションの開発を開始するには:

1. 少なくとも Windows 10 2019 更新プログラム (1903) を実行していることを確認してください。これは、Windows Mixed Reality エンドユーザーが OpenXR アプリケーションを実行するための最小要件です。  以前のバージョンの Windows 10 を使用している場合は、 <a href="https://www.microsoft.com/software-download/windows10" target="_blank">windows 10 Update Assistant</a>を使用してアップグレードできます。
2. Windows Mixed reality ヘッドセットを設定するか、指示に従って[Windows Mixed reality シミュレーターを有効](using-the-windows-mixed-reality-simulator.md)にします。

これで完了です。  Windows mixed Reality OpenXR ランタイムがインストールされ、すべての Windows Mixed Reality ユーザーに対して自動的にアクティブになります。  Microsoft Store は、ランタイムを最新の状態に保ちます。

Windows Mixed Reality OpenXR Runtime を再びアクティブにする必要がある場合は、[スタート] メニューから Mixed Reality ポータルを起動し、[...]] をクリックし、[OpenXR の設定] を選択します。  そのメニュー項目がない場合、OpenXR ランタイムは既にアクティブになっています。<br>
![Mixed Reality ポータルでの OpenXR の設定](images/mixed-reality-portal-set-up-openxr.png)

## <a name="getting-the-windows-mixed-reality-openxr-developer-tools"></a>Windows Mixed Reality OpenXR 開発者ツールの取得

Windows Mixed Reality OpenXR Runtime を試すには、 <a href="https://www.microsoft.com/store/productId/9n5cvvl23qbt" target="_blank">Mixed Reality OpenXR 開発者ツールアプリ</a>をインストールします。  このアプリは、OpenXR のさまざまな機能を、アクティブなランタイムと現在のヘッドセットに関する重要な情報を提供するシステムステータスページと共に実行するデモシーンを提供します。

HoloLens 2 のエミュレーターを使用する場合、Mixed Reality OpenXR 開発者ツールをインストールする最も簡単な方法は、 [Windows デバイスポータル](using-the-windows-device-portal.md)を使用することです。これを行うには、"OpenXR" ページに移動し、[開発者機能] の下にある [インストール] ボタンをクリックします。 (これは、物理 HoloLens 2 デバイスでも同様に機能します)。

![Mixed Reality OpenXR 開発者ツールアプリ](images/mixed-reality-openxr-developer-tools.png)

## <a name="building-a-sample-openxr-app"></a>サンプル OpenXR アプリのビルド

OpenXR の開発に必要なツールをまだインストールしていない場合は[、必ずインストール](install-the-tools.md)してください。

<a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a> プロジェクトでは、2 つの Visual Studio プロジェクト ファイルにより OpenXR の簡単な例が示されています。1 つは Win32 デスクトップ アプリ、もう 1 つは UWP HoloLens 2 アプリ向けです。  ソリューションには HoloLens UWP プロジェクトが含まれているため、Visual Studio にインストールされた[ユニバーサル Windows プラットフォームの開発ワークロード](install-the-tools.md#installation-checklist)を完全に開く必要があります。

Win32 と UWP のプロジェクトファイルは、パッケージ化と配置の違いによって分離されていますが、各プロジェクト内のアプリコードはほぼ同じであることに注意してください。

OpenXR Win32 デスクトップを構築した後。EXE を使用して、OpenXR をサポートする任意の desktop VR プラットフォームの VR ヘッドセットと共に使用できます。これは、Windows Mixed Reality ヘッドセットであるか、他のヘッドセットであるかどうかによって異なります。

OpenXR UWP アプリケーションパッケージをビルドした後、[そのパッケージ](using-visual-studio.md)を hololens 2 デバイスまたは Hololens 2 エミュレーターにデプロイできます。

## <a name="integrate-the-openxr-loader-into-a-project"></a>OpenXR loader をプロジェクトに統合する

既存のプロジェクトで OpenXR の使用を開始するには、OpenXR ローダーを追加します。  ローダーは、デバイス上のアクティブな OpenXR ランタイムを検出し、実装するコア関数および拡張関数へのアクセスを提供します。

[公式の OpenXR NuGet パッケージ](#reference-official-openxr-nuget-package)を Visual Studio プロジェクトから参照するか、Khronos GitHub リポジトリから[公式の OpenXR loader ソースを含める](#include-official-openxr-loader-source)ことができます。  どちらの方法を使用しても、OpenXR 1.0 のコア機能に加えて、公開された拡張機能にアクセスでき `KHR` `EXT` `MSFT` ます。

`MSFT_preview`拡張機能も試してみる場合は、Mixed Reality github リポジトリから[preview OpenXR ヘッダーをコピー](#using-preview-extensions)することができます。

### <a name="reference-official-openxr-nuget-package"></a>公式 OpenXR NuGet パッケージの参照

<a href="https://www.nuget.org/packages/OpenXR.Loader/" target="_blank"> **OpenXR** NuGet パッケージ</a>は、事前に構築された OpenXR ローダーを参照する最も簡単な方法です。Visual Studio C++ ソリューションの DLL。  これにより、OpenXR 1.0 のコア機能に加えて、公開された拡張機能にアクセスできるようになり `KHR` `EXT` `MSFT` ます。

OpenXR NuGet パッケージ参照を Visual Studio C++ ソリューションに追加するには、次のようにします。
1. **ソリューションエクスプローラー**で、OpenXR を使用するプロジェクトを右クリックし、[ **NuGet パッケージの管理...**] を選択します。
1. [**参照**] タブに切り替えて、 **OpenXR**を検索します。
1. **OpenXR**パッケージを選択し、右側の詳細ウィンドウで [インストール] をクリックします。
1. [OK] をクリックして、プロジェクトへの変更を受け入れます。
1. `#include <openxr/openxr.h>`OPENXR API の使用を開始するには、ソースファイルにを追加します。

動作中の OpenXR API の例については、 <a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a>サンプルアプリを参照してください。

### <a name="include-official-openxr-loader-source"></a>公式の OpenXR loader ソースを含める

たとえば、追加のローダーを避けるために、ローダーを自分でビルドする場合。DLL を使用して、公式の Khronos OpenXR loader ソースをプロジェクトに取り込むことができます。  これにより、OpenXR 1.0 のコア機能に加えて、公開された拡張機能にアクセスできるようになり `KHR` `EXT` `MSFT` ます。

ここで作業を開始するには、 <a href="https://github.com/KhronosGroup/OpenXR-SDK" target="_blank">GitHub の Khronos OpenXR リポジトリ</a>に記載されている手順に従ってください。  プロジェクトは CMake でビルドするように設定されています-MSBuild を使用している場合は、独自のプロジェクトにコードをコピーする必要があります。

## <a name="using-preview-extensions"></a>プレビュー拡張機能の使用

`MSFT_preview`[拡張機能のロードマップ](openxr.md#roadmap)に記載されている拡張機能は、フィードバックを収集するためにプレビューされている試験的なベンダーの拡張機能です。  これらの拡張機能は開発者向けデバイスのみを対象としており、実際の拡張機能が出荷されると削除されます。

使用可能な拡張機能を試すには `MSFT_preview` 、次の手順に従ってプロジェクトを更新します。
1. 上記のいずれかの方法に従って、OpenXR loader をプロジェクトに統合します。
1. プロジェクトの標準の OpenXR ヘッダーを、 <a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/openxr_preview/include/openxr" target="_blank">GitHub の Mixed Reality OpenXR リポジトリのプレビューヘッダー</a>に置き換えます。

次に、ターゲット HoloLens 2 またはデスクトップ PC でプレビュー拡張機能のサポートを有効にします。
  1. すべての[拡張機能](openxr.md#roadmap)を備えた最新の OpenXR ランタイムがあることを確認するには、対象のデバイスまたはエミュレーター内から**ストア**アプリを起動し、右上のメニューを開き、[**ダウンロードと更新**] をクリックして、[**更新プログラムの取得**] をクリックします。
  1. ターゲットデバイスで Windows デバイスポータルを有効にする:
     * ターゲットデバイスが HoloLens 2 デバイスの場合は、ターゲットデバイスで[次の手順を実行](using-the-windows-device-portal.md)します。  HoloLens 2 エミュレーターの既知の問題により、次の手順の UI がエミュレーターに表示されなくなるため、これには物理ヘッドセットが必要であることに注意してください。
     * ターゲットデバイスが、イマーシブヘッドセット周辺機器が接続されているデスクトップ PC の場合は、ターゲットのデスクトップ PC で<a href="https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-desktop#set-up-device-portal-on-windows-desktop" target="_blank">次の手順に従い</a>ます。
  1. 左ペインの [ **OpenXR** ] タブに移動し、[ **latest preview OpenXR runtime の使用**] を有効にします。  これにより、プレビューの拡張機能がアクティブ化されたデバイスでプレビューランタイムが有効になります。
     ![デバイスポータル OpenXR preview runtime チェックボックス](images/device-portal-openxr-preview-runtime.png)
  1. [Windows Mixed Reality 開発者ツール OpenXR](openxr-getting-started.md#getting-the-windows-mixed-reality-openxr-developer-tools)の [**システムステータス**] タブに表示されている**ランタイムバージョン**が、試してみる予定のプレビュー拡張機能の必要なバージョンと一致することを確認します。  その場合は、**拡張機能の一覧に**拡張機能が表示されます。  安定した拡張機能を使用できるようになると、そのプレビュー拡張機能が削除されることに注意してください。<br />
     ![Mixed Reality OpenXR 開発者ツール app System Status タブ](images/mixed-reality-openxr-developer-tools-status.png)

これらのプレビュー拡張機能のドキュメント、およびそれらの使用方法のサンプルについては、「 <a href="https://github.com/microsoft/OpenXR-MixedReality#openxr-preview-extensions" target="_blank">Mixed Reality OpenXR リポジトリ</a>」を参照してください。

## <a name="troubleshooting"></a>トラブルシューティング

OpenXR の開発に関する問題が発生した場合は、[トラブルシューティングのヒント](openxr-troubleshooting.md)を確認してください。