---
title: 定数バッファー ビュー (CBV)
description: 定数バッファーには、シェーダーの定数データが含まれます。 それらの価値は、データを変更する必要があるまでデータが存続し、任意の GPU シェーダーからアクセスできることです。
ms.assetid: 99AEC6B0-A43B-4B61-8C3A-ECC8DE1B69A7
keywords:
- 定数バッファー ビュー (CBV)
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 7179f8644970a24a9e7b9ce50a4bcb4d5d225d46
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370451"
---
# <a name="constant-buffer-view-cbv"></a><span data-ttu-id="f27eb-105">定数バッファー ビュー (CBV)</span><span class="sxs-lookup"><span data-stu-id="f27eb-105">Constant buffer view (CBV)</span></span>


<span data-ttu-id="f27eb-106">定数バッファーには、シェーダーの定数データが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f27eb-106">Constant buffers contain shader constant data.</span></span> <span data-ttu-id="f27eb-107">それらの価値は、データを変更する必要があるまでデータが存続し、任意の GPU シェーダーからアクセスできることです。</span><span class="sxs-lookup"><span data-stu-id="f27eb-107">The value of them is that the data persists, and can be accessed by any GPU shader, until it is necessary to change the data.</span></span>

<span data-ttu-id="f27eb-108">定数バッファーの一般的なデータは、ワールド、プロジェクション、およびビュー マトリックスです。これらは、1 つのフレームの描画全体を通して一定のままです。</span><span class="sxs-lookup"><span data-stu-id="f27eb-108">Typical data for a constant buffer would be world, projection and view matrices, which remain constant throughout the drawing of one frame.</span></span>

<span data-ttu-id="f27eb-109">定数バッファーのレイアウトは、HLSL レイアウトと一致する必要があります ([定数変数のパッキング規則](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-packing-rules)をご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="f27eb-109">Constant buffer layout should match the HLSL layout (refer to [Packing Rules for Constant Variables](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-packing-rules)).</span></span>

## <a name="span-idrelated-topicsspanrelated-topics"></a><span data-ttu-id="f27eb-110"><span id="related-topics"></span>関連トピック</span><span class="sxs-lookup"><span data-stu-id="f27eb-110"><span id="related-topics"></span>Related topics</span></span>


[<span data-ttu-id="f27eb-111">ビュー</span><span class="sxs-lookup"><span data-stu-id="f27eb-111">Views</span></span>](views.md)

 

 




