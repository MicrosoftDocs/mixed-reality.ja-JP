---
title: Unity のテキスト
description: Unity でテキストを表示するには、UI テキストと3D テキストメッシュという2種類のテキストコンポーネントを使用できます。
author: cre8ivepark
ms.author: dongpark
ms.date: 06/03/2019
ms.topic: article
keywords: Windows Mixed Reality、デザイン、コントロール、フォント、タイポグラフィ、ui、ux
ms.openlocfilehash: 8662ff8a8e1e99455354392d7dc852feb1fe1589
ms.sourcegitcommit: 7ca383ef1c5dc895ca2a289435f2e9d4c1ee6e65
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85345712"
---
# <a name="text-in-unity"></a>Unity のテキスト

Text は、holographic アプリで最も重要なコンポーネントの1つです。 Unity でテキストを表示するには、UI テキスト、3D テキストメッシュ、およびテキストメッシュ Pro の3種類のテキストコンポーネントを使用できます。 既定では、UI テキストと3D テキストメッシュはぼやけて表示され、大きすぎます。 HoloLens で管理しやすいサイズのシャープで高品質なテキストを取得するには、いくつかの変数を微調整する必要があります。 UI テキストと3D テキストメッシュコンポーネントの使用時にスケールファクターを適用して適切なディメンションを取得することで、表示品質を向上させることができます。

![シャープで美しいテキストを取得する方法](images/hug-text-02-640px.png)<br>
*Unity の既定のテキストがぼやけています*

## <a name="working-with-unitys-3d-text-text-mesh-and-ui-text"></a>Unity の3D テキスト (テキストメッシュ) と UI テキストの操作

Unity では、シーンに追加されるすべての新しい要素のサイズが 1 Unity 単位であることを前提としています。また、100% の変換スケールが、HoloLens で約1メーターに変換されることを前提としています。 フォントの場合、3D TextMesh の境界ボックスは、既定では約1メートルの高さになります。

![Unity でのフォントの操作](images/640px-hug-text-03.png)<br>
*既定の Unity 3D テキスト (テキストメッシュ) は1つの Unity ユニット (1 メートル) を占有します*

<br>
ほとんどのビジュアルデザイナーはポイントを使用して、実際の世界でのフォントサイズを定義します。 1メートルには約 2835 (2, 834.645666399962) のポイントがあります。 ポイントシステムの1メーターへの変換と Unity の既定のテキストメッシュのフォントサイズ13に基づき、13を2835で割った単純な数値は 0.0046 (正確には 0.004586111116) になります。これにより、最初に適切な標準スケールが得られます (0.005 に丸めたい場合もあります)。 テキストオブジェクトまたはコンテナーをこれらの値に拡張すると、デザインプログラムでフォントサイズを1:1 変換できるだけでなく、エクスペリエンス全体の一貫性を維持するための標準も提供されます。

![フォントサイズが異なる Unity 3D テキストメッシュ](images/Text_In_Unity_Measurements1.png)<br>
*Unity 3D テキストと UI テキストの値のスケーリング*

<br>

![フォントサイズが異なる Unity 3D テキストメッシュ](images/hug-text-05-1000px.png)<br>
*最適化された値を持つ Unity 3D テキストメッシュ*

<br>
UI またはキャンバスベースのテキスト要素をシーンに追加すると、サイズの不均衡が大きくなります。 2つのサイズの違いは約1000% です。これにより、UI ベースのテキストコンポーネントのスケールファクターが 0.00046 (正確には 0.0004586111116) または0.0005 値のになります。

![ユニット値ごとに異なる動的ピクセルを持つ Unity UI テキスト](images/hug-text-04-1000px.png)<br>
*最適化された値を含む Unity UI テキスト*

<br>

>[!NOTE]
>フォントの既定値は、そのフォントのテクスチャサイズ、またはフォントが Unity にインポートされた方法によって影響を受ける可能性があります。 これらのテストは、Unity の既定の Arial フォントおよびその他のインポートされたフォントに基づいて実行されました。

## <a name="working-with-text-mesh-pro"></a>Text メッシュ Pro の操作

Unity のテキストメッシュ Pro を使用すると、テキストの表示品質を保護できます。 [署名済み距離フィールド (.sdf)](https://steamcdn-a.akamaihd.net/apps/valve/2007/SIGGRAPH2007_AlphaTestedMagnification.pdf)手法を使用した距離に関係なく、鮮明なテキストのアウトラインがサポートされます。 上記で3D テキストメッシュと UI テキストに使用したのと同じ計算方法を使用して、通常のタイポグラフィポイントで使用する適切なスケーリング値を見つけることができます。 サイズが36の既定の3D テキストメッシュ Pro フォントのサイズは 2.5 Unity ユニット (2.5 m) であるため、スケール値0.005 を使用してポイントサイズを取得できます。 UI メニューの下にあるテキストメッシュ Pro の既定の境界サイズは 25 Unity 単位 (25m) です。 これにより、0.0005 のスケーリング値が得られます。

![フォントサイズが異なる Unity 3D テキストメッシュ](images/Text_In_Unity_Measurements2.png)<br>
*Unity 3D テキストと UI テキストの値のスケーリング*

## <a name="recommended-text-size"></a>推奨されるテキストのサイズ
ご想像のとおり、PC またはタブレットデバイスで使用する種類のサイズ (通常は 12 ~ 32pt) は2メートルの距離で非常に小さくなります。 これは、各フォントの特性によって異なりますが、一般的には、ユーザー研究の研究に基づいて、推奨される最小の表示角度と、読みやすくするためのフォントの高さは、0.35 °-0.4 °/12.21-13.97mm にあります。 これは、上で導入されたスケールファクターを使用した約 35 ~ 40pt です。 

0.45 m (45cm) でのほぼ相互作用の場合、フォントの表示角度と高さの最小値は0.4 °-0.5 °/3.14 – 3.9 mm です。 これは、前に紹介したスケールファクターを使用した12ポイントです。

![近距離および遠くの相互作用範囲 ](images/typography-distance-1000px.jpg)
 *のコンテンツとほぼの相互作用範囲*

### <a name="the-minimum-legible-font-size"></a>最小のフォントサイズの最小値
| Distance | 表示角度 | テキストの高さ | フォント サイズ |
|---------|---------|---------|---------|
| 45cm (直接操作距離) | 0.4 °-0.5 ° | 3.14 ~ 3.9 mm | 8.9 – 11.13 pt |
| 2分 | 0.35 °-0.4 ° | 12.21 – 13.97 mm | 34.63-39.58 pt |


### <a name="the-comfortably-legible-font-size"></a>判読しやすいフォントサイズ
| Distance | 表示角度 | テキストの高さ | フォント サイズ |
|---------|---------|---------|---------|
| 45cm (直接操作距離) | 0.65 °-0.8 ° | 5.1-6.3 mm | 14.47-17.8 pt |
| 2分 | 0.6 °-0.75 ° | 20.9-26.2 mm | 59.4-74.2 pt |

Segoe UI (Windows の既定のフォント) は、ほとんどの場合に適しています。 ただし、薄い垂直方向のストロークはバイブレーションので、読みやすさが低下するので、小さいサイズの明るいフォントや半明るいフォントファミリは使用しないようにしてください。 ストロークの太さが十分にある最新のフォントがうまく機能します。 たとえば、Helvetica, と Arial は、通常または太字の重みを使用して HoloLens で非常に読みやすくなります。


![角度 ](images/Text_In_Unity_ViewingAngle.jpg)
 *表示距離、角度、およびテキストの高さ*を表示する

## <a name="sharp-text-rendering-quality-with-proper-dimension"></a>適切なディメンションを使用した鋭いテキストレンダリング品質

これらのスケールファクターに基づき、 [UI テキストと3D テキストメッシュを使用してテキスト prefabs](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MRTK/SDK/StandardAssets/Prefabs/Text)を作成しました。 開発者は、これらの prefabs を使用して、鋭いテキストと一貫したフォントサイズを取得できます。

![適切なディメンションを使用した鋭いテキストレンダリング品質](images/hug-text-06-1000px.png)<br>
*適切なディメンションを使用した鋭いテキストレンダリング品質*

## <a name="shader-with-occlusion-support"></a>オクルージョンサポート付きのシェーダー

Unity の既定のフォントマテリアルでは、オクルージョンはサポートされていません。 このため、既定ではオブジェクトの背後にテキストが表示されます。 [遮蔽をサポートする](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Assets/MixedRealityToolkit/StandardAssets/Shaders/Text3DShader.shader)単純なシェーダーが含まれています。 次の画像は、既定のフォントマテリアル (左側) が付いたテキストと、適切な遮蔽 (right) のテキストを示しています。

![オクルージョンサポート付きのシェーダー](images/hug-text-07-1000px.png)<br>
*オクルージョンサポート付きのシェーダー*


## <a name="see-also"></a>関連項目
* [MRTK のテキスト Prefab](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Prefabs/Text)
* [文字体裁](typography.md)

 
