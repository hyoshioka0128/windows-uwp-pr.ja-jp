---
ms.assetid: 03A74239-D4B6-4E41-B2FA-6C04F225B844
title: "\"Hello, world\" アプリを作成する方法 (XAML)"
description: Extensible Application Markup Language (XAML) を使用して、C#簡単なこんにちは, world アプリを Windows 10 ユニバーサル Windows プラットフォーム (UWP) を対象とするを作成します。
ms.date: 03/06/2017
ms.topic: article
keywords: windows 10, uwp, 初めてのアプリ, hello world
ms.localizationpriority: medium
ms.openlocfilehash: d9a7f0302dfdc9f9fa980f0fe93a3371328f9e5c
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66367432"
---
# <a name="create-a-hello-world-app-xaml"></a>"Hello, world" アプリを作成する (XAML)

このチュートリアルには、XAML を使用する方法が説明しますとC#すると、単純な「こんにちは, world」アプリで Windows 10 ユニバーサル Windows プラットフォーム (UWP) の。 Microsoft Visual Studio での 1 つのプロジェクトでは、任意の Windows 10 デバイスで実行されているアプリを構築できます。

ここでは、次の方法について説明します。

-   新規作成**Visual Studio**を対象とするプロジェクト**Windows 10**と**UWP**します。
-   スタート ページの UI を変更するように XAML を記述する。
-   Visual Studio のローカル デスクトップでプロジェクトを実行する。
-   SpeechSynthesizer を使って、ボタンが押されたときにアプリがコンテンツを読み上げるようにする。


## <a name="before-you-start"></a>はじめに...

-   [ユニバーサル Windows アプリとは何ですか。](universal-application-platform-guide.md)
-   [Visual Studio 2017 (および Windows 10) をダウンロードします](https://developer.microsoft.com/windows/downloads)。 サポートが必要な場合は、[セットアップする](get-set-up.md)方法をご覧ください。
-   また、Visual Studio の既定のウィンドウ レイアウトを使用することを前提としています。 既定のレイアウトを変更した場合は、 **[ウィンドウ]** メニューの **[ウィンドウ レイアウトのリセット]** を使って、レイアウトをリセットできます。

> [!NOTE]
> このチュートリアルでは、Visual Studio Community 2017 を使います。 異なるバージョンの Visual Studio を使っている場合には、見た目が多少異なることがあります。

## <a name="video-summary"></a>ビデオの概要

<iframe src="https://channel9.msdn.com/Blogs/One-Dev-Minute/Writing-Your-First-Windows-10-App/player" width="640" height="360" allowFullScreen frameBorder="0"></iframe>



## <a name="step-1-create-a-new-project-in-visual-studio"></a>手順 1:Visual Studio で新しいプロジェクトを作成します。

1.  Visual Studio を起動します。

2.  **ファイル**メニューの **新規 > プロジェクト**を開く、*新しいプロジェクト*ダイアログ。

3.  左側のテンプレートの一覧から選択**インストール済み > Visual C# > Windows ユニバーサル**UWP プロジェクト テンプレートの一覧を表示します。

    ユニバーサル テンプレートが表示されない場合は、UWP アプリを作成するためのコンポーネントがない可能性があります。 インストール プロセスを繰り返して UWP サポートを追加することもできます ( *[新しいプロジェクト]* ダイアログで **[Visual Studio インストーラーを開く]** をクリック)。 参照してください[設定](get-set-up.md))。

    ![インストール プロセスを繰り返す方法](images/win10-cs-install.png)

4.  **[空白のアプリ (ユニバーサル Windows)]** テンプレートを選択し、 **[名前]** に「HelloWorld」と入力します。 **[OK]** を選択します。

    ![[新しいプロジェクト] ウィンドウ](images/win10-cs-01.png)

> [!NOTE]
> Visual Studio を初めて使う場合は、[設定] ダイアログ ボックスが表示され、**開発者モード**を有効にするよう求められることがあります。 開発者モードは、アプリをストアからだけではなく、直接実行するためのアクセス許可など、特定の機能を有効にする特別な設定です。 詳しくは、「[デバイスを開発用に有効にする](enable-your-device-for-development.md)」をご覧ください。 先に進むには、 **[開発者モード]** を選択し、 **[はい]** をクリックしてダイアログ ボックスを閉じます。

 ![開発者モードのアクティブ化ダイアログ](images/win10-cs-00.png)

5.  ターゲット バージョンと最小バージョンのダイアログが表示されます。 このチュートリアルでは既定の設定で問題ないため、 **[OK]** を選択してプロジェクトを作成します。

    ![ソリューション エクスプローラーのウィンドウ](images/win10-cs-02.png)

6.  新しいプロジェクトが開き、そのプロジェクトのファイルが右側の**ソリューション エクスプローラー**のウィンドウに表示されます。 場合によっては、ファイルを表示するために **[ソリューション エクスプローラー]** タブを選択する必要があります ( **[プロパティ]** タブではありません)。

    ![ソリューション エクスプローラーのウィンドウ](images/win10-cs-03.png)

**[空白のアプリ (ユニバーサル Windows)]** は最小限のテンプレートですが、多くのファイルが含まれています。 これらのファイルは、C# を使うすべての UWP アプリに必要です。 Visual Studio で作るすべてのプロジェクトには、これらのファイルが必ず含まれます。


### <a name="whats-in-the-files"></a>ファイルの内容

プロジェクトのファイルを表示して編集するには、**ソリューション エクスプローラー**でファイルをダブルクリックします。 フォルダーと同様、XAML ファイルを展開して、関連するコード ファイルを表示します。 XAML ファイルは、デザイン サーフェスと XAML エディターの両方を表示する分割ビューで開きます。
> [!NOTE]
> XAML とは Extensible Application Markup Language (XAML) は、アプリのユーザー インターフェイスを定義するための言語です。 XAML は、手動で入力することも、Visual Studio のデザイン ツールを使って作成することもできます。 .xaml ファイルには、ロジックが格納される .xaml.cs 分離コード ファイルがあります。 XAML と分離コードがまとまって、完全なクラスが作成されます。 詳しくは、「[XAML の概要](https://docs.microsoft.com/windows/uwp/xaml-platform/xaml-overview)」をご覧ください。

*App.xaml と App.xaml.cs*

-   App.xaml は、アプリ全体で使われるリソースを宣言するファイルです。
-   App.xaml.cs は、App.xaml の分離コード ファイルです。 すべての分離コード ページと同じように、`InitializeComponent` メソッドを呼び出すコンストラクターが含まれています。 `InitializeComponent` メソッドは自分で記述する必要はありません。 Visual Studio によって生成されるこのメソッドの主な目的は、XAML ファイルに宣言された要素を初期化することです。
-   App.xaml.cs は、アプリのエントリ ポイントです。
-   App.xaml.cs に処理するメソッドも含まれています[アクティベーション](../launch-resume/activate-an-app.md)と[中断](../launch-resume/suspend-an-app.md)アプリの。

*MainPage.xaml*

-   MainPage.xaml は、アプリの UI を定義する場所です。 要素の追加は、XAML マークアップを使って直接行うことも、Visual Studio のデザイン ツールを使って行うこともできます。
-   MainPage.xaml.cs は、MainPage.xaml のコード ビハインド ページです。 ここには、アプリのロジックとイベント ハンドラーを追加します。
-   これら 2 つのファイルで、[**Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) から継承される `MainPage` という新しいクラスを `HelloWorld` 名前空間に定義します。

*Package.appxmanifest*
-   名前、説明、タイル、開始ページなど、アプリを説明するマニフェスト ファイルです。
-   依存関係、リソースと、アプリが含まれているファイルの一覧が含まれています。

*ロゴのイメージのセット*
-   Assets/Square150x150Logo.scale-200.png と Wide310x150Logo.scale 200.png は、[スタート] メニューで、アプリ (サイズは Medium または全体のいずれか) を表します。
-   Assets/Square44x44Logo.png では、[スタート] メニューのタスク バー、およびタスク マネージャーのアプリの一覧でアプリを表します。
-   Assets/StoreLogo.png は、Microsoft Store 内のアプリを表します。
-   Assets/SplashScreen.scale-200.png は、アプリが起動したときに表示するスプラッシュ画面です。
-   システムがロックされているときに、ロック画面にアプリを表す Assets/LockScreenLogo.scale-200.png を使用できます。

## <a name="step-2-adding-a-button"></a>手順 2:ボタンの追加

### <a name="using-the-designer-view"></a>デザイナー ビューの使用

ページにボタンを追加しましょう。 このチュートリアルで使用するファイルの一部にすぎません前の表にします。App.xaml、MainPage.xaml で、MainPage.xaml.cs

1.  **MainPage.xaml** をダブルクリックしてデザイン ビューで開きます。

    画面の上部にグラフィック ビュー、その下部に XAML コード ビューがあります。 どちらのビューでも変更を加えることができますが、ここではグラフィック ビューを使います。

    ![ソリューション エクスプローラーのウィンドウ](images/win10-cs-04.png)

2.  左側の縦方向に配置された **[ツールボックス]** タブをクリックして UI コントロールの一覧を開きます  (タイトル バーのピン アイコンをクリックすると、このウィンドウを表示したままにすることができます)。

    ![ソリューション エクスプローラーのウィンドウ](images/win10-cs-05.png)

3.  **[コモン XAML コントロール]** を展開し、**Button** をドラッグしてデザイン キャンバスの中央に配置します。

    ![ソリューション エクスプローラーのウィンドウ](images/win10-cs-06.png)

    XAML コード ウィンドウを見ると、そこにも Button が追加されたことがわかります。

 ```XAML
<Button x:name="button" Content="Button" HorizontalAlignment="Left" Margin = "152,293,0,0" VerticalAlignment="Top"/>
 ```

4.  ボタンのテキストを変更します。

    XAML コード ビュー内をクリックし、Content の値を "Button" から "Hello, world!" に変更します。

```XAML
<Button x:name="button" Content="Hello, world!" HorizontalAlignment="Left" Margin = "152,293,0,0" VerticalAlignment="Top"/>
```

デザイン キャンバスに表示されたボタンが更新され、新しいテキストが表示されることがわかります。

![ソリューション エクスプローラーのウィンドウ](images/win10-cs-07.png)

## <a name="step-3-start-the-app"></a>手順 3:アプリを起動します


ここまでの操作で、非常に単純なアプリが作成されました。 ここで、アプリをビルド、デプロイ、起動してどうなるかを見てみましょう。 アプリは、ローカル コンピューター、シミュレーターかエミュレーター、またはリモート デバイスでデバッグできます。 Visual Studio の [ターゲット デバイス] メニューを示します。

![アプリをデバッグするデバイス ターゲットのドロップダウン リスト](images/uap-debug.png)

### <a name="start-the-app-on-a-desktop-device"></a>デスクトップ デバイスでアプリを起動する

既定では、アプリはローカル コンピューターで実行されます。 [ターゲット デバイス] メニューには、デスクトップ デバイス ファミリのデバイスでアプリをデバッグするためのいくつかのオプションが用意されています。

-   **シミュレーター**
-   **ローカル コンピューター**
-   **リモート コンピューター**

**ローカル コンピューターでデバッグを開始するには**

1.  **[標準]** ツール バーの [ターゲット デバイス] メニュー (![[デバッグの開始] メニュー](images/startdebug-full.png)) で、 **[ローカル コンピューター]** が選択されていることを確認します  (既定で選択されています)。
2.  ツール バーの **[デバッグの開始]** ボタン (![[デバッグの開始] ボタン](images/startdebug-sm.png)) をクリックします。

   または

   **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。

   または

   F5 キーを押す。

アプリがウィンドウで開かれ、最初に既定のスプラッシュ画面が表示されます。 スプラッシュ画面は、画像 (SplashScreen.png) と背景色によって定義されます (背景色はアプリのマニフェスト ファイルに指定します)。

スプラッシュ画面が消えた後、アプリが表示されます。 次のようになります。

![アプリの初期画面](images/win10-cs-08.png)

Windows キーを押して **[スタート]** メニューを開き、すべてのアプリを表示します。 ローカルにデプロイしたアプリのタイルが **[スタート]** メニューに追加されています。 後でもう一度 (デバッグ モード以外で) アプリを実行するときは、 **[スタート]** メニューでこのタイルをタップまたはクリックします。

お疲れさまでした。これで、初めての UWP アプリの作成は完了です。

**デバッグを停止するには**

   ツール バーの **[デバッグの停止]** ボタン (![[デバッグの停止] ボタン](images/stopdebug.png)) をクリックします。

   または

   **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。

   または

   アプリ ウィンドウを閉じます。

## <a name="step-4-event-handlers"></a>手順 4:イベント ハンドラー

"イベント ハンドラー" は複雑なもののように聞こえますが、イベント (ユーザーによるボタンのクリックなど) が発生したときに呼び出されるコードの別名にすぎません。

1.  アプリの実行を停止します (まだ停止していない場合)。

2.  デザイン キャンバス上のボタン コントロールをダブルクリックします。Visual Studio によってボタンのイベント ハンドラーが作成されます。

  もちろん、すべてのコードを手動で作成することもできます。 または、ボタンをクリックして選択し、右下の **[プロパティ]** ウィンドウを確認します。 **[イベント]** (小さな稲妻) に切り替えると、イベント ハンドラーの名前を追加することができます。

3.  *MainPage.xaml.cs* (分離コード ページ) でイベント ハンドラーを編集します。 ここから面白くなります。 既定のイベント ハンドラーは次のようになります。

```cs
private void Button_Click(object sender, RoutedEventArgs e)
{

}
```

  これを変更して次のようにします。

```cs
private async void Button_Click(object sender, RoutedEventArgs e)
{
    MediaElement mediaElement = new MediaElement();
    var synth = new Windows.Media.SpeechSynthesis.SpeechSynthesizer();
    Windows.Media.SpeechSynthesis.SpeechSynthesisStream stream = await synth.SynthesizeTextToStreamAsync("Hello, World!");
    mediaElement.SetSource(stream, stream.ContentType);
    mediaElement.Play();
}
```

メソッド シグネチャが含まれて かどうかを確認、 **async**アプリを実行しようとすると、キーワード、またはすると、エラーが発生します。

### <a name="what-did-we-just-do"></a>ここで実行したこと

このコードでは、いくつか Windows API を使用して音声合成オブジェクトを作成し、読み上げるテキストを指定します  (SpeechSynthesis の使い方について詳しくは、[SpeechSynthesis 名前空間](https://docs.microsoft.com/uwp/api/windows.media.speechsynthesis)のドキュメントをご覧ください)。

アプリを実行し、ボタンをクリックすると、コンピューター (または電話) が "Hello, World!" を文字どおりにしゃべります。


## <a name="summary"></a>概要

これで、Windows 10 と UWP の最初のアプリを作成しました。

アプリで使うコントロールを XAML によってレイアウトする方法については、[グリッドに関するチュートリアル](../design/layout/grid-tutorial.md)で学習するか、直接[次のステップ](learn-more.md)に進んでください。

## <a name="see-also"></a>関連項目

* [最初のアプリ](your-first-app.md)
* [UWP アプリを公開する](https://developer.microsoft.com/store/publish-apps)
* [UWP アプリの開発に関する how-to 記事](https://developer.microsoft.com/windows/apps/develop)
* [UWP 開発者向けサンプル コード](https://developer.microsoft.com/windows/samples)
* [ユニバーサル Windows アプリとは何ですか。](universal-application-platform-guide.md)
* [Windows アカウントにサインアップします。](sign-up.md)
