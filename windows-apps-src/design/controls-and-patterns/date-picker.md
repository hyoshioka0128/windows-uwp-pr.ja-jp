---
Description: DatePicker は、ユーザーがタッチ、マウス、またはキーボード入力を使ってローカライズされた日付値を選択できる標準化された方法です。
title: 日付の選択コントロール
ms.assetid: d4a01425-4dee-4de3-9a05-3e85c3fc03cb
isNew: true
label: Date picker
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: kisai
design-contact: ksulliv
dev-contact: joyate
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 1b8e03683d38b382d74bd6defbf7732578878960
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66362839"
---
# <a name="date-picker"></a><span data-ttu-id="7d114-104">日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="7d114-104">Date picker</span></span>

 

<span data-ttu-id="7d114-105">DatePicker は、ユーザーがタッチ、マウス、またはキーボード入力を使ってローカライズされた日付値を選択できる標準化された方法です。</span><span class="sxs-lookup"><span data-stu-id="7d114-105">The date picker gives you a standardized way to let users pick a localized date value using touch, mouse, or keyboard input.</span></span> 

> <span data-ttu-id="7d114-106">**重要な API**:[DatePicker クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.DatePicker)、[プロパティの日付](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.datepicker.date)</span><span class="sxs-lookup"><span data-stu-id="7d114-106">**Important APIs**: [DatePicker class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.DatePicker), [Date property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.datepicker.date)</span></span>


## <a name="is-this-the-right-control"></a><span data-ttu-id="7d114-107">適切なコントロールの選択</span><span class="sxs-lookup"><span data-stu-id="7d114-107">Is this the right control?</span></span>
<span data-ttu-id="7d114-108">日付の選択コントロールは、ユーザーが誕生日などの既知の日付 (カレンダーのコンテキストが重要ではない日) を選べるようにする場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="7d114-108">Use a date picker to let a user pick a known date, such as a date of birth, where the context of the calendar is not important.</span></span>

<span data-ttu-id="7d114-109">適切な日付コントロールの選択について詳しくは、「[日付と時刻コントロール](date-and-time.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7d114-109">For more info about choosing the right date control, see the [Date and time controls](date-and-time.md) article.</span></span>

## <a name="examples"></a><span data-ttu-id="7d114-110">例</span><span class="sxs-lookup"><span data-stu-id="7d114-110">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="7d114-111">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="7d114-111">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><span data-ttu-id="7d114-112"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/DatePicker">アプリを開き、DatePicker の動作を確認</a>してください。</span><span class="sxs-lookup"><span data-stu-id="7d114-112">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/DatePicker">open the app and see the DatePicker in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="7d114-113"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="7d114-113"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="7d114-114"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="7d114-114"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

<span data-ttu-id="7d114-115">エントリ ポイントには、選んだ日付が表示されます。ユーザーがエントリ ポイントを選ぶと、選択ツール サーフェイスが中央から縦方向に展開されて、日付を選べるようになります。</span><span class="sxs-lookup"><span data-stu-id="7d114-115">The entry point displays the chosen date, and when the user selects the entry point, a picker surface expands vertically from the middle for the user to make a selection.</span></span> <span data-ttu-id="7d114-116">日付の選択は他の UI をオーバーレイし、他の UI を別の位置に移動させることはありません。</span><span class="sxs-lookup"><span data-stu-id="7d114-116">The date picker overlays other UI; it doesn't push other UI out of the way.</span></span>

![展開した日付の選択コントロールの例](images/controls_datepicker_expand.png)

## <a name="create-a-date-picker"></a><span data-ttu-id="7d114-118">日付の選択コントロールの作成</span><span class="sxs-lookup"><span data-stu-id="7d114-118">Create a date picker</span></span>

<span data-ttu-id="7d114-119">次の例は、ヘッダーを含むシンプルな日付の選択コントロールを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7d114-119">This example shows how to create a simple date picker with a header.</span></span>

```xaml
<DatePicker x:Name=birthDatePicker Header="Date of birth"/>
```

```csharp
DatePicker birthDatePicker = new DatePicker();
birthDatePicker.Header = "Date of birth";
```

<span data-ttu-id="7d114-120">結果として、日付の選択コントロールは、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="7d114-120">The resulting date picker looks like this:</span></span>

![日付の選択コントロールの例](images/date-picker-closed.png)

> <span data-ttu-id="7d114-122">**注:** &nbsp;&nbsp;日付値の重要な情報については、「日付と時刻コントロール」の「[DateTime と Calendar の値](date-and-time.md#datetime-and-calendar-values)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7d114-122">**Note**&nbsp;&nbsp;For important info about date values, see [DateTime and Calendar values](date-and-time.md#datetime-and-calendar-values) in the Date and time controls article.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="7d114-123">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="7d114-123">Get the sample code</span></span>

- <span data-ttu-id="7d114-124">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="7d114-124">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-articles"></a><span data-ttu-id="7d114-125">関連記事</span><span class="sxs-lookup"><span data-stu-id="7d114-125">Related articles</span></span>

- [<span data-ttu-id="7d114-126">日付と時刻コントロール</span><span class="sxs-lookup"><span data-stu-id="7d114-126">Date and time controls</span></span>](date-and-time.md)
- [<span data-ttu-id="7d114-127">カレンダーの日付の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="7d114-127">Calendar date picker</span></span>](calendar-date-picker.md)
- [<span data-ttu-id="7d114-128">カレンダー ビュー</span><span class="sxs-lookup"><span data-stu-id="7d114-128">Calendar view</span></span>](calendar-view.md)
- [<span data-ttu-id="7d114-129">時刻の選択コントロール</span><span class="sxs-lookup"><span data-stu-id="7d114-129">Time picker</span></span>](time-picker.md)
