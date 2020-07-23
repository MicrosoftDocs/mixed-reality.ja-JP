---
title: 入門チュートリアル - 5. ソルバーを使用した動的なコンテンツの作成
description: このコースでは、Mixed Reality Toolkit (MRTK) を使用して Mixed Reality アプリケーションを作成する方法について説明します。
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: cbeaa8b65b7aecc0600294b3739fedfb903e568e
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86306653"
---
# <a name="5-creating-dynamic-content-using-solvers"></a><span data-ttu-id="f011b-105">5.ソルバーを使用した動的なコンテンツの作成</span><span class="sxs-lookup"><span data-stu-id="f011b-105">5. Creating dynamic content using Solvers</span></span>

## <a name="overview"></a><span data-ttu-id="f011b-106">概要</span><span class="sxs-lookup"><span data-stu-id="f011b-106">Overview</span></span>

<span data-ttu-id="f011b-107">このチュートリアルでは、複雑な空間配置シナリオを解決するために、MRTK で使用できる "ソルバー" という配置ツールを使用して、ホログラムを動的に配置する方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="f011b-107">In this tutorial, you will explore ways to dynamically place holograms using the MRTK's available placement tools, known as Solvers, to solve complex spatial placement scenarios.</span></span> <span data-ttu-id="f011b-108">MRTK では、ソルバーとは、シーン内に存在する自分、ユーザー、他のゲーム オブジェクトをオブジェクトが追跡できるようにするために使用される、スクリプトと動作のシステムです。</span><span class="sxs-lookup"><span data-stu-id="f011b-108">In the MRTK, Solvers are a system of scripts and behaviors used to allow objects to follow you, the user, or other game objects in the scene.</span></span> <span data-ttu-id="f011b-109">これらは、特定の場所にスナップして、アプリをさらに直感的にするために使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="f011b-109">They can also be used to snap to certain positions, making your app more intuitive.</span></span>

## <a name="objectives"></a><span data-ttu-id="f011b-110">目標</span><span class="sxs-lookup"><span data-stu-id="f011b-110">Objectives</span></span>

* <span data-ttu-id="f011b-111">MRTK ソルバーの紹介</span><span class="sxs-lookup"><span data-stu-id="f011b-111">Introduce the MRTK's Solvers</span></span>
* <span data-ttu-id="f011b-112">ソルバーを使用してユーザーをオブジェクトに誘導する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="f011b-112">Learn how to use Solvers to direct the user to objects</span></span>
* <span data-ttu-id="f011b-113">ソルバーを使用してオブジェクトの位置を変更する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="f011b-113">Learn how to use Solvers to reposition objects</span></span>

## <a name="location-of-solvers-in-the-mrtk"></a><span data-ttu-id="f011b-114">MRTK でのソルバーの場所</span><span class="sxs-lookup"><span data-stu-id="f011b-114">Location of Solvers in the MRTK</span></span>

 <span data-ttu-id="f011b-115">MRTK のソルバーは、MRTK SDK フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="f011b-115">The MRTK's Solvers are located in the MRTK SDK folder.</span></span> <span data-ttu-id="f011b-116">プロジェクトで使用可能なソルバーを表示するには、[プロジェクト] ウィンドウで、 **[アセット]**  >  **[MRTK]**  >  **[SDK]**  >  **[機能]**  >  **[ユーティリティ]**  >  **[ソルバー]** の順に移動します。</span><span class="sxs-lookup"><span data-stu-id="f011b-116">To see the available Solvers in your project, in the Project window, navigate to **Assets** > **MRTK** > **SDK** > **Features** > **Utilities** > **Solvers**:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section1-step1-1.png)

<span data-ttu-id="f011b-118">このチュートリアルでは、Directional Indicator Solver と Tap To Place Solver の実装方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f011b-118">In this tutorial, we will review the implementation of the Directional Indicator Solver and the Tap To Place Solver.</span></span> <span data-ttu-id="f011b-119">MRTK で利用可能なすべてのソルバーの詳細については、[MRTK ドキュメント ポータル](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)の[ソルバー](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html)に関するガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-119">To learn more about the full range of Solvers available in the MRTK, you can refer to the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

> [!NOTE]
> <span data-ttu-id="f011b-120">Directional Indicator Solver は、上記の [Solvers] フォルダーには含まれていません。これは試験的な機能であるため、[アセット] > [MRTK] > [SDK] > [試験的] > [機能] > [ユーティリティ] フォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="f011b-120">The Directional Indicator Solver is not located in the Solvers folders referenced above, but in the Assets > MRTK > SDK > Experimental > Features > Utilities folders, because it is an experimental feature.</span></span>

## <a name="using-the-directional-indicator-solver-to-direct-the-user-to-objects"></a><span data-ttu-id="f011b-121">Directional Indicator Solver を使用してユーザーをオブジェクトに誘導する</span><span class="sxs-lookup"><span data-stu-id="f011b-121">Using the Directional Indicator Solver to direct the user to objects</span></span>

<span data-ttu-id="f011b-122">[プロジェクト] ウィンドウで、 **[アセット]**  >  **[MRTK.Tutorials.GettingStarted]**  >  **[Prefabs]\(プレハブ\)** フォルダーの順に移動し、 **[シェブロン]** プレハブをクリックして [階層] ウィンドウにドラッグします。次に、[変換] の **[位置]** を X = 0, Y = 0, Z = 2 に設定して、RoverExplorer オブジェクトの近くに配置します。</span><span class="sxs-lookup"><span data-stu-id="f011b-122">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** folder, click-and-drag the **Chevron** prefab into the Hierarchy window, and set it's Transform **Position** to X = 0, Y = 0, Z = 2 to position it near the RoverExplorer object:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="f011b-124">シーンに含まれるカメラや他のアイコンがオブジェクトを見にくくしていたり操作の邪魔になったりしている場合は、上の図に示すように、<a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">ギズモをオフに切り替える</a>ことによってこれらを非表示にできます。</span><span class="sxs-lookup"><span data-stu-id="f011b-124">If you find that the camera or any other icons in your scene are hiding the objects or are distracting, you can hide these by <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">toggling the Gizmos</a> to the off position, as shown in the image above.</span></span> <span data-ttu-id="f011b-125">ギズモ メニューと、それを使用してシーン ビューを最適化する方法の詳細については、Unity の <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">ギズモ メニュー</a>に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-125">To learn more about the Gizmos menu and how you can use it to optimize your scene view, you can refer to Unity's <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">Gizmos menu</a> documentation.</span></span>

<span data-ttu-id="f011b-126">新しく追加したシェブロン オブジェクトの名前を **Indicator** に変更し、[インスペクター] ウィンドウで **[コンポーネントの追加]** ボタンを使用して、**DirectionalIndicator** と **Directional Indicator Controller (Script)** コンポーネントを追加します。</span><span class="sxs-lookup"><span data-stu-id="f011b-126">Rename the newly added Chevron object **Indicator**, then in the Inspector window, use the **Add Component** button to add the **DirectionalIndicator** and the **Directional Indicator Controller (Script)** component:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-2.png)

> [!NOTE]
> <span data-ttu-id="f011b-128">ソルバーを追加する場合 (この例では DirectionalIndicator コンポーネント)、ソルバーで SolverHandler コンポーネントが必要になるため、それが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="f011b-128">When you add a Solver, in this case, the DirectionalIndicator component, the SolverHandler component is automatically added because Solvers require it.</span></span>

> [!NOTE]
> <span data-ttu-id="f011b-129">Directional Indicator Controller (Script) は MRTK の一部ではありませんが、チュートリアル アセットには含まれていました。</span><span class="sxs-lookup"><span data-stu-id="f011b-129">The Directional Indicator Controller (Script) is not part of the MRTK but was included with the tutorial assets.</span></span>

<span data-ttu-id="f011b-130">DirectionalIndicator および SolverHandler コンポーネントを次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="f011b-130">Configure the DirectionalIndicator and SolverHandler components as follows:</span></span>

* <span data-ttu-id="f011b-131">**SolverHandler** コンポーネントの **[Tracked Target Type]\(追跡対象の種類\)** が **[ヘッド]** に設定されていることを確認します</span><span class="sxs-lookup"><span data-stu-id="f011b-131">Verify that the **SolverHandler** component's **Tracked Target Type** is set to **Head**</span></span>
* <span data-ttu-id="f011b-132">**RoverExplorer** を、[階層] ウィンドウから **[None (Transform)]\(なし (変換)\)** フィールドにドラッグして、**DirectionalIndicator** コンポーネントの **[Directional Target]\(方向のターゲット\)** に割り当てます</span><span class="sxs-lookup"><span data-stu-id="f011b-132">Assign the **RoverExplorer** to the **DirectionalIndicator** component's **Directional Target** by dragging it from the Hierarchy window into the **None (Transform)** field</span></span>
* <span data-ttu-id="f011b-133">**[View Offset]\(表示オフセット\)** を 0.2 に変更します</span><span class="sxs-lookup"><span data-stu-id="f011b-133">Change the **View Offset** to 0.2</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-3.png)

<span data-ttu-id="f011b-135">[再生] ボタンを押してゲーム モードに入り、マウスの右ボタンを押したままにしてマウスを左右に動かし、視線入力の方向を回転させます。次の点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-135">Press the Play button to enter Game mode, press-and-hold the right mouse button while moving your mouse to the left or right to rotate your gaze direction, and notice the following:</span></span>

* <span data-ttu-id="f011b-136">RoverExplorer オブジェクトから視線を外すと、Indicator オブジェクトが表示され、RoverExplorer オブジェクトを指します</span><span class="sxs-lookup"><span data-stu-id="f011b-136">When you look away from the RoverExplorer object, the Indicator object will appear and point towards the RoverExplorer object</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-4.png)

> [!NOTE]
> <span data-ttu-id="f011b-138">[シーン] ウィンドウにカメラの光線が表示されない場合は、上の図に示すように、ギズモ メニューが有効になっていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-138">If you don't see the camera ray in your Scene window, make sure your Gizmos menu is enabled, as shown in the image above.</span></span>

> [!TIP]
> <span data-ttu-id="f011b-139">エディター内入力シミュレーションの使用方法については、[MRTK ドキュメント ポータル](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)で「[エディター内ハンド入力シミュレーションを使用したシーンのテスト](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene)」ガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-139">To learn how to use the in-editor input simulation, you can refer to the [Using the In-Editor Hand Input Simulation to test a scene](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

> [!TIP]
> <span data-ttu-id="f011b-140">コンピューターにマイクがある場合は、"toggle diagnostics"(診断をトグル) という音声コマンドを使用することにより、[ゲーム] ウィンドウに表示される診断パネルのアクティブ状態を簡単に切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="f011b-140">If your computer has a microphone, you can easily toggle the active state of the Diagnostics panel that appears in the Game window by using the speech command "toggle diagnostics."</span></span> <span data-ttu-id="f011b-141">または、[MRTK Configuration Profile]\(MRTK 構成プロファイル\) > [診断] > [Enable Diagnostics System]\(診断システムを有効にする\) でも無効にできます。</span><span class="sxs-lookup"><span data-stu-id="f011b-141">Alternatively, you can disable it in the MRTK Configuration Profile > Diagnostics > Enable Diagnostics System.</span></span> <span data-ttu-id="f011b-142">ただし、開発中は、通常は診断システムをアクティブにしておくことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f011b-142">However, it is generally recommended to keep the Diagnostics System active during development.</span></span>

## <a name="using-the-tap-to-place-solver-to-reposition-objects"></a><span data-ttu-id="f011b-143">Tap to Place Solver を使用してオブジェクトの位置を変更する</span><span class="sxs-lookup"><span data-stu-id="f011b-143">Using the Tap to Place Solver to reposition objects</span></span>

<span data-ttu-id="f011b-144">[階層] ウィンドウで、RoverExplorer > **RoverAssembly** オブジェクトの順に選択します。次に、[インスペクター] ウィンドウで **[コンポーネントの追加]** ボタンを使用し、**Tap To Place (Script)** コンポーネントを追加して、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="f011b-144">In the Hierarchy window, select the RoverExplorer > **RoverAssembly** object, then in the Inspector window, use the **Add Component** button to add the **Tap To Place (Script)** component, and configure it as follows:</span></span>

* <span data-ttu-id="f011b-145">**SolverHandler** コンポーネントの **[Tracked Target Type]\(追跡対象の種類\)** が **[ヘッド]** に設定されていることを確認します</span><span class="sxs-lookup"><span data-stu-id="f011b-145">Verify that the **SolverHandler** component's **Tracked Target Type** is set to **Head**</span></span>
* <span data-ttu-id="f011b-146">**[Keep Orientation Vertical]\(向きを垂直に保つ\)** チェックボックスをオンにします</span><span class="sxs-lookup"><span data-stu-id="f011b-146">Check the **Keep Orientation Vertical** checkbox</span></span>
* <span data-ttu-id="f011b-147">**[Magnetic Surfaces]\(磁気サーフェス\)**  >  **[Element 0]\(要素 0\)** ドロップダウンから、 **[Spatial Awareness]\(空間認識\)**  以外のすべてのオプションをオフにします</span><span class="sxs-lookup"><span data-stu-id="f011b-147">From the **Magnetic Surfaces** > **Element 0** dropdown, uncheck all options expect **Spatial Awareness**</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-1.png)

> [!NOTE]
> <span data-ttu-id="f011b-149">[Magnetic Surfaces]\(磁気サーフェス\) 設定により、オブジェクトを配置するときに Tap To Place (Script) コンポーネントで検出できるオブジェクトが決定します。</span><span class="sxs-lookup"><span data-stu-id="f011b-149">The Magnetic Surfaces setting determines which objects the Tap To Place (Script) component can detect when placing an object.</span></span> <span data-ttu-id="f011b-150">この設定を [Spatial Awareness]\(空間認識\) のみに変更することにより、Tap To Place (Script) コンポーネントは、[Spatial Awareness]\(空間認識\) という名前の Unity レイヤーのオブジェクトにのみ Rover を配置できるようになります。この Unity レイヤーは、既定で HoloLens によって生成される空間認識メッシュです。</span><span class="sxs-lookup"><span data-stu-id="f011b-150">By changing the setting to only Spatial Awareness, the Tap To Place (Script) component will only be able to place the Rover on objects on the Unity Layer named Spatial Awareness, which by default is the Spatial Awareness Mesh generated by the HoloLens.</span></span>
>
><span data-ttu-id="f011b-151">レイヤーの詳細については、Unity の<a href="https://docs.unity3d.com/Manual/Layers.html" target="_blank">レイヤー</a>に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-151">To learn more about Layers, you can refer to Unity's <a href="https://docs.unity3d.com/Manual/Layers.html" target="_blank">Layers</a> documentation.</span></span>

> [!TIP]
> <span data-ttu-id="f011b-152">Tap To Place 機能を HoloLens でテストするときにこの空間認識メッシュを表示したい場合は、空間メッシュ オブザーバーの表示オプションを一時的に [表示] に設定できます。</span><span class="sxs-lookup"><span data-stu-id="f011b-152">If you want to see the Spatial Awareness Mesh when testing the Tap To Place functionality on your HoloLens, you can temporarily set the Spatial Mesh Observer's Display Option to Visible.</span></span> <span data-ttu-id="f011b-153">表示オプションを変更する方法については、「[空間認識表示オプションの変更](mr-learning-base-03.md#changing-the-spatial-awareness-display-option)」の手順を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-153">For a reminder on how to change the Display Option, you can refer to the [Changing the Spatial Awareness Display Option](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) instructions.</span></span>

<span data-ttu-id="f011b-154">[階層] ウィンドウで RoverAssembly オブジェクトを選択したまま、[インスペクター] ウィンドウで **On Placing Started ()** イベントを見つけて、 **+** アイコンをクリックし、新しいイベントを追加します。</span><span class="sxs-lookup"><span data-stu-id="f011b-154">With the RoverAssembly object still selected in the Hierarchy window, in the Inspector window, locate the **On Placing Started ()** event and click the **+** icon to add a new event:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-2.png)

<span data-ttu-id="f011b-156">イベントを次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="f011b-156">Configure the event as follows:</span></span>

* <span data-ttu-id="f011b-157">**RoverAssembly** オブジェクトを、[階層] ウィンドウから **[None (Object)]\(なし (オブジェクト)\)** フィールドにドラッグして、On Placing Started () イベントのリスナーとして割り当てます</span><span class="sxs-lookup"><span data-stu-id="f011b-157">Assign the **RoverAssembly** object as a listener for the On Placing Started () event by dragging it from the Hierarchy window into the **None (Object)** field</span></span>
* <span data-ttu-id="f011b-158">**[関数なし]** ドロップダウンから、**TapToPlace** > **float SurfaceNormalOffset** の順に選択し、イベントがトリガーされたときの SurfaceNormalOffset プロパティ値を更新します</span><span class="sxs-lookup"><span data-stu-id="f011b-158">From the **No Function** dropdown, select **TapToPlace** > **float SurfaceNormalOffset** to update the SurfaceNormalOffset property value when the event is triggered</span></span>
* <span data-ttu-id="f011b-159">引数が **0** に設定されていることを確認します</span><span class="sxs-lookup"><span data-stu-id="f011b-159">Verify that the argument is set to **0**</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-3.png)

<span data-ttu-id="f011b-161">[階層] ウィンドウの何もない場所を右クリックし、 **[3D オブジェクト]**  >  **[キューブ]** の順に選択して、地面を表す一時オブジェクトを作成し、**Transform** コンポーネントを次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="f011b-161">In the Hierarchy window, right-click on an empty spot and select **3D Object** > **Cube**, to create a temporary object representing the ground, and configure the **Transform** component as follows:</span></span>

* <span data-ttu-id="f011b-162">**位置**:X = 0、Y = -1.65、Z = 6</span><span class="sxs-lookup"><span data-stu-id="f011b-162">**Position**: X = 0, Y = -1.65, Z = 6</span></span>
* <span data-ttu-id="f011b-163">**回転**:X = 0、Y = 0、Z = 0</span><span class="sxs-lookup"><span data-stu-id="f011b-163">**Rotation**: X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="f011b-164">**スケール**:X = 10、Y = 0.2、Z = 10</span><span class="sxs-lookup"><span data-stu-id="f011b-164">**Scale**: X = 10, Y = 0.2, Z = 10</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-4.png)

<span data-ttu-id="f011b-166">[階層] ウィンドウで一時的な [キューブ] を選択したまま、[インスペクター] ウィンドウの **[レイヤー]** ドロップダウンを使用して、 **[Spatial Awareness]\(空間認識\)** レイヤーのみが含まれるようにキューブのレイヤー設定を変更します。</span><span class="sxs-lookup"><span data-stu-id="f011b-166">With the temporary Cube still selected in the Hierarchy window, in the Inspector window, use the **Layers** dropdown to change the Cube's Layer setting only to include the **Spatial Awareness** layer:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-5.png)

<span data-ttu-id="f011b-168">[再生] ボタンを押してゲーム モードに入り、マウスの右ボタンを押したまま、視線入力が RoverAssembly オブジェクトに当たるまでマウスを下方向に移動します。</span><span class="sxs-lookup"><span data-stu-id="f011b-168">Press the Play button to enter Game mode, then press-and-hold the right mouse button while moving your mouse down until the gaze hit's the RoverAssembly object:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-6.png)

<span data-ttu-id="f011b-170">マウスの左ボタンをクリックして、Tap To Place プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="f011b-170">Click the left mouse button to start the tap-to-place process:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-7.png)

<span data-ttu-id="f011b-172">マウスの右ボタンを押したままにしてマウスを左右に動かし、視線入力の方向を回転させます。適切な位置に配置できたら、マウスの左ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f011b-172">Press-and-hold the right mouse button while moving your mouse to the left or right to rotate your gaze direction, when you are happy with the placement, click the left mouse button:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-8.png)

<span data-ttu-id="f011b-174">ゲーム モードでの機能のテストが完了したら、キューブ オブジェクトを右クリックし、 **[削除]** を選択して、オブジェクトをシーンから削除します。</span><span class="sxs-lookup"><span data-stu-id="f011b-174">Once you are done testing the feature in the Game mode, right-click on the Cube object and select **Delete** to remove it from the scene:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-9.png)

## <a name="congratulations"></a><span data-ttu-id="f011b-176">結論</span><span class="sxs-lookup"><span data-stu-id="f011b-176">Congratulations</span></span>

<span data-ttu-id="f011b-177">このチュートリアルでは、MRTK の Directional Indicator Solver を使用して、UI 要素でユーザーを直感的にオブジェクトに誘導する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="f011b-177">In this tutorial, you learned how to use the MRTK's Directional Indicator Solver to have a UI element intuitively direct the user to objects.</span></span> <span data-ttu-id="f011b-178">Tap To Place Solver を使用してオブジェクトの位置を簡単に変更する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="f011b-178">You also learned how to use the Tap To Place Solver to reposition objects easily.</span></span>

<span data-ttu-id="f011b-179">MRTK に含まれるこれらのソルバーや他のソルバーについて学ぶには、[MRTK ドキュメント ポータル](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)の[ソルバー](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html)に関するガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f011b-179">To learn more about these and other solvers included with the MRTK,  you can refer to the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

[<span data-ttu-id="f011b-180">次のチュートリアル:6.ユーザー インターフェイスの作成</span><span class="sxs-lookup"><span data-stu-id="f011b-180">Next Tutorial: 6. Creating user interfaces</span></span>](mr-learning-base-06.md)
