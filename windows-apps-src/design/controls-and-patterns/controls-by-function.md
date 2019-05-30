---
Description: アプリで使うことができる一部のコントロールの機能別の一覧を示します。
title: 機能別コントロール
ms.assetid: 8DB4347B-91D6-4659-91F2-80ECF7BBB596
label: Controls by function
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 6de5e9d8899a7f270d30438a0563b879ccdab898
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66363139"
---
# <a name="controls-by-function"></a><span data-ttu-id="e51b0-104">機能別コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-104">Controls by function</span></span>

<span data-ttu-id="e51b0-105">Windows の XAML UI フレームワークには、UI 開発をサポートする多くのコントロールのライブラリが用意されています。</span><span class="sxs-lookup"><span data-stu-id="e51b0-105">The XAML UI framework for Windows provides an extensive library of controls that support UI development.</span></span> <span data-ttu-id="e51b0-106">これらのコントロールの一部は視覚的に表示されますが、それ以外のコントロールは他のコントロールまたはコンテンツ (画像やメディアなど) のコンテナーとして機能します。</span><span class="sxs-lookup"><span data-stu-id="e51b0-106">Some of these controls have a visual representation; others function as the containers for other controls or content, such as images and media.</span></span> 

<span data-ttu-id="e51b0-107">[XAML UI の基本のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=619992)をダウンロードすると、Windows UI コントロールの多くを実際に見ることができます。</span><span class="sxs-lookup"><span data-stu-id="e51b0-107">You can see many of the Windows UI controls in action by downloading the [XAML UI Basics sample](https://go.microsoft.com/fwlink/p/?LinkId=619992).</span></span>

<table>
<th align="left"><span data-ttu-id="e51b0-108">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="e51b0-108">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="e51b0-109">ある場合、 <strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong>アプリをインストールするには、ここをクリックして<a href="xamlcontrolsgallery:/item/NavigationView">アプリを開き、NavigationView の動作を参照してください。</a> </span><span class="sxs-lookup"><span data-stu-id="e51b0-109">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/NavigationView">open the app and see the NavigationView in action</a> </span></span></p>
    <ul>
    <li><span data-ttu-id="e51b0-110"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="e51b0-110"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="e51b0-111"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="e51b0-111"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>


<span data-ttu-id="e51b0-112">アプリで使うことができる一般的な XAML コントロールの機能別の一覧を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="e51b0-112">Here's a list by function of the common XAML controls you can use in your app.</span></span>

## <a name="appbars-and-commands"></a><span data-ttu-id="e51b0-113">アプリ バーとコマンド</span><span class="sxs-lookup"><span data-stu-id="e51b0-113">Appbars and commands</span></span>

### <a name="app-bar"></a><span data-ttu-id="e51b0-114">アプリ バー</span><span class="sxs-lookup"><span data-stu-id="e51b0-114">App bar</span></span>
<span data-ttu-id="e51b0-115">アプリ特有のコマンドを表示するツール バー。</span><span class="sxs-lookup"><span data-stu-id="e51b0-115">A toolbar for displaying application-specific commands.</span></span> <span data-ttu-id="e51b0-116">「コマンド バー」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-116">See Command bar.</span></span>

<span data-ttu-id="e51b0-117">参照 :[AppBar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBar)</span><span class="sxs-lookup"><span data-stu-id="e51b0-117">Reference: [AppBar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBar)</span></span> 

### <a name="app-bar-button"></a><span data-ttu-id="e51b0-118">アプリ バーのボタン</span><span class="sxs-lookup"><span data-stu-id="e51b0-118">App bar button</span></span>
<span data-ttu-id="e51b0-119">アプリ バー スタイルを使ってコマンドを表示するボタン。</span><span class="sxs-lookup"><span data-stu-id="e51b0-119">A button for showing commands using app bar styling.</span></span>

![アプリ バーのボタン アイコン](images/controls/app-bar-buttons.png) 

<span data-ttu-id="e51b0-121">参照 :[AppBarButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarButton)、 [SymbolIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SymbolIcon)、 [BitmapIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.BitmapIcon)、 [FontIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.FontIcon)、 [PathIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.PathIcon)</span><span class="sxs-lookup"><span data-stu-id="e51b0-121">Reference: [AppBarButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarButton), [SymbolIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SymbolIcon), [BitmapIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.BitmapIcon), [FontIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.FontIcon), [PathIcon](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.PathIcon)</span></span> 

<span data-ttu-id="e51b0-122">設計と操作方法:[アプリ バーとコマンド バーのコントロールのガイド](app-bars.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-122">Design and how-to: [App bar and command bar control guide](app-bars.md)</span></span> 

<span data-ttu-id="e51b0-123">サンプル コード:[コマンド実行の XAML サンプル](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span><span class="sxs-lookup"><span data-stu-id="e51b0-123">Sample code: [XAML Commanding sample](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span></span>

### <a name="app-bar-separator"></a><span data-ttu-id="e51b0-124">アプリ バーの区分線</span><span class="sxs-lookup"><span data-stu-id="e51b0-124">App bar separator</span></span>
<span data-ttu-id="e51b0-125">コマンド バーのコマンドのグループを視覚的に区切ります。</span><span class="sxs-lookup"><span data-stu-id="e51b0-125">Visually separates groups of commands in a command bar.</span></span>

<span data-ttu-id="e51b0-126">参照 :[AppBarSeparator](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarSeparator)</span><span class="sxs-lookup"><span data-stu-id="e51b0-126">Reference: [AppBarSeparator](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarSeparator)</span></span> 

<span data-ttu-id="e51b0-127">サンプル コード:[コマンド実行の XAML サンプル](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span><span class="sxs-lookup"><span data-stu-id="e51b0-127">Sample code: [XAML Commanding sample](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span></span>

### <a name="app-bar-toggle-button"></a><span data-ttu-id="e51b0-128">アプリ バーのトグル ボタン</span><span class="sxs-lookup"><span data-stu-id="e51b0-128">App bar toggle button</span></span>
<span data-ttu-id="e51b0-129">コマンド バーでコマンドを切り替えるボタン。</span><span class="sxs-lookup"><span data-stu-id="e51b0-129">A button for toggling commands in a command bar.</span></span>

<span data-ttu-id="e51b0-130">参照 :[AppBarToggleButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarToggleButton)</span><span class="sxs-lookup"><span data-stu-id="e51b0-130">Reference: [AppBarToggleButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AppBarToggleButton)</span></span> 

<span data-ttu-id="e51b0-131">サンプル コード:[コマンド実行の XAML サンプル](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span><span class="sxs-lookup"><span data-stu-id="e51b0-131">Sample code: [XAML Commanding sample](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span></span>

### <a name="command-bar"></a><span data-ttu-id="e51b0-132">コマンド バー</span><span class="sxs-lookup"><span data-stu-id="e51b0-132">Command bar</span></span>
<span data-ttu-id="e51b0-133">アプリ バーのボタン要素のサイズ変更を処理する専用のアプリ バー。</span><span class="sxs-lookup"><span data-stu-id="e51b0-133">A specialized app bar that handles the resizing of app bar button elements.</span></span>

![コマンド バー コントロール](images/command-bar-compact.png)

```xaml
<CommandBar>
    <AppBarButton Icon="Back" Label="Back" Click="AppBarButton_Click"/>
    <AppBarButton Icon="Stop" Label="Stop" Click="AppBarButton_Click"/>
    <AppBarButton Icon="Play" Label="Play" Click="AppBarButton_Click"/>
</CommandBar>
```
<span data-ttu-id="e51b0-135">参照 :[コマンド バー](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CommandBar)</span><span class="sxs-lookup"><span data-stu-id="e51b0-135">Reference: [CommandBar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CommandBar)</span></span> 

<span data-ttu-id="e51b0-136">設計と操作方法:[アプリ バーとコマンド バーのコントロールのガイド](app-bars.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-136">Design and how-to: [App bar and command bar control guide](app-bars.md)</span></span>

<span data-ttu-id="e51b0-137">サンプル コード:[コマンド実行の XAML サンプル](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span><span class="sxs-lookup"><span data-stu-id="e51b0-137">Sample code: [XAML Commanding sample](https://go.microsoft.com/fwlink/p/?LinkId=620019)</span></span>

## <a name="buttons"></a><span data-ttu-id="e51b0-138">ボタン</span><span class="sxs-lookup"><span data-stu-id="e51b0-138">Buttons</span></span>

### <a name="button"></a><span data-ttu-id="e51b0-139">Button</span><span class="sxs-lookup"><span data-stu-id="e51b0-139">Button</span></span>
<span data-ttu-id="e51b0-140">ユーザーの入力に応答して **Click** イベントを発生させるコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-140">A control that responds to user input and raises a **Click** event.</span></span>

![標準的なボタン](images/controls/button.png)

```xaml
<Button x:Name="button1" Content="Button" 
        Click="Button_Click" />
```

<span data-ttu-id="e51b0-142">参照 :[ボタン](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button)</span><span class="sxs-lookup"><span data-stu-id="e51b0-142">Reference: [Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button)</span></span> 

<span data-ttu-id="e51b0-143">設計と操作方法:[ボタン コントロールのガイド](buttons.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-143">Design and how-to: [Buttons control guide](buttons.md)</span></span> 

### <a name="hyperlink"></a><span data-ttu-id="e51b0-144">ハイパーリンク</span><span class="sxs-lookup"><span data-stu-id="e51b0-144">Hyperlink</span></span>
<span data-ttu-id="e51b0-145">「ハイパーリンク ボタン」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-145">See Hyperlink button.</span></span>

### <a name="hyperlink-button"></a><span data-ttu-id="e51b0-146">ハイパーリンク ボタン</span><span class="sxs-lookup"><span data-stu-id="e51b0-146">Hyperlink button</span></span>
<span data-ttu-id="e51b0-147">ブラウザーでマークアップ テキストとして表示され、指定された URI を開くボタンです。</span><span class="sxs-lookup"><span data-stu-id="e51b0-147">A button that appears as marked up text and opens the specified URI in a browser.</span></span>

![ハイパーリンク ボタン](images/controls/hyperlink-button.png)

```xaml
<HyperlinkButton Content="www.microsoft.com" 
                 NavigateUri="https://www.microsoft.com"/>
```

<span data-ttu-id="e51b0-149">参照 :[HyperlinkButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton)</span><span class="sxs-lookup"><span data-stu-id="e51b0-149">Reference: [HyperlinkButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton)</span></span> 

<span data-ttu-id="e51b0-150">設計と操作方法:[ハイパーリンク コントロールのガイド](hyperlinks.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-150">Design and how-to: [Hyperlinks control guide](hyperlinks.md)</span></span>

### <a name="repeat-button"></a><span data-ttu-id="e51b0-151">繰り返しボタン</span><span class="sxs-lookup"><span data-stu-id="e51b0-151">Repeat button</span></span>
<span data-ttu-id="e51b0-152">押されたときから離されるまでの間、繰り返し **Click** イベントを発生させるボタン。</span><span class="sxs-lookup"><span data-stu-id="e51b0-152">A button that raises its **Click** event repeatedly from the time it's pressed until it's released.</span></span> 

![繰り返しボタン コントロール](images/controls/repeat-button.png) 

```xaml
<RepeatButton x:Name="repeatButton1" Content="Repeat Button" 
              Click="RepeatButton_Click" />
```

<span data-ttu-id="e51b0-154">参照 :[RepeatButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Primitives.RepeatButton)</span><span class="sxs-lookup"><span data-stu-id="e51b0-154">Reference: [RepeatButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Primitives.RepeatButton)</span></span> 

<span data-ttu-id="e51b0-155">設計と操作方法:[ボタン コントロールのガイド](buttons.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-155">Design and how-to: [Buttons control guide](buttons.md)</span></span> 

## <a name="collectiondata-controls"></a><span data-ttu-id="e51b0-156">コレクション コントロールとデータ コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-156">Collection/data controls</span></span>

### <a name="flip-view"></a><span data-ttu-id="e51b0-157">フリップ ビュー</span><span class="sxs-lookup"><span data-stu-id="e51b0-157">Flip view</span></span>
<span data-ttu-id="e51b0-158">ユーザーが 1 つずつめくって表示することができる項目のコレクションを表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-158">A control that presents a collection of items that the user can flip through, one item at a time.</span></span>

```xaml
<FlipView x:Name="flipView1" SelectionChanged="FlipView_SelectionChanged">
    <Image Source="Assets/Logo.png" />
    <Image Source="Assets/SplashScreen.png" />
    <Image Source="Assets/SmallLogo.png" />
</FlipView>
```

<span data-ttu-id="e51b0-159">参照 :[FlipView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.FlipView)</span><span class="sxs-lookup"><span data-stu-id="e51b0-159">Reference: [FlipView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.FlipView)</span></span> 

<span data-ttu-id="e51b0-160">設計と操作方法:[フリップ ビュー コントロールのガイド](flipview.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-160">Design and how-to: [Flip view control guide](flipview.md)</span></span> 

### <a name="grid-view"></a><span data-ttu-id="e51b0-161">グリッド ビュー</span><span class="sxs-lookup"><span data-stu-id="e51b0-161">Grid view</span></span>
<span data-ttu-id="e51b0-162">縦方向にスクロールできる複数行と複数列で項目のコレクションを表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-162">A control that presents a collection of items in rows and columns that can scroll vertically.</span></span>

```xaml
<GridView x:Name="gridView1" SelectionChanged="GridView_SelectionChanged">
    <x:String>Item 1</x:String>
    <x:String>Item 2</x:String>
</GridView>
```

<span data-ttu-id="e51b0-163">参照 :[GridView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.GridView)</span><span class="sxs-lookup"><span data-stu-id="e51b0-163">Reference: [GridView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.GridView)</span></span> 

<span data-ttu-id="e51b0-164">設計と操作方法:[リスト](lists.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-164">Design and how-to: [Lists](lists.md)</span></span> 

<span data-ttu-id="e51b0-165">サンプル コード:[ListView のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=619900)</span><span class="sxs-lookup"><span data-stu-id="e51b0-165">Sample code: [ListView sample](https://go.microsoft.com/fwlink/p/?LinkId=619900)</span></span>

### <a name="items-control"></a><span data-ttu-id="e51b0-166">項目コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-166">Items control</span></span>
<span data-ttu-id="e51b0-167">データ テンプレートで指定された UI にある項目のコレクションを表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-167">A control that presents a collection of items in a UI specified by a data template.</span></span> 

```xaml
<ItemsControl/>
```

<span data-ttu-id="e51b0-168">参照 :[ItemsControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ItemsControl)</span><span class="sxs-lookup"><span data-stu-id="e51b0-168">Reference: [ItemsControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ItemsControl)</span></span> 

### <a name="list-view"></a><span data-ttu-id="e51b0-169">リスト ビュー</span><span class="sxs-lookup"><span data-stu-id="e51b0-169">List view</span></span>
<span data-ttu-id="e51b0-170">縦方向にスクロールできるリストで項目のコレクションを表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-170">A control that presents a collection of items in a list that can scroll vertically.</span></span>

```xaml
<ListView x:Name="listView1" SelectionChanged="ListView_SelectionChanged">
    <x:String>Item 1</x:String>
    <x:String>Item 2</x:String>
</ListView>
```

<span data-ttu-id="e51b0-171">参照 :[ListView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListView)</span><span class="sxs-lookup"><span data-stu-id="e51b0-171">Reference: [ListView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListView)</span></span> 

<span data-ttu-id="e51b0-172">設計と操作方法:[リスト](lists.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-172">Design and how-to: [Lists](lists.md)</span></span> 

<span data-ttu-id="e51b0-173">サンプル コード:[ListView のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=619900)</span><span class="sxs-lookup"><span data-stu-id="e51b0-173">Sample code: [ListView sample](https://go.microsoft.com/fwlink/p/?LinkId=619900)</span></span>

## <a name="date-and-time-controls"></a><span data-ttu-id="e51b0-174">日付と時刻コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-174">Date and time controls</span></span>

### <a name="calendar-date-picker"></a><span data-ttu-id="e51b0-175">カレンダーの日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-175">Calendar date picker</span></span>
<span data-ttu-id="e51b0-176">ドロップダウン カレンダー表示を使って、ユーザーが日付を選択できるコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-176">A control that lets a user select a date using a drop-down calendar display.</span></span>

![カレンダー ビューが開いたカレンダーの日付の選択コントロール](images/controls/calendar-date-picker-open.png)

```xaml
<CalendarDatePicker/>
```

<span data-ttu-id="e51b0-178">参照 :[CalendarDatePicker](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarDatePicker)</span><span class="sxs-lookup"><span data-stu-id="e51b0-178">Reference: [CalendarDatePicker](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarDatePicker)</span></span> 

<span data-ttu-id="e51b0-179">設計と操作方法:[予定表、日付、およびタイム コントロール](date-and-time.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-179">Design and how-to: [Calendar, date, and time controls](date-and-time.md)</span></span>
 
### <a name="calendar-view"></a><span data-ttu-id="e51b0-180">カレンダー ビュー</span><span class="sxs-lookup"><span data-stu-id="e51b0-180">Calendar view</span></span>
<span data-ttu-id="e51b0-181">ユーザーが 1 つまたは複数の日付を選択できる、構成可能なカレンダー表示。</span><span class="sxs-lookup"><span data-stu-id="e51b0-181">A configurable calendar display that lets a user select single or multiple dates.</span></span>

```xaml
<CalendarView/>
```

<span data-ttu-id="e51b0-182">参照 :[予定表ビュー](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarView)</span><span class="sxs-lookup"><span data-stu-id="e51b0-182">Reference: [CalendarView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarView)</span></span> 

<span data-ttu-id="e51b0-183">設計と操作方法:[予定表、日付、およびタイム コントロール](date-and-time.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-183">Design and how-to: [Calendar, date, and time controls](date-and-time.md)</span></span> 

### <a name="date-picker"></a><span data-ttu-id="e51b0-184">日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-184">Date picker</span></span>
<span data-ttu-id="e51b0-185">ユーザーが日付を選択できるコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-185">A control that lets a user select a date.</span></span>

![日付の選択コントロール](images/controls/date-picker.png)

```xaml
<DatePicker Header="Arrival Date"/>
```

<span data-ttu-id="e51b0-187">参照 :[DatePicker](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.DatePicker)</span><span class="sxs-lookup"><span data-stu-id="e51b0-187">Reference: [DatePicker](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.DatePicker)</span></span> 

<span data-ttu-id="e51b0-188">設計と操作方法:[予定表、日付、およびタイム コントロール](date-and-time.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-188">Design and how-to: [Calendar, date, and time controls](date-and-time.md)</span></span>
 
### <a name="time-picker"></a><span data-ttu-id="e51b0-189">時刻の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-189">Time picker</span></span>
<span data-ttu-id="e51b0-190">ユーザーが時間値を設定できるコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-190">A control that lets a user set a time value.</span></span>

![TimePicker コントロール](images/controls/time-picker.png) 

```xaml
<TimePicker Header="Arrival Time"/>
```

<span data-ttu-id="e51b0-192">参照 :[TimePicker](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TimePicker)</span><span class="sxs-lookup"><span data-stu-id="e51b0-192">Reference: [TimePicker](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TimePicker)</span></span> 

<span data-ttu-id="e51b0-193">設計と操作方法:[予定表、日付、およびタイム コントロール](date-and-time.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-193">Design and how-to: [Calendar, date, and time controls](date-and-time.md)</span></span>

## <a name="flyouts"></a><span data-ttu-id="e51b0-194">ポップアップ</span><span class="sxs-lookup"><span data-stu-id="e51b0-194">Flyouts</span></span>

### <a name="context-menu"></a><span data-ttu-id="e51b0-195">コンテキスト メニュー</span><span class="sxs-lookup"><span data-stu-id="e51b0-195">Context menu</span></span>
<span data-ttu-id="e51b0-196">「メニュー ポップアップ」および「ポップアップ メニュー」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-196">See Menu flyout and Popup menu.</span></span>

### <a name="flyout"></a><span data-ttu-id="e51b0-197">ポップアップ</span><span class="sxs-lookup"><span data-stu-id="e51b0-197">Flyout</span></span>
<span data-ttu-id="e51b0-198">ユーザーの操作が必要であることを示すメッセージを表示します</span><span class="sxs-lookup"><span data-stu-id="e51b0-198">Displays a message that requires user interaction.</span></span> <span data-ttu-id="e51b0-199">(ダイアログでは他のユーザー操作がブロックされますが、ポップアップでは別のウィンドウが作成されず、操作もブロックされません)。</span><span class="sxs-lookup"><span data-stu-id="e51b0-199">(Unlike a dialog, a flyout does not create a separate window, and does not block other user interaction.)</span></span>

![ポップアップ コントロール](images/controls/flyout.png)

```xaml
<Flyout>
    <StackPanel>
        <TextBlock Text="All items will be removed. Do you want to continue?"/>
        <Button Click="DeleteConfirmation_Click" Content="Yes, empty my cart"/>
    </StackPanel>
</Flyout>
```

<span data-ttu-id="e51b0-201">参照 :[フライアウト](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Flyout)</span><span class="sxs-lookup"><span data-stu-id="e51b0-201">Reference: [Flyout](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Flyout)</span></span> 

<span data-ttu-id="e51b0-202">設計と操作方法:[フライアウト](dialogs-and-flyouts/flyouts.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-202">Design and how-to: [Flyouts](dialogs-and-flyouts/flyouts.md)</span></span> 

### <a name="menu-flyout"></a><span data-ttu-id="e51b0-203">メニュー ポップアップ</span><span class="sxs-lookup"><span data-stu-id="e51b0-203">Menu flyout</span></span>
<span data-ttu-id="e51b0-204">ユーザーが現在行っている内容に関連するコマンドまたはオプションの一覧を一時的に表示します。</span><span class="sxs-lookup"><span data-stu-id="e51b0-204">Temporarily displays a list of commands or options related to what the user is currently doing.</span></span>

![メニュー ポップアップ コントロール](images/controls/menu-flyout.png) 

```xaml
<MenuFlyout>
    <MenuFlyoutItem Text="Reset" Click="Reset_Click"/>
    <MenuFlyoutSeparator/>
    <ToggleMenuFlyoutItem Text="Shuffle" 
                          IsChecked="{Binding IsShuffleEnabled, Mode=TwoWay}"/>
    <ToggleMenuFlyoutItem Text="Repeat" 
                          IsChecked="{Binding IsRepeatEnabled, Mode=TwoWay}"/>
</MenuFlyout>
```

<span data-ttu-id="e51b0-206">参照 :[MenuFlyout](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MenuFlyout)、 [MenuFlyoutItem](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MenuFlyoutItem)、 [MenuFlyoutSeparator](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MenuFlyoutSeparator)、 [ToggleMenuFlyoutItem](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToggleMenuFlyoutItem)</span><span class="sxs-lookup"><span data-stu-id="e51b0-206">Reference: [MenuFlyout](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MenuFlyout), [MenuFlyoutItem](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MenuFlyoutItem), [MenuFlyoutSeparator](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MenuFlyoutSeparator), [ToggleMenuFlyoutItem](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToggleMenuFlyoutItem)</span></span> 

<span data-ttu-id="e51b0-207">設計と操作方法:[メニューとショートカット メニュー](menus.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-207">Design and how-to: [Menus and context menus](menus.md)</span></span> 

<span data-ttu-id="e51b0-208">サンプル コード:[XAML のコンテキスト メニューのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=620021)</span><span class="sxs-lookup"><span data-stu-id="e51b0-208">Sample code: [XAML Context Menu sample](https://go.microsoft.com/fwlink/p/?LinkId=620021)</span></span>

### <a name="popup-menu"></a><span data-ttu-id="e51b0-209">ポップアップ メニュー</span><span class="sxs-lookup"><span data-stu-id="e51b0-209">Popup menu</span></span>
<span data-ttu-id="e51b0-210">指定したコマンドを表示するためのカスタム メニュー。</span><span class="sxs-lookup"><span data-stu-id="e51b0-210">A custom menu that presents commands that you specify.</span></span>

<span data-ttu-id="e51b0-211">参照 :[ポップアップ メニュー](https://docs.microsoft.com/uwp/api/Windows.UI.Popups.PopupMenu)</span><span class="sxs-lookup"><span data-stu-id="e51b0-211">Reference: [PopupMenu](https://docs.microsoft.com/uwp/api/Windows.UI.Popups.PopupMenu)</span></span> 

<span data-ttu-id="e51b0-212">設計と操作方法:[ダイアログ ボックス](dialogs-and-flyouts/dialogs.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-212">Design and how-to: [Dialogs](dialogs-and-flyouts/dialogs.md)</span></span> 

### <a name="tooltip"></a><span data-ttu-id="e51b0-213">ヒント</span><span class="sxs-lookup"><span data-stu-id="e51b0-213">Tooltip</span></span>
<span data-ttu-id="e51b0-214">要素についての情報を表示するポップアップ ウィンドウ。</span><span class="sxs-lookup"><span data-stu-id="e51b0-214">A pop-up window that displays information for an element.</span></span> 
 
![ヒント コントロール](images/controls/tool-tip.png)

```xaml
<Button Content="Button" Click="Button_Click" 
        ToolTipService.ToolTip="Click to perform action" />
```

<span data-ttu-id="e51b0-216">参照 :[ツールヒント](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToolTip)、 [ToolTipService](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToolTipService)</span><span class="sxs-lookup"><span data-stu-id="e51b0-216">Reference: [ToolTip](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToolTip), [ToolTipService](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToolTipService)</span></span> 

<span data-ttu-id="e51b0-217">設計と操作方法:ヒントのガイドライン</span><span class="sxs-lookup"><span data-stu-id="e51b0-217">Design and how-to: Guidelines for tooltips</span></span> 

## <a name="images"></a><span data-ttu-id="e51b0-218">画像</span><span class="sxs-lookup"><span data-stu-id="e51b0-218">Images</span></span>

### <a name="image"></a><span data-ttu-id="e51b0-219">イメージ</span><span class="sxs-lookup"><span data-stu-id="e51b0-219">Image</span></span>
<span data-ttu-id="e51b0-220">画像を表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-220">A control that presents an image.</span></span>

```xaml
<Image Source="Assets/Logo.png" />
```

<span data-ttu-id="e51b0-221">参照 :[イメージ](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Image)</span><span class="sxs-lookup"><span data-stu-id="e51b0-221">Reference: [Image](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Image)</span></span> 

<span data-ttu-id="e51b0-222">設計と操作方法:[イメージと ImageBrush](images-imagebrushes.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-222">Design and how-to: [Image and ImageBrush](images-imagebrushes.md)</span></span> 

<span data-ttu-id="e51b0-223">サンプル コード:[XAML イメージ サンプル](https://go.microsoft.com/fwlink/p/?linkid=226867)</span><span class="sxs-lookup"><span data-stu-id="e51b0-223">Sample code: [XAML images sample](https://go.microsoft.com/fwlink/p/?linkid=226867)</span></span>

## <a name="graphics-and-ink"></a><span data-ttu-id="e51b0-224">グラフィックスとインク</span><span class="sxs-lookup"><span data-stu-id="e51b0-224">Graphics and ink</span></span>

### <a name="inkcanvas"></a><span data-ttu-id="e51b0-225">InkCanvas</span><span class="sxs-lookup"><span data-stu-id="e51b0-225">InkCanvas</span></span>
<span data-ttu-id="e51b0-226">インク ストロークを受信し、表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-226">A control that receives and displays ink strokes.</span></span>

```xaml
<InkCanvas/>
```

<span data-ttu-id="e51b0-227">参照 :[InkCanvas](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)</span><span class="sxs-lookup"><span data-stu-id="e51b0-227">Reference: [InkCanvas](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)</span></span> 

### <a name="shapes"></a><span data-ttu-id="e51b0-228">図形</span><span class="sxs-lookup"><span data-stu-id="e51b0-228">Shapes</span></span>
<span data-ttu-id="e51b0-229">楕円形、四角形、直線、ベジエ パスなどのように表示できる、保持モードの各種グラフィック オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="e51b0-229">Various retained mode graphical objects that can be presented like ellipses, rectangles, lines, Bezier paths, etc.</span></span>

<span data-ttu-id="e51b0-230">![多角形](images/controls/shapes-polygon.png) 
![パス](images/controls/shapes-path.png)</span><span class="sxs-lookup"><span data-stu-id="e51b0-230">![A polygon](images/controls/shapes-polygon.png) 
![A path](images/controls/shapes-path.png)</span></span> 

```xaml
<Ellipse/>
<Path/>
<Rectangle/>
```

<span data-ttu-id="e51b0-231">参照 :[図形](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Shapes.Shape)</span><span class="sxs-lookup"><span data-stu-id="e51b0-231">Reference: [Shapes](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Shapes.Shape)</span></span> 

<span data-ttu-id="e51b0-232">方法: [図形の描画](../../graphics/drawing-shapes.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-232">How to: [Drawing shapes](../../graphics/drawing-shapes.md)</span></span> 

<span data-ttu-id="e51b0-233">サンプル コード:[XAML のベクトルに基づく描画サンプル](https://go.microsoft.com/fwlink/p/?linkid=226866)</span><span class="sxs-lookup"><span data-stu-id="e51b0-233">Sample code: [XAML vector-based drawing sample](https://go.microsoft.com/fwlink/p/?linkid=226866)</span></span>

## <a name="layout-controls"></a><span data-ttu-id="e51b0-234">レイアウト コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-234">Layout controls</span></span>

### <a name="border"></a><span data-ttu-id="e51b0-235">罫線</span><span class="sxs-lookup"><span data-stu-id="e51b0-235">Border</span></span>
<span data-ttu-id="e51b0-236">境界線、背景、またはこの両方を他のオブジェクトの周囲に描画するコンテナー コントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-236">A container control that draws a border, background, or both, around another object.</span></span>

![2 つの四角形の周囲の境界線](images/controls/border.png) 

```xaml
<Border BorderBrush="Blue" BorderThickness="4" 
        Height="108" Width="64" 
        Padding="8" CornerRadius="4">
    <Canvas>
        <Rectangle Fill="Orange"/>
        <Rectangle Fill="Green" Margin="0,44"/>
    </Canvas>
</Border>
```

<span data-ttu-id="e51b0-238">参照 :[境界線](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Border)</span><span class="sxs-lookup"><span data-stu-id="e51b0-238">Reference: [Border](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Border)</span></span>

### <a name="canvas"></a><span data-ttu-id="e51b0-239">キャンバス</span><span class="sxs-lookup"><span data-stu-id="e51b0-239">Canvas</span></span>
<span data-ttu-id="e51b0-240">キャンバスの左上隅を基準とする子要素の絶対配置をサポートするレイアウト パネル。</span><span class="sxs-lookup"><span data-stu-id="e51b0-240">A layout panel that supports the absolute positioning of child elements relative to the top left corner of the canvas.</span></span>
 
![キャンバス レイアウト パネル](images/controls/canvas.png) 

```xaml
<Canvas Width="120" Height="120">
    <Rectangle Fill="Red"/>
    <Rectangle Fill="Blue" Canvas.Left="20" Canvas.Top="20"/>
    <Rectangle Fill="Green" Canvas.Left="40" Canvas.Top="40"/>
    <Rectangle Fill="Orange" Canvas.Left="60" Canvas.Top="60"/>
</Canvas>
```

<span data-ttu-id="e51b0-242">参照 :[キャンバス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Canvas)</span><span class="sxs-lookup"><span data-stu-id="e51b0-242">Reference: [Canvas](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Canvas)</span></span>
 
### <a name="grid"></a><span data-ttu-id="e51b0-243">グリッド</span><span class="sxs-lookup"><span data-stu-id="e51b0-243">Grid</span></span>
<span data-ttu-id="e51b0-244">複数行と複数列での子要素の配置をサポートするレイアウト パネル。</span><span class="sxs-lookup"><span data-stu-id="e51b0-244">A layout panel that supports the arranging of child elements in rows and columns.</span></span>

![グリッド レイアウト パネル](images/controls/grid.png) 

```xaml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="50"/>
        <RowDefinition Height="50"/>
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="50"/>
        <ColumnDefinition Width="50"/>
    </Grid.ColumnDefinitions>
    <Rectangle Fill="Red"/>
    <Rectangle Fill="Blue" Grid.Row="1"/>
    <Rectangle Fill="Green" Grid.Column="1"/>
    <Rectangle Fill="Orange" Grid.Row="1" Grid.Column="1"/>
</Grid>
```

<span data-ttu-id="e51b0-246">参照 :[グリッド](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid)</span><span class="sxs-lookup"><span data-stu-id="e51b0-246">Reference: [Grid](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Grid)</span></span>
 
### <a name="panning-scroll-viewer"></a><span data-ttu-id="e51b0-247">パン スクロール ビューアー</span><span class="sxs-lookup"><span data-stu-id="e51b0-247">Panning scroll viewer</span></span>
<span data-ttu-id="e51b0-248">「スクロール ビューアー」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-248">See Scroll viewer.</span></span>

### <a name="relativepanel"></a><span data-ttu-id="e51b0-249">RelativePanel</span><span class="sxs-lookup"><span data-stu-id="e51b0-249">RelativePanel</span></span>
<span data-ttu-id="e51b0-250">互いまたは親パネルを基準にして、子オブジェクトの位置を決定し、調整できるパネル。</span><span class="sxs-lookup"><span data-stu-id="e51b0-250">A panel that lets you position and align child objects in relation to each other or the parent panel.</span></span>

![RelativePanel レイアウト パネル](images/controls/relative-panel.png) 

```xaml
<RelativePanel>
    <TextBox x:Name="textBox1" RelativePanel.AlignLeftWithPanel="True"/>
    <Button Content="Submit" RelativePanel.Below="textBox1"/>
</RelativePanel>
```

<span data-ttu-id="e51b0-252">参照 :[RelativePanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RelativePanel)</span><span class="sxs-lookup"><span data-stu-id="e51b0-252">Reference: [RelativePanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RelativePanel)</span></span>

### <a name="scroll-bar"></a><span data-ttu-id="e51b0-253">スクロール バー</span><span class="sxs-lookup"><span data-stu-id="e51b0-253">Scroll bar</span></span>
<span data-ttu-id="e51b0-254">「スクロール ビューアー」をご覧ください </span><span class="sxs-lookup"><span data-stu-id="e51b0-254">See scroll viewer.</span></span> <span data-ttu-id="e51b0-255">(ScrollBar は ScrollViewer の要素です。</span><span class="sxs-lookup"><span data-stu-id="e51b0-255">(ScrollBar is an element of ScrollViewer.</span></span> <span data-ttu-id="e51b0-256">通常、スタンドアロン コントロールとしては使用しません)。</span><span class="sxs-lookup"><span data-stu-id="e51b0-256">You don't typically use it as a stand-alone control.)</span></span>

<span data-ttu-id="e51b0-257">参照 :[スクロール バー](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Primitives.ScrollBar)</span><span class="sxs-lookup"><span data-stu-id="e51b0-257">Reference: [ScrollBar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Primitives.ScrollBar)</span></span>
 
### <a name="scroll-viewer"></a><span data-ttu-id="e51b0-258">スクロール ビューアー</span><span class="sxs-lookup"><span data-stu-id="e51b0-258">Scroll viewer</span></span>
<span data-ttu-id="e51b0-259">ユーザーが、コンテンツのパンとズームを実行できるようにするコンテナー コントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-259">A container control that lets the user pan and zoom its content.</span></span>

```xaml
<ScrollViewer ZoomMode="Enabled" MaxZoomFactor="10" 
              HorizontalScrollMode="Enabled" 
              HorizontalScrollBarVisibility="Visible"
              Height="200" Width="200">
    <Image Source="Assets/Logo.png" Height="400" Width="400"/>
</ScrollViewer>
```

<span data-ttu-id="e51b0-260">参照 :[ScrollViewer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer)</span><span class="sxs-lookup"><span data-stu-id="e51b0-260">Reference: [ScrollViewer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer)</span></span>

<span data-ttu-id="e51b0-261">設計と操作方法:[スクロール、パン コントロールのガイド](scroll-controls.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-261">Design and how-to: [Scroll and panning controls guide](scroll-controls.md)</span></span> 

<span data-ttu-id="e51b0-262">サンプル コード:[XAML のスクロール、パンとズームのサンプル](https://go.microsoft.com/fwlink/p/?linkid=238577)</span><span class="sxs-lookup"><span data-stu-id="e51b0-262">Sample code: [XAML scrolling, panning and zooming sample](https://go.microsoft.com/fwlink/p/?linkid=238577)</span></span>

### <a name="stack-panel"></a><span data-ttu-id="e51b0-263">スタック パネル</span><span class="sxs-lookup"><span data-stu-id="e51b0-263">Stack panel</span></span>
<span data-ttu-id="e51b0-264">子要素を水平方向または垂直方向の単一行に配置するレイアウト パネル。</span><span class="sxs-lookup"><span data-stu-id="e51b0-264">A layout panel that arranges child elements into a single line that can be oriented horizontally or vertically.</span></span>

![スタック パネル レイアウト コントロール](images/controls/stack-panel.png) 

```xaml
<StackPanel>
    <Rectangle Fill="Red"/>
    <Rectangle Fill="Blue"/>
    <Rectangle Fill="Green"/>
    <Rectangle Fill="Orange"/>
</StackPanel>
```

<span data-ttu-id="e51b0-266">参照 :[StackPanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.StackPanel)</span><span class="sxs-lookup"><span data-stu-id="e51b0-266">Reference: [StackPanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.StackPanel)</span></span>
 
### <a name="variablesizedwrapgrid"></a><span data-ttu-id="e51b0-267">VariableSizedWrapGrid</span><span class="sxs-lookup"><span data-stu-id="e51b0-267">VariableSizedWrapGrid</span></span>
<span data-ttu-id="e51b0-268">複数行と複数列での子要素の配置をサポートするレイアウト パネル。</span><span class="sxs-lookup"><span data-stu-id="e51b0-268">A layout panel that supports the arranging of child elements in rows and columns.</span></span> <span data-ttu-id="e51b0-269">各子要素を、複数の行と列に配置できます。</span><span class="sxs-lookup"><span data-stu-id="e51b0-269">Each child element can span multiple rows and columns.</span></span>

![可変サイズ折り返しグリッド レイアウト パネル](images/controls/variable-sized-wrap-grid.png) 

```xaml
<VariableSizedWrapGrid MaximumRowsOrColumns="3" ItemHeight="44" ItemWidth="44">
    <Rectangle Fill="Red"/>
    <Rectangle Fill="Blue" Height="80" 
               VariableSizedWrapGrid.RowSpan="2"/>
    <Rectangle Fill="Green" Width="80" 
               VariableSizedWrapGrid.ColumnSpan="2"/>
    <Rectangle Fill="Orange" Height="80" Width="80" 
               VariableSizedWrapGrid.RowSpan="2" 
               VariableSizedWrapGrid.ColumnSpan="2"/>
</VariableSizedWrapGrid>
```

<span data-ttu-id="e51b0-271">参照 :[VariableSizedWrapGrid](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.VariableSizedWrapGrid)</span><span class="sxs-lookup"><span data-stu-id="e51b0-271">Reference: [VariableSizedWrapGrid](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.VariableSizedWrapGrid)</span></span>

### <a name="viewbox"></a><span data-ttu-id="e51b0-272">Viewbox</span><span class="sxs-lookup"><span data-stu-id="e51b0-272">Viewbox</span></span>
<span data-ttu-id="e51b0-273">コンテンツを指定されたサイズに拡大縮小するコンテナー コントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-273">A container control that scales its content to a specified size.</span></span>

![Viewbox コントロール](images/controls/view-box.png) 

```xaml
<Viewbox MaxWidth="25" MaxHeight="25">
    <Image Source="Assets/Logo.png"/>
</Viewbox>
<Viewbox MaxWidth="75" MaxHeight="75">
    <Image Source="Assets/Logo.png"/>
</Viewbox>
<Viewbox MaxWidth="150" MaxHeight="150">
    <Image Source="Assets/Logo.png"/>
</Viewbox>
```

<span data-ttu-id="e51b0-275">参照 :[Viewbox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Viewbox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-275">Reference: [Viewbox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Viewbox)</span></span>
 
### <a name="zooming-scroll-viewer"></a><span data-ttu-id="e51b0-276">ズーム スクロール ビューアー</span><span class="sxs-lookup"><span data-stu-id="e51b0-276">Zooming scroll viewer</span></span>
<span data-ttu-id="e51b0-277">「スクロール ビューアー」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-277">See Scroll viewer.</span></span>

## <a name="media-controls"></a><span data-ttu-id="e51b0-278">メディア コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-278">Media controls</span></span>

### <a name="audio"></a><span data-ttu-id="e51b0-279">オーディオ</span><span class="sxs-lookup"><span data-stu-id="e51b0-279">Audio</span></span>
<span data-ttu-id="e51b0-280">「メディア要素」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-280">See Media element.</span></span>

### <a name="media-element"></a><span data-ttu-id="e51b0-281">メディア要素</span><span class="sxs-lookup"><span data-stu-id="e51b0-281">Media element</span></span>
<span data-ttu-id="e51b0-282">オーディオとビデオのコンテンツを再生するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-282">A control that plays audio and video content.</span></span>

```xaml
<MediaElement x:Name="myMediaElement"/>
```

<span data-ttu-id="e51b0-283">参照 :[MediaElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement)</span><span class="sxs-lookup"><span data-stu-id="e51b0-283">Reference: [MediaElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement)</span></span> 

<span data-ttu-id="e51b0-284">設計と操作方法:[メディア要素のコントロールのガイド](media-playback.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-284">Design and how-to: [Media element control guide](media-playback.md)</span></span>

### <a name="mediatransportcontrols"></a><span data-ttu-id="e51b0-285">MediaTransportControls</span><span class="sxs-lookup"><span data-stu-id="e51b0-285">MediaTransportControls</span></span>
<span data-ttu-id="e51b0-286">MediaElement の再生コントロールを提供するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-286">A control that provides playback controls for a MediaElement.</span></span>

![トランスポート コントロールを含むメディア要素](images/controls/media-transport-controls.png) 

```xaml
<MediaTransportControls MediaElement="myMediaElement"/>
```

<span data-ttu-id="e51b0-288">参照 :[MediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls)</span><span class="sxs-lookup"><span data-stu-id="e51b0-288">Reference: [MediaTransportControls](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls)</span></span> 

<span data-ttu-id="e51b0-289">設計と操作方法:[メディア要素のコントロールのガイド](media-playback.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-289">Design and how-to: [Media element control guide](media-playback.md)</span></span> 

<span data-ttu-id="e51b0-290">サンプル コード:[メディアのトランスポート コントロールのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=620023)</span><span class="sxs-lookup"><span data-stu-id="e51b0-290">Sample code: [Media Transport Controls sample](https://go.microsoft.com/fwlink/p/?LinkId=620023)</span></span>

### <a name="video"></a><span data-ttu-id="e51b0-291">Video</span><span class="sxs-lookup"><span data-stu-id="e51b0-291">Video</span></span>
<span data-ttu-id="e51b0-292">「メディア要素」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-292">See Media element.</span></span>

## <a name="navigation"></a><span data-ttu-id="e51b0-293">ナビゲーション</span><span class="sxs-lookup"><span data-stu-id="e51b0-293">Navigation</span></span>

### <a name="navigationview"></a><span data-ttu-id="e51b0-294">NavigationView</span><span class="sxs-lookup"><span data-stu-id="e51b0-294">NavigationView</span></span>

<span data-ttu-id="e51b0-295">適応性のあるコンテナーと、左側のナビゲーション ウィンドウで、上部のナビゲーションとタブ パターンを実装する柔軟なナビゲーション モデルの場合。</span><span class="sxs-lookup"><span data-stu-id="e51b0-295">An adaptable container and flexible navigation model that implements the left navigation pane, top navigation and tabs pattern.</span></span>

<span data-ttu-id="e51b0-296">参照 :[NavigationView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview)</span><span class="sxs-lookup"><span data-stu-id="e51b0-296">Reference: [NavigationView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview)</span></span>

<span data-ttu-id="e51b0-297">設計と操作方法:[NavigationView コントロールのガイド](navigationview.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-297">Design and how-to: [NavigationView control guide](navigationview.md)</span></span>

### <a name="splitview"></a><span data-ttu-id="e51b0-298">SplitView</span><span class="sxs-lookup"><span data-stu-id="e51b0-298">SplitView</span></span>

<span data-ttu-id="e51b0-299">2 つのビューを持つコンテナー コントロール。1 つはメイン コンテンツ用で、もう 1 つは、通常、ナビゲーション メニューに使います。</span><span class="sxs-lookup"><span data-stu-id="e51b0-299">A container control with two views; one view for the main content and another view that is typically used for a navigation menu.</span></span>

![分割ビュー コントロール](images/controls/split-view.png) 

```xaml
<SplitView>
    <SplitView.Pane>
        <!-- Menu content -->
    </SplitView.Pane>
    <SplitView.Content>
        <!-- Main content -->
    </SplitView.Content>
</SplitView>
```

<span data-ttu-id="e51b0-301">参照 :[SplitView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SplitView)</span><span class="sxs-lookup"><span data-stu-id="e51b0-301">Reference: [SplitView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SplitView)</span></span> 

<span data-ttu-id="e51b0-302">設計と操作方法:[分割ビュー コントロールのガイド](split-view.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-302">Design and how-to: [Split view control guide](split-view.md)</span></span>

### <a name="web-view"></a><span data-ttu-id="e51b0-303">Web ビュー</span><span class="sxs-lookup"><span data-stu-id="e51b0-303">Web view</span></span>

<span data-ttu-id="e51b0-304">Web コンテンツをホストするコンテナー コントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-304">A container control that hosts web content.</span></span>

```xaml
<WebView x:Name="webView1" Source="https://developer.microsoft.com" 
         Height="400" Width="800"/>
```

<span data-ttu-id="e51b0-305">参照 :[WebView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.WebView)</span><span class="sxs-lookup"><span data-stu-id="e51b0-305">Reference: [WebView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.WebView)</span></span> 

<span data-ttu-id="e51b0-306">設計と操作方法:Web ビューのガイドライン</span><span class="sxs-lookup"><span data-stu-id="e51b0-306">Design and how-to: Guidelines for Web views</span></span> 

<span data-ttu-id="e51b0-307">サンプル コード:[XAML の WebView コントロールのサンプル](https://go.microsoft.com/fwlink/p/?linkid=238582)</span><span class="sxs-lookup"><span data-stu-id="e51b0-307">Sample code: [XAML WebView control sample](https://go.microsoft.com/fwlink/p/?linkid=238582)</span></span>

### <a name="semantic-zoom"></a><span data-ttu-id="e51b0-308">セマンティック ズーム</span><span class="sxs-lookup"><span data-stu-id="e51b0-308">Semantic zoom</span></span>

<span data-ttu-id="e51b0-309">ユーザーが、項目のコレクションの 2 つの異なる表示の間でズームを実行できるようにするコンテナー コントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-309">A container control that lets the user zoom between two views of a collection of items.</span></span>

```xaml
<SemanticZoom>
    <ZoomedInView>
        <GridView></GridView>
    </ZoomedInView>
    <ZoomedOutView>
        <GridView></GridView>
    </ZoomedOutView>
</SemanticZoom>
```

<span data-ttu-id="e51b0-310">参照 :[SemanticZoom](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom)</span><span class="sxs-lookup"><span data-stu-id="e51b0-310">Reference: [SemanticZoom](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom)</span></span> 

<span data-ttu-id="e51b0-311">設計と操作方法:[セマンティック ズーム コントロールのガイド](semantic-zoom.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-311">Design and how-to: [Semantic zoom control guide](semantic-zoom.md)</span></span>

<span data-ttu-id="e51b0-312">サンプル コード:[XAML の GridView のグループ化と SemanticZoom サンプル](https://go.microsoft.com/fwlink/p/?linkid=226564)</span><span class="sxs-lookup"><span data-stu-id="e51b0-312">Sample code: [XAML GridView grouping and SemanticZoom sample](https://go.microsoft.com/fwlink/p/?linkid=226564)</span></span>

## <a name="progress-controls"></a><span data-ttu-id="e51b0-313">プログレス コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-313">Progress controls</span></span>

### <a name="progress-bar"></a><span data-ttu-id="e51b0-314">進行状況バー</span><span class="sxs-lookup"><span data-stu-id="e51b0-314">Progress bar</span></span>
<span data-ttu-id="e51b0-315">バーを表示して進行状況を示すコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-315">A control that indicates progress by displaying a bar.</span></span>

![進行状況バー コントロール](images/controls/progress-bar-determinate.png)

<span data-ttu-id="e51b0-317">特定の値を表示する進行状況バー。</span><span class="sxs-lookup"><span data-stu-id="e51b0-317">A progress bar that shows a specific value.</span></span>

```xaml
<ProgressBar x:Name="progressBar1" Value="50" Width="100"/>
```

![進行状況不定バー コントロール](images/controls/progress-bar-indeterminate.png)

<span data-ttu-id="e51b0-319">進行状況が不定であることを表す進行状況バー。</span><span class="sxs-lookup"><span data-stu-id="e51b0-319">A progress bar that shows indeterminate progress.</span></span>

```xaml
<ProgressBar x:Name="indeterminateProgressBar1" IsIndeterminate="True" Width="100"/>
```

<span data-ttu-id="e51b0-320">参照 :[ProgressBar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ProgressBar)</span><span class="sxs-lookup"><span data-stu-id="e51b0-320">Reference: [ProgressBar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ProgressBar)</span></span> 

<span data-ttu-id="e51b0-321">設計と操作方法:[進行状況コントロールのガイド](progress-controls.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-321">Design and how-to: [Progress controls guide](progress-controls.md)</span></span> 

### <a name="progress-ring"></a><span data-ttu-id="e51b0-322">進行状況リング</span><span class="sxs-lookup"><span data-stu-id="e51b0-322">Progress ring</span></span>
<span data-ttu-id="e51b0-323">リングを表示して進行状況が不定であることを示すコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-323">A control that indicates indeterminate progress by displaying a ring.</span></span> 

![進行状況リング コントロール](images/controls/progress-ring.png) 

```xaml
<ProgressRing x:Name="progressRing1" IsActive="True"/>
```

<span data-ttu-id="e51b0-325">参照 :[ProgressRing](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ProgressRing)</span><span class="sxs-lookup"><span data-stu-id="e51b0-325">Reference: [ProgressRing](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ProgressRing)</span></span> 

<span data-ttu-id="e51b0-326">設計と操作方法:[進行状況コントロールのガイド](progress-controls.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-326">Design and how-to: [Progress controls guide](progress-controls.md)</span></span> 

## <a name="text-controls"></a><span data-ttu-id="e51b0-327">テキスト コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-327">Text controls</span></span>

### <a name="auto-suggest-box"></a><span data-ttu-id="e51b0-328">自動提案ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-328">Auto suggest box</span></span>
<span data-ttu-id="e51b0-329">ユーザーが入力するときに、候補のテキストを表示するテキスト入力ボックスです。</span><span class="sxs-lookup"><span data-stu-id="e51b0-329">A text input box that provides suggested text as the user types.</span></span>

![検索の自動提案ボックス](images/controls/auto-suggest-box.png) 

<span data-ttu-id="e51b0-331">参照 :[AutoSuggestBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AutoSuggestBox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-331">Reference: [AutoSuggestBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AutoSuggestBox)</span></span>

<span data-ttu-id="e51b0-332">設計と操作方法:[テキスト コントロール](text-controls.md)、 [Auto suggest ボックス コントロールのガイド](auto-suggest-box.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-332">Design and how-to: [Text controls](text-controls.md), [Auto suggest box control guide](auto-suggest-box.md)</span></span>

<span data-ttu-id="e51b0-333">サンプル コード:[AutoSuggestBox 移行のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=619996)</span><span class="sxs-lookup"><span data-stu-id="e51b0-333">Sample code: [AutoSuggestBox migration sample](https://go.microsoft.com/fwlink/p/?LinkId=619996)</span></span>

### <a name="multi-line-text-box"></a><span data-ttu-id="e51b0-334">複数行テキスト ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-334">Multi-line text box</span></span>
<span data-ttu-id="e51b0-335">「テキスト ボックス」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-335">See Text box.</span></span>

### <a name="password-box"></a><span data-ttu-id="e51b0-336">パスワード ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-336">Password box</span></span>
<span data-ttu-id="e51b0-337">パスワードを入力するためのコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-337">A control for entering passwords.</span></span>

 ![パスワード ボックス](images/controls/password-box.png)

```xaml
<PasswordBox x:Name="passwordBox1" 
             PasswordChanged="PasswordBox_PasswordChanged" />
```

<span data-ttu-id="e51b0-339">参照 :[PasswordBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.PasswordBox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-339">Reference: [PasswordBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.PasswordBox)</span></span> 

<span data-ttu-id="e51b0-340">設計と操作方法:[テキスト コントロール](text-controls.md)、[パスワード ボックス コントロールのガイド](password-box.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-340">Design and how-to: [Text controls](text-controls.md), [Password box control guide](password-box.md)</span></span> 

<span data-ttu-id="e51b0-341">サンプル コード:[XAML テキスト表示サンプル](https://go.microsoft.com/fwlink/p/?linkid=238579)、 [XAML テキストのサンプルの編集](https://go.microsoft.com/fwlink/p/?linkid=251417)</span><span class="sxs-lookup"><span data-stu-id="e51b0-341">Sample code: [XAML text display sample](https://go.microsoft.com/fwlink/p/?linkid=238579), [XAML text editing sample](https://go.microsoft.com/fwlink/p/?linkid=251417)</span></span>

### <a name="rich-edit-box"></a><span data-ttu-id="e51b0-342">リッチ エディット ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-342">Rich edit box</span></span>
<span data-ttu-id="e51b0-343">書式付きテキスト、ハイパーリンク、イメージなどを含んだリッチ テキスト ドキュメントを編集できるコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-343">A control that lets a user edit rich text documents with content like formatted text, hyperlinks, and images.</span></span>

```xaml
<RichEditBox />
```

<span data-ttu-id="e51b0-344">参照 :[RichEditBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-344">Reference: [RichEditBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox)</span></span> 

<span data-ttu-id="e51b0-345">設計と操作方法:[テキスト コントロール](text-controls.md)、[リッチ エディット ボックス コントロールのガイド](rich-edit-box.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-345">Design and how-to: [Text controls](text-controls.md), [Rich edit box control guide](rich-edit-box.md)</span></span>

<span data-ttu-id="e51b0-346">サンプル コード:[XAML テキストのサンプル](https://go.microsoft.com/fwlink/p/?linkid=238578)</span><span class="sxs-lookup"><span data-stu-id="e51b0-346">Sample code: [XAML text sample](https://go.microsoft.com/fwlink/p/?linkid=238578)</span></span>

### <a name="search-box"></a><span data-ttu-id="e51b0-347">検索ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-347">Search box</span></span>
<span data-ttu-id="e51b0-348">「自動提案ボックス」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-348">See Auto suggest box.</span></span>

### <a name="single-line-text-box"></a><span data-ttu-id="e51b0-349">単一行テキスト ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-349">Single-line text box</span></span>
<span data-ttu-id="e51b0-350">「テキスト ボックス」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-350">See Text box.</span></span>

### <a name="static-textparagraph"></a><span data-ttu-id="e51b0-351">静的テキスト/段落</span><span class="sxs-lookup"><span data-stu-id="e51b0-351">Static text/paragraph</span></span>
<span data-ttu-id="e51b0-352">「テキスト ブロック」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="e51b0-352">See Text block.</span></span>

### <a name="text-block"></a><span data-ttu-id="e51b0-353">テキスト ブロック</span><span class="sxs-lookup"><span data-stu-id="e51b0-353">Text block</span></span>
<span data-ttu-id="e51b0-354">テキストを表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-354">A control that displays text.</span></span>

![テキスト ブロック コントロール](images/controls/text-block.png) 

```xaml
<TextBlock x:Name="textBlock1" Text="I am a TextBlock"/>
```

<span data-ttu-id="e51b0-356">参照 :[TextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock)、 [RichTextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock)</span><span class="sxs-lookup"><span data-stu-id="e51b0-356">Reference: [TextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock), [RichTextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock)</span></span> 

<span data-ttu-id="e51b0-357">設計と操作方法:[テキスト コントロール](text-controls.md)、[テキスト ブロック コントロール ガイド](text-block.md)、[リッチ テキスト ブロック コントロールのガイド](rich-text-block.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-357">Design and how-to: [Text controls](text-controls.md), [Text block control guide](text-block.md), [Rich text block control guide](rich-text-block.md)</span></span>

<span data-ttu-id="e51b0-358">サンプル コード:[XAML テキストのサンプル](https://go.microsoft.com/fwlink/p/?linkid=238578)</span><span class="sxs-lookup"><span data-stu-id="e51b0-358">Sample code: [XAML text sample](https://go.microsoft.com/fwlink/p/?linkid=238578)</span></span>

### <a name="text-box"></a><span data-ttu-id="e51b0-359">テキスト ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-359">Text box</span></span>
<span data-ttu-id="e51b0-360">1 行または複数行のプレーンテキスト フィールド。</span><span class="sxs-lookup"><span data-stu-id="e51b0-360">A single-line or multi-line plain text field.</span></span>

![テキスト ボックス コントロール](images/controls/text-box.png) 

```xaml
<TextBox x:Name="textBox1" Text="I am a TextBox" 
         TextChanged="TextBox_TextChanged"/>
```

<span data-ttu-id="e51b0-362">参照 :[TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-362">Reference: [TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox)</span></span> 

<span data-ttu-id="e51b0-363">設計と操作方法:[テキスト コントロール](text-controls.md)、[テキスト ボックス コントロールのガイド](text-box.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-363">Design and how-to: [Text controls](text-controls.md), [Text box control guide](text-box.md)</span></span> 

<span data-ttu-id="e51b0-364">サンプル コード:[XAML テキストのサンプル](https://go.microsoft.com/fwlink/p/?linkid=238578)</span><span class="sxs-lookup"><span data-stu-id="e51b0-364">Sample code: [XAML text sample](https://go.microsoft.com/fwlink/p/?linkid=238578)</span></span>

## <a name="selection-controls"></a><span data-ttu-id="e51b0-365">選択コントロール</span><span class="sxs-lookup"><span data-stu-id="e51b0-365">Selection controls</span></span>

### <a name="check-box"></a><span data-ttu-id="e51b0-366">チェック ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-366">Check box</span></span>
<span data-ttu-id="e51b0-367">ユーザーがオンまたはオフにできるコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-367">A control that a user can select or clear.</span></span>

![チェック ボックスの 3 状態](images/templates-checkbox-states-default.png)

```xaml
<CheckBox x:Name="checkbox1" Content="CheckBox" 
          Checked="CheckBox_Checked"/>
```

<span data-ttu-id="e51b0-369">参照 :[チェック ボックス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-369">Reference: [CheckBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox)</span></span> 

<span data-ttu-id="e51b0-370">設計と操作方法:[チェック ボックス コントロールのガイド](checkbox.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-370">Design and how-to: [Check box control guide](checkbox.md)</span></span> 

### <a name="combo-box"></a><span data-ttu-id="e51b0-371">コンボ ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-371">Combo box</span></span>
<span data-ttu-id="e51b0-372">ユーザーが選択できる項目のドロップダウン リスト。</span><span class="sxs-lookup"><span data-stu-id="e51b0-372">A drop-down list of items a user can select from.</span></span>

![開かれた状態のコンボ ボックス](images/controls/combo-box-open.png) 

```xaml
<ComboBox x:Name="comboBox1" Width="100"
          SelectionChanged="ComboBox_SelectionChanged">
    <x:String>Item 1</x:String>
    <x:String>Item 2</x:String>
    <x:String>Item 3</x:String>
</ComboBox>
```

<span data-ttu-id="e51b0-374">参照 :[ComboBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ComboBox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-374">Reference: [ComboBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ComboBox)</span></span> 

<span data-ttu-id="e51b0-375">設計と操作方法:[リスト](lists.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-375">Design and how-to: [Lists](lists.md)</span></span> 

### <a name="list-box"></a><span data-ttu-id="e51b0-376">リスト ボックス</span><span class="sxs-lookup"><span data-stu-id="e51b0-376">List box</span></span>
<span data-ttu-id="e51b0-377">ユーザーが選択できる項目のインライン リストを表示するコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-377">A control that presents an inline list of items that the user can select from.</span></span> 

![リスト ボックス コントロール](images/controls/list-box.png)

```xaml
<ListBox x:Name="listBox1" Width="100"
         SelectionChanged="ListBox_SelectionChanged">
    <x:String>Item 1</x:String>
    <x:String>Item 2</x:String>
    <x:String>Item 3</x:String>
</ListBox>
```

<span data-ttu-id="e51b0-379">参照 :[ListBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox)</span><span class="sxs-lookup"><span data-stu-id="e51b0-379">Reference: [ListBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox)</span></span> 

<span data-ttu-id="e51b0-380">設計と操作方法:[リスト](lists.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-380">Design and how-to: [Lists](lists.md)</span></span> 

### <a name="radio-button"></a><span data-ttu-id="e51b0-381">ラジオ ボタン</span><span class="sxs-lookup"><span data-stu-id="e51b0-381">Radio button</span></span>
<span data-ttu-id="e51b0-382">ユーザーがオプションのグループから 1 つのオプションを選択できるようにするコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-382">A control that allows a user to select a single option from a group of options.</span></span> <span data-ttu-id="e51b0-383">グループ化されたラジオ ボタンは、それぞれ相互に排他的です。</span><span class="sxs-lookup"><span data-stu-id="e51b0-383">When radio buttons are grouped together, they are mutually exclusive.</span></span>

![ラジオ ボタン コントロール](images/controls/radio-button.png)

```xaml
<RadioButton x:Name="radioButton1" Content="RadioButton 1" GroupName="Group1" 
             Checked="RadioButton_Checked"/>
<RadioButton x:Name="radioButton2" Content="RadioButton 2" GroupName="Group1" 
             Checked="RadioButton_Checked" IsChecked="True"/>
<RadioButton x:Name="radioButton3" Content="RadioButton 3" GroupName="Group1" 
             Checked="RadioButton_Checked"/>
```

<span data-ttu-id="e51b0-385">参照 :[オプション ボタン](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RadioButton)</span><span class="sxs-lookup"><span data-stu-id="e51b0-385">Reference: [RadioButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RadioButton)</span></span> 

<span data-ttu-id="e51b0-386">設計と操作方法:[ラジオ ボタン コントロールのガイド](radio-button.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-386">Design and how-to: [Radio button control guide](radio-button.md)</span></span>
 
### <a name="slider"></a><span data-ttu-id="e51b0-387">スライダー</span><span class="sxs-lookup"><span data-stu-id="e51b0-387">Slider</span></span>
<span data-ttu-id="e51b0-388">ユーザーがトラックに沿って Thumb コントロールを動かすことで値の範囲から選択できるようにするコントロール。</span><span class="sxs-lookup"><span data-stu-id="e51b0-388">A control that lets the user select from a range of values by moving a Thumb control along a track.</span></span>

![スライダー コントロール](images/controls/slider.png)

```xaml
<Slider x:Name="slider1" Width="100" ValueChanged="Slider_ValueChanged" />
```

<span data-ttu-id="e51b0-390">参照 :[スライダー](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Slider)</span><span class="sxs-lookup"><span data-stu-id="e51b0-390">Reference: [Slider](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Slider)</span></span> 

<span data-ttu-id="e51b0-391">設計と操作方法:[スライダー コントロールのガイド](slider.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-391">Design and how-to: [Slider control guide](slider.md)</span></span> 

### <a name="toggle-button"></a><span data-ttu-id="e51b0-392">トグル ボタン</span><span class="sxs-lookup"><span data-stu-id="e51b0-392">Toggle button</span></span>
<span data-ttu-id="e51b0-393">2 つの状態を切り替えることができるボタン。</span><span class="sxs-lookup"><span data-stu-id="e51b0-393">A button that can be toggled between 2 states.</span></span>

```xaml
<ToggleButton x:Name="toggleButton1" Content="Button" 
              Checked="ToggleButton_Checked"/>
```

<span data-ttu-id="e51b0-394">参照 :[トグル ボタン](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Primitives.ToggleButton)</span><span class="sxs-lookup"><span data-stu-id="e51b0-394">Reference: [ToggleButton](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Primitives.ToggleButton)</span></span>

<span data-ttu-id="e51b0-395">設計と操作方法:[切り替えコントロールのガイド](toggles.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-395">Design and how-to: [Toggle control guide](toggles.md)</span></span> 

### <a name="toggle-switch"></a><span data-ttu-id="e51b0-396">トグル スイッチ</span><span class="sxs-lookup"><span data-stu-id="e51b0-396">Toggle switch</span></span>
<span data-ttu-id="e51b0-397">2 つの状態を切り替えることができるスイッチ。</span><span class="sxs-lookup"><span data-stu-id="e51b0-397">A switch that can be toggled between 2 states.</span></span>

![トグル スイッチ コントロール](images/controls/toggle-switch.png) 

```xaml
<ToggleSwitch x:Name="toggleSwitch1" Header="ToggleSwitch" 
              OnContent="On" OffContent="Off" 
              Toggled="ToggleSwitch_Toggled"/>
```

<span data-ttu-id="e51b0-399">参照 :[ToggleSwitch](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToggleSwitch)</span><span class="sxs-lookup"><span data-stu-id="e51b0-399">Reference: [ToggleSwitch](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ToggleSwitch)</span></span> 

<span data-ttu-id="e51b0-400">設計と操作方法:[切り替えコントロールのガイド](toggles.md)</span><span class="sxs-lookup"><span data-stu-id="e51b0-400">Design and how-to: [Toggle control guide](toggles.md)</span></span> 
