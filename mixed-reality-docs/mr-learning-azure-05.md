---
title: Azure Cloud チュートリアル - 5. Azure Bot Service と LUIS との統合
description: このコースを完了すると、HoloLens 2 アプリケーション内に Azure Bot Service と自然言語の理解を実装する方法を学習できます。
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: mixed reality, unity, チュートリアル, hololens, hololens 2, azure bot service, luis, 自然言語, 会話ボット
ms.localizationpriority: high
ms.openlocfilehash: daf97cde1477a84c1776a069ec5b8d1a185b63cc
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376454"
---
# <a name="5-integrating-azure-bot-service"></a>5.Azure Bot Service の統合

このチュートリアルでは、**HoloLens 2** デモ アプリケーションの **Azure Bot Service** を使用して Language Understanding (LUIS) を追加し、ユーザーが**追跡対象オブジェクト**を検索するときにボットで支援できるようにする方法について説明します。 これは 2 部構成のチュートリアルです。第 1 部では [Bot Composer](https://docs.microsoft.com/composer/introduction) を使用して、コード不要のソリューションとしてボットを作成します。また、必要なデータをボットにフィードする Azure 関数を簡単に確認します。 第 2 部では、Unity プロジェクトの **BotManager (スクリプト)** を使用して、ホストされた Bot Service を使用します。

## <a name="objectives"></a>目標

## <a name="part-1"></a>第 1 部

* Azure Bot Service の基本について学習する
* Bot Composer を使用してボットを作成する方法を学習する
* Azure 関数を使用して Azure ストレージからデータを提供する方法を学習する

## <a name="part-2"></a>第 2 部

* このプロジェクトで Azure Bot Service を使用するシーンをセットアップする方法を学習する
* ボットとの会話によってオブジェクトを設定および検索する方法を学習する

## <a name="understanding-azure-bot-service"></a>Azure Bot Service について

**Azure Bot Service** によって開発者は、**LUIS** を利用してユーザーとの自然な会話を維持できるインテリジェントなボットを作成できます。 会話ボットは、ユーザーがどのようにアプリケーションと対話できるかを拡張する優れた方法です。 ボットは、[Language Understanding (LUIS)](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-v4-luis?view=azure-bot-service-4.0&tabs=csharp) の優れた機能によって高度な会話を維持する、[QnA Maker](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-qna?view=azure-bot-service-4.0&tabs=cs) を使用したナレッジ ベースとして機能することができます。

[Azure Bot Service](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0) の詳細情報を参照してください。

## <a name="part-1---creating-the-bot"></a>第 1 部 - ボットを作成する

Unity アプリケーションでボットを使用するには、まずそれを開発し、データを提供して、**Azure** 上でホストする必要があります。
ボットの目的は、データベースに格納されている "*追跡対象オブジェクト*" の数を確認し、"*追跡対象オブジェクト*" をその名前で検索して、それに関する基本的な情報をユーザーに通知できるようにすることです。

### <a name="a-quick-look-into-tracked-objects-azure-function"></a>追跡対象オブジェクトの Azure 関数の概要

これからボットの作成を開始しますが、それを有効にするには、データをプルできるリソースを提供する必要があります。 "*ボット*" によって**追跡対象オブジェクト**の量をカウントしたり、名前で特定のものを検索して詳細を示したりできるため、**Azure テーブル ストレージ**にアクセスできるシンプルな Azure 関数を使用します。

Azure 関数プロジェクトをダウンロードします: [追跡対象オブジェクトの Azure 関数](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/AzureFunction_TrackedObjectsService.zip)

この Azure 関数には、**Count** と **Find** という 2 つのアクションがあり、基本的な *HTTP* *GET* 呼び出しを使用して呼び出すことができます。 **Visual Studio** でコードを調べることができます。

[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview) の詳細情報を参照してください。

**Count** 関数では、非常にシンプルに、テーブルにあるすべての **TrackedObjects** のクエリを **Table Storage** に実行します。 一方、**Find** 関数では、*GET* 要求から *name* クエリ パラメーターを受け取り、一致する **TrackedObject** のクエリを**テーブル ストレージ**に対して実行し、DTO を JSON として返します。

この **Azure 関数**を **Visual Studio** から直接デプロイできます。
Azure 関数のデプロイについては、[こちら](https://docs.microsoft.com/azure/devops/pipelines/targets/azure-functions?view=azure-devops&tabs=dotnet-core%2Cyaml)を参照してください。

デプロイが完了したら、対応するリソースを **Azure Portal** で開き、 *[設定]* セクションの下にある **[構成]** をクリックします。 **[アプリケーション設定]** で、**追跡対象オブジェクト**が格納されている **Azure ストレージ**への "*接続文字列*" を指定する必要があります。 **[新しいアプリケーション設定]** をクリックし、名前として **AzureStorageConnectionString** を使用し、値として正しい "*接続文字列*" を指定します。 その後、 **[保存]** をクリックすると、**Azure 関数**の準備が完了し、次に作成する "*ボット*" にサービスを提供できるようになります。

### <a name="creating-a-conversation-bot"></a>会話ボットの作成

Bot Framework ベースの会話ボットを開発するには、いくつかの方法があります。 このレッスンでは、[Bot Framework Composer](https://docs.microsoft.com/composer/) デスクトップ アプリケーションを使用します。これは、迅速な開発に最適なビジュアル デザイナーです。

最新リリースは、[GitHub リポジトリ](https://github.com/microsoft/BotFramework-Composer/releases)からダウンロードできます。 Windows、Mac、Linux で使用できます。

**Bot Framework Composer** のインストール完了後、アプリケーションを開始すると、次のインターフェイスが表示されます。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-1.png)

このチュートリアルに必要なダイアログとトリガーを提供するボット コンポーザー プロジェクトを準備済みです。
プロジェクトをダウンロードします: [Bot Framework Composer プロジェクト](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/BotComposerProject_TrackedObjectsBot.zip)

上部のバーで **[開く]** をクリックし、ダウンロードした Bot Framework プロジェクトを選択します。それには **TrackedObjectsBot** という名前が付けられています。 プロジェクトが完全に読み込まれると、プロジェクトの準備ができていることがわかります。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-2.png)

左側にフォーカスを移動して、**ダイアログ パネル**を確認してみましょう。 **TrackedObjectsBot** という名前のダイアログが 1 つあります。その下に、いくつかの**トリガー**を確認できます。

[Bot Framework の概念](https://docs.microsoft.com/composer/concept-dialog)についての詳細情報を参照してください。

これらのトリガーで以下のことを実行します。

#### <a name="greeting"></a>Greeting

これは、"*ユーザー*" が会話を開始したときの、チャット "*ボット*" のエントリ ポイントです。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-3.png)

#### <a name="askingforcount"></a>AskingForCount

このダイアログは、"*ユーザー*" がすべての**追跡対象オブジェクト**をカウントすることを要求したときにトリガーされます。
トリガー フレーズは次のとおりです。

>* count me all (すべてカウント)
>* how many are stored (何個格納されている)

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-4.png)

[LUIS](https://docs.microsoft.com/composer/how-to-use-luis) を活用することで、"*ユーザー*" はそのように厳密なフレーズでたずねる必要がなく、"*ユーザー*" にとって自然な会話ができます。

このダイアログでは、"*ボット*" から Azure 関数 **Count** への会話も行われます。それについては後で詳しく説明します。

#### <a name="unknown-intent"></a>Unknown Intent

このダイアログは、"*ユーザー*" からの入力が、他のどのトリガー条件にも適合しない場合にトリガーされ、ユーザーに再度質問を試みる応答を行います。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-5.png)

#### <a name="findentity"></a>FindEntity

最後のダイアログは、データを分岐して "*ボット*" メモリに格納することで、より複雑になります。
詳細情報を知る必要がある**追跡対象オブジェクト**の *name* をユーザーにたずね、Azure 関数 **Find** に対してクエリを実行し、その応答を使用して会話を続行します。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-6.png)

**追跡対象オブジェクト**が見つからない場合は、ユーザーに通知し、会話を終了します。 該当する**追跡対象オブジェクト**が見つかった場合は、ボットによって、使用可能なプロパティが何であるかが確認され、それらについて報告が行われます。

### <a name="adapting-the-bot"></a>ボットの適応

**AskingForCount** および **FindEntity** トリガーからバックエンドへの会話が必要です。これは、さきほどデプロイした **Azure 関数**の正しい URL を追加する必要があることを意味します。

ダイアログ パネルで **[AskingForCount]** をクリックし、 *[HTTP 要求を送信します]* というアクションを見つけます。ここに **[URL]** というフィールドがあるのがわかります。それを **Count** 関数のエンドポイントの正しい URL に変更する必要があります。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section5-step1-1.png)

最後に、**FindEntity** トリガーを探し、 *[HTTP 要求を送信します]* アクションを見つけて、 **[URL]** フィールドの URL を **Find** 関数のエンドポイントに変更します。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section5-step1-2.png)

これですべてを設定したので、ボットをデプロイする準備ができました。 Bot Framework Composer をインストール済みであるため、そこから直接発行することができます。

[Bot Composer からのボットの発行](https://docs.microsoft.com/composer/how-to-publish-bot)に関する詳細情報を参照してください。

> [!TIP]
> トリガー フレーズ、新たな応答、会話の分岐を追加して、ボットを自由に試してみてください。

## <a name="part-2---putting-everything-together-in-unity"></a>第 2 部 - すべてを Unity にまとめる

### <a name="preparing-the-scene"></a>シーンの準備

[Project]\(プロジェクト\) ウィンドウで、 **[Assets]\(アセット\)**  > **MRTK.Tutorials.AzureCloudServices** >  **[Prefabs]\(プレハブ\)**  > **Manager** フォルダーの順に移動します。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-1.png)

そこから、プレハブ **ChatBotManager** をシーン階層に移動します。

ChatBotManager をシーンに追加したら、**Chat Bot Manager** コンポーネントをクリックします。
インスペクターには、入力する必要がある空の **[Direct Line Secret Key]\(ダイレクト ライン シークレット キー\)** フィールドがあることがわかります。

> [!TIP]
> Azure portal から "*シークレット キー*" を取得できます。そのためには、このチュートリアルの最初の部分で作成した、種類が **[ボット チャンネル登録]** のリソースを検索します。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-2.png)

次に、**ChatBotManager** オブジェクトを、**ChatBotPanel** オブジェクトにアタッチされた **ChatBotController** コンポーネントと接続します。 [Hierarchy]\(階層\) で **ChatBotPanel** を選択すると、空の **[Chat Bot Manager]** フィールドが表示されます。[Hierarchy]\(階層\) から **ChatBotManager** オブジェクトを空の **[Chat Bot Manager]** フィールドにドラッグします。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-3.png)

次に、ユーザーが操作できるように **ChatBotPanel** を開く方法が必要です。 [Scene]\(シーン\) ウィンドウで、**MainMenu** オブジェクトに *[Chat Bot]\(チャット ボット\)* というサイド ボタンが表示されています。それを使用して、この問題を解決します。

[Hierarchy]\(階層\) で **RootMenu** > **MainMenu** > **SideButtonCollection** > **ButtonChatBot** に移動し、インスペクターで *ButtonConfigHelper* スクリプトを見つけます。 そこには、**OnClick ()** イベント コールバックに空のスロットが表示されています。 **ChatBotPanel** をイベント スロットにドラッグ アンド ドロップします。ドロップダウン リストから *GameObject* に移動し、サブメニューで *SetActive (bool)* を選択して、チェックボックスをオンにします。

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-4.png)

これで、メイン メニューからチャット ボットを開始できるようになり、それによって、シーンが使用できる状態になりました。

### <a name="putting-the-bot-to-a-test"></a>ボットをテストに配置する

#### <a name="asking-about-the-quantity-of-tracked-objects"></a>追跡対象オブジェクトの数について質問する

まず、データベースに格納されている**追跡対象オブジェクト**の数をボットに質問するテストを行います。

> [!NOTE]
> 今回は、アプリケーションを HoloLens 2 から実行する必要があります。お使いのシステムで "*音声合成*" などのサービスを使用できない場合があるためです。

HoloLens 2 でアプリケーションを実行し、メイン メニューの横にある *[Chat Bot]\(チャット ボット\)* ボタンをクリックします。
ボットからあいさつがあったら、"**how many objects do we have?** " (オブジェクトは何個ありますか?) と質問します。
数量が通知され、会話が終了します。

#### <a name="asking-about-a-tracked-object"></a>追跡対象オブジェクトについて質問する

ここで、アプリケーションをもう一度実行します。今度は、"**find me a tracked object**" (追跡対象オブジェクトを検索) と依頼します。ボットから名前をたずねられるので、"car" (車) と答えるか、データベース内に存在することがわかっている他の "*追跡対象オブジェクト*" の名前を答えます。 ボットから、説明などの詳細情報と、空間アンカーが割り当てられているかどうかが通知されます。

> [!TIP]
> 存在しない "**追跡対象オブジェクト**" について質問してみて、ボットがどのように応答するかを聞いてください。

## <a name="congratulations"></a>結論

このチュートリアルでは、Azure Bot Framework を使用して、自然言語での会話によってアプリケーションを操作する方法について学習しました。 ご自身のボットを開発する方法と、それを実行するためのすべての可動要素について学習しました。

## <a name="conclusion"></a>まとめ

このチュートリアル シリーズを通して、**Azure Cloud Services** を使用してご自身のアプリケーションに新しい優れた機能を取り入れる方法を経験しました。
**Azure Storage** を使用してクラウドにデータと画像を格納すること、**Azure Custom Vision** を使用して画像を関連付け、モデルをトレーニングすること、**Azure Spatial Anchors** を使用してローカル コンテキストにオブジェクトを配置すること、**LUIS を搭載した Azure Bot Framework** を実装し、新しい自然な対話のパターンに対応した会話ボットを追加することができるようになりました。
