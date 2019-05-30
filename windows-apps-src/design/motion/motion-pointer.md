---
Description: ポインター アニメーションを使って、ユーザーが項目をタップまたはクリックしたときに視覚的なフィードバックをユーザーに提供します。
title: UWP アプリでのポインター クリックのアニメーション
ms.assetid: EEB10A2C-629A-4705-8468-4D019D74DDFF
ms.date: 08/09/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ee87a62796ed51d09d44cabecd0b49873145bd90
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366084"
---
# <a name="pointer-click-animations"></a><span data-ttu-id="2d81d-104">ポインター クリックのアニメーション</span><span class="sxs-lookup"><span data-stu-id="2d81d-104">Pointer click animations</span></span>



<span data-ttu-id="2d81d-105">ポインター アニメーションを使って、ユーザーが項目をタップまたはクリックしたときに視覚的なフィードバックをユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="2d81d-105">Use pointer animations to provide users with visual feedback when the user taps on an item.</span></span> <span data-ttu-id="2d81d-106">ポインター ダウン アニメーション (押された項目を若干縮小して傾ける) は、項目が最初にタップされたときに再生されます。</span><span class="sxs-lookup"><span data-stu-id="2d81d-106">The pointer down animation slightly shrinks and tilts the pressed item, and plays when an item is first tapped.</span></span> <span data-ttu-id="2d81d-107">ポインター アップ アニメーション (項目を元の位置に復元する) は、ユーザーがポインターから指を離したときに再生されます。</span><span class="sxs-lookup"><span data-stu-id="2d81d-107">The pointer up animation, which restores the item to its original position, is played when the user releases the pointer.</span></span>


> <span data-ttu-id="2d81d-108">**重要な API**:[**PointerUpThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PointerUpThemeAnimation)、 [ **PointerDownThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PointerDownThemeAnimation)</span><span class="sxs-lookup"><span data-stu-id="2d81d-108">**Important APIs**: [**PointerUpThemeAnimation class**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PointerUpThemeAnimation), [**PointerDownThemeAnimation class**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PointerDownThemeAnimation)</span></span>


## <a name="dos-and-donts"></a><span data-ttu-id="2d81d-109">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="2d81d-109">Do's and don'ts</span></span>

-   <span data-ttu-id="2d81d-110">ポインター アップ アニメーションを使うときには、ユーザーが指を離した直後にアニメーションを開始するようにします。</span><span class="sxs-lookup"><span data-stu-id="2d81d-110">When you use a pointer up animation, immediately trigger the animation when the user releases the pointer.</span></span> <span data-ttu-id="2d81d-111">これにより、タップによってトリガーされたアクション (新しいページへの移動など) の応答が遅れたとしても、ユーザーの操作が認識されたというフィードバックを即座に返すことができます。</span><span class="sxs-lookup"><span data-stu-id="2d81d-111">This provides instant feedback to the user that their action has been recognized, even if the action triggered by the tap (such as navigating to a new page) is slower to respond.</span></span>

## <a name="related-articles"></a><span data-ttu-id="2d81d-112">関連記事</span><span class="sxs-lookup"><span data-stu-id="2d81d-112">Related articles</span></span>

* [<span data-ttu-id="2d81d-113">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="2d81d-113">Animations overview</span></span>](https://docs.microsoft.com/windows/uwp/graphics/animations-overview)
* <span data-ttu-id="2d81d-114">[アニメーション ポインター数回のクリック](https://docs.microsoft.com/previous-versions/windows/apps/jj649432(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="2d81d-114">[Animating pointer clicks](https://docs.microsoft.com/previous-versions/windows/apps/jj649432(v=win.10))</span></span>
* <span data-ttu-id="2d81d-115">[クイック スタート:Library のアニメーションを使用して、UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="2d81d-115">[Quickstart: Animating your UI using library animations](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span></span>
* [<span data-ttu-id="2d81d-116">**PointerUpThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="2d81d-116">**PointerUpThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PointerUpThemeAnimation)
* [<span data-ttu-id="2d81d-117">**PointerDownThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="2d81d-117">**PointerDownThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PointerDownThemeAnimation)

 

 




