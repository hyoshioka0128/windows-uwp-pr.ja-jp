---
Description: RichTextBlockOverflow 要素を持つ RichTextBlock を使って、高度なテキスト レイアウトを作成します。
title: RichTextBlock
ms.assetid: E4BE4B1B-418E-4075-88F1-22C09DDF8E45
label: Rich text block
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: miguelrb
design-contact: ksulliv
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: e671c61058ec1c048fbb1b547cc79060a7cd0d0a
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66364343"
---
# <a name="rich-text-block"></a><span data-ttu-id="08332-104">リッチ テキスト ブロック</span><span class="sxs-lookup"><span data-stu-id="08332-104">Rich text block</span></span>

 

<span data-ttu-id="08332-105">リッチ テキスト ブロックは、段落、インライン UI 要素、複雑なテキスト レイアウトなどのサポートが必要な場合に使用できる、高度なテキスト レイアウト用のいくつかの機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="08332-105">Rich text blocks provide several features for advanced text layout that you can use when you need support for paragraphs, inline UI elements, or complex text layouts.</span></span>

> <span data-ttu-id="08332-106">**重要な API**:[RichTextBlock クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock)、 [RichTextBlockOverflow クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlockOverflow)、[クラスを段落](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Paragraph)、[タイポグラフィ クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Typography)</span><span class="sxs-lookup"><span data-stu-id="08332-106">**Important APIs**: [RichTextBlock class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock), [RichTextBlockOverflow class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlockOverflow), [Paragraph class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Paragraph), [Typography class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Typography)</span></span>

## <a name="is-this-the-right-control"></a><span data-ttu-id="08332-107">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="08332-107">Is this the right control?</span></span>

<span data-ttu-id="08332-108">複数の段落、段組などの複雑なテキスト レイアウト、インライン UI 要素 (画像など) をサポートする必要がある場合は、**RichTextBlock** を使います。</span><span class="sxs-lookup"><span data-stu-id="08332-108">Use a **RichTextBlock** when you need support for multiple paragraphs, multi-column or other complex text layouts, or inline UI elements like images.</span></span>

<span data-ttu-id="08332-109">**TextBlock** を使用して、アプリ内の読み取り専用テキストの大半を表示します。</span><span class="sxs-lookup"><span data-stu-id="08332-109">Use a **TextBlock** to display most read-only text in your app.</span></span> <span data-ttu-id="08332-110">これを使用すると、単一行または複数行のテキスト、インライン ハイパーリンク、書式 (太字、斜体、下線付きなど) が設定されたテキストを表示できます。</span><span class="sxs-lookup"><span data-stu-id="08332-110">You can use it to display single-line or multi-line text, inline hyperlinks, and text with formatting like bold, italic, or underlined.</span></span> <span data-ttu-id="08332-111">TextBlock は、よりシンプルなコンテンツ モデルを提供します。そのため、一般に使い方がより簡単で、テキスト レンダリングのパフォーマンスも RichTextBlock より優れています。</span><span class="sxs-lookup"><span data-stu-id="08332-111">TextBlock provides a simpler content model, so it’s typically easier to use, and it can provide better text rendering performance than RichTextBlock.</span></span> <span data-ttu-id="08332-112">ほとんどのアプリで UI テキストに適しています。</span><span class="sxs-lookup"><span data-stu-id="08332-112">It's preferred for most app UI text.</span></span> <span data-ttu-id="08332-113">テキスト内に改行を配置することはできますが、TextBlock は単一の段落を表示するために設計されており、テキストのインデントはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="08332-113">Although you can put line breaks in the text, TextBlock is designed to display a single paragraph and doesn’t support text indentation.</span></span>

<span data-ttu-id="08332-114">適切なテキスト コントロールの選択について詳しくは、「[テキスト コントロール](text-controls.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="08332-114">For more info about choosing the right text control, see the [Text controls](text-controls.md) article.</span></span>

## <a name="examples"></a><span data-ttu-id="08332-115">例</span><span class="sxs-lookup"><span data-stu-id="08332-115">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="08332-116">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="08332-116">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="08332-117"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/RichTextBlock">アプリを開き、RichTextBlock の動作を確認</a>してください。</span><span class="sxs-lookup"><span data-stu-id="08332-117">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/RichTextBlock">open the app and see the RichTextBlock in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="08332-118"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="08332-118"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="08332-119"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="08332-119"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="create-a-rich-text-block"></a><span data-ttu-id="08332-120">リッチ テキスト ブロックを作成する</span><span class="sxs-lookup"><span data-stu-id="08332-120">Create a rich text block</span></span>

<span data-ttu-id="08332-121">RichTextBlock のコンテンツ プロパティは [Blocks](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richtextblock.blocks) プロパティです。このプロパティでは、[Paragraph](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Paragraph) 要素によって段落に基づくテキストがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="08332-121">The content property of RichTextBlock is the [Blocks](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richtextblock.blocks) property, which supports paragraph based text via the [Paragraph](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Paragraph) element.</span></span> <span data-ttu-id="08332-122">アプリ内でコントロールのテキスト コンテンツに簡単にアクセスすることができる **Text** プロパティは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="08332-122">It doesn't have a **Text** property that you can use to easily access the control's text content in your app.</span></span> <span data-ttu-id="08332-123">しかし、RichTextBlock には、TextBlock にはない独自の機能がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="08332-123">However, RichTextBlock provides several unique features that TextBlock doesn’t provide.</span></span> 

<span data-ttu-id="08332-124">RichTextBlock では次の機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="08332-124">RichTextBlock supports:</span></span>
- <span data-ttu-id="08332-125">複数の段落。</span><span class="sxs-lookup"><span data-stu-id="08332-125">Multiple paragraphs.</span></span> <span data-ttu-id="08332-126">段落のインデントを設定するには [TextIndent](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richtextblock.textindent) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="08332-126">Set the indentation for paragraphs by setting the [TextIndent](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richtextblock.textindent) property.</span></span>
- <span data-ttu-id="08332-127">インライン UI 要素。</span><span class="sxs-lookup"><span data-stu-id="08332-127">Inline UI elements.</span></span> <span data-ttu-id="08332-128">画像などの UI 要素をテキスト内にインラインで表示するには [InlineUIContainer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.InlineUIContainer) を使います。</span><span class="sxs-lookup"><span data-stu-id="08332-128">Use an [InlineUIContainer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.InlineUIContainer) to display UI elements, such as images, inline with your text.</span></span>
- <span data-ttu-id="08332-129">オーバーフロー コンテナー。</span><span class="sxs-lookup"><span data-stu-id="08332-129">Overflow containers.</span></span> <span data-ttu-id="08332-130">段組テキスト レイアウトを作成するには [RichTextBlockOverflow](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlockOverflow) 要素を使います。</span><span class="sxs-lookup"><span data-stu-id="08332-130">Use [RichTextBlockOverflow](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlockOverflow) elements to create multi-column text layouts.</span></span>

### <a name="paragraphs"></a><span data-ttu-id="08332-131">段落</span><span class="sxs-lookup"><span data-stu-id="08332-131">Paragraphs</span></span>

<span data-ttu-id="08332-132">RichTextBlock コントロール内に表示するテキストのブロックを定義するには [Paragraph](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Paragraph) 要素を使います。</span><span class="sxs-lookup"><span data-stu-id="08332-132">You use [Paragraph](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Paragraph) elements to define the blocks of text to display within a RichTextBlock control.</span></span> <span data-ttu-id="08332-133">すべての RichTextBlock に少なくとも 1 つの Paragraph を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="08332-133">Every RichTextBlock should include at least one Paragraph.</span></span> 

<span data-ttu-id="08332-134">RichTextBlock のすべての段落のインデントを設定するには、[RichTextBlock.TextIndent](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richtextblock.textindent) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="08332-134">You can set the indent amount for all paragraphs in a RichTextBlock by setting the [RichTextBlock.TextIndent](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richtextblock.textindent) property.</span></span> <span data-ttu-id="08332-135">RichTextBlock 内の特定の段落でこの設定を上書きするには、[Paragraph.TextIndent](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.paragraph.textindent) プロパティを別の値に設定します。</span><span class="sxs-lookup"><span data-stu-id="08332-135">You can override this setting for specific paragraphs in a RichTextBlock by setting the [Paragraph.TextIndent](https://docs.microsoft.com/uwp/api/windows.ui.xaml.documents.paragraph.textindent) property to a different value.</span></span>

```xaml
<RichTextBlock TextIndent="12">
  <Paragraph TextIndent="24">First paragraph.</Paragraph>
  <Paragraph>Second paragraph.</Paragraph>
  <Paragraph>Third paragraph. <Bold>With an inline.</Bold></Paragraph>
</RichTextBlock>
```

### <a name="inline-ui-elements"></a><span data-ttu-id="08332-136">インライン UI 要素</span><span class="sxs-lookup"><span data-stu-id="08332-136">Inline UI elements</span></span>

<span data-ttu-id="08332-137">[InlineUIContainer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.InlineUIContainer) クラスを使うと、任意の UIElement をテキスト内にインラインで埋め込むことができます。</span><span class="sxs-lookup"><span data-stu-id="08332-137">The [InlineUIContainer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.InlineUIContainer) class lets you embed any UIElement inline with your text.</span></span> <span data-ttu-id="08332-138">Image をテキスト内にインラインで配置するシナリオが一般的ですが、Button、CheckBox などの対話型の要素を使うこともできます。</span><span class="sxs-lookup"><span data-stu-id="08332-138">A common scenario is to place an Image inline with your text, but you can also use interactive elements, like a Button or CheckBox.</span></span>

<span data-ttu-id="08332-139">同じ位置に複数の要素をインラインで埋め込むには、パネルを 1 つの InlineUIContainer の子として使って、そのパネルに複数の要素を配置することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="08332-139">If you want to embed more than one element inline in the same position, consider using a panel as the single InlineUIContainer child, and then place the multiple elements within that panel.</span></span>

<span data-ttu-id="08332-140">次の例は、InlineUIContainer を使って RichTextBlock に画像を挿入する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="08332-140">This example shows how to use an InlineUIContainer to insert an image into a RichTextBlock.</span></span> 

```xaml
<RichTextBlock>
    <Paragraph>
        <Italic>This is an inline image.</Italic>
        <InlineUIContainer>
            <Image Source="Assets/Square44x44Logo.png" Height="30" Width="30"/>
        </InlineUIContainer>
        Mauris auctor tincidunt auctor.
    </Paragraph>
</RichTextBlock>
```

## <a name="overflow-containers"></a><span data-ttu-id="08332-141">オーバーフロー コンテナー</span><span class="sxs-lookup"><span data-stu-id="08332-141">Overflow containers</span></span>

<span data-ttu-id="08332-142">[RichTextBlockOverflow](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlockOverflow) 要素を持つ RichTextBlock を使って、段組などの高度なページ レイアウトを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="08332-142">You can use a RichTextBlock with [RichTextBlockOverflow](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlockOverflow) elements to create multi-column or other advanced page layouts.</span></span> <span data-ttu-id="08332-143">RichTextBlockOverflow 要素のコンテンツは、常に RichTextBlock 要素から取得されます。</span><span class="sxs-lookup"><span data-stu-id="08332-143">The content for a RichTextBlockOverflow element always comes from a RichTextBlock element.</span></span> <span data-ttu-id="08332-144">RichTextBlockOverflow 要素をリンクするには、その要素を RichTextBlock または別の RichTextBlockOverflow の OverflowContentTarget として設定します。</span><span class="sxs-lookup"><span data-stu-id="08332-144">You link RichTextBlockOverflow elements by setting them as the OverflowContentTarget of a RichTextBlock or another RichTextBlockOverflow.</span></span>

<span data-ttu-id="08332-145">2 段組みのレイアウトを作成する簡単な例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="08332-145">Here's a simple example that creates a two column layout.</span></span> <span data-ttu-id="08332-146">より複雑な例については、「例」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="08332-146">See the Examples section for a more complex example.</span></span>

```xaml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
    <RichTextBlock Grid.Column="0" 
                   OverflowContentTarget="{Binding ElementName=overflowContainer}" >
        <Paragraph>
            Proin ac metus at quam luctus ultricies.
        </Paragraph>
    </RichTextBlock>
    <RichTextBlockOverflow x:Name="overflowContainer" Grid.Column="1"/>
</Grid>
```

## <a name="formatting-text"></a><span data-ttu-id="08332-147">テキストの書式設定</span><span class="sxs-lookup"><span data-stu-id="08332-147">Formatting text</span></span>

<span data-ttu-id="08332-148">RichTextBlock に格納されるのはプレーン テキストですが、各種の書式設定オプションを適用して、アプリでテキストをレンダリングする方法をカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="08332-148">Although the RichTextBlock stores plain text, you can apply various formatting options to customize how the text is rendered in your app.</span></span> <span data-ttu-id="08332-149">FontFamily、FontSize、FontStyle、Foreground、CharacterSpacing などの標準的なコントロール プロパティを設定して、テキストの外観を変更できます。</span><span class="sxs-lookup"><span data-stu-id="08332-149">You can set standard control properties like FontFamily, FontSize, FontStyle, Foreground, and CharacterSpacing to change the look of the text.</span></span> <span data-ttu-id="08332-150">インライン テキスト要素と Typography 添付プロパティを使ってテキストを書式設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="08332-150">You can also use inline text elements and Typography attached properties to format your text.</span></span> <span data-ttu-id="08332-151">これらのオプションが影響を与えるのは、RichTextBlock がローカルでテキストを表示する方法だけです。したがって、テキストをコピーしてリッチ テキスト コントロールなどに貼り付けても、書式設定は適用されません。</span><span class="sxs-lookup"><span data-stu-id="08332-151">These options affect only how the RichTextBlock displays the text locally, so if you copy and paste the text into a rich text control, for example, no formatting is applied.</span></span>

### <a name="inline-elements"></a><span data-ttu-id="08332-152">インライン要素</span><span class="sxs-lookup"><span data-stu-id="08332-152">Inline elements</span></span>

<span data-ttu-id="08332-153">[Windows.UI.Xaml.Documents](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents) 名前空間には、テキストの書式設定に使うことができるさまざまなインライン テキスト要素が用意されています (Bold、Italic、Run、Span、LineBreak など)。</span><span class="sxs-lookup"><span data-stu-id="08332-153">The [Windows.UI.Xaml.Documents](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents) namespace provides a variety of inline text elements that you can use to format your text, such as Bold, Italic, Run, Span, and LineBreak.</span></span> <span data-ttu-id="08332-154">テキストのセクションに書式設定を適用する典型的な方法では、テキストを Run 要素または Span 要素に配置して、その要素のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="08332-154">A typical way to apply formatting to sections of text is to place the text in a Run or Span element, and then set properties on that element.</span></span>

<span data-ttu-id="08332-155">次の例では、Paragraph の最初の語句が太字、青色、16 ポイントのテキストで表示されます。</span><span class="sxs-lookup"><span data-stu-id="08332-155">Here's a Paragraph with the first phrase shown in bold, blue, 16pt text.</span></span>

```xaml
<Paragraph>
    <Bold><Span Foreground="DarkSlateBlue" FontSize="16">Lorem ipsum dolor sit amet</Span></Bold>
    , consectetur adipiscing elit.
</Paragraph>
```

### <a name="typography"></a><span data-ttu-id="08332-156">文字体裁</span><span class="sxs-lookup"><span data-stu-id="08332-156">Typography</span></span>

<span data-ttu-id="08332-157">[Typography](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Typography) クラスの添付プロパティは、Microsoft OpenType の一連の Typography プロパティへのアクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="08332-157">The attached properties of the [Typography](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Documents.Typography) class provide access to a set of Microsoft OpenType typography properties.</span></span> <span data-ttu-id="08332-158">これらの添付プロパティは、RichTextBlock で設定することも、次の例のように個々のインライン テキスト要素で設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="08332-158">You can set these attached properties either on the RichTextBlock, or on individual inline text elements, as shown here.</span></span>

```xaml
<RichTextBlock Typography.StylisticSet4="True">
    <Paragraph>
        <Span Typography.Capitals="SmallCaps">Lorem ipsum dolor sit amet</Span>
        , consectetur adipiscing elit.
    </Paragraph>
</RichTextBlock>
```

## <a name="recommendations"></a><span data-ttu-id="08332-159">推奨事項</span><span class="sxs-lookup"><span data-stu-id="08332-159">Recommendations</span></span>

<span data-ttu-id="08332-160">文字体裁およびフォントのガイドラインに関するトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="08332-160">See Typography and Guidelines for fonts.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="08332-161">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="08332-161">Get the sample code</span></span>

- <span data-ttu-id="08332-162">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="08332-162">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-articles"></a><span data-ttu-id="08332-163">関連記事</span><span class="sxs-lookup"><span data-stu-id="08332-163">Related articles</span></span>

[<span data-ttu-id="08332-164">テキスト コントロール</span><span class="sxs-lookup"><span data-stu-id="08332-164">Text controls</span></span>](text-controls.md)

<span data-ttu-id="08332-165">**デザイナー向け**</span><span class="sxs-lookup"><span data-stu-id="08332-165">**For designers**</span></span>
- [<span data-ttu-id="08332-166">スペル チェックするためのガイドライン</span><span class="sxs-lookup"><span data-stu-id="08332-166">Guidelines for spell checking</span></span>](text-controls.md)
- <span data-ttu-id="08332-167">[検索の追加](https://docs.microsoft.com/previous-versions/windows/apps/hh465231(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="08332-167">[Adding search](https://docs.microsoft.com/previous-versions/windows/apps/hh465231(v=win.10))</span></span>
- [<span data-ttu-id="08332-168">テキスト入力するためのガイドライン</span><span class="sxs-lookup"><span data-stu-id="08332-168">Guidelines for text input</span></span>](text-controls.md)

<span data-ttu-id="08332-169">**開発者向け (XAML)**</span><span class="sxs-lookup"><span data-stu-id="08332-169">**For developers (XAML)**</span></span>
- [<span data-ttu-id="08332-170">TextBox クラス</span><span class="sxs-lookup"><span data-stu-id="08332-170">TextBox class</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox)
- [<span data-ttu-id="08332-171">Windows.UI.Xaml.Controls PasswordBox クラス</span><span class="sxs-lookup"><span data-stu-id="08332-171">Windows.UI.Xaml.Controls PasswordBox class</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.PasswordBox)


<span data-ttu-id="08332-172">**(その他) 開発者向け**</span><span class="sxs-lookup"><span data-stu-id="08332-172">**For developers (other)**</span></span>
- <span data-ttu-id="08332-173">[String.Length プロパティ](https://msdn.microsoft.com/library/system.string.length(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="08332-173">[String.Length property](https://msdn.microsoft.com/library/system.string.length(v=vs.110).aspx)</span></span>
