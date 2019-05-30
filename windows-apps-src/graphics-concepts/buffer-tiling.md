---
title: バッファーのタイル表示
description: バッファー リソースは 64 KB のタイルに分割されます。サイズが 64 KB の倍数でない場合は、最後のタイルに空きが生じます。
ms.assetid: 577DC6B0-F373-4748-AD80-2784C597C366
keywords:
- バッファーのタイル表示
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 34201c889ed984b27d50126bd2a04e9b320a17a3
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370652"
---
# <a name="buffer-tiling"></a><span data-ttu-id="7d8f1-104">バッファーのタイル表示</span><span class="sxs-lookup"><span data-stu-id="7d8f1-104">Buffer tiling</span></span>


<span data-ttu-id="7d8f1-105">[バッファー ](introduction-to-buffers.md) リソースは 64 KB のタイルに分割されます。サイズが 64 KB の倍数でない場合は、最後のタイルに空きが生じます。</span><span class="sxs-lookup"><span data-stu-id="7d8f1-105">A [Buffer](introduction-to-buffers.md) resource is divided into 64KB tiles, with some empty space in the last tile if the size is not a multiple of 64KB.</span></span>

<span data-ttu-id="7d8f1-106">構造化バッファーでは、タイリングのストライドに制約があってはなりません。</span><span class="sxs-lookup"><span data-stu-id="7d8f1-106">Structured buffers must have no constraint on the stride to be tiled.</span></span> <span data-ttu-id="7d8f1-107">しかし、[**StructuredBuffers**](https://docs.microsoft.com/windows/desktop/direct3dhlsl/sm5-object-structuredbuffer) を使用するためのハードウェアで可能となるパフォーマンスの最適化が、最初にタイリングを行うことにより損なわれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="7d8f1-107">But possible performance optimizations in hardware for using [**StructuredBuffers**](https://docs.microsoft.com/windows/desktop/direct3dhlsl/sm5-object-structuredbuffer) can be sacrificed by making them tiled in the first place.</span></span>

## <a name="span-idrelated-topicsspanrelated-topics"></a><span data-ttu-id="7d8f1-108"><span id="related-topics"></span>関連トピック</span><span class="sxs-lookup"><span data-stu-id="7d8f1-108"><span id="related-topics"></span>Related topics</span></span>


[<span data-ttu-id="7d8f1-109">ストリーミングのリソースの領域は並べて表示する方法</span><span class="sxs-lookup"><span data-stu-id="7d8f1-109">How a streaming resource's area is tiled</span></span>](how-a-streaming-resource-s-area-is-tiled.md)

 

 




