---
title: アプリのアクティブ化の処理
description: OnLaunched メソッドをオーバーライドすることで、アプリのアクティブ化を処理する方法について説明します。
ms.assetid: DA9A6A43-F09D-4512-A2AB-9B6132431007
ms.date: 07/02/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
dev_langs:
- csharp
- cppwinrt
- cpp
- vb
ms.openlocfilehash: 622fc4246c0ce8051135feab07295034b55a82e4
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370820"
---
# <a name="handle-app-activation"></a><span data-ttu-id="0ec41-104">アプリのアクティブ化の処理</span><span class="sxs-lookup"><span data-stu-id="0ec41-104">Handle app activation</span></span>

<span data-ttu-id="0ec41-105">アプリのアクティブ化をオーバーライドすることで処理する方法について説明します、 [ **Application.OnLaunched** ](/uwp/api/windows.ui.xaml.application.onlaunched)メソッド。</span><span class="sxs-lookup"><span data-stu-id="0ec41-105">Learn how to handle app activation by overriding the [**Application.OnLaunched**](/uwp/api/windows.ui.xaml.application.onlaunched) method.</span></span>

## <a name="override-the-launch-handler"></a><span data-ttu-id="0ec41-106">起動ハンドラーを上書きする</span><span class="sxs-lookup"><span data-stu-id="0ec41-106">Override the launch handler</span></span>

<span data-ttu-id="0ec41-107">何らかの理由で、アプリがアクティブになったときに、システムが送信、 [ **CoreApplicationView.Activated** ](/uwp/api/windows.applicationmodel.core.coreapplicationview.activated)イベント。</span><span class="sxs-lookup"><span data-stu-id="0ec41-107">When an app is activated, for any reason, the system sends the [**CoreApplicationView.Activated**](/uwp/api/windows.applicationmodel.core.coreapplicationview.activated) event.</span></span> <span data-ttu-id="0ec41-108">アクティブ化の種類の一覧については、[**ActivationKind**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ActivationKind) 列挙型をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ec41-108">For a list of activation types, see the [**ActivationKind**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ActivationKind) enumeration.</span></span>

<span data-ttu-id="0ec41-109">[  **Windows.UI.Xaml.Application**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Application) クラスで定義されているメソッドを上書きして、さまざまなアクティブ化の種類に対応することができます。</span><span class="sxs-lookup"><span data-stu-id="0ec41-109">The [**Windows.UI.Xaml.Application**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Application) class defines methods you can override to handle the various activation types.</span></span> <span data-ttu-id="0ec41-110">一部のアクティブ化の種類には、上書きできる専用のメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="0ec41-110">Several of the activation types have a specific method that you can override.</span></span> <span data-ttu-id="0ec41-111">それ以外のアクティブ化の種類では、[**OnActivated**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onactivated) メソッドを上書きします。</span><span class="sxs-lookup"><span data-stu-id="0ec41-111">For the other activation types, override the [**OnActivated**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onactivated) method.</span></span>

<span data-ttu-id="0ec41-112">アプリのクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="0ec41-112">Define the class for your application.</span></span>

```xml
<Application
    x:Class="AppName.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
```

<span data-ttu-id="0ec41-113">[  **OnLaunched**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onlaunched) メソッドを上書きします。</span><span class="sxs-lookup"><span data-stu-id="0ec41-113">Override the [**OnLaunched**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onlaunched) method.</span></span> <span data-ttu-id="0ec41-114">このメソッドは、ユーザーがアプリを起動するたびに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="0ec41-114">This method is called whenever the user launches the app.</span></span> <span data-ttu-id="0ec41-115">[  **LaunchActivatedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.LaunchActivatedEventArgs) パラメーターには、アプリの以前の状態とアクティブ化引数が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0ec41-115">The [**LaunchActivatedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.LaunchActivatedEventArgs) parameter contains the previous state of your app and the activation arguments.</span></span>

> [!NOTE]
> <span data-ttu-id="0ec41-116">、Windows の開始のタイルまたはアプリの一覧から中断されているアプリを起動するこのメソッドを呼び出すしません。</span><span class="sxs-lookup"><span data-stu-id="0ec41-116">On Windows, launching a suspended app from Start tile or app list doesn't call this method.</span></span>

```csharp
using System;
using Windows.ApplicationModel.Activation;
using Windows.UI.Xaml;

namespace AppName
{
   public partial class App
   {
      async protected override void OnLaunched(LaunchActivatedEventArgs args)
      {
         EnsurePageCreatedAndActivate();
      }

      // Creates the MainPage if it isn't already created.  Also activates
      // the window so it takes foreground and input focus.
      private MainPage EnsurePageCreatedAndActivate()
      {
         if (Window.Current.Content == null)
         {
             Window.Current.Content = new MainPage();
         }

         Window.Current.Activate();
         return Window.Current.Content as MainPage;
      }
   }
}
```

```vb
Class App
   Protected Overrides Sub OnLaunched(args As LaunchActivatedEventArgs)
      Window.Current.Content = New MainPage()
      Window.Current.Activate()
   End Sub
End Class
```

```cppwinrt
...
#include "MainPage.h"
#include "winrt/Windows.ApplicationModel.Activation.h"
#include "winrt/Windows.UI.Xaml.h"
#include "winrt/Windows.UI.Xaml.Controls.h"
...
using namespace winrt;
using namespace Windows::ApplicationModel::Activation;
using namespace Windows::UI::Xaml;
using namespace Windows::UI::Xaml::Controls;

struct App : AppT<App>
{
    App();

    /// <summary>
    /// Invoked when the application is launched normally by the end user.  Other entry points
    /// will be used such as when the application is launched to open a specific file.
    /// </summary>
    /// <param name="e">Details about the launch request and process.</param>
    void OnLaunched(LaunchActivatedEventArgs const& e)
    {
        Frame rootFrame{ nullptr };
        auto content = Window::Current().Content();
        if (content)
        {
            rootFrame = content.try_as<Frame>();
        }

        // Do not repeat app initialization when the Window already has content,
        // just ensure that the window is active
        if (rootFrame == nullptr)
        {
            // Create a Frame to act as the navigation context and associate it with
            // a SuspensionManager key
            rootFrame = Frame();

            rootFrame.NavigationFailed({ this, &App::OnNavigationFailed });

            if (e.PreviousExecutionState() == ApplicationExecutionState::Terminated)
            {
                // Restore the saved session state only when appropriate, scheduling the
                // final launch steps after the restore is complete
            }

            if (e.PrelaunchActivated() == false)
            {
                if (rootFrame.Content() == nullptr)
                {
                    // When the navigation stack isn't restored navigate to the first page,
                    // configuring the new page by passing required information as a navigation
                    // parameter
                    rootFrame.Navigate(xaml_typename<BlankApp1::MainPage>(), box_value(e.Arguments()));
                }
                // Place the frame in the current Window
                Window::Current().Content(rootFrame);
                // Ensure the current window is active
                Window::Current().Activate();
            }
        }
        else
        {
            if (e.PrelaunchActivated() == false)
            {
                if (rootFrame.Content() == nullptr)
                {
                    // When the navigation stack isn't restored navigate to the first page,
                    // configuring the new page by passing required information as a navigation
                    // parameter
                    rootFrame.Navigate(xaml_typename<BlankApp1::MainPage>(), box_value(e.Arguments()));
                }
                // Ensure the current window is active
                Window::Current().Activate();
            }
        }
    }
};
```

```cpp
using namespace Windows::ApplicationModel::Activation;
using namespace Windows::Foundation;
using namespace Windows::UI::Xaml;
using namespace AppName;
void App::OnLaunched(LaunchActivatedEventArgs^ args)
{
   EnsurePageCreatedAndActivate();
}

// Creates the MainPage if it isn't already created.  Also activates
// the window so it takes foreground and input focus.
void App::EnsurePageCreatedAndActivate()
{
    if (_mainPage == nullptr)
    {
        // Save the MainPage for use if we get activated later
        _mainPage = ref new MainPage();
    }
    Window::Current->Content = _mainPage;
    Window::Current->Activate();
}
```

## <a name="restore-application-data-if-app-was-suspended-then-terminated"></a><span data-ttu-id="0ec41-117">アプリが一時停止後に終了された場合は、アプリケーション データを復元する</span><span class="sxs-lookup"><span data-stu-id="0ec41-117">Restore application data if app was suspended then terminated</span></span>

<span data-ttu-id="0ec41-118">ユーザーが終了したアプリに切り替えると、システムは [**Activated**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplicationview.activated) イベントを送信します。このとき、[**Kind**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.kind) は **Launch** に設定され、[**PreviousExecutionState**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.previousexecutionstate) は **Terminated** または **ClosedByUser** に設定されます。</span><span class="sxs-lookup"><span data-stu-id="0ec41-118">When the user switches to your terminated app, the system sends the [**Activated**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplicationview.activated) event, with [**Kind**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.kind) set to **Launch** and [**PreviousExecutionState**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.previousexecutionstate) set to **Terminated** or **ClosedByUser**.</span></span> <span data-ttu-id="0ec41-119">アプリでは、保存されているアプリ データを読み込み、表示されているコンテンツを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0ec41-119">The app should load its saved application data and refresh its displayed content.</span></span>

```csharp
async protected override void OnLaunched(LaunchActivatedEventArgs args)
{
   if (args.PreviousExecutionState == ApplicationExecutionState.Terminated ||
       args.PreviousExecutionState == ApplicationExecutionState.ClosedByUser)
   {
      // TODO: Populate the UI with the previously saved application data
   }
   else
   {
      // TODO: Populate the UI with defaults
   }

   EnsurePageCreatedAndActivate();
}
```

```vb
Protected Overrides Sub OnLaunched(args As Windows.ApplicationModel.Activation.LaunchActivatedEventArgs)
   Dim restoreState As Boolean = False

   Select Case args.PreviousExecutionState
      Case ApplicationExecutionState.Terminated
         ' TODO: Populate the UI with the previously saved application data
         restoreState = True
      Case ApplicationExecutionState.ClosedByUser
         ' TODO: Populate the UI with the previously saved application data
         restoreState = True
      Case Else
         ' TODO: Populate the UI with defaults
   End Select

   Window.Current.Content = New MainPage(restoreState)
   Window.Current.Activate()
End Sub
```

```cppwinrt
void App::OnLaunched(Windows::ApplicationModel::Activation::LaunchActivatedEventArgs const& e)
{
    if (e.PreviousExecutionState() == ApplicationExecutionState::Terminated ||
        e.PreviousExecutionState() == ApplicationExecutionState::ClosedByUser)
    {
        // Populate the UI with the previously saved application data.
    }
    else
    {
        // Populate the UI with defaults.
    }
    ...
}
```

```cpp
void App::OnLaunched(Windows::ApplicationModel::Activation::LaunchActivatedEventArgs^ args)
{
   if (args->PreviousExecutionState == ApplicationExecutionState::Terminated ||
       args->PreviousExecutionState == ApplicationExecutionState::ClosedByUser)
   {
      // TODO: Populate the UI with the previously saved application data
   }
   else
   {
      // TODO: Populate the UI with defaults
   }

   EnsurePageCreatedAndActivate();
}
```

<span data-ttu-id="0ec41-120">[  **PreviousExecutionState**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.previousexecutionstate) の値が **NotRunning** である場合は、アプリがアプリケーション データの保存に失敗しているため、初めて起動するときのように最初からアプリをやり直す必要があります。</span><span class="sxs-lookup"><span data-stu-id="0ec41-120">If the value of [**PreviousExecutionState**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.previousexecutionstate) is **NotRunning**, the app failed to save its application data successfully and the app should start over as if it were being initially launched.</span></span>

## <a name="remarks"></a><span data-ttu-id="0ec41-121">注釈</span><span class="sxs-lookup"><span data-stu-id="0ec41-121">Remarks</span></span>

> [!NOTE]
> <span data-ttu-id="0ec41-122">現在のウィンドウにコンテンツ セットが既にある場合、アプリは初期化をスキップすることがあります。</span><span class="sxs-lookup"><span data-stu-id="0ec41-122">Apps can skip initialization if there is already content set on the current window.</span></span> <span data-ttu-id="0ec41-123">チェックすることができます、 [ **LaunchActivatedEventArgs.TileId** ](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.launchactivatedeventargs.tileid)プロパティかどうか、アプリが、プライマリやセカンダリ タイルから起動して、その情報に基づいて判断する必要があるかどうかを決定します。新しいやアプリのエクスペリエンスを再開します。</span><span class="sxs-lookup"><span data-stu-id="0ec41-123">You can check the [**LaunchActivatedEventArgs.TileId**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.launchactivatedeventargs.tileid) property to determine whether the app was launched from a primary or a secondary tile and, based on that information, decide whether you should present a fresh or resume app experience.</span></span>

## <a name="important-apis"></a><span data-ttu-id="0ec41-124">重要な API</span><span class="sxs-lookup"><span data-stu-id="0ec41-124">Important APIs</span></span>
* [<span data-ttu-id="0ec41-125">Windows.ApplicationModel.Activation</span><span class="sxs-lookup"><span data-stu-id="0ec41-125">Windows.ApplicationModel.Activation</span></span>](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation)
* [<span data-ttu-id="0ec41-126">Windows.UI.Xaml.Application</span><span class="sxs-lookup"><span data-stu-id="0ec41-126">Windows.UI.Xaml.Application</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Application)

## <a name="related-topics"></a><span data-ttu-id="0ec41-127">関連トピック</span><span class="sxs-lookup"><span data-stu-id="0ec41-127">Related topics</span></span>
* [<span data-ttu-id="0ec41-128">アプリの中断の処理</span><span class="sxs-lookup"><span data-stu-id="0ec41-128">Handle app suspend</span></span>](suspend-an-app.md)
* [<span data-ttu-id="0ec41-129">アプリの再開の処理</span><span class="sxs-lookup"><span data-stu-id="0ec41-129">Handle app resume</span></span>](resume-an-app.md)
* [<span data-ttu-id="0ec41-130">アプリに関するガイドラインの中断し、再開</span><span class="sxs-lookup"><span data-stu-id="0ec41-130">Guidelines for app suspend and resume</span></span>](https://docs.microsoft.com/windows/uwp/launch-resume/index)
* [<span data-ttu-id="0ec41-131">アプリのライフサイクル</span><span class="sxs-lookup"><span data-stu-id="0ec41-131">App lifecycle</span></span>](app-lifecycle.md)
