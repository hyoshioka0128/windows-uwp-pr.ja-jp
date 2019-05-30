---
Description: TimePicker は、ユーザーがタッチ、マウス、またはキーボード入力を使って時刻値を選択できる標準化された方法です。
title: 時刻の選択コントロール
ms.assetid: 5124ecda-09e6-449e-9d4a-d969dca46aa3
label: Time picker
template: detail.hbs
ms.date: 05/08/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: kisai
design-contact: ksulliv
dev-contact: joyate
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 58321c6c32536c07d3a56a05ce26b353ec32a982
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66364156"
---
# <a name="time-picker"></a><span data-ttu-id="6fcac-104">時刻の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="6fcac-104">Time picker</span></span>
 

<span data-ttu-id="6fcac-105">TimePicker は、ユーザーがタッチ、マウス、またはキーボード入力を使って時刻値を選択できる標準化された方法です。</span><span class="sxs-lookup"><span data-stu-id="6fcac-105">The time picker gives you a standardized way to let users pick a time value using touch, mouse, or keyboard input.</span></span> 

> <span data-ttu-id="6fcac-106">**重要な API**:[TimePicker クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TimePicker)、[時刻プロパティ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.timepicker.time)</span><span class="sxs-lookup"><span data-stu-id="6fcac-106">**Important APIs**: [TimePicker class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TimePicker), [Time property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.timepicker.time)</span></span>


## <a name="is-this-the-right-control"></a><span data-ttu-id="6fcac-107">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="6fcac-107">Is this the right control?</span></span>
<span data-ttu-id="6fcac-108">時刻の選択コントロールを使って、ユーザーが 1 つの時刻を選べるようにします。</span><span class="sxs-lookup"><span data-stu-id="6fcac-108">Use a time picker to let a user pick a single time value.</span></span>

<span data-ttu-id="6fcac-109">適切なコントロールの選択について詳しくは、「[日付と時刻コントロール](date-and-time.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="6fcac-109">For more info about choosing the right control, see the [Date and time controls](date-and-time.md) article.</span></span>

## <a name="examples"></a><span data-ttu-id="6fcac-110">例</span><span class="sxs-lookup"><span data-stu-id="6fcac-110">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="6fcac-111">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="6fcac-111">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="6fcac-112"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/TimePicker">アプリを開き、TimePicker の動作を確認</a>してください。</span><span class="sxs-lookup"><span data-stu-id="6fcac-112">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/TimePicker">open the app and see the TimePicker in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="6fcac-113"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="6fcac-113"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="6fcac-114"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="6fcac-114"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

<span data-ttu-id="6fcac-115">エントリ ポイントには、選んだ時刻が表示されます。ユーザーがエントリ ポイントを選ぶと、選択ツール サーフェスが中央から縦方向に展開されて、時刻を選べるようになります。</span><span class="sxs-lookup"><span data-stu-id="6fcac-115">The entry point displays the chosen time, and when the user selects the entry point, a picker surface expands vertically from the middle for the user to make a selection.</span></span> <span data-ttu-id="6fcac-116">時刻の選択は他の UI をオーバーレイし、他の UI を別の位置に移動させることはありません。</span><span class="sxs-lookup"><span data-stu-id="6fcac-116">The time picker overlays other UI; it doesn't push other UI out of the way.</span></span>

![展開した時刻の選択コントロールの例](images/controls_timepicker_expand.png)

## <a name="create-a-time-picker"></a><span data-ttu-id="6fcac-118">時刻の選択コントロールの作成</span><span class="sxs-lookup"><span data-stu-id="6fcac-118">Create a time picker</span></span>

<span data-ttu-id="6fcac-119">次の例は、ヘッダーを含むシンプルな時刻の選択コントロールを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="6fcac-119">This example shows how to create a simple time picker with a header.</span></span>

```xaml
<TimePicker x:Name=arrivalTimePicker Header="Arrival time"/>
```

```csharp
TimePicker arrivalTimePicker = new TimePicker();
arrivalTimePicker.Header = "Arrival time";
```

<span data-ttu-id="6fcac-120">結果として、時刻の選択コントロールは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="6fcac-120">The resulting time picker looks like this:</span></span>

![時刻の選択コントロールの例](images/time-picker-closed.png)

> [!NOTE]
> <span data-ttu-id="6fcac-122">日付と時刻の値の重要な情報については、「*日付と時刻コントロール*」の「[DateTime と Calendar の値](date-and-time.md#datetime-and-calendar-values)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="6fcac-122">For important info about date and time values, see [DateTime and Calendar values](date-and-time.md#datetime-and-calendar-values) in the *Date and time controls* article.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="6fcac-123">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="6fcac-123">Get the sample code</span></span>

- <span data-ttu-id="6fcac-124">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="6fcac-124">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-topics"></a><span data-ttu-id="6fcac-125">関連トピック</span><span class="sxs-lookup"><span data-stu-id="6fcac-125">Related topics</span></span>

- [<span data-ttu-id="6fcac-126">日付と時刻コントロール</span><span class="sxs-lookup"><span data-stu-id="6fcac-126">Date and time controls</span></span>](date-and-time.md)
- [<span data-ttu-id="6fcac-127">カレンダーの日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="6fcac-127">Calendar date picker</span></span>](calendar-date-picker.md)
- [<span data-ttu-id="6fcac-128">カレンダー ビュー</span><span class="sxs-lookup"><span data-stu-id="6fcac-128">Calendar view</span></span>](calendar-view.md)
- [<span data-ttu-id="6fcac-129">日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="6fcac-129">Date picker</span></span>](date-picker.md)
