---
title: Unity での座標系
description: Unity で、固定された、大規模で大規模な大規模な mixed reality エクスペリエンスを構築する方法について説明します。
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: 座標系、空間座標系、方向専用、取り付けられているスケール、拡大/縮小、室内スケール、ワールドスケール、360度、取り付けられている、室内、部屋、ワールド、スケール、位置、向き、Unity、アンカー、空間アンカー、ワールドアンカー、ワールドロック、ワールドロック、ボディロック、本体ロック、追跡損失、locatability、境界、recenter
ms.openlocfilehash: 36d74488b23587e5c89b40faf97921a10be7473b
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375769"
---
# <a name="coordinate-systems-in-unity"></a><span data-ttu-id="f9a3b-104">Unity での座標系</span><span class="sxs-lookup"><span data-stu-id="f9a3b-104">Coordinate systems in Unity</span></span>

<span data-ttu-id="f9a3b-105">Windows Mixed Reality は、大規模な[エクスペリエンス](coordinate-systems.md)スケールのアプリをサポートしています。また、向きのみのアプリや、部屋規模のアプリによって配置されたアプリを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-105">Windows Mixed Reality supports apps across a wide range of [experience scales](coordinate-systems.md), from orientation-only and seated-scale apps up through room-scale apps.</span></span> <span data-ttu-id="f9a3b-106">HoloLens では、さらに一歩進めて、世界規模のアプリを構築できます。これにより、ユーザーは5メートルを超えて、ビルのフロア全体を調べることができます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-106">On HoloLens, you can go further and build world-scale apps that let users walk beyond 5 meters, exploring an entire floor of a building and beyond.</span></span>

<span data-ttu-id="f9a3b-107">Unity で mixed reality エクスペリエンスを構築するための最初の手順は、アプリが対象とする[エクスペリエンススケール](coordinate-systems.md)を決定することです。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-107">Your first step in building a mixed reality experience in Unity is to determine which [experience scale](coordinate-systems.md) your app will target.</span></span>

## <a name="building-an-orientation-only-or-seated-scale-experience"></a><span data-ttu-id="f9a3b-108">向きのみまたは取り付けられたスケールエクスペリエンスの構築</span><span class="sxs-lookup"><span data-stu-id="f9a3b-108">Building an orientation-only or seated-scale experience</span></span>

<span data-ttu-id="f9a3b-109">**名前空間:** *unityengine. XR*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-109">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="f9a3b-110">**型:** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-110">**Type:** *XRDevice*</span></span>

<span data-ttu-id="f9a3b-111">**向きのみ**または取り付けられた**スケールエクスペリエンス**を構築するには、Unity を固定の追跡領域の種類に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-111">To build an **orientation-only** or **seated-scale experience**, you must set Unity to the Stationary tracking space type.</span></span> <span data-ttu-id="f9a3b-112">これにより、Unity のワールド座標系が、[参照の静止フレーム](coordinate-systems.md#spatial-coordinate-systems)を追跡するように設定されます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-112">This sets Unity's world coordinate system to track the [stationary frame of reference](coordinate-systems.md#spatial-coordinate-systems).</span></span> <span data-ttu-id="f9a3b-113">静止の追跡モードでは、アプリの起動時に、カメラの既定の場所 (前方が Z) の直前にあるエディターに配置されたコンテンツがユーザーの前に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-113">In the Stationary tracking mode, content placed in the editor just in front of the camera's default location (forward is -Z) will appear in front of the user when the app launches.</span></span>

```cs
XRDevice.SetTrackingSpaceType(TrackingSpaceType.Stationary);
```

<span data-ttu-id="f9a3b-114">**名前空間:** *unityengine. XR*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-114">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="f9a3b-115">**種類:** *inputtracking*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-115">**Type:** *InputTracking*</span></span>

<span data-ttu-id="f9a3b-116">360度のビデオビューアーのような純粋な**向きのみのエクスペリエンス**(位置指定更新によって錯覚が無駄になる) については、XR を設定でき[ます。InputTracking。 disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html)を true にします。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-116">For a pure **orientation-only experience** such as a 360-degree video viewer (where positional head updates would ruin the illusion), you can then set [XR.InputTracking.disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html) to true:</span></span>

```cs
InputTracking.disablePositionalTracking = true;
```

<span data-ttu-id="f9a3b-117">挿入された元の recenter を後で使用できるように、固定された**スケールエクスペリエンス**の場合は、XR を呼び出すことができ[ます。InputTracking. Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html)メソッド:</span><span class="sxs-lookup"><span data-stu-id="f9a3b-117">For a **seated-scale experience**, to let the user later recenter the seated origin, you can call the [XR.InputTracking.Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) method:</span></span>

```cs
InputTracking.Recenter();
```

## <a name="building-a-standing-scale-or-room-scale-experience"></a><span data-ttu-id="f9a3b-118">大規模または部屋規模のエクスペリエンスを構築する</span><span class="sxs-lookup"><span data-stu-id="f9a3b-118">Building a standing-scale or room-scale experience</span></span>

<span data-ttu-id="f9a3b-119">**名前空間:** *unityengine. XR*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-119">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="f9a3b-120">**型:** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-120">**Type:** *XRDevice*</span></span>

<span data-ttu-id="f9a3b-121">**大規模**または**部屋規模のエクスペリエンス**を実現するには、フロアを基準としたコンテンツを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-121">For a **standing-scale** or **room-scale experience**, you'll need to place content relative to the floor.</span></span> <span data-ttu-id="f9a3b-122">ユーザーが定義したフロアレベルのオリジンとオプションの部屋の境界を表す **[空間ステージ](coordinate-systems.md#spatial-coordinate-systems)** を使用して、ユーザーのフロアについては、最初の実行時に設定します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-122">You reason about the user's floor using the **[spatial stage](coordinate-systems.md#spatial-coordinate-systems)**, which represents the user's defined floor-level origin and optional room boundary, set up during first run.</span></span>

<span data-ttu-id="f9a3b-123">Unity が世界の座標系をフロアレベルで運用していることを確認するには、Unity を RoomScale tracking space 型に設定し、セットが成功することを確認します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-123">To ensure that Unity is operating with its world coordinate system at floor-level, you can set Unity to the RoomScale tracking space type, and ensure that the set succeeds:</span></span>

```cs
if (XRDevice.SetTrackingSpaceType(TrackingSpaceType.RoomScale))
{
    // RoomScale mode was set successfully.  App can now assume that y=0 in Unity world coordinate represents the floor.
}
else
{
    // RoomScale mode was not set successfully.  App cannot make assumptions about where the floor plane is.
}
```
* <span data-ttu-id="f9a3b-124">Settrackingspace 型によって true が返された場合、Unity は、そのワールド座標系を正常に切り替えて、[参照のステージフレーム](coordinate-systems.md#spatial-coordinate-systems)を追跡します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-124">If SetTrackingSpaceType returns true, Unity has successfully switched its world coordinate system to track the [stage frame of reference](coordinate-systems.md#spatial-coordinate-systems).</span></span>
* <span data-ttu-id="f9a3b-125">Settrackingspace 型から false が返された場合、Unity は参照のステージフレームに切り替えることができませんでした。ユーザーが環境にフロアを設定していない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-125">If SetTrackingSpaceType returns false, Unity was unable to switch to the stage frame of reference, likely because the user has not set up even a floor in their environment.</span></span> <span data-ttu-id="f9a3b-126">これは一般的ではありませんが、別の部屋にステージが設定されていて、ユーザーが新しいステージを設定せずに現在の部屋にデバイスを移動した場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-126">This is not common, but can happen if the stage was set up in a different room and the device was moved to the current room without the user setting up a new stage.</span></span>

<span data-ttu-id="f9a3b-127">アプリで RoomScale の追跡領域の種類が正常に設定されると、y = 0 平面に配置されたコンテンツがフロア上に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-127">Once your app successfully sets the RoomScale tracking space type, content placed on the y=0 plane will appear on the floor.</span></span> <span data-ttu-id="f9a3b-128">(0, 0, 0) の原点は、部屋のセットアップ中にユーザーがそこしたフロア上の特定の場所になります。これは、セットアップ中に接続されていた前方方向を表す-Z です。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-128">The origin at (0, 0, 0) will be the specific place on the floor where the user stood during room setup, with -Z representing the forward direction they were facing during setup.</span></span>

<span data-ttu-id="f9a3b-129">**名前空間:** *UNITYENGINE XR*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-129">**Namespace:** *UnityEngine.Experimental.XR*</span></span><br>
<span data-ttu-id="f9a3b-130">**型:** *境界*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-130">**Type:** *Boundary*</span></span>

<span data-ttu-id="f9a3b-131">スクリプトコードでは、TrackedArea の境界の種類を指定して、境界ポリゴンを取得するために、XR 型の TryGetGeometry メソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-131">In script code, you can then call the TryGetGeometry method on your the UnityEngine.Experimental.XR.Boundary type to get a boundary polygon, specifying a boundary type of TrackedArea.</span></span> <span data-ttu-id="f9a3b-132">ユーザーが境界を定義している場合 (頂点の一覧を取得した場合)、ユーザーに**ルームスケールエクスペリエンス**を提供するのが安全であることがわかっています。ユーザーは、作成したシーンを周囲に移動できます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-132">If the user defined a boundary (you get back a list of vertices), you know it is safe to deliver a **room-scale experience** to the user, where they can walk around the scene you create.</span></span>

<span data-ttu-id="f9a3b-133">ユーザーが境界を操作すると、境界が自動的に表示されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-133">Note that the system will automatically render the boundary when the user approaches it.</span></span> <span data-ttu-id="f9a3b-134">アプリでは、境界自体をレンダリングするためにこの多角形を使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-134">Your app does not need to use this polygon to render the boundary itself.</span></span> <span data-ttu-id="f9a3b-135">ただし、この境界多角形を使用してシーンオブジェクトをレイアウトすることで、ユーザーがテレを使用して物理的にオブジェクトに接続できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-135">However, you may choose to lay out your scene objects using this boundary polygon, to ensure the user can physically reach those objects without teleporting:</span></span>

```cs
var vertices = new List<Vector3>();
if (UnityEngine.Experimental.XR.Boundary.TryGetGeometry(vertices, Boundary.Type.TrackedArea))
{
    // Lay out your app's content within the boundary polygon, to ensure that users can reach it without teleporting.
}
```

## <a name="building-a-world-scale-experience"></a><span data-ttu-id="f9a3b-136">世界規模でのエクスペリエンスの構築</span><span class="sxs-lookup"><span data-stu-id="f9a3b-136">Building a world-scale experience</span></span>

<span data-ttu-id="f9a3b-137">**名前空間:** *UNITYENGINE. XR*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-137">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="f9a3b-138">**型:** *WorldAnchor*</span><span class="sxs-lookup"><span data-stu-id="f9a3b-138">**Type:** *WorldAnchor*</span></span>

<span data-ttu-id="f9a3b-139">ユーザーが 5 m を超えることができるようにする HoloLens の真の**ワールドスケールエクスペリエンス**では、ルームスケールエクスペリエンスに使用されるもの以外の新しい手法が必要になります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-139">For true **world-scale experiences** on HoloLens that let users wander beyond 5 meters, you'll need new techniques beyond those used for room-scale experiences.</span></span> <span data-ttu-id="f9a3b-140">使用する主な手法の1つとして、[空間アンカー](coordinate-systems.md#spatial-anchors)を作成して、ユーザーがローミングした距離に関係なく、物理的な場所にあるホログラムのクラスターを正確にロックし、[後のセッションで再びそれらのホログラムを見つける](coordinate-systems.md#spatial-anchor-persistence)ことができます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-140">One key technique you'll use is to create a [spatial anchor](coordinate-systems.md#spatial-anchors) to lock a cluster of holograms precisely in place in the physical world, regardless of how far the user has roamed, and then [find those holograms again in later sessions](coordinate-systems.md#spatial-anchor-persistence).</span></span>

<span data-ttu-id="f9a3b-141">Unity では、 **WorldAnchor** Unity コンポーネントをユーザーオブジェクトに追加することによって、空間アンカーを作成します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-141">In Unity, you create a spatial anchor by adding the **WorldAnchor** Unity component to a GameObject.</span></span>

### <a name="adding-a-world-anchor"></a><span data-ttu-id="f9a3b-142">ワールドアンカーの追加</span><span class="sxs-lookup"><span data-stu-id="f9a3b-142">Adding a World Anchor</span></span>

<span data-ttu-id="f9a3b-143">ワールドアンカーを追加するには、実際の世界に固定する変換を使用して、game オブジェクトで AddComponent<WorldAnchor>() を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-143">To add a world anchor, call AddComponent<WorldAnchor>() on the game object with the transform you want to anchor in the real world.</span></span>

```cs
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

<span data-ttu-id="f9a3b-144">以上で終わりです。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-144">That's it!</span></span> <span data-ttu-id="f9a3b-145">このゲームオブジェクトは、物理的な世界の現在の場所に固定されるようになりました。物理的な配置を確保するために、Unity のワールド座標が少し時間をかけて若干調整されていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-145">This game object will now be anchored to its current location in the physical world - you may see its Unity world coordinates adjust slightly over time to ensure that physical alignment.</span></span> <span data-ttu-id="f9a3b-146">この固定された場所を今後のアプリセッションで再び見つけるには、[永続](persistence-in-unity.md)化を使用します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-146">Use [persistence](persistence-in-unity.md) to find this anchored location again in a future app session.</span></span>

### <a name="removing-a-world-anchor"></a><span data-ttu-id="f9a3b-147">ワールドアンカーの削除</span><span class="sxs-lookup"><span data-stu-id="f9a3b-147">Removing a World Anchor</span></span>

<span data-ttu-id="f9a3b-148">他のユーザーが物理的な場所をロックし、このフレームを移動したくない場合は、ワールドアンカーコンポーネントで Destroy を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-148">If you no longer want the GameObject locked to a physical world location and don't intend on moving it this frame, then you can just call Destroy on the World Anchor component.</span></span>

```cs
Destroy(gameObject.GetComponent<WorldAnchor>());
```

<span data-ttu-id="f9a3b-149">このフレームを移動する場合は、代わりに DestroyImmediate を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-149">If you want to move the GameObject this frame, you need to call DestroyImmediate instead.</span></span>

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
```

### <a name="moving-a-world-anchored-gameobject"></a><span data-ttu-id="f9a3b-150">ワールド固定のオブジェクトの移動</span><span class="sxs-lookup"><span data-stu-id="f9a3b-150">Moving a World Anchored GameObject</span></span>

<span data-ttu-id="f9a3b-151">ワールドアンカーがある間は、このオブジェクトを移動できません。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-151">GameObject's cannot be moved while a World Anchor is on it.</span></span> <span data-ttu-id="f9a3b-152">このフレームを移動する必要がある場合は、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-152">If you need to move the GameObject this frame, you need to:</span></span>
1. <span data-ttu-id="f9a3b-153">ワールドアンカーコンポーネントを直ちに破棄する</span><span class="sxs-lookup"><span data-stu-id="f9a3b-153">DestroyImmediate the World Anchor component</span></span>
2. <span data-ttu-id="f9a3b-154">オブジェクトを移動する</span><span class="sxs-lookup"><span data-stu-id="f9a3b-154">Move the GameObject</span></span>
3. <span data-ttu-id="f9a3b-155">新しいワールドアンカーコンポーネントを、このオブジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-155">Add a new World Anchor component to the GameObject.</span></span>

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
gameObject.transform.position = new Vector3(0, 0, 2);
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

### <a name="handling-locatability-changes"></a><span data-ttu-id="f9a3b-156">Locatability の変更の処理</span><span class="sxs-lookup"><span data-stu-id="f9a3b-156">Handling Locatability Changes</span></span>

<span data-ttu-id="f9a3b-157">WorldAnchor は、ある時点で物理的な世界では特定できないことがあります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-157">A WorldAnchor may not be locatable in the physical world at a point in time.</span></span> <span data-ttu-id="f9a3b-158">このような場合、Unity は、固定されたオブジェクトの変換を更新しません。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-158">If that occurs, Unity will not be updating the transform of the anchored object.</span></span> <span data-ttu-id="f9a3b-159">これは、アプリの実行中にも変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-159">This also can change while an app is running.</span></span> <span data-ttu-id="f9a3b-160">Locatability の変更を処理できないと、オブジェクトが世界の正しい物理的な場所に表示されません。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-160">Failure to handle the change in locatability will cause the object to not appear in the correct physical location in the world.</span></span>

<span data-ttu-id="f9a3b-161">Locatability の変更について通知するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-161">To be notified about locatability changes:</span></span>
1. <span data-ttu-id="f9a3b-162">OnTrackingChanged イベントのサブスクライブ</span><span class="sxs-lookup"><span data-stu-id="f9a3b-162">Subscribe to the OnTrackingChanged event</span></span>
2. <span data-ttu-id="f9a3b-163">イベントを処理します</span><span class="sxs-lookup"><span data-stu-id="f9a3b-163">Handle the event</span></span>

<span data-ttu-id="f9a3b-164">**Ontrackingchanged**イベントは、基になる空間アンカーが、状態が "可能" から "見つからない" の間で変化するたびに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-164">The **OnTrackingChanged** event will be called whenever the underlying spatial anchor changes between a state of being locatable vs. not being locatable.</span></span>

```cs
anchor.OnTrackingChanged += Anchor_OnTrackingChanged;
```

<span data-ttu-id="f9a3b-165">次に、イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-165">Then handle the event:</span></span>

```cs
private void Anchor_OnTrackingChanged(WorldAnchor self, bool located)
{
    // This simply activates/deactivates this object and all children when tracking changes
    self.gameObject.SetActiveRecursively(located);
}
```

<span data-ttu-id="f9a3b-166">アンカーはすぐに配置されることがあります。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-166">Sometimes anchors are located immediately.</span></span> <span data-ttu-id="f9a3b-167">この場合、AddComponent<WorldAnchor>() がを返すと、アンカーのこの isLocated プロパティは true に設定されます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-167">In this case, this isLocated property of the anchor will be set to true when AddComponent<WorldAnchor>() returns.</span></span> <span data-ttu-id="f9a3b-168">その結果、OnTrackingChanged イベントはトリガーされません。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-168">As a result, the OnTrackingChanged event will not be triggered.</span></span> <span data-ttu-id="f9a3b-169">クリーンパターンでは、アンカーをアタッチした後、最初の IsLocated 状態を使用して OnTrackingChanged ハンドラーを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-169">A clean pattern would be to call your OnTrackingChanged handler with the initial IsLocated state after attaching an anchor.</span></span>

```cs
Anchor_OnTrackingChanged(anchor, anchor.isLocated);
```

## <a name="sharing-anchors-across-devices"></a><span data-ttu-id="f9a3b-170">デバイス間でのアンカーの共有</span><span class="sxs-lookup"><span data-stu-id="f9a3b-170">Sharing anchors across devices</span></span>

<span data-ttu-id="f9a3b-171"><a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure 空間アンカー</a>を使用して、ローカル WorldAnchor から持続性のあるクラウドアンカーを作成できます。これにより、アプリは複数の HoloLens、IOS、Android デバイスで検索できます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-171">You can use <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> to create a durable cloud anchor from a local WorldAnchor, which your app can then locate across multiple HoloLens, iOS and Android devices.</span></span>  <span data-ttu-id="f9a3b-172">複数のデバイスで共通の空間アンカーを共有することにより、各ユーザーは、同じ物理的な場所でそのアンカーを基準としてレンダリングされたコンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-172">By sharing a common spatial anchor across multiple devices, each user can see content rendered relative to that anchor in the same physical location.</span></span>  <span data-ttu-id="f9a3b-173">これにより、リアルタイム共有エクスペリエンスを実現できます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-173">This allows for real-time shared experiences.</span></span>

<span data-ttu-id="f9a3b-174">Unity で共有エクスペリエンスの構築を開始するには、5分間の<a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Azure 空間アンカー unity クイックスタート</a>をお試しください。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-174">To get started building shared experiences in Unity, try out the 5-minute <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Azure Spatial Anchors Unity quickstarts</a>.</span></span>

<span data-ttu-id="f9a3b-175">Azure 空間アンカーを使用して実行した後は、 <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">Unity でアンカーを作成して見つける</a>ことができます。</span><span class="sxs-lookup"><span data-stu-id="f9a3b-175">Once you're up and running with Azure Spatial Anchors, you can then <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">create and locate anchors in Unity</a>.</span></span>

## <a name="see-also"></a><span data-ttu-id="f9a3b-176">参照</span><span class="sxs-lookup"><span data-stu-id="f9a3b-176">See Also</span></span>
* [<span data-ttu-id="f9a3b-177">エクスペリエンススケール</span><span class="sxs-lookup"><span data-stu-id="f9a3b-177">Experience scales</span></span>](coordinate-systems.md#mixed-reality-experience-scales)
* [<span data-ttu-id="f9a3b-178">空間ステージ</span><span class="sxs-lookup"><span data-stu-id="f9a3b-178">Spatial stage</span></span>](coordinate-systems.md#stage-frame-of-reference)
* [<span data-ttu-id="f9a3b-179">Unity での損失の追跡</span><span class="sxs-lookup"><span data-stu-id="f9a3b-179">Tracking loss in Unity</span></span>](tracking-loss-in-unity.md)
* [<span data-ttu-id="f9a3b-180">空間アンカー</span><span class="sxs-lookup"><span data-stu-id="f9a3b-180">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="f9a3b-181">Unity の永続化</span><span class="sxs-lookup"><span data-stu-id="f9a3b-181">Persistence in Unity</span></span>](persistence-in-unity.md)
* [<span data-ttu-id="f9a3b-182">Unity での共有エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="f9a3b-182">Shared experiences in Unity</span></span>](shared-experiences-in-unity.md)
* <span data-ttu-id="f9a3b-183"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span><span class="sxs-lookup"><span data-stu-id="f9a3b-183"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span></span>
* <span data-ttu-id="f9a3b-184"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Azure 空間アンカー SDK for Unity</a></span><span class="sxs-lookup"><span data-stu-id="f9a3b-184"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Azure Spatial Anchors SDK for Unity</a></span></span>