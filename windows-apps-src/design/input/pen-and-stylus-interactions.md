---
Description: ペン デバイスやスタイラス デバイスからのカスタム操作 (自然な筆記/描画エクスペリエンスのためのデジタル インクなど) をサポートするユニバーサル Windows プラットフォーム (UWP) アプリを作成します。
title: UWP アプリでのペン操作と Windows Ink
ms.assetid: 3DA4F2D2-5405-42A1-9ED9-3A87BCD84C43
label: Pen interactions and Windows Ink in UWP apps
template: detail.hbs
keywords: Windows Ink, Windows の手書き入力, DirectInk, InkPresenter, InkCanvas, 手書き認識, ユーザー操作, 入力
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 5d60c85efe8f0a959ac66ffbd3dc8a05f312d0f2
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365648"
---
# <a name="pen-interactions-and-windows-ink-in-uwp-apps"></a><span data-ttu-id="bb164-104">UWP アプリでのペン操作と Windows Ink</span><span class="sxs-lookup"><span data-stu-id="bb164-104">Pen interactions and Windows Ink in UWP apps</span></span>

<span data-ttu-id="bb164-105">![画面のペン](images/ink/hero-small.png)</span><span class="sxs-lookup"><span data-stu-id="bb164-105">![Surface Pen](images/ink/hero-small.png)</span></span>  
<span data-ttu-id="bb164-106">*Surface ペン* ([Microsoft ストア](https://aka.ms/purchasesurfacepen)で購入できます)。</span><span class="sxs-lookup"><span data-stu-id="bb164-106">*Surface Pen* (available for purchase at the [Microsoft Store](https://aka.ms/purchasesurfacepen)).</span></span>

## <a name="overview"></a><span data-ttu-id="bb164-107">概要</span><span class="sxs-lookup"><span data-stu-id="bb164-107">Overview</span></span>

<span data-ttu-id="bb164-108">ペン入力向けにユニバーサル Windows プラットフォーム (UWP) アプリを最適化して、標準の [**ポインター デバイス**](https://docs.microsoft.com/uwp/api/Windows.Devices.Input.PointerDevice) 機能と最良の Windows Ink エクスペリエンスをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="bb164-108">Optimize your Universal Windows Platform (UWP) app for pen input to provide both standard [**pointer device**](https://docs.microsoft.com/uwp/api/Windows.Devices.Input.PointerDevice) functionality and the best Windows Ink experience for your users.</span></span>

> [!NOTE]
> <span data-ttu-id="bb164-109">ここでは主に、Windows Ink プラットフォームについて説明します。</span><span class="sxs-lookup"><span data-stu-id="bb164-109">This topic focuses on the Windows Ink platform.</span></span> <span data-ttu-id="bb164-110">ポインター入力処理 (マウス、タッチ、タッチパッドに類似) の概要については、「[ポインター入力の処理](handle-pointer-input.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bb164-110">For general pointer input handling (similar to mouse, touch, and touchpad), see [Handle pointer input](handle-pointer-input.md).</span></span>

| <span data-ttu-id="bb164-111">ビデオ</span><span class="sxs-lookup"><span data-stu-id="bb164-111">Videos</span></span> |   |
| --- | --- |
| <iframe src="https://channel9.msdn.com/Blogs/One-Dev-Minute/Using-Ink-in-Your-UWP-App/player" width="300" height="200" allowFullScreen frameBorder="0"></iframe> | <iframe src="https://channel9.msdn.com/Events/Ignite/2016/BRK2060/player" width="300" height="200" allowFullScreen frameBorder="0"></iframe> |
| <span data-ttu-id="bb164-112">*UWP アプリでのインクの使用*</span><span class="sxs-lookup"><span data-stu-id="bb164-112">*Using ink in your UWP app*</span></span> | <span data-ttu-id="bb164-113">*Windows ペンと手描き入力を使用して、魅力的なエンタープライズ アプリを構築するには*</span><span class="sxs-lookup"><span data-stu-id="bb164-113">*Use Windows Pen and Ink to build more engaging enterprise apps*</span></span> |

<span data-ttu-id="bb164-114">Windows Ink プラットフォームでペン デバイスを使うと、自然な形でデジタルの手書きノート、描画、コメントを作れます。</span><span class="sxs-lookup"><span data-stu-id="bb164-114">The Windows Ink platform, together with a pen device, provides a natural way to create digital handwritten notes, drawings, and annotations.</span></span> <span data-ttu-id="bb164-115">このプラットフォームは、デジタイザー入力のインク データとしてのキャプチャ、インク データの生成、インク データの管理、出力デバイスのインク ストロークとしてのインク データのレンダリング、手書き認識によるインクからテキストへの変換をサポートします。</span><span class="sxs-lookup"><span data-stu-id="bb164-115">The platform supports capturing digitizer input as ink data, generating ink data, managing ink data, rendering ink data as ink strokes on the output device, and converting ink to text through handwriting recognition.</span></span>

<span data-ttu-id="bb164-116">アプリでは、ユーザーが筆記や描画を行うときの基本的なペンの位置と動きのキャプチャに加えて、ストロークの筆圧の変化を追跡および収集することもできます。</span><span class="sxs-lookup"><span data-stu-id="bb164-116">In addition to capturing the basic position and movement of the pen as the user writes or draws, your app can also track and collect the varying amounts of pressure used throughout a stroke.</span></span> <span data-ttu-id="bb164-117">この情報が、ペン先の形状、サイズ、回転や、インクの色、用途 (プレーン インク、消去、強調表示、選択) などの設定と組み合わされて、紙の上でペン、鉛筆、ブラシを使っているときに近いユーザー エクスペリエンスが実現されます。</span><span class="sxs-lookup"><span data-stu-id="bb164-117">This information, along with settings for pen tip shape, size, and rotation, ink color, and purpose (plain ink, erasing, highlighting, and selecting), enables you to provide user experiences that closely resemble writing or drawing on paper with a pen, pencil, or brush.</span></span>

> [!NOTE]
> <span data-ttu-id="bb164-118">タッチ デジタイザーやマウス デバイスなど、他のポインター ベース デバイスからの手描き入力をアプリでサポートすることもできます。</span><span class="sxs-lookup"><span data-stu-id="bb164-118">Your app can also support ink input from other pointer-based devices, including touch digitizers and mouse devices.</span></span> 

<span data-ttu-id="bb164-119">インク プラットフォームは非常に柔軟で、</span><span class="sxs-lookup"><span data-stu-id="bb164-119">The ink platform is very flexible.</span></span> <span data-ttu-id="bb164-120">必要に応じてさまざまなレベルの機能をサポートできるようになっています。</span><span class="sxs-lookup"><span data-stu-id="bb164-120">It is designed to support various levels of functionality, depending on your requirements.</span></span>

<span data-ttu-id="bb164-121">Windows Ink UX のガイドラインについては、「[手描き入力コントロール](../controls-and-patterns/inking-controls.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bb164-121">For Windows Ink UX guidelines, see [Inking controls](../controls-and-patterns/inking-controls.md).</span></span>

## <a name="components-of-the-windows-ink-platform"></a><span data-ttu-id="bb164-122">Windows Ink プラットフォームのコンポーネント</span><span class="sxs-lookup"><span data-stu-id="bb164-122">Components of the Windows Ink platform</span></span>

| <span data-ttu-id="bb164-123">Component</span><span class="sxs-lookup"><span data-stu-id="bb164-123">Component</span></span> | <span data-ttu-id="bb164-124">説明</span><span class="sxs-lookup"><span data-stu-id="bb164-124">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="bb164-125">**InkCanvas**</span><span class="sxs-lookup"><span data-stu-id="bb164-125">**InkCanvas**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) | <span data-ttu-id="bb164-126">XAML UI プラットフォーム コントロール、既定では、受信し、インク ストロークまたは消去ストロークをペンからすべての入力を表示します。</span><span class="sxs-lookup"><span data-stu-id="bb164-126">A XAML UI platform control that, by default, receives and displays all input from a pen as either an ink stroke or an erase stroke.</span></span><br/><span data-ttu-id="bb164-127">InkCanvas の使用方法について詳しくは、「[Windows インク ストロークのテキスト認識](convert-ink-to-text.md)」と「[Windows Ink ストローク データの保存と取得](save-and-load-ink.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bb164-127">For more information about how to use the InkCanvas, see [Recognize Windows Ink strokes as text](convert-ink-to-text.md) and [Store and retrieve Windows Ink stroke data](save-and-load-ink.md).</span></span> |
| [<span data-ttu-id="bb164-128">**InkPresenter**</span><span class="sxs-lookup"><span data-stu-id="bb164-128">**InkPresenter**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) | <span data-ttu-id="bb164-129">[  **InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールと共にインスタンス化される分離コード オブジェクトです ([**InkCanvas.InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) プロパティによって公開されます)。</span><span class="sxs-lookup"><span data-stu-id="bb164-129">A code-behind object, instantiated along with an [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control (exposed through the [**InkCanvas.InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) property).</span></span> <span data-ttu-id="bb164-130">**InkCanvas** によって公開される既定の手描き入力機能のすべてと、追加のカスタマイズや個人用設定のための包括的な API のセットを提供します。</span><span class="sxs-lookup"><span data-stu-id="bb164-130">This object provides all default inking functionality exposed by the **InkCanvas**, along with a comprehensive set of APIs for additional customization and personalization.</span></span><br/><span data-ttu-id="bb164-131">InkPresenter の使用方法について詳しくは、「[Windows Ink ストロークのテキスト認識](convert-ink-to-text.md)」と「[Windows Ink ストローク データの保存と取得](save-and-load-ink.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bb164-131">For more information about how to use the InkPresenter, see [Recognize Windows Ink strokes as text](convert-ink-to-text.md) and [Store and retrieve Windows Ink stroke data](save-and-load-ink.md).</span></span> |
| [<span data-ttu-id="bb164-132">**InkToolbar**</span><span class="sxs-lookup"><span data-stu-id="bb164-132">**InkToolbar**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) | <span data-ttu-id="bb164-133">関連付けられているインクに関連する機能をアクティブ化するボタンのカスタマイズおよび拡張可能なコレクションを含む XAML UI プラットフォーム コントロール[ **InkCanvas**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas)します。</span><span class="sxs-lookup"><span data-stu-id="bb164-133">A XAML UI platform control containing a customizable and extensible collection of buttons that activate ink-related features in an associated [**InkCanvas**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas).</span></span><br/><span data-ttu-id="bb164-134">InkToolbar の使用方法について詳しくは、「[InkToolbar をユニバーサル Windows プラットフォーム (UWP) 手描き入力アプリに追加する](ink-toolbar.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bb164-134">For more information about how to use the InkToolbar, see [Add an InkToolbar to a Universal Windows Platform (UWP) inking app](ink-toolbar.md).</span></span> |
| [<span data-ttu-id="bb164-135">**IInkD2DRenderer**</span><span class="sxs-lookup"><span data-stu-id="bb164-135">**IInkD2DRenderer**</span></span>](https://docs.microsoft.com/windows/desktop/api/inkrenderer/nn-inkrenderer-iinkd2drenderer) | <span data-ttu-id="bb164-136">既定の [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールの代わりに、ユニバーサル Windows アプリが指定した Direct2D デバイス コンテキストにインク ストロークをレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="bb164-136">Enables the rendering of ink strokes onto the designated Direct2D device context of a Universal Windows app, instead of the default [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control.</span></span> <span data-ttu-id="bb164-137">これにより、手描き入力エクスペリエンスの全面的なカスタマイズが実現されます。</span><span class="sxs-lookup"><span data-stu-id="bb164-137">This enables full customization of the inking experience.</span></span><br/><span data-ttu-id="bb164-138">詳しくは、「[複雑なインクのサンプル](https://go.microsoft.com/fwlink/p/?LinkID=620314)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bb164-138">For more information, see the [Complex ink sample](https://go.microsoft.com/fwlink/p/?LinkID=620314).</span></span> |

## <a name="basic-inking-with-inkcanvas"></a><span data-ttu-id="bb164-139">InkCanvas による基本的な手描き入力</span><span class="sxs-lookup"><span data-stu-id="bb164-139">Basic inking with InkCanvas</span></span>

<span data-ttu-id="bb164-140">基本的な手描き機能を追加するには、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) UWP プラットフォーム コントロールをアプリの適切なページに配置します。</span><span class="sxs-lookup"><span data-stu-id="bb164-140">To add basic inking functionality, just place an [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) UWP platform control on the appropriate page in your app.</span></span>

<span data-ttu-id="bb164-141">既定では、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) はペンからの手描き入力のみをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="bb164-141">By default, the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) supports ink input only from a pen.</span></span> <span data-ttu-id="bb164-142">入力は、色と太さの既定の設定 (太さ 2 ピクセルの黒のボールペン) を使ってインク ストロークとしてレンダリングされるか、ストロークの消しゴムとして扱われます (ペンの消しゴムからの入力か、消しゴム ボタンで変更されたペン先からの入力の場合)。</span><span class="sxs-lookup"><span data-stu-id="bb164-142">The input is either rendered as an ink stroke using default settings for color and thickness (a black ballpoint pen with a thickness of 2 pixels), or treated as a stroke eraser (when input is from an eraser tip or the pen tip modified with an erase button).</span></span>

> [!NOTE]
> <span data-ttu-id="bb164-143">ペンの消しゴムまたは消しゴム ボタンがない場合は、ペン先からの入力を消去ストロークとして処理するように InkCanvas を構成できます。</span><span class="sxs-lookup"><span data-stu-id="bb164-143">If an eraser tip or button is not present, the InkCanvas can be configured to process input from the pen tip as an erase stroke.</span></span>

<span data-ttu-id="bb164-144">次の例では、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) を背景画像にオーバーレイしています。</span><span class="sxs-lookup"><span data-stu-id="bb164-144">In this example, an [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) overlays a background image.</span></span>

> [!NOTE]
> <span data-ttu-id="bb164-145">InkCanvas は既定[**高さ**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.Height)と[**幅**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.Width)サイズを自動的に要素の子である場合を除き、0 のプロパティその子要素など[StackPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.stackpanel
)または[グリッド](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.grid)コントロール。</span><span class="sxs-lookup"><span data-stu-id="bb164-145">An InkCanvas has default [**Height**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.Height) and [**Width**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.Width) properties of zero, unless it is the child of an element that automatically sizes its child elements, such as [StackPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.stackpanel
) or [Grid](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.grid) controls.</span></span>

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header"
                   Text="Basic ink sample"
                   Style="{ThemeResource HeaderTextBlockStyle}"
                   Margin="10,0,0,0" />            
    </StackPanel>
    <Grid Grid.Row="1">
        <Image Source="Assets\StoreLogo.png" />
        <InkCanvas x:Name="inkCanvas" />
    </Grid>
</Grid>
```

<span data-ttu-id="bb164-146">次の一連の画像は、この [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールによってペン入力がどのようにレンダリングされるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="bb164-146">This series of images shows how pen input is rendered by this [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control.</span></span>

| ![空の InkCanvas と背景画像](images/ink_basic_1_small.png) | ![インク ストロークを含む InkCanvas](images/ink_basic_2_small.png) | ![1 つのストロークが消去された InkCanvas](images/ink_basic_3_small.png) |
| --- | --- | ---|
| <span data-ttu-id="bb164-150">空の [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) と背景画像。</span><span class="sxs-lookup"><span data-stu-id="bb164-150">The blank [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) with a background image.</span></span> | <span data-ttu-id="bb164-151">インク ストロークを含む [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)。</span><span class="sxs-lookup"><span data-stu-id="bb164-151">The [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) with ink strokes.</span></span> | <span data-ttu-id="bb164-152">ストロークの一部が削除された [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)  (削除が部分ではなく全体にどのように影響するかに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="bb164-152">The [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) with one stroke erased (note how erase operates on an entire stroke, not a portion).</span></span> |

<span data-ttu-id="bb164-153">[  **InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールでサポートされている手書き入力機能は、[**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) という分離コード オブジェクトによって提供されます。</span><span class="sxs-lookup"><span data-stu-id="bb164-153">The inking functionality supported by the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control is provided by a code-behind object called the [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter).</span></span>

<span data-ttu-id="bb164-154">基本的な手書き入力では [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) のことを気にする必要はありませんが、</span><span class="sxs-lookup"><span data-stu-id="bb164-154">For basic inking, you don't have to concern yourself with the [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter).</span></span> <span data-ttu-id="bb164-155">[  **InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) の手書き入力動作をカスタマイズしたり構成したりするには、対応する **InkPresenter** オブジェクトにアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb164-155">However, to customize and configure inking behavior on the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas), you must access its corresponding **InkPresenter** object.</span></span>

## <a name="basic-customization-with-inkpresenter"></a><span data-ttu-id="bb164-156">InkPresenter による基本的なカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="bb164-156">Basic customization with InkPresenter</span></span>

<span data-ttu-id="bb164-157">[  **InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) オブジェクトは、各 [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールと共にインスタンス化されます。</span><span class="sxs-lookup"><span data-stu-id="bb164-157">An [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) object is instantiated with each [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control.</span></span>

> [!NOTE]
> <span data-ttu-id="bb164-158">[  **InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) を直接インスタンス化することはできません。</span><span class="sxs-lookup"><span data-stu-id="bb164-158">The [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) cannot be instantiated directly.</span></span> <span data-ttu-id="bb164-159">代わりに、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) の [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) プロパティを通じてアクセスします。</span><span class="sxs-lookup"><span data-stu-id="bb164-159">Instead, it is accessed through the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) property of the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas).</span></span> 

<span data-ttu-id="bb164-160">[  **InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) には、対応する [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールの既定の手書き入力動作のすべてに加えて、ストロークの追加のカスタマイズのための包括的な API のセット、および手描き入力 (標準および変更) の細かい管理を提供します。</span><span class="sxs-lookup"><span data-stu-id="bb164-160">Along with providing all default inking behaviors of its corresponding [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control, the [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) provides a comprehensive set of APIs for additional stroke customization and finer-grained management of the pen input (standard and modified).</span></span> <span data-ttu-id="bb164-161">たとえば、ストロークのプロパティ、サポートされている入力デバイスの種類、入力をオブジェクトで処理するかアプリに渡して処理するかなどを指定できます。</span><span class="sxs-lookup"><span data-stu-id="bb164-161">This includes stroke properties, supported input device types, and whether input is processed by the object or passed to the app for processing.</span></span>

> [!NOTE]
> <span data-ttu-id="bb164-162">標準のインク入力 (ペン先または消しゴムの先端やボタン) は、セカンダリ ハードウェア アフォーダンス (ペン バレル ボタン、マウスの右ボタン、または類似のメカニズムなど) で変更されません。</span><span class="sxs-lookup"><span data-stu-id="bb164-162">Standard ink input (from either pen tip or eraser tip/button) is not modified with a secondary hardware affordance, such as a pen barrel button, right mouse button, or similar mechanism.</span></span> 

<span data-ttu-id="bb164-163">既定では、インクはペン入力のみをサポートします。</span><span class="sxs-lookup"><span data-stu-id="bb164-163">By default, ink is supported for pen input only.</span></span> <span data-ttu-id="bb164-164">次の例では、ペンとマウスの両方の入力データをインク ストロークとして解釈するように [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) を構成しています。</span><span class="sxs-lookup"><span data-stu-id="bb164-164">Here, we configure the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) to interpret input data from both pen and mouse as ink strokes.</span></span> <span data-ttu-id="bb164-165">[  **InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) へのストロークのレンダリングに使うインク ストロークの最初の属性も設定しています。</span><span class="sxs-lookup"><span data-stu-id="bb164-165">We also set some initial ink stroke attributes used for rendering strokes to the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas).</span></span>

<span data-ttu-id="bb164-166">マウスとタッチによる手描き入力を有効化するには、[**InkPresenter**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.inking.inkpresenter) の [**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.InputDeviceTypes) プロパティを、必要な [**CoreInputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.core.coreinputdevicetypes) 値の組み合わせに設定します。</span><span class="sxs-lookup"><span data-stu-id="bb164-166">To enable mouse and touch inking, set the [**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.InputDeviceTypes) property of the [**InkPresenter**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.inking.inkpresenter) to the combination of [**CoreInputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.core.coreinputdevicetypes) values that you want.</span></span>

```csharp
public MainPage()
{
    this.InitializeComponent();

    // Set supported inking device types.
    inkCanvas.InkPresenter.InputDeviceTypes =
        Windows.UI.Core.CoreInputDeviceTypes.Mouse |
        Windows.UI.Core.CoreInputDeviceTypes.Pen;

    // Set initial ink stroke attributes.
    InkDrawingAttributes drawingAttributes = new InkDrawingAttributes();
    drawingAttributes.Color = Windows.UI.Colors.Black;
    drawingAttributes.IgnorePressure = false;
    drawingAttributes.FitToCurve = true;
    inkCanvas.InkPresenter.UpdateDefaultDrawingAttributes(drawingAttributes);
}
```

<span data-ttu-id="bb164-167">インク ストロークの属性は、ユーザー設定やアプリの要件に合わせて動的に設定できます。</span><span class="sxs-lookup"><span data-stu-id="bb164-167">Ink stroke attributes can be set dynamically to accommodate user preferences or app requirements.</span></span>

<span data-ttu-id="bb164-168">次の例では、ユーザーがインクの色を一覧から選べるようにしています。</span><span class="sxs-lookup"><span data-stu-id="bb164-168">Here, we let a user choose from a list of ink colors.</span></span>

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header"
                   Text="Basic ink customization sample"
                   VerticalAlignment="Center"
                   Style="{ThemeResource HeaderTextBlockStyle}"
                   Margin="10,0,0,0" />
        <TextBlock Text="Color:"
                   Style="{StaticResource SubheaderTextBlockStyle}"
                   VerticalAlignment="Center"
                   Margin="50,0,10,0"/>
        <ComboBox x:Name="PenColor"
                  VerticalAlignment="Center"
                  SelectedIndex="0"
                  SelectionChanged="OnPenColorChanged">
            <ComboBoxItem Content="Black"/>
            <ComboBoxItem Content="Red"/>
        </ComboBox>
    </StackPanel>
    <Grid Grid.Row="1">
        <Image Source="Assets\StoreLogo.png" />
        <InkCanvas x:Name="inkCanvas" />
    </Grid>
</Grid>
```

<span data-ttu-id="bb164-169">ユーザーが色を選択したら、その変更を処理して、それに合わせてインク ストロークの属性を更新します。</span><span class="sxs-lookup"><span data-stu-id="bb164-169">We then handle changes to the selected color and update the ink stroke attributes accordingly.</span></span>

```csharp
// Update ink stroke color for new strokes.
private void OnPenColorChanged(object sender, SelectionChangedEventArgs e)
{
    if (inkCanvas != null)
    {
        InkDrawingAttributes drawingAttributes =
            inkCanvas.InkPresenter.CopyDefaultDrawingAttributes();

        string value = ((ComboBoxItem)PenColor.SelectedItem).Content.ToString();

        switch (value)
        {
            case "Black":
                drawingAttributes.Color = Windows.UI.Colors.Black;
                break;
            case "Red":
                drawingAttributes.Color = Windows.UI.Colors.Red;
                break;
            default:
                drawingAttributes.Color = Windows.UI.Colors.Black;
                break;
        };

        inkCanvas.InkPresenter.UpdateDefaultDrawingAttributes(drawingAttributes);
    }
}
```

<span data-ttu-id="bb164-170">次の画像は、[**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) によるペン入力の処理とカスタマイズがどのように行われるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="bb164-170">These images shows how pen input is processed and customized by the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter).</span></span>

| ![既定の黒のインク ストロークを含む InkCanvas](images/ink-basic-custom-1-small.png) | ![ユーザーが選択した赤のインク ストロークを含む InkCanvas](images/ink-basic-custom-2-small.png) |
| --- | --- |
| <span data-ttu-id="bb164-173">既定の黒のインク ストロークを含む [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)。</span><span class="sxs-lookup"><span data-stu-id="bb164-173">The [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) with default black ink strokes.</span></span> | <span data-ttu-id="bb164-174">ユーザーが選択した赤のインク ストロークを含む [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)。</span><span class="sxs-lookup"><span data-stu-id="bb164-174">The [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) with user selected red ink strokes.</span></span> | 

<span data-ttu-id="bb164-175">手書き入力と消去以外の機能 (ストロークの選択など) を提供するには、アプリで処理するために [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) では未処理のままパススルーする入力をアプリで識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb164-175">To provide functionality beyond inking and erasing, such as stroke selection, your app must identify specific input for the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) to pass through unprocessed for handling by your app.</span></span>

## <a name="pass-through-input-for-advanced-processing"></a><span data-ttu-id="bb164-176">高度な処理のための入力のパススルー</span><span class="sxs-lookup"><span data-stu-id="bb164-176">Pass-through input for advanced processing</span></span>

<span data-ttu-id="bb164-177">既定では、[**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) によって、すべての入力がインク ストロークまたは消去ストロークとして処理されます。こうした入力には、セカンダリ ハードウェア アフォーダンス (ペン バレル ボタン、マウスの右ボタンなど) によって変更された入力も含まれます。</span><span class="sxs-lookup"><span data-stu-id="bb164-177">By default, [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) processes all input as either an ink stroke or an erase stroke, including input modified by a secondary hardware affordance such as a pen barrel button, a right mouse button, or similar.</span></span> <span data-ttu-id="bb164-178">ただし、ユーザーは通常、これらのセカンダリ アフォーダンスを使うときに、追加機能や動作の変更を期待します。</span><span class="sxs-lookup"><span data-stu-id="bb164-178">However, users typically expect some additional functionality or modified behavior with these secondary affordances.</span></span>

<span data-ttu-id="bb164-179">場合によっては、アプリの UI でユーザーが選択した内容に基づいて、セカンダリ アフォーダンス (通常はペン先に関連付けられていない機能) を持たないペンのための追加機能、その他の入力デバイスの種類、または変更された動作を公開することも必要になります。</span><span class="sxs-lookup"><span data-stu-id="bb164-179">In some cases, you might also need to expose additional functionality for pens without secondary affordances (functionality not usually associated with the pen tip), other input device types, or some type of modified behavior based on a user selection in your app's UI.</span></span>

<span data-ttu-id="bb164-180">そのような場合のために、[**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) は、特定の入力を処理しないように構成することができます。</span><span class="sxs-lookup"><span data-stu-id="bb164-180">To support this, [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) can be configured to leave specific input unprocessed.</span></span> <span data-ttu-id="bb164-181">この未処理の入力は、アプリにパススルーされて処理されます。</span><span class="sxs-lookup"><span data-stu-id="bb164-181">This unprocessed input is then passed through to your app for processing.</span></span>

### <a name="example---use-unprocessed-input-to-implement-stroke-selection"></a><span data-ttu-id="bb164-182">例 - 未処理の入力を使って、ストロークの選択を実装する</span><span class="sxs-lookup"><span data-stu-id="bb164-182">Example - Use unprocessed input to implement stroke selection</span></span> 

<span data-ttu-id="bb164-183">Windows Ink プラットフォームには、変更された入力を必要とする操作のためのサポート (ストロークの選択など) が組み込まれていません。</span><span class="sxs-lookup"><span data-stu-id="bb164-183">The Windows Ink platform does not provide built-in support for actions that require modified input, such as stroke selection.</span></span> <span data-ttu-id="bb164-184">このような機能をサポートするには、アプリでカスタム ソリューションを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb164-184">To support features like this, you must provide a custom solution in your apps.</span></span> 

<span data-ttu-id="bb164-185">次のコード例は、ペン バレル ボタン (またはマウスの右ボタン) で入力が変更された場合にストロークを選択できるようにする手順を示しています (すべてのコードは MainPage.xaml ファイルと MainPage.xaml.cs ファイルに含まれています)。</span><span class="sxs-lookup"><span data-stu-id="bb164-185">The following code example (all code is in the MainPage.xaml and MainPage.xaml.cs files) steps through how to enable stroke selection when input is modified with a pen barrel button (or right mouse button).</span></span>

1.  <span data-ttu-id="bb164-186">まず、MainPage.xaml で UI を設定します。</span><span class="sxs-lookup"><span data-stu-id="bb164-186">First, we set up the UI in MainPage.xaml.</span></span>

    <span data-ttu-id="bb164-187">ここでは、選択ストロークを描画するためのキャンバスを ([**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) の下に) 追加しています。</span><span class="sxs-lookup"><span data-stu-id="bb164-187">Here, we add a canvas (below the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)) to draw the selection stroke.</span></span> <span data-ttu-id="bb164-188">別のレイヤーを使って選択ストロークを描画すると、**InkCanvas** とそのコンテンツに影響を与えずに済みます。</span><span class="sxs-lookup"><span data-stu-id="bb164-188">Using a separate layer to draw the selection stroke leaves the **InkCanvas** and its content untouched.</span></span>

    ![下に選択キャンバスがある空の InkCanvas](images/ink-unprocessed-1-small.png)

      ```xaml
        <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
          <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
          </Grid.RowDefinitions>
          <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
            <TextBlock x:Name="Header"
              Text="Advanced ink customization sample"
              VerticalAlignment="Center"
              Style="{ThemeResource HeaderTextBlockStyle}"
              Margin="10,0,0,0" />
          </StackPanel>
          <Grid Grid.Row="1">
            <!-- Canvas for displaying selection UI. -->
            <Canvas x:Name="selectionCanvas"/>
            <!-- Inking area -->
            <InkCanvas x:Name="inkCanvas"/>
          </Grid>
        </Grid>
      ```

2.  <span data-ttu-id="bb164-190">MainPage.xaml.cs で、選択 UI のいくつかの要素への参照を保持するグローバル変数を宣言します。</span><span class="sxs-lookup"><span data-stu-id="bb164-190">In MainPage.xaml.cs, we declare a couple of global variables for keeping references to aspects of the selection UI.</span></span> <span data-ttu-id="bb164-191">具体的には、なげなわ選択ストロークと、選択されたストロークを強調表示する境界の四角形への参照を保持します。</span><span class="sxs-lookup"><span data-stu-id="bb164-191">Specifically, the selection lasso stroke and the bounding rectangle that highlights the selected strokes.</span></span>

      ```csharp
        // Stroke selection tool.
        private Polyline lasso;
        // Stroke selection area.
        private Rect boundingRect;
      ```

3.  <span data-ttu-id="bb164-192">次に、ペンとマウスの両方の入力データをインク ストロークとして解釈するように [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) を構成し、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) へのストロークのレンダリングに使うインク ストロークの最初の属性をいくつか設定します。</span><span class="sxs-lookup"><span data-stu-id="bb164-192">Next, we configure the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) to interpret input data from both pen and mouse as ink strokes, and set some initial ink stroke attributes used for rendering strokes to the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas).</span></span>

    <span data-ttu-id="bb164-193">ここで最も重要なのは、[InkPresenter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) の [**InputProcessingConfiguration**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputprocessingconfiguration) プロパティを使って、変更された入力がアプリで処理されるように指定することです。</span><span class="sxs-lookup"><span data-stu-id="bb164-193">Most importantly, we use the [**InputProcessingConfiguration**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputprocessingconfiguration) property of the [InkPresenter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) to indicate that any modified input should be processed by the app.</span></span> <span data-ttu-id="bb164-194">**InputProcessingConfiguration.RightDragAction** に [**InkInputRightDragAction.LeaveUnprocessed**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkInputRightDragAction) という値を割り当てて、変更された入力を指定します。</span><span class="sxs-lookup"><span data-stu-id="bb164-194">Modified input is specified by assigning **InputProcessingConfiguration.RightDragAction** a value of [**InkInputRightDragAction.LeaveUnprocessed**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkInputRightDragAction).</span></span> <span data-ttu-id="bb164-195">この値が設定されると、[InkPresenter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) によって [InkUnprocessedInput](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput) クラス (ユーザーが処理できるポインター イベントのセット) にパススルーされます。</span><span class="sxs-lookup"><span data-stu-id="bb164-195">When this value is set, the [InkPresenter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) passes through to the [InkUnprocessedInput](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput) class, a set of pointer events for you to handle.</span></span>

    <span data-ttu-id="bb164-196">[  **InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) によってパススルーされる [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerpressed)、[**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointermoved)、[**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerreleased) の各未処理イベントのリスナーが割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="bb164-196">We assign listeners for the unprocessed [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerpressed), [**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointermoved), and [**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerreleased) events passed through by the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter).</span></span> <span data-ttu-id="bb164-197">選択機能はすべてこれらのイベントのハンドラーに実装します。</span><span class="sxs-lookup"><span data-stu-id="bb164-197">All selection functionality is implemented in the handlers for these events.</span></span>

    <span data-ttu-id="bb164-198">最後に、[**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) の [**StrokeStarted**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokeinput.strokestarted) イベントと [**StrokesErased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.strokeserased) イベントのリスナーを割り当てます。</span><span class="sxs-lookup"><span data-stu-id="bb164-198">Finally, we assign listeners for the [**StrokeStarted**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokeinput.strokestarted) and [**StrokesErased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.strokeserased) events of the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter).</span></span> <span data-ttu-id="bb164-199">これらのイベントのハンドラーを使って、新しいストロークが開始された場合や既にあるストロークが消去された場合に選択 UI をクリーンアップします。</span><span class="sxs-lookup"><span data-stu-id="bb164-199">We use the handlers for these events to clean up the selection UI if a new stroke is started or an existing stroke is erased.</span></span>

    ![既定の黒のインク ストロークを含む InkCanvas](images/ink-unprocessed-2-small.png)

      ```csharp
        public MainPage()
        {
          this.InitializeComponent();

          // Set supported inking device types.
          inkCanvas.InkPresenter.InputDeviceTypes =
            Windows.UI.Core.CoreInputDeviceTypes.Mouse |
            Windows.UI.Core.CoreInputDeviceTypes.Pen;

          // Set initial ink stroke attributes.
          InkDrawingAttributes drawingAttributes = new InkDrawingAttributes();
          drawingAttributes.Color = Windows.UI.Colors.Black;
          drawingAttributes.IgnorePressure = false;
          drawingAttributes.FitToCurve = true;
          inkCanvas.InkPresenter.UpdateDefaultDrawingAttributes(drawingAttributes);

          // By default, the InkPresenter processes input modified by
          // a secondary affordance (pen barrel button, right mouse
          // button, or similar) as ink.
          // To pass through modified input to the app for custom processing
          // on the app UI thread instead of the background ink thread, set
          // InputProcessingConfiguration.RightDragAction to LeaveUnprocessed.
          inkCanvas.InkPresenter.InputProcessingConfiguration.RightDragAction =
              InkInputRightDragAction.LeaveUnprocessed;

          // Listen for unprocessed pointer events from modified input.
          // The input is used to provide selection functionality.
          inkCanvas.InkPresenter.UnprocessedInput.PointerPressed +=
              UnprocessedInput_PointerPressed;
          inkCanvas.InkPresenter.UnprocessedInput.PointerMoved +=
              UnprocessedInput_PointerMoved;
          inkCanvas.InkPresenter.UnprocessedInput.PointerReleased +=
              UnprocessedInput_PointerReleased;

          // Listen for new ink or erase strokes to clean up selection UI.
          inkCanvas.InkPresenter.StrokeInput.StrokeStarted +=
              StrokeInput_StrokeStarted;
          inkCanvas.InkPresenter.StrokesErased +=
              InkPresenter_StrokesErased;
        }
      ```

4.  <span data-ttu-id="bb164-201">次に、[**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) によってパススルーされる [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerpressed)、[**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointermoved)、[**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerreleased) の未処理イベントのハンドラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="bb164-201">We then define handlers for the unprocessed [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerpressed), [**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointermoved), and [**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkunprocessedinput.pointerreleased) events passed through by the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter).</span></span>

    <span data-ttu-id="bb164-202">なげなわストロークと境界の四角形を含むすべての選択機能をこれらのハンドラーに実装します。</span><span class="sxs-lookup"><span data-stu-id="bb164-202">All selection functionality is implemented in these handlers, including the lasso stroke and the bounding rectangle.</span></span>

    ![なげなわ選択](images/ink-unprocessed-3-small.png)

      ```csharp
        // Handle unprocessed pointer events from modified input.
        // The input is used to provide selection functionality.
        // Selection UI is drawn on a canvas under the InkCanvas.
        private void UnprocessedInput_PointerPressed(
          InkUnprocessedInput sender, PointerEventArgs args)
        {
          // Initialize a selection lasso.
          lasso = new Polyline()
          {
              Stroke = new SolidColorBrush(Windows.UI.Colors.Blue),
              StrokeThickness = 1,
              StrokeDashArray = new DoubleCollection() { 5, 2 },
              };

              lasso.Points.Add(args.CurrentPoint.RawPosition);

              selectionCanvas.Children.Add(lasso);
          }

          private void UnprocessedInput_PointerMoved(
            InkUnprocessedInput sender, PointerEventArgs args)
          {
            // Add a point to the lasso Polyline object.
            lasso.Points.Add(args.CurrentPoint.RawPosition);
          }

          private void UnprocessedInput_PointerReleased(
            InkUnprocessedInput sender, PointerEventArgs args)
          {
            // Add the final point to the Polyline object and
            // select strokes within the lasso area.
            // Draw a bounding box on the selection canvas
            // around the selected ink strokes.
            lasso.Points.Add(args.CurrentPoint.RawPosition);

            boundingRect =
              inkCanvas.InkPresenter.StrokeContainer.SelectWithPolyLine(
                lasso.Points);

            DrawBoundingRect();
          }
      ```

5.  <span data-ttu-id="bb164-204">PointerReleased イベント ハンドラーの最後の処理として、選択レイヤーのすべてのコンテンツ (なげなわストローク) をクリアして、なげなわの領域で囲まれたインク ストロークの周りに境界の四角形を 1 つ描画します。</span><span class="sxs-lookup"><span data-stu-id="bb164-204">To conclude the PointerReleased event handler, we clear the selection layer of all content (the lasso stroke) and then draw a single bounding rectangle around the ink strokes encompassed by the lasso area.</span></span>

    ![選択範囲の境界の四角形](images/ink-unprocessed-4-small.png)

      ```csharp
        // Draw a bounding rectangle, on the selection canvas, encompassing
        // all ink strokes within the lasso area.
        private void DrawBoundingRect()
        {
          // Clear all existing content from the selection canvas.
          selectionCanvas.Children.Clear();

          // Draw a bounding rectangle only if there are ink strokes
          // within the lasso area.
          if (!((boundingRect.Width == 0) ||
            (boundingRect.Height == 0) ||
            boundingRect.IsEmpty))
            {
              var rectangle = new Rectangle()
              {
                Stroke = new SolidColorBrush(Windows.UI.Colors.Blue),
                  StrokeThickness = 1,
                  StrokeDashArray = new DoubleCollection() { 5, 2 },
                  Width = boundingRect.Width,
                  Height = boundingRect.Height
              };

              Canvas.SetLeft(rectangle, boundingRect.X);
              Canvas.SetTop(rectangle, boundingRect.Y);

              selectionCanvas.Children.Add(rectangle);
            }
          }
      ```

6.  <span data-ttu-id="bb164-206">最後に、InkPresenter の [**StrokeStarted**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokeinput.strokestarted) イベントと [**StrokesErased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.strokeserased) イベントのハンドラーを定義します。</span><span class="sxs-lookup"><span data-stu-id="bb164-206">Finally, we define handlers for the [**StrokeStarted**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokeinput.strokestarted) and [**StrokesErased**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.strokeserased) InkPresenter events.</span></span>

    <span data-ttu-id="bb164-207">これらは両方とも同じクリーンアップ関数を呼び出します。これにより、新しいストロークが検出されるたびに現在の選択がクリアされます。</span><span class="sxs-lookup"><span data-stu-id="bb164-207">These both just call the same cleanup function to clear the current selection whenever a new stroke is detected.</span></span>

      ```csharp
        // Handle new ink or erase strokes to clean up selection UI.
        private void StrokeInput_StrokeStarted(
          InkStrokeInput sender, Windows.UI.Core.PointerEventArgs args)
        {
          ClearSelection();
        }

        private void InkPresenter_StrokesErased(
          InkPresenter sender, InkStrokesErasedEventArgs args)
        {
          ClearSelection();
        }
      ```

7.  <span data-ttu-id="bb164-208">次の例は、新しいストロークが開始された場合や既にあるストロークが消去された場合に選択キャンバスからすべての選択 UI を削除する関数を示しています。</span><span class="sxs-lookup"><span data-stu-id="bb164-208">Here's the function to remove all selection UI from the selection canvas when a new stroke is started or an existing stroke is erased.</span></span>

      ```csharp
        // Clean up selection UI.
        private void ClearSelection()
        {
          var strokes = inkCanvas.InkPresenter.StrokeContainer.GetStrokes();
          foreach (var stroke in strokes)
          {
            stroke.Selected = false;
          }
          ClearDrawnBoundingRect();
         }

        private void ClearDrawnBoundingRect()
        {
          if (selectionCanvas.Children.Any())
          {
            selectionCanvas.Children.Clear();
            boundingRect = Rect.Empty;
          }
        }
      ```

## <a name="custom-ink-rendering"></a><span data-ttu-id="bb164-209">カスタム インク レンダリング</span><span class="sxs-lookup"><span data-stu-id="bb164-209">Custom ink rendering</span></span>

<span data-ttu-id="bb164-210">既定では、手書き入力は待機時間が短いバックグラウンド スレッドで処理され、描画と同時にレンダリングが実行中となります ("ウェット" レンダリングが実行されます)。</span><span class="sxs-lookup"><span data-stu-id="bb164-210">By default, ink input is processed on a low-latency background thread and rendered in-progress, or "wet", as it is drawn.</span></span> <span data-ttu-id="bb164-211">ストロークが完了すると (ペンまたは指が画面を離れるか、マウスのボタンが離されると)、UI スレッドでストロークが処理されて、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) レイヤーへの "ドライ" レンダリングが行われます (アプリケーション コンテンツの上にレンダリングされてウェット インクが置き換えられます)。</span><span class="sxs-lookup"><span data-stu-id="bb164-211">When the stroke is completed (pen or finger lifted, or mouse button released), the stroke is processed on the UI thread and rendered "dry" to the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) layer (above the application content and replacing the wet ink).</span></span>

<span data-ttu-id="bb164-212">ウェット インク ストロークを "カスタム ドライ レンダリング" することによって、この既定の動作を上書きし、手描き入力エクスペリエンスを完全に制御することができます。</span><span class="sxs-lookup"><span data-stu-id="bb164-212">You can override this default behavior and completely control the inking experience by "custom drying" the wet ink strokes.</span></span> <span data-ttu-id="bb164-213">ほとんどのアプリケーションでは、通常、既定の動作で十分ですが、場合によっては、カスタム ドライ レンダリングが必要になります。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="bb164-213">While the default behavior is typically sufficient for most applications, there are a few cases where custom drying might be required, these include:</span></span>
- <span data-ttu-id="bb164-214">大きく複雑なインク ストロークのコレクションをより効率的に管理する場合</span><span class="sxs-lookup"><span data-stu-id="bb164-214">More efficient management of large, or complex, collections of ink strokes</span></span>
- <span data-ttu-id="bb164-215">大きなインク キャンバスでより効率的にパンやズームのサポートを行う場合</span><span class="sxs-lookup"><span data-stu-id="bb164-215">More efficient panning and zooming support on large ink canvases</span></span>
- <span data-ttu-id="bb164-216">Z オーダーを維持しながら、インクや他のオブジェクト (図形やテキストなど) をインターリーブする場合</span><span class="sxs-lookup"><span data-stu-id="bb164-216">Interleaving ink and other objects, such as shapes or text, while maintaining z-order</span></span> 
- <span data-ttu-id="bb164-217">ドライ レンダリングを行い、インクを DirectX 図形に同期的に変換する場合 (たとえば、ラスタライズされ、アプリケーション コンテンツに (個別の **InkCanvas** レイヤーとしてではなく) 統合される直線や図形など)。</span><span class="sxs-lookup"><span data-stu-id="bb164-217">Drying and converting ink synchronously into a DirectX shape (for example, a straight line or shape rasterized and integrated into application content instead of as a separate **InkCanvas** layer).</span></span>

<span data-ttu-id="bb164-218">カスタム ドライ レンダリングでは、手書き入力を管理して、既定の [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールの代わりにユニバーサル Windows アプリの Direct2D デバイス コンテキストにレンダリングするための [**IInkD2DRenderer**](https://docs.microsoft.com/windows/desktop/api/inkrenderer/nn-inkrenderer-iinkd2drenderer) オブジェクトが必要です。</span><span class="sxs-lookup"><span data-stu-id="bb164-218">Custom drying requires an [**IInkD2DRenderer**](https://docs.microsoft.com/windows/desktop/api/inkrenderer/nn-inkrenderer-iinkd2drenderer) object to manage the ink input and render it to the Direct2D device context of your Universal Windows app, instead of the default [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control.</span></span>

<span data-ttu-id="bb164-219">[  **ActivateCustomDrying**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.activatecustomdrying) を ([**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) が読み込まれる前に) 呼び出すと、[**SurfaceImageSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging.SurfaceImageSource) または [**VirtualSurfaceImageSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.virtualsurfaceimagesource) へのインク ストロークのドライ レンダリングの方法をカスタマイズするための [**InkSynchronizer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkSynchronizer) オブジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="bb164-219">By calling [**ActivateCustomDrying**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.activatecustomdrying) (before the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) is loaded), an app creates an [**InkSynchronizer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkSynchronizer) object to customize how an ink stroke is rendered dry to a [**SurfaceImageSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging.SurfaceImageSource) or [**VirtualSurfaceImageSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.virtualsurfaceimagesource).</span></span> 

<span data-ttu-id="bb164-220">[  **SurfaceImageSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging.SurfaceImageSource) と [**VirtualSurfaceImageSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.virtualsurfaceimagesource) はどちらも、アプリがアプリケーションのコンテンツに描画し、組み込むための DirectX 共有サーフェスを提供します。ただし VSIS は、効率的なパンやズームのために、画面よりも大きい仮想サーフェスを提供します。</span><span class="sxs-lookup"><span data-stu-id="bb164-220">Both [**SurfaceImageSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Imaging.SurfaceImageSource) and [**VirtualSurfaceImageSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.virtualsurfaceimagesource) provide a DirectX shared surface for your app to draw into and compose into your application's content, although VSIS provides a virtual surface that’s larger than the screen for performant panning and zooming.</span></span> <span data-ttu-id="bb164-221">これらのサーフェスの表示更新は XAML の UI スレッドと同期されるため、インクをいずれかにレンダリングしたとき、同時にウェット インクが InkCanvas から取り除かれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="bb164-221">Because visual updates to these surfaces are synchronized with the XAML UI thread, when ink is rendered to either, the wet ink can be removed from the InkCanvas  simultaneously.</span></span> 

<span data-ttu-id="bb164-222">ドライ インクを [SwapChainPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.swapchainpanel) 用にカスタマイズすることもできますが、UI スレッドとの同期は保証されません。インクを SwapChainPanel にレンダリングしたタイミングと、インクが InkCanvas から取り除かれるタイミングの間にずれが生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bb164-222">You can also custom dry ink to a [SwapChainPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.swapchainpanel), but synchronization with the UI thread is not guaranteed and there might be a delay between when the ink is rendered to your SwapChainPanel and when ink is removed from the InkCanvas.</span></span>

<span data-ttu-id="bb164-223">この機能の完全な例については、「[複雑なインクのサンプル](https://go.microsoft.com/fwlink/p/?LinkID=620314)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="bb164-223">For a full example of this functionality, see the [Complex ink sample](https://go.microsoft.com/fwlink/p/?LinkID=620314).</span></span>

> [!NOTE]
> <span data-ttu-id="bb164-224">カスタム ドライ レンダリングと [**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar)</span><span class="sxs-lookup"><span data-stu-id="bb164-224">Custom drying and the [**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar)</span></span>  
> <span data-ttu-id="bb164-225">カスタム ドライの実装によって、アプリが [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) の既定のインク レンダリング動作を上書きすると、レンダリングされたインク ストロークが InkToolbar で利用できなくなり、InkToolbar の組み込みの消去コマンドが正常に機能しなくなります。</span><span class="sxs-lookup"><span data-stu-id="bb164-225">If your app overrides the default ink rendering behavior of the [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) with a custom drying implementation, the rendered ink strokes are no longer available to the InkToolbar and the built-in erase commands of the InkToolbar do not work as expected.</span></span> <span data-ttu-id="bb164-226">消去機能を提供するには、すべてのポインター イベントを処理し、ストロークごとにヒット テストを実行すると共に、組み込みの [すべてのインクのデータを消去] コマンドをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bb164-226">To provide erase functionality, you must handle all pointer events, perform hit-testing on each stroke, and override the built-in "Erase all ink" command.</span></span>

## <a name="other-articles-in-this-section"></a><span data-ttu-id="bb164-227">このセクションの他の記事</span><span class="sxs-lookup"><span data-stu-id="bb164-227">Other articles in this section</span></span>

| <span data-ttu-id="bb164-228">トピック</span><span class="sxs-lookup"><span data-stu-id="bb164-228">Topic</span></span> | <span data-ttu-id="bb164-229">説明</span><span class="sxs-lookup"><span data-stu-id="bb164-229">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="bb164-230">インク ストロークを認識します。</span><span class="sxs-lookup"><span data-stu-id="bb164-230">Recognize ink strokes</span></span>](convert-ink-to-text.md) | <span data-ttu-id="bb164-231">インク ストロークを手書き認識によりテキストに変換したり、カスタム認識により図形に変換したりします。</span><span class="sxs-lookup"><span data-stu-id="bb164-231">Convert ink strokes to text using handwriting recognition, or to shapes using custom recognition.</span></span> |
| [<span data-ttu-id="bb164-232">インク ストロークを格納および取得</span><span class="sxs-lookup"><span data-stu-id="bb164-232">Store and retrieve ink strokes</span></span>](save-and-load-ink.md) | <span data-ttu-id="bb164-233">埋め込みの Ink Serialized Format (ISF) メタデータを使って、インク ストローク データをグラフィックス交換形式 (GIF) ファイルに保存します。</span><span class="sxs-lookup"><span data-stu-id="bb164-233">Store ink stroke data in a Graphics Interchange Format (GIF) file using embedded Ink Serialized Format (ISF) metadata.</span></span> |
| [<span data-ttu-id="bb164-234">UWP アプリを手描き入力機能に、InkToolbar を追加します。</span><span class="sxs-lookup"><span data-stu-id="bb164-234">Add an InkToolbar to a UWP inking app</span></span>](ink-toolbar.md) | <span data-ttu-id="bb164-235">既定の InkToolbar をユニバーサル Windows プラットフォーム (UWP) 手描き入力アプリに追加し、カスタム ペン ボタンを InkToolbar に追加して、カスタム ペン ボタンをカスタム ペン定義にバインドします。</span><span class="sxs-lookup"><span data-stu-id="bb164-235">Add a default InkToolbar to a Universal Windows Platform (UWP) inking app, add a custom pen button to the InkToolbar, and bind the custom pen button to a custom pen definition.</span></span> |

## <a name="related-articles"></a><span data-ttu-id="bb164-236">関連記事</span><span class="sxs-lookup"><span data-stu-id="bb164-236">Related articles</span></span>

* [<span data-ttu-id="bb164-237">概要します。UWP アプリでのインクをサポートします。</span><span class="sxs-lookup"><span data-stu-id="bb164-237">Get started: Support ink in your UWP app</span></span>](../../get-started/ink-walkthrough.md)
* [<span data-ttu-id="bb164-238">ポインター入力の処理</span><span class="sxs-lookup"><span data-stu-id="bb164-238">Handle pointer input</span></span>](handle-pointer-input.md)
* [<span data-ttu-id="bb164-239">入力デバイスの識別</span><span class="sxs-lookup"><span data-stu-id="bb164-239">Identify input devices</span></span>](identify-input-devices.md)

<span data-ttu-id="bb164-240">**Api**</span><span class="sxs-lookup"><span data-stu-id="bb164-240">**APIs**</span></span>

* [<span data-ttu-id="bb164-241">**Windows.Devices.Input**</span><span class="sxs-lookup"><span data-stu-id="bb164-241">**Windows.Devices.Input**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Devices.Input)
* [<span data-ttu-id="bb164-242">**Windows.UI.Input.Inking**</span><span class="sxs-lookup"><span data-stu-id="bb164-242">**Windows.UI.Input.Inking**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking)
* [<span data-ttu-id="bb164-243">**Windows.UI.Input.Inking.Core**</span><span class="sxs-lookup"><span data-stu-id="bb164-243">**Windows.UI.Input.Inking.Core**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.Core)

<span data-ttu-id="bb164-244">**サンプル**</span><span class="sxs-lookup"><span data-stu-id="bb164-244">**Samples**</span></span>
* [<span data-ttu-id="bb164-245">チュートリアルを開始します。UWP アプリでのインクをサポートします。</span><span class="sxs-lookup"><span data-stu-id="bb164-245">Get Started Tutorial: Support ink in your UWP app</span></span>](https://aka.ms/appsample-ink)
* [<span data-ttu-id="bb164-246">単純なインクのサンプル (C#/C++)</span><span class="sxs-lookup"><span data-stu-id="bb164-246">Simple ink sample (C#/C++)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620312)
* [<span data-ttu-id="bb164-247">複雑なインクのサンプル (C++)</span><span class="sxs-lookup"><span data-stu-id="bb164-247">Complex ink sample (C++)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620314)
* [<span data-ttu-id="bb164-248">インクのサンプル (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="bb164-248">Ink sample (JavaScript)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620308)
* [<span data-ttu-id="bb164-249">書籍のサンプルを色分け表示</span><span class="sxs-lookup"><span data-stu-id="bb164-249">Coloring book sample</span></span>](https://aka.ms/cpubsample-coloringbook)
* [<span data-ttu-id="bb164-250">ファミリのノートのサンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-250">Family notes sample</span></span>](https://aka.ms/cpubsample-familynotessample)
* [<span data-ttu-id="bb164-251">基本的な入力サンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-251">Basic input sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620302)
* [<span data-ttu-id="bb164-252">低待機時間の入力サンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-252">Low latency input sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620304)
* [<span data-ttu-id="bb164-253">ユーザー操作モードのサンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-253">User interaction mode sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=619894)
* [<span data-ttu-id="bb164-254">フォーカスの視覚効果のサンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-254">Focus visuals sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=619895)

<span data-ttu-id="bb164-255">**サンプルのアーカイブ**</span><span class="sxs-lookup"><span data-stu-id="bb164-255">**Archive Samples**</span></span>
* [<span data-ttu-id="bb164-256">入力:デバイス機能のサンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-256">Input: Device capabilities sample</span></span>](https://go.microsoft.com/fwlink/p/?linkid=231530)
* [<span data-ttu-id="bb164-257">入力:XAML ユーザー入力イベントのサンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-257">Input: XAML user input events sample</span></span>](https://go.microsoft.com/fwlink/p/?linkid=226855)
* [<span data-ttu-id="bb164-258">XAML のスクロール、パン、ズームのサンプル</span><span class="sxs-lookup"><span data-stu-id="bb164-258">XAML scrolling, panning, and zooming sample</span></span>](https://go.microsoft.com/fwlink/p/?linkid=251717)
* [<span data-ttu-id="bb164-259">入力:ジェスチャと GestureRecognizer の操作</span><span class="sxs-lookup"><span data-stu-id="bb164-259">Input: Gestures and manipulations with GestureRecognizer</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=231605)
