---
title: マルチユーザー機能のチュートリアル - 3. 複数のユーザーの接続
description: このコースでは、HoloLens 2 アプリケーション内でマルチユーザー共有エクスペリエンスを実装する方法を学習します。
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: Mixed Reality、Unity、チュートリアル、Hololens
ms.localizationpriority: high
ms.openlocfilehash: 56bd4e251d11e39d5495d3fcaf4e3c5fc4e087de
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86306732"
---
# <a name="3-connecting-multiple-users"></a>3.複数のユーザーの接続

このチュートリアルでは、ライブ共有エクスペリエンスの一部として複数のユーザーを接続する方法を学習します。 チュートリアルを終えるときには、複数のデバイスでアプリを実行して、各ユーザーが他のユーザーのアバターの動きをリアルタイムで確認できるようになります。

## <a name="objectives"></a>目標

* 共有エクスペリエンスで複数のユーザーを接続する方法を学習する

## <a name="preparing-the-scene"></a>シーンの準備

このセクションでは、チュートリアルのプレハブをいくつか追加してシーンを準備します。

[Project]\(プロジェクト\) ウィンドウで、 **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.MultiUserCapabilities]**  >  **[Prefabs]\(プレハブ\)** フォルダーに移動し、次のプレハブを [Hierarchy]\(階層\) ウィンドウにドラッグしてシーンに追加します。

* **NetworkLobby** プレハブ
* **SharedPlayground** プレハブ

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section1-step1-1.png)

[Project]\(プロジェクト\) ウィンドウで、 **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.AzureSpatialAnchors]**  >  **[Prefabs]\(プレハブ\)** フォルダーに移動し、次のプレハブを [Hierarchy]\(階層\) ウィンドウにドラッグしてシーンに追加します。

* **DebugWindow** プレハブ

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section1-step1-2.png)

## <a name="creating-the-user-prefab"></a>ユーザー プレハブを作成する

このセクションでは、共有エクスペリエンスでユーザーを表すために使用されるプレハブを作成します。

### <a name="1-create-and-configure-the-user"></a>1.ユーザーの作成と構成

[Hierarchy]\(ヒエラルキー\) ウィンドウで空の領域を右クリックし、 **[Create Empty]\(空のユーザーを作成\)** を選択してシーンに空のオブジェクトを追加し、オブジェクトに「**PhotonUser**」という名前を付けて、次のように構成します。

* [Transform]\(変換\) の **[Position]\(位置\)** が、X = 0、Y = 0、Z = 0 に設定されていることを確認する

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-1.png)

[Hierarchy]\(階層\) ウィンドウで、**PhotonUser** オブジェクトを選択し、[Inspector]\(インスペクター\) ウィンドウの **[Add Component]\(コンポーネントの追加\)** ボタンを使用して **Photon User (Script)** コンポーネントを PhotonUser オブジェクトに追加します。

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-2.png)

[Inspector]\(インスペクター\) ウィンドウで、 **[Add Component]\(コンポーネントの追加\)** ボタンを使用して PhotonUser オブジェクトに **Generic Net Sync (Script)** コンポーネントを追加し、次のように構成します。

* **[Is User]\(ユーザーである\)** チェックボックスをオンにする

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-3.png)

[Inspector]\(インスペクター\) ウィンドウで、 **[Add Component]\(コンポーネントの追加\)** ボタンを使用して PhotonUser オブジェクトに **Photon View (Script)** コンポーネントを追加し、次のように構成します。

* **[Observed Components]\(観察されるコンポーネント\)** フィールドに、**Generic Net Sync (Script)** コンポーネントを割り当てる

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step1-4.png)

### <a name="2-create-the-avatar"></a>2.アバターを作成する

[Project]\(プロジェクト\) ウィンドウで、 **[Assets]\(アセット\)**  > **MRTK** > **SDK** > **StandardAssets** >  **[Materials]\(素材\)** に移動し、MRTK の素材を見つけます。

次に、[Hierarchy]\(階層\) ウィンドウで、**PhotonUser** オブジェクトを右クリックして **[3D Object]\(3D オブジェクト\)**  >  **[Sphere]\(球体\)** を選択し、PhotonUser オブジェクトの子として球体オブジェクトを作成して次のように構成します。

* [Transform]\(変換\) の **[Position]\(位置\)** が、X = 0、Y = 0、Z = 0 に設定されていることを確認する
* [Transform]\(変換\) の **[Scale]\(スケール\)** を適切なサイズに変更する。例: X = 0.15、Y = 0.15、Z = 0.15
* [MeshRenderer] > [Materials]\(素材\) > **[Element 0]\(要素 0\)** フィールドに、**MRTK_Standard_White** 素材を割り当てる

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step2-1.png)

### <a name="3-create-the-prefab"></a>3.プレハブを作成する

[Project]\(プロジェクト\) ウィンドウで **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.MultiUserCapabilities]**  >  **[Resources]\(リソース\)** フォルダーに移動します。

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step3-1.png)

[Resources]\(リソース\) フォルダーを選択したまま、[Hierarchy]\(ヒエラルキー\) ウィンドウから **PhotonUser** オブジェクトを **[Resources]\(リソース\)** フォルダーに**クリックしてドラッグ**し、PhotonUser オブジェクトをプレハブにします。

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step3-2.png)

[Hierarchy]\(ヒエラルキー\) ウィンドウで **PhotonUser** オブジェクトを右クリックし、 **[Delete]\(削除\)** を選択してシーンから削除します。

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section2-step3-3.png)

## <a name="configuring-pun-to-instantiate-the-user-prefab"></a>PUN を構成してユーザー プレハブのインスタンスを作成する

このセクションでは、前のセクションで作成した PhotonUser プレハブを使用するようにプロジェクトを構成します。

[Project]\(プロジェクト\) ウィンドウで **[Assets]\(アセット\)**  >  **[MRTK.Tutorials.MultiUserCapabilities]**  >  **[Resources]\(リソース\)** フォルダーに移動します。

[Hierarchy]\(ヒエラルキー\) ウィンドウで **NetworkLobby** オブジェクトを展開して **NetworkRoom** 子オブジェクトを選択し、[Inspector]\(インスペクター\) ウィンドウで **Photon Room (Script)** コンポーネントを探し、次のように構成します。

* **"Photon User Prefab"(Photon ユーザー プレハブ)** フィールドに、[Resources]\(リソース\) フォルダーから **PhotonUser** プレハブを割り当てる

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section3-step1-1.png)

## <a name="trying-the-experience-with-multiple-users"></a>複数のユーザーのエクスペリエンスを試す

Unity プロジェクトをビルドして HoloLens に配置してから Unity に戻り、HoloLens でアプリが実行されている間にゲーム モードに入ると、頭 (HoloLens) を動かした時に HoloLens のユーザー アバターが動くのを確認できます。

![mr-learning-sharing](images/mr-learning-sharing/sharing-03-section4-step1-1.gif)

> [!TIP]
> HoloLens 2 に Unity プロジェクトをビルドして配置する方法を再確認するには、[HoloLens 2 にアプリをビルドする](mr-learning-base-02.md#building-your-application-to-your-hololens-2)手順に関する記事を参照してください。

> [!CAUTION]
> アプリから Photon に接続する必要があるため、お使いのコンピューターまたはデバイスがインターネットに接続されていることを確認してください。

## <a name="congratulations"></a>結論

複数のユーザーが同じエクスペリエンスに接続して、互いの動きを確認できるようにプロジェクトを構成できました。 次のチュートリアルでは、オブジェクトの動きが複数のデバイスで共有されるようにする機能を実装します。

[次のチュートリアル:4.オブジェクトの動きの複数のユーザーとの共有](mr-learning-sharing-04.md)
