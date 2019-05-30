---
Description: 音声認識エンジンが無音または認識できないサウンド (雑音) を無視し、音声入力を待機する時間の長さを設定します。
title: 音声認識のタイムアウトの設定
ms.assetid: 58F446AC-4A56-454D-8125-62A2C4DBFCC8
label: Speech recognition timeouts
template: detail.hbs
keywords: スピーチ, 音声, 音声認識, 自然言語, ディクテーション, 入力, ユーザーの操作
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: f321b9ec43f2c844854600b8260a7fdc189c0446
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365386"
---
# <a name="set-speech-recognition-timeouts"></a><span data-ttu-id="76862-104">音声認識のタイムアウトの設定</span><span class="sxs-lookup"><span data-stu-id="76862-104">Set speech recognition timeouts</span></span>


<span data-ttu-id="76862-105">音声認識エンジンが無音または認識できないサウンド (雑音) を無視し、音声入力を待機する時間の長さを設定します。</span><span class="sxs-lookup"><span data-stu-id="76862-105">Set how long a speech recognizer ignores silence or unrecognizable sounds (babble) and continues listening for speech input.</span></span>

> <span data-ttu-id="76862-106">**重要な API**:[**タイムアウト**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.timeouts)、 [ **SpeechRecognizerTimeouts**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizerTimeouts)</span><span class="sxs-lookup"><span data-stu-id="76862-106">**Important APIs**: [**Timeouts**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.timeouts), [**SpeechRecognizerTimeouts**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizerTimeouts)</span></span>

## <a name="set-a-timeout"></a><span data-ttu-id="76862-107">タイムアウトの設定</span><span class="sxs-lookup"><span data-stu-id="76862-107">Set a timeout</span></span>


<span data-ttu-id="76862-108">ここでは、さまざまな [**Timeouts**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.timeouts) 値を指定します。</span><span class="sxs-lookup"><span data-stu-id="76862-108">Here, we specify various [**Timeouts**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.timeouts) values:</span></span>

-   <span data-ttu-id="76862-109">InitialSilenceTimeout: SpeechRecognizer が (認識結果が生成されるまでの) 無音を検出し、音声入力が続かないと見なす時間の長さ。</span><span class="sxs-lookup"><span data-stu-id="76862-109">InitialSilenceTimeout - The length of time that a SpeechRecognizer detects silence (before any recognition results have been generated) and assumes speech input is not forthcoming.</span></span>
-   <span data-ttu-id="76862-110">BabbleTimeout: SpeechRecognizer が、認識できないサウンド (雑音) のリッスンを継続し、音声入力が終了したと見なし、認識処理を終了するまでの時間の長さ。</span><span class="sxs-lookup"><span data-stu-id="76862-110">BabbleTimeout - The length of time that a SpeechRecognizer continues to listen to unrecognizable sounds (babble) before it assumes speech input has ended and finalizes the recognition operation.</span></span>
-   <span data-ttu-id="76862-111">EndSilenceTimeout: SpeechRecognizer が (認識結果が生成された後の) 無音を検出し、音声入力が終了したと見なす時間の長さ。</span><span class="sxs-lookup"><span data-stu-id="76862-111">EndSilenceTimeout - The length of time that a SpeechRecognizer detects silence (after recognition results have been generated) and assumes speech input has ended.</span></span>

<span data-ttu-id="76862-112">**注**  あたり認識エンジンごとにタイムアウトを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="76862-112">**Note**  Timeouts can be set on a per-recognizer basis.</span></span>

 

```CSharp
// Set timeout settings.
recognizer.Timeouts.InitialSilenceTimeout = TimeSpan.FromSeconds(6.0);
recognizer.Timeouts.BabbleTimeout = TimeSpan.FromSeconds(4.0);
recognizer.Timeouts.EndSilenceTimeout = TimeSpan.FromSeconds(1.2);
```

## <a name="related-articles"></a><span data-ttu-id="76862-113">関連記事</span><span class="sxs-lookup"><span data-stu-id="76862-113">Related articles</span></span>


* <span data-ttu-id="76862-114">[音声操作](speech-interactions.md)
**サンプル**</span><span class="sxs-lookup"><span data-stu-id="76862-114">[Speech interactions](speech-interactions.md)
**Samples**</span></span>
* [<span data-ttu-id="76862-115">音声認識と音声合成のサンプル</span><span class="sxs-lookup"><span data-stu-id="76862-115">Speech recognition and speech synthesis sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 




