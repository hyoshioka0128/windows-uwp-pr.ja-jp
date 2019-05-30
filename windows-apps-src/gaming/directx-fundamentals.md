---
title: DirectX プログラミングの基本
description: DirectX プログラミングの基本について説明します。
ms.assetid: 05a1bc59-f32e-44a0-8902-94cf1e099b1b
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, DirectX, 読み込み, ラスタライズ, メッシュ, ビットマップ, 2D, 3D
ms.localizationpriority: medium
ms.openlocfilehash: 942a775fca262903b1ee72831b4eae6612d25786
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368865"
---
# <a name="fundamentals-of-directx-programming"></a><span data-ttu-id="97918-104">DirectX プログラミングの基本</span><span class="sxs-lookup"><span data-stu-id="97918-104">Fundamentals of DirectX programming</span></span>

<span data-ttu-id="97918-105">このセクションでは、DirectX プログラミングの基本的な情報について説明します。</span><span class="sxs-lookup"><span data-stu-id="97918-105">This section provides information about the basic blocks of DirectX programming.</span></span>

<span data-ttu-id="97918-106">「DirectX ゲームの 2D グラフィックス」トピックでは、2D ビットマップ グラフィックスおよびエフェクトの用途、およびこれらを Direct2D と Direct3D の両方のライブラリにある要素を組み合わせて利用しているゲームで使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="97918-106">2D graphics for DirectX games topic explains the use of 2D bitmap graphics and effects, and how to use them in your game using a combination of elements from both Direct2D and Direct3D libraries.</span></span>

<span data-ttu-id="97918-107">「Direct3D グラフィックスの学習ガイド」トピックでは、Direct3D で使われている概念の概要について説明します。</span><span class="sxs-lookup"><span data-stu-id="97918-107">Direct3D graphics learning guide topic provides an overview of the concepts that Direct3D uses.</span></span>

<span data-ttu-id="97918-108">「DirectX ゲームの基本的な 3D グラフィックス」トピックでは、3D グラフィックスの基本的な概念について説明します。5 つのパートから成るチュートリアルを利用して、Direct3D の概念や API を紹介します。</span><span class="sxs-lookup"><span data-stu-id="97918-108">Basic 3D graphics for DirectX games topic explains the fundamental concepts of 3D graphics using a five-part tutorial that introduces the Direct3D concept and API.</span></span> <span data-ttu-id="97918-109">このチュートリアルでは、Windows ランタイムを使用した Direct3D インターフェイスの初期化、頂点ごとのシェーダー操作の適用、ジオメトリの設定、シーンのラスタライズ、および隠面のカリングの各方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="97918-109">This tutorial shows you how to initialize Direct3D interfaces using Windows Runtime, apply per-vertex shader operations, set up the geometry, rasterize the scene, and cull hidden surfaces.</span></span>

<span data-ttu-id="97918-110">「DirectX ゲームでのリソースの読み込み」トピックでは、UWP ゲームで使用するために、メッシュ (モデル)、テクスチャ (ビットマップ)、コンパイル済みシェーダーの各オブジェクトをローカル ストレージや他のデータ ストリームから読み込むための基本的な手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="97918-110">Load resources in your DirectX game topic guides you through the basic steps for loading meshes (models), textures (bitmaps), and compiled shader objects from local storage or other data streams for use in your UWP game.</span></span>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="97918-111">トピック</span><span class="sxs-lookup"><span data-stu-id="97918-111">Topic</span></span></th>
<th align="left"><span data-ttu-id="97918-112">説明</span><span class="sxs-lookup"><span data-stu-id="97918-112">Description</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span data-ttu-id="97918-113"><a href="working-with-2d-graphics-in-your-directx-game.md">DirectX ゲームの 2D グラフィック</a></span><span class="sxs-lookup"><span data-stu-id="97918-113"><a href="working-with-2d-graphics-in-your-directx-game.md">2D graphics for DirectX games</a></span></span></p></td>
<td align="left"><p><span data-ttu-id="97918-114">DirectX を使用して 2D グラフィックスを作成します。</span><span class="sxs-lookup"><span data-stu-id="97918-114">Create 2D graphics using DirectX.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="97918-115"><a href="https://docs.microsoft.com/windows/uwp/graphics-concepts/index">Direct3D グラフィックス学習ガイド</a></span><span class="sxs-lookup"><span data-stu-id="97918-115"><a href="https://docs.microsoft.com/windows/uwp/graphics-concepts/index">Direct3D graphics learning guide</a></span></span></p></td>
<td align="left"><p><span data-ttu-id="97918-116">Direct3D でのグラフィックスの概念について説明します。</span><span class="sxs-lookup"><span data-stu-id="97918-116">Understand Direct3D graphics concepts.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="97918-117"><a href="an-introduction-to-3d-graphics-with-directx.md">DirectX ゲーム用の基本的な 3D グラフィック</a></span><span class="sxs-lookup"><span data-stu-id="97918-117"><a href="an-introduction-to-3d-graphics-with-directx.md">Basic 3D graphics for DirectX games</a></span></span></p></td>
<td align="left"><p><span data-ttu-id="97918-118">DirectX の基本的な 3D グラフィックスを作成します。</span><span class="sxs-lookup"><span data-stu-id="97918-118">Create basic 3D DirectX graphics.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="97918-119"><a href="load-a-game-asset.md">DirectX ゲームでリソースを読み込む</a></span><span class="sxs-lookup"><span data-stu-id="97918-119"><a href="load-a-game-asset.md">Load resources in your DirectX game</a></span></span></p></td>
<td align="left"><p><span data-ttu-id="97918-120">DirectX ゲームでメッシュを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="97918-120">Load meshes in your DirectX game.</span></span></p></td>
</tr>
</tbody>
</table>