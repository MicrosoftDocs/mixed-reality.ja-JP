---
title: Unity Play モード
description: Unity エディターの再生モードを使用して、アプリをデプロイせずにデバイスでの変更をプレビューします。
author: jonmlyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, リモート処理, holographic リモート処理, holographic リモート処理プレーヤー
ms.openlocfilehash: dca7ffba1270802fcabed8a88fe7428ef2981553
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277560"
---
# <a name="unity-play-mode"></a>Unity Play モード

Unity プロジェクトですばやく作業を行うには、"Play Mode" を使用します。 これにより、PC の Unity エディターでアプリがローカルで実行されます。 Unity では、Holographic Remoting を使用して、実際の HoloLens デバイスでコンテンツをすばやくプレビューすることができます。 再生モードは、開発用 PC に接続されている Windows Mixed Reality ヘッドセットでも使用できます。

## <a name="unity-play-mode-with-holographic-remoting"></a>Holographic リモート処理を使用した Unity Play モード

Holographic リモート処理を使用すると、PC の Unity エディターでアプリを実行しながら、HoloLens でアプリを体験できます。 宝石、ジェスチャ、音声、および空間マッピングの入力は、HoloLens から PC に送信されます。 レンダリングされたフレームが HoloLens に返されます。 これは、完全なプロジェクトをビルドして配置することなく、アプリをすばやくデバッグできる優れた方法です。
1. HoloLens で、 **Microsoft Store**にアクセスし、 **[Holographic Remoting Player](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** アプリをインストールします。
2. HoloLens で、 **Holographic Remoting Player**アプリを起動します。
3. Unity で、 **[ウィンドウ]** メニューにアクセスし、 **[Holographic エミュレーション]** を選択します。
4. **エミュレーションモード**を**リモートからデバイスに**設定します。
5. **[リモートコンピューター]** には、HOLOLENS の IP アドレスを入力します。
6. **[接続]** をクリックします。 **接続の状態**が [接続済み] に変わり、HoloLens で画面が空白になって**いる**ことを確認します。
7. **[再生]** ボタンをクリックして再生モードを開始し、HoloLens でアプリを体験します。

Holographic リモート処理には、高速 PC と Wi-fi 接続が必要です。 詳細については、「 [Holographic Remoting Player](holographic-remoting-player.md) 」を参照してください。

最適な結果を得るには、アプリが[フォーカスポイント](focus-point-in-unity.md)を正しく設定していることを確認します。 これにより、Holographic リモート処理によって、ワイヤレス接続の待機時間にシーンを最適に適応させることができます。

## <a name="see-also"></a>参照
* [Holographic Remoting Player](holographic-remoting-player.md)
