---
title: Holographic リモート処理のバージョン履歴
description: HoloLens 2 での Holographic リモート処理のバージョン履歴。
author: florianbagarmicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens、リモート処理、Holographic リモート処理
ms.openlocfilehash: 131c5237801c381a371b197a5b7d8e0ec64fa2d6
ms.sourcegitcommit: fef42e2908e49822f2d13b05d2f9260bf0d72158
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86061125"
---
# <a name="holographic-remoting-version-history"></a>Holographic リモート処理のバージョン履歴

> [!IMPORTANT]
> このガイダンスは、HoloLens 2 の Holographic リモート処理に固有のものです。

## <a name="version-221-july-6-2020"></a>バージョン 2.2.1 (2020 年7月6日)<a name="v2.2.1"></a>
> [!IMPORTANT]
> [Windows アプリ認定キット](https://developer.microsoft.com/windows/downloads/app-certification-kit/)のバージョン[2.2.0](holographic-remoting-version-history.md#v2.2.0)による検証は失敗します。 バージョン[2.2.0](holographic-remoting-version-history.md#v2.2.0)を使用していて、Microsoft ストアにアプリケーションを送信する場合は、バージョン2.2.1 以降に更新してください。
* [Windows アプリ認定キット](https://developer.microsoft.com/windows/downloads/app-certification-kit/)のコンプライアンスに関する問題を修正します。

## <a name="version-220-july-1-2020"></a>バージョン 2.2.0 (2020 年7月1日)<a name="v2.2.0"></a>
* [Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)を実行している Pc に Holographic リモート処理プレーヤーをインストールできるようになりました。これにより、イマーシブヘッドセットにストリーミングすることができます。
* Holographic リモート処理では、[モーションコントローラー](motion-controllers.md)がサポートされるようになりました。コントローラー固有のデータは、 [SpatialInteractionSource](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsource.controller#Windows_UI_Input_Spatial_SpatialInteractionSource_Controller)を使用して取得できます。
* [SpatialStageFrameOfReference](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference)がサポートされるようになり、現在のステージを[SpatialStageFrameOfReference](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current)経由で取得できるようになりました。 また、SpatialStageFrameOfReference を使用して新しいステージを要求することもできます[。 RequestNewStageAsync](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.requestnewstageasync)です。
* 以前のバージョンでは、Holographic リモート処理プレーヤーによって、プレーヤー側で予測が完全に処理されました。 バージョン2.2.0 以降では、Holographic リモート処理に時間の同期があり、予測はリモートアプリケーションによって完全に実行されます。 また、複雑なネットワークの状況下では、ユーザーがホログラムの安定性を向上させる必要があります。

## <a name="version-213-may-25-2020"></a>バージョン 2.1.3 (2020 年5月 25)<a name="v2.1.3"></a>
* [HolographicSpace CameraAdded](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.cameraadded?view=winrt-18362)イベントの動作が変更されました。 以前のバージョンでは、追加された[HolographicCamera](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera?view=winrt-18362)には、 [HolographicSpace](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.createnextframe?view=winrt-18362#Windows_Graphics_Holographic_HolographicSpace_CreateNextFrame)を使用して次のフレームを作成するときに有効な[HolographicCameraPose](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose?view=winrt-18362)があることは保証されて**いません**でした。 バージョン 2.1.3 HolographicSpace は、Holographic Remoting Player から来たポーズデータと同期されてい[ます。](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.cameraadded?view=winrt-18362)また、カメラが追加されると、そのカメラでは次のフレームに有効な[HolographicCameraPose](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose?view=winrt-18362)も使用できます。
* DepthBufferStreamResolution に**無効**にされました。これを使用して、RemoteContext.ConfigureDepthVideoStream を介した深度バッファーストリーミングを無効にすることができます。 HolographicCameraRenderingParameters を使用すると、 [CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer?view=winrt-18362#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_)は*E_ILLEGAL_METHOD_CALL*で失敗します。
* Holographic リモート処理プレーヤーのスタートアップ画面が再設計され、ユーザービューをブロックしないようになりました。
* 安定性の向上とバグの修正。

## <a name="version-212-april-5-2020"></a>バージョン 2.1.2 (2020 年4月5日)<a name="v2.1.2"></a>
* 最新の Holographic リモート処理プレーヤーと2.1.0 より小さいバージョンを使用したリモートアプリとの間で、オーディオの下位互換性の問題を修正した。
* Holographic リモート処理プレーヤーを予期せず閉じた空間アンカーの問題を修正しました。 この問題は、カスタムプレーヤーにも影響します。

## <a name="version-211-march-20-2020"></a>バージョン 2.1.1 (2020 年3月20日)<a name="v2.1.1"></a>
* AMD Gpu を使用する場合のリモートアプリのビデオエンコードに関する問題を修正します。
* Holographic リモート処理プレーヤーのパフォーマンスが向上しました。

## <a name="version-210-march-11-2020"></a>バージョン 2.1.0 (2020 年3月11日)<a name="v2.1.0"></a>
* UDP 経由で[RTP](https://en.wikipedia.org/wiki/Real-time_Transport_Protocol)を使用するようにネットワークトランスポートを切り替えました。 セキュリティで保護された接続では、 [Srtp](https://en.wikipedia.org/wiki/Secure_Real-time_Transport_Protocol)を使用します。 [Holographic リモート処理プレーヤー](holographic-remoting-player.md)は、以前にリリースされたすべての Holographic リモート処理バージョンと互換性があることに注意してください。 新しいネットワークトランスポートの利点を活用するには、Holographic リモート処理プレーヤーと、問題のリモートアプリの両方でバージョン2.1.0 を使用する必要があります。
* [CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_)のサポートが追加されました。 

## <a name="version-2020-february-2-2020"></a>バージョン2.0.20 以降 (2020 年2月2日)<a name="v2.0.20"></a>
* クラッシュの原因となるさまざまなバグが修正されています。

## <a name="version-2018-december-17-2019"></a>バージョン 2.0.18 (2019 年12月17日)<a name="v2.0.18"></a>
* [HolographicViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicviewconfiguration)のサポートを追加しました
* クラッシュの原因となるさまざまなバグが修正されています。
* HolographicCamera が受け入れられ、HolographicFrame に追加されたカメラとして表示されるために HolographicSpace CameraAdded コールバックが必要なバグを修正しました。

## <a name="version-2016-november-11-2019"></a>バージョン 2.0.16 (2019 年11月11日)<a name="2.0.16"></a>
* QR コードの追跡でデッドロックを修正します。
* メインスレッドでの待機をブロックしているため、固定されていない例外を修正しています。

## <a name="version-2014-october-26-2019"></a>バージョン 2.0.14 (2019 年10月26日)<a name="v2.0.14"></a>
* New PerceptionDevice Api のサポート (Windows 10 11 月2019更新プログラム)。
* SpatialGestureRecognizer によって保留中のジェスチャイベントがトリガーされない問題を修正しました。
* SpatialSurfaceObserver を使用する場合のスレッド処理の問題を修正します。 SetBoundingVolume。

## <a name="version-2012-october-18-2019"></a>バージョン 2.0.12 (2019 年10月18日)<a name="v2.0.12"></a>
* NavigationRail (X/Y/Z) を使用するときの SpatialGestureRecognizer のクラッシュを修正します。

## <a name="version-2010-october-10-2019"></a>バージョン 2.0.10 (2019 年10月10日)<a name="v2.0.10"></a>
* VR コントローラーの [トリガー] ボタンを使用するときのクラッシュを修正します。 Holographic リモート処理はコントローラーを完全にサポートしていません。 HoloLens 2 とペアになっている場合は、[トリガー] ボタンと [Windows] ボタンのみが動作します。

## <a name="version-209-september-19-2019"></a>バージョン 2.0.9 (2019 年9月19日)<a name="v2.0.9"></a>
* [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)のサポートを追加しました
* ```IPlayerContext2```次のメンバーを提供する新しいインターフェイスを追加しました (によって実装され ```PlayerContext``` ます)。
  - [BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout)プロパティ。
* ```Failed_RemoteFrameTooOld```に値を追加しました```BlitResult```
* 安定性と信頼性の向上

## <a name="version-208-august-20-2019"></a>バージョン 2.0.8 (2019 年8月20日)<a name="v2.0.8"></a>

* [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) as パラメーターを指定して[HolographicCameraRenderingParameters](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer)を呼び出すときのクラッシュを修正します。
* 安定性と信頼性の向上

## <a name="version-207-july-26-2019"></a>バージョン 2.0.7 (2019 年7月26日)<a name="v2.0.7"></a>

* HoloLens 2 の Holographic リモート処理の最初のパブリックリリース。

## <a name="see-also"></a>関連項目
* [カスタム Holographic リモート処理プレーヤーアプリの作成](holographic-remoting-create-player.md)
* [Holographic Remoting ホストアプリの作成](holographic-remoting-create-host.md)
* [Holographic リモート処理のトラブルシューティングと制限事項](holographic-remoting-troubleshooting.md)
* [Holographic Remoting ソフトウェア ライセンス条項](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Microsoft のプライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkId=521839)
