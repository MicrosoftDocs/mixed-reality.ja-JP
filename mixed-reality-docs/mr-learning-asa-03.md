---
title: Azure Spatial Anchors チュートリアル - 3. Azure Spatial Anchors の保存、取得、および共有
description: このコースを完了すると Mixed Reality アプリケーション内に Azure Spatial Anchors を実装する方法を学習できます。
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: 25676404a71daf41b6a5c7587fa9bed95ab813f6
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86304946"
---
# <a name="3-saving-retrieving-and-sharing-azure-spatial-anchors"></a><span data-ttu-id="f59d6-105">3.Azure Spatial Anchors の保存、取得、および共有</span><span class="sxs-lookup"><span data-stu-id="f59d6-105">3. Saving, retrieving, and sharing Azure Spatial Anchors</span></span>

<span data-ttu-id="f59d6-106">このチュートリアルでは、HoloLens 2 のストレージにアンカー ID を保存することにより、複数のアプリ セッションにわたって Azure Spatial Anchors を保存する方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-106">In this tutorial, you will learn how to save Azure Spatial Anchors across multiple app sessions by saving the anchor ID to the HoloLens 2's storage.</span></span> <span data-ttu-id="f59d6-107">また、このアンカー ID を他のデバイスと共有して、複数デバイスのアンカーの位置合わせ行う方法についても学習します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-107">You will also learn how to share this anchor ID to other devices for a multi-device anchor alignment.</span></span>

## <a name="objectives"></a><span data-ttu-id="f59d6-108">目標</span><span class="sxs-lookup"><span data-stu-id="f59d6-108">Objectives</span></span>

* <span data-ttu-id="f59d6-109">複数のアプリ セッション間で空間的な位置合わせを実現する方法を学習する。</span><span class="sxs-lookup"><span data-stu-id="f59d6-109">Learn how to achieve spatial alignment across multiple app sessions.</span></span>
* <span data-ttu-id="f59d6-110">複数のデバイス間で空間的な位置合わせを実現する方法を学習する。</span><span class="sxs-lookup"><span data-stu-id="f59d6-110">Learn how to achieve spatial alignment between multiple devices.</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="f59d6-111">シーンの準備</span><span class="sxs-lookup"><span data-stu-id="f59d6-111">Preparing the scene</span></span>

<span data-ttu-id="f59d6-112">[階層] ウィンドウで、 **[ButtonParent]** オブジェクトを展開します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-112">In the Hierarchy window, expand the **ButtonParent** object.</span></span> <span data-ttu-id="f59d6-113">**最後の 4 つの子ボタン**のオブジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-113">Select the **last four child button** objects.</span></span> <span data-ttu-id="f59d6-114">[インスペクター] ウィンドウで、名前フィールドの横にあるチェックボックスを**オンにして**、すべてのオブジェクトをアクティブにします。</span><span class="sxs-lookup"><span data-stu-id="f59d6-114">In the Inspector window, **check** the checkbox next to the name field to make all the objects active.</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-03-section1-step1-1.png)

<span data-ttu-id="f59d6-116">[階層] ウィンドウで、 **[ButtonParent]** オブジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-116">In the Hierarchy window, select the **ButtonParent** objects.</span></span> <span data-ttu-id="f59d6-117">次に、[インスペクター] ウィンドウで **[GridObjectCollection]** コンポーネントを見つけ、 **[Update Collection]\(コレクションの更新\)** ボタンをクリックして、すべての **[ButtonParent]** オブジェクトの子オブジェクトの位置を更新します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-117">Then in the Inspector window, locate the **GridObjectCollection** component and click the **Update Collection** button to update the position of all the **ButtonParent** object's child objects.</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-03-section1-step1-2.png)

## <a name="persisting-azure-spatial-anchors-between-app-sessions"></a><span data-ttu-id="f59d6-119">アプリ セッション間での Azure Spatial Anchors の永続化</span><span class="sxs-lookup"><span data-stu-id="f59d6-119">Persisting Azure Spatial Anchors between app sessions</span></span>

<span data-ttu-id="f59d6-120">このセクションでは、Azure Anchor ID を HoloLens のローカル ディスクに保存したり、そこから取得したりする方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-120">In this section, you will learn how to save and retrieve the Azure Anchor ID to and from the HoloLens' local disk.</span></span> <span data-ttu-id="f59d6-121">これにより、異なるアプリ セッション間で同じアンカー ID の Azure に対してクエリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="f59d6-121">This will allow you to query Azure for the same anchor ID between different app sessions.</span></span> <span data-ttu-id="f59d6-122">固定されたホログラムを前のアプリ セッションと同じ場所に配置できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f59d6-122">It will enable the anchored holograms to be positioned at the same location as in the previous app session.</span></span>

<span data-ttu-id="f59d6-123">[階層] ウィンドウで **[ButtonParent]** オブジェクトを展開し、**SaveAzureAnchorIdToDisk** と **GetAzureAnchorIdFromDisk** という名前の 2 つのボタンを探します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-123">In the Hierarchy window, expand the **ButtonParent** object and locate the two buttons named **SaveAzureAnchorIdToDisk** and **GetAzureAnchorIdFromDisk**:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-03-section2-step1-1.png)

<span data-ttu-id="f59d6-125">前のチュートリアルの[シーンを操作するためのボタンの構成](mr-learning-asa-02.md#configuring-the-buttons-to-operate-the-scene)と同じ手順に従い、 **[Interactable (Script)]** コンポーネントを次の 2 つのボタンそれぞれに対して構成します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-125">Follow the same steps as in the [configuring the buttons to operate the scene](mr-learning-asa-02.md#configuring-the-buttons-to-operate-the-scene) instructions from the previous tutorial to configure the **Interactable (Script)** component on each of the two buttons:</span></span>

* <span data-ttu-id="f59d6-126">**[SaveAzureAnchorIdToDisk]** ボタン オブジェクトの場合、[AnchorModuleScript] を **[SaveAzureAnchorIdToDisk ()]** 関数に割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f59d6-126">For the **SaveAzureAnchorIdToDisk** button object, assign the AnchorModuleScript > **SaveAzureAnchorIdToDisk ()** function.</span></span>
* <span data-ttu-id="f59d6-127">**[GetAzureAnchorIdFromDisk]** ボタン オブジェクトの場合、[AnchorModuleScript] を **[GetAzureAnchorIdFromDisk ()]** 関数に割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f59d6-127">For the **GetAzureAnchorIdFromDisk** button object, assign the AnchorModuleScript > **GetAzureAnchorIdFromDisk ()** function.</span></span>

<span data-ttu-id="f59d6-128">更新されたアプリを HoloLens にビルドすると、Azure Anchor ID を保存することで、アプリ セッション間で Azure Spatial Anchors を永続化できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f59d6-128">If you build the updated app to your HoloLens, you can now persist Azure Spatial Anchors between app sessions by saving the Azure Anchor ID.</span></span> <span data-ttu-id="f59d6-129">これをテストするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-129">To test it out, you can follow these steps:</span></span>

1. <span data-ttu-id="f59d6-130">Rover Explorer を目的の場所に移動します</span><span class="sxs-lookup"><span data-stu-id="f59d6-130">Move the Rover Explorer to the desired location</span></span>
2. <span data-ttu-id="f59d6-131">Azure セッションを開始します</span><span class="sxs-lookup"><span data-stu-id="f59d6-131">Start Azure Session</span></span>
3. <span data-ttu-id="f59d6-132">Azure Anchor を作成します (Rover Explorer の場所にアンカーを作成します)</span><span class="sxs-lookup"><span data-stu-id="f59d6-132">Create Azure Anchor (creates anchors at the location of the Rover Explorer)</span></span>
4. <span data-ttu-id="f59d6-133">Azure Anchor ID をディスクに保存します</span><span class="sxs-lookup"><span data-stu-id="f59d6-133">Save Azure Anchor ID to Disk</span></span>
5. <span data-ttu-id="f59d6-134">アプリを再起動します</span><span class="sxs-lookup"><span data-stu-id="f59d6-134">Restart the app</span></span>
6. <span data-ttu-id="f59d6-135">ディスクから Azure Anchor を取得します (保存したアンカー ID を読み込みます)</span><span class="sxs-lookup"><span data-stu-id="f59d6-135">Get Azure Anchor from Disk (loads the anchor ID you just saved)</span></span>
7. <span data-ttu-id="f59d6-136">Azure セッションを開始します</span><span class="sxs-lookup"><span data-stu-id="f59d6-136">Start Azure Session</span></span>
8. <span data-ttu-id="f59d6-137">Azure Anchor を見つけます (手順 3 の場所に Rover Explorer を配置します)</span><span class="sxs-lookup"><span data-stu-id="f59d6-137">Find Azure Anchor (positions the Rover Explorer at the location from step 3)</span></span>

> [!NOTE]
> <span data-ttu-id="f59d6-138">アプリを完全に再起動するには、イマーシブ アプリ ビューを終了した後、[スタート] メニューからこれを再起動する前に、Mixed Reality ホームのアプリ ウィンドウを閉じる必要があります。</span><span class="sxs-lookup"><span data-stu-id="f59d6-138">To fully restart the app, after exiting the immersive app view, the app window in the mixed reality home needs to be closed before relaunching it from the Start menu.</span></span> <span data-ttu-id="f59d6-139">詳細については、「[HoloLens でアプリを使用する](https://docs.microsoft.com/hololens/holographic-home#using-apps-on-hololens)」のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f59d6-139">For additional details, you can refer to the [Using apps on HoloLens](https://docs.microsoft.com/hololens/holographic-home#using-apps-on-hololens) documentation.</span></span>

## <a name="sharing-azure-spatial-anchors-between-devices"></a><span data-ttu-id="f59d6-140">デバイス間での Azure Spatial Anchors の共有</span><span class="sxs-lookup"><span data-stu-id="f59d6-140">Sharing Azure Spatial Anchors between devices</span></span>

<span data-ttu-id="f59d6-141">このセクションでは、複数のデバイス間で Azure Anchor ID を共有する方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-141">In this section, you will learn how to share the Azure Anchor ID between multiple devices.</span></span> <span data-ttu-id="f59d6-142">これにより、複数のデバイスが同じアンカー ID を Azure に対してクエリできるようになり、固定されたホログラムを空間的に位置合わせできるようになります。</span><span class="sxs-lookup"><span data-stu-id="f59d6-142">This will allow multiple devices to query Azure for the same anchor ID, allowing the anchored holograms to be spatially aligned.</span></span> <span data-ttu-id="f59d6-143">空間的な位置合わせ、つまり複数のデバイス間で同じ物理的な場所に同じホログラムを表示できることは、HoloLens 2 のローカル共有エクスペリエンスにとって重要です。</span><span class="sxs-lookup"><span data-stu-id="f59d6-143">Spatial alignment, i.e., seeing the same holograms in the same physical location between multiple devices, is key to local shared experiences in the HoloLens 2.</span></span>

<span data-ttu-id="f59d6-144">Azure Anchor ID をデバイス間で転送するには、[マルチユーザー機能のチュートリアル](mr-learning-sharing-02.md) シリーズで説明されている方法など、さまざまな方法があります。</span><span class="sxs-lookup"><span data-stu-id="f59d6-144">There are many ways to transfer Azure Anchor IDs between devices, including methods outlined in the [Multi-user capabilities tutorials](mr-learning-sharing-02.md) series.</span></span> <span data-ttu-id="f59d6-145">この例では、デバイス間でアンカー ID をアップロードおよびダウンロードする単純な Web サービスを使用します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-145">In this example, you will use a simple web service to upload and download anchor IDs between devices.</span></span>

<span data-ttu-id="f59d6-146">[階層] ウィンドウで、 **[ButtonParent]** オブジェクトを展開します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-146">In the Hierarchy window, expand the **ButtonParent** object.</span></span>   <span data-ttu-id="f59d6-147">**ShareAzureAnchorIdToNetwork** と、**GetAzureAnchorIdFromNetwork** という名前の 2 つのボタンを見つけます。</span><span class="sxs-lookup"><span data-stu-id="f59d6-147">Locate the two buttons named **ShareAzureAnchorIdToNetwork** and **GetAzureAnchorIdFromNetwork**:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-03-section3-step1-1.png)

<span data-ttu-id="f59d6-149">前のチュートリアルの[シーンを操作するためのボタンの構成](mr-learning-asa-02.md#configuring-the-buttons-to-operate-the-scene)と同じ手順に従い、 **[Interactable (Script)]** コンポーネントを次の 2 つのボタンそれぞれに対して構成します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-149">Follow the same steps as in the [configuring the buttons to operate the scene](mr-learning-asa-02.md#configuring-the-buttons-to-operate-the-scene) instructions from the previous tutorial to configure the **Interactable (Script)** component on each of the two buttons:</span></span>

* <span data-ttu-id="f59d6-150">**[ShareAzureAnchorIdToNetwork]** オブジェクトの場合は、[AnchorModuleScript] > **[ShareAzureAnchorIdToNetwork ()]** 関数を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f59d6-150">For the **ShareAzureAnchorIdToNetwork** object, assign the AnchorModuleScript > **ShareAzureAnchorIdToNetwork ()** function.</span></span>
* <span data-ttu-id="f59d6-151">**[GetAzureAnchorIdFromNetwork]** オブジェクトの場合は、[AnchorModuleScript] > **[GetAzureAnchorIdFromNetwork ()]** 関数を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f59d6-151">For the **GetAzureAnchorIdFromNetwork** object, assign the AnchorModuleScript > **GetAzureAnchorIdFromNetwork ()** function.</span></span>

<span data-ttu-id="f59d6-152">更新されたアプリを 2 つの HoloLens デバイスにビルドすると、Azure Anchor ID を共有することで、空間的な位置合わせを実現できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f59d6-152">If you build the updated app to two HoloLens devices, you can now achieve spatial alignment by sharing the Azure Anchor ID.</span></span> <span data-ttu-id="f59d6-153">これをテストするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-153">To test it out, you can follow these steps:</span></span>

1. <span data-ttu-id="f59d6-154">HoloLens デバイス 1 で次のようにします。Rover Explorer を目的の場所に移動します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-154">On HoloLens device 1: Move the Rover Explorer to the desired location.</span></span>
2. <span data-ttu-id="f59d6-155">HoloLens デバイス 1 で次のようにします。Azure セッションを開始します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-155">On HoloLens device 1: Start Azure Session.</span></span>
3. <span data-ttu-id="f59d6-156">HoloLens デバイス 1 で次のようにします。Azure Anchor を作成します (Rover Explorer の場所にアンカーを作成します)。</span><span class="sxs-lookup"><span data-stu-id="f59d6-156">On HoloLens device 1: Create Azure Anchor (creates anchors at the location of the Rover Explorer).</span></span>
4. <span data-ttu-id="f59d6-157">HoloLens デバイス 1 で次のようにします。Azure Anchor ID をネットワークに共有します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-157">On HoloLens device 1: Share Azure Anchor ID to Network.</span></span>
5. <span data-ttu-id="f59d6-158">HoloLens デバイス 2 で次のようにします。アプリを起動します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-158">On HoloLens device 2: Start the app.</span></span>
6. <span data-ttu-id="f59d6-159">HoloLens デバイス 2 で次のようにします。ネットワークから共有アンカー ID を取得します (HoloLens デバイス 1 から共有されたアンカー ID を取得します)。</span><span class="sxs-lookup"><span data-stu-id="f59d6-159">On HoloLens device 2: Get Shared Anchor ID from Network (fetches the anchor ID just shared from HoloLens device 1).</span></span>
7. <span data-ttu-id="f59d6-160">HoloLens デバイス 2 で次のようにします。Azure セッションを開始します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-160">On HoloLens device 2: Start Azure Session.</span></span>
8. <span data-ttu-id="f59d6-161">HoloLens デバイス 2 で次のようにします。Azure Anchor を見つけます (手順 3 の場所に Rover Explorer を配置します)。</span><span class="sxs-lookup"><span data-stu-id="f59d6-161">On HoloLens device 2: Find Azure Anchor (positions the Rover Explorer at the location from step 3).</span></span>

> [!TIP]
> <span data-ttu-id="f59d6-162">HoloLens が 1 つしかない場合でも、2 つ目の HoloLens デバイスを使用する代わりにアプリを再起動することで、機能をテストできます。</span><span class="sxs-lookup"><span data-stu-id="f59d6-162">If you only have one HoloLens, you can still test the functionality by restarting the app instead of using a second HoloLens device.</span></span>

## <a name="congratulations"></a><span data-ttu-id="f59d6-163">結論</span><span class="sxs-lookup"><span data-stu-id="f59d6-163">Congratulations</span></span>

<span data-ttu-id="f59d6-164">このチュートリアルでは、Azure Spatial Anchor ID を HoloLens のローカル ディスクに保存して、アプリのセッションとアプリの再起動の間で Azure Spatial Anchors を永続化する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="f59d6-164">In this tutorial, you learned how to persist Azure Spatial Anchors between app sessions and app restarts by saving the Azure Spatial Anchor ID to the local disk on HoloLens.</span></span> <span data-ttu-id="f59d6-165">また、Azure Spatial Anchors を複数のデバイス間で共有し、基本的なマルチユーザーの静的ホログラム共有エクスペリエンスを実現する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="f59d6-165">You also learned how to share Azure Spatial Anchors between multiple devices for a basic multi-user, static hologram shared experience.</span></span>

<span data-ttu-id="f59d6-166">次のチュートリアルでは、リアルタイムのフィードバックをユーザーに提供する方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="f59d6-166">In the next tutorial, you will learn how to provide users with real-time feedback.</span></span> <span data-ttu-id="f59d6-167">このフィードバックには、アンカーの作成、環境の品質についての理解、および Azure セッションの状態に関する情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f59d6-167">This feedback will include information about Anchor creation, the quality of environment understanding, and the Azure session's state.</span></span> <span data-ttu-id="f59d6-168">フィードバックがなければ、アンカーが Azure に正常にアップロードされたかどうか、環境の品質がアンカーの作成に十分であるかどうか、または現在の状態をユーザーが知ることができません。</span><span class="sxs-lookup"><span data-stu-id="f59d6-168">Without feedback, users may not know whether an anchor has successfully been uploaded to Azure, whether the quality of the environment is sufficient for anchor creation, or the current state.</span></span>

[<span data-ttu-id="f59d6-169">次のチュートリアル:4.Azure Spatial Anchors フィードバックの表示</span><span class="sxs-lookup"><span data-stu-id="f59d6-169">Next Tutorial: 4. Displaying Azure Spatial Anchor feedback</span></span>](mr-learning-asa-04.md)
