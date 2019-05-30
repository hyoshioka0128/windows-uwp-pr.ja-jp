---
Description: カレンダーの日付の選択コントロールは、カレンダーの曜日や埋まり具合などのコンテキスト情報が必要となるカレンダー ビューから単一の日付を選ぶ用途に最適なドロップダウン コントロールです。
title: カレンダーの日付の選択コントロール
ms.assetid: 9e0213e0-046a-4906-ba86-0b49be51ca99
label: Calendar date picker
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: kisai
design-contact: ksulliv
dev-contact: joyate
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 4de2f1cefc47e8740bfebbe7853ae317d25ab9d0
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66363219"
---
# <a name="calendar-date-picker"></a><span data-ttu-id="a37e8-104">カレンダーの日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="a37e8-104">Calendar date picker</span></span>

 

<span data-ttu-id="a37e8-105">カレンダーの日付の選択コントロールは、カレンダーの曜日や埋まり具合などのコンテキスト情報が必要となるカレンダー ビューから単一の日付を選ぶ用途に最適なドロップダウン コントロールです。</span><span class="sxs-lookup"><span data-stu-id="a37e8-105">The calendar date picker is a drop down control that’s optimized for picking a single date from a calendar view where contextual information like the day of the week or fullness of the calendar is important.</span></span> <span data-ttu-id="a37e8-106">追加のコンテキストを提供したり、使用可能な日付を制限したりするように、カレンダーを変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-106">You can modify the calendar to provide additional context or to limit available dates.</span></span>

> <span data-ttu-id="a37e8-107">**重要な API**:[CalendarDatePicker クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarDatePicker)、[プロパティを日付](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.date)、 [DateChanged イベント](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.datechanged)</span><span class="sxs-lookup"><span data-stu-id="a37e8-107">**Important APIs**: [CalendarDatePicker class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarDatePicker), [Date property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.date), [DateChanged event](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.datechanged)</span></span>


## <a name="is-this-the-right-control"></a><span data-ttu-id="a37e8-108">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="a37e8-108">Is this the right control?</span></span>
<span data-ttu-id="a37e8-109">**カレンダーの日付の選択コントロール**を使うと、ユーザーはコンテキストに沿ったカレンダー ビューから 1 つの日付を選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-109">Use a **calendar date picker** to let a user pick a single date from a contextual calendar view.</span></span> <span data-ttu-id="a37e8-110">予定日や出発日の選択などに使います。</span><span class="sxs-lookup"><span data-stu-id="a37e8-110">Use it for things like choosing an appointment or departure date.</span></span>

<span data-ttu-id="a37e8-111">ユーザーが誕生日などの既知の日付 (カレンダーのコンテキストとしては重要ではない日) を選べるようにするには、[日付の選択コントロール](date-picker.md)を使うことを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a37e8-111">To let a user pick a known date, such as a date of birth, where the context of the calendar is not important, consider using a [date picker](date-picker.md).</span></span>

<span data-ttu-id="a37e8-112">適切なコントロールの選択について詳しくは、「[日付と時刻コントロール](date-and-time.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a37e8-112">For more info about choosing the right control, see the [Date and time controls](date-and-time.md) article.</span></span>

## <a name="examples"></a><span data-ttu-id="a37e8-113">例</span><span class="sxs-lookup"><span data-stu-id="a37e8-113">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="a37e8-114">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="a37e8-114">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="a37e8-115"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/CalendarDatePicker">アプリを開き、CalendarDatePicker の動作を確認</a>してください。</span><span class="sxs-lookup"><span data-stu-id="a37e8-115">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/CalendarDatePicker">open the app and see the CalendarDatePicker in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="a37e8-116"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="a37e8-116"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="a37e8-117"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="a37e8-117"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

<span data-ttu-id="a37e8-118">日付が設定されていない場合、エントリ ポイントにはプレースホルダー テキストが表示されます。設定されている場合は、選んだ日付が表示されます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-118">The entry point displays placeholder text if a date has not been set; otherwise, it displays the chosen date.</span></span> <span data-ttu-id="a37e8-119">ユーザーがエントリ ポイントを選ぶと、カレンダー ビューが展開されて、ユーザーが日付を選べるようになります。</span><span class="sxs-lookup"><span data-stu-id="a37e8-119">When the user selects the entry point, a calendar view expands for the user to make a date selection.</span></span> <span data-ttu-id="a37e8-120">カレンダー ビューは他の UI をオーバーレイし、他の UI を別の位置に移動させることはありません。</span><span class="sxs-lookup"><span data-stu-id="a37e8-120">The calendar view overlays other UI; it doesn't push other UI out of the way.</span></span>

![カレンダーの日付の選択コントロールの例](images/calendar-date-picker-2-views.png)

## <a name="create-a-date-picker"></a><span data-ttu-id="a37e8-122">日付の選択コントロールの作成</span><span class="sxs-lookup"><span data-stu-id="a37e8-122">Create a date picker</span></span>

```xaml
<CalendarDatePicker x:Name="arrivalCalendarDatePicker" Header="Arrival date"/>
```

```csharp
CalendarDatePicker arrivalCalendarDatePicker = new CalendarDatePicker();
arrivalCalendarDatePicker.Header = "Arrival date";
```

<span data-ttu-id="a37e8-123">結果として、カレンダーの日付の選択コントロールは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-123">The resulting calendar date picker looks like this:</span></span>

![カレンダーの日付の選択コントロールの例](images/calendar-date-picker-closed.png)

<span data-ttu-id="a37e8-125">カレンダーの日付の選択コントロールの内部には、日付選択用の [CalendarView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarView) があります。</span><span class="sxs-lookup"><span data-stu-id="a37e8-125">The calendar date picker has an internal [CalendarView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarView) for picking a date.</span></span> <span data-ttu-id="a37e8-126">CalendarDatePicker には [IsTodayHighlighted](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.istodayhighlighted) や [FirstDayOfWeek](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.firstdayofweek) のような CalendarView プロパティのサブセットが存在し、内部の CalendarView に転送されるため、このサブセットを使って内部の CalendarView を変更できます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-126">A subset of CalendarView properties, like [IsTodayHighlighted](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.istodayhighlighted) and [FirstDayOfWeek](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.firstdayofweek), exist on CalendarDatePicker and are forwarded to the internal CalendarView to let you modify it.</span></span> 

<span data-ttu-id="a37e8-127">ただし、複数選択を許可するために、内部の CalendarView の [SelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendarview.selectionmode) を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="a37e8-127">However, you can't change the [SelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendarview.selectionmode) of the internal CalendarView to allow multiple selection.</span></span> <span data-ttu-id="a37e8-128">ユーザーが複数の日付を選べるようにしたり、カレンダーを常に表示しておく必要がある場合、カレンダーの日付の選択コントロールではなく、カレンダー ビューを使うことを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a37e8-128">If you need to let a user pick multiple dates or need a calendar to be always visible, consider using a calendar view instead of a calendar date picker.</span></span> <span data-ttu-id="a37e8-129">カレンダー表示を変更する方法について詳しくは、「[カレンダー ビュー](calendar-view.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a37e8-129">See the [Calendar view](calendar-view.md) article for more info on how you can modify the calendar display.</span></span>

### <a name="selecting-dates"></a><span data-ttu-id="a37e8-130">日付の選択</span><span class="sxs-lookup"><span data-stu-id="a37e8-130">Selecting dates</span></span>

<span data-ttu-id="a37e8-131">選んだ日付を取得または設定するには、[Date](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.date) プロパティを使います。</span><span class="sxs-lookup"><span data-stu-id="a37e8-131">Use the [Date](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.date) property to get or set the selected date.</span></span> <span data-ttu-id="a37e8-132">既定では、Date プロパティは **null** です。</span><span class="sxs-lookup"><span data-stu-id="a37e8-132">By default, the Date property is **null**.</span></span> <span data-ttu-id="a37e8-133">ユーザーがカレンダー ビューで日付を選ぶと、このプロパティが更新されます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-133">When a user selects a date in the calendar view, this property is updated.</span></span> <span data-ttu-id="a37e8-134">日付をクリアするには、カレンダー ビュー内で選んだ日付をクリックして選択を解除します。</span><span class="sxs-lookup"><span data-stu-id="a37e8-134">A user can clear the date by clicking the selected date in the calendar view to deselect it.</span></span> 

<span data-ttu-id="a37e8-135">次のようなコードで日付を設定できます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-135">You can set the date in your code like this.</span></span>

```csharp
myCalendarDatePicker.Date = new DateTime(1977, 1, 5);
```

<span data-ttu-id="a37e8-136">コードで Date を設定するときに、その値は [MinDate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.mindate) プロパティと [MaxDate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.maxdate) プロパティの制約を受けます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-136">When you set the Date in code, the value is constrained by the [MinDate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.mindate) and [MaxDate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.maxdate) properties.</span></span>
- <span data-ttu-id="a37e8-137">**Date** の値が **MinDate** よりも小さい場合、Date の値は **MinDate** に設定されます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-137">If **Date** is smaller than **MinDate**, the value is set to **MinDate**.</span></span>
- <span data-ttu-id="a37e8-138">**Date** の値が **MaxDate** よりも大きい場合、Date の値は **MaxDate** に設定されます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-138">If **Date** is greater than **MaxDate**, the value is set to **MaxDate**.</span></span>

<span data-ttu-id="a37e8-139">Date 値が変化したときに通知を受け取るには、[DateChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.datechanged) イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="a37e8-139">You can handle the [DateChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.datechanged) event to be notified when the Date value has changed.</span></span>

> [!NOTE]
> <span data-ttu-id="a37e8-140">日付値の重要な情報については、「日付と時刻コントロール」の「[DateTime と Calendar の値](date-and-time.md#datetime-and-calendar-values)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a37e8-140">For important info about date values, see [DateTime and Calendar values](date-and-time.md#datetime-and-calendar-values) in the Date and time controls article.</span></span>

### <a name="setting-a-header-and-placeholder-text"></a><span data-ttu-id="a37e8-141">ヘッダーとプレースホルダー テキストの設定</span><span class="sxs-lookup"><span data-stu-id="a37e8-141">Setting a header and placeholder text</span></span>

<span data-ttu-id="a37e8-142">[Header](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.header) (ラベル) と [PlaceholderText](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.placeholdertext) (透かし) をカレンダーの日付の選択コントロールに追加すると、ユーザーに用途を示すことができます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-142">You can add a [Header](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.header) (or label) and [PlaceholderText](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.placeholdertext) (or watermark) to the calendar date picker to give the user an indication of what it's used for.</span></span> <span data-ttu-id="a37e8-143">ヘッダーの外観をカスタマイズするには、Header ではなく [HeaderTemplate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.headertemplate) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="a37e8-143">To customize the look of the header, you can set the [HeaderTemplate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.headertemplate) property instead of Header.</span></span>

<span data-ttu-id="a37e8-144">既定のプレースホルダー テキストは、"日付を選択" です。</span><span class="sxs-lookup"><span data-stu-id="a37e8-144">The default placeholder text is "select a date".</span></span> <span data-ttu-id="a37e8-145">PlaceholderText プロパティに空の文字列を設定してこのテキストを削除するか、次のようにカスタム テキストを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-145">You can remove this by setting the PlaceholderText property to an empty string, or you can provide custom text as shown here.</span></span>

```xaml
<CalendarDatePicker x:Name="arrivalCalendarDatePicker" Header="Arrival date" 
                    PlaceholderText="Choose your arrival date"/>
```

## <a name="get-the-sample-code"></a><span data-ttu-id="a37e8-146">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="a37e8-146">Get the sample code</span></span>

- <span data-ttu-id="a37e8-147">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="a37e8-147">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a37e8-148">関連記事</span><span class="sxs-lookup"><span data-stu-id="a37e8-148">Related articles</span></span>

- [<span data-ttu-id="a37e8-149">日付と時刻コントロール</span><span class="sxs-lookup"><span data-stu-id="a37e8-149">Date and time controls</span></span>](date-and-time.md)
- [<span data-ttu-id="a37e8-150">カレンダー ビュー</span><span class="sxs-lookup"><span data-stu-id="a37e8-150">Calendar view</span></span>](calendar-view.md)
- [<span data-ttu-id="a37e8-151">日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="a37e8-151">Date picker</span></span>](date-picker.md)
- [<span data-ttu-id="a37e8-152">時刻の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="a37e8-152">Time picker</span></span>](time-picker.md)
