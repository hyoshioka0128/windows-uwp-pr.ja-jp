---
description: XAML コントロールに効果的にバインドできるプロパティは、*監視可能な*プロパティと呼ばれます。 このトピックでは、監視可能なプロパティを実装および使用する方法と、XAML コントロールをバインドする方法を示します。
title: 'XAML コントロール: C++/WinRT プロパティへのバインド'
ms.date: 04/24/2019
ms.topic: article
keywords: windows 10, uwp, 標準, c++, cpp, winrt, プロジェクション, XAML, コントロール, バインド, プロパティ
ms.localizationpriority: medium
ms.openlocfilehash: 2fe5c03eebd2b68e98ae908ea4624471fbd2b3d2
ms.sourcegitcommit: d23dab1533893b7fe0f01ca6eb273edfac4705e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65627668"
---
# <a name="xaml-controls-bind-to-a-cwinrt-property"></a><span data-ttu-id="3da4a-105">XAML コントロール: C++/WinRT プロパティへのバインド</span><span class="sxs-lookup"><span data-stu-id="3da4a-105">XAML controls; bind to a C++/WinRT property</span></span>
<span data-ttu-id="3da4a-106">XAML コントロールに効果的にバインドできるプロパティは、*監視可能な*プロパティと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-106">A property that can be effectively bound to a XAML control is known as an *observable* property.</span></span> <span data-ttu-id="3da4a-107">この概念は、*オブザーバー パターン*と呼ばれるソフトウェアの設計パターンに基づいています。</span><span class="sxs-lookup"><span data-stu-id="3da4a-107">This idea is based on the software design pattern known as the *observer pattern*.</span></span> <span data-ttu-id="3da4a-108">このトピックで監視可能なプロパティを実装する方法を示しています。 [C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)、および XAML コントロールをバインドする方法。</span><span class="sxs-lookup"><span data-stu-id="3da4a-108">This topic shows how to implement observable properties in [C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt), and how to bind XAML controls to them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3da4a-109">C++/WinRT でランタイム クラスを使用および作成する方法についての理解をサポートするために重要な概念と用語については、「[C++/WinRT での API の使用](consume-apis.md)」と「[C++/WinRT での作成者 API](author-apis.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3da4a-109">For essential concepts and terms that support your understanding of how to consume and author runtime classes with C++/WinRT, see [Consume APIs with C++/WinRT](consume-apis.md) and [Author APIs with C++/WinRT](author-apis.md).</span></span>

## <a name="what-does-observable-mean-for-a-property"></a><span data-ttu-id="3da4a-110">プロパティの*監視可能*とはどういう意味ですか?</span><span class="sxs-lookup"><span data-stu-id="3da4a-110">What does *observable* mean for a property?</span></span>
<span data-ttu-id="3da4a-111">たとえば、**BookSku** という名前のランタイム クラスに **Title** という名前のプロパティがあるとします。</span><span class="sxs-lookup"><span data-stu-id="3da4a-111">Let's say that a runtime class named **BookSku** has a property named **Title**.</span></span> <span data-ttu-id="3da4a-112">**Title** の値が変わるたびに **BookSku** が [**INotifyPropertyChanged::PropertyChanged**](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) イベントを発生させることを選択する場合、**Title** は監視可能なプロパティです。</span><span class="sxs-lookup"><span data-stu-id="3da4a-112">If **BookSku** chooses to raise the [**INotifyPropertyChanged::PropertyChanged**](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) event whenever the value of **Title** changes, then **Title** is an observable property.</span></span> <span data-ttu-id="3da4a-113">そのプロパティ (あれば) のどれが監視可能かを決定するのは **BookSku** の動作 (イベントを発生させるまたは発生させない) です。</span><span class="sxs-lookup"><span data-stu-id="3da4a-113">It's the behavior of **BookSku** (raising or not raising the event) that determines which, if any, of its properties are observable.</span></span>

<span data-ttu-id="3da4a-114">XAML テキスト要素、またはコントロールでは、更新された値を取得して、新しい値を表示するためにそれ自体を更新することで、これらのイベントをバインドし、処理することができます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-114">A XAML text element, or control, can bind to, and handle, these events by retrieving the updated value(s) and then updating itself to show the new value.</span></span>

> [!NOTE]
> <span data-ttu-id="3da4a-115">インストールと使用について、 C++WinRT Visual Studio Extension (VSIX) と (をまとめてプロジェクト テンプレートを提供し、ビルドのサポート)、NuGet パッケージを参照してください。 [Visual Studio のサポートC++/WinRT](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-xaml-the-vsix-extension-and-the-nuget-package)します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-115">For info about installing and using the C++/WinRT Visual Studio Extension (VSIX) and the NuGet package (which together provide project template and build support), see [Visual Studio support for C++/WinRT](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-xaml-the-vsix-extension-and-the-nuget-package).</span></span>

## <a name="create-a-blank-app-bookstore"></a><span data-ttu-id="3da4a-116">空のアプリ (Bookstore) を作成する</span><span class="sxs-lookup"><span data-stu-id="3da4a-116">Create a Blank App (Bookstore)</span></span>
<span data-ttu-id="3da4a-117">まず、Microsoft Visual Studio で、新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-117">Begin by creating a new project in Microsoft Visual Studio.</span></span> <span data-ttu-id="3da4a-118">作成、**空のアプリ (C++/WinRT)** プロジェクト、および名前を付けます*書店*します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-118">Create a **Blank App (C++/WinRT)** project, and name it *Bookstore*.</span></span>

<span data-ttu-id="3da4a-119">監視可能なタイトルのプロパティを持つブックを表すための新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-119">We're going to author a new class to represent a book that has an observable title property.</span></span> <span data-ttu-id="3da4a-120">同じコンパイル ユニット内のクラスを作成および使用しています。</span><span class="sxs-lookup"><span data-stu-id="3da4a-120">We're authoring and consuming the class within the same compilation unit.</span></span> <span data-ttu-id="3da4a-121">ただし、XAML からこのクラスへバインドできるようにしたいため、ランタイム クラスにします。</span><span class="sxs-lookup"><span data-stu-id="3da4a-121">But we want to be able to bind to this class from XAML, and for that reason it's going to be a runtime class.</span></span> <span data-ttu-id="3da4a-122">また、この作成と使用のどちらにも C++/WinRT を使用します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-122">And we're going to use C++/WinRT to both author and consume it.</span></span>

<span data-ttu-id="3da4a-123">新しいランタイム クラスの作成の最初の手順では、新しい **Midl ファイル (.idl)** 項目をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-123">The first step in authoring a new runtime class is to add a new **Midl File (.idl)** item to the project.</span></span> <span data-ttu-id="3da4a-124">「`BookSku.idl`」という名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-124">Name it `BookSku.idl`.</span></span> <span data-ttu-id="3da4a-125">`BookSku.idl` の既定のコンテンツを削除し、このランタイム クラスの宣言に貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-125">Delete the default contents of `BookSku.idl`, and paste in this runtime class declaration.</span></span>

```idl
// BookSku.idl
namespace Bookstore
{
    runtimeclass BookSku : Windows.UI.Xaml.Data.INotifyPropertyChanged
    {
        String Title;
    }
}
```

> [!NOTE]
> <span data-ttu-id="3da4a-126">ビュー モデル クラス&mdash;実際には、アプリケーションで宣言された任意のランタイム クラス&mdash;基底クラスから派生していない必要があります。</span><span class="sxs-lookup"><span data-stu-id="3da4a-126">Your view model classes&mdash;in fact, any runtime class that you declare in your application&mdash;need not derive from a base class.</span></span> <span data-ttu-id="3da4a-127">**BookSku**上で宣言されたクラスがその例を示します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-127">The **BookSku** class declared above is an example of that.</span></span> <span data-ttu-id="3da4a-128">インターフェイスを実装しますが、任意の基本クラスから派生していません。</span><span class="sxs-lookup"><span data-stu-id="3da4a-128">It implements an interface, but it doesn't derive from any base class.</span></span>
>
> <span data-ttu-id="3da4a-129">アプリケーションで宣言された任意のランタイム クラスを*は*ベースからの派生クラスと呼ばれる、*コンポーザブル*クラス。</span><span class="sxs-lookup"><span data-stu-id="3da4a-129">Any runtime class that you declare in the application that *does* derive from a base class is known as a *composable* class.</span></span> <span data-ttu-id="3da4a-130">構成可能なクラスに関する制約があります。</span><span class="sxs-lookup"><span data-stu-id="3da4a-130">And there are constraints around composable classes.</span></span> <span data-ttu-id="3da4a-131">アプリケーションに渡す、 [Windows アプリ認定キット](../debug-test-perf/windows-app-certification-kit.md)Visual Studio では、Microsoft Store での送信を検証するために使用するテスト (ため Microsoft Store に正常に取り込まれるアプリケーションの)、コンポーザブル クラスは、Windows の基本クラスから最終的に派生する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3da4a-131">For an application to pass the [Windows App Certification Kit](../debug-test-perf/windows-app-certification-kit.md) tests used by Visual Studio and by the Microsoft Store to validate submissions (and therefore for the application to be successfully ingested into the Microsoft Store), a composable class must ultimately derive from a Windows base class.</span></span> <span data-ttu-id="3da4a-132">つまり、継承階層の非常にルートにあるクラスは、Windows.\* 名前空間で生成された型である必要があります。</span><span class="sxs-lookup"><span data-stu-id="3da4a-132">Meaning that the class at the very root of the inheritance hierarchy must be a type originating in a Windows.\* namespace.</span></span> <span data-ttu-id="3da4a-133">ランタイム クラスを基底クラスから派生する必要は場合&mdash;を実装する例を**BindableBase**クラスから派生するは、ビュー モデルのすべての&mdash;から派生できます[ **Windows.UI.Xaml.DependencyObject**](/uwp/api/windows.ui.xaml.dependencyobject)します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-133">If you do need to derive a runtime class from a base class&mdash;for example, to implement a **BindableBase** class for all of your view models to derive from&mdash;then you can derive from [**Windows.UI.Xaml.DependencyObject**](/uwp/api/windows.ui.xaml.dependencyobject).</span></span>
>
> <span data-ttu-id="3da4a-134">ビュー モデルは、ビューの抽象化と表示 (XAML マークアップ) に直接バインドされているためです。</span><span class="sxs-lookup"><span data-stu-id="3da4a-134">A view model is an abstraction of a view, and so it's bound directly to the view (the XAML markup).</span></span> <span data-ttu-id="3da4a-135">データ モデルは、データの抽象化と、ビュー モデルからのみ使用され、XAML に直接バインドされていないことができます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-135">A data model is an abstraction of data, and it's consumed only from your view models, and not bound directly to XAML.</span></span> <span data-ttu-id="3da4a-136">そのため、ランタイム クラス、としてではなく C++ 構造体またはクラスとしては、データ モデルを宣言できます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-136">So, you can declare your data models not as runtime classes, but as C++ structs or classes.</span></span> <span data-ttu-id="3da4a-137">MIDL、内で宣言する必要はありませんし、自由に好きな継承階層を使用します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-137">They don't need to be declared in MIDL, and you're free to use whatever inheritance hierarchy you like.</span></span>

<span data-ttu-id="3da4a-138">ファイルを保存し、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="3da4a-138">Save the file and build the project.</span></span> <span data-ttu-id="3da4a-139">ビルド プロセス中に、`midl.exe` ツールが実行されて、ランタイム クラスを記述する Windows ランタイム メタデータ ファイル (`\Bookstore\Debug\Bookstore\Unmerged\BookSku.winmd`) が作成されます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-139">During the build process, the `midl.exe` tool is run to create a Windows Runtime metadata file (`\Bookstore\Debug\Bookstore\Unmerged\BookSku.winmd`) describing the runtime class.</span></span> <span data-ttu-id="3da4a-140">次に、`cppwinrt.exe` ツールが実行され、ランタイム クラスの作成と使用をサポートするソース コード ファイルが生成されます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-140">Then, the `cppwinrt.exe` tool is run to generate source code files to support you in authoring and consuming your runtime class.</span></span> <span data-ttu-id="3da4a-141">これらのファイルには、IDL で宣言した **BookSku** ランタイム クラスの実装を開始するためのスタブが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3da4a-141">These files include stubs to get you started implementing the **BookSku** runtime class that you declared in your IDL.</span></span> <span data-ttu-id="3da4a-142">これらのスタブは `\Bookstore\Bookstore\Generated Files\sources\BookSku.h` と `BookSku.cpp` です。</span><span class="sxs-lookup"><span data-stu-id="3da4a-142">Those stubs are `\Bookstore\Bookstore\Generated Files\sources\BookSku.h` and `BookSku.cpp`.</span></span>

<span data-ttu-id="3da4a-143">プロジェクト ノードを右クリックし、をクリックして**ファイル エクスプ ローラーでフォルダーを開く**します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-143">Right-click the project node and click **Open Folder in File Explorer**.</span></span> <span data-ttu-id="3da4a-144">これは、ファイル エクスプ ローラーでプロジェクト フォルダーを開きます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-144">This opens the project folder in File Explorer.</span></span> <span data-ttu-id="3da4a-145">スタブ ファイルをコピー、`BookSku.h`と`BookSku.cpp`から、`\Bookstore\Bookstore\Generated Files\sources\`フォルダー、プロジェクト フォルダーにある`\Bookstore\Bookstore\`します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-145">There, copy the stub files `BookSku.h` and `BookSku.cpp` from the `\Bookstore\Bookstore\Generated Files\sources\` folder and into the project folder, which is `\Bookstore\Bookstore\`.</span></span> <span data-ttu-id="3da4a-146">**ソリューション エクスプ ローラー**、プロジェクト ノードを選択したことを確認します**すべてのファイル**がオンにします。</span><span class="sxs-lookup"><span data-stu-id="3da4a-146">In **Solution Explorer**, with the project node selected, make sure **Show All Files** is toggled on.</span></span> <span data-ttu-id="3da4a-147">コピーしたスタブ ファイルを右クリックし、**[プロジェクトに含める]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="3da4a-147">Right-click the stub files that you copied, and click **Include In Project**.</span></span>

## <a name="implement-booksku"></a><span data-ttu-id="3da4a-148">**BookSku** を実装する</span><span class="sxs-lookup"><span data-stu-id="3da4a-148">Implement **BookSku**</span></span>
<span data-ttu-id="3da4a-149">ここで、`\Bookstore\Bookstore\BookSku.h` と `BookSku.cpp` を開いてランタイム クラスを実装してみましょう。</span><span class="sxs-lookup"><span data-stu-id="3da4a-149">Now, let's open `\Bookstore\Bookstore\BookSku.h` and `BookSku.cpp` and implement our runtime class.</span></span> <span data-ttu-id="3da4a-150">`BookSku.h` で、[**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring) を取るコンストラクター、タイトル文字列を格納するためのプライベート メンバー、およびタイトルが変更されたときに発生させるイベントのための別のプライベート メンバーを追加します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-150">In `BookSku.h`, add a constructor that takes a [**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring), a private member to store the title string, and another for the event that we'll raise when the title changes.</span></span> <span data-ttu-id="3da4a-151">これらの変更を行った後、`BookSku.h`ようになります。</span><span class="sxs-lookup"><span data-stu-id="3da4a-151">After making these changes, your `BookSku.h` will look like this.</span></span>

```cppwinrt
// BookSku.h
#pragma once
#include "BookSku.g.h"

namespace winrt::Bookstore::implementation
{
    struct BookSku : BookSkuT<BookSku>
    {
        BookSku() = delete;
        BookSku(winrt::hstring const& title);

        winrt::hstring Title();
        void Title(winrt::hstring const& value);
        winrt::event_token PropertyChanged(Windows::UI::Xaml::Data::PropertyChangedEventHandler const& value);
        void PropertyChanged(winrt::event_token const& token);
    
    private:
        winrt::hstring m_title;
        winrt::event<Windows::UI::Xaml::Data::PropertyChangedEventHandler> m_propertyChanged;
    };
}
```

<span data-ttu-id="3da4a-152">`BookSku.cpp` では、次のように関数を実装します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-152">In `BookSku.cpp`, implement the functions like this.</span></span>

```cppwinrt
// BookSku.cpp
#include "pch.h"
#include "BookSku.h"
#include "BookSku.g.cpp"

namespace winrt::Bookstore::implementation
{
    BookSku::BookSku(winrt::hstring const& title) : m_title{ title }
    {
    }

    winrt::hstring BookSku::Title()
    {
        return m_title;
    }

    void BookSku::Title(winrt::hstring const& value)
    {
        if (m_title != value)
        {
            m_title = value;
            m_propertyChanged(*this, Windows::UI::Xaml::Data::PropertyChangedEventArgs{ L"Title" });
        }
    }

    winrt::event_token BookSku::PropertyChanged(Windows::UI::Xaml::Data::PropertyChangedEventHandler const& handler)
    {
        return m_propertyChanged.add(handler);
    }

    void BookSku::PropertyChanged(winrt::event_token const& token)
    {
        m_propertyChanged.remove(token);
    }
}
```

<span data-ttu-id="3da4a-153">**タイトル**かどうか、値が設定されていますが、現在の値を異なるを確認しましたミューテーターの関数。</span><span class="sxs-lookup"><span data-stu-id="3da4a-153">In the **Title** mutator function, we check whether a value is being set that's different from the current value.</span></span> <span data-ttu-id="3da4a-154">そのため、タイトルを更新するとを発生させることも、 [ **INotifyPropertyChanged::PropertyChanged** ](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged)変更されたプロパティの名前と同じ引数を持つイベント。</span><span class="sxs-lookup"><span data-stu-id="3da4a-154">And, if so, we update the title and also raise the [**INotifyPropertyChanged::PropertyChanged**](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) event with an argument equal to the name of the property that has changed.</span></span> <span data-ttu-id="3da4a-155">これにより、ユーザー インターフェイス (UI) はどのプロパティの値を再クエリするのか分かるようになります。</span><span class="sxs-lookup"><span data-stu-id="3da4a-155">This is so that the user-interface (UI) will know which property's value to re-query.</span></span>

## <a name="declare-and-implement-bookstoreviewmodel"></a><span data-ttu-id="3da4a-156">**BookstoreViewModel** を宣言および実装する</span><span class="sxs-lookup"><span data-stu-id="3da4a-156">Declare and implement **BookstoreViewModel**</span></span>
<span data-ttu-id="3da4a-157">メイン XAML ページが、メイン ビュー モデルにバインドします。</span><span class="sxs-lookup"><span data-stu-id="3da4a-157">Our main XAML page is going to bind to a main view model.</span></span> <span data-ttu-id="3da4a-158">またそのビュー モデルは、**BookSku** 型のいずれかを含む、いくつかのプロパティを持つようになります。</span><span class="sxs-lookup"><span data-stu-id="3da4a-158">And that view model is going to have several properties, including one of type **BookSku**.</span></span> <span data-ttu-id="3da4a-159">この手順では、メイン ビュー モデル ランタイム クラスを宣言および実装します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-159">In this step, we'll declare and implement our main view model runtime class.</span></span>

<span data-ttu-id="3da4a-160">`BookstoreViewModel.idl` という名前の新しい **Midl ファイル (.idl)** 項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-160">Add a new **Midl File (.idl)** item named `BookstoreViewModel.idl`.</span></span>

```idl
// BookstoreViewModel.idl
import "BookSku.idl";

namespace Bookstore
{
    runtimeclass BookstoreViewModel
    {
        BookSku BookSku{ get; };
    }
}
```

<span data-ttu-id="3da4a-161">保存してビルドします。</span><span class="sxs-lookup"><span data-stu-id="3da4a-161">Save and build.</span></span> <span data-ttu-id="3da4a-162">`Generated Files\sources` フォルダーから `BookstoreViewModel.h` と `BookstoreViewModel.cpp` をプロジェクト フォルダーにコピーし、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-162">Copy `BookstoreViewModel.h` and `BookstoreViewModel.cpp` from the `Generated Files\sources` folder into the project folder, and include them in the project.</span></span> <span data-ttu-id="3da4a-163">これらのファイルを開き、次に示すように、ランタイム クラスを実装します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-163">Open those files and implement the runtime class as shown below.</span></span> <span data-ttu-id="3da4a-164">注方法で、 `BookstoreViewModel.h`、含まれています`BookSku.h`の実装の種類を宣言する**BookSku** (これは**winrt::Bookstore::implementation::BookSku**)。</span><span class="sxs-lookup"><span data-stu-id="3da4a-164">Note how, in `BookstoreViewModel.h`, we're including `BookSku.h`, which declares the implementation type for **BookSku** (which is **winrt::Bookstore::implementation::BookSku**).</span></span> <span data-ttu-id="3da4a-165">削除する予定していると`= default`既定のコンス トラクターから。</span><span class="sxs-lookup"><span data-stu-id="3da4a-165">And we're removing `= default` from the default constructor.</span></span>

```cppwinrt
// BookstoreViewModel.h
#pragma once
#include "BookstoreViewModel.g.h"
#include "BookSku.h"

namespace winrt::Bookstore::implementation
{
    struct BookstoreViewModel : BookstoreViewModelT<BookstoreViewModel>
    {
        BookstoreViewModel();

        Bookstore::BookSku BookSku();

    private:
        Bookstore::BookSku m_bookSku{ nullptr };
    };
}
```

```cppwinrt
// BookstoreViewModel.cpp
#include "pch.h"
#include "BookstoreViewModel.h"
#include "BookstoreViewModel.g.cpp"

namespace winrt::Bookstore::implementation
{
    BookstoreViewModel::BookstoreViewModel()
    {
        m_bookSku = winrt::make<Bookstore::implementation::BookSku>(L"Atticus");
    }

    Bookstore::BookSku BookstoreViewModel::BookSku()
    {
        return m_bookSku;
    }
}
```

> [!NOTE]
> <span data-ttu-id="3da4a-166">型`m_bookSku`射影の型は、(**winrt::Bookstore::BookSku**) とで使用するテンプレート パラメーター [ **winrt::make** ](/uwp/cpp-ref-for-winrt/make)が、実装の種類 (**winrt::Bookstore::implementation::BookSku**)。</span><span class="sxs-lookup"><span data-stu-id="3da4a-166">The type of `m_bookSku` is the projected type (**winrt::Bookstore::BookSku**), and the template parameter that you use with [**winrt::make**](/uwp/cpp-ref-for-winrt/make) is the implementation type (**winrt::Bookstore::implementation::BookSku**).</span></span> <span data-ttu-id="3da4a-167">この場合も、**[make]** は投影型のインスタンスを返します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-167">Even so, **make** returns an instance of the projected type.</span></span>

## <a name="add-a-property-of-type-bookstoreviewmodel-to-mainpage"></a><span data-ttu-id="3da4a-168">**BookstoreViewModel** 型のプロパティを **MainPage** に追加する</span><span class="sxs-lookup"><span data-stu-id="3da4a-168">Add a property of type **BookstoreViewModel** to **MainPage**</span></span>
<span data-ttu-id="3da4a-169">`MainPage.idl` を開きます。ここでメインの UI ページを表すランタイム クラスを宣言しています。</span><span class="sxs-lookup"><span data-stu-id="3da4a-169">Open `MainPage.idl`, which declares the runtime class that represents our main UI page.</span></span> <span data-ttu-id="3da4a-170">インポート ステートメントを追加して `BookstoreViewModel.idl` をインポートし、**BookstoreViewModel** 型の MainViewModel という名前の読み取り専用プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-170">Add an import statement to import `BookstoreViewModel.idl`, and add a read-only property named MainViewModel of type **BookstoreViewModel**.</span></span> <span data-ttu-id="3da4a-171">削除しても、 **MyProperty**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="3da4a-171">Also remove the **MyProperty** property.</span></span> <span data-ttu-id="3da4a-172">また、`import`ディレクティブでは、以下のリスト。</span><span class="sxs-lookup"><span data-stu-id="3da4a-172">Also note the `import` directive in the listing below.</span></span>

```idl
// MainPage.idl
import "BookstoreViewModel.idl";

namespace Bookstore
{
    runtimeclass MainPage : Windows.UI.Xaml.Controls.Page
    {
        MainPage();
        BookstoreViewModel MainViewModel{ get; };
    }
}
```

<span data-ttu-id="3da4a-173">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-173">Save the file.</span></span> <span data-ttu-id="3da4a-174">現時点では、完了するまで、プロジェクトをビルドしませんをソース コード ファイルを再生成しているため、有用なことは、今すぐ構築、 **MainPage**ランタイム クラスが実装されている (`\Bookstore\Bookstore\Generated Files\sources\MainPage.h`と`MainPage.cpp`)。</span><span class="sxs-lookup"><span data-stu-id="3da4a-174">The project won't build to completion at the moment, but building now is a useful thing to do because it regenerates the source code files in which the **MainPage** runtime class is implemented (`\Bookstore\Bookstore\Generated Files\sources\MainPage.h` and `MainPage.cpp`).</span></span> <span data-ttu-id="3da4a-175">これを今すぐビルドしてみてください。</span><span class="sxs-lookup"><span data-stu-id="3da4a-175">So go ahead and build now.</span></span> <span data-ttu-id="3da4a-176">この段階で表示するビルド エラーが **'MainViewModel': 'winrt::Bookstore::implementation::MainPage' のメンバーではない**します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-176">The build error you can expect to see at this stage is **'MainViewModel': is not a member of 'winrt::Bookstore::implementation::MainPage'**.</span></span>

<span data-ttu-id="3da4a-177">Include を省略した場合`BookstoreViewModel.idl`(の一覧を参照してください`MainPage.idl`上)、エラーが表示されます**を指定してください\<"MainViewModel"近く**。</span><span class="sxs-lookup"><span data-stu-id="3da4a-177">If you omit the include of `BookstoreViewModel.idl` (see the listing of `MainPage.idl` above), then you'll see the error **expecting \< near "MainViewModel"**.</span></span> <span data-ttu-id="3da4a-178">別のヒントは、同じ名前空間のすべての種類のままにすることを確認する: コードの一覧に表示される名前空間。</span><span class="sxs-lookup"><span data-stu-id="3da4a-178">Another tip is to make sure that you leave all types in the same namespace: the namespace that's shown in the code listings.</span></span>

<span data-ttu-id="3da4a-179">表示される予定ですエラーを解決するようになりましたする必要がありますのアクセサーのスタブをコピー、 **MainViewModel**生成されたファイルからのプロパティ (`\Bookstore\Bookstore\Generated Files\sources\MainPage.h`と`MainPage.cpp`) に`\Bookstore\Bookstore\MainPage.h`と`MainPage.cpp`します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-179">To resolve the error that we expect to see, you'll now need to copy the accessor stubs for the **MainViewModel** property out of the generated files (`\Bookstore\Bookstore\Generated Files\sources\MainPage.h` and `MainPage.cpp`) and into `\Bookstore\Bookstore\MainPage.h` and `MainPage.cpp`.</span></span> <span data-ttu-id="3da4a-180">そのための手順は次に説明します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-180">The steps to do that are described next.</span></span>

<span data-ttu-id="3da4a-181">`\Bookstore\Bookstore\MainPage.h`、含める`BookstoreViewModel.h`の実装の種類を宣言する**BookstoreViewModel** (これは**winrt::Bookstore::implementation::BookstoreViewModel**)。</span><span class="sxs-lookup"><span data-stu-id="3da4a-181">In `\Bookstore\Bookstore\MainPage.h`, include `BookstoreViewModel.h`, which declares the implementation type for **BookstoreViewModel** (which is **winrt::Bookstore::implementation::BookstoreViewModel**).</span></span> <span data-ttu-id="3da4a-182">ビュー モデルを格納するプライベート メンバーを追加します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-182">Add a private member to store the view model.</span></span> <span data-ttu-id="3da4a-183">プロパティのアクセサー関数 (およびメンバー m_mainViewModel) が、射影された型の観点から実装されることに注意してください。 **BookstoreViewModel** (これは**Bookstore::BookstoreViewModel**)。</span><span class="sxs-lookup"><span data-stu-id="3da4a-183">Note that the property accessor function (and the member m_mainViewModel) is implemented in terms of the projected type for **BookstoreViewModel** (which is **Bookstore::BookstoreViewModel**).</span></span> <span data-ttu-id="3da4a-184">M_mainViewModel を受け取るコンス トラクター オーバー ロードを使用して作成するため、アプリケーションと同じプロジェクト (コンパイル単位) での実装の種類は`nullptr_t`します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-184">The implementation type is in the same project (compilation unit) as the application, so we construct m_mainViewModel via the constructor overload that takes `nullptr_t`.</span></span> <span data-ttu-id="3da4a-185">削除しても、 **MyProperty**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="3da4a-185">Also remove the **MyProperty** property.</span></span>

```cppwinrt
// MainPage.h
...
#include "BookstoreViewModel.h"
...
namespace winrt::Bookstore::implementation
{
    struct MainPage : MainPageT<MainPage>
    {
        MainPage();

        Bookstore::BookstoreViewModel MainViewModel();

        void ClickHandler(Windows::Foundation::IInspectable const&, Windows::UI::Xaml::RoutedEventArgs const&);

    private:
        Bookstore::BookstoreViewModel m_mainViewModel{ nullptr };
    };
}
...
```

<span data-ttu-id="3da4a-186">`\Bookstore\Bookstore\MainPage.cpp`、呼び出す[ **winrt::make** ](/uwp/cpp-ref-for-winrt/make) (実装の種類) で m_mainViewModel に射影された型の新しいインスタンスを割り当てる。</span><span class="sxs-lookup"><span data-stu-id="3da4a-186">In `\Bookstore\Bookstore\MainPage.cpp`, call [**winrt::make**](/uwp/cpp-ref-for-winrt/make) (with the implementation type) to assign a new instance of the projected type to m_mainViewModel.</span></span> <span data-ttu-id="3da4a-187">ブックのタイトルの初期値を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-187">Assign an initial value for the book's title.</span></span> <span data-ttu-id="3da4a-188">MainViewModel プロパティのアクセサーを実装します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-188">Implement the accessor for the MainViewModel property.</span></span> <span data-ttu-id="3da4a-189">最後に、ボタンのイベント ハンドラーでブックのタイトルを更新します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-189">And finally, update the book's title in the button's event handler.</span></span> <span data-ttu-id="3da4a-190">削除しても、 **MyProperty**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="3da4a-190">Also remove the **MyProperty** property.</span></span>

```cppwinrt
// MainPage.cpp
#include "pch.h"
#include "MainPage.h"
#include "MainPage.g.cpp"

using namespace winrt;
using namespace Windows::UI::Xaml;

namespace winrt::Bookstore::implementation
{
    MainPage::MainPage()
    {
        m_mainViewModel = winrt::make<Bookstore::implementation::BookstoreViewModel>();
        InitializeComponent();
    }

    void MainPage::ClickHandler(Windows::Foundation::IInspectable const& /* sender */, Windows::UI::Xaml::RoutedEventArgs const& /* args */)
    {
        MainViewModel().BookSku().Title(L"To Kill a Mockingbird");
    }

    Bookstore::BookstoreViewModel MainPage::MainViewModel()
    {
        return m_mainViewModel;
    }
}
```

## <a name="bind-the-button-to-the-title-property"></a><span data-ttu-id="3da4a-191">**Title** プロパティにボタンをバインドする</span><span class="sxs-lookup"><span data-stu-id="3da4a-191">Bind the button to the **Title** property</span></span>
<span data-ttu-id="3da4a-192">メイン UI ページの XAML マークアップが含まれている `MainPage.xaml` を開きます。</span><span class="sxs-lookup"><span data-stu-id="3da4a-192">Open `MainPage.xaml`, which contains the XAML markup for our main UI page.</span></span> <span data-ttu-id="3da4a-193">次の一覧に示すように、ボタンから名前を削除し、変更、**コンテンツ**バインディング式にリテラルからプロパティ値。</span><span class="sxs-lookup"><span data-stu-id="3da4a-193">As shown in the listing below, remove the name from the button, and change its **Content** property value from a literal to a binding expression.</span></span> <span data-ttu-id="3da4a-194">バインド式の `Mode=OneWay` プロパティをメモします (ビュー モデルから UI へ一方向)。</span><span class="sxs-lookup"><span data-stu-id="3da4a-194">Note the `Mode=OneWay` property on the binding expression (one-way from the view model to the UI).</span></span> <span data-ttu-id="3da4a-195">そのプロパティが無いと、UI はプロパティの変更イベントに応答しません。</span><span class="sxs-lookup"><span data-stu-id="3da4a-195">Without that property, the UI will not respond to property changed events.</span></span>

```xaml
<Button Click="ClickHandler" Content="{x:Bind MainViewModel.BookSku.Title, Mode=OneWay}"/>
```

<span data-ttu-id="3da4a-196">ここでプロジェクトをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-196">Now build and run the project.</span></span> <span data-ttu-id="3da4a-197">ボタンをクリックして**クリック** イベント ハンドラーを実行します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-197">Click the button to execute the **Click** event handler.</span></span> <span data-ttu-id="3da4a-198">そのハンドラーがブックのタイトル ミューテーター関数を呼び出します。そのミューテーターがイベントを発生させるので、UI は **Title** プロパティが変更されたことがわかります。ボタンはそのプロパティの値を再クエリして、そのボタンの **Content** 値を更新します。</span><span class="sxs-lookup"><span data-stu-id="3da4a-198">That handler calls the book's title mutator function; that mutator raises an event to let the UI know that the **Title** property has changed; and the button re-queries that property's value to update its own **Content** value.</span></span>

## <a name="using-the-binding-markup-extension-with-cwinrt"></a><span data-ttu-id="3da4a-199">{バインド} マークアップ拡張機能を使用して c++/cli WinRT</span><span class="sxs-lookup"><span data-stu-id="3da4a-199">Using the {Binding} markup extension with C++/WinRT</span></span>
<span data-ttu-id="3da4a-200">現在リリースされているバージョンの C++/cli を実装する必要があります {binding} マークアップ拡張機能を使用するには、WinRT、 [ICustomPropertyProvider](/uwp/api/windows.ui.xaml.data.icustompropertyprovider)と[ICustomProperty](/uwp/api/windows.ui.xaml.data.icustomproperty)インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="3da4a-200">For the currently released version of C++/WinRT, in order to be able to use the {Binding} markup extension you'll need to implement the [ICustomPropertyProvider](/uwp/api/windows.ui.xaml.data.icustompropertyprovider) and [ICustomProperty](/uwp/api/windows.ui.xaml.data.icustomproperty) interfaces.</span></span>

## <a name="important-apis"></a><span data-ttu-id="3da4a-201">重要な API</span><span class="sxs-lookup"><span data-stu-id="3da4a-201">Important APIs</span></span>
* [<span data-ttu-id="3da4a-202">INotifyPropertyChanged::PropertyChanged</span><span class="sxs-lookup"><span data-stu-id="3da4a-202">INotifyPropertyChanged::PropertyChanged</span></span>](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged)
* [<span data-ttu-id="3da4a-203">winrt::make 関数テンプレート</span><span class="sxs-lookup"><span data-stu-id="3da4a-203">winrt::make function template</span></span>](/uwp/cpp-ref-for-winrt/make)

## <a name="related-topics"></a><span data-ttu-id="3da4a-204">関連トピック</span><span class="sxs-lookup"><span data-stu-id="3da4a-204">Related topics</span></span>
* [<span data-ttu-id="3da4a-205">C++/WinRT で API を使用する</span><span class="sxs-lookup"><span data-stu-id="3da4a-205">Consume APIs with C++/WinRT</span></span>](consume-apis.md)
* [<span data-ttu-id="3da4a-206">C++/WinRT で API を作成する</span><span class="sxs-lookup"><span data-stu-id="3da4a-206">Author APIs with C++/WinRT</span></span>](author-apis.md)
