---
title: アプリをアクティブ化する方法 (DirectX と C++)
description: ここでは、ユニバーサル Windows プラットフォーム (UWP) DirectX アプリのアクティブ化エクスペリエンスを定義する方法について説明します。
ms.assetid: b07c7da1-8a5e-5b57-6f77-6439bf653a53
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, DirectX, アクティブ化
ms.localizationpriority: medium
ms.openlocfilehash: 4aeba58af61cffa33626c64cebcbade272af109b
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368602"
---
# <a name="how-to-activate-an-app-directx-and-c"></a><span data-ttu-id="d8691-104">アプリをアクティブ化する方法 (DirectX と C++)</span><span class="sxs-lookup"><span data-stu-id="d8691-104">How to activate an app (DirectX and C++)</span></span>



<span data-ttu-id="d8691-105">ここでは、ユニバーサル Windows プラットフォーム (UWP) DirectX アプリのアクティブ化エクスペリエンスを定義する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d8691-105">This topic shows how to define the activation experience for a Universal Windows Platform (UWP) DirectX app.</span></span>

## <a name="register-the-app-activation-event-handler"></a><span data-ttu-id="d8691-106">アプリのアクティブ化イベント ハンドラーを登録する</span><span class="sxs-lookup"><span data-stu-id="d8691-106">Register the app activation event handler</span></span>


<span data-ttu-id="d8691-107">まず、[**CoreApplicationView::Activated**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplicationview.activated) イベントを処理するための登録を行います。このイベントは、アプリが開始され、オペレーティング システムによって初期化されるときに発生します。</span><span class="sxs-lookup"><span data-stu-id="d8691-107">First, register to handle the [**CoreApplicationView::Activated**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplicationview.activated) event, which is raised when your app is started and initialized by the operating system.</span></span>

<span data-ttu-id="d8691-108">次のコードをビュー プロバイダー (この例では **MyViewProvider** という名前) の [**IFrameworkView::Initialize**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.initialize) メソッドの実装に追加します。</span><span class="sxs-lookup"><span data-stu-id="d8691-108">Add this code to your implementation of the [**IFrameworkView::Initialize**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.initialize) method of your view provider (named **MyViewProvider** in the example):</span></span>

```cpp
void App::Initialize(CoreApplicationView^ applicationView)
{
    // Register event handlers for the app lifecycle. This example includes Activated, so that we
    // can make the CoreWindow active and start rendering on the window.
    applicationView->Activated +=
        ref new TypedEventHandler<CoreApplicationView^, IActivatedEventArgs^>(this, &App::OnActivated);
  
  //...

}
```

## <a name="activate-the-corewindow-instance-for-the-app"></a><span data-ttu-id="d8691-109">アプリの CoreWindow インスタンスをアクティブ化する</span><span class="sxs-lookup"><span data-stu-id="d8691-109">Activate the CoreWindow instance for the app</span></span>


<span data-ttu-id="d8691-110">アプリの起動時に、アプリの [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) への参照を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d8691-110">When your app starts, you must obtain a reference to the [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) for your app.</span></span> <span data-ttu-id="d8691-111">**CoreWindow** には、アプリがウィンドウ イベントの処理に使うウィンドウ イベント メッセージ ディスパッチャーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d8691-111">**CoreWindow** contains the window event message dispatcher that your app uses to process window events.</span></span> <span data-ttu-id="d8691-112">アプリのアクティブ化イベントのコールバックで、[**CoreWindow::GetForCurrentThread**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.getforcurrentthread) を呼び出して、この参照を取得します。</span><span class="sxs-lookup"><span data-stu-id="d8691-112">Obtain this reference in your callback for the app activation event by calling [**CoreWindow::GetForCurrentThread**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.getforcurrentthread).</span></span> <span data-ttu-id="d8691-113">この参照を取得したら、[**CoreWindow::Activate**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.activate) を呼び出して、メイン アプリ ウィンドウをアクティブ化します。</span><span class="sxs-lookup"><span data-stu-id="d8691-113">Once you have obtained this reference, activate the main app window by calling [**CoreWindow::Activate**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.activate).</span></span>

```cpp
void App::OnActivated(CoreApplicationView^ applicationView, IActivatedEventArgs^ args)
{
    // Run() won't start until the CoreWindow is activated.
    CoreWindow::GetForCurrentThread()->Activate();
}
```

## <a name="start-processing-event-message-for-the-main-app-window"></a><span data-ttu-id="d8691-114">メイン アプリ ウィンドウのイベント メッセージの処理の開始</span><span class="sxs-lookup"><span data-stu-id="d8691-114">Start processing event message for the main app window</span></span>


<span data-ttu-id="d8691-115">作成したコールバックは、アプリの [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) の [**CoreDispatcher**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreDispatcher) によって処理されるイベント メッセージとして発生します。</span><span class="sxs-lookup"><span data-stu-id="d8691-115">Your callbacks occur as event messages are processed by the [**CoreDispatcher**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreDispatcher) for the app's [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow).</span></span> <span data-ttu-id="d8691-116">このコールバックは、アプリのメイン ループ (ビュー プロバイダーの [**IFrameworkView::Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run) メソッドで実装) から [**CoreDispatcher::ProcessEvents**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.processevents) を呼び出さない場合は呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="d8691-116">This callback will not be invoked if you do not call [**CoreDispatcher::ProcessEvents**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.processevents) from your app's main loop (implemented in the [**IFrameworkView::Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run) method of your view provider).</span></span>

``` syntax
// This method is called after the window becomes active.
void App::Run()
{
    while (!m_windowClosed)
    {
        if (m_windowVisible)
        {
            CoreWindow::GetForCurrentThread()->Dispatcher->ProcessEvents(CoreProcessEventsOption::ProcessAllIfPresent);

            m_main->Update();

            if (m_main->Render())
            {
                m_deviceResources->Present();
            }
        }
        else
        {
            CoreWindow::GetForCurrentThread()->Dispatcher->ProcessEvents(CoreProcessEventsOption::ProcessOneAndAllPending);
        }
    }
}
```

## <a name="related-topics"></a><span data-ttu-id="d8691-117">関連トピック</span><span class="sxs-lookup"><span data-stu-id="d8691-117">Related topics</span></span>


* [<span data-ttu-id="d8691-118">(DirectX および C++) アプリを停止する方法</span><span class="sxs-lookup"><span data-stu-id="d8691-118">How to suspend an app (DirectX and C++)</span></span>](how-to-suspend-an-app-directx-and-cpp.md)
* [<span data-ttu-id="d8691-119">(DirectX および C++) アプリを再開する方法</span><span class="sxs-lookup"><span data-stu-id="d8691-119">How to resume an app (DirectX and C++)</span></span>](how-to-resume-an-app-directx-and-cpp.md)

 

 




