---
title: HoloLens Research モード
description: HoloLens で Research モードを使用すると、アプリケーションは主要なデバイスセンサーストリーム (深さ、環境追跡、および赤外線反射) にアクセスできます。
author: hferrone
ms.author: v-haferr
ms.date: 07/31/2020
ms.topic: article
keywords: Research モード, cv, rs4, コンピュータービジョン, 研究, HoloLens, HoloLens 2
ms.openlocfilehash: dd49186d1218b6a6a6c9a8d5943159daad3bcefb
ms.sourcegitcommit: 36316e2658d3dfa804d798b9f4fb2f9186052144
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2020
ms.locfileid: "87507696"
---
# <a name="hololens-research-mode"></a><span data-ttu-id="2cd18-104">HoloLens Research モード</span><span class="sxs-lookup"><span data-stu-id="2cd18-104">HoloLens Research Mode</span></span>

<span data-ttu-id="2cd18-105">Research モードは、デバイス上の主要センサーへのアクセスを提供するために、1世代の HoloLens で導入されました。特に、展開を意図していない研究アプリケーションを対象としています。</span><span class="sxs-lookup"><span data-stu-id="2cd18-105">Research Mode was introduced in the 1st Generation HoloLens to give access to key sensors on the device, specifically for research applications that are not intended for deployment.</span></span>  <span data-ttu-id="2cd18-106">HoloLens 2 の研究モードでは、HoloLens 1 の機能を保持し、追加のストリームへのアクセスを追加します。</span><span class="sxs-lookup"><span data-stu-id="2cd18-106">Research Mode for HoloLens 2 retains the capabilities of HoloLens 1, adding access to additional streams:</span></span>

* <span data-ttu-id="2cd18-107">**可視性の低い環境の追跡カメラ**-ヘッドの追跡とマップの作成にシステムが使用するグレースケールのカメラです。</span><span class="sxs-lookup"><span data-stu-id="2cd18-107">**Visible Light Environment Tracking Cameras** - Gray-scale cameras used by the system for head tracking and map building.</span></span>
* <span data-ttu-id="2cd18-108">**深度カメラ**–2つのモードで動作します。</span><span class="sxs-lookup"><span data-stu-id="2cd18-108">**Depth Camera** – Operates in two modes:</span></span>  
    + <span data-ttu-id="2cd18-109">セルフトラッキングに使用される AHAT、高頻度 (45 FPS) のほぼ深い検出。</span><span class="sxs-lookup"><span data-stu-id="2cd18-109">AHAT, high-frequency (45 FPS) near-depth sensing used for hand tracking.</span></span> <span data-ttu-id="2cd18-110">1番目のバージョンの短いスローモードとは異なる方法で、AHAT は、1メートルを超えるフェーズラップに擬似的な深さを与えます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-110">Differently from the 1st version short-throw mode, AHAT gives pseudo-depth with phase wrap beyond 1 meter.</span></span> 
    + <span data-ttu-id="2cd18-111">Long throw、低頻度 (1-5 FPS)、[空間マッピング](spatial-mapping.md)で使用される深い深さの検出</span><span class="sxs-lookup"><span data-stu-id="2cd18-111">Long-throw, low-frequency (1-5 FPS) far-depth sensing used by [Spatial Mapping](spatial-mapping.md)</span></span>

* <span data-ttu-id="2cd18-112">**IR 反射率ストリームの2つのバージョン**。 HoloLens が計算に使用します。</span><span class="sxs-lookup"><span data-stu-id="2cd18-112">**Two versions of the IR-reflectivity stream** - Used by the HoloLens to compute depth.</span></span> <span data-ttu-id="2cd18-113">これらのイメージは赤外線によって照らされ、アンビエントに見える光の影響を受けません。</span><span class="sxs-lookup"><span data-stu-id="2cd18-113">These images are illuminated by infrared and unaffected by ambient visible light.</span></span>

<span data-ttu-id="2cd18-114">HoloLens 2 を使用している場合は、以下の追加入力にもアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-114">If you're using a HoloLens 2 you also have access to the additional inputs below:</span></span>

* <span data-ttu-id="2cd18-115">**加速度計**–システムによって使用され、X 軸、Y 軸、Z 軸、重力に沿った線形加速度を決定します。</span><span class="sxs-lookup"><span data-stu-id="2cd18-115">**Accelerometer** – Used by the system to determine linear acceleration along the X, Y and Z axes and gravity.</span></span>
* <span data-ttu-id="2cd18-116">**ジャイロ**–回転を決定するためにシステムによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-116">**Gyro** – Used by the system to determine rotations.</span></span>
* <span data-ttu-id="2cd18-117">**磁力計**–絶対方向を推定するためにシステムによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-117">**Magnetometer** – Used by the system to estimate absolute orientation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cd18-118">リサーチモードは現在パブリックプレビュー段階です。</span><span class="sxs-lookup"><span data-stu-id="2cd18-118">Research Mode is currently in Public Preview.</span></span> <span data-ttu-id="2cd18-119">HoloLens 2 のサンプル、チュートリアル、完全な API ドキュメントは、Research モードの Git リポジトリの[Eccv 2020](https://eccv2020.eu/
 )で入手できます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-119">HoloLens 2 samples, tutorials, and full API documentation will be available at [ECCV 2020](https://eccv2020.eu/
 ) in the Research Mode Git repository.</span></span>

<span data-ttu-id="2cd18-120">![Research モードアプリのスクリーンショット](images/sensor-stream-viewer.jpg)</span><span class="sxs-lookup"><span data-stu-id="2cd18-120">![Research Mode app screenshot](images/sensor-stream-viewer.jpg)</span></span><br>
<span data-ttu-id="2cd18-121">*リサーチモードで使用可能な8個のセンサーストリームを表示するテストアプリケーションの mixed reality キャプチャ*</span><span class="sxs-lookup"><span data-stu-id="2cd18-121">*A mixed reality capture of a test application that displays the eight sensor streams available in Research Mode*</span></span>

## <a name="usage"></a><span data-ttu-id="2cd18-122">使用</span><span class="sxs-lookup"><span data-stu-id="2cd18-122">Usage</span></span>

<span data-ttu-id="2cd18-123">研究モードは、Computer Vision およびロボットのフィールドの新しいアイデアを調査する教育機関および産業用の研究者向けに設計されています。</span><span class="sxs-lookup"><span data-stu-id="2cd18-123">Research Mode is designed for academic and industrial researchers exploring new ideas in the fields of Computer Vision and Robotics.</span></span>  <span data-ttu-id="2cd18-124">これは、エンタープライズ環境に配置されているアプリケーションや、Microsoft Store またはその他の配布チャネルを通じて利用できるアプリケーションを対象としていません。</span><span class="sxs-lookup"><span data-stu-id="2cd18-124">It's not intended for applications deployed in enterprise environments or available through the Microsoft Store or other distribution channels.</span></span>

<span data-ttu-id="2cd18-125">さらに、Microsoft は、今後のハードウェアまたは OS の更新で、リサーチモードまたは同等の機能がサポートされることを保証しません。</span><span class="sxs-lookup"><span data-stu-id="2cd18-125">Additionally, Microsoft doesn't provide assurances that Research Mode or equivalent functionality is going to be supported in future hardware or OS updates.</span></span> <span data-ttu-id="2cd18-126">ただし、これによって、新しいアイデアの開発とテストには使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="2cd18-126">However, this shouldn't stop you from using it to develop and test new ideas!</span></span>

## <a name="security-and-performance"></a><span data-ttu-id="2cd18-127">セキュリティとパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="2cd18-127">Security and performance</span></span>

<span data-ttu-id="2cd18-128">リサーチモードを有効にすると、通常の状況下で HoloLens 2 を使用する場合よりも多くのバッテリ電源が使用されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2cd18-128">Be aware that enabling Research Mode uses more battery power than using the HoloLens 2 under normal conditions.</span></span> <span data-ttu-id="2cd18-129">これは、リサーチモード機能を使用しているアプリケーションが実行されていない場合でも当てはまります。</span><span class="sxs-lookup"><span data-stu-id="2cd18-129">This is true even if the application using the Research Mode features is not running.</span></span>  <span data-ttu-id="2cd18-130">このモードを有効にすると、アプリケーションがセンサーデータを誤用する可能性があるため、デバイスの全体的なセキュリティを低下させることもできます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-130">Enabling this mode can also lower the overall security of your device because applications may misuse sensor data.</span></span>  <span data-ttu-id="2cd18-131">デバイスのセキュリティの詳細については、「 [HoloLens のセキュリティ](https://docs.microsoft.com/hololens/hololens-faq-security)に関する FAQ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2cd18-131">You can find more information on device security in the [HoloLens security FAQ](https://docs.microsoft.com/hololens/hololens-faq-security).</span></span>  

## <a name="device-support"></a><span data-ttu-id="2cd18-132">デバイス サポート</span><span class="sxs-lookup"><span data-stu-id="2cd18-132">Device support</span></span>
<table><span data-ttu-id="2cd18-133">
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" /> </colgroup>
    </span><span class="sxs-lookup"><span data-stu-id="2cd18-133">
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" /> </colgroup>
    </span></span><tr>
        <td><span data-ttu-id="2cd18-134"><strong>機能</strong></span><span class="sxs-lookup"><span data-stu-id="2cd18-134"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="2cd18-135"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens (第 1 世代)</strong></a></span><span class="sxs-lookup"><span data-stu-id="2cd18-135"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens 1st Gen</strong></a></span></span></td>
        <td><span data-ttu-id="2cd18-136"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="2cd18-136"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="2cd18-137">ヘッドトラッキングカメラ</span><span class="sxs-lookup"><span data-stu-id="2cd18-137">Head Tracking Cameras</span></span></td>
        <td><span data-ttu-id="2cd18-138">✔️</span><span class="sxs-lookup"><span data-stu-id="2cd18-138">✔️</span></span></td>
        <td><span data-ttu-id="2cd18-139">✔️</span><span class="sxs-lookup"><span data-stu-id="2cd18-139">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2cd18-140">IR カメラ & 深度</span><span class="sxs-lookup"><span data-stu-id="2cd18-140">Depth & IR Camera</span></span></td>
        <td><span data-ttu-id="2cd18-141">✔️</span><span class="sxs-lookup"><span data-stu-id="2cd18-141">✔️</span></span></td>
        <td><span data-ttu-id="2cd18-142">✔️</span><span class="sxs-lookup"><span data-stu-id="2cd18-142">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2cd18-143">加速度計</span><span class="sxs-lookup"><span data-stu-id="2cd18-143">Accelerometer</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="2cd18-144">✔️</span><span class="sxs-lookup"><span data-stu-id="2cd18-144">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2cd18-145">ジャイロスコープ</span><span class="sxs-lookup"><span data-stu-id="2cd18-145">Gyroscope</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="2cd18-146">✔️</span><span class="sxs-lookup"><span data-stu-id="2cd18-146">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2cd18-147">磁力計</span><span class="sxs-lookup"><span data-stu-id="2cd18-147">Magnetometer</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="2cd18-148">✔️</span><span class="sxs-lookup"><span data-stu-id="2cd18-148">✔️</span></span></td>
    </tr>
</table>

## <a name="enabling-research-mode-hololens-1st-gen-and-hololens-2"></a><span data-ttu-id="2cd18-149">リサーチモードの有効化 (HoloLens ファースト世代および HoloLens 2)</span><span class="sxs-lookup"><span data-stu-id="2cd18-149">Enabling Research Mode (HoloLens 1st Gen and HoloLens 2)</span></span>

<span data-ttu-id="2cd18-150">リサーチモードは、開発者モードの拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="2cd18-150">Research Mode is an extension of Developer Mode.</span></span> <span data-ttu-id="2cd18-151">開始する前に、デバイスの開発機能を有効にして、リサーチモードの設定にアクセスできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cd18-151">Before starting, the developer features of the device need to be enabled to access the Research Mode settings:</span></span> 

* <span data-ttu-id="2cd18-152">[**スタート] メニューを開き > 設定**を開き、[**更新プログラム**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cd18-152">Open **Start Menu > Settings** and select **Updates**.</span></span>
* <span data-ttu-id="2cd18-153">**開発者向けに**選択し、**開発者モード**を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2cd18-153">Select **For Developers** and enable **Developer Mode**.</span></span>
* <span data-ttu-id="2cd18-154">下へスクロールし、**デバイス ポータル**を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2cd18-154">Scroll down and enable **Device Portal**.</span></span>

<span data-ttu-id="2cd18-155">開発者向け機能が有効になったら、[デバイスポータルに接続](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens)して、リサーチモードの機能を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2cd18-155">After the developer features  are enabled, [connect to the device portal](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens) to enable the Research Mode features:</span></span>

* <span data-ttu-id="2cd18-156">**デバイスポータル**で、**システム > リサーチモード**に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-156">Go to **System > Research Mode** in the **Device Portal**.</span></span>
* <span data-ttu-id="2cd18-157">[**センサーストリームへのアクセスを許可する**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2cd18-157">Select **Allow access to sensor stream**.</span></span>
* <span data-ttu-id="2cd18-158">ページの上部にある**電源**メニュー項目からデバイスを再起動します。</span><span class="sxs-lookup"><span data-stu-id="2cd18-158">Restart the device from the **Power** menu item at the top of the page.</span></span>

<span data-ttu-id="2cd18-159">デバイスを再起動すると、**デバイスポータル**から読み込まれたアプリケーションは、リサーチモードのストリームにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="2cd18-159">Once you've restarted the device, the applications loaded through the **Device Portal** can access Research Mode streams.</span></span>

<span data-ttu-id="2cd18-160">![HoloLens デバイスポータルの [リサーチモード] タブ](images/ResearchModeDevPortal.png)</span><span class="sxs-lookup"><span data-stu-id="2cd18-160">![Research Mode tab of HoloLens Device Portal](images/ResearchModeDevPortal.png)</span></span><br>
<span data-ttu-id="2cd18-161">*HoloLens デバイスポータルの [リサーチモード] ウィンドウ*</span><span class="sxs-lookup"><span data-stu-id="2cd18-161">*Research Mode window in the HoloLens Device Portal*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cd18-162">HoloLens 2 の研究モードは、ビルド19041.1356 以降で使用できます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-162">Research Mode for HoloLens 2 is available beginning with build 19041.1356.</span></span> <span data-ttu-id="2cd18-163">以前のビルドでアクセスする必要がある場合は、 [Insider Preview](https://docs.microsoft.com/hololens/hololens-insider)プログラムにサインアップしてください。</span><span class="sxs-lookup"><span data-stu-id="2cd18-163">If you need access in an earlier build, sign up for our [Insider Preview](https://docs.microsoft.com/hololens/hololens-insider) program.</span></span>

### <a name="using-sensor-data-in-your-apps"></a><span data-ttu-id="2cd18-164">アプリでセンサーデータを使用する</span><span class="sxs-lookup"><span data-stu-id="2cd18-164">Using sensor data in your apps</span></span>

<span data-ttu-id="2cd18-165">アプリケーションは、[メディアファンデーション](https://msdn.microsoft.com/library/windows/desktop/ms694197)を使用して写真とビデオのカメラストリームにアクセスするのと同じ方法でセンサーストリームデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-165">Applications can access the sensor stream data in the same way that photo and video camera streams are accessed through [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197).</span></span> 

<span data-ttu-id="2cd18-166">HoloLens 開発に使用できるすべての Api は、リサーチモードでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-166">All APIs that work for HoloLens development are also available in Research Mode.</span></span> <span data-ttu-id="2cd18-167">具体的には、アプリケーションは、各センサーフレームのキャプチャ時間で HoloLens が6つの領域にあることを正確に把握しています。</span><span class="sxs-lookup"><span data-stu-id="2cd18-167">In particular, the application  knows precisely where HoloLens is in 6DoF space at each sensor frame capture time.</span></span>

<span data-ttu-id="2cd18-168">さまざまなリサーチモードのストリームにアクセスする方法、[組み込みと extrを](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world)使用する方法、 [HoloLensForCV GitHub リポジトリ](https://github.com/Microsoft/HoloLensForCV)リポジトリにストリームを記録する方法に関するサンプルアプリケーションを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="2cd18-168">You can find sample applications on how to access the various Research Mode streams, how to use the [intrinsics and extrinsics](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world), and how to record streams in the [HoloLensForCV GitHub repo](https://github.com/Microsoft/HoloLensForCV) repo.</span></span>

 > [!NOTE]
 > <span data-ttu-id="2cd18-169">現時点では、HoloLensForCV サンプルは HoloLens 2 では機能しません。</span><span class="sxs-lookup"><span data-stu-id="2cd18-169">At this time, the HoloLensForCV sample doesn't work on HoloLens 2.</span></span>

## <a name="support"></a><span data-ttu-id="2cd18-170">サポート</span><span class="sxs-lookup"><span data-stu-id="2cd18-170">Support</span></span>

<span data-ttu-id="2cd18-171">HoloLensForCV リポジトリの[問題トラッカー](https://github.com/Microsoft/HololensForCV/issues)を使用して、フィードバックを投稿し、既知の問題を追跡してください。</span><span class="sxs-lookup"><span data-stu-id="2cd18-171">Please use the [issue tracker](https://github.com/Microsoft/HololensForCV/issues) in the HoloLensForCV repository to post feedback and track known issues.</span></span>

## <a name="see-also"></a><span data-ttu-id="2cd18-172">こちらもご覧ください</span><span class="sxs-lookup"><span data-stu-id="2cd18-172">See also</span></span>

* [<span data-ttu-id="2cd18-173">Microsoft メディア ファンデーション</span><span class="sxs-lookup"><span data-stu-id="2cd18-173">Microsoft Media Foundation</span></span>](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [<span data-ttu-id="2cd18-174">HoloLensForCV GitHub リポジトリ</span><span class="sxs-lookup"><span data-stu-id="2cd18-174">HoloLensForCV GitHub repo</span></span>](https://github.com/Microsoft/HoloLensForCV)
* [<span data-ttu-id="2cd18-175">Windows Device Portal を使用する</span><span class="sxs-lookup"><span data-stu-id="2cd18-175">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
