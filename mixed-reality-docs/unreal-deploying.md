---
title: Unreal でのデバイスへのデプロイ
description: 非 Real から HoloLens 2 にデバイスを展開するためのガイド
author: sw5813
ms.author: suwu
ms.date: 7/10/2020
ms.topic: article
keywords: Unreal、Unreal Engine 4、UE4、HoloLens、HoloLens 2、mixed reality、デバイスへのデプロイ、PC、ドキュメント
appliesto:
- HoloLens 2
ms.openlocfilehash: 2d0cd67db79c1970695334d826fbbaf0f2f92ec0
ms.sourcegitcommit: 2813f5b3027d47f7c6e9772338935eeccfa2aaec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86408180"
---
# <a name="deploy-to-device-in-unreal"></a>Unreal でのデバイスへのデプロイ

## <a name="overview"></a>概要
HoloLens 2 に Unreal アプリケーションを展開するには、次の2つの方法があります。 
* Unreal エディターから直接
* デバイスポータルを使用してアップロードされたパッケージとして

どちらのオプションでも、開発用の[デバイスポータル](using-the-windows-device-portal.md)を使用するように HoloLens を設定する必要があります。 

## <a name="deploying-to-device-from-the-unreal-editor"></a>Unreal エディターからデバイスへの配置

1. [**起動**] ボタンの横にあるドロップダウン矢印をクリックします。 最初は、HoloLens デバイスオプションが淡色表示になります。

![起動ドロップダウンオプション](images/unreal/launch-dropdown.png)

2. **デバイスマネージャー**を開きます。 HoloLens はデバイスの一覧に自動的に表示されないことに注意してください。

3. [**一覧にないデバイスの追加**] セクションを展開します。

4. **プラットフォーム**として**HoloLens**を選択します。

5. デバイスの IP アドレスとポート情報を、デバイス id としてコロンで区切って入力します。 たとえば、"127.0.0.1: 10080" (USB 経由で接続されている場合) などです。 デバイスポータルのユーザー名とパスワードの資格情報を使用します。

6. [**追加**] をクリックし、デバイスマネージャーを閉じます。 
    * エラー (アドレス、ユーザー名、パスワードなど) が間違っている場合は、メッセージが出力ログに出力されます。

![一覧にないデバイスの追加](images/unreal/add-unlisted-device.png)

7. [**起動**] ボタンの横にあるドロップダウン矢印をもう一度クリックすると、追加した HoloLens デバイスが表示されます。 Hololens にビルドしてデプロイする HoloLens デバイスを選択します。 

>[!NOTE]
>デバイスのビルドには、シェーダーの再コンパイルが含まれる場合があります (特に最初の実行時)。これには時間がかかることがあります。 デバイスは、アプリが実行されるまでスリープ状態にならないようにしてください (磨耗が必要な場合があります)。 それ以外の場合、シェーダーのコンパイルは失敗します。

## <a name="deploying-to-device-via-device-portal"></a>デバイスポータルを使用したデバイスへの展開

[アプリのパッケージ化とデプロイ](unreal-uxt-ch6.md#packaging-and-deploying-the-app-via-device-portal)に関する詳細な手順については、「unreal チュートリアルシリーズを使用したはじめに」の最後のセクションを参照してください。
