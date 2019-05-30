---
Description: エッジに基づく UI アニメーションでは、画面の端を起点とする UI の表示と非表示を切り替えられます。
title: UWP アプリでのエッジに基づく UI アニメーション
ms.assetid: 5A8F73B1-F4F6-424b-9EDF-A9766C5DEAE8
label: Motion--edge-based UI
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: fd7071092a66f46a81095a5cb6aff8b623a774a5
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366624"
---
# <a name="edge-based-ui-animations"></a><span data-ttu-id="69751-104">エッジに基づく UI アニメーション</span><span class="sxs-lookup"><span data-stu-id="69751-104">Edge-based UI animations</span></span>





<span data-ttu-id="69751-105">エッジに基づく UI アニメーションでは、画面の端を起点とする UI の表示と非表示を切り替えられます。</span><span class="sxs-lookup"><span data-stu-id="69751-105">Edge-based animations show or hide UI that originates from the edge of the screen.</span></span> <span data-ttu-id="69751-106">この表示と非表示のアクションは、ユーザーが開始することも、アプリから開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="69751-106">The show and hide actions can be initiated either by the user or by the app.</span></span> <span data-ttu-id="69751-107">UI は、アプリの手前に表示するか、メイン アプリ サーフェスの一部として表示することができます。</span><span class="sxs-lookup"><span data-stu-id="69751-107">The UI can either overlay the app or be part of the main app surface.</span></span> <span data-ttu-id="69751-108">UI をアプリ サーフェスの一部として表示する場合は、UI を表示できるようにアプリの残りの部分のサイズを調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="69751-108">If the UI is part of the app surface, the rest of the app might need to be resized to accommodate it.</span></span>

> <span data-ttu-id="69751-109">**重要な API**:[**EdgeUIThemeTransition クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.EdgeUIThemeTransition)</span><span class="sxs-lookup"><span data-stu-id="69751-109">**Important APIs**: [**EdgeUIThemeTransition class**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.EdgeUIThemeTransition)</span></span>


## <a name="dos-and-donts"></a><span data-ttu-id="69751-110">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="69751-110">Do's and don'ts</span></span>


-   <span data-ttu-id="69751-111">画面領域をあまり占有しないカスタム メッセージ バーやエラー バーを表示または非表示にするには、エッジ (端) UI アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="69751-111">Use edge UI animations to show or hide a custom message or error bar that does not extend far into the screen.</span></span>
-   <span data-ttu-id="69751-112">作業ウィンドウやカスタム ソフト キーボードなど、画面内側にスライドして領域を大きく確保する UI を表示するには、パネル アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="69751-112">Use panel animations to show UI that slides a significant distance into the screen, such as a task pane or a custom soft keyboard.</span></span>
-   <span data-ttu-id="69751-113">UI を開くには、それが関連付けられている端から画面内側にスライドします。</span><span class="sxs-lookup"><span data-stu-id="69751-113">Slide the UI in from the same edge it will be attached to.</span></span>
-   <span data-ttu-id="69751-114">UI を閉じるには、画面内側から、開いたときと同じ端に向かってスライドします。</span><span class="sxs-lookup"><span data-stu-id="69751-114">Slide the UI out to the same edge it came from.</span></span>
-   <span data-ttu-id="69751-115">UI のスライド操作に応じてアプリのコンテンツ サイズを変更する必要がある場合は、フェード アニメーションを使ってサイズを変更します。</span><span class="sxs-lookup"><span data-stu-id="69751-115">If the contents of the app need to resize in response to the UI sliding in or out, use fade animations for the resize.</span></span>
    -   <span data-ttu-id="69751-116">UI を画面内側に向かってスライドする場合は、エッジ (端) UI アニメーションまたはパネル アニメーションの後にフェード アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="69751-116">If the UI is sliding in, use a fade animation after the edge UI or panel animation.</span></span>
    -   <span data-ttu-id="69751-117">UI を画面外側に向かってスライドする場合は、エッジ (端) UI アニメーションまたはパネル アニメーションと同時にフェード アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="69751-117">If the UI is sliding out, use a fade animation at the same time as the edge UI or panel animation.</span></span>
-   <span data-ttu-id="69751-118">通知には、このアニメーションを適用しないでください。</span><span class="sxs-lookup"><span data-stu-id="69751-118">Don't apply these animations to notifications.</span></span> <span data-ttu-id="69751-119">エッジに基づく UI に通知を格納することはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="69751-119">Notifications should not be housed within edge-based UI.</span></span>
-   <span data-ttu-id="69751-120">画面のエッジ (端) にない UI コンテナーやコントロールには、エッジ (端) UI アニメーションとパネル アニメーションを適用しないでください。</span><span class="sxs-lookup"><span data-stu-id="69751-120">Don't apply the edge UI or panel animations to any UI container or control that is not at the edge of the screen.</span></span> <span data-ttu-id="69751-121">このアニメーションは、画面のエッジ (端) にある UI の開閉とサイズ変更にのみ使います。</span><span class="sxs-lookup"><span data-stu-id="69751-121">These animations are used only for showing, resizing, and dismissing UI at the edges of the screen.</span></span> <span data-ttu-id="69751-122">他のタイプの UI を移動するには、位置変更アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="69751-122">To move other types of UI, use reposition animations.</span></span>

    ![エッジ (端) UI アニメーションまたはパネル アニメーションを使うケースと位置変更を使うケースの図](images/edgevsreposition.png)

## <a name="related-articles"></a><span data-ttu-id="69751-124">関連記事</span><span class="sxs-lookup"><span data-stu-id="69751-124">Related articles</span></span>


<span data-ttu-id="69751-125">**開発者向け**</span><span class="sxs-lookup"><span data-stu-id="69751-125">**For developers**</span></span>
* [<span data-ttu-id="69751-126">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="69751-126">Animations overview</span></span>](https://docs.microsoft.com/windows/uwp/graphics/animations-overview)
* <span data-ttu-id="69751-127">[Edge ベースの UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649428(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="69751-127">[Animating edge-based UI](https://docs.microsoft.com/previous-versions/windows/apps/jj649428(v=win.10))</span></span>
* <span data-ttu-id="69751-128">[クイック スタート:Library のアニメーションを使用して、UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="69751-128">[Quickstart: Animating your UI using library animations](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span></span>
* [<span data-ttu-id="69751-129">**EdgeUIThemeTransition クラス**</span><span class="sxs-lookup"><span data-stu-id="69751-129">**EdgeUIThemeTransition class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.EdgeUIThemeTransition)
* [<span data-ttu-id="69751-130">**PaneThemeTransition クラス**</span><span class="sxs-lookup"><span data-stu-id="69751-130">**PaneThemeTransition class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PaneThemeTransition)
* <span data-ttu-id="69751-131">[フェード アニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649429(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="69751-131">[Animating fades](https://docs.microsoft.com/previous-versions/windows/apps/jj649429(v=win.10))</span></span>
* <span data-ttu-id="69751-132">[位置を変更をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649434(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="69751-132">[Animating repositions](https://docs.microsoft.com/previous-versions/windows/apps/jj649434(v=win.10))</span></span>

 

 




