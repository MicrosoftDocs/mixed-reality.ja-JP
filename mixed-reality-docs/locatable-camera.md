---
title: 場所を特定できるカメラ
description: HoloLens のフロント接続カメラに関する一般的な情報、そのしくみ、および開発者が使用できるプロファイルと解決方法について説明します。
author: cdedmonds
ms.author: wguyman
ms.date: 06/12/2019
ms.topic: article
keywords: カメラ、hololens、カラーカメラ、フロント接続、hololens 2、cv、コンピュータービジョン、基準、マーカー、qr コード、qr、写真、ビデオ
ms.openlocfilehash: b8e9d926db09d277b3fde7572dd68257599c8d5e
ms.sourcegitcommit: 09d9fa153cd9072f60e33a5f83ced8167496fcd7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/18/2020
ms.locfileid: "83520017"
---
# <a name="locatable-camera"></a><span data-ttu-id="f2c1a-104">場所を特定できるカメラ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-104">Locatable camera</span></span>

<span data-ttu-id="f2c1a-105">HoloLens には、デバイスの前面に取り付けられている世界中のカメラが搭載されています。これにより、アプリはユーザーに表示される内容を確認できます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-105">HoloLens includes a world-facing camera mounted on the front of the device, which enables apps to see what the user sees.</span></span> <span data-ttu-id="f2c1a-106">スマートフォン、ノートブック、またはデスクトップのカラーカメラの場合と同じように、開発者はカメラのアクセスと制御を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-106">Developers have access to and control of the camera, just as they would for color cameras on smartphones, portables, or desktops.</span></span> <span data-ttu-id="f2c1a-107">モバイルおよびデスクトップで動作する同じユニバーサル windows [media capture](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.aspx)および windows Media foundation Api が HoloLens で動作します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-107">The same universal windows [media capture](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.aspx) and windows media foundation APIs that work on mobile and desktop work on HoloLens.</span></span> <span data-ttu-id="f2c1a-108">Unity では、[これらの Windows api をラップ](locatable-camera-in-unity.md)して、HoloLens でのカメラの単純な使用を抽象化し、(ホログラムの有無にかかわらず) 通常の写真やビデオを撮影したり、カメラの位置をシーン上で検索したりするなどのタスクを実行しました。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-108">Unity [has also wrapped these windows APIs](locatable-camera-in-unity.md) to abstract simple usage of the camera on HoloLens for tasks such as taking regular photos and videos (with or without holograms) and locating the camera's position in and perspective on the scene.</span></span>

## <a name="device-camera-information"></a><span data-ttu-id="f2c1a-109">デバイスカメラ情報</span><span class="sxs-lookup"><span data-stu-id="f2c1a-109">Device camera information</span></span>

### <a name="hololens-first-generation"></a><span data-ttu-id="f2c1a-110">HoloLens (最初世代)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-110">HoloLens (first-generation)</span></span>

* <span data-ttu-id="f2c1a-111">自動白バランス、自動露出、およびフルイメージ処理パイプラインを使用して、フォーカスされたフォト/ビデオ (PV) カメラを修正します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-111">Fixed focus photo/video (PV) camera with auto white balance, auto exposure, and full image processing pipeline.</span></span>
* <span data-ttu-id="f2c1a-112">世界中のホワイトプライバシー LED は、カメラがアクティブになるたびに点灯します</span><span class="sxs-lookup"><span data-stu-id="f2c1a-112">White Privacy LED facing the world will illuminate whenever the camera is active</span></span>
* <span data-ttu-id="f2c1a-113">カメラは、30、24、20、15、および 5 fps で、次のモード (すべてのモードが16:9 の縦横比) をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-113">The camera supports the following modes (all modes are 16:9 aspect ratio) at 30, 24, 20, 15, and 5 fps:</span></span>

  |  <span data-ttu-id="f2c1a-114">ビデオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-114">Video</span></span>  |  <span data-ttu-id="f2c1a-115">プレビュー</span><span class="sxs-lookup"><span data-stu-id="f2c1a-115">Preview</span></span>  |  <span data-ttu-id="f2c1a-116">それでもなお</span><span class="sxs-lookup"><span data-stu-id="f2c1a-116">Still</span></span>  |  <span data-ttu-id="f2c1a-117">ビューの水平方向のフィールド (H 視界)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-117">Horizontal Field of View (H-FOV)</span></span> |  <span data-ttu-id="f2c1a-118">推奨される使用方法</span><span class="sxs-lookup"><span data-stu-id="f2c1a-118">Suggested usage</span></span> | 
  |----------|----------|----------|----------|----------|
  |  <span data-ttu-id="f2c1a-119">1280 x 720</span><span class="sxs-lookup"><span data-stu-id="f2c1a-119">1280x720</span></span> |  <span data-ttu-id="f2c1a-120">1280 x 720</span><span class="sxs-lookup"><span data-stu-id="f2c1a-120">1280x720</span></span> |  <span data-ttu-id="f2c1a-121">1280 x 720</span><span class="sxs-lookup"><span data-stu-id="f2c1a-121">1280x720</span></span> |  <span data-ttu-id="f2c1a-122">45度</span><span class="sxs-lookup"><span data-stu-id="f2c1a-122">45deg</span></span>  |  <span data-ttu-id="f2c1a-123">(ビデオ安定化を使用した既定のモード)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-123">(default mode with video stabilization)</span></span> | 
  |  <span data-ttu-id="f2c1a-124">該当なし</span><span class="sxs-lookup"><span data-stu-id="f2c1a-124">N/A</span></span> |  <span data-ttu-id="f2c1a-125">該当なし</span><span class="sxs-lookup"><span data-stu-id="f2c1a-125">N/A</span></span> |  <span data-ttu-id="f2c1a-126">2048x1152</span><span class="sxs-lookup"><span data-stu-id="f2c1a-126">2048x1152</span></span> |  <span data-ttu-id="f2c1a-127">67deg</span><span class="sxs-lookup"><span data-stu-id="f2c1a-127">67deg</span></span> |  <span data-ttu-id="f2c1a-128">高解像度の静止画像</span><span class="sxs-lookup"><span data-stu-id="f2c1a-128">Highest resolution still image</span></span> | 
  |  <span data-ttu-id="f2c1a-129">1408x792</span><span class="sxs-lookup"><span data-stu-id="f2c1a-129">1408x792</span></span> |  <span data-ttu-id="f2c1a-130">1408x792</span><span class="sxs-lookup"><span data-stu-id="f2c1a-130">1408x792</span></span> |  <span data-ttu-id="f2c1a-131">1408x792</span><span class="sxs-lookup"><span data-stu-id="f2c1a-131">1408x792</span></span> |  <span data-ttu-id="f2c1a-132">48度</span><span class="sxs-lookup"><span data-stu-id="f2c1a-132">48deg</span></span> |  <span data-ttu-id="f2c1a-133">ビデオ安定化前のオーバースキャン (埋め込み) 解像度</span><span class="sxs-lookup"><span data-stu-id="f2c1a-133">Overscan (padding) resolution before video stabilization</span></span> | 
  |  <span data-ttu-id="f2c1a-134">1344x756</span><span class="sxs-lookup"><span data-stu-id="f2c1a-134">1344x756</span></span> |  <span data-ttu-id="f2c1a-135">1344x756</span><span class="sxs-lookup"><span data-stu-id="f2c1a-135">1344x756</span></span> |  <span data-ttu-id="f2c1a-136">1344x756</span><span class="sxs-lookup"><span data-stu-id="f2c1a-136">1344x756</span></span> |  <span data-ttu-id="f2c1a-137">67deg</span><span class="sxs-lookup"><span data-stu-id="f2c1a-137">67deg</span></span> |  <span data-ttu-id="f2c1a-138">オーバースキャンによる大規模な視界のビデオモード</span><span class="sxs-lookup"><span data-stu-id="f2c1a-138">Large FOV video mode with overscan</span></span> | 
  |  <span data-ttu-id="f2c1a-139">896x504</span><span class="sxs-lookup"><span data-stu-id="f2c1a-139">896x504</span></span> |  <span data-ttu-id="f2c1a-140">896x504</span><span class="sxs-lookup"><span data-stu-id="f2c1a-140">896x504</span></span> |  <span data-ttu-id="f2c1a-141">896x504</span><span class="sxs-lookup"><span data-stu-id="f2c1a-141">896x504</span></span> |  <span data-ttu-id="f2c1a-142">48度</span><span class="sxs-lookup"><span data-stu-id="f2c1a-142">48deg</span></span> |  <span data-ttu-id="f2c1a-143">イメージ処理タスクの低電力/低解像度モード</span><span class="sxs-lookup"><span data-stu-id="f2c1a-143">Low power / Low resolution mode for image processing tasks</span></span> | 

### <a name="hololens-2"></a><span data-ttu-id="f2c1a-144">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f2c1a-144">HoloLens 2</span></span>

* <span data-ttu-id="f2c1a-145">自動ホワイトバランス、自動露出、およびフルイメージ処理パイプラインを使用して、写真/ビデオ (PV) カメラを自動フォーカスします。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-145">Auto-focus photo/video (PV) camera with auto white balance, auto exposure, and full image processing pipeline.</span></span>
* <span data-ttu-id="f2c1a-146">世界中のホワイトプライバシー LED は、カメラがアクティブになるたびに点灯します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-146">White Privacy LED facing the world will illuminate whenever the camera is active.</span></span>
* <span data-ttu-id="f2c1a-147">HoloLens 2 では、さまざまなカメラプロファイルがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-147">HoloLens 2 supports different camera profiles.</span></span> <span data-ttu-id="f2c1a-148">[カメラの機能を検出して選択](https://docs.microsoft.com//windows/uwp/audio-video-camera/camera-profiles)する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-148">Learn how to [discover and select camera capabilities](https://docs.microsoft.com//windows/uwp/audio-video-camera/camera-profiles).</span></span>
* <span data-ttu-id="f2c1a-149">カメラでは、次のプロファイルと解像度がサポートされています (すべてのビデオモードは16:9 縦横比です)。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-149">The camera supports the following profiles and resolutions (all video modes are 16:9 aspect ratio):</span></span>
  
  | <span data-ttu-id="f2c1a-150">プロファイル</span><span class="sxs-lookup"><span data-stu-id="f2c1a-150">Profile</span></span>                                         | <span data-ttu-id="f2c1a-151">ビデオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-151">Video</span></span>     | <span data-ttu-id="f2c1a-152">プレビュー</span><span class="sxs-lookup"><span data-stu-id="f2c1a-152">Preview</span></span>   | <span data-ttu-id="f2c1a-153">それでもなお</span><span class="sxs-lookup"><span data-stu-id="f2c1a-153">Still</span></span>     | <span data-ttu-id="f2c1a-154">フレーム レート</span><span class="sxs-lookup"><span data-stu-id="f2c1a-154">Frame rates</span></span> | <span data-ttu-id="f2c1a-155">ビューの水平方向のフィールド (H 視界)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-155">Horizontal Field of View (H-FOV)</span></span> | <span data-ttu-id="f2c1a-156">推奨される使用方法</span><span class="sxs-lookup"><span data-stu-id="f2c1a-156">Suggested usage</span></span>                             |
  |-------------------------------------------------|-----------|-----------|-----------|-------------|----------------------------------|---------------------------------------------|
  | <span data-ttu-id="f2c1a-157">Legacy、0 BalancedVideoAndPhoto、100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-157">Legacy,0  BalancedVideoAndPhoto,100</span></span>             | <span data-ttu-id="f2c1a-158">2272x1278</span><span class="sxs-lookup"><span data-stu-id="f2c1a-158">2272x1278</span></span> | <span data-ttu-id="f2c1a-159">2272x1278</span><span class="sxs-lookup"><span data-stu-id="f2c1a-159">2272x1278</span></span> |           | <span data-ttu-id="f2c1a-160">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-160">15,30</span></span>       | <span data-ttu-id="f2c1a-161">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-161">64.69</span></span>                            | <span data-ttu-id="f2c1a-162">高品質なビデオ記録</span><span class="sxs-lookup"><span data-stu-id="f2c1a-162">High quality video recording</span></span>                |
  | <span data-ttu-id="f2c1a-163">Legacy、0 BalancedVideoAndPhoto、100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-163">Legacy,0  BalancedVideoAndPhoto,100</span></span>             | <span data-ttu-id="f2c1a-164">896x504</span><span class="sxs-lookup"><span data-stu-id="f2c1a-164">896x504</span></span>   | <span data-ttu-id="f2c1a-165">896x504</span><span class="sxs-lookup"><span data-stu-id="f2c1a-165">896x504</span></span>   |           | <span data-ttu-id="f2c1a-166">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-166">15,30</span></span>       | <span data-ttu-id="f2c1a-167">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-167">64.69</span></span>                            | <span data-ttu-id="f2c1a-168">高品質の写真キャプチャ用のプレビューストリーム</span><span class="sxs-lookup"><span data-stu-id="f2c1a-168">Preview stream for high quality photo capture</span></span> |
  | <span data-ttu-id="f2c1a-169">Legacy、0 BalancedVideoAndPhoto、100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-169">Legacy,0  BalancedVideoAndPhoto,100</span></span>             |           |           | <span data-ttu-id="f2c1a-170">3904x2196</span><span class="sxs-lookup"><span data-stu-id="f2c1a-170">3904x2196</span></span> |             | <span data-ttu-id="f2c1a-171">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-171">64.69</span></span>                            | <span data-ttu-id="f2c1a-172">高品質な写真キャプチャ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-172">High quality photo capture</span></span>                  |
  | <span data-ttu-id="f2c1a-173">BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-173">BalancedVideoAndPhoto,120</span></span>                       | <span data-ttu-id="f2c1a-174">1952x1100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-174">1952x1100</span></span> | <span data-ttu-id="f2c1a-175">1952x1100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-175">1952x1100</span></span> | <span data-ttu-id="f2c1a-176">1952x1100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-176">1952x1100</span></span> | <span data-ttu-id="f2c1a-177">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-177">15,30</span></span>       | <span data-ttu-id="f2c1a-178">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-178">64.69</span></span>                            | <span data-ttu-id="f2c1a-179">長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-179">Long duration scenarios</span></span>                     |
  | <span data-ttu-id="f2c1a-180">BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-180">BalancedVideoAndPhoto,120</span></span>                       | <span data-ttu-id="f2c1a-181">1504x84 6</span><span class="sxs-lookup"><span data-stu-id="f2c1a-181">1504x846</span></span>  | <span data-ttu-id="f2c1a-182">1504x84 6</span><span class="sxs-lookup"><span data-stu-id="f2c1a-182">1504x846</span></span>  |           | <span data-ttu-id="f2c1a-183">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-183">15,30</span></span>       | <span data-ttu-id="f2c1a-184">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-184">64.69</span></span>                            | <span data-ttu-id="f2c1a-185">長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-185">Long duration scenarios</span></span>                     |
  | <span data-ttu-id="f2c1a-186">ビデオ会議、100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-186">VideoConferencing,100</span></span>                           | <span data-ttu-id="f2c1a-187">1952x1100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-187">1952x1100</span></span> | <span data-ttu-id="f2c1a-188">1952x1100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-188">1952x1100</span></span> | <span data-ttu-id="f2c1a-189">1952x1100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-189">1952x1100</span></span> | <span data-ttu-id="f2c1a-190">15、30、60</span><span class="sxs-lookup"><span data-stu-id="f2c1a-190">15,30,60</span></span>    | <span data-ttu-id="f2c1a-191">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-191">64.69</span></span>                            | <span data-ttu-id="f2c1a-192">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-192">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-193">ビデオ会議、100</span><span class="sxs-lookup"><span data-stu-id="f2c1a-193">Videoconferencing,100</span></span>                           | <span data-ttu-id="f2c1a-194">1504x84 6</span><span class="sxs-lookup"><span data-stu-id="f2c1a-194">1504x846</span></span>  | <span data-ttu-id="f2c1a-195">1504x84 6</span><span class="sxs-lookup"><span data-stu-id="f2c1a-195">1504x846</span></span>  |           | <span data-ttu-id="f2c1a-196">5、15、30、60</span><span class="sxs-lookup"><span data-stu-id="f2c1a-196">5,15,30,60</span></span>  | <span data-ttu-id="f2c1a-197">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-197">64.69</span></span>                            | <span data-ttu-id="f2c1a-198">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-198">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-199">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-199">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-200">1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="f2c1a-200">1920x1080</span></span> | <span data-ttu-id="f2c1a-201">1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="f2c1a-201">1920x1080</span></span> | <span data-ttu-id="f2c1a-202">1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="f2c1a-202">1920x1080</span></span> | <span data-ttu-id="f2c1a-203">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-203">15,30</span></span>       | <span data-ttu-id="f2c1a-204">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-204">64.69</span></span>                            | <span data-ttu-id="f2c1a-205">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-205">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-206">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-206">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-207">1280 x 720</span><span class="sxs-lookup"><span data-stu-id="f2c1a-207">1280x720</span></span>  | <span data-ttu-id="f2c1a-208">1280 x 720</span><span class="sxs-lookup"><span data-stu-id="f2c1a-208">1280x720</span></span>  | <span data-ttu-id="f2c1a-209">1280 x 720</span><span class="sxs-lookup"><span data-stu-id="f2c1a-209">1280x720</span></span>  | <span data-ttu-id="f2c1a-210">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-210">15,30</span></span>       | <span data-ttu-id="f2c1a-211">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-211">64.69</span></span>                            | <span data-ttu-id="f2c1a-212">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-212">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-213">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-213">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-214">1128x636</span><span class="sxs-lookup"><span data-stu-id="f2c1a-214">1128x636</span></span>  |           |           | <span data-ttu-id="f2c1a-215">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-215">15,30</span></span>       | <span data-ttu-id="f2c1a-216">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-216">64.69</span></span>                            | <span data-ttu-id="f2c1a-217">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-217">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-218">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-218">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-219">960 x 540</span><span class="sxs-lookup"><span data-stu-id="f2c1a-219">960x540</span></span>   |           |           | <span data-ttu-id="f2c1a-220">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-220">15,30</span></span>       | <span data-ttu-id="f2c1a-221">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-221">64.69</span></span>                            | <span data-ttu-id="f2c1a-222">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-222">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-223">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-223">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-224">760x428</span><span class="sxs-lookup"><span data-stu-id="f2c1a-224">760x428</span></span>   |           |           | <span data-ttu-id="f2c1a-225">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-225">15,30</span></span>       | <span data-ttu-id="f2c1a-226">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-226">64.69</span></span>                            | <span data-ttu-id="f2c1a-227">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-227">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-228">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-228">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-229">640 x 360</span><span class="sxs-lookup"><span data-stu-id="f2c1a-229">640x360</span></span>   |           |           | <span data-ttu-id="f2c1a-230">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-230">15,30</span></span>       | <span data-ttu-id="f2c1a-231">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-231">64.69</span></span>                            | <span data-ttu-id="f2c1a-232">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-232">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-233">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-233">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-234">500x282</span><span class="sxs-lookup"><span data-stu-id="f2c1a-234">500x282</span></span>   |           |           | <span data-ttu-id="f2c1a-235">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-235">15,30</span></span>       | <span data-ttu-id="f2c1a-236">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-236">64.69</span></span>                            | <span data-ttu-id="f2c1a-237">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-237">Video conferencing, long duration scenarios</span></span> |
  | <span data-ttu-id="f2c1a-238">ビデオ会議、100 BalancedVideoAndPhoto、120</span><span class="sxs-lookup"><span data-stu-id="f2c1a-238">Videoconferencing,100 BalancedVideoAndPhoto,120</span></span> | <span data-ttu-id="f2c1a-239">424x240</span><span class="sxs-lookup"><span data-stu-id="f2c1a-239">424x240</span></span>   |           |           | <span data-ttu-id="f2c1a-240">15、30</span><span class="sxs-lookup"><span data-stu-id="f2c1a-240">15,30</span></span>       | <span data-ttu-id="f2c1a-241">64.69</span><span class="sxs-lookup"><span data-stu-id="f2c1a-241">64.69</span></span>                            | <span data-ttu-id="f2c1a-242">ビデオ会議、長期間のシナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-242">Video conferencing, long duration scenarios</span></span> |

>[!NOTE]
><span data-ttu-id="f2c1a-243">[混合 reality キャプチャ](mixed-reality-capture.md)を利用して、アプリのビデオや写真を撮ることができます。これには、ホログラムやビデオの安定化が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-243">Customers can leverage [mixed reality capture](mixed-reality-capture.md) to take videos or photos of your app, which include holograms and video stabilization.</span></span>
>
><span data-ttu-id="f2c1a-244">開発者にとっては、顧客がコンテンツをキャプチャしたときに可能な限り、アプリを作成する際に考慮する必要がある考慮事項があります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-244">As a developer, there are considerations you should take into account when creating your app if you want it to look as good as possible when a customer captures content.</span></span> <span data-ttu-id="f2c1a-245">また、アプリ内で直接、mixed reality キャプチャを有効 (およびカスタマイズ) することもできます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-245">You can also enable (and customize) mixed reality capture from directly within your app.</span></span> <span data-ttu-id="f2c1a-246">詳細につい[ては、「開発者向けの混合現実のキャプチャ」を](mixed-reality-capture-for-developers.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-246">Learn more at [mixed reality capture for developers](mixed-reality-capture-for-developers.md).</span></span>

## <a name="locating-the-device-camera-in-the-world"></a><span data-ttu-id="f2c1a-247">デバイスカメラを世界中に配置する</span><span class="sxs-lookup"><span data-stu-id="f2c1a-247">Locating the Device Camera in the World</span></span>

<span data-ttu-id="f2c1a-248">HoloLens が写真やビデオを撮影する場合、キャプチャされたフレームには、世界中のカメラの位置と、カメラのレンズモデルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-248">When HoloLens takes photos and videos, the captured frames include the location of the camera in the world, as well as the lens model of the camera.</span></span> <span data-ttu-id="f2c1a-249">これにより、アプリケーションは、イメージのシナリオを強化するために、実際の環境におけるカメラの位置を理解することができます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-249">This allows applications to reason about the position of the camera in the real world for augmented imaging scenarios.</span></span> <span data-ttu-id="f2c1a-250">開発者は、お気に入りのイメージ処理またはカスタムコンピュータービジョンライブラリを使用して、独自のシナリオを独創ロールできます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-250">Developers can creatively roll their own scenarios using their favorite image processing or custom computer vision libraries.</span></span>

<span data-ttu-id="f2c1a-251">HoloLens ドキュメントの他の場所にある "カメラ" は、"仮想ゲームカメラ" (アプリがレンダリングするための、視錐) を指している場合があります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-251">"Camera" elsewhere in HoloLens documentation may refer to the "virtual game camera" (the frustum the app renders to).</span></span> <span data-ttu-id="f2c1a-252">特に明記しない限り、このページの "カメラ" は実際の RGB カラーカメラを表します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-252">Unless denoted otherwise, "camera" on this page refers to the real-world RGB color camera.</span></span>

### <a name="using-unity"></a><span data-ttu-id="f2c1a-253">Unity の使用</span><span class="sxs-lookup"><span data-stu-id="f2c1a-253">Using Unity</span></span>

<span data-ttu-id="f2c1a-254">' CameraIntrinsics ' と ' CameraCoordinateSystem ' からアプリケーション/ワールド座標系に移行するには、 [Unity の検索カメラ](locatable-camera-in-unity.md)の記事に記載されている手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-254">To go from the 'CameraIntrinsics' and 'CameraCoordinateSystem' to your application/world coordinate system, follow the instructions in the [Locatable camera in Unity](locatable-camera-in-unity.md) article.</span></span>  <span data-ttu-id="f2c1a-255">CameraToWorldMatrix は PhotoCaptureFrame クラスによって自動的に提供されるため、以下で説明する CameraCoordinateSystem の変換について心配する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-255">CameraToWorldMatrix is automatically provided by PhotoCaptureFrame class, and so you don't need to worry about the CameraCoordinateSystem transforms discussed below.</span></span>

### <a name="using-mediaframereference"></a><span data-ttu-id="f2c1a-256">MediaFrameReference の使用</span><span class="sxs-lookup"><span data-stu-id="f2c1a-256">Using MediaFrameReference</span></span>

<span data-ttu-id="f2c1a-257">これらの手順は、 [MediaFrameReference](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.mediaframereference)クラスを使用してカメラからイメージフレームを読み取る場合に適用されます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-257">These instructions apply if you are using the [MediaFrameReference](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.mediaframereference) class to read image frames from the camera.</span></span>

<span data-ttu-id="f2c1a-258">各イメージフレーム (写真またはビデオ) には、キャプチャ時にカメラでルート化された[SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem)が含まれています。これには、 [MediaFrameReference](https://docs.microsoft.com//uwp/api/Windows.Media.Capture.Frames.MediaFrameReference)の[CoordinateSystem](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.mediaframereference.coordinatesystem#Windows_Media_Capture_Frames_MediaFrameReference_CoordinateSystem)プロパティを使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-258">Each image frame (whether photo or video) includes a [SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem) rooted at the camera at the time of capture, which can be accessed using the [CoordinateSystem](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.mediaframereference.coordinatesystem#Windows_Media_Capture_Frames_MediaFrameReference_CoordinateSystem) property of your [MediaFrameReference](https://docs.microsoft.com//uwp/api/Windows.Media.Capture.Frames.MediaFrameReference).</span></span> <span data-ttu-id="f2c1a-259">さらに、各フレームには、カメラレンズモデルの説明が含まれています。これは、 [CameraIntrinsics](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics)プロパティにあります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-259">In addition, each frame contains a description of the camera lens model, which can be found in the [CameraIntrinsics](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics) property.</span></span> <span data-ttu-id="f2c1a-260">これらの変換は、ピクセルを生成した photons によって取得されたパスを表す3D 空間の光をピクセルごとに定義します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-260">Together, these transforms define for each pixel a ray in 3D space representing the path taken by the photons that produced the pixel.</span></span> <span data-ttu-id="f2c1a-261">これらの光線は、フレームの座標系から他の座標系 (例:[静止フレーム](coordinate-systems.md#stationary-frame-of-reference)から) への変換を取得することによって、アプリ内の他のコンテンツに関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-261">These rays can be related to other content in the app by obtaining the transform from the frame's coordinate system to some other coordinate system (e.g. from a [stationary frame of reference](coordinate-systems.md#stationary-frame-of-reference)).</span></span> <span data-ttu-id="f2c1a-262">要約すると、各イメージフレームには次のものが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-262">To summarize, each image frame provides the following:</span></span>
* <span data-ttu-id="f2c1a-263">ピクセルデータ (RGB/NV12/JPEG/など)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-263">Pixel Data (in RGB/NV12/JPEG/etc. format)</span></span>
* <span data-ttu-id="f2c1a-264">キャプチャの場所からの[SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-264">A [SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem) from the location of capture</span></span>
* <span data-ttu-id="f2c1a-265">カメラのレンズモードを含む[CameraIntrinsics](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics)クラス</span><span class="sxs-lookup"><span data-stu-id="f2c1a-265">A [CameraIntrinsics](https://docs.microsoft.com//uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics) class containing the lens mode of the camera</span></span>

<span data-ttu-id="f2c1a-266">[HolographicFaceTracking サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking)は、カメラの座標系と独自のアプリケーション座標系との間の変換をクエリするための非常に簡単な方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-266">The [HolographicFaceTracking sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking) shows the fairly straightforward way to query for the transform between the camera's coordinate system and your own application coordinate systems.</span></span>

### <a name="using-media-foundation"></a><span data-ttu-id="f2c1a-267">メディアファンデーションの使用</span><span class="sxs-lookup"><span data-stu-id="f2c1a-267">Using Media Foundation</span></span>

<span data-ttu-id="f2c1a-268">カメラからイメージフレームを読み取るためにメディアファンデーション直接使用している場合は、次のサンプルコードに示すように、各フレームの[MFSampleExtension_CameraExtrinsics 属性](https://docs.microsoft.com/windows/win32/medfound/mfsampleextension-cameraextrinsics)と[MFSampleExtension_PinholeCameraIntrinsics 属性](https://docs.microsoft.com/windows/win32/medfound/mfsampleextension-pinholecameraintrinsics)を使用して、アプリケーションの他の座標系を基準としたカメラフレームを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-268">If you are using Media Foundation directly to read image frames from the camera, you can use each frame's [MFSampleExtension_CameraExtrinsics attribute](https://docs.microsoft.com/windows/win32/medfound/mfsampleextension-cameraextrinsics) and [MFSampleExtension_PinholeCameraIntrinsics attribute](https://docs.microsoft.com/windows/win32/medfound/mfsampleextension-pinholecameraintrinsics) to locate camera frames relative to your application's other coordinate systems, as shown in this sample code:</span></span>

```cpp
#include <winrt/windows.perception.spatial.preview.h>
#include <mfapi.h>
#include <mfidl.h>
 
using namespace winrt::Windows::Foundation;
using namespace winrt::Windows::Foundation::Numerics;
using namespace winrt::Windows::Perception;
using namespace winrt::Windows::Perception::Spatial;
using namespace winrt::Windows::Perception::Spatial::Preview;
 
class CameraFrameLocator
{
public:
    struct CameraFrameLocation
    {
        SpatialCoordinateSystem CoordinateSystem;
        float4x4 CameraViewToCoordinateSytemTransform;
        MFPinholeCameraIntrinsics Intrinsics;
    };
 
    std::optional<CameraFrameLocation> TryLocateCameraFrame(IMFSample* pSample)
    {
        MFCameraExtrinsics cameraExtrinsics;
        MFPinholeCameraIntrinsics cameraIntrinsics;
        UINT32 sizeCameraExtrinsics = 0;
        UINT32 sizeCameraIntrinsics = 0;
        UINT64 sampleTimeQpc = 0;
 
        // query sample for calibration and validate
        if (FAILED(pSample->GetUINT64(MFSampleExtension_DeviceTimestamp, &sampleTimeQpc)) ||
            FAILED(pSample->GetBlob(MFSampleExtension_CameraExtrinsics, (UINT8*)& cameraExtrinsics, sizeof(cameraExtrinsics), &sizeCameraExtrinsics)) ||
            FAILED(pSample->GetBlob(MFSampleExtension_PinholeCameraIntrinsics, (UINT8*)& cameraIntrinsics, sizeof(cameraIntrinsics), &sizeCameraIntrinsics)) ||
            (sizeCameraExtrinsics != sizeof(cameraExtrinsics)) ||
            (sizeCameraIntrinsics != sizeof(cameraIntrinsics)) ||
            (cameraExtrinsics.TransformCount == 0))
        {
            return std::nullopt;
        }
 
        // compute extrinsic transform
        const auto& calibratedTransform = cameraExtrinsics.CalibratedTransforms[0];
        const GUID& dynamicNodeId = calibratedTransform.CalibrationId;
        const float4x4 cameraToDynamicNode =
            make_float4x4_from_quaternion(quaternion{ calibratedTransform.Orientation.x, calibratedTransform.Orientation.y, calibratedTransform.Orientation.z, calibratedTransform.Orientation.w }) *
            make_float4x4_translation(calibratedTransform.Position.x, calibratedTransform.Position.y, calibratedTransform.Position.z);
 
        // update locator cache for dynamic node
        if (dynamicNodeId != m_currentDynamicNodeId || !m_locator)
        {
            m_locator = SpatialGraphInteropPreview::CreateLocatorForNode(dynamicNodeId);
            if (!m_locator)
            {
                return std::nullopt;
            }
 
            m_frameOfReference = m_locator.CreateAttachedFrameOfReferenceAtCurrentHeading();
            m_currentDynamicNodeId = dynamicNodeId;
        }
 
        // locate dynamic node
        auto timestamp = PerceptionTimestampHelper::FromSystemRelativeTargetTime(TimeSpanFrodmQpcTicks(sampleTimeQpc));
        auto coordinateSystem = m_frameOfReference.GetStationaryCoordinateSystemAtTimestamp(timestamp);
        auto location = m_locator.TryLocateAtTimestamp(timestamp, coordinateSystem);
        if (!location)
        {
            return std::nullopt;
        }
 
        const float4x4 dynamicNodeToCoordinateSystem = make_float4x4_from_quaternion(location.Orientation()) * make_float4x4_translation(location.Position());
 
        return CameraFrameLocation{ coordinateSystem, cameraToDynamicNode * dynamicNodeToCoordinateSystem, cameraIntrinsics };
    }
 
private:
    GUID m_currentDynamicNodeId{ GUID_NULL };
    SpatialLocator m_locator{ nullptr };
    SpatialLocatorAttachedFrameOfReference m_frameOfReference{ nullptr };
 
    // Convert a duration value from a source tick frequency to a destination tick frequency.
    static inline int64_t SourceDurationTicksToDestDurationTicks(int64_t sourceDurationInTicks, int64_t sourceTicksPerSecond, int64_t destTicksPerSecond)
    {
        int64_t whole = (sourceDurationInTicks / sourceTicksPerSecond) * destTicksPerSecond;                          // 'whole' is rounded down in the target time units.
        int64_t part = (sourceDurationInTicks % sourceTicksPerSecond) * destTicksPerSecond / sourceTicksPerSecond;    // 'part' is the remainder in the target time units.
        return whole + part;
    }
 
    static inline TimeSpan TimeSpanFromQpcTicks(int64_t qpcTicks)
    {
        static const int64_t qpcFrequency = []
        {
            LARGE_INTEGER frequency;
            QueryPerformanceFrequency(&frequency);
            return frequency.QuadPart;
        }();
 
        return TimeSpan{ SourceDurationTicksToDestDurationTicks(qpcTicks, qpcFrequency, winrt::clock::period::den) / winrt::clock::period::num };
    }
};
```

### <a name="distortion-error"></a><span data-ttu-id="f2c1a-269">ディストーションエラー</span><span class="sxs-lookup"><span data-stu-id="f2c1a-269">Distortion Error</span></span>

<span data-ttu-id="f2c1a-270">HoloLens では、アプリケーションでフレームを利用できるようになる前に、ビデオストリームと静止画像ストリームがシステムのイメージ処理パイプラインで undistorted されます (プレビューストリームには、元のゆがんだフレームが含まれます)。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-270">On HoloLens, the video and still image streams are undistorted in the system's image processing pipeline before the frames are made available to the application (the preview stream contains the original distorted frames).</span></span> <span data-ttu-id="f2c1a-271">使用できるのは CameraIntrinsics だけなので、アプリケーションではイメージフレームが完全な pinhole カメラを表すものと想定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-271">Because only the CameraIntrinsics are made available, applications must assume image frames represent a perfect pinhole camera.</span></span>

<span data-ttu-id="f2c1a-272">HoloLens (第1世代) では、イメージプロセッサのディストーション関数は、フレームメタデータで CameraIntrinsics を使用しているときに最大10ピクセルのエラーを引き続き発生させる場合があります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-272">On HoloLens (first-generation), the undistortion function in the image processor may still leave an error of up to 10 pixels when using the CameraIntrinsics in the frame metadata.</span></span> <span data-ttu-id="f2c1a-273">多くのユースケースでは、このエラーは問題にはなりませんが、たとえば、ホログラムを実際のポスター/マーカーに整列させている場合、<10px オフセット (2 m の位置にあるホログラムの場合は約 11 mm) が発生した場合、この歪みエラーが原因である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-273">In many use cases, this error will not matter, but if you are aligning holograms to real world posters/markers, for example, and you notice a <10px offset (roughly 11mm for holograms positioned 2 meters away), this distortion error could be the cause.</span></span> 

## <a name="locatable-camera-usage-scenarios"></a><span data-ttu-id="f2c1a-274">お持ちのカメラの使用シナリオ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-274">Locatable Camera Usage Scenarios</span></span>

### <a name="show-a-photo-or-video-in-the-world-where-it-was-captured"></a><span data-ttu-id="f2c1a-275">キャプチャされた場所で写真またはビデオを表示する</span><span class="sxs-lookup"><span data-stu-id="f2c1a-275">Show a photo or video in the world where it was captured</span></span>

<span data-ttu-id="f2c1a-276">デバイスカメラのフレームには、イメージがどこで撮影されたかを正確に示すために使用できる "カメラからワールドへの変換" 変換が付属しています。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-276">The Device Camera frames come with a "Camera To World" transform, that can be used to show exactly where the device was when the image was taken.</span></span> <span data-ttu-id="f2c1a-277">たとえば、小さな holographic アイコンをこの場所 (CameraToWorld (Vector3)) に配置して、カメラが直面している方向に小さな矢印を描画する (CameraToWorld Yvector (Vector3)) ことができます ()。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-277">For example, you could position a small holographic icon at this location (CameraToWorld.MultiplyPoint(Vector3.zero)) and even draw a little arrow in the direction that the camera was facing (CameraToWorld.MultiplyVector(Vector3.forward)).</span></span>

### <a name="tag--pattern--poster--object-tracking"></a><span data-ttu-id="f2c1a-278">タグ/パターン/ポスター/オブジェクトの追跡</span><span class="sxs-lookup"><span data-stu-id="f2c1a-278">Tag / Pattern / Poster / Object Tracking</span></span>

<span data-ttu-id="f2c1a-279">多くの mixed reality アプリケーションでは、認識可能なイメージまたはビジュアルパターンを使用して、空間内の追跡可能なポイントを作成します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-279">Many mixed reality applications use a recognizable image or visual pattern to create a trackable point in space.</span></span> <span data-ttu-id="f2c1a-280">その後、そのポイントを基準としてオブジェクトをレンダリングしたり、既知の場所を作成したりするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-280">This is then used to render objects relative to that point or create a known location.</span></span> <span data-ttu-id="f2c1a-281">HoloLens の使用例としては、fiducials でタグ付けされた現実世界のオブジェクト (QR コードを使用したテレビモニターなど) の検索、fiducials に対するホログラムの配置、および Wi-fi を介して HoloLens と通信するように設定されているタブレットなどの非 HoloLens デバイスとの視覚的な組み合わせがあります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-281">Some uses for HoloLens include finding a real world object tagged with fiducials (e.g. a TV monitor with a QR code), placing holograms over fiducials, and visually pairing with non-HoloLens devices like tablets that have been setup to communicate with HoloLens via Wi-Fi.</span></span>

<span data-ttu-id="f2c1a-282">ビジュアルパターンを認識し、そのオブジェクトをアプリケーションのワールド空間に配置するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-282">To recognize a visual pattern, and then place that object in the applications world space, you'll need a few things:</span></span>
1. <span data-ttu-id="f2c1a-283">画像パターン認識ツールキット (QR コード、AR タグ、顔ファインダー、サークルトラッカー、OCR など)。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-283">An image pattern recognition toolkit, such as QR code, AR tags, face finder, circle trackers, OCR etc.</span></span>
2. <span data-ttu-id="f2c1a-284">実行時にイメージフレームを収集して認識レイヤーに渡す</span><span class="sxs-lookup"><span data-stu-id="f2c1a-284">Collect image frames at runtime, and pass them to the recognition layer</span></span>
3. <span data-ttu-id="f2c1a-285">画像の位置を、世界中や世界中の写真に戻すことができます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-285">Unproject their image locations back into world positions, or likely world rays.</span></span> 
4. <span data-ttu-id="f2c1a-286">これらの世界の場所に仮想モデルを配置する</span><span class="sxs-lookup"><span data-stu-id="f2c1a-286">Position your virtual models over these world locations</span></span>

<span data-ttu-id="f2c1a-287">いくつかの重要な画像処理リンク:</span><span class="sxs-lookup"><span data-stu-id="f2c1a-287">Some important image processing links:</span></span>
* [<span data-ttu-id="f2c1a-288">OpenCV</span><span class="sxs-lookup"><span data-stu-id="f2c1a-288">OpenCV</span></span>](https://opencv.org/)
* [<span data-ttu-id="f2c1a-289">QR タグ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-289">QR Tags</span></span>](https://en.wikipedia.org/wiki/QR_code)
* [<span data-ttu-id="f2c1a-290">FaceSDK</span><span class="sxs-lookup"><span data-stu-id="f2c1a-290">FaceSDK</span></span>](https://research.microsoft.com/projects/facesdk/)
* [<span data-ttu-id="f2c1a-291">Microsoft Translator</span><span class="sxs-lookup"><span data-stu-id="f2c1a-291">Microsoft Translator</span></span>](https://www.microsoft.com/translator/business)

<span data-ttu-id="f2c1a-292">対話型アプリケーションのフレームレートを維持することは、特に長時間実行されるイメージ認識アルゴリズムを扱う場合に重要です。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-292">Keeping an interactive application frame-rate is critical, especially when dealing with long-running image recognition algorithms.</span></span> <span data-ttu-id="f2c1a-293">このため、一般的には次のパターンを使用します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-293">For this reason, we commonly use the following pattern:</span></span>
1. <span data-ttu-id="f2c1a-294">メインスレッド: カメラオブジェクトを管理します</span><span class="sxs-lookup"><span data-stu-id="f2c1a-294">Main Thread: manages the camera object</span></span>
2. <span data-ttu-id="f2c1a-295">メインスレッド: 新しいフレームの要求 (非同期)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-295">Main Thread: requests new frames (async)</span></span>
3. <span data-ttu-id="f2c1a-296">メインスレッド: 新しいフレームを追跡スレッドに渡します</span><span class="sxs-lookup"><span data-stu-id="f2c1a-296">Main Thread: pass new frames to tracking thread</span></span>
4. <span data-ttu-id="f2c1a-297">追跡スレッド: キーポイントを収集するためのイメージの処理</span><span class="sxs-lookup"><span data-stu-id="f2c1a-297">Tracking Thread: processes image to collect key points</span></span>
5. <span data-ttu-id="f2c1a-298">メインスレッド: 検出されるキーポイントに一致するように仮想モデルを移動します</span><span class="sxs-lookup"><span data-stu-id="f2c1a-298">Main Thread: moves virtual model to match found key points</span></span>
6. <span data-ttu-id="f2c1a-299">メインスレッド: 手順2の繰り返し</span><span class="sxs-lookup"><span data-stu-id="f2c1a-299">Main Thread: repeat from step 2</span></span>

<span data-ttu-id="f2c1a-300">一部のイメージマーカーシステムは、1ピクセルの位置のみを提供します (他のユーザーが完全変換を提供するため、このセクションは必要ありません)。これは、可能な場所の射線に相当します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-300">Some image marker systems only provide a single pixel location (others provide the full transform in which case this section will not be needed), which equates to a ray of possible locations.</span></span> <span data-ttu-id="f2c1a-301">1つの3d 位置に移動するには、複数の光線を活用し、最終的な結果をおおよその交点で見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-301">To get to a single 3d location, we can then leverage multiple rays and find the final result by their approximate intersection.</span></span> <span data-ttu-id="f2c1a-302">そのために必要な作業を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-302">To do this, you'll need to:</span></span>
1. <span data-ttu-id="f2c1a-303">複数のカメライメージの収集を開始するループを取得する</span><span class="sxs-lookup"><span data-stu-id="f2c1a-303">Get a loop going collecting multiple camera images</span></span>
2. <span data-ttu-id="f2c1a-304">関連する特徴ポイントとそのワールド光線を検索する</span><span class="sxs-lookup"><span data-stu-id="f2c1a-304">Find the associated feature points, and their world rays</span></span>
3. <span data-ttu-id="f2c1a-305">特徴のディクショナリ (それぞれが複数のワールド線を持つ) がある場合は、次のコードを使用して、これらの光線の交差部分を解決できます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-305">When you have a dictionary of features, each with multiple world rays, you can use the following code to solve for the intersection of those rays:</span></span>

```
public static Vector3 ClosestPointBetweenRays(
   Vector3 point1, Vector3 normalizedDirection1,
   Vector3 point2, Vector3 normalizedDirection2) {
   float directionProjection = Vector3.Dot(normalizedDirection1, normalizedDirection2);
   if (directionProjection == 1) {
     return point1; // parallel lines
   }
   float projection1 = Vector3.Dot(point2 - point1, normalizedDirection1);
   float projection2 = Vector3.Dot(point2 - point1, normalizedDirection2);
   float distanceAlongLine1 = (projection1 - directionProjection * projection2) / (1 - directionProjection * directionProjection);
   float distanceAlongLine2 = (projection2 - directionProjection * projection1) / (directionProjection * directionProjection - 1);
   Vector3 pointOnLine1 = point1 + distanceAlongLine1 * normalizedDirection1;
   Vector3 pointOnLine2 = point2 + distanceAlongLine2 * normalizedDirection2;
   return Vector3.Lerp(pointOnLine2, pointOnLine1, 0.5f);
 }
```

<span data-ttu-id="f2c1a-306">追跡タグの場所が2つ以上ある場合は、ユーザーの現在のシナリオに合わせてモデル化シーンを配置できます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-306">Given two or more tracked tag locations, you can position a modelled scene to fit the user's current scenario.</span></span> <span data-ttu-id="f2c1a-307">重力を想定できない場合は、3つのタグ位置が必要になります。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-307">If you can't assume gravity, then you'll need three tag locations.</span></span> <span data-ttu-id="f2c1a-308">多くの場合、ホワイト球体がリアルタイムで追跡されるタグ位置を表し、blue 球体がモデル化タグの場所を表す単純な配色を使用します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-308">In many cases, we use a simple color scheme where white spheres represent real-time tracked tag locations, and blue spheres represent modelled tag locations.</span></span> <span data-ttu-id="f2c1a-309">これにより、ユーザーは配置品質を視覚的に測定できます。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-309">This allows the user to visually gauge the alignment quality.</span></span> <span data-ttu-id="f2c1a-310">ここでは、すべてのアプリケーションで次のセットアップを想定しています。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-310">We assume the following setup in all our applications:</span></span>
* <span data-ttu-id="f2c1a-311">2つ以上のモデル化タグの場所</span><span class="sxs-lookup"><span data-stu-id="f2c1a-311">Two or more modelled tag locations</span></span>
* <span data-ttu-id="f2c1a-312">シーン内の1つの ' 調整スペース ' は、タグの親です。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-312">One 'calibration space' which in the scene is the parent of the tags</span></span>
* <span data-ttu-id="f2c1a-313">カメラの機能識別子</span><span class="sxs-lookup"><span data-stu-id="f2c1a-313">Camera feature identifier</span></span>
* <span data-ttu-id="f2c1a-314">調整領域を移動して、モデル化タグをリアルタイムタグに整列させる動作 (他の接続はその相対的な位置であるため、モデル化マーカー自体ではなく、親スペースを移動することは注意してください)。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-314">Behavior which moves the calibration space to align the modelled tags with the real-time tags (we are careful to move the parent space, not the modelled markers themselves, because other connect is positions relative to them).</span></span>

```
// In the two tags case:
 Vector3 idealDelta = (realTags[1].EstimatedWorldPos - realTags[0].EstimatedWorldPos);
 Vector3 curDelta = (modelledTags[1].transform.position - modelledTags[0].transform.position);
 if (IsAssumeGravity) {
   idealDelta.y = 0;
   curDelta.y = 0;
 }
 Quaternion deltaRot = Quaternion.FromToRotation(curDelta, idealDelta);
 trans.rotation = Quaternion.LookRotation(deltaRot * trans.forward, trans.up);
 trans.position += realTags[0].EstimatedWorldPos - modelledTags[0].transform.position;
```

### <a name="track-or-identify-tagged-stationary-or-moving-real-world-objectsfaces-using-leds-or-other-recognizer-libraries"></a><span data-ttu-id="f2c1a-315">Led または他のレコグナイザーライブラリを使用して、タグ付き静止を追跡または特定したり、実際のオブジェクト/顔を移動したりします。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-315">Track or Identify Tagged Stationary or Moving real-world objects/faces using LEDs or other recognizer libraries</span></span>

<span data-ttu-id="f2c1a-316">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-316">Examples:</span></span>
* <span data-ttu-id="f2c1a-317">Led のある工業ロボット (または低速な移動オブジェクトの QR コード)</span><span class="sxs-lookup"><span data-stu-id="f2c1a-317">Industrial robots with LEDs (or QR codes for slower moving objects)</span></span>
* <span data-ttu-id="f2c1a-318">ルーム内のオブジェクトを識別して認識する</span><span class="sxs-lookup"><span data-stu-id="f2c1a-318">Identify and recognize objects in the room</span></span>
* <span data-ttu-id="f2c1a-319">部屋のメンバーを識別して認識します (たとえば、顔を holographic 連絡先カードを配置します)。</span><span class="sxs-lookup"><span data-stu-id="f2c1a-319">Identify and recognize people in the room (e.g. place holographic contact cards over faces)</span></span>

## <a name="see-also"></a><span data-ttu-id="f2c1a-320">関連項目</span><span class="sxs-lookup"><span data-stu-id="f2c1a-320">See also</span></span>
* [<span data-ttu-id="f2c1a-321">お持ちのカメラのサンプル</span><span class="sxs-lookup"><span data-stu-id="f2c1a-321">Locatable camera sample</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking)
* [<span data-ttu-id="f2c1a-322">Unity での場所を特定できるカメラ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-322">Locatable camera in Unity</span></span>](locatable-camera-in-unity.md)
* [<span data-ttu-id="f2c1a-323">複合現実キャプチャ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-323">Mixed reality capture</span></span>](mixed-reality-capture.md)
* [<span data-ttu-id="f2c1a-324">開発者向け複合現実キャプチャ</span><span class="sxs-lookup"><span data-stu-id="f2c1a-324">Mixed reality capture for developers</span></span>](mixed-reality-capture-for-developers.md)
* [<span data-ttu-id="f2c1a-325">メディアキャプチャの概要</span><span class="sxs-lookup"><span data-stu-id="f2c1a-325">Media capture introduction</span></span>](https://msdn.microsoft.com/library/windows/apps/mt243896.aspx)
* [<span data-ttu-id="f2c1a-326">Holographic face tracking サンプル</span><span class="sxs-lookup"><span data-stu-id="f2c1a-326">Holographic face tracking sample</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking)
