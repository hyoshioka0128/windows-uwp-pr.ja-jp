---
Description: 隣接するコントロールに入力する必要がある内容をユーザーに説明するためにラベルを使います。 また、関連するコントロールのグループにラベルを付けることや、関連するコントロールのグループの近くに説明テキストを表示することができます。
title: ラベル
ms.assetid: CFACCCD4-749F-43FB-947E-2591AE673804
label: Labels
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: miguelrb
design-contact: ksulliv
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 5996fb15c0d7302c7360c2e45613f0da2720d415
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66364652"
---
# <a name="labels"></a><span data-ttu-id="ec0fd-105">ラベル</span><span class="sxs-lookup"><span data-stu-id="ec0fd-105">Labels</span></span>

 

<span data-ttu-id="ec0fd-106">ラベルは、コントロールまたは関連するコントロールのグループの名前やタイトルです。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-106">A label is the name or title of a control or a group of related controls.</span></span>

> <span data-ttu-id="ec0fd-107">**重要な API**:ヘッダーのプロパティ、 [TextBlock クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock)</span><span class="sxs-lookup"><span data-stu-id="ec0fd-107">**Important APIs**: Header property, [TextBlock class](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock)</span></span>

<span data-ttu-id="ec0fd-108">XAML では、多くのコントロールに組み込みの Header プロパティがあり、これを使ってラベルを表示します。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-108">In XAML, many controls have a built-in Header property that you use to display the label.</span></span> <span data-ttu-id="ec0fd-109">Header プロパティがないコントロールの場合、またはコントロールのグループにラベルを付ける場合は、代わりに [TextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) を使います。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-109">For controls that don't have a Header property, or to label groups of controls, you can use a [TextBlock](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) instead.</span></span>

![標準的なラベル コントロールを示すスクリーンショット](images/label-standard.png)

## <a name="recommendations"></a><span data-ttu-id="ec0fd-111">推奨事項</span><span class="sxs-lookup"><span data-stu-id="ec0fd-111">Recommendations</span></span>


-   <span data-ttu-id="ec0fd-112">隣接するコントロールに入力する必要がある内容をユーザーに説明するためにラベルを使います。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-112">Use a label to indicate to the user what they should enter into an adjacent control.</span></span> <span data-ttu-id="ec0fd-113">また、関連するコントロールのグループにラベルを付けることや、関連するコントロールのグループの近くに説明テキストを表示することができます。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-113">You can also label a group of related controls, or display instructional text near a group of related controls.</span></span>
-   <span data-ttu-id="ec0fd-114">コントロールにラベルを付ける場合、説明テキストの文ではなく、名詞や簡潔な名詞句のラベルを入力します。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-114">When labeling controls, write the label as a noun or a concise noun phrase, not as a sentence, and not as instructional text.</span></span> <span data-ttu-id="ec0fd-115">コロン、その他の句読点は使わないでください。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-115">Avoid colons or other punctuation.</span></span>
-   <span data-ttu-id="ec0fd-116">ラベルに説明テキストを入力するときは、テキスト文字列を長くすることができ、句読点も使うことができます。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-116">When you do have instructional text in a label, you can be more generous with text-string length and also use punctuation.</span></span>


## <a name="get-the-sample-code"></a><span data-ttu-id="ec0fd-117">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="ec0fd-117">Get the sample code</span></span>
* [<span data-ttu-id="ec0fd-118">XAML UI の基本サンプル</span><span class="sxs-lookup"><span data-stu-id="ec0fd-118">XAML UI basics sample</span></span>](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/XamlUIBasics)

## <a name="related-topics"></a><span data-ttu-id="ec0fd-119">関連トピック</span><span class="sxs-lookup"><span data-stu-id="ec0fd-119">Related topics</span></span>
* [<span data-ttu-id="ec0fd-120">テキスト コントロール</span><span class="sxs-lookup"><span data-stu-id="ec0fd-120">Text controls</span></span>](text-controls.md)
* [<span data-ttu-id="ec0fd-121">TextBox.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-121">TextBox.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.header)
* [<span data-ttu-id="ec0fd-122">PasswordBox.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-122">PasswordBox.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.passwordbox.header)
* [<span data-ttu-id="ec0fd-123">ToggleSwitch.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-123">ToggleSwitch.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.toggleswitch.header)
* [<span data-ttu-id="ec0fd-124">DatePicker.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-124">DatePicker.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.datepicker.header)
* [<span data-ttu-id="ec0fd-125">TimePicker.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-125">TimePicker.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.timepicker.header)
* [<span data-ttu-id="ec0fd-126">Slider.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-126">Slider.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.slider.header)
* [<span data-ttu-id="ec0fd-127">ComboBox.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-127">ComboBox.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.combobox.header)
* [<span data-ttu-id="ec0fd-128">RichEditBox.Header プロパティ</span><span class="sxs-lookup"><span data-stu-id="ec0fd-128">RichEditBox.Header property</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richeditbox.header)
* [<span data-ttu-id="ec0fd-129">TextBlock クラス</span><span class="sxs-lookup"><span data-stu-id="ec0fd-129">TextBlock class</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock)

 

 




