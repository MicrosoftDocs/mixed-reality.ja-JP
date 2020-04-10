---
title: Windows Mixed Reality シミュレーターの使用
description: Windows Mixed Reality シミュレーターを使用すると、Windows Mixed Reality のイマーシブヘッドセットを使用せずに、お使いの PC で mixed reality アプリをテストすることができます。
author: pbarnettms
ms.author: pbarnett
ms.date: 04/25/2019
ms.topic: article
keywords: Windows Mixed Reality、シミュレーター、テスト
ms.openlocfilehash: 686cac4e9ab4b3354767e22cd87d37ffbb508dea
ms.sourcegitcommit: 37816514b8fe20669c487774b86e80ec08edcadf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2020
ms.locfileid: "81003298"
---
# <a name="using-the-windows-mixed-reality-simulator"></a>Windows Mixed Reality シミュレーターの使用

Windows Mixed Reality シミュレーターを使用すると、Windows Mixed Reality のイマーシブヘッドセットを使用せずに、お使いの PC で mixed reality アプリをテストすることができます。 Windows 10 の作成者の更新プログラムから入手できます。 シミュレーターは[HoloLens エミュレーター](using-the-hololens-emulator.md)に似ていますが、シミュレーターでは仮想マシンが使用されません。 シミュレーターで実行されているアプリは、イマーシブヘッドセットを使用している場合と同じように、Windows 10 デスクトップユーザーセッションで実行されます。 通常、イマーシブヘッドセットのセンサーによって読み取られる人間と環境の入力は、キーボード、マウス、または Xbox コントローラーを使用してシミュレートされます。 アプリをシミュレーターで実行するように変更する必要はなく、イマーシブヘッドセットで実行されていないことはわかりません。

## <a name="enabling-the-windows-mixed-reality-simulator"></a>Windows Mixed Reality シミュレーターの有効化

1. 開発者向けの設定から**開発者モードを有効にする**-> の更新プログラムとセキュリティ->
2. デスクトップから**Mixed Reality ポータル**を起動する
3. ポータルを初めて起動する場合は、セットアップエクスペリエンスを確認する必要があります。
   1. **[開始]** をクリックします。
   2. [**同意**する] をクリックして、契約に同意します
   3. 物理デバイスを使用せずにセットアップを続行するには、 **[シミュレーション用に設定 (開発者向け)]** をクリックします。
   4. [セットアップ] を**クリックして**選択内容を確認します
4. Mixed Reality ポータルの左側にある **[開発者向け]** ボタンをクリックします。
5. シミュレーション切り替え**スイッチをオンにする**
   * シミュレーションを有効にすると、既定では、シミュレートされた6つの自由可能なコントローラーの左側が有効になります。  Windows 10 5 月2019更新プログラムの前に、シミュレートされた6自由コントローラーをインストールするには、管理者権限が必要です。  表示される場合は、[ユーザーアカウント制御] ダイアログボックスを受け入れる必要があります。

これでシミュレーションが実行されます。

設定 で開発者モードを無効にする場合は、まず、Mixed Reality ポータルの **開発者向け** セクションで、シミュレーション切り替えスイッチを **オフ** に切り替える必要があります。

## <a name="deploying-apps-to-the-mixed-reality-simulator"></a>混合の現実シミュレーターへのアプリの配置

シミュレーターは仮想マシンを使用せずにローカル PC で実行されるため、デバッグ時にユニバーサル Windows アプリを**ローカルコンピューター**に配置するだけで済みます。

## <a name="basic-simulator-input"></a>基本的なシミュレーター入力

シミュレーターの制御は、多くの一般的な3D ビデオゲームや[HoloLens エミュレーター](using-the-hololens-emulator.md)とよく似ています。 入力オプションは、キーボード、マウス、または Xbox コントローラーで使用できます。

シミュレートされたユーザーがイマーシブヘッドセットを装着したときのアクションを指示することによって、シミュレーターを制御します。 操作を実行すると、シミュレートされたユーザーが移動され、イマーシブヘッドセットの場合と同じように応答するアプリとの対話が行われます。
* **前後左右に歩く** - キーボードの W、A、S、D キーまたは Xbox コントローラーの左スティックを使用します。
* **上下左右を見る** - マウスをクリックしてドラッグするか、キーボードの方向キーを使用するか、Xbox コントローラーの右スティックを使用します。
* **コントローラーでのアクションボタンの押下**-マウスを右クリックするか、キーボードの enter キーを押すか、または Xbox コントローラーの A ボタンを使用します。
* **[ホーム] ボタン**をクリックしてコントローラーを押す-キーボードの Windows キーまたは F2 キーを押すか、Xbox コントローラーの B ボタンを押します。
* **スクロール用のコントローラーの移動**-Alt キーを押したままマウスの右ボタンを押し、マウスを上下にドラッグするか、右のトリガーとボタンを押したまま右スティックを上下に移動します。

## <a name="tracked-controllers"></a>追跡対象のコントローラー

Mixed Reality シミュレーターでは、最大2つのハンド保持された追跡対象モーションコントローラーをシミュレートできます。 混合 Reality ポータルで切り替えスイッチを使用して有効にします。 各シミュレートされたコントローラーには次のものがあります。
* 空間内の位置と向き
* ホーム ボタン
* メニュー ボタン
* グリップボタン
* タッチパッド
* スティック
* バッテリレベル

## <a name="see-also"></a>参照
* [HoloLens のエミュレーターを使用する](using-the-hololens-emulator.md)
* [高度な Mixed Reality シミュレーター入力](advanced-hololens-emulator-and-mixed-reality-simulator-input.md)
* [Unity の空間マッピング](spatial-mapping-in-unity.md)
* [DirectX の空間マッピング](spatial-mapping-in-directx.md)
