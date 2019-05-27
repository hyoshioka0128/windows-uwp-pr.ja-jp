---
description: XAML アイテム コントロールに効果的にバインドできるコレクションは、*監視可能な*コレクションと呼ばれます。 このトピックでは、監視可能なコレクションを実装および使用する方法と、それに XAML アイテム コントロールをバインドする方法を示します。
title: 'XAML アイテム コントロール: C++/WinRT コレクションへのバインド'
ms.date: 04/24/2019
ms.topic: article
keywords: Windows 10、uwp、標準、c++、cpp、winrt、プロジェクション、XAML、コントロール、バインド、コレクション
ms.localizationpriority: medium
ms.openlocfilehash: 7669c6536f28d5f979567f5b433dbf614800bec3
ms.sourcegitcommit: d23dab1533893b7fe0f01ca6eb273edfac4705e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65627676"
---
# <a name="xaml-items-controls-bind-to-a-cwinrt-collection"></a><span data-ttu-id="6fdd9-105">XAML アイテム コントロール: C++/WinRT コレクションへのバインド</span><span class="sxs-lookup"><span data-stu-id="6fdd9-105">XAML items controls; bind to a C++/WinRT collection</span></span>

<span data-ttu-id="6fdd9-106">XAML アイテム コントロールに効果的にバインドできるコレクションは、*監視可能な*コレクションと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-106">A collection that can be effectively bound to a XAML items control is known as an *observable* collection.</span></span> <span data-ttu-id="6fdd9-107">この概念は、*オブザーバー パターン*と呼ばれるソフトウェアの設計パターンに基づいています。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-107">This idea is based on the software design pattern known as the *observer pattern*.</span></span> <span data-ttu-id="6fdd9-108">このトピックでは、監視可能なコレクションを実装する方法を示します[C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)、および XAML をバインドする方法にコントロールの項目。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-108">This topic shows how to implement observable collections in [C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt), and how to bind XAML items controls to them.</span></span>

<span data-ttu-id="6fdd9-109">このトピックの手順に従うしたいかどうかは、最初に記載されているプロジェクトを作成することをお勧めします。 [XAML コントロール; にバインドをC++/WinRT プロパティ](binding-property.md)します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-109">If you want to follow along with this topic, then we recommend that you first create the project that's described in [XAML controls; bind to a C++/WinRT property](binding-property.md).</span></span> <span data-ttu-id="6fdd9-110">このトピックでは、そのプロジェクトにより多くのコードを追加し、そのトピックで説明する概念に追加します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-110">This topic adds more code to that project, and it adds to the concepts explained in that topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fdd9-111">C++/WinRT でランタイム クラスを使用および作成する方法についての理解をサポートするために重要な概念と用語については、「[C++/WinRT での API の使用](consume-apis.md)」と「[C++/WinRT での作成者 API](author-apis.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-111">For essential concepts and terms that support your understanding of how to consume and author runtime classes with C++/WinRT, see [Consume APIs with C++/WinRT](consume-apis.md) and [Author APIs with C++/WinRT](author-apis.md).</span></span>

## <a name="what-does-observable-mean-for-a-collection"></a><span data-ttu-id="6fdd9-112">コレクションの*監視可能*とはどういう意味ですか?</span><span class="sxs-lookup"><span data-stu-id="6fdd9-112">What does *observable* mean for a collection?</span></span>
<span data-ttu-id="6fdd9-113">コレクションを表すランタイム クラスが、要素が追加されるまたは削除されるたびに [**IObservableVector&lt;T&gt;:: VectorChanged**](/uwp/api/windows.foundation.collections.iobservablevector-1.vectorchanged) イベントを発生することを選択する場合、そのランタイム クラスは監視可能なコレクションです。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-113">If a runtime class that represents a collection chooses to raise the [**IObservableVector&lt;T&gt;::VectorChanged**](/uwp/api/windows.foundation.collections.iobservablevector-1.vectorchanged) event whenever an element is added to it or removed from it, then the runtime class is an observable collection.</span></span> <span data-ttu-id="6fdd9-114">XAML アイテム コントロールでは、更新されたコレクションを取得して、現在の要素を表示するためにそれ自体を更新することで、これらのイベントをバインドし、処理することができます。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-114">A XAML items control can bind to, and handle, these events by retrieving the updated collection and then updating itself to show the current elements.</span></span>

> [!NOTE]
> <span data-ttu-id="6fdd9-115">インストールと使用について、 C++WinRT Visual Studio Extension (VSIX) と (をまとめてプロジェクト テンプレートを提供し、ビルドのサポート)、NuGet パッケージを参照してください。 [Visual Studio のサポートC++/WinRT](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-xaml-the-vsix-extension-and-the-nuget-package)します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-115">For info about installing and using the C++/WinRT Visual Studio Extension (VSIX) and the NuGet package (which together provide project template and build support), see [Visual Studio support for C++/WinRT](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-xaml-the-vsix-extension-and-the-nuget-package).</span></span>

## <a name="add-a-bookskus-collection-to-bookstoreviewmodel"></a><span data-ttu-id="6fdd9-116">**BookSkus** コレクションを **BookstoreViewModel** に追加する</span><span class="sxs-lookup"><span data-stu-id="6fdd9-116">Add a **BookSkus** collection to **BookstoreViewModel**</span></span>

<span data-ttu-id="6fdd9-117">「[XAML コントロール、C++/WinRT プロパティへのバインド](binding-property.md)」では、**BookSku** 型のプロパティをメイン ビュー モデルに追加しました。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-117">In [XAML controls; bind to a C++/WinRT property](binding-property.md), we added a property of type **BookSku** to our main view model.</span></span> <span data-ttu-id="6fdd9-118">この手順で使用して、 [ **winrt::single_threaded_observable_vector** ](/uwp/cpp-ref-for-winrt/single-threaded-observable-vector)の observablecollection を実装するためにファクトリ関数テンプレート**BookSku**で、同じビューのモデル。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-118">In this step, we'll use the [**winrt::single_threaded_observable_vector**](/uwp/cpp-ref-for-winrt/single-threaded-observable-vector) factory function template to help us implement an observable collection of **BookSku** on the same view model.</span></span>

<span data-ttu-id="6fdd9-119">`BookstoreViewModel.idl` で新しいプロパティを宣言します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-119">Declare a new property in `BookstoreViewModel.idl`.</span></span>

```idl
// BookstoreViewModel.idl
...
runtimeclass BookstoreViewModel
{
    BookSku BookSku{ get; };
    Windows.Foundation.Collections.IObservableVector<IInspectable> BookSkus{ get; };
}
...
```

> [!IMPORTANT]
> <span data-ttu-id="6fdd9-120">上の MIDL 3.0 一覧での種類、 **BookSkus**プロパティは[ **IObservableVector** ](/uwp/api/windows.foundation.collections.ivector_t_)の[ **IInspectable**](/windows/desktop/api/inspectable/nn-inspectable-iinspectable).</span><span class="sxs-lookup"><span data-stu-id="6fdd9-120">In the MIDL 3.0 listing above, note that the type of the **BookSkus** property is [**IObservableVector**](/uwp/api/windows.foundation.collections.ivector_t_) of [**IInspectable**](/windows/desktop/api/inspectable/nn-inspectable-iinspectable).</span></span> <span data-ttu-id="6fdd9-121">項目のソース、バインドがこのトピックの次のセクションで、 [ **ListBox** ](/uwp/api/windows.ui.xaml.controls.listbox)に**BookSkus**します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-121">In the next section of this topic, we'll be binding the items source of a [**ListBox**](/uwp/api/windows.ui.xaml.controls.listbox) to **BookSkus**.</span></span> <span data-ttu-id="6fdd9-122">リスト ボックスは、アイテム コントロールを正しく設定して、 [ **ItemsControl.ItemsSource** ](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource)プロパティ、型の値に設定する必要があります**IObservableVector** (または**IVector**) の**IInspectable**、やなどの相互運用型の[ **IBindableObservableVector**](/uwp/api/windows.ui.xaml.interop.ibindableobservablevector)します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-122">A list box is an items control, and to correctly set the [**ItemsControl.ItemsSource**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) property, you need to set it to a value of type **IObservableVector** (or **IVector**) of **IInspectable**, or of an interoperability type such as [**IBindableObservableVector**](/uwp/api/windows.ui.xaml.interop.ibindableobservablevector).</span></span>

<span data-ttu-id="6fdd9-123">保存してビルドします。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-123">Save and build.</span></span> <span data-ttu-id="6fdd9-124">コピーからアクセサー スタブ`BookstoreViewModel.h`と`BookstoreViewModel.cpp`で、`\Bookstore\Bookstore\Generated Files\sources`フォルダー (詳細については、前のトピックを参照してください。 [XAML コントロール; にバインドをC++/WinRT プロパティ](binding-property.md))。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-124">Copy the accessor stubs from `BookstoreViewModel.h` and `BookstoreViewModel.cpp` in the `\Bookstore\Bookstore\Generated Files\sources` folder (for more details, see the previous topic, [XAML controls; bind to a C++/WinRT property](binding-property.md)).</span></span> <span data-ttu-id="6fdd9-125">次のようにこれらのアクセサー スタブを実装します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-125">Implement those accessor stubs like this.</span></span>

```cppwinrt
// BookstoreViewModel.h
...
struct BookstoreViewModel : BookstoreViewModelT<BookstoreViewModel>
{
    BookstoreViewModel();

    Bookstore::BookSku BookSku();

    Windows::Foundation::Collections::IObservableVector<Windows::Foundation::IInspectable> BookSkus();

private:
    Bookstore::BookSku m_bookSku{ nullptr };
    Windows::Foundation::Collections::IObservableVector<Windows::Foundation::IInspectable> m_bookSkus;
};
...
```

```cppwinrt
// BookstoreViewModel.cpp
...
BookstoreViewModel::BookstoreViewModel()
{
    m_bookSku = winrt::make<Bookstore::implementation::BookSku>(L"Atticus");
    m_bookSkus = winrt::single_threaded_observable_vector<Windows::Foundation::IInspectable>();
    m_bookSkus.Append(m_bookSku);
}

Bookstore::BookSku BookstoreViewModel::BookSku()
{
    return m_bookSku;
}

Windows::Foundation::Collections::IObservableVector<Windows::Foundation::IInspectable> BookstoreViewModel::BookSkus()
{
    return m_bookSkus;
}
...
```

## <a name="bind-a-listbox-to-the-bookskus-property"></a><span data-ttu-id="6fdd9-126">**BookSkus** プロパティに ListBox をバインドします。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-126">Bind a ListBox to the **BookSkus** property</span></span>
<span data-ttu-id="6fdd9-127">メイン UI ページの XAML マークアップが含まれている `MainPage.xaml` を開きます。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-127">Open `MainPage.xaml`, which contains the XAML markup for our main UI page.</span></span> <span data-ttu-id="6fdd9-128">**Button** と同じ **StackPanel** 内に次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-128">Add the following markup inside the same **StackPanel** as the **Button**.</span></span>

```xaml
<ListBox ItemsSource="{x:Bind MainViewModel.BookSkus}">
    <ItemsControl.ItemTemplate>
        <DataTemplate x:DataType="local:BookSku">
            <TextBlock Text="{x:Bind Title, Mode=OneWay}"/>
        </DataTemplate>
    </ItemsControl.ItemTemplate>
</ListBox>
```

<span data-ttu-id="6fdd9-129">`MainPage.cpp` で、**クリック** イベント ハンドラーにコードの行を追加してブックをコレクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-129">In `MainPage.cpp`, add a line of code to the **Click** event handler to append a book to the collection.</span></span>

```cppwinrt
// MainPage.cpp
...
void MainPage::ClickHandler(IInspectable const&, RoutedEventArgs const&)
{
    MainViewModel().BookSku().Title(L"To Kill a Mockingbird");
    MainViewModel().BookSkus().Append(winrt::make<Bookstore::implementation::BookSku>(L"Moby Dick"));
}
...
```

<span data-ttu-id="6fdd9-130">ここでプロジェクトをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-130">Now build and run the project.</span></span> <span data-ttu-id="6fdd9-131">ボタンをクリックして**クリック** イベント ハンドラーを実行します。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-131">Click the button to execute the **Click** event handler.</span></span> <span data-ttu-id="6fdd9-132">**Append** の実装によりイベントが発生し、コレクションが変更されたことを UI が把握できるようにすることが分かります。**ListBox** はその独自の **Items** 値を更新するためにコレクションを再クエリします。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-132">We saw that the implementation of **Append** raises an event to let the UI know that the collection has changed; and the **ListBox** re-queries the collection to update its own **Items** value.</span></span> <span data-ttu-id="6fdd9-133">前と同様に、ブックのいずれかのタイトルが変わります。このタイトル変更は、ボタンとリスト ボックス内の両方に反映されます。</span><span class="sxs-lookup"><span data-stu-id="6fdd9-133">Just as before, the title of one of the books changes; and that title change is reflected both on the button and in the list box.</span></span>

## <a name="important-apis"></a><span data-ttu-id="6fdd9-134">重要な API</span><span class="sxs-lookup"><span data-stu-id="6fdd9-134">Important APIs</span></span>
* [<span data-ttu-id="6fdd9-135">IObservableVector&lt;T&gt;:: VectorChanged</span><span class="sxs-lookup"><span data-stu-id="6fdd9-135">IObservableVector&lt;T&gt;::VectorChanged</span></span>](/uwp/api/windows.foundation.collections.iobservablevector-1.vectorchanged)
* [<span data-ttu-id="6fdd9-136">winrt::make 関数テンプレート</span><span class="sxs-lookup"><span data-stu-id="6fdd9-136">winrt::make function template</span></span>](/uwp/cpp-ref-for-winrt/make)

## <a name="related-topics"></a><span data-ttu-id="6fdd9-137">関連トピック</span><span class="sxs-lookup"><span data-stu-id="6fdd9-137">Related topics</span></span>
* [<span data-ttu-id="6fdd9-138">C++/WinRT で API を使用する</span><span class="sxs-lookup"><span data-stu-id="6fdd9-138">Consume APIs with C++/WinRT</span></span>](consume-apis.md)
* [<span data-ttu-id="6fdd9-139">C++/WinRT で API を作成する</span><span class="sxs-lookup"><span data-stu-id="6fdd9-139">Author APIs with C++/WinRT</span></span>](author-apis.md)
