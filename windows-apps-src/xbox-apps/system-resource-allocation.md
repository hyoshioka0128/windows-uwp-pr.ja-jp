---
title: Xbox One 上の UWP アプリとゲームのシステム リソース
description: Xbox 上の UWP のシステム リソース
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 12e87019-4315-424e-b73c-426d565deef9
ms.localizationpriority: medium
ms.openlocfilehash: 8cc6ca24453be83f5c10cc6c86c508a5a3f99c4c
ms.sourcegitcommit: b9e2cd5232ad98f4ef367881b92000a3ae610844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "67131928"
---
# <a name="system-resources-for-uwp-apps-and-games-on-xbox-one"></a><span data-ttu-id="3d580-104">Xbox One 上の UWP アプリとゲームのシステム リソース</span><span class="sxs-lookup"><span data-stu-id="3d580-104">System resources for UWP apps and games on Xbox One</span></span>

<span data-ttu-id="3d580-105">Xbox One で実行されている UWP アプリは、システムやその他のアプリとリソースを共有します。</span><span class="sxs-lookup"><span data-stu-id="3d580-105">UWP apps running on Xbox One share resources with the system and other apps.</span></span> <span data-ttu-id="3d580-106">Xbox One アプリの UWP で利用可能なリソースは、アプリとして提出するか、Xbox Live クリエーターズ プログラム ゲームとして提出するかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="3d580-106">The resources available to a UWP on Xbox One app depend on whether you submit as an app or as an Xbox Live Creators Program game.</span></span>

* <span data-ttu-id="3d580-107">フォアグラウンドで実行されているときに利用可能な最大メモリ</span><span class="sxs-lookup"><span data-stu-id="3d580-107">Maximum available memory while running in the foreground:</span></span>
    * <span data-ttu-id="3d580-108">アプリ:1 GB</span><span class="sxs-lookup"><span data-stu-id="3d580-108">Apps: 1 GB</span></span>
    * <span data-ttu-id="3d580-109">ゲーム:5 GB</span><span class="sxs-lookup"><span data-stu-id="3d580-109">Games: 5 GB</span></span>

<span data-ttu-id="3d580-110">バックグラウンドで実行されているアプリに利用可能なメモリは最大 128 MB です。</span><span class="sxs-lookup"><span data-stu-id="3d580-110">The maximum memory available to an app running in the background is 128 MB.</span></span> <span data-ttu-id="3d580-111">バックグラウンド モードは、バックグラウンド ミュージック プレーヤーなどの同時アプリケーションにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="3d580-111">Background mode only applies to concurrent applications, like background music players.</span></span>  <span data-ttu-id="3d580-112">ゲームはバックグラウンドで一時停止および終了されます。</span><span class="sxs-lookup"><span data-stu-id="3d580-112">Games will be suspended and terminated in the background.</span></span>

<span data-ttu-id="3d580-113">これらの制限を超えると、メモリ割り当てエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="3d580-113">Exceeding these limitations will cause memory allocation failures.</span></span> <span data-ttu-id="3d580-114">メモリ使用量の監視について詳しくは、[MemoryManager クラス](https://docs.microsoft.com/uwp/api/windows.system.memorymanager)のリファレンスをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3d580-114">For more information about monitoring memory use, see the [MemoryManager class](https://docs.microsoft.com/uwp/api/windows.system.memorymanager) reference.</span></span>

> [!NOTE]
> <span data-ttu-id="3d580-115">Visual Studio デバッガーからアプリやゲームを実行するときに、これらのメモリの制約は適用されません。</span><span class="sxs-lookup"><span data-stu-id="3d580-115">When running your app or game from the Visual Studio debugger, these memory constraints do not apply.</span></span> <span data-ttu-id="3d580-116">この制限は、デバッグ モードで実行されていないときにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="3d580-116">This limit is only applicable when not running in debugging mode.</span></span>

* <span data-ttu-id="3d580-117">CPU</span><span class="sxs-lookup"><span data-stu-id="3d580-117">CPU</span></span>
    * <span data-ttu-id="3d580-118">アプリ: システムで実行されているアプリとゲームの数に応じて、2 ～ 4 個の CPU コアを共有します。</span><span class="sxs-lookup"><span data-stu-id="3d580-118">Apps: share of 2-4 CPU cores depending on the number of apps and games running on the system.</span></span>
    * <span data-ttu-id="3d580-119">ゲーム:排他的と 2 つの 4 CPU コアを共有します。</span><span class="sxs-lookup"><span data-stu-id="3d580-119">Games: 4 exclusive and 2 shared CPU cores.</span></span>

* <span data-ttu-id="3d580-120">GPU</span><span class="sxs-lookup"><span data-stu-id="3d580-120">GPU</span></span>
    * <span data-ttu-id="3d580-121">アプリ: システムで実行されているアプリとゲームの数に応じて、GPU の 45% を共有します。</span><span class="sxs-lookup"><span data-stu-id="3d580-121">Apps: share of 45% of the GPU depending on the number of apps and games running on the system.</span></span>
    * <span data-ttu-id="3d580-122">ゲーム: 利用可能な GPU サイクルへのフル アクセス。</span><span class="sxs-lookup"><span data-stu-id="3d580-122">Games: full access to available GPU cycles.</span></span>

* <span data-ttu-id="3d580-123">DirectX のサポート</span><span class="sxs-lookup"><span data-stu-id="3d580-123">DirectX support</span></span>
    * <span data-ttu-id="3d580-124">アプリ:DirectX 11 の機能レベル 10 です。</span><span class="sxs-lookup"><span data-stu-id="3d580-124">Apps: DirectX 11 Feature Level 10.</span></span>
    * <span data-ttu-id="3d580-125">ゲーム:DirectX 12、DirectX 11 の機能レベル 10.</span><span class="sxs-lookup"><span data-stu-id="3d580-125">Games: DirectX 12, and DirectX 11 Feature Level 10.</span></span>

* <span data-ttu-id="3d580-126">アプリおよびゲームを Xbox 向けに開発または Microsoft Store に提出するには、必ず x64 アーキテクチャをターゲットにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3d580-126">All apps and games must target the x64 architecture in order to be developed or submitted to the store for Xbox.</span></span>  

<span data-ttu-id="3d580-127">**アプリケーション開発**の場合、利用可能なリソースは標準 PC と比べて限られることがあり、システムで実行されているアプリやゲームの数によって異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3d580-127">For **application development**, resources available may be limited in comparison to a standard PC and can vary based on the number of apps and games running on the system.</span></span>

<span data-ttu-id="3d580-128">**ゲーム開発**の場合、Xbox One は、他のゲーム コンソールと同様に、その潜在的な機能を最大限に利用するために特定のハードウェア ベースの開発キットを必要とする、特殊なハードウェアです。</span><span class="sxs-lookup"><span data-stu-id="3d580-128">For **games development**, Xbox One, like other games consoles, is a specialized piece of hardware that requires a specific hardware-based development kit to access its full potential.</span></span> <span data-ttu-id="3d580-129">Xbox One のハードウェアの機能を最大限に利用する必要があるゲームを開発している場合、[ID@Xbox](https://www.xbox.com/Developers/id) プログラムに登録して Xbox One 開発キットにアクセスすることを検討してください。</span><span class="sxs-lookup"><span data-stu-id="3d580-129">If you are working on a game that requires access to the maximum potential of the Xbox One hardware, consider registering with the [ID@Xbox](https://www.xbox.com/Developers/id) program to get access to an Xbox One development kit.</span></span>

## <a name="see-also"></a><span data-ttu-id="3d580-130">関連項目</span><span class="sxs-lookup"><span data-stu-id="3d580-130">See also</span></span>
- [<span data-ttu-id="3d580-131">Xbox One の UWP</span><span class="sxs-lookup"><span data-stu-id="3d580-131">UWP on Xbox One</span></span>](index.md)
- [<span data-ttu-id="3d580-132">Xbox Live クリエーターズ プログラムを概要します。</span><span class="sxs-lookup"><span data-stu-id="3d580-132">Get started with the Xbox Live Creators Program</span></span>](https://docs.microsoft.com/gaming/xbox-live/get-started-with-creators/creators-program)
- [<span data-ttu-id="3d580-133">DirectX および Xbox One での UWP</span><span class="sxs-lookup"><span data-stu-id="3d580-133">DirectX and UWP on Xbox One</span></span>](https://walbourn.github.io/)