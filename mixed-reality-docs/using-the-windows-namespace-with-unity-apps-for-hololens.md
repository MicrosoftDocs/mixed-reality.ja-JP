---
title: HoloLens 用 Unity を使用した WinRT Api
description: HoloLens の Unity プロジェクトで WinRT Api (Windows 名前空間) を使用する方法について説明します。
author: mikeriches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Unity、WinRT、windows mixed reality、API、チュートリアル
ms.openlocfilehash: 80f950d7571a936e93eb08490ad83dbb34a50b3a
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277990"
---
# <a name="winrt-apis-with-unity-for-hololens"></a>HoloLens 用 Unity を使用した WinRT Api

このページでは、HoloLens の Unity プロジェクトで WinRT Api を使用する方法について説明します。

## <a name="mixed-reality-apis"></a>Mixed Reality Api

Windows SDK のサブセットが混在している .NET Standard 2.0 互換性のある投影で使用できるようになりました。これは、プリプロセッサディレクティブなしでプロジェクトで使用できます。 これには、ほとんどの Api が含まれています。このような名前空間には、後で追加の Api を含めるために拡張されることがあります。 予測された Api は、エディターでの実行中に使用できます。これにより、[再生モード](https://docs.microsoft.com//windows/mixed-reality/unity-play-mode)を使用できるようになります。 この投影法を使用するには、プロジェクトに次の変更を加えます。

1) [Unity 用の nuget](https://github.com/GlitchEnzo/NuGetForUnity)を使用して、 [MixedReality](https://www.nuget.org/packages/Microsoft.Windows.MixedReality.DotNetWinRT)の nuget パッケージへの参照を追加します。
2) `Microsoft.`を使用した `Windows` 名前空間へのプレフィックス参照:
```cs
using namespace Microsoft.Windows.Perception.Spatial;
```
3) ネイティブポインターキャストを `FromNativePtr`に置き換えます。
```cs
var worldOrigin = SpatialCoordinateSystem.FromNativePtr(unityWorldOriginPtr);
```

## <a name="conditionally-include-winrt-api-calls"></a>条件付きで WinRT API 呼び出しを含める

また、プリプロセッサディレクティブを使用して、ユニバーサル Windows プラットフォームと Xbox One プラットフォーム用に構築された Unity プロジェクトに対して WinRT Api を活用することもできます。WinRT Api を対象とする Unity スクリプトで作成するすべてのコードは、それらのビルドに対して条件付きで含める必要があります。 

これは、Unity の2つの手順で行うことができます。
1) プレーヤーの設定で、API 互換性レベルを **.net 4.6**または **.NET Standard 2.0**に設定する必要があります。
    -  > **Player** > **Configuration** > **Api の互換性レベル**を **.net 4.6**または **.NET Standard 2.0**に > **プロジェクト設定**を**編集**する
2) プリプロセッサディレクティブ**ENABLE_WINMD_SUPPORT**は、WinRT を利用したコードをラップする必要があります

次のコードスニペットは、[スクリプトのC#ユニバーサル WINDOWS プラットフォーム: WinRT API](https://docs.unity3d.com/Manual/windowsstore-scripts.html)の Unity 手動ページから抜粋したものです。 この例では、広告 ID が返されますが、UWP と Xbox One のみがビルドされます。

```
using UnityEngine;
public class WinRTAPI : MonoBehaviour {
    void Update() {
        auto adId = GetAdvertisingId();
        // ...
    }

    string GetAdvertisingId() {
        #if ENABLE_WINMD_SUPPORT
            return Windows.System.UserProfile.AdvertisingManager.AdvertisingId;
        #else
            return "";
        #endif
    }
}
```

## <a name="edit-your-scripts-in-a-unity-c-project"></a>Unity C#プロジェクトでスクリプトを編集する

Unity エディターでスクリプトをダブルクリックすると、既定ではエディタープロジェクトでスクリプトが起動されます。 Visual Studio プロジェクトで Windows ランタイムが参照されていないため、WinRT Api は不明であるように見えます。 さらに、 **ENABLE_WINMD_SUPPORT**ディレクティブは未定義になり、 *#if*ラップされたコードは、UWP Visual Studio ソリューションにプロジェクトをビルドするまで無視されます。

## <a name="see-also"></a>参照
* [Unity Visual Studio ソリューションのエクスポートとビルド](exporting-and-building-a-unity-visual-studio-solution.md)
* [Unity のサポート Windows ランタイム](https://docs.unity3d.com/Manual/IL2CPP-WindowsRuntimeSupport.html)
