---
Description: どの Fluent のモーションはタイミングと、イージング関数について説明します。
title: タイミングとイージング - UWP アプリでのアニメーション
label: Timing and easing
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: stmoy
design-contact: jeffarn
doc-status: Draft
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: b736a10a7284e3cc9aa193e082dc654e908afe40
ms.sourcegitcommit: cc0ef75f314658b14376eb60ef8e5bb4d7726e04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65444174"
---
# <a name="timing-and-easing"></a><span data-ttu-id="d2a7d-104">タイミングとイージング</span><span class="sxs-lookup"><span data-stu-id="d2a7d-104">Timing and easing</span></span>

<span data-ttu-id="d2a7d-105">モーションが現実世界に基づいている場合、私たちは速度とパフォーマンスへの期待を伴うデジタル メディアでもあります。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-105">While motion is based in the real world, we are also a digital medium, which comes with an expectation of speed and performance.</span></span>

## <a name="examples"></a><span data-ttu-id="d2a7d-106">例</span><span class="sxs-lookup"><span data-stu-id="d2a7d-106">Examples</span></span>

<table>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon.png" alt="XAML controls gallery" width="168"></img></td>
<td>
    <p><span data-ttu-id="d2a7d-107">ある場合、 <strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong>アプリをインストールするには、ここをクリックして<a href="xamlcontrolsgallery:/item/EasingFunction">アプリを開き、アクションのイージング関数を参照してください</a>します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-107">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/EasingFunction">open the app and see Easing Functions in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="d2a7d-108"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="d2a7d-108"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="d2a7d-109"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="d2a7d-109"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="how-fluent-motion-uses-time"></a><span data-ttu-id="d2a7d-110">Fluent モーションが時間を使用する方法</span><span class="sxs-lookup"><span data-stu-id="d2a7d-110">How Fluent motion uses time</span></span>

<span data-ttu-id="d2a7d-111">タイミングは、UI 内で出入りしたり、移動したりするオブジェクトのモーションを自然に感じさせる重要な要素です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-111">Timing is an important element to making motion feel natural for objects entering, exiting, or moving within the UI.</span></span>

1. <span data-ttu-id="d2a7d-112">ビューに入るオブジェクトまたはシーンはあっという間ですが、美しく彩ります。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-112">Objects or scenes entering the view are quick, but celebrated.</span></span> <span data-ttu-id="d2a7d-113">これらのアニメーションは、通常、シーンの階層的なビルドアップを可能にするために、シーンから出るときより継続時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-113">These animations are typically longer in duration than exits to allow for hierarchical build-up of a scene.</span></span>
1. <span data-ttu-id="d2a7d-114">ビューを出るオブジェクトまたはシーンは、非常にあっという間です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-114">Objects or scenes exiting the view are very quick.</span></span> <span data-ttu-id="d2a7d-115">ユーザーは、UI がどこに行ったかを理解できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-115">The user should be able to understand where the UI went.</span></span> <span data-ttu-id="d2a7d-116">ただし、UI が閉じたら、それが邪魔にならないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-116">However, once the UI is dismissed, it should get out of the way.</span></span>
1. <span data-ttu-id="d2a7d-117">シーンを移動するオブジェクトは、移動距離に適した時間が必要です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-117">Objects translating across a scene should have a duration appropriate to the amount of distance they travel.</span></span>

## <a name="timing-in-fluent-motion"></a><span data-ttu-id="d2a7d-118">Fluent モーションのタイミング</span><span class="sxs-lookup"><span data-stu-id="d2a7d-118">Timing in Fluent motion</span></span>

<span data-ttu-id="d2a7d-119">Fluent のモーションのタイミングでは、ベースラインとして 500 ミリ秒 (0.5 秒) を使用します。これはユーザーが瞬間に認識する最長時間です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-119">The timing of motion in Fluent uses 500ms (or one-half second) as a baseline because this is the maximum amount of time that a user perceives as instant.</span></span>

![ヒーロー イメージ](images/time.gif)

### <a name="150ms-exit"></a><span data-ttu-id="d2a7d-121">**150ミリ秒** (終了)</span><span class="sxs-lookup"><span data-stu-id="d2a7d-121">**150ms** (Exit)</span></span>

:::row:::
    :::column:::
<span data-ttu-id="d2a7d-122">オブジェクトまたはシーンの終了は、または終了しているページに使用します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-122">Use for objects or pages that are exiting the scene or closing.</span></span>
<span data-ttu-id="d2a7d-123">終了する UI の非常に速い方向性フィードバックを可能にします。ここでは、スムーズなアニメーションを実現するためにタイミングがフレーム レートを妨げることはありません。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-123">Allows for very quick directional feedback of exiting UI where timing does not impede upon framerate to achieve a smooth animation.</span></span>
    :::column-end:::
    :::column:::
        ![150ms motion](images/150msAlt.gif)
    :::column-end:::
:::row-end:::

### <a name="300ms-enter"></a><span data-ttu-id="d2a7d-124">**300 ミリ秒** (入力)</span><span class="sxs-lookup"><span data-stu-id="d2a7d-124">**300ms** (Enter)</span></span>

:::row:::
    :::column:::
<span data-ttu-id="d2a7d-125">オブジェクトまたはシーンを入力するか、開くページに使用します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-125">Use for objects or pages that are entering the scene or opening.</span></span>
<span data-ttu-id="d2a7d-126">シーンに入るときにコンテンツを彩るために適切な時間が確保されます。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-126">Allows a reasonable amount of time to celebrate content as it enters the scene.</span></span>
    :::column-end:::
    :::column:::
        ![300ms motion](images/300ms.gif)
    :::column-end:::
:::row-end:::

### <a name="500ms-move"></a><span data-ttu-id="d2a7d-127">**≤500 ミリ秒** (移動)</span><span class="sxs-lookup"><span data-stu-id="d2a7d-127">**≤500ms** (Move)</span></span>

:::row:::
    :::column:::
<span data-ttu-id="d2a7d-128">シーンは 1 つまたは複数のシーンの間で翻訳をオブジェクトに使用します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-128">Use for objects which are translating across a single scene or multiple scenes.</span></span> 
    :::column-end:::
    :::column:::
        ![500ms motion](images/500ms.gif)
    :::column-end:::
:::row-end:::

## <a name="easing-in-fluent-motion"></a><span data-ttu-id="d2a7d-129">Fluent モーションのイージング</span><span class="sxs-lookup"><span data-stu-id="d2a7d-129">Easing in Fluent motion</span></span>

<span data-ttu-id="d2a7d-130">イージングは、移動時のオブジェクトの速度を操作する方法です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-130">Easing is a way to manipulate the velocity of an object as it travels.</span></span> <span data-ttu-id="d2a7d-131">Fluent モーションのすべてのエクスペリエンスを結び付ける接着剤です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-131">It's the glue that ties together all the Fluent motion experiences.</span></span> <span data-ttu-id="d2a7d-132">極端ですが、システムで使用されるイージングは、システム内で移動するオブジェクトの物理的な操作感を統合することができます。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-132">While extreme, the easing used in the system helps unify the physical feel of objects moving throughout the system.</span></span> <span data-ttu-id="d2a7d-133">これは、現実世界を模倣し、移動中のオブジェクトがその環境に属しているように感じさせる 1 つの方法です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-133">This is one way to mimic the real world, and make objects in motion feel like they belong in their environment.</span></span>

![ヒーロー イメージ](images/easing.gif)

## <a name="apply-easing-to-motion"></a><span data-ttu-id="d2a7d-135">モーションへのイージングの適用</span><span class="sxs-lookup"><span data-stu-id="d2a7d-135">Apply easing to motion</span></span>

<span data-ttu-id="d2a7d-136">これらのイージングは、より自然な操作感を得るのに役立ち、Fluent モーションのために使用するベースラインとなります。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-136">These easings will help you achieve a more natural feel, and are the baseline we use for Fluent motion.</span></span>

<span data-ttu-id="d2a7d-137">コード例では、推奨されるイージング値を Storyboard アニメーション (XAML) または Composition アニメーション (C#) に適用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-137">The code examples show how to apply recommended easing values to Storyboard animations (XAML) or Composition animations (C#).</span></span>

### <a name="accelerate-exit"></a><span data-ttu-id="d2a7d-138">**高速化**(終了)</span><span class="sxs-lookup"><span data-stu-id="d2a7d-138">**Accelerate** (Exit)</span></span>

:::row:::
    :::column:::
<span data-ttu-id="d2a7d-139">UI またはシーンを終了するオブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-139">Use for UI or objects that are exiting the scene.</span></span>

<span data-ttu-id="d2a7d-140">オブジェクトは、電源になるし、エスケープ ベロシティに到達するまで、運動量を取得します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-140">Objects become powered and gain momentum until they reach escape velocity.</span></span>
<span data-ttu-id="d2a7d-141">結果として得られる感覚は、オブジェクトが、ユーザーの邪魔に活用し付属する新しいコンテンツの場所を確保する最も難しいその試行されています。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-141">The resulting feel is that the object is trying its hardest to get out of the user's way and make room for new content to come in.</span></span>
    :::column-end:::
    :::column:::
        ![accelerate easing](images/accelEase.gif)
    :::column-end:::
:::row-end:::

```
cubic-bezier(0.7 , 0 , 1 , 0.5)
```

```xaml
<!-- Use for XAML Storyboard animations. -->
<Storyboard x:Name="Storyboard">
    <DoubleAnimation Storyboard.TargetName="Translation" Storyboard.TargetProperty="X" From="0" To="200" Duration="0:0:0.15">
        <DoubleAnimation.EasingFunction>
            <ExponentialEase Exponent="4.5" EasingMode="EaseIn" />
        </DoubleAnimation.EasingFunction>
    </DoubleAnimation>
</Storyboard>
```

```csharp
// Use for Composition animations.
CubicBezierEasingFunction accelerate =
    _compositor.CreateCubicBezierEasingFunction(new Vector2(0.7f, 0.0f), new Vector2(1.0f, 0.5f));
_exitAnimation = _compositor.CreateScalarKeyFrameAnimation();
_exitAnimation.InsertKeyFrame(0.0f, _startValue);
_exitAnimation.InsertKeyFrame(1.0f, _endValue, accelerate);
_exitAnimation.Duration = TimeSpan.FromMilliseconds(150);
```

### <a name="decelerate-enter"></a><span data-ttu-id="d2a7d-142">**減速**(入力)</span><span class="sxs-lookup"><span data-stu-id="d2a7d-142">**Decelerate** (Enter)</span></span>

:::row:::
    :::column:::
<span data-ttu-id="d2a7d-143">オブジェクトまたはシーンを入力する UI を移動するか、起動に使用します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-143">Use for objects or UI entering the scene, either navigating or spawning.</span></span>

<span data-ttu-id="d2a7d-144">シーンのオブジェクトは、極端な摩擦が rest にオブジェクトの速度は満たされます。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-144">Once on-scene, the object is met with extreme friction, which slows the object to rest.</span></span>
<span data-ttu-id="d2a7d-145">結果として得られる感覚は、オブジェクトの旅行時間の長い距離を離れてからするか、極端な速度では、時に入力したして、rest の状態にすばやく返すことがしたです。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-145">The resulting feel is that the object traveled from a long distance away and entered at an extreme velocity, or is quickly returning to a rest state.</span></span>

<span data-ttu-id="d2a7d-146">無応答の少し前に、場合でも、受信オブジェクトの速度は高速で応答性を感じての効果を持ちます。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-146">Even if it's preceded by a moment of unresponsiveness, the velocity of the incoming object has the effect of feeling fast and responsive.</span></span>
    :::column-end:::
    :::column:::
        ![decelerate easing](images/decelEase.gif)
    :::column-end:::
:::row-end:::

```
cubic-bezier(0.1 , 0.9 , 0.2 , 1)
```

```xaml
<!-- Use for XAML Storyboard animations. -->
<Storyboard x:Name="Storyboard">
    <DoubleAnimation Storyboard.TargetName="Translation" Storyboard.TargetProperty="X" From="0" To="200" Duration="0:0:0.3">
        <DoubleAnimation.EasingFunction>
            <ExponentialEase Exponent="7" EasingMode="EaseOut" />
        </DoubleAnimation.EasingFunction>
    </DoubleAnimation>
</Storyboard>
```

```csharp
// Use for Composition animations.
CubicBezierEasingFunction decelerate =
    _compositor.CreateCubicBezierEasingFunction(new Vector2(0.1f, 0.9f), new Vector2(0.2f, 1.0f));
_enterAnimation = _compositor.CreateScalarKeyFrameAnimation();
_enterAnimation.InsertKeyFrame(0.0f, _startValue);
_enterAnimation.InsertKeyFrame(1.0f, _endValue, decelerate);
_enterAnimation.Duration = TimeSpan.FromMilliseconds(300);
```

### <a name="standard-easing-move"></a><span data-ttu-id="d2a7d-147">**標準的なイージング**(移動)</span><span class="sxs-lookup"><span data-stu-id="d2a7d-147">**Standard Easing** (Move)</span></span>

:::row:::
    :::column:::
<span data-ttu-id="d2a7d-148">これは、システム内でアニメーション化されたパラメーターの変更のイージング基準です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-148">This is the baseline easing for any animated parameter change inside of the system.</span></span>
<span data-ttu-id="d2a7d-149">単純な位置変更など、画面上で状態ごとに変化するオブジェクトに標準的なイージングを使用します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-149">Use standard easing for objects that change from state to state on-screen, such as a simple position change.</span></span> <span data-ttu-id="d2a7d-150">また、拡大するオブジェクトのように、シーン内でモーフィングするオブジェクトに使用します。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-150">Also, use it for objects morphing in-scene, like an object that grows.</span></span>

<span data-ttu-id="d2a7d-151">結果として得られる感覚は、A から B に状態を変更するオブジェクトの解決は、自然の強制によって実行される、です。</span><span class="sxs-lookup"><span data-stu-id="d2a7d-151">The resulting feel is that objects changing state from A to B are overcoming, and taken over by, natural forces.</span></span>
    :::column-end:::
    :::column:::
        ![standard easing](images/standardEase.gif)
    :::column-end:::
:::row-end:::

```
cubic-bezier(0.8 , 0 , 0.2 , 1)
```

```xaml
<!-- Use for XAML Storyboard animations. -->
<Storyboard x:Name="Storyboard">
    <DoubleAnimation Storyboard.TargetName="Translation" Storyboard.TargetProperty="X" From="0" To="200" Duration="0:0:0.5">
        <DoubleAnimation.EasingFunction>
            <CircleEase EasingMode="EaseInOut" />
        </DoubleAnimation.EasingFunction>
    </DoubleAnimation>
</Storyboard>
```

```csharp
// Use for Composition animations.
CubicBezierEasingFunction standard =
    _compositor.CreateCubicBezierEasingFunction(new Vector2(0.8f, 0.0f), new Vector2(0.2f, 1.0f));
 _moveAnimation = _compositor.CreateScalarKeyFrameAnimation();
 _moveAnimation.InsertKeyFrame(0.0f, _startValue);
 _moveAnimation.InsertKeyFrame(1.0f, _endValue, standard);
 _moveAnimation.Duration = TimeSpan.FromMilliseconds(500);
```

## <a name="related-articles"></a><span data-ttu-id="d2a7d-152">関連記事</span><span class="sxs-lookup"><span data-stu-id="d2a7d-152">Related articles</span></span>

- [<span data-ttu-id="d2a7d-153">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="d2a7d-153">Motion overview</span></span>](index.md)
- [<span data-ttu-id="d2a7d-154">方向性と重力</span><span class="sxs-lookup"><span data-stu-id="d2a7d-154">Directionality and gravity</span></span>](directionality-and-gravity.md)
