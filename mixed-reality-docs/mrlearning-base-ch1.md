---
title: MR Learning ベースのモジュールのプロジェクトの初期化と最初のアプリケーション
description: このコースでは、複合現実のアプリケーション内で Azure の顔認識機能を実装する方法について説明します。
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: 複合現実、unity、チュートリアル、hololens
ms.openlocfilehash: 95ba00d68eb5fb6c990ddee343ac58ebe00dbb10
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993648"
---
# <a name="mr-learning-base-module---project-initialization-and-first-application"></a><span data-ttu-id="14de1-104">MR Learning ベースのモジュールのプロジェクトの初期化と最初のアプリケーション</span><span class="sxs-lookup"><span data-stu-id="14de1-104">MR Learning Base Module - Project Initialization and First Application</span></span>

<span data-ttu-id="14de1-105">この最初のレッスンでは、提供、HoloLens 2 の最初のアプリケーションを起動し、デバイスにデプロイする Mixed Reality ツールキットには、機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="14de1-105">In this first lesson, you will learn some of the capabilities the Mixed Reality Toolkit has to offer, start your first application for the HoloLens 2, and deploy it to the device.</span></span>

## <a name="objectives"></a><span data-ttu-id="14de1-106">目標</span><span class="sxs-lookup"><span data-stu-id="14de1-106">Objectives</span></span>

* <span data-ttu-id="14de1-107">HoloLens の開発のためには、Unity を最適化します。</span><span class="sxs-lookup"><span data-stu-id="14de1-107">Optimize Unity for HoloLens development.</span></span>
* <span data-ttu-id="14de1-108">アセットをインポートして、シーンをセットアップします。</span><span class="sxs-lookup"><span data-stu-id="14de1-108">Import assets and setup the scene.</span></span>
* <span data-ttu-id="14de1-109">空間メッシュ、手の形のメッシュとフレーム レート カウンターの視覚化。</span><span class="sxs-lookup"><span data-stu-id="14de1-109">Visualization of the spatial mesh, hand meshes, and the framerate counter.</span></span>

## <a name="instructions"></a><span data-ttu-id="14de1-110">手順</span><span class="sxs-lookup"><span data-stu-id="14de1-110">Instructions</span></span>

### <a name="create-new-unity-project"></a><span data-ttu-id="14de1-111">新しい Unity プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="14de1-111">Create new Unity project</span></span>

1. <span data-ttu-id="14de1-112">Unity を起動します。</span><span class="sxs-lookup"><span data-stu-id="14de1-112">Start Unity.</span></span>
2. <span data-ttu-id="14de1-113">**[新規]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="14de1-113">Select **New**.</span></span>
<span data-ttu-id="14de1-114">![レッスン 1 から第 1 章の手順 2](images/Lesson1Chapter1Step2.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-114">![Lesson1 Chapter1 Step2](images/Lesson1Chapter1Step2.JPG)</span></span>
3. <span data-ttu-id="14de1-115">プロジェクト名を入力します (例。"MixedRealityBase")。</span><span class="sxs-lookup"><span data-stu-id="14de1-115">Enter a project name (e.g. "MixedRealityBase").</span></span>
<span data-ttu-id="14de1-116">![レッスン 1 から第 1 章の手順 3](images/Lesson1Chapter1Step3.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-116">![Lesson1 Chapter1 Step3](images/Lesson1Chapter1Step3.JPG)</span></span>
4. <span data-ttu-id="14de1-117">プロジェクトを保存する場所を入力します。</span><span class="sxs-lookup"><span data-stu-id="14de1-117">Enter a location to save your project.</span></span>
<span data-ttu-id="14de1-118">![レッスン 1 から第 1 章の手順 4](images/Lesson1Chapter1Step4.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-118">![Lesson1 Chapter1 Step4](images/Lesson1Chapter1Step4.JPG)</span></span>
5. <span data-ttu-id="14de1-119">必ず、プロジェクトに設定されて**3D**します。</span><span class="sxs-lookup"><span data-stu-id="14de1-119">Make sure the project is set to **3D**.</span></span>
<span data-ttu-id="14de1-120">![レッスン 1 から第 1 章の手順 5](images/Lesson1Chapter1Step5.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-120">![Lesson1 Chapter1 Step5](images/Lesson1Chapter1Step5.JPG)</span></span>
6. <span data-ttu-id="14de1-121">クリックして**プロジェクトを作成する**します。</span><span class="sxs-lookup"><span data-stu-id="14de1-121">Click **Create Project**.</span></span>
<span data-ttu-id="14de1-122">![レッスン 1 から第 1 章の手順 6](images/Lesson1Chapter1Step6.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-122">![Lesson1 Chapter1 Step6](images/Lesson1Chapter1Step6.JPG)</span></span>

### <a name="configure-the-unity-project-for-windows-mixed-reality"></a><span data-ttu-id="14de1-123">Windows Mixed Reality 用 Unity プロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="14de1-123">Configure the Unity project for Windows Mixed Reality</span></span>

1. <span data-ttu-id="14de1-124">ファイルにアクセスして、ビルド設定 ウィンドウを開く > ビルドの設定。</span><span class="sxs-lookup"><span data-stu-id="14de1-124">Open the build settings window by going to File>Build Settings.</span></span>
<span data-ttu-id="14de1-125">![レッスン 1 から第 4 章の手順 1](images/Lesson1Chapter4Step1.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-125">![Lesson1 Chapter4 Step1](images/Lesson1Chapter4Step1.JPG)</span></span>
2. <span data-ttu-id="14de1-126">「ユニバーサル Windows プラットフォーム」を選択して「ユニバーサル Windows プラットフォーム」に切り替えるし、プラットフォームの切り替えを「プラットフォームの切り替え」ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="14de1-126">Switch to “Universal Windows Platform” by selecting “Universal Windows Platform” and then click the “Switch Platform” button to switch platforms.</span></span> <span data-ttu-id="14de1-127">HoloLens 2 で実行されているアプリは、ユニバーサル Windows プラットフォーム (UWP) する必要があります。</span><span class="sxs-lookup"><span data-stu-id="14de1-127">Apps running on HoloLens 2 are required to be Universal Windows Platform (UWP).</span></span>
<span data-ttu-id="14de1-128">![レッスン 1 から第 4 章の手順 2](images/Lesson1Chapter4Step2.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-128">![Lesson1 Chapter4 Step2](images/Lesson1Chapter4Step2.JPG)</span></span>
3. <span data-ttu-id="14de1-129">ビルド ウィンドウで、Player の設定 をクリックして仮想現実を有効にし、inspector パネルでチェック ボックスをオン、「仮想現実サポートされて」XR の設定で次の図に示すようにします。</span><span class="sxs-lookup"><span data-stu-id="14de1-129">Enable virtual reality by clicking on Player Settings in the Build Window, and then in the inspector panel enable the “Virtual Reality Supported” checkbox under XR Settings, as shown in the image below.</span></span> <span data-ttu-id="14de1-130">Inspector パネルを表示するには、[ビルド設定] ウィンドウを邪魔をドラッグする必要がありますに注意してください。</span><span class="sxs-lookup"><span data-stu-id="14de1-130">Please note that you may need to drag the "Build Settings" window out of the way in order to see the inspector panel.</span></span> <span data-ttu-id="14de1-131">「仮想現実サポート」チェック ボックスは、複合現実にも適用されます/AR ヘッドセット ステレオスコ ピック ビジョン (レンダリングごとに異なるイメージ目ごとです) の有効化、を参照しています。![レッスン 1 から第 4 章の手順 3](images/Lesson1Chapter4Step3.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-131">The "Virtual Reality Supported" checkbox also applies to Mixed Reality / AR headsets because it refers to the enabling of stereoscopic vision (rendering different images for each eye.) ![Lesson1 Chapter4 Step3](images/Lesson1Chapter4Step3.JPG)</span></span>
4. <span data-ttu-id="14de1-132">同じ inspector] パネルで、[機能] セクションで「空間認識」のチェック ボックスが有効である [発行の設定を確認します。</span><span class="sxs-lookup"><span data-stu-id="14de1-132">In the same inspector panel, check that the “Spatial Perception” checkbox in the capabilities section is enabled, under Publishing Settings.</span></span> <span data-ttu-id="14de1-133">空間認識は、HoloLens 2 などの複合現実デバイスに空間マッピングのメッシュを視覚化できます。</span><span class="sxs-lookup"><span data-stu-id="14de1-133">Spatial Perception will allow us to visualize the spatial mapping mesh on a mixed reality device such as the HoloLens 2.</span></span> <span data-ttu-id="14de1-134">インスペクター ウィンドウ上の「XR 設定」と"その他の設定 の下で発行の設定があります。</span><span class="sxs-lookup"><span data-stu-id="14de1-134">Publishing settings are found in the Inspector panel, above "XR Settings" and under "Other Settings."</span></span>
<span data-ttu-id="14de1-135">![レッスン 1 から第 4 章の手順 4](images/Lesson1Chapter4Step4.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-135">![Lesson1 Chapter4 Step4](images/Lesson1Chapter4Step4.JPG)</span></span>

> <span data-ttu-id="14de1-136">注: 有効にするいくつかその他の一般的な機能が含まれます (音声コマンド) のマイクと InternetClient (ネットワーク接続が必要なサービスに接続する) のこのセクションでは使用されませんが、</span><span class="sxs-lookup"><span data-stu-id="14de1-136">NOTE: While not used in this section, some other common capabilities you may want to enable include Microphone (for voice commands) and InternetClient (for connecting to services requiring a network connection)</span></span>

### <a name="import-the-mixed-reality-toolkit"></a><span data-ttu-id="14de1-137">インポート、Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="14de1-137">Import the Mixed Reality Toolkit</span></span>

1. <span data-ttu-id="14de1-138">ダウンロード、 [Mixed Reality Toolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1.unitypackage) unity パッケージ化し、PC 上のフォルダーに保存します。</span><span class="sxs-lookup"><span data-stu-id="14de1-138">Download the [Mixed Reality Toolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1.unitypackage) unity package and save it to a folder on your PC.</span></span>

2. <span data-ttu-id="14de1-139">資産をクリックして、Mixed Reality Toolkit パッケージをインポート > インポート > カスタム パッケージ。</span><span class="sxs-lookup"><span data-stu-id="14de1-139">Import the Mixed Reality Toolkit package by clicking on Assets>Import>Custom Package.</span></span> <span data-ttu-id="14de1-140">手順 1. でダウンロードした Mixed Reality Toolkit パッケージを検索してインポート プロセスを開始することを開きます。</span><span class="sxs-lookup"><span data-stu-id="14de1-140">Find the Mixed Reality Toolkit package downloaded in Step 1 and open it to begin the importing process.</span></span> <span data-ttu-id="14de1-141">インポートのプロセスには数分お待ちください。</span><span class="sxs-lookup"><span data-stu-id="14de1-141">Please allow a few minutes for the importing process.</span></span>
    <span data-ttu-id="14de1-142">![レッスン 1 から第 2 章 Step2a](images/Lesson1Chapter2Step2a.JPG) ![レッスン 1 から第 2 章 Step2b](images/Lesson1Chapter2Step2b.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-142">![Lesson1 Chapter2 Step2a](images/Lesson1Chapter2Step2a.JPG) ![Lesson1 Chapter2 Step2b](images/Lesson1Chapter2Step2b.JPG)</span></span>

3. <span data-ttu-id="14de1-143">[次へ] のポップアップ ウィンドウでは、Mixed Reality Toolkit のインポートを開始するには、[インポート] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="14de1-143">In the next pop-up window, click “Import” to begin importing the Mixed Reality Toolkit.</span></span> <span data-ttu-id="14de1-144">図のように、すべての項目が確認を確認します。</span><span class="sxs-lookup"><span data-stu-id="14de1-144">Ensure all items are checked, as shown in the image.</span></span> <span data-ttu-id="14de1-145">Mixed Reality Toolkit の既定の設定を適用するよう求めるポップアップ ダイアログ ボックスを表示する場合は、「適用します」をクリックします</span><span class="sxs-lookup"><span data-stu-id="14de1-145">If you see a pop-up dialog box asking to apply Mixed Reality Toolkit default settings, click "Apply."</span></span>
    <span data-ttu-id="14de1-146">![レッスン 1 から第 2 章 Step3](images/Lesson1Chapter2Step3.JPG) ![レッスン 1 から第 2 章の手順 3](images/Lesson1Chapter2Step3b.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-146">![Lesson1 Chapter2 Step3](images/Lesson1Chapter2Step3.JPG) ![Lesson1 Chapter2 Step3](images/Lesson1Chapter2Step3b.JPG)</span></span>

### <a name="configure-the-mixed-reality-toolkit"></a><span data-ttu-id="14de1-147">Mixed Reality ツールキットを構成します。</span><span class="sxs-lookup"><span data-stu-id="14de1-147">Configure the Mixed Reality Toolkit</span></span>

1. <span data-ttu-id="14de1-148">Mixed Reality Toolkit バー、メニューから選択して、混合 Toolkit の構成 > 構成します。</span><span class="sxs-lookup"><span data-stu-id="14de1-148">Configure the Mixed Toolkit by selecting from the menu bar Mixed Reality Toolkit > Configure.</span></span> <span data-ttu-id="14de1-149">複合現実ツールキットをインポートした後、このメニュー項目が表示されない場合は、Unity を再起動してください。</span><span class="sxs-lookup"><span data-stu-id="14de1-149">If you don't see this menu item after importing the mixed reality toolkit, please restart Unity.</span></span>
<span data-ttu-id="14de1-150">![レッスン 1 から第 3 章の手順 1](images/Lesson1Chapter3Step1.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-150">![Lesson1 Chapter3 Step1](images/Lesson1Chapter3Step1.JPG)</span></span>
2. <span data-ttu-id="14de1-151">シーンようになりましたがいくつかの新しい項目と変更が Mixed Reality Toolkit から。</span><span class="sxs-lookup"><span data-stu-id="14de1-151">Your scene will now have several new items and modifications in it from the Mixed Reality Toolkit.</span></span> <span data-ttu-id="14de1-152">ファイルをクリックして別の名前で、シーンを保存 > として保存し、シーン BaseScene などの名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="14de1-152">Save your scene under a different name by clicking on File>Save As and give your scene a name, e.g., BaseScene.</span></span> <span data-ttu-id="14de1-153">プロジェクトの Assets フォルダーで「シーン」フォルダーに保存して別に整理されたシーンを保持します。</span><span class="sxs-lookup"><span data-stu-id="14de1-153">Keep your scene organized by saving it to the “Scenes” folder in your project’s Assets folder.</span></span>
<span data-ttu-id="14de1-154">![レッスン 1 から第 3 章 Step2a](images/Lesson1Chapter3Step2a.JPG)
![レッスン 1 から第 3 章 Step2b](images/Lesson1Chapter3Step2b.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-154">![Lesson1 Chapter3 Step2a](images/Lesson1Chapter3Step2a.JPG)
![Lesson1 Chapter3 Step2b](images/Lesson1Chapter3Step2b.JPG)</span></span>

### <a name="build-your-application-to-your-device"></a><span data-ttu-id="14de1-155">デバイスにアプリケーションを構築します。</span><span class="sxs-lookup"><span data-stu-id="14de1-155">Build your application to your device</span></span>

1. <span data-ttu-id="14de1-156">前のセクションからのビルド設定ウィンドウを閉じた場合、ビルド設定 ウィンドウ再度開くファイルに移動して > ビルドの設定。</span><span class="sxs-lookup"><span data-stu-id="14de1-156">If you closed the Build Settings window from the previous sections, open the build settings window again by going to File>Build Settings.</span></span>
    <span data-ttu-id="14de1-157">![レッスン 1 から第 5 章の手順 1](images/Lesson1Chapter5Step1.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-157">![Lesson1 Chapter5 Step1](images/Lesson1Chapter5Step1.JPG)</span></span>

2. <span data-ttu-id="14de1-158">試したいシーンが「開いているシーンを追加」ボタンをクリックして、"Scenes in Build"一覧に確認してください。</span><span class="sxs-lookup"><span data-stu-id="14de1-158">Ensure the scene you want to try is in the “Scenes in Build” list by clicking on the “Add Open Scenes” button.</span></span>

3. <span data-ttu-id="14de1-159">ビルド プロセスを開始するビルド ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="14de1-159">Press the Build button to begin the build process.</span></span>
    <span data-ttu-id="14de1-160">![レッスン 1 から第 5 章の手順 3](images/Lesson1Chapter5Step3.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-160">![Lesson1 Chapter5 Step3](images/Lesson1Chapter5Step3.JPG)</span></span>

4. <span data-ttu-id="14de1-161">作成し、アプリケーションの新しいフォルダーの名前します。</span><span class="sxs-lookup"><span data-stu-id="14de1-161">Create and name a new folder for your application.</span></span> <span data-ttu-id="14de1-162">名前のフォルダーの下の図の"App"は、アプリケーションを含むに作成されました。</span><span class="sxs-lookup"><span data-stu-id="14de1-162">In the image below, a folder with the name “App” was created to contain the application.</span></span> <span data-ttu-id="14de1-163">新しく作成したフォルダーにビルドを開始「フォルダーの選択」をクリックします。</span><span class="sxs-lookup"><span data-stu-id="14de1-163">Click “Select Folder” to begin building to the newly created folder.</span></span> <span data-ttu-id="14de1-164">ビルドが完了すると、Unity で [ビルド設定] ウィンドウを閉じると可能性があります。</span><span class="sxs-lookup"><span data-stu-id="14de1-164">After the build has completed, you may close the "Build Settings" window in Unity.</span></span> 
    <span data-ttu-id="14de1-165">![レッスン 1 から第 5 章の手順 4](images/Lesson1Chapter5Step4.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-165">![Lesson1 Chapter5 Step4](images/Lesson1Chapter5Step4.JPG)</span></span>

  > <span data-ttu-id="14de1-166">注: 構成をもう一度お試しください、ビルドが失敗した場合、または Unity を再起動して、再構築します。</span><span class="sxs-lookup"><span data-stu-id="14de1-166">NOTE: If the build fails, try building again or restarting Unity and building again.</span></span> <span data-ttu-id="14de1-167">エラーを表示する場合は、"エラー。CS0246 = tyoe または名前空間の名前が"XX"が見つかりませんでした (が存在することを使用して、ディレクティブまたはアセンブリ参照か)"、をインストールする必要がありますし、 [Windows 10 SDK (10.0.18362.0)。](<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk>)</span><span class="sxs-lookup"><span data-stu-id="14de1-167">If you see an error such as "Error: CS0246 = The tyoe or namespace name “XX” could not be found (are you missing a using directive or an assembly reference?)", then you may need to install [Windows 10 SDK (10.0.18362.0)](<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk>)</span></span>
  >

5. <span data-ttu-id="14de1-168">ビルドが完了した後、新しくビルドされたアプリケーション ファイルを格納している新しく作成したフォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="14de1-168">After the build is completed, open the newly created folder containing your newly built application files.</span></span> <span data-ttu-id="14de1-169">"MixedRealityBase.sln"ソリューション (または、プロジェクトの代替名を使用した場合は、対応する名前) をダブルクリックすると、Visual Studio でソリューション ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="14de1-169">Double click on the “MixedRealityBase.sln” solution (or the corresponding name, if you used an alternative name for your project) to open the solution file in Visual Studio.</span></span>

  > <span data-ttu-id="14de1-170">注:(つまり、"App"フォルダーを前の手順から名前付け規則に従う場合)、新しく作成したフォルダーを開くことを確認するように、ビルド フォルダー内の .sln ファイルと混同しないように、そのフォルダーの外部で同様に名前付きの .sln ファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="14de1-170">Note: Be sure to open the newly created folder (i.e., the "App" folder, if following the naming conventions from the previous steps), as there will be a similarly named .sln file outside of that folder that is not to be confused with the .sln file inside the build folder.</span></span> 

![レッスン 1 から第 5 章の手順 5](images/Lesson1Chapter5Step5.JPG)

  > <span data-ttu-id="14de1-172">注:Visual Studio、新しいコンポーネントをインストールするよう求めるお聞かせくださいとしてすべての前提条件となるコンポーネントがインストールされていることを確認する場合で指定された["ツールをインストールする ページ](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="14de1-172">Note: If Visual Studio asks you to install new components, please take a moment to ensure that all prerequisite components are installed as specified in [the "Install the Tools" page](install-the-tools.md)</span></span>

6. <span data-ttu-id="14de1-173">USB ケーブルを使用して PC、HoloLens 2 に差し込みます。</span><span class="sxs-lookup"><span data-stu-id="14de1-173">Plug your HoloLens 2 into your PC with the USB cable.</span></span> <span data-ttu-id="14de1-174">レッスンの手順では、HoloLens 2 デバイスでのテスト、デプロイする前提としています、中にすることもできますを展開する、 [HoloLens 2 エミュレーター](using-the-hololens-emulator.md)を作成することも、[サイドローディング用アプリ パッケージ](<https://docs.microsoft.com/en-us/windows/uwp/packaging/packaging-uwp-apps>)</span><span class="sxs-lookup"><span data-stu-id="14de1-174">While these lesson instructions assume you will be deploying a testing with a HoloLens 2 device, you may also choose to deploy to the [HoloLens 2 emulator](using-the-hololens-emulator.md) or choose to create an [app package for sideloading](<https://docs.microsoft.com/en-us/windows/uwp/packaging/packaging-uwp-apps>)</span></span>

7. <span data-ttu-id="14de1-175">デバイスに、ビルド前に、デバイスが開発者モードであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="14de1-175">Before building to your device, ensure that the device is in Developer Mode.</span></span> <span data-ttu-id="14de1-176">初めて HoloLens 2 へのデプロイの場合は、Visual Studio に、pin、HoloLens 2 をペアリングするように指示する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="14de1-176">If this is your first time deploying to the HoloLens 2, Visual Studio may ask you to pair your HoloLens 2 with a pin.</span></span> <span data-ttu-id="14de1-177">従ってください[手順](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio)開発者モードを有効にするか、Visual Studio とペアリングする必要がある場合。</span><span class="sxs-lookup"><span data-stu-id="14de1-177">Please follow [these instructions](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio) if you need to enable developer mode or pair with Visual Studio.</span></span>

8. <span data-ttu-id="14de1-178">"Release"構成と"ARM"アーキテクチャを選択して、HoloLens 2 を構築するための Visual Studio を構成します。</span><span class="sxs-lookup"><span data-stu-id="14de1-178">Configure Visual Studio for building to your HoloLens 2 by selecting the “Release” configuration and the “ARM” architecture.</span></span>
    <span data-ttu-id="14de1-179">![レッスン 1 から第 5 章 Step8](images/Lesson1Chapter5Step8.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-179">![Lesson1 Chapter5 Step8](images/Lesson1Chapter5Step8.JPG)</span></span>

9. <span data-ttu-id="14de1-180">最後に、デバッグを選択して、デバイスにビルド > デバッグなしで開始します。</span><span class="sxs-lookup"><span data-stu-id="14de1-180">The final step is to build to your device by selecting Debug>Start without Debugging.</span></span> <span data-ttu-id="14de1-181">"デバッグなしで開始 を選択すると、デバイス ビルドに成功すると、Visual Studio に表示されるデバッグ情報なしですぐに開始するアプリケーションとされます。</span><span class="sxs-lookup"><span data-stu-id="14de1-181">Selecting “Start without Debugging” will cause the application to immediately start on your device upon a successful build, but without Debugging information appearing in Visual Studio.</span></span> <span data-ttu-id="14de1-182">つまり、アプリケーションのアプリケーションを停止することがなく、HoloLens 2 で実行中に、USB ケーブルを切断することができます。</span><span class="sxs-lookup"><span data-stu-id="14de1-182">This also means that you can disconnect your USB cable while your application is running on your HoloLens 2 without stopping the application.</span></span> <span data-ttu-id="14de1-183">ビルドを選択することも > を自動的に起動するアプリケーションをしなくても、デバイスに展開するには、ソリューションの配置。</span><span class="sxs-lookup"><span data-stu-id="14de1-183">You may also select Build>Deploy Solution to deploy to your device without having the application automatically start.</span></span>
    <span data-ttu-id="14de1-184">![レッスン 1 から第 5 章 Step9](images/Lesson1Chapter5Step9.JPG)</span><span class="sxs-lookup"><span data-stu-id="14de1-184">![Lesson1 Chapter5 Step9](images/Lesson1Chapter5Step9.JPG)</span></span>

## <a name="congratulations"></a><span data-ttu-id="14de1-185">おめでとうございます</span><span class="sxs-lookup"><span data-stu-id="14de1-185">Congratulations</span></span>

<span data-ttu-id="14de1-186">今すぐが配置されました、最初の HoloLens 2 アプリケーション。</span><span class="sxs-lookup"><span data-stu-id="14de1-186">You now have now deployed your first HoloLens 2 application.</span></span> <span data-ttu-id="14de1-187">周りを説明しながら、HoloLens 2 によって認識されているすべてのサーフェイスをカバーする空間メッシュが表示されます。</span><span class="sxs-lookup"><span data-stu-id="14de1-187">As you walk around, you should see a spatial mesh cover all the surfaces that have been perceived by the HoloLens 2.</span></span> <span data-ttu-id="14de1-188">さらに、ハンドと本の指を追跡し、アプリのパフォーマンスを監視するためのフレーム レート カウンターにインジケーターを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="14de1-188">Additionally, you should see indicators on your hands and fingers for hand tracking and a frame rate counter for keeping an eye on app performance.</span></span> <span data-ttu-id="14de1-189">これらは、基礎となる部分、Mixed Reality ツールキットを使用して、すぐに付属のほんの一部です。</span><span class="sxs-lookup"><span data-stu-id="14de1-189">These are just a few of the foundational pieces, included out of the box, with the Mixed Reality Toolkit.</span></span> <span data-ttu-id="14de1-190">付属のレッスンでは、HoloLens 2 や Mixed Reality ツールキットの機能を十分に検証できるように、シーンへのコンテンツや対話機能の追加を開始します。</span><span class="sxs-lookup"><span data-stu-id="14de1-190">In the lessons to come, you will start adding more content and interactivity to your scene, so you can fully explore the capabilities of the HoloLens 2 and the Mixed Reality Toolkit.</span></span>

><span data-ttu-id="14de1-191">注:音声コマンドを使用して、フレーム レート カウンターを切り替える方法を説明する[レッスン 5](mrlearning-base-ch5.md)</span><span class="sxs-lookup"><span data-stu-id="14de1-191">Note: You will cover how to toggle the frame rate counter using a voice command in [Lesson 5](mrlearning-base-ch5.md)</span></span>

[<span data-ttu-id="14de1-192">次のレッスン:ユーザー インターフェイス、追跡、および現実ツールキットの構成を混在手の形</span><span class="sxs-lookup"><span data-stu-id="14de1-192">Next Lesson: User Interface, Hand Tracking, and Mixed Reality Toolkit Configuration</span></span>](mrlearning-base-ch2.md)