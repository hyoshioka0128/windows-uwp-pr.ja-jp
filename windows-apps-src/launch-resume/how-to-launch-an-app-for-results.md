---
title: 結果を取得するためのアプリの起動
description: 別のアプリからアプリを起動し、2 つのアプリの間でデータを交換する方法について説明します。 これは、"結果を取得するためのアプリの起動" と呼ばれます。
ms.assetid: AFC53D75-B3DD-4FF6-9FC0-9335242EE327
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 23d4a4e0159fc18ac524937326e69d6fbc3a627e
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370711"
---
# <a name="launch-an-app-for-results"></a><span data-ttu-id="2db61-105">結果を取得するためのアプリの起動</span><span class="sxs-lookup"><span data-stu-id="2db61-105">Launch an app for results</span></span>




<span data-ttu-id="2db61-106">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="2db61-106">**Important APIs**</span></span>

-   [<span data-ttu-id="2db61-107">**LaunchUriForResultsAsync**</span><span class="sxs-lookup"><span data-stu-id="2db61-107">**LaunchUriForResultsAsync**</span></span>](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows)
-   [<span data-ttu-id="2db61-108">**ValueSet**</span><span class="sxs-lookup"><span data-stu-id="2db61-108">**ValueSet**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet)

<span data-ttu-id="2db61-109">別のアプリからアプリを起動し、2 つのアプリの間でデータを交換する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2db61-109">Learn how to launch an app from another app and exchange data between the two.</span></span> <span data-ttu-id="2db61-110">これは、"*結果を取得するためのアプリの起動*" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="2db61-110">This is called *launching an app for results*.</span></span> <span data-ttu-id="2db61-111">この例では、[**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows) を使って、結果を取得するためのアプリの起動方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2db61-111">The example here shows you how to use [**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows) to launch an app for results.</span></span>

<span data-ttu-id="2db61-112">新しいアプリへの通信では、Windows 10 Api を使うと Windows アプリ (および Windows Web アプリ) をアプリと exchange のデータ ファイルとファイルを起動できます。</span><span class="sxs-lookup"><span data-stu-id="2db61-112">New app-to-app communication APIs in Windows 10 make it possible for Windows apps (and Windows Web apps) to launch an app and exchange data and files.</span></span> <span data-ttu-id="2db61-113">このため、複数のアプリを基にマッシュアップ ソリューションを構築できます。</span><span class="sxs-lookup"><span data-stu-id="2db61-113">This enables you to build mash-up solutions from multiple apps.</span></span> <span data-ttu-id="2db61-114">これらの新しい API を使うと、複数のアプリを使う必要のあった複雑な作業をシームレスに処理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="2db61-114">Using these new APIs, complex tasks that would have required the user to use multiple apps can now be handled seamlessly.</span></span> <span data-ttu-id="2db61-115">たとえば、アプリでソーシャル ネットワーキング アプリを起動して連絡先を選んだり、チェックアウト アプリを起動して支払処理を実行したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="2db61-115">For example, your app could launch a social networking app to choose a contact, or launch a checkout app to complete a payment process.</span></span>

<span data-ttu-id="2db61-116">結果を得るために起動するアプリは、起動されたアプリと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="2db61-116">The app that you'll launch for results will be referred to as the launched app.</span></span> <span data-ttu-id="2db61-117">アプリを起動するアプリは、呼び出し元アプリと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="2db61-117">The app that launches the app will be referred to as the calling app.</span></span> <span data-ttu-id="2db61-118">この例では、呼び出し元アプリと、起動されたアプリの両方を記述します。</span><span class="sxs-lookup"><span data-stu-id="2db61-118">For this example you will write both the calling app and the launched app.</span></span>

## <a name="step-1-register-the-protocol-to-be-handled-in-the-app-that-youll-launch-for-results"></a><span data-ttu-id="2db61-119">手順 1:結果を起動するアプリで処理するためのプロトコルを登録します。</span><span class="sxs-lookup"><span data-stu-id="2db61-119">Step 1: Register the protocol to be handled in the app that you'll launch for results</span></span>


<span data-ttu-id="2db61-120">起動アプリの Package.appxmanifest ファイルで、プロトコル拡張機能を **&lt;Application&gt;** セクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="2db61-120">In the Package.appxmanifest file of the launched app, add a protocol extension to the **&lt;Application&gt;** section.</span></span> <span data-ttu-id="2db61-121">この例では、**test-app2app** という名前の架空プロトコルを使います。</span><span class="sxs-lookup"><span data-stu-id="2db61-121">The example here uses a fictional protocol named **test-app2app**.</span></span>

<span data-ttu-id="2db61-122">プロトコル拡張機能の **ReturnResults** 属性に指定できる値は、次の 3 つのうちいずれかです。</span><span class="sxs-lookup"><span data-stu-id="2db61-122">The **ReturnResults** attribute in the protocol extension accepts one of these values:</span></span>

-   <span data-ttu-id="2db61-123">**optional**—結果を取得するためにアプリを起動する場合は、[**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows) メソッドを使います。結果を取得しない場合は、[**LaunchUriAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync) を使います。</span><span class="sxs-lookup"><span data-stu-id="2db61-123">**optional**—The app can be launched for results by using the [**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows) method, or not for results by using [**LaunchUriAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync).</span></span> <span data-ttu-id="2db61-124">**optional** を使うとき、起動アプリでは、結果を取得するためにアプリが起動されたかどうかを判別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2db61-124">When you use **optional**, the launched app must determine whether it was launched for results.</span></span> <span data-ttu-id="2db61-125">これを行うには、[**OnActivated**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onactivated) イベント引数を調べます。</span><span class="sxs-lookup"><span data-stu-id="2db61-125">It can do that by checking the [**OnActivated**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onactivated) event argument.</span></span> <span data-ttu-id="2db61-126">引数の [**IActivatedEventArgs.Kind**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.kind) プロパティが [**ActivationKind.ProtocolForResults**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ActivationKind) を返した場合、またはイベント引数の型が [**ProtocolActivatedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ProtocolActivatedEventArgs) である場合は、アプリが **LaunchUriForResultsAsync** を介して起動されます。</span><span class="sxs-lookup"><span data-stu-id="2db61-126">If the argument's [**IActivatedEventArgs.Kind**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.kind) property returns [**ActivationKind.ProtocolForResults**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ActivationKind), or if the type of the event argument is [**ProtocolActivatedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ProtocolActivatedEventArgs), the app was launched via **LaunchUriForResultsAsync**.</span></span>
-   <span data-ttu-id="2db61-127">**always**—アプリは、結果を取得するためにのみ起動することができます。つまり、[**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows) に対してのみ応答できます。</span><span class="sxs-lookup"><span data-stu-id="2db61-127">**always**—The app can be launched only for results; that is, it can respond only to [**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows).</span></span>
-   <span data-ttu-id="2db61-128">**none**—アプリは、結果を取得するために起動することはできません。[**LaunchUriAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync) に対してのみ応答できます。</span><span class="sxs-lookup"><span data-stu-id="2db61-128">**none**—The app cannot be launched for results; it can respond only to [**LaunchUriAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync).</span></span>

<span data-ttu-id="2db61-129">次のプロトコル拡張機能の例では、アプリは結果を取得するためにのみ起動することができます。</span><span class="sxs-lookup"><span data-stu-id="2db61-129">In this protocol-extension example, the app can be launched only for results.</span></span> <span data-ttu-id="2db61-130">以下で説明するように、この例では、**OnActivated** メソッド内部のロジックが簡素化されます。これは、"結果を取得するために起動する" ケースのみを処理し、アプリをアクティブ化する他の方法を処理する必要がないためです。</span><span class="sxs-lookup"><span data-stu-id="2db61-130">This simplifies the logic inside the **OnActivated** method, discussed below, because we have to handle only the "launched for results" case and not the other ways that the app could be activated.</span></span>

```xml
<Applications>
   <Application ...>

     <Extensions>
       <uap:Extension Category="windows.protocol">
         <uap:Protocol Name="test-app2app" ReturnResults="always">
           <uap:DisplayName>Test app-2-app</uap:DisplayName>
         </uap:Protocol>
       </uap:Extension>
     </Extensions>

   </Application>
</Applications>
```

## <a name="step-2-override-applicationonactivated-in-the-app-that-youll-launch-for-results"></a><span data-ttu-id="2db61-131">手順 2:結果の起動をアプリでの Application.OnActivated をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="2db61-131">Step 2: Override Application.OnActivated in the app that you'll launch for results</span></span>


<span data-ttu-id="2db61-132">このメソッドが起動アプリにまだ存在しない場合は、App.xaml.cs で定義されている `App` クラス内に作成します。</span><span class="sxs-lookup"><span data-stu-id="2db61-132">If this method does not already exist in the launched app, create it within the `App` class defined in App.xaml.cs.</span></span>

<span data-ttu-id="2db61-133">ソーシャル ネットワークで友だちを選ぶことができるアプリでは、この関数によって友だちを選ぶためのページを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="2db61-133">In an app that lets you pick your friends in a social network, this function could be where you open the people-picker page.</span></span> <span data-ttu-id="2db61-134">次の例では、**LaunchedForResultsPage** という名前のページが、結果を取得するためにアプリがアクティブ化されたときに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2db61-134">In this next example, a page named **LaunchedForResultsPage** is displayed when the app is activated for results.</span></span> <span data-ttu-id="2db61-135">ファイルの先頭に、次の **using** ステートメントが含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2db61-135">Ensure that the **using** statement is included at the top of the file.</span></span>

```cs
using Windows.ApplicationModel.Activation;
...
protected override void OnActivated(IActivatedEventArgs args)
{
    // Window management
    Frame rootFrame = Window.Current.Content as Frame;
    if (rootFrame == null)
    {
        rootFrame = new Frame();
        Window.Current.Content = rootFrame;
    }

    // Code specific to launch for results
    var protocolForResultsArgs = (ProtocolForResultsActivatedEventArgs)args;
    // Open the page that we created to handle activation for results.
    rootFrame.Navigate(typeof(LaunchedForResultsPage), protocolForResultsArgs);

    // Ensure the current window is active.
    Window.Current.Activate();
}
```

<span data-ttu-id="2db61-136">Package.appxmanifest ファイル内のプロトコル拡張機能では **ReturnResults** が **always** と指定されているため、上記のコードでは `args` を [**ProtocolForResultsActivatedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ProtocolForResultsActivatedEventArgs) に直接キャストすることができます。このとき、**ProtocolForResultsActivatedEventArgs** のみが、このアプリの **OnActivated** に送信されます。</span><span class="sxs-lookup"><span data-stu-id="2db61-136">Because the protocol extension in the Package.appxmanifest file specifies **ReturnResults** as **always**, the code just shown can cast `args` directly to [**ProtocolForResultsActivatedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ProtocolForResultsActivatedEventArgs) with confidence that only **ProtocolForResultsActivatedEventArgs** will be sent to **OnActivated** for this app.</span></span> <span data-ttu-id="2db61-137">結果を取得するための起動以外の方法でアプリがアクティブ化される可能性がある場合は、結果を取得するためにアプリが起動されたかどうかを判別するために [**IActivatedEventArgs.Kind**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.kind) プロパティが [**ActivationKind.ProtocolForResults**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ActivationKind) を返すかどうかを確認してください。</span><span class="sxs-lookup"><span data-stu-id="2db61-137">If your app can be activated in ways other than launching for results, you can check whether [**IActivatedEventArgs.Kind**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.iactivatedeventargs.kind) property returns [**ActivationKind.ProtocolForResults**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Activation.ActivationKind) to tell whether the app was launched for results.</span></span>

## <a name="step-3-add-a-protocolforresultsoperation-field-to-the-app-you-launch-for-results"></a><span data-ttu-id="2db61-138">手順 3:結果を起動するアプリに ProtocolForResultsOperation フィールドを追加します。</span><span class="sxs-lookup"><span data-stu-id="2db61-138">Step 3: Add a ProtocolForResultsOperation field to the app you launch for results</span></span>


```cs
private Windows.System.ProtocolForResultsOperation _operation = null;
```

<span data-ttu-id="2db61-139">[  **ProtocolForResultsOperation**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.protocolforresultsactivatedeventargs.protocolforresultsoperation) フィールドを使うと、起動されたアプリが呼び出し元のアプリに結果を返すことができるようになった場合に、そのタイミングを通知することができます。</span><span class="sxs-lookup"><span data-stu-id="2db61-139">You'll use the [**ProtocolForResultsOperation**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.protocolforresultsactivatedeventargs.protocolforresultsoperation) field to signal when the launched app is ready to return the result to the calling app.</span></span> <span data-ttu-id="2db61-140">この例では、このフィールドは **LaunchedForResultsPage** クラスに追加されます。これは、結果を取得するための起動処理をそのページから実行し、そのページにアクセスする必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="2db61-140">In this example, the field is added to the **LaunchedForResultsPage** class because you'll complete the launch-for-results operation from that page and will need access to it.</span></span>

## <a name="step-4-override-onnavigatedto-in-the-app-you-launch-for-results"></a><span data-ttu-id="2db61-141">手順 4:結果を起動するアプリで OnNavigatedTo() をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="2db61-141">Step 4: Override OnNavigatedTo() in the app you launch for results</span></span>


<span data-ttu-id="2db61-142">結果を取得するためにアプリを起動するときに表示するページで、[**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="2db61-142">Override the [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) method on the page that you'll display when your app is launched for results.</span></span> <span data-ttu-id="2db61-143">このメソッドがまだ存在しない場合は、&lt;ページ名&gt;.xaml.cs で定義されているページのクラス内に作成します。</span><span class="sxs-lookup"><span data-stu-id="2db61-143">If this method does not already exist, create it within the class for the page defined in &lt;pagename&gt;.xaml.cs.</span></span> <span data-ttu-id="2db61-144">ファイルの先頭に、次の **using** ステートメントが含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2db61-144">Ensure that the following **using** statement is included at the top of the file:</span></span>

```cs
using Windows.ApplicationModel.Activation
```

<span data-ttu-id="2db61-145">[  **OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) メソッド内の [**NavigationEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation.NavigationEventArgs) オブジェクトには、呼び出し元アプリから渡されたデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2db61-145">The [**NavigationEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Navigation.NavigationEventArgs) object in the [**OnNavigatedTo**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) method contains the data passed from the calling app.</span></span> <span data-ttu-id="2db61-146">データは最大で 100 KB になります。また、データは [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) オブジェクトに格納されます。</span><span class="sxs-lookup"><span data-stu-id="2db61-146">The data may not exceed 100KB and is stored in a [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) object.</span></span>

<span data-ttu-id="2db61-147">次のコード例では、起動されたアプリは、呼び出し元のアプリから送信されたデータが **TestData** というキーで [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) に格納されていることを想定しています。これは、サンプルの呼び出し元アプリで、データを送信するためにそのようにコード化されているためです。</span><span class="sxs-lookup"><span data-stu-id="2db61-147">In this example code, the launched app expects the data sent from the calling app to be in a [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) under a key named **TestData**, because that's what the example's calling app is coded to send.</span></span>

```cs
using Windows.ApplicationModel.Activation;
...
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    var protocolForResultsArgs = e.Parameter as ProtocolForResultsActivatedEventArgs;
    // Set the ProtocolForResultsOperation field.
    _operation = protocolForResultsArgs.ProtocolForResultsOperation;

    if (protocolForResultsArgs.Data.ContainsKey("TestData"))
    {
        string dataFromCaller = protocolForResultsArgs.Data["TestData"] as string;
    }
}
...
private Windows.System.ProtocolForResultsOperation _operation = null;
```

## <a name="step-5-write-code-to-return-data-to-the-calling-app"></a><span data-ttu-id="2db61-148">手順 5:呼び出し元のアプリにデータを返すコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="2db61-148">Step 5: Write code to return data to the calling app</span></span>


<span data-ttu-id="2db61-149">起動アプリで、[**ProtocolForResultsOperation**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.protocolforresultsactivatedeventargs.protocolforresultsoperation) を使って呼び出し元のアプリにデータを返します。</span><span class="sxs-lookup"><span data-stu-id="2db61-149">In the launched app, use [**ProtocolForResultsOperation**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.protocolforresultsactivatedeventargs.protocolforresultsoperation) to return data to the calling app.</span></span> <span data-ttu-id="2db61-150">次のコード例では、呼び出し元のアプリに返す値を格納する [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) オブジェクトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="2db61-150">In this example code, a [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) object is created that contains the value to return to the calling app.</span></span> <span data-ttu-id="2db61-151">その後で、**ProtocolForResultsOperation** フィールドを使って、呼び出し元のアプリに値を送信します。</span><span class="sxs-lookup"><span data-stu-id="2db61-151">The **ProtocolForResultsOperation** field is then used to send the value to the calling app.</span></span>

```cs
    ValueSet result = new ValueSet();
    result["ReturnedData"] = "The returned result";
    _operation.ReportCompleted(result);
```

## <a name="step-6-write-code-to-launch-the-app-for-results-and-get-the-returned-data"></a><span data-ttu-id="2db61-152">手順 6:結果のアプリを起動し、返されるデータを取得するコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="2db61-152">Step 6: Write code to launch the app for results and get the returned data</span></span>


<span data-ttu-id="2db61-153">次のコード例に示すように、呼び出し元のアプリの非同期メソッド内で、アプリを起動します。</span><span class="sxs-lookup"><span data-stu-id="2db61-153">Launch the app from within an async method in your calling app as shown in this example code.</span></span> <span data-ttu-id="2db61-154">**using** ステートメントは、コードをコンパイルするために必要となります。</span><span class="sxs-lookup"><span data-stu-id="2db61-154">Note the **using** statements, which are necessary for the code to compile:</span></span>

```cs
using System.Threading.Tasks;
using Windows.System;
...

async Task<string> LaunchAppForResults()
{
    var testAppUri = new Uri("test-app2app:"); // The protocol handled by the launched app
    var options = new LauncherOptions();
    options.TargetApplicationPackageFamilyName = "67d987e1-e842-4229-9f7c-98cf13b5da45_yd7nk54bq29ra";

    var inputData = new ValueSet();
    inputData["TestData"] = "Test data";

    string theResult = "";
    LaunchUriResult result = await Windows.System.Launcher.LaunchUriForResultsAsync(testAppUri, options, inputData);
    if (result.Status == LaunchUriStatus.Success &&
        result.Result != null &&
        result.Result.ContainsKey("ReturnedData"))
    {
        ValueSet theValues = result.Result;
        theResult = theValues["ReturnedData"] as string;
    }
    return theResult;
}
```

<span data-ttu-id="2db61-155">この例では、キー **TestData** を含んでいる [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) が、起動アプリに渡されます。</span><span class="sxs-lookup"><span data-stu-id="2db61-155">In this example, a [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) containing the key **TestData** is passed to the launched app.</span></span> <span data-ttu-id="2db61-156">起動アプリは、**ReturnedData** という名前のキーを持つ **ValueSet** を作成します。これには、呼び出し元に返される結果が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2db61-156">The launched app creates a **ValueSet** with a key named **ReturnedData** that contains the result returned to the caller.</span></span>

<span data-ttu-id="2db61-157">結果を取得するために起動するアプリは、呼び出し元アプリを実行する前にビルドし、展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2db61-157">You must build and deploy the app that you'll launch for results before running your calling app.</span></span> <span data-ttu-id="2db61-158">このように操作しないと、[**LaunchUriResult.Status**](https://docs.microsoft.com/uwp/api/Windows.System.LaunchUriStatus) は **LaunchUriStatus.AppUnavailable** を報告します。</span><span class="sxs-lookup"><span data-stu-id="2db61-158">Otherwise, [**LaunchUriResult.Status**](https://docs.microsoft.com/uwp/api/Windows.System.LaunchUriStatus) will report **LaunchUriStatus.AppUnavailable**.</span></span>

<span data-ttu-id="2db61-159">[  **TargetApplicationPackageFamilyName**](https://docs.microsoft.com/uwp/api/windows.system.launcheroptions.targetapplicationpackagefamilyname) を設定するときは、起動アプリのファミリ名が必要です。</span><span class="sxs-lookup"><span data-stu-id="2db61-159">You'll need the family name of the launched app when you set the [**TargetApplicationPackageFamilyName**](https://docs.microsoft.com/uwp/api/windows.system.launcheroptions.targetapplicationpackagefamilyname).</span></span> <span data-ttu-id="2db61-160">ファミリ名を取得する方法の 1 つは、起動アプリ内から、次の呼び出しを行うことです。</span><span class="sxs-lookup"><span data-stu-id="2db61-160">One way to get the family name is to make the following call from within the launched app:</span></span>

```cs
string familyName = Windows.ApplicationModel.Package.Current.Id.FamilyName;
```

## <a name="remarks"></a><span data-ttu-id="2db61-161">注釈</span><span class="sxs-lookup"><span data-stu-id="2db61-161">Remarks</span></span>


<span data-ttu-id="2db61-162">この方法の例については、結果を取得するためのアプリの起動の概要を説明した "hello world" アプリをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2db61-162">The example in this how-to provides a "hello world" introduction to launching an app for results.</span></span> <span data-ttu-id="2db61-163">重要な注意点は、新しい [**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows) API を使うと、アプリを非同期的に起動し、[**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) クラスを使って通信できるようになることです。</span><span class="sxs-lookup"><span data-stu-id="2db61-163">The key things to note are that the new [**LaunchUriForResultsAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows) API lets you asynchronously launch an app and communicate via the [**ValueSet**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet) class.</span></span> <span data-ttu-id="2db61-164">**ValueSet** を使って渡すデータは、100 KB に制限されます。</span><span class="sxs-lookup"><span data-stu-id="2db61-164">Passing data via a **ValueSet** is limited to 100KB.</span></span> <span data-ttu-id="2db61-165">より多くのデータを渡す必要がある場合は、アプリ間で渡すことができるファイル トークンを作成するための、[**SharedStorageAccessManager**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.DataTransfer.SharedStorageAccessManager) クラスを使ってファイルを共有することができます。</span><span class="sxs-lookup"><span data-stu-id="2db61-165">If you need to pass larger amounts of data, you can share files by using the [**SharedStorageAccessManager**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.DataTransfer.SharedStorageAccessManager) class to create file tokens that you can pass between apps.</span></span> <span data-ttu-id="2db61-166">たとえば、`inputData` という名前の **ValueSet** を指定し、起動アプリと共有するファイルのトークンを格納できます。</span><span class="sxs-lookup"><span data-stu-id="2db61-166">For example, given a **ValueSet** named `inputData`, you could store the token to a file that you want to share with the launched app:</span></span>

```cs
inputData["ImageFileToken"] = SharedStorageAccessManager.AddFile(myFile);
```

<span data-ttu-id="2db61-167">その後で、**LaunchUriForResultsAsync** を使って、トークンを起動アプリに渡します。</span><span class="sxs-lookup"><span data-stu-id="2db61-167">Then pass it to the launched app via **LaunchUriForResultsAsync**.</span></span>

## <a name="related-topics"></a><span data-ttu-id="2db61-168">関連トピック</span><span class="sxs-lookup"><span data-stu-id="2db61-168">Related topics</span></span>


* [<span data-ttu-id="2db61-169">**LaunchUri**</span><span class="sxs-lookup"><span data-stu-id="2db61-169">**LaunchUri**</span></span>](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync)
* [<span data-ttu-id="2db61-170">**LaunchUriForResultsAsync**</span><span class="sxs-lookup"><span data-stu-id="2db61-170">**LaunchUriForResultsAsync**</span></span>](https://docs.microsoft.com/uwp/api/windows.system.launcher.windows)
* [<span data-ttu-id="2db61-171">**ValueSet**</span><span class="sxs-lookup"><span data-stu-id="2db61-171">**ValueSet**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.ValueSet)

 

 
