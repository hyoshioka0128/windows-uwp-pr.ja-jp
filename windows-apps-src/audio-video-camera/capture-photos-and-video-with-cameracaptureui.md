---
ms.assetid: CC0D6E9B-128D-488B-912F-318F5EE2B8D3
description: この記事では、CameraCaptureUI クラスを使用して、Windows に組み込まれているカメラ UI で写真またはビデオをキャプチャする方法を説明します。
title: Windows の組み込みカメラ UI を使った写真とビデオのキャプチャ
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 35eed8310b406a960334c90d6c359c0313b2660c
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66358895"
---
# <a name="capture-photos-and-video-with-windows-built-in-camera-ui"></a>Windows の組み込みカメラ UI を使った写真とビデオのキャプチャ



この記事では、CameraCaptureUI クラスを使用して、Windows に組み込まれているカメラ UI で写真またはビデオをキャプチャする方法を説明します。 この機能は使いやすく、わずか数行のコードで、ユーザーがキャプチャした写真やビデオをアプリに取り込むことができます。

独自のカメラ用 UI を用意する場合、またはキャプチャ操作に対してより堅牢で低レベルな制御が必要な場合は、[**MediaCapture**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) オブジェクトを使用して、独自のキャプチャ操作を実装する必要があります。 詳しくは、「[MediaCapture を使った基本的な写真、ビデオ、およびオーディオのキャプチャ](basic-photo-video-and-audio-capture-with-MediaCapture.md)」をご覧ください。

> [!NOTE]
> 指定しないで、 **web カメラ**または**マイク**マニフェスト ファイルをアプリでは、CameraCaptureUI のみで使用する場合、アプリで機能します。 指定すると、アプリはデバイスのカメラのプライバシー設定に表示されますが、ユーザーがアプリからのカメラへのアクセスを拒否しても、CameraCaptureUI はメディアをキャプチャできます。 これは、Windows の組み込みのカメラ アプリが、写真、音声、ビデオのキャプチャをボタンを押して開始する必要がある、信頼されているファースト パーティ アプリであるためです。 アプリには、Windows アプリケーションの認定キットの認定、唯一の写真キャプチャ メカニズムとして CameraCaptureUI を使用する場合に、web カメラまたはマイク機能を指定する場合は、ストアに送信されたときに失敗します。
> MediaCapture を使用して、音声、写真、またはビデオをプログラムによってキャプチャする場合は、アプリのマニフェスト ファイルで Web カメラまたはマイク機能を指定する必要があります。

## <a name="capture-a-photo-with-cameracaptureui"></a>CameraCaptureUI を使った写真のキャプチャ

カメラ キャプチャ UI を使うには、プロジェクトに [**Windows.Media.Capture**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture) 名前空間を含めます。 返された画像ファイルでファイル操作を行うには、[**Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage) を含めます。

[!code-cs[UsingCaptureUI](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetUsingCaptureUI)]

写真をキャプチャするには、新しい [**CameraCaptureUI**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUI) オブジェクトを作成します。 オブジェクトの [**PhotoSettings**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.photosettings) プロパティを使うと、写真の画像形式など、返される写真のプロパティを指定することができます。 既定では、ユーザーはカメラ キャプチャ UI を使うことにより、返される前に写真のトリミングを行うことができます。ただし、この機能は [**AllowCropping**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureuiphotocapturesettings.allowcropping) プロパティを使って無効にすることもできます。 この例では、[**CroppedSizeInPixels**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureuiphotocapturesettings.croppedsizeinpixels) を設定して、返される画像のサイズが 200 x 200 ピクセルになるよう要求しています。

> [!NOTE]
> モバイル デバイス ファミリのデバイスでは、**CameraCaptureUI** での画像のトリミングはサポートされていません。 アプリがこれらのデバイスで実行されている場合、[**AllowCropping**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureuiphotocapturesettings.allowcropping) プロパティの値は無視されます。

写真をキャプチャすることを指定するには、[**CaptureFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.) を呼び出して、[**CameraCaptureUIMode.Photo**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUIMode) を指定します。 キャプチャに成功すると、このメソッドは、画像が格納された [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) インスタンスを返します。 ユーザーがキャプチャを取り消した場合、返されるオブジェクトは null になります。

[!code-cs[CapturePhoto](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetCapturePhoto)]

キャプチャした写真が格納されている **StorageFile** は、動的に生成された名前が付けられて、アプリのローカル フォルダーに保存されます。 キャプチャした写真をわかりやすく整理するため、別のフォルダーにファイルを移動することもできます。

[!code-cs[CopyAndDeletePhoto](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetCopyAndDeletePhoto)]

アプリで写真を使用するために、[**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap)オブジェクトを作成できます。このオブジェクトは、ユニバーサル Windows アプリのさまざまな機能で使用できます。

まず、プロジェクトに [**Windows.Graphics.Imaging**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Imaging) 名前空間を含める必要があります。

[!code-cs[UsingSoftwareBitmap](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetUsingSoftwareBitmap)]

画像ファイルからストリームを取得するには、[**OpenAsync**](https://docs.microsoft.com/uwp/api/windows.storage.istoragefile.openasync) を呼び出します。 ストリームのビットマップ デコーダーを取得するには、[**BitmapDecoder.CreateAsync**](https://docs.microsoft.com/uwp/api/windows.graphics.imaging.bitmapdecoder.createasync) を呼び出します。 次に、[**GetSoftwareBitmap**](https://docs.microsoft.com/uwp/api/windows.graphics.imaging.bitmapdecoder.getsoftwarebitmapasync) を呼び出して、画像の **SoftwareBitmap** 表現を取得します。

[!code-cs[SoftwareBitmap](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetSoftwareBitmap)]

UI に画像を表示するには、XAML ページで [**Image**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Image) コントロールを宣言します。

[!code-xml[ImageControl](./code/CameraCaptureUIWin10/cs/MainPage.xaml#SnippetImageControl)]

XAML ページでソフトウェア ビットマップを使用するには、[**Windows.UI.Xaml.Media.Imaging**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging) 名前空間の using 指定を含めます。

[!code-cs[UsingSoftwareBitmapSource](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetUsingSoftwareBitmapSource)]

**Image** コントロールでは、画像のソースが BGRA8 形式プリマルチプライ済みアルファまたはアルファなしであることが求められるため、静的メソッド [**SoftwareBitmap.Convert**](https://docs.microsoft.com/uwp/api/windows.graphics.imaging.softwarebitmap.windows) を呼び出して、目的の形式で新しいソフトウェア ビットマップを作成します。 次に、新しい [**SoftwareBitmapSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging.SoftwareBitmapSource) オブジェクトを作成して [**SetBitmapAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.softwarebitmapsource.setbitmapasync) を呼び出し、ソフトウェア ビットマップをソースに割り当てます。 最後に、キャプチャした写真を UI に表示できるように、**Image** コントロールの [**Source**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.image.source) プロパティを設定します。

[!code-cs[SetImageSource](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetSetImageSource)]

## <a name="capture-a-video-with-cameracaptureui"></a>CameraCaptureUI を使ったビデオのキャプチャ

ビデオをキャプチャするには、新しい [**CameraCaptureUI**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUI) オブジェクトを作成します。 オブジェクトの [**VideoSettings**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.videosettings) プロパティを使うと、ビデオの形式など、返されるビデオのプロパティを指定することができます。

ビデオをキャプチャすることを指定するには、[**CaptureFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.) を呼び出して、[**Video**](https://docs.microsoft.com/uwp/api/windows.media.capture.cameracaptureui.videosettings) を指定します。 キャプチャに成功すると、このメソッドは、ビデオが格納された [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) インスタンスを返します。 ユーザーがキャプチャを取り消した場合、返されるオブジェクトは null になります。

[!code-cs[CaptureVideo](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetCaptureVideo)]

キャプチャしたビデオ ファイルをどのように使うかは、アプリのシナリオによって異なります。 この記事の残りの部分では、キャプチャした 1 つ以上のビデオからメディア コンポジションをすばやく作成し、UI に表示する方法を説明します。

まず、ビデオ コンポジションを表示する [**MediaPlayerElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaPlayerElement) コントロールを XAML ページに追加します。

[!code-xml[MediaElement](./code/CameraCaptureUIWin10/cs/MainPage.xaml#SnippetMediaElement)]


カメラ キャプチャ UI から返されたビデオ ファイルを使用し、 **[CreateFromStorageFile](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource.createfromstoragefile)** を呼び出して、新しい [**MediaSource**](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource) を作成します。 **MediaPlayerElement** に関連付けられている既定の **[MediaPlayer](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer)** の **[Play](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplayer.Play)** メソッドを呼び出してビデオを再生します。

[!code-cs[PlayVideo](./code/CameraCaptureUIWin10/cs/MainPage.xaml.cs#SnippetPlayVideo)]
 

## <a name="related-topics"></a>関連トピック

* [カメラ](camera.md)
* [MediaCapture で基本的な写真、ビデオ、およびオーディオのキャプチャします。](basic-photo-video-and-audio-capture-with-MediaCapture.md)
* [**CameraCaptureUI**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUI) 
 

 




