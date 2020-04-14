---
title: HolographicSpace を取得する
description: HolographicSpace API について説明します。これは、holographic レンダリングと空間入力の中核となる概念です。
author: mikeriches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HolographicSpace, CoreWindow, 空間入力, レンダリング, スワップチェーン, holographic フレーム, 更新ループ, ゲームループ, 参照のフレーム, locatability, サンプルコード, チュートリアル
ms.openlocfilehash: 76211c8a5394e2e296748253df4eac063841746c
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277830"
---
# <a name="getting-a-holographicspace"></a><span data-ttu-id="e44d5-104">HolographicSpace を取得する</span><span class="sxs-lookup"><span data-stu-id="e44d5-104">Getting a HolographicSpace</span></span>

<span data-ttu-id="e44d5-105"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>クラスは、holographic 世界のポータルです。</span><span class="sxs-lookup"><span data-stu-id="e44d5-105">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> class is your portal into the holographic world.</span></span> <span data-ttu-id="e44d5-106">これは、イマーシブレンダリングを制御し、カメラデータを提供し、空間の推論 Api にアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="e44d5-106">It controls immersive rendering, provides camera data, and provides access to spatial reasoning APIs.</span></span> <span data-ttu-id="e44d5-107">UWP アプリの<a href="https://docs.microsoft.com/api/windows.ui.core.corewindow" target="_blank">Corewindow</a>または Win32 アプリの HWND 用に作成します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-107">You will create one for your UWP app's <a href="https://docs.microsoft.com/api/windows.ui.core.corewindow" target="_blank">CoreWindow</a> or your Win32 app's HWND.</span></span>

## <a name="set-up-the-holographic-space"></a><span data-ttu-id="e44d5-108">Holographic space を設定する</span><span class="sxs-lookup"><span data-stu-id="e44d5-108">Set up the holographic space</span></span>

<span data-ttu-id="e44d5-109">Holographic space オブジェクトの作成は、Windows Mixed Reality アプリを作成するための最初の手順です。</span><span class="sxs-lookup"><span data-stu-id="e44d5-109">Creating the holographic space object is the first step in making your Windows Mixed Reality app.</span></span> <span data-ttu-id="e44d5-110">従来の Windows アプリは、アプリケーションビューのコアウィンドウ用に作成された Direct3D スワップチェーンにレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="e44d5-110">Traditional Windows apps render to a Direct3D swap chain created for the core window of their application view.</span></span> <span data-ttu-id="e44d5-111">このスワップチェーンは、holographic UI のスレートに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-111">This swap chain is displayed to a slate in the holographic UI.</span></span> <span data-ttu-id="e44d5-112">アプリケーションが2D スレートではなく holographic を表示するようにするには、スワップチェーンではなく、コアウィンドウの holographic 領域を作成します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-112">To make your application view holographic rather than a 2D slate, create a holographic space for its core window instead of a swap chain.</span></span> <span data-ttu-id="e44d5-113">この holographic space によって作成された holographic フレームを表示すると、アプリが全画面表示モードになります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-113">Presenting holographic frames that are created by this holographic space puts your app into full-screen rendering mode.</span></span>

<span data-ttu-id="e44d5-114">[ *Holographic DirectX 11 アプリ (ユニバーサル Windows) テンプレート*から開始](creating-a-holographic-directx-project.md)する**UWP アプリ**の場合は、appview .cpp の**setwindow**メソッドで次のコードを探します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-114">For a **UWP app** [starting from the *Holographic DirectX 11 App (Universal Windows) template*](creating-a-holographic-directx-project.md), look for this code in the **SetWindow** method in AppView.cpp:</span></span>

```cpp
m_holographicSpace = HolographicSpace::CreateForCoreWindow(window);
```

<span data-ttu-id="e44d5-115">[ *Basichologram* win32 サンプルから始まる](creating-a-holographic-directx-project.md#creating-a-win32-project) **win32 アプリ**の場合は、 **app:: CreateWindowAndHolographicSpace**で HWND を作成し、関連付けられた<a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>を作成することによって、その hwnd に変換する方法の例を確認してください。</span><span class="sxs-lookup"><span data-stu-id="e44d5-115">For a **Win32 app** [starting from the *BasicHologram* Win32 sample](creating-a-holographic-directx-project.md#creating-a-win32-project), look at **App::CreateWindowAndHolographicSpace** for an example of how to create an HWND and then convert it into an immersive HWND by creating an associated <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>:</span></span>
```cpp
void App::CreateWindowAndHolographicSpace(HINSTANCE hInstance, int nCmdShow)
{
    // Store the instance handle in our class variable.
    m_hInst = hInstance;

    // Create the window for the HolographicSpace.
    hWnd = CreateWindowW(
        m_szWindowClass, 
        m_szTitle,
        WS_VISIBLE,
        CW_USEDEFAULT, 
        0, 
        CW_USEDEFAULT, 
        0, 
        nullptr, 
        nullptr, 
        hInstance, 
        nullptr);

    if (!hWnd)
    {
        winrt::check_hresult(E_FAIL);
    }

    {
        // Use WinRT factory to create the holographic space.
        using namespace winrt::Windows::Graphics::Holographic;
        winrt::com_ptr<IHolographicSpaceInterop> holographicSpaceInterop =
            winrt::get_activation_factory<HolographicSpace, IHolographicSpaceInterop>();
        winrt::com_ptr<ABI::Windows::Graphics::Holographic::IHolographicSpace> spHolographicSpace;
        winrt::check_hresult(holographicSpaceInterop->CreateForWindow(
            hWnd, __uuidof(ABI::Windows::Graphics::Holographic::IHolographicSpace),
            winrt::put_abi(spHolographicSpace)));

        if (!spHolographicSpace)
        {
            winrt::check_hresult(E_FAIL);
        }

        // Store the holographic space.
        m_holographicSpace = spHolographicSpace.as<HolographicSpace>();
    }

    // The DeviceResources class uses the preferred DXGI adapter ID from the holographic
    // space (when available) to create a Direct3D device. The HolographicSpace
    // uses this ID3D11Device to create and manage device-based resources such as
    // swap chains.
    m_deviceResources->SetHolographicSpace(m_holographicSpace);

    // The main class uses the holographic space for updates and rendering.
    m_main->SetHolographicSpace(hWnd, m_holographicSpace);

    // Show the window. This will activate the holographic view and switch focus
    // to the app in Windows Mixed Reality.
    ShowWindow(hWnd, nCmdShow);
    UpdateWindow(hWnd);
}
```

<span data-ttu-id="e44d5-116">UWP CoreWindow または Win32 HWND の HolographicSpace を取得したので、この HolographicSpace を使用して holographic カメラの処理、座標系の作成、および holographic レンダリングを行います。</span><span class="sxs-lookup"><span data-stu-id="e44d5-116">Now that you've obtained a HolographicSpace for either your UWP CoreWindow or Win32 HWND, you'll use that HolographicSpace to handle holographic cameras, create coordinate systems and do holographic rendering.</span></span> <span data-ttu-id="e44d5-117">現在の holographic space は、DirectX テンプレート内の複数の場所で使用されます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-117">The current holographic space is used in multiple places in the DirectX template:</span></span>
* <span data-ttu-id="e44d5-118">**DeviceResources**クラスは、Direct3D デバイスを作成するために、HolographicSpace オブジェクトからいくつかの情報を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-118">The **DeviceResources** class needs to get some information from the HolographicSpace object in order to create the Direct3D device.</span></span> <span data-ttu-id="e44d5-119">これは、holographic ディスプレイに関連付けられている DXGI アダプター ID です。</span><span class="sxs-lookup"><span data-stu-id="e44d5-119">This is the DXGI adapter ID associated with the holographic display.</span></span> <span data-ttu-id="e44d5-120"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>クラスは、アプリの Direct3D 11 デバイスを使用して、デバイスベースのリソース (各 holographic カメラのバックバッファーなど) を作成し、管理します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-120">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> class uses your app's Direct3D 11 device to create and manage device-based resources, such as the back buffers for each holographic camera.</span></span> <span data-ttu-id="e44d5-121">この関数が内部で何を行っているかについては、DeviceResources にあります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-121">If you're interested in seeing what this function does under the hood, you'll find it in DeviceResources.cpp.</span></span>
* <span data-ttu-id="e44d5-122">関数**DeviceResources:: InitializeUsingHolographicSpace**は、LUID を検索してアダプターを取得する方法と、優先アダプターが指定されていない場合に既定のアダプターを選択する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="e44d5-122">The function **DeviceResources::InitializeUsingHolographicSpace** demonstrates how to obtain the adapter by looking up the LUID – and how to choose a default adapter when no preferred adapter is specified.</span></span>
* <span data-ttu-id="e44d5-123">アプリのメインクラスは、更新とレンダリングのために**Appview:: SetWindow**または**App:: CreateWindowAndHolographicSpace**の holographic 空間を使用します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-123">The app's main class uses the holographic space from **AppView::SetWindow** or **App::CreateWindowAndHolographicSpace** for updates and rendering.</span></span>

>[!NOTE]
><span data-ttu-id="e44d5-124">以下のセクションでは、holographic UWP アプリテンプレートから開始したことを前提として、 **Appview:: SetWindow**のようなテンプレートの関数名について説明していますが、表示されるコードスニペットは、uwp アプリと Win32 アプリ間でも同様に適用されます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-124">While the sections below mention function names from the template like **AppView::SetWindow** that assume that you started from the holographic UWP app template, the code snippets you see will apply equally across UWP and Win32 apps.</span></span>

<span data-ttu-id="e44d5-125">次に、 **SetHolographicSpace**が appmain クラスで担当するセットアッププロセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-125">Next, we'll dive into the setup process that **SetHolographicSpace** is responsible for in the AppMain class.</span></span>

## <a name="subscribe-to-camera-events-create-and-remove-camera-resources"></a><span data-ttu-id="e44d5-126">カメライベントのサブスクライブ、カメラリソースの作成と削除</span><span class="sxs-lookup"><span data-stu-id="e44d5-126">Subscribe to camera events, create and remove camera resources</span></span>

<span data-ttu-id="e44d5-127">アプリの holographic コンテンツは holographic 空間に存在し、シーンのさまざまなパースペクティブを表す1つ以上の holographic カメラによって表示されます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-127">Your app's holographic content lives in its holographic space, and is viewed through one or more holographic cameras which represent different perspectives on the scene.</span></span> <span data-ttu-id="e44d5-128">Holographic 領域が完成したので、holographic カメラのデータを受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-128">Now that you have the holographic space, you can receive data for holographic cameras.</span></span>

<span data-ttu-id="e44d5-129">アプリは、バックバッファーレンダーターゲットビューのように、そのカメラに固有のリソースを作成することによって**CameraAdded**イベントに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-129">Your app needs to respond to **CameraAdded** events by creating any resources that are specific to that camera, like your back buffer render target view.</span></span> <span data-ttu-id="e44d5-130">このコードは、アプリが holographic フレームを作成する前に**Appview:: SetWindow**によって呼び出される**DeviceResources:: SetHolographicSpace**関数で確認できます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-130">You can see this code in the **DeviceResources::SetHolographicSpace** function, called by **AppView::SetWindow** before the app creates any holographic frames:</span></span>

```cpp
m_cameraAddedToken = m_holographicSpace.CameraAdded(
    std::bind(&AppMain::OnCameraAdded, this, _1, _2));
```

<span data-ttu-id="e44d5-131">また、アプリは、そのカメラ用に作成されたリソースを解放することによって、 **CameraRemoved**イベントに応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-131">Your app also needs to respond to **CameraRemoved** events by releasing resources that were created for that camera.</span></span>

<span data-ttu-id="e44d5-132">**DeviceResources:: SetHolographicSpace**から:</span><span class="sxs-lookup"><span data-stu-id="e44d5-132">From **DeviceResources::SetHolographicSpace**:</span></span>

```cpp
m_cameraRemovedToken = m_holographicSpace.CameraRemoved(
    std::bind(&AppMain::OnCameraRemoved, this, _1, _2));
```

<span data-ttu-id="e44d5-133">イベントハンドラーは、holographic レンダリングを滑らかにするために何らかの作業を完了する必要があります。これにより、アプリがまったくレンダリングできるようになります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-133">The event handlers must complete some work in order to keep holographic rendering flowing smoothly, and so that your app is able to render at all.</span></span> <span data-ttu-id="e44d5-134">詳細については、コードとコメントを参照してください。 main クラスで**OnCameraAdded**と**OnCameraRemoved**を検索すると、 **DeviceResources**によって**m_cameraResources**マップがどのように処理されるかを理解できます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-134">Read the code and comments for the details: you can look for **OnCameraAdded** and **OnCameraRemoved** in your main class to understand how the **m_cameraResources** map is handled by **DeviceResources**.</span></span>

<span data-ttu-id="e44d5-135">ここでは、AppMain と、アプリが holographic カメラについて認識できるようにするためのセットアップに焦点を合わせています。</span><span class="sxs-lookup"><span data-stu-id="e44d5-135">Right now, we're focused on AppMain and the setup that it does to enable your app to know about holographic cameras.</span></span> <span data-ttu-id="e44d5-136">この点を考慮して、次の2つの要件を確認することが重要です。</span><span class="sxs-lookup"><span data-stu-id="e44d5-136">With this in mind, it's important to take note of the following two requirements:</span></span>

1. <span data-ttu-id="e44d5-137">**CameraAdded**イベントハンドラーでは、アプリを非同期に処理して、新しい holographic カメラのリソースの作成とアセットの読み込みを完了できます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-137">For the **CameraAdded** event handler, the app can work asynchronously to finish creating resources and loading assets for the new holographic camera.</span></span> <span data-ttu-id="e44d5-138">この作業を完了するために複数のフレームを使用するアプリは、遅延を要求し、非同期読み込みの後に遅延を完了する必要があります。[PPL タスク](https://docs.microsoft.com/cpp/parallel/concrt/parallel-patterns-library-ppl)は、非同期処理を実行するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-138">Apps that take more than one frame to complete this work should request a deferral, and complete the deferral after loading asynchronously; a [PPL task](https://docs.microsoft.com/cpp/parallel/concrt/parallel-patterns-library-ppl) can be used to do asynchronous work.</span></span> <span data-ttu-id="e44d5-139">アプリは、イベントハンドラーが終了したとき、または遅延が完了したときに、そのカメラにすぐにレンダリングできるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-139">Your app must ensure that it's ready to render to that camera right away when it exits the event handler, or when it completes the deferral.</span></span> <span data-ttu-id="e44d5-140">イベントハンドラーを終了するか、遅延を完了すると、そのカメラを含む holographic フレームを受信する準備ができたことがシステムに通知されます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-140">Exiting the event handler or completing the deferral tells the system that your app is now ready to receive holographic frames with that camera included.</span></span>

2. <span data-ttu-id="e44d5-141">アプリは、 **CameraRemoved**イベントを受け取ると、バックバッファーへのすべての参照を解放し、関数をすぐに終了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-141">When the app receives a **CameraRemoved** event, it must release all references to the back buffer and exit the function right away.</span></span> <span data-ttu-id="e44d5-142">これには、レンダーターゲットビューや、 [Idxgiresource](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgiresource)への参照を保持する他のリソースが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-142">This includes render target views, and any other resource that might hold a reference to the [IDXGIResource](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgiresource).</span></span> <span data-ttu-id="e44d5-143">また、 **CameraResources:: ReleaseResourcesForBackBuffer**に示されているように、アプリは、バックバッファーがレンダーターゲットとしてアタッチされていないことを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-143">The app must also ensure that the back buffer is not attached as a render target, as shown in **CameraResources::ReleaseResourcesForBackBuffer**.</span></span> <span data-ttu-id="e44d5-144">処理速度を向上させるために、アプリはバックバッファーを解放し、タスクを起動して、そのカメラを破棄するために必要な他の作業を非同期に完了させることができます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-144">To help speed things along, your app can release the back buffer and then launch a task to asynchronously complete any other work that is necessary to tear down that camera.</span></span> <span data-ttu-id="e44d5-145">Holographic アプリテンプレートには、この目的で使用できる PPL タスクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e44d5-145">The holographic app template includes a PPL task that you can use for this purpose.</span></span>

>[!NOTE]
><span data-ttu-id="e44d5-146">追加または削除されたカメラがフレームにどのように表示されるかを確認するには、 **HolographicFrame** [addedcameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.addedcameras)プロパティと[removedcameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.removedcameras)プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-146">If you want to determine when an added or removed camera shows up on the frame, use the **HolographicFrame** [AddedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.addedcameras) and [RemovedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.removedcameras) properties.</span></span>

## <a name="create-a-frame-of-reference-for-your-holographic-content"></a><span data-ttu-id="e44d5-147">Holographic コンテンツの参照のフレームを作成する</span><span class="sxs-lookup"><span data-stu-id="e44d5-147">Create a frame of reference for your holographic content</span></span>

<span data-ttu-id="e44d5-148">HolographicSpace にレンダリングするには、アプリのコンテンツが[空間座標系](coordinate-systems-in-directx.md)に配置されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-148">Your app's content must be positioned in a [spatial coordinate system](coordinate-systems-in-directx.md) to be rendered in the HolographicSpace.</span></span> <span data-ttu-id="e44d5-149">システムには、ホログラムの座標系を確立するために使用できる2つの主要な参照フレームが用意されています。</span><span class="sxs-lookup"><span data-stu-id="e44d5-149">The system provides two primary frames of reference which you can use to establish a coordinate system for your holograms.</span></span>

<span data-ttu-id="e44d5-150">Windows Holographic には、デバイスに接続されている参照フレームと、デバイスがユーザーの環境を移動するときに静止している参照フレームの2種類があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-150">There are two kinds of reference frames in Windows Holographic: reference frames attached to the device, and reference frames that remain stationary as the device moves through the user's environment.</span></span> <span data-ttu-id="e44d5-151">Holographic アプリテンプレートでは、既定で静止参照フレームが使用されます。これは、世界中にロックされているホログラムをレンダリングする最も簡単な方法の1つです。</span><span class="sxs-lookup"><span data-stu-id="e44d5-151">The holographic app template uses a stationary reference frame by default; this is one of the simplest ways to render world-locked holograms.</span></span>

<span data-ttu-id="e44d5-152">静止参照フレームは、デバイスの現在の場所の近くに位置を安定させるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="e44d5-152">Stationary reference frames are designed to stabilize positions near the device's current location.</span></span> <span data-ttu-id="e44d5-153">これは、デバイスの周囲の領域の詳細を学習するため、デバイスからさらに多くの座標がユーザーの環境に対して若干ずれられることを意味します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-153">This means that coordinates further from the device are allowed to drift slightly with respect to the user's environment as the device learns more about the space around it.</span></span> <span data-ttu-id="e44d5-154">静止した参照フレームを作成するには、[空間ステージ](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage)から座標系を取得する方法と、既定の<a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>を使用する方法の2つがあります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-154">There are two ways to create a stationary frame of reference: acquire the coordinate system from the [spatial stage](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), or use the default <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span></span> <span data-ttu-id="e44d5-155">イマーシブヘッドセット用の Windows Mixed Reality アプリを作成する場合、推奨される開始点は[空間ステージ](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage)です。これには、プレーヤーによって摩耗されたイマーシブヘッドセットの機能に関する情報も表示されます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-155">If you are creating a Windows Mixed Reality app for immersive headsets, the recommended starting point is the [spatial stage](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), which also provides information about the capabilities of the immersive headset worn by the player.</span></span> <span data-ttu-id="e44d5-156">ここでは、既定の<a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>の使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-156">Here, we show how to use the default <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span></span>

<span data-ttu-id="e44d5-157">空間ロケーターは、Windows Mixed Reality デバイスを表し、デバイスの動きを追跡し、位置に対して相対的に理解できる座標系を提供します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-157">The spatial locator represents the Windows Mixed Reality device, and tracks the motion of the device and provides coordinate systems that can be understood relative to its location.</span></span>

<span data-ttu-id="e44d5-158">**Appmain:: OnHolographicDisplayIsAvailableChanged**から:</span><span class="sxs-lookup"><span data-stu-id="e44d5-158">From **AppMain::OnHolographicDisplayIsAvailableChanged**:</span></span>

```cpp
spatialLocator = SpatialLocator::GetDefault();
```

<span data-ttu-id="e44d5-159">アプリが起動されたときに、静止参照フレームを1回作成します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-159">Create the stationary reference frame once when the app is launched.</span></span> <span data-ttu-id="e44d5-160">これは、アプリが起動されたときに原点がデバイスの位置に配置された、ワールド座標系を定義することに似ています。</span><span class="sxs-lookup"><span data-stu-id="e44d5-160">This is analogous to defining a world coordinate system, with the origin placed at the device's position when the app is launched.</span></span> <span data-ttu-id="e44d5-161">この参照フレームはデバイスと共に移動しません。</span><span class="sxs-lookup"><span data-stu-id="e44d5-161">This reference frame doesn't move with the device.</span></span>

<span data-ttu-id="e44d5-162">**Appmain:: SetHolographicSpace**から:</span><span class="sxs-lookup"><span data-stu-id="e44d5-162">From **AppMain::SetHolographicSpace**:</span></span>

```cpp
m_stationaryReferenceFrame =
    m_spatialLocator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```

<span data-ttu-id="e44d5-163">すべての参照フレームは重力に沿っています。つまり、y 軸はユーザーの環境に対して "up" を指します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-163">All reference frames are gravity aligned, meaning that the y axis points "up" with respect to the user's environment.</span></span> <span data-ttu-id="e44d5-164">Windows では "右手" 座標系が使用されるため、– z 軸の方向は、参照フレームの作成時にデバイスが接続している "前方" 方向と一致します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-164">Since Windows uses "right-handed" coordinate systems, the direction of the –z axis coincides with the "forward" direction the device is facing when the reference frame is created.</span></span>

>[!NOTE]
><span data-ttu-id="e44d5-165">アプリが個々のホログラムを正確に配置する必要がある場合は、 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a>を使用して、個々のホログラムを実際の世界の位置に固定します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-165">When your app requires precise placement of individual holograms, use a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a> to anchor the individual hologram to a position in the real world.</span></span> <span data-ttu-id="e44d5-166">たとえば、ユーザーが特別な関心のあるポイントを示す場合は、空間アンカーを使用します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-166">For example, use a spatial anchor when the user indicates a point to be of special interest.</span></span> <span data-ttu-id="e44d5-167">アンカー位置はずれませんが、調整することができます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-167">Anchor positions do not drift, but they can be adjusted.</span></span> <span data-ttu-id="e44d5-168">既定では、アンカーが調整されると、修正が行われた後、その位置が次の複数のフレームに配置されるようになります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-168">By default, when an anchor is adjusted, it eases its position into place over the next several frames after the correction has occurred.</span></span> <span data-ttu-id="e44d5-169">アプリケーションによっては、これが発生したときに、別の方法で調整を処理することが必要になる場合があります (たとえば、ホログラムが非表示になるまでは、このように遅延させます)。</span><span class="sxs-lookup"><span data-stu-id="e44d5-169">Depending on your application, when this occurs you may want to handle the adjustment in a different manner (e.g. by deferring it until the hologram is out of view).</span></span> <span data-ttu-id="e44d5-170">これらのカスタマイズは、 <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystem" target="_blank">RawCoordinateSystem</a>プロパティと<a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted" target="_blank">RawCoordinateSystemAdjusted</a>イベントによって有効になります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-170">The <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystem" target="_blank">RawCoordinateSystem</a> property and <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted" target="_blank">RawCoordinateSystemAdjusted</a> events enable these customizations.</span></span>

## <a name="respond-to-locatability-changed-events"></a><span data-ttu-id="e44d5-171">Locatability 変更イベントへの応答</span><span class="sxs-lookup"><span data-stu-id="e44d5-171">Respond to locatability changed events</span></span>

<span data-ttu-id="e44d5-172">世界中にロックされているホログラムをレンダリングするには、デバイスが世界中で検出できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-172">Rendering world-locked holograms requires the device to be able to locate itself in the world.</span></span> <span data-ttu-id="e44d5-173">これは、環境の状態が原因で常に発生するとは限りません。その場合、ユーザーは追跡の中断を視覚的に示すことが期待される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-173">This may not always be possible due to environmental conditions, and if so, the user may expect a visual indication of the tracking interruption.</span></span> <span data-ttu-id="e44d5-174">この視覚的な表示は、デバイスに接続されている参照フレームを使用して、世界に固定するのではなく、レンダリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e44d5-174">This visual indication must be rendered using reference frames attached to the device, instead of stationary to the world.</span></span>

<span data-ttu-id="e44d5-175">アプリは、何らかの理由で追跡が中断された場合に、通知を受け取るように要求できます。</span><span class="sxs-lookup"><span data-stu-id="e44d5-175">You app can request to be notified if tracking is interrupted for any reason.</span></span> <span data-ttu-id="e44d5-176">Locatの変更後のイベントに登録して、デバイスが世界中に配置されているかどうかを検出します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-176">Register for the LocatabilityChanged event to detect when the device's ability to locate itself in the world changes.</span></span> <span data-ttu-id="e44d5-177">**Appmain:: SetHolographicSpace から:**</span><span class="sxs-lookup"><span data-stu-id="e44d5-177">From **AppMain::SetHolographicSpace:**</span></span>

```cpp
m_locatabilityChangedToken = m_spatialLocator.LocatabilityChanged(
    std::bind(&HolographicApp6Main::OnLocatabilityChanged, this, _1, _2));
```

<span data-ttu-id="e44d5-178">次に、このイベントを使用して、ホログラムを世界にどのようにレンダリングするかを決定します。</span><span class="sxs-lookup"><span data-stu-id="e44d5-178">Then use this event to determine when holograms cannot be rendered stationary to the world.</span></span>

## <a name="see-also"></a><span data-ttu-id="e44d5-179">参照</span><span class="sxs-lookup"><span data-stu-id="e44d5-179">See also</span></span>
* [<span data-ttu-id="e44d5-180">DirectX でのレンダリング</span><span class="sxs-lookup"><span data-stu-id="e44d5-180">Rendering in DirectX</span></span>](rendering-in-directx.md)
* [<span data-ttu-id="e44d5-181">DirectX の座標系</span><span class="sxs-lookup"><span data-stu-id="e44d5-181">Coordinate systems in DirectX</span></span>](coordinate-systems-in-directx.md)
