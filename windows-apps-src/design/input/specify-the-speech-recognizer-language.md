---
Description: 音声認識に使われるインストール済みの言語を選ぶ方法について説明します。
title: 音声認識エンジンの言語の指定
ms.assetid: 4C463A1B-AF6A-46FD-A839-5D6724955B38
label: Specify the speech recognizer language
template: detail.hbs
keywords: スピーチ, 音声, 音声認識, 自然言語, ディクテーション, 入力, ユーザーの操作
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 778aa04861fa7704f4235763a429bb77f92a8b65
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365326"
---
# <a name="specify-the-speech-recognizer-language"></a><span data-ttu-id="40eda-104">音声認識エンジンの言語の指定</span><span class="sxs-lookup"><span data-stu-id="40eda-104">Specify the speech recognizer language</span></span>


<span data-ttu-id="40eda-105">音声認識に使われるインストール済みの言語を選ぶ方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="40eda-105">Learn how to select an installed language to use for speech recognition.</span></span>

> <span data-ttu-id="40eda-106">**重要な API**:[**SupportedTopicLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedtopiclanguages)、 [ **SupportedGrammarLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedgrammarlanguages)、 [**言語**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language)</span><span class="sxs-lookup"><span data-stu-id="40eda-106">**Important APIs**: [**SupportedTopicLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedtopiclanguages), [**SupportedGrammarLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedgrammarlanguages), [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language)</span></span>


<span data-ttu-id="40eda-107">ここでは、システムにインストールされている言語を列挙し、どの言語が既定の言語であるかを指定します。また、音声認識用に別の言語を選びます。</span><span class="sxs-lookup"><span data-stu-id="40eda-107">Here, we enumerate the languages installed on a system, identify which is the default language, and select a different language for recognition.</span></span>

<span data-ttu-id="40eda-108">**前提条件:**</span><span class="sxs-lookup"><span data-stu-id="40eda-108">**Prerequisites:**</span></span>

<span data-ttu-id="40eda-109">このトピックは、「[音声認識](speech-recognition.md)」に基づいています。</span><span class="sxs-lookup"><span data-stu-id="40eda-109">This topic builds on [Speech recognition](speech-recognition.md).</span></span>

<span data-ttu-id="40eda-110">音声認識と認識の制約についての基本的な知識が必要です。</span><span class="sxs-lookup"><span data-stu-id="40eda-110">You should have a basic understanding of speech recognition and recognition constraints.</span></span>

<span data-ttu-id="40eda-111">ユニバーサル Windows プラットフォーム (UWP) アプリを開発するのが初めての場合は、以下のトピックに目を通して、ここで説明されているテクノロジをよく理解できるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="40eda-111">If you're new to developing Universal Windows Platform (UWP) apps, have a look through these topics to get familiar with the technologies discussed here.</span></span>

-   [<span data-ttu-id="40eda-112">初めてのアプリの作成</span><span class="sxs-lookup"><span data-stu-id="40eda-112">Create your first app</span></span>](https://docs.microsoft.com/windows/uwp/get-started/your-first-app)
-   <span data-ttu-id="40eda-113">「[イベントとルーティング イベントの概要](https://docs.microsoft.com/windows/uwp/xaml-platform/events-and-routed-events-overview)」に記載されているイベントの説明</span><span class="sxs-lookup"><span data-stu-id="40eda-113">Learn about events with [Events and routed events overview](https://docs.microsoft.com/windows/uwp/xaml-platform/events-and-routed-events-overview)</span></span>

<span data-ttu-id="40eda-114">**ユーザー エクスペリエンス ガイドライン:**</span><span class="sxs-lookup"><span data-stu-id="40eda-114">**User experience guidelines:**</span></span>

<span data-ttu-id="40eda-115">魅力的な音声認識対応アプリの設計に役立つ便利なヒントについては、「[音声機能の設計ガイドライン](https://docs.microsoft.com/windows/uwp/input-and-devices/speech-interactions)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="40eda-115">For helpful tips about designing a useful and engaging speech-enabled app, see [Speech design guidelines](https://docs.microsoft.com/windows/uwp/input-and-devices/speech-interactions) .</span></span>

## <a name="identify-the-default-language"></a><span data-ttu-id="40eda-116">既定の言語を指定する</span><span class="sxs-lookup"><span data-stu-id="40eda-116">Identify the default language</span></span>


<span data-ttu-id="40eda-117">音声認識エンジンでは、システムの音声認識の言語を既定の認識言語として使います。</span><span class="sxs-lookup"><span data-stu-id="40eda-117">A speech recognizer uses the system speech language as its default recognition language.</span></span> <span data-ttu-id="40eda-118">この言語は、デバイスで [設定] &gt; [システム] &gt; [音声認識] &gt; [音声認識の言語] の順に移動し、画面上でユーザーが設定します。</span><span class="sxs-lookup"><span data-stu-id="40eda-118">This language is set by the user on the device Settings &gt; System &gt; Speech &gt; Speech Language screen.</span></span>

<span data-ttu-id="40eda-119">[  **SystemSpeechLanguage**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.systemspeechlanguage) 静的プロパティを調べて、既定の言語を特定します。</span><span class="sxs-lookup"><span data-stu-id="40eda-119">We identify the default language by checking the [**SystemSpeechLanguage**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.systemspeechlanguage) static property.</span></span>

```CSharp
var language = SpeechRecognizer.SystemSpeechLanguage; 
```

## <a name="confirm-an-installed-language"></a><span data-ttu-id="40eda-120">インストールされている言語を確認する</span><span class="sxs-lookup"><span data-stu-id="40eda-120">Confirm an installed language</span></span>


<span data-ttu-id="40eda-121">インストールされている言語はデバイスによって異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="40eda-121">Installed languages can vary between devices.</span></span> <span data-ttu-id="40eda-122">特定の制約を使う際にある言語に依存する場合は、その言語が存在するかどうかを確認してください。</span><span class="sxs-lookup"><span data-stu-id="40eda-122">You should verify the existence of a language if you depend on it for a particular constraint.</span></span>

<span data-ttu-id="40eda-123">**注**  新しい言語パックをインストールした後、再起動が必要です。</span><span class="sxs-lookup"><span data-stu-id="40eda-123">**Note**  A reboot is required after a new language pack is installed.</span></span> <span data-ttu-id="40eda-124">エラー コード SPERR 例外\_いない\_場合は、指定した言語がサポートされていないか、インストール終了していませんが見つかりました (0x8004503a) が発生します。</span><span class="sxs-lookup"><span data-stu-id="40eda-124">An exception with error code SPERR\_NOT\_FOUND (0x8004503a) is raised if the specified language is not supported or has not finished installing.</span></span>

 

<span data-ttu-id="40eda-125">[  **SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) クラスの 2 つの静的プロパティのいずれかを調べて、デバイスでサポートされる言語を特定します。</span><span class="sxs-lookup"><span data-stu-id="40eda-125">Determine the supported languages on a device by checking one of two static properties of the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) class:</span></span>

-   <span data-ttu-id="40eda-126">[**SupportedTopicLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedtopiclanguages)などのコレクション[**言語**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language)定義済みの音声入力と web 検索の文法と使用するオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="40eda-126">[**SupportedTopicLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedtopiclanguages)—The collection of [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language) objects used with predefined dictation and web search grammars.</span></span>

-   <span data-ttu-id="40eda-127">[**SupportedGrammarLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedgrammarlanguages)などのコレクション[**言語**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language)一覧制約または Speech Recognition Grammar Specification (SRGS) ファイルで使用されるオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="40eda-127">[**SupportedGrammarLanguages**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.supportedgrammarlanguages)—The collection of [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language) objects used with a list constraint or a Speech Recognition Grammar Specification (SRGS) file.</span></span>

## <a name="specify-a-language"></a><span data-ttu-id="40eda-128">言語を指定する</span><span class="sxs-lookup"><span data-stu-id="40eda-128">Specify a language</span></span>


<span data-ttu-id="40eda-129">言語を指定するには、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) コンストラクターで [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language) オブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="40eda-129">To specify a language, pass a [**Language**](https://docs.microsoft.com/uwp/api/Windows.Globalization.Language) object in the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) constructor.</span></span>

<span data-ttu-id="40eda-130">ここでは、認識言語として "en-US" を指定します。</span><span class="sxs-lookup"><span data-stu-id="40eda-130">Here, we specify "en-US" as the recognition language.</span></span>


```CSharp
var language = new Windows.Globalization.Language(“en-US”); 
var recognizer = new SpeechRecognizer(language); 
```

## <a name="remarks"></a><span data-ttu-id="40eda-131">注釈</span><span class="sxs-lookup"><span data-stu-id="40eda-131">Remarks</span></span>


<span data-ttu-id="40eda-132">トピック制約を構成するには、[**SpeechRecognitionTopicConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionTopicConstraint) を [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) の [**Constraints**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.constraints) コレクションに追加して、[**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="40eda-132">A topic constraint can be configured by adding a [**SpeechRecognitionTopicConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionTopicConstraint) to the [**Constraints**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.constraints) collection of the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) and then calling [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync).</span></span> <span data-ttu-id="40eda-133">サポートされているトピックの言語で認識エンジンが初期化されていない場合は、**TopicLanguageNotSupported** の [**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) が返されます。</span><span class="sxs-lookup"><span data-stu-id="40eda-133">A [**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) of **TopicLanguageNotSupported** is returned if the recognizer is not initialized with a supported topic language.</span></span>

<span data-ttu-id="40eda-134">一覧の制約を構成するには、[**SpeechRecognitionListConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionListConstraint) を [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) の [**Constraints**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.constraints) コレクションに追加して、[**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="40eda-134">A list constraint is configured by adding a [**SpeechRecognitionListConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionListConstraint) to the [**Constraints**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.constraints) collection of the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) and then calling [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync).</span></span> <span data-ttu-id="40eda-135">カスタム一覧の言語を直接指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="40eda-135">You cannot specify the language of a custom list directly.</span></span> <span data-ttu-id="40eda-136">代わりに、認識エンジンの言語を使って一覧が処理されます。</span><span class="sxs-lookup"><span data-stu-id="40eda-136">Instead, the list will be processed using the language of the recognizer.</span></span>

<span data-ttu-id="40eda-137">SRGS 文法は、[**SpeechRecognitionGrammarFileConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionGrammarFileConstraint) クラスによって表されるオープン スタンダードの XML 形式です。</span><span class="sxs-lookup"><span data-stu-id="40eda-137">An SRGS grammar is an open-standard XML format represented by the [**SpeechRecognitionGrammarFileConstraint**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionGrammarFileConstraint) class.</span></span> <span data-ttu-id="40eda-138">カスタム一覧とは異なり、SRGS マークアップで文法の言語を指定できます。</span><span class="sxs-lookup"><span data-stu-id="40eda-138">Unlike custom lists, you can specify the language of the grammar in the SRGS markup.</span></span> <span data-ttu-id="40eda-139">[**CompileConstraintsAsync** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync)が失敗し、 [ **SpeechRecognitionResultStatus** ](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus)の**TopicLanguageNotSupported**場合、認識エンジンSRGS マークアップと同じ言語には初期化されません。</span><span class="sxs-lookup"><span data-stu-id="40eda-139">[**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync) fails with a [**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) of **TopicLanguageNotSupported** if the recognizer is not initialized to the same language as the SRGS markup.</span></span>

## <a name="related-articles"></a><span data-ttu-id="40eda-140">関連記事</span><span class="sxs-lookup"><span data-stu-id="40eda-140">Related articles</span></span>

<span data-ttu-id="40eda-141">**開発者向け**</span><span class="sxs-lookup"><span data-stu-id="40eda-141">**Developers**</span></span>

* [<span data-ttu-id="40eda-142">音声操作</span><span class="sxs-lookup"><span data-stu-id="40eda-142">Speech interactions</span></span>](speech-interactions.md)

<span data-ttu-id="40eda-143">**デザイナー向け**</span><span class="sxs-lookup"><span data-stu-id="40eda-143">**Designers**</span></span>

* [<span data-ttu-id="40eda-144">音声認識のデザイン ガイドライン</span><span class="sxs-lookup"><span data-stu-id="40eda-144">Speech design guidelines</span></span>](https://docs.microsoft.com/windows/uwp/input-and-devices/speech-interactions)

<span data-ttu-id="40eda-145">**サンプル**</span><span class="sxs-lookup"><span data-stu-id="40eda-145">**Samples**</span></span>

* [<span data-ttu-id="40eda-146">音声認識と音声合成のサンプル</span><span class="sxs-lookup"><span data-stu-id="40eda-146">Speech recognition and speech synthesis sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 




