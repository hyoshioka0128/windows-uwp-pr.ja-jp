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
# <a name="continuous-dictation"></a>継続的なディクテーション

長い形式の継続的なディクテーション音声入力をキャプチャし、認識する方法について説明します。

> **重要な API**:[**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession)、 [ **ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession)

「[音声認識](speech-recognition.md)」では、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) オブジェクトの [**RecognizeAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizeasync) メソッドまたは [**RecognizeWithUIAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizewithuiasync) メソッドを使って、比較的短い音声入力をキャプチャし、認識する方法について説明しました。たとえば、ショート メッセージ サービス (SMS) のメッセージを作成したり、質問したりする場合です。

ディクテーションまたはメールなど、より長い継続的な音声認識セッションの場合は、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) の [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティを使って [**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession) オブジェクトを取得します。

> [!NOTE]
> 音声入力言語のサポートによって異なります、[デバイス](https://docs.microsoft.com/windows/uwp/design/devices/)アプリが実行されています。 Pc とラップトップの場合は、EN-US のみは認識、音声認識でサポートされているすべての言語を認識できる Xbox や携帯電話中に。 詳細については、次を参照してください。[音声認識エンジンの言語を指定](specify-the-speech-recognizer-language.md)します。

## <a name="set-up"></a>設定

アプリには、継続的なディクテーション セッションを管理するためのオブジェクトがいくつか必要です。

- 1 インスタンスの [**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) オブジェクト。
- ディクテーション中の UI を更新するための UI ディスパッチャーへの参照。
- ユーザーが発声し、蓄積された単語を追跡する方法。

ここでは、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) インスタンスを、コード ビハインド クラスのプライベート フィールドとして宣言します。 継続的なディクテーションが、1 つの XAML (Extensible Application Markup Language) ページを超えて持続する場合、アプリは、参照を別の場所に格納する必要があります。

```CSharp
private SpeechRecognizer speechRecognizer;
```

ディクテーション中に認識エンジンは、バックグラウンド スレッドからイベントを生成します。 バックグラウンド スレッドは、XAML の UI を直接更新できないため、アプリはディスパッチャーを使って、認識イベントに応答して UI を更新する必要があります。

ここでは、プライベート フィールドを宣言し、それが後で UI ディスパッチャーで初期化されます。

```CSharp
// Speech events may originate from a thread other than the UI thread.
// Keep track of the UI thread dispatcher so that we can update the
// UI in a thread-safe manner.
private CoreDispatcher dispatcher;
```

ユーザーが発声した内容を追跡するには、音声認識エンジンによって生成された認識イベントを処理する必要があります。 これらのイベントは、ユーザーの発声のチャンクを認識した結果を提供します。

ここでは、[**StringBuilder**](https://docs.microsoft.com/dotnet/api/system.text.stringbuilder?redirectedfrom=MSDN) オブジェクトを使って、セッション中に取得したすべての認識結果を保持します。 新しい検索結果は、処理されるに従って **StringBuilder** に追加されます。

```CSharp
private StringBuilder dictatedTextBuilder;
```

## <a name="initialization"></a>初期化

継続的な音声認識の初期化時には、次の操作を行う必要があります。

- 連続的な認識のイベント ハンドラーでアプリの UI を更新する場合は、UI スレッドのディスパッチャーを取得します。
- 音声認識エンジンを初期化します。
- 組み込みのディクテーション文法をコンパイルします。
    **注**  音声認識が認識可能なボキャブラリを定義するには少なくとも 1 つの制約が必要です。 制約が指定されていない場合は、定義済みのディクテーション文法が使われます。 「[音声認識](speech-recognition.md)」をご覧ください。
- 認識イベントのイベント リスナーをセットアップします。

この例では、[**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) ページ イベントで音声認識を初期化します。

1. 音声認識エンジンが生成するイベントはバックグラウンド スレッドで発生するため、UI スレッドを更新するためのディスパッチャーへの参照を作成します。 [**OnNavigatedTo** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto)が UI スレッドで常に呼び出されます。
```csharp
this.dispatcher = CoreWindow.GetForCurrentThread().Dispatcher;
```

2.  その後、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) インスタンスを初期化します。
```csharp
this.speechRecognizer = new SpeechRecognizer();
```

3.  そして、[**SpeechRecognizer**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer) によって認識される語句と単語をすべて定義する文法を追加し、コンパイルします。

    文法を明示的に指定しない場合は、既定で定義済みのディクテーション文法が使われます。 通常、一般的なディクテーションには、既定の文法が最適です。

    ここでは、文法を追加せずに、すぐに [**CompileConstraintsAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.compileconstraintsasync) を呼び出します。

    
```csharp
SpeechRecognitionCompilationResult result =
      await speechRecognizer.CompileConstraintsAsync();
```

## <a name="handle-recognition-events"></a>認識イベントの処理

[  **RecognizeAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizeasync) または [**RecognizeWithUIAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.recognizewithuiasync) を呼び出して、1 つの短い発声または語句をキャプチャできます。 

ただし、より長い継続的な認識セッションをキャプチャするには、ユーザーが話す間にバックグラウンドで動作するイベント リスナーを指定し、ディクテーション文字列を作成するためのハンドラーを定義します。

そして、認識エンジンの [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティを使って、継続的な認識セッションを管理するためのメソッドとイベントを提供する [**SpeechContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechContinuousRecognitionSession) オブジェクトを取得します。

特に、次の 2 つのイベントが重要です。

- [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated)、認識エンジンがいくつかの結果を生成されたときに発生します。
- [**完了した**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed)、継続的な認識セッションが終了した場合に発生します。

[  **ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントは、ユーザーが発声すると発生します。 認識エンジンは、ユーザーの発声を聞き続け、音声入力のチャンクを渡すイベントを定期的に生成します。 音声入力は、イベントの引数の [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) プロパティを使って確認し、イベント ハンドラーで適切な処置を行う必要があります。たとえば、StringBuilder オブジェクトにテキストを追加します。

[  **SpeechRecognitionResult**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResult) のインスタンスである [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) プロパティは、音声入力を受け入れるかどうかを決定するために役立ちます。 [  **SpeechRecognitionResult**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResult) には、このための 2 つのプロパティが用意されています。

- [**ステータス**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.status)認識が成功したかどうかを示します。 さまざまな原因により、認識できない場合もあります。
- [**信頼度**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.confidence)相対の信頼性、認識エンジンに正しい単語が理解されていることを示します。

継続的な認識をサポートするための基本的な手順は次のとおりです。  

1. ここでは、[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) 継続的認識イベントのハンドラーを [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) ページ イベントに登録します。
```csharp
speechRecognizer.ContinuousRecognitionSession.ResultGenerated +=
        ContinuousRecognitionSession_ResultGenerated;
```

2.  そして、[**Confidence**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.confidence) プロパティを確認します。 Confidence の値が [**Medium**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionConfidence) 以上である場合は、StringBuilder にテキストを追加します。 入力の収集時に UI も更新します。

    **注**  、 [ **ResultGenerated** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) UI を直接更新することはできませんが、バック グラウンド スレッドでイベントが発生します。 ハンドラーは、UI を更新する必要がある場合 (として、\[音声認識と音声合成のサンプル\]は)、を通じて UI スレッドへの更新をディスパッチする必要があります、 [ **RunAsync** ](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows)ディスパッチャーのメソッド。
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

3.  その後、[**Completed**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed) イベントを処理します。これが、継続的なディクテーションの終了を示します。

    セッションは、[**StopAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.stopasync) メソッドまたは [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) メソッド (次のセクションを参照) を呼び出すと終了します。 セッションは、エラーが発生したときや、ユーザーが発声を停止したときに終了することもあります。 イベントの引数の [**Status**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionresult.status) プロパティを確認して、セッションが終了した理由を特定してください ([**SpeechRecognitionResultStatus**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus))。

    ここでは、[**Completed**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.completed) 継続的認識イベントのハンドラーを [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) ページ イベントに登録します。
```csharp
speechRecognizer.ContinuousRecognitionSession.Completed +=
      ContinuousRecognitionSession_Completed;
```

4.  イベント ハンドラーは Status プロパティを確認して、正常に認識できたかどうかを判断します。 また、ユーザーが発声を停止した場合の処理も行います。 多くの場合、[**TimeoutExceeded**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionResultStatus) によって、正常に認識されたと見なされます。これは、ユーザーの発声が終了したことを意味するためです。 快適に使えるように、このケースをコード内で処理する必要があります。

    **注**  、 [ **ResultGenerated** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) UI を直接更新することはできませんが、バック グラウンド スレッドでイベントが発生します。 ハンドラーは、UI を更新する必要がある場合 (として、\[音声認識と音声合成のサンプル\]は)、を通じて UI スレッドへの更新をディスパッチする必要があります、 [ **RunAsync** ](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows)ディスパッチャーのメソッド。
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

## <a name="provide-ongoing-recognition-feedback"></a>実行中の認識に対するフィードバックの提供


人が会話する場合は、話の内容を完全に理解するためにコンテキストが必要であることがよくあります。 同様に、信頼性の高い認識結果を提供するために音声認識エンジンにコンテキストが必要である場合がよくあります。 たとえば、"weight" および "wait" という単語は、それ自体だけでは区別できないため、周囲の単語からコンテキストをさらに探り出す必要があります。 認識エンジンは、単語や語句を正しく認識したことを、ある程度確信するまでは、[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントを生成しません。

したがって、ユーザーが話し続けても、認識エンジンが [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントを生成できると確信するまでは結果が表示されないため、ユーザーにとって快適とはいえない結果になる場合があります。

この不十分な応答性を改善するには、[**HypothesisGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.hypothesisgenerated) イベントを処理します。 このイベントは、処理中の単語と一致すると思われる新しいセットを認識エンジンが生成するたびに発生します。 イベント引数は、現在一致している内容を含む [**Hypothesis**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognitionhypothesisgeneratedeventargs.hypothesis) プロパティを提供します。 話し続けるユーザーに、これらを表示して、処理がまだ続行されていることを知らせます。 認識エンジンが十分に確信し、認識結果が確定されたら、暫定の **Hypothesis** 結果を、[**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントで提供される最終的な [**Result**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.result) に置き換えます。

ここでは、仮のテキストと省略記号 ("…") を、出力 [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) の現在の値に追加します。 テキスト ボックスの内容は、新しい仮の結果が生成されるたびに更新され、最後に、最終的な結果が [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントから取得されます。

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

## <a name="start-and-stop-recognition"></a>認識の開始と停止


認識セッションを開始する前に、音声認識エンジンの [**State**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.state) プロパティの値を確認します。 音声認識エンジンは、[**Idle**](https://docs.microsoft.com/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizerState) 状態である必要があります。

音声認識エンジンの状態を確認した後、音声認識エンジンの [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティの [**StartAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.startasync) メソッドを呼び出してセッションを開始します。

```CSharp
if (speechRecognizer.State == SpeechRecognizerState.Idle)
{
  await speechRecognizer.ContinuousRecognitionSession.StartAsync();
}
```

認識を停止するには、次の 2 つの方法があります。

-   [**StopAsync** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.stopasync)認識イベントの完全な保留中のことができます ([**ResultGenerated** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated)続けますが、認識保留中のすべての操作が完了するまでに発生します)。
-   [**CancelAsync** ](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync)がすぐに認識セッションを終了し、保留中の結果を破棄します。

音声認識エンジンの状態を確認したら、音声認識エンジンの [**ContinuousRecognitionSession**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.continuousrecognitionsession) プロパティの [**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) メソッドを呼び出してセッションを停止します。

```CSharp
if (speechRecognizer.State != SpeechRecognizerState.Idle)
{
  await speechRecognizer.ContinuousRecognitionSession.CancelAsync();
}
```

> [!NOTE]
> [  **CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) を呼び出した後に [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントが発生する場合があります。  
> マルチスレッドであるために、[**CancelAsync**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.cancelasync) を呼び出したときに [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) イベントがスタックに残っている可能性があります。 その場合は、**ResultGenerated** イベントも発生します。  
> プライベート フィールドを設定しているときに認識セッションをキャンセルした場合は、その値を常に [**ResultGenerated**](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated) ハンドラーで確認してください。 たとえば、セッションをキャンセルしたときにプライベート フィールドを null に設定している場合はハンドラー内でフィールドが初期化されると想定しないでください。

 

## <a name="related-articles"></a>関連記事


* [音声操作](speech-interactions.md)

**サンプル**
* [音声認識と音声合成のサンプル](https://go.microsoft.com/fwlink/p/?LinkID=619897)
 

 




