---
author: stevewhims
description: このトピックでは、C++/CX と C++/WinRT オブジェクト間の変換に使用できる 2 つのヘルパー関数について説明します。
title: C++/WinRT と C++/CX 間の相互運用
ms.author: stwhi
ms.date: 10/09/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10、uwp、標準、c++、cpp、winrt、プロジェクション、ポート、移行、相互運用、C++/CX
ms.localizationpriority: medium
ms.openlocfilehash: a21255299207bf6de06661e63936e6715c1f41c9
ms.sourcegitcommit: 310a4555fedd4246188a98b31f6c094abb33ec60
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2018
ms.locfileid: "5125980"
---
# <a name="interop-between-cwinrt-and-ccx"></a><span data-ttu-id="a4fdb-104">C++/WinRT と C++/CX 間の相互運用</span><span class="sxs-lookup"><span data-stu-id="a4fdb-104">Interop between C++/WinRT and C++/CX</span></span>

<span data-ttu-id="a4fdb-105">徐々 にコードを移植するための戦略、 [、C++/cli CX](/cpp/cppcx/visual-c-language-reference-c-cx)プロジェクトを[、C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)で説明[C への移行/C + から WinRT/CX](move-to-winrt-from-cx.md)します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-105">Strategies for gradually porting the code in your [C++/CX](/cpp/cppcx/visual-c-language-reference-c-cx) project to [C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt) are discussed in [Move to C++/WinRT from C++/CX](move-to-winrt-from-cx.md).</span></span>

<span data-ttu-id="a4fdb-106">このトピックでは、C++ 間の変換に使用できる 2 つのヘルパー関数 +/CX と C++/cli 同じプロジェクト内の WinRT オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-106">This topic shows two helper functions that you can use to convert between C++/CX and C++/WinRT objects within the same project.</span></span> <span data-ttu-id="a4fdb-107">それらを使用するには、2 つの言語プロジェクションを使用するコード間で相互運用機能またはから、C++ コードを移植するには、関数を使用できます/CX を C++/WinRT します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-107">You can use them to interop between code that uses the two language projections, or you can use the functions as you port your code from C++/CX to C++/WinRT.</span></span>

## <a name="fromcx-and-tocx-functions"></a><span data-ttu-id="a4fdb-108">from_cx and to_cx 関数</span><span class="sxs-lookup"><span data-stu-id="a4fdb-108">from_cx and to_cx functions</span></span>
<span data-ttu-id="a4fdb-109">以下のヘルパー関数では、C++/CX オブジェクトを同等の C++/WinRT オブジェクトに変換します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-109">The helper function below converts a C++/CX object to an equivalent C++/WinRT object.</span></span> <span data-ttu-id="a4fdb-110">この関数は、C++/CX オブジェクトを基礎となる [**IUnknown**](https://msdn.microsoft.com/library/windows/desktop/ms680509) インターフェイス ポインターにキャストします。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-110">The function casts a C++/CX object to its underlying [**IUnknown**](https://msdn.microsoft.com/library/windows/desktop/ms680509) interface pointer.</span></span> <span data-ttu-id="a4fdb-111">次に、このポインター上で [**QueryInterface**](https://msdn.microsoft.com/library/windows/desktop/ms682521) を呼び出し、C++/WinRT オブジェクトの既定のインターフェイスを照会します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-111">It then calls [**QueryInterface**](https://msdn.microsoft.com/library/windows/desktop/ms682521) on that pointer to query for the default interface of the C++/WinRT object.</span></span> <span data-ttu-id="a4fdb-112">**QueryInterface**は、C++/CX safe_cast 拡張と同等の Windows ランタイム アプリケーション バイナリ インターフェイス (ABI) です。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-112">**QueryInterface** is the Windows Runtime application binary interface (ABI) equivalent of the C++/CX safe_cast extension.</span></span> <span data-ttu-id="a4fdb-113">[**winrt::put_abi**](/uwp/cpp-ref-for-winrt/put-abi) 関数は、別の値に設定できるように C++/WinRT オブジェクトの基礎となる **IUnknown** インターフェイス ポインターのアドレスを取得します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-113">And, the [**winrt::put_abi**](/uwp/cpp-ref-for-winrt/put-abi) function retrieves the address of a C++/WinRT object's underlying **IUnknown** interface pointer so that it can be set to another value.</span></span>

```cppwinrt
template <typename T>
T from_cx(Platform::Object^ from)
{
    T to{ nullptr };

    winrt::check_hresult(reinterpret_cast<::IUnknown*>(from)
        ->QueryInterface(winrt::guid_of<T>(),
            reinterpret_cast<void**>(winrt::put_abi(to))));

    return to;
}
```

<span data-ttu-id="a4fdb-114">以下のヘルパー関数では、C++/WinRT オブジェクトを同等の C++/CX オブジェクトに変換します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-114">The helper function below converts a C++/WinRT object to an equivalent C++/CX object.</span></span> <span data-ttu-id="a4fdb-115">[**winrt::get_abi**](/uwp/cpp-ref-for-winrt/get-abi) 関数は、C++/WinRT オブジェクトの基礎となる **IUnknown** インターフェイスのポインターを取得します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-115">The [**winrt::get_abi**](/uwp/cpp-ref-for-winrt/get-abi) function retrieves a pointer to a C++/WinRT object's underlying **IUnknown** interface.</span></span> <span data-ttu-id="a4fdb-116">この関数は、C++/CX safe_cast 拡張を使用して要求された C++/CX 型を照会する前に、このポインターを C++/CX オブジェクトにキャストします。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-116">The function casts that pointer to a C++/CX object before using the C++/CX safe_cast extension to query for the requested C++/CX type.</span></span>

```cppwinrt
template <typename T>
T^ to_cx(winrt::Windows::Foundation::IUnknown const& from)
{
    return safe_cast<T^>(reinterpret_cast<Platform::Object^>(winrt::get_abi(from)));
}
```

## <a name="example-project-showing-the-two-helper-functions-in-use"></a><span data-ttu-id="a4fdb-117">使用中の 2 つのヘルパー関数を示す例のプロジェクト</span><span class="sxs-lookup"><span data-stu-id="a4fdb-117">Example project showing the two helper functions in use</span></span>

<span data-ttu-id="a4fdb-118">簡単な方法で、c++ のコードを徐々 に移植するシナリオを再現するには + CX プロジェクトを C++/WinRT、c++ のいずれかを使用して Visual Studio で新しいプロジェクトを作成して開始することができます/WinRT プロジェクト テンプレート (c++ [Visual Studio サポートを参照してください/WinRT、と VSIX](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-and-the-vsix))。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-118">To reproduce, in a simple way, the scenario of gradually porting the code in a C++/CX project to C++/WinRT, you can begin by creating a new project in Visual Studio using one of the C++/WinRT project templates (see [Visual Studio support for C++/WinRT, and the VSIX](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-and-the-vsix)).</span></span>

<span data-ttu-id="a4fdb-119">この例のプロジェクトも、C++ の間で可能性のある名前空間の競合を処理するために、コードの異なる断片の名前空間のエイリアスを使用する方法を示しています/WinRT プロジェクションと c++/cli/CX プロジェクション。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-119">This example project also illustrates how you can use namespace aliases for the different islands of code, in order to deal with otherwise potential namespace collisions between the C++/WinRT projection and the C++/CX projection.</span></span>

- <span data-ttu-id="a4fdb-120">**Visual C**を作成 \> **Windows ユニバーサル** > **コア アプリ (、C++/WinRT)** プロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-120">Create a **Visual C++** \> **Windows Universal** > **Core App (C++/WinRT)** project.</span></span>
- <span data-ttu-id="a4fdb-121">プロジェクトのプロパティで**C/C++** \> **一般的な** \> **Windows ランタイム拡張機能の使用** \> **[はい (/ZW)**。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-121">In project properties, **C/C++** \> **General** \> **Consume Windows Runtime Extension** \> **Yes (/ZW)**.</span></span> <span data-ttu-id="a4fdb-122">C++ プロジェクトのサポートを有効にしますこの/CX します。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-122">This turns on project support for C++/CX.</span></span>
- <span data-ttu-id="a4fdb-123">内容を置き換える`App.cpp`以下に示すコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="a4fdb-123">Replace the contents of `App.cpp` with the code listing below.</span></span>

```cppwinrt
// App.cpp
#include "pch.h"
#include <sstream>

namespace cx
{
    using namespace Windows::Foundation;
}

namespace winrt
{
    using namespace Windows;
    using namespace Windows::ApplicationModel::Core;
    using namespace Windows::Foundation;
    using namespace Windows::Foundation::Numerics;
    using namespace Windows::UI;
    using namespace Windows::UI::Core;
    using namespace Windows::UI::Composition;
}

template <typename T>
T from_cx(Platform::Object^ from)
{
    T to{ nullptr };

    winrt::check_hresult(reinterpret_cast<::IUnknown*>(from)
        ->QueryInterface(winrt::guid_of<T>(),
            reinterpret_cast<void**>(winrt::put_abi(to))));

    return to;
}

template <typename T>
T^ to_cx(winrt::Windows::Foundation::IUnknown const& from)
{
    return safe_cast<T^>(reinterpret_cast<Platform::Object^>(winrt::get_abi(from)));
}

struct App : winrt::implements<App, winrt::IFrameworkViewSource, winrt::IFrameworkView>
{
    winrt::CompositionTarget m_target{ nullptr };
    winrt::VisualCollection m_visuals{ nullptr };
    winrt::Visual m_selected{ nullptr };
    winrt::float2 m_offset{};

    winrt::IFrameworkView CreateView()
    {
        return *this;
    }

    void Initialize(winrt::CoreApplicationView const &)
    {
    }

    void Load(winrt::hstring const&)
    {
    }

    void Uninitialize()
    {
    }

    void Run()
    {
        winrt::CoreWindow window = winrt::CoreWindow::GetForCurrentThread();
        window.Activate();

        winrt::CoreDispatcher dispatcher = window.Dispatcher();
        dispatcher.ProcessEvents(winrt::CoreProcessEventsOption::ProcessUntilQuit);
    }

    void SetWindow(winrt::CoreWindow const & window)
    {
        winrt::Compositor compositor;
        winrt::ContainerVisual root = compositor.CreateContainerVisual();
        m_target = compositor.CreateTargetForCurrentView();
        m_target.Root(root);
        m_visuals = root.Children();

        window.PointerPressed({ this, &App::OnPointerPressed });
        window.PointerMoved({ this, &App::OnPointerMoved });

        window.PointerReleased([&](auto && ...)
        {
            m_selected = nullptr;
        });
    }

    void OnPointerPressed(IInspectable const &, winrt::PointerEventArgs const & args)
    {
        winrt::float2 const point = args.CurrentPoint().Position();

        for (winrt::Visual visual : m_visuals)
        {
            winrt::float3 const offset = visual.Offset();
            winrt::float2 const size = visual.Size();

            if (point.x >= offset.x &&
                point.x < offset.x + size.x &&
                point.y >= offset.y &&
                point.y < offset.y + size.y)
            {
                m_selected = visual;
                m_offset.x = offset.x - point.x;
                m_offset.y = offset.y - point.y;
            }
        }

        if (m_selected)
        {
            m_visuals.Remove(m_selected);
            m_visuals.InsertAtTop(m_selected);
        }
        else
        {
            AddVisual(point);
        }
    }

    void OnPointerMoved(IInspectable const &, winrt::PointerEventArgs const & args)
    {
        if (m_selected)
        {
            winrt::float2 const point = args.CurrentPoint().Position();

            m_selected.Offset(
            {
                point.x + m_offset.x,
                point.y + m_offset.y,
                0.0f
            });
        }
    }

    void AddVisual(winrt::float2 const point)
    {
        winrt::Compositor compositor = m_visuals.Compositor();
        winrt::SpriteVisual visual = compositor.CreateSpriteVisual();

        static winrt::Color colors[] =
        {
            { 0xDC, 0x5B, 0x9B, 0xD5 },
            { 0xDC, 0xED, 0x7D, 0x31 },
            { 0xDC, 0x70, 0xAD, 0x47 },
            { 0xDC, 0xFF, 0xC0, 0x00 }
        };

        static unsigned last = 0;
        unsigned const next = ++last % _countof(colors);
        visual.Brush(compositor.CreateColorBrush(colors[next]));

        float const BlockSize = 100.0f;

        visual.Size(
        {
            BlockSize,
            BlockSize
        });

        visual.Offset(
        {
            point.x - BlockSize / 2.0f,
            point.y - BlockSize / 2.0f,
            0.0f,
        });

        m_visuals.InsertAtTop(visual);

        m_selected = visual;
        m_offset.x = -BlockSize / 2.0f;
        m_offset.y = -BlockSize / 2.0f;
    }
};

int __stdcall wWinMain(HINSTANCE, HINSTANCE, PWSTR, int)
{
    winrt::init_apartment();

    winrt::Uri uri(L"http://aka.ms/cppwinrt");
    std::wstringstream wstringstream;
    wstringstream << L"C++/WinRT: " << uri.Domain().c_str() << std::endl;

    // Convert from a C++/WinRT type to a C++/CX type.
    cx::Uri^ cx = to_cx<cx::Uri>(uri);
    wstringstream << L"C++/CX: " << cx->Domain->Data() << std::endl;
    ::OutputDebugString(wstringstream.str().c_str());

    // Convert from a C++/CX type to a C++/WinRT type.
    winrt::Uri uri_from_cx = from_cx<winrt::Uri>(cx);
    WINRT_ASSERT(uri.Domain() == uri_from_cx.Domain());
    WINRT_ASSERT(uri == uri_from_cx);

    winrt::CoreApplication::Run(winrt::make<App>());
}
```

## <a name="important-apis"></a><span data-ttu-id="a4fdb-124">重要な API</span><span class="sxs-lookup"><span data-stu-id="a4fdb-124">Important APIs</span></span>
* [<span data-ttu-id="a4fdb-125">IUnknown インターフェイス</span><span class="sxs-lookup"><span data-stu-id="a4fdb-125">IUnknown interface</span></span>](https://msdn.microsoft.com/library/windows/desktop/ms680509)
* [<span data-ttu-id="a4fdb-126">QueryInterface 関数</span><span class="sxs-lookup"><span data-stu-id="a4fdb-126">QueryInterface function</span></span>](https://msdn.microsoft.com/library/windows/desktop/ms682521)
* [<span data-ttu-id="a4fdb-127">winrt::get_abi 関数</span><span class="sxs-lookup"><span data-stu-id="a4fdb-127">winrt::get_abi function</span></span>](/uwp/cpp-ref-for-winrt/get-abi)
* [<span data-ttu-id="a4fdb-128">winrt::put_abi 関数</span><span class="sxs-lookup"><span data-stu-id="a4fdb-128">winrt::put_abi function</span></span>](/uwp/cpp-ref-for-winrt/put-abi)

## <a name="related-topics"></a><span data-ttu-id="a4fdb-129">関連トピック</span><span class="sxs-lookup"><span data-stu-id="a4fdb-129">Related topics</span></span>
* [<span data-ttu-id="a4fdb-130">C++/CX</span><span class="sxs-lookup"><span data-stu-id="a4fdb-130">C++/CX</span></span>](/cpp/cppcx/visual-c-language-reference-c-cx)
* [<span data-ttu-id="a4fdb-131">C++/CX から C++/WinRT への移行</span><span class="sxs-lookup"><span data-stu-id="a4fdb-131">Move to C++/WinRT from C++/CX</span></span>](move-to-winrt-from-cx.md)
