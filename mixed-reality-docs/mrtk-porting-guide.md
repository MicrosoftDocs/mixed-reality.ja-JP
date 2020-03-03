---
title: 既存のアプリを HoloLens 2 で利用できるようにする
description: HoloLens (第 1 世代) または古い MRTK の既存アプリがあり、MRTK バージョン 2 および HoloLens 2 への移植を考えている開発者が対象です。
author: grbury
ms.author: grbury
ms.date: 10/14/2019
ms.topic: article
ms.localizationpriority: high
keywords: Windows Mixed Reality, テスト, MRTK, MRTK バージョン 2, HoloLens 2
ms.openlocfilehash: 8e0c66a1c3d8ebd5422d19a02f313147ecf76653
ms.sourcegitcommit: 40b37104b0aec4554502dcc7dc430e340a6fa46a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77092036"
---
# <a name="get-your-existing-app-ready-for-hololens-2"></a>既存のアプリを HoloLens 2 で利用できるようにする

このガイドは、HoloLens (第 1 世代) 用の既存の Unity アプリケーションを持つ開発者が、アプリケーションを HoloLens 2 デバイス用に移植する場合に役立ちます。 HoloLens (第 1 世代) の Unity アプリケーションを HoloLens 2 に移植する主な手順は 4 つあります。 

次のセクションで、各ステージについて詳しく説明します。

| 手順 1 | 手順 2 | 手順 3 | 手順 4 |
|----------|-------------------|-------------------|-------------------|
| ![Visual Studio のロゴ](images/visualstudio_logo.png) | ![Unity のロゴ](images/final_unity_logo.png)| ![Unity のアイコン](images/hololens2_icon.jpg) | ![MRTK のロゴ](images/final_mrtk-small_logo.png) |
| 最新のツールのダウンロード | Unity プロジェクトの更新 | ARM 用にコンパイル | MRTK v2 に移行

前提条件:

移植プロセスを開始する前に、開発者がソース管理を使用してアプリケーションの元の状態のスナップショットを保存しておくことを**強くお勧めします**。 さらに、プロセス中のさまざまな時点でチェックポイントの状態を*保存*することを推奨します。 移植プロセスの中で、元のアプリケーションの別の Unity インスタンスを並べて比較できるようにするのも非常に便利です。 

> [!NOTE]
> 移植の前に、Windows Mixed Reality の開発用に最新のツールがインストールされていることを確認します。 ほとんどの既存 HoloLens 開発者は、主に最新バージョンの Visual Studio 2019 への更新と適切な Windows SDK のインストールを行うことになります。 以下の内容では、Unity のさまざまなバージョンと Mixed Reality Toolkit (MRTK) バージョン 2 についてさらに詳しく説明します。
>
> 詳しくは、[ツールのインストール](install-the-tools.md)に関するページをご覧ください。

## <a name="migrate-project-to-the-latest-version-of-unity"></a>プロジェクトを最新バージョンの Unity に移行する

[MRTK v2](https://github.com/microsoft/MixedRealityToolkit-Unity) を使用している場合、Unity または MRTK で互換性に影響する変更が発生しない最適な長期サポート パスは [Unity 2018 LTS](https://unity3d.com/unity/qa/lts-releases) になります。 また、MRTK v2 は Unity 2018 LTS のサポートを常に保証していますが、必ずしも Unity 2019.x のすべてのイテレーションのサポートが保証されるわけではありません。 

[Unity 2018 LTS](https://unity3d.com/unity/qa/lts-releases) と Unity 2019.x の他の相違点を明らかにするために、以下では、これら 2 つのバージョン間でのトレードオフについて説明します。 2 つの主な違いは、Unity 2019 で ARM64 用にコンパイルする機能です。 

開発者は、現在プロジェクトに存在するすべての[プラグインの依存関係](https://docs.unity3d.com/Manual/Plugins.html)を評価し、これらの DLL が ARM64 でビルドできるかどうかを判断する必要があります。 ARM64 でハードに依存するプラグインをビルドできない場合は、Unity 2018 LTS を使用する必要があります。


| Unity 2018 LTS | Unity 2019.x |
|----------|-------------------|
| ARM32 ビルドのサポート | ARM32 および ARM64 ビルドのサポート |
| 安定版の LTS ビルド リリース | ベータ版の安定性 |
| [.NET スクリプト バックエンド](https://docs.unity3d.com/2018.4/Documentation/Manual/windowsstore-dotnet.html) *非推奨* | [.NET スクリプト バックエンド](https://docs.unity3d.com/2018.4/Documentation/Manual/windowsstore-dotnet.html) *削除済み* |
| UNET Networking *非推奨* | UNET Networking *非推奨* |

## <a name="update-sceneproject-settings-in-unity"></a>Unity でシーンまたはプロジェクト設定を更新する

デバイスで最適な結果を得るために、[Unity 2018 LTS](https://unity3d.com/unity/qa/lts-releases) または Unity 2019 以降への更新を行った後、Unity を特定の設定に更新すること をお勧めします。 この設定については、 **[Unity の推奨設定](Recommended-settings-for-Unity.md)** で詳しく説明しています。

もう一度お伝えしますが、[.NET スクリプト バックエンド](https://docs.unity3d.com/Manual/windowsstore-dotnet.html)は、Unity 2018 で非推奨となり、Unity 2019 で*削除*されます。 開発者の皆様には、プロジェクトの [IL2CPP](https://docs.unity3d.com/Manual/IL2CPP.html) への切り替えを検討することを強くお勧めします。 

> [!NOTE]
> IL2CPP スクリプト バックエンドを使用すると、Unity から Visual Studio へのビルド時間が長くなる場合があります。そのため、開発者は、[IL2CPP ビルド時間の最適化](https://docs.unity3d.com/Manual/IL2CPP-OptimizingBuildTimes.html)のために開発者のコンピューターをセットアップする必要があります。
> また、大きなアセット (スクリプト ファイルを除く) がある場合や、常にシーンやアセットを変更する Unity プロジェクトの場合は、[キャッシュ サーバー](https://docs.unity3d.com/Manual/CacheServer.html)をセットアップするとよいでしょう。 プロジェクトを開く際に、Unity は条件を満たすアセットを内部キャッシュ フォーマットで開発者のコンピューターに格納します。 項目を変更した場合は、再インポートして再処理されるようにする必要があります。 このプロセスが 1 回実行されると、キャッシュ サーバーに保存され、すべての開発者と共有されます。すべての開発者がローカルで新しい変更の再インポート処理を行う必要がなくなるので、時間を節約できます。

開発者は、更新した Unity のバージョンに移行してから、互換性に影響する変更に対処した後で、HoloLens (第 1 世代) で現在のアプリケーションをビルドしてテストする必要があります。 この時点でソース管理にコミットを作成し、保存しておくとよいでしょう。 

## <a name="compile-dependenciesplugins-for-arm-processor"></a>ARM プロセッサ用の依存関係およびプラグインのコンパイル

HoloLens (第 1 世代) は、x86 プロセッサ上でアプリケーションを実行するのに対して、HoloLens 2 は ARM プロセッサを使用します。 したがって、既存の HoloLens アプリケーションは、ARM をサポートするように移植する必要があります。 前述のように、Unity 2018 LTS は ARM32 アプリのコンパイルをサポートしますが、Unity 2019.x は ARM32 アプリと ARM64 アプリのコンパイルをサポートします。 一般的に、パフォーマンスに重要な相違があるため、ARM64 アプリケーションでの開発が推奨されます。 ただし、そのためには、すべての[プラグインの依存関係](https://docs.unity3d.com/Manual/Plugins.html)も ARM64 でビルドする必要があります。 

アプリケーション内のすべての DLL 依存関係を確認してください。 不要になった依存関係は、プロジェクトから削除することをお勧めします。 必要な残りのプラグインについて、Unity プロジェクトにそれぞれ ARM32 または ARM64 バイナリを取り込みます。 

関連する DLL を取り込んだ後、Unity から Visual Studio ソリューションをビルドし、アプリケーションが ARM プロセッサでビルドできるかどうかを試すために、Visual Studio で AppX を ARM 向けにコンパイルします。 ソース管理ソリューションでコミットとしてアプリケーションを保存することをお勧めします。

## <a name="update-to-mrtk-version-2"></a>MRTK バージョン 2 に更新する

[MRTK バージョン 2](https://github.com/microsoft/MixedRealityToolkit-Unity) は、Unity をベースにした新しいツールキットで、HoloLens (第 1 世代) と HoloLens 2 の両方をサポートします。 また、手による操作や視線追跡など、HoloLens 2 のすべての新機能が追加されています。

MRTK バージョン 2 の使用方法の詳細については、以下を参照してください。
- [MRTK のランディング ページ](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
- [MRTK をお使いになる前に](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
- [MRTK の手](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSystem/HandTracking.html)
- [MRTK の視線追跡](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html)

### <a name="prepare-for-the-migration"></a>移行を準備する

新しい [MRTK v2 用の *.unitypackage ファイル](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases)を取り込む前に、**1) MRTK v1 を組み込んだ任意のカスタム ビルド コード**と、**2) 入力操作や UX コンポーネントのカスタム ビルド コード**のインベントリを取得することを推奨します。 Mixed Reality 開発者が MRTK v2 を取り込む際に最も競合が起きやすいのは、入力と操作に関係する部分です。 [MRTK v2 入力モデル](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)を読んで理解しておくことをお勧めします。

最後に、新しい [MRTK v2](https://github.com/microsoft/MixedRealityToolkit-Unity) は、スクリプトのモデルおよびシーン内マネージャー オブジェクトから、構成およびサービス プロバイダー アーキテクチャに移行されています。 これにより、シーンの階層とアーキテクチャのモデルがクリーンになりますが、新しい構成プロファイルを習得する必要があります。 したがって、重要な設定やプロファイルについて理解し、アプリケーションのニーズに合わせて調整することができるように、[Mixed Reality ツールキット構成ガイド](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html)を参照してください。 

### <a name="perform-the-migration"></a>移行する

[MRTK v2](https://github.com/microsoft/MixedRealityToolkit-Unity) をインポートすると、高い確率で、Unity プロジェクトでたくさんのコンパイラ関連エラーが発生します。 一般的に、これらの原因は新しい名前空間の構造と新しいコンポーネント名です。 スクリプトの名前空間とコンポーネントを新しいものに変更し、これらのエラーを解決します。 

HTK/MRTK と MRTK v2 の具体的な API の相違点については、[MRTK バージョン 2 wiki](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html) の移植ガイドをご覧ください。

### <a name="best-practices"></a>ベスト プラクティス

- [MRTK 標準シェーダー](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html)の使用を優先する。
- 互換性に影響する種類の変更には 1 つずつ対応する (例:IFocusable を [IMixedRealityFocusHandler](https://microsoft.github.io/MixedRealityToolkit-Unity/api/Microsoft.MixedReality.Toolkit.Input.IMixedRealityFocusHandler.html) に)。
- 変更のたびにテストし、ソース管理を使用する。
- 可能な場合は既定の MRTK UX (ボタン、スレートなど) を使用する。
- MRTK ファイルを直接変更するのは避け、MRTK コンポーネントのラッパーを作成する。
    - この操作をすると、将来の MRTK インジェストや更新が容易になります。
- MRTK で提供されているサンプルのシーンを確認する (特に *HandInteractionExamples.scene*)。
- キャンバス ベースの UI を四角形、コライダー、TextMeshPro テキストで再構築する。
- [深度バッファーの共有](camera-in-unity.md#sharing-your-depth-buffers-with-windows)、または[フォーカス ポイントの設定](focus-point-in-unity.md)を有効にする。パフォーマンスを向上させたい場合は、16 ビットの深度バッファーを使用します。 色をレンダリングするとき、深度もレンダリングするようにする。 Unity では、一般的に、透明なゲームオブジェクトとテキスト ゲームオブジェクトの深度は書き込まれません。 
- 単一パスのインスタンス化レンダリング パスを設定する。
- [MRTK 用の HoloLens 2 構成プロファイル](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Profiles/Profiles.html#hololens-2-profile)を利用する

### <a name="testing-your-application"></a>アプリケーションのテスト

MRTK バージョン 2 では、手による操作を直接 Unity でシミュレートすること、および手による操作と視線追跡用の新しい API を使用して開発を行うことができます。 十分なユーザー エクスペリエンスを作成するには、HoloLens 2 デバイスが必要です。 より詳しく理解するために、ドキュメントとツールの学習を開始することをお勧めします。 [MRTK v2](https://github.com/microsoft/MixedRealityToolkit-Unity) は HoloLens (第 1 世代) での開発をサポートしています。このため、エアタップによる選択などの従来の入力モデルを HoloLens (第 1 世代) でテストできます。 

## <a name="updating-your-interaction-model-for-hololens-2"></a>HoloLens 2 向けの操作モデルの更新

アプリケーションを移植して HoloLens 2 に対応するよう準備できたら、操作モデルやホログラムの設計配置の更新を検討できるようになります。
HoloLens (第 1 世代) では、アプリケーションで視線入力とコミットによる操作モデルが使われており、視野に収まるようにホログラムがかなり遠くにある可能性が高くなります。

アプリケーションの設計を HoloLens 2 に最適な状態になるように更新する手順は次のとおりです。
1.  MRTK コンポーネント:事前の作業で [MRTK v2](https://github.com/microsoft/MixedRealityToolkit-Unity) を追加した場合は、HoloLens 2 用に設計および最適化されているさまざまなコンポーネントやスクリプトを活用できます。

2.  操作モデル:操作モデルを更新することを検討します。 ほとんどのシナリオでは、視線入力とコミットを手に切り替えることをお勧めします。 通常、ホログラムは手の届かないところにあるので、手に切り替えることで、ポインティング レイやグラブ ジェスチャによる遠隔インタラクションを利用することになります。

3.  ホログラムの配置:手による操作モデルに切り替えた後は、手で近接インタラクションのグラブ ジェスチャを使用して、直接それらを操作できるように、ホログラムを近くに移動することを検討します。 直接つかんだり操作を行ったりするために近くに移動させることが推奨されるホログラムの種類は、小さなターゲット メニュー、コントロール、ボタン、およびグラブしたり調べたりしても HoloLens 2 の視野に収まる小さなホログラムです。
<br>
どのアプリケーションやシナリオにも同じものはないので、フィードバックや継続する学習に基づいて設計ガイダンスを見直し、掲載し続ける予定です。


## <a name="additional-caveats-and-learnings-about-moving-applications-from-x86-to-arm"></a>X86 から ARM へのアプリケーションの移行に関するその他の注意事項と確認事項

- 単純な Unity アプリケーションは、ARM アプリケーション バンドルを構築できるため、またはバンドルを実行するためにデバイスに直接デプロイできるため、シンプルです。 一部の Unity ネイティブ プラグインでは、特定の開発上の課題が発生する可能性があります。 このため、すべての Unity ネイティブ プラグインを Visual Studio 2019 にアップグレードし、その後、ARM 用に再構築する必要があります。

- 1 つのアプリケーションで Unity AudioKinetic Wwise プラグインが使用されており、そのバージョンの Unity には UWP ARM プラグインがなかったため、ARM で実行するその問題のアプリケーションにサウンド機能を再構成するためにかなりの労力が必要でした。 開発プランに必要なすべてのプラグインがインストールされていて、Unity で利用できることを確認してください。

- 場合によっては、アプリケーションが必要とするプラグインに UWP/ARM プラグインが存在しない場合があります。これにより、アプリケーションを移植して HoloLens 2 で実行する機能がブロックされます。 問題を解決して ARM のサポートを提供するには、プラグインのプロバイダーにお問い合わせください。

- シェーダーの minfloat (および min16float、minint などのバリアント) の動作は、HoloLens 2 と HoloLens (第 1 世代) で異なる場合があります。 具体的には、「少なくとも指定された数のビットが使われる」ことが保証されます。 ほとんどの Intel/Nvidia の GPU では、単なる 32 ビットとして扱われます。 ARM では、指定されたビット数が実際に使用されます。 つまり、実際には、HoloLens 2 でのこれらの数値の精度や範囲は、HoloLens (第 1 世代) よりも小さくなります。

- ARM では _asm 命令は動作しないと見られるので、_asm 命令を使用しているコードはすべて書き直す必要があります。

- ARM では xmmintrin.h、emmintrin.h、tmmintrin.h、immintrin.h などの各種ヘッダーは使用できないため、ARM では SIMD 命令セットはサポートされません。

- ARM のシェーダー コンパイラは、シェーダーの読み込み時ではなく、シェーダーが読み込まれた後またはシェーダーが依存するものが変更された後の最初の描画呼び出しの中で実行されます。 コンパイルする必要があるシェーダーの数によっては、フレーム レートへの影響が顕著になる場合があります。 これは、HoloLens 2 と HoloLens (第 1 世代) でのシェーダーの処理、パッケージ化、更新の方法の違いに対してさまざまな影響を与えます。

## <a name="see-also"></a>関連項目
* [ツールのインストール](install-the-tools.md)
* [MRTK バージョン 2 をお使いになる前に](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [HTK API 対 MRTK API](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html)
* [Unity で推奨される設定](recommended-settings-for-unity.md)
* [Mixed Reality のパフォーマンスを理解する](understanding-performance-for-mixed-reality.md)

