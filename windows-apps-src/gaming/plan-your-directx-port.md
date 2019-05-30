---
title: DirectX の移植の計画
description: DirectX 9 から DirectX 11 とユニバーサル Windows プラットフォーム (UWP) へのゲーム移植プロジェクトを計画してください。グラフィックス コードのアップグレードと、Windows ランタイム環境へのゲームの配置が必要です。
ms.assetid: 3c0c33ca-5d15-ae12-33f8-9b5d8da08155
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, DirectX, 移植
ms.localizationpriority: medium
ms.openlocfilehash: 247c7cb05027520cb7a39e04ff65579297b66dc9
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368303"
---
# <a name="plan-your-directx-port"></a><span data-ttu-id="fb2c9-104">DirectX の移植の計画</span><span class="sxs-lookup"><span data-stu-id="fb2c9-104">Plan your DirectX port</span></span>



<span data-ttu-id="fb2c9-105">**概要**</span><span class="sxs-lookup"><span data-stu-id="fb2c9-105">**Summary**</span></span>

-   <span data-ttu-id="fb2c9-106">DirectX の移植の計画</span><span class="sxs-lookup"><span data-stu-id="fb2c9-106">Plan your DirectX port</span></span>
-   [<span data-ttu-id="fb2c9-107">Direct3d11 Direct3D 9 からの重要な変更</span><span class="sxs-lookup"><span data-stu-id="fb2c9-107">Important changes from Direct3D 9 to Direct3D 11</span></span>](understand-direct3d-11-1-concepts.md)
-   [<span data-ttu-id="fb2c9-108">機能のマッピング</span><span class="sxs-lookup"><span data-stu-id="fb2c9-108">Feature mapping</span></span>](feature-mapping.md)


<span data-ttu-id="fb2c9-109">DirectX 9 から DirectX 11 とユニバーサル Windows プラットフォーム (UWP) へのゲーム移植プロジェクトを計画してください。グラフィックス コードのアップグレードと、Windows ランタイム環境へのゲームの配置が必要です。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-109">Plan your game porting project from DirectX 9 to DirectX 11 and Universal Windows Platform (UWP): upgrade your graphics code, and put your game in the Windows Runtime environment.</span></span>

## <a name="plan-to-port-graphics-code"></a><span data-ttu-id="fb2c9-110">グラフィックス コードの移植の計画</span><span class="sxs-lookup"><span data-stu-id="fb2c9-110">Plan to port graphics code</span></span>


<span data-ttu-id="fb2c9-111">UWP へのゲームの移植を開始する前に、ゲームに Direct3D 8 の要素が残っていない状態にすることが重要です。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-111">Before you begin porting your game to UWP, it's important to ensure that your game does not have any holdovers from Direct3D 8.</span></span> <span data-ttu-id="fb2c9-112">ゲームに固定関数パイプラインが残っていないことを確かめてください。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-112">Ensure that your game doesn't have any remnants of the fixed function pipeline.</span></span> <span data-ttu-id="fb2c9-113">固定パイプライン機能など、推奨されなくなった機能の全一覧については、「[推奨されなくなった機能](https://docs.microsoft.com/windows/desktop/direct3d10/d3d10-graphics-programming-guide-api-features-deprecated)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-113">For a complete list of deprecated features, including fixed pipeline functionality, see [Deprecated Features](https://docs.microsoft.com/windows/desktop/direct3d10/d3d10-graphics-programming-guide-api-features-deprecated).</span></span>

<span data-ttu-id="fb2c9-114">Direct3D 9 から Direct3D 11 へのアップグレードは、変更箇所を探して置き換える作業にとどまりません。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-114">Upgrading from Direct3D 9 to Direct3D 11 is more than a search-and-replace change.</span></span> <span data-ttu-id="fb2c9-115">Direct3D デバイス、デバイス コンテキスト、グラフィックス インフラストラクチャの違いを把握し、Direct3D 9 以降のその他の重要な変更について理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-115">You need to know the difference between the Direct3D device, device context, and graphics infrastructure, and learn about other important changes since Direct3D 9.</span></span> <span data-ttu-id="fb2c9-116">このセクションの他のトピックを読むことで、このプロセスを開始できます。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-116">You can start this process by reading the other topics in this section.</span></span>

<span data-ttu-id="fb2c9-117">D3DX と DXUT のヘルパー ライブラリは、独自のヘルパー ライブラリか、コミュニティ ツールに置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-117">You must replace the D3DX and DXUT helper libraries with your own helper libraries, or with community tools.</span></span> <span data-ttu-id="fb2c9-118">詳しくは、「[DirectX 11 API への DirectX 9 の機能のマッピング](feature-mapping.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-118">See the [Feature mapping](feature-mapping.md) section for more info.</span></span>

> <span data-ttu-id="fb2c9-119">**注**  を使用することができます、 [DirectX ツール キット](https://go.microsoft.com/fwlink/p/?LinkID=248929)または[DirectXTex](https://go.microsoft.com/fwlink/p/?LinkID=248926) D3DX と DXUT で以前提供されているいくつかの機能を置き換える。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-119">**Note**   You can use the [DirectX Tool Kit](https://go.microsoft.com/fwlink/p/?LinkID=248929) or [DirectXTex](https://go.microsoft.com/fwlink/p/?LinkID=248926) to replace some functionality that was formerly provided by D3DX and DXUT.</span></span>

 

<span data-ttu-id="fb2c9-120">アセンブリ言語で記述されたシェーダーは、HLSL シェーダー モデル 4 レベル 9 を使用してにアップグレードする必要があります\_1 または 9\_3 つの機能、およびシェーダー効果ライブラリは HLSL の構文のより新しいバージョンに更新する必要があります用に記述します。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-120">Shaders written in assembly language should be upgraded to HLSL using shader model 4 level 9\_1 or 9\_3 functionality, and shaders written for the Effects library will need to be updated to a more recent version of HLSL syntax.</span></span> <span data-ttu-id="fb2c9-121">詳しくは、「[DirectX 11 API への DirectX 9 の機能のマッピング](feature-mapping.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-121">See the [Feature mapping](feature-mapping.md) section for more info.</span></span>

<span data-ttu-id="fb2c9-122">さまざまな [Direct3D 機能レベル](https://docs.microsoft.com/windows/desktop/direct3d11/overviews-direct3d-11-devices-downlevel-intro)について確かめてください。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-122">Get familiar with the different [Direct3D feature levels](https://docs.microsoft.com/windows/desktop/direct3d11/overviews-direct3d-11-devices-downlevel-intro).</span></span> <span data-ttu-id="fb2c9-123">機能レベルは、既知の機能のセットを定義することで、幅広いビデオ ハードウェアを分類するものです。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-123">Feature levels classify a wide range of video hardware by defining sets of known functionality.</span></span> <span data-ttu-id="fb2c9-124">各セットは 9.1 ～ 11.2 のバージョンの Direct3D にほぼ対応しています。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-124">Each set roughly corresponds to versions of Direct3D, from 9.1 through 11.2.</span></span> <span data-ttu-id="fb2c9-125">すべての機能レベルで DirectX 11 API を使います。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-125">All feature levels use the DirectX 11 API.</span></span>

## <a name="plan-to-port-win32-ui-code-to-corewindow"></a><span data-ttu-id="fb2c9-126">CoreWindow への Win32 UI コードの移植の計画</span><span class="sxs-lookup"><span data-stu-id="fb2c9-126">Plan to port Win32 UI code to CoreWindow</span></span>


<span data-ttu-id="fb2c9-127">UWP アプリは、[**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) と呼ばれる、アプリ コンテナーに対して作成されるウィンドウで実行されます。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-127">UWP apps run in a window created for an app container, called a [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow).</span></span> <span data-ttu-id="fb2c9-128">ゲームでは、デスクトップのウィンドウよりも必要な実装の詳細が少ない [**IFrameworkView**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.IFrameworkView) からの継承によってウィンドウを制御します。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-128">Your game controls the window by inheriting from [**IFrameworkView**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.IFrameworkView), which requires less implementation details than a desktop window.</span></span> <span data-ttu-id="fb2c9-129">ゲームのメイン ループは [**IFrameworkView::Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run) メソッドにあります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-129">Your game's main loop will be in the [**IFrameworkView::Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run) method.</span></span>

<span data-ttu-id="fb2c9-130">UWP アプリのライフサイクルはデスクトップ アプリとは大きく異なります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-130">The lifecycle of a UWP app is very different from a desktop app.</span></span> <span data-ttu-id="fb2c9-131">ゲームの保存は頻繁に行う必要があります。中断イベントが発生したときに、アプリで実行中のコードを停止できる時間が限られているうえ、アプリの再開時には、プレーヤーが中断時の状態からすぐにゲームを再開できるようにする必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-131">You'll need to save the game often, because when a suspend event happens your app only has a limited amount of time to stop running code, and you want to make sure the player can get back to where they were right away when your app resumes.</span></span> <span data-ttu-id="fb2c9-132">ゲームの保存は、再開時に連続したゲームプレイ エクスペリエンスを維持できるだけの頻度で行う必要があります。ただし、フレームレートに影響したり、ゲームに引っかかりをもたらしたりしない程度にしてください。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-132">Games should save just often enough to maintain a continuous gameplay experience from resume, but not so often that the game saves impact framerate or cause the game to stutter.</span></span> <span data-ttu-id="fb2c9-133">ゲームは、ゲームが終了状態から再開されたときに、必要に応じてゲームの状態を読み込む必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-133">Your game will potentially need to load game state when the game resumes from a terminated state.</span></span>

<span data-ttu-id="fb2c9-134">[DirectXMath](https://docs.microsoft.com/windows/desktop/dxmath/ovw-xnamath-progguide) は、D3DXMath と XNAMath の代わりになり、数学演算ライブラリが必要になったときに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-134">[DirectXMath](https://docs.microsoft.com/windows/desktop/dxmath/ovw-xnamath-progguide) can be used as a replacement for D3DXMath and XNAMath, and it can come in handy if you need a math library.</span></span> <span data-ttu-id="fb2c9-135">DirectXMath には、高速かつ移植可能なデータ型と、シェーダーで利用できるように整列およびパッキングされた型があります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-135">DirectXMath has fast, portable data types, and types that are aligned and packed for use with shaders.</span></span>

<span data-ttu-id="fb2c9-136">[インタロック API](https://docs.microsoft.com/windows/desktop/Sync/what-s-new-in-synchronization) などのネイティブ ライブラリは、ARM の組み込みメソッドをサポートするために拡張されました。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-136">Native libraries such as the [Interlocked API](https://docs.microsoft.com/windows/desktop/Sync/what-s-new-in-synchronization) have been expanded to support ARM intrinsics.</span></span> <span data-ttu-id="fb2c9-137">ゲームでインタロック API を使う場合は、DirectX 11 と UWP でも使い続けることができます。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-137">If your game uses interlocked APIs, you can keep using them in DirectX 11 and UWP.</span></span>

<span data-ttu-id="fb2c9-138">Microsoft のテンプレートとコード サンプルでは新しい C++ 機能が使われており、馴染みがない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-138">Our templates and code samples use new C++ features that you might not be familiar with yet.</span></span> <span data-ttu-id="fb2c9-139">たとえば、UI スレッドをブロックすることなく Direct3D リソースを読み込むために、非同期メソッドが[**ラムダ式**](https://docs.microsoft.com/cpp/cpp/lambda-expressions-in-cpp)と共に使われます。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-139">For example, asynchronous methods are used with [**lambda expressions**](https://docs.microsoft.com/cpp/cpp/lambda-expressions-in-cpp) to load Direct3D resources without blocking the UI thread.</span></span>

<span data-ttu-id="fb2c9-140">頻繁に使う 2 つの概念があります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-140">There are two concepts you'll use often:</span></span>

-   <span data-ttu-id="fb2c9-141">マネージ リファレンス ([ **^ 演算子**](https://docs.microsoft.com/cpp/windows/handle-to-object-operator-hat-cpp-component-extensions)) と [**マネージ クラス**](https://docs.microsoft.com/cpp/windows/classes-and-structs-cpp-component-extensions) (ref クラス) は、Windows ランタイムの基本となる部分です。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-141">Managed references ([**^ operator**](https://docs.microsoft.com/cpp/windows/handle-to-object-operator-hat-cpp-component-extensions)) and [**managed classes**](https://docs.microsoft.com/cpp/windows/classes-and-structs-cpp-component-extensions) (ref classes) are a fundamental part of the Windows Runtime.</span></span> <span data-ttu-id="fb2c9-142">Windows ランタイム コンポーネントとのインターフェイスとして機能するマネージ ref クラスを使う必要があります。具体的には、[**IFrameworkView**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.IFrameworkView) などです。詳しくはチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-142">You will need to use managed ref classes to interface with Windows Runtime components, for example [**IFrameworkView**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.IFrameworkView) (more on that in the walkthrough).</span></span>
-   <span data-ttu-id="fb2c9-143">Direct3D 11 の COM インターフェイスを操作する場合は、[**Microsoft::WRL::ComPtr**](https://docs.microsoft.com/cpp/windows/comptr-class) テンプレート型を使うと COM ポインターが使いやすくなります。</span><span class="sxs-lookup"><span data-stu-id="fb2c9-143">When working with Direct3D 11 COM interfaces, use the [**Microsoft::WRL::ComPtr**](https://docs.microsoft.com/cpp/windows/comptr-class) template type to make COM pointers easier to use.</span></span>

 

 




