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
# <a name="drag-animations"></a>ドラッグ アニメーション




ドラッグ アンド ドロップ アニメーションは、リスト内で項目を移動するときや、特定の項目を別の項目上にドロップするときなど、オブジェクトを移動する際に使います。

> **重要な API**:[**DragItemThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.dragitemthemeanimation.)


## <a name="dos-and-donts"></a>推奨と非推奨


**ドラッグ開始のアニメーション**

-   ドラッグの開始アニメーションは、ユーザーがオブジェクトを動かし始めるときに使います。
-   ドラッグ アンド ドロップ操作の影響を受けるオブジェクトが他に存在する場合に限り、それらのオブジェクトをアニメーションに含めるようにします。
-   ドラッグの開始アニメーションによって始まったアニメーションのシーケンスの終了には、ドラッグの終了アニメーションを使います。 ドラッグの終了アニメーションにより、ドラッグの開始アニメーションで変化したドラッグされたオブジェクトのサイズが元に戻ります。

**ドラッグ終了のアニメーション**

-   ドラッグの終了アニメーションは、ドラッグされたオブジェクトをドロップするときに使います。
-   ドラッグの終了アニメーションは、リストの追加および削除アニメーションと組み合わせて使います。
-   ドラッグの開始アニメーションに影響を受けるオブジェクトが存在する場合に限り、それらのオブジェクトをドラッグの終了アニメーションに含めるようにします。
-   ドラッグの終了アニメーションは、ドラッグの開始アニメーションよりも先に使わないでください。 ドラッグ シーケンスの完了後にオブジェクトを元のサイズに戻すためには、両方のアニメーションを使う必要があります。

**ドラッグ間アニメーションを入力してください。**

-   項目間でのドラッグの開始アニメーションは、2 つのオブジェクトの間のドロップ可能な場所にドラッグ ソースをドラッグするときに使います。
-   適度な大きさのドロップ ターゲット領域を選んでください。 この領域が小さすぎると、ドラッグ ソースをドロップする際に重ね合わせるのが難しくなるため、好ましくありません。
-   ドロップ可能な場所を示すために影響を受けるオブジェクトが移動するときには、互いにまっすぐに引き離すことをお勧めします。 移動方向が上下になるか、左右になるかは、影響を受けるオブジェクトが並ぶ向きによって異なります。
-   ドラッグ ソースを領域内にドロップできない場合、項目間でのドラッグの開始アニメーションは使わないでください。 項目間へのドラッグの開始アニメーションは、影響を受けるオブジェクトの間にドラッグ ソースをドラッグできることをユーザーに知らせるためのものです。

**Leave アニメーション間でドラッグします**

-   項目間でのドラッグの中止アニメーションは、ユーザーがオブジェクトをドラッグして 2 つのオブジェクトの間のドロップ可能な領域から出すときに使います。
-   項目間でのドラッグの開始アニメーションよりも先に、項目間でのドラッグの中止アニメーションを使わないでください。


## <a name="related-articles"></a>関連記事

**開発者向け**
* [アニメーションの概要](https://docs.microsoft.com/windows/uwp/graphics/animations-overview)
* [ドラッグ アンド ドロップのシーケンスをアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/jj649427(v=win.10))
* [クイック スタート:Library のアニメーションを使用して、UI をアニメーション化](https://docs.microsoft.com/previous-versions/windows/apps/hh452703(v=win.10))
* [**DragItemThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.dragitemthemeanimation.)
* [**DropTargetItemThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.droptargetitemthemeanimation.)
* [**DragOverThemeAnimation クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.dragoverthemeanimation.)


 




