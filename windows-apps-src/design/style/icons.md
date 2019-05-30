---
Description: 優れたアイコンは、文字の体裁やその他のデザイン言語と調和するものです。 アイコンは比喩と混用しないようにします。優れたアイコンは、できるだけすばやくシンプルに、必要なことのみを伝えます。
title: アイコン
ms.assetid: b90ac02d-5467-4304-99bd-292d6272a014
label: Icons
template: detail.hbs
ms.date: 05/02/2018
ms.topic: article
keywords: windows 10, uwp
design-contact: Judysa
doc-status: Published
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 5e464251200812e79474d05d9d0a680b49167871
ms.sourcegitcommit: 7da28cf4f4e8390bc9a21a9488b03af39271cbbe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64564536"
---
# <a name="icons-for-uwp-apps"></a><span data-ttu-id="2aa59-105">UWP アプリのアイコン</span><span class="sxs-lookup"><span data-stu-id="2aa59-105">Icons for UWP apps</span></span>

![アイコンのヘッダー画像](images/icons/header-icons.png)

<span data-ttu-id="2aa59-107">アイコンは、アクション、概念、または製品の簡潔にした視覚表現を提供します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-107">Icons provide a visual shorthand for an action, concept, or product.</span></span> <span data-ttu-id="2aa59-108">シンボリック イメージに意味を凝縮することによって、アイコンは言語の壁を乗り越えることができ、非常に価値のあるリソースである画面領域を節約するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-108">By compressing meaning into a symbolic image, icons can cross language barriers and help conserve an extremely valuable resource: screen space.</span></span> 

<span data-ttu-id="2aa59-109">アイコンはアプリ内、およびアプリの外部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-109">Icons can appear in apps—and outside them:</span></span> 

:::row:::
    :::column:::
        **Icons inside the app**

        ![icons inside the app](images/icons/inside-icons.png)
<span data-ttu-id="2aa59-110">アプリ内では、アイコンを使用して、テキストのコピーの設定 ページに移動するなどの操作を表すため。</span><span class="sxs-lookup"><span data-stu-id="2aa59-110">Inside your app, you use icons to represent an action, such as copying text or navigating to the settings page.</span></span>
    :::column-end:::
    :::column:::
<span data-ttu-id="2aa59-111">**アプリ外部のアイコン**</span><span class="sxs-lookup"><span data-stu-id="2aa59-111">**Icons outside the app**</span></span>

        ![icons outside the app](images/icons/outside-icons.jpg)
<span data-ttu-id="2aa59-112">Windows では、アプリでは、外部、アイコンを使用して、アプリの [スタート] メニューとタスク バーを表します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-112">Outside your app, Windows uses an icon to represent your app in the start menu and in the taskbar.</span></span> <span data-ttu-id="2aa59-113">場合は、ユーザーの [スタート] メニューにアプリをピン留めを選択開始のアプリのタイルはアプリのアイコンを機能できます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-113">If the user chooses to pin your app to the start menu, your app's start tile can feature your app's icon.</span></span> <span data-ttu-id="2aa59-114">アプリのアイコン、タイトル バーに表示され、アプリのロゴとスプラッシュ スクリーンを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-114">Your app's icon appears in the title bar and you can choose to create a splash screen with your app's logo.</span></span>
    :::column-end:::
:::row-end:::

<span data-ttu-id="2aa59-115">この記事では、アプリ内のアイコンについて説明します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-115">This article describes icons within your app.</span></span> <span data-ttu-id="2aa59-116">アプリの外部のアイコン (アプリ アイコン) の詳細については、「[アプリおよびタイル アイコンに関する記事](/windows/uwp/design/shell/tiles-and-notifications/app-assets)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2aa59-116">To learn about icons outside your app (app icons), see the [app and tile icons article](/windows/uwp/design/shell/tiles-and-notifications/app-assets).</span></span>

## <a name="when-to-use-icons"></a><span data-ttu-id="2aa59-117">アイコンを使う状況</span><span class="sxs-lookup"><span data-stu-id="2aa59-117">When to use icons</span></span>

<span data-ttu-id="2aa59-118">アイコンは領域を節約できますが、アイコンをいつ使用する必要があるか説明します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-118">Icons can save space, but when should you use them?</span></span> 

:::row:::
    :::column:::
        ![do](images/do.svg)
        ![icons standard image](images/icons/icons-standard.svg)<br>

<span data-ttu-id="2aa59-119">アクション、切り取り、コピー、貼り付けなどと、保存、またはナビゲーション メニューで、ナビゲーション項目のアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-119">Use an icon for actions, like cut, copy, paste, and save, or for navigation items in a navigation menu.</span></span>
    :::column-end:::
    :::column:::
        ![don't](images/dont.svg)
        ![icons concept image](images/icons/icons-concept.svg)<br>

<span data-ttu-id="2aa59-120">表現するという概念に既に存在する場合は、アイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-120">Use an icon if one already exists for the concept you want to represent.</span></span> <span data-ttu-id="2aa59-121">(アイコンが存在するかどうかを確認は、Segoe アイコンの一覧を確認します)。</span><span class="sxs-lookup"><span data-stu-id="2aa59-121">(To see whether an icon exists, check the Segoe icon list.)</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        ![do](images/do.svg)
        ![icon shopping cart](images/icons/icon-shopping-cart.svg)<br>

<span data-ttu-id="2aa59-122">ユーザーが、アイコンの意味を理解するが簡単が小さなサイズのチェック ボックスをオフにするのに十分な単純な場合は、アイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-122">Use an icon if it's easy for the user to understand what the icon means and it's simple enough to be clear at small sizes.</span></span>
    :::column-end:::
    :::column:::
        ![dont](images/dont.svg)
        ![icons concept image](images/icons/icon-bad-example.png)<br>

<span data-ttu-id="2aa59-123">その意味が明確でない場合、または複雑な図形を明確にする必要がある場合、アイコンを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="2aa59-123">Don't use an icon if its meaning isn't clear, or if making it clear requires a complex shape.</span></span>
    :::column-end:::
:::row-end:::



## <a name="using-the-right-type-of-icon"></a><span data-ttu-id="2aa59-124">適切な種類のアイコンの使用</span><span class="sxs-lookup"><span data-stu-id="2aa59-124">Using the right type of icon</span></span>

<span data-ttu-id="2aa59-125">アイコンを作成する方法は数多くあります。</span><span class="sxs-lookup"><span data-stu-id="2aa59-125">There are many ways to create an icon.</span></span> <span data-ttu-id="2aa59-126">Segoe MDL2 アセットなどの記号フォントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-126">You can use a symbol font like Segoe MDL2 Assets.</span></span> <span data-ttu-id="2aa59-127">ベクトルに基づくイメージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-127">You could create your own vector-based image.</span></span> <span data-ttu-id="2aa59-128">ビットマップ画像も使用できますが、お勧めしません。</span><span class="sxs-lookup"><span data-stu-id="2aa59-128">You can even use a bitmap image, although we don't recommend it.</span></span> <span data-ttu-id="2aa59-129">アプリにアイコンを追加するさまざまな方法の概要を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-129">Here's a summary of the different ways you can add an icon to your app.</span></span> 

### <a name="use-a-predefined-icon"></a><span data-ttu-id="2aa59-130">定義済みのアイコンを使用します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-130">Use a predefined icon.</span></span>
:::row:::
    :::column:::
<span data-ttu-id="2aa59-131">Microsoft では、1000 以上のアイコン Segoe MDL2 資産のフォントの形式で提供します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-131">Microsoft provides over 1000 icons in the form of the Segoe MDL2 Assets font.</span></span> <span data-ttu-id="2aa59-132">フォントからアイコンを取得するのは直感的ではない可能性がありますが、マイクロソフトのフォントの表示テクノロジでは、これらのアイコンが任意のディスプレイ、解像度、サイズではっきりと鮮明に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-132">It might not be intuitive to get an icon from a font, but our font display technology means these icons will look crisp and sharp on any display, at any resolution, and at any size.</span></span> <span data-ttu-id="2aa59-133">手順については、次を参照してください。 [Segoe MDL2 アイコン](segoe-ui-symbol-font.md)します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-133">For instructions, see [Segoe MDL2 icons](segoe-ui-symbol-font.md).</span></span>
    :::column-end:::
    :::column:::
        ![pre-defined icon image](images/icons/predefined-icon.png)
    :::column-end:::
:::row-end:::

### <a name="use-a-font"></a><span data-ttu-id="2aa59-134">フォントを使用します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-134">Use a font.</span></span>
:::row:::
    :::column:::
<span data-ttu-id="2aa59-135">-Segoe MDL2 資産フォントを使用することも、ユーザーが Wingdings または Webdings などのシステムにインストールされている任意のフォントを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-135">You don't have to use the Segoe MDL2 Assets font--you can use any font the user has installed on their system, such as Wingdings or Webdings.</span></span>
    :::column-end:::
    :::column:::
        ![wingdings image](images/icons/wingdings.png)
    :::column-end:::
:::row-end:::

### <a name="use-a-scalable-vector-graphics-svg-file"></a><span data-ttu-id="2aa59-136">スケーラブル ベクター グラフィックス (SVG) ファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-136">Use a Scalable Vector Graphics (SVG) file.</span></span>
:::row:::
    :::column:::
<span data-ttu-id="2aa59-137">常に鮮明に任意のサイズまたは解像度であるために、SVG のリソースは、アイコンに最適です。</span><span class="sxs-lookup"><span data-stu-id="2aa59-137">SVG resources are ideal for icons, because they always look sharp at any size or resolution.</span></span> <span data-ttu-id="2aa59-138">ほとんどの描画アプリケーションは、SVG にエクスポートできます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-138">Most drawing applications can export to SVG.</span></span> <span data-ttu-id="2aa59-139">手順については、次を参照してください。 [SVGImageSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.svgimagesource)します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-139">For instructions, see [SVGImageSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.imaging.svgimagesource).</span></span>
    :::column-end:::
    :::column:::
        ![SVG image](images/icons/icon-scale.gif)
    :::column-end:::
:::row-end:::

### <a name="use-geometry-objects"></a><span data-ttu-id="2aa59-140">ジオメトリ オブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-140">Use Geometry objects.</span></span>
:::row:::
    :::column:::
<span data-ttu-id="2aa59-141">、SVG ファイルと同様、ジオメトリは、ので、常にシャープなベクトル ベースのリソースです。</span><span class="sxs-lookup"><span data-stu-id="2aa59-141">Like SVG files, geometries are a vector-based resource, so they always look sharp.</span></span> <span data-ttu-id="2aa59-142">ただし、それぞれの点と曲線を個々に指定する必要があるため、ジオメトリの作成は複雑です。</span><span class="sxs-lookup"><span data-stu-id="2aa59-142">However, creating a geometry is complicated because you have to individually specify each point and curve.</span></span> <span data-ttu-id="2aa59-143">実際にはアプリの実行中にアイコンを変更する必要がある場合のみ最適です (アプリをアニメーション化する場合など)。</span><span class="sxs-lookup"><span data-stu-id="2aa59-143">It's really only a good choice if you need to modify the icon while your app is running (to animate it, for example).</span></span> <span data-ttu-id="2aa59-144">手順については、「[ジオメトリのコマンドの移動と描画](../../xaml-platform/move-draw-commands-syntax.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2aa59-144">For instructions, see [Move and draw commands for geometries](../../xaml-platform/move-draw-commands-syntax.md).</span></span> 
    :::column-end:::
    :::column:::
        ![Geometry objects image](images/icons/geometry-objects.png)
    :::column-end:::
:::row-end:::

### <a name="you-can-also-use-a-bitmap-image-such-as-png-gif-or-jpeg-although-we-dont-recommend-it"></a><span data-ttu-id="2aa59-145">お勧めしませんが、PNG、GIF、JPEG などのビットマップ画像を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-145">You can also use a bitmap image, such as PNG, GIF, or JPEG, although we don't recommend it.</span></span>
:::row:::
    :::column:::
<span data-ttu-id="2aa59-146">ビットマップ イメージは、ので、あるアイコンをクリックする大きさと画面の解像度に応じて拡大または縮小するのには、特定のサイズで作成されます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-146">Bitmap images are created at a specific size, so they have to be scaled up or down depending on how large you want the icon to be and the resolution of the screen.</span></span> <span data-ttu-id="2aa59-147">画像を縮小すると、ぼやけて見えることがあります。画像を拡大すると、むらのあるピクセル化された外観になることがあります。</span><span class="sxs-lookup"><span data-stu-id="2aa59-147">When the image is scaled down (shrunk), it can appear blurry; when it's scaled up, it can appear blocky and pixelated.</span></span> <span data-ttu-id="2aa59-148">ビットマップ画像を使用する必要がある場合は、JPEG ではなく PNG または GIF を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2aa59-148">If you have to use a bitmap image we recommend using a PNG or GIF over a JPEG.</span></span> 
    :::column-end:::
    :::column:::
        ![don't](images/dont.svg)
        ![Bitmap image](images/icons/bitmap-image.png)
    :::column-end:::
:::row-end:::

## <a name="make-the-icon-do-something"></a><span data-ttu-id="2aa59-149">アイコンで何かを行う</span><span class="sxs-lookup"><span data-stu-id="2aa59-149">Make the icon do something</span></span>

<span data-ttu-id="2aa59-150">アイコンを作成したら、次の手順はコマンドまたはナビゲーション操作に関連付けることで行うようにすることです。</span><span class="sxs-lookup"><span data-stu-id="2aa59-150">Once you have an icon, the next step is to make it do something by associating it with command or a navigation action.</span></span> <span data-ttu-id="2aa59-151">これを行う最善の方法では、ボタンまたはコマンド バーにアイコンを追加します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-151">The best way to do this is to add the icon to a button or a command bar.</span></span> 

![コマンド バーのイメージ](images/icons/app-bar-desktop.svg)

## <a name="create-an-icon-button"></a><span data-ttu-id="2aa59-153">アイコン ボタンの作成</span><span class="sxs-lookup"><span data-stu-id="2aa59-153">Create an icon button</span></span>

<span data-ttu-id="2aa59-154">アイコンは標準的なボタンに配置することができます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-154">You can put an icon in a standard button.</span></span> <span data-ttu-id="2aa59-155">ボタンは幅広い場所で使用できるため、アクション アイコンが表示される場所に関して、柔軟性がやや高くなります。</span><span class="sxs-lookup"><span data-stu-id="2aa59-155">Since you can use buttons in a wider variet of places, this gives you a little more flexibility for where your action icon appears.</span></span> 

<span data-ttu-id="2aa59-156">ボタンにアイコンを追加する方法は次のようにいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="2aa59-156">The are a few ways to add an icon to a button:</span></span>

:::row:::
    :::column span="2":::
        <b>Step 1</b><br>
<span data-ttu-id="2aa59-157">ボタンのフォント ファミリを設定`Segoe MDL2 Assets`と unicode の値を使用するグリフのコンテンツのプロパティ。</span><span class="sxs-lookup"><span data-stu-id="2aa59-157">Set the button's font family to `Segoe MDL2 Assets` and its content property to the unicode value of the glyph you want to use:</span></span>
    :::column-end:::
    :::column:::
        ![Create an icon button step 1](images/icons/create-icon-step-1.svg)
    :::column-end:::
:::row-end:::

```xaml 
<Button FontFamily="Segoe MDL2 Assets" Content="&#xE102;" />
```

:::row:::
    :::column span="2":::
        <b>Step 2</b><br>
<span data-ttu-id="2aa59-158">Icon 要素のオブジェクトのいずれかを使用できます。[BitmapIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.bitmapicon)、 [FontIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.fonticon)、 [PathIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.pathicon)、または[SymbolIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.symbolicon)します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-158">You can use one of the icon element objects: [BitmapIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.bitmapicon), [FontIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.fonticon), [PathIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.pathicon), or [SymbolIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.symbolicon).</span></span> <span data-ttu-id="2aa59-159">これは複数の種類のアイコンが、選択してする場合はアイコンと他の種類のテキストなどのコンテンツを結合することができます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-159">This gives you more types of icons to choose from, and enables you to combine icons and other types of content, such as text, if you want:</span></span>
    :::column-end:::
    :::column:::
        ![Create an icon button step 2](images/icons/icon-text-step-2.svg)
    :::column-end:::
:::row-end:::

```xaml 
<Button>
    <StackPanel>
        <SymbolIcon Symbol="Play" />
        <TextBlock>Play the movie</TextBlock>
    </StackPanel>
</Button>
```

## <a name="create-a-series-of-icons-in-a-command-bar"></a><span data-ttu-id="2aa59-160">コマンド バーでの一連のアイコンの作成</span><span class="sxs-lookup"><span data-stu-id="2aa59-160">Create a series of icons in a command bar</span></span>

:::row:::
    :::column span:::
<span data-ttu-id="2aa59-161">切り取り/コピー/貼り付けまたは描画写真編集プログラムでは、コマンドのセットに追加するなど、一連の同時コマンドがある場合、[コマンド バー](../controls-and-patterns/app-bars.md)します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-161">When you have a series of commands that go together, such as cut/copy/paste or a set of drawing commands for a photo-editing program, put them together in a [command bar](../controls-and-patterns/app-bars.md).</span></span> <span data-ttu-id="2aa59-162">コマンド バーは、1 つ以上のアプリ バーのボタンまたはアプリ バーのトグル ボタンを取得します。それぞれのボタンはアクションを表します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-162">A command bar takes one or more app bar buttons or app bar toggle buttons, each of which represents an action.</span></span> <span data-ttu-id="2aa59-163">それぞれのボタンには、表示されるアイコンを制御するために使用する[アイコン](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.appbarbutton#Windows_UI_Xaml_Controls_AppBarButton_Icon) プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="2aa59-163">Each button has an [Icon](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.appbarbutton#Windows_UI_Xaml_Controls_AppBarButton_Icon) property you use to control which icon it displays.</span></span> <span data-ttu-id="2aa59-164">アイコンを指定するには、さまざまな方法があります。</span><span class="sxs-lookup"><span data-stu-id="2aa59-164">There are a variety of ways to specify the icon.</span></span> 
    :::column-end:::
    :::column:::
        ![Example of a command bar with icons](images/icons/create-icon-command-bar.svg)
    :::column-end:::
:::row-end:::

<span data-ttu-id="2aa59-165">最も簡単な方法は、指定した定義済みのアイコンの一覧を使用することです。"戻る" または "停止" などのアイコン名を指定するだけで、システムが描画します。</span><span class="sxs-lookup"><span data-stu-id="2aa59-165">The easiest way is to use the list of predefined icons we provide—simply specify the icon name, such as "Back" or "Stop", and the system will draw it:</span></span> 

``` xaml
<CommandBar>
    <AppBarToggleButton Icon="Shuffle" Label="Shuffle" Click="AppBarButton_Click" />
    <AppBarToggleButton Icon="RepeatAll" Label="Repeat" Click="AppBarButton_Click"/>
    <AppBarSeparator/>
    <AppBarButton Icon="Back" Label="Back" Click="AppBarButton_Click"/>
    <AppBarButton Icon="Stop" Label="Stop" Click="AppBarButton_Click"/>
    <AppBarButton Icon="Play" Label="Play" Click="AppBarButton_Click"/>
    <AppBarButton Icon="Forward" Label="Forward" Click="AppBarButton_Click"/>
</CommandBar>

```
<span data-ttu-id="2aa59-166">アイコン名の完全な一覧については、「[Symbol 列挙値](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.symbol)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2aa59-166">For the complete list of icon names, see the [Symbol enumeration](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.symbol).</span></span> 

<span data-ttu-id="2aa59-167">コマンド バーにあるボタンにアイコンを指定する方法は他にもあります。</span><span class="sxs-lookup"><span data-stu-id="2aa59-167">There are other ways to provide icons for a button in a command bar:</span></span>

+ <span data-ttu-id="2aa59-168">[FontIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.fonticon) - アイコンは指定されたフォント ファミリのグリフに基づきます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-168">[FontIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.fonticon) - the icon is based on a glyph from the specified font family.</span></span>
+ <span data-ttu-id="2aa59-169">[BitmapIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.bitmapicon) - アイコンは指定された **URI** を持つビットマップ画像ファイルに基づきます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-169">[BitmapIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.bitmapicon) - the icon is based on a bitmap image file with the specified **Uri**.</span></span>
+ <span data-ttu-id="2aa59-170">[PathIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.pathicon) - アイコンは [Path](/uwp/api/windows.ui.xaml.shapes.path) データに基づきます。</span><span class="sxs-lookup"><span data-stu-id="2aa59-170">[PathIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.pathicon) - the icon is based on [Path](/uwp/api/windows.ui.xaml.shapes.path) data.</span></span>

<span data-ttu-id="2aa59-171">コマンド バーの詳細については、「[コマンド バーの記事](../controls-and-patterns/app-bars.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2aa59-171">To learn more about command bars, see the [command bar article](../controls-and-patterns/app-bars.md).</span></span> 



## <a name="related-articles"></a><span data-ttu-id="2aa59-172">関連記事</span><span class="sxs-lookup"><span data-stu-id="2aa59-172">Related articles</span></span>

* [<span data-ttu-id="2aa59-173">タイルおよびアイコンのアセットのガイドライン</span><span class="sxs-lookup"><span data-stu-id="2aa59-173">Guidelines for tile and icon assets</span></span>](../shell/tiles-and-notifications/app-assets.md)
