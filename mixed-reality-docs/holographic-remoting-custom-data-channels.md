---
title: カスタム Holographic リモート処理データチャネル
description: カスタムデータチャネルは、既に確立されている Holographic リモート処理接続を介してユーザーデータを送信するために使用できます。
author: NPohl-MSFT
ms.author: nopohl
ms.date: 08/01/2019
ms.topic: article
keywords: HoloLens、リモート処理、Holographic リモート処理
ms.openlocfilehash: 9f7f20023d496412b331606e03d0c5110bb4864f
ms.sourcegitcommit: ca949efe0279995a376750d89e23d7123eb44846
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68718086"
---
# <a name="custom-holographic-remoting-data-channels"></a><span data-ttu-id="78b94-104">カスタム Holographic リモート処理データチャネル</span><span class="sxs-lookup"><span data-stu-id="78b94-104">Custom Holographic Remoting data channels</span></span>

>[!NOTE]
><span data-ttu-id="78b94-105">このガイダンスは、HoloLens 2 の Holographic リモート処理に固有のものです。</span><span class="sxs-lookup"><span data-stu-id="78b94-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

<span data-ttu-id="78b94-106">カスタムデータチャネルを使用して、確立されたリモート処理接続を介してカスタムデータを送信します。</span><span class="sxs-lookup"><span data-stu-id="78b94-106">Use custom data channels to send custom data over an established remoting connection.</span></span>

>[!IMPORTANT]
><span data-ttu-id="78b94-107">カスタムデータチャネルには、カスタムホストアプリとカスタムプレーヤーアプリが必要です。これは、2つのカスタムアプリ間の通信を可能にするためです。</span><span class="sxs-lookup"><span data-stu-id="78b94-107">Custom data channels require a custom host app and a custom player app, as it allows for communication between the two custom apps.</span></span>

>[!TIP]
><span data-ttu-id="78b94-108">単純なピンポン方の例については、 [Holographic リモート処理サンプル github リポジトリ](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples)内のホストとプレーヤーのサンプルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="78b94-108">A simple ping-pong example can be found in the host and player samples inside the [Holographic Remoting samples github repository](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span></span> <span data-ttu-id="78b94-109">サンプル```#define ENABLE_CUSTOM_DATA_CHANNEL_SAMPLE```コードを有効にするには、samplehostmain .h/SamplePlayerMain ファイル内でコメントを解除します。</span><span class="sxs-lookup"><span data-stu-id="78b94-109">Uncomment ```#define ENABLE_CUSTOM_DATA_CHANNEL_SAMPLE``` inside the SampleHostMain.h / SamplePlayerMain.h files to enable the sample code.</span></span>


# <a name="create-a-custom-data-channel"></a><span data-ttu-id="78b94-110">カスタムデータチャネルを作成する</span><span class="sxs-lookup"><span data-stu-id="78b94-110">Create a custom data channel</span></span>


<span data-ttu-id="78b94-111">カスタムデータチャネルを作成するには、次のフィールドが必要です。</span><span class="sxs-lookup"><span data-stu-id="78b94-111">To create a custom data channel, the following fields are required:</span></span>
```cpp
std::recursive_mutex m_customDataChannelLock;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel m_customDataChannel = nullptr;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnDataReceived_revoker m_customChannelDataReceivedEventRevoker;
winrt::Microsoft::Holographic::AppRemoting::IDataChannel::OnClosed_revoker m_customChannelClosedEventRevoker;
```

<span data-ttu-id="78b94-112">接続が正常に確立されると、ホスト側とプレーヤー側のどちらからでも、新しいデータチャネルの作成を開始できます。</span><span class="sxs-lookup"><span data-stu-id="78b94-112">After a connection was successfully established, the creation of new data channels can be initiated from either the host side and/or the player side.</span></span> <span data-ttu-id="78b94-113">Remotecontext と PlayerContext はどちらも、これ```CreateDataChannel()```を行うための方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="78b94-113">Both the RemoteContext and the PlayerContext provide a ```CreateDataChannel()``` method to do this.</span></span> <span data-ttu-id="78b94-114">最初のパラメーターは、susequent 操作でデータチャネルを識別するために使用されるチャネル ID です。</span><span class="sxs-lookup"><span data-stu-id="78b94-114">The first parameter is the channel ID which is used to identify the data channel in susequent operations.</span></span> <span data-ttu-id="78b94-115">2番目のパラメーターは、このチャネルのデータを相手側に転送する優先度を指定する優先順位です。</span><span class="sxs-lookup"><span data-stu-id="78b94-115">The second paramter is the priority which specifies the priority with which data of this channel is transfered to the other side.</span></span> <span data-ttu-id="78b94-116">チャネル Id の有効な範囲は、ホスト64側の場合は63、プレーヤー側の場合は127を含む0になります。</span><span class="sxs-lookup"><span data-stu-id="78b94-116">The valid range for channel IDs is 0 up to and including 63 for the host side and 64 up to and including 127 for the player side.</span></span> <span data-ttu-id="78b94-117">有効な優先```Low```順位```Medium```は```High``` 、、または (両側) です。</span><span class="sxs-lookup"><span data-stu-id="78b94-117">Valid priorities are ```Low```, ```Medium``` or ```High``` (on both sides).</span></span>

<span data-ttu-id="78b94-118">**ホスト**側でデータチャネルの作成を開始するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="78b94-118">To initiate the creation of a data channel on the **host** side:</span></span>
```cpp
// Valid channel ids for channels created on the host side are 0 up to and including 63
m_remoteContext.CreateDataChannel(0, DataChannelPriority::Low);
```

<span data-ttu-id="78b94-119">**プレーヤー**側でデータチャネルの作成を開始するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="78b94-119">To initiate the creation of a data channel on the **player** side:</span></span>
```cpp
// Valid channel ids for channels created on the player side are 64 up to and including 127
m_playerContext.CreateDataChannel(64, DataChannelPriority::Low);
```

>[!NOTE]
><span data-ttu-id="78b94-120">新しいカスタムデータチャネルを作成するには、1つの```CreateDataChannel```側 (ホストまたはプレーヤー) だけがメソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="78b94-120">To create a new custom data channel, only one side (either host or player) needs to call the ```CreateDataChannel``` method.</span></span>

## <a name="handling-custom-data-channel-events"></a><span data-ttu-id="78b94-121">カスタムデータチャネルイベントの処理</span><span class="sxs-lookup"><span data-stu-id="78b94-121">Handling custom data channel events</span></span>

<span data-ttu-id="78b94-122">カスタムデータチャネル```OnDataChannelCreated```を確立するには、(プレーヤーとホスト側の両方で) イベントを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="78b94-122">To establish a custom data channel, the ```OnDataChannelCreated``` event needs to be handled (on both the player and the host side).</span></span> <span data-ttu-id="78b94-123">このメソッドは、ユーザーデータチャネルがいずれかの側で作成され```IDataChannel``` 、このチャネルを介してデータを送受信するために使用できるオブジェクトを提供するときにトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="78b94-123">It triggers when a user data channel has been created by either side and provides a ```IDataChannel``` object, which can be used to send and receive data over this channel.</span></span>

<span data-ttu-id="78b94-124">```OnDataChannelCreated```イベントにリスナーを登録するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="78b94-124">To register a listener on the ```OnDataChannelCreated``` event:</span></span>
```cpp
m_onDataChannelCreatedEventRevoker = m_remoteContext.OnDataChannelCreated(winrt::auto_revoke,
    [this](const IDataChannel& dataChannel, uint8_t channelId)
    {
        std::lock_guard lock(m_customDataChannelLock);
        m_customDataChannel = dataChannel;

        // Register to OnDataReceived and OnClosed event of the data channel here, see below...
    });
```

<span data-ttu-id="78b94-125">データを受信したときに通知を受け取るに```OnDataReceived```は、 ```OnDataChannelCreated```ハンドラー ```IDataChannel```によって提供されるオブジェクトのイベントに登録します。</span><span class="sxs-lookup"><span data-stu-id="78b94-125">To get notified when data is received, register to the ```OnDataReceived``` event on the ```IDataChannel``` object provided by the ```OnDataChannelCreated``` handler.</span></span> <span data-ttu-id="78b94-126">データチャネルが```OnClosed```閉じられたときに通知を受け取るには、イベントに登録します。</span><span class="sxs-lookup"><span data-stu-id="78b94-126">Register to the ```OnClosed``` event, to get notified when the data channel has been closed.</span></span>

```cpp
m_customChannelDataReceivedEventRevoker = m_customDataChannel.OnDataReceived(winrt::auto_revoke, 
    [this]()
    {
        // React on data received via the custom data channel here.
    });

m_customChannelClosedEventRevoker = m_customDataChannel.OnClosed(winrt::auto_revoke,
    [this]()
    {
        // React on data channel closed here.

        std::lock_guard lock(m_customDataChannelLock);
        if (m_customDataChannel)
        {
            m_customDataChannel = nullptr;
        }
    });
```

## <a name="sending-data"></a><span data-ttu-id="78b94-127">データの送信</span><span class="sxs-lookup"><span data-stu-id="78b94-127">Sending data</span></span>

<span data-ttu-id="78b94-128">カスタムデータチャネルを介して```IDataChannel::SendData()```データを送信するには、メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="78b94-128">To send data over a custom data channel, use the ```IDataChannel::SendData()``` method.</span></span> <span data-ttu-id="78b94-129">1つ目のパラメーター ```winrt::array_view<const uint8_t>```は、送信する必要があるデータのです。</span><span class="sxs-lookup"><span data-stu-id="78b94-129">The first paramter is a ```winrt::array_view<const uint8_t>``` to the data that should be send.</span></span> <span data-ttu-id="78b94-130">2番目のパラメーターは、もう一方の側が受信を承認するまで、データを再送信するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="78b94-130">The second parameter specifies wheter the data should be resend, until the other side acknowledge the reception.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="78b94-131">ネットワークの状態が正しくない場合は、同じデータパケットが複数回到着する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="78b94-131">In case of bad network conditions, the same data packet might arrive more than once.</span></span> <span data-ttu-id="78b94-132">受信コードでは、この状況に対処できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="78b94-132">The receiving code must be able to handle this situation.</span></span>

```cpp
uint8_t data[] = {1};
m_customDataChannel.SendData(data, true);
```

## <a name="closing-a-custom-data-channel"></a><span data-ttu-id="78b94-133">カスタムデータチャネルを閉じる</span><span class="sxs-lookup"><span data-stu-id="78b94-133">Closing a custom data channel</span></span>

<span data-ttu-id="78b94-134">カスタムデータチャネルを閉じるには、 ```IDataChannel::Close()```メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="78b94-134">To close a custom data channel, use the ```IDataChannel::Close()``` method.</span></span> <span data-ttu-id="78b94-135">カスタムデータチャネルが閉じられる```OnClosed```と、イベントによって両方の側に通知されます。</span><span class="sxs-lookup"><span data-stu-id="78b94-135">Both sides will be notified by the ```OnClosed``` event once the custom data channel has been closed.</span></span>

```cpp
m_customDataChannel.Close();
```

## <a name="see-also"></a><span data-ttu-id="78b94-136">関連項目</span><span class="sxs-lookup"><span data-stu-id="78b94-136">See Also</span></span>
* [<span data-ttu-id="78b94-137">Holographic Remoting ホストアプリの作成</span><span class="sxs-lookup"><span data-stu-id="78b94-137">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="78b94-138">カスタム Holographic リモート処理プレーヤーアプリの作成</span><span class="sxs-lookup"><span data-stu-id="78b94-138">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="78b94-139">Holographic リモート処理のトラブルシューティングと制限事項</span><span class="sxs-lookup"><span data-stu-id="78b94-139">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="78b94-140">Holographic リモート処理ソフトウェアライセンス条項</span><span class="sxs-lookup"><span data-stu-id="78b94-140">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="78b94-141">Microsoft のプライバシーに関する声明</span><span class="sxs-lookup"><span data-stu-id="78b94-141">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)