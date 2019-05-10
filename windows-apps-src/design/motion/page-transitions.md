---
Description: UWP アプリでページの切り替え効果を使用する方法について説明します。
title: UWP アプリのページ切り替え効果
template: detail.hbs
ms.date: 04/08/2018
ms.topic: article
keywords: windows 10, uwp
pm-contact: stmoy
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 9b3244c24ff4fa8e3c85ee9970536b1b35d8efd5
ms.sourcegitcommit: cc0ef75f314658b14376eb60ef8e5bb4d7726e04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65444198"
---
# <a name="page-transitions"></a><span data-ttu-id="3269b-104">ページ切り替え効果</span><span class="sxs-lookup"><span data-stu-id="3269b-104">Page transitions</span></span>

<span data-ttu-id="3269b-105">ページ切り替え効果により、ユーザーがアプリ内のページ間を移動するため、ページ間の関係がフィードバックされます。</span><span class="sxs-lookup"><span data-stu-id="3269b-105">Page transitions navigate users between pages in an app, providing feedback as the relationship between pages.</span></span> <span data-ttu-id="3269b-106">ページ切り替え効果により、ナビゲーション階層の最上位にいるのか、兄弟ページ間を移動しているのか、またはページ階層をより深く移動しているのかを、ユーザーが理解しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="3269b-106">Page transitions help users understand if they are at the top of a navigation hierarchy, moving between sibling pages, or navigating deeper into the page hierarchy.</span></span>

<span data-ttu-id="3269b-107">アプリ内のページ間のナビゲーションについて 2 つの異なるアニメーション (*ページの更新*および*ドリル*) が提供されており、[**NavigationTransitionInfo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.navigationtransitioninfo) のサブクラスとして表されています。</span><span class="sxs-lookup"><span data-stu-id="3269b-107">Two different animations are provided for navigation between pages in an app, *Page refresh* and *Drill*, and are represented by subclasses of [**NavigationTransitionInfo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.navigationtransitioninfo).</span></span>

## <a name="examples"></a><span data-ttu-id="3269b-108">例</span><span class="sxs-lookup"><span data-stu-id="3269b-108">Examples</span></span>

<table>
<th align="left"><span data-ttu-id="3269b-109">XAML コントロール ギャラリー</span><span class="sxs-lookup"><span data-stu-id="3269b-109">XAML Controls Gallery</span></span><th>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon.png" alt="XAML controls gallery" width="168"></img></td>
<td>
    <p><span data-ttu-id="3269b-110">ある場合、 <strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong>アプリをインストールするには、ここをクリックして<a href="xamlcontrolsgallery:/item/PageTransition">アプリを開き、操作ページの切り替え効果を参照してください</a>します。</span><span class="sxs-lookup"><span data-stu-id="3269b-110">If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/PageTransition">open the app and see Page Transitions in action</a>.</span></span></p>
    <ul>
    <li><span data-ttu-id="3269b-111"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="3269b-111"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span></li>
    <li><span data-ttu-id="3269b-112"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="3269b-112"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span></li>
    </ul>
</td>
</tr>
</table>

## <a name="page-refresh"></a><span data-ttu-id="3269b-113">ページの更新</span><span class="sxs-lookup"><span data-stu-id="3269b-113">Page refresh</span></span>

<span data-ttu-id="3269b-114">ページの更新は、受信したコンテンツのスライド アップ アニメーションとフェード イン アニメーションの組み合わせです。</span><span class="sxs-lookup"><span data-stu-id="3269b-114">Page refresh is a combination of a slide up animation and a fade in animation for the incoming content.</span></span> <span data-ttu-id="3269b-115">ページの更新は、ユーザーがナビゲーション スタックの最上位に移動したときに使用します (タブ間や左側のナビゲーションの項目間の移動など)。</span><span class="sxs-lookup"><span data-stu-id="3269b-115">Use page refresh when the user is taken to the top of a navigational stack, such as navigating between tabs or left-nav items.</span></span>

<span data-ttu-id="3269b-116">ユーザーが処理を開始したという意識を持てるようにします。</span><span class="sxs-lookup"><span data-stu-id="3269b-116">The desired feeling is that the user has started over.</span></span>

![ページの更新のアニメーション](images/page-refresh.gif)

<span data-ttu-id="3269b-118">ページの更新のアニメーションは、[**EntranceNavigationTransitionInfoClass**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.entrancenavigationtransitioninfo) で表されます。</span><span class="sxs-lookup"><span data-stu-id="3269b-118">The page refresh animation is represented by the [**EntranceNavigationTransitionInfoClass**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.entrancenavigationtransitioninfo).</span></span>

```csharp
// Explicitly play the page refresh animation
myFrame.Navigate(typeof(Page2), null, new EntranceNavigationTransitionInfo());

```

<span data-ttu-id="3269b-119">**注意**:A [**フレーム**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame)自動的に使用して[ **NavigationThemeTransition** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.navigationthemetransition)を 2 つのページ間のナビゲーションをアニメーション化します。</span><span class="sxs-lookup"><span data-stu-id="3269b-119">**Note**: A [**Frame**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.frame) automatically uses [**NavigationThemeTransition**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.navigationthemetransition) to animate navigation between two pages.</span></span> <span data-ttu-id="3269b-120">既定では、アニメーションはページの更新です。</span><span class="sxs-lookup"><span data-stu-id="3269b-120">By default, the animation is page refresh.</span></span>

## <a name="drill"></a><span data-ttu-id="3269b-121">ドリル</span><span class="sxs-lookup"><span data-stu-id="3269b-121">Drill</span></span>

<span data-ttu-id="3269b-122">ドリルは、項目を選択した後で詳細情報を表示するなど、ユーザーがアプリ内でより深く移動するときに使用します。</span><span class="sxs-lookup"><span data-stu-id="3269b-122">Use drill when users navigate deeper into an app, such as displaying more information after selecting an item.</span></span>

<span data-ttu-id="3269b-123">ユーザーがアプリ内をより深く移動したという意識を持てるようにします。</span><span class="sxs-lookup"><span data-stu-id="3269b-123">The desired feeling is that the user has gone deeper into the app.</span></span>

![ドリルのアニメーション](images/drill.gif)

<span data-ttu-id="3269b-125">ドリルのアニメーションは、[**DrillInNavigationTransitionInfo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.drillinnavigationtransitioninfo) クラスで表されます。</span><span class="sxs-lookup"><span data-stu-id="3269b-125">The drill animation is represented by the [**DrillInNavigationTransitionInfo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.drillinnavigationtransitioninfo) class.</span></span>

```csharp
// Play the drill in animation
myFrame.Navigate(typeof(Page2), null, new DrillInNavigationTransitionInfo());
```

## <a name="horizontal-slide"></a><span data-ttu-id="3269b-126">水平方向のスライド</span><span class="sxs-lookup"><span data-stu-id="3269b-126">Horizontal slide</span></span>

<span data-ttu-id="3269b-127">水平方向のスライドを使用して、互いの横にある兄弟のページが表示されることを示します。</span><span class="sxs-lookup"><span data-stu-id="3269b-127">Use horizontal slide to show that sibling pages appear next to each other.</span></span> <span data-ttu-id="3269b-128">[NavigationView](../controls-and-patterns/navigationview.md)コントロールでは、上部のナビゲーションでのこのアニメーションを自動的に使用しますが、独自の水平方向のナビゲーション エクスペリエンスを構築する場合するを実装できます SlideNavigationTransitionInfo で水平方向にスライドします。</span><span class="sxs-lookup"><span data-stu-id="3269b-128">The [NavigationView](../controls-and-patterns/navigationview.md) control automatically uses this animation for top nav, but if you are building your own horizontal navigation experience, then you can implement horizontal slide with SlideNavigationTransitionInfo.</span></span>

<span data-ttu-id="3269b-129">必要な感情は、ユーザーが互いの横にあるページ間で移動することです。</span><span class="sxs-lookup"><span data-stu-id="3269b-129">The desired feeling is that the user is navigating between pages that are next to each other.</span></span> 

```csharp
// Navigate to the right, ie. from LeftPage to RightPage
myFrame.Navigate(typeof(RightPage), null, new SlideNavigationTransitionInfo() { Effect = SlideNavigationTransitionEffect.FromRight } );

// Navigate to the left, ie. from RightPage to LeftPage
myFrame.Navigate(typeof(LeftPage), null, new SlideNavigationTransitionInfo() { Effect = SlideNavigationTransitionEffect.FromLeft } );
```

## <a name="suppress"></a><span data-ttu-id="3269b-130">抑制</span><span class="sxs-lookup"><span data-stu-id="3269b-130">Suppress</span></span>

<span data-ttu-id="3269b-131">ナビゲーション中にアニメーションの再生を回避するには、[**SuppressNavigationTransitionInfo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.suppressnavigationtransitioninfo) を他の **NavigationTransitionInfo** サブタイプの代わりに使用します。</span><span class="sxs-lookup"><span data-stu-id="3269b-131">To avoid playing any animation during navigation, use [**SuppressNavigationTransitionInfo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.suppressnavigationtransitioninfo) in the place of other **NavigationTransitionInfo** subtypes.</span></span>

```csharp
// Suppress the default animation
myFrame.Navigate(typeof(Page2), null, new SuppressNavigationTransitionInfo());
```

<span data-ttu-id="3269b-132">アニメーションの抑制は、[接続型アニメーション](connected-animation.md)または暗黙的な表示/非表示アニメーションを使用して独自の切り替え効果を作成している場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3269b-132">Suppressing the animation is useful if you are building your own transition using [Connected Animations](connected-animation.md) or implicit show/hide animations.</span></span>

## <a name="backwards-navigation"></a><span data-ttu-id="3269b-133">逆方向のナビゲーション</span><span class="sxs-lookup"><span data-stu-id="3269b-133">Backwards navigation</span></span>

<span data-ttu-id="3269b-134">`Frame.GoBack(NavigationTransitionInfo)` を使用して逆方向に移動するときに特定の切り替え効果を再生することができます。</span><span class="sxs-lookup"><span data-stu-id="3269b-134">You can use `Frame.GoBack(NavigationTransitionInfo)` to play a specific transition when navigating backwards.</span></span>

<span data-ttu-id="3269b-135">これは、たとえば応答性の高いマスター/詳細シナリオなど、画面サイズに基づいて移動動作を動的に変更する場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="3269b-135">This can be useful when you modify navigation behavior dynamically based on screen size; for example, in a responsive master/detail scenario.</span></span>

## <a name="related-topics"></a><span data-ttu-id="3269b-136">関連トピック</span><span class="sxs-lookup"><span data-stu-id="3269b-136">Related topics</span></span>

- [<span data-ttu-id="3269b-137">2 つのページ間を移動します。</span><span class="sxs-lookup"><span data-stu-id="3269b-137">Navigate between two pages</span></span>](../basics/navigate-between-two-pages.md)
- [<span data-ttu-id="3269b-138">UWP アプリでのモーション</span><span class="sxs-lookup"><span data-stu-id="3269b-138">Motion in UWP apps</span></span>](index.md)
