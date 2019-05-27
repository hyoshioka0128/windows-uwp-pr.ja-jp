---
title: Win32 でのビジュアル層の使用
description: Win32 デスクトップ アプリの UI を強化するために、ビジュアル レイヤーを使用します。
template: detail.hbs
ms.date: 03/18/2019
ms.topic: article
keywords: UWP、レンダリング、合成、win32
ms.author: jimwalk
author: jwmsft
ms.localizationpriority: medium
ms.openlocfilehash: c9b4ec38b0dd1f6eca3f43cfded74c6292c08100
ms.sourcegitcommit: d1c3e13de3da3f7dce878b3735ee53765d0df240
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66215195"
---
# <a name="using-the-visual-layer-with-win32"></a><span data-ttu-id="e67cf-104">Win32 でのビジュアル層の使用</span><span class="sxs-lookup"><span data-stu-id="e67cf-104">Using the Visual Layer with Win32</span></span>

<span data-ttu-id="e67cf-105">Windows ランタイムの合成 Api を使用することができます (とも呼ばれる、[ビジュアル層](/windows/uwp/composition/visual-layer)) Win32 アプリを Windows 10 のユーザー用に光を最新のエクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-105">You can use Windows Runtime Composition APIs (also called the [Visual layer](/windows/uwp/composition/visual-layer)) in your Win32 apps to create modern experiences that light up for Windows 10 users.</span></span>

<span data-ttu-id="e67cf-106">このチュートリアルの完成したコードは GitHub で入手できます。[Win32 HelloComposition サンプル](https://github.com/Microsoft/Windows.UI.Composition-Win32-Samples/tree/master/cpp/HelloComposition)します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-106">The complete code for this tutorial is available on GitHub: [Win32 HelloComposition sample](https://github.com/Microsoft/Windows.UI.Composition-Win32-Samples/tree/master/cpp/HelloComposition).</span></span>

<span data-ttu-id="e67cf-107">その UI コンポジションを正確に制御を必要とするユニバーサルの Windows アプリケーションへのアクセスがある、 [Windows.UI.Composition](/uwp/api/windows.ui.composition) UI の構成し、表示方法をきめ細かに制御する名前空間。</span><span class="sxs-lookup"><span data-stu-id="e67cf-107">Universal Windows Applications that need precise control over their UI composition have access to the [Windows.UI.Composition](/uwp/api/windows.ui.composition) namespace to exert fine grained control over how their UI is composed and rendered.</span></span> <span data-ttu-id="e67cf-108">この合成 API はただしでは、UWP アプリに限定されません。</span><span class="sxs-lookup"><span data-stu-id="e67cf-108">This composition API is not limited to UWP apps, however.</span></span> <span data-ttu-id="e67cf-109">Win32 デスクトップ アプリケーションでは、UWP と Windows 10 の最新のコンポジション システムを利用できます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-109">Win32 desktop applications can take advantage of the modern composition systems in UWP and Windows 10.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e67cf-110">前提条件</span><span class="sxs-lookup"><span data-stu-id="e67cf-110">Prerequisites</span></span>

<span data-ttu-id="e67cf-111">UWP API をホストしているが、これらの前提条件です。</span><span class="sxs-lookup"><span data-stu-id="e67cf-111">The UWP hosting API has these prerequisites.</span></span>

- <span data-ttu-id="e67cf-112">Win32 でも UWP を使用してアプリ開発の知識があると仮定します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-112">We assume that you have some familiarity with app development using Win32 and UWP.</span></span> <span data-ttu-id="e67cf-113">For more info, see:</span><span class="sxs-lookup"><span data-stu-id="e67cf-113">For more info, see:</span></span>
  - [<span data-ttu-id="e67cf-114">Win32 の概要とC++</span><span class="sxs-lookup"><span data-stu-id="e67cf-114">Get Started with Win32 and C++</span></span>](/windows/desktop/learnwin32/learn-to-program-for-windows)
  - [<span data-ttu-id="e67cf-115">Windows 10 アプリを概要します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-115">Get started with Windows 10 apps</span></span>](/windows/uwp/get-started/)
  - [<span data-ttu-id="e67cf-116">Windows 10 のデスクトップ アプリケーションを拡張します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-116">Enhance your desktop application for Windows 10</span></span>](/windows/uwp/porting/desktop-to-uwp-enhance)
- <span data-ttu-id="e67cf-117">Windows 10 バージョン 1803 以降</span><span class="sxs-lookup"><span data-stu-id="e67cf-117">Windows 10 version 1803 or later</span></span>
- <span data-ttu-id="e67cf-118">Windows 10 SDK 17134 またはそれ以降</span><span class="sxs-lookup"><span data-stu-id="e67cf-118">Windows 10 SDK 17134 or later</span></span>

## <a name="how-to-use-composition-apis-from-a-win32-desktop-application"></a><span data-ttu-id="e67cf-119">Win32 デスクトップ アプリケーションから合成 Api を使用する方法</span><span class="sxs-lookup"><span data-stu-id="e67cf-119">How to use Composition APIs from a Win32 desktop application</span></span>

<span data-ttu-id="e67cf-120">このチュートリアルでは、単純な Win32 を作成C++アプリを UWP の合成要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-120">In this tutorial, you create a simple Win32 C++ app and add UWP Composition elements to it.</span></span> <span data-ttu-id="e67cf-121">焦点は正しく、プロジェクトの構成、相互運用機能のコードの作成、および Windows 合成 Api を使用して単純なものを描画します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-121">The focus is on correctly configuring the project, creating the interop code, and drawing something simple using Windows Composition APIs.</span></span> <span data-ttu-id="e67cf-122">次のような完成したアプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-122">The finished app looks like this.</span></span>

![実行中のアプリの UI](images/visual-layer-interop/win32-comp-interop-app-ui.png)

## <a name="create-a-c-win32-project-in-visual-studio"></a><span data-ttu-id="e67cf-124">作成、 C++ Visual Studio での Win32 プロジェクト</span><span class="sxs-lookup"><span data-stu-id="e67cf-124">Create a C++ Win32 project in Visual Studio</span></span>

<span data-ttu-id="e67cf-125">最初の手順では、Visual Studio で、Win32 アプリ プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-125">The first step is to create the Win32 app project in Visual Studio.</span></span>

<span data-ttu-id="e67cf-126">新しい Win32 アプリケーション プロジェクトを作成するC++という_HelloComposition_:</span><span class="sxs-lookup"><span data-stu-id="e67cf-126">To create a new Win32 Application project in C++ named _HelloComposition_:</span></span>

1. <span data-ttu-id="e67cf-127">Visual Studio を開き、選択**ファイル** > **新規** > **プロジェクト**します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-127">Open Visual Studio and select **File** > **New** > **Project**.</span></span>

    <span data-ttu-id="e67cf-128">**新しいプロジェクト**ダイアログ ボックスが開きます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-128">The **New Project** dialog opens.</span></span>
1. <span data-ttu-id="e67cf-129">下、**インストール済み**カテゴリで、展開、 **Visual C++** ノードをクリックして**Windows デスクトップ**します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-129">Under the **Installed** category, expand the **Visual C++** node, and then select **Windows Desktop**.</span></span>
1. <span data-ttu-id="e67cf-130">選択、 **Windows デスクトップ アプリケーション**テンプレート。</span><span class="sxs-lookup"><span data-stu-id="e67cf-130">Select the **Windows Desktop Application** template.</span></span>
1. <span data-ttu-id="e67cf-131">名前を入力します_HelloComposition_、 をクリックし、 **OK**します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-131">Enter the name _HelloComposition_, then click **OK**.</span></span>

    <span data-ttu-id="e67cf-132">Visual Studio では、プロジェクトを作成し、メイン アプリケーション ファイルのエディターを開きます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-132">Visual Studio creates the project and opens the editor for the main app file.</span></span>

## <a name="configure-the-project-to-use-windows-runtime-apis"></a><span data-ttu-id="e67cf-133">Windows ランタイム Api を使用してプロジェクトを構成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-133">Configure the project to use Windows Runtime APIs</span></span>

<span data-ttu-id="e67cf-134">使用して Windows ランタイム (WinRT) アプリの Win32 Api を使用するC++/WinRT です。</span><span class="sxs-lookup"><span data-stu-id="e67cf-134">To use Windows Runtime (WinRT) APIs in your Win32 app, we use C++/WinRT.</span></span> <span data-ttu-id="e67cf-135">追加する Visual Studio プロジェクトを構成する必要があるC++/WinRT サポートします。</span><span class="sxs-lookup"><span data-stu-id="e67cf-135">You need to configure your Visual Studio project to add C++/WinRT support.</span></span>

<span data-ttu-id="e67cf-136">(詳細については、次を参照してください。[概要C++/WinRT - 追加する Windows デスクトップ アプリケーション プロジェクトを変更するC++/WinRT サポート](/windows/uwp/cpp-and-winrt-apis/get-started.md#modify-a-windows-desktop-application-project-to-add-cwinrt-support))。</span><span class="sxs-lookup"><span data-stu-id="e67cf-136">(For details, see [Get started with C++/WinRT - Modify a Windows Desktop application project to add C++/WinRT support](/windows/uwp/cpp-and-winrt-apis/get-started.md#modify-a-windows-desktop-application-project-to-add-cwinrt-support)).</span></span>

1. <span data-ttu-id="e67cf-137">**プロジェクト**] メニューの [プロジェクトのプロパティを開きます (_HelloComposition プロパティ_) を指定した値に設定は、次の設定を確認してください。</span><span class="sxs-lookup"><span data-stu-id="e67cf-137">From the **Project** menu, open the project properties (_HelloComposition Properties_) and ensure the following settings are set to the specified values:</span></span>

    - <span data-ttu-id="e67cf-138">**構成**、_すべての構成_します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-138">For **Configuration**, select _All Configurations_.</span></span> <span data-ttu-id="e67cf-139">**プラットフォーム**、_すべてのプラットフォーム_します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-139">For **Platform**, select _All Platforms_.</span></span>
    - <span data-ttu-id="e67cf-140">**構成プロパティ** > **全般** > **Windows SDK バージョン** = _10.0.17763.0_以上</span><span class="sxs-lookup"><span data-stu-id="e67cf-140">**Configuration Properties** > **General** > **Windows SDK Version** = _10.0.17763.0_ or greater</span></span>

    ![SDK バージョンを設定](images/visual-layer-interop/sdk-version.png)

    - <span data-ttu-id="e67cf-142">**C/C++** > **言語** >   **C++言語標準** = _ISO C++ 17 標準 (/stf:c + + 17)_</span><span class="sxs-lookup"><span data-stu-id="e67cf-142">**C/C++** > **Language** > **C++ Language Standard** = _ISO C++ 17 Standard (/stf:c++17)_</span></span>

    ![標準的な言語を設定します。](images/visual-layer-interop/language-standard.png)

    - <span data-ttu-id="e67cf-144">**リンカー** > **入力** > **追加の依存関係**含める必要があります"_windowsapp.lib_"。</span><span class="sxs-lookup"><span data-stu-id="e67cf-144">**Linker** > **Input** > **Additional Dependencies** must include "_windowsapp.lib_".</span></span> <span data-ttu-id="e67cf-145">これは、一覧に含まれていませんを追加します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-145">If it's not included in the list, add it.</span></span>

    ![リンカーの依存関係を追加します。](images/visual-layer-interop/linker-dependencies.png)

1. <span data-ttu-id="e67cf-147">プリコンパイル済みヘッダーを更新します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-147">Update the precompiled header</span></span>

    - <span data-ttu-id="e67cf-148">名前を変更`stdafx.h`と`stdafx.cpp`に`pch.h`と`pch.cpp`、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="e67cf-148">Rename `stdafx.h` and `stdafx.cpp` to `pch.h` and `pch.cpp`, respectively.</span></span>
    - <span data-ttu-id="e67cf-149">プロジェクトのプロパティを設定**C/C++** > **プリコンパイル済みヘッダー** > **プリコンパイル済みヘッダー ファイル**に*pch.h*します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-149">Set project property **C/C++** > **Precompiled Headers** > **Precompiled Header File** to *pch.h*.</span></span>
    - <span data-ttu-id="e67cf-150">検索し、置換`#include "stdafx.h"`で`#include "pch.h"`ですべてのファイル。</span><span class="sxs-lookup"><span data-stu-id="e67cf-150">Find and replace `#include "stdafx.h"` with `#include "pch.h"` in all files.</span></span>

        <span data-ttu-id="e67cf-151">(**編集** > **検索し、置換** > **ファイル内の検索**)</span><span class="sxs-lookup"><span data-stu-id="e67cf-151">(**Edit** > **Find and Replace** > **Find in Files**)</span></span>

        ![検索し、置換 stdafx.h](images/visual-layer-interop/replace-stdafx.png)

    - <span data-ttu-id="e67cf-153">`pch.h`、含める`winrt/base.h`と`unknwn.h`します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-153">In `pch.h`, include `winrt/base.h` and `unknwn.h`.</span></span>

        ```cppwinrt
        // reference additional headers your program requires here
        #include <unknwn.h>
        #include <winrt/base.h>
        ```

<span data-ttu-id="e67cf-154">進む前にエラーがないかどうかを確認するには、この時点でプロジェクトをビルドすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e67cf-154">It's a good idea to build the project at this point to make sure there are no errors before going on.</span></span>

## <a name="create-a-class-to-host-composition-elements"></a><span data-ttu-id="e67cf-155">ホストの合成要素のクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-155">Create a class to host composition elements</span></span>

<span data-ttu-id="e67cf-156">コンテンツのホストにビジュアル層で作成、クラスを作成 (_CompositionHost_) を相互運用機能を管理し、合成要素を作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-156">To host content you create with the visual layer, create a class (_CompositionHost_) to manage interop and create composition elements.</span></span> <span data-ttu-id="e67cf-157">これは、構成などの合成 Api をホストするための大部分を実行します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-157">This is where you do most of the configuration for hosting Composition APIs, including:</span></span>

- <span data-ttu-id="e67cf-158">取得、[コンポジター](/uwp/api/windows.ui.composition.compositor)が作成され、オブジェクトを管理、 [Windows.UI.Composition](/uwp/api/windows.ui.composition)名前空間。</span><span class="sxs-lookup"><span data-stu-id="e67cf-158">getting a [Compositor](/uwp/api/windows.ui.composition.compositor), which creates and manages objects in the [Windows.UI.Composition](/uwp/api/windows.ui.composition) namespace.</span></span>
- <span data-ttu-id="e67cf-159">作成、 [DispatcherQueueController](/uwp/api/windows.system.dispatcherqueuecontroller)/[DispatcherQueue](/uwp/api/windows.system.dispatcherqueue) WinRT Api のタスクを管理します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-159">creating a [DispatcherQueueController](/uwp/api/windows.system.dispatcherqueuecontroller)/[DispatcherQueue](/uwp/api/windows.system.dispatcherqueue) to manage tasks for the WinRT APIs.</span></span>
- <span data-ttu-id="e67cf-160">作成、 [DesktopWindowTarget](/uwp/api/windows.ui.composition.desktop.desktopwindowtarget)と合成オブジェクトを表示する合成コンテナー。</span><span class="sxs-lookup"><span data-stu-id="e67cf-160">creating a [DesktopWindowTarget](/uwp/api/windows.ui.composition.desktop.desktopwindowtarget) and Composition container to display the composition objects.</span></span>

<span data-ttu-id="e67cf-161">このクラスをシングルトン スレッド処理の問題を回避すること。</span><span class="sxs-lookup"><span data-stu-id="e67cf-161">We make this class a singleton to avoid threading issues.</span></span> <span data-ttu-id="e67cf-162">たとえば、CompositionHost のと同じスレッド上の 2 番目のインスタンスをインスタンス化すると、エラーが発生するは、スレッドあたりの 1 つのディスパッチャー キューのみ作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-162">For example, you can only create one dispatcher queue per thread, so instantiating a second instance of CompositionHost on the same thread would cause an error.</span></span>

> [!TIP]
> <span data-ttu-id="e67cf-163">必要がある場合は、すべてのコードは、チュートリアルを使用すると適切な場所にいるかどうかを確認するチュートリアルの最後に完全なコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-163">If you need to, check the complete code at the end of the tutorial to make sure all the code is in the right places as you work through the tutorial.</span></span>

1. <span data-ttu-id="e67cf-164">プロジェクトに新しいクラス ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-164">Add a new class file to your project.</span></span>
    - <span data-ttu-id="e67cf-165">**ソリューション エクスプ ローラー**を右クリックして、 _HelloComposition_プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="e67cf-165">In **Solution Explorer**, right click the _HelloComposition_ project.</span></span>
    - <span data-ttu-id="e67cf-166">コンテキスト メニューで選択**追加** > **クラス.** .</span><span class="sxs-lookup"><span data-stu-id="e67cf-166">In the context menu, select **Add** > **Class...**.</span></span>
    - <span data-ttu-id="e67cf-167">**クラスの追加**ダイアログ ボックスで、クラス名_CompositionHost.cs_、 をクリックし、**追加**します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-167">In the **Add Class** dialog, name the class _CompositionHost.cs_, then click **Add**.</span></span>

1. <span data-ttu-id="e67cf-168">ヘッダーを含めると_using_合成相互運用機能に必要な。</span><span class="sxs-lookup"><span data-stu-id="e67cf-168">Include headers and _usings_ required for composition interop.</span></span>
    - <span data-ttu-id="e67cf-169">CompositionHost.h でこれらの追加_が含まれています_ファイルの上部にあります。</span><span class="sxs-lookup"><span data-stu-id="e67cf-169">In CompositionHost.h, add these _includes_ at the top of the file.</span></span>

    ```cppwinrt
    #pragma once
    #include <winrt/Windows.UI.Composition.Desktop.h>
    #include <windows.ui.composition.interop.h>
    #include <DispatcherQueue.h>
    ```

    - <span data-ttu-id="e67cf-170">CompositionHost.cpp でこれらの追加_using_後に、ファイルの上部にある_が含まれています_します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-170">In CompositionHost.cpp, add these _usings_ at the top of the file, after any _includes_.</span></span>

    ```cppwinrt
    using namespace winrt;
    using namespace Windows::System;
    using namespace Windows::UI;
    using namespace Windows::UI::Composition;
    using namespace Windows::UI::Composition::Desktop;
    using namespace Windows::Foundation::Numerics;
    ```

1. <span data-ttu-id="e67cf-171">シングルトン パターンを使用するクラスを編集します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-171">Edit the class to use the singleton pattern.</span></span>
    - <span data-ttu-id="e67cf-172">CompositionHost.h でプライベート コンス トラクターを確認します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-172">In CompositionHost.h, make the constructor private.</span></span>
    - <span data-ttu-id="e67cf-173">宣言のパブリック静的_GetInstance_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-173">Declare a public static _GetInstance_ method.</span></span>

    ```cppwinrt
    class CompositionHost
    {
    public:
        ~CompositionHost();
        static CompositionHost* GetInstance();

    private:
        CompositionHost();
    };
    ```

    - <span data-ttu-id="e67cf-174">CompositionHost.cpp、追加の定義、 _GetInstance_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-174">In CompositionHost.cpp, add the definition of the _GetInstance_ method.</span></span>

    ```cppwinrt
    CompositionHost* CompositionHost::GetInstance()
    {
        static CompositionHost instance;
        return &instance;
    }
    ```

1. <span data-ttu-id="e67cf-175">CompositionHost.h には、変数のプライベート メンバーを宣言、コンポジター、DispatcherQueueController、および DesktopWindowTarget。</span><span class="sxs-lookup"><span data-stu-id="e67cf-175">In CompositionHost.h, declare private member variables for the Compositor, DispatcherQueueController, and DesktopWindowTarget.</span></span>

    ```cppwinrt
    winrt::Windows::UI::Composition::Compositor m_compositor{ nullptr };
    winrt::Windows::System::DispatcherQueueController m_dispatcherQueueController{ nullptr };
    winrt::Windows::UI::Composition::Desktop::DesktopWindowTarget m_target{ nullptr };
    ```

1. <span data-ttu-id="e67cf-176">合成相互運用オブジェクトを初期化するためにパブリック メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-176">Add a public method to initialize the composition interop objects.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e67cf-177">_初期化_、呼び出すことが、 _EnsureDispatcherQueue_、 _CreateDesktopWindowTarget_、および_CreateCompositionRoot_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-177">In _Initialize_, you call the _EnsureDispatcherQueue_, _CreateDesktopWindowTarget_, and _CreateCompositionRoot_ methods.</span></span> <span data-ttu-id="e67cf-178">次の手順では、これらのメソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-178">You create these methods in the next steps.</span></span>

    - <span data-ttu-id="e67cf-179">という名前のパブリック メソッドを宣言で CompositionHost.h、_初期化_を引数として、HWND を受け取る。</span><span class="sxs-lookup"><span data-stu-id="e67cf-179">In CompositionHost.h, declare a public method named _Initialize_ that takes an HWND as an argument.</span></span>

    ```cppwinrt
    void Initialize(HWND hwnd);
    ```

    - <span data-ttu-id="e67cf-180">CompositionHost.cpp、追加の定義、_初期化_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-180">In CompositionHost.cpp, add the definition of the _Initialize_ method.</span></span>

    ```cppwinrt
    void CompositionHost::Initialize(HWND hwnd)
    {
        EnsureDispatcherQueue();
        if (m_dispatcherQueueController) m_compositor = Compositor();

        CreateDesktopWindowTarget(hwnd);
        CreateCompositionRoot();
    }
    ```

1. <span data-ttu-id="e67cf-181">Windows 合成を使用するスレッドのディスパッチャー キューを作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-181">Create a dispatcher queue on the thread that will be using Windows Composition.</span></span>

    <span data-ttu-id="e67cf-182">ディスパッチャー キューを持つため、このメソッドは 1 つ目の初期化中にスレッドには、コンポジターを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e67cf-182">A Compositor must be created on a thread that has a dispatcher queue, so this method is called first during initialization.</span></span>

    - <span data-ttu-id="e67cf-183">という名前のプライベート メソッドを宣言で CompositionHost.h、 _EnsureDispatcherQueue_します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-183">In CompositionHost.h, declare a private method named _EnsureDispatcherQueue_.</span></span>

    ```cppwinrt
    void EnsureDispatcherQueue();
    ```

    - <span data-ttu-id="e67cf-184">CompositionHost.cpp、追加の定義、 _EnsureDispatcherQueue_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-184">In CompositionHost.cpp, add the definition of the _EnsureDispatcherQueue_ method.</span></span>

    ```cppwinrt
    void CompositionHost::EnsureDispatcherQueue()
    {
        namespace abi = ABI::Windows::System;

        if (m_dispatcherQueueController == nullptr)
        {
            DispatcherQueueOptions options
            {
                sizeof(DispatcherQueueOptions), /* dwSize */
                DQTYPE_THREAD_CURRENT,          /* threadType */
                DQTAT_COM_ASTA                  /* apartmentType */
            };

            Windows::System::DispatcherQueueController controller{ nullptr };
            check_hresult(CreateDispatcherQueueController(options, reinterpret_cast<abi::IDispatcherQueueController**>(put_abi(controller))));
            m_dispatcherQueueController = controller;
        }
    }
    ```

1. <span data-ttu-id="e67cf-185">合成ターゲットとしては、アプリのウィンドウを登録します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-185">Register your app's window as a composition target.</span></span>
    - <span data-ttu-id="e67cf-186">という名前のプライベート メソッドを宣言で CompositionHost.h、 _CreateDesktopWindowTarget_を引数として、HWND を受け取る。</span><span class="sxs-lookup"><span data-stu-id="e67cf-186">In CompositionHost.h, declare a private method named _CreateDesktopWindowTarget_ that takes an HWND as an argument.</span></span>

    ```cppwinrt
    void CreateDesktopWindowTarget(HWND window);
    ```

    - <span data-ttu-id="e67cf-187">CompositionHost.cpp、追加の定義、 _CreateDesktopWindowTarget_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-187">In CompositionHost.cpp, add the definition of the _CreateDesktopWindowTarget_ method.</span></span>

    ```cppwinrt
    void CompositionHost::CreateDesktopWindowTarget(HWND window)
    {
        namespace abi = ABI::Windows::UI::Composition::Desktop;

        auto interop = m_compositor.as<abi::ICompositorDesktopInterop>();
        DesktopWindowTarget target{ nullptr };
        check_hresult(interop->CreateDesktopWindowTarget(window, false, reinterpret_cast<abi::IDesktopWindowTarget**>(put_abi(target))));
        m_target = target;
    }
    ```

1. <span data-ttu-id="e67cf-188">ビジュアル オブジェクトを保持するためにルート ビジュアル コンテナーを作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-188">Create a root visual container to hold visual objects.</span></span>
    - <span data-ttu-id="e67cf-189">という名前のプライベート メソッドを宣言で CompositionHost.h、 _CreateCompositionRoot_します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-189">In CompositionHost.h, declare a private method named _CreateCompositionRoot_.</span></span>

    ```cppwinrt
    void CreateCompositionRoot();
    ```

    - <span data-ttu-id="e67cf-190">CompositionHost.cpp、追加の定義、 _CreateCompositionRoot_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-190">In CompositionHost.cpp, add the definition of the _CreateCompositionRoot_ method.</span></span>

    ```cppwinrt
    void CompositionHost::CreateCompositionRoot()
    {
        auto root = m_compositor.CreateContainerVisual();
        root.RelativeSizeAdjustment({ 1.0f, 1.0f });
        root.Offset({ 124, 12, 0 });
        m_target.Root(root);
    }
    ```

<span data-ttu-id="e67cf-191">エラーがないかどうかを確認するには、現在のプロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="e67cf-191">Build the project now to make sure there are no errors.</span></span>

<span data-ttu-id="e67cf-192">これらのメソッドは、ビジュアル層の UWP と Win32 Api の間の相互運用機能に必要なコンポーネントを設定します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-192">These methods set up the components needed for interop between the UWP visual layer and Win32 APIs.</span></span> <span data-ttu-id="e67cf-193">これで、アプリにコンテンツを追加できます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-193">Now you can add content to your app.</span></span>

### <a name="add-composition-elements"></a><span data-ttu-id="e67cf-194">合成要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-194">Add composition elements</span></span>

<span data-ttu-id="e67cf-195">インフラストラクチャを導入するに表示する合成コンテンツを生成できます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-195">With the infrastructure in place, you can now generate the Composition content you want to show.</span></span>

<span data-ttu-id="e67cf-196">この例では、ランダムに色付きの正方形を作成するコードを追加する[SpriteVisual](/uwp/api/windows.ui.composition.spritevisual)短い遅延の後に削除すると、そのアニメーションとします。</span><span class="sxs-lookup"><span data-stu-id="e67cf-196">For this example, you add code that creates a randomly-colored square [SpriteVisual](/uwp/api/windows.ui.composition.spritevisual) with an animation that causes it to drop after a short delay.</span></span>

1. <span data-ttu-id="e67cf-197">合成要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-197">Add a composition element.</span></span>
    - <span data-ttu-id="e67cf-198">CompositionHost.h でという名前のパブリック メソッドを宣言_AddElement_を受け取る 3 **float**引数として値。</span><span class="sxs-lookup"><span data-stu-id="e67cf-198">In CompositionHost.h, declare a public method named _AddElement_ that takes 3 **float** values as arguments.</span></span>

    ```cppwinrt
    void AddElement(float size, float x, float y);
    ```

    - <span data-ttu-id="e67cf-199">CompositionHost.cpp、追加の定義、 _AddElement_メソッド。</span><span class="sxs-lookup"><span data-stu-id="e67cf-199">In CompositionHost.cpp, add the definition of the _AddElement_ method.</span></span>

    ```cppwinrt
    void CompositionHost::AddElement(float size, float x, float y)
    {
        if (m_target.Root())
        {
            auto visuals = m_target.Root().as<ContainerVisual>().Children();
            auto visual = m_compositor.CreateSpriteVisual();

            auto element = m_compositor.CreateSpriteVisual();
            uint8_t r = (double)(double)(rand() % 255);;
            uint8_t g = (double)(double)(rand() % 255);;
            uint8_t b = (double)(double)(rand() % 255);;

            element.Brush(m_compositor.CreateColorBrush({ 255, r, g, b }));
            element.Size({ size, size });
            element.Offset({ x, y, 0.0f, });

            auto animation = m_compositor.CreateVector3KeyFrameAnimation();
            auto bottom = (float)600 - element.Size().y;
            animation.InsertKeyFrame(1, { element.Offset().x, bottom, 0 });

            using timeSpan = std::chrono::duration<int, std::ratio<1, 1>>;

            std::chrono::seconds duration(2);
            std::chrono::seconds delay(3);

            animation.Duration(timeSpan(duration));
            animation.DelayTime(timeSpan(delay));
            element.StartAnimation(L"Offset", animation);
            visuals.InsertAtTop(element);

            visuals.InsertAtTop(visual);
        }
    }
    ```

## <a name="create-and-show-the-window"></a><span data-ttu-id="e67cf-200">作成し、ウィンドウを表示します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-200">Create and show the window</span></span>

<span data-ttu-id="e67cf-201">ここで、Win32 UI には、ボタンと UWP コンポジションのコンテンツを追加できます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-201">Now, you can add a button and the UWP composition content to your Win32 UI.</span></span>

1. <span data-ttu-id="e67cf-202">ファイルの上部にある、HelloComposition.cpp 含める_CompositionHost.h_BTN_ADD を定義し、CompositionHost のインスタンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-202">In HelloComposition.cpp, at the top of the file, include _CompositionHost.h_, define BTN_ADD, and get an instance of CompositionHost.</span></span>

    ```cppwinrt
    #include "CompositionHost.h"

    // #define MAX_LOADSTRING 100 // This is already in the file.
    #define BTN_ADD 1000

    CompositionHost* compHost = CompositionHost::GetInstance();
    ```

1. <span data-ttu-id="e67cf-203">`InitInstance`メソッドを作成するウィンドウのサイズを変更します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-203">In the `InitInstance` method, change the size of the window that's created.</span></span> <span data-ttu-id="e67cf-204">(このコマンドラインで次のように変更します`CW_USEDEFAULT, 0`に`900, 672`。)。</span><span class="sxs-lookup"><span data-stu-id="e67cf-204">(In this line, change `CW_USEDEFAULT, 0` to `900, 672`.)</span></span>

    ```cppwinrt
    HWND hWnd = CreateWindowW(szWindowClass, szTitle, WS_OVERLAPPEDWINDOW,
        CW_USEDEFAULT, 0, 900, 672, nullptr, nullptr, hInstance, nullptr);
    ```

1. <span data-ttu-id="e67cf-205">WndProc 関数に、追加`case WM_CREATE`を_メッセージ_の switch ブロックです。</span><span class="sxs-lookup"><span data-stu-id="e67cf-205">In the WndProc function, add `case WM_CREATE` to the _message_ switch block.</span></span> <span data-ttu-id="e67cf-206">ここで、CompositionHost を初期化し、ボタンを作成します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-206">In this case, you initialize the CompositionHost and create the button.</span></span>

    ```cppwinrt
    case WM_CREATE:
    {
        compHost->Initialize(hWnd);
        srand(time(nullptr));

        CreateWindow(TEXT("button"), TEXT("Add element"),
            WS_VISIBLE | WS_CHILD | BS_PUSHBUTTON,
            12, 12, 100, 50,
            hWnd, (HMENU)BTN_ADD, nullptr, nullptr);
    }
    break;
    ```

1. <span data-ttu-id="e67cf-207">WndProc 関数では、UI に合成要素を追加するボタンのクリックを処理します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-207">Also in the WndProc function, handle the button click to add a composition element to the UI.</span></span> 

    <span data-ttu-id="e67cf-208">追加`case BTN_ADD`を_wmId_ WM_COMMAND ブロック内の switch ブロックです。</span><span class="sxs-lookup"><span data-stu-id="e67cf-208">Add `case BTN_ADD` to the _wmId_ switch block inside the WM_COMMAND block.</span></span>

    ```cppwinrt
    case BTN_ADD: // addButton click
    {
        double size = (double)(rand() % 150 + 50);
        double x = (double)(rand() % 600);
        double y = (double)(rand() % 200);
        compHost->AddElement(size, x, y);
        break;
    }
    ```

<span data-ttu-id="e67cf-209">ビルドして、アプリを実行することができますようになりました。</span><span class="sxs-lookup"><span data-stu-id="e67cf-209">You can now build and run your app.</span></span> <span data-ttu-id="e67cf-210">必要がある場合は、すべてのコードは、適切な場所にいるかどうかを確認するチュートリアルの最後に完全なコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-210">If you need to, check the complete code at the end of the tutorial to make sure all the code is in the right places.</span></span>

<span data-ttu-id="e67cf-211">アプリを実行する ボタンをクリックすると、UI に追加するアニメーションの正方形が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e67cf-211">When you run the app and click the button, you should see animated squares added to the UI.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e67cf-212">その他の資料</span><span class="sxs-lookup"><span data-stu-id="e67cf-212">Additional resources</span></span>

- [<span data-ttu-id="e67cf-213">Win32 HelloComposition サンプル (GitHub)</span><span class="sxs-lookup"><span data-stu-id="e67cf-213">Win32 HelloComposition sample (GitHub)</span></span>](https://github.com/Microsoft/Windows.UI.Composition-Win32-Samples/tree/master/cpp/HelloComposition)
- [<span data-ttu-id="e67cf-214">Win32 の概要とC++</span><span class="sxs-lookup"><span data-stu-id="e67cf-214">Get Started with Win32 and C++</span></span>](/windows/desktop/learnwin32/learn-to-program-for-windows)
- <span data-ttu-id="e67cf-215">[Windows 10 アプリの概要](/windows/uwp/get-started/)(UWP)</span><span class="sxs-lookup"><span data-stu-id="e67cf-215">[Get started with Windows 10 apps](/windows/uwp/get-started/) (UWP)</span></span>
- <span data-ttu-id="e67cf-216">[Windows 10 のデスクトップ アプリケーションの拡張](/windows/uwp/porting/desktop-to-uwp-enhance)(UWP)</span><span class="sxs-lookup"><span data-stu-id="e67cf-216">[Enhance your desktop application for Windows 10](/windows/uwp/porting/desktop-to-uwp-enhance) (UWP)</span></span>
- <span data-ttu-id="e67cf-217">[名前空間の Windows.UI.Composition](/uwp/api/windows.ui.composition) (UWP)</span><span class="sxs-lookup"><span data-stu-id="e67cf-217">[Windows.UI.Composition namespace](/uwp/api/windows.ui.composition) (UWP)</span></span>

## <a name="complete-code"></a><span data-ttu-id="e67cf-218">コードを完成させる</span><span class="sxs-lookup"><span data-stu-id="e67cf-218">Complete code</span></span>

<span data-ttu-id="e67cf-219">CompositionHost クラスと InitInstance メソッドの完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="e67cf-219">Here's the complete code for the CompositionHost class and the InitInstance method.</span></span>

### <a name="compositionhosth"></a><span data-ttu-id="e67cf-220">CompositionHost.h</span><span class="sxs-lookup"><span data-stu-id="e67cf-220">CompositionHost.h</span></span>

```cppwinrt
#pragma once
#include <winrt/Windows.UI.Composition.Desktop.h>
#include <windows.ui.composition.interop.h>
#include <DispatcherQueue.h>

class CompositionHost
{
public:
    ~CompositionHost();
    static CompositionHost* GetInstance();

    void Initialize(HWND hwnd);
    void AddElement(float size, float x, float y);

private:
    CompositionHost();

    void CreateDesktopWindowTarget(HWND window);
    void EnsureDispatcherQueue();
    void CreateCompositionRoot();

    winrt::Windows::UI::Composition::Compositor m_compositor{ nullptr };
    winrt::Windows::UI::Composition::Desktop::DesktopWindowTarget m_target{ nullptr };
    winrt::Windows::System::DispatcherQueueController m_dispatcherQueueController{ nullptr };
};
```

### <a name="compositionhostcpp"></a><span data-ttu-id="e67cf-221">CompositionHost.cpp</span><span class="sxs-lookup"><span data-stu-id="e67cf-221">CompositionHost.cpp</span></span>

```cppwinrt
#include "pch.h"
#include "CompositionHost.h"

using namespace winrt;
using namespace Windows::System;
using namespace Windows::UI;
using namespace Windows::UI::Composition;
using namespace Windows::UI::Composition::Desktop;
using namespace Windows::Foundation::Numerics;

CompositionHost::CompositionHost()
{
}

CompositionHost* CompositionHost::GetInstance()
{
    static CompositionHost instance;
    return &instance;
}

CompositionHost::~CompositionHost()
{
}

void CompositionHost::Initialize(HWND hwnd)
{
    EnsureDispatcherQueue();
    if (m_dispatcherQueueController) m_compositor = Compositor();

    if (m_compositor)
    {
        CreateDesktopWindowTarget(hwnd);
        CreateCompositionRoot();
    }
}

void CompositionHost::EnsureDispatcherQueue()
{
    namespace abi = ABI::Windows::System;

    if (m_dispatcherQueueController == nullptr)
    {
        DispatcherQueueOptions options
        {
            sizeof(DispatcherQueueOptions), /* dwSize */
            DQTYPE_THREAD_CURRENT,          /* threadType */
            DQTAT_COM_ASTA                  /* apartmentType */
        };

        Windows::System::DispatcherQueueController controller{ nullptr };
        check_hresult(CreateDispatcherQueueController(options, reinterpret_cast<abi::IDispatcherQueueController**>(put_abi(controller))));
        m_dispatcherQueueController = controller;
    }
}

void CompositionHost::CreateDesktopWindowTarget(HWND window)
{
    namespace abi = ABI::Windows::UI::Composition::Desktop;

    auto interop = m_compositor.as<abi::ICompositorDesktopInterop>();
    DesktopWindowTarget target{ nullptr };
    check_hresult(interop->CreateDesktopWindowTarget(window, false, reinterpret_cast<abi::IDesktopWindowTarget**>(put_abi(target))));
    m_target = target;
}

void CompositionHost::CreateCompositionRoot()
{
    auto root = m_compositor.CreateContainerVisual();
    root.RelativeSizeAdjustment({ 1.0f, 1.0f });
    root.Offset({ 124, 12, 0 });
    m_target.Root(root);
}

void CompositionHost::AddElement(float size, float x, float y)
{
    if (m_target.Root())
    {
        auto visuals = m_target.Root().as<ContainerVisual>().Children();
        auto visual = m_compositor.CreateSpriteVisual();

        auto element = m_compositor.CreateSpriteVisual();
        uint8_t r = (double)(double)(rand() % 255);;
        uint8_t g = (double)(double)(rand() % 255);;
        uint8_t b = (double)(double)(rand() % 255);;

        element.Brush(m_compositor.CreateColorBrush({ 255, r, g, b }));
        element.Size({ size, size });
        element.Offset({ x, y, 0.0f, });

        auto animation = m_compositor.CreateVector3KeyFrameAnimation();
        auto bottom = (float)600 - element.Size().y;
        animation.InsertKeyFrame(1, { element.Offset().x, bottom, 0 });

        using timeSpan = std::chrono::duration<int, std::ratio<1, 1>>;

        std::chrono::seconds duration(2);
        std::chrono::seconds delay(3);

        animation.Duration(timeSpan(duration));
        animation.DelayTime(timeSpan(delay));
        element.StartAnimation(L"Offset", animation);
        visuals.InsertAtTop(element);

        visuals.InsertAtTop(visual);
    }
}
```

### <a name="hellocompositioncpp-partial"></a><span data-ttu-id="e67cf-222">HelloComposition.cpp (部分的)</span><span class="sxs-lookup"><span data-stu-id="e67cf-222">HelloComposition.cpp (Partial)</span></span>

```cppwinrt
#include "pch.h"
#include "HelloComposition.h"
#include "CompositionHost.h"

#define MAX_LOADSTRING 100
#define BTN_ADD 1000

CompositionHost* compHost = CompositionHost::GetInstance();

// Global Variables:

// ...
// ... code not shown ...
// ...

BOOL InitInstance(HINSTANCE hInstance, int nCmdShow)
{
   hInst = hInstance; // Store instance handle in our global variable

   HWND hWnd = CreateWindowW(szWindowClass, szTitle, WS_OVERLAPPEDWINDOW,
      CW_USEDEFAULT, 0, 900, 672, nullptr, nullptr, hInstance, nullptr);

// ...
// ... code not shown ...
// ...
}

// ...

LRESULT CALLBACK WndProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam)
{
    switch (message)
    {
// Add this...
    case WM_CREATE:
    {
        compHost->Initialize(hWnd);
        srand(time(nullptr));

        CreateWindow(TEXT("button"), TEXT("Add element"),
            WS_VISIBLE | WS_CHILD | BS_PUSHBUTTON,
            12, 12, 100, 50,
            hWnd, (HMENU)BTN_ADD, nullptr, nullptr);
    }
    break;
// ...
    case WM_COMMAND:
    {
        int wmId = LOWORD(wParam);
        // Parse the menu selections:
        switch (wmId)
        {
        case IDM_ABOUT:
            DialogBox(hInst, MAKEINTRESOURCE(IDD_ABOUTBOX), hWnd, About);
            break;
        case IDM_EXIT:
            DestroyWindow(hWnd);
            break;
// Add this...
        case BTN_ADD: // addButton click
        {
            double size = (double)(rand() % 150 + 50);
            double x = (double)(rand() % 600);
            double y = (double)(rand() % 200);
            compHost->AddElement(size, x, y);
            break;
        }
// ...
        default:
            return DefWindowProc(hWnd, message, wParam, lParam);
        }
    }
    break;
    case WM_PAINT:
    {
        PAINTSTRUCT ps;
        HDC hdc = BeginPaint(hWnd, &ps);
        // TODO: Add any drawing code that uses hdc here...
        EndPaint(hWnd, &ps);
    }
    break;
    case WM_DESTROY:
        PostQuitMessage(0);
        break;
    default:
        return DefWindowProc(hWnd, message, wParam, lParam);
    }
    return 0;
}

// ...
// ... code not shown ...
// ...
```