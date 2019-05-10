---
Description: モーションは方向性と重力を Fluent 方法について説明します。
title: 方向性と重力 - UWP アプリでのアニメーション
label: Directionality and gravity
template: detail.hbs
ms.date: 10/02/2018
ms.topic: article
keywords: windows 10, uwp
pm-contact: stmoy
design-contact: jeffarn
doc-status: Draft
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: ef005ffd018bf52d70067cdfedbb9c98b079bd89
ms.sourcegitcommit: cc0ef75f314658b14376eb60ef8e5bb4d7726e04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65444205"
---
# <a name="directionality-and-gravity"></a><span data-ttu-id="2f2b9-104">方向性と重力</span><span class="sxs-lookup"><span data-stu-id="2f2b9-104">Directionality and gravity</span></span>

<span data-ttu-id="2f2b9-105">方向指示は、ユーザーがエクスペリエンス全体を通じて行う取り組みの概念的モデルを強固にするために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-105">Directional signals help to solidify the mental model of the journey a user takes across experiences.</span></span> <span data-ttu-id="2f2b9-106">任意の動きの方向は、空間の連続性だけでなく、空間内のオブジェクトの整合性もサポートすることが重要です。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-106">It is important that the direction of any motion support both the continuity of the space as well as the integrity of the objects in the space.</span></span>

<span data-ttu-id="2f2b9-107">方向性は重力のような力を受けます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-107">Directional movement is subject to forces like gravity.</span></span> <span data-ttu-id="2f2b9-108">動きに力を加えるとモーションの自然な操作感が強化されます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-108">Applying forces to movement reinforces the natural feel of the motion.</span></span>

## <a name="examples"></a><span data-ttu-id="2f2b9-109">例</span><span class="sxs-lookup"><span data-stu-id="2f2b9-109">Examples</span></span>

<table>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon.png" alt="XAML controls gallery" width="168"></img></td>
<td>
    <p><span data-ttu-id="2f2b9-110">ある場合、 <strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong>アプリをインストールするには、ここをクリックして<a href="xamlcontrolsgallery:/category/Motion">アプリを開き、アクションでモーションを参照してください</a>します。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-110">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/category/Motion">open the app and see Motion in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="2f2b9-111"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="2f2b9-111"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="2f2b9-112"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="2f2b9-112"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="direction-of-movement"></a><span data-ttu-id="2f2b9-113">動きの方向</span><span class="sxs-lookup"><span data-stu-id="2f2b9-113">Direction of movement</span></span>

:::row:::
    :::column:::
        Direction of movement corresponds to physical motion. Just like in nature, objects can move in any world axis - X,Y,Z. This is how we think of the movement of objects on the screen.

        When you move objects, avoid unnatural collisions. Keep in mind where objects come from and go to, and alway support higher level constructs that may be used in the scene, such as scroll direction or layout hierarchy.
    :::column-end:::
    :::column:::
        ![direction backward in](images/Direction.gif)
    :::column-end:::
:::row-end:::

## <a name="direction-of-navigation"></a><span data-ttu-id="2f2b9-114">ナビゲーションの方向</span><span class="sxs-lookup"><span data-stu-id="2f2b9-114">Direction of navigation</span></span>

<span data-ttu-id="2f2b9-115">アプリ内のシーン間のナビゲーションの方向は、概念的なものです。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-115">The direction of navigation between scenes in your app is conceptual.</span></span> <span data-ttu-id="2f2b9-116">ユーザーは前後に移動します。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-116">Users navigate forward and back.</span></span> <span data-ttu-id="2f2b9-117">シーンはビューの内外に移動します。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-117">Scenes move in and out of view.</span></span> <span data-ttu-id="2f2b9-118">これらの概念は物理的な動きと連携してユーザーを誘導します。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-118">These concepts combine with physical movement to guide the user.</span></span>

<span data-ttu-id="2f2b9-119">ナビゲーションによりオブジェクトが前のシーンから新しいシーンに移動する場合、オブジェクトは画面上で A から B の単純な移動を行います。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-119">When navigation causes an object to travel from the previous scene to the new scene, the object makes a simple A-to-B move on the screen.</span></span> <span data-ttu-id="2f2b9-120">動きがより物理的に感じられるようにするために、標準的なイージングに加えて、重力の感覚が追加されます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-120">To ensure that the movement feels more physical, the standard easing is added, as well as the feeling of gravity.</span></span>

<span data-ttu-id="2f2b9-121">"戻る" ナビゲーションでは、動きが逆になります (B から A)。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-121">For back navigation, the move is reversed (B-to-A).</span></span> <span data-ttu-id="2f2b9-122">ユーザーは戻る移動をしたときに、できるだけ早く以前の状態に戻ることを期待します。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-122">When the user navigates back, they have an expectation to be returned to the previous state as soon as possible.</span></span> <span data-ttu-id="2f2b9-123">タイミングはより迅速で直接的であり、減速のイージングを使用します。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-123">The timing is quicker, more direct, and uses the decelerate easing.</span></span>

<span data-ttu-id="2f2b9-124">ここでは、前後のナビゲーション中に選択された項目が画面上に表示されたままになるため、これらの原則が適用されます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-124">Here, these priciples are applied as the selected item stays on screen during forward and back navigation.</span></span>

![継続的なモーションの UI の例](images/continuous3.gif)

<span data-ttu-id="2f2b9-126">ナビゲーションにより画面上の項目が置き換えられると、既存のシーンの移動先と、新しいシーンの移動元を示すことが重要です。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-126">When navigation causes items on the screen to be replaced, its important to show where the exiting scene went to, and where the new scene is coming from.</span></span>

<span data-ttu-id="2f2b9-127">これには次のようないくつかの利点があります。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-127">This has several benefits:</span></span>

- <span data-ttu-id="2f2b9-128">空間に対するユーザーの概念的モデルが確立されます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-128">It solidifies the user's mental model of the space.</span></span>
- <span data-ttu-id="2f2b9-129">既存のシーンの継続時間により、後続のシーンに対してコンテンツをアニメーション化する準備をするためのより長い時間が提供されます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-129">The duration of the exiting scene provides more time to prepare content to be animated in for the incoming scene.</span></span>
- <span data-ttu-id="2f2b9-130">これにより、アプリの体感的なパフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-130">It improves the perceived performance of the app.</span></span>

<span data-ttu-id="2f2b9-131">ナビゲーションに関して考慮すべき目立たない 4 つの方向があります。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-131">There are 4 discreet directions of navigation to consider.</span></span>

:::row:::
    :::column:::
        **Forward-In**

        Celebrate content entering the scene in a manner that does not collide with outgoing content. Content decelerates into the scene.
    :::column-end:::
    :::column:::
        ![direction forward in](images/forwardIN.gif)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        **Forward-Out**

        Content exits quickly. Objects accelerate off screen.
    :::column-end:::
    :::column:::
        ![direction forward out](images/forwardOUT.gif)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        **Backward-In**

        Same as Forward-In, but reversed.
    :::column-end:::
    :::column:::
        ![direction backward in](images/backwardIN.gif)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        **Backward-Out**

        Same as Forward-Out, but reversed.
    :::column-end:::
    :::column:::
        ![direction backward out](images/backwardOUT.gif)
    :::column-end:::
:::row-end:::

## <a name="gravity"></a><span data-ttu-id="2f2b9-132">重力</span><span class="sxs-lookup"><span data-stu-id="2f2b9-132">Gravity</span></span>

<span data-ttu-id="2f2b9-133">重力によりエクスペリエンスがより自然に感じられるようになります。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-133">Gravity makes your experiences feel more natural.</span></span> <span data-ttu-id="2f2b9-134">z 軸上を移動し、画面上のアフォー ダンスでシーンに固定されていないオブジェクトは、重力の影響を受ける可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-134">Objects that move on the Z-axis and are not anchored to the scene by an onscreen affordance have the potential to be affected by gravity.</span></span> <span data-ttu-id="2f2b9-135">オブジェクトがシーンから開放され、脱出速度に到達する前に、重力がオブジェクトを引き下げ、オブジェクトの移動に伴い軌跡のより自然なカーブが生み出されます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-135">As an object breaks free of the scene and before it reaches escape velocity, gravity pulls down on the object, creating a more natural curve of the object trajectory as it moves.</span></span>

<span data-ttu-id="2f2b9-136">通常、オブジェクトがあるシーンから別のシーンに移動する必要があるときに、重力が生じます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-136">Gravity typically manifests when an object must jump from one scene to another.</span></span> <span data-ttu-id="2f2b9-137">このため、接続型アニメーションには重力の概念が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-137">Because of this, connected animation uses the concept of gravity.</span></span>

<span data-ttu-id="2f2b9-138">ここでは、グリッドの先頭行にある要素が重力の影響を受け、要素がその場所を離れて前方に移動するときに若干下がります。</span><span class="sxs-lookup"><span data-stu-id="2f2b9-138">Here, an element in the top row of the grid is affected by gravity, causing it to drop slightly as it leaves its place and moves to the front.</span></span>

![逆方向へのイン](images/continuity-photos.gif)

## <a name="related-articles"></a><span data-ttu-id="2f2b9-140">関連記事</span><span class="sxs-lookup"><span data-stu-id="2f2b9-140">Related articles</span></span>

- [<span data-ttu-id="2f2b9-141">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="2f2b9-141">Motion overview</span></span>](index.md)
- [<span data-ttu-id="2f2b9-142">タイミングと、簡略化</span><span class="sxs-lookup"><span data-stu-id="2f2b9-142">Timing and easing</span></span>](timing-and-easing.md)
