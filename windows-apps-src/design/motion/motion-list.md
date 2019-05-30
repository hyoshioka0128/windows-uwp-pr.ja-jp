---
Description: リスト アニメーションを使うと、写真のアルバムや検索結果の一覧などのコレクションに対して任意の数の項目を挿入または削除できます。
title: UWP アプリでの追加と削除のアニメーション
ms.assetid: A85006AE-4992-457a-B514-500B8BEF5DC8
label: Motion--add and delete animations
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 228fec1571ab3f9c01b4a8dd4084e19bc28dbfe7
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366741"
---
# <a name="add-and-delete-animations"></a><span data-ttu-id="5f33f-104">追加と削除のアニメーション</span><span class="sxs-lookup"><span data-stu-id="5f33f-104">Add and delete animations</span></span>



<span data-ttu-id="5f33f-105">リスト アニメーションを使うと、写真のアルバムや検索結果の一覧などのコレクションに対して任意の数の項目を挿入または削除できます。</span><span class="sxs-lookup"><span data-stu-id="5f33f-105">List animations let you insert or remove single or multiple items from a collection, such as a photo album or a list of search results.</span></span>

> <span data-ttu-id="5f33f-106">**重要な API**:[**AddDeleteThemeTransition クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.adddeletethemetransition.)</span><span class="sxs-lookup"><span data-stu-id="5f33f-106">**Important APIs**: [**AddDeleteThemeTransition class**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.adddeletethemetransition.)</span></span>


## <a name="dos-and-donts"></a><span data-ttu-id="5f33f-107">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="5f33f-107">Do's and don'ts</span></span>


-   <span data-ttu-id="5f33f-108">リスト アニメーションは、既にある一連の項目に新しい項目を 1 つ追加するときに使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-108">Use list animations to add a single new item to an existing set of items.</span></span> <span data-ttu-id="5f33f-109">たとえば、新しい電子メールを受け取ったときや、既にあるセットに新しい写真をインポートするときに使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-109">For example, use them when a new email arrives or when a new photo is imported into an existing set.</span></span>
-   <span data-ttu-id="5f33f-110">リスト アニメーションは、一連の項目に対して複数の項目を一度に追加するときに使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-110">Use list animations to add several items to a set at one time.</span></span> <span data-ttu-id="5f33f-111">たとえば、一連の新しい写真を既にあるコレクションにインポートするときに使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-111">For example, use them when you import a new set of photos to an existing collection.</span></span> <span data-ttu-id="5f33f-112">複数項目の追加と削除は、個々のオブジェクトの処理に間が生じることなく同時に実行されます。</span><span class="sxs-lookup"><span data-stu-id="5f33f-112">The addition or deletion of multiple items should happen at the same time, with no delay between the action on the individual objects.</span></span>
-   <span data-ttu-id="5f33f-113">追加と削除のリスト アニメーションは、ペアで使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-113">Use add and delete list animations as a pair.</span></span> <span data-ttu-id="5f33f-114">一方のアニメーションを使った場合は、逆の操作として対応するもう一方のアニメーションを使うようにしてください。</span><span class="sxs-lookup"><span data-stu-id="5f33f-114">Whenever you use one of these animations, use the corresponding animation for the opposite action.</span></span>
-   <span data-ttu-id="5f33f-115">リスト アニメーションは、要素または要素のグループを一度に追加または削除できる項目リストに使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-115">Use list animations with a list of items to which you can add or delete one element or group of elements at once.</span></span>
-   <span data-ttu-id="5f33f-116">コンテナーを表示したり非表示にしたりする目的でリスト アニメーションを使うのは避けてください。</span><span class="sxs-lookup"><span data-stu-id="5f33f-116">Don't use list animations to display or remove a container.</span></span> <span data-ttu-id="5f33f-117">リスト アニメーションは、既に表示されているコレクションまたはセットのメンバーに対して使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-117">These animations are for members of a collection or set that is already being displayed.</span></span> <span data-ttu-id="5f33f-118">アプリ サーフェス上に一時的なコンテナーを表示したり非表示にしたりするには、ポップアップ アニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-118">Use pop-up animations to show or hide a transient container on top of the app surface.</span></span> <span data-ttu-id="5f33f-119">アプリ サーフェスの一部となっているコンテナーを表示したり置き換えたりするには、コンテンツ切り替えアニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-119">Use content transition animations to display or replace a container that is part of the app surface.</span></span>
-   <span data-ttu-id="5f33f-120">項目のセット全体に対してリスト アニメーションを使うのは避けてください。</span><span class="sxs-lookup"><span data-stu-id="5f33f-120">Don't use list animations on an entire set of items.</span></span> <span data-ttu-id="5f33f-121">コンテナー内のコレクション全体を追加したり削除したりするには、コンテンツ切り替えアニメーションを使います。</span><span class="sxs-lookup"><span data-stu-id="5f33f-121">Use the content transition animations to add or remove an entire collection within your container.</span></span>



## <a name="related-articles"></a><span data-ttu-id="5f33f-122">関連記事</span><span class="sxs-lookup"><span data-stu-id="5f33f-122">Related articles</span></span>

* [<span data-ttu-id="5f33f-123">アニメーションの概要</span><span class="sxs-lookup"><span data-stu-id="5f33f-123">Animations overview</span></span>](https://docs.microsoft.com/windows/uwp/graphics/animations-overview)
* <span data-ttu-id="5f33f-124">[一覧の追加と削除をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649430(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="5f33f-124">[Animating list additions and deletions](https://docs.microsoft.com/previous-versions/windows/apps/jj649430(v=win.10))</span></span>
* <span data-ttu-id="5f33f-125">[クイック スタート:Library のアニメーションを使用して、UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="5f33f-125">[Quickstart: Animating your UI using library animations](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))</span></span>
* [<span data-ttu-id="5f33f-126">**AddDeleteThemeTransition クラス**</span><span class="sxs-lookup"><span data-stu-id="5f33f-126">**AddDeleteThemeTransition class**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.adddeletethemetransition.)

 

 




