---
Description: タッチ向けに最適化される一方で、さまざまな入力デバイスで一貫した機能を提供する、直観的で独特なユーザー操作エクスペリエンスを備えたユニバーサル Windows プラットフォーム (UWP) アプリを作成します。
title: タッチ操作
ms.assetid: DA6EBC88-EB18-4418-A98A-457EA1DEA88A
label: Touch interactions
template: detail.hbs
keywords: タッチ, ポインター, 入力, ユーザーの操作
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: d5de2af483ca000909e60e94fc41d2a88a405219
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365180"
---
# <a name="touch-interactions"></a><span data-ttu-id="c62a1-104">タッチ操作</span><span class="sxs-lookup"><span data-stu-id="c62a1-104">Touch interactions</span></span>


<span data-ttu-id="c62a1-105">タッチがユーザーの主な入力方法になるという想定でアプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-105">Design your app with the expectation that touch will be the primary input method of your users.</span></span> <span data-ttu-id="c62a1-106">UWP コントロールを使う場合は、タッチパッド、マウス、ペン/スタイラスをサポートするために追加のプログラミングを行う必要はありません。UWP アプリでは、それらが無料で提供されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-106">If you use UWP controls, support for touchpad, mouse, and pen/stylus requires no additional programming, because UWP apps provide this for free.</span></span>

<span data-ttu-id="c62a1-107">ただし、タッチ用に最適化された UI が従来の UI よりも常に優れているとは限らないことに留意してください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-107">However, keep in mind that a UI optimized for touch is not always superior to a traditional UI.</span></span> <span data-ttu-id="c62a1-108">どちらの UI にも、テクノロジとアプリに固有の長所と短所があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-108">Both provide advantages and disadvantages that are unique to a technology and application.</span></span> <span data-ttu-id="c62a1-109">タッチ操作主体の UI に移行する際に、タッチ (タッチパッドを含む)、ペン/スタイラス、マウス、キーボードの各入力の主な違いを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-109">In the move to a touch-first UI, it is important to understand the core differences between touch (including touchpad), pen/stylus, mouse, and keyboard input.</span></span>

> <span data-ttu-id="c62a1-110">**重要な API**:[**Windows.UI.Xaml.Input**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input)、 [ **Windows.UI.Core**](https://docs.microsoft.com/uwp/api/Windows.UI.Core)、 [ **Windows.Devices.Input**](https://docs.microsoft.com/uwp/api/Windows.Devices.Input)</span><span class="sxs-lookup"><span data-stu-id="c62a1-110">**Important APIs**: [**Windows.UI.Xaml.Input**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input), [**Windows.UI.Core**](https://docs.microsoft.com/uwp/api/Windows.UI.Core), [**Windows.Devices.Input**](https://docs.microsoft.com/uwp/api/Windows.Devices.Input)</span></span>


<span data-ttu-id="c62a1-111">多くのデバイスに、1 本または複数の指 (つまりタッチ接触) を入力として使うことをサポートするマルチタッチ画面が搭載されています。</span><span class="sxs-lookup"><span data-stu-id="c62a1-111">Many devices have multi-touch screens that support using one or more fingers (or touch contacts) as input.</span></span> <span data-ttu-id="c62a1-112">タッチ接触とその移動は、さまざまなユーザー操作をサポートするタッチ ジェスチャや操作として解釈されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-112">The touch contacts, and their movement, are interpreted as touch gestures and manipulations to support various user interactions.</span></span>

<span data-ttu-id="c62a1-113">ユニバーサル Windows プラットフォーム (UWP) にはタッチ入力を処理するためのさまざまなメカニズムがあり、ユーザーが安心して操作できるイマーシブ エクスペリエンスを実現できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-113">The Universal Windows Platform (UWP) includes a number of different mechanisms for handling touch input, enabling you to create an immersive experience that your users can explore with confidence.</span></span> <span data-ttu-id="c62a1-114">ここでは、UWP アプリでタッチ入力を使用する場合の基本事項について説明します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-114">Here, we cover the basics of using touch input in a UWP app.</span></span>

<span data-ttu-id="c62a1-115">タッチ操作には、次の 3 つが必要です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-115">Touch interactions require three things:</span></span>

-   <span data-ttu-id="c62a1-116">タッチ パネル ディスプレイ。</span><span class="sxs-lookup"><span data-stu-id="c62a1-116">A touch-sensitive display.</span></span>
-   <span data-ttu-id="c62a1-117">1 本以上の指による、そのディスプレイへの直接的な (ディスプレイに近接センサーがあり、ホバー検知がサポートされている場合は近接的な) 接触</span><span class="sxs-lookup"><span data-stu-id="c62a1-117">The direct contact (or proximity to, if the display has proximity sensors and supports hover detection) of one or more fingers on that display.</span></span>
-   <span data-ttu-id="c62a1-118">タッチ接触の動き (または、時間のしきい値に基づく動きの欠落)。</span><span class="sxs-lookup"><span data-stu-id="c62a1-118">Movement of the touch contacts (or lack thereof, based on a time threshold).</span></span>

<span data-ttu-id="c62a1-119">タッチ センサーから提供される入力データは、次のように使うことができます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-119">The input data provided by the touch sensor can be:</span></span>

-   <span data-ttu-id="c62a1-120">1 つ以上の UI 要素に直接的な操作 (パン、回転、サイズ変更、移動など) を行う物理的なジェスチャとして解釈する。</span><span class="sxs-lookup"><span data-stu-id="c62a1-120">Interpreted as a physical gesture for direct manipulation of one or more UI elements (such as panning, rotating, resizing, or moving).</span></span> <span data-ttu-id="c62a1-121">プロパティ ウィンドウ、ダイアログ ボックス、その他の UI アフォーダンスを通じた要素との対話的操作は、間接的な操作と見なされます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-121">In contrast, interacting with an element through its properties window, dialog box, or other UI affordance is considered indirect manipulation.</span></span>
-   <span data-ttu-id="c62a1-122">マウス、ペンなどの代替の入力方式として見なす。</span><span class="sxs-lookup"><span data-stu-id="c62a1-122">Recognized as an alternative input method, such as mouse or pen.</span></span>
-   <span data-ttu-id="c62a1-123">他の入力方法の外観を補完するために使う (ペンで描画したインク ストロークをこするなど)。</span><span class="sxs-lookup"><span data-stu-id="c62a1-123">Used to complement or modify aspects of other input methods, such as smudging an ink stroke drawn with a pen.</span></span>

<span data-ttu-id="c62a1-124">タッチ入力では、通常、画面上の要素を直接操作します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-124">Touch input typically involves the direct manipulation of an element on the screen.</span></span> <span data-ttu-id="c62a1-125">要素は、そのヒット テスト領域内でのタッチ接触をすぐに応答し、削除など、タッチ接触の後続の動きに適切に反応します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-125">The element responds immediately to any touch contact within its hit test area, and reacts appropriately to any subsequent movement of the touch contacts, including removal.</span></span>

<span data-ttu-id="c62a1-126">カスタム タッチ ジェスチャと操作は、慎重に設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-126">Custom touch gestures and interactions should be designed carefully.</span></span> <span data-ttu-id="c62a1-127">直感的で、応答性が高く、見つけやすい必要があり、ユーザーが安心してアプリを操作できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-127">They should be intuitive, responsive, and discoverable, and they should let users explore your app with confidence.</span></span>

<span data-ttu-id="c62a1-128">アプリの機能がサポートされているすべての入力デバイスの種類で一貫して公開されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-128">Ensure that app functionality is exposed consistently across every supported input device type.</span></span> <span data-ttu-id="c62a1-129">必要に応じて、キーボード操作に対応するテキスト入力、またはマウスやペンの UI アフォーダンスなど、なんらかの形で間接的な入力モードを用意します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-129">If necessary, use some form of indirect input mode, such as text input for keyboard interactions, or UI affordances for mouse and pen.</span></span>

<span data-ttu-id="c62a1-130">多くのユーザーにとって従来型入力デバイス (マウスやキーボードなど) が親しみやすく魅力的であることを念頭に置いてください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-130">Remember that traditional input devices (such as mouse and keyboard), are familiar and appealing to many users.</span></span> <span data-ttu-id="c62a1-131">従来型入力デバイスは、速度、正確さ、触覚的なフィードバックという点で、タッチ操作より優れている場合があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-131">They can offer speed, accuracy, and tactile feedback that touch might not.</span></span>

<span data-ttu-id="c62a1-132">すべての入力デバイスに固有なそれぞれの対話式操作のエクスペリエンスにより、多様な機能や基本設定をサポートし、できるだけ幅広い対象者の関心を引くことで、アプリのユーザーを増やすことができます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-132">Providing unique and distinctive interaction experiences for all input devices will support the widest range of capabilities and preferences, appeal to the broadest possible audience, and attract more customers to your app.</span></span>

## <a name="compare-touch-interaction-requirements"></a><span data-ttu-id="c62a1-133">タッチ操作の要件の比較</span><span class="sxs-lookup"><span data-stu-id="c62a1-133">Compare touch interaction requirements</span></span>

<span data-ttu-id="c62a1-134">次の表に、タッチ操作に最適な UWP アプリの設計時に考慮する必要がある、入力デバイス間の違いをいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-134">The following table shows some of the differences between input devices that you should consider when you design touch-optimized UWP apps.</span></span>

<table>
<tbody><tr><th><span data-ttu-id="c62a1-135">要因</span><span class="sxs-lookup"><span data-stu-id="c62a1-135">Factor</span></span></th><th><span data-ttu-id="c62a1-136">タッチ操作</span><span class="sxs-lookup"><span data-stu-id="c62a1-136">Touch interactions</span></span></th><th><span data-ttu-id="c62a1-137">マウス、キーボード、ペン/スタイラス操作</span><span class="sxs-lookup"><span data-stu-id="c62a1-137">Mouse, keyboard, pen/stylus interactions</span></span></th><th><span data-ttu-id="c62a1-138">タッチパッド</span><span class="sxs-lookup"><span data-stu-id="c62a1-138">Touchpad</span></span></th></tr>
<tr><td rowspan="3"><span data-ttu-id="c62a1-139">有効桁数</span><span class="sxs-lookup"><span data-stu-id="c62a1-139">Precision</span></span></td><td><span data-ttu-id="c62a1-140">指先が接触する領域は単一の XY 座標よりも広いので、意図していないコマンドがアクティブ化される可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-140">The contact area of a fingertip is greater than a single x-y coordinate, which increases the chances of unintended command activations.</span></span></td><td><span data-ttu-id="c62a1-141">マウスとペン/スタイラスを使うと正確な XY 座標を指定できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-141">The mouse and pen/stylus supply a precise x-y coordinate.</span></span></td><td><span data-ttu-id="c62a1-142">マウスと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-142">Same as mouse.</span></span></td></tr>
<tr><td><span data-ttu-id="c62a1-143">接触する領域の形は移動を通じて変化します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-143">The shape  of the contact area changes throughout the movement.</span></span>  </td><td><span data-ttu-id="c62a1-144">マウスの移動とペン/スタイラスのストロークによって正確な XY 座標を指定できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-144">Mouse movements and pen/stylus strokes supply precise x-y coordinates.</span></span> <span data-ttu-id="c62a1-145">キーボード フォーカスは明示的です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-145">Keyboard focus is explicit.</span></span></td><td><span data-ttu-id="c62a1-146">マウスと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-146">Same as mouse.</span></span></td></tr>
<tr><td><span data-ttu-id="c62a1-147">ターゲット設定に役立つマウス カーソルはありません。</span><span class="sxs-lookup"><span data-stu-id="c62a1-147">There is no mouse cursor to assist with targeting.</span></span></td><td><span data-ttu-id="c62a1-148">マウス カーソル、ペン/スタイラス カーソル、キーボード フォーカスはすべてターゲット設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-148">The mouse cursor, pen/stylus cursor, and keyboard focus all assist with targeting.</span></span></td><td><span data-ttu-id="c62a1-149">マウスと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-149">Same as mouse.</span></span></td></tr>
<tr><td rowspan="3"><span data-ttu-id="c62a1-150">人体構造</span><span class="sxs-lookup"><span data-stu-id="c62a1-150">Human anatomy</span></span></td><td><span data-ttu-id="c62a1-151">1 本または複数の指で直線移動を行うのは困難なので、指先の動きは正確さに欠けます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-151">Fingertip movements are imprecise, because a straight-line motion with one or more fingers is difficult.</span></span> <span data-ttu-id="c62a1-152">これは、手関節が曲がることや動きに関係する関節の数が原因です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-152">This is due to the curvature of hand joints and the number of joints involved in the motion.</span></span></td><td><span data-ttu-id="c62a1-153">マウスまたはペン/スタイラスを制御する手の物理的な移動距離は、画面上のカーソルの移動距離よりも短いので、マウスまたはペン/スタイラスで直線移動を行う方が簡単です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-153">It's easier to perform a straight-line motion with the mouse or pen/stylus because the hand that controls them travels a shorter physical distance than the cursor on the screen.</span></span></td><td><span data-ttu-id="c62a1-154">マウスと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-154">Same as mouse.</span></span></td></tr>
<tr><td><span data-ttu-id="c62a1-155">ディスプレイ デバイスのタッチ画面には、指の位置とユーザーのデバイスの持ち方が原因で届きにくくなる領域もあります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-155">Some areas on the touch surface of a display device can be difficult to reach due to finger posture and the user's grip on the device.</span></span></td><td><span data-ttu-id="c62a1-156">マウスとペン/スタイラスは画面のどの部分にも届き、キーボードではタブ オーダーによってどのコントロールにもアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-156">The mouse and pen/stylus can reach any part of the screen while any control should be accessible by the keyboard through tab order.</span></span> </td><td><span data-ttu-id="c62a1-157">指の位置と持ち方が問題になることがあります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-157">Finger posture and grip can be an issue.</span></span></td></tr>
<tr><td><span data-ttu-id="c62a1-158">オブジェクトは、1 本以上の指先またはユーザーの手で隠れる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-158">Objects might be obscured by one or more fingertips or the user's hand.</span></span> <span data-ttu-id="c62a1-159">これをオクルージョンと呼びます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-159">This is known as occlusion.</span></span></td><td><span data-ttu-id="c62a1-160">間接的な入力デバイスでは、オクルージョンは発生しません。</span><span class="sxs-lookup"><span data-stu-id="c62a1-160">Indirect input devices do not cause  occlusion.</span></span></td><td><span data-ttu-id="c62a1-161">マウスと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-161">Same as mouse.</span></span></td></tr>
<tr><td><span data-ttu-id="c62a1-162">オブジェクトの状態</span><span class="sxs-lookup"><span data-stu-id="c62a1-162">Object state</span></span></td><td><span data-ttu-id="c62a1-163">タッチでは、ディスプレイ デバイスのタッチ画面がタッチされているか (オン) タッチされていないか (オフ) の 2 状態モデルが使われます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-163">Touch uses a two-state model: the touch surface of a display device  is either touched (on) or not (off).</span></span> <span data-ttu-id="c62a1-164">追加の視覚的なフィードバックをトリガーできるホバー状態はありません。</span><span class="sxs-lookup"><span data-stu-id="c62a1-164">There is no hover state that can trigger additional visual feedback.</span></span></td><td>
<p><span data-ttu-id="c62a1-165">マウス、ペン/スタイラス、キーボードはすべて、離した状態 (オフ)、押した状態 (オン)、ホバー状態 (フォーカス) の 3 状態モデルを公開します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-165">A mouse, pen/stylus, and keyboard all expose a three-state model: up (off), down (on), and hover (focus).</span></span></p>
<p><span data-ttu-id="c62a1-166">ホバーすると、UI 要素に関連付けられたヒントを調べて参考にすることができます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-166">Hover lets users explore and learn through tooltips  associated with UI elements.</span></span> <span data-ttu-id="c62a1-167">ホバーまたはフォーカスを合わせたときの効果によって操作可能なオブジェクトがわかり、ターゲット設定にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-167">Hover and focus effects  can relay which objects are interactive and also help with targeting.</span></span> 
</p>
</td><td><span data-ttu-id="c62a1-168">マウスと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-168">Same as mouse.</span></span></td></tr>
<tr><td rowspan="2"><span data-ttu-id="c62a1-169">豊富な操作</span><span class="sxs-lookup"><span data-stu-id="c62a1-169">Rich interaction</span></span></td><td><span data-ttu-id="c62a1-170">タッチ画面において複数の入力ポイント (指先) で操作できるマルチタッチをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-170">Supports multi-touch: multiple input points (fingertips) on a touch surface.</span></span></td><td><span data-ttu-id="c62a1-171">単一の入力ポイントをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-171">Supports a single input point.</span></span></td><td><span data-ttu-id="c62a1-172">タッチと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-172">Same as touch.</span></span></td></tr>
<tr><td><span data-ttu-id="c62a1-173">タップ、ドラッグ、スライド、ピンチ、回転などのジェスチャによるオブジェクトの直接操作をサポートします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-173">Supports direct manipulation of objects through gestures such as tapping, dragging, sliding, pinching, and rotating.</span></span></td><td><span data-ttu-id="c62a1-174">マウス、ペン/スタイラス、キーボードは間接的な入力デバイスなので、直接操作はサポートされません。</span><span class="sxs-lookup"><span data-stu-id="c62a1-174">No support for direct manipulation as mouse, pen/stylus, and keyboard are indirect input devices.</span></span></td><td><span data-ttu-id="c62a1-175">マウスと同じです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-175">Same as mouse.</span></span></td></tr>
</tbody></table>



<span data-ttu-id="c62a1-176">**注**  間接的な入力が 25 年以上の洗練化のメリットがありました。</span><span class="sxs-lookup"><span data-stu-id="c62a1-176">**Note**   Indirect input has had the benefit of more than 25 years of refinement.</span></span> <span data-ttu-id="c62a1-177">ホバーすると表示されるヒントなどの機能は、タッチパッド、マウス、ペン/スタイラス、キーボード入力での UI の操作を解決するために特別に設計されています。</span><span class="sxs-lookup"><span data-stu-id="c62a1-177">Features such as hover-triggered tooltips have been designed to solve UI exploration specifically for touchpad, mouse, pen/stylus, and keyboard input.</span></span> <span data-ttu-id="c62a1-178">このような UI 機能は、他のデバイスのユーザー エクスペリエンスを損なうことなく、タッチ入力で充実したエクスペリエンスを提供するために再設計されました。</span><span class="sxs-lookup"><span data-stu-id="c62a1-178">UI features like this have been re-designed for the rich experience provided by touch input, without compromising the user experience for these other devices.</span></span>

 

## <a name="use-touch-feedback"></a><span data-ttu-id="c62a1-179">タッチのフィードバックの使用</span><span class="sxs-lookup"><span data-stu-id="c62a1-179">Use touch feedback</span></span>

<span data-ttu-id="c62a1-180">アプリとの対話中に適切な視覚的なフィードバックには、ユーザーの認識、については、およびその相互作用が、アプリと Windows プラットフォームの両方でどのように解釈される方法に合わせてが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-180">Appropriate visual feedback during interactions with your app helps users recognize, learn, and adapt to how their interactions are interpreted by both the app and the Windows platform.</span></span> <span data-ttu-id="c62a1-181">視覚的なフィードバックの用途は、対話的操作の成功の表示、システム状態の中継、コントロール感の向上、エラーの低減、システムと入力デバイスに関するユーザーの理解の支援、対話的操作の促進などです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-181">Visual feedback can indicate successful interactions, relay system status, improve the sense of control, reduce errors, help users understand the system and input device, and encourage interaction.</span></span>

<span data-ttu-id="c62a1-182">位置に基づく正確性が求められる操作をタッチ入力で行う場合は、視覚的なフィードバックが重要です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-182">Visual feedback is critical when the user relies on touch input for activities that require accuracy and precision based on location.</span></span> <span data-ttu-id="c62a1-183">タッチ入力が検出された場所に必ずフィードバックを表示して、アプリとそのコントロールで定義されたカスタム ターゲット設定規則をユーザーが把握できるようにします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-183">Display feedback whenever and wherever touch input is detected, to help the user understand any custom targeting rules that are defined by your app and its controls.</span></span>


## <a name="targeting"></a><span data-ttu-id="c62a1-184">ターゲット設定</span><span class="sxs-lookup"><span data-stu-id="c62a1-184">Targeting</span></span>

<span data-ttu-id="c62a1-185">ターゲット設定は、次の要素によって最適化します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-185">Targeting is optimized through:</span></span>

-   <span data-ttu-id="c62a1-186">タッチ ターゲットのサイズ</span><span class="sxs-lookup"><span data-stu-id="c62a1-186">Touch target sizes</span></span>

    <span data-ttu-id="c62a1-187">明確なサイズのガイドラインによって、ターゲット設定しやすいオブジェクトとコントロールが含まれる快適な UI を備えたアプリになるようにします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-187">Clear size guidelines ensure that applications provide a comfortable UI that contains objects and controls that are easy and safe to target.</span></span>

-   <span data-ttu-id="c62a1-188">接触形状</span><span class="sxs-lookup"><span data-stu-id="c62a1-188">Contact geometry</span></span>

    <span data-ttu-id="c62a1-189">指が接触する領域全体によって、意図された可能性が最も高いターゲット オブジェクトを特定します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-189">The entire contact area of the finger determines the most likely target object.</span></span>

-   <span data-ttu-id="c62a1-190">スクラブ</span><span class="sxs-lookup"><span data-stu-id="c62a1-190">Scrubbing</span></span>

    <span data-ttu-id="c62a1-191">グループ内の項目 (ラジオ ボタンなど) 間で指をドラッグすると、それらの項目を簡単にターゲット設定し直すことができます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-191">Items within a group are easily re-targeted by dragging the finger between them (for example, radio buttons).</span></span> <span data-ttu-id="c62a1-192">指を離すと現在の項目がアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-192">The current item is activated when the touch is released.</span></span>

-   <span data-ttu-id="c62a1-193">揺らす</span><span class="sxs-lookup"><span data-stu-id="c62a1-193">Rocking</span></span>

    <span data-ttu-id="c62a1-194">密集した複数の項目 (ハイパーリンクなど) を指で押してスライドせずに前後に揺らすと、それらの項目を簡単にターゲット設定し直すことができます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-194">Densely packed items (for example, hyperlinks) are easily re-targeted by pressing the finger down and, without sliding, rocking it back and forth over the items.</span></span> <span data-ttu-id="c62a1-195">オクルージョンが原因で、現在の項目はヒントまたはステータス バーで特定され、指を離すとアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-195">Due to occlusion, the current item is identified through a tooltip or the status bar and is activated when the touch is released.</span></span>

## <a name="accuracy"></a><span data-ttu-id="c62a1-196">正確性</span><span class="sxs-lookup"><span data-stu-id="c62a1-196">Accuracy</span></span>

<span data-ttu-id="c62a1-197">以下を使って、対話的操作が雑な場合に備えて設計します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-197">Design for sloppy interactions by using:</span></span>

-   <span data-ttu-id="c62a1-198">コンテンツの操作時に目的の位置で簡単に停止できるようにするスナップ位置。</span><span class="sxs-lookup"><span data-stu-id="c62a1-198">Snap-points that can make it easier to stop at desired locations when users interact with content.</span></span>
-   <span data-ttu-id="c62a1-199">手をわずかに曲げて動かした場合でも垂直方向または水平方向のパンを実行できる方向 "レール"。詳しくは、「[パンのガイドライン](guidelines-for-panning.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-199">Directional "rails" that can assist with vertical or horizontal panning, even when the hand moves in a slight arc. For more information, see [Guidelines for panning](guidelines-for-panning.md).</span></span>

## <a name="occlusion"></a><span data-ttu-id="c62a1-200">オクルージョン</span><span class="sxs-lookup"><span data-stu-id="c62a1-200">Occlusion</span></span>

<span data-ttu-id="c62a1-201">指と手のオクルージョンは、次の要素によって回避します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-201">Finger and hand occlusion is avoided through:</span></span>

-   <span data-ttu-id="c62a1-202">UI のサイズと配置</span><span class="sxs-lookup"><span data-stu-id="c62a1-202">Size and positioning of UI</span></span>

    <span data-ttu-id="c62a1-203">UI 要素を十分に大きくして、指先が接触する領域で完全にふさぐことができないようにします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-203">Make UI elements big enough so that they cannot be completely covered by a fingertip contact area.</span></span>

    <span data-ttu-id="c62a1-204">メニューとポップアップは、できる限り接触する領域の上に配置します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-204">Position menus and pop-ups above the contact area whenever possible.</span></span>

-   <span data-ttu-id="c62a1-205">ヒント</span><span class="sxs-lookup"><span data-stu-id="c62a1-205">Tooltips</span></span>

    <span data-ttu-id="c62a1-206">指がオブジェクトに接触し続けているときは、ヒントを表示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-206">Show tooltips when a user maintains finger contact on an object.</span></span> <span data-ttu-id="c62a1-207">オブジェクトの機能について説明する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-207">This is useful for describing object functionality.</span></span> <span data-ttu-id="c62a1-208">ヒントが呼び出されないようにするには、ユーザーは指先をオブジェクトの外にドラッグします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-208">The user can drag the fingertip off the object to avoid invoking the tooltip.</span></span>

    <span data-ttu-id="c62a1-209">小さいオブジェクトの場合は、ヒントをずらして、指先が接触する領域でふさがれないようにします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-209">For small objects, offset tooltips so they are not covered by the fingertip contact area.</span></span> <span data-ttu-id="c62a1-210">これはターゲット設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-210">This is helpful for targeting.</span></span>

-   <span data-ttu-id="c62a1-211">正確さを確保するためのハンドル</span><span class="sxs-lookup"><span data-stu-id="c62a1-211">Handles for precision</span></span>

    <span data-ttu-id="c62a1-212">正確さが要求される場合 (テキスト選択など)、正確さを向上させるためにオフセットされる選択ハンドルを用意します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-212">Where precision is required (for example, text selection), provide selection handles that are offset to improve accuracy.</span></span> <span data-ttu-id="c62a1-213">詳しくは、「[テキストと画像の選択のガイドライン (Windows ランタイム アプリ)](guidelines-for-textselection.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-213">For more information, see [Guidelines for selecting text and images (Windows Runtime apps)](guidelines-for-textselection.md).</span></span>

## <a name="timing"></a><span data-ttu-id="c62a1-214">タイミング</span><span class="sxs-lookup"><span data-stu-id="c62a1-214">Timing</span></span>

<span data-ttu-id="c62a1-215">直接操作を行うために、時間制限のあるモードの変更を避けます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-215">Avoid timed mode changes in favor of direct manipulation.</span></span> <span data-ttu-id="c62a1-216">直接操作は、オブジェクトに対するリアルタイムで物理的な直接処理をシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-216">Direct manipulation simulates the direct, real-time physical handling of an object.</span></span> <span data-ttu-id="c62a1-217">オブジェクトは指の動きに合わせて反応します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-217">The object responds as the fingers are moved.</span></span>

<span data-ttu-id="c62a1-218">一方、時間制限のある操作は、タッチ操作の後に発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-218">A timed interaction, on the other hand, occurs after a touch interaction.</span></span> <span data-ttu-id="c62a1-219">通常、時間制限のある操作では、時間、距離、速度などの見えないしきい値に基づいて実行するコマンドが決定されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-219">Timed interactions typically depend on invisible thresholds like time, distance, or speed to determine what command to perform.</span></span> <span data-ttu-id="c62a1-220">システムで操作が実行されるまで、時間制限のある操作では視覚的なフィードバックは返されません。</span><span class="sxs-lookup"><span data-stu-id="c62a1-220">Timed interactions have no visual feedback until the system performs the action.</span></span>

<span data-ttu-id="c62a1-221">直接操作には、時間制限のある対話式操作と比べて、いくつかの利点があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-221">Direct manipulation provides a number of benefits over timed interactions:</span></span>

-   <span data-ttu-id="c62a1-222">対話式操作中に視覚的なフィードバックがすばやく返されるので、ユーザーはより集中して、すべてを制御しているという安心感を持って操作できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-222">Instant visual feedback during interactions make users feel more engaged, confident, and in control.</span></span>
-   <span data-ttu-id="c62a1-223">直接操作は元に戻すことができるので、安心してシステムを使うことができます。ユーザーは、論理的かつ直観的な方法で操作を簡単にさかのぼることができます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-223">Direct manipulations make it safer to explore a system because they are reversible—users can easily step back through their actions in a logical and intuitive manner.</span></span>
-   <span data-ttu-id="c62a1-224">オブジェクトに直接影響して実際の対話式操作を模倣する操作は、より直観的で見つけやすく覚えやすい対話式操作です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-224">Interactions that directly affect objects and mimic real world interactions are more intuitive, discoverable, and memorable.</span></span> <span data-ttu-id="c62a1-225">わかりにくい抽象的な対話式操作には依存しません。</span><span class="sxs-lookup"><span data-stu-id="c62a1-225">They don't rely on obscure or abstract interactions.</span></span>
-   <span data-ttu-id="c62a1-226">時間制限のある対話式操作は、任意の見えないしきい値に達する必要があるので、実行が難しい場合があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-226">Timed interactions can be difficult to perform, as users must reach arbitrary and invisible thresholds.</span></span>

<span data-ttu-id="c62a1-227">また、次の点を考慮することを強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-227">In addition, the following are strongly recommended:</span></span>

-   <span data-ttu-id="c62a1-228">操作は、使う指の数で区別しないでください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-228">Manipulations should not be distinguished by the number of fingers used.</span></span>
-   <span data-ttu-id="c62a1-229">複合操作をサポートしてください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-229">Interactions should support compound manipulations.</span></span> <span data-ttu-id="c62a1-230">たとえば、ピンチによるズームを行いながら指をドラッグしてパンできるようにします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-230">For example, pinch to zoom while dragging the fingers to pan.</span></span>
-   <span data-ttu-id="c62a1-231">対話式操作を時間で区別しないでください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-231">Interactions should not be distinguished by time.</span></span> <span data-ttu-id="c62a1-232">実行にかかる時間に関係なく、同じ対話式操作を行うと同じ結果が得られるようにします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-232">The same interaction should have the same outcome regardless of the time taken to perform it.</span></span> <span data-ttu-id="c62a1-233">時間ベースのアクティブ化では、ユーザーは遅延を強いられるので、直接操作のイマーシブの特性が損なわれ、システムの応答性が低く感じられるようになります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-233">Time-based activations introduce mandatory delays for users and detract from both the immersive nature of direct manipulation and the perception of system responsiveness.</span></span>

    <span data-ttu-id="c62a1-234">**注**  この例外は、学習と調査 (例、プレス アンド ホールド) を支援するために特定の時間指定の相互作用を使用します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-234">**Note**  An exception to this is where you use specific timed interactions to assist in learning and exploration (for example, press and hold).</span></span>

     

-   <span data-ttu-id="c62a1-235">適切な説明と視覚的な合図を使うと、高度な対話式操作を非常に効果的に使用できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-235">Appropriate descriptions and visual cues have a great effect on the use of advanced interactions.</span></span>


## <a name="app-views"></a><span data-ttu-id="c62a1-236">アプリ ビュー</span><span class="sxs-lookup"><span data-stu-id="c62a1-236">App views</span></span>


<span data-ttu-id="c62a1-237">アプリのビューのパン/スクロールとズームの設定を使って、ユーザー操作エクスペリエンスを調整します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-237">Tweak the user interaction experience through the pan/scroll and zoom settings of your app views.</span></span> <span data-ttu-id="c62a1-238">アプリ ビューによって、ユーザーがアプリとそのコンテンツにアクセスして操作する方法が決まります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-238">An app view dictates how a user accesses and manipulates your app and its content.</span></span> <span data-ttu-id="c62a1-239">ビューは、慣性、コンテンツ境界の跳ね返り、スナップ位置などの動作も提供します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-239">Views also provide behaviors such as inertia, content boundary bounce, and snap points.</span></span>

<span data-ttu-id="c62a1-240">[  **ScrollViewer**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer) コントロールのパンとスクロールの設定により、ビューのコンテンツがビューポートに収まらない場合に、単一のビュー内でユーザーがどのように移動するかが決まります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-240">Pan and scroll settings of the [**ScrollViewer**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer) control dictate how users navigate within a single view, when the content of the view doesn't fit within the viewport.</span></span> <span data-ttu-id="c62a1-241">単一のビューは、たとえば雑誌や本のページ、コンピューターのフォルダー構造、ドキュメントのライブラリ、フォト アルバムなどです。</span><span class="sxs-lookup"><span data-stu-id="c62a1-241">A single view can be, for example, a page of a magazine or book, the folder structure of a computer, a library of documents, or a photo album.</span></span>

<span data-ttu-id="c62a1-242">ズームの設定は、光学式ズーム ([**ScrollViewer**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer) コントロールによってサポートされる) と [**Semantic Zoom**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) コントロールの両方に適用されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-242">Zoom settings apply to both optical zoom (supported by the [**ScrollViewer**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer) control) and the [**Semantic Zoom**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) control.</span></span> <span data-ttu-id="c62a1-243">セマンティック ズームは、タッチに最適化された手法の 1 つであり、関連する大量のデータやコンテンツを 1 つのビュー内に表示してナビゲートします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-243">Semantic Zoom is a touch-optimized technique for presenting and navigating large sets of related data or content within a single view.</span></span> <span data-ttu-id="c62a1-244">この機能では、2 つの分類モード (ズーム レベル) が使われます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-244">It works by using two distinct modes of classification, or zoom levels.</span></span> <span data-ttu-id="c62a1-245">これは、1 つのビュー内でのパンとスクロールに似ています。</span><span class="sxs-lookup"><span data-stu-id="c62a1-245">This is analogous to panning and scrolling within a single view.</span></span> <span data-ttu-id="c62a1-246">パンとスクロールは、セマンティック ズームと組み合わせて使うことができます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-246">Panning and scrolling can be used in conjunction with Semantic Zoom.</span></span>

<span data-ttu-id="c62a1-247">パン/スクロールとズーム動作を変更するには、アプリのビューとイベントを使います。</span><span class="sxs-lookup"><span data-stu-id="c62a1-247">Use app views and events to modify the pan/scroll and zoom behaviors.</span></span> <span data-ttu-id="c62a1-248">こうすることで、ポインターとジェスチャ イベントを処理する場合よりもスムーズな操作エクスペリエンスを提供できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-248">This can provide a smoother interaction experience than is possible through the handling of pointer and gesture events.</span></span>

<span data-ttu-id="c62a1-249">アプリ ビューについて詳しくは、「[コントロール、レイアウト、テキスト](https://docs.microsoft.com/windows/uwp/design/basics/)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-249">For more info about app views, see [Controls, layouts, and text](https://docs.microsoft.com/windows/uwp/design/basics/).</span></span>

## <a name="custom-touch-interactions"></a><span data-ttu-id="c62a1-250">カスタム タッチ操作</span><span class="sxs-lookup"><span data-stu-id="c62a1-250">Custom touch interactions</span></span>


<span data-ttu-id="c62a1-251">独自の対話式操作サポートを実装する場合は、ユーザーはアプリの UI 要素を直接操作できる直感的なエクスペリエンスを期待しているということを心に留めておいてください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-251">If you implement your own interaction support, keep in mind that users expect an intuitive experience involving direct interaction with the UI elements in your app.</span></span> <span data-ttu-id="c62a1-252">プラットフォーム コントロール ライブラリでカスタムの対話式操作をモデル化し、一貫性と見つけやすさを維持することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-252">We recommend that you model your custom interactions on the platform control libraries to keep things consistent and discoverable.</span></span> <span data-ttu-id="c62a1-253">これらのライブラリのコントロールでは、標準的な対話式操作、アニメーション化された物理的効果、視覚的フィードバック、アクセシビリティなど、完全なユーザー操作エクスペリエンスが提供されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-253">The controls in these libraries provide the full user interaction experience, including standard interactions, animated physics effects, visual feedback, and accessibility.</span></span> <span data-ttu-id="c62a1-254">はっきりとした明確に定義されている要件があり、基本的な対話式操作ではシナリオがサポートされない場合のみ、カスタムの対話式操作を作ってください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-254">Create custom interactions only if there is a clear, well-defined requirement and basic interactions don't support your scenario.</span></span>

<span data-ttu-id="c62a1-255">カスタマイズされたタッチ サポートを提供するために、さまざまな [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) イベントを処理できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-255">To provide customized touch support, you can handle various [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) events.</span></span> <span data-ttu-id="c62a1-256">これらのイベントは、次の 3 つのレベルのアブストラクションにグループ化されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-256">These events are grouped into three levels of abstraction.</span></span>

-   <span data-ttu-id="c62a1-257">静的ジェスチャ イベントは、対話式操作が完了した後に発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-257">Static gesture events are triggered after an interaction is complete.</span></span> <span data-ttu-id="c62a1-258">ジェスチャ イベントには、[**Tapped**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.tapped)、[**DoubleTapped**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.doubletapped)、[**RightTapped**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.righttapped)、[**Holding**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.holding) があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-258">Gesture events include [**Tapped**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.tapped), [**DoubleTapped**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.doubletapped), [**RightTapped**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.righttapped), and [**Holding**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.holding).</span></span>

    <span data-ttu-id="c62a1-259">[  **IsTapEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.istapenabled)、[**IsDoubleTapEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.isdoubletapenabled)、[**IsRightTapEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.isrighttapenabled)、[**IsHoldingEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.isholdingenabled) を **false** に設定して、これらのジェスチャ イベントを無効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-259">You can disable gesture events on specific elements by setting [**IsTapEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.istapenabled), [**IsDoubleTapEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.isdoubletapenabled), [**IsRightTapEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.isrighttapenabled), and [**IsHoldingEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.isholdingenabled) to **false**.</span></span>

-   <span data-ttu-id="c62a1-260">[  **PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed) や [**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointermoved) などのポインター イベントは、ポインター モーションや、押すイベントと離すイベントの識別機能などの下位レベルの詳細を提供します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-260">Pointer events such as [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed) and [**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointermoved) provide low-level details for each touch contact, including pointer motion and the ability to distinguish press and release events.</span></span>

    <span data-ttu-id="c62a1-261">ポインターは、統合イベント メカニズムを持つ一般的な入力の種類です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-261">A pointer is a generic input type with a unified event mechanism.</span></span> <span data-ttu-id="c62a1-262">アクティブな入力ソース (タッチ、タッチパッド、マウス、またはペン) についての画面位置などの基本的な情報を公開します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-262">It exposes basic info, such as screen position, on the active input source, which can be touch, touchpad, mouse, or pen.</span></span>

-   <span data-ttu-id="c62a1-263">[  **ManipulationStarted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarted) などの操作ジェスチャ イベントは継続的な対話式操作を示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-263">Manipulation gesture events, such as [**ManipulationStarted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarted), indicate an ongoing interaction.</span></span> <span data-ttu-id="c62a1-264">操作ジェスチャ イベントはユーザーが要素にタッチしたときに発生し、ユーザーが指を離すか操作が取り消されるまで続きます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-264">They start firing when the user touches an element and continue until the user lifts their finger(s), or the manipulation is canceled.</span></span>

    <span data-ttu-id="c62a1-265">操作イベントには、ズーム、パン、回転などのマルチタッチ操作や、ドラッグなどの慣性と速度データを使った操作の場合は、操作イベントを使います。</span><span class="sxs-lookup"><span data-stu-id="c62a1-265">Manipulation events include multi-touch interactions such as zooming, panning, or rotating, and interactions that use inertia and velocity data such as dragging.</span></span> <span data-ttu-id="c62a1-266">操作イベントで提供される情報は、実行された操作のフォームを識別するのではなく、位置、変換デルタ、速度などのタッチ データを含みます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-266">The information provided by the manipulation events doesn't identify the form of the interaction that was performed, but rather includes data such as position, translation delta, and velocity.</span></span> <span data-ttu-id="c62a1-267">このタッチ データを使って、実行された操作の種類を確認できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-267">You can use this touch data to determine the type of interaction that should be performed.</span></span>

<span data-ttu-id="c62a1-268">UWP でサポートされている基本的なタッチ ジェスチャのセットを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-268">Here is the basic set of touch gestures supported by the UWP.</span></span>

| <span data-ttu-id="c62a1-269">名前</span><span class="sxs-lookup"><span data-stu-id="c62a1-269">Name</span></span>           | <span data-ttu-id="c62a1-270">種類</span><span class="sxs-lookup"><span data-stu-id="c62a1-270">Type</span></span>                 | <span data-ttu-id="c62a1-271">説明</span><span class="sxs-lookup"><span data-stu-id="c62a1-271">Description</span></span>                                                                            |
|----------------|----------------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="c62a1-272">タップ</span><span class="sxs-lookup"><span data-stu-id="c62a1-272">Tap</span></span>            | <span data-ttu-id="c62a1-273">静的ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="c62a1-273">Static gesture</span></span>       | <span data-ttu-id="c62a1-274">1 本の指で画面をタッチし、その指を上げます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-274">One finger touches the screen and lifts up.</span></span>                                            |
| <span data-ttu-id="c62a1-275">長押し</span><span class="sxs-lookup"><span data-stu-id="c62a1-275">Press and hold</span></span> | <span data-ttu-id="c62a1-276">静的ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="c62a1-276">Static gesture</span></span>       | <span data-ttu-id="c62a1-277">1 本の指で画面をタッチし、そのまま押し続けます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-277">One finger touches the screen and stays in place.</span></span>                                      |
| <span data-ttu-id="c62a1-278">スライド</span><span class="sxs-lookup"><span data-stu-id="c62a1-278">Slide</span></span>          | <span data-ttu-id="c62a1-279">操作ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="c62a1-279">Manipulation gesture</span></span> | <span data-ttu-id="c62a1-280">1 本または複数の指で画面をタッチし、同じ方向に動かします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-280">One or more fingers touch the screen and move in the same direction.</span></span>                   |
| <span data-ttu-id="c62a1-281">スワイプ</span><span class="sxs-lookup"><span data-stu-id="c62a1-281">Swipe</span></span>          | <span data-ttu-id="c62a1-282">操作ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="c62a1-282">Manipulation gesture</span></span> | <span data-ttu-id="c62a1-283">1 本または複数の指で画面をタッチし、同じ方向に少しだけ動かします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-283">One or more fingers touch the screen and move a short distance in the same direction.</span></span>  |
| <span data-ttu-id="c62a1-284">回転</span><span class="sxs-lookup"><span data-stu-id="c62a1-284">Turn</span></span>           | <span data-ttu-id="c62a1-285">操作ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="c62a1-285">Manipulation gesture</span></span> | <span data-ttu-id="c62a1-286">2 本以上の指で画面をタッチし、時計回りまたは反時計回りに動かします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-286">Two or more fingers touch the screen and move in a clockwise or counter-clockwise arc.</span></span> |
| <span data-ttu-id="c62a1-287">ピンチ</span><span class="sxs-lookup"><span data-stu-id="c62a1-287">Pinch</span></span>          | <span data-ttu-id="c62a1-288">操作ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="c62a1-288">Manipulation gesture</span></span> | <span data-ttu-id="c62a1-289">2 本以上の指で画面をタッチし、それらの指を近づけていきます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-289">Two or more fingers touch the screen and move closer together.</span></span>                         |
| <span data-ttu-id="c62a1-290">ストレッチ</span><span class="sxs-lookup"><span data-stu-id="c62a1-290">Stretch</span></span>        | <span data-ttu-id="c62a1-291">操作ジェスチャ</span><span class="sxs-lookup"><span data-stu-id="c62a1-291">Manipulation gesture</span></span> | <span data-ttu-id="c62a1-292">2 本以上の指で画面をタッチし、それらの指を離していきます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-292">Two or more fingers touch the screen and move farther apart.</span></span>                           |

 

<!-- mijacobs: Removing for now. We don't have a real page to link to yet. 
For more info about gestures, manipulations, and interactions, see [Custom user interactions](custom-user-input-portal.md).
-->

## <a name="gesture-events"></a><span data-ttu-id="c62a1-293">ジェスチャ イベント</span><span class="sxs-lookup"><span data-stu-id="c62a1-293">Gesture events</span></span>


<span data-ttu-id="c62a1-294">個々のコントロールについて詳しくは、「[コントロールの一覧](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-294">For details about individual controls, see [Controls list](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/).</span></span>

## <a name="pointer-events"></a><span data-ttu-id="c62a1-295">ポインター イベント</span><span class="sxs-lookup"><span data-stu-id="c62a1-295">Pointer events</span></span>


<span data-ttu-id="c62a1-296">ポインター イベントは、タッチ、タッチパッド、ペン、マウスなど、さまざまなアクティブな入力ソースによって生成されます (従来のマウス イベントに代わるものです)。</span><span class="sxs-lookup"><span data-stu-id="c62a1-296">Pointer events are raised by a variety of active input sources, including touch, touchpad, pen, and mouse (they replace traditional mouse events.)</span></span>

<span data-ttu-id="c62a1-297">ポインター イベントは、単一の入力ポイント (指、ペンの先端、マウス カーソル) に基づき、速度ベースの操作をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="c62a1-297">Pointer events are based on a single input point (finger, pen tip, mouse cursor) and do not support velocity-based interactions.</span></span>

<span data-ttu-id="c62a1-298">ポインター イベントと、関連するイベント引数の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-298">Here is a list of pointer events and their related event argument.</span></span>

| <span data-ttu-id="c62a1-299">イベント/クラス</span><span class="sxs-lookup"><span data-stu-id="c62a1-299">Event or class</span></span>                                                       | <span data-ttu-id="c62a1-300">説明</span><span class="sxs-lookup"><span data-stu-id="c62a1-300">Description</span></span>                                                   |
|----------------------------------------------------------------------|---------------------------------------------------------------|
| [<span data-ttu-id="c62a1-301">**PointerPressed**</span><span class="sxs-lookup"><span data-stu-id="c62a1-301">**PointerPressed**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed)             | <span data-ttu-id="c62a1-302">1 本の指で画面をタッチしたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-302">Occurs when a single finger touches the screen.</span></span>               |
| [<span data-ttu-id="c62a1-303">**PointerReleased**</span><span class="sxs-lookup"><span data-stu-id="c62a1-303">**PointerReleased**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerreleased)           | <span data-ttu-id="c62a1-304">その同じタッチによる接触が離れたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-304">Occurs when that same touch contact is lifted.</span></span>                |
| [<span data-ttu-id="c62a1-305">**PointerMoved**</span><span class="sxs-lookup"><span data-stu-id="c62a1-305">**PointerMoved**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointermoved)                 | <span data-ttu-id="c62a1-306">画面上でポインターがドラッグされたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-306">Occurs when the pointer is dragged across the screen.</span></span>         |
| [<span data-ttu-id="c62a1-307">**PointerEntered**</span><span class="sxs-lookup"><span data-stu-id="c62a1-307">**PointerEntered**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerentered)             | <span data-ttu-id="c62a1-308">ポインターが要素のヒット テスト領域内に入ったときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-308">Occurs when a pointer enters the hit test area of an element.</span></span> |
| [<span data-ttu-id="c62a1-309">**PointerExited**</span><span class="sxs-lookup"><span data-stu-id="c62a1-309">**PointerExited**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerexited)               | <span data-ttu-id="c62a1-310">ポインターが要素のヒット テスト領域から出たときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-310">Occurs when a pointer exits the hit test area of an element.</span></span>  |
| [<span data-ttu-id="c62a1-311">**PointerCanceled**</span><span class="sxs-lookup"><span data-stu-id="c62a1-311">**PointerCanceled**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointercanceled)           | <span data-ttu-id="c62a1-312">タッチによる接触が異常に失われたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-312">Occurs when a touch contact is abnormally lost.</span></span>               |
| [<span data-ttu-id="c62a1-313">**PointerCaptureLost**</span><span class="sxs-lookup"><span data-stu-id="c62a1-313">**PointerCaptureLost**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointercapturelost)     | <span data-ttu-id="c62a1-314">別の要素でポインター キャプチャが行われたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-314">Occurs when a pointer capture is taken by another element.</span></span>    |
| [<span data-ttu-id="c62a1-315">**PointerWheelChanged**</span><span class="sxs-lookup"><span data-stu-id="c62a1-315">**PointerWheelChanged**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerwheelchanged)   | <span data-ttu-id="c62a1-316">マウス ホイールのデルタ値が変化すると発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-316">Occurs when the delta value of a mouse wheel changes.</span></span>         |
| [<span data-ttu-id="c62a1-317">**PointerRoutedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="c62a1-317">**PointerRoutedEventArgs**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.PointerRoutedEventArgs) | <span data-ttu-id="c62a1-318">すべてのポインター イベントのデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-318">Provides data for all pointer events.</span></span>                         |

 

<span data-ttu-id="c62a1-319">次の例に、[**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed)、[**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerreleased)、[**PointerExited**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerexited) の各イベントを使って [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) オブジェクトに対するタップ操作を処理する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-319">The following example shows how to use the [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed), [**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerreleased), and [**PointerExited**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerexited) events to handle a tap interaction on a [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) object.</span></span>

<span data-ttu-id="c62a1-320">最初に、XAML (Extensible Application Markup Language) で、`touchRectangle` という名前の [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) コントロールが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-320">First, a [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) named `touchRectangle` is created in Extensible Application Markup Language (XAML).</span></span>

```XAML
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Rectangle Name="touchRectangle"
           Height="100" Width="200" Fill="Blue" />
</Grid>
```
<span data-ttu-id="c62a1-321">次に、[**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed)、[**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerreleased)、[**PointerExited**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerexited) の各イベントのリスナーが指定されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-321">Next, listeners for the [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed), [**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerreleased), and [**PointerExited**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerexited) events are specified.</span></span>

```cpp
MainPage::MainPage()
{
    InitializeComponent();

    // Pointer event listeners.
    touchRectangle->PointerPressed += ref new PointerEventHandler(this, &MainPage::touchRectangle_PointerPressed);
    touchRectangle->PointerReleased += ref new PointerEventHandler(this, &MainPage::touchRectangle_PointerReleased);
    touchRectangle->PointerExited += ref new PointerEventHandler(this, &MainPage::touchRectangle_PointerExited);
}
```

```cs
public MainPage()
{
    this.InitializeComponent();

    // Pointer event listeners.
    touchRectangle.PointerPressed += touchRectangle_PointerPressed;
    touchRectangle.PointerReleased += touchRectangle_PointerReleased;
    touchRectangle.PointerExited += touchRectangle_PointerExited;
}
```

```vb
Public Sub New()

    ' This call is required by the designer.
    InitializeComponent()

    ' Pointer event listeners.
    AddHandler touchRectangle.PointerPressed, AddressOf touchRectangle_PointerPressed
    AddHandler touchRectangle.PointerReleased, AddressOf Me.touchRectangle_PointerReleased
    AddHandler touchRectangle.PointerExited, AddressOf touchRectangle_PointerExited

End Sub
```

<span data-ttu-id="c62a1-322">最後に、[**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed) イベント ハンドラーが [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) の [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) と [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) を大きくし、[**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerreleased) と [**PointerExited**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerexited) の各イベント ハンドラーは **Height** と **Width** を開始値に戻します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-322">Finally, the [**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed) event handler increases the [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) and [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) of the [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle), while the [**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerreleased) and [**PointerExited**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerexited) event handlers set the **Height** and **Width** back to their starting values.</span></span>

```cpp
// Handler for pointer exited event.
void MainPage::touchRectangle_PointerExited(Object^ sender, PointerRoutedEventArgs^ e)
{
    Rectangle^ rect = (Rectangle^)sender;

    // Pointer moved outside Rectangle hit test area.
    // Reset the dimensions of the Rectangle.
    if (nullptr != rect)
    {
        rect->Width = 200;
        rect->Height = 100;
    }
}

// Handler for pointer released event.
void MainPage::touchRectangle_PointerReleased(Object^ sender, PointerRoutedEventArgs^ e)
{
    Rectangle^ rect = (Rectangle^)sender;

    // Reset the dimensions of the Rectangle.
    if (nullptr != rect)
    {
        rect->Width = 200;
        rect->Height = 100;
    }
}

// Handler for pointer pressed event.
void MainPage::touchRectangle_PointerPressed(Object^ sender, PointerRoutedEventArgs^ e)
{
    Rectangle^ rect = (Rectangle^)sender;

    // Change the dimensions of the Rectangle.
    if (nullptr != rect)
    {
        rect->Width = 250;
        rect->Height = 150;
    }
}
```

```cs
// Handler for pointer exited event.
private void touchRectangle_PointerExited(object sender, PointerRoutedEventArgs e)
{
    Rectangle rect = sender as Rectangle;

    // Pointer moved outside Rectangle hit test area.
    // Reset the dimensions of the Rectangle.
    if (null != rect)
    {
        rect.Width = 200;
        rect.Height = 100;
    }
}
// Handler for pointer released event.
private void touchRectangle_PointerReleased(object sender, PointerRoutedEventArgs e)
{
    Rectangle rect = sender as Rectangle;

    // Reset the dimensions of the Rectangle.
    if (null != rect)
    {
        rect.Width = 200;
        rect.Height = 100;
    }
}

// Handler for pointer pressed event.
private void touchRectangle_PointerPressed(object sender, PointerRoutedEventArgs e)
{
    Rectangle rect = sender as Rectangle;

    // Change the dimensions of the Rectangle.
    if (null != rect)
    {
        rect.Width = 250;
        rect.Height = 150;
    }
}
```

```vb
' Handler for pointer exited event.
Private Sub touchRectangle_PointerExited(sender As Object, e As PointerRoutedEventArgs)
    Dim rect As Rectangle = CType(sender, Rectangle)

    ' Pointer moved outside Rectangle hit test area.
    ' Reset the dimensions of the Rectangle.
    If (rect IsNot Nothing) Then
        rect.Width = 200
        rect.Height = 100
    End If
End Sub

' Handler for pointer released event.
Private Sub touchRectangle_PointerReleased(sender As Object, e As PointerRoutedEventArgs)
    Dim rect As Rectangle = CType(sender, Rectangle)

    ' Reset the dimensions of the Rectangle.
    If (rect IsNot Nothing) Then
        rect.Width = 200
        rect.Height = 100
    End If
End Sub

' Handler for pointer pressed event.
Private Sub touchRectangle_PointerPressed(sender As Object, e As PointerRoutedEventArgs)
    Dim rect As Rectangle = CType(sender, Rectangle)

    ' Change the dimensions of the Rectangle.
    If (rect IsNot Nothing) Then
        rect.Width = 250
        rect.Height = 150
    End If
End Sub
```

## <a name="manipulation-events"></a><span data-ttu-id="c62a1-323">操作イベント</span><span class="sxs-lookup"><span data-stu-id="c62a1-323">Manipulation events</span></span>


<span data-ttu-id="c62a1-324">アプリで複数の指を使った操作や速度データを必要とする操作をサポートする必要がある場合は、操作イベントを使います。</span><span class="sxs-lookup"><span data-stu-id="c62a1-324">Use manipulation events if you need to support multiple finger interactions in your app, or interactions that require velocity data.</span></span>

<span data-ttu-id="c62a1-325">操作イベントを使うと、ドラッグ、ズーム、長押しなどの操作を検出できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-325">You can use manipulation events to detect interactions such as drag, zoom, and hold.</span></span>

<span data-ttu-id="c62a1-326">操作イベントと、関連するイベント引数の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-326">Here is a list of manipulation events and related event arguments.</span></span>

| <span data-ttu-id="c62a1-327">イベント/クラス</span><span class="sxs-lookup"><span data-stu-id="c62a1-327">Event or class</span></span>                                                                                               | <span data-ttu-id="c62a1-328">説明</span><span class="sxs-lookup"><span data-stu-id="c62a1-328">Description</span></span>                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="c62a1-329">**ManipulationStarting イベント**</span><span class="sxs-lookup"><span data-stu-id="c62a1-329">**ManipulationStarting event**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarting)                                   | <span data-ttu-id="c62a1-330">操作プロセッサが最初に作成されると発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-330">Occurs when the manipulation processor is first created.</span></span>                                                                                  |
| [<span data-ttu-id="c62a1-331">**ManipulationStarted イベント**</span><span class="sxs-lookup"><span data-stu-id="c62a1-331">**ManipulationStarted event**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarted)                                     | <span data-ttu-id="c62a1-332">入力デバイスが [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) に対する操作を開始すると発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-332">Occurs when an input device begins a manipulation on the [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement).</span></span>                                            |
| [<span data-ttu-id="c62a1-333">**ManipulationDelta イベント**</span><span class="sxs-lookup"><span data-stu-id="c62a1-333">**ManipulationDelta event**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta)                                         | <span data-ttu-id="c62a1-334">入力デバイスが操作中に位置を変更すると発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-334">Occurs when the input device changes position during a manipulation.</span></span>                                                                      |
| [<span data-ttu-id="c62a1-335">**ManipulationInertiaStarting イベント**</span><span class="sxs-lookup"><span data-stu-id="c62a1-335">**ManipulationInertiaStarting event**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationinertiastartingevent)                | <span data-ttu-id="c62a1-336">操作中に入力デバイスが [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) オブジェクトとのコンタクトを失ったときと慣性が開始したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-336">Occurs when the input device loses contact with the [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) object during a manipulation and inertia begins.</span></span> |
| [<span data-ttu-id="c62a1-337">**ManipulationCompleted イベント**</span><span class="sxs-lookup"><span data-stu-id="c62a1-337">**ManipulationCompleted event**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationcompleted)                                 | <span data-ttu-id="c62a1-338">[  **UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) に対する操作と慣性が完了すると発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-338">Occurs when a manipulation and inertia on the [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) are complete.</span></span>                                          |
| [<span data-ttu-id="c62a1-339">**ManipulationStartingRoutedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="c62a1-339">**ManipulationStartingRoutedEventArgs**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.ManipulationStartingRoutedEventArgs)               | <span data-ttu-id="c62a1-340">[  **ManipulationStarting**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarting) イベントのデータを指定します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-340">Provides data for the [**ManipulationStarting**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarting) event.</span></span>                                         |
| [<span data-ttu-id="c62a1-341">**ManipulationStartedRoutedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="c62a1-341">**ManipulationStartedRoutedEventArgs**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.ManipulationStartedRoutedEventArgs)                 | <span data-ttu-id="c62a1-342">[  **ManipulationStarted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarted) イベントのデータを指定します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-342">Provides data for the [**ManipulationStarted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarted) event.</span></span>                                           |
| [<span data-ttu-id="c62a1-343">**ManipulationDeltaRoutedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="c62a1-343">**ManipulationDeltaRoutedEventArgs**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.ManipulationDeltaRoutedEventArgs)                     | <span data-ttu-id="c62a1-344">[  **ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) イベントのデータを指定します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-344">Provides data for the [**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) event.</span></span>                                               |
| [<span data-ttu-id="c62a1-345">**ManipulationInertiaStartingRoutedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="c62a1-345">**ManipulationInertiaStartingRoutedEventArgs**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.ManipulationInertiaStartingRoutedEventArgs) | <span data-ttu-id="c62a1-346">[  **ManipulationInertiaStarting**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationinertiastarting) イベントのデータを指定します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-346">Provides data for the [**ManipulationInertiaStarting**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationinertiastarting) event.</span></span>                           |
| [<span data-ttu-id="c62a1-347">**ManipulationVelocities**</span><span class="sxs-lookup"><span data-stu-id="c62a1-347">**ManipulationVelocities**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Input.ManipulationVelocities)                                              | <span data-ttu-id="c62a1-348">操作の実行速度を指定します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-348">Describes the speed at which manipulations occur.</span></span>                                                                                         |
| [<span data-ttu-id="c62a1-349">**ManipulationCompletedRoutedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="c62a1-349">**ManipulationCompletedRoutedEventArgs**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.ManipulationCompletedRoutedEventArgs)             | <span data-ttu-id="c62a1-350">[  **ManipulationCompleted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationcompleted) イベントのデータを指定します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-350">Provides data for the [**ManipulationCompleted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationcompleted) event.</span></span>                                       |

 

<span data-ttu-id="c62a1-351">ジェスチャは、一連の操作イベントで構成されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-351">A gesture consists of a series of manipulation events.</span></span> <span data-ttu-id="c62a1-352">ユーザーが画面をタッチしたときなど、各ジェスチャは [**ManipulationStarted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarted) イベントから始まります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-352">Each gesture starts with a [**ManipulationStarted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationstarted) event, such as when a user touches the screen.</span></span>

<span data-ttu-id="c62a1-353">次に、1 つ以上の [**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) イベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-353">Next, one or more [**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) events are fired.</span></span> <span data-ttu-id="c62a1-354">たとえば、画面をタッチして画面上で指をドラッグした場合です。</span><span class="sxs-lookup"><span data-stu-id="c62a1-354">For example, if you touch the screen and then drag your finger across the screen.</span></span> <span data-ttu-id="c62a1-355">最後に、対話的操作が完了すると [**ManipulationCompleted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationcompleted) イベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-355">Finally, a [**ManipulationCompleted**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationcompleted) event is raised when the interaction finishes.</span></span>

<span data-ttu-id="c62a1-356">**注**  タッチ スクリーン モニターを持っていない場合は、マウスとマウス ホイールのインターフェイスを使用してシミュレーター内で操作イベント コードをテストできます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-356">**Note**  If you don't have a touch-screen monitor, you can test your manipulation event code in the simulator using a mouse and mouse wheel interface.</span></span>

 

<span data-ttu-id="c62a1-357">次の例に、[**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) イベントを使って、[**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) に対するスライド操作を処理し、画面上でオブジェクトを移動する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-357">The following example shows how to use the [**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) events to handle a slide interaction on a [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) and move it across the screen.</span></span>

<span data-ttu-id="c62a1-358">まず、XAML で [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) と [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) が 200 の `touchRectangle` という名前の [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) を作成します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-358">First, a [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) named `touchRectangle` is created in XAML with a [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) and [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) of 200.</span></span>

```XAML
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Rectangle Name="touchRectangle"
               Width="200" Height="200" Fill="Blue" 
               ManipulationMode="All"/>
</Grid>
```

<span data-ttu-id="c62a1-359">次に、[**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) を移動するための `dragTranslation` という名前のグローバルな [**TranslateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) を作成します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-359">Next, a global [**TranslateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) named `dragTranslation` is created for translating the [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle).</span></span> <span data-ttu-id="c62a1-360">[  **Rectangle** で **ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) イベント リスナーが指定され、`dragTranslation` が [**Rectangle** の **RenderTransform**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.rendertransform) に追加されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-360">A [**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) event listener is specified on the **Rectangle**, and `dragTranslation` is added to the [**RenderTransform**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.rendertransform) of the **Rectangle**.</span></span>

```cpp
// Global translation transform used for changing the position of 
// the Rectangle based on input data from the touch contact.
Windows::UI::Xaml::Media::TranslateTransform^ dragTranslation;
```

```cs
// Global translation transform used for changing the position of 
// the Rectangle based on input data from the touch contact.
private TranslateTransform dragTranslation;
```

```vb
' Global translation transform used for changing the position of 
' the Rectangle based on input data from the touch contact.
Private dragTranslation As TranslateTransform
```

```cpp
MainPage::MainPage()
{
    InitializeComponent();

    // Listener for the ManipulationDelta event.
    touchRectangle->ManipulationDelta += 
        ref new ManipulationDeltaEventHandler(
            this, 
            &MainPage::touchRectangle_ManipulationDelta);
    // New translation transform populated in 
    // the ManipulationDelta handler.
    dragTranslation = ref new TranslateTransform();
    // Apply the translation to the Rectangle.
    touchRectangle->RenderTransform = dragTranslation;
}
```

```cs
public MainPage()
{
    this.InitializeComponent();

    // Listener for the ManipulationDelta event.
    touchRectangle.ManipulationDelta += touchRectangle_ManipulationDelta;
    // New translation transform populated in 
    // the ManipulationDelta handler.
    dragTranslation = new TranslateTransform();
    // Apply the translation to the Rectangle.
    touchRectangle.RenderTransform = this.dragTranslation;
}
```

```vb
Public Sub New()

    ' This call is required by the designer.
    InitializeComponent()

    ' Listener for the ManipulationDelta event.
    AddHandler touchRectangle.ManipulationDelta,
        AddressOf testRectangle_ManipulationDelta
    ' New translation transform populated in 
    ' the ManipulationDelta handler.
    dragTranslation = New TranslateTransform()
    ' Apply the translation to the Rectangle.
    touchRectangle.RenderTransform = dragTranslation

End Sub
```

<span data-ttu-id="c62a1-361">最後に、[**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) イベント ハンドラーで、[**TranslateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) を [**Delta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.input.manipulationdeltaroutedeventargs.delta) プロパティで使って [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) の位置を更新します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-361">Finally, in the [**ManipulationDelta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.manipulationdelta) event handler, the position of the [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) is updated by using the [**TranslateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) on the [**Delta**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.input.manipulationdeltaroutedeventargs.delta) property.</span></span>

```cpp
// Handler for the ManipulationDelta event.
// ManipulationDelta data is loaded into the
// translation transform and applied to the Rectangle.
void MainPage::touchRectangle_ManipulationDelta(Object^ sender,
    ManipulationDeltaRoutedEventArgs^ e)
{
    // Move the rectangle.
    dragTranslation->X += e->Delta.Translation.X;
    dragTranslation->Y += e->Delta.Translation.Y;
    
}
```

```cs
// Handler for the ManipulationDelta event.
// ManipulationDelta data is loaded into the
// translation transform and applied to the Rectangle.
void touchRectangle_ManipulationDelta(object sender,
    ManipulationDeltaRoutedEventArgs e)
{
    // Move the rectangle.
    dragTranslation.X += e.Delta.Translation.X;
    dragTranslation.Y += e.Delta.Translation.Y;
}
```

```vb
' Handler for the ManipulationDelta event.
' ManipulationDelta data Is loaded into the
' translation transform And applied to the Rectangle.
Private Sub testRectangle_ManipulationDelta(
    sender As Object,
    e As ManipulationDeltaRoutedEventArgs)

    ' Move the rectangle.
    dragTranslation.X = (dragTranslation.X + e.Delta.Translation.X)
    dragTranslation.Y = (dragTranslation.Y + e.Delta.Translation.Y)

End Sub
```

## <a name="routed-events"></a><span data-ttu-id="c62a1-362">ルーティング イベント</span><span class="sxs-lookup"><span data-stu-id="c62a1-362">Routed events</span></span>


<span data-ttu-id="c62a1-363">ここに記載されたポインター イベント、ジェスチャ イベント、操作イベントはすべて、*ルーティング イベント*として実装されます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-363">All of the pointer events, gesture events and manipulation events mentioned here are implemented as *routed events*.</span></span> <span data-ttu-id="c62a1-364">つまりこのイベントは、最初にイベントを発生したオブジェクト以外のオブジェクトによって処理される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c62a1-364">This means that the event can potentially be handled by objects other than the one that originally raised the event.</span></span> <span data-ttu-id="c62a1-365">[  **UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) の親コンテナーや、アプリのルート [**Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) などのオブジェクト ツリーの一連の親は、元の要素が存在しなくても、これらのイベントを処理することを選択できます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-365">Successive parents in an object tree, such as the parent containers of a [**UIElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) or the root [**Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) of your app, can choose to handle these events even if the original element does not.</span></span> <span data-ttu-id="c62a1-366">逆に、イベントを処理するどのオブジェクトも、親要素に達しないように、処理済みイベントをマークできます。</span><span class="sxs-lookup"><span data-stu-id="c62a1-366">Conversely, any object that does handle the event can mark the event handled so that it no longer reaches any parent element.</span></span> <span data-ttu-id="c62a1-367">ルーティング イベントの概念について、およびそれがルーティング イベントのハンドラーの記述方法にどのように影響するかについて詳しくは、「[イベントとルーティング イベントの概要](https://docs.microsoft.com/previous-versions/windows/apps/hh758286(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c62a1-367">For more info about the routed event concept and how it affects how you write handlers for routed events, see [Events and routed events overview](https://docs.microsoft.com/previous-versions/windows/apps/hh758286(v=win.10)).</span></span>

## <a name="dos-and-donts"></a><span data-ttu-id="c62a1-368">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="c62a1-368">Dos and don'ts</span></span>


-   <span data-ttu-id="c62a1-369">期待される主な入力方法としてタッチ操作を使うアプリを設計します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-369">Design applications with touch interaction as the primary expected input method.</span></span>
-   <span data-ttu-id="c62a1-370">あらゆる種類 (タッチ、ペン、スタイラス、マウスなど) の操作に対する視覚的なフィードバックを提供します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-370">Provide visual feedback for interactions of all types (touch, pen, stylus, mouse, etc.)</span></span>
-   <span data-ttu-id="c62a1-371">タッチ ターゲットのサイズ、接触形状、スクラブ、揺らす操作を調整してターゲット設定を最適化します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-371">Optimize targeting by adjusting touch target size, contact geometry, scrubbing and rocking.</span></span>
-   <span data-ttu-id="c62a1-372">スナップ位置と方向 "レール" を使って精度を最適化します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-372">Optimize accuracy through the use of snap points and directional "rails".</span></span>
-   <span data-ttu-id="c62a1-373">密集した UI 項目のタッチの精度を高めるためにヒントとハンドルを用意します。</span><span class="sxs-lookup"><span data-stu-id="c62a1-373">Provide tooltips and handles to help improve touch accuracy for tightly packed UI items.</span></span>
-   <span data-ttu-id="c62a1-374">できるだけ時間制限のある操作を使わないようにします (適切な使用例: 長押し)。</span><span class="sxs-lookup"><span data-stu-id="c62a1-374">Don't use timed interactions whenever possible (example of appropriate use: touch and hold).</span></span>
-   <span data-ttu-id="c62a1-375">できる限り、操作の区別に使われた数の指は使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="c62a1-375">Don't use the number of fingers used to distinguish the manipulation whenever possible.</span></span>


## <a name="related-articles"></a><span data-ttu-id="c62a1-376">関連記事</span><span class="sxs-lookup"><span data-stu-id="c62a1-376">Related articles</span></span>

* [<span data-ttu-id="c62a1-377">ポインター入力の処理</span><span class="sxs-lookup"><span data-stu-id="c62a1-377">Handle pointer input</span></span>](handle-pointer-input.md)
* [<span data-ttu-id="c62a1-378">入力デバイスの識別</span><span class="sxs-lookup"><span data-stu-id="c62a1-378">Identify input devices</span></span>](identify-input-devices.md)

<span data-ttu-id="c62a1-379">**サンプル**</span><span class="sxs-lookup"><span data-stu-id="c62a1-379">**Samples**</span></span>

* [<span data-ttu-id="c62a1-380">基本的な入力サンプル</span><span class="sxs-lookup"><span data-stu-id="c62a1-380">Basic input sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620302)
* [<span data-ttu-id="c62a1-381">低待機時間の入力サンプル</span><span class="sxs-lookup"><span data-stu-id="c62a1-381">Low latency input sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620304)
* [<span data-ttu-id="c62a1-382">ユーザー操作モードのサンプル</span><span class="sxs-lookup"><span data-stu-id="c62a1-382">User interaction mode sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=619894)
* [<span data-ttu-id="c62a1-383">フォーカスの視覚効果のサンプル</span><span class="sxs-lookup"><span data-stu-id="c62a1-383">Focus visuals sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=619895)

<span data-ttu-id="c62a1-384">**サンプルのアーカイブ**</span><span class="sxs-lookup"><span data-stu-id="c62a1-384">**Archive Samples**</span></span>

* [<span data-ttu-id="c62a1-385">入力:デバイス機能のサンプル</span><span class="sxs-lookup"><span data-stu-id="c62a1-385">Input: Device capabilities sample</span></span>](https://go.microsoft.com/fwlink/p/?linkid=231530)
* [<span data-ttu-id="c62a1-386">入力:XAML ユーザー入力イベントのサンプル</span><span class="sxs-lookup"><span data-stu-id="c62a1-386">Input: XAML user input events sample</span></span>](https://go.microsoft.com/fwlink/p/?linkid=226855)
* [<span data-ttu-id="c62a1-387">XAML のスクロール、パン、ズームのサンプル</span><span class="sxs-lookup"><span data-stu-id="c62a1-387">XAML scrolling, panning, and zooming sample</span></span>](https://go.microsoft.com/fwlink/p/?linkid=251717)
* [<span data-ttu-id="c62a1-388">入力:ジェスチャと GestureRecognizer の操作</span><span class="sxs-lookup"><span data-stu-id="c62a1-388">Input: Gestures and manipulations with GestureRecognizer</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=231605)
 

 




