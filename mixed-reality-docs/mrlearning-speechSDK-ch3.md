---
title: Azure Speech Services のチュートリアル - 3. Azure Cognitive Services の Speech Translation コンポーネントの追加
description: このコースでは、Mixed Reality アプリケーション内で Azure Speech SDK を実装する方法を学習します。
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: d8e73e24f0522ff71b95ea1886d59893216b0597
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "79028341"
---
# <a name="3-adding-the-azure-cognitive-services-speech-translation-component"></a>3.Azure Cognitive Services の Speech Translation コンポーネントの追加

このチュートリアルでは、Speech Translation をプロジェクトに追加します。これにより、音声を 3 つの異なる言語に翻訳して書き起こすことができます。

## <a name="objectives"></a>目標

* Azure Speech Translation を統合する方法を学習する

## <a name="instructions"></a>手順

[Hierarchy]\(階層\) ウィンドウで **Lunarcom** オブジェクトを選択し、[Inspector]\(インスペクター\) ウィンドウで **[Add Component]\(コンポーネントの追加\)** ボタンを使用して、**Lunarcom Translation Recognizer (Script)** コンポーネントを Lunarcom オブジェクトに追加し、次のように構成します。

* **[Target Language]\(対象言語\)** を選択した言語 (たとえば、[_German_]\(ドイツ語\)) に変更します。

![mrlearning-speech](images/mrlearning-speech/tutorial3-section1-step1-1.png)

> [!NOTE]
> Lunarcom Translation Recognizer (Script) コンポーネントは MRTK の一部ではありません。 このチュートリアルのアセットと共に提供されました。

ゲーム モードに入ったら、まずサテライト ボタンを押して音声翻訳をテストすることができます。 次に、お使いのコンピューターにマイクがあると仮定して、何かを話すと、選択した言語に音声が翻訳されて、ターミナルのパネル上に文字で表示されます。

![mrlearning-speech](images/mrlearning-speech/tutorial3-section1-step1-2.png)

> [!CAUTION]
> アプリケーションは Azure に接続する必要があるため、お使いのコンピューター/デバイスがインターネットに接続されていることを確認してください。

## <a name="congratulations"></a>結論

プロジェクトでは、話した言葉を複数の異なる言語に正常に翻訳できるようになりました。 デバイスでアプリケーションを実行して、機能が適切に動作していることを確認してください。

[次のチュートリアル: 4.インテントの設定と自然言語の理解](mrlearning-speechSDK-ch4.md)
