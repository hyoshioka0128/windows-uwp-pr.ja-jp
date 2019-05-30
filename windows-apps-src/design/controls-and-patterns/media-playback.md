---
Description: ビデオ、オーディオ、および画像を表示したり聴いたりするには、メディア プレーヤーを使います。
title: メディア プレーヤー
ms.assetid: 9AABB5DE-1D81-4791-AB47-7F058F64C491
dev.assetid: AF2F2008-9B53-430C-BBC3-8888F631B0B0
label: Media player
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: b212ff435e58bdb8766972d1832bbf0690db3ed1
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66364740"
---
# <a name="media-player"></a><span data-ttu-id="b01de-104">メディア プレーヤー</span><span class="sxs-lookup"><span data-stu-id="b01de-104">Media player</span></span>



<span data-ttu-id="b01de-105">ビデオやオーディオを表示したり聴いたりするには、メディア プレーヤーを使います。</span><span class="sxs-lookup"><span data-stu-id="b01de-105">The media player is used to view and listen to video and audio.</span></span> <span data-ttu-id="b01de-106">メディアはインラインで (ページに埋め込むか、その他のコントロールのグループを使う) 再生するか、専用の全画面表示で再生できます。</span><span class="sxs-lookup"><span data-stu-id="b01de-106">Media playback can be inline (embedded in a page or with a group of other controls) or in a dedicated full-screen view.</span></span> <span data-ttu-id="b01de-107">プレーヤーのボタン セットやコントロール バーの背景を変更したり、必要に応じてレイアウトを整理したりできます。</span><span class="sxs-lookup"><span data-stu-id="b01de-107">You can modify the player's button set, change the background of the control bar, and arrange layouts as you see fit.</span></span> <span data-ttu-id="b01de-108">ユーザーが必要とするのは基本的なコントロール セット (再生/一時停止、巻き戻し、早送り) です。</span><span class="sxs-lookup"><span data-stu-id="b01de-108">Just keep in mind that users expect a basic control set (play/pause, skip back, skip forward).</span></span>

![トランスポート コントロールを含むメディア プレーヤー要素](images/controls/mtc_double_video_inprod.png)

> <span data-ttu-id="b01de-110">**重要な API**:[MediaPlayerElement クラス](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement)、 [MediaTransportControls クラス](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediatransportcontrols)</span><span class="sxs-lookup"><span data-stu-id="b01de-110">**Important APIs**: [MediaPlayerElement class](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement), [MediaTransportControls class](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediatransportcontrols)</span></span>


> [!NOTE]
> <span data-ttu-id="b01de-111">**MediaPlayerElement** は Windows 10 バージョン 1607 以降でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="b01de-111">**MediaPlayerElement** is only available in Windows 10, version 1607 and up.</span></span> <span data-ttu-id="b01de-112">Windows 10 の以前のバージョン用にアプリを開発する場合は、代わりに [MediaElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement) を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-112">If you are developing an app for an earlier version of Windows 10 you will need to use [MediaElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement) instead.</span></span> <span data-ttu-id="b01de-113">このページの推奨事項はすべて MediaElement にも適用されます。</span><span class="sxs-lookup"><span data-stu-id="b01de-113">All of the recommendations on this page apply to MediaElement as well.</span></span>

## <a name="is-this-the-right-control"></a><span data-ttu-id="b01de-114">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="b01de-114">Is this the right control?</span></span>

<span data-ttu-id="b01de-115">アプリでオーディオまたはビデオを再生する場合は、メディア プレーヤーを使います。</span><span class="sxs-lookup"><span data-stu-id="b01de-115">Use a media player when you want to play audio or video in your app.</span></span> <span data-ttu-id="b01de-116">画像のコレクションを表示するには、[フリップ ビュー](flipview.md)を使います。</span><span class="sxs-lookup"><span data-stu-id="b01de-116">To display a collection of images, use a [Flip view](flipview.md).</span></span>

## <a name="examples"></a><span data-ttu-id="b01de-117">例</span><span class="sxs-lookup"><span data-stu-id="b01de-117">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="b01de-118">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="b01de-118">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="b01de-119"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックしてアプリを開き、<a href="xamlcontrolsgallery:/item/MediaPlayerElement">MediaPlayerElement</a> または <a href="xamlcontrolsgallery:/item/MediaPlayer">MediaPlayer</a> の動作を確認してください。</span><span class="sxs-lookup"><span data-stu-id="b01de-119">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to open the app and see the <a href="xamlcontrolsgallery:/item/MediaPlayerElement">MediaPlayerElement</a> or <a href="xamlcontrolsgallery:/item/MediaPlayer">MediaPlayer</a> in action.</span></span></p>
    <ul>
    <li><span data-ttu-id="b01de-120"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="b01de-120"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="b01de-121"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="b01de-121"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

<span data-ttu-id="b01de-122">Windows 10 Get Started アプリのメディア プレイヤー。</span><span class="sxs-lookup"><span data-stu-id="b01de-122">A media player in the Windows 10 Get Started app.</span></span>

![Windows 10 Get Started アプリのメディア要素](images/control-examples/mtc_getstarted_example.png)

## <a name="create-a-media-player"></a><span data-ttu-id="b01de-124">メディア プレーヤーの作成</span><span class="sxs-lookup"><span data-stu-id="b01de-124">Create a media player</span></span>
<span data-ttu-id="b01de-125">XAML で [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) オブジェクトを作成してアプリにメディアを追加し、オーディオやビデオ ファイルを指定する [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) に [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) を設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-125">Add media to your app by creating a [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) object in XAML and set the [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) to a [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) that points to an audio or video file.</span></span>

<span data-ttu-id="b01de-126">この XAML は [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) を作成し、その [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) プロパティをアプリのローカルにあるビデオ ファイルの URI に設定するコードを示します。</span><span class="sxs-lookup"><span data-stu-id="b01de-126">This XAML creates a [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) and sets its [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) property to the URI of a video file that's local to the app.</span></span> <span data-ttu-id="b01de-127">ページが読み込まれると、**MediaPlayerElement** によって再生が開始します。</span><span class="sxs-lookup"><span data-stu-id="b01de-127">The **MediaPlayerElement** begins playing when the page loads.</span></span> <span data-ttu-id="b01de-128">メディアがすぐに再生されないようにするには、[AutoPlay](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.autoplay) プロパティを **false** に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-128">To suppress media from starting right away, you can set the [AutoPlay](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.autoplay) property to **false**.</span></span>

```xaml
<MediaPlayerElement x:Name="mediaSimple"
                    Source="ms-appx:///Videos/video1.mp4"
                    Width="400" AutoPlay="True"/>
```

<span data-ttu-id="b01de-129">この XAML は、組み込みのトランスポート コントロールを有効化し、さらに [AutoPlay](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.autoplay) プロパティを **false** に設定した [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) を作成します。</span><span class="sxs-lookup"><span data-stu-id="b01de-129">This XAML creates a [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) with the built in transport controls enabled and the [AutoPlay](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.autoplay) property set to **false.**</span></span>


```xaml
<MediaPlayerElement x:Name="mediaPlayer"
                    Source="ms-appx:///Videos/video1.mp4"
                    Width="400"
                    AutoPlay="False"
                    AreTransportControlsEnabled="True"/>
```

### <a name="media-transport-controls"></a><span data-ttu-id="b01de-130">メディア トランスポート コントロール</span><span class="sxs-lookup"><span data-stu-id="b01de-130">Media transport controls</span></span>
<span data-ttu-id="b01de-131">[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) には、再生、停止、一時停止、音量、ミュート、シーク (進行状況)、字幕、オーディオ トラックの選択を処理する組み込みのトランスポート コントロールがあります。</span><span class="sxs-lookup"><span data-stu-id="b01de-131">[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) has built in transport controls that handle play, stop, pause, volume, mute, seeking/progress, closed captions, and audio track selection.</span></span> <span data-ttu-id="b01de-132">これらのコントロールを有効にするには、[AreTransportControlsEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.AreTransportControlsEnabled) を **true** に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-132">To enable these controls, set [AreTransportControlsEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.AreTransportControlsEnabled) to **true**.</span></span> <span data-ttu-id="b01de-133">これらのコントロールを無効にするには、**AreTransportControlsEnabled** を **false** に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-133">To disable them, set **AreTransportControlsEnabled** to **false**.</span></span> <span data-ttu-id="b01de-134">トランスポート コントロールは、[MediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls) クラスで表されます。</span><span class="sxs-lookup"><span data-stu-id="b01de-134">The transport controls are represented by the [MediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls) class.</span></span> <span data-ttu-id="b01de-135">トランスポート コントロールは、そのまま使用することも、さまざまな方法でカスタマイズすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b01de-135">You can use the transport controls as-is, or customize them in various ways.</span></span> <span data-ttu-id="b01de-136">詳しくは、[MediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls) クラスのリファレンスと「[Create custom transport controls](custom-transport-controls.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-136">For more info, see the [MediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls) class reference and [Create custom transport controls](custom-transport-controls.md).</span></span>

<span data-ttu-id="b01de-137">トランスポート コントロールは 1 行および 2 行のレイアウトをサポートします。</span><span class="sxs-lookup"><span data-stu-id="b01de-137">The transport controls support single- and double-row layouts.</span></span> <span data-ttu-id="b01de-138">最初の例は、メディアのタイムラインの左側に再生/一時停止ボタンを配置した 1 行のレイアウトです。</span><span class="sxs-lookup"><span data-stu-id="b01de-138">The first example here is a single-row layout, with the play/pause button located to the left of the media timeline.</span></span> <span data-ttu-id="b01de-139">このレイアウトは、インライン メディア再生とコンパクトな画面に適しています。</span><span class="sxs-lookup"><span data-stu-id="b01de-139">This layout is best reserved for inline media playback and compact screens.</span></span>

![1 行の MTC コントロールの例](images/controls/mtc_single_inprod_02.png)

<span data-ttu-id="b01de-141">ほとんどの使用シナリオ (特に大きな画面) では、2 行のコントロールのレイアウト (下の図) をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b01de-141">The double-row controls layout (below) is recommended for most usage scenarios, especially on larger screens.</span></span> <span data-ttu-id="b01de-142">このレイアウトでは、コントロールの領域がより多く確保されており、ユーザーが簡単にタイムラインを操作できます。</span><span class="sxs-lookup"><span data-stu-id="b01de-142">This layout provides more space for controls and makes the timeline easier for the user to operate.</span></span>

![携帯電話に表示される 2 行の MTC コントロールの例](images/controls/mtc_double_inprod.png)

<span data-ttu-id="b01de-144">**システムのメディアのトランスポート コントロール**</span><span class="sxs-lookup"><span data-stu-id="b01de-144">**System media transport controls**</span></span>

<span data-ttu-id="b01de-145">[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) は、システム メディア トランスポート コントロールと自動的に統合されます。</span><span class="sxs-lookup"><span data-stu-id="b01de-145">[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) is automatically integrated with the system media transport controls.</span></span> <span data-ttu-id="b01de-146">システム メディア トランスポート コントロールは、キーボードのメディア ボタンなどのハードウェア メディア キーを押すとポップアップするコントロールです。</span><span class="sxs-lookup"><span data-stu-id="b01de-146">The system media transport controls are the controls that pop up when hardware media keys are pressed, such as the media buttons on keyboards.</span></span> <span data-ttu-id="b01de-147">詳しくは、[SystemMediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.Media.SystemMediaTransportControls) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-147">For more info, see [SystemMediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.Media.SystemMediaTransportControls).</span></span>

> <span data-ttu-id="b01de-148">**注**&nbsp; &nbsp; [MediaElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement)はメディアの輸送コントロール自身に接続する必要がありますので、システムと自動的に統合されません。</span><span class="sxs-lookup"><span data-stu-id="b01de-148">**Note**&nbsp;&nbsp; [MediaElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement) does not automatically integrate with the system media transport controls so you must connect them yourself.</span></span> <span data-ttu-id="b01de-149">詳しくは、「[システム メディア トランスポート コントロール](https://docs.microsoft.com/windows/uwp/audio-video-camera/system-media-transport-controls)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-149">For more information, see [System Media Transport Controls](https://docs.microsoft.com/windows/uwp/audio-video-camera/system-media-transport-controls).</span></span>


### <a name="set-the-media-source"></a><span data-ttu-id="b01de-150">メディア ソースを設定する</span><span class="sxs-lookup"><span data-stu-id="b01de-150">Set the media source</span></span>
<span data-ttu-id="b01de-151">ネットワーク上のファイルまたはアプリに埋め込まれたファイルを再生する場合は、ファイルのパスを使用して [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) プロパティを [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-151">To play files on the network or files embedded with the app, set the [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) property to a [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) with the path of the file.</span></span>

<span data-ttu-id="b01de-152">**ヒント:**   、インターネットからファイルを開くには、宣言する必要があります、**インターネット (クライアント)** アプリのマニフェスト (Package.appxmanifest) で機能します。</span><span class="sxs-lookup"><span data-stu-id="b01de-152">**Tip**  To open files from the internet, you need to declare the **Internet (Client)** capability in your app's manifest (Package.appxmanifest).</span></span> <span data-ttu-id="b01de-153">機能の宣言について詳しくは、「[アプリ機能の宣言](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-153">For more info about declaring capabilities, see [App capability declarations](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations).</span></span>

 

<span data-ttu-id="b01de-154">次のコードでは、XAML で定義した [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) の [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) プロパティを、[TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) に入力したファイルのパスに設定してみます。</span><span class="sxs-lookup"><span data-stu-id="b01de-154">This code attempts to set the [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) property of the [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) defined in XAML to the path of a file entered into a [TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox).</span></span>

```xaml
<TextBox x:Name="txtFilePath" Width="400"
         FontSize="20"
         KeyUp="TxtFilePath_KeyUp"
         Header="File path"
         PlaceholderText="Enter file path"/>
```

```csharp
private void TxtFilePath_KeyUp(object sender, KeyRoutedEventArgs e)
{
    if (e.Key == Windows.System.VirtualKey.Enter)
    {
        TextBox tbPath = sender as TextBox;

        if (tbPath != null)
        {
            LoadMediaFromString(tbPath.Text);
        }
    }
}

private void LoadMediaFromString(string path)
{
    try
    {
        Uri pathUri = new Uri(path);
        mediaPlayer.Source = MediaSource.CreateFromUri(pathUri);
    }
    catch (Exception ex)
    {
        if (ex is FormatException)
        {
            // handle exception.
            // For example: Log error or notify user problem with file
        }
    }
}
```

<span data-ttu-id="b01de-155">メディア ソースをアプリに埋め込まれたメディア ファイルに設定するには、**ms-appx:///** で始まるパスで [Uri](https://docs.microsoft.com/uwp/api/windows.foundation.uri.) を初期化し、その Uri で [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) を作成してから、[Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) をその Uri に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-155">To set the media source to a media file embedded in the app, initialize a [Uri](https://docs.microsoft.com/uwp/api/windows.foundation.uri.) with the path prefixed with **ms-appx:///**, create a [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) with the Uri and then set the [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) to the Uri.</span></span> <span data-ttu-id="b01de-156">たとえば、**Videos** サブフォルダーにある **video1.mp4** というファイルのパスは、**ms-appx:///Videos/video1.mp4** のようになります。</span><span class="sxs-lookup"><span data-stu-id="b01de-156">For example, for a file called **video1.mp4** that is in a **Videos** subfolder, the path would look like: **ms-appx:///Videos/video1.mp4**</span></span>

<span data-ttu-id="b01de-157">次のコードは、XAML で以前に定義した [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) の [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) プロパティを **ms-appx:///Videos/video1.mp4** に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-157">This code sets the [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) property of the [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) defined previously in XAML to **ms-appx:///Videos/video1.mp4**.</span></span>

```csharp
private void LoadEmbeddedAppFile()
{
    try
    {
        Uri pathUri = new Uri("ms-appx:///Videos/video1.mp4");
        mediaPlayer.Source = MediaSource.CreateFromUri(pathUri);
    }
    catch (Exception ex)
    {
        if (ex is FormatException)
        {
            // handle exception.
            // For example: Log error or notify user problem with file
        }
    }
}
```

### <a name="open-local-media-files"></a><span data-ttu-id="b01de-158">ローカル メディア ファイルを開く</span><span class="sxs-lookup"><span data-stu-id="b01de-158">Open local media files</span></span>
<span data-ttu-id="b01de-159">ローカル システムや OneDrive のファイルを開くには、[FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) を使ってファイルを取得し、[Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) を使ってメディア ソースを設定します。または、プログラムによってユーザーのメディア フォルダーにアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="b01de-159">To open files on the local system or from OneDrive, you can use the [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) to get the file and [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) to set the media source, or you can programmatically access the user media folders.</span></span>

<span data-ttu-id="b01de-160">アプリがユーザーの操作なしで、**Music** または **Video** フォルダーにアクセスする必要がある場合、たとえばユーザーのコレクションのすべての音楽ファイルやビデオ ファイルを列挙し、アプリで表示する場合は、**音楽ライブラリ**および**ビデオ ライブラリ**機能を宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-160">If your app needs access without user interaction to the **Music** or **Video** folders, for example, if you are enumerating all the music or video files in the user's collection and displaying them in your app, then you need to declare the **Music Library** and **Video Library** capabilities.</span></span> <span data-ttu-id="b01de-161">詳しくは、「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](https://docs.microsoft.com/windows/uwp/files/quickstart-managing-folders-in-the-music-pictures-and-videos-libraries)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-161">For more info, see [Files and folders in the Music, Pictures, and Videos libraries](https://docs.microsoft.com/windows/uwp/files/quickstart-managing-folders-in-the-music-pictures-and-videos-libraries).</span></span>

<span data-ttu-id="b01de-162">ユーザーはどのファイルにアクセスしているかを完全に制御できるので、[FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) には、ユーザーの **Music** または **Video** フォルダーなど、ローカル ファイル システム上のファイルにアクセスするための特別な機能は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="b01de-162">The [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) does not require special capabilities to access files on the local file system, such as the user's **Music** or **Video** folders, since the user has complete control over which file is being accessed.</span></span> <span data-ttu-id="b01de-163">セキュリティとプライバシーの観点から、アプリで使用する機能の数は最小限にすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b01de-163">From a security and privacy standpoint, it is best to minimize the number of capabilities your app uses.</span></span>

<span data-ttu-id="b01de-164">**FileOpenPicker を使用してローカルのメディアを開く**</span><span class="sxs-lookup"><span data-stu-id="b01de-164">**To open local media using FileOpenPicker**</span></span>

1.  <span data-ttu-id="b01de-165">ユーザーがメディア ファイルを選べるようにするには、[FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b01de-165">Call [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) to let the user pick a media file.</span></span>

    <span data-ttu-id="b01de-166">[FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) クラスを使って、メディア ファイルを選びます。</span><span class="sxs-lookup"><span data-stu-id="b01de-166">Use the [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) class to select a media file.</span></span> <span data-ttu-id="b01de-167">**FileOpenPicker** が表示するファイルの種類を指定する [FileTypeFilter](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.filetypefilter) を設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-167">Set the [FileTypeFilter](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.filetypefilter) to specify which file types the **FileOpenPicker** displays.</span></span> <span data-ttu-id="b01de-168">[PickSingleFileAsync](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync) を呼び出して、ファイル ピッカーを起動し、ファイルを取得します。</span><span class="sxs-lookup"><span data-stu-id="b01de-168">Call [PickSingleFileAsync](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync) to launch the file picker and get the file.</span></span>

2.  <span data-ttu-id="b01de-169">[MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) を使用して、選んだメディア ファイルを [MediaPlayerElement.Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) として設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-169">Use a [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) to set the chosen media file as the [MediaPlayerElement.Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source).</span></span>

    <span data-ttu-id="b01de-170">[FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) から返された [StorageFile](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) を使用するには、[MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) で [CreateFromStorageFile](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource.createfromstoragefile) メソッドを呼び出して、それを [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) の [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) として設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-170">To use the [StorageFile](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) returned from the [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker), you need to call the [CreateFromStorageFile](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource.createfromstoragefile) method on [MediaSource](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) and set it as the [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) of [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement).</span></span> <span data-ttu-id="b01de-171">その後、[MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) で [Play](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.play) を呼び出して、メディアを開始します。</span><span class="sxs-lookup"><span data-stu-id="b01de-171">Then call [Play](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.play) on the [MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) to start the media.</span></span>


<span data-ttu-id="b01de-172">この例は、[FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) を使ってファイルを選び、そのファイルを [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) の [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) に設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b01de-172">This example shows how to use the [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) to choose a file and set the file as the [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) of a [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement).</span></span>

```xaml
<MediaPlayerElement x:Name="mediaPlayer"/>
...
<Button Content="Choose file" Click="Button_Click"/>
```

```csharp
private async void Button_Click(object sender, RoutedEventArgs e)
{
    await SetLocalMedia();
}

async private System.Threading.Tasks.Task SetLocalMedia()
{
    var openPicker = new Windows.Storage.Pickers.FileOpenPicker();

    openPicker.FileTypeFilter.Add(".wmv");
    openPicker.FileTypeFilter.Add(".mp4");
    openPicker.FileTypeFilter.Add(".wma");
    openPicker.FileTypeFilter.Add(".mp3");

    var file = await openPicker.PickSingleFileAsync();

    // mediaPlayer is a MediaPlayerElement defined in XAML
    if (file != null)
    {
        mediaPlayer.Source = MediaSource.CreateFromStorageFile(file);

        mediaPlayer.MediaPlayer.Play();
    }
}
```

### <a name="set-the-poster-source"></a><span data-ttu-id="b01de-173">ポスター ソースを設定する</span><span class="sxs-lookup"><span data-stu-id="b01de-173">Set the poster source</span></span>
<span data-ttu-id="b01de-174">[PosterSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.PosterSource) プロパティを使って、メディアの読み込みが終わるまで  [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) に視覚的な表示を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="b01de-174">You can use the [PosterSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.PosterSource) property to provide your [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) with a visual representation before the media is loaded.</span></span> <span data-ttu-id="b01de-175">**PosterSource** は、スクリーン ショットや映画のポスターなど、メディアの代わりに表示される画像です。</span><span class="sxs-lookup"><span data-stu-id="b01de-175">A **PosterSource** is an image, such as a screen shot or movie poster, that is displayed in place of the media.</span></span> <span data-ttu-id="b01de-176">**PosterSource** は、次のような状況で表示されます。</span><span class="sxs-lookup"><span data-stu-id="b01de-176">The **PosterSource** is displayed in the following situations:</span></span>

-   <span data-ttu-id="b01de-177">有効なソースが設定されていないとき。</span><span class="sxs-lookup"><span data-stu-id="b01de-177">When a valid source is not set.</span></span> <span data-ttu-id="b01de-178">たとえば、[Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) が設定されていないとき、**Source** が **Null** に設定されているとき、またはソースが無効であるとき ([MediaFailed](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.mediafailed) イベントが発生したときと同様) です。</span><span class="sxs-lookup"><span data-stu-id="b01de-178">For example, [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) is not set, **Source** was set to **Null**, or the source is invalid (as is the case when a [MediaFailed](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.mediafailed) event occurs).</span></span>
-   <span data-ttu-id="b01de-179">メディアの読み込み中。</span><span class="sxs-lookup"><span data-stu-id="b01de-179">While media is loading.</span></span> <span data-ttu-id="b01de-180">たとえば、有効なソースが設定されていても、[MediaOpened](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.mediaopened) イベントがまだ発生していないときです。</span><span class="sxs-lookup"><span data-stu-id="b01de-180">For example, a valid source is set, but the [MediaOpened](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.mediaopened) event has not occurred yet.</span></span>
-   <span data-ttu-id="b01de-181">別のデバイスにメディアをストリーミングしているとき。</span><span class="sxs-lookup"><span data-stu-id="b01de-181">When media is streaming to another device.</span></span>
-   <span data-ttu-id="b01de-182">メディアがオーディオのみであるとき。</span><span class="sxs-lookup"><span data-stu-id="b01de-182">When the media is audio only.</span></span>

<span data-ttu-id="b01de-183">[Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) がアルバムのトラックに設定され、[PosterSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.PosterSource) がアルバムの表紙の画像を設定された [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="b01de-183">Here's a [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) with its [Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) set to an album track, and it's [PosterSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.PosterSource) set to an image of the album cover.</span></span>

```xaml
<MediaPlayerElement Source="ms-appx:///Media/Track1.mp4" PosterSource="Media/AlbumCover.png"/>
```

### <a name="keep-the-devices-screen-active"></a><span data-ttu-id="b01de-184">デバイスの画面をアクティブに維持する</span><span class="sxs-lookup"><span data-stu-id="b01de-184">Keep the device's screen active</span></span>
<span data-ttu-id="b01de-185">通常、ユーザーがいないときはバッテリーを節約するために画面が暗くなり、最終的には電源がオフになりますが、ビデオ アプリでは、ユーザーがビデオを見られるように画面をオンのままにしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-185">Typically, a device dims the display (and eventually turns it off) to save battery life when the user is away, but video apps need to keep the screen on so the user can see the video.</span></span> <span data-ttu-id="b01de-186">アプリでビデオを再生しているときなど、無操作状態が検出されてもディスプレイの電源が切れないようにするには、[DisplayRequest.RequestActive](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestactive) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b01de-186">To prevent the display from being deactivated when user action is no longer detected, such as when an app is playing video, you can call [DisplayRequest.RequestActive](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestactive).</span></span> <span data-ttu-id="b01de-187">[DisplayRequest](https://docs.microsoft.com/uwp/api/Windows.System.Display.DisplayRequest) クラスを使うと、ユーザーがビデオを見られるように画面をオンのままにするよう Windows に指示することができます。</span><span class="sxs-lookup"><span data-stu-id="b01de-187">The [DisplayRequest](https://docs.microsoft.com/uwp/api/Windows.System.Display.DisplayRequest) class lets you tell Windows to keep the display turned on so the user can see the video.</span></span>

<span data-ttu-id="b01de-188">消費電力とバッテリーの駆動時間を節約するため、不要になったら、[DisplayRequest.RequestRelease](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestrelease) を呼び出して表示要求を解放してください。</span><span class="sxs-lookup"><span data-stu-id="b01de-188">To conserve power and battery life, you should call [DisplayRequest.RequestRelease](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestrelease) to release the display request when it is no longer required.</span></span> <span data-ttu-id="b01de-189">Windows は、アプリが画面から消されると自動的にアプリのアクティブな表示要求を非アクティブ化し、アプリがフォアグラウンドに戻ると再びアクティブ化します。</span><span class="sxs-lookup"><span data-stu-id="b01de-189">Windows automatically deactivates your app's active display requests when your app moves off screen, and re-activates them when your app comes back to the foreground.</span></span>

<span data-ttu-id="b01de-190">表示要求を解放する必要があるのは、次のような場合です。</span><span class="sxs-lookup"><span data-stu-id="b01de-190">Here are some situations when you should release the display request:</span></span>

-   <span data-ttu-id="b01de-191">ユーザーの操作、バッファリング、限られた帯域幅のための調整などでビデオの再生が一時停止になる。</span><span class="sxs-lookup"><span data-stu-id="b01de-191">Video playback is paused, for example, by user action, buffering, or adjustment due to limited bandwidth.</span></span>
-   <span data-ttu-id="b01de-192">再生が停止する。</span><span class="sxs-lookup"><span data-stu-id="b01de-192">Playback stops.</span></span> <span data-ttu-id="b01de-193">たとえば、ビデオの再生が完了したり、プレゼンテーションが終了したりする。</span><span class="sxs-lookup"><span data-stu-id="b01de-193">For example, the video is done playing or the presentation is over.</span></span>
-   <span data-ttu-id="b01de-194">再生エラーが発生した。</span><span class="sxs-lookup"><span data-stu-id="b01de-194">A playback error has occurred.</span></span> <span data-ttu-id="b01de-195">たとえば、ネットワーク接続の問題や破損したファイル。</span><span class="sxs-lookup"><span data-stu-id="b01de-195">For example, network connectivity issues or a corrupted file.</span></span>

> <span data-ttu-id="b01de-196">**注**&nbsp;&nbsp;[MediaPlayerElement.IsFullWindow](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.IsFullWindow) が true に設定されていて、メディアが再生中である場合、ディスプレイは自動的に非アクティブ化されなくなります。</span><span class="sxs-lookup"><span data-stu-id="b01de-196">**Note**&nbsp;&nbsp; If [MediaPlayerElement.IsFullWindow](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.IsFullWindow) is set to true and media is playing, the display will automatically be prevented from deactivating.</span></span>

<span data-ttu-id="b01de-197">**アクティブな画面を保持するには**</span><span class="sxs-lookup"><span data-stu-id="b01de-197">**To keep the screen active**</span></span>

1.  <span data-ttu-id="b01de-198">[DisplayRequest](https://docs.microsoft.com/uwp/api/Windows.System.Display.DisplayRequest) グローバル変数を作成します。</span><span class="sxs-lookup"><span data-stu-id="b01de-198">Create a global [DisplayRequest](https://docs.microsoft.com/uwp/api/Windows.System.Display.DisplayRequest) variable.</span></span> <span data-ttu-id="b01de-199">null に初期化します。</span><span class="sxs-lookup"><span data-stu-id="b01de-199">Initialize it to null.</span></span>
```csharp
// Create this variable at a global scope. Set it to null.
private DisplayRequest appDisplayRequest = null;
```

2.  <span data-ttu-id="b01de-200">[RequestActive](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestactive) を呼び出して、アプリで表示をオンのままにする必要があることを Windows に通知します。</span><span class="sxs-lookup"><span data-stu-id="b01de-200">Call [RequestActive](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestactive) to notify Windows that the app requires the display to remain on.</span></span>

3.  <span data-ttu-id="b01de-201">ビデオの再生が再生エラーによって停止、一時停止、中断したときには必ず、[RequestRelease](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestrelease) を呼び出して表示要求を解放します。</span><span class="sxs-lookup"><span data-stu-id="b01de-201">Call [RequestRelease](https://docs.microsoft.com/uwp/api/windows.system.display.displayrequest.requestrelease) to release the display request whenever video playback is stopped, paused, or interrupted by a playback error.</span></span> <span data-ttu-id="b01de-202">アプリにアクティブな表示要求がなくなった場合、Windows は、デバイスが使われていないときには表示を暗くし、最終的には電源をオフにしてバッテリーを節約します。</span><span class="sxs-lookup"><span data-stu-id="b01de-202">When your app no longer has any active display requests, Windows saves battery life by dimming the display (and eventually turning it off) when the device is not being used.</span></span>

    <span data-ttu-id="b01de-203">各 [MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) には、[PlaybackRate](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.playbackrate)、[PlaybackState](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.playbackstate)、[Position](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.position) など、メディア再生のさまざまな側面を制御する [MediaPlaybackSession](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession) 型の [PlaybackSession](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.playbacksession) があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-203">Each [MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) has a [PlaybackSession](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.playbacksession) of type [MediaPlaybackSession](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession) that controls various aspects of media playback such as [PlaybackRate](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.playbackrate), [PlaybackState](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.playbackstate) and [Position](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.position).</span></span> <span data-ttu-id="b01de-204">ここでは、[MediaPlayer.PlaybackSession](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.playbacksession) で [PlaybackStateChanged](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.playbackstatechanged) イベントを使って、表示要求を解放する必要がある状況を検出します。</span><span class="sxs-lookup"><span data-stu-id="b01de-204">Here, you use the [PlaybackStateChanged](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.playbackstatechanged) event on  [MediaPlayer.PlaybackSession](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.playbacksession) to detect situations when you should release the display request.</span></span> <span data-ttu-id="b01de-205">次に、[NaturalVideoHeight](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.naturalvideoheight) プロパティを使って、オーディオ ファイルとビデオ ファイルのどちらが再生されているかを確認し、ビデオが再生されている場合にのみ画面をアクティブなままにします。</span><span class="sxs-lookup"><span data-stu-id="b01de-205">Then, use the [NaturalVideoHeight](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.naturalvideoheight) property to determine whether an audio or video file is playing, and keep the screen active only if video is playing.</span></span>

    ```xaml
    <MediaPlayerElement x:Name="mpe" Source="ms-appx:///Media/video1.mp4"/>
    ```

    ```csharp
    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        mpe.MediaPlayer.PlaybackSession.PlaybackStateChanged += MediaPlayerElement_CurrentStateChanged;
        base.OnNavigatedTo(e);
    }

    private void MediaPlayerElement_CurrentStateChanged(object sender, RoutedEventArgs e)
    {
        MediaPlaybackSession playbackSession = sender as MediaPlaybackSession;
        if (playbackSession != null && playbackSession.NaturalVideoHeight != 0)
        {
            if(playbackSession.PlaybackState == MediaPlaybackState.Playing)
            {
                if(appDisplayRequest == null)
                {
                    // This call creates an instance of the DisplayRequest object
                    appDisplayRequest = new DisplayRequest();
                    appDisplayRequest.RequestActive();
                }
            }
            else // PlaybackState is Buffering, None, Opening or Paused
            {
                if(appDisplayRequest != null)
                {
                      // Deactivate the displayr request and set the var to null
                      appDisplayRequest.RequestRelease();
                      appDisplayRequest = null;
                }
            }
        }

    }
    ```

### <a name="control-the-media-player-programmatically"></a><span data-ttu-id="b01de-206">プログラムでメディア プレーヤーを制御する</span><span class="sxs-lookup"><span data-stu-id="b01de-206">Control the media player programmatically</span></span>
<span data-ttu-id="b01de-207">[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) には、[MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) プロパティを介してオーディオやビデオの再生を制御するプロパティ、メソッド、イベントが多数用意されています。</span><span class="sxs-lookup"><span data-stu-id="b01de-207">[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) provides numerous properties, methods, and events for controlling audio and video playback through the [MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) property.</span></span> <span data-ttu-id="b01de-208">プロパティ、メソッド、イベントの完全な一覧については、[MediaPlayer](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer) のリファレンス ページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-208">For a full listing of properties, methods, and events, see the [MediaPlayer](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer) reference page.</span></span>

### <a name="advanced-media-playback-scenarios"></a><span data-ttu-id="b01de-209">高度なメディア再生のシナリオ</span><span class="sxs-lookup"><span data-stu-id="b01de-209">Advanced media playback scenarios</span></span>
<span data-ttu-id="b01de-210">プレイリストを再生するような複雑なメディア再生のシナリオでは、オーディオ言語間を切り替えたり、カスタム メタデータ トラックを作成したりするため、[MediaPlayerElement.Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) を [MediaPlaybackItem](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybackitem) または [MediaPlaybackList](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacklist) に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-210">For more complex media playback scenarios like playing a playlist, switching between audio languages or creating custom metadata tracks set the [MediaPlayerElement.Source](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) to a [MediaPlaybackItem](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybackitem) or a [MediaPlaybackList](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacklist).</span></span> <span data-ttu-id="b01de-211">参照してください、[メディアの再生](https://docs.microsoft.com/windows/uwp/audio-video-camera/media-playback-with-mediasource)さまざまな高度なメディア機能を有効にする方法の詳細についてのページ。</span><span class="sxs-lookup"><span data-stu-id="b01de-211">See the [Media playback](https://docs.microsoft.com/windows/uwp/audio-video-camera/media-playback-with-mediasource) page for more information on how to enable various advanced media functionality.</span></span>

### <a name="enable-full-window-video-rendering"></a><span data-ttu-id="b01de-212">フル ウィンドウのビデオ レンダリングを有効にする</span><span class="sxs-lookup"><span data-stu-id="b01de-212">Enable full window video rendering</span></span>

<span data-ttu-id="b01de-213">フル ウィンドウのレンダリングを有効または無効にするには、[IsFullWindow](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.isfullwindow) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-213">Set the [IsFullWindow](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.isfullwindow) property to enable and disable full window rendering.</span></span> <span data-ttu-id="b01de-214">プログラムを使ってアプリにフル ウィンドウのレンダリングを設定する場合、手動で行う代わりに **IsFullWindow** を常に使う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-214">When you programmatically set full window rendering in your app, you should always use **IsFullWindow** instead of doing it manually.</span></span> <span data-ttu-id="b01de-215">**IsFullWindow** により、システム レベルの最適化が実行され、パフォーマンスとバッテリーの寿命が向上します。</span><span class="sxs-lookup"><span data-stu-id="b01de-215">**IsFullWindow** insures that system level optimizations are performed that improve performance and battery life.</span></span> <span data-ttu-id="b01de-216">フル ウィンドウのレンダリングが正しく設定されていない場合、これらの最適化が有効になっていない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-216">If full window rendering is not set up correctly, these optimizations may not be enabled.</span></span>

<span data-ttu-id="b01de-217">フル ウィンドウのレンダリングを切り替える [AppBarButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarButton) を作成するコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="b01de-217">Here is some code that creates an [AppBarButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarButton) that toggles full window rendering.</span></span>

```xaml
<AppBarButton Icon="FullScreen"
              Label="Full Window"
              Click="FullWindow_Click"/>>
```

```csharp
private void FullWindow_Click(object sender, object e)
{
    mediaPlayer.IsFullWindow = !media.IsFullWindow;
}
```

### <a name="resize-and-stretch-video"></a><span data-ttu-id="b01de-218">ビデオのサイズを変更し、拡大する</span><span class="sxs-lookup"><span data-stu-id="b01de-218">Resize and stretch video</span></span>

<span data-ttu-id="b01de-219">[Stretch](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.stretch) プロパティを使って、コンテナー内でのビデオ コンテンツや [PosterSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.postersource) のサイズを変更します。</span><span class="sxs-lookup"><span data-stu-id="b01de-219">Use the [Stretch](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.stretch) property to change how the video content and/or the [PosterSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.postersource) fills the container it's in.</span></span> <span data-ttu-id="b01de-220">この要素は、[Stretch](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) の値に応じてビデオのサイズ変更と拡大を行います。</span><span class="sxs-lookup"><span data-stu-id="b01de-220">This resizes and stretches the video depending on the [Stretch](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) value.</span></span> <span data-ttu-id="b01de-221">**Stretch** 状態は、多くのテレビ セットの画像サイズの設定に似ています。</span><span class="sxs-lookup"><span data-stu-id="b01de-221">The **Stretch** states are similar to picture size settings on many TV sets.</span></span> <span data-ttu-id="b01de-222">ボタンにフックしてユーザーが好みの設定を選ぶことができるようにします。</span><span class="sxs-lookup"><span data-stu-id="b01de-222">You can hook this up to a button and allow the user to choose which setting they prefer.</span></span>

-   <span data-ttu-id="b01de-223">[None](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) は、元のサイズでコンテンツのネイティブの解像度を表示します。</span><span class="sxs-lookup"><span data-stu-id="b01de-223">[None](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) displays the native resolution of the content in its original size.</span></span>
-   <span data-ttu-id="b01de-224">[Uniform](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) は、縦横比、画像コンテンツを維持したままスペースを最大限に使用します。</span><span class="sxs-lookup"><span data-stu-id="b01de-224">[Uniform](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) fills up as much of the space as possible while preserving the aspect ratio and the image content.</span></span> <span data-ttu-id="b01de-225">これにより、ビデオの端に水平方向または垂直方向の黒いバーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="b01de-225">This can result in horizontal or vertical black bars at the edges of the video.</span></span> <span data-ttu-id="b01de-226">これはワイドスクリーン モードに似ています。</span><span class="sxs-lookup"><span data-stu-id="b01de-226">This is similar to wide-screen modes.</span></span>
-   <span data-ttu-id="b01de-227">[UniformToFill](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) は、縦横比を維持したままスペース全体を使用します。</span><span class="sxs-lookup"><span data-stu-id="b01de-227">[UniformToFill](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) fills up the entire space while preserving the aspect ratio.</span></span> <span data-ttu-id="b01de-228">これにより、画像の一部がトリミングされることがあります。</span><span class="sxs-lookup"><span data-stu-id="b01de-228">This can result in some of the image being cropped.</span></span> <span data-ttu-id="b01de-229">これは全画面モードに似ています。</span><span class="sxs-lookup"><span data-stu-id="b01de-229">This is similar to full-screen modes.</span></span>
-   <span data-ttu-id="b01de-230">[Fill](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) は、縦横比を維持せずに、スペース全体を使用します。</span><span class="sxs-lookup"><span data-stu-id="b01de-230">[Fill](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) fills up the entire space, but does not preserve the aspect ratio.</span></span> <span data-ttu-id="b01de-231">画像はトリミングされませんが、拡大されることがあります。</span><span class="sxs-lookup"><span data-stu-id="b01de-231">None of image is cropped, but stretching may occur.</span></span> <span data-ttu-id="b01de-232">これはストレッチ モードに似ています。</span><span class="sxs-lookup"><span data-stu-id="b01de-232">This is similar to stretch modes.</span></span>

![Stretch 列挙値](images/Image_Stretch.jpg)

<span data-ttu-id="b01de-234">ここでは、[AppBarButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarButton) を使って、[Stretch](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) オプションを順に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="b01de-234">Here, an [AppBarButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarButton) is used to cycle through the [Stretch](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Stretch) options.</span></span> <span data-ttu-id="b01de-235">**switch** ステートメントは、[Stretch](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaelement.stretch) プロパティの現在の状態をチェックし、**Stretch** 列挙で次の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-235">A **switch** statement checks the current state of the [Stretch](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaelement.stretch) property and sets it to the next value in the **Stretch** enumeration.</span></span> <span data-ttu-id="b01de-236">これにより、ユーザーはさまざまな拡大の状態を順番に表示することができます。</span><span class="sxs-lookup"><span data-stu-id="b01de-236">This lets the user cycle through the different stretch states.</span></span>

```xaml
<AppBarButton Icon="Switch"
              Label="Resize Video"
              Click="PictureSize_Click" />
```

```csharp
private void PictureSize_Click(object sender, RoutedEventArgs e)
{
    switch (mediaPlayer.Stretch)
    {
        case Stretch.Fill:
            mediaPlayer.Stretch = Stretch.None;
            break;
        case Stretch.None:
            mediaPlayer.Stretch = Stretch.Uniform;
            break;
        case Stretch.Uniform:
            mediaPlayer.Stretch = Stretch.UniformToFill;
            break;
        case Stretch.UniformToFill:
            mediaPlayer.Stretch = Stretch.Fill;
            break;
        default:
            break;
    }
}
```

### <a name="enable-low-latency-playback"></a><span data-ttu-id="b01de-237">待機時間が短い再生を可能にする</span><span class="sxs-lookup"><span data-stu-id="b01de-237">Enable low-latency playback</span></span>

<span data-ttu-id="b01de-238">[RealTimePlayback](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.realtimeplayback) プロパティを **true** に設定すると、[MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) の再生の最初の待機時間を短くすることができます。</span><span class="sxs-lookup"><span data-stu-id="b01de-238">Set the [RealTimePlayback](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.realtimeplayback) property to **true** on a [MediaPlayerElement.MediaPlayer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) to enable the media player element to reduce the initial latency for playback.</span></span> <span data-ttu-id="b01de-239">これは双方向通信アプリには重要で、ゲームのシナリオにも適用できる場合があります。</span><span class="sxs-lookup"><span data-stu-id="b01de-239">This is critical for two-way communications apps, and can be applicable to some gaming scenarios.</span></span> <span data-ttu-id="b01de-240">このモードでは、リソースがより多く消費され、電力効率が低下する点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="b01de-240">Be aware that this mode is more resource intensive and less power-efficient.</span></span>

<span data-ttu-id="b01de-241">この例では、[MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) を作って、[RealTimePlayback](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.realtimeplayback) を **true** に設定します。</span><span class="sxs-lookup"><span data-stu-id="b01de-241">This example creates a [MediaPlayerElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement) and sets [RealTimePlayback](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.realtimeplayback) to **true**.</span></span>


```csharp
MediaPlayerElement mp = new MediaPlayerElement();
mp.MediaPlayer.RealTimePlayback = true;
```

## <a name="recommendations"></a><span data-ttu-id="b01de-242">推奨事項</span><span class="sxs-lookup"><span data-stu-id="b01de-242">Recommendations</span></span>

<span data-ttu-id="b01de-243">メディア プレイヤーは淡色テーマと濃色テーマの両方をサポートしていますが、ほとんどのエンターテインメント シナリオでは、濃色テーマを使用することでエクスペリエンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="b01de-243">The media player supports both light and dark themes, but dark theme provides a better experience for most entertainment scenarios.</span></span> <span data-ttu-id="b01de-244">暗い背景を使うと、(特に高感度条件では) コントラストが強調され、表示エクスペリエンスに影響を及ぼすコントロール バーが制限されます。</span><span class="sxs-lookup"><span data-stu-id="b01de-244">The dark background provides better contrast, in particular for low-light conditions, and limits the control bar from interfering in the viewing experience.</span></span>

<span data-ttu-id="b01de-245">ビデオ コンテンツを再生する場合、インライン モードよりも全画面表示モードを促進することにより、専用の表示エクスペリエンスを使うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b01de-245">When playing video content, encourage a dedicated viewing experience by promoting full-screen mode over inline mode.</span></span> <span data-ttu-id="b01de-246">全画面表示エクスペリエンスが最適であり、インライン モードではオプションが制限されます。</span><span class="sxs-lookup"><span data-stu-id="b01de-246">The full-screen viewing experience is optimal, and options are restricted in the inline mode.</span></span>

<span data-ttu-id="b01de-247">画面領域がある場合や、10 フィート エクスペリエンス向けに設計する場合は、2 行のレイアウトを採用します。</span><span class="sxs-lookup"><span data-stu-id="b01de-247">If you have the screen real estate or are designing for the 10-foot experience, go with the double-row layout.</span></span> <span data-ttu-id="b01de-248">このレイアウトでは、コンパクトな 1 行のレイアウトよりもコントロールの領域が多く確保され、10 フィート環境ではゲームパッドによる移動が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="b01de-248">It provides more space for controls than the compact single-row layout and it is easier to navigate using gamepad for 10-foot.</span></span>

> <span data-ttu-id="b01de-249">**注**&nbsp;&nbsp; アプリケーションを 10 フィート エクスペリエンスに最適化する方法について詳しくは、「[Xbox およびテレビ向け設計](../devices/designing-for-tv.md)」の記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-249">**Note**&nbsp;&nbsp; Visit the [Designing for Xbox and TV](../devices/designing-for-tv.md) article for more information on optimizing your application for the 10-foot experience.</span></span>

<span data-ttu-id="b01de-250">既定のコントロールはメディア再生に最適化されていますが、アプリに最適なエクスペリエンスを実現するために、必要なカスタム オプションをメディア プレーヤーに追加できます。</span><span class="sxs-lookup"><span data-stu-id="b01de-250">The default controls have been optimized for media playback, however you have the ability to add custom options you need to the media player in order to provide the best experience for you app.</span></span> <span data-ttu-id="b01de-251">カスタム コントロールの追加について詳しくは、「[カスタム トランスポート コントロールを作成する](custom-transport-controls.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b01de-251">Visit [Create custom transport controls](custom-transport-controls.md) to learn more about adding custom controls.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="b01de-252">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="b01de-252">Get the sample code</span></span>

- <span data-ttu-id="b01de-253">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="b01de-253">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-articles"></a><span data-ttu-id="b01de-254">関連記事</span><span class="sxs-lookup"><span data-stu-id="b01de-254">Related articles</span></span>

- [<span data-ttu-id="b01de-255">UWP アプリのコマンド設計の基本</span><span class="sxs-lookup"><span data-stu-id="b01de-255">Command design basics for UWP apps</span></span>](https://docs.microsoft.com/windows/uwp/layout/commanding-basics)
- [<span data-ttu-id="b01de-256">UWP アプリのコンテンツのデザインの基礎</span><span class="sxs-lookup"><span data-stu-id="b01de-256">Content design basics for UWP apps</span></span>](https://docs.microsoft.com/windows/uwp/layout/content-basics)
