---
title: ツールのインストール
description: ここでは Mixed Reality の開発の準備を開始します。 この記事では、HoloLens および Windows Mixed Reality のイマーシブ ヘッドセット開発に推奨される Unity、Visual Studio、その他のツールの最新バージョンが常に反映されています。
author: thetuvix
ms.author: alexturn
ms.date: 07/31/2020
ms.topic: article
ms.localizationpriority: high
keywords: 最新, ツール, はじめに, 基本, unity, visual studio, ツールキット
ms.openlocfilehash: f5c779aa0bb89fe66b53419b03ec1b4d3e6b562b
ms.sourcegitcommit: ef0bf03833eda826ed0b884859b4573775112aba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87476902"
---
# <a name="install-the-tools"></a>ツールのインストール

Microsoft HoloLens および Windows Mixed Reality イマーシブ (VR) ヘッドセット用のアプリケーションを構築するために必要なツールを取得します。 Windows Mixed Reality 開発用の別個の SDK はありません。Windows 10 SDK と一緒に Visual Studio をご使用ください。

Mixed Reality デバイスをお持ちでない場合はどのようにしたらよいでしょうか。 HoloLens なしで Mixed Reality アプリの機能をテストするために、[HoloLens エミュレーター](using-the-hololens-emulator.md)をインストールすることができます。 [Windows Mixed Reality シミュレーター](using-the-windows-mixed-reality-simulator.md)を使用して、イマーシブ ヘッドセット用の Mixed Reality アプリをテストすることもできます。 Unity を使用している場合は、[Mixed Reality Toolkit (MRTK)](https://github.com/Microsoft/MixedRealityToolkit-Unity) の入力シミュレーションを使用して、ハンドトラッキングや視線追跡入力などのさまざまな種類の入力操作をテストできます。

Mixed Reality アプリの作成を開始する最も簡単な方法として、Unity ゲーム エンジンをインストールすることをお勧めします。 ただし、カスタム エンジンを使用する場合は、DirectX に対してビルドすることもできます。

>[!TIP]
>このページをブックマークに登録して定期的にチェックし、Mixed Reality 開発に推奨される各ツールの最新バージョンを常に最新の状態に保ってください。

<br>

## <a name="installation-checklist"></a>インストールのチェックリスト


| ツール | メモ |
|---------|---------|
| ![Windows ロゴ](images/Windows10_logo.png)<br><br><a href="https://www.microsoft.com/software-download/windows10" target="_blank">**Windows 10** (手動インストールのリンク)</a><br><br>お使いの PC のオペレーティング システムが、Mixed Reality アプリケーションの構築対象プラットフォームと一致するように、Windows 10 の最新バージョンをインストールしてください。  | **Windows 10 のインストール** <br> [設定] の [Windows Update] を利用するか、インストール メディアを作成して (左の列のリンクを使用して)、Windows 10 の最新バージョンをインストールできます。 <br><br>Windows 10 の各リリースで使用可能な最新の Mixed Reality 機能については、[最新のリリース ノート](release-notes-october-2018.md)を参照してください。 [設定] > [更新とセキュリティ] > [開発者向け] から、**PC で開発者モードを有効にします**。 <br><br> **エンタープライズ管理および会社管理の PC の場合の注意事項**<br>お使いの PC が組織の IT 部門によって管理されている場合、更新するために管理者への連絡が必要な場合があります。 <br><br> **Windows の 'N' バージョン**<br> Windows Mixed Reality イマーシブ (VR) ヘッドセットは、Windows の 'N' バージョンではサポートされていません。 |
| ![Visual Studio のロゴ](images/visualstudio_logo.png)<br><br><a href="https://visualstudio.microsoft.com/downloads/" target="_blank">**Visual Studio 2019 (16.2 以降)** (インストールのリンク)</a> <br><br>完全な機能を備えた Windows などの統合開発環境 (IDE) です。 コードの記述、デバッグ、テスト、配置には、Visual Studio を使用します。 | 次のワークロードをインストールします。 <br><br>**● C++ によるデスクトップ開発**<br>**● ユニバーサル Windows プラットフォーム (UWP) の開発**<br><br>HoloLens 向けの開発を行う場合は、UWP ワークロード内に次のオプションのコンポーネントがあることを確認してください。<br><br>**● USB デバイスの接続**<br><br>**Unity に関する注意事項**<br>特定の目的のために意図的により新しいバージョンの (LTS 以外の) Unity をインストールしようとしているのでなければ、Visual Studio のインストールの一部として Unity ワークロードをインストールする "*のではなく*"、下記のように **Unity 2019 LTS** ストリームをインストールすることをお勧めします。<br><br>**注:**<br>Visual Studio 2019 バージョン 16.0 での Mixed Reality アプリのデバッグに関して既知の問題がいくつかあります。  必ず、**Visual Studio 2019 バージョン 16.2 以降**に更新してください。 |
| ![Windows ロゴ](images/Windows10_logo.png)<br><br><a href="https://developer.microsoft.com//windows/downloads/windows-10-sdk" target="_blank">**Windows 10 SDK (10.0.18362.0)** (手動インストールのリンク)</a> <br><br>HoloLens 2 で Windows 10 アプリを作成するための最新のヘッダー、ライブラリ、メタデータ、ツールが用意されています。 | **HoloLens 2 アプリを構築するには、ビルド 18362 以降の Windows SDK をインストールする必要があります。**<br> <br> デスクトップの Windows Mixed Reality ヘッドセットまたは HoloLens (第 1 世代) 用のアプリケーションのみを開発している場合は、Visual Studio 2017 によってインストールされた Windows SDK を使用することができます。 |
| ![Visual Studio のロゴ](images/HoloLensIcon.jpg)<br><br><a href="https://go.microsoft.com/fwlink/?linkid=2132415" target="_blank">**HoloLens 2 エミュレーター (Windows Holographic バージョン 2004、2020 年 6 月の更新プログラム)** (インストール リンク:10.0.19041.1106)</a><br> <br><a href="https://go.microsoft.com/fwlink/?linkid=2065980" target="_blank">**HoloLens (第 1 世代) エミュレーター** (インストールのリンク:10.0.17763.134)</a> <br><br>エミュレーターを使用すると、物理的な HoloLens を使用せずに、HoloLens 仮想マシン イメージ上でアプリケーションを実行できます。<br> <br> | エミュレーターの使用を開始する方法については、「[Using the HoloLens emulator (HoloLens エミュレーターを使用する)](using-the-hololens-emulator.md)」を参照してください。<br> <br> エミュレーターのインストールを成功させるには、**ご使用のシステムが Hyper-V をサポートしている必要があります**。 詳細については、以下の「システム要件」セクションを参照してください。 <br>|

## <a name="choose-your-engine"></a>エンジンの選択

これで、Windows 10、Visual Studio、Windows 10 SDK の準備ができました。次に、構築の基盤となるエンジンを選択します。 

[!INCLUDE[](~/includes/tools-overview.md)]
