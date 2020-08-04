---
title: 入門チュートリアル - 9. 音声コマンドの使用
description: このコースでは、Mixed Reality ツールキット (MRTK) を使用して Mixed Reality アプリケーションを作成する方法について説明します。
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: b0b9771d9569d100a354af96a34cd20ef2a3d7c4
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376594"
---
# <a name="9-using-speech-commands"></a><span data-ttu-id="579db-105">9.音声コマンドの使用</span><span class="sxs-lookup"><span data-stu-id="579db-105">9. Using speech commands</span></span>

## <a name="overview"></a><span data-ttu-id="579db-106">概要</span><span class="sxs-lookup"><span data-stu-id="579db-106">Overview</span></span>

<span data-ttu-id="579db-107">このチュートリアルでは、音声コマンドを作成する方法と、それらをグローバルに制御する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="579db-107">In this tutorial, you will learn how to create speech commands and how to control them globally.</span></span> <span data-ttu-id="579db-108">また、音声コマンドを制御するオブジェクトをユーザーが確認する必要があるローカルの音声コマンドを制御する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="579db-108">You will also learn how to control local speech commands that require the user to look at the object that controls the speech command.</span></span>

## <a name="objectives"></a><span data-ttu-id="579db-109">目標</span><span class="sxs-lookup"><span data-stu-id="579db-109">Objectives</span></span>

* <span data-ttu-id="579db-110">音声コマンドを作成する方法について説明します</span><span class="sxs-lookup"><span data-stu-id="579db-110">Learn how to create speech commands</span></span>
* <span data-ttu-id="579db-111">音声コマンドをグローバルおよびローカルで制御する方法について説明します</span><span class="sxs-lookup"><span data-stu-id="579db-111">Learn how to control speech commands globally and locally</span></span>

## <a name="ensuring-the-microphone-capability-is-enabled"></a><span data-ttu-id="579db-112">マイク機能が有効になっていることを確認する</span><span class="sxs-lookup"><span data-stu-id="579db-112">Ensuring the Microphone capability is enabled</span></span>

<span data-ttu-id="579db-113">[Unity] メニューで、[Mixed Reality Toolkit] > [Utilities]\(ユーティリティ\) > **[Configure Unity Project]\(Unity プロジェクトの構成\)** をクリックして **[MRTK Project Configurator]** ウィンドウを開き、 **[UWP Capabilities]\(UWP 機能\)** セクションで **[Enable Microphone Capability]\(マイク機能を有効にする\)** がグレーで表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="579db-113">In the Unity menu, select Mixed Reality Toolkit > Utilities > **Configure Unity Project** to open the **MRTK Project Configurator** window, then in the **UWP Capabilities** section, verify that **Enable Microphone Capability** is greyed out:</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section1-step1-1.png)

> [!NOTE]
> <span data-ttu-id="579db-115">このチュートリアル シリーズの冒頭で Unity プロジェクトを構成したときに、[MRTK Project Configurator 設定を適用する](mr-learning-base-02.md#1-apply-the-mrtk-project-configurator-settings)手順中にマイク機能を有効にしておく必要がありました。</span><span class="sxs-lookup"><span data-stu-id="579db-115">The Microphone capability should have been enabled during the [Apply the MRTK Project Configurator settings](mr-learning-base-02.md#1-apply-the-mrtk-project-configurator-settings) instructions when you configured the Unity project at the beginning of this tutorial series.</span></span> <span data-ttu-id="579db-116">しかし、有効にしていない場合は、ここで有効にしてください。</span><span class="sxs-lookup"><span data-stu-id="579db-116">However, if it is not enabled, make sure you enable it now.</span></span>

## <a name="creating-speech-commands"></a><span data-ttu-id="579db-117">音声コマンドを作成する</span><span class="sxs-lookup"><span data-stu-id="579db-117">Creating speech commands</span></span>

<span data-ttu-id="579db-118">[階層] ウィンドウで **[MixedRealityToolkit]** オブジェクトを選択し、[インスペクター] ウィンドウで [MixedRealityToolkit] > **[入力]** タブを選択して、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="579db-118">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, select the MixedRealityToolkit > **Input** tab and take the following steps:</span></span>

* <span data-ttu-id="579db-119">**[Speech]\(音声\)** セクションを展開します</span><span class="sxs-lookup"><span data-stu-id="579db-119">Expand the **Speech** section</span></span>
* <span data-ttu-id="579db-120">**DefaultMixedRealitySpeechCommandsProfile** を複製し、適切な名前 (たとえば、_GettingStarted_MixedRealitySpeechCommandsProfile_) を指定します</span><span class="sxs-lookup"><span data-stu-id="579db-120">Clone the **DefaultMixedRealitySpeechCommandsProfile** and give it a suitable name, for example, _GettingStarted_MixedRealitySpeechCommandsProfile_</span></span>
* <span data-ttu-id="579db-121">**[Start Behaviour]\(開始動作\)** が **[Auto Start]\(自動開始\)** に設定されていることを確認します</span><span class="sxs-lookup"><span data-stu-id="579db-121">Verify that **Start Behaviour** is set to **Auto Start**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="579db-123">MRTK プロファイルを複製する方法については、[MRTK プロファイルの構成](mr-learning-base-03.md)に関するページにある手順を参照してください。</span><span class="sxs-lookup"><span data-stu-id="579db-123">For a reminder on how to clone MRTK profiles, you can refer to the [Configuring the MRTK profiles](mr-learning-base-03.md) instructions.</span></span>

<span data-ttu-id="579db-124">[Speech]\(音声\) > **[Speech Commands]\(音声コマンド\)** セクションで、 **[+Add a New Speech Command]\(新しい音声コマンドの追加\)** ボタンを 4 回クリックして、既存の音声コマンドの一覧に新しい音声コマンドを 4 つ追加します。次に、 **[Keyword]\(キーワード\)** フィールドに次の語句を入力します。</span><span class="sxs-lookup"><span data-stu-id="579db-124">In the Speech > **Speech Commands** section, click the **+ Add a New Speech Command** button four times to add four new speech commands to the list of the existing speech commands, then in the **Keyword** fields enter the following phrases:</span></span>

* <span data-ttu-id="579db-125">Enable Indicator\(インジケーターの有効化\)</span><span class="sxs-lookup"><span data-stu-id="579db-125">Enable Indicator</span></span>
* <span data-ttu-id="579db-126">Enable Tap to Place\(タップの有効化\)</span><span class="sxs-lookup"><span data-stu-id="579db-126">Enable Tap to Place</span></span>
* <span data-ttu-id="579db-127">Enable Bounding Box\(境界ボックスの有効化\)</span><span class="sxs-lookup"><span data-stu-id="579db-127">Enable Bounding Box</span></span>
* <span data-ttu-id="579db-128">Disable Bounding Box\(境界ボックスの無効化\)</span><span class="sxs-lookup"><span data-stu-id="579db-128">Disable Bounding Box</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section2-step1-2.png)

> [!TIP]
> <span data-ttu-id="579db-130">コンピューターにマイクが搭載されていない場合は、音声コマンドにキーコードを割り当てることができます。これにより、対応するキーが押されたときにそれらをトリガーできます。</span><span class="sxs-lookup"><span data-stu-id="579db-130">If your computer does not have a microphone you can assign a KeyCode to the speech commands, which will let you trigger them when the corresponding key is pressed.</span></span>

## <a name="controlling-speech-commands"></a><span data-ttu-id="579db-131">音声コマンドを制御する</span><span class="sxs-lookup"><span data-stu-id="579db-131">Controlling speech commands</span></span>

<span data-ttu-id="579db-132">[プロジェクト] ウィンドウで、 **[Assets]\(アセット\)**  >  **[MRTK]**  >  **[SDK]**  >  **[Features]\(機能\)**  >  **[UX]**  >  **[Prefabs]\(プレハブ\)**  >  **[ToolTip]\(ヒント\)** フォルダーの順に移動して、ヒント プレハブを見つけます。</span><span class="sxs-lookup"><span data-stu-id="579db-132">In the Project window, navigate to the **Assets** > **MRTK** > **SDK** > **Features** > **UX** > **Prefabs** > **ToolTip** folder to locate the tooltip prefabs:</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-1.png)

<span data-ttu-id="579db-134">[階層] ウィンドウで空の領域を右クリックし、 **[Create Empty]\(空を作成\)** を選択してシーンに空のオブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="579db-134">In the Hierarchy window, right-click on an empty spot and select **Create Empty** to add an empty object to your scene.</span></span>

<span data-ttu-id="579db-135">プロジェクトに **SpeechInputHandler_Global** という名前を指定します。次に、[インスペクター] ウィンドウで、 **[コンポーネントの追加]** ボタンを使用して **[SpeechInputHandler]** コンポーネントを追加し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="579db-135">Name the object **SpeechInputHandler_Global**, then in the Inspector window, use the **Add Component** button to add the **SpeechInputHandler** component and configure it as follows:</span></span>

* <span data-ttu-id="579db-136">**[Is Focus Required]\(フォーカスが必要\)** チェックボックスを**オフ**にして、ユーザーが SpeechInputHandler コンポーネントを使用してオブジェクトを確認しなくても音声コマンドをトリガーできるようにします</span><span class="sxs-lookup"><span data-stu-id="579db-136">**Uncheck** the **Is Focus Required** checkbox, so the user is not required to look at the object with the SpeechInputHandler component to trigger the speech command</span></span>
* <span data-ttu-id="579db-137">[プロジェクト] ウィンドウで、 **[Speech Confirmation Tooltip Prefab]\(Speech Confirmation ヒント プレハブ\)** フィールドに **SpeechConfirmation Tooltip** プレハブを割り当てて、音声コマンドが認識されるとこのプレハブが表示されるようにします</span><span class="sxs-lookup"><span data-stu-id="579db-137">From the Project window, assign the **SpeechConfirmation Tooltip** prefab to the **Speech Confirmation Tooltip Prefab** field, to have this prefab appear when a speech command is recognized</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-2.png)

<span data-ttu-id="579db-139">SpeechInputHandler コンポーネントで、小さい **+** アイコンを 3 回クリックして、3 つのキーワード要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="579db-139">On the SpeechInputHandler component, click the small **+** icon three times to add three keyword elements:</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-3.png)

<span data-ttu-id="579db-141">**[Element 0]\(要素 0\)** を展開し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="579db-141">Expand **Element 0** and configure it as follows:</span></span>

* <span data-ttu-id="579db-142">**[Keyword]\(キーワード\)** フィールドに「**Enable Indicator\(インジケーターの有効化\)** 」と入力して、前のセクションで作成した [Enable Indicator]\(インジケーターの有効化\) 音声コマンドを参照します</span><span class="sxs-lookup"><span data-stu-id="579db-142">In the **Keyword** field, enter **Enable Indicator**, to reference the Enable Indicator speech command you created in the previous section</span></span>
* <span data-ttu-id="579db-143">小さい **+** アイコンをクリックして、イベントを追加します</span><span class="sxs-lookup"><span data-stu-id="579db-143">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="579db-144">[階層] ウィンドウで、 **[None (Object)]\(なし (オブジェクト)\)** フィールドに **Indicator** オブジェクトを割り当てます</span><span class="sxs-lookup"><span data-stu-id="579db-144">From the Hierarchy window, assign the **Indicator** object to the **None (Object)** field</span></span>
* <span data-ttu-id="579db-145">**[No Function]\(関数なし\)** ドロップダウンから、 **[GameObject]**  >  **[SetActive (bool)]** の順に選択し、イベントがトリガーされたときに実行するアクションとして、この関数を設定します</span><span class="sxs-lookup"><span data-stu-id="579db-145">From the **No Function** dropdown, select **GameObject** > **SetActive (bool)** to set this function as the action to be executed when the event is triggered</span></span>
* <span data-ttu-id="579db-146">引数チェックボックスが**オン**になっていることを確認します</span><span class="sxs-lookup"><span data-stu-id="579db-146">Check the argument checkbox, so it is **checked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-4.png)

<span data-ttu-id="579db-148">**[Element 1]\(要素 1\)** を展開し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="579db-148">Expand **Element 1** and configure it as follows:</span></span>

* <span data-ttu-id="579db-149">**[Keyword]\(キーワード\)** フィールドに「**Enable Bounding Box\(境界ボックスの有効化\)** 」と入力して、前のセクションで作成した [Enable Bounding Box]\(境界ボックスの有効化\) コマンドを参照します</span><span class="sxs-lookup"><span data-stu-id="579db-149">In the **Keyword** field, enter **Enable Bounding Box**, to reference the Enable Bounding Box command you created in the previous section</span></span>
* <span data-ttu-id="579db-150">小さい **+** アイコンをクリックして、イベントを追加します</span><span class="sxs-lookup"><span data-stu-id="579db-150">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="579db-151">[階層] ウィンドウで、 **[None (Object)]\(なし (オブジェクト)\)** フィールドに **RoverExplorer** オブジェクトを割り当てます</span><span class="sxs-lookup"><span data-stu-id="579db-151">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="579db-152">**[No Function]\(関数なし\)** ドロップダウンから、 **[BoundingBox]**  >  **[bool enabled]** の順に選択し、イベントがトリガーされたときにこのプロパティ値を更新するようにします</span><span class="sxs-lookup"><span data-stu-id="579db-152">From the **No Function** dropdown, select **BoundingBox** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="579db-153">引数チェックボックスが**オン**になっていることを確認します</span><span class="sxs-lookup"><span data-stu-id="579db-153">Check the argument checkbox, so it is **checked**</span></span>
* <span data-ttu-id="579db-154">小さい **[+]** アイコンをクリックして、別のイベントを追加します</span><span class="sxs-lookup"><span data-stu-id="579db-154">Click the small **+** icon to add another event</span></span>
* <span data-ttu-id="579db-155">[階層] ウィンドウで、 **[None (Object)]\(なし (オブジェクト)\)** フィールドに **RoverExplorer** オブジェクトを割り当てます</span><span class="sxs-lookup"><span data-stu-id="579db-155">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="579db-156">**[No Function]\(関数なし\)** ドロップダウンから、 **[ObjectManipulator]**  >  **[bool enabled]** の順に選択し、イベントがトリガーされたときにこのプロパティ値を更新するようにします</span><span class="sxs-lookup"><span data-stu-id="579db-156">From the **No Function** dropdown, select **ObjectManipulator** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="579db-157">引数チェックボックスが**オン**になっていることを確認します</span><span class="sxs-lookup"><span data-stu-id="579db-157">Check the argument checkbox, so it is **checked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-5.png)

<span data-ttu-id="579db-159">**[Element 2]\(要素 2\)** を展開し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="579db-159">Expand **Element 2** and configure it as follows:</span></span>

* <span data-ttu-id="579db-160">**[Keyword]\(キーワード\)** フィールドに「**Disable Bounding Box\(境界ボックスの無効化\)** 」と入力して、前のセクションで作成した [Disable Bounding Box]\(境界ボックスの無効化\) コマンドを参照します</span><span class="sxs-lookup"><span data-stu-id="579db-160">In the **Keyword** field, enter **Disable Bounding Box**, to reference the Disable Bounding Box command you created in the previous section</span></span>
* <span data-ttu-id="579db-161">小さい **+** アイコンをクリックして、イベントを追加します</span><span class="sxs-lookup"><span data-stu-id="579db-161">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="579db-162">[階層] ウィンドウで、 **[None (Object)]\(なし (オブジェクト)\)** フィールドに **RoverExplorer** オブジェクトを割り当てます</span><span class="sxs-lookup"><span data-stu-id="579db-162">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="579db-163">**[No Function]\(関数なし\)** ドロップダウンから、 **[BoundingBox]**  >  **[bool enabled]** の順に選択し、イベントがトリガーされたときにこのプロパティ値を更新するようにします</span><span class="sxs-lookup"><span data-stu-id="579db-163">From the **No Function** dropdown, select **BoundingBox** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="579db-164">引数チェックボックスが**オフ**になっていることを確認します</span><span class="sxs-lookup"><span data-stu-id="579db-164">Verify that the argument checkbox is **unchecked**</span></span>
* <span data-ttu-id="579db-165">小さい **[+]** アイコンをクリックして、別のイベントを追加します</span><span class="sxs-lookup"><span data-stu-id="579db-165">Click the small **+** icon to add another event</span></span>
* <span data-ttu-id="579db-166">[階層] ウィンドウで、 **[None (Object)]\(なし (オブジェクト)\)** フィールドに **RoverExplorer** オブジェクトを割り当てます</span><span class="sxs-lookup"><span data-stu-id="579db-166">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="579db-167">**[No Function]\(関数なし\)** ドロップダウンから、 **[ObjectManipulator]**  >  **[bool enabled]** の順に選択し、イベントがトリガーされたときにこのプロパティ値を更新するようにします</span><span class="sxs-lookup"><span data-stu-id="579db-167">From the **No Function** dropdown, select **ObjectManipulator** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="579db-168">引数チェックボックスが**オフ**になっていることを確認します</span><span class="sxs-lookup"><span data-stu-id="579db-168">Verify that the argument checkbox is **unchecked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-6.png)

<span data-ttu-id="579db-170">[階層] ウィンドウで、[RoverExplorer] > **[RoverAssembly]** オブジェクトの順に選択します。次に、[インスペクター] ウィンドウで、 **[コンポーネントの追加]** ボタンを使用して **[SpeechInputHandler]** コンポーネントを追加し、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="579db-170">In the Hierarchy window, select the RoverExplorer > **RoverAssembly** object, then in the Inspector window, use the **Add Component** button to add the **SpeechInputHandler** component and configure it as follows:</span></span>

* <span data-ttu-id="579db-171">**[Is Focus Required]\(フォーカスが必要\)** チェックボックスが**オン**になっていることを確認します。これにより、ユーザーは音声コマンドをトリガーするために SpeechInputHandler コンポーネント (RoverAssembly) を使用してオブジェクトを確認する必要が生じます</span><span class="sxs-lookup"><span data-stu-id="579db-171">Verify that the **Is Focus Required** checkbox is **check**, so the user is required to look at the object with the SpeechInputHandler component, i.e., the RoverAssembly, to trigger the speech command</span></span>
* <span data-ttu-id="579db-172">[プロジェクト] ウィンドウで、 **[Speech Confirmation Tooltip Prefab]\(Speech Confirmation ヒント プレハブ\)** フィールドに **SpeechConfirmation Tooltip** プレハブを割り当てて、音声コマンドが認識されるとこのプレハブが表示されるようにします</span><span class="sxs-lookup"><span data-stu-id="579db-172">From the Project window, assign the **SpeechConfirmation Tooltip** prefab to the **Speech Confirmation Tooltip Prefab** field, to have this prefab appear when a speech command is recognized</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-7.png)

<span data-ttu-id="579db-174">SpeechInputHandler コンポーネントで、小さい **+** アイコンをクリックしてキーワード要素を追加し、新しく作成された要素を展開して、次のように構成します。</span><span class="sxs-lookup"><span data-stu-id="579db-174">On the SpeechInputHandler component, click the small **+** icon to add a keyword element, expand the newly created element, then configure it as follows:</span></span>

* <span data-ttu-id="579db-175">**[Keyword]\(キーワード\)** フィールドに「**Enable Tap to Place\(タップの有効化\)** 」と入力して、前のセクションで作成した [Enable Tap to Place]\(タップの有効化\) コマンドを参照します</span><span class="sxs-lookup"><span data-stu-id="579db-175">In the **Keyword** field, enter **Enable Tap to Place**, to reference the Enable Tap to Place command you created in the previous section</span></span>
* <span data-ttu-id="579db-176">小さい **+** アイコンをクリックして、イベントを追加します</span><span class="sxs-lookup"><span data-stu-id="579db-176">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="579db-177">[階層] ウィンドウで、 **[None (Object)]\(なし (オブジェクト)\)** フィールドにオブジェクト自体 (同じ **RoverAssembly** オブジェクト) を割り当てます</span><span class="sxs-lookup"><span data-stu-id="579db-177">From the Hierarchy window, assign the object itself, i.e., the same **RoverAssembly** object, to the **None (Object)** field</span></span>
* <span data-ttu-id="579db-178">**[No Function]\(関数なし\)** ドロップダウンから、**TapToPlace** >  **[bool enabled]** の順に選択し、イベントがトリガーされたときにこのプロパティ値を更新するようにします</span><span class="sxs-lookup"><span data-stu-id="579db-178">From the **No Function** dropdown, select **TapToPlace** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="579db-179">引数チェックボックスが**オン**になっていることを確認します</span><span class="sxs-lookup"><span data-stu-id="579db-179">Check the argument checkbox, so it is **checked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-8.png)

## <a name="congratulations"></a><span data-ttu-id="579db-181">結論</span><span class="sxs-lookup"><span data-stu-id="579db-181">Congratulations</span></span>

<span data-ttu-id="579db-182">このチュートリアルでは、音声コマンドを作成する方法と、それらをグローバルに制御する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="579db-182">In this tutorial, you learned how to create speech commands and how to control them globally.</span></span> <span data-ttu-id="579db-183">音声コマンドを制御するオブジェクトをユーザーが確認する必要があるローカルの音声コマンドを制御する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="579db-183">You also learned how to control local speech commands that require the user to look at the object that controls the speech command.</span></span>

<span data-ttu-id="579db-184">また、[入門チュートリアル](mr-learning-base-01.md) シリーズも終了しました。</span><span class="sxs-lookup"><span data-stu-id="579db-184">This also concludes the [Getting started tutorials](mr-learning-base-01.md) series.</span></span> <span data-ttu-id="579db-185">これらのチュートリアルでは、MRTK を使用して最初から完全な mixed reality エクスペリエンスを正常に構築できました。</span><span class="sxs-lookup"><span data-stu-id="579db-185">Through these tutorials, you have successfully built a complete mixed reality experience from scratch using the MRTK.</span></span>

<span data-ttu-id="579db-186">次の [Azure Spatial Anchors のチュートリアル](mr-learning-asa-01.md)と[マルチユーザー機能のチュートリアル](mr-learning-sharing-01.md)の 2 つのチュートリアル シリーズでは、まず、Azure Spatial Anchors をプロジェクトに統合して、実際に作成した Rover Explorer のエクスペリエンスを固定する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="579db-186">In the next two tutorial series, [Azure Spatial Anchors tutorials](mr-learning-asa-01.md) and [Multi-user capabilities tutorials](mr-learning-sharing-01.md), you will first learn how to integrate Azure Spatial Anchors into your project to anchor the Rover Explorer experience you created in the real world.</span></span> <span data-ttu-id="579db-187">次に、ユーザーとオブジェクトの移動をリアルタイムで共有するために、マルチユーザー機能をプロジェクトに追加する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="579db-187">Then, you will learn how to add multi-user capabilities to your project to share user and object movements in real-time.</span></span>
