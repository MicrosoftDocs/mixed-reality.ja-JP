---
title: Unity 開発の概要
description: Unity で Mixed Reality アプリのビルドを開始します。
author: thetuvix
ms.author: kurtie
ms.date: 07/29/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unity, Mixed Reality, 開発, 概要, 新しいプロジェクト, 移植, 機能, カメラ, シミュレーション, エミュレーション, ドキュメント
ms.openlocfilehash: 4679e1a2b58a7e0d77e6b295803624a4de1fac19
ms.sourcegitcommit: ef0bf03833eda826ed0b884859b4573775112aba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87476714"
---
# <a name="unity-development-overview"></a><span data-ttu-id="f170a-104">Unity 開発の概要</span><span class="sxs-lookup"><span data-stu-id="f170a-104">Unity development overview</span></span>

<span data-ttu-id="f170a-105">[Mixed Reality アプリ](app-views.md)を構築する最速の方法は、[Unity](https://unity.com) を使用することです。</span><span class="sxs-lookup"><span data-stu-id="f170a-105">The fastest path to building a [mixed reality app](app-views.md) is with [Unity](https://unity.com).</span></span> <span data-ttu-id="f170a-106">時間を取って、[Unity のチュートリアル](https://unity3d.com/learn/tutorials)をご覧になることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f170a-106">We recommend that you take time to explore the [Unity tutorials](https://unity3d.com/learn/tutorials).</span></span> <span data-ttu-id="f170a-107">資産が必要な場合、Unity には包括的な[資産ストア](https://www.assetstore.unity3d.com/)があります。</span><span class="sxs-lookup"><span data-stu-id="f170a-107">If you need assets, Unity has a comprehensive [Asset Store](https://www.assetstore.unity3d.com/).</span></span> <span data-ttu-id="f170a-108">Unity についての基本的な理解ができたら、[チュートリアル](tutorials.md)にアクセスして、Unity を使用した Mixed Reality 開発の詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="f170a-108">Once you have built up a basic understanding of Unity, you can visit the [tutorials](tutorials.md) to learn the specifics of mixed reality development with Unity.</span></span> <span data-ttu-id="f170a-109">[Unity Mixed Reality フォーラム](https://forum.unity3d.com/forums/hololens.102/)にアクセスして、Unity で Mixed Reality アプリを構築する他のコミュニティと協働し、遭遇しがちな問題の解決策を見つけてください。</span><span class="sxs-lookup"><span data-stu-id="f170a-109">Be sure to visit the [Unity Mixed Reality forums](https://forum.unity3d.com/forums/hololens.102/) to engage with the rest of the community building mixed reality apps in Unity and find solutions to problems you might run into.</span></span>

<span data-ttu-id="f170a-110">Unity を使用して Mixed Reality アプリの構築を開始するには、まず、[ツールをインストール](install-the-tools.md)します。</span><span class="sxs-lookup"><span data-stu-id="f170a-110">To get started building mixed reality apps with Unity, first [install the tools](install-the-tools.md).</span></span>

## <a name="new-unity-project-with-mixed-reality-toolkit"></a><span data-ttu-id="f170a-111">Mixed Reality Toolkit による新しい Unity プロジェクト</span><span class="sxs-lookup"><span data-stu-id="f170a-111">New Unity Project with Mixed Reality Toolkit</span></span> 

<span data-ttu-id="f170a-112">Unity で開発する最も簡単な方法は、Mixed Reality Toolkit を使用することです。これを使用すると、プロジェクトでの設定を自動的に行い、用意されている一連の Mixed Reality 機能を利用して開発を促進できます。</span><span class="sxs-lookup"><span data-stu-id="f170a-112">The easiest way to develop in Unity is with the Mixed Reality Toolkit, which will help you set up with the project automatically, and provide a set of mixed reality features to accelerate your development.</span></span> <span data-ttu-id="f170a-113">詳細を確認して使い始めるには、[Mixed Reality Toolkit v2](mrtk-getting-started.md) に関する記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f170a-113">Check out [Mixed Reality Toolkit v2](mrtk-getting-started.md) to learn more and get started.</span></span> 

## <a name="porting-an-existing-unity-app-to-windows-mixed-reality"></a><span data-ttu-id="f170a-114">既存の Unity アプリを Windows Mixed Reality に移植する</span><span class="sxs-lookup"><span data-stu-id="f170a-114">Porting an existing Unity app to Windows Mixed Reality</span></span>

<span data-ttu-id="f170a-115">Windows Mixed Reality への移植を予定している既存の Unity プロジェクトがある場合は、[Unity 移植ガイド](porting-guides.md)に従って作業を開始してください。</span><span class="sxs-lookup"><span data-stu-id="f170a-115">If you have an existing Unity project that you're porting to Windows Mixed Reality, follow along with the [Unity porting guide](porting-guides.md) to get started.</span></span>

## <a name="configuring-new-unity-project-for-windows-mixed-reality"></a><span data-ttu-id="f170a-116">Windows Mixed Reality 用に新しい Unity プロジェクトを構成する</span><span class="sxs-lookup"><span data-stu-id="f170a-116">Configuring new Unity project for Windows Mixed Reality</span></span>

<span data-ttu-id="f170a-117">Mixed Reality Toolkit をインポートせずに新しい Unity プロジェクトを作成する場合は、いくつかの Unity 設定を Windows Mixed Reality 用に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f170a-117">If you're creating a new Unity project without importing Mixed Reality Toolkit, there are a small set of Unity settings you need to change for Windows Mixed Reality.</span></span> <span data-ttu-id="f170a-118">これらの設定は、プロジェクトごととシーンごとの 2 つのカテゴリに分類されます。</span><span class="sxs-lookup"><span data-stu-id="f170a-118">These settings are broken down into two categories: per-project and per-scene.</span></span> <span data-ttu-id="f170a-119">ステップ バイ ステップ ガイドについては、「[Windows Mixed Reality 用の新しい Unity プロジェクトを構成する](Configure-Unity-Project.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f170a-119">See here for a step-by-step guide to [Configure new Unity Project for Windows Mixed Reality](Configure-Unity-Project.md)</span></span>

## <a name="adding-mixed-reality-capabilities-and-inputs"></a><span data-ttu-id="f170a-120">Mixed Reality の機能と入力値を追加する</span><span class="sxs-lookup"><span data-stu-id="f170a-120">Adding mixed reality capabilities and inputs</span></span>

<span data-ttu-id="f170a-121">プロジェクトに MRTK V2 をセットアップするか、前述のようにプロジェクトを構成したら、標準の Unity ゲーム オブジェクト (カメラなど) が**座位のエクスペリエンス**に対応してすぐに点灯します。ユーザーが頭を移動すると、カメラの位置が自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="f170a-121">Once you've setup MRTK V2 with your project or configured your project as described above, standard Unity game objects like the camera will light up immediately for a **seated-scale experience**, with the camera's position updated automatically as the user moves their head through the world.</span></span>

<span data-ttu-id="f170a-122">Unity に直接組み込まれている API を使用して、[空間ステージ](coordinate-systems.md#spatial-coordinate-systems)、[ジェスチャ、モーション コントローラー](gestures-and-motion-controllers-in-unity.md)、[音声入力](voice-input-in-unity.md)など、Windows Mixed Reality 機能のサポートを追加できます。</span><span class="sxs-lookup"><span data-stu-id="f170a-122">Adding support for Windows Mixed Reality features, such as [spatial stages](coordinate-systems.md#spatial-coordinate-systems), [gestures, motion controllers](gestures-and-motion-controllers-in-unity.md), or [voice input](voice-input-in-unity.md) is achieved using APIs built directly into Unity.</span></span> 

<span data-ttu-id="f170a-123">まず、お使いのアプリケーションが対象にできる[エクスペリエンスのスケール](coordinate-systems.md)を確認します。</span><span class="sxs-lookup"><span data-stu-id="f170a-123">First, review the [experience scales](coordinate-systems.md) that your application can target:</span></span>
* <span data-ttu-id="f170a-124">**向き限定**や**座位のエクスペリエンス**を構築する場合は、Unity 上で追跡する空間の種類を [[ひな形]](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience) に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f170a-124">If you're looking to build an **orientation-only** or **seated-scale experience**, you'll need to set Unity's tracking space type to [Stationary](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).</span></span>
* <span data-ttu-id="f170a-125">**立位**または**空間スケールのエクスペリエンス**を構築する場合は、Unity 上で追跡する空間の種類を確実に [RoomScale](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience) に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f170a-125">If you're looking to build a **standing-scale** or **room-scale experience**, you'll need to ensure Unity's tracking space type is successfully set to [RoomScale](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).</span></span>
* <span data-ttu-id="f170a-126">ユーザーが 5 メートルを超えてローミングできるようにする**ワールドスケール**のエクスペリエンスを HoloLens 上で構築する場合は、[WorldAnchor](coordinate-systems-in-unity.md#building-a-world-scale-experience) コンポーネントを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f170a-126">If you're looking to build a **world-scale** experience on HoloLens that lets users roam beyond 5 meters, you'll need to use the [WorldAnchor](coordinate-systems-in-unity.md#building-a-world-scale-experience) component.</span></span>

<span data-ttu-id="f170a-127">Mixed Reality アプリケーションのコアな構成要素はすべて、他の Unity API と一貫した手法で公開されています。</span><span class="sxs-lookup"><span data-stu-id="f170a-127">All of the core building blocks for mixed reality applications are exposed in a manner consistent with other Unity APIs.</span></span> <span data-ttu-id="f170a-128">また、Mixed Reality Toolkit を通じて入手することもできます。</span><span class="sxs-lookup"><span data-stu-id="f170a-128">They are also available through the Mixed Reality Toolkit.</span></span>
* [<span data-ttu-id="f170a-129">カメラ</span><span class="sxs-lookup"><span data-stu-id="f170a-129">Camera</span></span>](camera-in-unity.md)
* [<span data-ttu-id="f170a-130">座標系</span><span class="sxs-lookup"><span data-stu-id="f170a-130">Coordinate systems</span></span>](coordinate-systems-in-unity.md)
* [<span data-ttu-id="f170a-131">視線入力</span><span class="sxs-lookup"><span data-stu-id="f170a-131">Gaze</span></span>](gaze-in-unity.md)
* [<span data-ttu-id="f170a-132">ジェスチャとモーション コントローラー</span><span class="sxs-lookup"><span data-stu-id="f170a-132">Gestures and motion controllers</span></span>](gestures-and-motion-controllers-in-unity.md)
* [<span data-ttu-id="f170a-133">音声入力</span><span class="sxs-lookup"><span data-stu-id="f170a-133">Voice input</span></span>](voice-input-in-unity.md)
* [<span data-ttu-id="f170a-134">永続化</span><span class="sxs-lookup"><span data-stu-id="f170a-134">Persistence</span></span>](persistence-in-unity.md)
* [<span data-ttu-id="f170a-135">立体音響</span><span class="sxs-lookup"><span data-stu-id="f170a-135">Spatial sound</span></span>](spatial-sound-in-unity.md)
* [<span data-ttu-id="f170a-136">空間マッピング</span><span class="sxs-lookup"><span data-stu-id="f170a-136">Spatial mapping</span></span>](spatial-mapping-in-unity.md)

<span data-ttu-id="f170a-137">以下に示す、多くの Mixed Reality アプリケーション上で使用される他の重要な機能も、Unity アプリに公開されています。</span><span class="sxs-lookup"><span data-stu-id="f170a-137">There are other key features that many mixed reality applications will want to use that are also exposed to Unity apps:</span></span>
* [<span data-ttu-id="f170a-138">共有エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="f170a-138">Shared experiences</span></span>](shared-experiences-in-unity.md)
* [<span data-ttu-id="f170a-139">場所を特定できるカメラ</span><span class="sxs-lookup"><span data-stu-id="f170a-139">Locatable camera</span></span>](locatable-camera-in-unity.md)
* [<span data-ttu-id="f170a-140">フォーカス ポイント</span><span class="sxs-lookup"><span data-stu-id="f170a-140">Focus point</span></span>](focus-point-in-unity.md)
* [<span data-ttu-id="f170a-141">追跡の損失</span><span class="sxs-lookup"><span data-stu-id="f170a-141">Tracking loss</span></span>](tracking-loss-in-unity.md)
* [<span data-ttu-id="f170a-142">キーボード</span><span class="sxs-lookup"><span data-stu-id="f170a-142">Keyboard</span></span>](keyboard-input-in-unity.md)

## <a name="running-your-unity-project-on-a-real-or-simulated-device"></a><span data-ttu-id="f170a-143">実際のデバイスまたはシミュレートされたデバイス上で Unity プロジェクトを実行する</span><span class="sxs-lookup"><span data-stu-id="f170a-143">Running your Unity project on a real or simulated device</span></span>

<span data-ttu-id="f170a-144">ホログラフィック Unity プロジェクトをテストする準備ができたら、次の手順として、[Unity Visual Studio ソリューションをエクスポートしてビルド](exporting-and-building-a-unity-visual-studio-solution.md)します。</span><span class="sxs-lookup"><span data-stu-id="f170a-144">Once you've got your holographic Unity project ready for testing, your next step is to [export and build a Unity Visual Studio solution](exporting-and-building-a-unity-visual-studio-solution.md).</span></span>

<span data-ttu-id="f170a-145">その VS ソリューションが手元にあれば、実際のデバイスまたはシミュレートされたデバイスのどちらかを使用して、次の 3 つの方法のいずかでアプリケーションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="f170a-145">With that VS solution in hand, you can then run your application in one of three ways, using either a real or simulated device:</span></span>
* [<span data-ttu-id="f170a-146">実際の HoloLens または Windows Mixed Reality イマーシブ ヘッドセットにデプロイする</span><span class="sxs-lookup"><span data-stu-id="f170a-146">Deploy to a real HoloLens or Windows Mixed Reality immersive headset</span></span>](using-visual-studio.md)
* [<span data-ttu-id="f170a-147">HoloLens エミュレーターにデプロイする</span><span class="sxs-lookup"><span data-stu-id="f170a-147">Deploy to the HoloLens emulator</span></span>](using-the-hololens-emulator.md)
* [<span data-ttu-id="f170a-148">Windows Mixed Reality イマーシブ ヘッドセット シミュレーターにデプロイする</span><span class="sxs-lookup"><span data-stu-id="f170a-148">Deploy to the Windows Mixed Reality immersive headset simulator</span></span>](using-the-windows-mixed-reality-simulator.md)

## <a name="unity-documentation"></a><span data-ttu-id="f170a-149">Unity のドキュメント</span><span class="sxs-lookup"><span data-stu-id="f170a-149">Unity documentation</span></span>

<span data-ttu-id="f170a-150">このドキュメントは docs.microsoft.com 上で入手できますが、Unity では、Windows Mixed Reality 機能に関するドキュメントが Unity エディターと共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="f170a-150">In addition to this documentation available on docs.microsoft.com, Unity installs documentation for Windows Mixed Reality functionality alongside the Unity Editor.</span></span> <span data-ttu-id="f170a-151">Unity が提供するドキュメントには、次の 2 つのセクションがあります。</span><span class="sxs-lookup"><span data-stu-id="f170a-151">The Unity provided documentation includes two separate sections:</span></span>
1. <span data-ttu-id="f170a-152">**Unity スクリプト リファレンス**</span><span class="sxs-lookup"><span data-stu-id="f170a-152">**Unity scripting reference**</span></span>
    * <span data-ttu-id="f170a-153">ドキュメントのこのセクションには、Unity が提供するスクリプト作成 API の詳細が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f170a-153">This section of the documentation contains details of the scripting API that Unity provides.</span></span>
    * <span data-ttu-id="f170a-154">**[ヘルプ] > [Scripting Reference]\(スクリプト作成のリファレンス\)**  を使用して、Unity エディターからアクセス可能です</span><span class="sxs-lookup"><span data-stu-id="f170a-154">Accessible from the Unity Editor through **Help > Scripting Reference**</span></span>
2. <span data-ttu-id="f170a-155">**Unity マニュアル**</span><span class="sxs-lookup"><span data-stu-id="f170a-155">**Unity manual**</span></span>
    * <span data-ttu-id="f170a-156">このマニュアルは、基本的な手法から高度な手法まで、Unity の使用方法を学習できるように編成されています。</span><span class="sxs-lookup"><span data-stu-id="f170a-156">This manual is designed to help you learn how to use Unity, from basic to advanced techniques.</span></span>
    * <span data-ttu-id="f170a-157">**[ヘルプ] > [マニュアル]** を使用して、Unity エディターからアクセス可能です</span><span class="sxs-lookup"><span data-stu-id="f170a-157">Accessible from the Unity Editor through **Help > Manual**</span></span>

## <a name="see-also"></a><span data-ttu-id="f170a-158">関連項目</span><span class="sxs-lookup"><span data-stu-id="f170a-158">See also</span></span>
* [<span data-ttu-id="f170a-159">Mixed Reality Toolkit v2</span><span class="sxs-lookup"><span data-stu-id="f170a-159">Mixed Reality Toolkit v2</span></span>](mrtk-getting-started.md)
* [<span data-ttu-id="f170a-160">MR の基本 100:Unity の概要</span><span class="sxs-lookup"><span data-stu-id="f170a-160">MR Basics 100: Getting started with Unity</span></span>](holograms-100.md)
* [<span data-ttu-id="f170a-161">Unity で推奨される設定</span><span class="sxs-lookup"><span data-stu-id="f170a-161">Recommended settings for Unity</span></span>](recommended-settings-for-unity.md)
* [<span data-ttu-id="f170a-162">Unity のパフォーマンスに関する推奨事項</span><span class="sxs-lookup"><span data-stu-id="f170a-162">Performance recommendations for Unity</span></span>](performance-recommendations-for-unity.md)
* [<span data-ttu-id="f170a-163">Unity Visual Studio ソリューションのエクスポートとビルド</span><span class="sxs-lookup"><span data-stu-id="f170a-163">Exporting and building a Unity Visual Studio solution</span></span>](exporting-and-building-a-unity-visual-studio-solution.md)
* [<span data-ttu-id="f170a-164">Windows 名前空間と HoloLens 用 Unity アプリの使用</span><span class="sxs-lookup"><span data-stu-id="f170a-164">Using the Windows namespace with Unity apps for HoloLens</span></span>](using-the-windows-namespace-with-unity-apps-for-hololens.md)
* [<span data-ttu-id="f170a-165">Unity と Visual Studio を使用するためのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="f170a-165">Best practices for working with Unity and Visual Studio</span></span>](best-practices-for-working-with-unity-and-visual-studio.md)
* [<span data-ttu-id="f170a-166">Unity の再生モード</span><span class="sxs-lookup"><span data-stu-id="f170a-166">Unity Play Mode</span></span>](unity-play-mode.md)
* [<span data-ttu-id="f170a-167">移植ガイド</span><span class="sxs-lookup"><span data-stu-id="f170a-167">Porting guides</span></span>](porting-guides.md)
