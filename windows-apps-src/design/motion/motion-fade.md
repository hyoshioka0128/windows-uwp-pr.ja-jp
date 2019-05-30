---
Description: フェード アニメーションは、項目を画面に表示したり、項目を画面から非表示にするときに使います。 一般的なフェード アニメーションは、フェード インとフェード アウトの 2 つです。
title: UWP アプリでのフェード アニメーション
ms.assetid: 975E5EE3-EFBE-4159-8D10-3C94143DD07F
label: Motion--fades
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 3d8642e911a3ad4275e0a7a0f147ca9d70f415b0
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366796"
---
# <a name="fade-animations"></a><span data-ttu-id="6c3f0-105">フェード アニメーション</span><span class="sxs-lookup"><span data-stu-id="6c3f0-105">Fade animations</span></span>



<span data-ttu-id="6c3f0-106">フェード アニメーションは、項目を画面に表示したり、項目を画面から非表示にするときに使います。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-106">Use fade animations to bring items into a view or to take items out of a view.</span></span> <span data-ttu-id="6c3f0-107">一般的なフェード アニメーションは、フェード インとフェード アウトの 2 つです。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-107">The two common fade animations are fade-in and fade-out.</span></span>

> <span data-ttu-id="6c3f0-108">**重要な API**:[**FadeInThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.FadeInThemeAnimation)、 [ **FadeOutThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.FadeOutThemeAnimation)</span><span class="sxs-lookup"><span data-stu-id="6c3f0-108">**Important APIs**: [**FadeInThemeAnimation class**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.FadeInThemeAnimation), [**FadeOutThemeAnimation class**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.FadeOutThemeAnimation)</span></span>


## <a name="dos-and-donts"></a><span data-ttu-id="6c3f0-109">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="6c3f0-109">Do's and don'ts</span></span>


-   <span data-ttu-id="6c3f0-110">アプリで互いに関係のない要素や、テキストの多い要素を切り替えるときには、フェード アウトとフェード インを使います。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-110">When your app transitions between unrelated or text-heavy elements, use a fade-out followed by a fade-in.</span></span> <span data-ttu-id="6c3f0-111">そうすることで、差し替え前のオブジェクトが完全に消えてから差し替え後のオブジェクトを表示させることができます。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-111">This allows the outgoing object to completely disappear before the incoming object is visible.</span></span>
-   <span data-ttu-id="6c3f0-112">差し替える 2 つの要素のサイズが一定であり、ユーザーに同じ項目を見ているような印象を与えたいときには、差し替え後の要素を差し替え前の要素の上にフェード インさせます。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-112">Fade in the incoming element or elements on top of the outgoing elements if the size of the elements remains constant, and if you want the user to feel that they're looking at the same item.</span></span> <span data-ttu-id="6c3f0-113">フェード インが完了したら、差し替え前の項目は消すことができます。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-113">Once the fade-in is complete, the outgoing item can be removed.</span></span> <span data-ttu-id="6c3f0-114">これは、差し替え後の項目が差し替え前の項目を完全に覆い隠せる場合にのみ可能な方法です。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-114">This is only a viable option when the outgoing item will be completely covered by the incoming item.</span></span>
-   <span data-ttu-id="6c3f0-115">リストの項目を追加または削除する目的でフェード アニメーションを使うのは避けてください。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-115">Avoid fade animations to add or delete items in a list.</span></span> <span data-ttu-id="6c3f0-116">そのような場合には、専用に作成したリスト アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-116">Instead, use the list animations created for that purpose.</span></span>
-   <span data-ttu-id="6c3f0-117">フェード アニメーションは、ページの全コンテンツを変化させるときには使わないでください。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-117">Avoid fade animations to change the entire contents of a page.</span></span> <span data-ttu-id="6c3f0-118">そのような場合には、専用に作成したページ切り替えアニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-118">Instead, use the page transition animations created for that purpose.</span></span>
-   <span data-ttu-id="6c3f0-119">フェード アウトは要素を削除するための繊細な方法です。</span><span class="sxs-lookup"><span data-stu-id="6c3f0-119">Fade-out is a subtle way to remove an element.</span></span>
## <a name="related-articles"></a><span data-ttu-id="6c3f0-120">関連記事</span><span class="sxs-lookup"><span data-stu-id="6c3f0-120">Related articles</span></span>

* [<span data-ttu-id="6c3f0-121">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="6c3f0-121">Animations overview</span></span>](https://docs.microsoft.com/windows/uwp/graphics/animations-overview)
* <span data-ttu-id="6c3f0-122">[フェード アニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649429(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="6c3f0-122">[Animating fades](https://docs.microsoft.com/previous-versions/windows/apps/jj649429(v=win.10))</span></span>
* <span data-ttu-id="6c3f0-123">[クイック スタート:Library のアニメーションを使用して、UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="6c3f0-123">[Quickstart: Animating your UI using library animations](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span></span>
* [<span data-ttu-id="6c3f0-124">**FadeInThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="6c3f0-124">**FadeInThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.FadeInThemeAnimation)
* [<span data-ttu-id="6c3f0-125">**FadeOutThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="6c3f0-125">**FadeOutThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.FadeOutThemeAnimation)

 

 




