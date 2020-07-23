---
title: マルチユーザー機能のチュートリアル - 1。 はじめに
description: このコースでは、HoloLens 2 アプリケーション内でマルチユーザー共有エクスペリエンスを実装する方法を学習します。
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: eff600ba6388732ab9aa200ce41494cac1dddf35
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86306797"
---
# <a name="1-introduction"></a><span data-ttu-id="2ffed-105">1.はじめに</span><span class="sxs-lookup"><span data-stu-id="2ffed-105">1. Introduction</span></span>

## <a name="overview"></a><span data-ttu-id="2ffed-106">概要</span><span class="sxs-lookup"><span data-stu-id="2ffed-106">Overview</span></span>

<span data-ttu-id="2ffed-107">マルチユーザー機能のチュートリアルへようこそ。</span><span class="sxs-lookup"><span data-stu-id="2ffed-107">Welcome to the Multi-User Capabilities tutorials!</span></span> <span data-ttu-id="2ffed-108">このチュートリアル シリーズでは、<a href="https://www.photonengine.com/PUN" target="_blank">Photon Unity Networking</a> (PUN) を使用したマルチユーザー エクスペリエンスの構築方法の基礎について学習します。</span><span class="sxs-lookup"><span data-stu-id="2ffed-108">Through this tutorial series, you will learn the fundamentals of building a multi-user experience using <a href="https://www.photonengine.com/PUN" target="_blank">Photon Unity Networking</a> (PUN).</span></span> <span data-ttu-id="2ffed-109">PUN は、Mixed Reality の開発者が共有エクスペリエンスを作成するために使用できるいくつかのネットワーク オプションの 1 つです。</span><span class="sxs-lookup"><span data-stu-id="2ffed-109">PUN is one of several networking options available to mixed reality developers to create shared experiences.</span></span>

<span data-ttu-id="2ffed-110">このシリーズのチュートリアル:</span><span class="sxs-lookup"><span data-stu-id="2ffed-110">Tutorials in this series:</span></span>

* [<span data-ttu-id="2ffed-111">Photon Unity Networking の設定</span><span class="sxs-lookup"><span data-stu-id="2ffed-111">Setting up Photon Unity Networking</span></span>](mr-learning-sharing-02.md)
* [<span data-ttu-id="2ffed-112">複数のユーザーの接続</span><span class="sxs-lookup"><span data-stu-id="2ffed-112">Connecting multiple users</span></span>](mr-learning-sharing-03.md)
* [<span data-ttu-id="2ffed-113">複数のユーザーとオブジェクトの移動を共有する</span><span class="sxs-lookup"><span data-stu-id="2ffed-113">Sharing object movements with multiple users</span></span>](mr-learning-sharing-04.md)
* [<span data-ttu-id="2ffed-114">Azure Spatial Anchors の共有エクスペリエンスへの統合</span><span class="sxs-lookup"><span data-stu-id="2ffed-114">Integrating Azure Spatial Anchors into a shared experience</span></span>](mr-learning-sharing-05.md)

## <a name="objectives"></a><span data-ttu-id="2ffed-115">目標</span><span class="sxs-lookup"><span data-stu-id="2ffed-115">Objectives</span></span>

* <span data-ttu-id="2ffed-116">PUN アプリを作成して Unity プロジェクトをそれに接続する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="2ffed-116">Learn how to create a PUN app and connect your Unity project to it</span></span>
* <span data-ttu-id="2ffed-117">共有エクスペリエンスで複数のユーザーを接続する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="2ffed-117">Learn how to connect multiple users in a shared experience</span></span>
* <span data-ttu-id="2ffed-118">他のユーザーとオブジェクトの移動を共有する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="2ffed-118">Learn how to share the object movements with other users</span></span>
* <span data-ttu-id="2ffed-119">複数のデバイス間で空間的な位置合わせを実現する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="2ffed-119">Learn how to achieve spatial alignment between multiple devices</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ffed-120">前提条件</span><span class="sxs-lookup"><span data-stu-id="2ffed-120">Prerequisites</span></span>

* <span data-ttu-id="2ffed-121">適切な[ツールがインストールされている](install-the-tools.md)構成済みの Windows 10 コンピューター</span><span class="sxs-lookup"><span data-stu-id="2ffed-121">A Windows 10 computer configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="2ffed-122">Windows 10 SDK 10.0.18362.0 以降</span><span class="sxs-lookup"><span data-stu-id="2ffed-122">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="2ffed-123">[開発用に構成された](using-visual-studio.md#enabling-developer-mode) HoloLens 2 デバイス</span><span class="sxs-lookup"><span data-stu-id="2ffed-123">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="2ffed-124">Unity 2019.3.15 がインストールされ、ユニバーサル Windows プラットフォーム ビルド サポート モジュールが追加された <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a></span><span class="sxs-lookup"><span data-stu-id="2ffed-124"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the Universal Windows Platform Build Support module added</span></span>
* <span data-ttu-id="2ffed-125">「[Spatial Anchors リソースを作成する](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource)」セクション ([クイック スタート:Azure Spatial Anchors を使用する Unity HoloLens アプリを作成する](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) チュートリアルにあります) を完了します。</span><span class="sxs-lookup"><span data-stu-id="2ffed-125">Completed the [Create a Spatial Anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) section of the [Quickstart: Create a Unity HoloLens app that uses Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) tutorial</span></span>
* <span data-ttu-id="2ffed-126">[入門チュートリアル](mr-learning-base-01.md) シリーズを完了しているか、Unity および MRTK の基本操作に関する以前の経験</span><span class="sxs-lookup"><span data-stu-id="2ffed-126">Completed the [Getting started tutorials](mr-learning-base-01.md) series or some basic prior experience with Unity and MRTK</span></span>
* <span data-ttu-id="2ffed-127">[Azure Spatial Anchors のチュートリアル](mr-learning-asa-01.md) シリーズを完了しているか、Azure Spatial Anchors アカウントの作成に関する以前の経験</span><span class="sxs-lookup"><span data-stu-id="2ffed-127">Completed the [Azure Spatial Anchors tutorials](mr-learning-asa-01.md) series or prior experience creating an Azure Spatial Anchors Account</span></span>
* <span data-ttu-id="2ffed-128">HoloLens に加えて Android にもデプロイする場合</span><span class="sxs-lookup"><span data-stu-id="2ffed-128">If you intend to deploy to Android as well as HoloLens</span></span>
  * <span data-ttu-id="2ffed-129">Windows コンピューターか macOS コンピューターに USB 接続された、<a href="https://developer.android.com/studio/debug/dev-options" target="_blank">開発者向けオプションが有効</a>に設定された <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">ARCore 対応</a>の Android デバイス</span><span class="sxs-lookup"><span data-stu-id="2ffed-129">A <a href="https://developer.android.com/studio/debug/dev-options" target="_blank">developer enabled</a> and <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">ARCore capable</a> Android device with USB connection to your Windows or macOS computer</span></span>
  * <span data-ttu-id="2ffed-130">Unity 2019.3.15 がインストールされ、Android ビルド サポート モジュールが追加された <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a></span><span class="sxs-lookup"><span data-stu-id="2ffed-130"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the Android Build Support module added</span></span>
* <span data-ttu-id="2ffed-131">HoloLens に加えて iOS にもデプロイする場合</span><span class="sxs-lookup"><span data-stu-id="2ffed-131">If you intend to deploy to iOS as well as HoloLens</span></span>
  * <span data-ttu-id="2ffed-132"><a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> および <a href="https://cocoapods.org" target="_blank">CocoaPods</a> の最新バージョンがインストールされた macOS コンピューター</span><span class="sxs-lookup"><span data-stu-id="2ffed-132">A macOS computer with the latest version of <a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> and <a href="https://cocoapods.org" target="_blank">CocoaPods</a> installed</span></span>
  * <span data-ttu-id="2ffed-133">macOS コンピューターに USB 接続された、<a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">ARKit 互換</a> iOS デバイス</span><span class="sxs-lookup"><span data-stu-id="2ffed-133">An <a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">ARKit compatible</a> iOS device with USB connection to your macOS computer</span></span>
  * <span data-ttu-id="2ffed-134">Unity 2019.3.15 がインストールされ、iOS ビルド サポート モジュールが追加された <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a></span><span class="sxs-lookup"><span data-stu-id="2ffed-134"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the iOS Build Support module added</span></span>

> [!CAUTION]
> <span data-ttu-id="2ffed-135">このチュートリアル シリーズで推奨されている Mixed Reality Toolkit のバージョンは MRTK 2.4.0 です。</span><span class="sxs-lookup"><span data-stu-id="2ffed-135">The recommended Mixed Reality Toolkit version for this tutorial series is MRTK 2.4.0.</span></span>

> [!CAUTION]
> <span data-ttu-id="2ffed-136">このチュートリアル シリーズで推奨されている Unity バージョンは Unity 2019.3.15 です。</span><span class="sxs-lookup"><span data-stu-id="2ffed-136">The recommended Unity version for this tutorial series is Unity 2019.3.15.</span></span> <span data-ttu-id="2ffed-137">これは、上のリンクされた前提条件に記載されている Unity のバージョン要件に代わるものです。</span><span class="sxs-lookup"><span data-stu-id="2ffed-137">This supersedes any Unity version requirements stated in the prerequisites linked above.</span></span>

[<span data-ttu-id="2ffed-138">次のチュートリアル:2.Photon Unity ネットワークの設定</span><span class="sxs-lookup"><span data-stu-id="2ffed-138">Next Tutorial: 2. Setting up Photon Unity Networking</span></span>](mr-learning-sharing-02.md)
