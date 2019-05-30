---
Description: 長い形式の継続的なディクテーション音声入力をキャプチャし、認識する方法について説明します。
title: 継続的なディクテーションの有効化
ms.assetid: 383B3E23-1678-4FBB-B36E-6DE2DA9CA9DC
label: Continuous dictation
template: detail.hbs
keywords: スピーチ, 音声, 音声認識, 自然言語, ディクテーション, 入力, ユーザーの操作
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 3709a9076ce1d258ce2eca7f97aa1478088a9044
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66363564"
---
# <a name="continuous-dictation"></a><span data-ttu-id="de683-104">継続的なディクテーション</span><span class="sxs-lookup"><span data-stu-id="de683-104">Continuous dictation</span></span>

<span data-ttu-id="de683-105">長い形式の継続的なディクテーション音声入力をキャプチャし、認識する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="de683-105">Learn how to capture and recognize long-form, continuous dictation speech input.</span></span>

> <span data-ttu-id="de683-106">**重要な API**:[**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession)、 [ **ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession)</span><span class="sxs-lookup"><span data-stu-id="de683-106">**Important APIs**: [**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession), [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession)</span></span>

<span data-ttu-id="de683-107">「[音声認識](speech-recognition.md)」では、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) オブジェクトの [**RecognizeAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizeasync) メソッドまたは [**RecognizeWithUIAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizewithuiasync) メソッドを使って、比較的短い音声入力をキャプチャし、認識する方法について説明しました。たとえば、ショート メッセージ サービス (SMS) のメッセージを作成したり、質問したりする場合です。</span><span class="sxs-lookup"><span data-stu-id="de683-107">In [Speech recognition](speech-recognition.md), you learned how to capture and recognize relatively short speech input using the [**RecognizeAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizeasync) or [**RecognizeWithUIAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizewithuiasync) methods of a [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) object, for example, when composing a short message service (SMS) message or when asking a question.</span></span>

<span data-ttu-id="de683-108">ディクテーションまたはメールなど、より長い継続的な音声認識セッションの場合は、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) の [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティを使って [**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession) オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="de683-108">For longer, continuous speech recognition sessions, such as dictation or email, use the [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) property of a [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) to obtain a [**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession) object.</span></span>

> [!NOTE]
> <span data-ttu-id="de683-109">音声入力言語のサポートによって異なります、[デバイス](https://docs.microsoft.com/windows/uwp/design/devices/)アプリが実行されています。</span><span class="sxs-lookup"><span data-stu-id="de683-109">Dictation language support depends on the [device](https://docs.microsoft.com/windows/uwp/design/devices/) where your app is running.</span></span> <span data-ttu-id="de683-110">Pc とラップトップの場合は、EN-US のみは認識、音声認識でサポートされているすべての言語を認識できる Xbox や携帯電話中に。</span><span class="sxs-lookup"><span data-stu-id="de683-110">For PCs and laptops, only en-US is recognized, while Xbox and phones can recognize all languages supported by speech recognition.</span></span> <span data-ttu-id="de683-111">詳細については、次を参照してください。[音声認識エンジンの言語を指定](specify-the-speech-recognizer-language.md)します。</span><span class="sxs-lookup"><span data-stu-id="de683-111">For more info, see [Specify the speech recognizer language](specify-the-speech-recognizer-language.md).</span></span>

## <a name="set-up"></a><span data-ttu-id="de683-112">設定</span><span class="sxs-lookup"><span data-stu-id="de683-112">Set up</span></span>

<span data-ttu-id="de683-113">アプリには、継続的なディクテーション セッションを管理するためのオブジェクトがいくつか必要です。</span><span class="sxs-lookup"><span data-stu-id="de683-113">Your app needs a few objects to manage a continuous dictation session:</span></span>

- <span data-ttu-id="de683-114">1 インスタンスの [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="de683-114">An instance of a [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) object.</span></span>
- <span data-ttu-id="de683-115">ディクテーション中の UI を更新するための UI ディスパッチャーへの参照。</span><span class="sxs-lookup"><span data-stu-id="de683-115">A reference to a UI dispatcher to update the UI during dictation.</span></span>
- <span data-ttu-id="de683-116">ユーザーが発声し、蓄積された単語を追跡する方法。</span><span class="sxs-lookup"><span data-stu-id="de683-116">A way to track the accumulated words spoken by the user.</span></span>

<span data-ttu-id="de683-117">ここでは、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) インスタンスを、コード ビハインド クラスのプライベート フィールドとして宣言します。</span><span class="sxs-lookup"><span data-stu-id="de683-117">Here, we declare a [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) instance as a private field of the code-behind class.</span></span> <span data-ttu-id="de683-118">継続的なディクテーションが、1 つの XAML (Extensible Application Markup Language) ページを超えて持続する場合、アプリは、参照を別の場所に格納する必要があります。</span><span class="sxs-lookup"><span data-stu-id="de683-118">Your app needs to store a reference elsewhere if you want continuous dictation to persist beyond a single Extensible Application Markup Language (XAML) page.</span></span>

```CSharp
private SpeechRecognizer speechRecognizer;
```

<span data-ttu-id="de683-119">ディクテーション中に認識エンジンは、バックグラウンド スレッドからイベントを生成します。</span><span class="sxs-lookup"><span data-stu-id="de683-119">During dictation, the recognizer raises events from a background thread.</span></span> <span data-ttu-id="de683-120">バックグラウンド スレッドは、XAML の UI を直接更新できないため、アプリはディスパッチャーを使って、認識イベントに応答して UI を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="de683-120">Because a background thread cannot directly update the UI in XAML, your app must use a dispatcher to update the UI in response to recognition events.</span></span>

<span data-ttu-id="de683-121">ここでは、プライベート フィールドを宣言し、それが後で UI ディスパッチャーで初期化されます。</span><span class="sxs-lookup"><span data-stu-id="de683-121">Here, we declare a private field that will be initialized later with the UI dispatcher.</span></span>

```CSharp
// Speech events may originate from a thread other than the UI thread.
// Keep track of the UI thread dispatcher so that we can update the
// UI in a thread-safe manner.
private CoreDispatcher dispatcher;
```

<span data-ttu-id="de683-122">ユーザーが発声した内容を追跡するには、音声認識エンジンによって生成された認識イベントを処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="de683-122">To track what the user is saying, you need to handle recognition events raised by the speech recognizer.</span></span> <span data-ttu-id="de683-123">これらのイベントは、ユーザーの発声のチャンクを認識した結果を提供します。</span><span class="sxs-lookup"><span data-stu-id="de683-123">These events provide the recognition results for chunks of user utterances.</span></span>

<span data-ttu-id="de683-124">ここでは、[**StringBuilder**](https://docs.microsoft.com/dotnet/api/system.text.stringbuilder?redirectedfrom=MSDN) オブジェクトを使って、セッション中に取得したすべての認識結果を保持します。</span><span class="sxs-lookup"><span data-stu-id="de683-124">Here, we use a [**StringBuilder**](https://docs.microsoft.com/dotnet/api/system.text.stringbuilder?redirectedfrom=MSDN) object to hold all the recognition results obtained during the session.</span></span> <span data-ttu-id="de683-125">新しい検索結果は、処理されるに従って **StringBuilder** に追加されます。</span><span class="sxs-lookup"><span data-stu-id="de683-125">New results are appended to the **StringBuilder** as they are processed.</span></span>

```CSharp
private StringBuilder dictatedTextBuilder;
```

## <a name="initialization"></a><span data-ttu-id="de683-126">初期化</span><span class="sxs-lookup"><span data-stu-id="de683-126">Initialization</span></span>

<span data-ttu-id="de683-127">継続的な音声認識の初期化時には、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="de683-127">During the initialization of continuous speech recognition, you must:</span></span>

- <span data-ttu-id="de683-128">連続的な認識のイベント ハンドラーでアプリの UI を更新する場合は、UI スレッドのディスパッチャーを取得します。</span><span class="sxs-lookup"><span data-stu-id="de683-128">Fetch the dispatcher for the UI thread if you update the UI of your app in the continuous recognition event handlers.</span></span>
- <span data-ttu-id="de683-129">音声認識エンジンを初期化します。</span><span class="sxs-lookup"><span data-stu-id="de683-129">Initialize the speech recognizer.</span></span>
- <span data-ttu-id="de683-130">組み込みのディクテーション文法をコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="de683-130">Compile the built-in dictation grammar.</span></span>
    <span data-ttu-id="de683-131">**注**  音声認識が認識可能なボキャブラリを定義するには少なくとも 1 つの制約が必要です。</span><span class="sxs-lookup"><span data-stu-id="de683-131">**Note**   Speech recognition requires at least one constraint to define a recognizable vocabulary.</span></span> <span data-ttu-id="de683-132">制約が指定されていない場合は、定義済みのディクテーション文法が使われます。</span><span class="sxs-lookup"><span data-stu-id="de683-132">If no constraint is specified, a predefined dictation grammar is used.</span></span> <span data-ttu-id="de683-133">「[音声認識](speech-recognition.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="de683-133">See [Speech recognition](speech-recognition.md).</span></span>
- <span data-ttu-id="de683-134">認識イベントのイベント リスナーをセットアップします。</span><span class="sxs-lookup"><span data-stu-id="de683-134">Set up the event listeners for recognition events.</span></span>

<span data-ttu-id="de683-135">この例では、[**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) ページ イベントで音声認識を初期化します。</span><span class="sxs-lookup"><span data-stu-id="de683-135">In this example, we initialize speech recognition in the [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) page event.</span></span>

1. <span data-ttu-id="de683-136">音声認識エンジンが生成するイベントはバックグラウンド スレッドで発生するため、UI スレッドを更新するためのディスパッチャーへの参照を作成します。</span><span class="sxs-lookup"><span data-stu-id="de683-136">Because events raised by the speech recognizer occur on a background thread, create a reference to the dispatcher for updates to the UI thread.</span></span> <span data-ttu-id="de683-137">[**OnNavigatedTo** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto)が UI スレッドで常に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="de683-137">[**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) is always invoked on the UI thread.</span></span>
```csharp
this.dispatcher = CoreWindow.GetForCurrentThread().Dispatcher;
```

2.  <span data-ttu-id="de683-138">その後、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) インスタンスを初期化します。</span><span class="sxs-lookup"><span data-stu-id="de683-138">We then initialize the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) instance.</span></span>
```csharp
this.speechRecognizer = new SpeechRecognizer();
```

3.  <span data-ttu-id="de683-139">そして、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) によって認識される語句と単語をすべて定義する文法を追加し、コンパイルします。</span><span class="sxs-lookup"><span data-stu-id="de683-139">We then add and compile the grammar that defines all of the words and phrases that can be recognized by the [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer).</span></span>

    <span data-ttu-id="de683-140">文法を明示的に指定しない場合は、既定で定義済みのディクテーション文法が使われます。</span><span class="sxs-lookup"><span data-stu-id="de683-140">If you don't specify a grammar explicitly, a predefined dictation grammar is used by default.</span></span> <span data-ttu-id="de683-141">通常、一般的なディクテーションには、既定の文法が最適です。</span><span class="sxs-lookup"><span data-stu-id="de683-141">Typically, the default grammar is best for general dictation.</span></span>

    <span data-ttu-id="de683-142">ここでは、文法を追加せずに、すぐに [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="de683-142">Here, we call [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync) immediately without adding a grammar.</span></span>

    
```csharp
SpeechRecognitionCompilationResult result =
      await speechRecognizer.CompileConstraintsAsync();
```

## <a name="handle-recognition-events"></a><span data-ttu-id="de683-143">認識イベントの処理</span><span class="sxs-lookup"><span data-stu-id="de683-143">Handle recognition events</span></span>

<span data-ttu-id="de683-144">[  **RecognizeAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizeasync) または [**RecognizeWithUIAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizewithuiasync) を呼び出して、1 つの短い発声または語句をキャプチャできます。</span><span class="sxs-lookup"><span data-stu-id="de683-144">You can capture a single, brief utterance or phrase by calling [**RecognizeAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizeasync) or [**RecognizeWithUIAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizewithuiasync).</span></span> 

<span data-ttu-id="de683-145">ただし、より長い継続的な認識セッションをキャプチャするには、ユーザーが話す間にバックグラウンドで動作するイベント リスナーを指定し、ディクテーション文字列を作成するためのハンドラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="de683-145">However, to capture a longer, continuous recognition session, we specify event listeners to run in the background as the user speaks and define handlers to build the dictation string.</span></span>

<span data-ttu-id="de683-146">そして、認識エンジンの [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティを使って、継続的な認識セッションを管理するためのメソッドとイベントを提供する [**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession) オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="de683-146">We then use the [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) property of our recognizer to obtain a [**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession) object that provides methods and events for managing a continuous recognition session.</span></span>

<span data-ttu-id="de683-147">特に、次の 2 つのイベントが重要です。</span><span class="sxs-lookup"><span data-stu-id="de683-147">Two events in particular are critical:</span></span>

- <span data-ttu-id="de683-148">[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated)、認識エンジンがいくつかの結果を生成されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="de683-148">[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated), which occurs when the recognizer has generated some results.</span></span>
- <span data-ttu-id="de683-149">[**完了した**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed)、継続的な認識セッションが終了した場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="de683-149">[**Completed**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed), which occurs when the continuous recognition session has ended.</span></span>

<span data-ttu-id="de683-150">[  **ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントは、ユーザーが発声すると発生します。</span><span class="sxs-lookup"><span data-stu-id="de683-150">The [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event is raised as the user speaks.</span></span> <span data-ttu-id="de683-151">認識エンジンは、ユーザーの発声を聞き続け、音声入力のチャンクを渡すイベントを定期的に生成します。</span><span class="sxs-lookup"><span data-stu-id="de683-151">The recognizer continuously listens to the user and periodically raises an event that passes a chunk of speech input.</span></span> <span data-ttu-id="de683-152">音声入力は、イベントの引数の [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) プロパティを使って確認し、イベント ハンドラーで適切な処置を行う必要があります。たとえば、StringBuilder オブジェクトにテキストを追加します。</span><span class="sxs-lookup"><span data-stu-id="de683-152">You must examine the speech input, using the [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) property of the event argument, and take appropriate action in the event handler, such as appending the text to a StringBuilder object.</span></span>

<span data-ttu-id="de683-153">[  **SpeechRecognitionResult**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResult) のインスタンスである [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) プロパティは、音声入力を受け入れるかどうかを決定するために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="de683-153">As an instance of [**SpeechRecognitionResult**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResult), the [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) property is useful for determining whether you want to accept the speech input.</span></span> <span data-ttu-id="de683-154">[  **SpeechRecognitionResult**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResult) には、このための 2 つのプロパティが用意されています。</span><span class="sxs-lookup"><span data-stu-id="de683-154">A [**SpeechRecognitionResult**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResult) provides two properties for this:</span></span>

- <span data-ttu-id="de683-155">[**ステータス**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.status)認識が成功したかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="de683-155">[**Status**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.status) indicates whether the recognition was successful.</span></span> <span data-ttu-id="de683-156">さまざまな原因により、認識できない場合もあります。</span><span class="sxs-lookup"><span data-stu-id="de683-156">Recognition can fail for a variety of reasons.</span></span>
- <span data-ttu-id="de683-157">[**信頼度**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.confidence)相対の信頼性、認識エンジンに正しい単語が理解されていることを示します。</span><span class="sxs-lookup"><span data-stu-id="de683-157">[**Confidence**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.confidence) indicates the relative confidence that the recognizer understood the correct words.</span></span>

<span data-ttu-id="de683-158">継続的な認識をサポートするための基本的な手順は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="de683-158">Here are the basic steps for supporting continuous recognition:</span></span>  

1. <span data-ttu-id="de683-159">ここでは、[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) 継続的認識イベントのハンドラーを [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) ページ イベントに登録します。</span><span class="sxs-lookup"><span data-stu-id="de683-159">Here, we register the handler for the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) continuous recognition event in the [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) page event.</span></span>
```csharp
speechRecognizer.ContinuousRecognitionSession.ResultGenerated +=
        ContinuousRecognitionSession_ResultGenerated;
```

2.  <span data-ttu-id="de683-160">そして、[**Confidence**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.confidence) プロパティを確認します。</span><span class="sxs-lookup"><span data-stu-id="de683-160">We then check the [**Confidence**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.confidence) property.</span></span> <span data-ttu-id="de683-161">Confidence の値が [**Medium**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionConfidence) 以上である場合は、StringBuilder にテキストを追加します。</span><span class="sxs-lookup"><span data-stu-id="de683-161">If the value of Confidence is [**Medium**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionConfidence) or better, we append the text to the StringBuilder.</span></span> <span data-ttu-id="de683-162">入力の収集時に UI も更新します。</span><span class="sxs-lookup"><span data-stu-id="de683-162">We also update the UI as we collect input.</span></span>

    <span data-ttu-id="de683-163">**注**  、 [ **ResultGenerated** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) UI を直接更新することはできませんが、バック グラウンド スレッドでイベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="de683-163">**Note**  the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event is raised on a background thread that cannot update the UI directly.</span></span> <span data-ttu-id="de683-164">ハンドラーは、UI を更新する必要がある場合 (として、\[音声認識と音声合成のサンプル\]は)、を通じて UI スレッドへの更新をディスパッチする必要があります、 [ **RunAsync** ](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows)ディスパッチャーのメソッド。</span><span class="sxs-lookup"><span data-stu-id="de683-164">If a handler needs to update the UI (as the \[Speech and TTS sample\] does), you must dispatch the updates to the UI thread through the [**RunAsync**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows) method of the dispatcher.</span></span>
```csharp
private async void ContinuousRecognitionSession_ResultGenerated(
      SpeechContinuousRecognitionSession sender,
      SpeechContinuousRecognitionResultGeneratedEventArgs args)
      {

        if (args.Result.Confidence == SpeechRecognitionConfidence.Medium ||
          args.Result.Confidence == SpeechRecognitionConfidence.High)
          {
            dictatedTextBuilder.Append(args.Result.Text + " ");

            await dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
              dictationTextBox.Text = dictatedTextBuilder.ToString();
              btnClearText.IsEnabled = true;
            });
          }
        else
        {
          await dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
              dictationTextBox.Text = dictatedTextBuilder.ToString();
            });
        }
      }
```

3.  <span data-ttu-id="de683-165">その後、[**Completed**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed) イベントを処理します。これが、継続的なディクテーションの終了を示します。</span><span class="sxs-lookup"><span data-stu-id="de683-165">We then handle the [**Completed**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed) event, which indicates the end of continuous dictation.</span></span>

    <span data-ttu-id="de683-166">セッションは、[**StopAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.stopasync) メソッドまたは [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) メソッド (次のセクションを参照) を呼び出すと終了します。</span><span class="sxs-lookup"><span data-stu-id="de683-166">The session ends when you call the [**StopAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.stopasync) or [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) methods (described the next section).</span></span> <span data-ttu-id="de683-167">セッションは、エラーが発生したときや、ユーザーが発声を停止したときに終了することもあります。</span><span class="sxs-lookup"><span data-stu-id="de683-167">The session can also end when an error occurs, or when the user has stopped speaking.</span></span> <span data-ttu-id="de683-168">イベントの引数の [**Status**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.status) プロパティを確認して、セッションが終了した理由を特定してください ([**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus))。</span><span class="sxs-lookup"><span data-stu-id="de683-168">Check the [**Status**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.status) property of the event argument to determine why the session ended ([**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus)).</span></span>

    <span data-ttu-id="de683-169">ここでは、[**Completed**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed) 継続的認識イベントのハンドラーを [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) ページ イベントに登録します。</span><span class="sxs-lookup"><span data-stu-id="de683-169">Here, we register the handler for the [**Completed**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed) continuous recognition event in the [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) page event.</span></span>
```csharp
speechRecognizer.ContinuousRecognitionSession.Completed +=
      ContinuousRecognitionSession_Completed;
```

4.  <span data-ttu-id="de683-170">イベント ハンドラーは Status プロパティを確認して、正常に認識できたかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="de683-170">The event handler checks the Status property to determine whether the recognition was successful.</span></span> <span data-ttu-id="de683-171">また、ユーザーが発声を停止した場合の処理も行います。</span><span class="sxs-lookup"><span data-stu-id="de683-171">It also handles the case where the user has stopped speaking.</span></span> <span data-ttu-id="de683-172">多くの場合、[**TimeoutExceeded**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) によって、正常に認識されたと見なされます。これは、ユーザーの発声が終了したことを意味するためです。</span><span class="sxs-lookup"><span data-stu-id="de683-172">Often, a [**TimeoutExceeded**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) is considered successful recognition as it means the user has finished speaking.</span></span> <span data-ttu-id="de683-173">快適に使えるように、このケースをコード内で処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="de683-173">You should handle this case in your code for a good experience.</span></span>

    <span data-ttu-id="de683-174">**注**  、 [ **ResultGenerated** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) UI を直接更新することはできませんが、バック グラウンド スレッドでイベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="de683-174">**Note**  the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event is raised on a background thread that cannot update the UI directly.</span></span> <span data-ttu-id="de683-175">ハンドラーは、UI を更新する必要がある場合 (として、\[音声認識と音声合成のサンプル\]は)、を通じて UI スレッドへの更新をディスパッチする必要があります、 [ **RunAsync** ](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows)ディスパッチャーのメソッド。</span><span class="sxs-lookup"><span data-stu-id="de683-175">If a handler needs to update the UI (as the \[Speech and TTS sample\] does), you must dispatch the updates to the UI thread through the [**RunAsync**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows) method of the dispatcher.</span></span>
```csharp
private async void ContinuousRecognitionSession_Completed(
      SpeechContinuousRecognitionSession sender,
      SpeechContinuousRecognitionCompletedEventArgs args)
      {
        if (args.Status != SpeechRecognitionResultStatus.Success)
        {
          if (args.Status == SpeechRecognitionResultStatus.TimeoutExceeded)
          {
            await dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
              rootPage.NotifyUser(
                "Automatic Time Out of Dictation",
                NotifyType.StatusMessage);

              DictationButtonText.Text = " Continuous Recognition";
              dictationTextBox.Text = dictatedTextBuilder.ToString();
            });
          }
          else
          {
            await dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
              rootPage.NotifyUser(
                "Continuous Recognition Completed: " + args.Status.ToString(),
                NotifyType.StatusMessage);

              DictationButtonText.Text = " Continuous Recognition";
            });
          }
        }
      }
```

## <a name="provide-ongoing-recognition-feedback"></a><span data-ttu-id="de683-176">実行中の認識に対するフィードバックの提供</span><span class="sxs-lookup"><span data-stu-id="de683-176">Provide ongoing recognition feedback</span></span>


<span data-ttu-id="de683-177">人が会話する場合は、話の内容を完全に理解するためにコンテキストが必要であることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="de683-177">When people converse, they often rely on context to fully understand what is being said.</span></span> <span data-ttu-id="de683-178">同様に、信頼性の高い認識結果を提供するために音声認識エンジンにコンテキストが必要である場合がよくあります。</span><span class="sxs-lookup"><span data-stu-id="de683-178">Similarly, the speech recognizer often needs context to provide high-confidence recognition results.</span></span> <span data-ttu-id="de683-179">たとえば、"weight" および "wait" という単語は、それ自体だけでは区別できないため、周囲の単語からコンテキストをさらに探り出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="de683-179">For example, by themselves, the words "weight" and "wait" are indistinguishable until more context can be gleaned from surrounding words.</span></span> <span data-ttu-id="de683-180">認識エンジンは、単語や語句を正しく認識したことを、ある程度確信するまでは、[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントを生成しません。</span><span class="sxs-lookup"><span data-stu-id="de683-180">Until the recognizer has some confidence that a word, or words, have been recognized correctly, it will not raise the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event.</span></span>

<span data-ttu-id="de683-181">したがって、ユーザーが話し続けても、認識エンジンが [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントを生成できると確信するまでは結果が表示されないため、ユーザーにとって快適とはいえない結果になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="de683-181">This can result in a less than ideal experience for the user as they continue speaking and no results are provided until the recognizer has high enough confidence to raise the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event.</span></span>

<span data-ttu-id="de683-182">この不十分な応答性を改善するには、[**HypothesisGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.hypothesisgenerated) イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="de683-182">Handle the [**HypothesisGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.hypothesisgenerated) event to improve this apparent lack of responsiveness.</span></span> <span data-ttu-id="de683-183">このイベントは、処理中の単語と一致すると思われる新しいセットを認識エンジンが生成するたびに発生します。</span><span class="sxs-lookup"><span data-stu-id="de683-183">This event is raised whenever the recognizer generates a new set of potential matches for the word being processed.</span></span> <span data-ttu-id="de683-184">イベント引数は、現在一致している内容を含む [**Hypothesis**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionhypothesisgeneratedeventargs.hypothesis) プロパティを提供します。</span><span class="sxs-lookup"><span data-stu-id="de683-184">The event argument provides an [**Hypothesis**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionhypothesisgeneratedeventargs.hypothesis) property that contains the current matches.</span></span> <span data-ttu-id="de683-185">話し続けるユーザーに、これらを表示して、処理がまだ続行されていることを知らせます。</span><span class="sxs-lookup"><span data-stu-id="de683-185">Show these to the user as they continue speaking and reassure them that processing is still active.</span></span> <span data-ttu-id="de683-186">認識エンジンが十分に確信し、認識結果が確定されたら、暫定の **Hypothesis** 結果を、[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントで提供される最終的な [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="de683-186">Once confidence is high and a recognition result has been determined, replace the interim **Hypothesis** results with the final [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) provided in the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event.</span></span>

<span data-ttu-id="de683-187">ここでは、仮のテキストと省略記号 ("…") を、出力 [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) の現在の値に追加します。</span><span class="sxs-lookup"><span data-stu-id="de683-187">Here, we append the hypothetical text and an ellipsis ("…") to the current value of the output [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox).</span></span> <span data-ttu-id="de683-188">テキスト ボックスの内容は、新しい仮の結果が生成されるたびに更新され、最後に、最終的な結果が [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントから取得されます。</span><span class="sxs-lookup"><span data-stu-id="de683-188">The contents of the text box are updated as new hypotheses are generated and until the final results are obtained from the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event.</span></span>

```CSharp
private async void SpeechRecognizer_HypothesisGenerated(
  SpeechRecognizer sender,
  SpeechRecognitionHypothesisGeneratedEventArgs args)
  {

    string hypothesis = args.Hypothesis.Text;
    string textboxContent = dictatedTextBuilder.ToString() + " " + hypothesis + " ...";

    await dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
    {
      dictationTextBox.Text = textboxContent;
      btnClearText.IsEnabled = true;
    });
  }
```

## <a name="start-and-stop-recognition"></a><span data-ttu-id="de683-189">認識の開始と停止</span><span class="sxs-lookup"><span data-stu-id="de683-189">Start and stop recognition</span></span>


<span data-ttu-id="de683-190">認識セッションを開始する前に、音声認識エンジンの [**State**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.state) プロパティの値を確認します。</span><span class="sxs-lookup"><span data-stu-id="de683-190">Before starting a recognition session, check the value of the speech recognizer [**State**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.state) property.</span></span> <span data-ttu-id="de683-191">音声認識エンジンは、[**Idle**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizerState) 状態である必要があります。</span><span class="sxs-lookup"><span data-stu-id="de683-191">The speech recognizer must be in an [**Idle**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizerState) state.</span></span>

<span data-ttu-id="de683-192">音声認識エンジンの状態を確認した後、音声認識エンジンの [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティの [**StartAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.startasync) メソッドを呼び出してセッションを開始します。</span><span class="sxs-lookup"><span data-stu-id="de683-192">After checking the state of the speech recognizer, we start the session by calling the [**StartAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.startasync) method of the speech recognizer's [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) property.</span></span>

```CSharp
if (speechRecognizer.State == SpeechRecognizerState.Idle)
{
  await speechRecognizer.ContinuousRecognitionSession.StartAsync();
}
```

<span data-ttu-id="de683-193">認識を停止するには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="de683-193">Recognition can be stopped in two ways:</span></span>

-   <span data-ttu-id="de683-194">[**StopAsync** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.stopasync)認識イベントの完全な保留中のことができます ([**ResultGenerated** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated)続けますが、認識保留中のすべての操作が完了するまでに発生します)。</span><span class="sxs-lookup"><span data-stu-id="de683-194">[**StopAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.stopasync) lets any pending recognition events complete ([**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) continues to be raised until all pending recognition operations are complete).</span></span>
-   <span data-ttu-id="de683-195">[**CancelAsync** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync)がすぐに認識セッションを終了し、保留中の結果を破棄します。</span><span class="sxs-lookup"><span data-stu-id="de683-195">[**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) terminates the recognition session immediately and discards any pending results.</span></span>

<span data-ttu-id="de683-196">音声認識エンジンの状態を確認したら、音声認識エンジンの [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティの [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) メソッドを呼び出してセッションを停止します。</span><span class="sxs-lookup"><span data-stu-id="de683-196">After checking the state of the speech recognizer, we stop the session by calling the [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) method of the speech recognizer's [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) property.</span></span>

```CSharp
if (speechRecognizer.State != SpeechRecognizerState.Idle)
{
  await speechRecognizer.ContinuousRecognitionSession.CancelAsync();
}
```

> [!NOTE]
> <span data-ttu-id="de683-197">[  **CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) を呼び出した後に [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントが発生する場合があります。</span><span class="sxs-lookup"><span data-stu-id="de683-197">A [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event can occur after a call to [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync).</span></span>  
> <span data-ttu-id="de683-198">マルチスレッドであるために、[**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) を呼び出したときに [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントがスタックに残っている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="de683-198">Because of multithreading, a [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) event might still remain on the stack when [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) is called.</span></span> <span data-ttu-id="de683-199">その場合は、**ResultGenerated** イベントも発生します。</span><span class="sxs-lookup"><span data-stu-id="de683-199">If so, the **ResultGenerated** event still fires.</span></span>  
> <span data-ttu-id="de683-200">プライベート フィールドを設定しているときに認識セッションをキャンセルした場合は、その値を常に [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) ハンドラーで確認してください。</span><span class="sxs-lookup"><span data-stu-id="de683-200">If you set any private fields when canceling the recognition session, always confirm their values in the [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) handler.</span></span> <span data-ttu-id="de683-201">たとえば、セッションをキャンセルしたときにプライベート フィールドを null に設定している場合はハンドラー内でフィールドが初期化されると想定しないでください。</span><span class="sxs-lookup"><span data-stu-id="de683-201">For example, don't assume a field is initialized in your handler if you set them to null when you cancel the session.</span></span>

 

## <a name="related-articles"></a><span data-ttu-id="de683-202">関連記事</span><span class="sxs-lookup"><span data-stu-id="de683-202">Related articles</span></span>


* [<span data-ttu-id="de683-203">音声操作</span><span class="sxs-lookup"><span data-stu-id="de683-203">Speech interactions</span></span>](speech-interactions.md)

<span data-ttu-id="de683-204">**サンプル**</span><span class="sxs-lookup"><span data-stu-id="de683-204">**Samples**</span></span>
* [<span data-ttu-id="de683-205">音声認識と音声合成のサンプル</span><span class="sxs-lookup"><span data-stu-id="de683-205">Speech recognition and speech synthesis sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 




