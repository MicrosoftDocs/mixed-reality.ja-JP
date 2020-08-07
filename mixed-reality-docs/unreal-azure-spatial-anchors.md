---
title: Unreal での Azure Spatial Anchors
description: Unreal エンジンでの Azure 空間アンカーの作成に関する概要です。
author: hferrone
services: azure-spatial-anchors
ms.author: v-haferr
ms.date: 07/01/2020
ms.topic: tutorial
ms.service: azure-spatial-anchors
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens 2, Azure, Azure 開発, Spatial Anchors, Mixed Reality, 開発, 機能, 新しいプロジェクト, エミュレーター, ドキュメント, ガイド, ホログラム, ゲーム開発
ms.openlocfilehash: c7189407bea4b38e7305f0dda7637b82d3325704
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87377347"
---
# <a name="azure-spatial-anchors-in-unreal"></a>Unreal での Azure Spatial Anchors

## <a name="overview"></a>概要

Azure Spatial Anchors は、現実世界のアンカー ポイントを拡張現実デバイスを使って検出、共有、永続化できるようにする Microsoft Mixed Reality サービスです。 このドキュメントでは、Azure Spatial Anchors サービスを Unreal プロジェクトに統合する方法について説明します。 さらに情報が必要な場合は、[Azure Spatial Anchors サービス](https://azure.microsoft.com/services/spatial-anchors/)に関するページを参照してください。

> [!IMPORTANT]
> ローカル アンカーはデバイスに格納されますが、Azure 空間アンカーはクラウドに格納されます。 アンカーをデバイスにローカルに格納することをご希望の場合は、[ローカル空間アンカー](unreal-spatial-anchors.md)のドキュメントにその手順が説明されています。 また、ローカル アンカーと Azure のアンカーは、競合することなく同じプロジェクトで使用できます。

## <a name="prerequisites"></a>前提条件

このガイドを完了するには、次のことが必要です。

- インストール済みの [Unreal バージョン 4.25](https://www.unrealengine.com/get-now) 以降
- Unreal にセットアップされた [HoloLens 2 プロジェクト](unreal-uxt-ch1.md) 
- 「[Azure Spatial Anchors の概要](https://docs.microsoft.com/azure/spatial-anchors/overview)」の確認
- C++ と Unreal に関する基本的な知識

## <a name="getting-azure-spatial-anchors-account-info"></a>Azure Spatial Anchors アカウント情報を取得する

プロジェクトで Azure Spatial Anchors を使用する前に、次のことを行う必要があります。
* [Spatial Anchors リソースを作成](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens#create-a-spatial-anchors-resource)し、次に示すアカウント フィールドをコピーします。 これらの値は、アプリケーションのアカウントでユーザーを認証するために使用されます。
    * **アカウント ID**
    * **アカウント キー**

詳細については、[Azure Spatial Anchors の認証](https://docs.microsoft.com/azure/spatial-anchors/concepts/authentication?tabs=csharp)に関するドキュメントを参照してください。

> [!NOTE]
> Unreal 4.25 での Azure Spatial Anchors では、Azure AD 認証トークンがサポートされていませんが、この機能のサポートは今後のリリースで導入される予定です。

## <a name="adding-azure-spatial-anchors-plugins"></a>Azure Spatial Anchors プラグインを追加する

Azure Spatial Anchors プラグインを、次のようにして、Unreal エディターで有効にします。
1. **[編集] > [プラグイン]** の順にクリックし、**AzureSpatialAnchors** と **AzureSpatialAnchorsForWMR** を検索します。
2. 両方のプラグインの **[有効]** チェックボックスをオンにして、アプリケーションの Azure Spatial Anchors ブループリント ライブラリへのアクセスを許可します。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-01.png)

完了したら、プラグインの変更を有効にするために、Unreal エディターを再起動します。 これで、プロジェクトで Azure Spatial Anchors を使用する準備ができました。

## <a name="starting-a-spatial-anchors-session"></a>Spatial Anchors セッションを開始する
Azure Spatial Anchors セッションを使用すると、クライアント アプリケーションが Azure Spatial Anchors サービスと通信できるようになります。 Azure 空間アンカーの作成、永続化、共有には、Azure Spatial Anchors セッションを作成して開始する必要があります。

1. アプリケーションで使用しているポーンのブループリントを開きます。
2. **[アカウント ID]** と **[アカウント キー]** 用に 2 つの文字列変数を追加し、Azure Spatial Anchors アカウントから対応する値を割り当てて、セッションを認証します。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-02.png)

次の手順で、Azure Spatial Anchors セッションを開始します。
1. **AR セッション**が HoloLens アプリケーションで実行されていることを確認します。これは、AR セッションが実行されていないと、Azure Spatial Anchors セッションを開始できないからです。 セットアップされているものがない場合は、[AR セッション資産を作成](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch3#adding-the-session-asset)します。
2. **Start Azure Spatial Anchors Session** カスタム イベントを追加し、次のスクリーンショットに示すように構成します。
    * セッションを作成しても、既定ではセッションは開始されません。このため、開発者は Azure Spatial Anchors サービスでの認証用にそのセッションを構成できます。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-03.png)

3. Azure Spatial Anchors セッションを構成して、 **[アカウント ID]** と **[アカウント キー]** を指定します。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-04.png)

4. Azure Spatial Anchors セッションを開始し、アプリケーションで Azure 空間アンカーを作成して配置できるようにします。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-05.png)

サービスを使用しなくなった場合は、イベント グラフ ブループリントの Azure Spatial Anchors リソースをクリーンアップすることをお勧めします。

1. その Azure Spatial Anchors セッションを停止します。 そのセッションは実行されなくなりますが、関連付けられているリソースは Azure Spatial Anchors プラグインにまだ存在しています。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-06.png)

2. Azure Spatial Anchors セッションを破棄して、その Azure Spatial Anchors プラグインでまだ認識されている Azure Spatial Anchors セッション リソースをクリーンアップします。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-07.png)

イベント グラフ ブループリントは、次のスクリーンショットのようになります。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-08.png)


## <a name="creating-an-anchor"></a>アンカーを作成する
Azure 空間アンカーは、拡張現実アプリケーション空間における現実世界のポーズを表します。これにより、拡張現実コンテンツが現実世界の場所に固定されます。 Azure 空間アンカーは、異なるユーザー間で共有することもできます。 この共有により、異なるデバイス上に描画される拡張現実コンテンツを、現実世界の同一の場所に配置することが可能になります。 

新しい Azure 空間アンカーを作成するには:
1. Azure Spatial Anchors セッションが実行されていることを確認します。 Azure Spatial Anchors セッションが 1 つも実行されていない場合、アプリケーションは Azure 空間アンカーの作成や永続化を行えません。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-09.png)

2. Unreal **[Scene コンポーネント](https://docs.unrealengine.com/API/Runtime/Engine/Components/USceneComponent/index.html)** を作成または取得します。これは、場所が永続化されている必要があります。 
    * 次の図では、**Scene Component Needing Anchor** コンポーネントが変数として使用されています。 Unreal Scene コンポーネントは、[AR ピン](https://docs.unrealengine.com/BlueprintAPI/HoloLensAR/ARPin/index.html)と Azure 空間アンカーのためのアプリケーション ワールド変換を確立するために必要です。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-10.png)

Unreal Scene コンポーネント用の Azure 空間アンカーを構築して保存するには:
1. Unreal Scene コンポーネントの [Pin コンポーネント](https://docs.unrealengine.com/BlueprintAPI/ARAugmentedReality/Pin/PinComponent/index.html)を呼び出し、Scene コンポーネントの **World Transform** を AR ピンで使用するワールド トランスフォームとして指定します。
    * Unreal は、AR ピンを使用してアプリケーション空間内の AR ポイントを追跡します。これは、Azure 空間アンカーを作成するために使用されます。 Unreal では、AR ピンは HoloLens の SpatialAnchor に似ています。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-11.png)

2. 新しく作成した AR ピンを使用して、**Create Cloud Anchor** を呼び出します。
    * Create Cloud Anchor では、Azure Spatial Anchors サービス内ではなく、ローカルに Azure 空間アンカーが作成されます。 Azure 空間アンカーの有効期限などのパラメーターは、サービスを使用して Azure 空間アンカーを作成する前に設定できます。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-12.png)

3. Azure 空間アンカーの有効期限を設定します。 開発者は、この関数の Lifetime パラメーターを使用して、アンカーがサービスによって維持される期間を秒単位で指定できます。
    * たとえば、有効期限を 1 週間とする場合、60 秒 x 60 分 x 24 時間 x 7 日で、604,800 秒と指定します。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-13.png)

アンカーのパラメーターを設定したら、アンカーの保存準備ができたことを宣言します。 次の例では、新しく作成した Azure 空間アンカーが、保存が必要な一連の Azure 空間アンカーに追加されています。 このセットは、ポーン ブループリントの変数として宣言されています。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-14.png)

## <a name="saving-an-anchor"></a>アンカーを保存する

パラメーターを指定して Azure 空間アンカーを構成したら、**Save Cloud Anchor** を呼び出します。 Save Cloud Anchor では、Azure Spatial Anchors サービスにそのアンカーが宣言されます。 Save Cloud Anchor への呼び出しが成功すると、Azure 空間アンカーは、その Azure Spatial Anchors サービスの他のユーザーにも使用できるようになります。  

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-15.png)

> [!NOTE]
> Save Cloud Anchor は非同期関数で、**EventTick** などのゲーム スレッド イベントでのみ呼び出すことができます。 Save Cloud Anchor は、カスタムのブループリント関数では、使用可能なブループリント関数として表示されない場合があります。 ただし、ポーン イベント グラフ ブループリント エディターでは使用できます。

次の例では、Azure 空間アンカーは入力イベント コールバック中にセットに保存されます。 その後、アンカーは EventTick に保存されます。 Azure Spatial Anchors セッションで作成した空間データの量によっては、Azure 空間アンカーの保存を複数回試行することが必要になる場合があります。 そのため、保存の呼び出しが成功したかどうかを確認することをお勧めします。

アンカーが保存されていない場合は、これから保存する必要のあるアンカーのセットにそのアンカーをもう一度追加します。 将来的には、アンカーが Azure Spatial Anchors サービスに正常に保存されるまで、EventTick によってアンカーの保存が試みられるようになる予定です。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-16.png)

アンカーが保存されると、その AR ピンの変換を、アプリケーションにコンテンツを配置するための参照変換として使用できるようになります。 他のユーザーは、このアンカーを検出し、現実世界のさまざまなデバイス向けに AR コンテンツを配置できます。

## <a name="deleting-an-anchor"></a>アンカーを削除する

**Delete Cloud Anchor** を呼び出して、Azure Spatial Anchors サービスからアンカーを削除できます。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-17.png)

> [!NOTE]
> Delete Cloud Anchor は潜在関数で、EventTick などのゲーム スレッド イベントでのみ呼び出すことができます。 Delete Cloud Anchor は、カスタムのブループリント関数では、使用可能なブループリント関数として表示されない場合があります。 ただし、ポーン イベント グラフ ブループリント エディターでは使用できます。

次の例では、カスタム入力イベントで、アンカーに削除のフラグが設定されています。 その後、EventTick で削除が試行されます。 アンカーの削除が失敗した場合は、その Azure 空間アンカーを削除のフラグが設定されているアンカーのセットに追加し、EventTick で後でもう一度試行します。

イベント グラフ ブループリントは、次のスクリーンショットのようになります。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-18.png)


## <a name="locating-pre-existing-anchors"></a>既存のアンカーを検索する

Azure 空間アンカーを作成するだけでなく、仲間が Azure Spatial Anchors サービスを使って作成したアンカーを検出することもできます。

1. 検出したいアンカーの Azure 空間アンカー識別子を取得します。
    * アンカー識別子は、前の Azure Spatial Anchors セッションで同じデバイスによって作成されたアンカー用に取得できます。 また、その Azure Spatial Anchors サービスと対話するピア デバイスで作成して共有することもできます。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-24.png)

2. **AzureSpatialAnchorsEvent** コンポーネントをポーン ブループリントに追加します。
    * このコンポーネントを使用すると、Azure 空間アンカーが検索されるときに呼び出されるイベントなど、さまざまな Azure Spatial Anchors イベントをサブスクライブできます。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-19.png)

3. **AzureSpatialAnchorsEvent** コンポーネントの **ASAAnchor Located Delegate** をサブスクライブします。
    * このデリゲートを使用すると、Azure Spatial Anchors アカウントに関連付けられている新しいアンカーが検索されたときに、アプリケーションで認識できます。
    * このイベント コールバックでは、仲間が Azure Spatial Anchors セッションを使用して作成した Azure 空間アンカーには、既定で AR ピンが作成されません。 検出された Azure 空間アンカーの AR ピンを作成するため、開発者は **Create ARPin Around Azure Cloud Spatial Anchor** を呼び出すことができます。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-20.png)

仲間が Azure Spatial Anchors サービスを使用して作成した Azure 空間アンカーを検索するには、そのアプリケーションで **Azure Spatial Anchors Watcher** を作成する必要があります。
1. Azure Spatial Anchors セッションが実行されていることを確認します。
2. **AzureSpatialAnchorsLocateCriteria** を作成します。
    * ユーザーからの距離や別のアンカーからの距離など、さまざまな位置パラメーターを指定できます。
3. **AzureSpatialAnchorsLocateCritieria** で、目的の Azure 空間アンカー識別子を宣言します。
4. **Create Watcher** を呼び出します。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-21.png)

これで、アプリケーションで、Azure Spatial Anchors サービスに認識されている Azure 空間アンカーの検索が開始されます。この結果、ユーザーは仲間が作成した Azure 空間アンカーを見つけることができるようになります。

Azure 空間アンカーを見つけたら、**Stop Watcher** を呼び出して Azure Spatial Anchors Watcher を停止し、監視リソースをクリーンアップします。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-22.png)

最終的なイベント グラフ ブループリントは、次のスクリーンショットのようになります。

![Spatial Anchors プラグイン](images/asa-unreal/unreal-spatial-anchors-img-23.png)


## <a name="next-steps"></a>次の手順
* [ローカル空間アンカー](unreal-spatial-anchors.md)
* [Spatial Anchors のドキュメント](https://docs.microsoft.com/azure/spatial-anchors/)
* [空間アンカーの機能](https://azure.microsoft.com/services/spatial-anchors/#features)
* [効果的なアンカー エクスペリエンスのガイドライン](https://docs.microsoft.com/azure/spatial-anchors/concepts/guidelines-effective-anchor-experiences)