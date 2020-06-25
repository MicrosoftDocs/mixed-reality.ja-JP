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
# <a name="text-in-unity"></a><span data-ttu-id="6d1de-104">Unity のテキスト</span><span class="sxs-lookup"><span data-stu-id="6d1de-104">Text in Unity</span></span>

<span data-ttu-id="6d1de-105">Text は、holographic アプリで最も重要なコンポーネントの1つです。</span><span class="sxs-lookup"><span data-stu-id="6d1de-105">Text is one of the most important components in holographic apps.</span></span> <span data-ttu-id="6d1de-106">Unity でテキストを表示するには、UI テキスト、3D テキストメッシュ、およびテキストメッシュ Pro の3種類のテキストコンポーネントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-106">To display text in Unity, there are three types of text components you can use — UI Text, 3D Text Mesh, and Text Mesh Pro.</span></span> <span data-ttu-id="6d1de-107">既定では、UI テキストと3D テキストメッシュはぼやけて表示され、大きすぎます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-107">By default, UI Text and 3D Text Mesh appear blurry and are too big.</span></span> <span data-ttu-id="6d1de-108">HoloLens で管理しやすいサイズのシャープで高品質なテキストを取得するには、いくつかの変数を微調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-108">You need to tweak a few variables to get sharp, high-quality text that has a manageable size in HoloLens.</span></span> <span data-ttu-id="6d1de-109">UI テキストと3D テキストメッシュコンポーネントの使用時にスケールファクターを適用して適切なディメンションを取得することで、表示品質を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-109">By applying a scaling factor to get proper dimensions when using the UI Text and 3D Text Mesh components, you can achieve better rendering quality.</span></span>

<span data-ttu-id="6d1de-110">![シャープで美しいテキストを取得する方法](images/hug-text-02-640px.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-110">![How to get sharp and beautiful text](images/hug-text-02-640px.png)</span></span><br>
<span data-ttu-id="6d1de-111">*Unity の既定のテキストがぼやけています*</span><span class="sxs-lookup"><span data-stu-id="6d1de-111">*Blurry default text in Unity*</span></span>

## <a name="working-with-unitys-3d-text-text-mesh-and-ui-text"></a><span data-ttu-id="6d1de-112">Unity の3D テキスト (テキストメッシュ) と UI テキストの操作</span><span class="sxs-lookup"><span data-stu-id="6d1de-112">Working with Unity's 3D Text (Text Mesh) and UI Text</span></span>

<span data-ttu-id="6d1de-113">Unity では、シーンに追加されるすべての新しい要素のサイズが 1 Unity 単位であることを前提としています。また、100% の変換スケールが、HoloLens で約1メーターに変換されることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="6d1de-113">Unity assumes that all new elements added to a scene are 1 Unity Unit in size, or 100% transform scale, which translates to about 1 meter on HoloLens.</span></span> <span data-ttu-id="6d1de-114">フォントの場合、3D TextMesh の境界ボックスは、既定では約1メートルの高さになります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-114">In the case of fonts, the bounding box for a 3D TextMesh comes in by default at about 1 meter in height.</span></span>

<span data-ttu-id="6d1de-115">![Unity でのフォントの操作](images/640px-hug-text-03.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-115">![Working with Fonts in Unity](images/640px-hug-text-03.png)</span></span><br>
<span data-ttu-id="6d1de-116">*既定の Unity 3D テキスト (テキストメッシュ) は1つの Unity ユニット (1 メートル) を占有します*</span><span class="sxs-lookup"><span data-stu-id="6d1de-116">*Default Unity 3D Text (Text Mesh) occupies 1 Unity Unit which is 1 meter*</span></span>

<br>
<span data-ttu-id="6d1de-117">ほとんどのビジュアルデザイナーはポイントを使用して、実際の世界でのフォントサイズを定義します。</span><span class="sxs-lookup"><span data-stu-id="6d1de-117">Most visual designers use points to define font sizes in the real world.</span></span> <span data-ttu-id="6d1de-118">1メートルには約 2835 (2, 834.645666399962) のポイントがあります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-118">There are about 2835 (2,834.645666399962) points in 1 meter.</span></span> <span data-ttu-id="6d1de-119">ポイントシステムの1メーターへの変換と Unity の既定のテキストメッシュのフォントサイズ13に基づき、13を2835で割った単純な数値は 0.0046 (正確には 0.004586111116) になります。これにより、最初に適切な標準スケールが得られます (0.005 に丸めたい場合もあります)。</span><span class="sxs-lookup"><span data-stu-id="6d1de-119">Based on the point system conversion to 1 meter and Unity's default Text Mesh font size of 13, the simple math of 13 divided by 2835 equals 0.0046 (0.004586111116 to be exact) which provides a good standard scale to start with (some may wish to round to 0.005).</span></span> <span data-ttu-id="6d1de-120">テキストオブジェクトまたはコンテナーをこれらの値に拡張すると、デザインプログラムでフォントサイズを1:1 変換できるだけでなく、エクスペリエンス全体の一貫性を維持するための標準も提供されます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-120">Scaling the text object or container to these values will not only allow for the 1:1 conversion of font sizes in a design program, but also provides a standard so you can maintain consistency throughout your experience.</span></span>

<span data-ttu-id="6d1de-121">![フォントサイズが異なる Unity 3D テキストメッシュ](images/Text_In_Unity_Measurements1.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-121">![Unity 3D Text Mesh with different font sizes](images/Text_In_Unity_Measurements1.png)</span></span><br>
<span data-ttu-id="6d1de-122">*Unity 3D テキストと UI テキストの値のスケーリング*</span><span class="sxs-lookup"><span data-stu-id="6d1de-122">*Scaling values for the Unity 3D Text and UI Text*</span></span>

<br>

<span data-ttu-id="6d1de-123">![フォントサイズが異なる Unity 3D テキストメッシュ](images/hug-text-05-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-123">![Unity 3D Text Mesh with different font sizes](images/hug-text-05-1000px.png)</span></span><br>
<span data-ttu-id="6d1de-124">*最適化された値を持つ Unity 3D テキストメッシュ*</span><span class="sxs-lookup"><span data-stu-id="6d1de-124">*Unity 3D Text Mesh with optimized values*</span></span>

<br>
<span data-ttu-id="6d1de-125">UI またはキャンバスベースのテキスト要素をシーンに追加すると、サイズの不均衡が大きくなります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-125">When adding a UI or canvas based text element to a scene, the size disparity is greater still.</span></span> <span data-ttu-id="6d1de-126">2つのサイズの違いは約1000% です。これにより、UI ベースのテキストコンポーネントのスケールファクターが 0.00046 (正確には 0.0004586111116) または0.0005 値のになります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-126">The differences in the two sizes is about 1000%, which would bring the scale factor for UI based text components to 0.00046 (0.0004586111116 to be exact) or 0.0005 for the rounded value.</span></span>

<span data-ttu-id="6d1de-127">![ユニット値ごとに異なる動的ピクセルを持つ Unity UI テキスト](images/hug-text-04-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-127">![Unity UI Text with different dynamic pixels per unit values](images/hug-text-04-1000px.png)</span></span><br>
<span data-ttu-id="6d1de-128">*最適化された値を含む Unity UI テキスト*</span><span class="sxs-lookup"><span data-stu-id="6d1de-128">*Unity UI Text with optimized values*</span></span>

<br>

>[!NOTE]
><span data-ttu-id="6d1de-129">フォントの既定値は、そのフォントのテクスチャサイズ、またはフォントが Unity にインポートされた方法によって影響を受ける可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-129">The default value of any font may be affected by the texture size of that font or how the font was imported into Unity.</span></span> <span data-ttu-id="6d1de-130">これらのテストは、Unity の既定の Arial フォントおよびその他のインポートされたフォントに基づいて実行されました。</span><span class="sxs-lookup"><span data-stu-id="6d1de-130">These tests were performed based on the default Arial font in Unity, as well as one other imported font.</span></span>

## <a name="working-with-text-mesh-pro"></a><span data-ttu-id="6d1de-131">Text メッシュ Pro の操作</span><span class="sxs-lookup"><span data-stu-id="6d1de-131">Working with Text Mesh Pro</span></span>

<span data-ttu-id="6d1de-132">Unity のテキストメッシュ Pro を使用すると、テキストの表示品質を保護できます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-132">With Unity's Text Mesh Pro, you can secure the text rendering quality.</span></span> <span data-ttu-id="6d1de-133">[署名済み距離フィールド (.sdf)](https://steamcdn-a.akamaihd.net/apps/valve/2007/SIGGRAPH2007_AlphaTestedMagnification.pdf)手法を使用した距離に関係なく、鮮明なテキストのアウトラインがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-133">It supports crisp text outlines regardless of the distance using the [Signed Distance Field (SDF)](https://steamcdn-a.akamaihd.net/apps/valve/2007/SIGGRAPH2007_AlphaTestedMagnification.pdf) technique.</span></span> <span data-ttu-id="6d1de-134">上記で3D テキストメッシュと UI テキストに使用したのと同じ計算方法を使用して、通常のタイポグラフィポイントで使用する適切なスケーリング値を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-134">Using the same calculation method that we used above for the 3D Text Mesh and UI Text, we can find the proper scaling values to use with conventional typographic points.</span></span> <span data-ttu-id="6d1de-135">サイズが36の既定の3D テキストメッシュ Pro フォントのサイズは 2.5 Unity ユニット (2.5 m) であるため、スケール値0.005 を使用してポイントサイズを取得できます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-135">Since the default 3D Text Mesh Pro font with the size of 36 has a bounding size of 2.5 Unity units (2.5m), we can use a scaling value of 0.005 to get the point size.</span></span> <span data-ttu-id="6d1de-136">UI メニューの下にあるテキストメッシュ Pro の既定の境界サイズは 25 Unity 単位 (25m) です。</span><span class="sxs-lookup"><span data-stu-id="6d1de-136">The Text Mesh Pro under the UI menu has a default bounding size of 25 Unity units (25m).</span></span> <span data-ttu-id="6d1de-137">これにより、0.0005 のスケーリング値が得られます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-137">This gives us 0.0005 for the scaling value.</span></span>

<span data-ttu-id="6d1de-138">![フォントサイズが異なる Unity 3D テキストメッシュ](images/Text_In_Unity_Measurements2.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-138">![Unity 3D Text Mesh with different font sizes](images/Text_In_Unity_Measurements2.png)</span></span><br>
<span data-ttu-id="6d1de-139">*Unity 3D テキストと UI テキストの値のスケーリング*</span><span class="sxs-lookup"><span data-stu-id="6d1de-139">*Scaling values for the Unity 3D Text and UI Text*</span></span>

## <a name="recommended-text-size"></a><span data-ttu-id="6d1de-140">推奨されるテキストのサイズ</span><span class="sxs-lookup"><span data-stu-id="6d1de-140">Recommended text size</span></span>
<span data-ttu-id="6d1de-141">ご想像のとおり、PC またはタブレットデバイスで使用する種類のサイズ (通常は 12 ~ 32pt) は2メートルの距離で非常に小さくなります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-141">As you can expect, type sizes that we use on a PC or a tablet device (typically between 12–32pt) look quite small at a distance of 2 meters.</span></span> <span data-ttu-id="6d1de-142">これは、各フォントの特性によって異なりますが、一般的には、ユーザー研究の研究に基づいて、推奨される最小の表示角度と、読みやすくするためのフォントの高さは、0.35 °-0.4 °/12.21-13.97mm にあります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-142">It depends on the characteristics of each font, but in general the recommended minimum viewing angle and the font height for legibility are around 0.35°-0.4°/12.21-13.97mm based on our user research studies.</span></span> <span data-ttu-id="6d1de-143">これは、上で導入されたスケールファクターを使用した約 35 ~ 40pt です。</span><span class="sxs-lookup"><span data-stu-id="6d1de-143">It is about 35-40pt with the scaling factor introduced above.</span></span> 

<span data-ttu-id="6d1de-144">0.45 m (45cm) でのほぼ相互作用の場合、フォントの表示角度と高さの最小値は0.4 °-0.5 °/3.14 – 3.9 mm です。</span><span class="sxs-lookup"><span data-stu-id="6d1de-144">For the near interaction at 0.45m (45cm), the minimum legible font's viewing angle and the height are 0.4°-0.5° / 3.14–3.9mm.</span></span> <span data-ttu-id="6d1de-145">これは、前に紹介したスケールファクターを使用した12ポイントです。</span><span class="sxs-lookup"><span data-stu-id="6d1de-145">It is about 9-12pt with the scaling factor introduced above.</span></span>

<span data-ttu-id="6d1de-146">![近距離および遠くの相互作用範囲 ](images/typography-distance-1000px.jpg)
 *のコンテンツとほぼの相互作用範囲*</span><span class="sxs-lookup"><span data-stu-id="6d1de-146">![Near and far interaction range](images/typography-distance-1000px.jpg)
*Content at near and far interaction range*</span></span>

### <a name="the-minimum-legible-font-size"></a><span data-ttu-id="6d1de-147">最小のフォントサイズの最小値</span><span class="sxs-lookup"><span data-stu-id="6d1de-147">The minimum legible font size</span></span>
| <span data-ttu-id="6d1de-148">Distance</span><span class="sxs-lookup"><span data-stu-id="6d1de-148">Distance</span></span> | <span data-ttu-id="6d1de-149">表示角度</span><span class="sxs-lookup"><span data-stu-id="6d1de-149">Viewing angle</span></span> | <span data-ttu-id="6d1de-150">テキストの高さ</span><span class="sxs-lookup"><span data-stu-id="6d1de-150">Text height</span></span> | <span data-ttu-id="6d1de-151">フォント サイズ</span><span class="sxs-lookup"><span data-stu-id="6d1de-151">Font size</span></span> |
|---------|---------|---------|---------|
| <span data-ttu-id="6d1de-152">45cm (直接操作距離)</span><span class="sxs-lookup"><span data-stu-id="6d1de-152">45cm (direct manipulation distance)</span></span> | <span data-ttu-id="6d1de-153">0.4 °-0.5 °</span><span class="sxs-lookup"><span data-stu-id="6d1de-153">0.4°-0.5°</span></span> | <span data-ttu-id="6d1de-154">3.14 ~ 3.9 mm</span><span class="sxs-lookup"><span data-stu-id="6d1de-154">3.14–3.9mm</span></span> | <span data-ttu-id="6d1de-155">8.9 – 11.13 pt</span><span class="sxs-lookup"><span data-stu-id="6d1de-155">8.9–11.13pt</span></span> |
| <span data-ttu-id="6d1de-156">2分</span><span class="sxs-lookup"><span data-stu-id="6d1de-156">2m</span></span> | <span data-ttu-id="6d1de-157">0.35 °-0.4 °</span><span class="sxs-lookup"><span data-stu-id="6d1de-157">0.35°-0.4°</span></span> | <span data-ttu-id="6d1de-158">12.21 – 13.97 mm</span><span class="sxs-lookup"><span data-stu-id="6d1de-158">12.21–13.97mm</span></span> | <span data-ttu-id="6d1de-159">34.63-39.58 pt</span><span class="sxs-lookup"><span data-stu-id="6d1de-159">34.63-39.58pt</span></span> |


### <a name="the-comfortably-legible-font-size"></a><span data-ttu-id="6d1de-160">判読しやすいフォントサイズ</span><span class="sxs-lookup"><span data-stu-id="6d1de-160">The comfortably legible font size</span></span>
| <span data-ttu-id="6d1de-161">Distance</span><span class="sxs-lookup"><span data-stu-id="6d1de-161">Distance</span></span> | <span data-ttu-id="6d1de-162">表示角度</span><span class="sxs-lookup"><span data-stu-id="6d1de-162">Viewing angle</span></span> | <span data-ttu-id="6d1de-163">テキストの高さ</span><span class="sxs-lookup"><span data-stu-id="6d1de-163">Text height</span></span> | <span data-ttu-id="6d1de-164">フォント サイズ</span><span class="sxs-lookup"><span data-stu-id="6d1de-164">Font size</span></span> |
|---------|---------|---------|---------|
| <span data-ttu-id="6d1de-165">45cm (直接操作距離)</span><span class="sxs-lookup"><span data-stu-id="6d1de-165">45cm (direct manipulation distance)</span></span> | <span data-ttu-id="6d1de-166">0.65 °-0.8 °</span><span class="sxs-lookup"><span data-stu-id="6d1de-166">0.65°-0.8°</span></span> | <span data-ttu-id="6d1de-167">5.1-6.3 mm</span><span class="sxs-lookup"><span data-stu-id="6d1de-167">5.1-6.3mm</span></span> | <span data-ttu-id="6d1de-168">14.47-17.8 pt</span><span class="sxs-lookup"><span data-stu-id="6d1de-168">14.47-17.8pt</span></span> |
| <span data-ttu-id="6d1de-169">2分</span><span class="sxs-lookup"><span data-stu-id="6d1de-169">2m</span></span> | <span data-ttu-id="6d1de-170">0.6 °-0.75 °</span><span class="sxs-lookup"><span data-stu-id="6d1de-170">0.6°-0.75°</span></span> | <span data-ttu-id="6d1de-171">20.9-26.2 mm</span><span class="sxs-lookup"><span data-stu-id="6d1de-171">20.9-26.2mm</span></span> | <span data-ttu-id="6d1de-172">59.4-74.2 pt</span><span class="sxs-lookup"><span data-stu-id="6d1de-172">59.4-74.2pt</span></span> |

<span data-ttu-id="6d1de-173">Segoe UI (Windows の既定のフォント) は、ほとんどの場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="6d1de-173">Segoe UI (the default font for Windows) works well in most cases.</span></span> <span data-ttu-id="6d1de-174">ただし、薄い垂直方向のストロークはバイブレーションので、読みやすさが低下するので、小さいサイズの明るいフォントや半明るいフォントファミリは使用しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="6d1de-174">However, avoid using light or semi light font families in small size since thin vertical strokes will vibrate and it will degrade the legibility.</span></span> <span data-ttu-id="6d1de-175">ストロークの太さが十分にある最新のフォントがうまく機能します。</span><span class="sxs-lookup"><span data-stu-id="6d1de-175">Modern fonts with enough stroke thickness work well.</span></span> <span data-ttu-id="6d1de-176">たとえば、Helvetica, と Arial は、通常または太字の重みを使用して HoloLens で非常に読みやすくなります。</span><span class="sxs-lookup"><span data-stu-id="6d1de-176">For example, Helvetica and Arial look gorgeous and are very legible in HoloLens with regular or bold weights.</span></span>


<span data-ttu-id="6d1de-177">![角度 ](images/Text_In_Unity_ViewingAngle.jpg)
 *表示距離、角度、およびテキストの高さ*を表示する</span><span class="sxs-lookup"><span data-stu-id="6d1de-177">![Viewing Angle](images/Text_In_Unity_ViewingAngle.jpg)
*Viewing distance, angle, and text height*</span></span>

## <a name="sharp-text-rendering-quality-with-proper-dimension"></a><span data-ttu-id="6d1de-178">適切なディメンションを使用した鋭いテキストレンダリング品質</span><span class="sxs-lookup"><span data-stu-id="6d1de-178">Sharp text rendering quality with proper dimension</span></span>

<span data-ttu-id="6d1de-179">これらのスケールファクターに基づき、 [UI テキストと3D テキストメッシュを使用してテキスト prefabs](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MRTK/SDK/StandardAssets/Prefabs/Text)を作成しました。</span><span class="sxs-lookup"><span data-stu-id="6d1de-179">Based on these scaling factors, we have created [text prefabs with UI Text and 3D Text Mesh](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MRTK/SDK/StandardAssets/Prefabs/Text).</span></span> <span data-ttu-id="6d1de-180">開発者は、これらの prefabs を使用して、鋭いテキストと一貫したフォントサイズを取得できます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-180">Developers can use these prefabs to get sharp text and consistent font size.</span></span>

<span data-ttu-id="6d1de-181">![適切なディメンションを使用した鋭いテキストレンダリング品質](images/hug-text-06-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-181">![Sharp text rendering quality with proper dimension](images/hug-text-06-1000px.png)</span></span><br>
<span data-ttu-id="6d1de-182">*適切なディメンションを使用した鋭いテキストレンダリング品質*</span><span class="sxs-lookup"><span data-stu-id="6d1de-182">*Sharp text rendering quality with proper dimension*</span></span>

## <a name="shader-with-occlusion-support"></a><span data-ttu-id="6d1de-183">オクルージョンサポート付きのシェーダー</span><span class="sxs-lookup"><span data-stu-id="6d1de-183">Shader with occlusion support</span></span>

<span data-ttu-id="6d1de-184">Unity の既定のフォントマテリアルでは、オクルージョンはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6d1de-184">Unity's default font material does not support occlusion.</span></span> <span data-ttu-id="6d1de-185">このため、既定ではオブジェクトの背後にテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6d1de-185">Because of this, you will see the text behind the objects by default.</span></span> <span data-ttu-id="6d1de-186">[遮蔽をサポートする](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Assets/MixedRealityToolkit/StandardAssets/Shaders/Text3DShader.shader)単純なシェーダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6d1de-186">We have included a simple [shader that supports the occlusion](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Assets/MixedRealityToolkit/StandardAssets/Shaders/Text3DShader.shader).</span></span> <span data-ttu-id="6d1de-187">次の画像は、既定のフォントマテリアル (左側) が付いたテキストと、適切な遮蔽 (right) のテキストを示しています。</span><span class="sxs-lookup"><span data-stu-id="6d1de-187">The image below shows the text with default font material (left) and the text with proper occlusion (right).</span></span>

<span data-ttu-id="6d1de-188">![オクルージョンサポート付きのシェーダー](images/hug-text-07-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="6d1de-188">![Shader with occlusion support](images/hug-text-07-1000px.png)</span></span><br>
<span data-ttu-id="6d1de-189">*オクルージョンサポート付きのシェーダー*</span><span class="sxs-lookup"><span data-stu-id="6d1de-189">*Shader with occlusion support*</span></span>


## <a name="see-also"></a><span data-ttu-id="6d1de-190">関連項目</span><span class="sxs-lookup"><span data-stu-id="6d1de-190">See also</span></span>
* [<span data-ttu-id="6d1de-191">MRTK のテキスト Prefab</span><span class="sxs-lookup"><span data-stu-id="6d1de-191">Text Prefab in the MRTK</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Prefabs/Text)
* [<span data-ttu-id="6d1de-192">文字体裁</span><span class="sxs-lookup"><span data-stu-id="6d1de-192">Typography</span></span>](typography.md)

 
