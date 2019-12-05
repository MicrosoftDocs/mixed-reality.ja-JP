---
title: 色、光、マテリアル
description: Mixed Reality のコンテンツの設計では、エクスペリエンスで使用される各ビジュアル資産の色、ライト、マテリアルを慎重に検討する必要があります。
author: mavitazk
ms.author: pinkb
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality、デザイン、カラー、ライト、素材
ms.openlocfilehash: b29fe8da92e67d15592f9d4503bc278d4fe9fd95
ms.sourcegitcommit: 05fa75193059a2dac4b580a9eef7b6c4bb64d8d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74835088"
---
# <a name="color-light-and-materials"></a><span data-ttu-id="bca9d-104">色、光、マテリアル</span><span class="sxs-lookup"><span data-stu-id="bca9d-104">Color, light and materials</span></span>

<span data-ttu-id="bca9d-105">Mixed Reality のコンテンツの設計では、エクスペリエンスで使用される各ビジュアル資産の色、ライト、マテリアルを慎重に検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-105">Designing content for mixed reality requires careful consideration of color, lighting, and materials for each of the visual assets used in your experience.</span></span> <span data-ttu-id="bca9d-106">これらの決定は、明るい色や素材を使用したイマーシブ環境の雰囲気の設定、機能の目的 (たとえば、よりよくある行動をユーザーに警告するための照明色の使用など) の両方に適しています。</span><span class="sxs-lookup"><span data-stu-id="bca9d-106">These decisions can be for both aesthetic purposes, like using light and material to set the tone of an immersive environment, and functional purposes, like using striking colors to alert users of an impending action.</span></span> <span data-ttu-id="bca9d-107">これらの各決定は、エクスペリエンスのターゲットデバイスの機会と制約に照らし合わせて検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-107">Each of these decisions must be weighed against the opportunities and constraints of your experience’s target device.</span></span>

<span data-ttu-id="bca9d-108">次に示すのは、イマーシブと holographic ヘッドセットの両方でのアセットのレンダリングに固有のガイドラインです。</span><span class="sxs-lookup"><span data-stu-id="bca9d-108">Below are guidelines specific to rendering assets on both immersive and holographic headsets.</span></span> <span data-ttu-id="bca9d-109">これらの多くは、他の技術領域に密接に関連しており、関連する項目の一覧に[ついて](color,-light-and-materials.md#see-also)は、この記事の最後にある「関連項目」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-109">Many of these are closely tied to other technical areas and a list of related subjects can be found in the [See also](color,-light-and-materials.md#see-also) section at the end of this article.</span></span>

## <a name="rendering-on-immersive-vs-holographic-devices"></a><span data-ttu-id="bca9d-110">イマーシブおよび holographic デバイスでのレンダリング</span><span class="sxs-lookup"><span data-stu-id="bca9d-110">Rendering on immersive vs. holographic devices</span></span>

<span data-ttu-id="bca9d-111">イマーシブヘッドセットでレンダリングされるコンテンツは、holographic ヘッドセットでレンダリングされるコンテンツと比較すると、視覚的に異なります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-111">Content rendered in immersive headsets will appear visually different when compared to content rendered in holographic headsets.</span></span> <span data-ttu-id="bca9d-112">イマーシブヘッドセットでは、通常、2D 画面の場合と同じようにコンテンツがレンダリングされますが、HoloLens のような holographic ヘッドセットは、カラーシーケンシャルで、「」を参照して、ホログラムをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="bca9d-112">While immersive headsets generally render content much as you would expect on a 2D screen, holographic headsets like HoloLens use color-sequential, see-through RGB displays to renders holograms.</span></span>

<span data-ttu-id="bca9d-113">Holographic ヘッドセットで holographic エクスペリエンスをテストするには、常に時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-113">Always take time to test your holographic experiences in a holographic headset.</span></span> <span data-ttu-id="bca9d-114">コンテンツの外観は、holographic デバイス専用に構築されている場合でも、セカンダリモニター、スナップショット、および spectator ビューで表示されるものとは異なります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-114">The appearance of content, even if it is built specifically for holographic devices, will differ as seen on secondary monitors, snapshots, and in spectator view.</span></span> <span data-ttu-id="bca9d-115">デバイスのエクスペリエンスについて説明し、ホログラムの照明をテストして、コンテンツがどのようにレンダリングされるかについて、すべての辺 (および上および下) から観察することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-115">Remember to walk around experiences with a device, testing the lighting of holograms and observing from all sides (as well as from above and below) how your content is rendered.</span></span> <span data-ttu-id="bca9d-116">デバイスのさまざまな明るさの設定でテストしてください。すべてのユーザーが想定されている既定値と、さまざまな照明条件のセットを共有することはほとんどありません。</span><span class="sxs-lookup"><span data-stu-id="bca9d-116">Be sure to test at a range of brightness settings on the device, as it is unlikely all users will share an assumed default, as well as a diverse set of lighting conditions.</span></span>

## <a name="fundamentals-of-rendering-on-holographic-devices"></a><span data-ttu-id="bca9d-117">Holographic デバイスでのレンダリングの基礎</span><span class="sxs-lookup"><span data-stu-id="bca9d-117">Fundamentals of rendering on holographic devices</span></span>
* <span data-ttu-id="bca9d-118">Holographic のデバイスには追加の**ディスプレイがあり**ます。実際の世界から光に光を追加することによって、ホログラムが作成されます。白は明るいと表示され、黒は透明に見えます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-118">**Holographic devices have additive displays** – Holograms are created by adding light to the light from the real world – white will appear brightly, while black will appear transparent.</span></span>
* <span data-ttu-id="bca9d-119">**色の影響はユーザーの環境によって異なり**ます。ユーザーの部屋にはさまざまな照明条件があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-119">**Colors impact varies with the user’s environment** – There are many diverse lighting conditions in a user’s room.</span></span> <span data-ttu-id="bca9d-120">わかりやすくするために、適切なコントラストレベルでコンテンツを作成します。</span><span class="sxs-lookup"><span data-stu-id="bca9d-120">Create content with appropriate levels of contrast to help with clarity.</span></span>
* <span data-ttu-id="bca9d-121">**動的な照明を避ける**– holographic エクスペリエンスで一様に点灯するホログラムは最も効率的です。</span><span class="sxs-lookup"><span data-stu-id="bca9d-121">**Avoid dynamic lighting** – Holograms that are uniformly lit in holographic experiences are the most efficient.</span></span> <span data-ttu-id="bca9d-122">高度な機能を使用すると、モバイルデバイスの機能を超える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-122">Using advanced, dynamic lighting will likely exceed the capabilities of mobile devices.</span></span> <span data-ttu-id="bca9d-123">動的ライティングが必要な場合は、 [Mixed Reality Toolkit の標準シェーダー](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_MRTKStandardShader.md)を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bca9d-123">When dynamic lighting is required, it is recommended to use the [Mixed Reality Toolkit Standard shader](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_MRTKStandardShader.md).</span></span> 

## <a name="designing-with-color"></a><span data-ttu-id="bca9d-124">色を使用したデザイン</span><span class="sxs-lookup"><span data-stu-id="bca9d-124">Designing with color</span></span>

<span data-ttu-id="bca9d-125">加法表示の性質により、holographic の表示によって特定の色が異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-125">Due to the nature of additive displays, certain colors can appear different on holographic displays.</span></span> <span data-ttu-id="bca9d-126">照明環境ではいくつかの色が表示されますが、他の色は少ないインパクトとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-126">Some colors will pop in lighting environments while others will appear as less impactful.</span></span> <span data-ttu-id="bca9d-127">クール色は背景に recede 傾向があり、ウォームカラーは前景に移動します。</span><span class="sxs-lookup"><span data-stu-id="bca9d-127">Cool colors tend to recede into the background while warm colors jump to the foreground.</span></span> <span data-ttu-id="bca9d-128">エクスペリエンスの色を調べる際には、次の要因を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-128">Consider these factors as you explore color in your experiences:</span></span>
* <span data-ttu-id="bca9d-129">色**域**-HoloLens は、概念的には Adobe RGB に似ています。</span><span class="sxs-lookup"><span data-stu-id="bca9d-129">**Gamut** - HoloLens benefits from a "wide gamut" of color, conceptually similar to Adobe RGB.</span></span> <span data-ttu-id="bca9d-130">その結果、色によっては、デバイス内のさまざまな品質と表現が表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-130">As a result, some colors can exhibit different qualities and representation in the device.</span></span>
* <span data-ttu-id="bca9d-131">**ガンマ**-レンダリングされるイメージの明るさとコントラストは、イマーシブデバイスと holographic デバイスで異なります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-131">**Gamma** - The brightness and contrast of the rendered image will vary between immersive and holographic devices.</span></span> <span data-ttu-id="bca9d-132">多くの場合、これらのデバイスの違いは、色や影の暗い領域を作成したり、明るくしたりするように見えます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-132">These device differences often appear to make dark areas of color and shadows, more or less bright.</span></span>
* <span data-ttu-id="bca9d-133">**色の分離**-"色を分割した" または "カラー fringing" とも呼ばれ、ユーザーが目のオブジェクトを追跡するときに、最も一般的に色の分離が発生します。</span><span class="sxs-lookup"><span data-stu-id="bca9d-133">**Color separation** - Also called "color breakup" or "color fringing", color separation most commonly occurs with moving holograms (including cursor) when a user tracks objects with their eyes.</span></span>
* <span data-ttu-id="bca9d-134">**色の統一性**-通常、ホログラムは、背景に関係なくカラーの統一性を維持するために十分な明るい色で表示されます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-134">**Color uniformity** - Typically holograms are rendered brightly enough so that they maintain color uniformity, regardless of the background.</span></span> <span data-ttu-id="bca9d-135">大きな領域が blotchy になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-135">Large areas may become blotchy.</span></span> <span data-ttu-id="bca9d-136">明るい、純色の大きな領域は避けてください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-136">Avoid large regions of bright, solid color.</span></span>
* <span data-ttu-id="bca9d-137">**明るい色の表示**-白は非常に明るいため、控えめに使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-137">**Rendering light colors** - White appears very bright and should be used sparingly.</span></span> <span data-ttu-id="bca9d-138">ほとんどの場合、R 235 G 235 B 235 に関する白い値を検討してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-138">For most cases, consider a white value around R 235 G 235 B 235.</span></span> <span data-ttu-id="bca9d-139">大きな明るい領域では、ユーザー不快感が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-139">Large bright areas may cause user discomfort.</span></span>

<span data-ttu-id="bca9d-140">**ダークカラーのレンダリング**</span><span class="sxs-lookup"><span data-stu-id="bca9d-140">**Rendering dark colors**</span></span>

<span data-ttu-id="bca9d-141">加法表示の性質により、暗い色は透明に見えます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-141">Due to the nature of additive displays, dark colors appear transparent.</span></span> <span data-ttu-id="bca9d-142">純色の黒のオブジェクトは、実際の世界とは異なるものとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-142">A solid black object will appear no different from the real world.</span></span> <span data-ttu-id="bca9d-143">下記の「アルファチャネル」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-143">See Alpha channel below.</span></span> <span data-ttu-id="bca9d-144">"Black" のように見えるようにするには、16、16、16のような非常に濃い灰色の RGB 値を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-144">To give the appearance of “black” try a very dark grey RGB value such as 16,16,16.</span></span>

<span data-ttu-id="bca9d-145">![標準とワイド色域](images/640px-widegamut.png)</span><span class="sxs-lookup"><span data-stu-id="bca9d-145">![Normal vs. wide color gamut](images/640px-widegamut.png)</span></span><br>
<span data-ttu-id="bca9d-146">*標準またはワイド色域*</span><span class="sxs-lookup"><span data-stu-id="bca9d-146">*Normal vs. wide color gamut*</span></span>

## <a name="technical-considerations"></a><span data-ttu-id="bca9d-147">技術的な考慮事項</span><span class="sxs-lookup"><span data-stu-id="bca9d-147">Technical considerations</span></span>
* <span data-ttu-id="bca9d-148">**別名**-ホログラム、ギザギザ、"階段のよく検討" のように、ホログラムのジオメトリのエッジが実際の世界を満たしていることを認識します。</span><span class="sxs-lookup"><span data-stu-id="bca9d-148">**Aliasing** - Be considerate of aliasing, jagged or “stair steps” where the edge of a hologram’s geometry meets the real world.</span></span> <span data-ttu-id="bca9d-149">詳細が高いテクスチャを使用すると、この効果を aggravate ことができます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-149">Using textures with high detail can aggravate this effect.</span></span> <span data-ttu-id="bca9d-150">テクスチャをマップし、フィルター処理を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-150">Textures should be mapped and filtering enabled.</span></span> <span data-ttu-id="bca9d-151">ホログラムの端をフェードさせるか、オブジェクトの周囲に黒いエッジ境界線を作成するテクスチャを追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-151">Consider fading the edges of holograms or adding a texture that creates a black edge border around objects.</span></span> <span data-ttu-id="bca9d-152">可能であれば、thin geometry は避けてください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-152">Avoid thin geometry where possible.</span></span>
* <span data-ttu-id="bca9d-153">**アルファチャネル**-ホログラムをレンダリングしていないすべてのパーツに対して完全に透明にするには、アルファチャネルをクリアする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-153">**Alpha channel** - You must clear your alpha channel to fully transparent for any parts where you are not rendering a hologram.</span></span> <span data-ttu-id="bca9d-154">アルファを未定義のままにすると、デバイスまたは Spectator ビューで画像やビデオを撮影するときに、視覚的な成果物が得られます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-154">Leaving the alpha undefined leads to visual artifacts when taking images/videos from the device or with Spectator View.</span></span>
* <span data-ttu-id="bca9d-155">**テクスチャの補正**-ライトは holographic ディスプレイで追加されるため、視覚効果が意図せずになることが多いため、明るい色の広い領域を避けることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bca9d-155">**Texture softening** - Since light is additive in holographic displays, it is best to avoid large regions of bright, solid color as they often do not produce the intended visual effect.</span></span>

## <a name="storytelling-with-light-and-color"></a><span data-ttu-id="bca9d-156">薄いと color を使用したストーリーテリング</span><span class="sxs-lookup"><span data-stu-id="bca9d-156">Storytelling with light and color</span></span>

<span data-ttu-id="bca9d-157">色と色を使用すると、ユーザーの環境でのホログラムの表示がより自然になり、ユーザーのためのガイダンスやヘルプが提供されます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-157">Light and color can help make your holograms appear more naturally in a user's environment as well as offer guidance and help for the user.</span></span> <span data-ttu-id="bca9d-158">Holographic エクスペリエンスについては、照明と色を調べる際に、次の要因を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-158">For holographic experiences, consider these factors as you explore lighting and color:</span></span>

:::row:::
    :::column:::
* <span data-ttu-id="bca9d-159">**Vignetting** -マテリアルを暗くするための ' vignette ' 効果は、ビューのフィールドの中央にユーザーの注意を集中するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="bca9d-159">**Vignetting** - A 'vignette' effect to darken materials can help focus the user's attention on the center of the field of view.</span></span> <span data-ttu-id="bca9d-160">この効果により、ユーザーの見つめベクターから、ある程度の半径でホログラムのマテリアルが暗くなります。</span><span class="sxs-lookup"><span data-stu-id="bca9d-160">This effect darkens the hologram's material at some radius from the user's gaze vector.</span></span> <span data-ttu-id="bca9d-161">これは、ユーザーのビューが斜投影または glancing 角度からホログラムを持つ場合にも有効であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-161">Note that this is also effective when the user's views holograms from an oblique or glancing angle.</span></span><br>
* <span data-ttu-id="bca9d-162">**強調**描画: 色、明るさ、および光源を比較して、オブジェクトまたは相互作用のポイントに注目します。</span><span class="sxs-lookup"><span data-stu-id="bca9d-162">**Emphasis** - Draw attention to objects or points of interaction by contrasting colors, brightness, and lighting.</span></span> <span data-ttu-id="bca9d-163">ストーリーテリングの照明メソッドの詳細については、「[ピクセル Cinematography-コンピューターグラフィックスの照明アプローチ](http://media.siggraph.org/education/cgsource/Archive/ConfereceCourses/S96/course30.pdf)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bca9d-163">For a more detailed look at lighting methods in storytelling, see [Pixel Cinematography - A Lighting Approach for Computer Graphics](http://media.siggraph.org/education/cgsource/Archive/ConfereceCourses/S96/course30.pdf).</span></span><br>
        <br>
        <span data-ttu-id="bca9d-164">*Image: 色を使用してストーリーテリング要素の強調を表示します。ここでは、[フラグメント](https://www.microsoft.com/p/fragments/9nblggh5ggm8)からのシーンに示します。*</span><span class="sxs-lookup"><span data-stu-id="bca9d-164">*Image: Use of color to show emphasis for storytelling elements, shown here in a scene from [Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8).*</span></span>
    :::column-end:::
        :::column:::
        ![色を使用して、ストーリーテリング要素の強調を表示します。ここでは、フラグメントからのシーンに示します。](images/640px-fragments.jpg)<br>
    :::column-end:::
:::row-end:::


<br>

---

## <a name="see-also"></a><span data-ttu-id="bca9d-166">関連項目</span><span class="sxs-lookup"><span data-stu-id="bca9d-166">See also</span></span>
* [<span data-ttu-id="bca9d-167">色の分離</span><span class="sxs-lookup"><span data-stu-id="bca9d-167">Color Separation</span></span>](hologram-stability.md#color-separation)
* [<span data-ttu-id="bca9d-168">ホログラム</span><span class="sxs-lookup"><span data-stu-id="bca9d-168">Holograms</span></span>](hologram.md)
* [<span data-ttu-id="bca9d-169">Microsoft デザイン言語-色</span><span class="sxs-lookup"><span data-stu-id="bca9d-169">Microsoft Design Language - color</span></span>](https://www.microsoft.com/design/color)
* [<span data-ttu-id="bca9d-170">ユニバーサル Windows プラットフォーム-色</span><span class="sxs-lookup"><span data-stu-id="bca9d-170">Universal Windows Platform - color</span></span>](https://docs.microsoft.com/windows/uwp/style/color)