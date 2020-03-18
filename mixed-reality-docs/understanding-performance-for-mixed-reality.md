---
title: Mixed Reality のパフォーマンスについて
description: Windows Mixed Reality アプリのパフォーマンスの最適化に関する高度なトピックと詳細
author: Troy-Ferrell
ms.author: trferrel
ms.date: 3/26/2019
ms.topic: article
keywords: Windows Mixed Reality、Mixed Reality、Virtual Reality、VR、MR、パフォーマンス、最適化、CPU、GPU
ms.openlocfilehash: 287b95363acff00ab7a0407475e0a419fc076611
ms.sourcegitcommit: 184227dc591ca2791f523d520555730ba1e95b5c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79479575"
---
# <a name="understanding-performance-for-mixed-reality"></a>Mixed reality のパフォーマンスについて

この記事では、Mixed Reality アプリのパフォーマンスの重要性について説明します。  アプリケーションが最適なフレームレートで実行されない場合、ユーザーエクスペリエンスが大幅に低下する可能性があります。 ホログラムが不安定になり、環境のヘッドトラッキングが不正確になり、ユーザーのエクスペリエンスが低下します。 パフォーマンスは、ポーランド語のタスクではなく、混合現実の開発のためのファーストクラスの機能と考える必要があります。

各ターゲットプラットフォームのパフォーマンスフレームの値の一覧を次に示します。

| プラットフォーム | ターゲットフレームレート |
|----------|-------------------|
| [HoloLens](hololens-hardware-details.md) | 60 FPS |
| [Windows Mixed Reality ウルトラ Pc](immersive-headset-hardware-details.md) | 90 FPS |
| [Windows Mixed Reality Pc](immersive-headset-hardware-details.md) | 60 FPS |

次のフレームワークでは、ターゲットフレームレートに到達するためのベストプラクティスについて概説します。 Unity で開発する場合は、unity 環境でのフレームレートの測定と向上に関するヒントについては、 [unity のパフォーマンスに関する推奨事項](performance-recommendations-for-unity.md)に関する記事を参照してください。

## <a name="understanding-performance-bottlenecks"></a>パフォーマンスのボトルネックについて

アプリの不採算事業フレームレートがある場合、最初の手順は、アプリケーションが計算を集中的に使用している場所を分析して理解することです。 シーンをレンダリングする作業には、CPU と GPU の2つの主要なプロセッサがあります。 これらはそれぞれ、混合 Reality アプリのさまざまな側面を処理します。 ボトルネックが発生する可能性がある主な場所には、次の3つがあります。 

1. **アプリスレッド-CPU** -このスレッドは、アプリロジックを担います。 これには、入力、アニメーション、物理、およびその他のアプリロジックの処理が含まれます。
2. **スレッドを gpu にレンダリングする**-このスレッドは、gpu への描画呼び出しを送信します。 アプリでキューブやモデルなどのオブジェクトをレンダリングする場合、このスレッドは GPU に要求を送信してこれらの操作を実行します。
3. **GPU** -このプロセッサは、通常、3d データ (モデル、テクスチャなど) をピクセルに変換するために、アプリケーションのグラフィックスパイプラインを処理します。 最終的には、デバイスの画面に送信する2D イメージが生成されます。

![フレームの有効期間](images/lifetime-of-a-frame.png)

一般に、HoloLens アプリケーションは GPU にバインドされますが、常にではありません。 以下のツールと手法を使用して、特定のアプリがボトルネックになっている場所を把握してください。

## <a name="how-to-analyze-your-application"></a>アプリケーションを分析する方法

混合現実アプリケーションのパフォーマンスプロファイルを理解できるツールは多数あります。 これらを使用すると、ボトルネックがある場所と理由を見つけることができるため、対処できます。

アプリケーションの詳細なプロファイル情報を取得するための一般的なツールを次に示します。
- [Intel グラフィックスパフォーマンスアナライザー](https://software.intel.com/gpa)
- [Visual Studio のグラフィックスデバッガー](https://docs.microsoft.com/visualstudio/debugger/graphics/visual-studio-graphics-diagnostics?view=vs-2017)
- [Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html)
- [Unity フレームデバッガー](https://docs.unity3d.com/Manual/FrameDebugger.html)

### <a name="how-to-profile-in-any-environment"></a>任意の環境でプロファイリングする方法

アプリケーションで GPU バインドと CPU バインドのどちらを使用しているかを判断する方法の1つは、レンダーターゲットの出力の解像度を下げることです。 計算するピクセル数を減らすことにより、GPU の負荷が軽減されます。 デバイスは、小さいテクスチャにレンダリングされ、その後、最後のイメージを表示するためにアップサンプリングされます。

レンダリングの解像度を下げると、次のようになります。
1) アプリケーションのフレームレートが**増加**し、 **GPU にバインド**されている可能性があります。
1) アプリケーションのフレームレートが**変更**されていないため、 **CPU バインド**されている可能性があります

>[!NOTE]
>Unity では、 *[XRSettings](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)* プロパティを使用して、実行時にアプリケーションのレンダーターゲットの解像度を簡単に変更することができます。 デバイスに表示される最終的なイメージには、固定された解決策があります。 このプラットフォームでは、解像度の低い出力をサンプリングして、ディスプレイに表示する解像度の高いイメージを構築します。 
>
>```CS
>UnityEngine.XR.XRSettings.renderScale = 0.7f;
>```

## <a name="how-to-improve-your-application"></a>アプリケーションを改善する方法

### <a name="cpu-performance-recommendations"></a>CPU パフォーマンスに関する推奨事項

一般に、CPU 上の mixed reality アプリケーションでほとんどの作業を行うには、シーンの "シミュレーション" を実行し、アプリケーションロジックを処理する必要があります。 通常、最適化の対象となる領域は次のとおりです。

- アニメーション
- 物理
- メモリの割り当て
- 複雑なアルゴリズム ( 逆のキネマティック、パスの検索)

### <a name="gpu-performance-recommendations"></a>GPU のパフォーマンスに関する推奨事項

#### <a name="understanding-bandwidth-vs-fill-rate"></a>帯域幅とフィルレートを理解する
GPU でフレームをレンダリングする場合、通常、アプリケーションはメモリ帯域幅またはフィルレートによって制限されます。

- **メモリ帯域幅**は、GPU がメモリから実行できる読み取りと書き込みの比率です。
    - 帯域幅の制限を特定するには、テクスチャの品質を下げ、フレームレートが改善されたかどうかを確認します。
    - Unity では、[**編集** > **プロジェクトの設定**] > [ **[品質設定](https://docs.unity3d.com/Manual/class-QualitySettings.html)** ] で **[テクスチャの品質]** を変更することによってこれを行うことができます。
- **Fill rate**は、GPU によって1秒あたりに描画できるピクセルを表します。
    - フィルレートの制限を特定するには、ディスプレイの解像度を下げ、フレームレートが改善されたかどうかを確認します。 
    - Unity では、XRSettings プロパティを使用してこれを行うことができ *[ます。](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)*

通常、メモリ帯域幅には次のいずれかの最適化が伴います。
1) テクスチャ解像度を下げる
2) 使用するテクスチャ (法線、反射など) を減らす

Fill rate は、レンダリングされた最終的なピクセルに対して計算する必要がある操作の数を減らすことに焦点を合わせています。 これには、次の制限が含まれます。
1) 表示/処理するオブジェクトの数
2) シェーダーあたりの操作数
3) 最終結果に対する GPU ステージの数 (ジオメトリシェーダー、処理後の影響など)
4) レンダリングするピクセル数 (表示解像度)

#### <a name="reduce-polygon-count"></a>多角形の数を減らす

ポリゴンの数が多いほど、GPU に対する操作が増えることになります。シーン[の多角形の数を減らす](https://docs.microsoft.com/dynamics365/mixed-reality/import-tool/optimize-models#performance-targets)と、レンダリング時間が短縮されます。 コストがかかる可能性のあるジオメトリの網掛けに関連する要因は他にもありますが、polygon count は、シーンがどの程度高価にレンダリングされるかを判断するための最も簡単なメトリックです。

#### <a name="limit-overdraw"></a>オーバードローを制限する

Occluding オブジェクトによって非表示になっているため、複数のオブジェクトがレンダリングされても画面に表示されない場合は、高いオーバードローが発生します。 その背後にオブジェクトがある壁を見てみましょう。 すべてのジオメトリはレンダリングのために処理されますが、不透明な壁面だけをレンダリングする必要があります。 この結果、不要な操作が発生します。

#### <a name="shaders"></a>シェーダー

シェーダーは、GPU 上で実行され、レンダリングの2つの重要な手順を実行する小さなプログラムです。
1) 描画する頂点と画面空間内の位置を決定する (頂点シェーダー)
    - 頂点シェーダーは、通常、各メッシュの頂点ごとに実行されます。
2) 各ピクセルの色を決定する (ピクセルシェーダー)
    - ピクセルシェーダーは、描画されるテクスチャに対してジオメトリによってレンダリングされるピクセルごとに実行されます。

通常、シェーダーでは、多くの変換と照明計算が実行されます。 複雑な照明モデル、影、およびその他の操作によって、優れた結果が得られる場合もありますが、価格もあります。 シェーダーで計算される操作の数を減らすと、フレームあたりの GPU に必要な作業が大幅に減少します。

##### <a name="shader-coding-recommendations"></a>シェーダーのコーディングに関する推奨事項

- 可能な限り、バイリニアフィルタリングを使用する
- 同時に乗算と加算を行うために、MAD 組み込みを使用するように式を再配置します。
- CPU で可能な限り Precalculate し、素材に定数として渡します。
- **ピクセルシェーダーから頂点シェーダーへの移動操作を優先する**
    - 一般に、頂点の数は、ピクセル数よりもはるかに小さくなっています (720p は921600ピクセル、1080p は2073600ピクセル、など)。

#### <a name="remove-gpu-stages"></a>GPU ステージの削除

処理後の影響は非常に高額であり、アプリケーションの塗りつぶしレートが高くなる可能性があります。 これには、MSAA などのアンチエイリアシング技法が含まれます。 HoloLens では、これらの手法を完全に回避することをお勧めします。また、geometry、ハル、compute シェーダーなどの追加のシェーダーステージを回避することをお勧めします。

## <a name="memory-recommendations"></a>メモリに関する推奨事項

過剰なメモリの割り当ておよび解放操作を行うと、パフォーマンスが低下したり、フレームがフリーズしたり、その他の有害な動作が発生したりする可能性があります。 メモリ管理はガベージコレクターによって制御されるため、Unity で開発するときは、メモリに関する考慮事項を理解することが特に重要です。

#### <a name="object-pooling"></a>オブジェクトプール

オブジェクトプールは、オブジェクトの継続的な割り当てと割り当て解除のコストを削減するための一般的な手法です。 これを行うには、同一のオブジェクトの大規模なプールを割り当て、時間の経過と共にオブジェクトを絶えず破棄するのではなく、このプールから使用可能な非アクティブなインスタンスを再利用します。 オブジェクトプールは、アプリの有効期間が可変の再使用可能なコンポーネントに最適です。

## <a name="see-also"></a>関連項目
- [Unity のパフォーマンスに関する推奨事項](performance-recommendations-for-unity.md)
- [Unity で推奨される設定](recommended-settings-for-unity.md)
- [3D モデルの最適化](https://docs.microsoft.com/dynamics365/mixed-reality/import-tool/optimize-models#performance-targets)
- [リアルタイム3D モデルの変換と最適化に関するベストプラクティス](https://docs.microsoft.com/dynamics365/mixed-reality/import-tool/best-practices)

