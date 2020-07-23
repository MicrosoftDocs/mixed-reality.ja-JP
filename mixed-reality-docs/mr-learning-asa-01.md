---
title: Azure Spatial Anchors チュートリアル - 1. はじめに
description: このコースを完了すると Mixed Reality アプリケーション内に Azure Spatial Anchors を実装する方法を学習できます。
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: 6a015b4c9f6a5c1a92697ef9909443234a98ab09
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86304999"
---
# <a name="1-introduction"></a><span data-ttu-id="02fb0-105">1.はじめに</span><span class="sxs-lookup"><span data-stu-id="02fb0-105">1. Introduction</span></span>

## <a name="overview"></a><span data-ttu-id="02fb0-106">概要</span><span class="sxs-lookup"><span data-stu-id="02fb0-106">Overview</span></span>

<span data-ttu-id="02fb0-107">Azure Spatial Anchors チュートリアルにようこそ。</span><span class="sxs-lookup"><span data-stu-id="02fb0-107">Welcome to the Azure Spatial Anchors tutorials!</span></span> <span data-ttu-id="02fb0-108">このチュートリアル シリーズをとおして、<a href="https://azure.microsoft.com/services/spatial-anchors" target="_blank">Azure Spatial Anchors</a> (ASA) の基礎と完全な複合現実体験を現実の世界で実現する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="02fb0-108">Through this tutorial series, you will learn the fundamentals of <a href="https://azure.microsoft.com/services/spatial-anchors" target="_blank">Azure Spatial Anchors</a> (ASA) and how to anchor a complete mixed reality experience in the real world.</span></span> <span data-ttu-id="02fb0-109">プロジェクトを Android と iOS にデプロイする方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="02fb0-109">You will also learn how to deploy your project to Android and iOS.</span></span>

<span data-ttu-id="02fb0-110">このシリーズのチュートリアル:</span><span class="sxs-lookup"><span data-stu-id="02fb0-110">Tutorials in this series:</span></span>

1. [<span data-ttu-id="02fb0-111">はじめに</span><span class="sxs-lookup"><span data-stu-id="02fb0-111">Introduction</span></span>](mr-learning-asa-01.md)
2. [<span data-ttu-id="02fb0-112">Azure Spatial Anchors をお使いになる前に</span><span class="sxs-lookup"><span data-stu-id="02fb0-112">Getting started with Azure Spatial Anchors</span></span>](mr-learning-asa-02.md)
3. [<span data-ttu-id="02fb0-113">Azure Spatial Anchors の保存、取得、共有</span><span class="sxs-lookup"><span data-stu-id="02fb0-113">Saving, retrieving, and sharing Azure Spatial Anchors</span></span>](mr-learning-asa-03.md)
4. [<span data-ttu-id="02fb0-114">Azure Spatial Anchors のフィードバックの表示</span><span class="sxs-lookup"><span data-stu-id="02fb0-114">Displaying Azure Spatial Anchor feedback</span></span>](mr-learning-asa-04.md)
5. [<span data-ttu-id="02fb0-115">Android と iOS 用の Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="02fb0-115">Azure Spatial Anchors for Android and iOS</span></span>](mr-learning-asa-05.md)

## <a name="objectives"></a><span data-ttu-id="02fb0-116">目標</span><span class="sxs-lookup"><span data-stu-id="02fb0-116">Objectives</span></span>

* <span data-ttu-id="02fb0-117">空間アンカーを作成し、Azure から取得する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="02fb0-117">Learn how to create spatial anchors and fetch them from Azure</span></span>
* <span data-ttu-id="02fb0-118">アプリ セッション間で空間的な位置合わせを実現する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="02fb0-118">Learn how to achieve spatial alignment across app sessions</span></span>
* <span data-ttu-id="02fb0-119">複数のデバイス間で空間的な位置合わせを実現する方法を学習する</span><span class="sxs-lookup"><span data-stu-id="02fb0-119">Learn how to achieve spatial alignment between multiple devices</span></span>
* <span data-ttu-id="02fb0-120">プロジェクトを準備し、構築し、Android と iOS にデプロイする方法を学習する</span><span class="sxs-lookup"><span data-stu-id="02fb0-120">Learn how to prepare, build, and deploy your project to Android and iOS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02fb0-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="02fb0-121">Prerequisites</span></span>

* <span data-ttu-id="02fb0-122">正しい[ツールがインストールされている](install-the-tools.md)構成済みの Windows 10 コンピューター</span><span class="sxs-lookup"><span data-stu-id="02fb0-122">A Windows 10 computer configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="02fb0-123">Windows 10 SDK 10.0.18362.0 以降のバージョン</span><span class="sxs-lookup"><span data-stu-id="02fb0-123">Windows 10 SDK 10.0.18362.0 or later version</span></span>
* <span data-ttu-id="02fb0-124">[開発用に構成された](using-visual-studio.md#enabling-developer-mode) HoloLens 2 デバイス</span><span class="sxs-lookup"><span data-stu-id="02fb0-124">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="02fb0-125">Unity 2019.3.15 がインストールされ、ユニバーサル Windows プラットフォーム ビルド サポート モジュールが追加された <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a></span><span class="sxs-lookup"><span data-stu-id="02fb0-125"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the Universal Windows Platform Build Support module added</span></span>
* <span data-ttu-id="02fb0-126">「[Spatial Anchors リソースを作成する](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource)」セクション ([クイック スタート:Azure Spatial Anchors を使用する Unity HoloLens アプリを作成する](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) チュートリアルにあります) を完了します。</span><span class="sxs-lookup"><span data-stu-id="02fb0-126">Completed the [Create a Spatial Anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) section of the [Quickstart: Create a Unity HoloLens app that uses Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) tutorial</span></span>
* <span data-ttu-id="02fb0-127">[入門チュートリアル](mr-learning-base-01.md) シリーズを完了しているか、以前に Unity と MRTK の基本操作を経験していること</span><span class="sxs-lookup"><span data-stu-id="02fb0-127">Finished the [Getting started tutorials](mr-learning-base-01.md) series or some basic prior experience with Unity and MRTK</span></span>
* <span data-ttu-id="02fb0-128">[Azure Spatial Anchors のチュートリアル](mr-learning-asa-01.md) シリーズを完了しているか、以前に Azure Spatial Anchors アカウントの作成を経験していること</span><span class="sxs-lookup"><span data-stu-id="02fb0-128">Completed the [Azure Spatial Anchors tutorials](mr-learning-asa-01.md) series or previous experience creating an Azure Spatial Anchors Account</span></span>
* <span data-ttu-id="02fb0-129">HoloLens に加えて Android にもデプロイする場合</span><span class="sxs-lookup"><span data-stu-id="02fb0-129">If you intend to deploy to Android as well as HoloLens</span></span>
  * <span data-ttu-id="02fb0-130">Windows コンピューターか macOS コンピューターに USB 接続された、<a href="https://developer.android.com/studio/debug/dev-options" target="_blank">開発者向けオプションが有効</a>に設定された <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">ARCore 対応</a>の Android デバイス</span><span class="sxs-lookup"><span data-stu-id="02fb0-130">A <a href="https://developer.android.com/studio/debug/dev-options" target="_blank">developer enabled</a> and <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">ARCore capable</a> Android device with USB connection to your Windows or macOS computer</span></span>
  * <span data-ttu-id="02fb0-131">Unity 2019.3.15 がインストールされ、Android ビルド サポート モジュールが追加された <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a></span><span class="sxs-lookup"><span data-stu-id="02fb0-131"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the Android Build Support module added</span></span>
* <span data-ttu-id="02fb0-132">HoloLens に加えて iOS にもデプロイする場合</span><span class="sxs-lookup"><span data-stu-id="02fb0-132">If you intend to deploy to iOS as well as HoloLens</span></span>
  * <span data-ttu-id="02fb0-133"><a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> および <a href="https://cocoapods.org" target="_blank">CocoaPods</a> の最新バージョンがインストールされた macOS コンピューター</span><span class="sxs-lookup"><span data-stu-id="02fb0-133">A macOS computer with the latest version of <a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> and <a href="https://cocoapods.org" target="_blank">CocoaPods</a> installed</span></span>
  * <span data-ttu-id="02fb0-134">macOS コンピューターに USB 接続された、<a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">ARKit 互換</a> iOS デバイス</span><span class="sxs-lookup"><span data-stu-id="02fb0-134">An <a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">ARKit compatible</a> iOS device with USB connection to your macOS computer</span></span>
  * <span data-ttu-id="02fb0-135">2019.3.15 がインストールされ、iOS ビルド サポート モジュールが追加された <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a></span><span class="sxs-lookup"><span data-stu-id="02fb0-135"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the iOS Build Support module added</span></span>

> [!CAUTION]
> <span data-ttu-id="02fb0-136">このチュートリアル シリーズで推奨されている Mixed Reality Toolkit のバージョンは MRTK 2.4.0 です。</span><span class="sxs-lookup"><span data-stu-id="02fb0-136">The recommended Mixed Reality Toolkit version for this tutorial series is MRTK 2.4.0.</span></span>

> [!CAUTION]
> <span data-ttu-id="02fb0-137">このチュートリアル シリーズで推奨されている Unity バージョンは Unity 2019.3.15 です。</span><span class="sxs-lookup"><span data-stu-id="02fb0-137">The recommended Unity version for this tutorial series is Unity 2019.3.15.</span></span> <span data-ttu-id="02fb0-138">これは、上のリンクされた前提条件に記載されている Unity のバージョン要件に代わるものです。</span><span class="sxs-lookup"><span data-stu-id="02fb0-138">This supersedes any Unity version requirements stated in the prerequisites linked above.</span></span>

[<span data-ttu-id="02fb0-139">次のチュートリアル:2.Azure Spatial Anchors をお使いになる前に</span><span class="sxs-lookup"><span data-stu-id="02fb0-139">Next Tutorial: 2. Getting started with Azure Spatial Anchors</span></span>](mr-learning-asa-02.md)
