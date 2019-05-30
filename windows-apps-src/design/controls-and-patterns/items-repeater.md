---
Description: ItemsRepeater は、軽量のコントロールを生成し、項目のコレクションの表現です。
title: ItemsRepeater
label: ItemsRepeater
template: detail.hbs
ms.date: 02/01/2019
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 93a81501b524826484111419899675fbb99b86fa
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66364756"
---
# <a name="itemsrepeater"></a><span data-ttu-id="fafaf-104">ItemsRepeater</span><span class="sxs-lookup"><span data-stu-id="fafaf-104">ItemsRepeater</span></span>

<span data-ttu-id="fafaf-105">使用して、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)エクスペリエンスをカスタム コレクションを作成するには柔軟なレイアウト システム、カスタム ビュー、および仮想化を使用します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-105">Use an [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) to create custom collection experiences using a flexible layout system, custom views, and virtualization.</span></span>

<span data-ttu-id="fafaf-106">異なり[ListView](/uwp/api/windows.ui.xaml.controls.listview)、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)包括的なエンド ユーザー エクスペリエンスを提供しない既定の UI は持たず、フォーカスや選択した場合、ユーザーの相互作用に関するポリシーが用意されていません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-106">Unlike [ListView](/uwp/api/windows.ui.xaml.controls.listview), [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) does not provide a comprehensive end-user experience – it has no default UI and provides no policy around focus, selection, or user interaction.</span></span> <span data-ttu-id="fafaf-107">代わりに、独自の一意のコレクション ベースのエクスペリエンスとカスタム コントロールの作成に使用できる構成要素になります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-107">Instead, it’s a building block that you can use to create your own unique collection-based experiences and custom controls.</span></span> <span data-ttu-id="fafaf-108">組み込みのポリシーではない、必要なエクスペリエンスを構築するポリシーをアタッチするを使用します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-108">While it has no built-in policy, it enables you to attach policy to build the experience you require.</span></span> <span data-ttu-id="fafaf-109">たとえば、keyboarding ポリシーでは、選択ポリシーなどを使用するレイアウトを定義できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-109">For example, you can define the layout to use, the keyboarding policy, the selection policy, etc.</span></span>

<span data-ttu-id="fafaf-110">考えることができます[ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)よう ListView に完全に制御ではなく、データドリブンのパネルでは、概念的として。</span><span class="sxs-lookup"><span data-stu-id="fafaf-110">You can think of [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) conceptually as a data-driven panel, rather than as a complete control like ListView.</span></span> <span data-ttu-id="fafaf-111">表示するデータ項目のコレクション、各データ項目の UI 要素を生成する項目テンプレート、要素のサイズし、配置方法を決定するレイアウトを指定します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-111">You specify a collection of data items to be displayed, an item template that generates a UI element for each data item, and a layout that determines how the elements are sized and positioned.</span></span> <span data-ttu-id="fafaf-112">次 ItemsRepeater は、データ ソースに基づいて子要素を生成し、レイアウトと項目テンプレートで指定したとおりに表示されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-112">Then, ItemsRepeater produces child elements based on the data source, and displays them as specified by the item template and layout.</span></span> <span data-ttu-id="fafaf-113">表示される項目を同種にする ItemsRepeater データ テンプレート セレクターで指定した条件に基づいてデータ項目を表すコンテンツを読み込むことができますので必要はありません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-113">The items displayed do not need to be homogenous because ItemsRepeater can load content to represent the data items based on criteria you specify in a data template selector.</span></span>

| <span data-ttu-id="fafaf-114">**Windows の UI ライブラリを入手します。**</span><span class="sxs-lookup"><span data-stu-id="fafaf-114">**Get the Windows UI Library**</span></span> |
| - |
| <span data-ttu-id="fafaf-115">このコントロールは、Windows の UI ライブラリを新しいコントロール、および UWP アプリの UI 機能を含む NuGet パッケージの一部として含まれています。</span><span class="sxs-lookup"><span data-stu-id="fafaf-115">This control is included as part of the Windows UI Library, a NuGet package that contains new controls and UI features for UWP apps.</span></span> <span data-ttu-id="fafaf-116">インストール手順を含む詳細については、次を参照してください。、 [Windows UI ライブラリの概要](https://docs.microsoft.com/uwp/toolkits/winui/)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-116">For more info, including installation instructions, see the [Windows UI Library overview](https://docs.microsoft.com/uwp/toolkits/winui/).</span></span> |

> <span data-ttu-id="fafaf-117">**重要な API**:[ItemsRepeater クラス](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)、 [ScrollViewer クラス](/uwp/api/windows.ui.xaml.controls.scrollviewer)</span><span class="sxs-lookup"><span data-stu-id="fafaf-117">**Important APIs**: [ItemsRepeater class](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater), [ScrollViewer class](/uwp/api/windows.ui.xaml.controls.scrollviewer)</span></span>

## <a name="is-this-the-right-control"></a><span data-ttu-id="fafaf-118">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="fafaf-118">Is this the right control?</span></span>

<span data-ttu-id="fafaf-119">使用して、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)データのコレクションに対するカスタムの表示を作成します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-119">Use an [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) to create custom displays for collections of data.</span></span> <span data-ttu-id="fafaf-120">基本的な一連の項目を表示する使用できますが、多くの場合、カスタム コントロールのテンプレートの表示要素として使用する場合があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-120">While it can be used to present a basic set of items, you might often use it as the display element in the template of a custom control.</span></span>

<span data-ttu-id="fafaf-121">リストまたは最小限のカスタマイズにグリッドにデータを表示する、ボックスの制御が必要な場合は、使用を検討して、 [ListView](/uwp/api/windows.ui.xaml.controls.listview)または[GridView](/uwp/api/windows.ui.xaml.controls.gridview)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-121">If you need an out-of-the-box control to display data in a list or grid with minimal customization, consider using a [ListView](/uwp/api/windows.ui.xaml.controls.listview) or [GridView](/uwp/api/windows.ui.xaml.controls.gridview).</span></span>

<span data-ttu-id="fafaf-122">ItemsRepeater の組み込みアイテム コレクションではありません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-122">ItemsRepeater does not have a built-in Items collection.</span></span> <span data-ttu-id="fafaf-123">別のデータ ソースへのバインドではなく、直接、項目のコレクションを提供する必要があるかどうかより高ポリシー エクスペリエンスが必要な可能性があり、使用する必要があります[ListView](/uwp/api/windows.ui.xaml.controls.listview)または[GridView](/uwp/api/windows.ui.xaml.controls.gridview)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-123">If you need to provide an Items collection directly, rather than binding to a separate data source, then you're likely in need of a more high-policy experience and should use [ListView](/uwp/api/windows.ui.xaml.controls.listview) or [GridView](/uwp/api/windows.ui.xaml.controls.gridview).</span></span>

<span data-ttu-id="fafaf-124">[ItemsControl](/uwp/api/windows.ui.xaml.controls.itemscontrol) ItemsRepeater 両方が、エクスペリエンスのカスタマイズ可能なコレクションを有効にする、ItemsRepeater に仮想化の UI レイアウトがサポートしている場合に ItemsControl はありません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-124">[ItemsControl](/uwp/api/windows.ui.xaml.controls.itemscontrol) and ItemsRepeater both enable customizable collection experiences, but ItemsRepeater supports virtualizing UI layouts, while ItemsControl does not.</span></span> <span data-ttu-id="fafaf-125">ItemsControl のではなく ItemsRepeater をかどうかを使用したことをお勧めします。 そのデータから、いくつかの項目を表示またはコントロールを作成するカスタム コレクションのみにします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-125">We recommend using ItemsRepeater instead of ItemsControl, whether its for just presenting a few items from data or building a custom collection control.</span></span>

> [!NOTE]
> <span data-ttu-id="fafaf-126">ItemsControl は、ニーズを満たすし、ItemsRepeater が思うような状況があればのフィードバックを送信してください、 [Windows UI ライブラリ GitHub プロジェクト](https://github.com/Microsoft/microsoft-ui-xaml/issues)お知らせします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-126">If you have a situation where you feel ItemsControl meets your needs and ItemsRepeater doesn't, please leave feedback on the [Windows UI Library GitHub project](https://github.com/Microsoft/microsoft-ui-xaml/issues) and let us know.</span></span>

## <a name="examples"></a><span data-ttu-id="fafaf-127">例</span><span class="sxs-lookup"><span data-stu-id="fafaf-127">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="fafaf-128">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="fafaf-128">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="fafaf-129">ある場合、 <strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong>アプリをインストールするには、ここをクリックして、アプリを開きを参照してください、 <a href="xamlcontrolsgallery:/item/ItemsRepeater">ItemsRepeater</a>アクションにします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-129">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to open the app and see the <a href="xamlcontrolsgallery:/item/ItemsRepeater">ItemsRepeater</a> in action.</span></span></p>
    <ul>
    <li><span data-ttu-id="fafaf-130"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="fafaf-130"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="fafaf-131"><a href="https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlUIBasics">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="fafaf-131"><a href="https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlUIBasics">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="scrolling-with-itemsrepeater"></a><span data-ttu-id="fafaf-132">ItemsRepeater とスクロール</span><span class="sxs-lookup"><span data-stu-id="fafaf-132">Scrolling with ItemsRepeater</span></span>

<span data-ttu-id="fafaf-133">[**ItemsRepeater** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)から派生していない[**コントロール**](/uwp/api/windows.ui.xaml.controls.control)コントロール テンプレートがあるないため、します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-133">[**ItemsRepeater**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) does not derive from [**Control**](/uwp/api/windows.ui.xaml.controls.control), so it doesn't have a control template.</span></span> <span data-ttu-id="fafaf-134">したがって、スクロール、ListView などの組み込みが含まれていないか、コレクションの他のコントロールの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="fafaf-134">Therefore, it doesn't contain any built-in scrolling like a ListView or other collection controls do.</span></span>

<span data-ttu-id="fafaf-135">使用すると、 **ItemsRepeater**でラップしてスクロール機能を提供する必要があります、 [ **ScrollViewer** ](/uwp/api/windows.ui.xaml.controls.scrollviewer)コントロール。</span><span class="sxs-lookup"><span data-stu-id="fafaf-135">When you use an **ItemsRepeater**, you should provide scrolling functionality by wrapping it in a [**ScrollViewer**](/uwp/api/windows.ui.xaml.controls.scrollviewer) control.</span></span>

> [!NOTE]
> <span data-ttu-id="fafaf-136">-Windows の以前のバージョンで、アプリが実行される場合、リリースされた*する前に*Windows 10、バージョンは 1809 - も必要がありますをホストする、 **ScrollViewer**内で、 [ **ItemsRepeaterScrollHost**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeaterscrollhost)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-136">If your app will run on earlier versions of Windows - those released *before* Windows 10, version 1809 - then you also need to host the **ScrollViewer** inside the [**ItemsRepeaterScrollHost**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeaterscrollhost).</span></span> 
> ```xaml
> <muxc:ItemsRepeaterScrollHost>
>     <ScrollViewer>
>         <muxc:ItemsRepeater ... />
>     </ScrollViewer>
> </muxc:ItemsRepeaterScrollHost>
> ```
> <span data-ttu-id="fafaf-137">アプリは 1809 およびそれ以降のバージョンの Windows 10 の最新バージョンでのみ実行する場合、使用する必要はありません、 [ **ItemsRepeaterScrollHost**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeaterscrollhost)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-137">If your app will only run on recent versions of Windows 10, version 1809 and later - then there is no need to use the [**ItemsRepeaterScrollHost**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeaterscrollhost).</span></span>
>
> <span data-ttu-id="fafaf-138">Windows 10、バージョンは 1809、以前**ScrollViewer**を実装しなかったため、 [ **IScrollAnchorProvider** ](/uwp/api/windows.ui.xaml.controls.iscrollanchorprovider)インターフェイス、 **ItemsRepeater**必要があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-138">Prior to Windows 10, version 1809, **ScrollViewer** did not implement the [**IScrollAnchorProvider**](/uwp/api/windows.ui.xaml.controls.iscrollanchorprovider) interface that the **ItemsRepeater** needs.</span></span>  <span data-ttu-id="fafaf-139">**ItemsRepeaterScrollHost**により、 **ItemsRepeater**と連携する**ScrollViewer**で正しく表示される項目の場所を保持するために以前のリリースユーザーが表示されています。</span><span class="sxs-lookup"><span data-stu-id="fafaf-139">The **ItemsRepeaterScrollHost** enables the **ItemsRepeater** to coordinate with **ScrollViewer** on earlier releases to correctly preserve the visible location of items the user is viewing.</span></span>  <span data-ttu-id="fafaf-140">それ以外の場合、項目が移動またはリスト内の項目が変更されたか、アプリのサイズが変更されたときに突然消える表示可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-140">Otherwise, the items might appear to move or disappear suddenly when the items in the list are changed or the app is resized.</span></span>

## <a name="create-an-itemsrepeater"></a><span data-ttu-id="fafaf-141">作成、ItemsRepeater</span><span class="sxs-lookup"><span data-stu-id="fafaf-141">Create an ItemsRepeater</span></span>

<span data-ttu-id="fafaf-142">使用する、 [ **ItemsRepeater**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)を設定して表示するデータを指定する必要がある、 **ItemsSource**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-142">To use an [**ItemsRepeater**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater), you need to give it the data to display by setting the **ItemsSource** property.</span></span> <span data-ttu-id="fafaf-143">設定して項目を表示する方法を指示し、 [ **ItemTemplate** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate)プロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-143">Then, tell it how to display the items by setting the [**ItemTemplate**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate) property.</span></span>

### <a name="itemssource"></a><span data-ttu-id="fafaf-144">ItemsSource</span><span class="sxs-lookup"><span data-stu-id="fafaf-144">ItemsSource</span></span>

<span data-ttu-id="fafaf-145">ビューを設定するには、設定、 [ **ItemsSource** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemssource)プロパティをデータ項目のコレクション。</span><span class="sxs-lookup"><span data-stu-id="fafaf-145">To populate the view, set the [**ItemsSource**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemssource) property to a collection of data items.</span></span> <span data-ttu-id="fafaf-146">ここでは、 **ItemsSource**コレクションのインスタンスに直接コードで設定されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-146">Here, the **ItemsSource** is set in code directly to an instance of a collection.</span></span>

```csharp
ObservableCollection<string> Items = new ObservableCollection<string>();

ItemsRepeater itemsRepeater1 = new ItemsRepeater();
itemsRepeater1.ItemsSource = Items;
```

<span data-ttu-id="fafaf-147">バインドすることも、 **ItemsSource**プロパティを XAML でのコレクション。</span><span class="sxs-lookup"><span data-stu-id="fafaf-147">You can also bind the **ItemsSource** property to a collection in XAML.</span></span> <span data-ttu-id="fafaf-148">データ バインディングについて詳しくは、「[データ バインディングの概要](https://docs.microsoft.com/windows/uwp/data-binding/data-binding-quickstart)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="fafaf-148">For more info about data binding, see [Data binding overview](https://docs.microsoft.com/windows/uwp/data-binding/data-binding-quickstart).</span></span>


```xaml
<ItemsRepeater ItemsSource="{x:Bind Items}"/>
```

### <a name="itemtemplate"></a><span data-ttu-id="fafaf-149">ItemTemplate</span><span class="sxs-lookup"><span data-stu-id="fafaf-149">ItemTemplate</span></span>
<span data-ttu-id="fafaf-150">データ項目を視覚化する方法を指定するには、設定、 [ **ItemTemplate** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate)プロパティを[ **DataTemplate** ](/uwp/api/windows.ui.xaml.datatemplate)または[ **DataTemplateSelector** ](/uwp/api/windows.ui.xaml.controls.datatemplateselector)を定義します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-150">To specify how a data item is visualized, set the [**ItemTemplate**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate) property to a [**DataTemplate**](/uwp/api/windows.ui.xaml.datatemplate) or [**DataTemplateSelector**](/uwp/api/windows.ui.xaml.controls.datatemplateselector) you have defined.</span></span> <span data-ttu-id="fafaf-151">データ テンプレートでは、データを視覚化する方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-151">The data template defines how the data is visualized.</span></span> <span data-ttu-id="fafaf-152">既定では、項目がビューでは、表示される、 **TextBlock**使用データ オブジェクトの文字列表現。</span><span class="sxs-lookup"><span data-stu-id="fafaf-152">By default, the item is displayed in the view with a **TextBlock** the uses the string representation of the data object.</span></span>

<span data-ttu-id="fafaf-153">ただし、通常、個々 の項目の表示に使用する 1 つまたは複数のコントロールの外観とレイアウトを定義するテンプレートを使用して、データのより高度なプレゼンテーションを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-153">However, you typically want to show a more rich presentation of your data by using a template that defines the layout and appearance of one or more controls that you'll use to display an individual item.</span></span> <span data-ttu-id="fafaf-154">テンプレートで使用するコントロールは、データ オブジェクトのプロパティにバインドすることができますも定義されている静的コンテンツをインラインです。</span><span class="sxs-lookup"><span data-stu-id="fafaf-154">The controls you use in the template can be bound to the properties of the data object, or have static content defined inline.</span></span>

#### <a name="datatemplate"></a><span data-ttu-id="fafaf-155">DataTemplate</span><span class="sxs-lookup"><span data-stu-id="fafaf-155">DataTemplate</span></span>
<span data-ttu-id="fafaf-156">この例では、データ オブジェクトは、単純な文字列です。</span><span class="sxs-lookup"><span data-stu-id="fafaf-156">In this example, the data object is a simple string.</span></span> <span data-ttu-id="fafaf-157">**DataTemplate**テキスト、およびスタイルの左側にイメージが含まれています、 **TextBlock**青緑色で文字列を表示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-157">The **DataTemplate** includes an image to the left of the text, and styles the **TextBlock** to display the string in a teal color.</span></span>

> [!NOTE]
> <span data-ttu-id="fafaf-158">使用すると、 [X:bind マークアップ拡張機能](https://docs.microsoft.com/windows/uwp/xaml-platform/x-bind-markup-extension)で、 **DataTemplate**、データ型を指定する必要が (`x:DataType`)、DataTemplate にします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-158">When you use the [x:Bind markup extension](https://docs.microsoft.com/windows/uwp/xaml-platform/x-bind-markup-extension) in a **DataTemplate**, you have to specify the DataType (`x:DataType`) on the DataTemplate.</span></span>

```xaml
<DataTemplate x:DataType="x:String">
    <Grid>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="47"/>
            <ColumnDefinition/>
        </Grid.ColumnDefinitions>
        <Image Source="Assets/placeholder.png" Width="32" Height="32"
               HorizontalAlignment="Left"/>
        <TextBlock Text="{x:Bind}" Foreground="Teal"
                   FontSize="15" Grid.Column="1"/>
    </Grid>
</DataTemplate>
```

<span data-ttu-id="fafaf-159">ここではこれを表示するときの項目は表示**DataTemplate**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-159">Here's how the items would appear when displayed with this **DataTemplate**.</span></span>

![データ テンプレートを使用して表示される項目](images/listview-itemstemplate.png)

<span data-ttu-id="fafaf-161">使用される要素の数、 **DataTemplate**の項目は、多数のアイテムを表示する場合に、パフォーマンス上の大きな影響を与えることができます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-161">The number of elements used in the **DataTemplate** for an item can have a significant impact on performance if your view displays a large number of items.</span></span> <span data-ttu-id="fafaf-162">詳細な情報と使用方法の例の**DataTemplate**一覧で、項目の外観を定義する以下のように[項目コンテナーとテンプレート](item-containers-templates.md)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-162">For more info and examples of how to use **DataTemplate**s to define the look of items in your list, see [Item containers and templates](item-containers-templates.md).</span></span>

> [!TIP]
> <span data-ttu-id="fafaf-163">便宜上、ときに指定できますを静的リソースとして参照されているのではなく、インラインのテンプレートを宣言する、 **DataTemplate**または**DataTemplateSelector** の直接の子として**ItemsRepeater**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-163">For convenience when you want to declare the template inline rather than referenced as a static resource, you can specify the **DataTemplate** or **DataTemplateSelector** as the direct child of the **ItemsRepeater**.</span></span>  <span data-ttu-id="fafaf-164">値として割り当てられる、 **ItemTemplate**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-164">It will be assigned as the value of the **ItemTemplate** property.</span></span> <span data-ttu-id="fafaf-165">たとえば、これは有効です。</span><span class="sxs-lookup"><span data-stu-id="fafaf-165">For example, this is valid:</span></span>
> ```xaml
> <ItemsRepeater ItemsSource="{x:Bind Items}">
>     <DataTemplate>
>         <!-- ... -->
>     </DataTemplate>
> </ItemsRepeater>
> ```

> [!TIP]
> <span data-ttu-id="fafaf-166">異なり**ListView**とコレクションの他のコントロール、 **ItemsRepeater**から要素をラップしません、 **DataTemplate**追加項目コンテナーが含まれる既定のポリシーなど、余白、パディング、ビジュアルの選択、またはビジュアルの状態の上のポインター。</span><span class="sxs-lookup"><span data-stu-id="fafaf-166">Unlike **ListView** and other collection controls, the **ItemsRepeater** doesn't wrap the elements from a **DataTemplate** with an additional item container that includes default policy such as margins, padding, selection visuals, or a pointer over visual state.</span></span> <span data-ttu-id="fafaf-167">代わりに、 **ItemsRepeater**内の定義を表示するだけ、 **DataTemplate**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-167">Instead, **ItemsRepeater** only presents what is defined in the **DataTemplate**.</span></span> <span data-ttu-id="fafaf-168">アイテムとしてリスト ビュー アイテムを同じ見た目をする場合は、含めることができますに明示的に、コンテナーなど**ListViewItem**、データ テンプレート。</span><span class="sxs-lookup"><span data-stu-id="fafaf-168">If you want your items to have the same look as a list view item, you can explicitly include a container, like **ListViewItem**, in your data template.</span></span> <span data-ttu-id="fafaf-169">**ItemsRepeater**が表示されます、 **ListViewItem**ビジュアルがなさない自動的に複数選択チェック ボックスを表示または選択範囲のように、その他の機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-169">**ItemsRepeater** will show the **ListViewItem** visuals, but doesn't automatically make use of other functionality, like selection or showing the multi-select checkbox.</span></span>
>
> <span data-ttu-id="fafaf-170">同様に、実際のコントロールのコレクションの場合は、データの収集など**ボタン**(`List<Button>`) を配置することができます、 **ContentPresenter**で、 **DataTemplate**にコントロールを表示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-170">Similarly, if your data collection is a collection of actual controls, like **Button** (`List<Button>`), you can put a **ContentPresenter** in your **DataTemplate** to display the control.</span></span>

#### <a name="datatemplateselector"></a><span data-ttu-id="fafaf-171">DataTemplateSelector</span><span class="sxs-lookup"><span data-stu-id="fafaf-171">DataTemplateSelector</span></span>

<span data-ttu-id="fafaf-172">ビューに表示する項目は、同じ型である必要はありません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-172">The items you display in your view do not need to be of the same type.</span></span> <span data-ttu-id="fafaf-173">行うことができます、 [ **ItemTemplate** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate)プロパティを[ **DataTemplateSelector** ](/uwp/api/windows.ui.xaml.controls.datatemplateselector)を異なる選択**DataTemplate**s は、指定した条件に基づいています。</span><span class="sxs-lookup"><span data-stu-id="fafaf-173">You can provide the [**ItemTemplate**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate) property with a [**DataTemplateSelector**](/uwp/api/windows.ui.xaml.controls.datatemplateselector) to select different **DataTemplate**s based on criteria you specify.</span></span>

<span data-ttu-id="fafaf-174">この例では、 **DataTemplateSelector**が定義されている 2 つの異なる間を決定する**DataTemplate**大と小の項目を表す秒。</span><span class="sxs-lookup"><span data-stu-id="fafaf-174">This example assumes a **DataTemplateSelector** has been defined that decides between two different **DataTemplate**s to represent a Large and Small item.</span></span>

```xaml
<ItemsRepeater ...>
    <ItemsRepeater.ItemTemplate>
        <local:VariableSizeTemplateSelector Large="{StaticResource LargeItemTemplate}" 
                                            Small="{StaticResource SmallItemTemplate}"/>
    </ItemsRepeater.ItemTemplate>
</ItemsRepeater>
```

<span data-ttu-id="fafaf-175">定義するときに、 **DataTemplateSelector**で使用する**ItemsRepeater**のみのオーバーライドを実装する必要があります、 [ **SelectTemplateCore(Object)** ](/uwp/api/windows.ui.xaml.controls.datatemplateselector.selecttemplatecore#Windows_UI_Xaml_Controls_DataTemplateSelector_SelectTemplateCore_System_Object_)メソッド。</span><span class="sxs-lookup"><span data-stu-id="fafaf-175">When defining a **DataTemplateSelector** to use with **ItemsRepeater** you only need to implement an override for the [**SelectTemplateCore(Object)**](/uwp/api/windows.ui.xaml.controls.datatemplateselector.selecttemplatecore#Windows_UI_Xaml_Controls_DataTemplateSelector_SelectTemplateCore_System_Object_) method.</span></span> <span data-ttu-id="fafaf-176">詳細と例については、次を参照してください。 [ **DataTemplateSelector**](/uwp/api/windows.ui.xaml.controls.datatemplateselector)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-176">For more info and examples, see [**DataTemplateSelector**](/uwp/api/windows.ui.xaml.controls.datatemplateselector).</span></span>

> [!NOTE]
> <span data-ttu-id="fafaf-177">代わりに**DataTemplate**独自に実装するためにはより高度なシナリオで要素を作成する方法を管理する[ **Windows.UI.Xaml.Controls.IElementFactory** ](/uwp/api/windows.ui.xaml.controls.ielementfactory)として使用する、 **ItemTemplate**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-177">An alternative to **DataTemplate**s to manage how elements are created in more advanced scenarios is to implement your own [**Windows.UI.Xaml.Controls.IElementFactory**](/uwp/api/windows.ui.xaml.controls.ielementfactory) to use as the **ItemTemplate**.</span></span>  <span data-ttu-id="fafaf-178">要求されたときにコンテンツを生成することができます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-178">It will be responsible for generating content when requested.</span></span>

## <a name="configure-the-data-source"></a><span data-ttu-id="fafaf-179">データ ソースを構成します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-179">Configure the data source</span></span>

<span data-ttu-id="fafaf-180">使用して、 [ItemsSource](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemssource)プロパティを使用して項目のコンテンツを生成するコレクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-180">Use the [ItemsSource](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemssource) property to specify the collection to use to generate the content of items.</span></span> <span data-ttu-id="fafaf-181">ItemsSource を設定するには任意の型を実装する**IEnumerable**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-181">You can set the ItemsSource to any type that implements **IEnumerable**.</span></span> <span data-ttu-id="fafaf-182">データ ソースによって実装される追加のコレクション インターフェイスは、データと対話する ItemsRepeater に可能な機能を決定します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-182">Additional collection interfaces implemented by your data source determine what functionality is available to the ItemsRepeater to interact with your data.</span></span>

<span data-ttu-id="fafaf-183">この一覧は、使用可能なインターフェイスとそれぞれの使用を検討する場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-183">This list shows available interfaces and when to consider using each one.</span></span>

- <span data-ttu-id="fafaf-184">[IEnumerable](/dotnet/api/system.collections.generic.ienumerable-1)(.NET)/ [IIterable](/uwp/api/windows.foundation.collections.iiterable_t_)</span><span class="sxs-lookup"><span data-stu-id="fafaf-184">[IEnumerable](/dotnet/api/system.collections.generic.ienumerable-1)(.NET) / [IIterable](/uwp/api/windows.foundation.collections.iiterable_t_)</span></span>

  - <span data-ttu-id="fafaf-185">小規模の静的なデータ セットを使用できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-185">Can be used for small, static data sets.</span></span>

    <span data-ttu-id="fafaf-186">データ ソースには、少なくとも、IEnumerable を実装する必要があります/IIterable インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="fafaf-186">At a minimum, the data source must implement the IEnumerable / IIterable interface.</span></span> <span data-ttu-id="fafaf-187">これはすべてサポートされている場合、コントロールはインデックス値を使用して項目にアクセスするために使用できるコピーを作成するとすべてを反復処理します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-187">If this is all that's supported then the control will iterate through everything once to create a copy that it can use to access items via an index value.</span></span>

- <span data-ttu-id="fafaf-188">[IReadonlyList](/dotnet/api/system.collections.generic.ireadonlylist-1)(.NET)/ [IVectorView](/uwp/api/windows.foundation.collections.ivectorview_t_)</span><span class="sxs-lookup"><span data-stu-id="fafaf-188">[IReadonlyList](/dotnet/api/system.collections.generic.ireadonlylist-1)(.NET) / [IVectorView](/uwp/api/windows.foundation.collections.ivectorview_t_)</span></span>

  - <span data-ttu-id="fafaf-189">静的で読み取り専用のデータ セットを使用できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-189">Can be used for static, read-only data sets.</span></span>

    <span data-ttu-id="fafaf-190">コントロールの項目にアクセスすることにより、インデックスを内部の冗長コピーを回避できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-190">Enables the control to access items by index and avoids the redundant internal copy.</span></span>

- <span data-ttu-id="fafaf-191">[IList](/dotnet/api/system.collections.generic.ilist-1)(.NET)/ [IVector](/uwp/api/windows.foundation.collections.ivector_t_)</span><span class="sxs-lookup"><span data-stu-id="fafaf-191">[IList](/dotnet/api/system.collections.generic.ilist-1)(.NET) / [IVector](/uwp/api/windows.foundation.collections.ivector_t_)</span></span>

  - <span data-ttu-id="fafaf-192">静的なデータ セットを使用できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-192">Can be used for static data sets.</span></span>

    <span data-ttu-id="fafaf-193">コントロールの項目にアクセスすることにより、インデックスを内部の冗長コピーを回避できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-193">Enables the control to access items by index and avoids the redundant internal copy.</span></span>

    <span data-ttu-id="fafaf-194">**警告**:一覧およびベクトルを実装しなくても変更[INotifyCollectionChanged](/dotnet/api/system.collections.specialized.inotifycollectionchanged) UI に反映されません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-194">**Warning**: Changes to the list/vector without implementing [INotifyCollectionChanged](/dotnet/api/system.collections.specialized.inotifycollectionchanged) won't be reflected in the UI.</span></span>

- <span data-ttu-id="fafaf-195">[INotifyCollectionChanged](/dotnet/api/system.collections.specialized.inotifycollectionchanged)(.NET)</span><span class="sxs-lookup"><span data-stu-id="fafaf-195">[INotifyCollectionChanged](/dotnet/api/system.collections.specialized.inotifycollectionchanged)(.NET)</span></span>

  - <span data-ttu-id="fafaf-196">変更通知をサポートすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-196">Recommended to support change notification.</span></span>

    <span data-ttu-id="fafaf-197">観察し、データ ソースでの変更に反応し、UI の変更を反映させるコントロールを有効にします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-197">Enables the control to observe and react to changes in the data source and reflect those changes in the UI.</span></span>

- [<span data-ttu-id="fafaf-198">IObservableVector</span><span class="sxs-lookup"><span data-stu-id="fafaf-198">IObservableVector</span></span>](/uwp/api/windows.foundation.collections.iobservablevector_t_)

  - <span data-ttu-id="fafaf-199">変更通知をサポートしています</span><span class="sxs-lookup"><span data-stu-id="fafaf-199">Supports change notification</span></span>

    <span data-ttu-id="fafaf-200">ように、 **INotifyCollectionChanged**インターフェイス、これにより、コントロールを確認し、データ ソースでの変更に対応します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-200">Like the **INotifyCollectionChanged** interface, this enables the control to observe and react to changes in the data source.</span></span>

    <span data-ttu-id="fafaf-201">**警告**:Windows.Foundation.IObservableVector\<T > '移動' 操作をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-201">**Warning**: The Windows.Foundation.IObservableVector\<T> doesn’t support a 'Move' action.</span></span> <span data-ttu-id="fafaf-202">これには、項目の UI のビジュアルの状態が失われる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-202">This can cause the UI for an item to lose its visual state.</span></span>  <span data-ttu-id="fafaf-203">たとえば、現在選択されている、または 'Remove' を 'Add' 後に、移動を実現する場所にフォーカスがある項目を使用して、フォーカスを失って、選択できなくなります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-203">For example, an item that is currently selected and/or has focus where the move is achieved by a ‘Remove’ followed by an ‘Add’ will lose focus and no longer be selected.</span></span>

    <span data-ttu-id="fafaf-204">Platform.Collections.Vector\<T > IObservableVector を使用して\<T > とはこの同じ制限があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-204">The Platform.Collections.Vector\<T> uses IObservableVector\<T> and has this same limitation.</span></span> <span data-ttu-id="fafaf-205">サポート '移動' アクションが必要です。 使用している場合、 **INotifyCollectionChanged**インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="fafaf-205">If support for a 'Move' action is required then use the **INotifyCollectionChanged** interface.</span></span>  <span data-ttu-id="fafaf-206">.NET ObservableCollection\<T > クラスで使用**INotifyCollectionChanged**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-206">The .NET ObservableCollection\<T> class uses **INotifyCollectionChanged**.</span></span>

- [<span data-ttu-id="fafaf-207">IKeyIndexMapping</span><span class="sxs-lookup"><span data-stu-id="fafaf-207">IKeyIndexMapping</span></span>](/uwp/api/microsoft.ui.xaml.controls.ikeyindexmapping)

  - <span data-ttu-id="fafaf-208">ときに一意識別子は各項目を関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-208">When a unique identifier can be associated with each item.</span></span>  <span data-ttu-id="fafaf-209">コレクションの変更操作として 'Reset' を使用する場合にお勧めします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-209">Recommended when using 'Reset' as the collection change action.</span></span>

    <span data-ttu-id="fafaf-210">ハード リセット' のアクションの一部として受信した後、既存の UI を非常に効率的に回復するコントロールできるように、 **INotifyCollectionChanged**または**IObservableVector**イベント。</span><span class="sxs-lookup"><span data-stu-id="fafaf-210">Enables the control to very efficiently recover the existing UI after receiving a hard 'Reset' action as part of an **INotifyCollectionChanged** or **IObservableVector** event.</span></span> <span data-ttu-id="fafaf-211">リセットを受信した後、コントロールは、既に作成してその要素に現在のデータを関連付ける、指定された一意の ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-211">After receiving a reset the control will use the provided unique ID to associate the current data with elements it had already created.</span></span> <span data-ttu-id="fafaf-212">インデックスのマッピングにキーがないコントロールは、データの UI の作成の最初からやり直す必要があると仮定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-212">Without the key to index mapping the control would have to assume it needs to start over from scratch in creating UI for the data.</span></span>

<span data-ttu-id="fafaf-213">IKeyIndexMapping、以外に、上に示したインターフェイスは、ListView および GridView のように ItemsRepeater で同じ動作を提供します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-213">The interfaces listed above, other than IKeyIndexMapping, provide the same behavior in ItemsRepeater as they do in ListView and GridView.</span></span>


<span data-ttu-id="fafaf-214">次のインターフェイス、ItemsSource に ListView と GridView コントロールで特別な機能を有効にする現在効果はありません、ItemsRepeater で。</span><span class="sxs-lookup"><span data-stu-id="fafaf-214">The following interfaces on an ItemsSource enable special functionality in the ListView and GridView controls, but currently have no effect on an ItemsRepeater:</span></span>

- [<span data-ttu-id="fafaf-215">ISupportIncrementalLoading</span><span class="sxs-lookup"><span data-stu-id="fafaf-215">ISupportIncrementalLoading</span></span>](/uwp/api/windows.ui.xaml.data.isupportincrementalloading)
- [<span data-ttu-id="fafaf-216">IItemsRangeInfo</span><span class="sxs-lookup"><span data-stu-id="fafaf-216">IItemsRangeInfo</span></span>](/uwp/api/windows.ui.xaml.data.iitemsrangeinfo)
- [<span data-ttu-id="fafaf-217">ISelectionInfo</span><span class="sxs-lookup"><span data-stu-id="fafaf-217">ISelectionInfo</span></span>](/uwp/api/windows.ui.xaml.data.iselectioninfo)

> [!TIP]
> <span data-ttu-id="fafaf-218">ご意見をお寄せください</span><span class="sxs-lookup"><span data-stu-id="fafaf-218">We want your feedback!</span></span> <span data-ttu-id="fafaf-219">皆さんに、 [Windows UI ライブラリ GitHub プロジェクト](https://github.com/Microsoft/microsoft-ui-xaml/issues)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-219">Let us know what you think on the [Windows UI Library GitHub project](https://github.com/Microsoft/microsoft-ui-xaml/issues).</span></span> <span data-ttu-id="fafaf-220">など、自分の考えを既存の提案の追加を検討する[#374](https://github.com/Microsoft/microsoft-ui-xaml/issues/374):ItemsRepeater の増分読み込みのサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-220">Consider adding your thoughts on existing proposals such as [#374](https://github.com/Microsoft/microsoft-ui-xaml/issues/374): Add incremental loading support for ItemsRepeater.</span></span>

<span data-ttu-id="fafaf-221">ユーザーがスクロール アップまたはスケール ダウン、データを増分読み込みする他の方法では ScrollViewer のビューポートの位置を観察し、ビューポートの範囲に近づくとデータを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-221">An alternative approach to incrementally load your data as the user scrolls up or down is to observe the position of the ScrollViewer's viewport and load more data as the viewport approaches the extent.</span></span>

```xaml
<ScrollViewer ViewChanged="ScrollViewer_ViewChanged">
    <ItemsRepeater ItemsSource="{x:Bind MyItemsSource}" .../>
</ScrollViewer>
```

```csharp
private async void ScrollViewer_ViewChanged(object sender, ScrollViewerViewChangedEventArgs e)
{
    if (!e.IsIntermediate)
    {
        var scroller = (ScrollViewer)sender;
        var distanceToEnd = scroller.ExtentHeight - (scroller.VerticalOffset + scroller.ViewportHeight);

        // trigger if within 2 viewports of the end
        if (distanceToEnd <= 2.0 * scroller.ViewportHeight
                && MyItemsSource.HasMore && !itemsSource.Busy)
        {
            // show an indeterminate progress UI
            myLoadingIndicator.Visibility = Visibility.Visible;

            await MyItemsSource.LoadMoreItemsAsync(/*DataFetchSize*/);

            loadingIndicator.Visibility = Visibility.Collapsed;
        }
    }
}
```

## <a name="change-the-layout-of-items"></a><span data-ttu-id="fafaf-222">項目のレイアウト変更</span><span class="sxs-lookup"><span data-stu-id="fafaf-222">Change the layout of items</span></span>

<span data-ttu-id="fafaf-223">項目が表示されている、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)配置されるか、[レイアウト](/uwp/api/microsoft.ui.xaml.controls.layout)サイズとその子要素の配置を管理するオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="fafaf-223">Items shown by the [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) are arranged by a [Layout](/uwp/api/microsoft.ui.xaml.controls.layout) object that manages the sizing and positioning of its child elements.</span></span> <span data-ttu-id="fafaf-224">ItemsRepeater を併用すると、レイアウト オブジェクトには、UI の仮想化ができるようにします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-224">When used with an ItemsRepeater, the Layout object enables UI virtualization.</span></span> <span data-ttu-id="fafaf-225">用意されたレイアウトは[StackLayout](/uwp/api/microsoft.ui.xaml.controls.stacklayout)と[UniformGridLayout](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-225">The layouts provided are [StackLayout](/uwp/api/microsoft.ui.xaml.controls.stacklayout) and [UniformGridLayout](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout).</span></span> <span data-ttu-id="fafaf-226">既定では、ItemsRepeater は縦方向の StackLayout を使用します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-226">By default, ItemsRepeater uses a StackLayout with vertical orientation.</span></span>

### <a name="stacklayout"></a><span data-ttu-id="fafaf-227">StackLayout</span><span class="sxs-lookup"><span data-stu-id="fafaf-227">StackLayout</span></span>

<span data-ttu-id="fafaf-228">[StackLayout](/uwp/api/microsoft.ui.xaml.controls.stacklayout)要素を水平方向または垂直方向の向きを設定する 1 行に整列します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-228">[StackLayout](/uwp/api/microsoft.ui.xaml.controls.stacklayout) arranges elements into a single line that you can orient horizontally or vertically.</span></span>

<span data-ttu-id="fafaf-229">設定することができます、[間隔](/en-us/uwp/api/microsoft.ui.xaml.controls.stacklayout.spacing)項目間のスペースの量を調整するプロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-229">You can set the [Spacing](/en-us/uwp/api/microsoft.ui.xaml.controls.stacklayout.spacing) property to adjust the amount of space between items.</span></span> <span data-ttu-id="fafaf-230">間隔がレイアウトの方向に適用される[向き](/uwp/api/microsoft.ui.xaml.controls.stacklayout.orientation)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-230">Spacing is applied in the direction of the layout's [Orientation](/uwp/api/microsoft.ui.xaml.controls.stacklayout.orientation).</span></span>

![スタック レイアウト間隔](images/stack-layout.png)

<span data-ttu-id="fafaf-232">この例では、水平方向と 8 ピクセルの間隔、StackLayout を ItemsRepeater.Layout プロパティを設定する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-232">This example shows how to set the ItemsRepeater.Layout property to a StackLayout with horizontal orientation and spacing of 8 pixels.</span></span>

```xaml
<!-- xmlns:muxc="using:Microsoft.UI.Xaml.Controls" -->
<muxc:ItemsRepeater ItemsSource="{x:Bind Items}" ItemTemplate="{StaticResource MyTemplate}">
    <muxc:ItemsRepeater.Layout>
        <muxc:StackLayout Orientation="Horizontal" Spacing="8"/>
    </muxc:ItemsRepeater.Layout>
</muxc:ItemsRepeater>
```

### <a name="uniformgridlayout"></a><span data-ttu-id="fafaf-233">UniformGridLayout</span><span class="sxs-lookup"><span data-stu-id="fafaf-233">UniformGridLayout</span></span>

<span data-ttu-id="fafaf-234">[UniformGridLayout](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout)折り返しレイアウトで要素を順番に配置します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-234">The [UniformGridLayout](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout) positions elements sequentially in a wrapping layout.</span></span> <span data-ttu-id="fafaf-235">項目が左から右から順にレイアウトときに、[向き](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.orientation)は**水平**、一番上から下へ、印刷の向きがレイアウトと**垂直**。</span><span class="sxs-lookup"><span data-stu-id="fafaf-235">Items are layed out in order from left-to-right when the [Orientation](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.orientation) is **Horizontal**, and layed out top-to-bottom when the Orientation is **Vertical**.</span></span> <span data-ttu-id="fafaf-236">すべての項目を同じサイズです。</span><span class="sxs-lookup"><span data-stu-id="fafaf-236">Every item is sized equally.</span></span>

![統一されたグリッド レイアウトの間隔](images/uniform-grid-layout.png)

<span data-ttu-id="fafaf-238">各行の水平レイアウト内の項目の数は、最小のアイテムの幅の影響を受けます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-238">The number of items in each row of a horizontal layout is influenced by the minimum item width.</span></span> <span data-ttu-id="fafaf-239">項目の最小の高さ、縦方向のレイアウトの各列内の項目の数が反映されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-239">The number of items in each column of a vertical layout is influenced by the minimum item height.</span></span>

- <span data-ttu-id="fafaf-240">明示的に設定して使用する最小サイズを指定することができます、 [MinItemHeight](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.minitemheight)と[MinItemWidth](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.minitemwidth)プロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-240">You can explicitly provide a minimum size to use by setting the [MinItemHeight](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.minitemheight) and [MinItemWidth](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.minitemwidth) properties.</span></span>
- <span data-ttu-id="fafaf-241">最小サイズを指定しない場合、最初の項目の測定のサイズは、項目ごとの最小サイズと見なされます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-241">If you don't specify a minimum size, the measured size of the first item is considered the minimum size per item.</span></span>

<span data-ttu-id="fafaf-242">行と列の間に設定して、レイアウトの最小間隔を設定することも、 [MinColumnSpacing](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.mincolumnspacing)と[MinRowSpacing](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.minrowspacing)プロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-242">You can also set minimum spacing for the layout to include between rows and columns by setting the [MinColumnSpacing](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.mincolumnspacing) and [MinRowSpacing](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.minrowspacing) properties.</span></span>

![統一されたグリッドのサイズ変更との間隔](images/uniform-grid-sizing-spacing.png)

<span data-ttu-id="fafaf-244">数の行または列内の項目が特定された場合は、項目の最小サイズとの間隔に基づき、後に未使用領域の行または列の最後の項目の後に残っています (図のように、以前) である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-244">After the number if items in a row or column has been determined based on the item's minimum size and spacing, there might be unused space left after the last item in the row or column (as illustrated in the previous image).</span></span> <span data-ttu-id="fafaf-245">余分なスペースが無視されますになっていることを使用して、各項目のサイズを増やすまたは項目間の余分なスペースを作成するために使用するかどうかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-245">You can specify whether any extra space is ignored, used to increase the size of each item, or used to create extra space between the items.</span></span> <span data-ttu-id="fafaf-246">これによって制御されますが、 [ItemsStretch](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsstretch)と[ItemsJustification](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsjustification)プロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-246">This is controlled by the [ItemsStretch](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsstretch) and [ItemsJustification](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsjustification) properties.</span></span>

<span data-ttu-id="fafaf-247">設定することができます、 [ItemsStretch](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsstretch)未使用領域を埋める、アイテムのサイズを増やす方法を指定するプロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-247">You can set the [ItemsStretch](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsstretch) property to specify how the item size is increased to fill the unused space.</span></span>

<span data-ttu-id="fafaf-248">この一覧は、使用可能な値を示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-248">This list shows the available values.</span></span> <span data-ttu-id="fafaf-249">定義には、既定値が前提としています**向き**の**水平**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-249">The definitions assume the default **Orientation** of **Horizontal**.</span></span>

- <span data-ttu-id="fafaf-250">**[なし]** :余分なスペースは、行の終わりに未使用のまま。</span><span class="sxs-lookup"><span data-stu-id="fafaf-250">**None**: Extra space is left unused at the end of the row.</span></span> <span data-ttu-id="fafaf-251">これが既定値です。</span><span class="sxs-lookup"><span data-stu-id="fafaf-251">This is the default.</span></span>
- <span data-ttu-id="fafaf-252">**入力**:項目には、使用可能な領域 (垂直方向の場合は高さ) を使用する追加の幅が与えられます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-252">**Fill**: The items are given extra width to use up the available space (height if vertical).</span></span>
- <span data-ttu-id="fafaf-253">**Uniform**:項目が、使用可能な領域を使用する追加の幅を指定して、縦横比を維持するために余分な高さを指定 (高さと幅が切り替わった場合、垂直方向)。</span><span class="sxs-lookup"><span data-stu-id="fafaf-253">**Uniform**: The items are given extra width to use up the available space, and given extra height in order to maintain aspect ratio (height and width are switched if vertical).</span></span>

<span data-ttu-id="fafaf-254">このイメージの効果を示しています、 **ItemsStretch**水平レイアウト内の値。</span><span class="sxs-lookup"><span data-stu-id="fafaf-254">This image shows the effect of the **ItemsStretch** values in a horizontal layout.</span></span>

![統一されたグリッド項目の拡張](images/uniform-grid-item-stretch.png)

<span data-ttu-id="fafaf-256">ときに**ItemsStretch**は**None**、設定することができます、 [ItemsJustification](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsjustification)アイテムを揃えるための領域の使用方法を指定するプロパティ。</span><span class="sxs-lookup"><span data-stu-id="fafaf-256">When **ItemsStretch** is **None**, you can set the [ItemsJustification](/uwp/api/microsoft.ui.xaml.controls.uniformgridlayout.itemsjustification) property to specify how extra space is used to align the items.</span></span>

<span data-ttu-id="fafaf-257">この一覧は、使用可能な値を示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-257">This list shows the available values.</span></span> <span data-ttu-id="fafaf-258">定義には、既定値が前提としています**向き**の**水平**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-258">The definitions assume the default **Orientation** of **Horizontal**.</span></span>

- <span data-ttu-id="fafaf-259">**開始**:項目は、行の先頭に配置されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-259">**Start**: Items are aligned with the start of the row.</span></span> <span data-ttu-id="fafaf-260">余分なスペースは、行の終わりに未使用のまま。</span><span class="sxs-lookup"><span data-stu-id="fafaf-260">Extra space is left unused at the end of the row.</span></span> <span data-ttu-id="fafaf-261">これが既定値です。</span><span class="sxs-lookup"><span data-stu-id="fafaf-261">This is the default.</span></span>
- <span data-ttu-id="fafaf-262">**Center**:項目は、行の中央に揃えて配置されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-262">**Center**: Items are aligned in the center of the row.</span></span> <span data-ttu-id="fafaf-263">余分なスペースは、先頭と行の末尾に均等に分割されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-263">Extra space is divided evenly at the start and end of the row.</span></span>
- <span data-ttu-id="fafaf-264">**終了**:項目は、行の末尾に揃えて配置されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-264">**End**: Items are aligned with the end of the row.</span></span> <span data-ttu-id="fafaf-265">余分なスペースは、行の先頭に使用されていないまま。</span><span class="sxs-lookup"><span data-stu-id="fafaf-265">Extra space is left unused at the start of the row.</span></span>
- <span data-ttu-id="fafaf-266">**SpaceAround**:項目が均等に分散されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-266">**SpaceAround**: Items are distributed evenly.</span></span> <span data-ttu-id="fafaf-267">等しいメモリ領域のサイズは前に、と後の各項目に追加されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-267">An equal amount of space is added before and after each item.</span></span>
- <span data-ttu-id="fafaf-268">**スペース**:項目が均等に分散されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-268">**SpaceBetween**: Items are distributed evenly.</span></span> <span data-ttu-id="fafaf-269">各項目の間と同じメモリ領域のサイズが追加されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-269">An equal amount of space is added between each item.</span></span> <span data-ttu-id="fafaf-270">先頭と行の末尾にスペースは追加されません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-270">No space is added at the start and end of the row.</span></span>
- <span data-ttu-id="fafaf-271">**SpaceEvenly**:項目は、両方の各項目の間、および開始、行の末尾にある空き領域量が等しいを均等に分散されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-271">**SpaceEvenly**: Items are distributed evenly with an equal amount of space both between each item and at the start and end of the row.</span></span>

<span data-ttu-id="fafaf-272">このイメージの効果を示しています、 **ItemsStretch** (行ではなく列に適用) 垂直レイアウト内の値。</span><span class="sxs-lookup"><span data-stu-id="fafaf-272">This image shows the effect of the **ItemsStretch** values in a vertical layout (applied to columns instead of rows).</span></span>

![統一されたグリッド項目の位置揃え](images/uniform-grid-item-justification.png)

> [!TIP]
> <span data-ttu-id="fafaf-274">**ItemsStretch**プロパティに影響、_メジャー_レイアウトのパスします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-274">The **ItemsStretch** property affects the _measure_ pass of layout.</span></span> <span data-ttu-id="fafaf-275">**ItemsJustification**プロパティに影響、_配置_レイアウトのパスします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-275">The **ItemsJustification** property affects the _arrange_ pass of layout.</span></span>

<span data-ttu-id="fafaf-276">この例では、設定、 **ItemsRepeater.Layout**プロパティを**UniformGridLayout**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-276">This example shows how to set the **ItemsRepeater.Layout** property to a **UniformGridLayout**.</span></span>

```xaml
<!-- xmlns:muxc="using:Microsoft.UI.Xaml.Controls" -->
<muxc:ItemsRepeater ItemsSource="{x:Bind Items}"
                    ItemTemplate="{StaticResource MyTemplate}">
    <muxc:ItemsRepeater.Layout>
        <muxc:UniformGridLayout MinItemWidth="200"
                                MinColumnSpacing="28"
                                ItemsJustification="SpaceAround"/>
    </muxc:ItemsRepeater.Layout>
</muxc:ItemsRepeater>
```

## <a name="lifecycle-events"></a><span data-ttu-id="fafaf-277">ライフ サイクル イベント</span><span class="sxs-lookup"><span data-stu-id="fafaf-277">Lifecycle events</span></span>

<span data-ttu-id="fafaf-278">内の項目をホストする場合、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)など、一部のコンテンツの非同期ダウンロードを開始すると、要素に関連付ける選択を追跡するためのメカニズム、項目が表示または表示を停止するときに、何らかのアクションを実行する必要がありますか一部のバック グラウンド タスクを停止します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-278">When you host items in an [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater), you might need to take some action when an item is shown or stops being shown, such as start an asynchronous download of some content, associate the element with a mechanism to track selection, or stop some background task.</span></span>

<span data-ttu-id="fafaf-279">仮想化コントロールのため、これが再利用されるときに、要素をライブ ビジュアル ツリーから削除されないことがロード/アンロード イベントに依存できません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-279">In a virtualizing control, you cannot rely on Loaded/Unloaded events because the element might not be removed from the live visual tree when it's recycled.</span></span> <span data-ttu-id="fafaf-280">代わりに、その他のイベントは、要素のライフ サイクル管理に提供されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-280">Instead, other events are provided to manage the lifecycle of elements.</span></span> <span data-ttu-id="fafaf-281">この図はの ItemsRepeater でと、関連するイベントが発生したときに、要素のライフ サイクルを示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-281">This diagram shows the lifecycle of an element in an ItemsRepeater, and when the related events are raised.</span></span>

![ライフ サイクル イベントのダイアグラム](images/items-repeater-lifecycle.png)

- <span data-ttu-id="fafaf-283">[**ElementPrepared** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.elementprepared)要素が使用できるように行われるたびに発生します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-283">[**ElementPrepared**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.elementprepared) occurs each time an element is made ready for use.</span></span> <span data-ttu-id="fafaf-284">これは、要素が既に存在し、リサイクルのキューから再使用されているだけでなく、新しく作成された要素に対して発生します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-284">This occurs for both a newly created element as well as an element that already exists and is being re-used from the recycle queue.</span></span>
- <span data-ttu-id="fafaf-285">[**ElementClearing** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.elementclearing)たびに、要素の範囲外になる場合など、リサイクルのキューに送信されたアイテムの実現に発生します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-285">[**ElementClearing**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.elementclearing) occurs immediately each time an element has been sent to the recycle queue, such as when it falls outside the range of realized items.</span></span>
- <span data-ttu-id="fafaf-286">[**ElementIndexChanged** ](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.elementindexchanged
) UIElement を表す項目のインデックスが変更されていることに気付きましたそれぞれに対して行われます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-286">[**ElementIndexChanged**](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.elementindexchanged
) occurs for each realized UIElement where the index for the item it represents has changed.</span></span> <span data-ttu-id="fafaf-287">たとえば、別のアイテムが追加またはデータ ソースの削除、順序の後に続く項目のインデックスは、このイベントを受信します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-287">For example, when another item is added or removed in the data source, the index for items that come after in the ordering receive this event.</span></span>

<span data-ttu-id="fafaf-288">この例では、これらのイベントを使用できます ItemsRepeater を使用して項目を表示するカスタム コントロールで項目の選択を追跡するカスタム選択サービスにアタッチする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-288">This example shows how you could use these events to attach a custom selection service to track item selection in a custom control that uses ItemsRepeater to display items.</span></span>

```xaml
<!-- xmlns:muxc="using:Microsoft.UI.Xaml.Controls" -->
<UserControl ...>
    ...
    <ScrollViewer>
        <muxc:ItemsRepeater ItemsSource="{x:Bind Items}"
                            ItemTemplate="{StaticResource MyTemplate}"
                            ElementPrepared="OnElementPrepared"
                            ElementIndexChanged="OnElementIndexChanged"
                            ElementClearing="OnElementClearing">
        </muxc:ItemsRepeater>
    </ScrollViewer>
    ...
</UserControl>
```

```csharp
interface ISelectable
{
    int SelectionIndex { get; set; }
    void UnregisterSelectionModel(SelectionModel selectionModel);
    void RegisterSelectionModel(SelectionModel selectionModel);
}

private void OnElementPrepared(ItemsRepeater sender, ElementPreparedEventArgs args)
{
    var selectable = args.Element as ISelectable;
    if (selectable != null)
    {
        // Wire up this item to recognize a 'select' and listen for programmatic
        // changes to the selection model to know when to update its visual state.
        selectable.SelectionIndex = args.Index;
        selectable.RegisterSelectionModel(this.SelectionModel);
    }
}

private void OnElementIndexChanged(ItemsRepeater sender, ElementIndexChangedEventArgs args)
{
    var selectable = args.Element as ISelectable;
    if (selectable != null)
    {
        // Sync the ID we use to notify the selection model when the item
        // we represent has changed location in the data source.
        selectable.SelectionIndex = args.NewIndex;
    }
}

private void OnElementClearing(ItemsRepeater sender, ElementClearingEventArgs args)
{
    var selectable = args.Element as ISelectable;
    if (selectable != null)
    {
        // Disconnect handlers to recognize a 'select' and stop
        // listening for programmatic changes to the selection model.
        selectable.UnregisterSelectionModel(this.SelectionModel);
        selectable.SelectionIndex = -1;
    }
}
```

## <a name="sorting-filtering-and-resetting-the-data"></a><span data-ttu-id="fafaf-289">データのリセットと並べ替え、フィルター処理</span><span class="sxs-lookup"><span data-stu-id="fafaf-289">Sorting, Filtering and Resetting the Data</span></span>

<span data-ttu-id="fafaf-290">フィルター処理またはデータ セットの並べ替えなどのアクションを実行するときに従来可能性がありますが、新しいデータにデータの前のセットを比較してで細かい変更通知を発行[INotifyCollectionChanged](/uwp/api/windows.ui.xaml.interop.inotifycollectionchanged)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-290">When you perform actions such as filtering or sorting your data set, you traditionally may have compared the previous set of data to the new data, then issued granular change notifications via [INotifyCollectionChanged](/uwp/api/windows.ui.xaml.interop.inotifycollectionchanged).</span></span> <span data-ttu-id="fafaf-291">ただし、完全に古いデータを新しいデータで置き換えるし、使用してコレクションの変更通知をトリガーしやすく、多くの場合、[リセット](/uwp/api/windows.ui.xaml.interop.notifycollectionchangedaction)アクション代わりにします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-291">However, it is often easier to completely replace the old data with the new data and trigger a collection change notification using the [Reset](/uwp/api/windows.ui.xaml.interop.notifycollectionchangedaction) action instead.</span></span>

<span data-ttu-id="fafaf-292">通常、リセットは、既存の子要素をリリースしてやり直すのリセット中に、データが変更する方法に正確に認識があるないために、スクロール位置の 0 から始まるから UI を構築するコントロールをによりします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-292">Typically, a reset causes a control to release existing child elements and start over, building the UI from the beginning at scroll position 0 as it has no awareness of exactly how the data has changed during the reset.</span></span>

<span data-ttu-id="fafaf-293">ただし、として、コレクションに割り当てられている場合、ItemsSource サポート一意識別子を実装して、 [IKeyIndexMapping](/uwp/api/microsoft.ui.xaml.controls.ikeyindexmapping)インターフェイス、ItemsRepeater をすばやく特定できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-293">However, if the collection assigned as the ItemsSource supports unique identifiers by implementing the [IKeyIndexMapping](/uwp/api/microsoft.ui.xaml.controls.ikeyindexmapping) interface, then the ItemsRepeater can quickly identify:</span></span>

- <span data-ttu-id="fafaf-294">前に、と、リセット後の両方に存在していたデータの再利用可能な Uielement</span><span class="sxs-lookup"><span data-stu-id="fafaf-294">reusable UIElements for data that existed both before and after the reset</span></span>
- <span data-ttu-id="fafaf-295">削除された表示される項目以前</span><span class="sxs-lookup"><span data-stu-id="fafaf-295">previously visible items that were removed</span></span>
- <span data-ttu-id="fafaf-296">新しく追加された項目が表示されます</span><span class="sxs-lookup"><span data-stu-id="fafaf-296">new items added that will be visible</span></span>

<span data-ttu-id="fafaf-297">これにより、ItemsRepeater のスクロール位置の 0 から経由で開始することができます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-297">This lets the ItemsRepeater avoid starting over from scroll position 0.</span></span> <span data-ttu-id="fafaf-298">パフォーマンスを向上させるその結果のリセットを変更していないデータの Uielement を迅速に復元することもできます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-298">It also lets it quickly restore the UIElements for data that didn't change in a reset, resulting in better performance.</span></span>

<span data-ttu-id="fafaf-299">この例は、垂直方向のスタックで項目の一覧を表示する方法を示しています。 場所_MyItemsSource_は、基になる項目のリストをラップするカスタム データ ソース。</span><span class="sxs-lookup"><span data-stu-id="fafaf-299">This example shows how to display a list of items in a vertical stack where _MyItemsSource_ is a custom data source that wraps an underlying list of items.</span></span> <span data-ttu-id="fafaf-300">これは、公開、_データ_プロパティが、リセットがトリガーされる項目ソースとして使用する新しいリストを再割り当てを使用できます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-300">It exposes a _Data_ property that can be used to re-assign a new list to use as the items source, which then triggers a reset.</span></span>

```xaml
<ScrollViewer x:Name="sv">
    <ItemsRepeater x:Name="repeater"
                ItemsSource="{x:Bind MyItemsSource}"
                ItemTemplate="{StaticResource MyTemplate}">
       <ItemsRepeater.Layout>
           <StackLayout ItemSpacing="8"/>
       </ItemsRepeater.Layout>
   </ItemsRepeater>
</ScrollViewer>
```

```csharp
public MainPage()
{
    this.InitializeComponent();

    // Similar to an ItemsControl, a developer sets the ItemsRepeater's ItemsSource.
    // Here we provide our custom source that supports unique IDs which enables
    // ItemsRepeater to be smart about handling resets from the data.
    // Unique IDs also make it easy to do things apply sorting/filtering
    // without impacting any state (i.e. selection).
    MyItemsSource myItemsSource = new MyItemsSource(data);

    repeater.ItemsSource = myItemsSource;

    // ...

    // We can sort/filter the data using whatever mechanism makes the
    // most sense (LINQ, database query, etc.) and then reassign
    // it, which in our implementation triggers a reset.
    myItemsSource.Data = someNewData;
}

// ...


public class MyItemsSource : IReadOnlyList<ItemBase>, IKeyIndexMapping, INotifyCollectionChanged
{
    private IList<ItemBase> _data;

    public MyItemsSource(IEnumerable<ItemBase> data)
    {
        if (data == null) throw new ArgumentNullException();

        this._data = data.ToList();
    }

    public IList<ItemBase> Data
    {
        get { return _data; }
        set
        {
            _data = value;

            // Instead of tossing out existing elements and re-creating them,
            // ItemsRepeater will reuse the existing elements and match them up
            // with the data again.
            this.CollectionChanged?.Invoke(
                this,
                new NotifyCollectionChangedEventArgs(NotifyCollectionChangedAction.Reset));
        }
    }

    #region IReadOnlyList<T>

    public ItemBase this[int index] => this.Data != null
        ? this.Data[index]
        : throw new IndexOutOfRangeException();

    public int Count => this.Data != null ? this.Data.Count : 0;
    public IEnumerator<ItemBase> GetEnumerator() => this.Data.GetEnumerator();
    IEnumerator IEnumerable.GetEnumerator() => this.GetEnumerator();

    #endregion

    #region INotifyCollectionChanged

    public event NotifyCollectionChangedEventHandler CollectionChanged;

    #endregion

    #region IKeyIndexMapping

    private int lastRequestedIndex = IndexNotFound;
    private const int IndexNotFound = -1;

    // When UniqueIDs are supported, the ItemsRepeater caches the unique ID for each item
    // with the matching UIElement that represents the item.  When a reset occurs the
    // ItemsRepeater pairs up the already generated UIElements with items in the data
    // source.
    // ItemsRepeater uses IndexForUniqueId after a reset to probe the data and identify
    // the new index of an item to use as the anchor.  If that item no
    // longer exists in the data source it may try using another cached unique ID until
    // either a match is found or it determines that all the previously visible items
    // no longer exist.
    public int IndexForUniqueId(string uniqueId)
    {
        // We'll try to increase our odds of finding a match sooner by starting from the
        // position that we know was last requested and search forward.
        var start = lastRequestedIndex;
        for (int i = start; i < this.Count; i++)
        {
            if (this[i].PrimaryKey.Equals(uniqueId))
                return i;
        }

        // Then try searching backward.
        start = Math.Min(this.Count - 1, lastRequestedIndex);
        for (int i = start; i >= 0; i--)
        {
            if (this[i].PrimaryKey.Equals(uniqueId))
                return i;
        }

        return IndexNotFound;
    }

    public string UniqueIdForIndex(int index)
    {
        var key = this[index].PrimaryKey;
        lastRequestedIndex = index;
        return key;
    }

    #endregion
}

```

## <a name="create-a-custom-collection-control"></a><span data-ttu-id="fafaf-301">コレクションのカスタム コントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-301">Create a custom collection control</span></span>

<span data-ttu-id="fafaf-302">使用することができます、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)独自の型の各項目を表示するコントロールを備えたカスタム コレクション コントロールを作成します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-302">You can use the [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) to create a custom collection control complete with its own type of control to present each item.</span></span>

> [!NOTE]
> <span data-ttu-id="fafaf-303">使用してに似ています**ItemsControl**がから派生するのではなく**ItemsControl**配置して、 **ItemsPresenter** から派生するコントロールテンプレートで**コントロール**を挿入し、 **ItemsRepeater**コントロール テンプレートにします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-303">This is similar to using **ItemsControl**, but instead of deriving from **ItemsControl** and putting an **ItemsPresenter** in the control template, you derive from **Control** and insert an **ItemsRepeater** in the control template.</span></span> <span data-ttu-id="fafaf-304">カスタム コレクション コントロール"は、" **ItemsRepeater**と"は、" **ItemsControl**します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-304">The custom collection control "has an" **ItemsRepeater** versus "is an" **ItemsControl**.</span></span> <span data-ttu-id="fafaf-305">つまり、ことを公開するプロパティを明示的に選択する必要がありますではなくこれをサポートしないようにプロパティが継承されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-305">This implies that you must also explicitly choose which properties to expose, rather than which inherited properties to not support.</span></span>

<span data-ttu-id="fafaf-306">この例では、配置、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)という名前のカスタム コントロールのテンプレートで_MediaCollectionView_し、そのプロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-306">This example shows how to place an [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) in the template of a custom control named _MediaCollectionView_ and expose its properties.</span></span>

```xaml
<!-- xmlns:muxc="using:Microsoft.UI.Xaml.Controls" -->
<Style TargetType="local:MediaCollectionView">
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="local:MediaCollectionView">
                <Border
                    Background="{TemplateBinding Background}"
                    BorderBrush="{TemplateBinding BorderBrush}"
                    BorderThickness="{TemplateBinding BorderThickness}">
                    <ScrollViewer x:Name="ScrollViewer">
                        <muxc:ItemsRepeater x:Name="ItemsRepeater"
                                            ItemsSource="{TemplateBinding ItemsSource}"
                                            ItemTemplate="{TemplateBinding ItemTemplate}"
                                            Layout="{TemplateBinding Layout}"
                                            TabFocusNavigation="{TemplateBinding TabFocusNavigation}"/>
                    </ScrollViewer>
                </Border>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

```csharp
public sealed class MediaCollectionView : Control
{
    public object ItemsSource
    {
        get { return (object)GetValue(ItemsSourceProperty); }
        set { SetValue(ItemsSourceProperty, value); }
    }

    // Using a DependencyProperty as the backing store for ItemsSource.  This enables animation, styling, binding, etc...
    public static readonly DependencyProperty ItemsSourceProperty =
        DependencyProperty.Register(nameof(ItemsSource), typeof(object), typeof(MediaCollectionView), new PropertyMetadata(0));

    public DataTemplate ItemTemplate
    {
        get { return (DataTemplate)GetValue(ItemTemplateProperty); }
        set { SetValue(ItemTemplateProperty, value); }
    }

    // Using a DependencyProperty as the backing store for ItemTemplate.  This enables animation, styling, binding, etc...
    public static readonly DependencyProperty ItemTemplateProperty =
        DependencyProperty.Register(nameof(ItemTemplate), typeof(DataTemplate), typeof(MediaCollectionView), new PropertyMetadata(0));

    public Layout Layout
    {
        get { return (Layout)GetValue(LayoutProperty); }
        set { SetValue(LayoutProperty, value); }
    }

    // Using a DependencyProperty as the backing store for Layout.  This enables animation, styling, binding, etc...
    public static readonly DependencyProperty LayoutProperty =
        DependencyProperty.Register(nameof(Layout), typeof(Layout), typeof(MediaCollectionView), new PropertyMetadata(0));

    public MediaCollectionView()
    {
        this.DefaultStyleKey = typeof(MediaCollectionView);
    }
}
```

## <a name="display-grouped-items"></a><span data-ttu-id="fafaf-307">グループ化された項目を表示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-307">Display grouped items</span></span>

<span data-ttu-id="fafaf-308">入れ子にすることができます、 [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)で、 [ItemTemplate](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate)入れ子になったを作成する別の ItemsRepeater のレイアウトを仮想化します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-308">You can nest an [ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) in the [ItemTemplate](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater.itemtemplate) of another ItemsRepeater to create nested virtualizing layouts.</span></span> <span data-ttu-id="fafaf-309">フレームワークが表示されない要素のまたは現在のビューポートの近くに不要な実現を最小限に抑えることによってリソースの使用効率がなります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-309">The framework will make efficient use of resources by minimizing unnecessary realization of elements that aren't visible or near the current viewport.</span></span>

<span data-ttu-id="fafaf-310">この例では、垂直方向のスタックにグループ化された項目の一覧を表示する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-310">This example shows how you can display a list of grouped items in a vertical stack.</span></span> <span data-ttu-id="fafaf-311">外部 ItemsRepeater には、各グループが生成されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-311">The outer ItemsRepeater generates each group.</span></span> <span data-ttu-id="fafaf-312">各グループのテンプレートでは、別 ItemsRepeater には、項目が生成されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-312">In the template for each group, another ItemsRepeater generates the items.</span></span>

```xaml
<!-- xmlns:muxc="using:Microsoft.UI.Xaml.Controls" -->
<ScrollViewer>
  <muxc:ItemsRepeater ItemsSource="{x:Bind AppNotifications}"
                      Layout="{StaticResource MyGroupLayout}">
    <muxc:ItemsRepeater.ItemTemplate>
      <DataTemplate x:DataType="ExampleApp:AppNotifications">
        <!-- Group -->
        <StackPanel>
          <!-- Header -->
          TextBlock Text="{x:Bind AppTitle}"/>
          <!-- Items -->
          <muxc:ItemsRepeater ItemsSource="{x:Bind Notifications}"
                              Layout="{StaticResource MyItemLayout}"
                              ItemTemplate="{StaticResource MyTemplate}"/>
          <!-- Footer -->
          <Button Content="{x:Bind FooterText}"/>
        </StackPanel>
      </DataTemplate>
    </muxc:ItemsRepeater.ItemTemplate>
  </muxc:ItemsRepeater>
</ScrollViewer>
```

<span data-ttu-id="fafaf-313">この例では、ユーザー設定を使用して変更できるし、は、次のように水平方向のスクロール リストとして表示されますが、さまざまなカテゴリがあるアプリケーションのレイアウトを示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-313">This example shows a layout for an app that has various categories that can change with user preference and are presented as horizontally scrolling lists, as shown here.</span></span>

![項目の repeater を入れ子になったレイアウト](images/items-repeater-nested-layout.png)

```xaml
<!-- xmlns:muxc="using:Microsoft.UI.Xaml.Controls" -->
<!-- Include the <muxc:ItemsRepeaterScrollHost> if targeting Windows 10 versions earlier than 1809. -->
<ScrollViewer>
  <muxc:ItemsRepeater ItemsSource="{x:Bind Categories}"
                      Background="LightGreen">
    <muxc:ItemsRepeater.ItemTemplate>
      <DataTemplate x:DataType="local:Category">
        <StackPanel Margin="12,0">
          <TextBlock Text="{x:Bind Name}" Style="{ThemeResource TitleTextBlockStyle}"/>
          <!-- Include the <muxc:ItemsRepeaterScrollHost> if targeting Windows 10 versions earlier than 1809. -->
          <ScrollViewer HorizontalScrollMode="Enabled"
                                          VerticalScrollMode="Disabled"
                                          HorizontalScrollBarVisibility="Auto" >
            <muxc:ItemsRepeater ItemsSource="{x:Bind Items}"
                                Background="Orange">
              <muxc:ItemsRepeater.ItemTemplate>
                <DataTemplate x:DataType="local:CategoryItem">
                  <Grid Margin="10"
                        Height="60" Width="120"
                        Background="LightBlue">
                    <TextBlock Text="{x:Bind Name}"
                               Style="{StaticResource SubtitleTextBlockStyle}"
                               Margin="4"/>
                  </Grid>
                </DataTemplate>
              </muxc:ItemsRepeater.ItemTemplate>
              <muxc:ItemsRepeater.Layout>
                <muxc:StackLayout Orientation="Horizontal"/>
              </muxc:ItemsRepeater.Layout>
            </muxc:ItemsRepeater>
          </ScrollViewer>
        </StackPanel>
      </DataTemplate>
    </muxc:ItemsRepeater.ItemTemplate>
  </muxc:ItemsRepeater>
</ScrollViewer>
```

## <a name="bringing-an-element-into-view"></a><span data-ttu-id="fafaf-315">要素をビューに取り込む</span><span class="sxs-lookup"><span data-stu-id="fafaf-315">Bringing an Element Into View</span></span>

<span data-ttu-id="fafaf-316">既に、XAML フレームワークは、1) がキーボード フォーカスを受け取るまたは 2) がナレーターのフォーカスを受け取ったときに、ビューに、FrameworkElement を取り込むを処理します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-316">The XAML framework already handles bringing a FrameworkElement into view when it either 1) receives keyboard focus or 2) receives Narrator focus.</span></span> <span data-ttu-id="fafaf-317">要素を明示的にビューを表示する必要があるその他のケースである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-317">There may be other cases where you need to explicitly bring an element into view.</span></span> <span data-ttu-id="fafaf-318">たとえば、ページ ナビゲーションの後に、UI の状態を復元するかユーザー アクションへの応答で。</span><span class="sxs-lookup"><span data-stu-id="fafaf-318">For example, in response to a user action or to restore the state of the UI after a page navigation.</span></span>

<span data-ttu-id="fafaf-319">仮想化された要素をビューに取り込む手順を以下にします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-319">Bringing a virtualized element into view involves the following:</span></span>
1. <span data-ttu-id="fafaf-320">項目の UIElement を実現します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-320">Realize a UIElement for an item</span></span>
2. <span data-ttu-id="fafaf-321">要素が有効な位置を持つようにするためのレイアウトを実行します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-321">Run the layout to ensure the element has a valid position</span></span>
3. <span data-ttu-id="fafaf-322">実際の要素を表示する要求を開始します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-322">Initiate a request to bring the realized element into view</span></span>

<span data-ttu-id="fafaf-323">次の例では、ページ ナビゲーションの後のフラットな縦方向のリストで項目のスクロール位置の復元の一環として、次の手順を示します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-323">The example below demonstrates these steps as part of restoring the scroll position of an item in a flat, vertical list after a page navigation.</span></span> <span data-ttu-id="fafaf-324">入れ子になった ItemsRepeaters を使用してデータを階層の場合は、アプローチは、基本的に同じですが、階層の各レベルで行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-324">In the case of hierarchical data using nested ItemsRepeaters the approach is essentially the same, but must be done at each level of the hierarchy.</span></span>

```xaml
<ScrollViewer x:Name="scrollviewer">
  <ItemsRepeater x:Name="repeater" .../>
</ScrollViewer>
```

```csharp
public class MyPage : Page
{
    // ...

    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        base.OnNavigatedTo(e);

            // retrieve saved offset + index(es) of the tracked element and then bring it into view.
            // ... 

            var element = repeater.GetOrCreateElement(index);

            // ensure the item is given a valid position
            element.UpdateLayout();

            element.StartBringIntoView(new BringIntoViewOptions()
            {
                VerticalOffset = relativeVerticalOffset
            });
    }

    protected override void OnNavigatingFrom(NavigatingCancelEventArgs e)
    {
        base.OnNavigatingFrom(e);

        // retrieve and save the relative offset and index(es) of the scrollviewer's current anchor element ...
        var anchor = this.scrollviewer.CurrentAnchor;
        var index = this.repeater.GetElementIndex(anchor);
        var anchorBounds = anchor.TransformToVisual(this.scrollviewer).TransformBounds(new Rect(0, 0, anchor.ActualWidth, anchor.ActualHeight));
        relativeVerticalOffset = this.sv.VerticalOffset – anchorBounds.Top;
    }
}

```

## <a name="enable-accessibility"></a><span data-ttu-id="fafaf-325">ユーザー補助機能を有効にします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-325">Enable Accessibility</span></span>

<span data-ttu-id="fafaf-326">[ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)既定のアクセシビリティのエクスペリエンスを提供しています。</span><span class="sxs-lookup"><span data-stu-id="fafaf-326">[ItemsRepeater](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater) does not provide a default accessibility experience.</span></span> <span data-ttu-id="fafaf-327">ドキュメント[UWP アプリのユーザビリティを](/windows/uwp/design/usability)包括的なユーザー エクスペリエンスを提供する豊富なアプリの確認に役立つ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-327">The documentation on [Usability for UWP apps](/windows/uwp/design/usability) provides a wealth of information to help you ensure your app provides an inclusive user experience.</span></span> <span data-ttu-id="fafaf-328">カスタム コントロールを作成する、ItemsRepeater を使用している場合はありますし、ドキュメントを参照してください[カスタム オートメーション ピア](/windows/uwp/design/accessibility/custom-automation-peers)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-328">If you're using the ItemsRepeater to create a custom control then be sure to see the documentation on [Custom automation peers](/windows/uwp/design/accessibility/custom-automation-peers).</span></span>

### <a name="keyboarding"></a><span data-ttu-id="fafaf-329">キーボード入力</span><span class="sxs-lookup"><span data-stu-id="fafaf-329">Keyboarding</span></span>
<span data-ttu-id="fafaf-330">フォーカスの移動 ItemsRepeater を提供する最小限の keyboarding サポートは XAML のに基づいて[Keyboarding の 2D の方向ナビゲーション](/windows/uwp/design/input/focus-navigation#2d-directional-navigation-for-keyboard)します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-330">The minimal keyboarding support for focus movement that ItemsRepeater provides is based on XAML's [2D Directional Navigation for Keyboarding](/windows/uwp/design/input/focus-navigation#2d-directional-navigation-for-keyboard).</span></span>

![方向ナビゲーション](/windows/uwp/design/input/images/keyboard/directional-navigation.png)

<span data-ttu-id="fafaf-332">ItemsRepeater の[XYFocusKeyboardNavigation モード](/uwp/api/windows.ui.xaml.input.xyfocuskeyboardnavigationmode)は_有効_既定。</span><span class="sxs-lookup"><span data-stu-id="fafaf-332">The ItemsRepeater's [XYFocusKeyboardNavigation mode](/uwp/api/windows.ui.xaml.input.xyfocuskeyboardnavigationmode) is _Enabled_ by default.</span></span> <span data-ttu-id="fafaf-333">意図したエクスペリエンスによって共通のサポートの追加を検討する[キーボードの相互作用](/windows/uwp/design/input/keyboard-interactions)Home、End、PageUp、PageDown など。</span><span class="sxs-lookup"><span data-stu-id="fafaf-333">Depending on the intended experience, consider adding support for common [Keyboard Interactions](/windows/uwp/design/input/keyboard-interactions) such as Home, End, PageUp, and PageDown.</span></span>

<span data-ttu-id="fafaf-334">ItemsRepeater は自動的に、その項目の既定のタブ オーダー (かどうかを仮想化された) かどうかに従うこと、データ内の項目が指定されているのと同じ順序を確認します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-334">The ItemsRepeater does automatically ensure that the default tab order for its items (whether virtualized or not) follows the same order that the items are given in the data.</span></span> <span data-ttu-id="fafaf-335">既定で、ItemsRepeater はその[TabFocusNavigation](/uwp/api/windows.ui.xaml.uielement.tabfocusnavigation)プロパティに設定[1 回](/uwp/api/windows.ui.xaml.input.keyboardnavigationmode)の一般的な既定ではなく_ローカル_。</span><span class="sxs-lookup"><span data-stu-id="fafaf-335">By default the ItemsRepeater has its [TabFocusNavigation](/uwp/api/windows.ui.xaml.uielement.tabfocusnavigation) property set to [Once](/uwp/api/windows.ui.xaml.input.keyboardnavigationmode) instead of the common default of _Local_.</span></span>

> [!NOTE]
> <span data-ttu-id="fafaf-336">ItemsRepeater は、最後にフォーカスがある項目を自動的に保存されていません。</span><span class="sxs-lookup"><span data-stu-id="fafaf-336">The ItemsRepeater does not automatically remember the last focused item.</span></span>  <span data-ttu-id="fafaf-337">これは、ユーザーが使用する場合 Shift + tab 最後の実行可能性がありますが項目を実現することを意味します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-337">This means that when a user is using Shift+Tab they may be taken to the last realized item.</span></span>

### <a name="announcing-item-x-of-y-in-screen-readers"></a><span data-ttu-id="fafaf-338">お知らせ"項目_X_の_Y_"スクリーン リーダーで</span><span class="sxs-lookup"><span data-stu-id="fafaf-338">Announcing "Item _X_ of _Y_" in Screen Readers</span></span>

<span data-ttu-id="fafaf-339">値など、適切なオートメーション プロパティの設定を管理する必要がある**PositionInSet**と**SizeOfSet**、まま項目が追加されると、最新の状態を確認してくださいなど、削除、移動します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-339">You need to manage setting the appropriate automation properties, such as values for **PositionInSet** and **SizeOfSet**, and ensure they remain up-to-date when items are added, moved, removed, etc.</span></span>

<span data-ttu-id="fafaf-340">カスタム レイアウトの中である可能性がありますいない視覚的な順序を明らかにシーケンスします。</span><span class="sxs-lookup"><span data-stu-id="fafaf-340">In some custom layouts there may not be an obvious sequence to the visual order.</span></span>  <span data-ttu-id="fafaf-341">ユーザーは、スクリーン リーダーによって使用される PositionInSet と SizeOfSet プロパティの値が (0 ベースとカウントが自然に一致するように 1 ずつオフセット)、データ内の項目が表示される順序を一致する最小期待します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-341">Users minimally expect that the values for the PositionInSet and SizeOfSet properties used by screen readers will match the order the items appear in the data (offset by 1 to match natural counting versus being 0-based).</span></span>

<span data-ttu-id="fafaf-342">これを実現する最善の方法は、アイテム コントロールの実装のオートメーション ピアのことで、 [GetPositionInSetCore](/uwp/api/windows.ui.xaml.automation.peers.automationpeer.getpositioninsetcore)と[GetSizeOfSetCore](/uwp/api/windows.ui.xaml.automation.peers.automationpeer.getsizeofsetcore)メソッドとレポート、データ セット内の項目の位置コントロールで表されます。</span><span class="sxs-lookup"><span data-stu-id="fafaf-342">The best way to achieve this is by having the automation peer for the item control implement the [GetPositionInSetCore](/uwp/api/windows.ui.xaml.automation.peers.automationpeer.getpositioninsetcore) and [GetSizeOfSetCore](/uwp/api/windows.ui.xaml.automation.peers.automationpeer.getsizeofsetcore) methods and report the position of the item in the data set represented by the control.</span></span> <span data-ttu-id="fafaf-343">実行時の支援技術がアクセスするときに値を計算してのみと、問題以外を最新に保つことになります。</span><span class="sxs-lookup"><span data-stu-id="fafaf-343">The value is only computed at run-time when accessed by an assistive technology and keeping it up-to-date becomes a non-issue.</span></span> <span data-ttu-id="fafaf-344">値は、データの順序と一致します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-344">The value matches the data order.</span></span>

<span data-ttu-id="fafaf-345">この例では、そう方法でしたというカスタム コントロールを表示するときに_CardControl_します。</span><span class="sxs-lookup"><span data-stu-id="fafaf-345">This example shows how you could do this when presenting a custom control called _CardControl_.</span></span>

```xaml
<ScrollViewer >
    <ItemsRepeater x:Name="repeater" ItemsSource="{x:Bind MyItemsSource}">
       <ItemsRepeater.ItemTemplate>
           <DataTemplate x:DataType="local:CardViewModel">
               <local:CardControl Item="{x:Bind}"/>
           </DataTemplate>
       </ItemsRepeater.ItemTemplate>
   </ItemsRepeater>
</ScrollViewer>
```

```csharp
internal sealed class CardControl : CardControlBase
{
    protected override AutomationPeer OnCreateAutomationPeer() => new CardControlAutomationPeer(this);

    private sealed class CardControlAutomationPeer : FrameworkElementAutomationPeer
    {
        private readonly CardControl owner;

        public CardControlAutomationPeer(CardControl owner) : base(owner) => this.owner = owner;

        protected override int GetPositionInSetCore()
          => ((ItemsRepeater)owner.Parent)?.GetElementIndex(this.owner) + 1 ?? base.GetPositionInSetCore();

        protected override int GetSizeOfSetCore()
          => ((ItemsRepeater)owner.Parent)?.ItemsSourceView?.Count ?? base.GetSizeOfSetCore();
    }
}
```

## <a name="related-articles"></a><span data-ttu-id="fafaf-346">関連記事</span><span class="sxs-lookup"><span data-stu-id="fafaf-346">Related articles</span></span>

- [<span data-ttu-id="fafaf-347">リスト</span><span class="sxs-lookup"><span data-stu-id="fafaf-347">Lists</span></span>](lists.md)
- [<span data-ttu-id="fafaf-348">ItemsRepeater</span><span class="sxs-lookup"><span data-stu-id="fafaf-348">ItemsRepeater</span></span>](/uwp/api/microsoft.ui.xaml.controls.itemsrepeater)
- [<span data-ttu-id="fafaf-349">ScrollViewer</span><span class="sxs-lookup"><span data-stu-id="fafaf-349">ScrollViewer</span></span>](/uwp/api/windows.ui.xaml.controls.scrollviewer)
