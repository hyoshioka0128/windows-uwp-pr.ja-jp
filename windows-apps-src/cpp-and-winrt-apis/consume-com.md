---
description: このトピックでは、完全な Direct2D コードの例を使用し、C++/WinRT を使って COM クラスとインターフェイスを利用する方法を示します。
title: C++/WinRT での COM コンポーネントの使用
ms.date: 04/24/2019
ms.topic: article
keywords: windows 10、uwp、standard、c++、cpp、winrt、COM、コンポーネント、クラス、インターフェイス
ms.localizationpriority: medium
ms.openlocfilehash: 2c36c7b896b4d08240f08e85570110b45e0a9f3c
ms.sourcegitcommit: ba24a6237355119ef3e36687417f390c8722bd67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66421262"
---
# <a name="consume-com-components-with-cwinrt"></a><span data-ttu-id="4d60b-104">C++/WinRT での COM コンポーネントの使用</span><span class="sxs-lookup"><span data-stu-id="4d60b-104">Consume COM components with C++/WinRT</span></span>

<span data-ttu-id="4d60b-105">機能を使用することができます、 [C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt) DirectX Api のパフォーマンスの高い、2-d および 3-D グラフィックスなどの COM コンポーネントを使用するライブラリ。</span><span class="sxs-lookup"><span data-stu-id="4d60b-105">You can use the facilities of the [C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt) library to consume COM components, such as the high-performance 2-D and 3-D graphics of the DirectX APIs.</span></span> <span data-ttu-id="4d60b-106">C +/cli WinRT はパフォーマンスを損なうことがなく、DirectX を使用する最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="4d60b-106">C++/WinRT is the simplest way to use DirectX without compromising performance.</span></span> <span data-ttu-id="4d60b-107">このトピックでは、Direct2D のコード例を使用して、C + を使用する方法について説明/cli WinRT の COM クラスとインターフェイスを使用します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-107">This topic uses a Direct2D code example to show how to use C++/WinRT to consume COM classes and interfaces.</span></span> <span data-ttu-id="4d60b-108">同じの C + 内での COM および Windows ランタイム プログラミングを混在させることができます、もちろん、/cli WinRT プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="4d60b-108">You can, of course, mix COM and Windows Runtime programming within the same C++/WinRT project.</span></span>

<span data-ttu-id="4d60b-109">このトピックの最後には、最小限の Direct2D アプリケーションの完全なソース コードの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="4d60b-109">At the end of this topic, you'll find a full source code listing of a minimal Direct2D application.</span></span> <span data-ttu-id="4d60b-110">そのコードからの抜粋のリフトが C + を使用して COM コンポーネントを使用する方法を説明するために使用され/cli WinRT C + のさまざまな機能を使用して/cli WinRT ライブラリ。</span><span class="sxs-lookup"><span data-stu-id="4d60b-110">We'll lift excerpts from that code and use them to illustrate how to consume COM components using C++/WinRT using various facilities of the C++/WinRT library.</span></span>

## <a name="com-smart-pointers-winrtcomptruwpcpp-ref-for-winrtcom-ptr"></a><span data-ttu-id="4d60b-111">COM スマート ポインター ([**winrt::com_ptr**](/uwp/cpp-ref-for-winrt/com-ptr))</span><span class="sxs-lookup"><span data-stu-id="4d60b-111">COM smart pointers ([**winrt::com_ptr**](/uwp/cpp-ref-for-winrt/com-ptr))</span></span>

<span data-ttu-id="4d60b-112">COM をプログラムするオブジェクト (つまり、また、バック グラウンドでの Windows ランタイム Api では、COM の進化したものである場合は true) ではなく、インターフェイスを直接操作します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-112">When you program with COM, you work directly with interfaces rather than with objects (that's also true behind the scenes for Windows Runtime APIs, which are an evolution of COM).</span></span> <span data-ttu-id="4d60b-113">COM クラスの関数を呼び出すにはたとえば、アクティブ化する、クラス、インターフェイスを取得し、そのインターフェイスの関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-113">To call a function on a COM class, for example, you activate the class, get an interface back, and then you call functions on that interface.</span></span> <span data-ttu-id="4d60b-114">オブジェクトの状態にアクセスするにアクセスしないデータ メンバーは直接代わりに、インターフェイスのアクセサーとミューテーター関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-114">To access the state of an object, you don't access its data members directly; instead, you call accessor and mutator functions on an interface.</span></span>

<span data-ttu-id="4d60b-115">具体的には、インターフェイスとの対話について話している*ポインター*します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-115">To be more specific, we're talking about interacting with interface *pointers*.</span></span> <span data-ttu-id="4d60b-116">そのためでの COM スマート ポインター型の存在を利点がC++/WinRT&mdash;、 [ **winrt::com_ptr** ](/uwp/cpp-ref-for-winrt/com-ptr)型。</span><span class="sxs-lookup"><span data-stu-id="4d60b-116">And for that, we benefit from the existence of the COM smart pointer type in C++/WinRT&mdash;the [**winrt::com_ptr**](/uwp/cpp-ref-for-winrt/com-ptr) type.</span></span>

```cppwinrt
#include <d2d1_1.h>
...
winrt::com_ptr<ID2D1Factory1> factory;
```

<span data-ttu-id="4d60b-117">上記のコードに初期化されていないのスマート ポインターを宣言する方法を示しています、 [ **ID2D1Factory1** ](https://docs.microsoft.com/windows/desktop/api/d2d1_1/nn-d2d1_1-id2d1factory1) COM インターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="4d60b-117">The code above shows how to declare an uninitialized smart pointer to a [**ID2D1Factory1**](https://docs.microsoft.com/windows/desktop/api/d2d1_1/nn-d2d1_1-id2d1factory1) COM interface.</span></span> <span data-ttu-id="4d60b-118">まだ指しているために、スマート ポインターに初期化されていません、 **ID2D1Factory1** (それが指していないインターフェイスで)、実際のオブジェクトに属しているインターフェイス。</span><span class="sxs-lookup"><span data-stu-id="4d60b-118">The smart pointer is uninitialized, so it's not yet pointing to a **ID2D1Factory1** interface belonging to any actual object (it's not pointing to an interface at all).</span></span> <span data-ttu-id="4d60b-119">。 これを行う可能性がありますが、COM 参照カウントを指す、インターフェイスの所有するオブジェクトの有効期間を管理し、そのインターフェイスの関数を呼び出すことで、メディアを使用して機能があります (スマート ポインターをされている)。</span><span class="sxs-lookup"><span data-stu-id="4d60b-119">But it has the potential to do so; and (being a smart pointer) it has the ability via COM reference counting to manage the lifetime of the owning object of the interface that it points to, and to be the medium by which you call functions on that interface.</span></span>

## <a name="com-functions-that-return-an-interface-pointer-as-void"></a><span data-ttu-id="4d60b-120">としてインターフェイス ポインターを返す COM 関数**void**</span><span class="sxs-lookup"><span data-stu-id="4d60b-120">COM functions that return an interface pointer as **void**</span></span>

<span data-ttu-id="4d60b-121">呼び出すことができます、 [ **com_ptr::put_void** ](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrput_void-function)初期化されていないのスマート ポインターに書き込む関数には、生のポインターの基になります。</span><span class="sxs-lookup"><span data-stu-id="4d60b-121">You can call the [**com_ptr::put_void**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrput_void-function) function to write to an uninitialized smart pointer's underlying raw pointer.</span></span>

```cppwinrt
D2D1_FACTORY_OPTIONS options{ D2D1_DEBUG_LEVEL_NONE };
D2D1CreateFactory(
    D2D1_FACTORY_TYPE_SINGLE_THREADED,
    __uuidof(factory),
    &options,
    factory.put_void()
);
```

<span data-ttu-id="4d60b-122">呼び出し前のコード、 [ **D2D1CreateFactory** ](/windows/desktop/api/d2d1/nf-d2d1-d2d1createfactory)を返す関数、 **ID2D1Factory1**インターフェイス ポインターがその最後のパラメーターを使用して**void\* \*** 型。</span><span class="sxs-lookup"><span data-stu-id="4d60b-122">The code above calls the [**D2D1CreateFactory**](/windows/desktop/api/d2d1/nf-d2d1-d2d1createfactory) function, which returns an **ID2D1Factory1** interface pointer via its last parameter, which has **void\*\*** type.</span></span> <span data-ttu-id="4d60b-123">多くの COM 関数が返す、 **void\*\*** します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-123">Many COM functions return a **void\*\***.</span></span> <span data-ttu-id="4d60b-124">このような関数では、使用[ **com_ptr::put_void** ](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrput_void-function)示すようにします。</span><span class="sxs-lookup"><span data-stu-id="4d60b-124">For such functions, use [**com_ptr::put_void**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrput_void-function) as shown.</span></span>

## <a name="com-functions-that-return-a-specific-interface-pointer"></a><span data-ttu-id="4d60b-125">特定のインターフェイス ポインターを返す COM 関数</span><span class="sxs-lookup"><span data-stu-id="4d60b-125">COM functions that return a specific interface pointer</span></span>

<span data-ttu-id="4d60b-126">[ **D3D11CreateDevice** ](/windows/desktop/api/d3d11/nf-d3d11-d3d11createdevice)関数が返される、 [ **ID3D11Device** ](/windows/desktop/api/d3d11/nn-d3d11-id3d11device)が - 最後から 3 番目のパラメーターを使用してインターフェイス ポインター**ID3D11Device\* \*** 型。</span><span class="sxs-lookup"><span data-stu-id="4d60b-126">The [**D3D11CreateDevice**](/windows/desktop/api/d3d11/nf-d3d11-d3d11createdevice) function returns an [**ID3D11Device**](/windows/desktop/api/d3d11/nn-d3d11-id3d11device) interface pointer via its third-from-last parameter, which has **ID3D11Device\*\*** type.</span></span> <span data-ttu-id="4d60b-127">そのような特定のインターフェイス ポインターを返す関数を使用して[ **com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function)します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-127">For functions that return a specific interface pointer like that, use [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function).</span></span>

```cppwinrt
winrt::com_ptr<ID3D11Device> device;
D3D11CreateDevice(
    ...
    device.put(),
    ...);
```

<span data-ttu-id="4d60b-128">生の呼び出す方法を示しますこの 1 つ前に、のセクションのコード例**D2D1CreateFactory**関数。</span><span class="sxs-lookup"><span data-stu-id="4d60b-128">The code example in the section before this one shows how to call the raw **D2D1CreateFactory** function.</span></span> <span data-ttu-id="4d60b-129">実際には、このトピックのコード例を呼び出すときに**D2D1CreateFactory**生の API をラップするヘルパー関数テンプレートを使用して、コード例が実際に使用するように[ **com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function).</span><span class="sxs-lookup"><span data-stu-id="4d60b-129">But in fact, when the code example for this topic calls **D2D1CreateFactory**, it uses a helper function template that wraps the raw API, and so the code example actually uses [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function).</span></span>

```cppwinrt
winrt::com_ptr<ID2D1Factory1> factory;
D2D1CreateFactory(
    D2D1_FACTORY_TYPE_SINGLE_THREADED,
    options,
    factory.put());
```

## <a name="com-functions-that-return-an-interface-pointer-as-iunknown"></a><span data-ttu-id="4d60b-130">としてインターフェイス ポインターを返す COM 関数**IUnknown**</span><span class="sxs-lookup"><span data-stu-id="4d60b-130">COM functions that return an interface pointer as **IUnknown**</span></span>

<span data-ttu-id="4d60b-131">[ **DWriteCreateFactory** ](/windows/desktop/api/dwrite/nf-dwrite-dwritecreatefactory)関数では、DirectWrite ファクトリのインターフェイス ポインターを返しますが、最後のパラメーターを使用して[ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)型。</span><span class="sxs-lookup"><span data-stu-id="4d60b-131">The [**DWriteCreateFactory**](/windows/desktop/api/dwrite/nf-dwrite-dwritecreatefactory) function returns a DirectWrite factory interface pointer via its last parameter, which has [**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown) type.</span></span> <span data-ttu-id="4d60b-132">このような関数の場合、使用[ **com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function)、解釈をキャストするが、 **IUnknown**します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-132">For such a function, use [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function), but reinterpret cast that to **IUnknown**.</span></span>

```cppwinrt
DWriteCreateFactory(
    DWRITE_FACTORY_TYPE_SHARED,
    __uuidof(dwriteFactory2),
    reinterpret_cast<IUnknown**>(dwriteFactory2.put()));
```

## <a name="re-seat-a-winrtcomptr"></a><span data-ttu-id="4d60b-133">再度接続クライアント ライセンスを**winrt::com_ptr**</span><span class="sxs-lookup"><span data-stu-id="4d60b-133">Re-seat a **winrt::com_ptr**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d60b-134">ある場合、 [ **winrt::com_ptr** ](/uwp/cpp-ref-for-winrt/com-ptr)を既に接続されている (その内部の生のポインターは、ターゲットを既に持って) 再を別のオブジェクトを指す接続クライアント ライセンスするし、最初に割り当てる必要があります`nullptr`&mdash;次のコード例で示すようにします。</span><span class="sxs-lookup"><span data-stu-id="4d60b-134">If you have a [**winrt::com_ptr**](/uwp/cpp-ref-for-winrt/com-ptr) that's already seated (its internal raw pointer already has a target) and you want to re-seat it to point to a different object, then you first need to assign `nullptr` to it&mdash;as shown in the code example below.</span></span> <span data-ttu-id="4d60b-135">ない場合は、既に取り付けられていない**com_ptr**に対処する問題を描画 (を呼び出すと[ **com_ptr::put** ](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function)または[ **com_ptr:。put_void**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrput_void-function)) によって、その内部ポインターが null でないことをアサートします。</span><span class="sxs-lookup"><span data-stu-id="4d60b-135">If you don't, then an already-seated **com_ptr** will draw the issue to your attention (when you call [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptr_put-function) or [**com_ptr::put_void**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrput_void-function)) by asserting that its internal pointer is not null.</span></span>

```cppwinrt
winrt::com_ptr<ID2D1SolidColorBrush> brush;
...
    brush.put()
...
brush = nullptr; // Important because we're about to re-seat
target->CreateSolidColorBrush(
    color_orange,
    D2D1::BrushProperties(0.8f),
    brush.put()));
```

## <a name="handle-hresult-error-codes"></a><span data-ttu-id="4d60b-136">HRESULT エラー コードを処理します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-136">Handle HRESULT error codes</span></span>

<span data-ttu-id="4d60b-137">COM 関数の場合から返された HRESULT の値を確認し、エラー コードを表すことは、例外をスロー、 [ **winrt::check_hresult**](/uwp/cpp-ref-for-winrt/error-handling/check-hresult)します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-137">To check the value of a HRESULT returned from a COM function, and throw an exception in the event that it represents an error code, call [**winrt::check_hresult**](/uwp/cpp-ref-for-winrt/error-handling/check-hresult).</span></span>

```cppwinrt
winrt::check_hresult(D2D1CreateFactory(
    D2D1_FACTORY_TYPE_SINGLE_THREADED,
    __uuidof(factory),
    options,
    factory.put_void()));
```

## <a name="com-functions-that-take-a-specific-interface-pointer"></a><span data-ttu-id="4d60b-138">特定のインターフェイス ポインターを使用する COM 関数</span><span class="sxs-lookup"><span data-stu-id="4d60b-138">COM functions that take a specific interface pointer</span></span>

<span data-ttu-id="4d60b-139">呼び出すことができます、 [ **com_ptr::get** ](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrget-function)関数に渡す、 **com_ptr**を同じ型の特定のインターフェイス ポインターを受け取る関数。</span><span class="sxs-lookup"><span data-stu-id="4d60b-139">You can call the [**com_ptr::get**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrget-function) function to pass your **com_ptr** to a function that takes a specific interface pointer of the same type.</span></span>

```cppwinrt
... ExampleFunction(
    winrt::com_ptr<ID2D1Factory1> const& factory,
    winrt::com_ptr<IDXGIDevice> const& dxdevice)
{
    ...
    winrt::check_hresult(factory->CreateDevice(dxdevice.get(), ...));
    ...
}
```

## <a name="com-functions-that-take-an-iunknown-interface-pointer"></a><span data-ttu-id="4d60b-140">COM 関数を受け取る、 **IUnknown**インターフェイス ポインター</span><span class="sxs-lookup"><span data-stu-id="4d60b-140">COM functions that take an **IUnknown** interface pointer</span></span>

<span data-ttu-id="4d60b-141">呼び出すことができます、 [ **winrt::get_unknown** ](/uwp/cpp-ref-for-winrt/windows-foundation-iunknown#get_unknown-function) free 関数に渡す、 **com_ptr**を受け取る関数に、 **IUnknown**インターフェイスポインター。</span><span class="sxs-lookup"><span data-stu-id="4d60b-141">You can call the [**winrt::get_unknown**](/uwp/cpp-ref-for-winrt/windows-foundation-iunknown#get_unknown-function) free function to pass your **com_ptr** to a function that takes an **IUnknown** interface pointer.</span></span>

```cppwinrt
winrt::check_hresult(factory->CreateSwapChainForCoreWindow(
    ...
    winrt::get_unknown(CoreWindow::GetForCurrentThread()),
    ...));
```

## <a name="passing-and-returning-com-smart-pointers"></a><span data-ttu-id="4d60b-142">受け渡しおよび返却 COM スマート ポインター</span><span class="sxs-lookup"><span data-stu-id="4d60b-142">Passing and returning COM smart pointers</span></span>

<span data-ttu-id="4d60b-143">形式で COM スマート ポインターを取り込む関数、 **winrt::com_ptr**定数の参照渡しまたは参照渡し、これを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d60b-143">A function taking a COM smart pointer in the form of a **winrt::com_ptr** should do so by constant reference, or by reference.</span></span>

```cppwinrt
... GetDxgiFactory(winrt::com_ptr<ID3D11Device> const& device) ...

... CreateDevice(..., winrt::com_ptr<ID3D11Device>& device) ...
```

<span data-ttu-id="4d60b-144">返す関数、 **winrt::com_ptr**値によってこれを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d60b-144">A function that returns a **winrt::com_ptr** should do so by value.</span></span>

```cppwinrt
winrt::com_ptr<ID2D1Factory1> CreateFactory() ...
```

## <a name="query-a-com-smart-pointer-for-a-different-interface"></a><span data-ttu-id="4d60b-145">別のインターフェイスの COM スマート ポインターをクエリします。</span><span class="sxs-lookup"><span data-stu-id="4d60b-145">Query a COM smart pointer for a different interface</span></span>

<span data-ttu-id="4d60b-146">使用することができます、 [ **com_ptr::as** ](/uwp/cpp-ref-for-winrt/com-ptr#com_ptras-function)別のインターフェイスの COM スマート ポインターのクエリを実行する関数。</span><span class="sxs-lookup"><span data-stu-id="4d60b-146">You can use the [**com_ptr::as**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptras-function) function to query a COM smart pointer for a different interface.</span></span> <span data-ttu-id="4d60b-147">関数は、クエリが成功しなかった場合、例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="4d60b-147">The function throws an exception if the query doesn't succeed.</span></span>

```cppwinrt
void ExampleFunction(winrt::com_ptr<ID3D11Device> const& device)
{
    ...
    winrt::com_ptr<IDXGIDevice> const dxdevice{ device.as<IDXGIDevice>() };
    ...
}
```

<span data-ttu-id="4d60b-148">また、使用して[ **com_ptr::try_as**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrtry_as-function)、に対して確認できる値を返す`nullptr`にクエリが成功したかどうかを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4d60b-148">Alternatively, use [**com_ptr::try_as**](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrtry_as-function), which returns a value that you can check against `nullptr` to see whether the query succeeded.</span></span>

## <a name="full-source-code-listing-of-a-minimal-direct2d-application"></a><span data-ttu-id="4d60b-149">Direct2D アプリケーションに最小限の完全なソース コードの一覧</span><span class="sxs-lookup"><span data-stu-id="4d60b-149">Full source code listing of a minimal Direct2D application</span></span>

<span data-ttu-id="4d60b-150">ビルドし、Visual Studio でこのソース コード例、最初を実行する場合は、作成、新しい**Core アプリ (C +/cli WinRT)** します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-150">If you want to build and run this source code example then first, in Visual Studio, create a new **Core App (C++/WinRT)**.</span></span> <span data-ttu-id="4d60b-151">`Direct2D` プロジェクトの適切な名前ですが、という名前を好きなデザイン。</span><span class="sxs-lookup"><span data-stu-id="4d60b-151">`Direct2D` is a reasonable name for the project, but you can name it anything you like.</span></span> <span data-ttu-id="4d60b-152">開いている`App.cpp`内容をすべてを削除し、以下のリストを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="4d60b-152">Open `App.cpp`, delete its entire contents, and paste in the listing below.</span></span>

<span data-ttu-id="4d60b-153">使用して次のコード、 [winrt::com_ptr::capture 関数](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrcapture-function)可能な場合。</span><span class="sxs-lookup"><span data-stu-id="4d60b-153">The code below uses the [winrt::com_ptr::capture function](/uwp/cpp-ref-for-winrt/com-ptr#com_ptrcapture-function) where possible.</span></span>

```cppwinrt
#include "pch.h"
#include <d2d1_1.h>
#include <d3d11.h>
#include <dxgi1_2.h>
#include <winrt/Windows.Graphics.Display.h>

using namespace winrt;

using namespace Windows;
using namespace Windows::ApplicationModel::Core;
using namespace Windows::UI;
using namespace Windows::UI::Core;
using namespace Windows::Graphics::Display;

namespace
{
    winrt::com_ptr<ID2D1Factory1> CreateFactory()
    {
        D2D1_FACTORY_OPTIONS options{};

#ifdef _DEBUG
        options.debugLevel = D2D1_DEBUG_LEVEL_INFORMATION;
#endif

        winrt::com_ptr<ID2D1Factory1> factory;

        winrt::check_hresult(D2D1CreateFactory(
            D2D1_FACTORY_TYPE_SINGLE_THREADED,
            options,
            factory.put()));

        return factory;
    }

    HRESULT CreateDevice(D3D_DRIVER_TYPE const type, winrt::com_ptr<ID3D11Device>& device)
    {
        WINRT_ASSERT(!device);

        return D3D11CreateDevice(
            nullptr,
            type,
            nullptr,
            D3D11_CREATE_DEVICE_BGRA_SUPPORT,
            nullptr, 0,
            D3D11_SDK_VERSION,
            device.put(),
            nullptr,
            nullptr);
    }

    winrt::com_ptr<ID3D11Device> CreateDevice()
    {
        winrt::com_ptr<ID3D11Device> device;
        HRESULT hr{ CreateDevice(D3D_DRIVER_TYPE_HARDWARE, device) };

        if (DXGI_ERROR_UNSUPPORTED == hr)
        {
            hr = CreateDevice(D3D_DRIVER_TYPE_WARP, device);
        }

        winrt::check_hresult(hr);
        return device;
    }

    winrt::com_ptr<ID2D1DeviceContext> CreateRenderTarget(
        winrt::com_ptr<ID2D1Factory1> const& factory,
        winrt::com_ptr<ID3D11Device> const& device)
    {
        WINRT_ASSERT(factory);
        WINRT_ASSERT(device);

        winrt::com_ptr<IDXGIDevice> const dxdevice{ device.as<IDXGIDevice>() };

        winrt::com_ptr<ID2D1Device> d2device;
        winrt::check_hresult(factory->CreateDevice(dxdevice.get(), d2device.put()));

        winrt::com_ptr<ID2D1DeviceContext> target;
        winrt::check_hresult(d2device->CreateDeviceContext(D2D1_DEVICE_CONTEXT_OPTIONS_NONE, target.put()));
        return target;
    }

    winrt::com_ptr<IDXGIFactory2> GetDxgiFactory(winrt::com_ptr<ID3D11Device> const& device)
    {
        WINRT_ASSERT(device);

        winrt::com_ptr<IDXGIDevice> const dxdevice{ device.as<IDXGIDevice>() };

        winrt::com_ptr<IDXGIAdapter> adapter;
        winrt::check_hresult(dxdevice->GetAdapter(adapter.put()));

        winrt::com_ptr<IDXGIFactory2> factory;
        factory.capture(adapter, &IDXGIAdapter::GetParent);
        return factory;
    }

    void CreateDeviceSwapChainBitmap(
        winrt::com_ptr<IDXGISwapChain1> const& swapchain,
        winrt::com_ptr<ID2D1DeviceContext> const& target)
    {
        WINRT_ASSERT(swapchain);
        WINRT_ASSERT(target);

        winrt::com_ptr<IDXGISurface> surface;
        surface.capture(swapchain, &IDXGISwapChain1::GetBuffer, 0);

        D2D1_BITMAP_PROPERTIES1 const props{ D2D1::BitmapProperties1(
            D2D1_BITMAP_OPTIONS_TARGET | D2D1_BITMAP_OPTIONS_CANNOT_DRAW,
            D2D1::PixelFormat(DXGI_FORMAT_B8G8R8A8_UNORM, D2D1_ALPHA_MODE_IGNORE)) };

        winrt::com_ptr<ID2D1Bitmap1> bitmap;

        winrt::check_hresult(target->CreateBitmapFromDxgiSurface(surface.get(),
            props,
            bitmap.put()));

        target->SetTarget(bitmap.get());
    }

    winrt::com_ptr<IDXGISwapChain1> CreateSwapChainForCoreWindow(winrt::com_ptr<ID3D11Device> const& device)
    {
        WINRT_ASSERT(device);

        winrt::com_ptr<IDXGIFactory2> const factory{ GetDxgiFactory(device) };

        DXGI_SWAP_CHAIN_DESC1 props{};
        props.Format = DXGI_FORMAT_B8G8R8A8_UNORM;
        props.SampleDesc.Count = 1;
        props.BufferUsage = DXGI_USAGE_RENDER_TARGET_OUTPUT;
        props.BufferCount = 2;
        props.SwapEffect = DXGI_SWAP_EFFECT_FLIP_SEQUENTIAL;

        winrt::com_ptr<IDXGISwapChain1> swapChain;

        winrt::check_hresult(factory->CreateSwapChainForCoreWindow(
            device.get(),
            winrt::get_unknown(CoreWindow::GetForCurrentThread()),
            &props,
            nullptr, // all or nothing
            swapChain.put()));

        return swapChain;
    }

    constexpr D2D1_COLOR_F color_white{ 1.0f,  1.0f,  1.0f,  1.0f };
    constexpr D2D1_COLOR_F color_orange{ 0.92f,  0.38f,  0.208f,  1.0f };
}

struct App : implements<App, IFrameworkViewSource, IFrameworkView>
{
    winrt::com_ptr<ID2D1Factory1> m_factory;
    winrt::com_ptr<ID2D1DeviceContext> m_target;
    winrt::com_ptr<IDXGISwapChain1> m_swapChain;
    winrt::com_ptr<ID2D1SolidColorBrush> m_brush;
    float m_dpi{};

    IFrameworkView CreateView()
    {
        return *this;
    }

    void Initialize(CoreApplicationView const&)
    {
    }

    void Load(hstring const&)
    {
        CoreWindow const window{ CoreWindow::GetForCurrentThread() };

        window.SizeChanged([&](auto&&...)
        {
            if (m_target)
            {
                ResizeSwapChainBitmap();
                Render();
            }
        });

        DisplayInformation const display{ DisplayInformation::GetForCurrentView() };
        m_dpi = display.LogicalDpi();

        display.DpiChanged([&](DisplayInformation const& display, IInspectable const&)
        {
            if (m_target)
            {
                m_dpi = display.LogicalDpi();
                m_target->SetDpi(m_dpi, m_dpi);
                CreateDeviceSizeResources();
                Render();
            }
        });

        m_factory = CreateFactory();
        CreateDeviceIndependentResources();
    }

    void Uninitialize()
    {
    }

    void Run()
    {
        CoreWindow const window{ CoreWindow::GetForCurrentThread() };
        window.Activate();

        Render();
        CoreDispatcher const dispatcher{ window.Dispatcher() };
        dispatcher.ProcessEvents(CoreProcessEventsOption::ProcessUntilQuit);
    }

    void SetWindow(CoreWindow const&) {}

    void Draw()
    {
        m_target->Clear(color_white);

        D2D1_SIZE_F const size{ m_target->GetSize() };
        D2D1_RECT_F const rect{ 100.0f, 100.0f, size.width - 100.0f, size.height - 100.0f };
        m_target->DrawRectangle(rect, m_brush.get(), 100.0f);

        char buffer[1024];
        (void)snprintf(buffer, sizeof(buffer), "Draw %.2f x %.2f @ %.2f\n", size.width, size.height, m_dpi);
        ::OutputDebugStringA(buffer);
    }

    void Render()
    {
        if (!m_target)
        {
            winrt::com_ptr<ID3D11Device> const device{ CreateDevice() };
            m_target = CreateRenderTarget(m_factory, device);
            m_swapChain = CreateSwapChainForCoreWindow(device);

            CreateDeviceSwapChainBitmap(m_swapChain, m_target);

            m_target->SetDpi(m_dpi, m_dpi);

            CreateDeviceResources();
            CreateDeviceSizeResources();
        }

        m_target->BeginDraw();
        Draw();
        m_target->EndDraw();

        HRESULT const hr{ m_swapChain->Present(1, 0) };

        if (S_OK != hr && DXGI_STATUS_OCCLUDED != hr)
        {
            ReleaseDevice();
        }
    }

    void ReleaseDevice()
    {
        m_target = nullptr;
        m_swapChain = nullptr;

        ReleaseDeviceResources();
    }

    void ResizeSwapChainBitmap()
    {
        WINRT_ASSERT(m_target);
        WINRT_ASSERT(m_swapChain);

        m_target->SetTarget(nullptr);

        if (S_OK == m_swapChain->ResizeBuffers(0, // all buffers
            0, 0, // client area
            DXGI_FORMAT_UNKNOWN, // preserve format
            0)) // flags
        {
            CreateDeviceSwapChainBitmap(m_swapChain, m_target);
            CreateDeviceSizeResources();
        }
        else
        {
            ReleaseDevice();
        }
    }

    void CreateDeviceIndependentResources()
    {
    }

    void CreateDeviceResources()
    {
        winrt::check_hresult(m_target->CreateSolidColorBrush(
            color_orange,
            D2D1::BrushProperties(0.8f),
            m_brush.put()));
    }

    void CreateDeviceSizeResources()
    {
    }

    void ReleaseDeviceResources()
    {
        m_brush = nullptr;
    }
};

int __stdcall wWinMain(HINSTANCE, HINSTANCE, PWSTR, int)
{
    CoreApplication::Run(winrt::make<App>());
}
```

## <a name="working-with-com-types-such-as-bstr-and-variant"></a><span data-ttu-id="4d60b-154">BSTR や VARIANT などの COM 型の使用</span><span class="sxs-lookup"><span data-stu-id="4d60b-154">Working with COM types, such as BSTR and VARIANT</span></span>

<span data-ttu-id="4d60b-155">ご覧のとおり、C +/cli WinRT を実装して、COM インターフェイスを呼び出すことのサポートを提供します。</span><span class="sxs-lookup"><span data-stu-id="4d60b-155">As you can see, C++/WinRT provides support for both implementing and calling COM interfaces.</span></span> <span data-ttu-id="4d60b-156">BSTR および VARIANT などの COM 型の使用をお勧めしますが提供するラッパーを使用すること、 [Windows 実装ライブラリ (が)](https://github.com/Microsoft/wil)など**wil::unique_bstr**と**wil::unique_バリアント**(リソースの有効期間管理)。</span><span class="sxs-lookup"><span data-stu-id="4d60b-156">For using COM types, such as BSTR and VARIANT, we recommend that you use wrappers provided by the [Windows Implementation Libraries (WIL)](https://github.com/Microsoft/wil), such as **wil::unique_bstr** and **wil::unique_variant** (which manage resources lifetimes).</span></span>

<span data-ttu-id="4d60b-157">[WIL](https://github.com/Microsoft/wil) Active Template Library (ATL) と、ビジュアルなどのフレームワークよりも優先されますC++コンパイラの COM をサポートします。</span><span class="sxs-lookup"><span data-stu-id="4d60b-157">[WIL](https://github.com/Microsoft/wil) supersedes frameworks such as the Active Template Library (ATL), and the Visual C++ compiler's COM Support.</span></span> <span data-ttu-id="4d60b-158">独自のラッパーを記述または (適切な Api) と、未加工の形式で BSTR や VARIANT などの COM 型を使用することお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4d60b-158">And we recommend it over writing your own wrappers, or using COM types such as BSTR and VARIANT in their raw form (together with the appropriate APIs).</span></span>

## <a name="important-apis"></a><span data-ttu-id="4d60b-159">重要な API</span><span class="sxs-lookup"><span data-stu-id="4d60b-159">Important APIs</span></span>
* [<span data-ttu-id="4d60b-160">winrt::check_hresult 関数</span><span class="sxs-lookup"><span data-stu-id="4d60b-160">winrt::check_hresult function</span></span>](/uwp/cpp-ref-for-winrt/error-handling/check-hresult)
* [<span data-ttu-id="4d60b-161">winrt::com_ptr 構造体のテンプレート</span><span class="sxs-lookup"><span data-stu-id="4d60b-161">winrt::com_ptr struct template</span></span>](/uwp/cpp-ref-for-winrt/com-ptr)
* [<span data-ttu-id="4d60b-162">winrt::Windows::Foundation::IUnknown 構造体</span><span class="sxs-lookup"><span data-stu-id="4d60b-162">winrt::Windows::Foundation::IUnknown struct</span></span>](/uwp/cpp-ref-for-winrt/windows-foundation-iunknown)
