---
title: 1. はじめに
description: Unreal Engine 4 と Mixed Reality ツールキット UX ツール プラグインを使用して簡単なチェス アプリを構築するためのチュートリアル シリーズのパート 6 の 1
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, Mixed Reality, チュートリアル, 入門, mrtk, uxt, UX ツール, ドキュメント
ms.openlocfilehash: 39e4e7218341dcc69eacf01f43b5e0721e76031b
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720378"
---
# <a name="1-getting-started"></a>1.はじめに

Mixed Reality を初めて使用する場合でも、経験豊富なプロの方でも、[HoloLens 2](https://docs.microsoft.com/windows/mixed-reality/) と [Unreal Engine](https://www.unrealengine.com/en-US/) を使用して体験を始めることができます。 このチュートリアル シリーズでは、[Unreal 用 Mixed Reality ツールキット](https://github.com/microsoft/MixedRealityToolkit-Unreal)の一部である [UX ツール プラグイン](https://github.com/microsoft/MixedReality-UXTools-Unreal)を使用してインタラクティブなチェス アプリを構築する方法をステップごとに説明します。 プラグインは、コード、ブループリント、例を使用してプロジェクトに一般的な UX 機能を追加するのに役立ちます。 

![ビューポートの終わりのシーン](images/unreal-uxt/5-endscene.PNG)

シリーズが完了するまでに、次のことを実際に体験できます。
* 新しいプロジェクトの開始
* Mixed Reality 用の設定
* ユーザー入力の操作
* ボタンの追加
* エミュレーターまたはデバイスでの再生

ご不明な点がある場合は、[Unreal 開発の概要](https://docs.microsoft.com/windows/mixed-reality/unreal-development-overview)を確認してください。

## <a name="prerequisites"></a>前提条件
ジャンプする前に、次の要件を満たしていることを確認してください。
* Windows 10 1809 以降
* Windows 10 SDK 10.0.18362.0 以降
* [Unreal Engine](https://www.unrealengine.com/en-US/get-now) 4.25 以降
* [開発用に構成された](using-visual-studio.md#enabling-developer-mode) Microsoft HoloLens 2 デバイスまたはエミュレーター
* 以下のワークロードを含む Visual Studio 2019

### <a name="installing-visual-studio-2019"></a>Visual Studio 2019 のインストール
最後の手順は、次のように Visual Studio をセットアップすることです。
1. [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) の最新バージョンのインストール
2. 次の[ワークロード](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-workloads)をインストールします。
    * C++ によるデスクトップ開発
    * .NET デスクトップ開発
    * ユニバーサル Windows プラットフォームの開発

3. 次の[コンポーネント](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-individual-components)をインストールします。
    * コンパイラ、ビルド ツール、ランタイム > MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (最新バージョン)

以上で作業は終了です。 これで、チェス アプリ プロジェクトを開始するためのすべての設定が完了しました。

[次のセクション: 2.プロジェクトと最初のアプリケーションの初期化](unreal-uxt-ch2.md)