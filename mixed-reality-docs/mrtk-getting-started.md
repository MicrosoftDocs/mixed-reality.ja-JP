---
title: MRTK バージョン 2 の概要
description: MRTK の活用に関心がある開発初心者向け
author: cre8ivepark
ms.author: dongpark
ms.date: 05/15/2019
ms.topic: article
ms.localizationpriority: high
keywords: Windows Mixed Reality, テスト, Mixed Reality Toolkit, MRTK バージョン2, MRTK, ツール, SDK, HoloLens, HoloLens 2
ms.openlocfilehash: 64f5925154a2987cd04293fd4c04bbd9f48bacbf
ms.sourcegitcommit: ef0bf03833eda826ed0b884859b4573775112aba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87477014"
---
# <a name="getting-started-with-mrtk-for-unity"></a><span data-ttu-id="47fec-104">Unity 用の MRTK の概要</span><span class="sxs-lookup"><span data-stu-id="47fec-104">Getting started with MRTK for Unity</span></span>
![MRTK](images/UX/MRTK_UX_Hero.png)

## <a name="what-is-mixed-reality-toolkit-mrtk"></a><span data-ttu-id="47fec-106">Mixed Reality Toolkit (MRTK) とは</span><span class="sxs-lookup"><span data-stu-id="47fec-106">What is Mixed Reality Toolkit (MRTK)?</span></span>
<span data-ttu-id="47fec-107">MRTK は、HoloLens が最初にリリースされて以来培われてきたすばらしいオープン ソースのツールキットであり、貢献してくれた開発者コミュニティの努力によって、現在の姿があります。</span><span class="sxs-lookup"><span data-stu-id="47fec-107">The MRTK is an amazing open source toolkit that has been around since the HoloLens was first released, and would not be where it is today without the hard work of our developer community who have contributed to it.</span></span> <span data-ttu-id="47fec-108">過去 3 年間で、Microsoft では開発者コミュニティのフィードバックを受け、最も重要な懸念事項に対応するために MRTK v2 を構築しました。</span><span class="sxs-lookup"><span data-stu-id="47fec-108">Over the past 3 years, we have listened to the feedback of our developer community, and built MRTK v2 to take the biggest concerns into account.</span></span>  

<span data-ttu-id="47fec-109">Unity 用の MRTK は、Mixed Reality アプリケーション向けのオープンソースのクロスプラットフォーム開発キットです。</span><span class="sxs-lookup"><span data-stu-id="47fec-109">MRTK for Unity is an open-source, cross-platform development kit for mixed reality applications.</span></span> <span data-ttu-id="47fec-110">MRTK には、空間でのインタラクションのための、クロスプラットフォームの入力システム、基本コンポーネント、共通の構成要素が備わっています。</span><span class="sxs-lookup"><span data-stu-id="47fec-110">MRTK provides a cross-platform input system, foundational components, and common building blocks for spatial interactions.</span></span> <span data-ttu-id="47fec-111">MRTK バージョン 2 は、Microsoft HoloLens、Windows Mixed Reality イマーシブ (VR) ヘッドセット、OpenVR プラットフォームをターゲットとしたアプリケーションの開発を加速させることを目的としています。</span><span class="sxs-lookup"><span data-stu-id="47fec-111">MRTK version 2 is intended to accelerate the development of applications targeting Microsoft HoloLens, Windows Mixed Reality immersive (VR) headsets and OpenVR platform.</span></span> <span data-ttu-id="47fec-112">このプロジェクトは、参入障壁を減らすこと、Mixed Reality アプリケーションを作成すること、全体の成長に応じてコミュニティに貢献することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="47fec-112">The project is aimed at reducing barriers to entry, creating mixed reality applications, and contributing back to the community as we all grow.</span></span>

<br>

>[!VIDEO https://channel9.msdn.com/Shows/Docs-Mixed-Reality/Setting-up-your-HoloLens-2-development-environment/player?format=ny]

<span data-ttu-id="47fec-113">詳細については、[GitHub にある MRTK のドキュメント](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="47fec-113">See the [MRTK's documentation on GitHub](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html) to explore more.</span></span>

## <a name="new-with-mrtk-v2"></a><span data-ttu-id="47fec-114">MRTK v2 の新機能</span><span class="sxs-lookup"><span data-stu-id="47fec-114">New with MRTK v2</span></span>
<span data-ttu-id="47fec-115">これらのプラットフォーム ツールに込めた Microsoft の成果に注目して欲しいと考えています。</span><span class="sxs-lookup"><span data-stu-id="47fec-115">We want to stress our commitment to these platform tools.</span></span>  <span data-ttu-id="47fec-116">事実、Microsoft では MRTK バージョン 2 を活かして、セットアップ エクスペリエンス (OOBE) などのすぐに使えるエクスペリエンスや Mixed Reality Learning アプリケーションを開発しました。</span><span class="sxs-lookup"><span data-stu-id="47fec-116">In fact, we leveraged MRTK version 2 to develop our inbox experiences, such as the setup experience (OOBE) and our Mixed Reality Learning application.</span></span>  <span data-ttu-id="47fec-117">また、新しい HoloLens 2 機能は、まずは MRTK 経由で公開されることを期待していただいてかまいません。Microsoft では、お客様が当社のプラットフォーム上で開発を行ううえで、それが最適な方法であると確信しているからです。</span><span class="sxs-lookup"><span data-stu-id="47fec-117">You can also expect to see new HoloLens 2 capabilities first exposed through MRTK because we believe it’s the best way to develop on our platform.</span></span> 

### <a name="modular"></a><span data-ttu-id="47fec-118">モジュール式</span><span class="sxs-lookup"><span data-stu-id="47fec-118">Modular</span></span>
<span data-ttu-id="47fec-119">モジュール式の手法でビルドされているため、ツールキットのすべての機能をプロジェクトに組み込む必要はありません。</span><span class="sxs-lookup"><span data-stu-id="47fec-119">We have built it in a modular way, so there's no need to take every bit of the toolkit into your project.</span></span>  <span data-ttu-id="47fec-120">実際に、これにはいくつかの利点があります。</span><span class="sxs-lookup"><span data-stu-id="47fec-120">There are actually a few benefits to this.</span></span>  <span data-ttu-id="47fec-121">プロジェクトを小規模に保ち、管理を容易にすることができます。</span><span class="sxs-lookup"><span data-stu-id="47fec-121">It keeps your project size smaller, and makes it easier to manage.</span></span>  <span data-ttu-id="47fec-122">さらに、スクリプト作成が可能なオブジェクトによってビルドされており、インターフェイス駆動型であるため、組み込みのコンポーネントをお客様独自のものに置き換えて、他のサービス、システム、およびプラットフォームをサポートすることも可能です。</span><span class="sxs-lookup"><span data-stu-id="47fec-122">Additionally, because it’s built with scriptable objects and is interface-driven, it’s also possible for you to replace the components that are included with your own, to support other services, systems, and platforms.</span></span>

### <a name="cross-platform"></a><span data-ttu-id="47fec-123">クロスプラットフォーム</span><span class="sxs-lookup"><span data-stu-id="47fec-123">Cross-platform</span></span>
<span data-ttu-id="47fec-124">他のプラットフォームに関しては、クロスプラットフォームのサポートを備えています。</span><span class="sxs-lookup"><span data-stu-id="47fec-124">Speaking of other platforms, it has cross-platform support.</span></span>  <span data-ttu-id="47fec-125">また、このことによって、何もしなくてもすべての単一プラットフォームがサポートされるわけではありませんが、ビルド ターゲットを他のプラットフォームに切り替えたときに、どのツールキットのコードも中断されないことを保証しています。</span><span class="sxs-lookup"><span data-stu-id="47fec-125">And while this doesn’t mean every single platform is supported out of the box, we have made sure none of the toolkit code will break when you switch your build target to other platforms.</span></span>  <span data-ttu-id="47fec-126">モジュール式の設計による堅牢性と拡張性を備えることから、適切な手法を利用して、ARCore、ARKit、および OpenVR などの複数のプラットフォームをサポートできます。</span><span class="sxs-lookup"><span data-stu-id="47fec-126">The robustness and extensibility with the modular design sets you up on a good path to be able to support multiple platforms, such as ARCore, ARKit, and OpenVR.</span></span>

### <a name="performant"></a><span data-ttu-id="47fec-127">高いパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="47fec-127">Performant</span></span>
<span data-ttu-id="47fec-128">モバイル プラットフォームに対応し、パフォーマンスを考慮して構築されています。</span><span class="sxs-lookup"><span data-stu-id="47fec-128">Working with mobile platforms, we constructed it with performance in mind.</span></span>  <span data-ttu-id="47fec-129">このことは非常に重要であり、Microsoft ではツールがお客様の妨げにならないことを保証したいと考えました。</span><span class="sxs-lookup"><span data-stu-id="47fec-129">This is super important, and we wanted to ensure that the tools are not going to work against you.</span></span>

## <a name="see-also"></a><span data-ttu-id="47fec-130">関連項目</span><span class="sxs-lookup"><span data-stu-id="47fec-130">See also</span></span>
* [<span data-ttu-id="47fec-131">MRTK 入門ガイド</span><span class="sxs-lookup"><span data-stu-id="47fec-131">MRTK getting started guide</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [<span data-ttu-id="47fec-132">MRTK のドキュメント ホーム</span><span class="sxs-lookup"><span data-stu-id="47fec-132">MRTK documentation home</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [<span data-ttu-id="47fec-133">ツールのインストール</span><span class="sxs-lookup"><span data-stu-id="47fec-133">Install the tools</span></span>](install-the-tools.md)
* [<span data-ttu-id="47fec-134">HTK/MRTK から MRTK バージョン 2 への移植</span><span class="sxs-lookup"><span data-stu-id="47fec-134">Porting from HTK/MRTK to MRTK version 2</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html)
