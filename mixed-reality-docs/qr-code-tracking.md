---
title: QR コードの追跡
description: HoloLens 2 で QR コードを検出する方法について説明します。
author: dorreneb
ms.author: dobrown
ms.date: 05/15/2019
ms.topic: article
keywords: vr, lbe, 位置情報ベースのエンターテインメント, vr アーケード, アーケード, イマーシブ, qr, qr コード, hololens2
ms.openlocfilehash: 6d3dc442c28e498cc00e14325398de2026261a17
ms.sourcegitcommit: ef0bf03833eda826ed0b884859b4573775112aba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87476764"
---
# <a name="qr-code-tracking"></a><span data-ttu-id="050b0-104">QR コードの追跡</span><span class="sxs-lookup"><span data-stu-id="050b0-104">QR code tracking</span></span>

<span data-ttu-id="050b0-105">HoloLens 2 では、ヘッドセット周辺の環境内の QR コードを検出し、各コードの実際の場所で座標系を確立します。</span><span class="sxs-lookup"><span data-stu-id="050b0-105">HoloLens 2 can detect QR codes in the environment around the headset, establishing a coordinate system at each code's real-world location.</span></span>

## <a name="device-support"></a><span data-ttu-id="050b0-106">デバイス サポート</span><span class="sxs-lookup"><span data-stu-id="050b0-106">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="050b0-107">機能</span><span class="sxs-lookup"><span data-stu-id="050b0-107">Feature</span></span></th><th style="width:150px"> <span data-ttu-id="050b0-108"><a href="hololens-hardware-details.md">HoloLens (第 1 世代)</a></span><span class="sxs-lookup"><span data-stu-id="050b0-108"><a href="hololens-hardware-details.md">HoloLens (1st gen)</a></span></span></th><th style="width:150px"><span data-ttu-id="050b0-109">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="050b0-109">HoloLens 2</span></span></th><th style="width:150px"> <span data-ttu-id="050b0-110"><a href="immersive-headset-hardware-details.md">イマーシブ ヘッドセット</a></span><span class="sxs-lookup"><span data-stu-id="050b0-110"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="050b0-111">QR コードの検出</span><span class="sxs-lookup"><span data-stu-id="050b0-111">QR code detection</span></span></td><td style="text-align: center;"><span data-ttu-id="050b0-112">️</span><span class="sxs-lookup"><span data-stu-id="050b0-112">️</span></span></td><td style="text-align: center;"> <span data-ttu-id="050b0-113">✔️</span><span class="sxs-lookup"><span data-stu-id="050b0-113">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="050b0-114">✔️</span><span class="sxs-lookup"><span data-stu-id="050b0-114">✔️</span></span></td>
</tr>
</table>

>[!NOTE]
><span data-ttu-id="050b0-115">デスクトップ Pc でのイマーシブ Windows Mixed Reality ヘッドセットを使用した QR コードの追跡は、Windows 10 バージョン2004以降でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="050b0-115">QR code tracking with immersive Windows Mixed Reality headsets on desktop PCs is supported on Windows 10 Version 2004 and higher.</span></span> <span data-ttu-id="050b0-116">MixedReality () API を使用して、機能が現在のデバイスでサポートされているかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="050b0-116">Use the Microsoft.MixedReality.QRCodeWatcher.IsSupported() API to determine whether the feature is supported on the current device.</span></span>

## <a name="getting-the-qr-package"></a><span data-ttu-id="050b0-117">QR パッケージの取得</span><span class="sxs-lookup"><span data-stu-id="050b0-117">Getting the QR package</span></span>
<span data-ttu-id="050b0-118">QR コード検出用の NuGet パッケージは[こちら](https://nuget.org/Packages/Microsoft.MixedReality.QR)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="050b0-118">You can download the NuGet package for QR code detection [here](https://nuget.org/Packages/Microsoft.MixedReality.QR).</span></span>

## <a name="detecting-qr-codes"></a><span data-ttu-id="050b0-119">QR コードの検出</span><span class="sxs-lookup"><span data-stu-id="050b0-119">Detecting QR codes</span></span>

### <a name="adding-the-webcam-capability"></a><span data-ttu-id="050b0-120">Web カメラ機能の追加</span><span class="sxs-lookup"><span data-stu-id="050b0-120">Adding the webcam capability</span></span>
<span data-ttu-id="050b0-121">QR コードを検出するには、マニフェストに機能を追加する必要があり `webcam` ます。</span><span class="sxs-lookup"><span data-stu-id="050b0-121">You will need to add the capability `webcam` to your manifest to detect QR codes.</span></span> <span data-ttu-id="050b0-122">この機能は、ユーザーの環境で検出されたコード内のデータに機密情報が含まれている場合に必要です。</span><span class="sxs-lookup"><span data-stu-id="050b0-122">This capability is required as the data within detected codes in the user's environment may contain sensitive information.</span></span>

<span data-ttu-id="050b0-123">アクセス許可を要求するには、次のように呼び出し `QRCodeWatcher.RequestAccessAsync()` ます。</span><span class="sxs-lookup"><span data-stu-id="050b0-123">Permission can be requested by calling `QRCodeWatcher.RequestAccessAsync()`:</span></span>

<span data-ttu-id="050b0-124">_Visual_</span><span class="sxs-lookup"><span data-stu-id="050b0-124">_C#:_</span></span>
```cs
await QRCodeWatcher.RequestAccessAsync();
```

<span data-ttu-id="050b0-125">_C++_</span><span class="sxs-lookup"><span data-stu-id="050b0-125">_C++:_</span></span>
```cpp
co_await QRCodeWatcher.RequestAccessAsync();
```

<span data-ttu-id="050b0-126">QRCodeWatcher オブジェクトを構築する前に、アクセス許可を要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="050b0-126">Permission must be requested before you construct a QRCodeWatcher object.</span></span>

<span data-ttu-id="050b0-127">QR コードの検出には機能が必要ですが、 `webcam` 検出はデバイスの追跡カメラを使用して行われます。</span><span class="sxs-lookup"><span data-stu-id="050b0-127">While QR code detection requires the `webcam` capability, the detection occurs using the device's tracking cameras.</span></span> <span data-ttu-id="050b0-128">これにより、デバイスの写真/ビデオ (PV) カメラとの検出と比較して、より広範な検出とバッテリ寿命が提供されます。</span><span class="sxs-lookup"><span data-stu-id="050b0-128">This provides a wider detection FOV and better battery life compared to detection with the device's photo/video (PV) camera.</span></span>

### <a name="detecting-qr-codes-in-unity"></a><span data-ttu-id="050b0-129">Unity での QR コードの検出</span><span class="sxs-lookup"><span data-stu-id="050b0-129">Detecting QR codes in Unity</span></span>

<span data-ttu-id="050b0-130">Unity の QR コード検出 API は、MRTK に依存せずに使用できます。</span><span class="sxs-lookup"><span data-stu-id="050b0-130">You can use the QR code detection API in Unity without taking a dependency on MRTK.</span></span> <span data-ttu-id="050b0-131">これを行うには、nuget [For Unity](https://github.com/GlitchEnzo/NuGetForUnity)を使用して nuget パッケージをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="050b0-131">To do so, you must install the NuGet package using [NuGet for Unity](https://github.com/GlitchEnzo/NuGetForUnity).</span></span>

<span data-ttu-id="050b0-132">サンプル Unity アプリには、QR コードに holographic 二乗と、関連するデータ (GUID、物理サイズ、タイムスタンプ、デコードされたデータなど) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="050b0-132">There is a sample Unity app that displays a holographic square over QR codes, along with the associated data such as GUID, physical size, timestamp, and decoded data.</span></span> <span data-ttu-id="050b0-133">このアプリは、にあり https://github.com/chgatla-microsoft/QRTracking/tree/master/SampleQRCodes ます。</span><span class="sxs-lookup"><span data-stu-id="050b0-133">This app can be located at https://github.com/chgatla-microsoft/QRTracking/tree/master/SampleQRCodes.</span></span>

### <a name="detecting-qr-codes-in-c"></a><span data-ttu-id="050b0-134">C++ での QR コードの検出</span><span class="sxs-lookup"><span data-stu-id="050b0-134">Detecting QR codes in C++</span></span>

```cpp
using namespace winrt::Windows::Foundation;
using namespace winrt::Microsoft::MixedReality::QR;

class QRListHelper
{
public:
    QRListHelper(MyApplication& app) :
        m_app(app)
    {}

    IAsyncAction SetUpQRCodes()
    {
        if (QRCodeWatcher::IsSupported())
        {
            QRCodeWatcherAccessStatus status = co_await QRCodeWatcher::RequestAccessAsync();
            InitializeQR(status);
        }
    }

private:
    void OnAddedQRCode(const IInspectable&, const QRCodeAddedEventArgs& args)
    {
        m_app.OnAddedQRCode(args);
    }

    void OnUpdatedQRCode(const IInspectable&, const QRCodeUpdatedEventArgs& args)
    {
        m_app.OnUpdatedQRCode(args);
    }

    void OnEnumerationComplete(const IInspectable&, const IInspectable&)
    {
        m_app.OnEnumerationComplete();
    }

    MyApplication& m_app;
    QRCodeWatcher m_qrWatcher{ nullptr };

    void InitializeQR(QRCodeWatcherAccessStatus status)
    {
        if (status == QRCodeWatcherAccessStatus::Allowed)
        {
            m_qrWatcher = QRCodeWatcher();
            m_qrWatcher.Added({ this, &QRListHelper::OnAddedQRCode });
            m_qrWatcher.Updated({ this, &QRListHelper::OnUpdatedQRCode });
            m_qrWatcher.EnumerationCompleted({ this, &QRListHelper::OnEnumerationComplete });
            m_qrWatcher.Start();
        }
        else
        {
            // Permission denied by system or user
            // Handle the failures
        }
    }
};
```

## <a name="getting-the-coordinate-system-for-a-qr-code"></a><span data-ttu-id="050b0-135">QR コードの座標系を取得する</span><span class="sxs-lookup"><span data-stu-id="050b0-135">Getting the coordinate system for a QR code</span></span>

<span data-ttu-id="050b0-136">検出された各 QR コードは、次に示すように、左上の高速検出四角形の左上隅にある QR コードに一致する[空間座標システム](coordinate-systems.md)を公開します。</span><span class="sxs-lookup"><span data-stu-id="050b0-136">Each detected QR code exposes a [spatial coordinate system](coordinate-systems.md) aligned with the QR code at the top left corner of the fast detection square in the top left as seen below.</span></span>  <span data-ttu-id="050b0-137">QR SDK を直接使用している場合、Z 軸は用紙を指しています (図には示されていません)。 Unity 座標に変換されると、Z 軸は用紙から外れ、左手で示されます。</span><span class="sxs-lookup"><span data-stu-id="050b0-137">When directly using the QR SDK, the Z-axis is pointing into the paper (not shown) - when converted into Unity coordinates, the Z-axis points out of the paper and is left-handed.</span></span>

<span data-ttu-id="050b0-138">QR コードの SpatialCoordinateSystem は、示されているように配置されます。</span><span class="sxs-lookup"><span data-stu-id="050b0-138">A QR code's SpatialCoordinateSystem aligns as shown.</span></span> <span data-ttu-id="050b0-139">この座標系は、 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.createcoordinatesystemfornode" target="_blank">SpatialGraphInteropPreview:: CreateCoordinateSystemForNode</a>を呼び出し、コードの SpatialGraphNodeId を渡すことによって、プラットフォームから取得できます。</span><span class="sxs-lookup"><span data-stu-id="050b0-139">This coordinate system can be obtained from the platform by calling <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.createcoordinatesystemfornode" target="_blank">SpatialGraphInteropPreview::CreateCoordinateSystemForNode</a> and passing in the code's SpatialGraphNodeId.</span></span>

![QR コードの座標系](images/Qr-coordinatesystem.png) 

<span data-ttu-id="050b0-141">QRCode オブジェクトの場合、次の C++ コードは、QR コードの座標系を使用して、四角形を作成して配置する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="050b0-141">For a QRCode object, the following C++ code shows how to create a rectangle and place it using the QR code's coordinate system:</span></span>

```cpp
// Creates a 2D rectangle in the x-y plane, with the specified properties.
std::vector<float3> MyApplication::CreateRectangle(float width, float height)
{
    std::vector<float3> vertices(4);

    vertices[0] = { 0, 0, 0 };
    vertices[1] = { width, 0, 0 };
    vertices[2] = { width, height, 0 };
    vertices[3] = { 0, height, 0 };

    return vertices;
}
```

<span data-ttu-id="050b0-142">次のように、物理的なサイズを使用して QR 四角形を作成できます。</span><span class="sxs-lookup"><span data-stu-id="050b0-142">You can use the physical size to create the QR rectangle:</span></span>

```cpp
std::vector<float3> qrVertices = CreateRectangle(code.PhysicalSideLength(), code.PhysicalSideLength()); 
```

<span data-ttu-id="050b0-143">座標系は、QR コードを描画したり、場所にホログラムをアタッチしたりするために使用できます。</span><span class="sxs-lookup"><span data-stu-id="050b0-143">The coordinate system can be used to draw the QR code or attach holograms to the location:</span></span>

```cpp
using namespace winrt::Windows::Perception::Spatial;
using namespace winrt::Windows::Perception::Spatial::Preview;
SpatialCoordinateSystem qrCoordinateSystem = SpatialGraphInteropPreview::CreateCoordinateSystemForNode(code.SpatialGraphNodeId());
```

<span data-ttu-id="050b0-144">*QRCodeAddedHandler*は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="050b0-144">Altogether, your *QRCodeAddedHandler* may look something like this:</span></span>

```cpp
void MyApplication::OnAddedQRCode(const QRCodeAddedEventArgs& args)
{
    QRCode code = args.Code();
    std::vector<float3> qrVertices = CreateRectangle(code.PhysicalSideLength(), code.PhysicalSideLength());
    std::vector<unsigned short> qrCodeIndices = TriangulatePoints(qrVertices);
    XMFLOAT3 qrAreaColor = XMFLOAT3(DirectX::Colors::Aqua);

    SpatialCoordinateSystem qrCoordinateSystem = SpatialGraphInteropPreview::CreateCoordinateSystemForNode(code.SpatialGraphNodeId());
    std::shared_ptr<SceneObject> m_qrShape =
        std::make_shared<SceneObject>(
            m_deviceResources,
            qrVertices,
            qrCodeIndices,
            qrAreaColor,
            qrCoordinateSystem);

    m_sceneController->AddSceneObject(m_qrShape);
}
```

## <a name="best-practices-for-qr-code-detection"></a><span data-ttu-id="050b0-145">QR コードの検出のベストプラクティス</span><span class="sxs-lookup"><span data-stu-id="050b0-145">Best practices for QR code detection</span></span>

### <a name="quiet-zones-around-qr-codes"></a><span data-ttu-id="050b0-146">QR コードに関する非表示のゾーン</span><span class="sxs-lookup"><span data-stu-id="050b0-146">Quiet zones around QR Codes</span></span>

<span data-ttu-id="050b0-147">QR コードを正しく読み取るには、コードのすべての辺の周りに余白が必要です。</span><span class="sxs-lookup"><span data-stu-id="050b0-147">To be read correctly, QR codes require a margin around all sides of the code.</span></span> <span data-ttu-id="050b0-148">この余白には、印刷されたコンテンツを含めることはできません。また、4つのモジュール (コード内の1つの黒い四角形) にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="050b0-148">This margin must not contain any printed content and should be four modules (a single black square in the code) wide.</span></span> 

<span data-ttu-id="050b0-149">[QR 仕様](https://www.qrcode.com/en/howto/code.html)には、非表示ゾーンに関する詳細情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="050b0-149">The [QR spec](https://www.qrcode.com/en/howto/code.html) contains more information about quiet zones.</span></span>

### <a name="lighting-and-backdrop"></a><span data-ttu-id="050b0-150">照明と背景</span><span class="sxs-lookup"><span data-stu-id="050b0-150">Lighting and backdrop</span></span>
<span data-ttu-id="050b0-151">QR コード検出の品質は、さまざまな照明と背景に影響します。</span><span class="sxs-lookup"><span data-stu-id="050b0-151">QR code detection quality is susceptible to varying illumination and backdrop.</span></span> 

<span data-ttu-id="050b0-152">特に明るい照明を持つシーンでは、グレーの背景に黒のコードを印刷します。</span><span class="sxs-lookup"><span data-stu-id="050b0-152">In a scene with particularly bright lighting, print a code that is black on a gray background.</span></span> <span data-ttu-id="050b0-153">それ以外の場合は、黒の QR コードを白い背景に印刷します。</span><span class="sxs-lookup"><span data-stu-id="050b0-153">Otherwise, print a black QR code on a white background.</span></span>

<span data-ttu-id="050b0-154">コードの背景が特に暗い場合は、検出率が低い場合はグレーのコードで黒を試してみてください。</span><span class="sxs-lookup"><span data-stu-id="050b0-154">If the backdrop to the code is particularly dark, try a black on gray code if your detection rate is low.</span></span> <span data-ttu-id="050b0-155">背景が比較的薄い場合は、通常のコードが正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="050b0-155">If the backdrop is relatively light, a regular code should work fine.</span></span>

### <a name="size-of-qr-codes"></a><span data-ttu-id="050b0-156">QR コードのサイズ</span><span class="sxs-lookup"><span data-stu-id="050b0-156">Size of QR codes</span></span>
<span data-ttu-id="050b0-157">Windows Mixed Reality デバイスは、それぞれ 5 cm 未満の QR コードでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="050b0-157">Windows Mixed Reality devices do not work with QR codes with sides smaller than 5 cm each.</span></span>

<span data-ttu-id="050b0-158">5から 10 cm の長さの辺までの QR コードの場合、コードを検出するには非常に近い必要があります。</span><span class="sxs-lookup"><span data-stu-id="050b0-158">For QR codes between 5 and 10 cm length sides, you must be fairly close to detect the code.</span></span> <span data-ttu-id="050b0-159">また、このサイズでコードを検出するのにも時間がかかります。</span><span class="sxs-lookup"><span data-stu-id="050b0-159">It will also take longer to detect codes at this size.</span></span> 

<span data-ttu-id="050b0-160">コードを正確に検出するための正確な時間は、QR コードのサイズだけでなく、コードから離れた場所までの距離に依存します。</span><span class="sxs-lookup"><span data-stu-id="050b0-160">The exact time to detect codes depends not only on the size of the QR codes, but how far you are away from the code.</span></span> <span data-ttu-id="050b0-161">コードに近づけると、サイズの問題を相殺するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="050b0-161">Moving closer to the code will help offset issues with size.</span></span>

### <a name="distance-and-angular-position-from-the-qr-code"></a><span data-ttu-id="050b0-162">QR コードからの距離と角度の位置</span><span class="sxs-lookup"><span data-stu-id="050b0-162">Distance and angular position from the QR code</span></span>
<span data-ttu-id="050b0-163">追跡カメラは、特定のレベルの詳細のみを検出できます。</span><span class="sxs-lookup"><span data-stu-id="050b0-163">The tracking cameras can only detect a certain level of detail.</span></span> <span data-ttu-id="050b0-164">実際に小さいコードの場合は、< 10cm を横に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="050b0-164">For really small codes - < 10cm along the sides - you must be fairly close.</span></span> <span data-ttu-id="050b0-165">バージョン1の QR コードが 10 ~ 25 cm 幅を超える場合、最小検出距離は0.15 メートルから0.5 メートルの範囲内です。</span><span class="sxs-lookup"><span data-stu-id="050b0-165">For a version 1 QR code varying from 10 to 25 cm wide, the minimum detection distance ranges from 0.15 meters to 0.5 meters.</span></span> 

<span data-ttu-id="050b0-166">サイズの検出距離は直線的に増加します。</span><span class="sxs-lookup"><span data-stu-id="050b0-166">The detection distance for size increases linearly.</span></span> 

<span data-ttu-id="050b0-167">QR 検出は、角度の範囲 (+ = 45deg) で動作します。</span><span class="sxs-lookup"><span data-stu-id="050b0-167">QR detection works with a range of angles += 45deg.</span></span> <span data-ttu-id="050b0-168">これは、コードを検出するための適切な解決策があることを確認するためのものです。</span><span class="sxs-lookup"><span data-stu-id="050b0-168">This is to ensure we have proper resolution to detect the code.</span></span>

### <a name="qr-codes-with-logos"></a><span data-ttu-id="050b0-169">ロゴ付き QR コード</span><span class="sxs-lookup"><span data-stu-id="050b0-169">QR codes with logos</span></span>
<span data-ttu-id="050b0-170">ロゴ付きの QR コードはテストされていないため、現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="050b0-170">QR codes with logos have not been tested and are currently unsupported.</span></span>

### <a name="managing-qr-code-data"></a><span data-ttu-id="050b0-171">QR コードデータの管理</span><span class="sxs-lookup"><span data-stu-id="050b0-171">Managing QR code data</span></span>
<span data-ttu-id="050b0-172">Windows Mixed Reality デバイスは、ドライバーのシステムレベルで QR コードを検出します。</span><span class="sxs-lookup"><span data-stu-id="050b0-172">Windows Mixed Reality devices detect QR codes at the system level in the driver.</span></span> <span data-ttu-id="050b0-173">デバイスが再起動されると、検出された QR コードは失われ、次に新しいオブジェクトとして再検出されます。</span><span class="sxs-lookup"><span data-stu-id="050b0-173">When the device is rebooted, the detected QR codes are gone and will be re-detected as new objects next time.</span></span>

<span data-ttu-id="050b0-174">特定のタイムスタンプよりも古い QR コードを無視するようにアプリを構成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="050b0-174">It is recommended to configure your app to ignore QR codes older than a specific timestamp.</span></span> <span data-ttu-id="050b0-175">現時点では、API は QR コード履歴のクリアをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="050b0-175">Currently, the API does not support clearing QR code history.</span></span>

### <a name="qr-code-placement-in-a-space"></a><span data-ttu-id="050b0-176">スペースでの QR コードの配置</span><span class="sxs-lookup"><span data-stu-id="050b0-176">QR code placement in a space</span></span>
<span data-ttu-id="050b0-177">QR コードを配置する場所と方法に関する推奨事項については、「 [HoloLens の環境に関する考慮事項](environment-considerations-for-hololens.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="050b0-177">For recommendations on where and how to place QR codes, please refer to [Environment considerations for HoloLens](environment-considerations-for-hololens.md).</span></span>

## <a name="qr-api-reference"></a><span data-ttu-id="050b0-178">QR API リファレンス</span><span class="sxs-lookup"><span data-stu-id="050b0-178">QR API reference</span></span>

```cs
namespace Microsoft.MixedReality.QR
{
    /// <summary>
    /// Represents a detected QR code.
    /// </remarks>
    public class QRCode
    {
        /// <summary>
        /// Unique id that identifies this QR code for this session.
        /// </summary>
        public Guid Id { get; }

        /// <summary>
        /// Spatial graph node id for this QR code to create a coordinate system.
        /// </summary>
        public Guid SpatialGraphNodeId { get; }

        /// <summary>
        /// Version of this QR code. Version 1-40 are regular QR codes and M1 to M4 are Micro QR code formats 1-4.
        /// </summary>
        public QRVersion Version { get; }

        /// <summary>
        /// Physical width and height of this QR code in meters.
        /// </summary>
        public float PhysicalSideLength { get; }

        /// <summary>
        /// Decoded QR code data.
        /// </summary>
        public String Data { get; }

        /// <summary>
        /// Size of the RawData of this QR code.
        /// </summary>
        public UInt32 RawDataSize { get; }

        /// <summary>
        /// Gets the error-corrected raw data bytes.
        /// Used when the platform is unable to decode the code's format,
        /// allowing your app to decode as needed.
        /// </summary>
        public void GetRawData(byte[] buffer);

        /// <summary>
        /// The last detected time in 100ns QPC ticks.
        /// </summary>
        public System.TimeSpan SystemRelativeLastDetectedTime { get; }

        /// <summary>
        /// The last detected time.
        /// </summary>
        public System.DateTimeOffset LastDetectedTime { get; }
    }

    /// <summary>
    /// Event arguments for a QRCodeWatcher's Added event.
    /// </summary>
    public class QRCodeAddedEventArgs
    {
        /// <summary>
        /// Gets the QR Code that was added
        /// </summary>
        public QRCode Code { get; }
    }

    /// <summary>
    /// Event arguments for a QRCodeWatcher's Removed event.
    /// </summary>
    public class QRCodeRemovedEventArgs
    {
        /// <summary>
        /// Gets the QR Code that was removed.
        /// </summary>
        public QRCode Code { get; }
    }

    /// <summary>
    /// Event arguments for a QRCodeWatcher's Updated event.
    /// </summary>
    public class QRCodeUpdatedEventArgs
    {
        /// <summary>
        /// Gets the QR Code that was updated.
        /// </summary>
        public QRCode Code { get; }
    }

    /// <summary>
    /// Represents the status of an access request for QR code detection.
    /// </summary>
    public enum QRCodeWatcherAccessStatus
    {
        /// <summary>
        /// The system has denied permission for the app to detect QR codes.
        /// </summary>
        DeniedBySystem = 0,
        /// <summary>
        /// The app has not declared the webcam capability in its manifest.
        /// </summary>
        NotDeclaredByApp = 1,
        /// <summary>
        /// The user has denied permission for the app to detect QR codes.
        /// </summary>
        DeniedByUser = 2,
        /// <summary>
        /// A user prompt is required to get permission to detect QR codes.
        /// </summary>
        UserPromptRequired = 3,
        /// <summary>
        /// The user has given permission to detect QR codes.
        /// </summary>
        Allowed = 4,
    }

    /// <summary>
    /// Detects QR codes in the user's environment.
    /// </summary>
    public class QRCodeWatcher
    {
        /// <summary>
        /// Gets whether QR code detection is supported on the current device.
        /// </summary>
        public static bool IsSupported();

        /// <summary>
        /// Request user consent before using QR code detection.
        /// </summary>
        public static IAsyncOperation<QRCodeWatcherAccessStatus> RequestAccessAsync();

        /// <summary>
        /// Constructs a new QRCodeWatcher.
        /// </summary>
        public QRCodeWatcher();

        /// <summary>
        /// Starts detecting QR codes.
        /// </summary>
        /// <remarks>
        /// Start should only be called once RequestAccessAsync has succeeded.
        /// Start should not be called if QR code detection is not supported.
        /// Check that IsSupported returns true before calling Start.
        /// </remarks>
        public void Start();

        /// <summary>
        /// Stops detecting QR codes.
        /// </summary>
        public void Stop();

        /// <summary>
        /// Get the list of QR codes detected.
        /// </summary>
        /// <remarks>
        /// </remarks>
        public IList<QRCode> GetList();

        /// <summary>
        /// Event representing the addition of a QR Code.
        /// </summary>
        public event EventHandler<QRCodeAddedEventArgs> Added;

        /// <summary>
        /// Event representing the removal of a QR Code.
        /// </summary>
        public event EventHandler<QRCodeRemovedEventArgs> Removed;

        /// <summary>
        /// Event representing the update of a QR Code.
        /// </summary>
        public event EventHandler<QRCodeUpdatedEventArgs> Updated;

        /// <summary>
        /// Event representing the enumeration of QR Codes completing after a Start call.
        /// </summary>
        public event EventHandler<Object> EnumerationCompleted;
    }

    /// <summary>
    /// Version info for QR codes, including Micro QR codes.
    /// </summary>
    public enum QRVersion
    {
        QR1 = 1,
        QR2 = 2,
        QR3 = 3,
        QR4 = 4,
        QR5 = 5,
        QR6 = 6,
        QR7 = 7,
        QR8 = 8,
        QR9 = 9,
        QR10 = 10,
        QR11 = 11,
        QR12 = 12,
        QR13 = 13,
        QR14 = 14,
        QR15 = 15,
        QR16 = 16,
        QR17 = 17,
        QR18 = 18,
        QR19 = 19,
        QR20 = 20,
        QR21 = 21,
        QR22 = 22,
        QR23 = 23,
        QR24 = 24,
        QR25 = 25,
        QR26 = 26,
        QR27 = 27,
        QR28 = 28,
        QR29 = 29,
        QR30 = 30,
        QR31 = 31,
        QR32 = 32,
        QR33 = 33,
        QR34 = 34,
        QR35 = 35,
        QR36 = 36,
        QR37 = 37,
        QR38 = 38,
        QR39 = 39,
        QR40 = 40,
        MicroQRM1 = 41,
        MicroQRM2 = 42,
        MicroQRM3 = 43,
        MicroQRM4 = 44,
    }
}
```

## <a name="see-also"></a><span data-ttu-id="050b0-179">関連項目</span><span class="sxs-lookup"><span data-stu-id="050b0-179">See also</span></span>
* [<span data-ttu-id="050b0-180">座標系</span><span class="sxs-lookup"><span data-stu-id="050b0-180">Coordinate systems</span></span>](coordinate-systems.md)
* <span data-ttu-id="050b0-181"><a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a></span><span class="sxs-lookup"><span data-stu-id="050b0-181"><a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a></span></span>
