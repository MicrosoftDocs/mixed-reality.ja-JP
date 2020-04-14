---
title: Holographic リモート処理プレーヤー
description: Holographic Remoting Player は、Holographic リモート処理をサポートする PC アプリやゲームに接続するコンパニオンアプリです。 Holographic リモート処理では、Wi-fi 接続を使用して、PC から Microsoft HoloLens にコンテンツを Holographic します。
author: florianbagarmicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens、リモート処理、Holographic リモート処理
ms.openlocfilehash: e5255fb5537201058c491f5e4c682bb1c22d0edb
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81278210"
---
# <a name="holographic-remoting-player"></a>Holographic リモート処理プレーヤー

>[!IMPORTANT]
>HoloLens 2 の Holographic リモート処理は、メジャーバージョンの変更です。 [ **Hololens (第1世代)** のリモートアプリケーション](add-holographic-remoting.md)では、NuGet**パッケージバージョン 1.x**および[ **hololens 2**のリモートアプリケーション](holographic-remoting-create-host.md)を使用する必要が**あります2.x を使用する**必要があります。 これは、HoloLens 2 用に作成されたリモートアプリケーションが HoloLens (第1世代) と互換性がないことを意味します。

[Holographic Remoting Player](https://www.microsoft.com/p/holographic-remoting-player/9nblggh4sv40)は、Holographic リモート処理をサポートする PC アプリやゲームに接続するコンパニオンアプリです。 Holographic リモート処理では、Wi-fi 接続を使用して、PC から Microsoft HoloLens にコンテンツを Holographic します。

Holographic リモート処理プレーヤーは、特に Holographic リモート処理をサポートするように設計された PC アプリでのみ使用できます。

Holographic リモート処理プレーヤーは、HoloLens (第1世代) と HoloLens 2 の両方で使用できます。  HoloLens で Holographic リモート処理をサポートする PC アプリは、HoloLens 2 での Holographic リモート処理をサポートするように更新する必要があります。 サポートされているバージョンについて不明な点がある場合は、アプリプロバイダーにお問い合わせください。

## <a name="connecting-to-the-holographic-remoting-player"></a>Holographic リモート処理プレーヤーに接続する

アプリの指示に従って、Holographic リモート処理プレーヤーに接続します。 次のように、HoloLens デバイスの IP アドレスを入力する必要があります。これは、リモート処理プレーヤーのメイン画面で確認できます。

![Holographic リモート処理プレーヤー](images/holographicremotingplayer.png)

メイン画面が表示されるたびに、アプリが接続されていないことがわかります。

Holographic remoting 接続は暗号化されて**いない**ことに注意してください。 信頼できる Wi-fi 接続では、常に Holographic リモート処理を使用する必要があります。

## <a name="quality-and-performance"></a>品質とパフォーマンス

エクスペリエンスの品質とパフォーマンスは、次の3つの要因によって異なります。
* 実行している**holographic エクスペリエンス**-高解像度または高度なコンテンツをレンダリングするアプリでは、より高速な PC またはより高速なワイヤレス接続が必要になる場合があります。
* **Pc のハードウェア**-pc は、1秒あたり60のフレームで holographic エクスペリエンスを実行およびエンコードできる必要があります。 グラフィックスカードの場合は、一般に、GeForce GTX 970 または AMD Radeon R9 290 以上をお勧めします。 ここでも、特定のエクスペリエンスでは、より高いまたは低いカードが必要になる場合があります。
* Wi-fi**接続**-holographic エクスペリエンスは wi-fi 経由でストリーミングされます。 低負荷の高速ネットワークを使用して、品質を最大化します。 Wi-fi ではなくイーサネットケーブルで接続されている PC を使用すると、品質が向上する場合もあります。

## <a name="diagnostics"></a>診断

接続の品質を測定するには、Holographic リモート処理プレーヤーのメイン画面で [**診断の有効化]** を言います。 診断が有効になっている場合、 **HoloLens (第1世代)** で、アプリには次の情報が表示されます。

* **FPS** -リモートプレーヤーが受信して1秒間にレンダリングするレンダリングフレームの平均数。 最適なは 60 FPS です。
* **[待機時間]** -フレームが PC から HoloLens に移動するまでにかかる平均時間。 精度が低下します。 これは、Wi-fi ネットワークに大きく依存します。

**HoloLens 2**では、アプリには次のように表示されます。

![Holographic リモート処理プレーヤーの診断](images/holographicremotingplayer-diag.png)

* **Render** -リモートプレーヤーが最後の1秒間にレンダリングしたフレームの数。 これは、ネットワーク経由で到着したフレームの数とは関係がありません (**ビデオフレーム**を参照)。 さらに、レンダリングされたフレーム間の平均/最大レンダリングデルタ時間 (ミリ秒) が表示されます。

* **ビデオフレーム**-表示される最初の数字はスキップされたビデオフレーム、2つ目はビデオフレームを再利用し、3番目はビデオフレームを受信します。 すべての数値は、最後の1秒間のカウントを表します。
    * ```Received frames``` は、最後の1秒間に到着したビデオフレームの数です。 通常の条件下では、これは60になりますが、これはネットワークの問題のためにフレームがドロップされたか、またはリモート/リモート側が想定されたレートでフレームを生成しないことを示すインジケーターです。
    * ```Reused frames``` は、最後の1秒間に複数回使用されたビデオフレームの数です。 たとえば、ビデオフレームが遅れて到着した場合でも、プレーヤーのレンダリングループはフレームをレンダリングしますが、前のフレームで既に使用されていたビデオフレームを*再利用*する必要があります。
    * ```Skipped frames``` は、プレーヤーのレンダリングループによって使用されていないビデオフレームの数です。 たとえば、ネットワークのジッターでは、受信するビデオフレームが均等に分散されないようにすることができます。 たとえば、何らかの遅延が発生し、他のユーザーが時間内に到着した場合、60Hz で実行したときに16.66 ミリ秒のデルタが得られなくなります。 プレーヤーのレンダーループの2つのタイマー刻みの間に複数のフレームが到着する可能性があります。 この場合、プレーヤーは、常に最新の受信したビデオフレームを常に表示することが想定されているため、1つ以上のフレームを*スキップ*します。

    >[!NOTE]
    >ネットワークのジッターを使用する場合、スキップされたフレームと再利用されるフレームは通常、ほぼ同じです。 これに対して、[スキップされたフレーム] のみが表示される場合は、プレーヤーがターゲットフレームレートにヒットしないことを示すインジケーターです。 この場合は、問題を診断するときに、レンダーデルタの最大時間を監視する必要があります。

* **ビデオフレームのデルタ**-最後の1秒間に受信したビデオフレーム間の最小/最大デルタです。 通常、この数は、ネットワークのジッターに起因する問題が発生した場合に、スキップまたは再利用されたフレームと関連付けられます。
* **Latency** -最後の1秒間の平均待機時間 (ミリ秒)。 このコンテキストでのターンアラウンドとは、hololens の待機/センサーデータを hololens からリモートまたはリモート側に送信してから、HoloLens ディスプレイにそのポーズ/テレメトリデータのビデオフレームを表示するまでの時間を意味します。
* **破棄されるビデオフレーム**-最後の1秒間に破棄されたビデオフレームの数。接続が確立されたためです。 破棄されるビデオフレームの主な原因は、ビデオフレームが順番に到着せず、既に新しいものが存在するためにその理由を破棄する必要がある場合です。 これは破棄された*フレーム*に似ていますが、リモート処理スタックの下位のレベルにあります。 破棄されたビデオフレームは、ネットワークの状態が非常に悪い場合にのみ必要です。



メイン画面では、 **[診断を無効**にする] を使用して診断を無効にすることができます。

## <a name="pc-system-requirements"></a>PC のシステム要件
* お使いの PC では、Windows 10 の記念日更新以降が実行されている**必要があり**ます。
* GeForce GTX 970 または AMD Radeon R9 290 以上のグラフィックスカードをお勧めします。
* ワイヤレスホップの数を減らすには、コンピューターをイーサネット経由でネットワークに接続することをお勧めします。

## <a name="see-also"></a>参照
* [HoloLens (第1世代): Holographic リモート処理の追加](add-holographic-remoting.md)
* [HoloLens 2: Holographic リモート処理リモートアプリの作成](holographic-remoting-create-host.md)
* [Holographic Remoting ソフトウェア ライセンス条項](https://docs.microsoft.com//legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Microsoft のプライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkId=521839)
