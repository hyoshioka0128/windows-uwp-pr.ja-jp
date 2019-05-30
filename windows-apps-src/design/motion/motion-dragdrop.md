---
Description: ドラッグ アンド ドロップ アニメーションは、リスト内で項目を移動するときや、特定の項目を別の項目上にドロップするときなど、オブジェクトを移動する際に使います。
title: UWP アプリでのドラッグ アニメーション
ms.assetid: 6064755F-6E24-4901-A4FF-263F05F0DFD6
label: Motion--Drag and drop
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 07707160846f3d63c7d0c097fb7b84def08be9e7
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366690"
---
# <a name="drag-animations"></a><span data-ttu-id="6bb1b-104">ドラッグ アニメーション</span><span class="sxs-lookup"><span data-stu-id="6bb1b-104">Drag animations</span></span>




<span data-ttu-id="6bb1b-105">ドラッグ アンド ドロップ アニメーションは、リスト内で項目を移動するときや、特定の項目を別の項目上にドロップするときなど、オブジェクトを移動する際に使います。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-105">Use drag-and-drop animations when users move objects, such as moving an item within a list, or dropping an item on top of another.</span></span>

> <span data-ttu-id="6bb1b-106">**重要な API**:[**DragItemThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.dragitemthemeanimation.)</span><span class="sxs-lookup"><span data-stu-id="6bb1b-106">**Important APIs**: [**DragItemThemeAnimation class**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.dragitemthemeanimation.)</span></span>


## <a name="dos-and-donts"></a><span data-ttu-id="6bb1b-107">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="6bb1b-107">Do's and don'ts</span></span>


<span data-ttu-id="6bb1b-108">**ドラッグ開始のアニメーション**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-108">**Drag start animation**</span></span>

-   <span data-ttu-id="6bb1b-109">ドラッグの開始アニメーションは、ユーザーがオブジェクトを動かし始めるときに使います。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-109">Use the drag start animation when the user begins to move an object.</span></span>
-   <span data-ttu-id="6bb1b-110">ドラッグ アンド ドロップ操作の影響を受けるオブジェクトが他に存在する場合に限り、それらのオブジェクトをアニメーションに含めるようにします。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-110">Include affected objects in the animation if and only if there are other objects that can be affected by the drag-and-drop operation.</span></span>
-   <span data-ttu-id="6bb1b-111">ドラッグの開始アニメーションによって始まったアニメーションのシーケンスの終了には、ドラッグの終了アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-111">Use the drag end animation to complete any animation sequence that began with the drag start animation.</span></span> <span data-ttu-id="6bb1b-112">ドラッグの終了アニメーションにより、ドラッグの開始アニメーションで変化したドラッグされたオブジェクトのサイズが元に戻ります。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-112">This reverses the size change in the dragged object that was caused by the drag start animation.</span></span>

<span data-ttu-id="6bb1b-113">**ドラッグ終了のアニメーション**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-113">**Drag end animation**</span></span>

-   <span data-ttu-id="6bb1b-114">ドラッグの終了アニメーションは、ドラッグされたオブジェクトをドロップするときに使います。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-114">Use the drag end animation when the user drops a dragged object.</span></span>
-   <span data-ttu-id="6bb1b-115">ドラッグの終了アニメーションは、リストの追加および削除アニメーションと組み合わせて使います。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-115">Use the drag end animation in combination with add and delete animations for lists.</span></span>
-   <span data-ttu-id="6bb1b-116">ドラッグの開始アニメーションに影響を受けるオブジェクトが存在する場合に限り、それらのオブジェクトをドラッグの終了アニメーションに含めるようにします。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-116">Include affected objects in the drag end animation if and only if you included those same affected objects in the drag start animation.</span></span>
-   <span data-ttu-id="6bb1b-117">ドラッグの終了アニメーションは、ドラッグの開始アニメーションよりも先に使わないでください。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-117">Don't use the drag end animation if you have not first used the drag start animation.</span></span> <span data-ttu-id="6bb1b-118">ドラッグ シーケンスの完了後にオブジェクトを元のサイズに戻すためには、両方のアニメーションを使う必要があります。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-118">You need to use both animations to return objects to their original sizes after the drag sequence is complete.</span></span>

<span data-ttu-id="6bb1b-119">**ドラッグ間アニメーションを入力してください。**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-119">**Drag between enter animation**</span></span>

-   <span data-ttu-id="6bb1b-120">項目間でのドラッグの開始アニメーションは、2 つのオブジェクトの間のドロップ可能な場所にドラッグ ソースをドラッグするときに使います。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-120">Use the drag between enter animation when the user drags the drag source into a drop area where it can be dropped between two other objects.</span></span>
-   <span data-ttu-id="6bb1b-121">適度な大きさのドロップ ターゲット領域を選んでください。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-121">Choose a reasonable drop target area.</span></span> <span data-ttu-id="6bb1b-122">この領域が小さすぎると、ドラッグ ソースをドロップする際に重ね合わせるのが難しくなるため、好ましくありません。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-122">This area should not be so small that it is difficult for the user to position the drag source for the drop.</span></span>
-   <span data-ttu-id="6bb1b-123">ドロップ可能な場所を示すために影響を受けるオブジェクトが移動するときには、互いにまっすぐに引き離すことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-123">The recommended direction to move affected objects to show the drop area is directly apart from each other.</span></span> <span data-ttu-id="6bb1b-124">移動方向が上下になるか、左右になるかは、影響を受けるオブジェクトが並ぶ向きによって異なります。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-124">Whether they move vertically or horizontally depends on the orientation of the affected objects to each other.</span></span>
-   <span data-ttu-id="6bb1b-125">ドラッグ ソースを領域内にドロップできない場合、項目間でのドラッグの開始アニメーションは使わないでください。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-125">Don't use the drag between enter animation if the drag source cannot be dropped in an area.</span></span> <span data-ttu-id="6bb1b-126">項目間へのドラッグの開始アニメーションは、影響を受けるオブジェクトの間にドラッグ ソースをドラッグできることをユーザーに知らせるためのものです。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-126">The drag between enter animation tells the user that the drag source can be dropped between the affected objects.</span></span>

<span data-ttu-id="6bb1b-127">**Leave アニメーション間でドラッグします**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-127">**Drag between leave animation**</span></span>

-   <span data-ttu-id="6bb1b-128">項目間でのドラッグの中止アニメーションは、ユーザーがオブジェクトをドラッグして 2 つのオブジェクトの間のドロップ可能な領域から出すときに使います。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-128">Use the drag between leave animation when the user drags an object away from an area where it could have been dropped between two other objects.</span></span>
-   <span data-ttu-id="6bb1b-129">項目間でのドラッグの開始アニメーションよりも先に、項目間でのドラッグの中止アニメーションを使わないでください。</span><span class="sxs-lookup"><span data-stu-id="6bb1b-129">Don't use the drag between leave animation if you have not first used the drag between enter animation.</span></span>


## <a name="related-articles"></a><span data-ttu-id="6bb1b-130">関連記事</span><span class="sxs-lookup"><span data-stu-id="6bb1b-130">Related articles</span></span>

<span data-ttu-id="6bb1b-131">**開発者向け**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-131">**For developers**</span></span>
* [<span data-ttu-id="6bb1b-132">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="6bb1b-132">Animations overview</span></span>](https://docs.microsoft.com/windows/uwp/graphics/animations-overview)
* <span data-ttu-id="6bb1b-133">[ドラッグ アンド ドロップのシーケンスをアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649427(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="6bb1b-133">[Animating drag-and-drop sequences](https://docs.microsoft.com/previous-versions/windows/apps/jj649427(v=win.10))</span></span>
* <span data-ttu-id="6bb1b-134">[クイック スタート:Library のアニメーションを使用して、UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="6bb1b-134">[Quickstart: Animating your UI using library animations](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span></span>
* [<span data-ttu-id="6bb1b-135">**DragItemThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-135">**DragItemThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.dragitemthemeanimation.)
* [<span data-ttu-id="6bb1b-136">**DropTargetItemThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-136">**DropTargetItemThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.droptargetitemthemeanimation.)
* [<span data-ttu-id="6bb1b-137">**DragOverThemeAnimation クラス**</span><span class="sxs-lookup"><span data-stu-id="6bb1b-137">**DragOverThemeAnimation class**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.dragoverthemeanimation.)


 




