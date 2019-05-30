---
Description: ハイパーリンクはユーザーを、アプリの別の部分、別のアプリ、または別のブラウザー アプリを使って呼び出した URI (Uniform Resource Identifier) に誘導します。
title: ハイパーリンク
ms.assetid: 74302FF0-65FC-4820-B59A-718A765EF7F0
label: Hyperlinks
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: kisai
design-contact: kimsea
dev-contact: stpete
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: b17220a039612e0b13cd9842800c37c39bf194dd
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66362757"
---
# <a name="hyperlinks"></a><span data-ttu-id="99d9b-104">ハイパーリンク</span><span class="sxs-lookup"><span data-stu-id="99d9b-104">Hyperlinks</span></span>

 

<span data-ttu-id="99d9b-105">ハイパーリンクはユーザーを、アプリの別の部分、別のアプリ、または別のブラウザー アプリを使って呼び出した URI (Uniform Resource Identifier) に誘導します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-105">Hyperlinks navigate the user to another part of the app, to another app, or launch a specific uniform resource identifier (URI) using a separate browser app.</span></span> <span data-ttu-id="99d9b-106">XAML アプリにハイパーリンクを追加するには 2 つの方法、**ハイパーリンク** テキスト要素と **HyperlinkButton** コントロールがあります。</span><span class="sxs-lookup"><span data-stu-id="99d9b-106">There are two ways that you can add a hyperlink to a XAML app: the **Hyperlink** text element and **HyperlinkButton** control.</span></span>

> <span data-ttu-id="99d9b-107">**重要な API**:[ハイパーリンクのテキスト要素](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Hyperlink)、 [HyperlinkButton コントロール](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton)</span><span class="sxs-lookup"><span data-stu-id="99d9b-107">**Important APIs**: [Hyperlink text element](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Hyperlink), [HyperlinkButton control](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton)</span></span>

![ハイパーリンク ボタン](images/controls/hyperlink-button.png)


## <a name="is-this-the-right-control"></a><span data-ttu-id="99d9b-109">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="99d9b-109">Is this the right control?</span></span>

<span data-ttu-id="99d9b-110">ユーザーがテキストを選び、そのテキストに関する詳しい情報が表示される場所に移動するとき、この操作に応答するテキストが必要となる場合に、ハイパーリンクを使います。</span><span class="sxs-lookup"><span data-stu-id="99d9b-110">Use a hyperlink when you need text that responds when selected and navigates the user to more information about the text that was selected.</span></span>

<span data-ttu-id="99d9b-111">必要に応じて適切な種類のハイパーリンクを選んでください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-111">Choose the right type of hyperlink based on your needs:</span></span>

-   <span data-ttu-id="99d9b-112">テキスト コントロール内でインライン **ハイパーリンク** テキスト要素を使用します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-112">Use an inline **Hyperlink** text element inside of a text control.</span></span> <span data-ttu-id="99d9b-113">ハイパーリンク要素は他のテキスト要素とともに表示され、すべて InlineCollection で使うことができます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-113">A Hyperlink element flows with other text elements and you can use it in any InlineCollection.</span></span> <span data-ttu-id="99d9b-114">自動テキスト折り返しを必要とするが、大きいサイズのヒット ターゲットを必要としない場合は、テキスト ハイパーリンクを使います。</span><span class="sxs-lookup"><span data-stu-id="99d9b-114">Use a text hyperlink if you want automatic text wrapping and don't necessarily need a large hit target.</span></span> <span data-ttu-id="99d9b-115">ハイパーリンク テキストのサイズは小さく、ターゲットとして使うのが難しくなることがあります (特にタッチ操作の場合)。</span><span class="sxs-lookup"><span data-stu-id="99d9b-115">Hyperlink text can be small and difficult to target, especially for touch.</span></span>
-   <span data-ttu-id="99d9b-116">スタンドアロンのハイパーリンクには **HyperlinkButton** を使用します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-116">Use a **HyperlinkButton** for stand-alone hyperlinks.</span></span> <span data-ttu-id="99d9b-117">HyperlinkButton は、ボタンを使用する任意の場所で使用できる特殊なボタン コントロールです。</span><span class="sxs-lookup"><span data-stu-id="99d9b-117">A HyperlinkButton is a specialized Button control that you can use anywhere that you would use a Button.</span></span>
-   <span data-ttu-id="99d9b-118">クリック可能なイメージを作成するには[イメージ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.image) と一緒にそのコンテンツとして **HyperlinkButton** を使用します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-118">Use a **HyperlinkButton** with an [Image](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.image) as its content to make a clickable image.</span></span>

## <a name="examples"></a><span data-ttu-id="99d9b-119">例</span><span class="sxs-lookup"><span data-stu-id="99d9b-119">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="99d9b-120">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="99d9b-120">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="99d9b-121"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/HyperlinkButton">アプリを開き、HyperlinkButton の動作を確認</a>してください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-121">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/HyperlinkButton">open the app and see the HyperlinkButton in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="99d9b-122"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="99d9b-122"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="99d9b-123"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="99d9b-123"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="create-a-hyperlink-text-element"></a><span data-ttu-id="99d9b-124">ハイパーリンク テキスト要素を作成する</span><span class="sxs-lookup"><span data-stu-id="99d9b-124">Create a Hyperlink text element</span></span>

<span data-ttu-id="99d9b-125">この例では、[TextBlock](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock) 内のハイパーリンク テキスト要素の使用方法を示します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-125">This example shows how to use a Hyperlink text element inside of a [TextBlock](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock).</span></span>

```xml
<StackPanel Width="200">
    <TextBlock Text="Privacy" Style="{StaticResource SubheaderTextBlockStyle}"/>
    <TextBlock TextWrapping="WrapWholeWords">
        <Span xml:space="preserve"><Run>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Read the </Run><Hyperlink NavigateUri="http://www.contoso.com">Contoso Privacy Statement</Hyperlink><Run> in your browser.</Run> Donec pharetra, enim sit amet mattis tincidunt, felis nisi semper lectus, vel porta diam nisi in augue.</Span>
    </TextBlock>
</StackPanel>

```
<span data-ttu-id="99d9b-126">ハイパーリンクは、インラインで周囲のテキストと表示されます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-126">The hyperlink appears inline and flows with the surrounding text:</span></span>

![テキスト要素としてのハイパーリンクの例](images/controls_hyperlink-element.png) 

> <span data-ttu-id="99d9b-128">**ヒント**&nbsp;&nbsp;テキスト コントロールでハイパーリンクを XAML のその他のテキスト要素と一緒に使用する場合、[スパン](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.span) コンテナーにコンテンツを配置してスパンに `xml:space="preserve"` 属性を適用すると、ハイパーリンクとその他の要素間に空白を保持します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-128">**Tip**&nbsp;&nbsp;When you use a Hyperlink in a text control with other text elements in XAML, place the content in a [Span](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.span) container and apply the `xml:space="preserve"` attribute to the Span to keep the white space between the Hyperlink and other elements.</span></span>

## <a name="create-a-hyperlinkbutton"></a><span data-ttu-id="99d9b-129">HyperlinkButton を作成する</span><span class="sxs-lookup"><span data-stu-id="99d9b-129">Create a HyperlinkButton</span></span>

<span data-ttu-id="99d9b-130">テキストおよび画像の両方で HyperlinkButton を使用する方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-130">Here's how to use a HyperlinkButton, both with text and with an image.</span></span>

```xml
<StackPanel>
    <TextBlock Text="About" Style="{StaticResource TitleTextBlockStyle}"/>
    <HyperlinkButton NavigateUri="http://www.contoso.com">
        <Image Source="Assets/ContosoLogo.png"/>
    </HyperlinkButton>
    <TextBlock Text="Version: 1.0.0001" Style="{StaticResource CaptionTextBlockStyle}"/>
    <HyperlinkButton Content="Contoso.com" NavigateUri="http://www.contoso.com"/>
    <HyperlinkButton Content="Acknowledgments" NavigateUri="http://www.contoso.com"/>
    <HyperlinkButton Content="Help" NavigateUri="http://www.contoso.com"/>
</StackPanel>

```

<span data-ttu-id="99d9b-131">テキスト コンテンツの付いたハイパーリンク ボタンは、マークアップ テキストとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-131">The hyperlink buttons with text content appear as marked-up text.</span></span> <span data-ttu-id="99d9b-132">Contoso ロゴ画像もクリック可能なハイパーリンクです。</span><span class="sxs-lookup"><span data-stu-id="99d9b-132">The Contoso logo image is also a clickable hyperlink:</span></span>

![ボタン コントロールとしてのハイパーリンクの例](images/controls_hyperlink-button-image.png)

<span data-ttu-id="99d9b-134">次の例は、HyperlinkButton をコードで作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="99d9b-134">This example shows how to create a HyperlinkButton in code.</span></span>

```csharp
var helpLinkButton = new HyperlinkButton();
helpLinkButton.Content = "Help";
helpLinkButton.NavigateUri = new Uri("http://www.contoso.com");
```

## <a name="handle-navigation"></a><span data-ttu-id="99d9b-135">ナビゲーションの処理</span><span class="sxs-lookup"><span data-stu-id="99d9b-135">Handle navigation</span></span>

<span data-ttu-id="99d9b-136">どちらの種類のハイパーリンクでも同様にナビゲーションを処理します。**NavigateUri** プロパティを設定するか、または**クリック**イベントを処理することができます。 </span><span class="sxs-lookup"><span data-stu-id="99d9b-136">For both kinds of hyperlinks, you handle navigation the same way; you can set the **NavigateUri** property, or handle the **Click** event.</span></span>

<span data-ttu-id="99d9b-137">**URI に移動します**</span><span class="sxs-lookup"><span data-stu-id="99d9b-137">**Navigate to a URI**</span></span>

<span data-ttu-id="99d9b-138">ハイパーリンクを使用して URI に移動するには、NavigateUri プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-138">To use the hyperlink to navigate to a URI, set the NavigateUri property.</span></span> <span data-ttu-id="99d9b-139">ユーザーがハイパーリンクをクリックしてまたはタップすると、指定された URI が既定のブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-139">When a user clicks or taps the hyperlink, the specified URI opens in the default browser.</span></span> <span data-ttu-id="99d9b-140">既定のブラウザーは、アプリと別のプロセスで実行されます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-140">The default browser runs in a separate process from your app.</span></span>

> [!NOTE]
> <span data-ttu-id="99d9b-141">URI は [Windows.Foundation.Uri](/uwp/api/windows.foundation.uri) クラスで表されます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-141">A URI is represented by the [Windows.Foundation.Uri](/uwp/api/windows.foundation.uri) class.</span></span> <span data-ttu-id="99d9b-142">.NET を使用したプログラミングでは、このクラスは表示されないため、[System.Uri](https://docs.microsoft.com/dotnet/api/system.uri)クラスを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="99d9b-142">When programming with .NET, this class is hidden and you should use the [System.Uri](https://docs.microsoft.com/dotnet/api/system.uri) class.</span></span> <span data-ttu-id="99d9b-143">詳しくは、これらのクラスのリファレンス ページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-143">For more info, see the reference pages for these classes.</span></span>

<span data-ttu-id="99d9b-144">**http:** または **https:** スキームを使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-144">You don't have to use **http:** or **https:** schemes.</span></span> <span data-ttu-id="99d9b-145">ブラウザーに読み込むのに適したリソース コンテンツがこれらの場所にある場合は、**ms-appx:** 、**ms-appdata:** 、または **ms-resources:** などのスキームを使うことができます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-145">You can use schemes such as **ms-appx:**, **ms-appdata:**, or **ms-resources:**, if there's resource content at these locations that's appropriate to load in a browser.</span></span> <span data-ttu-id="99d9b-146">ただし、**file:** スキームは明確に禁止されます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-146">However, the **file:** scheme is specifically blocked.</span></span> <span data-ttu-id="99d9b-147">詳しくは、「[URI スキーム](https://docs.microsoft.com/previous-versions/windows/apps/jj655406(v=win.10))」 をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-147">For more info, see [URI schemes](https://docs.microsoft.com/previous-versions/windows/apps/jj655406(v=win.10)).</span></span>

<span data-ttu-id="99d9b-148">ユーザーがハイパーリンクをクリックすると、URI の種類とスキームのシステムのハンドラーに NavigateUri プロパティの値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-148">When a user clicks the hyperlink, the value of the NavigateUri property is passed to a system handler for URI types and schemes.</span></span> <span data-ttu-id="99d9b-149">システムは、NavigateUri の指定された URI のスキームに対して登録されているアプリを起動します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-149">The system then launches the app that is registered for the scheme of the URI provided for NavigateUri.</span></span>

<span data-ttu-id="99d9b-150">ハイパーリンクで、コンテンツを既定の Web ブラウザーで読み込む必要がない場合 (ブラウザーを表示しない場合) は、NavigateUri の値を設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-150">If you don't want the hyperlink to load content in a default Web browser (and don't want a browser to appear), then don't set a value for NavigateUri.</span></span> <span data-ttu-id="99d9b-151">代わりに、Click イベントを処理し、目的に合ったコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-151">Instead, handle the Click event, and write code that does what you want.</span></span>


<span data-ttu-id="99d9b-152">**クリック イベントを処理します。**</span><span class="sxs-lookup"><span data-stu-id="99d9b-152">**Handle the Click event**</span></span>

<span data-ttu-id="99d9b-153">アプリ内のナビゲーションなど、ブラウザーの URI の起動以外の操作に Click イベントを使用します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-153">Use the Click event for actions other than launching a URI in a browser, such as navigation within the app.</span></span> <span data-ttu-id="99d9b-154">たとえば、ブラウザーを開くのではなく、新しいアプリのページを読み込む場合は、クリック イベント ハンドラー内で [Frame.Navigate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate) メソッドを呼び出して新しいアプリのページに移動します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-154">For example, if you want to load a new app page rather than opening a browser, call a [Frame.Navigate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate) method within your Click event handler to navigate to the new app page.</span></span> <span data-ttu-id="99d9b-155">同様にアプリ内にある [WebView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.webview) コントロール内で外部の絶対 URI を読み込む場合は、[WebView.Navigate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.webview.navigate) を Click ハンドラーのロジックの一部として呼び出します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-155">If you want an external, absolute URI to load within a [WebView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.webview) control that also exists in your app, call [WebView.Navigate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.webview.navigate) as part of your Click handler logic.</span></span>

<span data-ttu-id="99d9b-156">通常は、これらはハイパーリンク要素を使用する別の 2 つの方法に相当するので、Click イベントの処理は行わず、NavigateUri 値も指定しません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-156">You don't typically handle the Click event as well as specifying a NavigateUri value, as these represent two different ways of using the hyperlink element.</span></span> <span data-ttu-id="99d9b-157">既定のブラウザーで URI を開き、NavigateUri の値を指定した場合は、クリック イベントは処理しません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-157">If your intent is to open the URI in the default browser, and you have specified a value for NavigateUri, don't handle the Click event.</span></span> <span data-ttu-id="99d9b-158">逆に、クリック イベントを処理する場合は、NavigateUri を指定しないでください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-158">Conversely, if you handle the Click event, don't specify a NavigateUri.</span></span>

<span data-ttu-id="99d9b-159">既定のブラウザーが NavigateUri に指定されている任意の有効なターゲットを読み込むことを防ぐためにClick イベント ハンドラー内でできることはありません。ハイパーリンクがアクティブ化されると操作は自動的に (非同期的に) 行われ、Click イベント ハンドラー内で取り消すことはできません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-159">There's nothing you can do within the Click event handler to prevent the default browser from loading any valid target specified for NavigateUri; that action takes place automatically (asynchronously) when the hyperlink is activated and can't be canceled from within the Click event handler.</span></span> 

## <a name="hyperlink-underlines"></a><span data-ttu-id="99d9b-160">ハイパーリンクの下線</span><span class="sxs-lookup"><span data-stu-id="99d9b-160">Hyperlink underlines</span></span>
<span data-ttu-id="99d9b-161">既定では、ハイパーリンクに下線が引かれます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-161">By default, hyperlinks are underlined.</span></span> <span data-ttu-id="99d9b-162">この下線は、アクセシビリティ要件を満たすために役立つので重要です。</span><span class="sxs-lookup"><span data-stu-id="99d9b-162">This underline is important because it helps meet accessibility requirements.</span></span> <span data-ttu-id="99d9b-163">色覚に障碍があるユーザーは、ハイパーリンクとその他のテキストを区別するために下線を使用します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-163">Color-blind users use the underline to distinguish between hyperlinks and other text.</span></span> <span data-ttu-id="99d9b-164">下線を無効にした場合は、ハイパーリンクを他のテキストと区別するために、FontWeight または FontStyle など、他の書式設定の違いを追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-164">If you disable underlines, you should consider adding some other type of formatting difference to distinguish hyperlinks from other text, such as FontWeight or FontStyle.</span></span>

<span data-ttu-id="99d9b-165">**ハイパーリンクのテキスト要素**</span><span class="sxs-lookup"><span data-stu-id="99d9b-165">**Hyperlink text elements**</span></span>

<span data-ttu-id="99d9b-166">[UnderlineStyle](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.hyperlink.underlinestyle) プロパティを設定すると下線の表示を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-166">You can set the [UnderlineStyle](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.hyperlink.underlinestyle) property to disable the underline.</span></span> <span data-ttu-id="99d9b-167">これを行う場合は、リンクを表すテキストを区別するために [FontWeight](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement.fontweight) または [FontStyle](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement.fontstyle) を使うことを検討します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-167">If you do, consider using [FontWeight](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement.fontweight) or [FontStyle](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement.fontstyle) to differentiate your link text.</span></span>

<span data-ttu-id="99d9b-168">**HyperlinkButton**</span><span class="sxs-lookup"><span data-stu-id="99d9b-168">**HyperlinkButton**</span></span> 

<span data-ttu-id="99d9b-169">既定では、HyperlinkButton は、[Content](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.contentcontrol.content) プロパティの値として文字列を設定すると、下線付きテキストとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-169">By default, the HyperlinkButton appears as underlined text when you set a string as the value for the [Content](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.contentcontrol.content) property.</span></span>

<span data-ttu-id="99d9b-170">次の場合、テキストは下線付きで表示されません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-170">The text does not appear underlined in the following cases:</span></span>
- <span data-ttu-id="99d9b-171">コンテンツのプロパティの値として [TextBlock](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock) を設定し、TextBlock の [Text](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock.text) プロパティを設定した場合。</span><span class="sxs-lookup"><span data-stu-id="99d9b-171">You set a [TextBlock](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock) as the value for the Content property, and set the [Text](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock.text) property on the TextBlock.</span></span>
- <span data-ttu-id="99d9b-172">HyperlinkButton を再テンプレートして [ContentPresenter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.contentpresenter) テンプレート パーツの名前を変更した場合。</span><span class="sxs-lookup"><span data-stu-id="99d9b-172">You re-template the HyperlinkButton and change the name of the [ContentPresenter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.contentpresenter) template part.</span></span>

<span data-ttu-id="99d9b-173">下線の無いテキストとして表示されるボタンが必要な場合は、標準のボタン コントロールを使い、そのスタイルのプロパティに組み込みの `TextBlockButtonStyle` システム リソースを適用することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-173">If you need a button that appears as non-underlined text, consider using a standard Button control and applying the built-in `TextBlockButtonStyle` system resource to its Style property.</span></span>

## <a name="notes-for-hyperlink-text-element"></a><span data-ttu-id="99d9b-174">ハイパーリンク テキスト要素の注意点</span><span class="sxs-lookup"><span data-stu-id="99d9b-174">Notes for Hyperlink text element</span></span>

<span data-ttu-id="99d9b-175">このセクションは、ハイパーリンク テキスト要素にのみ該当します。HyperlinkButton コントロールには該当しません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-175">This section applies only to the Hyperlink text element, not to the HyperlinkButton control.</span></span>

<span data-ttu-id="99d9b-176">**入力イベント**</span><span class="sxs-lookup"><span data-stu-id="99d9b-176">**Input events**</span></span>

<span data-ttu-id="99d9b-177">ハイパーリンクは [UIElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement) ではないため、Tapped、PointerPressed などの UI 要素の入力イベントのセットはありません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-177">Because a Hyperlink is not a [UIElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement), it does not have the set of UI element input events such as Tapped, PointerPressed, and so on.</span></span> <span data-ttu-id="99d9b-178">代わりに、ハイパーリンクには、独自の Click イベントに加えて、NavigateUri として指定されている任意の URI を読み込むシステムの暗黙的な動作があります。</span><span class="sxs-lookup"><span data-stu-id="99d9b-178">Instead, a Hyperlink has its own Click event, plus the implicit behavior of the system loading any URI specified as the NavigateUri.</span></span> <span data-ttu-id="99d9b-179">システムは、ハイパーリンクのアクションを呼び出し、応答で Click イベントを発生させる必要があるすべての入力動作を処理します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-179">The system handles all input actions that should invoke the Hyperlink actions and raises the Click event in response.</span></span>

<span data-ttu-id="99d9b-180">**コンテンツ**</span><span class="sxs-lookup"><span data-stu-id="99d9b-180">**Content**</span></span>

<span data-ttu-id="99d9b-181">ハイパーリンクには、その [Inlines](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.span.inlines) コレクション内にあるコンテンツの制限があります。</span><span class="sxs-lookup"><span data-stu-id="99d9b-181">Hyperlink has restrictions on the content that can exist in its [Inlines](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.span.inlines) collection.</span></span> <span data-ttu-id="99d9b-182">具体的には、ハイパーリンクは、[実行](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.run)および別のハイパーリンクではないその他の[スパン](/uwp/api/windows.ui.xaml.documents.span) タイプのみ許可します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-182">Specifically, a Hyperlink only permits [Run](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.run) and other [Span](/uwp/api/windows.ui.xaml.documents.span) types that aren't another Hyperlink.</span></span> <span data-ttu-id="99d9b-183">[InlineUIContainer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.inlineuicontainer) は、ハイパーリンクの Inlines コレクション内にはありません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-183">[InlineUIContainer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.inlineuicontainer) can't be in the Inlines collection of a Hyperlink.</span></span> <span data-ttu-id="99d9b-184">制限されたコンテンツを追加しようとすると、無効な引数の例外、または XAML 解析例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-184">Attempting to add restricted content throws an invalid argument exception or XAML parse exception.</span></span>

<span data-ttu-id="99d9b-185">**ハイパーリンクとテーマまたはスタイルの動作**</span><span class="sxs-lookup"><span data-stu-id="99d9b-185">**Hyperlink and theme/style behavior**</span></span>

<span data-ttu-id="99d9b-186">ハイパーリンクは [コントロール](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control) から継承しないため、[Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) プロパティまたは [Template](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.template) がありません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-186">Hyperlink doesn't inherit from [Control](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control), so it doesn't have a [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) property or a [Template](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.template).</span></span> <span data-ttu-id="99d9b-187">Foreground または FontFamily など、[TextElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement) から継承されたプロパティを編集してハイパーリンクの外観を変更できますが、一般的なスタイルまたはテンプレートを使用して変更を適用することはできません。</span><span class="sxs-lookup"><span data-stu-id="99d9b-187">You can edit the properties that are inherited from [TextElement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement), such as Foreground or FontFamily, to change the appearance of a Hyperlink, but you can't use a common style or template to apply changes.</span></span> <span data-ttu-id="99d9b-188">テンプレートを使う代わりに、一貫性を保つためにハイパーリンクのプロパティの値の一般的なリソースの使用を検討してください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-188">Instead of using a template, consider using common resources for values of Hyperlink properties to provide consistency.</span></span> <span data-ttu-id="99d9b-189">一部のプロパティのハイパーリンクは、システムによって提供される {themeresource} マークアップ拡張機能の値から既定の設定を使用します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-189">Some properties of Hyperlink use defaults from a {ThemeResource} markup extension value provided by the system.</span></span> <span data-ttu-id="99d9b-190">これにより、ハイパーリンクの外観は、実行時にシステム テーマが変更されると、適切な方法で切り替わります。</span><span class="sxs-lookup"><span data-stu-id="99d9b-190">This enables the Hyperlink appearance to switch in appropriate ways when the user changes the system theme at run-time.</span></span>

<span data-ttu-id="99d9b-191">ハイパーリンクの既定の色は、システムのアクセント カラーです。</span><span class="sxs-lookup"><span data-stu-id="99d9b-191">The default color of the hyperlink is the accent color of the system.</span></span> <span data-ttu-id="99d9b-192">[Foreground](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement.foreground)  プロパティを設定するとこれを上書きできます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-192">You can set the [Foreground](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.textelement.foreground) property to override this.</span></span>

## <a name="recommendations"></a><span data-ttu-id="99d9b-193">推奨事項</span><span class="sxs-lookup"><span data-stu-id="99d9b-193">Recommendations</span></span>

-   <span data-ttu-id="99d9b-194">ハイパーリンクを使う場合は、移動のみを目的としてください。他の操作のためにハイパーリンクは使わないでください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-194">Only use hyperlinks for navigation; don't use them for other actions.</span></span>
-   <span data-ttu-id="99d9b-195">テキスト ベースのハイパーリンクには、書体見本の本文スタイルを使います。</span><span class="sxs-lookup"><span data-stu-id="99d9b-195">Use the Body style from the type ramp for text-based hyperlinks.</span></span> <span data-ttu-id="99d9b-196">[フォントと Windows 10 の書体見本](../style/typography.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="99d9b-196">Read about [fonts and the Windows 10 type ramp](../style/typography.md).</span></span>
-   <span data-ttu-id="99d9b-197">個々のハイパーリンクの間には十分な間隔を空けます。これにより、それぞれのハイパーリンクを区別することができ、ハイパーリンクを間違えずに選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-197">Keep discrete hyperlinks far enough apart so that the user can differentiate between them and has an easy time selecting each one.</span></span>
-   <span data-ttu-id="99d9b-198">ユーザーの移動先を示すヒントをハイパーリンクに追加します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-198">Add tooltips to hyperlinks that indicate to where the user will be directed.</span></span> <span data-ttu-id="99d9b-199">ユーザーが外部サイトに移動する場合は、ヒント内にトップレベルのドメイン名を入れ、補助的なフォント色を使ってそのテキストのスタイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="99d9b-199">If the user will be directed to an external site, include the top-level domain name inside the tooltip, and style the text with a secondary font color.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="99d9b-200">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="99d9b-200">Get the sample code</span></span>

- <span data-ttu-id="99d9b-201">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="99d9b-201">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-articles"></a><span data-ttu-id="99d9b-202">関連記事</span><span class="sxs-lookup"><span data-stu-id="99d9b-202">Related articles</span></span>

- [<span data-ttu-id="99d9b-203">テキスト コントロール</span><span class="sxs-lookup"><span data-stu-id="99d9b-203">Text controls</span></span>](text-controls.md)
- [<span data-ttu-id="99d9b-204">ツールヒントのガイドライン</span><span class="sxs-lookup"><span data-stu-id="99d9b-204">Guidelines for tooltips</span></span>](tooltips.md)

<span data-ttu-id="99d9b-205">**開発者向け (XAML)**</span><span class="sxs-lookup"><span data-stu-id="99d9b-205">**For developers (XAML)**</span></span>
- [<span data-ttu-id="99d9b-206">Windows.UI.Xaml.Documents.Hyperlink クラス</span><span class="sxs-lookup"><span data-stu-id="99d9b-206">Windows.UI.Xaml.Documents.Hyperlink class</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Hyperlink)
- [<span data-ttu-id="99d9b-207">Windows.UI.Xaml.Controls.HyperlinkButton クラス</span><span class="sxs-lookup"><span data-stu-id="99d9b-207">Windows.UI.Xaml.Controls.HyperlinkButton class</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton)
