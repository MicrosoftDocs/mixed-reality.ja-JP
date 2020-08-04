---
title: 入門チュートリアル - 8. 視線追跡の使用
description: このコースでは、Mixed Reality Toolkit (MRTK) を使用して複合現実のアプリケーションを作成する方法について説明します。
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: 31552cba9a68d1f1214395dbf4e4ed84ecd3f388
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376604"
---
# <a name="8-using-eye-tracking"></a>8.視線追跡の使用

## <a name="overview"></a>概要

このチュートリアルでは、HoloLens 2 の視線追跡を有効にし、視線追跡をオブジェクトに追加して、ユーザーがオブジェクトを見たときにアクションをトリガーする方法について説明します。

> [!NOTE]
> このプロジェクトを HoloLens (第 1 世代) にもデプロイする場合、視線追跡は HoloLens 2 でのみサポートされることに注意してください。

## <a name="objectives"></a>目標

* HoleLens 2 の視線追跡を有効にする方法を学習する
* 視線追跡を使用してアクションをトリガーする方法を学習する

## <a name="ensuring-the-eye-gaze-input-capability-is-enabled"></a>視線入力機能を確実に有効にする

[Unity] メニューで、[Mixed Reality Toolkit] > [ユーティリティ] > **[Configure Unity Project]\(Unity プロジェクトの構成\)** の順に選択して **[MRTK Project Configurator]** ウィンドウを開き、 **[UWP Capabilities]\(UWP 機能\)** セクションで **[Enable Eye Gaze Input Capability]\(視線入力機能を有効にする\)** がグレーで表示されていることを確認します。

![mr-learning-base](images/mr-learning-base/base-08-section1-step1-1.png)

> [!NOTE]
> 視線入力機能は、このチュートリアル シリーズの冒頭で Unity プロジェクトを構成したときに、[MRTK Project Configurator 設定を適用する](mr-learning-base-02.md#1-apply-the-mrtk-project-configurator-settings)手順で有効にする必要がありました。 しかし、有効にしていない場合は、ここで必ず有効にしてください。

## <a name="enabling-eye-based-gaze-in-the-gaze-provider"></a>Gaze Provider で目の動きに基づく視線入力を有効にする

[Hierarchy]\(階層\) ウィンドウで **[MixedRealityToolkit]** オブジェクトを選択し、[Inspector]\(インスペクター\) ウィンドウで [MixedRealityToolkit] > **[入力]** タブの順に選択して、次の手順を実行します。

* **DefaultHoloLens2InputSystemProfile** をクローンし、適切な名前 (たとえば、_GettingStarted_HoloLens2InputSystemProfile_) を付けます
* **[ポインター]** セクションを展開します
* **DefaultMixedRealityPointerProfile** をクローンし、適切な名前 (たとえば、_GettingStarted_MixedRealityPointerProfile_) を付けます
* **[Gaze Settings]\(視線入力の設定\)** セクションを見つけて、 **[Is Eye Tracking Enabled]\(視線追跡を有効にする\)** チェックボックスをオンにします

![mr-learning-base](images/mr-learning-base/base-08-section2-step1-1.png)

> [!TIP]
> MRTK プロファイルをクローンする方法については、[MRTK プロファイルの構成](mr-learning-base-03.md)に関するページにある手順を参照してください。

## <a name="enabling-simulated-eye-tracking-for-the-unity-editor"></a>Unity エディターの視線追跡シミュレーションを有効にする

[Hierarchy]\(階層\) ウィンドウで **[MixedRealityToolkit]** オブジェクトを選択し、[Inspector]\(インスペクター\) ウィンドウで **[入力]** タブの順に選択して、次の手順を実行します。

* **[Input Data Providers]\(入力データ プロバイダー\)**  >  **[Input Simulation Service]\(入力シミュレーション サービス\)** セクションの順に展開します
* **DefaultMixedRealityInputSimulationProfile** をクローンし、適切な名前 (たとえば、_GettingStarted_MixedRealityInputSimulationProfile_) を付けます
* **[Eye Simulation]\(視線シミュレーション\)** セクションを見つけて、 **[Simulate Eye Position]\(目の位置のシミュレーション\)** チェックボックスをオンにします

![mr-learning-base](images/mr-learning-base/base-08-section3-step1-1.png)

## <a name="adding-eye-tracking-to-objects"></a>視線追跡をオブジェクトに追加する

[Hierarchy]\(階層\) ウィンドウで、[RoverExplorer] > **[ボタン]** オブジェクトの順に展開し、3 つの子ボタン オブジェクトのそれぞれについて、[SeeItSayItLabel] > **[TextMeshPro]** オブジェクトの順に選択します。

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-1.png)

[Inspector]\(インスペクター\) ウィンドウで 3 つの TextMeshPro オブジェクトが選択されたままの状態で、 **[Add Component]\(コンポーネントの追加\)** ボタンを使用して、選択されたすべてのオブジェクトに次のコンポーネントを追加します。

* **Box Collider** コンポーネント
* **EyeTrackingTarget** コンポーネント

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-2.png)

[Hierarchy]\(階層\) ウィンドウで、 **[ヒント]** > [SeeItSayItLabel] > **TextMeshPro** オブジェクトの順に選択し、**EyeTrackingTarget** コンポーネントを次のように構成します。

* **On Look At Start ()** イベント セクション内
  * 小さい **[+]** アイコンをクリックして、別のイベントを追加します
  * オブジェクト自体、つまり同じ **TextMeshPro** オブジェクトを **[None (Object)]\(なし (オブジェクト)\)** フィールドに割り当てます
  * **[No Function]\(関数なし\)** ドロップダウンから、 **[TextMeshPro]**  >  **[float fontSize]** の順に選択し、イベントがトリガーされたときにこのプロパティ値を更新するようにします
  * 引数を **0.06**に設定して、現在のフォント サイズ 0.04 を 50% 増加します
* **On Look Away ()** イベント セクション内
  * 小さい **[+]** アイコンをクリックして、別のイベントを追加します
  * オブジェクト自体、つまり同じ **TextMeshPro** オブジェクトを **[None (Object)]\(なし (オブジェクト)\)** フィールドに割り当てます
  * **[No Function]\(関数なし\)** ドロップダウンから、 **[TextMeshPro]**  >  **[float fontSize]** の順に選択し、イベントがトリガーされたときにこのプロパティ値を更新するようにします
  * 引数を **0.04** に設定し、フォント サイズを 0.04 に戻します

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-3.png)

**[Explode]\(展開\)** > [SeeItSayItLabel] > **[TextMeshPro]** オブジェクトと **[リセット]** > [SeeItSayItLabel] > **[TextMeshPro]** オブジェクトに対して、この手順を**繰り返し**ます。

ここで、ゲーム モードに入り、マウスの右ボタンを押したまま、視線がラベルの 1 つをヒットするまでマウスを移動すると、フォント サイズが 50% 増加され、視線が離れると元のサイズに戻ることを確認できます。

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-4.png)

## <a name="congratulations"></a>結論

このチュートリアルでは、HoloLens 2 の視線追跡を有効にし、視線追跡をオブジェクトに追加して、ユーザーがオブジェクトを見たときにアクションをトリガーする方法を学習しました。

[次のチュートリアル:9.音声コマンドの使用](mr-learning-base-09.md)