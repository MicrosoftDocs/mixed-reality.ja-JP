---
title: マルチユーザー機能のチュートリアル - 3. 複数のユーザーの接続
description: このコースでは、HoloLens 2 アプリケーション内でマルチユーザー共有エクスペリエンスを実装する方法を学習します。
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: 5937b581e92ffc5a13b55574ffd8a0ca7c4bca40
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376394"
---
# <a name="3-connecting-multiple-users"></a><span data-ttu-id="67e25-105">3.複数のユーザーの接続</span><span class="sxs-lookup"><span data-stu-id="67e25-105">3. Connecting multiple users</span></span>

<span data-ttu-id="67e25-106">このチュートリアルでは、ライブ共有エクスペリエンスの一部として複数のユーザーを接続する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="67e25-106">In this tutorial, you will learn how to connect multiple users as part of a live shared experience.</span></span> <span data-ttu-id="67e25-107">チュートリアルを終えるときには、複数のデバイスでアプリを実行して、各ユーザーが他のユーザーのアバターの動きをリアルタイムで確認できるようになります。</span><span class="sxs-lookup"><span data-stu-id="67e25-107">By the end of the tutorial, you will be able to run the app on multiple devices and have each user see the avatar of other users move in real-time.</span></span>

## <a name="objectives"></a><span data-ttu-id="67e25-108">目標</span><span class="sxs-lookup"><span data-stu-id="67e25-108">Objectives</span></span>

* <span data-ttu-id="67e25-109">共有エクスペリエンスで複数のユーザーを接続する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="67e25-109">Learn how to connect multiple users in a shared experience</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="67e25-110">シーンの準備</span><span class="sxs-lookup"><span data-stu-id="67e25-110">Preparing the scene</span></span>

<span data-ttu-id="67e25-111">このセクションでは、チュートリアルのプレハブをいくつか追加してシーンを準備します。</span><span class="sxs-lookup"><span data-stu-id="67e25-111">In this section, you will prepare the scene by adding some of the tutorial prefabs.</span></span>

<span data-ttu-id="67e25-112">[Project]\(プロジェクト\) ウィンドウで、 **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.MultiUserCapabilities]**  >  **[Prefabs]\(プレハブ\)** フォルダーに移動し、次のプレハブを [Hierarchy]\(階層\) ウィンドウにドラッグしてシーンに追加します。</span><span class="sxs-lookup"><span data-stu-id="67e25-112">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs** folder, then click-and-drag the following prefabs into the Hierarchy window to add them to your scene:</span></span>

* <span data-ttu-id="67e25-113">**NetworkLobby** プレハブ</span><span class="sxs-lookup"><span data-stu-id="67e25-113">**NetworkLobby** prefab</span></span>
* <span data-ttu-id="67e25-114">**SharedPlayground** プレハブ</span><span class="sxs-lookup"><span data-stu-id="67e25-114">**SharedPlayground** prefab</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section1-step1-1.png)

<span data-ttu-id="67e25-116">[Project]\(プロジェクト\) ウィンドウで、 **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.AzureSpatialAnchors]**  >  **[Prefabs]\(プレハブ\)** フォルダーに移動し、次のプレハブを [Hierarchy]\(階層\) ウィンドウにドラッグしてシーンに追加します。</span><span class="sxs-lookup"><span data-stu-id="67e25-116">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.AzureSpatialAnchors** > **Prefabs** folder, then click-and-drag the following prefab into the Hierarchy window to add it to your scene:</span></span>

* <span data-ttu-id="67e25-117">**DebugWindow** プレハブ</span><span class="sxs-lookup"><span data-stu-id="67e25-117">**DebugWindow** prefab</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section1-step1-2.png)

## <a name="creating-the-user-prefab"></a><span data-ttu-id="67e25-119">ユーザー プレハブを作成する</span><span class="sxs-lookup"><span data-stu-id="67e25-119">Creating the user prefab</span></span>

<span data-ttu-id="67e25-120">このセクションでは、共有エクスペリエンスでユーザーを表すために使用されるプレハブを作成します。</span><span class="sxs-lookup"><span data-stu-id="67e25-120">In this section, you will create a prefab that will be used to represent the users in the shared experience.</span></span>

### <a name="1-create-and-configure-the-user"></a><span data-ttu-id="67e25-121">1.ユーザーの作成と構成</span><span class="sxs-lookup"><span data-stu-id="67e25-121">1. Create and configure the user</span></span>

<span data-ttu-id="67e25-122">[Hierarchy]\(ヒエラルキー\) ウィンドウで空の領域を右クリックし、 **[Create Empty]\(空のユーザーを作成\)** を選択してシーンに空のオブジェクトを追加し、オブジェクトに「**PhotonUser**」という名前を付けて、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="67e25-122">In the Hierarchy window, right-click on an empty area and select **Create Empty** to add an empty object to your scene, name the object **PhotonUser**, and configure it as follows:</span></span>

* <span data-ttu-id="67e25-123">[Transform]\(変換\) の **[Position]\(位置\)** が、X = 0、Y = 0、Z = 0 に設定されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="67e25-123">Ensure the Transform **Position** is set to X = 0, Y = 0, Z = 0:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-1.png)

<span data-ttu-id="67e25-125">[Hierarchy]\(階層\) ウィンドウで、**PhotonUser** オブジェクトを選択し、[Inspector]\(インスペクター\) ウィンドウの **[Add Component]\(コンポーネントの追加\)** ボタンを使用して **Photon User (Script)** コンポーネントを PhotonUser オブジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="67e25-125">In the Hierarchy window, select the **PhotonUser** object, then in the Inspector window, use the **Add Component** button to add the **Photon User (Script)** component to the PhotonUser object:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-2.png)

<span data-ttu-id="67e25-127">[Inspector]\(インスペクター\) ウィンドウで、 **[Add Component]\(コンポーネントの追加\)** ボタンを使用して PhotonUser オブジェクトに **Generic Net Sync (Script)** コンポーネントを追加し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="67e25-127">In the Inspector window, use the **Add Component** button to add the **Generic Net Sync (Script)** component to the PhotonUser object and configure it as follows:</span></span>

* <span data-ttu-id="67e25-128">**[Is User]\(ユーザーである\)** チェックボックスをオンにする</span><span class="sxs-lookup"><span data-stu-id="67e25-128">Check the **Is User** checkbox</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-3.png)

<span data-ttu-id="67e25-130">[Inspector]\(インスペクター\) ウィンドウで、 **[Add Component]\(コンポーネントの追加\)** ボタンを使用して PhotonUser オブジェクトに **Photon View (Script)** コンポーネントを追加し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="67e25-130">In the Inspector window, use the **Add Component** button to add the **Photon View (Script)** component to the PhotonUser object and configure it as follows:</span></span>

* <span data-ttu-id="67e25-131">**[Observed Components]\(観察されるコンポーネント\)** フィールドに、**Generic Net Sync (Script)** コンポーネントを割り当てる</span><span class="sxs-lookup"><span data-stu-id="67e25-131">To the **Observed Components** field, assign the **Generic Net Sync (Script)** component</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-4.png)

### <a name="2-create-the-avatar"></a><span data-ttu-id="67e25-133">2.アバターを作成する</span><span class="sxs-lookup"><span data-stu-id="67e25-133">2. Create the avatar</span></span>

<span data-ttu-id="67e25-134">[Project]\(プロジェクト\) ウィンドウで、 **[Assets]\(アセット\)**  > **MRTK** > **SDK** > **StandardAssets** >  **[Materials]\(素材\)** に移動し、MRTK の素材を見つけます。</span><span class="sxs-lookup"><span data-stu-id="67e25-134">In the Project window, navigate to the **Assets** > **MRTK** > **SDK** > **StandardAssets** > **Materials** folder to locate the MRTK materials.</span></span>

<span data-ttu-id="67e25-135">次に、[Hierarchy]\(階層\) ウィンドウで、**PhotonUser** オブジェクトを右クリックして **[3D Object]\(3D オブジェクト\)**  >  **[Sphere]\(球体\)** を選択し、PhotonUser オブジェクトの子として球体オブジェクトを作成して次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="67e25-135">Then, in the Hierarchy window, right-click on the **PhotonUser** object and select **3D Object** > **Sphere** to create a sphere object as a child of the PhotonUser object and configure it as follows:</span></span>

* <span data-ttu-id="67e25-136">[Transform]\(変換\) の **[Position]\(位置\)** が、X = 0、Y = 0、Z = 0 に設定されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="67e25-136">Ensure the Transform **Position** is set to X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="67e25-137">[Transform]\(変換\) の **[Scale]\(スケール\)** を適切なサイズに変更する。例: X = 0.15、Y = 0.15、Z = 0.15</span><span class="sxs-lookup"><span data-stu-id="67e25-137">Change the Transform **Scale** to a suitable size, for example, X = 0.15, Y = 0.15, Z = 0.15</span></span>
* <span data-ttu-id="67e25-138">[MeshRenderer] > [Materials]\(素材\) > **[Element 0]\(要素 0\)** フィールドに、**MRTK_Standard_White** 素材を割り当てる</span><span class="sxs-lookup"><span data-stu-id="67e25-138">To the MeshRenderer > Materials > **Element 0** field, assign the **MRTK_Standard_White** material</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step2-1.png)

### <a name="3-create-the-prefab"></a><span data-ttu-id="67e25-140">3.プレハブを作成する</span><span class="sxs-lookup"><span data-stu-id="67e25-140">3. Create the prefab</span></span>

<span data-ttu-id="67e25-141">[Project]\(プロジェクト\) ウィンドウで **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.MultiUserCapabilities]**  >  **[Resources]\(リソース\)** フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="67e25-141">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** folder:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step3-1.png)

<span data-ttu-id="67e25-143">[Resources]\(リソース\) フォルダーを選択したまま、[Hierarchy]\(ヒエラルキー\) ウィンドウから **PhotonUser** オブジェクトを **[Resources]\(リソース\)** フォルダーに**クリックしてドラッグ**し、PhotonUser オブジェクトをプレハブにします。</span><span class="sxs-lookup"><span data-stu-id="67e25-143">With the Resources folder still selected, **click-and-drag** the **PhotonUser** object from the Hierarchy window into the **Resources** folder to make the PhotonUser object a prefab:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step3-2.png)

<span data-ttu-id="67e25-145">[Hierarchy]\(ヒエラルキー\) ウィンドウで **PhotonUser** オブジェクトを右クリックし、 **[Delete]\(削除\)** を選択してシーンから削除します。</span><span class="sxs-lookup"><span data-stu-id="67e25-145">In the Hierarchy window, right-click on the **PhotonUser** object and select **Delete** to remove it from the scene:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step3-3.png)

## <a name="configuring-pun-to-instantiate-the-user-prefab"></a><span data-ttu-id="67e25-147">PUN を構成してユーザー プレハブのインスタンスを作成する</span><span class="sxs-lookup"><span data-stu-id="67e25-147">Configuring PUN to instantiate the user prefab</span></span>

<span data-ttu-id="67e25-148">このセクションでは、前のセクションで作成した PhotonUser プレハブを使用するようにプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="67e25-148">In this section, you will configure the project to use the PhotonUser prefab you created in the previous section.</span></span>

<span data-ttu-id="67e25-149">[Project]\(プロジェクト\) ウィンドウで **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.MultiUserCapabilities]**  >  **[Resources]\(リソース\)** フォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="67e25-149">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** folder.</span></span>

<span data-ttu-id="67e25-150">[Hierarchy]\(ヒエラルキー\) ウィンドウで **NetworkLobby** オブジェクトを展開して **NetworkRoom** 子オブジェクトを選択し、[Inspector]\(インスペクター\) ウィンドウで **Photon Room (Script)** コンポーネントを探し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="67e25-150">In the Hierarchy window, expand the **NetworkLobby** object and select the **NetworkRoom** child object, then in the Inspector window, locate the **Photon Room (Script)** component and configure it as follows:</span></span>

* <span data-ttu-id="67e25-151">**"Photon User Prefab"(Photon ユーザー プレハブ)** フィールドに、[Resources]\(リソース\) フォルダーから **PhotonUser** プレハブを割り当てる</span><span class="sxs-lookup"><span data-stu-id="67e25-151">To the **Photon User Prefab** field, assign the **PhotonUser** prefab from the Resources folder</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section3-step1-1.png)

## <a name="trying-the-experience-with-multiple-users"></a><span data-ttu-id="67e25-153">複数のユーザーのエクスペリエンスを試す</span><span class="sxs-lookup"><span data-stu-id="67e25-153">Trying the experience with multiple users</span></span>

<span data-ttu-id="67e25-154">Unity プロジェクトをビルドして HoloLens に配置してから Unity に戻り、HoloLens でアプリが実行されている間にゲーム モードに入ると、頭 (HoloLens) を動かした時に HoloLens のユーザー アバターが動くのを確認できます。</span><span class="sxs-lookup"><span data-stu-id="67e25-154">If you now build and deploy the Unity project to your HoloLens, then, back in Unity, enter Game mode while the app is running on your HoloLens, you will see the HoloLens user avatar move when you move your head (HoloLens) around:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section4-step1-1.gif)

> [!TIP]
> <span data-ttu-id="67e25-156">HoloLens 2 に Unity プロジェクトをビルドして配置する方法を再確認するには、[HoloLens 2 にアプリをビルドする](mr-learning-base-02.md#building-your-application-to-your-hololens-2)手順に関する記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="67e25-156">For a reminder on how to build and deploy your Unity project to HoloLens 2, you can refer to the [Building your app to your HoloLens 2](mr-learning-base-02.md#building-your-application-to-your-hololens-2) instructions.</span></span>

> [!CAUTION]
> <span data-ttu-id="67e25-157">アプリから Photon に接続する必要があるため、お使いのコンピューターまたはデバイスがインターネットに接続されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="67e25-157">The app needs to connect to Photon, so make sure your computer/device is connected to the internet.</span></span>

## <a name="congratulations"></a><span data-ttu-id="67e25-158">結論</span><span class="sxs-lookup"><span data-stu-id="67e25-158">Congratulations</span></span>

<span data-ttu-id="67e25-159">複数のユーザーが同じエクスペリエンスに接続して、互いの動きを確認できるようにプロジェクトを構成できました。</span><span class="sxs-lookup"><span data-stu-id="67e25-159">You have successfully configured your project to allow multiple users to connect to the same experience and see each other's movements.</span></span> <span data-ttu-id="67e25-160">次のチュートリアルでは、オブジェクトの動きが複数のデバイスで共有されるようにする機能を実装します。</span><span class="sxs-lookup"><span data-stu-id="67e25-160">In the next tutorial, you will implement functionality so that the movements of objects are also shared across multiple devices.</span></span>

[<span data-ttu-id="67e25-161">次のチュートリアル:4.オブジェクトの動きの複数のユーザーとの共有</span><span class="sxs-lookup"><span data-stu-id="67e25-161">Next Tutorial: 4. Sharing object movements with multiple users</span></span>](mr-learning-sharing-04.md)
