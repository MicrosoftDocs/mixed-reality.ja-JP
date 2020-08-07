---
title: 2. プロジェクトと最初のアプリケーションの初期化
description: Unreal Engine 4 と Mixed Reality ツールキット UX ツール プラグインを使用して簡単なチェス アプリを構築するためのチュートリアル シリーズのパート 6 の 2
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, Mixed Reality, チュートリアル, 入門, mrtk, uxt, UX ツール, ドキュメント
ms.openlocfilehash: 1fce9c34b1d31c56eb628979089399926f3cbf51
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376510"
---
# <a name="2-initializing-your-project-and-first-application"></a><span data-ttu-id="23e00-104">2.プロジェクトと最初のアプリケーションの初期化</span><span class="sxs-lookup"><span data-stu-id="23e00-104">2. Initializing your project and first application</span></span>

## <a name="overview"></a><span data-ttu-id="23e00-105">概要</span><span class="sxs-lookup"><span data-stu-id="23e00-105">Overview</span></span>

<span data-ttu-id="23e00-106">この最初のチュートリアルでは、HoloLens 2 用の新しい Unreal アプリケーションの使用を開始します。</span><span class="sxs-lookup"><span data-stu-id="23e00-106">In this first tutorial, you'll get started with a new Unreal application for HoloLens 2.</span></span> <span data-ttu-id="23e00-107">これには、HoloLens プラグインの追加、レベルの作成と照明、およびゲーム ボードとチェスの駒の設定が含まれます。</span><span class="sxs-lookup"><span data-stu-id="23e00-107">This is going to include adding the HoloLens plugin, creating and lighting a level, and populating it with a game board and chess piece.</span></span> <span data-ttu-id="23e00-108">3D チェスの駒とオブジェクト マテリアルには、事前に作成された資産を使用するため、何もないところからモデリングする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="23e00-108">You'll be using pre-made assets for the 3D chess piece and object materials, so don't worry about modeling anything from scratch.</span></span> <span data-ttu-id="23e00-109">このチュートリアルを完了するまでに、複合現実に対応できる空のキャンバスが完成します。</span><span class="sxs-lookup"><span data-stu-id="23e00-109">By the end of this tutorial you'll have a blank canvas that's ready for mixed reality.</span></span>

<span data-ttu-id="23e00-110">続行する前に、「[はじめに](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch1)」ページにあるすべての前提条件を確認してください。</span><span class="sxs-lookup"><span data-stu-id="23e00-110">Before continuing, make sure you have all the prerequisites from the [Getting Started](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch1) page.</span></span>

## <a name="objectives"></a><span data-ttu-id="23e00-111">目標</span><span class="sxs-lookup"><span data-stu-id="23e00-111">Objectives</span></span>
* <span data-ttu-id="23e00-112">HoloLens 開発用の Unreal プロジェクトの構成</span><span class="sxs-lookup"><span data-stu-id="23e00-112">Configuring an Unreal project for HoloLens development</span></span>
* <span data-ttu-id="23e00-113">資産のインポートとシーンのセットアップ</span><span class="sxs-lookup"><span data-stu-id="23e00-113">Importing assets and setting up a scene</span></span>
* <span data-ttu-id="23e00-114">ブループリントを使用したアクターとスクリプトレベルのイベントの作成</span><span class="sxs-lookup"><span data-stu-id="23e00-114">Creating Actors and script-level events with blueprints</span></span>

## <a name="creating-a-new-unreal-project"></a><span data-ttu-id="23e00-115">新しい Unreal プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="23e00-115">Creating a new Unreal project</span></span>
<span data-ttu-id="23e00-116">最初に必要なのは、作業するプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="23e00-116">The first thing you need is a project to work with.</span></span> <span data-ttu-id="23e00-117">HoloLens 用の Unreal アプリを初めて作成する場合は、Epic Launcher から[サポート ファイルをダウンロードする](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch6#packaging-and-deploying-the-app)必要があります。</span><span class="sxs-lookup"><span data-stu-id="23e00-117">If this is your first time creating an Unreal app for HoloLens, you'll need to [download supporting files](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch6#packaging-and-deploying-the-app) from the Epic Launcher.</span></span>

1. <span data-ttu-id="23e00-118">Unreal Engine を起動します。</span><span class="sxs-lookup"><span data-stu-id="23e00-118">Launch Unreal Engine</span></span>

2. <span data-ttu-id="23e00-119">**[New Project Categories]\(新規プロジェクトのカテゴリ\)** で、 **[ゲーム]** を選択して **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-119">Select **Games** in **New Project Categories** and click **Next**.</span></span> 

![ゲーム プロジェクト テンプレートの選択](images/unreal-uxt/2-gamestemplate.png)

3. <span data-ttu-id="23e00-121">**[Blank]\(空のプロジェクト\)** テンプレートを選択して **[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-121">Select the **Blank** Template and click **Next**.</span></span> 

![[Blank]\(空のプロジェクト\) テンプレートを選択する](images/unreal-uxt/2-template.PNG)

4. <span data-ttu-id="23e00-123">**[C++]** 、 **[Scalable 3D or 2D]\(スケーラブル 3D または 2D\)、[Mobile/Tablet]\(モバイル/タブレット\)** 、 **[No Starter Content]\(スターター コンテンツを有効にしない\)** を **[Project Settings]\(プロジェクト設定\)** として設定し、保存場所を選択して、 **[Create Project]\(プロジェクトの作成)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-123">Set **C++**, **Scalable 3D or 2D, Mobile/Tablet**, and **No Starter Content** as your **Project Settings**, then choose a save location and click **Create Project**.</span></span> 

> [!NOTE]
> <span data-ttu-id="23e00-124">UX Tools プラグインをビルドするには、ブループリント プロジェクトではなく、C++ プロジェクトを選択する必要があります。UX Tools プラグインは、この後のセクション 4 でセットアップします。</span><span class="sxs-lookup"><span data-stu-id="23e00-124">You must select a C++ project rather than a Blueprint project in order to build the UX Tools plugin, which you'll be setting up later on in section 4.</span></span>

![最初のプロジェクト設定](images/unreal-uxt/2-project-settings.PNG)

<span data-ttu-id="23e00-126">Unreal エディターでプロジェクトが自動的に開きます。つまり、次のセクションに進む準備はできています。</span><span class="sxs-lookup"><span data-stu-id="23e00-126">The project should open up automatically in the Unreal editor, which means you're ready for the next section.</span></span>

## <a name="enabling-required-plugins"></a><span data-ttu-id="23e00-127">必要なプラグインの有効化</span><span class="sxs-lookup"><span data-stu-id="23e00-127">Enabling required plugins</span></span>
<span data-ttu-id="23e00-128">オブジェクトをシーンに追加する前に、2 つのプラグインを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="23e00-128">Before you start adding objects to the scene you'll need to enable two plugins.</span></span>

1. <span data-ttu-id="23e00-129">**[編集] > [プラグイン]** を開き、組み込みオプション リストから **[拡張現実]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="23e00-129">Open **Edit > Plugins** and select **Augmented Reality** from the built-in options list.</span></span> 
    * <span data-ttu-id="23e00-130">**HoloLens** まで下にスクロールし、 **[有効]** をオンにします。</span><span class="sxs-lookup"><span data-stu-id="23e00-130">Scroll down to **HoloLens** and check **Enabled**.</span></span> 

![HoloLens プラグインの有効化](images/unreal-uxt/2-plugins.PNG)

2. <span data-ttu-id="23e00-132">組み込みオプション リストから **[仮想現実]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="23e00-132">Select **Virtual Reality** from the built-in options list.</span></span> 
    * <span data-ttu-id="23e00-133">**[Microsoft Windows Mixed Reality]** まで下にスクロールし、 **[有効]** をオンにして、エディターを再起動します。</span><span class="sxs-lookup"><span data-stu-id="23e00-133">Scroll down to **Microsoft Windows Mixed Reality**, check **Enabled**, and restart your editor.</span></span> 

![Windows Mixed Reality プラグインを有効にする](images/unreal-uxt/2-virtual-reality-plugin.PNG)

> [!NOTE]
> <span data-ttu-id="23e00-135">HoloLens 2 の開発には、両方のプラグインが必要です。</span><span class="sxs-lookup"><span data-stu-id="23e00-135">Both plugins are required for HoloLens 2 development.</span></span>

<span data-ttu-id="23e00-136">これで空のレベルを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="23e00-136">With that done your empty level is ready for company.</span></span>

## <a name="creating-a-level"></a><span data-ttu-id="23e00-137">レベルの作成</span><span class="sxs-lookup"><span data-stu-id="23e00-137">Creating a level</span></span>
<span data-ttu-id="23e00-138">次のタスクは、参照とスケール用の開始点とキューブを使用して単純なプレーヤーのセットアップを作成することです。</span><span class="sxs-lookup"><span data-stu-id="23e00-138">Your next task is to create a simple player setup with a starting point and a cube for reference and scale.</span></span>

1. <span data-ttu-id="23e00-139">**[ファイル] > [新しいレベル]** を選択し、 **[空のレベル]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="23e00-139">Select **File > New Level** and choose **Empty Level**.</span></span> <span data-ttu-id="23e00-140">この時点では、ビューポートの既定のシーンは空です。</span><span class="sxs-lookup"><span data-stu-id="23e00-140">The default scene in the viewport should now be empty.</span></span>

2. <span data-ttu-id="23e00-141">**[モード]** タブから **[基本]** を選択し、 **[PlayerStart]** をシーンにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="23e00-141">Select **Basic** from the **Modes** tab and drag **PlayerStart** into the scene.</span></span> 
    * <span data-ttu-id="23e00-142">**[詳細]** タブで、 **[場所]** を **X = 0**、**Y = 0**、および **Z = 0**  に設定します。これにより、アプリの起動時にユーザーがシーンの中心に設定されます。</span><span class="sxs-lookup"><span data-stu-id="23e00-142">Set **Location** to **X = 0**, **Y = 0**, and **Z = 0** in the **Details** tab. This sets the user at the center of the scene when the app starts up.</span></span>

![PlayerStart を表示したビューポート](images/unreal-uxt/2-playerstart.PNG)

3. <span data-ttu-id="23e00-144">**[キューブ]** を **[基本]** タブからシーンにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="23e00-144">Drag a **Cube** from the **Basic** tab into the scene.</span></span> 
    * <span data-ttu-id="23e00-145">**[位置]** を **X = 50**、**Y = 0**、および **Z = 0** に設定します。</span><span class="sxs-lookup"><span data-stu-id="23e00-145">Set **Location** to **X = 50**, **Y = 0**, and **Z = 0**.</span></span> <span data-ttu-id="23e00-146">これにより、キューブは開始時にプレーヤーから 50 cm 離れた位置に配置されます。</span><span class="sxs-lookup"><span data-stu-id="23e00-146">This positions the cube 50 cm away from the player at start time.</span></span> 
    * <span data-ttu-id="23e00-147">キューブを縮小するには、 **[スケール]** を **X = 0.2**、**Y = 0.2**、および **Z = 0.2** に変更します。</span><span class="sxs-lookup"><span data-stu-id="23e00-147">Change **Scale** to **X = 0.2**, **Y = 0.2**, and **Z = 0.2** to shrink the cube down.</span></span> 

<span data-ttu-id="23e00-148">シーンにライトを追加しない限り、キューブを表示することはできません。これは、シーンをテストする前の最後のタスクです。</span><span class="sxs-lookup"><span data-stu-id="23e00-148">You won’t be able to see the cube unless you add a light to your scene, which is your last task before testing the scene.</span></span>

4. <span data-ttu-id="23e00-149">**[モード]** パネルの **[Lights]\(ライト\)** タブに切り替えて、**Directional Light** をシーンにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="23e00-149">Switch to the **Lights** tab in the **Modes** panel and drag a **Directional Light** into the scene.</span></span> <span data-ttu-id="23e00-150">ライトが見えるように、**PlayerStart** の上にライトを配置します。</span><span class="sxs-lookup"><span data-stu-id="23e00-150">Position the light above **PlayerStart** so you can see it.</span></span>

![ライトが追加されたビューポート](images/unreal-uxt/2-light.PNG)

5. <span data-ttu-id="23e00-152">**[ファイル] > [現在を保存]** に移動し、レベルに **Main** という名前を付けて、 **[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-152">Go to **File > Save Current**, name your level **Main**, and click **Save**.</span></span> 

<span data-ttu-id="23e00-153">シーンを設定したら、ツールバーの **[再生]** を押して、キューブの動作を確認します。</span><span class="sxs-lookup"><span data-stu-id="23e00-153">With the scene set, press **Play** in the toolbar to see your cube in action!</span></span> <span data-ttu-id="23e00-154">作業内容を鑑賞したら、**Esc** を押してアプリケーションを停止します。</span><span class="sxs-lookup"><span data-stu-id="23e00-154">When you're finished admiring your work, press **Esc** to stop the application.</span></span>

![ビューポート内のキューブ](images/unreal-uxt/2-cube.PNG)

<span data-ttu-id="23e00-156">シーンがセットアップされたので、チェス盤とピースを追加して、アプリケーション環境を完成させます。</span><span class="sxs-lookup"><span data-stu-id="23e00-156">Now that the scene is setup, you can start adding in the chess board and piece to round out the application environment.</span></span>

## <a name="importing-assets"></a><span data-ttu-id="23e00-157">資産のインポート</span><span class="sxs-lookup"><span data-stu-id="23e00-157">Importing assets</span></span>
<span data-ttu-id="23e00-158">現在、シーンは空であるように見えますが、既製の資産をプロジェクトにインポートして修正します。</span><span class="sxs-lookup"><span data-stu-id="23e00-158">The scene is looking a bit empty at the moment, but you'll fix that by importing the ready-made assets into the project.</span></span>

1. <span data-ttu-id="23e00-159">[GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/blob/master/ChessApp/ChessAssets.7z) 資産フォルダーをダウンロードして解凍します。</span><span class="sxs-lookup"><span data-stu-id="23e00-159">Download and unzip the [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/blob/master/ChessApp/ChessAssets.7z) assets folder.</span></span>

2. <span data-ttu-id="23e00-160">**[コンテンツ ブラウザー]** から **[新規追加] > [新しいフォルダー]** をクリックし、**ChessAssets** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-160">Click **Add New > New Folder** from the **Content Browser** and name it **ChessAssets**.</span></span> 
    * <span data-ttu-id="23e00-161">新しいフォルダーをダブルクリックします。ここに 3D 資産をインポートします。</span><span class="sxs-lookup"><span data-stu-id="23e00-161">Double-click the new folder - this is where you'll import the 3D assets.</span></span>

![ソース パネルの表示と非表示](images/unreal-uxt/2-showhidesources.PNG)

3. <span data-ttu-id="23e00-163">**[コンテンツ ブラウザー]** から **[インポート]** をクリックし、解凍した資産フォルダー内のすべての項目を選択して、 **[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-163">Click **Import** from the **Content Browser**, select all the items in the unzipped assets folder and click **Open**.</span></span> 
    * <span data-ttu-id="23e00-164">このフォルダーには、チェス盤の 3D オブジェクト メッシュと FBX 形式のピース、およびマテリアルに使用する TGA 形式のテクスチャ マップが含まれています。</span><span class="sxs-lookup"><span data-stu-id="23e00-164">This folder contains the 3D object meshes for the chess board and pieces in FBX format and texture maps in TGA format that you'll use to for materials.</span></span>  

4. <span data-ttu-id="23e00-165">[FBX インポート オプション] ウィンドウが表示されたら、 **[マテリアル]** セクションを展開し、 **[マテリアルのインポート方法]** を **[マテリアルを作成しない]** に変更します。</span><span class="sxs-lookup"><span data-stu-id="23e00-165">When the FBX Import Options window pops up, expand the **Material** section and change **Material Import Method** to **Do Not Create Material**.</span></span>
    * <span data-ttu-id="23e00-166">**[Import All]\(すべてインポート\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-166">Click **Import All**.</span></span>

![FBX インポート オプション](images/unreal-uxt/2-nocreatemat.PNG)

<span data-ttu-id="23e00-168">これで、資産に対して行う必要な操作は終わりました。</span><span class="sxs-lookup"><span data-stu-id="23e00-168">That's all you need to do for the assets.</span></span> <span data-ttu-id="23e00-169">次の一連のタスクでは、ブループリントを使用してアプリケーションの構成要素を作成します。</span><span class="sxs-lookup"><span data-stu-id="23e00-169">Your next set of tasks is to create the building blocks of the application with blueprints.</span></span>

## <a name="adding-blueprints"></a><span data-ttu-id="23e00-170">ブループリントの追加</span><span class="sxs-lookup"><span data-stu-id="23e00-170">Adding blueprints</span></span>

1. <span data-ttu-id="23e00-171">**[コンテンツ ブラウザー]** で、 **[新規追加] > [新しいフォルダー]** をクリックし、**Content Browser** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-171">Click **Add New > New Folder** in the **Content Browser** and name it **Content Browser**.</span></span> 

> [!NOTE]
> <span data-ttu-id="23e00-172">[ブループリント](https://docs.unrealengine.com/en-US/Engine/Blueprints/index.html)を初めて使用する場合、これらのブループリントは、新しい種類のアクターとスクリプト レベルのイベントを作成するためのノードベースのインターフェースを提供する特別な資産になります。</span><span class="sxs-lookup"><span data-stu-id="23e00-172">If you're new to [blueprints](https://docs.unrealengine.com/en-US/Engine/Blueprints/index.html), they're special assets that provide a node-based interface for creating new types of Actors and script level events.</span></span> 

2. <span data-ttu-id="23e00-173">**[ブループリント]** フォルダーをダブルクリックし、右クリックして **[ブループリント クラス]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="23e00-173">Double-click into the **Blueprints** folder, then right-click and select **Blueprint Class**.</span></span>         
    * <span data-ttu-id="23e00-174">**[Actor]\(アクター\)** を選択して、ブループリントに **Board** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-174">Select **Actor** and name the blueprint **Board**.</span></span> 

![ブループリントの親クラスを選択する](images/unreal-uxt/2-bpparent.PNG)

<span data-ttu-id="23e00-176">次のスクリーンショットに示すように、新しい **[ボード]** ブループリントが **[ブループリント]** フォルダーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="23e00-176">The new **Board** blueprint now shows up in the **Blueprints** folder as seen in the following screenshot.</span></span> 

![新しい Board ブループリント](images/unreal-uxt/2-bpboard.PNG)

<span data-ttu-id="23e00-178">作成したオブジェクトにマテリアルを追加するためのすべての設定が完了しました。</span><span class="sxs-lookup"><span data-stu-id="23e00-178">You're all set to start adding materials to the created objects.</span></span>

## <a name="working-with-materials"></a><span data-ttu-id="23e00-179">マテリアルの操作</span><span class="sxs-lookup"><span data-stu-id="23e00-179">Working with materials</span></span>
<span data-ttu-id="23e00-180">作成したオブジェクトは既定で灰色になりますが、これはあまり見栄えのよいものではありません。</span><span class="sxs-lookup"><span data-stu-id="23e00-180">The objects you've created are default grey, which isn't much fun to look at.</span></span> <span data-ttu-id="23e00-181">このチュートリアルの最後のタスク セットは、オブジェクトにマテリアルとメッシュを追加することです。</span><span class="sxs-lookup"><span data-stu-id="23e00-181">Adding materials and meshes to your objects is the last set of tasks in this tutorial.</span></span>

1. <span data-ttu-id="23e00-182">**[ボード]** をダブルクリックして、ブループリント エディターを開きます。</span><span class="sxs-lookup"><span data-stu-id="23e00-182">Double-click **Board** to open the blueprint editor.</span></span> 

2. <span data-ttu-id="23e00-183">**[コンポーネント]** パネルから **[コンポーネントの追加] > [シーン]** をクリックし、**Root** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-183">Click **Add Component > Scene** from the **Components** panel and name it **Root**.</span></span> <span data-ttu-id="23e00-184">以下のスクリーンショットでは、**Root** が **DefaultSceneRoot** の子として表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="23e00-184">Notice that **Root** shows up as a child of **DefaultSceneRoot** in the screenshot below:</span></span>

![ルートを置き換える](images/unreal-uxt/2-root-blueprint.PNG)


3. <span data-ttu-id="23e00-186">**ルート**をクリックアンドドラッグして **DefaultSceneRoot** に置換し、ビューポート内の球体を削除します。</span><span class="sxs-lookup"><span data-stu-id="23e00-186">Click-and-drag **Root** onto **DefaultSceneRoot** to replace it and get rid of the sphere in the viewport.</span></span> 

![ルートを置き換える](images/unreal-uxt/2-root.PNG)


4. <span data-ttu-id="23e00-188">**[コンポーネント]** パネルから **[コンポーネントの追加] > [静的メッシュ]** をクリックし、**SM_Board** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-188">Click **Add Component > Static Mesh** from the **Components** panel and name it **SM_Board**.</span></span> <span data-ttu-id="23e00-189">これは、**ルート**の下に子オブジェクトとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="23e00-189">It will appear as a child object under **Root**.</span></span>

![スタティック メッシュの追加](images/unreal-uxt/2-sm-board.PNG)

4. <span data-ttu-id="23e00-191">**[SM_Board]** をクリックし、 **[詳細]** パネルの **[静的メッシュ]** セクションまで下にスクロールして、ドロップダウンから **[ChessBoard]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="23e00-191">Click **SM_Board**, scroll down to the **Static Mesh** section of the **Details** panel, and select **ChessBoard** from the dropdown.</span></span> 

![ビューポート内のボード メッシュ](images/unreal-uxt/2-sm-board-view.PNG)

5.  <span data-ttu-id="23e00-193">引き続き **[詳細]** パネルで、 **[マテリアル]** セクションを展開し、ドロップダウンから **[新しい資産の作成] > [マテリアル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-193">Still in the **Details** panel, expand the **Materials** section and click **Create New Asset > Material** from the dropdown.</span></span> 
    * <span data-ttu-id="23e00-194">この資産に **M_ChessBoard** という名前を付けて、**ChessAssets** フォルダーに保存します。</span><span class="sxs-lookup"><span data-stu-id="23e00-194">Name the material **M_ChessBoard** and save it to the **ChessAssets** folder.</span></span> 

![新しいマテリアルを作成する](images/unreal-uxt/2-newmat.PNG)

6.  <span data-ttu-id="23e00-196">マテリアル エディターを開くには、**M_ChessBoard** マテリアルのイメージをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-196">Double-click the **M_ChessBoard** material imaged to open the Material Editor.</span></span> 

![マテリアル エディターを開く](images/unreal-uxt/2-material-editor.PNG)

7. <span data-ttu-id="23e00-198">マテリアル エディターで右クリックして、 **[Texture Sample]\(テクスチャ サンプル\)** を検索します。</span><span class="sxs-lookup"><span data-stu-id="23e00-198">In the Material Editor, right-click and search for **Texture Sample**.</span></span> 
    * <span data-ttu-id="23e00-199">**[詳細]** パネルの **[Material Expression Texture Base]\(マテリアル式テクスチャ ベース\)** セクションを展開し、 **[テクスチャ]** を **ChessBoard_Albedo** に設定します。</span><span class="sxs-lookup"><span data-stu-id="23e00-199">Expand the **Material Expression Texture Base** section in the **Details** panel and set **Texture** to **ChessBoard_Albedo**.</span></span> 
    * <span data-ttu-id="23e00-200">**[RGB]** 出力ピンを **M_ChessBoard** の [Base Color]\(基本色\) ピンにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="23e00-200">Drag the **RGB** output pin to the Base Color pin of **M_ChessBoard**.</span></span> 

![基本色を設定する](images/unreal-uxt/2-boardalbedomat.PNG)

8.  <span data-ttu-id="23e00-202">前の手順をさらに 4 回繰り返して、次の設定でさらに 4 つの **[テクスチャ サンプル]** ノードを作成します。</span><span class="sxs-lookup"><span data-stu-id="23e00-202">Repeat the previous step four more times to create four more **Texture Sample** nodes with the following settings:</span></span>
    * <span data-ttu-id="23e00-203">**[テクスチャ]** を **ChessBoard_AO** に設定し、**RGB** を **[アンビエント オクルージョン]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-203">Set **Texture** to **ChessBoard_AO** and link the **RGB** to the **Ambient Occlusion** pin.</span></span>
    * <span data-ttu-id="23e00-204">**[テクスチャ]** を **ChessBoard_Metal** に設定し、**RGB** を **[メタリック]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-204">Set **Texture** to **ChessBoard_Metal** and link the **RGB** to the **Metallic** pin.</span></span> 
    * <span data-ttu-id="23e00-205">**[テクスチャ]** を **ChessBoard_Normal** に設定し、**RGB** を **[ノーマル]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-205">Set **Texture** to **ChessBoard_Normal** and link the **RGB** to the **Normal** pin.</span></span>
    * <span data-ttu-id="23e00-206">**[テクスチャ]** を **ChessBoard_Rough** に設定し、**RGB** を **[ラフネス]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-206">Set **Texture** to **ChessBoard_Rough** and link the **RGB** to the **Roughness** pin.</span></span> 
    * <span data-ttu-id="23e00-207">**[Save]** (保存) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-207">Click **Save**.</span></span> 

![残りのテクスチャを接続する](images/unreal-uxt/2-boardmat.PNG)

<span data-ttu-id="23e00-209">続行する前に、マテリアルの設定が上のスクリーンショットのようになっていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="23e00-209">Make sure the your material setup looks like the above screenshot before continuing.</span></span>

## <a name="populating-the-scene"></a><span data-ttu-id="23e00-210">シーンへのデータの読み込み</span><span class="sxs-lookup"><span data-stu-id="23e00-210">Populating the scene</span></span>
<span data-ttu-id="23e00-211">**[ボード]** ブループリントに戻ると、作成したばかりのマテリアルが適用されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="23e00-211">If you go back to the **Board** blueprint, you'll see that the material you just created has been applied.</span></span> <span data-ttu-id="23e00-212">あとは、シーンをセットアップするだけです。</span><span class="sxs-lookup"><span data-stu-id="23e00-212">All that's left is setting up the scene!</span></span> <span data-ttu-id="23e00-213">最初に、以下のプロパティを変更して、ボードが適切なサイズであり、シーンに配置されたときに角度が適切であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="23e00-213">First, change the following properties to make sure the board is a reasonable size and angled correctly when it's placed in the scene:</span></span>
1.  <span data-ttu-id="23e00-214">**[スケール]** を **(0.05、0.05、0.05)** に設定し、 **[Z 回転]** を **90** に設定します。</span><span class="sxs-lookup"><span data-stu-id="23e00-214">Set **Scale** to **(0.05, 0.05, 0.05)** and **Z Rotation** to **90**.</span></span> 
    * <span data-ttu-id="23e00-215">上部のツールバーの **[コンパイル]** をクリックし、 **[保存]** をクリックして、メイン ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="23e00-215">Click **Compile** in the top toolbar, then **Save** and return to the Main window.</span></span> 

![マテリアルが適用されたチェス盤](images/unreal-uxt/2-chessboard.PNG)

2.  <span data-ttu-id="23e00-217">**[キューブ] > [編集] > [削除]** を右クリックして、 **[ボード]** を **[コンテンツ ブラウザー]** からビューポートにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="23e00-217">Right-click **Cube > Edit > Delete** and drag **Board** from the **Content Browser** into the viewport.</span></span> 
    * <span data-ttu-id="23e00-218">**[位置]** を **X = 80**、**Y = 0**、および **Z = -20** に設定します。</span><span class="sxs-lookup"><span data-stu-id="23e00-218">Set **Location** to **X = 80**, **Y = 0**, and **Z = -20**.</span></span> 

3.  <span data-ttu-id="23e00-219">**[Play]\(プレイ\)** ボタンをクリックして、新しいチェス盤をレベルに表示します。</span><span class="sxs-lookup"><span data-stu-id="23e00-219">Click the **Play** button to view your new board in the level.</span></span> <span data-ttu-id="23e00-220">**Esc** キーを押してエディターに戻ります。</span><span class="sxs-lookup"><span data-stu-id="23e00-220">Press **Esc** to return to the editor.</span></span> 

<span data-ttu-id="23e00-221">次に、ボードで行ったのと同じ手順に従って、チェスの駒を作成します。</span><span class="sxs-lookup"><span data-stu-id="23e00-221">Now you'll follow the same steps to create a chess piece as you did with the board:</span></span>

1. <span data-ttu-id="23e00-222">**[ブループリント]** フォルダーに移動し、右クリックして **[ブループリント クラス]** を選択し、 **[アクター]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="23e00-222">Go to the **Blueprints** folder, right-click and select **Blueprint Class** and choose **Actor**.</span></span> <span data-ttu-id="23e00-223">このアクターに **WhiteKing** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-223">Name the actor **WhiteKing**.</span></span>

2. <span data-ttu-id="23e00-224">**WhiteKing** をダブルクリックしてブループリント エディターで開き、 **[コンポーネントの追加] > [シーン]** をクリックして、**Root** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-224">Double click **WhiteKing** to open it in the Blueprint Editor, click **Add Component > Scene** and name it **Root**.</span></span> 
    * <span data-ttu-id="23e00-225">**Root** を **DefaultSceneRoot** にドラッグアンドドロップして置換します。</span><span class="sxs-lookup"><span data-stu-id="23e00-225">Drag-and-drop **Root** onto **DefaultSceneRoot** to replace it.</span></span> 

3. <span data-ttu-id="23e00-226">**[コンポーネントの追加]> [スタティック メッシュ]** をクリックし、**SM_King** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="23e00-226">Click **Add Component > Static Mesh** and name it **SM_King**.</span></span> 
    * <span data-ttu-id="23e00-227">[詳細] パネルで、 **[Static Mesh]\(スタティック メッシュ\)** を **Chess_King** に設定し、 **[Material]\(マテリアル\)** を、**M_ChessWhite**という名前の新しいマテリアルに設定します。</span><span class="sxs-lookup"><span data-stu-id="23e00-227">Set **Static Mesh** to **Chess_King** and **Material** to a new Material called **M_ChessWhite** in the Details panel.</span></span> 

4. <span data-ttu-id="23e00-228">マテリアル エディターで、**M_ChessWhite** を開き、次の **[テクスチャ サンプル]** ノードを次のものに接続します。</span><span class="sxs-lookup"><span data-stu-id="23e00-228">Open **M_ChessWhite** in the Material editor and hook up the following **Texture Sample** nodes to the following:</span></span>
    * <span data-ttu-id="23e00-229">**[テクスチャ]** を **ChessWhite_AO** に設定し、**RGB** を **[アンビエント オクルージョン]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-229">Set **Texture** to **ChessWhite_AO** and link the **RGB** to the **Ambient Occlusion** pin.</span></span>
    * <span data-ttu-id="23e00-230">**[テクスチャ]** を **ChessWhite_Metal** に設定し、**RGB** を **[メタリック]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-230">Set **Texture** to **ChessWhite_Metal** and link the **RGB** to the **Metallic** pin.</span></span> 
    * <span data-ttu-id="23e00-231">**[テクスチャ]** を **ChessWhite_Normal** に設定し、**RGB** を **[ノーマル]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-231">Set **Texture** to **ChessWhite_Normal** and link the **RGB** to the **Normal** pin.</span></span>
    * <span data-ttu-id="23e00-232">**[テクスチャ]** を **ChessWhite_Rough** に設定し、**RGB** を **[ラフネス]** ピンにリンクします。</span><span class="sxs-lookup"><span data-stu-id="23e00-232">Set **Texture** to **ChessWhite_Rough** and link the **RGB** to the **Roughness** pin.</span></span> 
    * <span data-ttu-id="23e00-233">**[Save]** (保存) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="23e00-233">Click **Save**.</span></span> 

<span data-ttu-id="23e00-234">続行する前に、**M_ChessKing** マテリアルは次の図のようになります。</span><span class="sxs-lookup"><span data-stu-id="23e00-234">Your **M_ChessKing** material should look like the following image before continuing.</span></span>

![チェスのキングのマテリアルを作成する](images/unreal-uxt/2-chesskingmat.PNG)

<span data-ttu-id="23e00-236">もう少しで完了です。あとは新しいチェスの駒をシーンに追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="23e00-236">You're almost there, just need to add the new chess piece into the scene:</span></span> 

1. <span data-ttu-id="23e00-237">**WhiteKing** ブループリントを開いて、 **[Scale]\(スケール\)** を **(0.05, 0.05, 0.05)** に、 **[Z 回転]** を **90** に変更します。</span><span class="sxs-lookup"><span data-stu-id="23e00-237">Open the **WhiteKing** blueprint and change the **Scale** to **(0.05, 0.05, 0.05)** and **Z Rotation** to **90**.</span></span>
    * <span data-ttu-id="23e00-238">ブループリントをコンパイルして保存した後、メイン ウィンドウに戻ります。</span><span class="sxs-lookup"><span data-stu-id="23e00-238">Compile and save your blueprint, then head back to the main window.</span></span> 

2.  <span data-ttu-id="23e00-239">**WhiteKing** をビューポートにドラッグし、 **[ワールド アウトライナー]** パネルに切り替え、**WhiteKing** を **[ボード]** にドラッグして、子オブジェクトにします。</span><span class="sxs-lookup"><span data-stu-id="23e00-239">Drag **WhiteKing** into the viewport, switch to the **World Outliner** panel drag **WhiteKing** onto **Board** to make it a child object.</span></span>

![[World Outliner]\(ワールド アウトライナー\)](images/unreal-uxt/2-child.PNG)

3.  <span data-ttu-id="23e00-241">**[詳細]** パネルの **[Transform]\(トランスフォーム\)** で、**WhiteKing** の **[Location]\(位置\)** を **X = -26**、**Y = 4**、**Z = 0** に設定します。</span><span class="sxs-lookup"><span data-stu-id="23e00-241">In the **Details** panel under **Transform**, set **WhiteKing**'s **Location** to **X = -26**, **Y = 4**, and **Z = 0**.</span></span>

<span data-ttu-id="23e00-242">これでおしまいです!</span><span class="sxs-lookup"><span data-stu-id="23e00-242">That's a wrap!</span></span> <span data-ttu-id="23e00-243">**[再生]** をクリックして、データ設定されているレベルの動作を確認し、終了する準備ができたら **Esc** を押します。</span><span class="sxs-lookup"><span data-stu-id="23e00-243">Click **Play** to see your populated level in action, and press **Esc** when you're ready to exit.</span></span> <span data-ttu-id="23e00-244">このチュートリアルでは、単純なプロジェクトを作成するための多くの基本について説明しましたが、プロジェクトはシリーズの次の部分である「複合現実の設定」に進む準備ができています。</span><span class="sxs-lookup"><span data-stu-id="23e00-244">This tutorial covered a lot of ground creating a simple project, but your project is ready to move on to the next part of the series: setting up for mixed reality.</span></span> 

[<span data-ttu-id="23e00-245">次のセクション: 3.Mixed Reality 用のプロジェクト設定</span><span class="sxs-lookup"><span data-stu-id="23e00-245">Next Section: 3. Set up your project for mixed reality</span></span>](unreal-uxt-ch3.md)
