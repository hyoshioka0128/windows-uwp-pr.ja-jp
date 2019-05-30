---
Description: ユニバーサル Windows プラットフォーム (UWP) アプリのナビゲーションは、ナビゲーション構造、ナビゲーション要素、システム レベルの機能から成る柔軟なモデルに基づいています。
title: UWP アプリのナビゲーションの基本
ms.assetid: B65D33BA-AAFE-434D-B6D5-1A0C49F59664
label: Navigation design basics
template: detail.hbs
op-migration-status: ready
ms.date: 07/16/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 1c764eeb57ec8046a93e7fb58e156fa68daea8df
ms.sourcegitcommit: 13fe5d04bdb43c75d0fc4de18c2c3d4ae58ff982
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "64564525"
---
# <a name="navigation-design-basics-for-uwp-apps"></a><span data-ttu-id="9070e-104">UWP アプリのナビゲーション デザインの基本</span><span class="sxs-lookup"><span data-stu-id="9070e-104">Navigation design basics for UWP apps</span></span>

![ナビゲーションの基本のヘッダー](images/nav/navigation-basics-header.jpg)

<span data-ttu-id="9070e-106">アプリをページの集まりと考えると、*ナビゲーション*は、ページ間およびページ内を移動する動作を表します。</span><span class="sxs-lookup"><span data-stu-id="9070e-106">If you think of an app as a collection of pages, *navigation* describes the act of moving between pages and within a page.</span></span> <span data-ttu-id="9070e-107">これはユーザー エクスペリエンスの出発点です。これによって、ユーザーは利用するコンテンツと機能を見つけます。</span><span class="sxs-lookup"><span data-stu-id="9070e-107">It's the starting point of the user experience, and it's how users find the content and features they're interested in.</span></span> <span data-ttu-id="9070e-108">これは非常に重要ですが、適切な設計が難しい場合もあります。</span><span class="sxs-lookup"><span data-stu-id="9070e-108">It's very important, and it can be difficult to get right.</span></span>

<span data-ttu-id="9070e-109">ナビゲーションに関して行うことができる膨大な数の選択肢があります。</span><span class="sxs-lookup"><span data-stu-id="9070e-109">We have a huge number of choices to make for navigation.</span></span> <span data-ttu-id="9070e-110">以下を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="9070e-110">We could:</span></span>

:::row:::
    :::column:::
        ![navigation example 1](images/nav/nav-1.svg)

<span data-ttu-id="9070e-111">ユーザーは、一連の順序でページを経由する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9070e-111">Require users to go through a series of pages in order.</span></span>
    :::column-end:::
    :::column:::
        ![navigation example 2](images/nav/nav-2.svg)

<span data-ttu-id="9070e-112">ユーザーが任意のページに直接ジャンプできるメニューを提供します。</span><span class="sxs-lookup"><span data-stu-id="9070e-112">Provide a menu that allows users to jump directly to any page.</span></span>
    :::column-end:::
    :::column:::
        ![navigation example 3](images/nav/nav-3.svg)

<span data-ttu-id="9070e-113">すべてを 1 ページに配置し、コンテンツを表示するためのフィルター処理メカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="9070e-113">Place everything on a single page and provide filtering mechanisms for viewing content.</span></span>
    :::column-end:::
:::row-end:::

<span data-ttu-id="9070e-114">1 つのナビゲーション デザインですべてのアプリに対応することはできませんが、アプリの適切な設計を判断するための原則やガイドラインがあります。</span><span class="sxs-lookup"><span data-stu-id="9070e-114">While there's no single navigation design that works for every app, there are principles and guidelines to help you decide the right design for your app.</span></span>

## <a name="principles-of-good-navigation"></a><span data-ttu-id="9070e-115">優れたナビゲーションの原則</span><span class="sxs-lookup"><span data-stu-id="9070e-115">Principles of good navigation</span></span>

<span data-ttu-id="9070e-116">優れたナビゲーション デザインの基本原則から始めましょう。</span><span class="sxs-lookup"><span data-stu-id="9070e-116">Let's start with the basic principles of good navigation design:</span></span>

- <span data-ttu-id="9070e-117">**整合性:** ユーザーの期待を満たします。</span><span class="sxs-lookup"><span data-stu-id="9070e-117">**Consistency:** Meet user expectations.</span></span>
- <span data-ttu-id="9070e-118">**わかりやすくするため:** 必要があるよりしません。</span><span class="sxs-lookup"><span data-stu-id="9070e-118">**Simplicity:** Don't do more than you need to.</span></span>
- <span data-ttu-id="9070e-119">**わかりやすくするため:** 明確なパスとオプションを提供します。</span><span class="sxs-lookup"><span data-stu-id="9070e-119">**Clarity:** Provide clear paths and options.</span></span>

### <a name="consistency"></a><span data-ttu-id="9070e-120">一貫性</span><span class="sxs-lookup"><span data-stu-id="9070e-120">Consistency</span></span>

<span data-ttu-id="9070e-121">ナビゲーションは、ユーザーの期待に沿ったものである必要があります。</span><span class="sxs-lookup"><span data-stu-id="9070e-121">Navigation should be consistent with user expectations.</span></span> <span data-ttu-id="9070e-122">使用して[標準コントロール](#use-the-right-controls)ユーザーは、アイコン、場所の標準の規則をよく理解し、次をスタイル設定は行うことナビゲーション予測可能で直感的なユーザー。</span><span class="sxs-lookup"><span data-stu-id="9070e-122">Using [standard controls](#use-the-right-controls) that users are familiar with and following standard conventions for icons, location, and styling will make navigation predictable and intuitive for users.</span></span>

![ページ コンポーネントのイメージ](images/nav/page-components.svg)

> <span data-ttu-id="9070e-124">ユーザーは特定の UI 要素が標準の位置にあることを期待します。</span><span class="sxs-lookup"><span data-stu-id="9070e-124">Users expect to find certain UI elements in standard locations.</span></span>

### <a name="simplicity"></a><span data-ttu-id="9070e-125">シンプルさ</span><span class="sxs-lookup"><span data-stu-id="9070e-125">Simplicity</span></span>

<span data-ttu-id="9070e-126">ナビゲーション項目が少ないほど、ユーザーの意思決定がシンプルになります。</span><span class="sxs-lookup"><span data-stu-id="9070e-126">Fewer navigation items simplify decision making for users.</span></span> <span data-ttu-id="9070e-127">重要な移動先に簡単にアクセスできるようにして、重要度の低い項目を非表示にすることで、ユーザーは目的の場所にすばやく移動できるようになります。</span><span class="sxs-lookup"><span data-stu-id="9070e-127">Providing easy access to important destinations and hiding less important items will help users get where they want, faster.</span></span>

:::row:::
    :::column:::
        ![do example](images/nav/do.svg)

        ![navview good](images/nav/navview-good.svg)

<span data-ttu-id="9070e-128">使い慣れたナビゲーション メニューで、ナビゲーション項目を表示します。</span><span class="sxs-lookup"><span data-stu-id="9070e-128">Present navigation items in a familiar navigation menu.</span></span>
    :::column-end:::
    :::column:::
        ![don't example](images/nav/dont.svg)

        ![navview bad](images/nav/navview-bad.svg)

<span data-ttu-id="9070e-129">多くのナビゲーション オプションを持つユーザーの重荷となってください。</span><span class="sxs-lookup"><span data-stu-id="9070e-129">Overwhelm users with many navigation options.</span></span>
    :::column-end:::
:::row-end:::

### <a name="clarity"></a><span data-ttu-id="9070e-130">明確さ</span><span class="sxs-lookup"><span data-stu-id="9070e-130">Clarity</span></span>

<span data-ttu-id="9070e-131">明確なパスを示すと、ユーザーは論理的なナビゲーションを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="9070e-131">Clear paths allow for logical navigation for users.</span></span> <span data-ttu-id="9070e-132">ナビゲーション オプションをわかりやすくし、ページ間の関係を明確にすることで、ユーザーが自分の位置を見失うことを防止できます。</span><span class="sxs-lookup"><span data-stu-id="9070e-132">Making navigation options obvious and clarifying relationships between pages should prevent users from getting lost.</span></span>

![実行例](images/nav/clarity-image.svg)

> <span data-ttu-id="9070e-134">移動先にはわかりやすいラベルが付けられているため、ユーザーは自分の位置を知ることができます。</span><span class="sxs-lookup"><span data-stu-id="9070e-134">Destinations are clearly labeled so users know where they are.</span></span>

## <a name="general-recommendations"></a><span data-ttu-id="9070e-135">一般的な推奨事項</span><span class="sxs-lookup"><span data-stu-id="9070e-135">General recommendations</span></span>

<span data-ttu-id="9070e-136">一貫性、シンプルさ、明確さという設計原則を念頭に置いて、一般的な推奨事項を作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="9070e-136">Now, let's take our design principles--consistency, simplicity, and clarity--and use them to come up with some general recommendations.</span></span>

1. <span data-ttu-id="9070e-137">ユーザーのことを考えてください。</span><span class="sxs-lookup"><span data-stu-id="9070e-137">Think about your users.</span></span> <span data-ttu-id="9070e-138">アプリ使用時のユーザーの一般的な移動パスを追跡し、ページごとに、ユーザーがそのページを表示している理由と、次にどこに移動しようとしているかを考えてください。</span><span class="sxs-lookup"><span data-stu-id="9070e-138">Trace out typical paths they might take through your app, and for each page, think about why the user is there and where they might want to go.</span></span>

2. <span data-ttu-id="9070e-139">詳細のナビゲーション階層を回避します。</span><span class="sxs-lookup"><span data-stu-id="9070e-139">Avoid deep navigation hierarchies.</span></span> <span data-ttu-id="9070e-140">3 レベルを超えるナビゲーションでは、ユーザーは迷ってしまい、深い階層から抜け出せなくなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9070e-140">If you go beyond three levels of navigation, you risk stranding your user in a deep hierarchy that they will have difficulty leaving.</span></span>

3. <span data-ttu-id="9070e-141">「ホッピング」を避けます。</span><span class="sxs-lookup"><span data-stu-id="9070e-141">Avoid "pogo-sticking."</span></span> <span data-ttu-id="9070e-142">ホッピングとは、関連するコンテンツに移動するために、ユーザーが上のレベルに移動して、それから下のレベルに移動する必要があるナビゲーションを意味します。</span><span class="sxs-lookup"><span data-stu-id="9070e-142">Pogo-sticking occurs when there is related content, but navigating to it requires the user to go up a level and then down again.</span></span>

## <a name="use-the-right-structure"></a><span data-ttu-id="9070e-143">適切な構造を使う</span><span class="sxs-lookup"><span data-stu-id="9070e-143">Use the right structure</span></span>

<span data-ttu-id="9070e-144">ナビゲーションの一般的な原則について説明しました。次に、アプリの構造について考えます。</span><span class="sxs-lookup"><span data-stu-id="9070e-144">Now that you're familiar with general navigation principles, how should you structure your app?</span></span> <span data-ttu-id="9070e-145">2 種類の一般的な構造があります。フラット構造と階層構造です。</span><span class="sxs-lookup"><span data-stu-id="9070e-145">There are two general structures: flat and hierarchal.</span></span>

:::row:::
    :::column:::
        ![Pages arranged in a flat structure](images/nav/flat-lateral-structure.svg)
    :::column-end:::
    :::column span="2":::
        ### Flat/lateral

<span data-ttu-id="9070e-146">フラット構造/水平構造では、ページは横方向に存在します。</span><span class="sxs-lookup"><span data-stu-id="9070e-146">In a flat/lateral structure, pages exist side-by-side.</span></span> <span data-ttu-id="9070e-147">どのような順序でもページ間を移動できます。</span><span class="sxs-lookup"><span data-stu-id="9070e-147">You can go from one page to another in any order.</span></span>

<span data-ttu-id="9070e-148">次のような場合に、フラット構造の使用を推奨します。</span><span class="sxs-lookup"><span data-stu-id="9070e-148">We recommend using a flat structure when:</span></span>

- <span data-ttu-id="9070e-149">ページをどのような順序でも表示できる場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-149">The pages can be viewed in any order.</span></span>
- <span data-ttu-id="9070e-150">各ページはそれぞれ異なるページであり、明確な親/子関係がない場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-150">The pages are clearly distinct from each other and don't have an obvious parent/child relationship.</span></span>
- <span data-ttu-id="9070e-151">グループには、8 未満のページがあります。</span><span class="sxs-lookup"><span data-stu-id="9070e-151">There are less than 8 pages in the group.</span></span> <br>
<span data-ttu-id="9070e-152">(ページ数が 8 ページ以上の場合、ページが一意であるかどうかを判断したり、グループ内の現在の位置を把握したりするのが難しくなる場合があります。</span><span class="sxs-lookup"><span data-stu-id="9070e-152">(When there are more pages, it might be difficult for users to understand how the pages are unique or to understand their current location within the group.</span></span> <span data-ttu-id="9070e-153">このことがアプリでは問題にはならないと考えられる場合は、ページをピアとして作成します。</span><span class="sxs-lookup"><span data-stu-id="9070e-153">If you don't think that's an issue for your app, go ahead and make the pages peers.</span></span> <span data-ttu-id="9070e-154">このことが問題となる可能性がある場合は、階層構造を使って、ページを 2 つ以上の小さなグループに分割することを検討してください。)</span><span class="sxs-lookup"><span data-stu-id="9070e-154">Otherwise, consider using a hierarchical structure to break the pages into two or more smaller groups.)</span></span>

    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        ![Pages arranged in a hierarchy](images/nav/hierarchical-structure.svg)
    :::column-end:::
    :::column span="2":::
        ### Hierarchical

<span data-ttu-id="9070e-155">階層構造では、ページはツリー状の構造に配置されています。</span><span class="sxs-lookup"><span data-stu-id="9070e-155">In a hierarchical structure, pages are organized into a tree-like structure.</span></span> <span data-ttu-id="9070e-156">それぞれの子ページの親は 1 つですが、親ページは 1 つ以上の子ページを持つことができます。</span><span class="sxs-lookup"><span data-stu-id="9070e-156">Each child page has one parent, but a parent can have one or more child pages.</span></span> <span data-ttu-id="9070e-157">子ページにアクセスするには、親ページを経由します。</span><span class="sxs-lookup"><span data-stu-id="9070e-157">To reach a child page, you travel through the parent.</span></span>

<span data-ttu-id="9070e-158">階層構造体は、多数のページにわたる複雑なコンテンツを配置する場合に適してします。</span><span class="sxs-lookup"><span data-stu-id="9070e-158">Hierarchical structures are good for organizing complex content that spans lots of pages.</span></span> <span data-ttu-id="9070e-159">欠点は、ナビゲーションのオーバーヘッドが発生することです。階層が深くなると、ページからページへの移動するために、多くのクリックが必要となります。</span><span class="sxs-lookup"><span data-stu-id="9070e-159">The downside is some navigation overhead: the deeper the structure, the more clicks it takes to get from page to page.</span></span>

<span data-ttu-id="9070e-160">階層をお勧めときに構造体します。</span><span class="sxs-lookup"><span data-stu-id="9070e-160">We recommend a hierarchical structure when:</span></span>
        
- <span data-ttu-id="9070e-161">特定の順序でページを移動する必要がある場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-161">Pages should be traversed in a specific order.</span></span>
- <span data-ttu-id="9070e-162">ページ間に明白な親子関係がある場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-162">There is a clear parent-child relationship between pages.</span></span>
- <span data-ttu-id="9070e-163">グループ内のページ数が 7 ページを超える場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-163">There are more than 7 pages in the group.</span></span>
        
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        ![an app with a hybrid structure](images/nav/combining-structures.svg)
    :::column-end:::
    :::column span="2":::
        ### Combining structures

<span data-ttu-id="9070e-164">1 つの構造または; その他に選択しません。適切に設計の多くのアプリでは、両方を使用します。</span><span class="sxs-lookup"><span data-stu-id="9070e-164">You don't have choose to one structure or the other; many well-design apps use both.</span></span> <span data-ttu-id="9070e-165">アプリでは、トップレベルのページにはフラット構造を使って、任意の順序で参照できるようにし、複雑な関係のあるページには階層構造を使うことができます。</span><span class="sxs-lookup"><span data-stu-id="9070e-165">An app can use flat structures for top-level pages that can be viewed in any order, and hierarchical structures for pages that have more complex relationships.</span></span>

<span data-ttu-id="9070e-166">ナビゲーション構造に複数のレベルがある場合は、現在のサブツリー内のピアにのみリンクするピア ツー ピアのナビゲーション要素を使うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9070e-166">If your navigation structure has multiple levels, we recommend that peer-to-peer navigation elements only link to the peers within their current subtree.</span></span> <span data-ttu-id="9070e-167">2 つのレベルを持つナビゲーション構造を示しています、隣接する図を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="9070e-167">Consider the adjacent illustration, which shows a navigation structure that has two levels:</span></span>

- <span data-ttu-id="9070e-168">レベル 1 では、ピア ツー ピアのナビゲーション要素によって、ページ A、B、C、および D へのアクセスが提供されます。</span><span class="sxs-lookup"><span data-stu-id="9070e-168">At level 1, the peer-to-peer navigation element should provide access to pages A, B, C, and D.</span></span>
- <span data-ttu-id="9070e-169">レベル 2 では、A2 ページのピア ツー ピアのナビゲーション要素は、他の A2 ページにのみリンクしています。</span><span class="sxs-lookup"><span data-stu-id="9070e-169">At level 2, the peer-to-peer navigation elements for the A2 pages should only link to the other A2 pages.</span></span> <span data-ttu-id="9070e-170">これらのナビゲーション要素は、C サブツリー内にあるレベル 2 のページにはリンクしていません。</span><span class="sxs-lookup"><span data-stu-id="9070e-170">They should not link to level 2 pages in the C subtree.</span></span>
    :::column-end:::
:::row-end:::

## <a name="use-the-right-controls"></a><span data-ttu-id="9070e-171">適切なコントロールを使用する</span><span class="sxs-lookup"><span data-stu-id="9070e-171">Use the right controls</span></span>

<span data-ttu-id="9070e-172">ページの構造を決定したら、ユーザーがページ間をどのように移動するかを決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9070e-172">Once you've decided on a page structure, you need to decide how users navigate through those pages.</span></span> <span data-ttu-id="9070e-173">UWP にはさまざまなナビゲーション コントロールが用意されていて、アプリで一貫性があり信頼性が高いナビゲーション エクスペリエンスを提供するために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="9070e-173">UWP provides a variety of navigation controls to help ensure a consistent, reliable navigation experience in your app.</span></span>

:::row:::
    :::column:::
        ![Frame image](images/nav/thumbnail-frame.svg)
    :::column-end:::
    :::column span="2":::
        [**Frame**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame)

<span data-ttu-id="9070e-174">少数の例外を除き、複数のページがあるアプリではフレームを使用します。</span><span class="sxs-lookup"><span data-stu-id="9070e-174">With few exceptions, any app that has multiple pages uses a frame.</span></span> <span data-ttu-id="9070e-175">通常、アプリにはフレームと、ナビゲーション ビュー コントロールなどの主要なナビゲーション要素を含むメイン ページがあります。</span><span class="sxs-lookup"><span data-stu-id="9070e-175">Typically, an app has a main page that contains the frame and a primary navigation element, such as a navigation view control.</span></span> <span data-ttu-id="9070e-176">ユーザーがページを選択すると、フレームがページを読み込んで表示します。</span><span class="sxs-lookup"><span data-stu-id="9070e-176">When the user selects a page, the frame loads and displays it.</span></span>
:::row-end:::

:::row:::
    :::column:::
        ![tabs and pivot image](images/nav/thumbnail-tabs-pivot.svg)
    :::column-end:::
    :::column span="2":::
        [**Top navigation and tabs**](../controls-and-patterns/navigationview.md)

<span data-ttu-id="9070e-177">同じレベルにあるページへのリンクの横方向の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="9070e-177">Displays a horizontal list of links to pages at the same level.</span></span> <span data-ttu-id="9070e-178">[NavigationView](../controls-and-patterns/navigationview.md)コントロールは、上部のナビゲーションを実装し、パターンのタブします。</span><span class="sxs-lookup"><span data-stu-id="9070e-178">The [NavigationView](../controls-and-patterns/navigationview.md) control implements the top navigation and tabs patterns.</span></span>
        
<span data-ttu-id="9070e-179">上部のナビゲーションを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-179">Use top navigation when:</span></span>

- <span data-ttu-id="9070e-180">画面上のすべてのナビゲーション オプションを表示するには。</span><span class="sxs-lookup"><span data-stu-id="9070e-180">You want to show all navigation options on the screen.</span></span>
- <span data-ttu-id="9070e-181">アプリのコンテンツを追加する領域を必要とします。</span><span class="sxs-lookup"><span data-stu-id="9070e-181">You desire more space for your app's content.</span></span>
- <span data-ttu-id="9070e-182">アイコンは、ナビゲーションのカテゴリを明確に記述できません。</span><span class="sxs-lookup"><span data-stu-id="9070e-182">Icons cannot clearly describe your navigation categories.</span></span>
        
<span data-ttu-id="9070e-183">ときにタブを使用します。</span><span class="sxs-lookup"><span data-stu-id="9070e-183">Use tabs when:</span></span>

- <span data-ttu-id="9070e-184">ナビゲーション履歴とページの状態を保存するには。</span><span class="sxs-lookup"><span data-stu-id="9070e-184">You want to preserve navigation history and page state.</span></span>
- <span data-ttu-id="9070e-185">頻繁にタブを切り替えるユーザーを必要とします。</span><span class="sxs-lookup"><span data-stu-id="9070e-185">You expect users to switch between tabs frequently.</span></span>

:::row-end:::

:::row:::
    :::column:::
         ![tabs and pivot image](images/nav/thumbnail-tabs-pivot.svg)
    :::column-end:::
        :::column span="2":::
    [<span data-ttu-id="9070e-186">**Pivot**</span><span class="sxs-lookup"><span data-stu-id="9070e-186">**Pivot**</span></span>](../controls-and-patterns/pivot.md)
    
<span data-ttu-id="9070e-187">ような[ナビゲーション ビュー](../controls-and-patterns/navigationview.md)タッチと若干異なるナビゲーションの動作の追加をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="9070e-187">Similar to [Navigation View](../controls-and-patterns/navigationview.md), but with additional support for touch and slightly different navigation behavior.</span></span>
    
<span data-ttu-id="9070e-188">ピボットを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-188">Use a pivot when:</span></span>
- <span data-ttu-id="9070e-189">項目間のタッチ スワイプを許可するアプリで使用します。</span><span class="sxs-lookup"><span data-stu-id="9070e-189">You want your app to allow touch-swiping between categories</span></span>
- <span data-ttu-id="9070e-190">カルーセル infintely のナビゲーション オプションをします。</span><span class="sxs-lookup"><span data-stu-id="9070e-190">You want navigation options to carousel infintely</span></span>
- <span data-ttu-id="9070e-191">カテゴリ間のナビゲーション動作を広範囲に制御する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="9070e-191">You do not need extensive control over navigation behavior between categories</span></span>

:::row-end:::

:::row:::
    :::column:::
        ![navview image](images/nav/thumbnail-navview.svg)
    :::column-end:::
    :::column span="2":::
        [**Left navigation**](../controls-and-patterns/navigationview.md)

<span data-ttu-id="9070e-192">トップレベルのページへのリンクの縦方向の一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="9070e-192">Displays a vertical list of links to top-level pages.</span></span> <span data-ttu-id="9070e-193">次の場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="9070e-193">Use when:</span></span>
        
- <span data-ttu-id="9070e-194">ページがトップレベルに存在する場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-194">The pages exist at the top level.</span></span>
- <span data-ttu-id="9070e-195">多くのナビゲーション項目 (5 以上の場合) があります。</span><span class="sxs-lookup"><span data-stu-id="9070e-195">There are many navigation items (more than 5)</span></span>
- <span data-ttu-id="9070e-196">ユーザーが頻繁にページ間を切り替えることを前提としていない場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-196">You don't expect users to switch between pages frequently.</span></span>

:::row-end:::
        
:::row:::
    :::column:::
        ![Master details image](images/nav/thumbnail-master-detail.svg)
    :::column-end:::
    :::column span="2":::
        [**Master/details**](../controls-and-patterns/master-details.md)

<span data-ttu-id="9070e-197">項目の一覧 (マスター ビュー) を表示します。</span><span class="sxs-lookup"><span data-stu-id="9070e-197">Displays a list (master view) of items.</span></span> <span data-ttu-id="9070e-198">項目を選ぶと、対応するページが詳細セクションに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9070e-198">Selecting an item displays its corresponding page in the details section.</span></span> <span data-ttu-id="9070e-199">次の場合に使用します。</span><span class="sxs-lookup"><span data-stu-id="9070e-199">Use when:</span></span>
        
- <span data-ttu-id="9070e-200">ユーザーが頻繁に子項目間を切り替えることを前提としている場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-200">You expect users to switch between child items frequently.</span></span>
- <span data-ttu-id="9070e-201">ユーザーが個々の項目や項目のグループに対して高いレベルの操作 (削除や並べ替えなど) を実行できるようにする場合、およびユーザーが各項目の詳細情報の表示や更新を実行できるようにする場合。</span><span class="sxs-lookup"><span data-stu-id="9070e-201">You want to enable the user to perform high-level operations, such as deleting or sorting, on individual items or groups of items, and also want to enable the user to view or update the details for each item.</span></span>

<span data-ttu-id="9070e-202">マスター/詳細は、メールの受信トレイ、連絡先リスト、データ入力に適しています。</span><span class="sxs-lookup"><span data-stu-id="9070e-202">Master/details is well suited for email inboxes, contact lists, and data entry.</span></span>
:::row-end:::

:::row:::
    :::column:::
        ![Hyperlinks and buttons image](images/nav/thumbnail-hyperlinks-buttons.svg)
    :::column-end:::
    :::column span="2":::
        [**Hyperlinks**](../controls-and-patterns/hyperlinks.md)

<span data-ttu-id="9070e-203">埋め込まれたナビゲーション要素は、ページのコンテンツに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9070e-203">Embedded navigation elements can appear in a page's content.</span></span> <span data-ttu-id="9070e-204">他のナビゲーション要素はページの全体で一貫性がありますが、それとは異なり、コンテンツに埋め込まれたナビゲーション要素はそれぞれのページに固有のナビゲーション要素です。</span><span class="sxs-lookup"><span data-stu-id="9070e-204">Unlike other navigation elements, which should be consistent across the pages, content-embedded navigation elements are unique from page to page.</span></span>
:::row-end:::

## <a name="next-add-navigation-code-to-your-app"></a><span data-ttu-id="9070e-205">次に：アプリへのナビゲーションのコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="9070e-205">Next: Add navigation code to your app</span></span>

<span data-ttu-id="9070e-206">次の記事「[基本的なナビゲーションを実装する](navigate-between-two-pages.md)」では、アプリで 2 つのページ間で基本的なナビゲーションを行うための、Frame コントロールを使用するために必要なコードを示します。</span><span class="sxs-lookup"><span data-stu-id="9070e-206">The next article, [Implement basic navigation](navigate-between-two-pages.md), shows the code required to use a Frame control to enable basic navigation between two pages in your app.</span></span>
