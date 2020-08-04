---
title: 入門チュートリアル - 1. はじめに
description: このコースでは、Mixed Reality Toolkit (MRTK) を使用して複合現実のアプリケーションを作成する方法について説明します。
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: 330863d36abe051e8fe17b87ce913b1b110e2d3d
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376434"
---
# <a name="1-introduction"></a><span data-ttu-id="ea3f8-105">1.はじめに</span><span class="sxs-lookup"><span data-stu-id="ea3f8-105">1. Introduction</span></span>

## <a name="overview"></a><span data-ttu-id="ea3f8-106">概要</span><span class="sxs-lookup"><span data-stu-id="ea3f8-106">Overview</span></span>

<span data-ttu-id="ea3f8-107">入門チュートリアル シリーズへようこそ。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-107">Welcome to the Getting Started tutorial series!</span></span> <span data-ttu-id="ea3f8-108">これらのチュートリアルでは、Mixed Reality Toolkit (MRTK) と、それらの一部の機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-108">Over the course of these tutorials, you'll learn about the Mixed Reality Toolkit (MRTK) and some of the features it has to offer.</span></span> <span data-ttu-id="ea3f8-109">NASA の火星探査ローバーをモデルとするホログラムをユーザーが探ることができる、複合現実のエクスペリエンスも構築します。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-109">You'll also build a mixed reality experience where the user can explore a hologram modeled after NASA's Mars Curiosity Rover.</span></span> <span data-ttu-id="ea3f8-110">このシリーズの終わりには、MRTK について、およびこれでどのようにご自分の開発プロセスをスピード化できるかについて深く理解できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-110">By the end of this series, you'll have a firm grasp of MRTK and how it can speed up your development process.</span></span>

<span data-ttu-id="ea3f8-111">このシリーズのチュートリアルは連続してものであるため、正しい順序で進めてください。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-111">Tutorials in this series are meant to be sequential, so please go through them in the correct order:</span></span>

1. [<span data-ttu-id="ea3f8-112">はじめに</span><span class="sxs-lookup"><span data-stu-id="ea3f8-112">Introduction</span></span>](mr-learning-base-01.md)
2. [<span data-ttu-id="ea3f8-113">プロジェクトの初期化と最初のアプリケーションの配置</span><span class="sxs-lookup"><span data-stu-id="ea3f8-113">Initializing your project and deploying your first application</span></span>](mr-learning-base-02.md)
3. [<span data-ttu-id="ea3f8-114">MRTK プロファイルの構成</span><span class="sxs-lookup"><span data-stu-id="ea3f8-114">Configuring the MRTK profiles</span></span>](mr-learning-base-03.md)
4. [<span data-ttu-id="ea3f8-115">シーンへのオブジェクトの配置</span><span class="sxs-lookup"><span data-stu-id="ea3f8-115">Positioning objects in the scene</span></span>](mr-learning-base-04.md)
5. [<span data-ttu-id="ea3f8-116">ソルバーを使用した動的なコンテンツの作成</span><span class="sxs-lookup"><span data-stu-id="ea3f8-116">Creating dynamic content using Solvers</span></span>](mr-learning-base-05.md)
6. [<span data-ttu-id="ea3f8-117">ユーザー インターフェイスの作成</span><span class="sxs-lookup"><span data-stu-id="ea3f8-117">Creating user interfaces</span></span>](mr-learning-base-06.md)
7. [<span data-ttu-id="ea3f8-118">3D オブジェクトの操作</span><span class="sxs-lookup"><span data-stu-id="ea3f8-118">Interacting with 3D objects</span></span>](mr-learning-base-07.md)
8. [<span data-ttu-id="ea3f8-119">視線追跡の使用</span><span class="sxs-lookup"><span data-stu-id="ea3f8-119">Using eye-tracking</span></span>](mr-learning-base-08.md)
9. [<span data-ttu-id="ea3f8-120">音声コマンドの使用</span><span class="sxs-lookup"><span data-stu-id="ea3f8-120">Using voice commands</span></span>](mr-learning-base-09.md)

## <a name="objectives"></a><span data-ttu-id="ea3f8-121">目標</span><span class="sxs-lookup"><span data-stu-id="ea3f8-121">Objectives</span></span>

* <span data-ttu-id="ea3f8-122">MRTK 用に Unity を構成する方法について学ぶ</span><span class="sxs-lookup"><span data-stu-id="ea3f8-122">Learn how to configure Unity for MRTK</span></span>
* <span data-ttu-id="ea3f8-123">ご自分のデバイスの構築および展開方法について学習する</span><span class="sxs-lookup"><span data-stu-id="ea3f8-123">Learn how to build and deploy to your device</span></span>
* <span data-ttu-id="ea3f8-124">MRTK の一部の主要機能の使用方法について学習する</span><span class="sxs-lookup"><span data-stu-id="ea3f8-124">Learn how to use some of MRTK's key features</span></span>
* <span data-ttu-id="ea3f8-125">完全な複合現実エクスペリエンスを構築する</span><span class="sxs-lookup"><span data-stu-id="ea3f8-125">Create a complete mixed reality experience</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea3f8-126">前提条件</span><span class="sxs-lookup"><span data-stu-id="ea3f8-126">Prerequisites</span></span>

* <span data-ttu-id="ea3f8-127">正しい[ツールがインストールされている](install-the-tools.md)構成済みの Windows 10 PC</span><span class="sxs-lookup"><span data-stu-id="ea3f8-127">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="ea3f8-128">[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk/) 10.0.18362.0 以降</span><span class="sxs-lookup"><span data-stu-id="ea3f8-128">[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk/) 10.0.18362.0 or later</span></span>
* <span data-ttu-id="ea3f8-129">[開発用に構成された](using-visual-studio.md#enabling-developer-mode) HoloLens 2 デバイス</span><span class="sxs-lookup"><span data-stu-id="ea3f8-129">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="ea3f8-130">Unity 2019.3.15 がインストールされ、ユニバーサル Windows プラットフォーム ビルド サポート モジュールが追加された <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a></span><span class="sxs-lookup"><span data-stu-id="ea3f8-130"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the Universal Windows Platform Build Support module added</span></span>

> [!CAUTION]
> <span data-ttu-id="ea3f8-131">このチュートリアル シリーズで推奨される MRTK のバージョンは MRTK 2.4.0 です。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-131">The recommended MRTK version for this tutorial series is MRTK 2.4.0.</span></span>

> [!CAUTION]
> <span data-ttu-id="ea3f8-132">このチュートリアル シリーズで推奨される Unity バージョンは Unity 2019.3.15 です。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-132">The recommended Unity version for this tutorial series is Unity 2019.3.15.</span></span> <span data-ttu-id="ea3f8-133">これは、上の前提条件のリンクに記載されているすべての Unity のバージョンに優先されます。</span><span class="sxs-lookup"><span data-stu-id="ea3f8-133">This supersedes any Unity version requirements stated in the prerequisites linked above.</span></span>

[<span data-ttu-id="ea3f8-134">次のチュートリアル:2.プロジェクトの初期化と最初のアプリケーションの配置</span><span class="sxs-lookup"><span data-stu-id="ea3f8-134">Next Tutorial: 2. Initializing your project and deploying your first application</span></span>](mr-learning-base-02.md)
