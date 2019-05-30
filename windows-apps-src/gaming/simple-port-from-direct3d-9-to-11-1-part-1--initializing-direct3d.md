---
title: Direct3D 11 の初期化
description: Direct3D デバイスとデバイス コンテキストへのハンドルを取得する方法や、DXGI を使ってスワップ チェーンを設定する方法など、Direct3D 9 の初期化コードを Direct3D 11 に変換する方法について説明します。
ms.assetid: 1bd5e8b7-fd9d-065c-9ff3-1a9b1c90da29
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, Direct3D 11, 初期化, 移植, Direct3D 9
ms.localizationpriority: medium
ms.openlocfilehash: c5a7f33ddbc6d70af5293b92165892c2098e452d
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368032"
---
# <a name="initialize-direct3d-11"></a><span data-ttu-id="e4750-104">Direct3D 11 の初期化</span><span class="sxs-lookup"><span data-stu-id="e4750-104">Initialize Direct3D 11</span></span>



<span data-ttu-id="e4750-105">**概要**</span><span class="sxs-lookup"><span data-stu-id="e4750-105">**Summary**</span></span>

-   <span data-ttu-id="e4750-106">作業 1:Direct3D 11 の初期化</span><span class="sxs-lookup"><span data-stu-id="e4750-106">Part 1: Initialize Direct3D 11</span></span>
-   [<span data-ttu-id="e4750-107">パート 2: レンダリングのフレームワークを変換します。</span><span class="sxs-lookup"><span data-stu-id="e4750-107">Part 2: Convert the rendering framework</span></span>](simple-port-from-direct3d-9-to-11-1-part-2--rendering.md)
-   [<span data-ttu-id="e4750-108">パート 3:ポート、ゲームのループ</span><span class="sxs-lookup"><span data-stu-id="e4750-108">Part 3: Port the game loop</span></span>](simple-port-from-direct3d-9-to-11-1-part-3--viewport-and-game-loop.md)


<span data-ttu-id="e4750-109">Direct3D デバイスとデバイス コンテキストへのハンドルを取得する方法や、DXGI を使ってスワップ チェーンを設定する方法など、Direct3D 9 の初期化コードを Direct3D 11 に変換する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e4750-109">Shows how to convert Direct3D 9 initialization code to Direct3D 11, including how to get handles to the Direct3D device and the device context and how to use DXGI to set up a swap chain.</span></span> <span data-ttu-id="e4750-110">「[チュートリアル: DirectX 11 とユニバーサル Windows プラットフォーム (UWP) への簡単な Direct3D 9 アプリの移植](walkthrough--simple-port-from-direct3d-9-to-11-1.md)」のパート 1 です。</span><span class="sxs-lookup"><span data-stu-id="e4750-110">Part 1 of the [Port a simple Direct3D 9 app to DirectX 11 and Universal Windows Platform (UWP)](walkthrough--simple-port-from-direct3d-9-to-11-1.md) walkthrough.</span></span>

## <a name="initialize-the-direct3d-device"></a><span data-ttu-id="e4750-111">Direct3D デバイスの初期化</span><span class="sxs-lookup"><span data-stu-id="e4750-111">Initialize the Direct3D device</span></span>


<span data-ttu-id="e4750-112">Direct3D 9 では、[**IDirect3D9::CreateDevice**](https://docs.microsoft.com/windows/desktop/api/d3d9/nf-d3d9-idirect3d9-createdevice) を呼び出して、Direct3D デバイスへのハンドルを作成しました。</span><span class="sxs-lookup"><span data-stu-id="e4750-112">In Direct3D 9, we created a handle to the Direct3D device by calling [**IDirect3D9::CreateDevice**](https://docs.microsoft.com/windows/desktop/api/d3d9/nf-d3d9-idirect3d9-createdevice).</span></span> <span data-ttu-id="e4750-113">最初に [**IDirect3D9 interface**](https://docs.microsoft.com/windows/desktop/api/d3d9helper/nn-d3d9helper-idirect3d9) へのポインターを取得し、Direct3D デバイスとスワップ チェーンの構成を制御するさまざまなパラメーターを指定しました。</span><span class="sxs-lookup"><span data-stu-id="e4750-113">We started by getting a pointer to [**IDirect3D9 interface**](https://docs.microsoft.com/windows/desktop/api/d3d9helper/nn-d3d9helper-idirect3d9) and we specified a number of parameters to control the configuration of the Direct3D device and the swap chain.</span></span> <span data-ttu-id="e4750-114">それを実行する前に、[**GetDeviceCaps**](https://docs.microsoft.com/windows/desktop/api/wingdi/nf-wingdi-getdevicecaps) を呼び出して、デバイスが実行できない処理を求めていないことを確認しました。</span><span class="sxs-lookup"><span data-stu-id="e4750-114">Before doing this we called [**GetDeviceCaps**](https://docs.microsoft.com/windows/desktop/api/wingdi/nf-wingdi-getdevicecaps) to make sure we weren't asking the device to do something it couldn't do.</span></span>

<span data-ttu-id="e4750-115">Direct3D 9</span><span class="sxs-lookup"><span data-stu-id="e4750-115">Direct3D 9</span></span>

```cpp
UINT32 AdapterOrdinal = 0;
D3DDEVTYPE DeviceType = D3DDEVTYPE_HAL;
D3DCAPS9 caps;
m_pD3D->GetDeviceCaps(AdapterOrdinal, DeviceType, &caps); // caps bits

D3DPRESENT_PARAMETERS params;
ZeroMemory(&params, sizeof(D3DPRESENT_PARAMETERS));

// Swap chain parameters:
params.hDeviceWindow = m_hWnd;
params.AutoDepthStencilFormat = D3DFMT_D24X8;
params.BackBufferFormat = D3DFMT_X8R8G8B8;
params.MultiSampleQuality = D3DMULTISAMPLE_NONE;
params.MultiSampleType = D3DMULTISAMPLE_NONE;
params.SwapEffect = D3DSWAPEFFECT_DISCARD;
params.Windowed = true;
params.PresentationInterval = 0;
params.BackBufferCount = 2;
params.BackBufferWidth = 0;
params.BackBufferHeight = 0;
params.EnableAutoDepthStencil = true;
params.Flags = 2;

m_pD3D->CreateDevice(
    0,
    D3DDEVTYPE_HAL,
    m_hWnd,
    64,
    &params,
    &m_pd3dDevice
    );
```

<span data-ttu-id="e4750-116">Direct3D 11 では、デバイス コンテキストとグラフィックス インフラストラクチャはデバイス自体とは別と見なされます。</span><span class="sxs-lookup"><span data-stu-id="e4750-116">In Direct3D 11, the device context and graphics infrastructure is considered separate from the device itself.</span></span> <span data-ttu-id="e4750-117">初期化は複数の手順に分かれます。</span><span class="sxs-lookup"><span data-stu-id="e4750-117">Initialization is divided into multiple steps.</span></span>

<span data-ttu-id="e4750-118">まず、デバイスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e4750-118">First we create the device.</span></span> <span data-ttu-id="e4750-119">デバイスでサポートしている機能レベルの一覧を取得します。これにより、GPU に関する必要な情報がほとんどわかります。</span><span class="sxs-lookup"><span data-stu-id="e4750-119">We get a list of the feature levels the device supports - this informs most of what we need to know about the GPU.</span></span> <span data-ttu-id="e4750-120">また、Direct3D にアクセスするためだけに、インターフェイスを作成する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="e4750-120">Also, we don't need to create an interface just to access Direct3D.</span></span> <span data-ttu-id="e4750-121">代わりに、[**D3D11CreateDevice**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-d3d11createdevice) コア API を使います。</span><span class="sxs-lookup"><span data-stu-id="e4750-121">Instead we use the [**D3D11CreateDevice**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-d3d11createdevice) core API.</span></span> <span data-ttu-id="e4750-122">これにより、デバイスへのハンドルとデバイスのイミディエイト コンテキストが提供されます。</span><span class="sxs-lookup"><span data-stu-id="e4750-122">This gives us a handle to the device and the device's immediate context.</span></span> <span data-ttu-id="e4750-123">デバイス コンテキストは、パイプラインの状態を設定し、レンダリング コマンドを生成するために使われます。</span><span class="sxs-lookup"><span data-stu-id="e4750-123">The device context is used to set pipeline state and generate rendering commands.</span></span>

<span data-ttu-id="e4750-124">Direct3D 11 デバイスとコンテキストを作成すると、COM のポインター機能を利用して、最新バージョンのインターフェイスを取得できます。このインターフェイスには追加機能が含まれているため、常に取得することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e4750-124">After creating the Direct3D 11 device and context, we can take advantage of COM pointer functionality to get the most recent version of the interfaces, which include additional capability and are always recommended.</span></span>

> <span data-ttu-id="e4750-125">**注**   D3D\_機能\_レベル\_9\_(2.0 のシェーダー モデルに対応) する 1 は、Microsoft Store ゲームがサポートするために必要な最小のレベル。</span><span class="sxs-lookup"><span data-stu-id="e4750-125">**Note**   D3D\_FEATURE\_LEVEL\_9\_1 (which corresponds to shader model 2.0) is the minimum level your Microsoft Store game is required to support.</span></span> <span data-ttu-id="e4750-126">(9 をサポートしていない場合、ゲームの ARM のパッケージの証明が失敗する\_1)。かどうかは、ゲームにも、シェーダー モデル 3 の機能のレンダリング パスが含まれています、D3D を含める必要があります\_機能\_レベル\_9\_配列内の 3。</span><span class="sxs-lookup"><span data-stu-id="e4750-126">(Your game's ARM packages will fail certification if you don't support 9\_1.) If your game also includes a rendering path for shader model 3 features, then you should include D3D\_FEATURE\_LEVEL\_9\_3 in the array.</span></span>

 

<span data-ttu-id="e4750-127">Direct3D 11</span><span class="sxs-lookup"><span data-stu-id="e4750-127">Direct3D 11</span></span>

```cpp
// This flag adds support for surfaces with a different color channel 
// ordering than the API default. It is required for compatibility with
// Direct2D.
UINT creationFlags = D3D11_CREATE_DEVICE_BGRA_SUPPORT;

#if defined(_DEBUG)
// If the project is in a debug build, enable debugging via SDK Layers.
creationFlags |= D3D11_CREATE_DEVICE_DEBUG;
#endif

// This example only uses feature level 9.1.
D3D_FEATURE_LEVEL featureLevels[] = 
{
    D3D_FEATURE_LEVEL_9_1
};

// Create the Direct3D 11 API device object and a corresponding context.
ComPtr<ID3D11Device> device;
ComPtr<ID3D11DeviceContext> context;
D3D11CreateDevice(
    nullptr, // Specify nullptr to use the default adapter.
    D3D_DRIVER_TYPE_HARDWARE,
    nullptr,
    creationFlags,
    featureLevels,
    ARRAYSIZE(featureLevels),
    D3D11_SDK_VERSION, // UWP apps must set this to D3D11_SDK_VERSION.
    &device, // Returns the Direct3D device created.
    nullptr,
    &context // Returns the device immediate context.
    );

// Store pointers to the Direct3D 11.2 API device and immediate context.
device.As(&m_d3dDevice);

context.As(&m_d3dContext);
```

## <a name="create-a-swap-chain"></a><span data-ttu-id="e4750-128">スワップ チェーンの作成</span><span class="sxs-lookup"><span data-stu-id="e4750-128">Create a swap chain</span></span>


<span data-ttu-id="e4750-129">Direct3D 11 には、DirectX Graphics Infrastructure (DXGI) と呼ばれるデバイス API が含まれています。</span><span class="sxs-lookup"><span data-stu-id="e4750-129">Direct3D 11 includes a device API called DirectX graphics infrastructure (DXGI).</span></span> <span data-ttu-id="e4750-130">DXGI インターフェイスを使うと、(たとえば、) スワップ チェーンを構成する方法を制御し、共有デバイスを設定できます。</span><span class="sxs-lookup"><span data-stu-id="e4750-130">The DXGI interface allows us to (for example) control how the swap chain is configured and set up shared devices.</span></span> <span data-ttu-id="e4750-131">Direct3D の初期化のこの手順では、DXGI を使って、スワップ チェーンを作成します。</span><span class="sxs-lookup"><span data-stu-id="e4750-131">At this step in initializing Direct3D, we're going to use DXGI to create a swap chain.</span></span> <span data-ttu-id="e4750-132">デバイスを作成しているため、インターフェイス チェーンに従って DXGI アダプターに戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="e4750-132">Since we created the device, we can follow an interface chain back to the DXGI adapter.</span></span>

<span data-ttu-id="e4750-133">Direct3D デバイスでは、DXGI の COM インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="e4750-133">The Direct3D device implements a COM interface for DXGI.</span></span> <span data-ttu-id="e4750-134">最初に、そのインターフェイスを取得し、それを使って、デバイスをホストしている DXGI アダプターを要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e4750-134">First we need to get that interface and use it to request the DXGI adapter hosting the device.</span></span> <span data-ttu-id="e4750-135">次に、DXGI アダプターを使って、DXGI ファクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="e4750-135">Then we use the DXGI adapter to create a DXGI factory.</span></span>

> <span data-ttu-id="e4750-136">**注**   COM インターフェイスのうち、最初の応答が使用することがありますので[ **QueryInterface**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_))します。</span><span class="sxs-lookup"><span data-stu-id="e4750-136">**Note**   These are COM interfaces so your first response might be to use [**QueryInterface**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-queryinterface(q_)).</span></span> <span data-ttu-id="e4750-137">しかし、代わりに、[**Microsoft::WRL::ComPtr**](https://docs.microsoft.com/cpp/windows/comptr-class) スマート ポインターを使ってください。</span><span class="sxs-lookup"><span data-stu-id="e4750-137">You should use [**Microsoft::WRL::ComPtr**](https://docs.microsoft.com/cpp/windows/comptr-class) smart pointers instead.</span></span> <span data-ttu-id="e4750-138">次に、[**As()** ](https://docs.microsoft.com/previous-versions/br230426(v=vs.140)) メソッドを呼び出して、適切なインターフェイスの種類の空の COM ポインターを提供します。</span><span class="sxs-lookup"><span data-stu-id="e4750-138">Then just call the [**As()**](https://docs.microsoft.com/previous-versions/br230426(v=vs.140)) method, supplying an empty COM pointer of the correct interface type.</span></span>

 

<span data-ttu-id="e4750-139">**Direct3D 11**</span><span class="sxs-lookup"><span data-stu-id="e4750-139">**Direct3D 11**</span></span>

```cpp
ComPtr<IDXGIDevice2> dxgiDevice;
m_d3dDevice.As(&dxgiDevice);

// Then, the adapter hosting the device;
ComPtr<IDXGIAdapter> dxgiAdapter;
dxgiDevice->GetAdapter(&dxgiAdapter);

// Then, the factory that created the adapter interface:
ComPtr<IDXGIFactory2> dxgiFactory;
dxgiAdapter->GetParent(
    __uuidof(IDXGIFactory2),
    &dxgiFactory
    );
```

<span data-ttu-id="e4750-140">DXGI ファクトリを作成したので、それを使って、スワップ チェーンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="e4750-140">Now that we have the DXGI factory, we can use it to create the swap chain.</span></span> <span data-ttu-id="e4750-141">スワップ チェーンのパラメーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="e4750-141">Let's define the swap chain parameters.</span></span> <span data-ttu-id="e4750-142">画面の形式を指定する必要があります選択します[ **DXGI\_形式\_B8G8R8A8\_UNORM** ](https://docs.microsoft.com/windows/desktop/api/dxgiformat/ne-dxgiformat-dxgi_format) Direct2D との互換性があるためです。</span><span class="sxs-lookup"><span data-stu-id="e4750-142">We need to specify the surface format; we'll choose [**DXGI\_FORMAT\_B8G8R8A8\_UNORM**](https://docs.microsoft.com/windows/desktop/api/dxgiformat/ne-dxgiformat-dxgi_format) because it's compatible with Direct2D.</span></span> <span data-ttu-id="e4750-143">画面のスケーリング、マルチサンプリング、ステレオ レンダリングは、この例では使わないため、オフにします。</span><span class="sxs-lookup"><span data-stu-id="e4750-143">We'll turn off display scaling, multisampling, and stereo rendering because they aren't used in this example.</span></span> <span data-ttu-id="e4750-144">CoreWindow で直接実行するため、幅と高さを 0 に設定したままにし、全画面の値を自動的に取得できます。</span><span class="sxs-lookup"><span data-stu-id="e4750-144">Since we are running directly in a CoreWindow we can leave the width and height set to 0 and get full-screen values automatically.</span></span>

> <span data-ttu-id="e4750-145">**注**  常にセット、 *SDKVersion* D3D11 パラメーター\_SDK\_UWP アプリのバージョン。</span><span class="sxs-lookup"><span data-stu-id="e4750-145">**Note**   Always set the *SDKVersion* parameter to D3D11\_SDK\_VERSION for UWP apps.</span></span>

 

<span data-ttu-id="e4750-146">**Direct3D 11**</span><span class="sxs-lookup"><span data-stu-id="e4750-146">**Direct3D 11**</span></span>

```cpp
ComPtr<IDXGISwapChain1> swapChain;
dxgiFactory->CreateSwapChainForCoreWindow(
    m_d3dDevice.Get(),
    reinterpret_cast<IUnknown*>(window),
    &swapChainDesc,
    nullptr,
    &swapChain
    );
swapChain.As(&m_swapChain);
```

<span data-ttu-id="e4750-147">画面に表示できる実際よりもより多くの場合、レンダリングは確実に、1 を使用してフレームの待機時間を設定します[ **DXGI\_スワップ\_効果\_反転\_シーケンシャル**](https://docs.microsoft.com/windows/desktop/api/dxgi/ne-dxgi-dxgi_swap_effect).</span><span class="sxs-lookup"><span data-stu-id="e4750-147">To ensure we aren't rendering more often than the screen can actually display, we set frame latency to 1 and use [**DXGI\_SWAP\_EFFECT\_FLIP\_SEQUENTIAL**](https://docs.microsoft.com/windows/desktop/api/dxgi/ne-dxgi-dxgi_swap_effect).</span></span> <span data-ttu-id="e4750-148">これにより、電力が節約されます。また、これはストアの認定の要件です。このチュートリアルのパート 2 では、画面への表示について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="e4750-148">This saves power and is a store certification requirement; we'll learn more about presenting to the screen in part 2 of this walkthrough.</span></span>

> <span data-ttu-id="e4750-149">**注**  を使用することができますマルチ スレッド (たとえば、 [ **ThreadPool** ](https://docs.microsoft.com/uwp/api/Windows.System.Threading)作業項目) レンダリング スレッドがブロックされている間に他の作業を続行します。</span><span class="sxs-lookup"><span data-stu-id="e4750-149">**Note**   You can use multithreading (for example, [**ThreadPool**](https://docs.microsoft.com/uwp/api/Windows.System.Threading) work items) to continue other work while the rendering thread is blocked.</span></span>

 

<span data-ttu-id="e4750-150">**Direct3D 11**</span><span class="sxs-lookup"><span data-stu-id="e4750-150">**Direct3D 11**</span></span>

```cpp
dxgiDevice->SetMaximumFrameLatency(1);
```

<span data-ttu-id="e4750-151">これで、レンダリングのためにバック バッファーを設定できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e4750-151">Now we can set up the back buffer for rendering.</span></span>

## <a name="configure-the-back-buffer-as-a-render-target"></a><span data-ttu-id="e4750-152">レンダー ターゲットとしてのバック バッファーの構成</span><span class="sxs-lookup"><span data-stu-id="e4750-152">Configure the back buffer as a render target</span></span>


<span data-ttu-id="e4750-153">最初に、バック バッファーへのハンドルを取得する必要があります </span><span class="sxs-lookup"><span data-stu-id="e4750-153">First we have to get a handle to the back buffer.</span></span> <span data-ttu-id="e4750-154">(注: バック バッファーが、DXGI スワップ チェーンによって所有されている DirectX 9 で Direct3D デバイスによって所有されている一方です。)レンダー ターゲットを作成して、レンダー ターゲットとして使用する Direct3D デバイスを説明し、*ビュー*バック バッファーを使用します。</span><span class="sxs-lookup"><span data-stu-id="e4750-154">(Note that the back buffer is owned by the DXGI swap chain, whereas in DirectX 9 it was owned by the Direct3D device.) Then we tell the Direct3D device to use it as the render target by creating a render target *view* using the back buffer.</span></span>

<span data-ttu-id="e4750-155">**Direct3D 11**</span><span class="sxs-lookup"><span data-stu-id="e4750-155">**Direct3D 11**</span></span>

```cpp
ComPtr<ID3D11Texture2D> backBuffer;
m_swapChain->GetBuffer(
    0,
    __uuidof(ID3D11Texture2D),
    &backBuffer
    );

// Create a render target view on the back buffer.
m_d3dDevice->CreateRenderTargetView(
    backBuffer.Get(),
    nullptr,
    &m_renderTargetView
    );
```

<span data-ttu-id="e4750-156">これでデバイス コンテキストが使えるようになりました。</span><span class="sxs-lookup"><span data-stu-id="e4750-156">Now the device context comes into play.</span></span> <span data-ttu-id="e4750-157">デバイス コンテキスト インターフェイスを使って、新しく作成したレンダー ターゲット ビューを使うように Direct3D に指示します。</span><span class="sxs-lookup"><span data-stu-id="e4750-157">We tell Direct3D to use our newly-created render target view by using the device context interface.</span></span> <span data-ttu-id="e4750-158">ウィンドウ全体をビューポートとしてターゲットにできるように、バック バッファーの幅と高さを取得します。</span><span class="sxs-lookup"><span data-stu-id="e4750-158">We'll retrieve the width and height of the back buffer so that we can target the whole window as our viewport.</span></span> <span data-ttu-id="e4750-159">バック バッファーはスワップ チェーンに関連付けられています。そのため、ウィンドウ サイズが変更された場合 (ユーザーがゲーム ウィンドウを別のモニターにドラッグした場合など) は、バック バッファーのサイズを変更し、一部の設定をやり直す必要があります。</span><span class="sxs-lookup"><span data-stu-id="e4750-159">Note that the back buffer is attached to the swap chain, so if the window size changes (for example, the user drags the game window to another monitor) the back buffer will need to be resized and some setup will need to be redone.</span></span>

<span data-ttu-id="e4750-160">**Direct3D 11**</span><span class="sxs-lookup"><span data-stu-id="e4750-160">**Direct3D 11**</span></span>

```cpp
D3D11_TEXTURE2D_DESC backBufferDesc = {0};
backBuffer->GetDesc(&backBufferDesc);

CD3D11_VIEWPORT viewport(
    0.0f,
    0.0f,
    static_cast<float>(backBufferDesc.Width),
    static_cast<float>(backBufferDesc.Height)
    );

m_d3dContext->RSSetViewports(1, &viewport);
```

<span data-ttu-id="e4750-161">デバイス ハンドルと全画面のレンダー ターゲットを作成したので、ジオメトリを読み込み、描画する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="e4750-161">Now that we have a device handle and a full-screen render target, we are ready to load and draw geometry.</span></span> <span data-ttu-id="e4750-162">引き続き[パート 2。レンダリング](simple-port-from-direct3d-9-to-11-1-part-2--rendering.md)します。</span><span class="sxs-lookup"><span data-stu-id="e4750-162">Continue to [Part 2: Rendering](simple-port-from-direct3d-9-to-11-1-part-2--rendering.md).</span></span>

 

 




