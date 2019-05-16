---
title: 直接操作
description: 直接操作の入力モデルの概要
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/02/2019
ms.topic: article
keywords: 実際には、視線の先、視線の先を対象との相互作用、混在、デザイン、ほぼ手 HoloLens
ms.openlocfilehash: 803157bb248a5541ed524ac4f828ccbba9d59ce1
ms.sourcegitcommit: 82d4e5cf4ad46bfdc44d0606844e28c75b6e67ce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65730508"
---
# <a name="direct-manipulation"></a>直接操作

HoloLens 2 では、自分の手でホログラム dircly をタッチすることができますを直接操作の入力モデルがあります。 直接操作の目的は、現実の世界と同じように動作するオブジェクトです。 それを押すだけでボタンをアクティブ化しもおよびを取得、取得、してオブジェクトを移動できます。 これらのシナリオで 2D のコンテンツは、仮想のタッチ スクリーンのように動作します。

直接の操作は、簡単にについては、ユーザーとが楽しいです。 Arm の範囲内にあるコンテンツと対話するための使用に適してつまり、「近くに渡します」入力モデルと見なされます。

直接操作は、アフォー ダンスに基づく、つまりユーザー フレンドリです。 ユーザーに教えるにシンボリック ジェスチャはありません。 すべての対話は、タッチまたは取得できるビジュアル要素の周囲に構築されます。

## <a name="device-support"></a>デバイスのサポート

| 入力モデル | [HoloLens (第 1 世代)](https://review.docs.microsoft.com/en-us/windows/mixed-reality/hololens-hardware-details?branch=master) | HoloLens 2 |[イマーシブ ヘッドセット](https://review.docs.microsoft.com/en-us/windows/mixed-reality/immersive-headset-hardware-details?branch=master)|
|:-------- | :-------| :--------| :------------|
| 直接操作 | ❌ がサポートされていません | 推奨 ✔️ | ➕ 代替[をポイントし、コミット](https://review.docs.microsoft.com/en-us/windows/mixed-reality/point-and-commit?branch=master)をお勧めします。

直接操作では、HoloLens 2 では、プライマリ入力モデルを新しい関節手動追跡システムを使用します。 入力モデルでは、アニメーション コント ローラーを使用してイマーシブ ヘッドセットに収録されてもが、オブジェクトの操作の外部での相互作用の主要な手段としては推奨されません。  直接 manipluation は HoloLens v1 でご利用いただけません。

## <a name="collidable-fingertip"></a>Collidable 指先

HoloLens 2 では、ユーザーの実際の手が認識され、左側と右側のスケルトン モデルとして解釈されます。 手を直接ホログラム手を加えることのアイデアを実装するために理想的には、5 コライダーを接続できます各ハンドのスケルトン モデルのすぐに利用できる 5。 ただし、実際には、触るフィードバックがないことによる 10 collidable すぐ予期しない競合、発生ホログラム。 

そのため、それぞれインデックスの指でのみコライダーをお勧めします。 Collidable インデックス ヒントは、次の図に示すようにまだ 1 本の指のキーを押して、1 本指でタップ、2 本の指のキーを押して、5 本の指のキーを押してなどの他の指に関連する多様なタッチ ジェスチャのアクティブなタッチ ポイントとして使用できます。

![Collidable 指先イメージ](images/Collidable-Fingertip-720px.jpg)

### <a name="sphere-collider"></a>球のコライダー

ランダムな汎用図形を使用せずに球コライダーを使用して、ほぼ対象とする場合より優れた的な手掛かりを提供することを視覚的に表示するためにお勧めします。 球の直径は、タッチの精度を向上させるインデックス本の指の太さと一致する必要があります。 手 API を呼び出すことによって、変数の本の指の太さを取得する簡単になります。

### <a name="fingertip-cursor"></a>指先カーソル

インデックスの指で collidable 球体をレンダリングするだけでなく対話形式での近くに対象とするエクスペリエンスの向上を実現するために、指先カーソル高度なソリューションを作成しました。 インデックスの指で接続されているドーナツ型のカーソルになります。 近接、に従って動的に反応する方向と以下のようにサイズの観点から、ターゲット。

* 人差し指ホログラムに向かって移動すると、カーソルはホログラムの画面に並列では常と、徐々 にそれに応じてそのサイズを縮小します。
* 指表面に触れてとすぐに、カーソルがドットに縮小し、タッチ イベントを出力します。

対話型のフィードバックでは、ユーザーは web コンテンツへのハイパーリンクをトリガーする、次のように、ボタンを押すなどのタスクを対象とするほぼ高精度を実現できます。 

![指先カーソル イメージ](images/Fingertip-Cursor-720px.jpg)

## <a name="bounding-box-with-proximity-shader"></a>近接シェーダーで境界ボックス

ホログラム自体には、触るフィードバックがないことを補正するために、ビジュアルおよびオーディオの両方のフィードバックを提供する機能も必要です。 そのため、近接シェーダーで境界ボックスの概念を生成します。 境界ボックスは、3 D オブジェクトを囲む最小帯域幅消費型領域です。 境界ボックスには、近接シェーダーと呼ばれる、対話型の表示メカニズムがあります。 近接シェーダーに動作します。

* 人差し指が範囲内と、境界ボックスの画面で指のスポット ライトがキャストされます。
* 画面に指が近づいたら、適宜にスポット ライトがでまとめます。
* 指、画面をタッチとすぐに、境界ボックス全体は色を変更またはタッチの状態を反映するように視覚効果を生成します。
* その一方で、サウンド効果は、タッチを視覚的フィードバックを強化するためにアクティブにできます。

![近接シェーダーのイメージの境界ボックス](images/Bounding-Box-With-Proximity-Shader-720px.jpg)

## <a name="pressable-button"></a>Pressable ボタン

Collidable 指でのユーザーが、非常に基本的な holographic UI コンポーネントは、pressable ボタンと対話する準備ができてようになりました。 Pressable ボタンは、直接本の指のキーを押してに合わせた holographic ボタンです。 ここでも、触るフィードバックがないことによる pressable ボタンに触るフィードバックに関連する問題に対処するいくつかのメカニズムを提供します。

* 最初のメカニズムは、前のセクションに記載された、近接シェーダーで境界ボックスです。 深く理解する方法をユーザーの近接を提供する機能、ボタンを含む連絡先。
* 2 つ目は、低下します。 指先をボタンに接続した後、キーを押して、感を作成します。 このメカニズムは、ボタンは、深さ軸に沿った指と緊密に移動します。 ボタンは、(キーを押します) で指定された深さに達すると、渡された後に (リリース) の深さを離れるときにトリガーできます。
* ボタンがトリガーされたときに、フィードバックを強化するために、サウンド効果を追加する必要があります。

![Pressable ボタンの画像](images/Pressable-Button-720px.jpg)

## <a name="2d-slate-interaction"></a>2D のスレートの相互作用

2D スレートは、web ブラウザーなどの 2D アプリのコンテンツをホストしている holographic コンテナーです。 物理タッチ画面との対話のメンタル モデルを利用することを直接操作を使用して 2D スレートと対話するための設計概念です。

スレートの連絡先と操作。

* インデックス本の指を使用して、ハイパーリンクやボタンを押します。
* スレートのコンテンツをスクロール アップ/ダウン、人差し指を使用します。
* ユーザーは、in および out 本の指の動きを相対に従ってスレートのコンテンツを拡大する 2 つの人差し指を使用します。

![2D のスレート イメージ](images/2D-Slate-Interaction-720px.jpg)

2D を操作するためには、それ自体をスレートします。

* 角や辺に最も近い操作アフォーを明らかに手をアプローチします。
* 操作アフォーをつかんで、上隅にあるアフォーで統一されたスケーリングを実行、およびエッジ アフォーを介してリフローします。
* 2D のスレートは、全体のスレートを移動することができますの上部にある holobar を取得します。

![スレートの操作のイメージ](images/Manipulate-2d-slate-720px.jpg)

## <a name="3d-object-manipulation"></a>3D オブジェクトの操作

HoloLens 2 には、境界ボックスを各 3D オブジェクトに適用することで 3D hologramphic オブジェクトを操作ユーザーが直接に手を有効にすることができます。 境界ボックスは、その近接シェーダーを通じてより優れた深さ perception を提供します。 境界ボックスを 2 つの 3D オブジェクトの操作のデザイン方法があります。

### <a name="affordance-based-manipulation"></a>アフォー ダンス ベースの操作

これにより、境界ボックスとその周り操作アフォーを使用して 3D オブジェクトを操作できます。 ユーザーの手の形は、3 D オブジェクトの近くとすぐに、境界ボックスと最も近いアフォー ダンス開示されます。 ユーザーは、オブジェクト全体、回転するエッジ アフォーおよびを一様にスケール上隅にあるアフォーを移動する、境界ボックスを取得できます。

![3D オブジェクトの操作のイメージ](images/3D-Object-Manipulation-720px.jpg)

### <a name="non-affordance-based-manipulation"></a>非アフォー ダンス ベースの操作

このメカニズムで境界ボックスにアフォー ダンスはアタッチされません。 ユーザーは、のみ、境界ボックスを表示し、直接やり取りすることができます。 境界ボックスは、1 つの手でグラブされる場合平行移動とオブジェクトの回転、モーション センサーとして手のアイコンの向きに関連付けられます。 オブジェクトは、2 つの手をグラブ ユーザーで変換、スケールおよび回転させる 2 つのハンドの動作を相対に従ってことができます。

特定の操作には、有効桁数が必要ですを使用することをお勧めします。**アフォー ダンスに基づく操作**粒度の高いレベルを提供するため、します。 柔軟な操作は、ことをお勧めする使用**非アフォー ダンス操作**はインスタントとおもしろいエクスペリエンスことができます。

## <a name="instinctual-gestures"></a>Instinctual ジェスチャ

HoloLens とは異なり (第 1 世代) 講師ユーザー ブルーム エア タップなどのいくつかの定義済みジェスチャ。 HoloLens の 2、シンボルのジェスチャを記憶するユーザーをお願いはありません。 すべての必要なユーザー ジェスチャ、ホログラムと内容との対話をユーザーの必要性は instinctual です。 Instinctual ジェスチャを実現する方法は、UI アフォーのデザインによってジェスチャを実行するユーザーをガイドです。

などの場合は、オブジェクトのグラブまたは 2 本の指のピンチでのコントロール ポイントにぜひ、オブジェクトまたはコントロール ポイントは小にします。 5 本の指グラブを実行することをする場合、オブジェクトまたはコントロール ポイントが比較的大きななければなりません。 ボタンと同様に、小さなボタンはユーザーを制限する大きなボタンをユーザーの手のひらで押すお勧めします中に 1 本の指を押します。

![](images/Instinctual-Gestures-720px.jpg)

## <a name="symmetric-design-between-hands-and-6-dof-controllers"></a>ハンドと 6 の自由度のコント ローラーの間の対称のデザイン

お気付き相互作用の parallels VR で AR およびモーションのコント ローラー内のハンド間に描画できることがあります。 両方の入力は、それぞれの環境での直接の操作をトリガーする使用できます。 HoloLens の 2 をグラブしてドラッグ近距離 works 手をあまりグラブ ボタンと同じ方法では、WMR でモーション コント ローラーには。 これにより、2 つのプラットフォーム間の相互作用に関する知識をユーザーに提供され、便利だとこれまで決めた場合、他のいずれかからアプリを移植します。

## <a name="optimize-with-eye-tracking"></a>視線を最適化します

ホログラムを誤ってトリガーすることがなくもう手を任意の場所を移動できない場合は、ストレスも簡単になることができますが、意図したとおりに動作する場合、直接操作を魔法のようなと思われることができます。
ユーザーの目的は、どのような改善を識別する視線が可能性のあるできます。

* **ときに**:誤って操作応答のトリガーを減らします。 視線では、どのようなユーザーが現在進行中でより良く理解できます。
たとえば、以上に到達すると、実際の作業のツールを取得するときに、holographic (説明) のテキストを読んでいるとします。

  これにより、誤ってに (おそらくもが、ユーザーのフィールドの視野 (FOV) 外に) する前に気付きですかもいくつかの対話型 holographic ボタンに手を移動します。

  要するに：ユーザーいないホログラムしばらくの間、見てまだ、タッチまたは把握イベントが検出されましたが、ユーザーがそのホログラムと対話する目的で実際にいる可能性があります。

* **どれを**:別の例にはとは別に正の値の false のアクティブ化をアドレス指定にはよりどのホログラムを取得したりの観点からクリアは、いくつかホログラムがそれぞれの近くに配置されている場合は特に、積集合の正確なポイントは指定できません流行っていますよねを識別するが含まれていますその他。

  あるときに目追跡 HoloLens 2 で特定の制限について正確に視線の先を目、まだが非常に役立ちますの深さのような違いのための相互作用の近く手入力で操作するときにそれを判断できます。  つまりは手がの背後にある、またはホログラムたとえば操作ウィジェットを正確に取得する前にあるかどうかを確認する困難な場合があります。

* **場所**:どのようなユーザーに関する情報を使用はクイック スロー ジェスチャで見る。 ホログラムを取得し、約、目的の送信先に出すように頼みます。  

    場合もありますがこの中に非常に不正確な変換先は問題なく、すばやく手のジェスチャを実行する可能性があります。 これは、視線助け、目的の位置に戻すベクトルをスローして手のアイコンのリーン場所です。

## <a name="see-also"></a>関連項目

* [視線入力とコミット](gaze-and-commit.md)
* [ポイントとコミット](point-and-commit.md)
* [操作の基礎](interaction-fundamentals.md)