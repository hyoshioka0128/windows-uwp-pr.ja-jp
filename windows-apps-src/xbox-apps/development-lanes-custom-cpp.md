---
title: ユニバーサル Windows プラットフォーム (UWP) を使用した Xbox での C++ ゲーム開発
description: Xbox での C++ UWP ゲーム開発。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 6ae36021-94d3-43df-9e96-69a93cfe8b56
ms.localizationpriority: medium
ms.openlocfilehash: 585289fdc66b8730036f3d14faeafce8c22c09a7
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371359"
---
# <a name="bring-custom-c-games-to-uwp-on-xbox"></a><span data-ttu-id="0ae39-104">カスタム C++ ゲームを Xbox の UWP に移行する</span><span class="sxs-lookup"><span data-stu-id="0ae39-104">Bring custom C++ games to UWP on Xbox</span></span>

<span data-ttu-id="0ae39-105">カスタム C++ エンジンを作成する場合、Xbox One では C++ が完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="0ae39-105">If you are writing a custom C++ engine, Xbox One has full support for C++.</span></span> 

<span data-ttu-id="0ae39-106">ユニバーサル Windows プラットフォーム (UWP) の C++ ゲームは、レンダリングに DirectX を使用します。</span><span class="sxs-lookup"><span data-stu-id="0ae39-106">C++ games on the Universal Windows Platform (UWP) use DirectX for rendering.</span></span> <span data-ttu-id="0ae39-107">詳しくは、「[DirectX のグラフィックスとゲーミング](https://msdn.microsoft.com/library/windows/desktop/ee663274(v=vs.85).aspx)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ae39-107">Learn more at [DirectX Graphics and Gaming](https://msdn.microsoft.com/library/windows/desktop/ee663274(v=vs.85).aspx).</span></span>

<span data-ttu-id="0ae39-108">開発には、[C++ コンポーネント拡張機能](https://docs.microsoft.com/cpp/cppcx/visual-c-language-reference-c-cx) (C++/CX) または[標準 C++](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) (Win32 と COM) を使うことができます。</span><span class="sxs-lookup"><span data-stu-id="0ae39-108">You can write [C++ with component extensions](https://docs.microsoft.com/cpp/cppcx/visual-c-language-reference-c-cx) (C++/CX) or [standard C++](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) (Win32 and COM).</span></span>

<span data-ttu-id="0ae39-109">コンソールを開発キットとして使用する方法と Visual Studio から展開する方法については、「[ゲームと DirectX](../gaming/index.md)」および「[ファースト ステップ ガイド](getting-started.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ae39-109">To learn how to turn your console into a development kit and how to deploy from Visual Studio, see [Games and DirectX](../gaming/index.md) and the [getting started](getting-started.md) guide.</span></span>

> [!NOTE]
> <span data-ttu-id="0ae39-110">現時点では、Xbox One で DirectX 12 はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="0ae39-110">Xbox One does not support DirectX 12 at this time.</span></span>


## <a name="see-also"></a><span data-ttu-id="0ae39-111">関連項目</span><span class="sxs-lookup"><span data-stu-id="0ae39-111">See also</span></span>
- [<span data-ttu-id="0ae39-112">既存のゲームの Xbox への移行</span><span class="sxs-lookup"><span data-stu-id="0ae39-112">Bringing existing games to Xbox</span></span>](development-lanes-landing.md)
- [<span data-ttu-id="0ae39-113">Xbox One の UWP</span><span class="sxs-lookup"><span data-stu-id="0ae39-113">UWP on Xbox One</span></span>](index.md)

