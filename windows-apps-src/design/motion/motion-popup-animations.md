---
Description: ポップアップ アニメーションを使って、ポップアップ UI やカスタム ポップアップ UI 要素の表示と非表示を切り替えます。 ポップアップ要素とは、アプリのコンテンツの上に表示されるコンテナーのことで、ユーザーがポップアップ要素の外部をタップまたはクリックすると消えます。
title: UWP アプリでのポップアップ UI のアニメーション
ms.assetid: 4E9025CE-FC90-4d4c-9DE6-EC6B6F2AD9DF
label: Motion--Pop-up animations
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ee3d6a7fc29ec2adfeb149a3bc84f27c482c3be7
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366700"
---
# <a name="pop-up-ui-animations"></a><span data-ttu-id="4f19c-105">ポップアップ UI のアニメーション</span><span class="sxs-lookup"><span data-stu-id="4f19c-105">Pop-up UI animations</span></span>



<span data-ttu-id="4f19c-106">ポップアップ アニメーションを使って、ポップアップ UI やカスタム ポップアップ UI 要素の表示と非表示を切り替えます。</span><span class="sxs-lookup"><span data-stu-id="4f19c-106">Use pop-up animations to show and hide pop-up UI for flyouts or custom pop-up UI elements.</span></span> <span data-ttu-id="4f19c-107">ポップアップ要素とは、アプリのコンテンツの上に表示されるコンテナーのことで、ユーザーがポップアップ要素の外部をタップまたはクリックすると消えます。</span><span class="sxs-lookup"><span data-stu-id="4f19c-107">Pop-up elements are containers that appear over the app's content and are dismissed if the user taps or clicks outside of the pop-up element.</span></span>

> <span data-ttu-id="4f19c-108">**重要な API**:[**PopInThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PopInThemeAnimation)、 [ **PopupThemeTransition クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PopupThemeTransition)</span><span class="sxs-lookup"><span data-stu-id="4f19c-108">**Important APIs**: [**PopInThemeAnimation class**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PopInThemeAnimation), [**PopupThemeTransition class**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PopupThemeTransition)</span></span>


## <a name="dos-and-donts"></a><span data-ttu-id="4f19c-109">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="4f19c-109">Do's and don'ts</span></span>


-   <span data-ttu-id="4f19c-110">ポップアップ アニメーションは、アプリ ページ自体には含まれないカスタム ポップアップ UI 要素を表示したり非表示にしたりするために使います。</span><span class="sxs-lookup"><span data-stu-id="4f19c-110">Use pop-up animations to show or hide custom pop-up UI elements that aren't a part of the app page itself.</span></span> <span data-ttu-id="4f19c-111">Windows で用意されているコモン コントロールには、既にこのアニメーションが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="4f19c-111">The common controls provided by Windows already have these animations built in.</span></span>
-   <span data-ttu-id="4f19c-112">ヒントやダイアログにポップアップ アニメーションを使わないでください。</span><span class="sxs-lookup"><span data-stu-id="4f19c-112">Don't use pop-up animations for tooltips or dialogs.</span></span>
-   <span data-ttu-id="4f19c-113">アプリのメイン コンテンツ内の UI の表示と非表示を切り替えるためにポップアップ アニメーションを使わないでください。ポップアップ アニメーションは、メイン アプリ コンテンツの上に表示されるポップアップ コンテナーの表示と非表示を切り替えるときにのみ使います。</span><span class="sxs-lookup"><span data-stu-id="4f19c-113">Don't use pop-up animations to show or hide UI within the main content of your app; only use pop-up animations to show or hide a pop-up container that displays on top of the main app content.</span></span>

## <a name="related-articles"></a><span data-ttu-id="4f19c-114">関連記事</span><span class="sxs-lookup"><span data-stu-id="4f19c-114">Related articles</span></span>

* [<span data-ttu-id="4f19c-115">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="4f19c-115">Animations overview</span></span>](https://docs.microsoft.com/windows/uwp/graphics/animations-overview)
* <span data-ttu-id="4f19c-116">[ポップアップの UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649433(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="4f19c-116">[Animating pop-up UI](https://docs.microsoft.com/previous-versions/windows/apps/jj649433(v=win.10))</span></span>
* <span data-ttu-id="4f19c-117">[クイック スタート:Library のアニメーションを使用して、UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="4f19c-117">[Quickstart: Animating your UI using library animations](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span></span>
* [<span data-ttu-id="4f19c-118">**PopInThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="4f19c-118">**PopInThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PopInThemeAnimation)
* [<span data-ttu-id="4f19c-119">**PopOutThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="4f19c-119">**PopOutThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PopOutThemeAnimation)
* [<span data-ttu-id="4f19c-120">**PopupThemeTransition クラス**</span><span class="sxs-lookup"><span data-stu-id="4f19c-120">**PopupThemeTransition class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PopupThemeTransition)

 

 




