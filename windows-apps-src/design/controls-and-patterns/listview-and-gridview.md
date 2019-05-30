---
Description: ListView と GridView コントロールを使用して、表示イメージのギャラリーや一連の電子メール メッセージなどのデータのセットを操作します。
title: リスト ビューとグリッド ビュー
label: List view and grid view
template: detail.hbs
ms.date: 05/20/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: f8532ba0-5510-4686-9fcf-87fd7c643e7b
pm-contact: predavid
design-contact: kimsea
dev-contact: ranjeshj
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 1664da65beed21dededb481aadd56f793af20f01
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66364681"
---
# <a name="list-view-and-grid-view"></a><span data-ttu-id="a72c2-104">リスト ビューとグリッド ビュー</span><span class="sxs-lookup"><span data-stu-id="a72c2-104">List view and grid view</span></span>

<span data-ttu-id="a72c2-105">ほとんどのアプリでは、イメージ ギャラリー、メール メッセージなどのデータのセットを操作および表示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-105">Most applications manipulate and display sets of data, such as a gallery of images or a set of email messages.</span></span> <span data-ttu-id="a72c2-106">XAML UI フレームワークでは、アプリ内でデータを簡単に表示、操作するための ListView コントロールと GridView コントロールが用意されています。</span><span class="sxs-lookup"><span data-stu-id="a72c2-106">The XAML UI framework provides ListView and GridView controls that make it easy to display and manipulate data in your app.</span></span>  

> <span data-ttu-id="a72c2-107">**重要な API**:[ListView クラス](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listview)、 [GridView クラス](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.gridview)、 [ItemsSource プロパティ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource)、[項目のプロパティ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items)</span><span class="sxs-lookup"><span data-stu-id="a72c2-107">**Important APIs**: [ListView class](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listview), [GridView class](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.gridview), [ItemsSource property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource), [Items property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items)</span></span>

<span data-ttu-id="a72c2-108">ListView と GridView はどちらも ListViewBase クラスから派生しているため、同じ機能を持ちますが、データの表示方法が異なります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-108">ListView and GridView both derive from the ListViewBase class, so they have the same functionality, but display data differently.</span></span> <span data-ttu-id="a72c2-109">この記事では、特に指定がない限り、ListView についての説明は ListView コントロールにも GridView コントロールにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-109">In this article, when we talk about ListView, the info applies to both the ListView and GridView controls unless otherwise specified.</span></span> <span data-ttu-id="a72c2-110">ListView や ListViewItem などのクラスの説明については、プレフィックスの "List" を "Grid" に置き換えることで、対応するグリッド クラス (GridView または GridViewItem) に適用できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-110">We may refer to classes like ListView or ListViewItem, but the “List” prefix can be replaced with “Grid” for the corresponding grid equivalent (GridView or GridViewItem).</span></span> 

## <a name="is-this-the-right-control"></a><span data-ttu-id="a72c2-111">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-111">Is this the right control?</span></span>

<span data-ttu-id="a72c2-112">ListView では、データを縦方向の 1 列に並べて表示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-112">The ListView displays data stacked vertically in a single column.</span></span> <span data-ttu-id="a72c2-113">メールや検索結果の一覧など、順序が付けられた項目の一覧を表示するときによく使います。</span><span class="sxs-lookup"><span data-stu-id="a72c2-113">It's often used to show an ordered list of items, such as a list of emails or search results.</span></span> 

![グループ化されたデータを表示するリスト ビュー](images/simple-list-view-phone.png)

<span data-ttu-id="a72c2-115">GridView は、縦方向にスクロールできる複数行と複数列で項目のコレクションを表示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-115">The GridView presents a collection of items in rows and columns that can scroll vertically.</span></span> <span data-ttu-id="a72c2-116">データはまず横方向に並べられ、すべての列にデータが入ると、次の行に折り返して並べられます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-116">Data is stacked horizontally until it fills the columns, then continues with the next row.</span></span> <span data-ttu-id="a72c2-117">フォト ギャラリーのように、各項目の表示内容が豊富で表示領域を広く使う必要がある場合によく使います。</span><span class="sxs-lookup"><span data-stu-id="a72c2-117">It's often used when you need to show a rich visualization of each item that takes more space, such as a photo gallery.</span></span> 

![コンテンツ ライブラリの例](images/controls_list_contentlibrary.png)

<span data-ttu-id="a72c2-119">使用するコントロールを選ぶための詳しい比較とガイダンスについては、「[リスト](lists.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-119">For a more detailed comparison and guidance on which control to use, see [Lists](lists.md).</span></span>

## <a name="examples"></a><span data-ttu-id="a72c2-120">例</span><span class="sxs-lookup"><span data-stu-id="a72c2-120">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="a72c2-121">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="a72c2-121">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="a72c2-122"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックしてアプリを開き、<a href="xamlcontrolsgallery:/item/ListView">ListView</a> または <a href="xamlcontrolsgallery:/item/GridView">GridView</a> の動作を確認してください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-122">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to open the app and see the <a href="xamlcontrolsgallery:/item/ListView">ListView</a> or <a href="xamlcontrolsgallery:/item/GridView">GridView</a> in action.</span></span></p>
    <ul>
    <li><span data-ttu-id="a72c2-123"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="a72c2-123"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="a72c2-124"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="a72c2-124"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="create-a-list-view"></a><span data-ttu-id="a72c2-125">リスト ビューの作成</span><span class="sxs-lookup"><span data-stu-id="a72c2-125">Create a list view</span></span>

<span data-ttu-id="a72c2-126">リスト ビューは [ItemsControl](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol) であるため、あらゆる種類の項目のコレクションを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-126">List view is an [ItemsControl](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol), so it can contain a collection of items of any type.</span></span> <span data-ttu-id="a72c2-127">リスト ビューを使って項目を表示するには、[Items](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items) コレクションに項目を追加しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-127">It must have items in its [Items](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items) collection before it can show anything on the screen.</span></span> <span data-ttu-id="a72c2-128">ビューのデータを設定するには、項目を直接 [Items](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items) コレクションに追加するか、データ ソースに [ItemsSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-128">To populate the view, you can add items directly to the [Items](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items) collection, or set the [ItemsSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) property to a data source.</span></span> 

<span data-ttu-id="a72c2-129">**重要**&nbsp;&nbsp;リストにデータを設定するときには Items または ItemsSource を使用しますが、同時に両方を使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="a72c2-129">**Important**&nbsp;&nbsp;You can use either Items or ItemsSource to populate the list, but you can't use both at the same time.</span></span> <span data-ttu-id="a72c2-130">ItemsSource プロパティを設定して XAML で項目を追加した場合、追加された項目は無視されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-130">If you set the ItemsSource property and you add an item in XAML, the added item is ignored.</span></span> <span data-ttu-id="a72c2-131">ItemsSource プロパティを設定してコードで Items コレクションに項目を追加した場合、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-131">If you set the ItemsSource property and you add an item to the Items collection in code, an exception is thrown.</span></span>

> <span data-ttu-id="a72c2-132">**注**&nbsp;&nbsp;この記事の例の多くでは、説明を簡単にするために **Items** コレクションを直接設定しています。</span><span class="sxs-lookup"><span data-stu-id="a72c2-132">**Note**&nbsp;&nbsp;Many of the examples in this article populate the **Items** collection directly for the sake of simplicity.</span></span> <span data-ttu-id="a72c2-133">ただし、リストの項目は、オンライン データベースの書籍一覧など、動的なソースから取得される方が一般的です。</span><span class="sxs-lookup"><span data-stu-id="a72c2-133">However, it's more common for the items in a list to come from a dynamic source, like a list of books from an online database.</span></span> <span data-ttu-id="a72c2-134">このようなケースでは、**ItemsSource** プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-134">You use the **ItemsSource** property for this purpose.</span></span> 

### <a name="add-items-to-the-items-collection"></a><span data-ttu-id="a72c2-135">Items コレクションへの項目の追加</span><span class="sxs-lookup"><span data-stu-id="a72c2-135">Add items to the Items collection</span></span>

<span data-ttu-id="a72c2-136">[Items](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items) コレクションに項目を追加するには、XAML かコードを使います。</span><span class="sxs-lookup"><span data-stu-id="a72c2-136">You can add items to the [Items](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.items) collection using XAML or code.</span></span> <span data-ttu-id="a72c2-137">通常、項目が少数で、その項目が変わらず、XAML で簡単に定義できる場合や、実行時にコードで項目を生成する場合は、この方法で項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-137">You typically add items this way if you have a small number of items that don't change and are easily defined in XAML, or if you generate the items in code at run time.</span></span> 

<span data-ttu-id="a72c2-138">XAML で項目をインラインで定義したリスト ビューを次に示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-138">Here's a list view with items defined inline in XAML.</span></span> <span data-ttu-id="a72c2-139">XAML で項目を定義すると、定義した項目は Items コレクションに自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-139">When you define the items in XAML, they are automatically added to the Items collection.</span></span>

<span data-ttu-id="a72c2-140">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-140">**XAML**</span></span>
```xaml
<ListView x:Name="listView1"> 
   <x:String>Item 1</x:String> 
   <x:String>Item 2</x:String> 
   <x:String>Item 3</x:String> 
   <x:String>Item 4</x:String> 
   <x:String>Item 5</x:String> 
</ListView>  
```

<span data-ttu-id="a72c2-141">作成したリスト ビューのコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-141">Here's the list view created in code.</span></span> <span data-ttu-id="a72c2-142">生成されるリストは、XAML で作ったものと同じです。</span><span class="sxs-lookup"><span data-stu-id="a72c2-142">The resulting list is the same as the one created previously in XAML.</span></span>

<span data-ttu-id="a72c2-143">**C#**</span><span class="sxs-lookup"><span data-stu-id="a72c2-143">**C#**</span></span>
```csharp
// Create a new ListView and add content. 
ListView listView1 = new ListView(); 
listView1.Items.Add("Item 1"); 
listView1.Items.Add("Item 2"); 
listView1.Items.Add("Item 3"); 
listView1.Items.Add("Item 4"); 
listView1.Items.Add("Item 5");
 
// Add the ListView to a parent container in the visual tree. 
stackPanel1.Children.Add(listView1); 
```

<span data-ttu-id="a72c2-144">ListView は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-144">The ListView looks like this.</span></span>

![単純なリスト ビュー](images/listview-simple.png)

### <a name="set-the-items-source"></a><span data-ttu-id="a72c2-146">項目ソースの設定</span><span class="sxs-lookup"><span data-stu-id="a72c2-146">Set the items source</span></span>

<span data-ttu-id="a72c2-147">通常、リスト ビューを使って、データベースやインターネットなどのソースからデータを表示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-147">You typically use a list view to display data from a source such as a database or the Internet.</span></span> <span data-ttu-id="a72c2-148">データ ソースからリスト ビューのデータを設定するには、[ItemsSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) プロパティをデータ項目のコレクションに設定します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-148">To populate a list view from a data source, you set its [ItemsSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) property to a collection of data items.</span></span>

<span data-ttu-id="a72c2-149">以下の例では、コードでコレクションのインスタンスに直接リスト ビューの ItemsSource を設定しています。</span><span class="sxs-lookup"><span data-stu-id="a72c2-149">Here, the list view's ItemsSource is set in code directly to an instance of a collection.</span></span>

<span data-ttu-id="a72c2-150">**C#**</span><span class="sxs-lookup"><span data-stu-id="a72c2-150">**C#**</span></span>
```csharp 
// Instead of hard coded items, the data could be pulled 
// asynchronously from a database or the internet.
ObservableCollection<string> listItems = new ObservableCollection<string>();
listItems.Add("Item 1");
listItems.Add("Item 2");
listItems.Add("Item 3");
listItems.Add("Item 4");
listItems.Add("Item 5");

// Create a new list view, add content, 
ListView itemListView = new ListView();
itemListView.ItemsSource = listItems;

// Add the list view to a parent container in the visual tree.
stackPanel1.Children.Add(itemListView);
```

<span data-ttu-id="a72c2-151">ItemsSource プロパティを、XAML でコレクションにバインドすることもできます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-151">You can also bind the ItemsSource property to a collection in XAML.</span></span> <span data-ttu-id="a72c2-152">データ バインディングについて詳しくは、「[データ バインディングの概要](https://docs.microsoft.com/windows/uwp/data-binding/data-binding-quickstart)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-152">For more info about data binding, see [Data binding overview](https://docs.microsoft.com/windows/uwp/data-binding/data-binding-quickstart).</span></span>

<span data-ttu-id="a72c2-153">ここでは、ページのプライベート データ コレクションを公開する `Items` という名前のパブリック プロパティに ItemsSource をバインドします。</span><span class="sxs-lookup"><span data-stu-id="a72c2-153">Here, the ItemsSource is bound to a public property named `Items` that exposes the Page's private data collection.</span></span>

<span data-ttu-id="a72c2-154">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-154">**XAML**</span></span>
```xaml
<ListView x:Name="itemListView" ItemsSource="{x:Bind Items}"/>
```

<span data-ttu-id="a72c2-155">**C#**</span><span class="sxs-lookup"><span data-stu-id="a72c2-155">**C#**</span></span>
```csharp
private ObservableCollection<string> _items = new ObservableCollection<string>();

public ObservableCollection<string> Items
{
    get { return this._items; }
}

protected override void OnNavigatedTo(NavigationEventArgs e)
{
    base.OnNavigatedTo(e);

    // Instead of hard coded items, the data could be pulled 
    // asynchronously from a database or the internet.
    Items.Add("Item 1");
    Items.Add("Item 2");
    Items.Add("Item 3");
    Items.Add("Item 4");
    Items.Add("Item 5");
}
```

<span data-ttu-id="a72c2-156">リスト ビューにグループ化されたデータを表示する必要がある場合、[CollectionViewSource](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) にバインドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-156">If you need to show grouped data in your list view, you must bind to a [CollectionViewSource](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource).</span></span> <span data-ttu-id="a72c2-157">CollectionViewSource は XAML のコレクション クラスのプロキシとして機能し、グループ化サポートを有効にします。</span><span class="sxs-lookup"><span data-stu-id="a72c2-157">The CollectionViewSource acts as a proxy for the collection class in XAML and enables grouping support.</span></span> <span data-ttu-id="a72c2-158">詳しくは、[CollectionViewSource](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-158">For more info, see [CollectionViewSource](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource).</span></span>

## <a name="data-template"></a><span data-ttu-id="a72c2-159">データ テンプレート</span><span class="sxs-lookup"><span data-stu-id="a72c2-159">Data template</span></span>

<span data-ttu-id="a72c2-160">項目のデータ テンプレートによって、データの表示方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-160">An item’s data template defines how the data is visualized.</span></span> <span data-ttu-id="a72c2-161">既定では、データ項目は、バインドされているデータ オブジェクトの文字列表現としてリスト ビューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-161">By default, a data item is displayed in the list view as the string representation of the data object it's bound to.</span></span> <span data-ttu-id="a72c2-162">データ項目の特定のプロパティに [DisplayMemberPath](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.displaymemberpath) を設定すると、そのプロパティの文字列表現を表示できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-162">You can show the string representation of a particular property of the data item by setting the [DisplayMemberPath](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.displaymemberpath) to that property.</span></span>

<span data-ttu-id="a72c2-163">しかし、通常はもっとリッチな表現でデータを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-163">However, you typically want to show a more rich presentation of your data.</span></span> <span data-ttu-id="a72c2-164">リスト ビューでの項目の表示方法を正確に指定するには、[DataTemplate](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.DataTemplate) を作成します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-164">To specify exactly how items in the list view are displayed, you create a [DataTemplate](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.DataTemplate).</span></span> <span data-ttu-id="a72c2-165">DataTemplate の XAML では、個々の項目を表示するために使うコントロールのレイアウトと外観を定義します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-165">The XAML in the DataTemplate defines the layout and appearance of controls used to display an individual item.</span></span> <span data-ttu-id="a72c2-166">レイアウト内のコントロールでは、データ オブジェクトのプロパティにバインドすることも、静的コンテンツをインラインで定義することもできます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-166">The controls in the layout can be bound to properties of a data object, or have static content defined inline.</span></span> <span data-ttu-id="a72c2-167">DataTemplate は、リスト コントロールの [ItemTemplate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemtemplate) プロパティに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-167">You assign the DataTemplate to the [ItemTemplate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemtemplate) property of the list control.</span></span>

<span data-ttu-id="a72c2-168">この例では、データ項目は単純な文字列です。</span><span class="sxs-lookup"><span data-stu-id="a72c2-168">In this example, the data item is a simple string.</span></span> <span data-ttu-id="a72c2-169">DataTemplate を使って、文字列の左側に画像を追加し、文字列を青緑で表示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-169">You use a DataTemplate to add an image to the left of the string, and show the string in teal.</span></span>

> <span data-ttu-id="a72c2-170">**注**&nbsp;&nbsp;DataTemplate で [x:Bind markup extension](https://docs.microsoft.com/windows/uwp/xaml-platform/x-bind-markup-extension) を使用する場合、DataTemplate に DataType (`x:DataType`) を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-170">**Note**&nbsp;&nbsp;When you use the [x:Bind markup extension](https://docs.microsoft.com/windows/uwp/xaml-platform/x-bind-markup-extension) in a DataTemplate, you have to specify the DataType (`x:DataType`) on the DataTemplate.</span></span>

<span data-ttu-id="a72c2-171">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-171">**XAML**</span></span>
```XAML
<ListView x:Name="listView1">
    <ListView.ItemTemplate>
        <DataTemplate x:DataType="x:String">
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="47"/>
                    <ColumnDefinition/>
                </Grid.ColumnDefinitions>
                <Image Source="Assets/placeholder.png" Width="32" Height="32" 
                       HorizontalAlignment="Left"/>
                <TextBlock Text="{x:Bind}" Foreground="Teal" 
                           FontSize="14" Grid.Column="1"/>
            </Grid> 
        </DataTemplate>
    </ListView.ItemTemplate>
    <x:String>Item 1</x:String>
    <x:String>Item 2</x:String>
    <x:String>Item 3</x:String>
    <x:String>Item 4</x:String>
    <x:String>Item 5</x:String>
</ListView>
```

<span data-ttu-id="a72c2-172">このデータ テンプレートを使ってデータ項目を表示すると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-172">Here's what the data items look like when displayed with this data template.</span></span>

![データ テンプレートを使ったリスト ビュー項目](images/listview-itemstemplate.png)

<span data-ttu-id="a72c2-174">データ テンプレートは、リスト ビューの外観を定義する主要な方法です。</span><span class="sxs-lookup"><span data-stu-id="a72c2-174">Data templates are the primary way you define the look of your list view.</span></span> <span data-ttu-id="a72c2-175">リストに多数の項目を表示した場合、パフォーマンスが大幅に低下することもあります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-175">They can also have a significant impact on performance if your list displays a large number of items.</span></span> <span data-ttu-id="a72c2-176">この記事では、ほとんどの例で単純な文字列データを使用しており、データ テンプレートを指定していません。</span><span class="sxs-lookup"><span data-stu-id="a72c2-176">In this article, we use simple string data for most of the examples, and don't specify a data template.</span></span> <span data-ttu-id="a72c2-177">データ テンプレートと項目コンテナーを使用してリストまたはグリッドの項目の外観を定義する詳しい方法とその例については、「[項目コンテナーやテンプレート](item-containers-templates.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-177">For more info and examples of how to use data templates and item containers to define the look of items in your list or grid, see [Item containers and templates](item-containers-templates.md).</span></span> 

## <a name="change-the-layout-of-items"></a><span data-ttu-id="a72c2-178">項目のレイアウト変更</span><span class="sxs-lookup"><span data-stu-id="a72c2-178">Change the layout of items</span></span>

<span data-ttu-id="a72c2-179">リスト ビューまたはグリッド ビューに項目を追加すると、項目コンテナー内で各項目が自動的に折り返され、すべての項目コンテナーがレイアウトされます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-179">When you add items to a list view or grid view, the control automatically wraps each item in an item container and then lays out all of the item containers.</span></span> <span data-ttu-id="a72c2-180">この項目コンテナーのレイアウト方法は、コントロールの [ItemsPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemspanel) によって決まります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-180">How these item containers are laid out depends on the [ItemsPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemspanel) of the control.</span></span>  
- <span data-ttu-id="a72c2-181">**ListView** では既定で [ItemsStackPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel) が使用され、次のような縦 1 列のリストが生成されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-181">By default, **ListView** uses an [ItemsStackPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel), which produces a vertical list, like this.</span></span>

![単純なリスト ビュー](images/listview-simple.png)

- <span data-ttu-id="a72c2-183">**GridView** では [ItemsWrapGrid](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemswrapgrid) が使用されます。次のように、項目が水平方向に追加され、折り返されて縦方向にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="a72c2-183">**GridView** uses an [ItemsWrapGrid](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemswrapgrid), which adds items horizontally, and wraps and scrolls vertically, like this.</span></span>

![単純なグリッド ビュー](images/gridview-simple.png)

<span data-ttu-id="a72c2-185">項目のレイアウトを変更するには、項目パネルのプロパティを調整するか、既定のパネルを別のパネルに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-185">You can modify the layout of items by adjusting properties on the items panel, or you can replace the default panel with another panel.</span></span>

> <span data-ttu-id="a72c2-186">注&nbsp;&nbsp;ItemsPanel を変更する場合、仮想化を無効にしないように注意してください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-186">Note&nbsp;&nbsp;Be careful to not disable virtualization if you change the ItemsPanel.</span></span> <span data-ttu-id="a72c2-187">**ItemsStackPanel** と **ItemsWrapGrid** はどちらも仮想化をサポートしており、安全に使用できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-187">Both **ItemsStackPanel** and **ItemsWrapGrid** support virtualization, so these are safe to use.</span></span> <span data-ttu-id="a72c2-188">他のパネルを使用すると、仮想化が無効になり、リスト ビューのパフォーマンスが低下する場合があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-188">If you use any other panel, you might disable virtualization and slow the performance of the list view.</span></span> <span data-ttu-id="a72c2-189">詳しくは、「[Performance (パフォーマンス)](https://docs.microsoft.com/windows/uwp/debug-test-perf/performance-and-xaml-ui)」のリスト ビューに関する記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-189">For more info, see the list view articles under [Performance](https://docs.microsoft.com/windows/uwp/debug-test-perf/performance-and-xaml-ui).</span></span> 

<span data-ttu-id="a72c2-190">この例では、**ItemsStackPanel** の [Orientation](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel.orientation) プロパティを変更することで、**ListView** に項目コンテナーを横 1 列にレイアウトする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a72c2-190">This example shows how to make a **ListView** lay out its item containers in a horizontal list by changing the [Orientation](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel.orientation) property of the **ItemsStackPanel**.</span></span>
<span data-ttu-id="a72c2-191">リスト ビューは既定で縦方向にスクロールするため、横方向にスクロールさせるには、リスト ビュー内部の [ScrollViewer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer) のプロパティもいくつか調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-191">Because the list view scrolls vertically by default, you also need to adjust some properties on the list view’s internal [ScrollViewer](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer) to make it scroll horizontally.</span></span>
- <span data-ttu-id="a72c2-192">[ScrollViewer.HorizontalScrollMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.horizontalscrollmode) を **Enabled** または **Auto** に設定</span><span class="sxs-lookup"><span data-stu-id="a72c2-192">[ScrollViewer.HorizontalScrollMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.horizontalscrollmode) to **Enabled** or **Auto**</span></span>
- <span data-ttu-id="a72c2-193">[ScrollViewer.HorizontalScrollBarVisibility](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.horizontalscrollbarvisibility) を **Auto** に設定</span><span class="sxs-lookup"><span data-stu-id="a72c2-193">[ScrollViewer.HorizontalScrollBarVisibility](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.horizontalscrollbarvisibility) to **Auto**</span></span> 
- <span data-ttu-id="a72c2-194">[ScrollViewer.VerticalScrollMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.verticalscrollmode) を **Disabled** に設定</span><span class="sxs-lookup"><span data-stu-id="a72c2-194">[ScrollViewer.VerticalScrollMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.verticalscrollmode) to **Disabled**</span></span> 
- <span data-ttu-id="a72c2-195">[ScrollViewer.VerticalScrollBarVisibility](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.verticalscrollbarvisibility) を **Hidden** に設定</span><span class="sxs-lookup"><span data-stu-id="a72c2-195">[ScrollViewer.VerticalScrollBarVisibility](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.scrollviewer.verticalscrollbarvisibility) to **Hidden**</span></span> 

> <span data-ttu-id="a72c2-196">**注**&nbsp;&nbsp;ここに示す例ではリスト ビューの幅が規定されていないため、水平スクロール バーは表示されません。</span><span class="sxs-lookup"><span data-stu-id="a72c2-196">**Note**&nbsp;&nbsp;These examples are shown with the list view width unconstrained, so the horizontal scrollbars are not shown.</span></span> <span data-ttu-id="a72c2-197">このコードを実行する場合、ListView に `Width="180"` を設定してスクロール バーを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-197">If you run this code, you can set `Width="180"` on the ListView to make the scrollbars show.</span></span>

<span data-ttu-id="a72c2-198">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-198">**XAML**</span></span>
```xaml
<ListView Height="60" 
          ScrollViewer.HorizontalScrollMode="Enabled" 
          ScrollViewer.HorizontalScrollBarVisibility="Auto"
          ScrollViewer.VerticalScrollMode="Disabled"
          ScrollViewer.VerticalScrollBarVisibility="Hidden">
    <ListView.ItemsPanel>
        <ItemsPanelTemplate>
            <ItemsStackPanel Orientation="Horizontal"/>
        </ItemsPanelTemplate>
    </ListView.ItemsPanel>
    <x:String>Item 1</x:String>
    <x:String>Item 2</x:String>
    <x:String>Item 3</x:String>
    <x:String>Item 4</x:String>
    <x:String>Item 5</x:String>
</ListView>
```

<span data-ttu-id="a72c2-199">このリストは次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-199">The resulting list looks like this.</span></span>

![横長のリスト ビュー](images/listview-horizontal.png)

 <span data-ttu-id="a72c2-201">次の例の **ListView** では、**ItemsStackPanel** ではなく **ItemsWrapGrid** を使用して、縦方向に折り返すリストで項目をレイアウトします。</span><span class="sxs-lookup"><span data-stu-id="a72c2-201">In the next example, the **ListView** lays out items in a vertical wrapping list by using an **ItemsWrapGrid** instead of an **ItemsStackPanel**.</span></span> 
 
> <span data-ttu-id="a72c2-202">**注**&nbsp;&nbsp;コントロールでコンテナーを折り返すには、リスト ビューの高さを規定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-202">**Note**&nbsp;&nbsp;The height of the list view must be constrained to force the control to wrap the containers.</span></span>

<span data-ttu-id="a72c2-203">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-203">**XAML**</span></span>
```xaml
<ListView Height="100"
          ScrollViewer.HorizontalScrollMode="Enabled" 
          ScrollViewer.HorizontalScrollBarVisibility="Auto"
          ScrollViewer.VerticalScrollMode="Disabled"
          ScrollViewer.VerticalScrollBarVisibility="Hidden">
    <ListView.ItemsPanel>
        <ItemsPanelTemplate>
            <ItemsWrapGrid/>
        </ItemsPanelTemplate>
    </ListView.ItemsPanel>
    <x:String>Item 1</x:String>
    <x:String>Item 2</x:String>
    <x:String>Item 3</x:String>
    <x:String>Item 4</x:String>
    <x:String>Item 5</x:String>
</ListView>
```

<span data-ttu-id="a72c2-204">このリストは次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-204">The resulting list looks like this.</span></span>

![グリッド レイアウトを使ったリスト ビュー](images/listview-itemswrapgrid.png)

<span data-ttu-id="a72c2-206">グループ化したデータをリスト ビューに表示する場合、ItemsPanel によって指定されるのは個々の項目のレイアウト方法ではなく、項目グループのレイアウト方法です。たとえば、前に示した横方向の ItemsStackPanel を使用して、グループ化されたデータを表示する場合、次に示すようにグループは横方向に配置されますが、各グループの項目は縦に重ねて表示されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-206">If you show grouped data in your list view, the ItemsPanel determines how the item groups are layed out, not how the individual items are layed out. For example, if the horizontal ItemsStackPanel shown previously is used to show grouped data, the groups are arranged horizontally, but the items in each group are still stacked vertically, as shown here.</span></span>

![グループ化された横方向のリスト ビュー](images/listview-horizontal-groups.png)

## <a name="item-selection-and-interaction"></a><span data-ttu-id="a72c2-208">項目の選択と操作</span><span class="sxs-lookup"><span data-stu-id="a72c2-208">Item selection and interaction</span></span>

<span data-ttu-id="a72c2-209">ユーザーがリスト ビューを操作する方法は、いくつか選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-209">You can choose from various ways to let a user interact with a list view.</span></span> <span data-ttu-id="a72c2-210">既定では、ユーザーは 1 つの項目を選択できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-210">By default, a user can select a single item.</span></span> <span data-ttu-id="a72c2-211">[SelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectionmode) プロパティを変更することで、複数選択を有効にしたり、選択を無効にしたりできます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-211">You can change the [SelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectionmode) property to enable multi-selection or to disable selection.</span></span> <span data-ttu-id="a72c2-212">[IsItemClickEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.isitemclickenabled) プロパティを設定することで、ユーザーが項目をクリックしたときに項目を選択するのではなく、ボタンと同じように操作を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-212">You can set the [IsItemClickEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.isitemclickenabled) property so that a user clicks an item to invoke an action (like a button) instead of selecting the item.</span></span>

> <span data-ttu-id="a72c2-213">**注**&nbsp;&nbsp; ListView と GridView のどちらも、SelectionMode プロパティについては [ListViewSelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewselectionmode) 列挙値を使用します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-213">**Note**&nbsp;&nbsp;Both ListView and GridView use the [ListViewSelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewselectionmode) enumeration for their SelectionMode properties.</span></span> <span data-ttu-id="a72c2-214">IsItemClickEnabled は既定で **False** であるため、設定する必要があるのはクリック モードを有効にする場合のみです。</span><span class="sxs-lookup"><span data-stu-id="a72c2-214">IsItemClickEnabled is **False** by default, so you need to set it only to enable click mode.</span></span>

<span data-ttu-id="a72c2-215">次の表に、ユーザーがリスト ビューを操作する方法と、その操作に対する応答方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-215">This table shows the ways a user can interact with a list view, and how you can respond to the interaction.</span></span>

<span data-ttu-id="a72c2-216">有効にする操作:</span><span class="sxs-lookup"><span data-stu-id="a72c2-216">To enable this interaction:</span></span> | <span data-ttu-id="a72c2-217">使用する設定:</span><span class="sxs-lookup"><span data-stu-id="a72c2-217">Use these settings:</span></span> | <span data-ttu-id="a72c2-218">処理するイベント:</span><span class="sxs-lookup"><span data-stu-id="a72c2-218">Handle this event:</span></span> | <span data-ttu-id="a72c2-219">選択された項目の取得に使うプロパティ:</span><span class="sxs-lookup"><span data-stu-id="a72c2-219">Use this property to get the selected item:</span></span>
----------------------------|---------------------|--------------------|--------------------------------------------
<span data-ttu-id="a72c2-220">操作なし</span><span class="sxs-lookup"><span data-stu-id="a72c2-220">No interaction</span></span> | <span data-ttu-id="a72c2-221">[SelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectionmode) = **None**、[IsItemClickEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.isitemclickenabled) = **False**</span><span class="sxs-lookup"><span data-stu-id="a72c2-221">[SelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectionmode) = **None**, [IsItemClickEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.isitemclickenabled) = **False**</span></span> | <span data-ttu-id="a72c2-222">なし</span><span class="sxs-lookup"><span data-stu-id="a72c2-222">N/A</span></span> | <span data-ttu-id="a72c2-223">なし</span><span class="sxs-lookup"><span data-stu-id="a72c2-223">N/A</span></span> 
<span data-ttu-id="a72c2-224">単一選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-224">Single selection</span></span> | <span data-ttu-id="a72c2-225">SelectionMode = **Single**、IsItemClickEnabled = **False**</span><span class="sxs-lookup"><span data-stu-id="a72c2-225">SelectionMode = **Single**, IsItemClickEnabled = **False**</span></span> | [<span data-ttu-id="a72c2-226">SelectionChanged</span><span class="sxs-lookup"><span data-stu-id="a72c2-226">SelectionChanged</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) | <span data-ttu-id="a72c2-227">[SelectedItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selecteditem)、[SelectedIndex](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectedindex)</span><span class="sxs-lookup"><span data-stu-id="a72c2-227">[SelectedItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selecteditem), [SelectedIndex](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectedindex)</span></span>  
<span data-ttu-id="a72c2-228">複数選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-228">Multiple selection</span></span> | <span data-ttu-id="a72c2-229">SelectionMode = **Multiple**、IsItemClickEnabled = **False**</span><span class="sxs-lookup"><span data-stu-id="a72c2-229">SelectionMode = **Multiple**, IsItemClickEnabled = **False**</span></span> | [<span data-ttu-id="a72c2-230">SelectionChanged</span><span class="sxs-lookup"><span data-stu-id="a72c2-230">SelectionChanged</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) | [<span data-ttu-id="a72c2-231">SelectedItems</span><span class="sxs-lookup"><span data-stu-id="a72c2-231">SelectedItems</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selecteditems)  
<span data-ttu-id="a72c2-232">拡張選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-232">Extended selection</span></span> | <span data-ttu-id="a72c2-233">SelectionMode = **Extended**、IsItemClickEnabled = **False**</span><span class="sxs-lookup"><span data-stu-id="a72c2-233">SelectionMode = **Extended**, IsItemClickEnabled = **False**</span></span> | [<span data-ttu-id="a72c2-234">SelectionChanged</span><span class="sxs-lookup"><span data-stu-id="a72c2-234">SelectionChanged</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) | [<span data-ttu-id="a72c2-235">SelectedItems</span><span class="sxs-lookup"><span data-stu-id="a72c2-235">SelectedItems</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selecteditems)  
<span data-ttu-id="a72c2-236">Click</span><span class="sxs-lookup"><span data-stu-id="a72c2-236">Click</span></span> | <span data-ttu-id="a72c2-237">SelectionMode = **None**、IsItemClickEnabled = **True**</span><span class="sxs-lookup"><span data-stu-id="a72c2-237">SelectionMode = **None**, IsItemClickEnabled = **True**</span></span> | [<span data-ttu-id="a72c2-238">ItemClick</span><span class="sxs-lookup"><span data-stu-id="a72c2-238">ItemClick</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.itemclick) | <span data-ttu-id="a72c2-239">なし</span><span class="sxs-lookup"><span data-stu-id="a72c2-239">N/A</span></span> 

> <span data-ttu-id="a72c2-240">**注**&nbsp;&nbsp;Windows 10 以降では、IsItemClickEnabled を有効にして ItemClick イベントを発生させる場合でも、SelectionMode を Single、Multiple、Extended のいずれにも設定できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-240">**Note**&nbsp;&nbsp;Starting in Windows 10, you can enable IsItemClickEnabled to raise an ItemClick event while SelectionMode is also set to Single, Multiple, or Extended.</span></span> <span data-ttu-id="a72c2-241">その場合、ItemClick イベントが最初に発生し、次に SelectionChanged イベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-241">If you do this, the ItemClick event is raised first, and then the SelectionChanged event is raised.</span></span> <span data-ttu-id="a72c2-242">ただし ItemClick イベント ハンドラーで別のページに移動するような場合では、SelectionChanged イベントが発生せず、項目が選択されません。</span><span class="sxs-lookup"><span data-stu-id="a72c2-242">In some cases, like if you navigate to another page in the ItemClick event handler, the SelectionChanged event is not raised and the item is not selected.</span></span>

<span data-ttu-id="a72c2-243">次に示すように、このプロパティを XAML またはコードで設定することができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-243">You can set these properties in XAML or in code, as shown here.</span></span>

<span data-ttu-id="a72c2-244">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-244">**XAML**</span></span>
```xaml
<ListView x:Name="myListView" SelectionMode="Multiple"/>

<GridView x:Name="myGridView" SelectionMode="None" IsItemClickEnabled="True"/> 
```

<span data-ttu-id="a72c2-245">**C#**</span><span class="sxs-lookup"><span data-stu-id="a72c2-245">**C#**</span></span>
```csharp
myListView.SelectionMode = ListViewSelectionMode.Multiple; 

myGridView.SelectionMode = ListViewSelectionMode.None;
myGridView.IsItemClickEnabled = true;
```

### <a name="read-only"></a><span data-ttu-id="a72c2-246">読み取り専用かどうか</span><span class="sxs-lookup"><span data-stu-id="a72c2-246">Read-only</span></span>

<span data-ttu-id="a72c2-247">SelectionMode プロパティを **ListViewSelectionMode.None** に設定することで、項目の選択を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-247">You can set the SelectionMode property to **ListViewSelectionMode.None** to disable item selection.</span></span> <span data-ttu-id="a72c2-248">これによりコントロールが読み取り専用モードになり、ユーザーの操作には使われず、データの表示のみに使われます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-248">This puts the control in read only mode, to be used for displaying data, but not for interacting with it.</span></span> <span data-ttu-id="a72c2-249">コントロール自体は無効にならず、項目の選択のみが無効になります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-249">The control itself is not disabled, only item selection is disabled.</span></span>

### <a name="single-selection"></a><span data-ttu-id="a72c2-250">単一選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-250">Single selection</span></span>

<span data-ttu-id="a72c2-251">次の表では、SelectionMode が **Single** の場合のキーボード操作、マウス操作、タッチ操作について説明します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-251">This table describes the keyboard, mouse, and touch interactions when SelectionMode is **Single**.</span></span>

<span data-ttu-id="a72c2-252">修飾キー</span><span class="sxs-lookup"><span data-stu-id="a72c2-252">Modifier key</span></span> | <span data-ttu-id="a72c2-253">操作</span><span class="sxs-lookup"><span data-stu-id="a72c2-253">Interaction</span></span>
-------------|------------
<span data-ttu-id="a72c2-254">なし</span><span class="sxs-lookup"><span data-stu-id="a72c2-254">None</span></span> | <li><span data-ttu-id="a72c2-255">ユーザーはスペース バー、マウスのクリック、タッチ操作のタップを使って 1 つの項目を選択できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-255">A user can select a single item using the space bar, mouse click, or touch tap.</span></span></li>
<span data-ttu-id="a72c2-256">Ctrl</span><span class="sxs-lookup"><span data-stu-id="a72c2-256">Ctrl</span></span> | <li><span data-ttu-id="a72c2-257">ユーザーはスペース バー、マウスのクリック、タッチ操作のタップを使って 1 つの項目の選択を解除できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-257">A user can deselect a single item using the space bar, mouse click, or touch tap.</span></span></li><li><span data-ttu-id="a72c2-258">方向キーを使うと、選択した項目とは関係なくフォーカスを移動できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-258">Using the arrow keys, a user can move focus independently of selection.</span></span></li>

<span data-ttu-id="a72c2-259">SelectionMode が **Single** の場合、[SelectedItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selecteditem) プロパティから選択したデータ項目を取得できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-259">When SelectionMode is **Single**, you can get the selected data item from the [SelectedItem](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selecteditem) property.</span></span> <span data-ttu-id="a72c2-260">[SelectedIndex](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectedindex) プロパティを使って、選択した項目のコレクション内のインデックスを取得できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-260">You can get the index in the collection of the selected item using the [SelectedIndex](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectedindex) property.</span></span> <span data-ttu-id="a72c2-261">項目が選択されていない場合、SelectedItem は **null** になり、SelectedIndex は -1 になります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-261">If no item is selected, SelectedItem is **null**, and SelectedIndex is -1.</span></span> 
 
<span data-ttu-id="a72c2-262">**Items** コレクションに含まれない項目を **SelectedItem** として設定しようとすると、その操作は無視され、SelectedItem が **null** になります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-262">If you try to set an item that is not in the **Items** collection as the **SelectedItem**, the operation is ignored and SelectedItem is**null**.</span></span> <span data-ttu-id="a72c2-263">ただし、リスト内の **Items** の範囲外のインデックスを **SelectedIndex** に設定しようとすると、**System.ArgumentException** 例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-263">However, if you try to set the **SelectedIndex** to an index that's out of the range of the **Items** in the list, a **System.ArgumentException** exception occurs.</span></span> 

### <a name="multiple-selection"></a><span data-ttu-id="a72c2-264">複数選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-264">Multiple selection</span></span>

<span data-ttu-id="a72c2-265">次の表では、SelectionMode が **Multiple** の場合のキーボード操作、マウス操作、タッチ操作について説明します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-265">This table describes the keyboard, mouse, and touch interactions when SelectionMode is **Multiple**.</span></span>

<span data-ttu-id="a72c2-266">修飾キー</span><span class="sxs-lookup"><span data-stu-id="a72c2-266">Modifier key</span></span> | <span data-ttu-id="a72c2-267">操作</span><span class="sxs-lookup"><span data-stu-id="a72c2-267">Interaction</span></span>
-------------|------------
<span data-ttu-id="a72c2-268">なし</span><span class="sxs-lookup"><span data-stu-id="a72c2-268">None</span></span> | <li><span data-ttu-id="a72c2-269">ユーザーは、スペース バー、マウスのクリック、タッチ操作のタップを使って、フォーカスのある項目の選択状態を切り替えることで、複数の項目を選択できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-269">A user can select multiple items using the space bar, mouse click, or touch tap to toggle selection on the focused item.</span></span></li><li><span data-ttu-id="a72c2-270">方向キーを使うと、選択した項目とは関係なくフォーカスを移動できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-270">Using the arrow keys, a user can move focus independently of selection.</span></span></li>
<span data-ttu-id="a72c2-271">Shift</span><span class="sxs-lookup"><span data-stu-id="a72c2-271">Shift</span></span> | <li><span data-ttu-id="a72c2-272">ユーザーは、選択する最初の項目をクリックまたはタップした後、選択する最後の項目をクリックまたはタップすることで、複数の項目を連続的に選択できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-272">A user can select multiple contiguous items by clicking or tapping the first item in the selection and then the last item in the selection.</span></span></li><li><span data-ttu-id="a72c2-273">方向キーを使用すると、Shift キーが押されたときに選択された項目を起点として連続的に選択することができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-273">Using the arrow keys, a user can create a contiguous selection starting with the item selected when Shift is pressed.</span></span></li>

### <a name="extended-selection"></a><span data-ttu-id="a72c2-274">拡張選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-274">Extended selection</span></span>

<span data-ttu-id="a72c2-275">次の表では、SelectionMode が **Extended** の場合のキーボード操作、マウス操作、タッチ操作について説明します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-275">This table describes the keyboard, mouse, and touch interactions when SelectionMode is **Extended**.</span></span>

<span data-ttu-id="a72c2-276">修飾キー</span><span class="sxs-lookup"><span data-stu-id="a72c2-276">Modifier key</span></span> | <span data-ttu-id="a72c2-277">操作</span><span class="sxs-lookup"><span data-stu-id="a72c2-277">Interaction</span></span>
-------------|------------
<span data-ttu-id="a72c2-278">なし</span><span class="sxs-lookup"><span data-stu-id="a72c2-278">None</span></span> | <li><span data-ttu-id="a72c2-279">**Single** の選択と同じです。</span><span class="sxs-lookup"><span data-stu-id="a72c2-279">The behavior is the same as **Single** selection.</span></span></li>
<span data-ttu-id="a72c2-280">Ctrl</span><span class="sxs-lookup"><span data-stu-id="a72c2-280">Ctrl</span></span> | <li><span data-ttu-id="a72c2-281">ユーザーは、スペース バー、マウスのクリック、タッチ操作のタップを使って、フォーカスのある項目の選択状態を切り替えることで、複数の項目を選択できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-281">A user can select multiple items using the space bar, mouse click, or touch tap to toggle selection on the focused item.</span></span></li><li><span data-ttu-id="a72c2-282">方向キーを使うと、選択した項目とは関係なくフォーカスを移動できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-282">Using the arrow keys, a user can move focus independently of selection.</span></span></li>
<span data-ttu-id="a72c2-283">Shift</span><span class="sxs-lookup"><span data-stu-id="a72c2-283">Shift</span></span> | <li><span data-ttu-id="a72c2-284">ユーザーは、選択する最初の項目をクリックまたはタップした後、選択する最後の項目をクリックまたはタップすることで、複数の項目を連続的に選択できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-284">A user can select multiple contiguous items by clicking or tapping the first item in the selection and then the last item in the selection.</span></span></li><li><span data-ttu-id="a72c2-285">方向キーを使用すると、Shift キーが押されたときに選択された項目を起点として連続的に選択することができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-285">Using the arrow keys, a user can create a contiguous selection starting with the item selected when Shift is pressed.</span></span></li>

<span data-ttu-id="a72c2-286">SelectionMode が **Multiple** または **Extended** の場合、選択したデータ項目を [SelectedItems](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selecteditems) プロパティから取得できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-286">When SelectionMode is **Multiple** or **Extended**, you can get the selected data items from the [SelectedItems](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selecteditems) property.</span></span> 

<span data-ttu-id="a72c2-287">**SelectedIndex**、**SelectedItem**、**SelectedItems** の各プロパティは同期されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-287">The **SelectedIndex**, **SelectedItem**, and **SelectedItems** properties are synchronized.</span></span> <span data-ttu-id="a72c2-288">たとえば、SelectedIndex を -1 に設定すると、SelectedItem は **null** に設定され、SelectedItems が空になります。SelectedItem を **null** に設定すると、SelectedIndex が -1 に設定され、SelectedItems が空になります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-288">For example, if you set SelectedIndex to -1, SelectedItem is set to **null** and SelectedItems is empty; if you set SelectedItem to **null**, SelectedIndex is set to -1 and SelectedItems is empty.</span></span>

<span data-ttu-id="a72c2-289">複数選択モードの場合、**SelectedItem** には最初に選択された項目が含まれ、**Selectedindex** には最初に選択した項目のインデックスが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-289">In multi-select mode, **SelectedItem** contains the item that was selected first, and **Selectedindex** contains the index of the item that was selected first.</span></span> 

### <a name="respond-to-selection-changes"></a><span data-ttu-id="a72c2-290">選択範囲の変更への対応</span><span class="sxs-lookup"><span data-stu-id="a72c2-290">Respond to selection changes</span></span>

<span data-ttu-id="a72c2-291">リスト ビューにおける選択内容の変更に対応するには、[SelectionChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-291">To respond to selection changes in a list view, handle the [SelectionChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) event.</span></span> <span data-ttu-id="a72c2-292">イベント ハンドラーのコードでは、[SelectionChangedEventArgs.AddedItems](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.selectionchangedeventargs.addeditems) プロパティから選ばれた項目の一覧を取得できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-292">In the event handler code, you can get the list of selected items from the [SelectionChangedEventArgs.AddedItems](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.selectionchangedeventargs.addeditems) property.</span></span> <span data-ttu-id="a72c2-293">選択が解除された項目は、[SelectionChangedEventArgs.RemovedItems](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.selectionchangedeventargs.removeditems) プロパティから取得できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-293">You can get any items that were deselected from the [SelectionChangedEventArgs.RemovedItems](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.selectionchangedeventargs.removeditems) property.</span></span> <span data-ttu-id="a72c2-294">ユーザーが Shift キーを押しながら一連の項目を選択しない限り、AddedItems コレクションと RemovedItems コレクションに含まれる項目の数は 1 個までになります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-294">The AddedItems and RemovedItems collections contain at most 1 item unless the user selects a range of items by holding down the Shift key.</span></span>

<span data-ttu-id="a72c2-295">次の例では、**SelectionChanged** イベントを処理してさまざまな項目コレクションにアクセスする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-295">This example shows how to handle the **SelectionChanged** event and access the various items collections.</span></span>

<span data-ttu-id="a72c2-296">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-296">**XAML**</span></span>
```xaml
<StackPanel HorizontalAlignment="Right">
    <ListView x:Name="listView1" SelectionMode="Multiple" 
              SelectionChanged="ListView1_SelectionChanged">
        <x:String>Item 1</x:String>
        <x:String>Item 2</x:String>
        <x:String>Item 3</x:String>
        <x:String>Item 4</x:String>
        <x:String>Item 5</x:String>
    </ListView>
    <TextBlock x:Name="selectedItem"/>
    <TextBlock x:Name="selectedIndex"/>
    <TextBlock x:Name="selectedItemCount"/>
    <TextBlock x:Name="addedItems"/>
    <TextBlock x:Name="removedItems"/>
</StackPanel> 
```

<span data-ttu-id="a72c2-297">**C#**</span><span class="sxs-lookup"><span data-stu-id="a72c2-297">**C#**</span></span>
```csharp
private void ListView1_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    if (listView1.SelectedItem != null)
    {
        selectedItem.Text = 
            "Selected item: " + listView1.SelectedItem.ToString();
    }
    else
    {
        selectedItem.Text = 
            "Selected item: null";
    }
    selectedIndex.Text = 
        "Selected index: " + listView1.SelectedIndex.ToString();
    selectedItemCount.Text = 
        "Items selected: " + listView1.SelectedItems.Count.ToString();
    addedItems.Text = 
        "Added: " + e.AddedItems.Count.ToString();
    removedItems.Text = 
        "Removed: " + e.RemovedItems.Count.ToString();
}
```

### <a name="click-mode"></a><span data-ttu-id="a72c2-298">クリック モード</span><span class="sxs-lookup"><span data-stu-id="a72c2-298">Click mode</span></span>

<span data-ttu-id="a72c2-299">項目を選択するのではなく、ボタンのように項目をクリックできるように、リスト ビューを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-299">You can change a list view so that a user clicks items like buttons instead of selecting them.</span></span> <span data-ttu-id="a72c2-300">この方法は、たとえば、リストまたはグリッド内の項目をユーザーがクリックしたときに新しいページに移動するアプリで便利です。</span><span class="sxs-lookup"><span data-stu-id="a72c2-300">For example, this is useful when your app navigates to a new page when your user clicks an item in a list or grid.</span></span> <span data-ttu-id="a72c2-301">この動作を有効にするには、次のように設定します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-301">To enable this behavior:</span></span>
- <span data-ttu-id="a72c2-302">**SelectionMode** を **None** に設定します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-302">Set **SelectionMode** to **None**.</span></span>
- <span data-ttu-id="a72c2-303">**IsItemClickEnabled** を **true** に設定します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-303">Set **IsItemClickEnabled** to **true**.</span></span>
- <span data-ttu-id="a72c2-304">ユーザーが項目をクリックしたときに処理を実行する **ItemClick** イベントを設定します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-304">Handle the **ItemClick** event to do something when your user clicks an item.</span></span>

<span data-ttu-id="a72c2-305">クリックできる項目を持つリスト ビューの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-305">Here's a list view with clickable items.</span></span> <span data-ttu-id="a72c2-306">ItemClick イベント ハンドラーのコードによって、新しいページに移動します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-306">The code in the ItemClick event handler navigates to a new page.</span></span>

<span data-ttu-id="a72c2-307">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-307">**XAML**</span></span>
```xaml
<ListView SelectionMode="None"
          IsItemClickEnabled="True" 
          ItemClick="ListView1_ItemClick">
    <x:String>Page 1</x:String>
    <x:String>Page 2</x:String>
    <x:String>Page 3</x:String>
    <x:String>Page 4</x:String>
    <x:String>Page 5</x:String>
</ListView>
```

<span data-ttu-id="a72c2-308">**C#**</span><span class="sxs-lookup"><span data-stu-id="a72c2-308">**C#**</span></span>
```csharp
private void ListView1_ItemClick(object sender, ItemClickEventArgs e)
{
    switch (e.ClickedItem.ToString())
    {
        case "Page 1":
            this.Frame.Navigate(typeof(Page1));
            break;

        case "Page 2":
            this.Frame.Navigate(typeof(Page2));
            break;

        case "Page 3":
            this.Frame.Navigate(typeof(Page3));
            break;

        case "Page 4":
            this.Frame.Navigate(typeof(Page4));
            break;

        case "Page 5":
            this.Frame.Navigate(typeof(Page5));
            break;

        default:
            break;
    }
}
```

### <a name="select-a-range-of-items-programmatically"></a><span data-ttu-id="a72c2-309">プログラムを使った一定範囲の項目の選択</span><span class="sxs-lookup"><span data-stu-id="a72c2-309">Select a range of items programmatically</span></span>

<span data-ttu-id="a72c2-310">場合によっては、プログラムからリスト ビューの項目の選択を操作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-310">Sometimes, you need to manipulate a list view’s item selection programmatically.</span></span> <span data-ttu-id="a72c2-311">たとえば、ユーザーがリスト内のすべての項目を選択できるように、 **[すべて選択]** ボタンを用意する場合があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-311">For example, you might have a **Select all** button to let a user select all items in a list.</span></span> <span data-ttu-id="a72c2-312">この場合、SelectedItems コレクションの項目を 1 つずつ追加したり削除したりすることは、一般的に効率的とは言えません。</span><span class="sxs-lookup"><span data-stu-id="a72c2-312">In this case, it’s usually not very efficient to add and remove items from the SelectedItems collection one by one.</span></span> <span data-ttu-id="a72c2-313">各項目を変更するたびに SelectionChanged イベントが発生し、インデックス値を操作するのではなく項目を直接操作すると、項目の仮想化が解除されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-313">Each item change causes a SelectionChanged event to occur, and when you work with the items directly instead of working with index values, the item is de-virtualized.</span></span>

<span data-ttu-id="a72c2-314">[SelectAll](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectall)、[SelectRange](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectrange)、[DeselectRange](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.deselectrange) の各メソッドを使用すると、SelectedItems プロパティを使用する場合よりも効率的に選択内容を変更できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-314">The [SelectAll](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectall), [SelectRange](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectrange), and [DeselectRange](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.deselectrange) methods provide a more efficient way to modify the selection than using the SelectedItems property.</span></span> <span data-ttu-id="a72c2-315">このメソッドでは、項目インデックスの範囲を使って選択と選択解除を行います。</span><span class="sxs-lookup"><span data-stu-id="a72c2-315">These methods select or deselect using ranges of item indexes.</span></span> <span data-ttu-id="a72c2-316">インデックスのみを使うため、仮想化された項目は仮想化の状態を維持します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-316">Items that are virtualized remain virtualized, because only the index is used.</span></span> <span data-ttu-id="a72c2-317">元の選択状態に関係なく、指定範囲のすべての項目が選択 (または選択解除) されます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-317">All items in the specified range are selected (or deselected), regardless of their original selection state.</span></span> <span data-ttu-id="a72c2-318">SelectionChanged イベントは、このメソッドを 1 回呼び出すたびに 1 回のみ発生します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-318">The SelectionChanged event occurs only once for each call to these methods.</span></span>

> <span data-ttu-id="a72c2-319">**重要**&nbsp;&nbsp;このメソッドは、SelectionMode プロパティが Multiple または Extended に設定されているときにのみ呼び出してください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-319">**Important**&nbsp;&nbsp;You should call these methods only when the SelectionMode property is set to Multiple or Extended.</span></span> <span data-ttu-id="a72c2-320">SelectionMode が Single または None のときに SelectRange を呼び出すと、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-320">If you call SelectRange when the SelectionMode is Single or None, an exception is thrown.</span></span>

<span data-ttu-id="a72c2-321">インデックスの範囲を使って項目を選択する場合、[SelectedRanges](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectedranges) プロパティを使って、リスト内の選択範囲をすべて取得します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-321">When you select items using index ranges, use the [SelectedRanges](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase.selectedranges) property to get all selected ranges in the list.</span></span>

<span data-ttu-id="a72c2-322">ItemsSource に [IItemsRangeInfo](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.iitemsrangeinfo) を実装し、このようなメソッドを使って選択内容を変更する場合、SelectionChangedEventArgs には **AddedItems** プロパティと **RemovedItems** プロパティが設定されません。</span><span class="sxs-lookup"><span data-stu-id="a72c2-322">If the ItemsSource implements [IItemsRangeInfo](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.iitemsrangeinfo), and you use these methods to modify the selection, the **AddedItems** and **RemovedItems** properties are not set in the SelectionChangedEventArgs.</span></span> <span data-ttu-id="a72c2-323">このプロパティを設定するには、項目オブジェクトの仮想化を解除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a72c2-323">Setting these properties requires de-virtualizing the item object.</span></span> <span data-ttu-id="a72c2-324">代わりに **SelectedRanges** プロパティを使って項目を取得します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-324">Use the **SelectedRanges** property to get the items instead.</span></span>

<span data-ttu-id="a72c2-325">SelectAll メソッドを呼び出すと、コレクション内のすべての項目を選択できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-325">You can select all items in a collection by calling the SelectAll method.</span></span> <span data-ttu-id="a72c2-326">ただし、すべての項目の選択を解除するメソッドはありません。</span><span class="sxs-lookup"><span data-stu-id="a72c2-326">However, there is no corresponding method to deselect all items.</span></span> <span data-ttu-id="a72c2-327">すべての項目の選択を解除するには、DeselectRange を呼び出して [ItemIndexRange](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.itemindexrange) を渡します。このとき、[FirstIndex](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.itemindexrange.firstindex) 値を 0 とし、[Length](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.itemindexrange.length) 値をコレクション内の項目数と同じ値にします。</span><span class="sxs-lookup"><span data-stu-id="a72c2-327">You can deselect all items by calling DeselectRange and passing an [ItemIndexRange](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.itemindexrange) with a [FirstIndex](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.itemindexrange.firstindex) value of 0 and a [Length](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.itemindexrange.length) value equal to the number of items in the collection.</span></span> 

<span data-ttu-id="a72c2-328">**XAML**</span><span class="sxs-lookup"><span data-stu-id="a72c2-328">**XAML**</span></span>
```xaml
<StackPanel Width="160">
    <Button Content="Select all" Click="SelectAllButton_Click"/>
    <Button Content="Deselect all" Click="DeselectAllButton_Click"/>
    <ListView x:Name="listView1" SelectionMode="Multiple">
        <x:String>Item 1</x:String>
        <x:String>Item 2</x:String>
        <x:String>Item 3</x:String>
        <x:String>Item 4</x:String>
        <x:String>Item 5</x:String>
    </ListView>
</StackPanel>
```

<span data-ttu-id="a72c2-329">**C#**</span><span class="sxs-lookup"><span data-stu-id="a72c2-329">**C#**</span></span>
```csharp
private void SelectAllButton_Click(object sender, RoutedEventArgs e)
{
    if (listView1.SelectionMode == ListViewSelectionMode.Multiple ||
        listView1.SelectionMode == ListViewSelectionMode.Extended)
    {
        listView1.SelectAll();
    }
}

private void DeselectAllButton_Click(object sender, RoutedEventArgs e)
{
    if (listView1.SelectionMode == ListViewSelectionMode.Multiple ||
        listView1.SelectionMode == ListViewSelectionMode.Extended)
    {
        listView1.DeselectRange(new ItemIndexRange(0, (uint)listView1.Items.Count));
    }
}
```

<span data-ttu-id="a72c2-330">選択した項目の外観を変更する方法について詳しくは、「[項目コンテナーやテンプレート](item-containers-templates.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-330">For info about how to change the look of selected items, see [Item containers and templates](item-containers-templates.md).</span></span>

### <a name="drag-and-drop"></a><span data-ttu-id="a72c2-331">ドラッグ アンド ドロップ</span><span class="sxs-lookup"><span data-stu-id="a72c2-331">Drag and drop</span></span>

<span data-ttu-id="a72c2-332">ListView コントロールと GridView コントロールは、項目内、項目間、および他の ListView コントロールと GridView コントロール間での項目のドラッグ アンド ドロップをサポートします。</span><span class="sxs-lookup"><span data-stu-id="a72c2-332">ListView and GridView controls support drag and drop of items within themselves, and between themselves and other ListView and GridView controls.</span></span> <span data-ttu-id="a72c2-333">ドラッグ アンド ドロップのパターンの実装について詳しくは、「[ドラッグ アンド ドロップ](https://docs.microsoft.com/windows/uwp/design/input/drag-and-drop)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a72c2-333">For more info about implementing the drag and drop pattern, see [Drag and drop](https://docs.microsoft.com/windows/uwp/design/input/drag-and-drop).</span></span> 

## <a name="get-the-sample-code"></a><span data-ttu-id="a72c2-334">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="a72c2-334">Get the sample code</span></span>

- <span data-ttu-id="a72c2-335">[XAML ListView と GridView のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlListView)- ListView と GridView コントロールを示しています。</span><span class="sxs-lookup"><span data-stu-id="a72c2-335">[XAML ListView and GridView sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlListView) - Demonstrates the ListView and GridView controls.</span></span>
- <span data-ttu-id="a72c2-336">[XAML ドラッグ アンド ドロップのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlDragAndDrop) - ListView コントロールを使用したドラッグ アンド ドロップを示します。</span><span class="sxs-lookup"><span data-stu-id="a72c2-336">[XAML Drag and drop sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlDragAndDrop) - Demonstrates drag and drop with the ListView control.</span></span>
- <span data-ttu-id="a72c2-337">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="a72c2-337">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a72c2-338">関連記事</span><span class="sxs-lookup"><span data-stu-id="a72c2-338">Related articles</span></span>

- [<span data-ttu-id="a72c2-339">リスト</span><span class="sxs-lookup"><span data-stu-id="a72c2-339">Lists</span></span>](lists.md)
- [<span data-ttu-id="a72c2-340">項目コンテナーとテンプレート</span><span class="sxs-lookup"><span data-stu-id="a72c2-340">Item containers and templates</span></span>](item-containers-templates.md)
- [<span data-ttu-id="a72c2-341">ドラッグ アンド ドロップ</span><span class="sxs-lookup"><span data-stu-id="a72c2-341">Drag and drop</span></span>](https://docs.microsoft.com/windows/uwp/app-to-app/drag-and-drop)
