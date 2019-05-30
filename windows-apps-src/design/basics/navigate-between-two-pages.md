---
Description: ユニバーサル Windows プラットフォーム (UWP) アプリで基本的な 2 つのページ間のピア ツー ピア ナビゲーションを有効にする方法について説明します。
title: 2 ページ間でのピア ツー ピアのナビゲーション
ms.assetid: 0A364C8B-715F-4407-9426-92267E8FB525
label: Peer-to-peer navigation between two pages
template: detail.hbs
op-migration-status: ready
ms.date: 07/13/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
dev_langs:
- csharp
- cppwinrt
- cpp
ms.openlocfilehash: 3bc377e87d01106a1a2e7157dbe08f1ab022f52a
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66361056"
---
# <a name="implement-navigation-between-two-pages"></a><span data-ttu-id="a1572-104">2 ページ間でのナビゲーションを実装する</span><span class="sxs-lookup"><span data-stu-id="a1572-104">Implement navigation between two pages</span></span>

<span data-ttu-id="a1572-105">フレームおよびページを使用した、アプリでの基本的なピア ツー ピアのナビゲーションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a1572-105">Learn how to use a frame and pages to enable basic peer-to-peer navigation in your app.</span></span> 

> <span data-ttu-id="a1572-106">**重要な API**:[**Windows.UI.Xaml.Controls.Frame** ](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame)クラス、 [ **Windows.UI.Xaml.Controls.Page** ](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page)クラス、 [ **Windows.UI.Xaml.Navigation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation)名前空間</span><span class="sxs-lookup"><span data-stu-id="a1572-106">**Important APIs**: [**Windows.UI.Xaml.Controls.Frame**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame) class, [**Windows.UI.Xaml.Controls.Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) class, [**Windows.UI.Xaml.Navigation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation) namespace</span></span>

![ピア ツー ピアのナビゲーション](images/peertopeer.png)

## <a name="1-create-a-blank-app"></a><span data-ttu-id="a1572-108">1. 空のアプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="a1572-108">1. Create a blank app</span></span>

1.  <span data-ttu-id="a1572-109">Microsoft Visual Studio のメニューで、 **[ファイル]**  >  **[新しいプロジェクト]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-109">On the Microsoft Visual Studio menu, choose **File** > **New Project**.</span></span>
2.  <span data-ttu-id="a1572-110">**[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual C#]**  >  **[Windows]**  >  **[ユニバーサル]** ノード、または **[Visual C++]**  >  **[Windows]**  >  **[ユニバーサル]** ノードの順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-110">In the left pane of the **New Project** dialog box, choose the **Visual C#** > **Windows** > **Universal** or the **Visual C++** > **Windows** > **Universal** node.</span></span>
3.  <span data-ttu-id="a1572-111">中央のウィンドウで、 **[空のアプリケーション]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-111">In the center pane, choose **Blank App**.</span></span>
4.  <span data-ttu-id="a1572-112">**[名前]** ボックスに「**NavApp1**」と入力し、 **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-112">In the **Name** box, enter **NavApp1**, and then choose the **OK** button.</span></span>
    <span data-ttu-id="a1572-113">ソリューションが作られ、プロジェクト ファイルが**ソリューション エクスプローラー**に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-113">The solution is created, and the project files appear in **Solution Explorer**.</span></span>
5.  <span data-ttu-id="a1572-114">プログラムを実行するには、メニューから **[デバッグ]**  >  **[デバッグの開始]** の順にクリックするか、F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="a1572-114">To run the program, choose **Debug** > **Start Debugging** from the menu, or press F5.</span></span>
    <span data-ttu-id="a1572-115">空白のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-115">A blank page is displayed.</span></span>
6.  <span data-ttu-id="a1572-116">デバッグを終了して Visual Studio に戻るには、アプリを終了するか、メニューから **[デバッグの停止]** クリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-116">To stop debugging and return to Visual Studio, exit the app, or click **Stop Debugging** from the menu.</span></span>

## <a name="2-add-basic-pages"></a><span data-ttu-id="a1572-117">2. 基本ページの追加</span><span class="sxs-lookup"><span data-stu-id="a1572-117">2. Add basic pages</span></span>

<span data-ttu-id="a1572-118">次に、プロジェクトにページを 2 つ追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-118">Next, add two pages to the project.</span></span>

1.  <span data-ttu-id="a1572-119">**ソリューション エクスプローラー**で、 **[BlankApp]** プロジェクト ノードを右クリックして、ショートカット メニューを開きます。</span><span class="sxs-lookup"><span data-stu-id="a1572-119">In **Solution Explorer**, right-click the **BlankApp** project node to open the shortcut menu.</span></span>
2.  <span data-ttu-id="a1572-120">ショートカット メニューで **[追加]**  >  **[新しい項目]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-120">Choose **Add** > **New Item** from the shortcut menu.</span></span>
3.  <span data-ttu-id="a1572-121">**[新しい項目の追加]** ダイアログ ボックスの中央のウィンドウで、 **[空白のページ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-121">In the **Add New Item** dialog box, choose **Blank Page** in the middle pane.</span></span>
4.  <span data-ttu-id="a1572-122">**[名前]** ボックスに「**Page1**」(または「**Page2**」) と入力し、 **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-122">In the **Name** box, enter **Page1** (or **Page2**) and press the **Add** button.</span></span>
5. <span data-ttu-id="a1572-123">手順 1 ～ 4 を繰り返して、2 つ目のページを追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-123">Repeat steps 1-4 to add the second page.</span></span>

<span data-ttu-id="a1572-124">これで、NavApp1 プロジェクトの一部としてこれらのファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-124">Now, these files should be listed as part of your NavApp1 project.</span></span>

<table>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="a1572-125">C#</span><span class="sxs-lookup"><span data-stu-id="a1572-125">C#</span></span></th>
<th align="left"><span data-ttu-id="a1572-126">C++</span><span class="sxs-lookup"><span data-stu-id="a1572-126">C++</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="vertical-align:top;"><ul>
<li><span data-ttu-id="a1572-127">Page1.xaml</span><span class="sxs-lookup"><span data-stu-id="a1572-127">Page1.xaml</span></span></li>
<li><span data-ttu-id="a1572-128">Page1.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="a1572-128">Page1.xaml.cs</span></span></li>
<li><span data-ttu-id="a1572-129">Page2.xaml</span><span class="sxs-lookup"><span data-stu-id="a1572-129">Page2.xaml</span></span></li>
<li><span data-ttu-id="a1572-130">Page2.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="a1572-130">Page2.xaml.cs</span></span></li>
</ul></td>
<td style="vertical-align:top;"><ul>
<li><span data-ttu-id="a1572-131">Page1.xaml</span><span class="sxs-lookup"><span data-stu-id="a1572-131">Page1.xaml</span></span></li>
<li><span data-ttu-id="a1572-132">Page1.xaml.cpp</span><span class="sxs-lookup"><span data-stu-id="a1572-132">Page1.xaml.cpp</span></span></li>
<li><span data-ttu-id="a1572-133">Page1.xaml.h</span><span class="sxs-lookup"><span data-stu-id="a1572-133">Page1.xaml.h</span></span></li>
<li><span data-ttu-id="a1572-134">Page2.xaml</span><span class="sxs-lookup"><span data-stu-id="a1572-134">Page2.xaml</span></span></li>
<li><span data-ttu-id="a1572-135">Page2.xaml.cpp</span><span class="sxs-lookup"><span data-stu-id="a1572-135">Page2.xaml.cpp</span></span></li>
<li><span data-ttu-id="a1572-136">Page2.xaml.h</span><span class="sxs-lookup"><span data-stu-id="a1572-136">Page2.xaml.h</span></span>

</li>
</ul></td>
</tr>
</tbody>
</table>

<span data-ttu-id="a1572-137">Page1.xaml に次のコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-137">In Page1.xaml, add the following content:</span></span>

-   <span data-ttu-id="a1572-138">`pageTitle` という名前を付けた [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) 要素を、ルートの [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid) の子要素として追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-138">A [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) element named `pageTitle` as a child element of the root [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid).</span></span> <span data-ttu-id="a1572-139">[  **Text**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock.text) プロパティを `Page 1` に変更します。</span><span class="sxs-lookup"><span data-stu-id="a1572-139">Change the [**Text**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock.text) property to `Page 1`.</span></span>
```xaml
<TextBlock x:Name="pageTitle" Text="Page 1" />
```

-   <span data-ttu-id="a1572-140">[  **HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) 要素を、ルートの [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid) の子要素として `pageTitle` [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) 要素の後に追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-140">A [**HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) element as a child element of the root [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid) and after the `pageTitle` [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) element.</span></span>
```xaml
<HyperlinkButton Content="Click to go to page 2"
                 Click="HyperlinkButton_Click"
                 HorizontalAlignment="Center"/>
```

<span data-ttu-id="a1572-141">Page1.xaml 分離コード ファイルに、Page2.xaml に移動するために追加した [**HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) の `Click` イベントを処理する次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-141">In the Page1.xaml code-behind file, add the following code to handle the `Click` event of the [**HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) you added to navigate to Page2.xaml.</span></span>

```csharp
private void HyperlinkButton_Click(object sender, RoutedEventArgs e)
{
    this.Frame.Navigate(typeof(Page2));
}
```

```cppwinrt
void Page1::HyperlinkButton_Click(Windows::Foundation::IInspectable const& sender, Windows::UI::Xaml::RoutedEventArgs const& args)
{
    Frame().Navigate(winrt::xaml_typename<NavApp1::Page2>());
}
```

```cpp
void Page1::HyperlinkButton_Click(Platform::Object^ sender, RoutedEventArgs^ e)
{
    this->Frame->Navigate(Windows::UI::Xaml::Interop::TypeName(Page2::typeid));
}
```

<span data-ttu-id="a1572-142">Page2.xaml に次のコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-142">In Page2.xaml, add the following content:</span></span>

-   <span data-ttu-id="a1572-143">`pageTitle` という名前を付けた [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) 要素を、ルートの [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid) の子要素として追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-143">A [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) element named `pageTitle` as a child element of the root [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid).</span></span> <span data-ttu-id="a1572-144">[  **Text**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock.text) プロパティの値を `Page 2` に変更します。</span><span class="sxs-lookup"><span data-stu-id="a1572-144">Change the value of the [**Text**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock.text) property to `Page 2`.</span></span>
```xaml
<TextBlock x:Name="pageTitle" Text="Page 2" />
```

-   <span data-ttu-id="a1572-145">[  **HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) 要素を、ルートの [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid) の子要素として `pageTitle` [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) 要素の後に追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-145">A [**HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) element as a child element of the root [**Grid**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid) and after the `pageTitle` [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) element.</span></span>
```xaml
<HyperlinkButton Content="Click to go to page 1" 
                 Click="HyperlinkButton_Click"
                 HorizontalAlignment="Center"/>
```

<span data-ttu-id="a1572-146">Page2.xaml 分離コード ファイルに、Page1.xaml に移動するための [**HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) の `Click` イベントを処理する次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-146">In the Page2.xaml code-behind file, add the following code to handle the `Click` event of the [**HyperlinkButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) to navigate to Page1.xaml.</span></span>

```csharp
private void HyperlinkButton_Click(object sender, RoutedEventArgs e)
{
    this.Frame.Navigate(typeof(Page1));
}
```

```cppwinrt
void Page2::HyperlinkButton_Click(Windows::Foundation::IInspectable const& sender, Windows::UI::Xaml::RoutedEventArgs const& args)
{
    Frame().Navigate(winrt::xaml_typename<NavApp1::Page1>());
}
```

```cpp
void Page2::HyperlinkButton_Click(Platform::Object^ sender, RoutedEventArgs^ e)
{
    this->Frame->Navigate(Windows::UI::Xaml::Interop::TypeName(Page1::typeid));
}
```

> [!NOTE]
> <span data-ttu-id="a1572-147">C++ プロジェクトの場合は、別のページを参照する各ページのヘッダー ファイルに `#include` ディレクティブを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1572-147">For C++ projects, you must add a `#include` directive in the header file of each page that references another page.</span></span> <span data-ttu-id="a1572-148">ここで示したページ間のナビゲーションの例では、page1.xaml.h ファイルに `#include "Page2.xaml.h"` が、page2.xaml.h に `#include "Page1.xaml.h"` が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a1572-148">For the inter-page navigation example presented here, page1.xaml.h file contains `#include "Page2.xaml.h"`, in turn, page2.xaml.h contains `#include "Page1.xaml.h"`.</span></span>

<span data-ttu-id="a1572-149">ページが用意できたら、Page1.xaml をアプリの開始時に表示されるように設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1572-149">Now that we've prepared the pages, we need to make Page1.xaml display when the app starts.</span></span>

<span data-ttu-id="a1572-150">App.xaml 分離コードファイルを開き、`OnLaunched` ハンドラーを変更します。</span><span class="sxs-lookup"><span data-stu-id="a1572-150">Open the App.xaml code-behind file and change the `OnLaunched` handler.</span></span>

<span data-ttu-id="a1572-151">次に、[**Frame.Navigate**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate) の呼び出しに、`MainPage` ではなく `Page1` を追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-151">Here, we specify `Page1` in the call to [**Frame.Navigate**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate) instead of `MainPage`.</span></span>

```csharp
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    Frame rootFrame = Window.Current.Content as Frame;
 
    // Do not repeat app initialization when the Window already has content,
    // just ensure that the window is active
    if (rootFrame == null)
    {
        // Create a Frame to act as the navigation context and navigate to the first page
        rootFrame = new Frame();
        rootFrame.NavigationFailed += OnNavigationFailed;
 
        if (e.PreviousExecutionState == ApplicationExecutionState.Terminated)
        {
            //TODO: Load state from previously suspended application
        }
 
        // Place the frame in the current Window
        Window.Current.Content = rootFrame;
    }
 
    if (rootFrame.Content == null)
    {
        // When the navigation stack isn't restored navigate to the first page,
        // configuring the new page by passing required information as a navigation
        // parameter
        rootFrame.Navigate(typeof(Page1), e.Arguments);
    }
    // Ensure the current window is active
    Window.Current.Activate();
}
```

```cppwinrt
void App::OnLaunched(LaunchActivatedEventArgs const& e)
{
    Frame rootFrame{ nullptr };
    auto content = Window::Current().Content();
    if (content)
    {
        rootFrame = content.try_as<Frame>();
    }

    // Do not repeat app initialization when the Window already has content,
    // just ensure that the window is active
    if (rootFrame == nullptr)
    {
        // Create a Frame to act as the navigation context and associate it with
        // a SuspensionManager key
        rootFrame = Frame();

        rootFrame.NavigationFailed({ this, &App::OnNavigationFailed });

        if (e.PreviousExecutionState() == ApplicationExecutionState::Terminated)
        {
            // Restore the saved session state only when appropriate, scheduling the
            // final launch steps after the restore is complete
        }

        if (e.PrelaunchActivated() == false)
        {
            if (rootFrame.Content() == nullptr)
            {
                // When the navigation stack isn't restored navigate to the first page,
                // configuring the new page by passing required information as a navigation
                // parameter
                rootFrame.Navigate(xaml_typename<NavApp1::Page1>(), box_value(e.Arguments()));
            }
            // Place the frame in the current Window
            Window::Current().Content(rootFrame);
            // Ensure the current window is active
            Window::Current().Activate();
        }
    }
    else
    {
        if (e.PrelaunchActivated() == false)
        {
            if (rootFrame.Content() == nullptr)
            {
                // When the navigation stack isn't restored navigate to the first page,
                // configuring the new page by passing required information as a navigation
                // parameter
                rootFrame.Navigate(xaml_typename<NavApp1::Page1>(), box_value(e.Arguments()));
            }
            // Ensure the current window is active
            Window::Current().Activate();
        }
    }
}
```

```cpp
void App::OnLaunched(Windows::ApplicationModel::Activation::LaunchActivatedEventArgs^ e)
{
    auto rootFrame = dynamic_cast<Frame^>(Window::Current->Content);

    // Do not repeat app initialization when the Window already has content,
    // just ensure that the window is active
    if (rootFrame == nullptr)
    {
        // Create a Frame to act as the navigation context and associate it with
        // a SuspensionManager key
        rootFrame = ref new Frame();

        rootFrame->NavigationFailed += 
            ref new Windows::UI::Xaml::Navigation::NavigationFailedEventHandler(
                this, &App::OnNavigationFailed);

        if (e->PreviousExecutionState == ApplicationExecutionState::Terminated)
        {
            // TODO: Load state from previously suspended application
        }
        
        // Place the frame in the current Window
        Window::Current->Content = rootFrame;
    }

    if (rootFrame->Content == nullptr)
    {
        // When the navigation stack isn't restored navigate to the first page,
        // configuring the new page by passing required information as a navigation
        // parameter
        rootFrame->Navigate(Windows::UI::Xaml::Interop::TypeName(Page1::typeid), e->Arguments);
    }

    // Ensure the current window is active
    Window::Current->Activate();
}
```

> [!NOTE]
> <span data-ttu-id="a1572-152">次のコードの戻り値を使用して[ **Navigate** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate)アプリの最初のウィンドウ フレームにナビゲーションが失敗した場合は、アプリケーション例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="a1572-152">The code here uses the return value of [**Navigate**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate) to throw an app exception if the navigation to the app's initial window frame fails.</span></span> <span data-ttu-id="a1572-153">**Navigate** が **true** を返す場合は、ナビゲーションが行われます。</span><span class="sxs-lookup"><span data-stu-id="a1572-153">When **Navigate** returns **true**, the navigation happens.</span></span>

<span data-ttu-id="a1572-154">次に、アプリをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="a1572-154">Now, build and run the app.</span></span> <span data-ttu-id="a1572-155">"Click to go to page 2" と書かれているリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-155">Click the link that says "Click to go to page 2".</span></span> <span data-ttu-id="a1572-156">上部に "Page 2" と書かれた 2 番目のページが読み込まれ、フレームに表示される必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1572-156">The second page that says "Page 2" at the top should be loaded and displayed in the frame.</span></span>

### <a name="about-the-frame-and-page-classes"></a><span data-ttu-id="a1572-157">Frame クラスと Page クラスについて</span><span class="sxs-lookup"><span data-stu-id="a1572-157">About the Frame and Page classes</span></span>

<span data-ttu-id="a1572-158">アプリにさらに機能を加える前に、追加したページに用意されているアプリ内のナビゲーションについて見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="a1572-158">Before we add more functionality to our app, let's look at how the pages we added provide navigation within our app.</span></span>

<span data-ttu-id="a1572-159">まず、App.xaml 分離コード ファイルの `App.OnLaunched` メソッドで、アプリの [**Frame**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame) (`rootFrame`) が作成されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-159">First, a [**Frame**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame) called `rootFrame` is created for the app in the `App.OnLaunched` method in the App.xaml code-behind file.</span></span> <span data-ttu-id="a1572-160">**Frame** クラスは、[**Navigate**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate)、[**GoBack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.goback)、[**GoForward**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.goforward) などのさまざまなナビゲーション メソッドと、[**BackStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.backstack)、[**ForwardStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.forwardstack)、[**BackStackDepth**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.backstackdepth) などのプロパティをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a1572-160">The **Frame** class supports various navigation methods such as [**Navigate**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate), [**GoBack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.goback), and [**GoForward**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.goforward), and properties such as [**BackStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.backstack), [**ForwardStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.forwardstack), and [**BackStackDepth**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.backstackdepth).</span></span>
 
<span data-ttu-id="a1572-161">[  **Navigate**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate) メソッドを使って、この **Frame** にコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-161">The [**Navigate**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.navigate) method is used to display content in this **Frame**.</span></span> <span data-ttu-id="a1572-162">既定では、このメソッドは MainPage.xaml を読み込みます。</span><span class="sxs-lookup"><span data-stu-id="a1572-162">By default, this method loads MainPage.xaml.</span></span> <span data-ttu-id="a1572-163">この例では、`Page1` が **Navigate** メソッドに渡されるため、メソッドは **Frame** に `Page1` を読み込みます。</span><span class="sxs-lookup"><span data-stu-id="a1572-163">In our example, `Page1` is passed to the **Navigate** method, so the method loads `Page1` in the **Frame**.</span></span> 

<span data-ttu-id="a1572-164">`Page1` は [**Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) クラスのサブクラスです。</span><span class="sxs-lookup"><span data-stu-id="a1572-164">`Page1` is a subclass of the [**Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) class.</span></span> <span data-ttu-id="a1572-165">**Page** クラスには、**Page** が含まれる **Frame** を取得する読み取り専用の **Frame** プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="a1572-165">The **Page** class has a read-only **Frame** property that gets the **Frame** containing the **Page**.</span></span> <span data-ttu-id="a1572-166">`Page1` で **HyperlinkButton** の **Click** イベント ハンドラーが `this.Frame.Navigate(typeof(Page2))` を呼び出すと、**Frame** に Page2.xaml のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-166">When the **Click** event handler of the **HyperlinkButton** in `Page1` calls `this.Frame.Navigate(typeof(Page2))`, the **Frame** displays the content of Page2.xaml.</span></span>

<span data-ttu-id="a1572-167">最後に、フレームにページが読み込まれるたびに、そのページが [**PageStackEntry**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation.PageStackEntry) として、[**Frame**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.frame) の [**BackStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.backstack) または [**ForwardStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.forwardstack) に追加され、[履歴と前に戻る移動](navigation-history-and-backwards-navigation.md)が可能になります。</span><span class="sxs-lookup"><span data-stu-id="a1572-167">Finally, whenever a page is loaded into the frame, that page is added as a [**PageStackEntry**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation.PageStackEntry) to the [**BackStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.backstack) or [**ForwardStack**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.forwardstack) of the [**Frame**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.frame), allowing for [history and backwards navigation](navigation-history-and-backwards-navigation.md).</span></span>

## <a name="3-pass-information-between-pages"></a><span data-ttu-id="a1572-168">3.ページ間での情報の受け渡し</span><span class="sxs-lookup"><span data-stu-id="a1572-168">3. Pass information between pages</span></span>

<span data-ttu-id="a1572-169">このアプリでは、ページ間の移動は行いますが、実際に何かの処理を行うわけではありません。</span><span class="sxs-lookup"><span data-stu-id="a1572-169">Our app navigates between two pages, but it really doesn't do anything interesting yet.</span></span> <span data-ttu-id="a1572-170">多くの場合、アプリに複数のページがあれば、ページ間で情報を共有する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1572-170">Often, when an app has multiple pages, the pages need to share information.</span></span> <span data-ttu-id="a1572-171">最初のページから 2 番目のページへ情報を渡してみましょう。</span><span class="sxs-lookup"><span data-stu-id="a1572-171">Let's pass some information from the first page to the second page.</span></span>

<span data-ttu-id="a1572-172">Page1.xaml 置き換えます、 **HyperlinkButton** 、次を追加した[ **StackPanel**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.StackPanel)。</span><span class="sxs-lookup"><span data-stu-id="a1572-172">In Page1.xaml, replace the **HyperlinkButton** you added earlier with the following [**StackPanel**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.StackPanel).</span></span>

<span data-ttu-id="a1572-173">ここでは、追加、 [ **TextBlock** ](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock)ラベルと[ **TextBox** ](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) `name`テキスト文字列を入力するためです。</span><span class="sxs-lookup"><span data-stu-id="a1572-173">Here, we add a [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) label and a [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) `name` for entering a text string.</span></span>

```xaml
<StackPanel>
    <TextBlock HorizontalAlignment="Center" Text="Enter your name"/>
    <TextBox HorizontalAlignment="Center" Width="200" Name="name"/>
    <HyperlinkButton Content="Click to go to page 2" 
                     Click="HyperlinkButton_Click"
                     HorizontalAlignment="Center"/>
</StackPanel>
```

<span data-ttu-id="a1572-174">Page1.xaml 分離コード ファイルの `HyperlinkButton_Click` イベント ハンドラーで、`name` **TextBox** の `Text` プロパティを参照するパラメーターを `Navigate` メソッドに追加します。</span><span class="sxs-lookup"><span data-stu-id="a1572-174">In the `HyperlinkButton_Click` event handler of the Page1.xaml code-behind file, add a parameter referencing the `Text` property of the `name` **TextBox** to the `Navigate` method.</span></span>

```csharp
private void HyperlinkButton_Click(object sender, RoutedEventArgs e)
{
    this.Frame.Navigate(typeof(Page2), name.Text);
}
```

```cppwinrt
void Page1::HyperlinkButton_Click(Windows::Foundation::IInspectable const& sender, Windows::UI::Xaml::RoutedEventArgs const& args)
{
    Frame().Navigate(winrt::xaml_typename<NavApp1::Page2>(), winrt::box_value(name().Text()));
}
```

```cpp
void Page1::HyperlinkButton_Click(Platform::Object^ sender, RoutedEventArgs^ e)
{
    this->Frame->Navigate(Windows::UI::Xaml::Interop::TypeName(Page2::typeid), name->Text);
}
```

<span data-ttu-id="a1572-175">Page2.xaml で、前に追加した **HyperlinkButton** を次の **StackPanel** に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a1572-175">In Page2.xaml, replace the **HyperlinkButton** you added earlier with the following **StackPanel**.</span></span>

<span data-ttu-id="a1572-176">次に、[**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) を追加して、Page1 から渡された文字列を表示します。</span><span class="sxs-lookup"><span data-stu-id="a1572-176">Here, we add a [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) for displaying the text string passed from Page1.</span></span>

```xaml
<StackPanel>
    <TextBlock HorizontalAlignment="Center" Name="greeting"/>
    <HyperlinkButton Content="Click to go to page 1" 
                     Click="HyperlinkButton_Click"
                     HorizontalAlignment="Center"/>
</StackPanel>
```

<span data-ttu-id="a1572-177">Page2.xaml 分離コード ファイルで、次のコードを追加して `OnNavigatedTo` メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="a1572-177">In the Page2.xaml code-behind file, add the following to override the `OnNavigatedTo` method:</span></span>

```csharp
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    if (e.Parameter is string && !string.IsNullOrWhiteSpace((string)e.Parameter))
    {
        greeting.Text = $"Hi, {e.Parameter.ToString()}";
    }
    else
    {
        greeting.Text = "Hi!";
    }
    base.OnNavigatedTo(e);
}
```

```cppwinrt
void Page2::OnNavigatedTo(Windows::UI::Xaml::Navigation::NavigationEventArgs const& e)
{
    auto propertyValue{ e.Parameter().as<Windows::Foundation::IPropertyValue>() };
    if (propertyValue.Type() == Windows::Foundation::PropertyType::String)
    {
        greeting().Text(L"Hi, " + winrt::unbox_value<winrt::hstring>(e.Parameter()));
    }
    else
    {
        greeting().Text(L"Hi!");
    }
    __super::OnNavigatedTo(e);
}
```

```cpp
void Page2::OnNavigatedTo(NavigationEventArgs^ e)
{
    if (dynamic_cast<Platform::String^>(e->Parameter) != nullptr)
    {
        greeting->Text = "Hi, " + e->Parameter->ToString();
    }
    else
    {
        greeting->Text = "Hi!";
    }
    ::Windows::UI::Xaml::Controls::Page::OnNavigatedTo(e);
}
```

<span data-ttu-id="a1572-178">アプリを実行し、テキスト ボックスに自分の名前を入力し、 **[Click to go to page 2]** と書かれているリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="a1572-178">Run the app, type your name in the text box, and then click the link that says **Click to go to page 2**.</span></span> 

<span data-ttu-id="a1572-179">`Page1` の **HyperlinkButton** の **Click** イベントで `this.Frame.Navigate(typeof(Page2), name.Text)` を呼び出すと、`name.Text` プロパティが `Page2` に渡され、イベント データの値がページに表示されるメッセージに使用されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-179">When the **Click** event of the **HyperlinkButton** in `Page1` calls `this.Frame.Navigate(typeof(Page2), name.Text)`, the `name.Text` property is passed to `Page2`, and the value from the event data is used for the message displayed on the page.</span></span>

## <a name="4-cache-a-page"></a><span data-ttu-id="a1572-180">4。ページのキャッシュ</span><span class="sxs-lookup"><span data-stu-id="a1572-180">4. Cache a page</span></span>

<span data-ttu-id="a1572-181">ページのコンテンツと状態は既定ではキャッシュされないため、情報をキャッシュする場合は、アプリの各ページでキャッシュを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a1572-181">Page content and state is not cached by default, so if you'd like to cache information, you must enable it in each page of your app.</span></span>

<span data-ttu-id="a1572-182">この基本的なピア ツー ピアの例では、戻るボタンはありませんが (戻るナビゲーションは「[前に戻る移動](navigation-history-and-backwards-navigation.md)」で示しました)、`Page2` で戻るボタンをクリックした場合、`Page1` の **TextBox** (およびその他のすべてのフィールド) は既定の状態に設定されます。</span><span class="sxs-lookup"><span data-stu-id="a1572-182">In our basic peer-to-peer example, there is no back button (we demonstrate back navigation in [backwards navigation](navigation-history-and-backwards-navigation.md)), but if you did click a back button on `Page2`, the **TextBox** (and any other field) on `Page1` would be set to its default state.</span></span> <span data-ttu-id="a1572-183">これを回避する方法の 1 つは、[**NavigationCacheMode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.navigationcachemode) プロパティを使って、ページがフレームのページ キャッシュに追加されるように指定することです。</span><span class="sxs-lookup"><span data-stu-id="a1572-183">One way to work around this is to use the [**NavigationCacheMode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.navigationcachemode) property to specify that a page be added to the frame's page cache.</span></span> 

<span data-ttu-id="a1572-184">`Page1` のコンストラクターで、**NavigationCacheMode** を **Enabled** に設定して、フレームのページ キャッシュを超えるまでページのすべてのコンテンツと状態の値を保持することができます。</span><span class="sxs-lookup"><span data-stu-id="a1572-184">In the constructor of `Page1`, you can set **NavigationCacheMode** to **Enabled** to retains all content and state values for the page until the page cache for the frame is exceeded.</span></span> <span data-ttu-id="a1572-185">[  **CacheSize**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.cachesize) の制限を無視する場合は、[**NavigationCacheMode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.navigationcachemode) を [**Required**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation.NavigationCacheMode) に設定します。これで、フレームにキャッシュできる、ナビゲーション履歴内のページ数を指定します。</span><span class="sxs-lookup"><span data-stu-id="a1572-185">Set [**NavigationCacheMode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.navigationcachemode) to [**Required**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation.NavigationCacheMode) if you want to ignore [**CacheSize**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame.cachesize) limits, which specify the number of pages in the navigation history that can be cached for the frame.</span></span> <span data-ttu-id="a1572-186">ただし、キャッシュ サイズの制限は、デバイスのメモリの制限に依存しており、重要である可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a1572-186">However, keep in mind that cache size limits might be crucial, depending on the memory limits of a device.</span></span>

```csharp
public Page1()
{
    this.InitializeComponent();
    this.NavigationCacheMode = Windows.UI.Xaml.Navigation.NavigationCacheMode.Enabled;
}
```

```cppwinrt
Page1::Page1()
{
    InitializeComponent();
    NavigationCacheMode(Windows::UI::Xaml::Navigation::NavigationCacheMode::Enabled);
}
```

```cpp
Page1::Page1()
{
    this->InitializeComponent();
    this->NavigationCacheMode = Windows::UI::Xaml::Navigation::NavigationCacheMode::Enabled;
}
```

## <a name="related-articles"></a><span data-ttu-id="a1572-187">関連記事</span><span class="sxs-lookup"><span data-stu-id="a1572-187">Related articles</span></span>
* [<span data-ttu-id="a1572-188">UWP アプリのナビゲーションのデザインの基礎</span><span class="sxs-lookup"><span data-stu-id="a1572-188">Navigation design basics for UWP apps</span></span>](https://docs.microsoft.com/windows/uwp/layout/navigation-basics)
* [<span data-ttu-id="a1572-189">タブおよびピボットするためのガイドライン</span><span class="sxs-lookup"><span data-stu-id="a1572-189">Guidelines for tabs and pivots</span></span>](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tabs-pivot)
* [<span data-ttu-id="a1572-190">ナビゲーション ウィンドウのガイドライン</span><span class="sxs-lookup"><span data-stu-id="a1572-190">Guidelines for navigation panes</span></span>](https://docs.microsoft.com/windows/uwp/controls-and-patterns/nav-pane)
