---
Description: 目的がはっきりとしており、適切にデザインされたモーションは、アプリに強い印象を与え、精巧で完成度の高い操作性を感じさせます。 コンテキストの変化がわかりやすく、視覚的な切り替えがエクスペリエンスに結び付きます。
title: UWP アプリでのモーションとアニメーション
ms.assetid: 21AA1335-765E-433A-85D8-560B340AE966
label: Motion
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: stmoy
design-contact: jeffarn
doc-status: Published
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 1096bdab340c3f0fef24b5815423f72b0f5c8219
ms.sourcegitcommit: cc0ef75f314658b14376eb60ef8e5bb4d7726e04
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65444169"
---
# <a name="motion-for-uwp-apps"></a><span data-ttu-id="07dbf-105">UWP アプリのモーション</span><span class="sxs-lookup"><span data-stu-id="07dbf-105">Motion for UWP apps</span></span>

![モーション アイコン](../images/motion-2x.png)

<span data-ttu-id="07dbf-107">Fluent モーションはアプリで目的を果たします。</span><span class="sxs-lookup"><span data-stu-id="07dbf-107">Fluent motion serves a purpose in your app.</span></span> <span data-ttu-id="07dbf-108">これは、ユーザーの動作に基づいてインテリジェントなフィードバックを提供し、UI にアクティブな印象を与え、アプリ内でユーザーのナビゲーションを誘導します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-108">It gives intelligent feedback based on the user's behavior, keeps the UI feeling alive, and guides the user's navigation through your app.</span></span> <span data-ttu-id="07dbf-109">Fluent モーションは、ユーザーとそのデジタル エクスペリエンス間の感情面の結び付きを生み出します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-109">Fluent motion elicits an emotional connection between a user and their digital experience.</span></span> <span data-ttu-id="07dbf-110">マイクロソフトでは、ユーザーが既に現実世界から認識している自然な動きの基盤のうえに構築し、そこからシステムを拡張します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-110">We build on a foundation of natural movement the user already understands from the physical world, and we extend our system from there.</span></span>

## <a name="examples"></a><span data-ttu-id="07dbf-111">例</span><span class="sxs-lookup"><span data-stu-id="07dbf-111">Examples</span></span>

<table>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon.png" alt="XAML controls gallery" width="168"></img></td>
<td>
    <p><span data-ttu-id="07dbf-112"><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/category/Motion">アプリを開き、モーションの動作を確認</a>してください。</span><span class="sxs-lookup"><span data-stu-id="07dbf-112">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/category/Motion">open the app and see Motion in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="07dbf-113"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="07dbf-113"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="07dbf-114"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="07dbf-114"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="fluent-motion-principles"></a><span data-ttu-id="07dbf-115">Fluent モーションの原則</span><span class="sxs-lookup"><span data-stu-id="07dbf-115">Fluent motion principles</span></span>

### <a name="physical"></a><span data-ttu-id="07dbf-116">運動能力</span><span class="sxs-lookup"><span data-stu-id="07dbf-116">Physical</span></span>

<span data-ttu-id="07dbf-117">動作中のオブジェクトは、現実世界でのオブジェクトの動作を示します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-117">Objects in motion exhibit behaviors of objects in the real world.</span></span> <span data-ttu-id="07dbf-118">滑らかで応答性の高い動きによって、自然な操作性を感じさせるエクスペリエンスが実現され、感情面の結び付きが生みだされ、個性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="07dbf-118">Fluid, responsive movement makes the experience feel natural, creating emotional connections and adding personality.</span></span>

![物理モーションの UI の例](images/Physical.gif)
> <span data-ttu-id="07dbf-120">タッチで UI を操作すると、UI の動きが、操作の速度に直接関連します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-120">When you interact with UI via touch, the movement of the UI is directly related to the velocity of the interaction.</span></span> <span data-ttu-id="07dbf-121">また、タッチは直接操作であるため、操作するオブジェクトが周囲のオブジェクトに影響します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-121">And because touch is direct manipulation, the object you interact with affects the objects around it.</span></span>

### <a name="functional"></a><span data-ttu-id="07dbf-122">機能性</span><span class="sxs-lookup"><span data-stu-id="07dbf-122">Functional</span></span>

<span data-ttu-id="07dbf-123">モーションは目的を果たし、確信があります。</span><span class="sxs-lookup"><span data-stu-id="07dbf-123">Motion serves a purpose and has conviction.</span></span> <span data-ttu-id="07dbf-124">複雑さに関してユーザーをサポートし、階層を確立する手助けをします。</span><span class="sxs-lookup"><span data-stu-id="07dbf-124">It guides the user through complexity and helps establish hierarchy.</span></span> <span data-ttu-id="07dbf-125">モーションは、パフォーマンスが向上した印象を与え、体感する待ち時間を隠蔽することでユーザー エクスペリエンスを最適化します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-125">Movement gives the impression of enhanced performance and optimizes the user experience by hiding perceived latency.</span></span>

![機能的なモーションの UI の例](images/functional.gif)
> <span data-ttu-id="07dbf-127">ページ切り替えは、目的に特化されています。</span><span class="sxs-lookup"><span data-stu-id="07dbf-127">Page transitions are purpose-built.</span></span> <span data-ttu-id="07dbf-128">ページが相互に関連する方法に関するヒントを提供します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-128">They give hints about how pages are related to each other.</span></span> <span data-ttu-id="07dbf-129">パフォーマンスが最適でない場合でも速く感じられるような方法で移動します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-129">They move in a manner that's perceived as fast even when performance is not optimal.</span></span>

### <a name="continuous"></a><span data-ttu-id="07dbf-130">継続性</span><span class="sxs-lookup"><span data-stu-id="07dbf-130">Continuous</span></span>

<span data-ttu-id="07dbf-131">ポイントからポイントへの滑らか動きは、自然に目を引きつけ、ユーザーを誘導します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-131">Fluid movement from point to point naturally draws the eye and guides the user.</span></span> <span data-ttu-id="07dbf-132">適切にユーザーのタスクをまとめて、よりコンシューマブルで親しみやすく感じられるようにします。</span><span class="sxs-lookup"><span data-stu-id="07dbf-132">It elegantly stitches together a user’s task, making it feel more consumable and friendly.</span></span>

![継続的なモーションの UI の例](images/continuous3.gif)
> <span data-ttu-id="07dbf-134">オブジェクトは、シーン間を移動したり、シーン内でモーフィングして継続性を提供し、ユーザーがコンテキストを維持できるようにします。</span><span class="sxs-lookup"><span data-stu-id="07dbf-134">Objects can travel from scene to scene or morph within a scene to provide continuity and help the user maintain context.</span></span>

### <a name="contextual"></a><span data-ttu-id="07dbf-135">状況依存</span><span class="sxs-lookup"><span data-stu-id="07dbf-135">Contextual</span></span>

<span data-ttu-id="07dbf-136">インテリジェントなモーションは、UI を操作する方法に沿った方法でユーザーにフィードバックを提供します。</span><span class="sxs-lookup"><span data-stu-id="07dbf-136">Intelligent motion provides feedback to the user in a manner that's aligned with how they manipulated the UI.</span></span> <span data-ttu-id="07dbf-137">操作はユーザーを中心にしています。</span><span class="sxs-lookup"><span data-stu-id="07dbf-137">Interaction is centered around the user.</span></span> <span data-ttu-id="07dbf-138">動きはフォーム ファクターに適切であると感じられ、シナリオに基づいて設計されています。</span><span class="sxs-lookup"><span data-stu-id="07dbf-138">The movement feels appropriate to the form-factor and designed around the scenario.</span></span> <span data-ttu-id="07dbf-139">各ユーザーにとって快適である必要があります。</span><span class="sxs-lookup"><span data-stu-id="07dbf-139">It should be comfortable for each user.</span></span>

![状況依存のモーションの UI の例](images/Contextual.gif)
> <span data-ttu-id="07dbf-141">アニメーションはユーザーの操作に沿ったものである必要があります。</span><span class="sxs-lookup"><span data-stu-id="07dbf-141">Animation should tie back to the user interaction.</span></span> <span data-ttu-id="07dbf-142">コンテキスト メニューは、ユーザーがアクティブ化したポイントから展開されます。</span><span class="sxs-lookup"><span data-stu-id="07dbf-142">A context menu is deployed from a point where the user activated it.</span></span>

## <a name="motion-articles"></a><span data-ttu-id="07dbf-143">モーションの記事</span><span class="sxs-lookup"><span data-stu-id="07dbf-143">Motion articles</span></span>

:::row:::
    :::column:::
        ### [Timing and easing](timing-and-easing.md)
        Timing and easing are important elements that make motion feel natural for objects entering, exiting, or moving within the UI.
    :::column-end:::
    :::column:::
        ### [Directionality and gravity](directionality-and-gravity.md)
        Directional signals help provide a solid mental model of the journey a user takes across experiences. Directional movement is subject to forces like gravity, which reinforces the natural feel of the movement.
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        ### [Page transitions](page-transitions.md)
        Page transitions navigate users between pages in an app, providing feedback about the relationship between pages. They help users understand where they are in the navigation hierarchy.
    :::column-end:::
    :::column:::
        ### [Connected animation](connected-animation.md)
        Connected animations let you create a dynamic and compelling navigation experience by animating the transition of an element between two different views.
    :::column-end:::
:::row-end:::
