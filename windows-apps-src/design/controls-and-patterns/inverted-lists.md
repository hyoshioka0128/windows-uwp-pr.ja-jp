---
Description: 反転リストを使って新しい項目を下部に追加します。
title: 反転リスト
label: Inverted lists
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 52c1d63d-69c1-48d6-a234-6f39296e4bfd
pm-contact: predavid
design-contact: kimsea
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: c552109b243688c2618425adce797c4d208eac31
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66364775"
---
# <a name="inverted-lists"></a><span data-ttu-id="cca94-104">反転リスト</span><span class="sxs-lookup"><span data-stu-id="cca94-104">Inverted lists</span></span>

 

<span data-ttu-id="cca94-105">リスト ビューを使って、送信者と受信者を見た目で区別しやすい項目を利用するチャット エクスペリエンスで会話を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="cca94-105">You can use a list view to present a conversation in a chat experience with items that are visually distinct to represent the sender/receiver.</span></span>  <span data-ttu-id="cca94-106">異なる色と水平方向の配置を使って送信者と受信者のメッセージを区別すると、ユーザーはすばやく自分の会話の位置を確認できます。</span><span class="sxs-lookup"><span data-stu-id="cca94-106">Using different colors and horizontal alignment to separate messages from the sender/receiver helps the user quickly orient themselves in a conversation.</span></span>

> <span data-ttu-id="cca94-107">**重要な API**:[ListView クラス](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listview)、 [ItemsStackPanel クラス](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel)、 [ItemsUpdatingScrollMode プロパティ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel.itemsupdatingscrollmode)</span><span class="sxs-lookup"><span data-stu-id="cca94-107">**Important APIs**:  [ListView class](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listview), [ItemsStackPanel class](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel), [ItemsUpdatingScrollMode property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel.itemsupdatingscrollmode)</span></span>
 
<span data-ttu-id="cca94-108">通常では、上から下ではなく、下から上に一覧を表示することが必要になります。</span><span class="sxs-lookup"><span data-stu-id="cca94-108">You will typically need to present the list such that it appears to grow from the bottom up instead of from the top down.</span></span>  <span data-ttu-id="cca94-109">新しいメッセージを受信して末尾に追加するときは、以前のメッセージを上にスライドして空きを作り、ユーザーの注目が新着メッセージに集まるようにします。</span><span class="sxs-lookup"><span data-stu-id="cca94-109">When a new message arrives and is added to the end, the previous messages slide up to make room drawing the user’s attention to the latest arrival.</span></span>  <span data-ttu-id="cca94-110">ただし、ユーザーが上にスクロールして以前の返信を確認している場合は、ユーザーの集中を妨害することのないように、新しいメッセージの受信で表示位置を変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="cca94-110">However, if a user has scrolled up to view previous replies then the arrival of a new message must not cause a visual shift that would disrupt their focus.</span></span>

![反転リストを使ったチャット アプリ](images/listview-inverted.png)

## <a name="create-an-inverted-list"></a><span data-ttu-id="cca94-112">反転リストを作成する</span><span class="sxs-lookup"><span data-stu-id="cca94-112">Create an inverted list</span></span>

<span data-ttu-id="cca94-113">反転リストを作成するには、リスト ビューと共に、項目パネルとして [ItemsStackPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel) を使います。</span><span class="sxs-lookup"><span data-stu-id="cca94-113">To create an inverted list, use a list view with an [ItemsStackPanel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel) as its items panel.</span></span> <span data-ttu-id="cca94-114">ItemsStackPanel で、[ItemsUpdatingScrollMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel.itemsupdatingscrollmode) を [KeepLastItemInView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsupdatingscrollmode) に設定します。</span><span class="sxs-lookup"><span data-stu-id="cca94-114">On the ItemsStackPanel, set the [ItemsUpdatingScrollMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel.itemsupdatingscrollmode) to [KeepLastItemInView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsupdatingscrollmode).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cca94-115">**KeepLastItemInView** 列挙値は、Windows 10 バージョン 1607 以上で利用できます。</span><span class="sxs-lookup"><span data-stu-id="cca94-115">The **KeepLastItemInView** enum value is available starting with Windows 10, version 1607.</span></span> <span data-ttu-id="cca94-116">この値は、アプリを以前のバージョンの Windows 10 で実行するときには使用できません。</span><span class="sxs-lookup"><span data-stu-id="cca94-116">You can't use this value when your app runs on earlier versions of Windows 10.</span></span>

<span data-ttu-id="cca94-117">この例は、リスト ビューの項目を下部に配置する方法や、項目に変更があったときに最後の項目をビュー内に維持するように指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cca94-117">This example shows how to align the list view’s items to the bottom and indicate that when there is a change to the items the last item should remain in view.</span></span>
 
 <span data-ttu-id="cca94-118">**XAML**</span><span class="sxs-lookup"><span data-stu-id="cca94-118">**XAML**</span></span>
 ```xaml
<ListView>
    <ListView.ItemsPanel>
        <ItemsPanelTemplate>
            <ItemsStackPanel VerticalAlignment="Bottom"
                             ItemsUpdatingScrollMode="KeepLastItemInView"/>
        </ItemsPanelTemplate>
    </ListView.ItemsPanel>
</ListView>
```

## <a name="dos-and-donts"></a><span data-ttu-id="cca94-119">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="cca94-119">Do's and don'ts</span></span>

- <span data-ttu-id="cca94-120">送信者のメッセージと受信者のメッセージを両側に配置して、ユーザーが会話のフローを簡単に理解できるようにします。</span><span class="sxs-lookup"><span data-stu-id="cca94-120">Align messages from the sender/receiver on opposite sides to make the flow of conversation clear to users.</span></span>
- <span data-ttu-id="cca94-121">ユーザーが既に会話の末尾を読んでいて次のメッセージを待っている場合は、既存のメッセージを上に移動して最新のメッセージを表示するアニメーションを表示します。</span><span class="sxs-lookup"><span data-stu-id="cca94-121">Animate the existing messages out of the way to display the latest message if the user is already at the end of the conversation awaiting the next message.</span></span>
- <span data-ttu-id="cca94-122">ユーザーが会話の末尾を読んでいない場合は、項目を移動することによってユーザーの集中を妨害してはいけません。</span><span class="sxs-lookup"><span data-stu-id="cca94-122">Don’t disrupt the users focus by moving items if they’re not reading the end of the conversation.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="cca94-123">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="cca94-123">Get the sample code</span></span>

- [<span data-ttu-id="cca94-124">XAML の下から順に一覧の例</span><span class="sxs-lookup"><span data-stu-id="cca94-124">XAML Bottom-up list sample</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlBottomUpList)