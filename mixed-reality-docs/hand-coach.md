---
title: 手コーチ
description: 3D ハンドは、システムがユーザーの手を認識しない場合にトリガーされます。
author: grayclee
ms.author: glee
ms.date: 09/25/2019
ms.topic: article
keywords: Windows Mixed Reality、設計、手作業、イマーシブヘッドセット、MRTK、ハンズオン、
ms.openlocfilehash: 38da046256dce3242b464a0741f2afa7fb19ff3c
ms.sourcegitcommit: 7ca383ef1c5dc895ca2a289435f2e9d4c1ee6e65
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85345668"
---
# <a name="hand-coach"></a><span data-ttu-id="99e2a-104">手コーチ</span><span class="sxs-lookup"><span data-stu-id="99e2a-104">Hand coach</span></span>
![例: 手動](images/HandCoach/MRTK_handCoach.jpg)<br>

<span data-ttu-id="99e2a-106">ユーザーの手がシステムによって検出されなかった場合にトリガーされる、3D でモデル化されたハンドです。</span><span class="sxs-lookup"><span data-stu-id="99e2a-106">Hand coach is 3D modeled hands that are triggered when the system does not detect the user’s hands.</span></span> <span data-ttu-id="99e2a-107">これは、ジェスチャが学習されていないときにユーザーをガイドする "教職員" コンポーネントとして実装されます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-107">This is implemented as a “teaching” component that helps guide the user when the gesture has not been taught.</span></span> <span data-ttu-id="99e2a-108">ユーザーが指定されたジェスチャをピリオドに対して実行していない場合、針は遅延でループします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-108">If users have not done the specified gesture for a period, the hands will loop with a delay.</span></span> <span data-ttu-id="99e2a-109">針を使用すると、ボタンを押すか、またはホログラムを選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-109">The Hand coach could be used to represent pressing a button or picking up a hologram.</span></span>  

## <a name="hand-coach-provided"></a><span data-ttu-id="99e2a-110">提供される手</span><span class="sxs-lookup"><span data-stu-id="99e2a-110">Hand coach provided</span></span>

<span data-ttu-id="99e2a-111">現在の相互作用モデルは、スクロール、遠くの選択、およびニアタップなどのさまざまなジェスチャコントロールを表します。</span><span class="sxs-lookup"><span data-stu-id="99e2a-111">The current interaction model represents a wide variety of gesture controls such as scrolling, far select, and near tap.</span></span> <span data-ttu-id="99e2a-112"><a href="https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets">Mrtk</a>に用意されている既存のジェスチャの完全な一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="99e2a-112">Below is a full list of existing hand gestures provided in<a href="https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets"> MRTK</a>:</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="99e2a-113">![Near Select の例](images/HandCoach/NearSelect.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-113">![Example of Near Select](images/HandCoach/NearSelect.gif)</span></span><br>
       <span data-ttu-id="99e2a-114">**Near Select の例: ボタンを選択する方法または対話型オブジェクトを閉じる方法**</span><span class="sxs-lookup"><span data-stu-id="99e2a-114">**Example of Near Select - Used show how to select buttons or close interactable objects**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="99e2a-115">![エアタップの例](images/HandCoach/AirTap.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-115">![Example of Air Tap](images/HandCoach/AirTap.gif)</span></span><br>
        <span data-ttu-id="99e2a-116">**エアタップの例-遠く離れたオブジェクトを選択する方法を示すために使用されます。**</span><span class="sxs-lookup"><span data-stu-id="99e2a-116">**Example of Air Tap - Used to show how to select objects that are far away**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="99e2a-117">![移動の例](images/HandCoach/Move.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-117">![Example of Move](images/HandCoach/Move.gif)</span></span><br>
       <span data-ttu-id="99e2a-118">**スペースでのオブジェクトの移動の例-スペースでのホログラムの移動方法を示すために使用されます。**</span><span class="sxs-lookup"><span data-stu-id="99e2a-118">**Example of Moving an object in space-Used to show how to move a hologram in space**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="99e2a-119">![回転の例](images/HandCoach/Rotate.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-119">![Example of Rotate](images/HandCoach/Rotate.gif)</span></span><br>
       <span data-ttu-id="99e2a-120">**回転の例 (ホログラムまたはオブジェクトの回転方法を示すために使用)**</span><span class="sxs-lookup"><span data-stu-id="99e2a-120">**Example of Rotate-Used to show how to rotate holograms or objects**</span></span><br>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
       <span data-ttu-id="99e2a-121">![スケールの例](images/HandCoach/Scale.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-121">![Example of Scale](images/HandCoach/Scale.gif)</span></span><br>
       <span data-ttu-id="99e2a-122">**拡大/縮小するホログラムの操作方法を示すために使用されるスケールの例**</span><span class="sxs-lookup"><span data-stu-id="99e2a-122">**Example of Scale- Used to show how to manipulate holograms to be bigger or smaller**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="99e2a-123">![パームアップの例](images/HandCoach/PalmUp.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-123">![Example of Palm Up](images/HandCoach/PalmUp.gif)</span></span><br>
        <span data-ttu-id="99e2a-124">**パームアップの例–メニューを表示するために使用することをお勧めします。**</span><span class="sxs-lookup"><span data-stu-id="99e2a-124">**Example of Palm up – Suggested use, to bring up hand menus**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="99e2a-125">![コードの切り替えの例](images/HandCoach/HandFlip.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-125">![Example of HandFlip](images/HandCoach/HandFlip.gif)</span></span><br>
       <span data-ttu-id="99e2a-126">**手動フリップ-メニューを表示する別の方法**</span><span class="sxs-lookup"><span data-stu-id="99e2a-126">**Exmaple of Hand Flip – Another way to bring up Hand Menus**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="99e2a-127">![スクロールの例](images/HandCoach/Scoll.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-127">![Example of Scroll](images/HandCoach/Scoll.gif)</span></span><br>
       <span data-ttu-id="99e2a-128">**スクロールの例–リストまたは長いドキュメントをスクロールするために使用されます。**</span><span class="sxs-lookup"><span data-stu-id="99e2a-128">**Example of Scroll – Used for scrolling a list or a long document**</span></span><br>
    :::column-end:::
:::row-end:::

## <a name="design-concepts"></a><span data-ttu-id="99e2a-129">設計概念</span><span class="sxs-lookup"><span data-stu-id="99e2a-129">Design concepts</span></span>

<span data-ttu-id="99e2a-130">Hololens2 については、instinctual と自然なジェスチャに基づいて手動で相互作用を設計しました。</span><span class="sxs-lookup"><span data-stu-id="99e2a-130">For Hololens2, we designed out hand interactions based on instinctual and natural hand gestures.</span></span> <span data-ttu-id="99e2a-131">これらは、ほとんどのユーザーにとって直観的であると考えられます。したがって、専用のジェスチャの学習時間は作成されませんでした。</span><span class="sxs-lookup"><span data-stu-id="99e2a-131">We believe these to be intuitive to most users and thus did not create dedicated gesture learning moments.</span></span> <span data-ttu-id="99e2a-132">代わりに、このようなジェスチャの詳細については、行き詰まっている可能性のあるユーザー、またはホログラムとの対話に慣れていないユーザーを支援するための手を作成しました。</span><span class="sxs-lookup"><span data-stu-id="99e2a-132">Instead, we created the hand coach to help users who might get stuck or are unfamiliar with interacting with holograms learn about these gestures.</span></span> <span data-ttu-id="99e2a-133">学習に時間がかかりません。ユーザーに対して、ユーザーの操作を実行する方法が最適なオプションであることを示しています。</span><span class="sxs-lookup"><span data-stu-id="99e2a-133">Without a learning moment, we felt that showing users how to perform an action by demonstrating it would be the best option.</span></span> <span data-ttu-id="99e2a-134">この調査では、ユーザーはジェスチャを調べることができましたが、少しのガイダンスが必要でした。</span><span class="sxs-lookup"><span data-stu-id="99e2a-134">In our studies, we found that users were able to figure out the gesture but needed a little guidance.</span></span> <span data-ttu-id="99e2a-135">ユーザーが特定の期間にわたってオブジェクトと対話しないことを検出した場合は、正しい針と指の位置を示す針がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-135">If we detect that a user does not interact with an object for a period, a Hand coach would be triggered demonstrating the correct hand and finger placement.</span></span> 

### <a name="intuitive"></a><span data-ttu-id="99e2a-136">にくい</span><span class="sxs-lookup"><span data-stu-id="99e2a-136">Intuitive</span></span>

<span data-ttu-id="99e2a-137">手をアニメーション化する場合は、明らかにして混乱を shoudn't させる必要があります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-137">When animating hands, it should be obvious and shoudn't cause any confusion.</span></span> <span data-ttu-id="99e2a-138">実際のアニメーションは、その目的を理解するためにユーザーに呼び出すするジェスチャを表しています。</span><span class="sxs-lookup"><span data-stu-id="99e2a-138">The animation of the hands is a representation of the gesture your trying to evoke to the user to understand it's purpose.</span></span> 

<span data-ttu-id="99e2a-139">たとえば、ユーザーがボタンを押すと、ボタンを押すという手がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-139">For example, if you wish a user to press a button, a hand pressing a button would be triggered.</span></span>

<span data-ttu-id="99e2a-140">![例: 手動でタップする](images/HandCoach/NearSelect_unity.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-140">![Example: Hand coach Near Tap](images/HandCoach/NearSelect_unity.gif)</span></span><br>
<span data-ttu-id="99e2a-141">*Gem の近くをタップしたときのデモ*</span><span class="sxs-lookup"><span data-stu-id="99e2a-141">*Hand Coach demonstrating Near Tapping a Gem*</span></span>  

### <a name="hand-scale"></a><span data-ttu-id="99e2a-142">手動スケール</span><span class="sxs-lookup"><span data-stu-id="99e2a-142">Hand scale</span></span>

<span data-ttu-id="99e2a-143">UI メニューを使用してさまざまなサイズをテストしました。そのため、サイズが真だったとしても、menacing のように感じられますが、小さすぎるとジェスチャを確認して理解するのは困難でした。</span><span class="sxs-lookup"><span data-stu-id="99e2a-143">We tested various hand sizes with the UI menus and felt that if the hands were true to size, it gave a menacing feeling but if they were too small then it was hard to see and understand the gesture.</span></span> 

<span data-ttu-id="99e2a-144">**ボイスオーバーとハンド**</span><span class="sxs-lookup"><span data-stu-id="99e2a-144">**Voice over and hands**</span></span>

<span data-ttu-id="99e2a-145">ユーザーは、音声によって1つの命令セットをリッスンできないことを想定しています。</span><span class="sxs-lookup"><span data-stu-id="99e2a-145">Don’t expect users can listen to one set of instructions via voice over and watch different instructions via Hand coach.</span></span> <span data-ttu-id="99e2a-146">Sensory の過負荷を軽減するために、ユーザーが注目したり競争したりするのに役立つ手順を順番に説明します。</span><span class="sxs-lookup"><span data-stu-id="99e2a-146">Sequence your instructions to help users focus versus compete for their attention to reduce sensory overload.</span></span>


## <a name="can-i-create-my-own"></a><span data-ttu-id="99e2a-147">自分で作成できますか。</span><span class="sxs-lookup"><span data-stu-id="99e2a-147">Can I create my own?</span></span>

<span data-ttu-id="99e2a-148">はい、ご利用いただけます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-148">Yes!</span></span> <span data-ttu-id="99e2a-149">ゲーム用に独自の独自のジェスチャを作成し、コミュニティに投稿することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-149">We encourage you to create your own unique gesture for your game and contribute back to the community!</span></span>
<span data-ttu-id="99e2a-150">アプリに使用できる Rigged ハンドの Maya ファイルが提供されています。このファイルは、 <a href="files/HandCoach_MRTK.zip">HandCoach_MRTK.zipダウンロード</a>できます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-150">We have provided a Maya file of a Rigged hand that can be used for your app which can be downloaded here: <a href="files/HandCoach_MRTK.zip"> Download HandCoach_MRTK.zip</a></span></span>

<span data-ttu-id="99e2a-151">![Maya でのアニメーションの例](images/HandCoach/MayaSelect_Gif.gif)</span><span class="sxs-lookup"><span data-stu-id="99e2a-151">![Example of Animated Hands in Maya](images/HandCoach/MayaSelect_Gif.gif)</span></span><br>
<span data-ttu-id="99e2a-152">*Maya のアニメーションの例*</span><span class="sxs-lookup"><span data-stu-id="99e2a-152">*Example of animated Hand Poking a box in Maya*</span></span>


<span data-ttu-id="99e2a-153">**推奨 authoring tool**</span><span class="sxs-lookup"><span data-stu-id="99e2a-153">**Recommended authoring tool**</span></span>

<span data-ttu-id="99e2a-154">3D アーティストの中では、多くの場合、 [Autodesk の Maya](https://www.youtube.com/watch?v=q0K3n0Gf8mA)を使用します。これは、HoloLens を使用して、資産の作成方法を変革できます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-154">Among 3D artists, many choose to use [Autodesk’s Maya which itself is able to use HoloLens](https://www.youtube.com/watch?v=q0K3n0Gf8mA) to transform the way assets are created.</span></span> <span data-ttu-id="99e2a-155">提供されるハンズオンファイルは Maya バイナリファイルであるため、Maya を使用してハンドをアニメーション化してエクスポートすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-155">The hands file provided is a Maya Binary File, so it is recommended to use Maya to animate and export the hands.</span></span> <span data-ttu-id="99e2a-156">別の3D プログラムを使用する場合は、「」を参照<b>してください。FBX</b>: <a href="files/HandCoachMRTK_FBX.zip">HandCoachMRTK_FBX.zipをダウンロード</a>して、独自のコントローラー設定を作成します。</span><span class="sxs-lookup"><span data-stu-id="99e2a-156">If you prefer to use another 3D program, here is a <b>.FBX</b>: <a href="files/HandCoachMRTK_FBX.zip">           Download HandCoachMRTK_FBX.zip</a> to create your own controller setup.</span></span> 

<span data-ttu-id="99e2a-157">提供されている maya ファイルをダウンロードして使用する場合は、unity を0.6 にスケールダウンすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-157">If using the downloadable maya Hand File provided, it is suggested to scale down the hands in unity to 0.6.</span></span>

<span data-ttu-id="99e2a-158">![例: Maya の手動のリモートテストマシン群](images/HandCoach/MayaExample.png)</span><span class="sxs-lookup"><span data-stu-id="99e2a-158">![Example: Hand coach rig in Maya](images/HandCoach/MayaExample.png)</span></span><br>
<span data-ttu-id="99e2a-159">*Rigged ハンド*</span><span class="sxs-lookup"><span data-stu-id="99e2a-159">*Rigged Hands*</span></span>

### <a name="technical-specs"></a><span data-ttu-id="99e2a-160">技術仕様</span><span class="sxs-lookup"><span data-stu-id="99e2a-160">Technical Specs</span></span>

*   <span data-ttu-id="99e2a-161">Maya Ascii 形式で使用できる2つのききファイル</span><span class="sxs-lookup"><span data-stu-id="99e2a-161">Two handed File is available in Maya Ascii format</span></span>
*    <span data-ttu-id="99e2a-162">左手のバイナリ形式では、Right および Left を使用できます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-162">Right and Left Hand is available in Maya Binary format</span></span>
*   <span data-ttu-id="99e2a-163">Maya ファイルを 24 FPS に設定する</span><span class="sxs-lookup"><span data-stu-id="99e2a-163">Set your Maya file to 24 FPS</span></span>
*   <span data-ttu-id="99e2a-164">ファイル内には、2つのききまたはシングルききのジェスチャに使用できる左側と右側のハンドがあります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-164">Within the file, there is a left and right hand which can be used for two handed or single-handed gestures.</span></span> <span data-ttu-id="99e2a-165">右側は、既定でのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-165">The right hand will only be visible by default.</span></span>
*   <span data-ttu-id="99e2a-166">フェードの最初と最後に約10フレームのバッファーを残しておくことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-166">It is suggested to leave a buffer of about 10 frames at the beginning and end for fades</span></span>
*   <span data-ttu-id="99e2a-167">指定したターゲットを使用してオブジェクトをアニメーション化する場合は、既定のボックスまたは Null にアニメーション化することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-167">If animating a object with a specified target, its best practice to animate to a Default box or Null.</span></span>
*   <span data-ttu-id="99e2a-168">ボックスなどの物理的なオブジェクトをアニメーション化する場合、そのベストプラクティスとして、Maya 内の平行移動はアニメーション化せず、Unity またはコードでアニメーション化することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-168">If the hand is animating a physical object such as a box, its best practice to not animate the translation in Maya but wait to animate it in Unity or in Code.</span></span>
*   <span data-ttu-id="99e2a-169">意味のある情報を伝達するには、表示されるアニメーションは1.5 秒でなければなりません</span><span class="sxs-lookup"><span data-stu-id="99e2a-169">Visible Animation should be 1.5 secs for any meaningful information to be conveyed</span></span>
*   <span data-ttu-id="99e2a-170">アニメーションに問題がなければ、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-170">When you feel satisfied with your animation:</span></span>
    *   <span data-ttu-id="99e2a-171">すべてのジョイントおよび焼き付けるキーフレームを選択する</span><span class="sxs-lookup"><span data-stu-id="99e2a-171">Select all joints and bake key frames</span></span>
    *   <span data-ttu-id="99e2a-172">コントローラーを削除し、ジョイントとメッシュを選択して、FBX としてエクスポートします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-172">Delete the Controllers, Select the joints and mesh and export as an FBX</span></span>
    *  <span data-ttu-id="99e2a-173">複数のアニメーションがある場合は、Maya の組み込みゲームエクスポーターを使用できます。https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/Maya/files/Game-Exporter-htm.html</span><span class="sxs-lookup"><span data-stu-id="99e2a-173">If there are Multiple Animations, you can use Maya’s built in Game Exporter: https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/Maya/files/Game-Exporter-htm.html</span></span>

## <a name="exporting-from-maya"></a><span data-ttu-id="99e2a-174">Maya からのエクスポート</span><span class="sxs-lookup"><span data-stu-id="99e2a-174">Exporting from Maya</span></span>

<span data-ttu-id="99e2a-175">アニメーションに問題がなければ</span><span class="sxs-lookup"><span data-stu-id="99e2a-175">After you are satisfied with your animation</span></span>
* <span data-ttu-id="99e2a-176">すべての結合を選択: > 階層を選択します</span><span class="sxs-lookup"><span data-stu-id="99e2a-176">Select all joints: Select > Hierarchy</span></span>

     ![例: メニューの場所](images/HandCoach/Hierarchy.png)<br>
* <span data-ttu-id="99e2a-178">アニメーションを焼き付けるする: アニメーションに切り替える > キー > 焼き付けるアニメーション</span><span class="sxs-lookup"><span data-stu-id="99e2a-178">Bake out your animation: Switch to Animation > Key > Bake Animation</span></span>

     ![例: メニューの場所](images/HandCoach/BakeAnimation.png)<br>
* <span data-ttu-id="99e2a-180">コントローラーのマシン: Outliner > MainR_Grp または MainL_Grp を削除します。</span><span class="sxs-lookup"><span data-stu-id="99e2a-180">Delete the Controller Rig: Outliner > MainR_Grp or MainL_Grp</span></span>

     ![例: メニューの場所](images/HandCoach/ControllerRig.png)<br>

* <span data-ttu-id="99e2a-182">[FBX としてエクスポート]: 選択 JNT + メッシュ: ファイル > エクスポートの選択 (オプションボックス) > エクスポートの選択</span><span class="sxs-lookup"><span data-stu-id="99e2a-182">Export as FBX: Select JNT + Mesh: File > Export Selection (option box) > Export Selection</span></span>

     ![例: メニューの場所](images/HandCoach/OptionBox.png)<br>

     ![例: メニューの場所](images/HandCoach/SelectionExport.png)<br>

     ![例: メニューの場所](images/HandCoach/FBXSelection.png)<br>


 <span data-ttu-id="99e2a-186">FBX としてエクスポートし、Unity に導入する場合は、針を0.6 にスケーリングします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-186">When exporting as a FBX and brought into Unity, scale the hands down to 0.6.</span></span> <span data-ttu-id="99e2a-187">これは、実際の表示に最適なバランスであることがわかりました。</span><span class="sxs-lookup"><span data-stu-id="99e2a-187">We found that this was perfect balance for displaying the hands.</span></span> 

<span data-ttu-id="99e2a-188">![例: Unity の設定](images/HandCoach/HandHintScale.png)</span><span class="sxs-lookup"><span data-stu-id="99e2a-188">![Example: Unity Settings](images/HandCoach/HandHintScale.png)</span></span><br>
<span data-ttu-id="99e2a-189">*MRTK で HandCoach_R prefab の Unity 設定が見つかりました*</span><span class="sxs-lookup"><span data-stu-id="99e2a-189">*Unity Settings for HandCoach_R prefab found in MRTK*</span></span>


## <a name="implementing-hands-into-your-unity-project"></a><span data-ttu-id="99e2a-190">Unity プロジェクトにハンズオンを実装する</span><span class="sxs-lookup"><span data-stu-id="99e2a-190">Implementing Hands into your Unity project</span></span>

### <a name="best-practices"></a><span data-ttu-id="99e2a-191">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="99e2a-191">Best practices</span></span>
*    <span data-ttu-id="99e2a-192">Unity を0.6 にスケールダウンすることをお勧めします</span><span class="sxs-lookup"><span data-stu-id="99e2a-192">It is suggested to scale down the hands in unity to 0.6</span></span>
*   <span data-ttu-id="99e2a-193">針は2回再生され、完了していない場合はジェスチャが完了するまで連続してループされます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-193">Hands should be played twice and if not completed then continuously looped until gesture is completed.</span></span> <span data-ttu-id="99e2a-194">ユーザーが登録してジェスチャを確認するまでの時間を確保するために、針を2回ループする必要があります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-194">The hands should be looped twice to ensure the user had time to register and see the gesture.</span></span> <span data-ttu-id="99e2a-195">ループの間で、ハンドインとフェードアウトを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-195">The hands should fade in and out between loops.</span></span> 
 *  <span data-ttu-id="99e2a-196">ユーザーの手が HL2 カメラによって表示されていても、ユーザーが必要な対話を行っていない場合は、10秒後にハンドが表示されます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-196">If user’s hands are visible by HL2 cameras but users are not doing the interaction needed of them the hands will appear after 10 seconds.</span></span>
*   <span data-ttu-id="99e2a-197">ユーザーの手が HL2 カメラによって表示されない場合は、5秒後に針が表示されます。</span><span class="sxs-lookup"><span data-stu-id="99e2a-197">If user’s hands are NOT visible by HL2 cameras, the hands will appear after 5 seconds.</span></span>  
*   <span data-ttu-id="99e2a-198">アニメーションの途中でユーザーの手が HL2 カメラによって視覚的に追跡されている場合は、アニメーションが完了してフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-198">If user’s hands are visibly tracked by HL2 cameras in the middle of the animation, the animation will complete and fade out.</span></span>
*   <span data-ttu-id="99e2a-199">ボイスオーバーを含む場合は、ハンドのジェスチャに対応することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-199">If you are including voice over, we suggest that it corresponds to the gesture of the hand.</span></span>
*   <span data-ttu-id="99e2a-200">少なくとも1回は、ユーザーがスタックしていることが検出された場合にのみ、ジェスチャを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="99e2a-200">If you have taught the hands at least once, only repeat the gesture if its detected that the user is stuck.</span></span>
*   <span data-ttu-id="99e2a-201">特定の指と位置が重要である場合は、アニメーションの微妙な差異をユーザーがはっきりと確認できるようにします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-201">If specific finger/hand positions are critical, ensure users can clearly see these nuances in the animation.</span></span> <span data-ttu-id="99e2a-202">最も重要な部分が明確に表示されるように、角度を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="99e2a-202">Try angling the hands so the most important parts are clearly visible.</span></span> 
* <span data-ttu-id="99e2a-203">手にひずみがある場合は、Unity の品質設定にアクセスして、ボーンの量を増やす必要があります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-203">If you notice distortion on the hands, you need to go to Unity's Quality settings increase the amount of bones.</span></span> 
 <span data-ttu-id="99e2a-204">Unity の編集 > プロジェクトの設定 > 品質 > 他の > Blend の重みにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="99e2a-204">Go to Unity's Edit > Project Settings > Quality > Other > Blend Weights.</span></span> <span data-ttu-id="99e2a-205">Smooth 関節を表示するには、"4 つの骨" が選択されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="99e2a-205">Make sure "4 bones" are selected to see Smooth Joints.</span></span> 

   ![例: メニューの場所](images/HandCoach/ProjectSettings.png)<br>





### <a name="what-to-avoid"></a><span data-ttu-id="99e2a-207">避けるべきこと</span><span class="sxs-lookup"><span data-stu-id="99e2a-207">What to avoid</span></span>
* <span data-ttu-id="99e2a-208">ハンドのサイズが大きすぎます</span><span class="sxs-lookup"><span data-stu-id="99e2a-208">Scaling the Hands too large</span></span>
* <span data-ttu-id="99e2a-209">ユーザーに近すぎるユーザーを配置する</span><span class="sxs-lookup"><span data-stu-id="99e2a-209">placing the Hands too close to the user</span></span>
* <span data-ttu-id="99e2a-210">ハンズオンは、1回だけ学習する必要があります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-210">Hands should only be taught once.</span></span> <span data-ttu-id="99e2a-211">教育を超えると混乱を招き、messiness</span><span class="sxs-lookup"><span data-stu-id="99e2a-211">Over teaching can cause confusion and messiness</span></span>
*   <span data-ttu-id="99e2a-212">Unity に取り込むには、最新の MRTK をこちらからダウンロードしてください。https://github.com/microsoft/MixedRealityToolkit-Unity</span><span class="sxs-lookup"><span data-stu-id="99e2a-212">Bringing it into Unity, please download the latest MRTK  here: https://github.com/microsoft/MixedRealityToolkit-Unity</span></span>
    *   <span data-ttu-id="99e2a-213">素材: Teaching_Hand2</span><span class="sxs-lookup"><span data-stu-id="99e2a-213">Material: Teaching_Hand2</span></span>
    *   <span data-ttu-id="99e2a-214">スクリプト: <a href= "https://github.com/MixedRealityToolkit-Unity/blob/'HandCoachUX'/Documentation/README_HandCoach.md">mrtk</a>での mrtk のガイドラインを参照してください。</span><span class="sxs-lookup"><span data-stu-id="99e2a-214">Scripts: Refer to MRTK guidelines for <a href= "https://github.com/MixedRealityToolkit-Unity/blob/'HandCoachUX'/Documentation/README_HandCoach.md"> MRTK hand coach </a></span></span>
    *   <span data-ttu-id="99e2a-215">プロジェクトごとの設定</span><span class="sxs-lookup"><span data-stu-id="99e2a-215">Per- project setting</span></span>
        *   <span data-ttu-id="99e2a-216">UWP に設定されたシーン: 命令は、「Windows Mixed Reality 用の[Unity プロジェクトの構成](Configure-Unity-Project.md)」にあります。</span><span class="sxs-lookup"><span data-stu-id="99e2a-216">Scene set to UWP: Instruction can be found on the [Configure Unity Project](Configure-Unity-Project.md) for Windows Mixed Reality</span></span>

## <a name="see-also"></a><span data-ttu-id="99e2a-217">関連項目</span><span class="sxs-lookup"><span data-stu-id="99e2a-217">See also</span></span>
* [<span data-ttu-id="99e2a-218">相互作用-基本</span><span class="sxs-lookup"><span data-stu-id="99e2a-218">Interaction-fundamentals</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="99e2a-219">資産の作成プロセス</span><span class="sxs-lookup"><span data-stu-id="99e2a-219">Asset Creation Process</span></span>](asset-creation-process.md)
* [<span data-ttu-id="99e2a-220">ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="99e2a-220">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="99e2a-221">ツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="99e2a-221">Install the Tools</span></span>](install-the-tools.md)
* [<span data-ttu-id="99e2a-222">Unity プロジェクトの構成</span><span class="sxs-lookup"><span data-stu-id="99e2a-222">Configure Unity Project</span></span>](Configure-Unity-Project.md)
* [<span data-ttu-id="99e2a-223">Unity 開発の概要</span><span class="sxs-lookup"><span data-stu-id="99e2a-223">Unity development overview</span></span>](unity-development-overview.md)
* [<span data-ttu-id="99e2a-224">MRTK 101</span><span class="sxs-lookup"><span data-stu-id="99e2a-224">MRTK 101</span></span>](mrtk-101.md)
