---
ms.assetid: 05E418B4-5A62-42BD-BF66-A0762216D033
description: このトピックでは、メディア キャプチャのプレビュー ストリームから単一のプレビュー フレームを取得する方法について説明します。
title: プレビュー フレームの取得
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 9963955649b98f226fbb81871b2ac391035ba41a
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66360887"
---
# <a name="get-a-preview-frame"></a><span data-ttu-id="c95e2-104">プレビュー フレームの取得</span><span class="sxs-lookup"><span data-stu-id="c95e2-104">Get a preview frame</span></span>


<span data-ttu-id="c95e2-105">このトピックでは、メディア キャプチャのプレビュー ストリームから単一のプレビュー フレームを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c95e2-105">This topic shows you how to get a single preview frame from the media capture preview stream.</span></span>

> [!NOTE] 
> <span data-ttu-id="c95e2-106">この記事の内容は、写真やビデオの基本的なキャプチャ機能を実装するための手順を紹介した「[MediaCapture を使った基本的な写真、ビデオ、およびオーディオのキャプチャ](basic-photo-video-and-audio-capture-with-MediaCapture.md)」で取り上げた概念やコードに基づいています。</span><span class="sxs-lookup"><span data-stu-id="c95e2-106">This article builds on concepts and code discussed in [Basic photo, video, and audio capture with MediaCapture](basic-photo-video-and-audio-capture-with-MediaCapture.md), which describes the steps for implementing basic photo and video capture.</span></span> <span data-ttu-id="c95e2-107">そちらの記事で基本的なメディア キャプチャのパターンを把握してから、高度なキャプチャ シナリオに進むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c95e2-107">We recommend that you familiarize yourself with the basic media capture pattern in that article before moving on to more advanced capture scenarios.</span></span> <span data-ttu-id="c95e2-108">この記事で紹介しているコードは、MediaCapture のインスタンスが既に作成され適切に初期化されていることと、アクティブなビデオ プレビュー ストリームを含んだ [**CaptureElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CaptureElement) が存在することを前提としています。</span><span class="sxs-lookup"><span data-stu-id="c95e2-108">The code in this article assumes that your app already has an instance of MediaCapture that has been properly initialized, and that you have a [**CaptureElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CaptureElement) with an active video preview stream.</span></span>

<span data-ttu-id="c95e2-109">プレビュー フレームをキャプチャするためには、基本的なメディア キャプチャに必要な名前空間に加え、次の名前空間が必要となります。</span><span class="sxs-lookup"><span data-stu-id="c95e2-109">In addition to the namespaces required for basic media capture, capturing a preview frame requires the following namespace.</span></span>

[!code-cs[PreviewFrameUsing](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetPreviewFrameUsing)]

<span data-ttu-id="c95e2-110">プレビュー フレームを要求するとき、フレームの受信に使う形式を指定するには、必要な形式を指定して [**VideoFrame**](https://docs.microsoft.com/uwp/api/Windows.Media.VideoFrame) オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="c95e2-110">When you request a preview frame, you can specify the format in which you would like to receive the frame by creating a [**VideoFrame**](https://docs.microsoft.com/uwp/api/Windows.Media.VideoFrame) object with the format you desire.</span></span> <span data-ttu-id="c95e2-111">この例では、[**VideoDeviceController.GetMediaStreamProperties**](https://docs.microsoft.com/uwp/api/windows.media.devices.videodevicecontroller.getmediastreamproperties) の呼び出しで [**MediaStreamType.VideoPreview**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaStreamType) を指定し、プレビュー ストリームのプロパティを要求することで、プレビュー ストリームと同じ解像度でビデオ フレームを作成します。</span><span class="sxs-lookup"><span data-stu-id="c95e2-111">This example creates a video frame that is the same resolution as the preview stream by calling [**VideoDeviceController.GetMediaStreamProperties**](https://docs.microsoft.com/uwp/api/windows.media.devices.videodevicecontroller.getmediastreamproperties) and specifying [**MediaStreamType.VideoPreview**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaStreamType) to request the properties for the preview stream.</span></span> <span data-ttu-id="c95e2-112">プレビュー ストリームの幅と高さを使って新しいビデオ フレームを作成しています。</span><span class="sxs-lookup"><span data-stu-id="c95e2-112">The width and height of the preview stream is used to create the new video frame.</span></span>

[!code-cs[CreateFormatFrame](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetCreateFormatFrame)]

<span data-ttu-id="c95e2-113">[  **MediaCapture**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) オブジェクトが初期化されていてアクティブなプレビュー ストリームが存在する場合、[**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) を呼び出してプレビュー ストリームを取得します。</span><span class="sxs-lookup"><span data-stu-id="c95e2-113">If your [**MediaCapture**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) object is initialized and you have an active preview stream, call [**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) to get a preview stream.</span></span> <span data-ttu-id="c95e2-114">引数には、最後のステップで作成したビデオ フレームを渡し、取得するフレームの形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="c95e2-114">Pass in the video frame created in the last step to specify the format of the returned frame.</span></span>

[!code-cs[GetPreviewFrameAsync](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetGetPreviewFrameAsync)]

<span data-ttu-id="c95e2-115">プレビュー フレームの [**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) 表現は、[**VideoFrame**](https://docs.microsoft.com/uwp/api/Windows.Media.VideoFrame) オブジェクトの [**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.softwarebitmap) プロパティにアクセスして取得します。</span><span class="sxs-lookup"><span data-stu-id="c95e2-115">Get a [**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) representation of the preview frame by accessing the [**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.softwarebitmap) property of the [**VideoFrame**](https://docs.microsoft.com/uwp/api/Windows.Media.VideoFrame) object.</span></span> <span data-ttu-id="c95e2-116">ソフトウェア ビットマップの保存、読み込み、変更については、「[イメージング](imaging.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c95e2-116">For information about saving, loading, and modifying software bitmaps, see [Imaging](imaging.md).</span></span>

[!code-cs[GetPreviewBitmap](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetGetPreviewBitmap)]

<span data-ttu-id="c95e2-117">Direct3D API で画像を扱う場合は、プレビュー フレームの [**IDirect3DSurface**](https://docs.microsoft.com/uwp/api/Windows.Graphics.DirectX.Direct3D11.IDirect3DSurface) 表現を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="c95e2-117">You can also get a [**IDirect3DSurface**](https://docs.microsoft.com/uwp/api/Windows.Graphics.DirectX.Direct3D11.IDirect3DSurface) representation of the preview frame if you want to use the image with Direct3D APIs.</span></span>

[!code-cs[GetPreviewSurface](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetGetPreviewSurface)]

> [!IMPORTANT]
> <span data-ttu-id="c95e2-118">**GetPreviewFrameAsync** の呼び出し方法と、アプリが実行されているデバイスによっては、返される **VideoFrame** の [**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.softwarebitmap) プロパティまたは [**Direct3DSurface**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.direct3dsurface) プロパティのどちらかが null になることがあります。</span><span class="sxs-lookup"><span data-stu-id="c95e2-118">Either the [**SoftwareBitmap**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.softwarebitmap) property or the [**Direct3DSurface**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.direct3dsurface) property of the returned **VideoFrame** may be null depending on how you call **GetPreviewFrameAsync** and also depending on the device on which your app is running.</span></span>

> - <span data-ttu-id="c95e2-119">**VideoFrame** 引数を受け入れる [**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) のオーバーロードを呼び出した場合、返される **VideoFrame** の **SoftwareBitmap** は null 以外になり、**Direct3DSurface** プロパティは null になります。</span><span class="sxs-lookup"><span data-stu-id="c95e2-119">If you call the overload of [**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) that accepts a **VideoFrame** argument, the returned **VideoFrame** will have a non-null **SoftwareBitmap** and the **Direct3DSurface** property will be null.</span></span>
> - <span data-ttu-id="c95e2-120">Direct3D サーフェスを使ってフレームを内部で表すデバイスで引数のない [**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) のオーバーロードを呼び出した場合、**Direct3DSurface** プロパティは null 以外になり、**SoftwareBitmap** プロパティは null になります。</span><span class="sxs-lookup"><span data-stu-id="c95e2-120">If you call the overload of [**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) that has no arguments on a device that uses a Direct3D surface to represent the frame internally, the **Direct3DSurface** property will be non-null and the **SoftwareBitmap** property will be null.</span></span>
> - <span data-ttu-id="c95e2-121">Direct3D サーフェスを使ってフレームを内部で表すデバイスで引数のない [**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) のオーバーロードを呼び出した場合、**SoftwareBitmap** プロパティは null 以外になり、**Direct3DSurface** プロパティは null になります。</span><span class="sxs-lookup"><span data-stu-id="c95e2-121">If you call the overload of [**GetPreviewFrameAsync**](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.getpreviewframeasync) that has no arguments on a device that does not use a Direct3D surface to represent the frame internally, the **SoftwareBitmap** property will be non-null and the **Direct3DSurface** property will be null.</span></span>

<span data-ttu-id="c95e2-122">アプリは、**SoftwareBitmap** プロパティまたは **Direct3DSurface** プロパティによって返されるオブジェクトで動作を試みる前に、必ず null 値をチェックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c95e2-122">Your app should always check for a null value before trying to operate on the objects returned by the **SoftwareBitmap** or **Direct3DSurface** properties.</span></span>

<span data-ttu-id="c95e2-123">プレビュー フレームが不要になったら必ず、その [**Close**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.close) メソッド (C# 内で Dispose に投影される) を呼び出して、フレームによって使われているリソースを解放してください。</span><span class="sxs-lookup"><span data-stu-id="c95e2-123">When you are done using the preview frame, be sure to call its [**Close**](https://docs.microsoft.com/uwp/api/windows.media.videoframe.close) method (projected to Dispose in C#) to free the resources used by the frame.</span></span> <span data-ttu-id="c95e2-124">または、**using** パターンを使ってもかまいません。その場合は、オブジェクトが自動的に破棄されます。</span><span class="sxs-lookup"><span data-stu-id="c95e2-124">Or, use the **using** pattern, which automatically disposes of the object.</span></span>

[!code-cs[CleanUpPreviewFrame](./code/BasicMediaCaptureWin10/cs/MainPage.xaml.cs#SnippetCleanUpPreviewFrame)]

## <a name="related-topics"></a><span data-ttu-id="c95e2-125">関連トピック</span><span class="sxs-lookup"><span data-stu-id="c95e2-125">Related topics</span></span>

* [<span data-ttu-id="c95e2-126">カメラ</span><span class="sxs-lookup"><span data-stu-id="c95e2-126">Camera</span></span>](camera.md)
* [<span data-ttu-id="c95e2-127">MediaCapture で基本的な写真、ビデオ、およびオーディオのキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="c95e2-127">Basic photo, video, and audio capture with MediaCapture</span></span>](basic-photo-video-and-audio-capture-with-MediaCapture.md)
 

 




