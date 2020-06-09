---
title: 音声入力
description: HoloLens 2 および Unreal engine での音声入力の設定と使用に関するチュートリアル
author: hferrone
ms.author: v-haferr
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality、Unreal、Unreal Engine 4、UE4、HoloLens 2、音声、音声入力、音声認識、Mixed Reality、開発、機能、ドキュメント、ガイド、ホログラム、ゲーム開発
ms.openlocfilehash: 134a8c5bbeb700a973d3732d24fa9078feb568ef
ms.sourcegitcommit: 7f50210b71a65631fd1bc3fdb215064e0db34333
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84551788"
---
# <a name="voice-input-in-unreal"></a><span data-ttu-id="1df55-104">Unreal での音声入力</span><span class="sxs-lookup"><span data-stu-id="1df55-104">Voice Input in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="1df55-105">概要</span><span class="sxs-lookup"><span data-stu-id="1df55-105">Overview</span></span>
<span data-ttu-id="1df55-106">Unreal の音声入力を使用すると、ハンドジェスチャを使用しなくても、または HoloLens 2 のみがサポートされるようになります。</span><span class="sxs-lookup"><span data-stu-id="1df55-106">Voice input in Unreal allows you to interact with a hologram without having to use hand gestures and is only supported HoloLens 2.</span></span> <span data-ttu-id="1df55-107">HoloLens 2 での音声入力は、他のすべてのユニバーサル Windows アプリで音声をサポートする同じエンジンによって機能していますが、Unreal は独自のエンジンを使用して音声入力を処理します。</span><span class="sxs-lookup"><span data-stu-id="1df55-107">Even though voice input on HoloLens 2 is powered by the same engine that supports speech in all other Universal Windows Apps, Unreal uses a more limited engine of its own to process voice input.</span></span> <span data-ttu-id="1df55-108">これにより、次のセクションで説明するように、Unreal の音声入力機能が定義済みの音声マッピングに限定されます。</span><span class="sxs-lookup"><span data-stu-id="1df55-108">This limits voice input features in Unreal to predefined speech mappings, which is covered in the following sections.</span></span> 

## <a name="enabling-speech-recognition"></a><span data-ttu-id="1df55-109">音声認識を有効にする</span><span class="sxs-lookup"><span data-stu-id="1df55-109">Enabling Speech Recognition</span></span>

<span data-ttu-id="1df55-110">HoloLens で音声認識を有効にするには:</span><span class="sxs-lookup"><span data-stu-id="1df55-110">To enable speech recognition on HoloLens:</span></span>
1. <span data-ttu-id="1df55-111">[プロジェクトの設定] を選択して **> プラットフォーム > HoloLens > 機能**を選択し、**マイク**を有効にします。</span><span class="sxs-lookup"><span data-stu-id="1df55-111">Select **Project Settings > Platform > HoloLens > Capabilities** and enable **Microphone**.</span></span> 
2. <span data-ttu-id="1df55-112">[設定] で音声認識を有効にし、[**プライバシー] > [>** ] を選択します。 **English**</span><span class="sxs-lookup"><span data-stu-id="1df55-112">Enabled speech recognition in **Settings > Privacy > Speech** and select **English**.</span></span>

> [!NOTE]
> <span data-ttu-id="1df55-113">音声認識は常に、**設定**アプリで構成された Windows 表示言語で機能します。</span><span class="sxs-lookup"><span data-stu-id="1df55-113">Speech recognition always functions in the Windows display language configured in the **Settings** app.</span></span> <span data-ttu-id="1df55-114">また、サービス品質を最大限に高めるために、**オンライン音声認識**を有効にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1df55-114">It’s recommended that you also enable **Online speech recognition** for the best service quality.</span></span>

![Windows 音声認識の設定](images/unreal/speech-recognition-settings.png)

3. <span data-ttu-id="1df55-116">アプリケーションが最初にマイクを有効にするかどうかを確認すると、ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1df55-116">A dialog will show up when the application first starts to ask if you want to enable the microphone.</span></span> <span data-ttu-id="1df55-117">**[はい]** を選択すると、アプリで音声入力が開始されます。</span><span class="sxs-lookup"><span data-stu-id="1df55-117">Selecting **Yes** starts voice input in the app.</span></span>

<span data-ttu-id="1df55-118">音声入力には、特別な Windows Mixed Reality Api は必要ありません。これは、既存の Unreal Engine 4[入力](https://docs.unrealengine.com/Gameplay/Input/index.html)マッピング API を基に構築されています。</span><span class="sxs-lookup"><span data-stu-id="1df55-118">Voice input doesn’t require any special Windows Mixed Reality APIs; it's built on the existing Unreal Engine 4 [Input](https://docs.unrealengine.com/Gameplay/Input/index.html) mapping API.</span></span> 

## <a name="adding-speech-mappings"></a><span data-ttu-id="1df55-119">音声マッピングの追加</span><span class="sxs-lookup"><span data-stu-id="1df55-119">Adding Speech Mappings</span></span>
<span data-ttu-id="1df55-120">音声入力を使用する場合は、音声をアクションに接続することが重要な手順です。</span><span class="sxs-lookup"><span data-stu-id="1df55-120">Connecting speech to action is an important step when using voice input.</span></span> <span data-ttu-id="1df55-121">これらのマッピングは、ユーザーが話す可能性のある音声キーワードをアプリで監視し、リンクされたアクションを起動します。</span><span class="sxs-lookup"><span data-stu-id="1df55-121">These mappings monitor the app for speech keywords that a user might say, then fire off a linked action.</span></span> <span data-ttu-id="1df55-122">音声マッピングは、次の方法で見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="1df55-122">You can find Speech Mappings by:</span></span>
1. <span data-ttu-id="1df55-123">[**プロジェクト設定の編集 >**] を選択し、[**エンジン**] セクションまでスクロールして [**入力**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="1df55-123">Selecting **Edit > Project Settings**, scrolling to the **Engine** section, and clicking **Input**.</span></span>

<span data-ttu-id="1df55-124">ジャンプコマンドの新しい音声マッピングを追加するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="1df55-124">To add a new Speech Mapping for a jump command:</span></span>
1. <span data-ttu-id="1df55-125">[ **+** **配列要素**] の横にあるアイコンをクリックし、次の値を入力します。</span><span class="sxs-lookup"><span data-stu-id="1df55-125">Click the **+** icon next to **Array elements** and fill out the following values:</span></span>
    * <span data-ttu-id="1df55-126">**アクション名**の**jumpWord**</span><span class="sxs-lookup"><span data-stu-id="1df55-126">**jumpWord** for **Action Name**</span></span>
    * <span data-ttu-id="1df55-127">**Speech キーワード**の**ジャンプ**</span><span class="sxs-lookup"><span data-stu-id="1df55-127">**jump** for **Speech Keyword**</span></span>

> [!NOTE]
> <span data-ttu-id="1df55-128">すべての英語の単語または短い文をキーワードとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="1df55-128">Any English word(s) or short sentence(s) can be used as a keyword.</span></span> 

![UE4 Engine の入力設定](images/unreal/engine-input.png)

<span data-ttu-id="1df55-130">音声マッピングは、アクションや軸のマッピングなどの入力コンポーネントとして、またはイベントグラフのブループリントノードとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="1df55-130">Speech Mappings can be used as Input components like Action or Axis Mappings or as blueprint nodes in the Event Graph.</span></span> <span data-ttu-id="1df55-131">たとえば、ジャンプコマンドをリンクして、単語が話されるタイミングに応じて2つの異なるログを出力することができます。</span><span class="sxs-lookup"><span data-stu-id="1df55-131">For example, you could link the jump command to print out two different logs depending on when the word is spoken:</span></span>

1. <span data-ttu-id="1df55-132">ブループリントをダブルクリックして、**イベントグラフ**で開きます。</span><span class="sxs-lookup"><span data-stu-id="1df55-132">Double-click a blueprint to open it in the **Event Graph**.</span></span>
2. <span data-ttu-id="1df55-133">**右クリック**して音声マッピングの**アクション名**(この場合は**jumpWord**) を検索し、 **enter キー**を押します。</span><span class="sxs-lookup"><span data-stu-id="1df55-133">**Right-click** and search for the **Action Name** of your speech mapping (in this case **jumpWord**), then hit **Enter**.</span></span> <span data-ttu-id="1df55-134">これにより、グラフに**入力アクション**ノードが追加されます。</span><span class="sxs-lookup"><span data-stu-id="1df55-134">This adds an **Input Action** node to the graph.</span></span>
3. <span data-ttu-id="1df55-135">次の図に示すように、**押さ**れた pin をドラッグアンドドロップして文字列ノードを**印刷**します。</span><span class="sxs-lookup"><span data-stu-id="1df55-135">Drag and drop the **Pressed** pin to **Print String** node as shown in the image below.</span></span> <span data-ttu-id="1df55-136">**解放**された pin は空のままにすることができ、音声マッピングの場合は何も実行されません。</span><span class="sxs-lookup"><span data-stu-id="1df55-136">You can leave the **Released** pin empty, it won't execute anything for speech mappings.</span></span>
 
![音声の単純なアクション](images/unreal/voice-input-img-03.png)

4. <span data-ttu-id="1df55-138">アプリを再生します。 word の**ジャンプ**を言い、コンソールでログを出力します。</span><span class="sxs-lookup"><span data-stu-id="1df55-138">Play the app, say the word **jump** and watch the console print out the logs!</span></span>

<span data-ttu-id="1df55-139">これで、HoloLens アプリへの音声入力の追加を開始する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1df55-139">That's all the setup you'll need to start adding voice input to your HoloLens apps in Unreal.</span></span> <span data-ttu-id="1df55-140">音声と対話機能の詳細については、以下のリンクを参照してください。ユーザー向けに作成しているエクスペリエンスについて考えてください。</span><span class="sxs-lookup"><span data-stu-id="1df55-140">You can find more information on speech and interactivity can be found at the links below, and be sure to think about the experience you're creating for your users.</span></span>

## <a name="see-also"></a><span data-ttu-id="1df55-141">こちらもご覧ください</span><span class="sxs-lookup"><span data-stu-id="1df55-141">See also</span></span>
* [<span data-ttu-id="1df55-142">音声入力</span><span class="sxs-lookup"><span data-stu-id="1df55-142">Voice Input</span></span>](voice-input.md)
* [<span data-ttu-id="1df55-143">視線入力とコミット</span><span class="sxs-lookup"><span data-stu-id="1df55-143">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="1df55-144">本能的な操作</span><span class="sxs-lookup"><span data-stu-id="1df55-144">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="1df55-145">MR 入力 212:音声</span><span class="sxs-lookup"><span data-stu-id="1df55-145">MR Input 212: Voice</span></span>](holograms-212.md)

