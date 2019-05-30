---
description: UI の背後には、ビジネス レイヤーとデータ レイヤーがあります。
title: UWP に Windows Phone Silverlight のビジネス データおよびデータ層の移植
ms.assetid: 27c66759-2b35-41f5-9f7a-ceb97f4a0e3f
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: c2f9ff93396562452028990e877d42782cff4ef2
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372210"
---
#  <a name="porting-windowsphone-silverlight-business-and-data-layers-to-uwp"></a><span data-ttu-id="040c3-104">UWP に Windows Phone Silverlight のビジネス データおよびデータ層の移植</span><span class="sxs-lookup"><span data-stu-id="040c3-104">Porting Windows Phone Silverlight business and data layers to UWP</span></span>


<span data-ttu-id="040c3-105">前のトピックは、「[入出力、デバイス、アプリ モデルの移植](wpsl-to-uwp-input-and-sensors.md)」でした。</span><span class="sxs-lookup"><span data-stu-id="040c3-105">The previous topic was [Porting for I/O, device, and app model](wpsl-to-uwp-input-and-sensors.md).</span></span>

<span data-ttu-id="040c3-106">UI の背後には、ビジネス レイヤーとデータ レイヤーがあります。</span><span class="sxs-lookup"><span data-stu-id="040c3-106">Behind your UI are your business and data layers.</span></span> <span data-ttu-id="040c3-107">こうしたレイヤーのコードでは、オペレーティング システムと .NET Framework API (たとえば、バックグラウンド処理、場所、カメラ、ファイル システム、ネットワーク、その他のデータ アクセスなど) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="040c3-107">The code in these layers calls operating system and .NET Framework APIs (for example, background processing, location, the camera, the file system, network, and other data access).</span></span> <span data-ttu-id="040c3-108">その大半が[ユニバーサル Windows プラットフォーム (UWP) アプリ](https://docs.microsoft.com/previous-versions/windows/br211369(v=win.10))で利用可能であり、したがって変更なくこのコードの大半を移植できると考えられます。</span><span class="sxs-lookup"><span data-stu-id="040c3-108">The vast majority of those are [available to a Universal Windows Platform (UWP) app](https://docs.microsoft.com/previous-versions/windows/br211369(v=win.10)), so you can expect to be able to port much of this code without change.</span></span>

## <a name="asynchronous-methods"></a><span data-ttu-id="040c3-109">非同期メソッド</span><span class="sxs-lookup"><span data-stu-id="040c3-109">Asynchronous methods</span></span>

<span data-ttu-id="040c3-110">ユニバーサル Windows プラットフォーム (UWP) で優先されることの 1 つは、真に一貫して応答性が高いアプリを構築できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="040c3-110">One of the priorities of the Universal Windows Platform (UWP) is to enable you to build apps that are truly, and consistently, responsive.</span></span> <span data-ttu-id="040c3-111">アニメーションは常にスムーズで、パンやスワイプなどのタッチ操作は遅延なく瞬時であり、UI が指に密着するように感じさせます。</span><span class="sxs-lookup"><span data-stu-id="040c3-111">Animations are always smooth, and touch interactions such as panning and swiping are instantaneous and free of lag, making it feel like the UI is glued to your finger.</span></span> <span data-ttu-id="040c3-112">これを実現するために、50 ミリ秒以内の完了が保証できないすべての UWP API は非同期になり、名前の後に **Async** が付加されています。</span><span class="sxs-lookup"><span data-stu-id="040c3-112">To achieve this, any UWP API that can't guarantee to complete within 50ms has been made asynchronous and its name suffixed with **Async**.</span></span> <span data-ttu-id="040c3-113">UI スレッドは、**Async** メソッドの呼び出し後に直ちに戻り、別のスレッドで処理を実行します。</span><span class="sxs-lookup"><span data-stu-id="040c3-113">Your UI thread will return immediately from calling an **Async** method, and the work will take place on another thread.</span></span> <span data-ttu-id="040c3-114">**Async** メソッドの使用は、構文的に非常に簡単であり、C# の **await** 演算子、JavaScript promise オブジェクト、C++ 後続タスクを使います。</span><span class="sxs-lookup"><span data-stu-id="040c3-114">Consuming an **Async** method is made very easy, syntactically, using the C# **await** operator, JavaScript promise objects, and C++ continuations.</span></span> <span data-ttu-id="040c3-115">詳しくは、「[非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-universal-windows-platform-apps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-115">For more info, see [Asynchronous programming](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-universal-windows-platform-apps).</span></span>

## <a name="background-processing"></a><span data-ttu-id="040c3-116">バックグラウンド処理</span><span class="sxs-lookup"><span data-stu-id="040c3-116">Background processing</span></span>

<span data-ttu-id="040c3-117">Windows Phone Silverlight アプリを使用してマネージできます**ScheduledTaskAgent**アプリがフォア グラウンドにないときにタスクを実行するオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="040c3-117">A Windows Phone Silverlight app can use a managed **ScheduledTaskAgent** object to perform a task while the app is not in the foreground.</span></span> <span data-ttu-id="040c3-118">UWP アプリでは、同様の方法でバックグラウンド タスクを作成、登録するために [**BackgroundTaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) クラスを使います。</span><span class="sxs-lookup"><span data-stu-id="040c3-118">A UWP app uses the [**BackgroundTaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) class to create and register a background task in a similar way.</span></span> <span data-ttu-id="040c3-119">バックグラウンド タスクの処理を実装するクラスを定義します。</span><span class="sxs-lookup"><span data-stu-id="040c3-119">You define a class that implements the work of your background task.</span></span> <span data-ttu-id="040c3-120">システムでは、バックグラウンド タスクを定期的に実行し、処理を実行するクラスの [**Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.ibackgroundtask.) メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="040c3-120">The system runs your background task periodically, calling the [**Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.ibackgroundtask.) method of your class to execute the work.</span></span> <span data-ttu-id="040c3-121">UWP アプリでは、アプリ パッケージ マニフェストで**バックグラウンド タスク**の宣言を忘れずに設定します。</span><span class="sxs-lookup"><span data-stu-id="040c3-121">In a UWP app, remember to set the **Background Tasks** declaration in the app package manifest.</span></span> <span data-ttu-id="040c3-122">詳しくは、「[バックグラウンド タスクによるアプリのサポート](https://docs.microsoft.com/windows/uwp/launch-resume/support-your-app-with-background-tasks)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-122">For more info, see [Support your app with background tasks](https://docs.microsoft.com/windows/uwp/launch-resume/support-your-app-with-background-tasks).</span></span>

<span data-ttu-id="040c3-123">Windows Phone Silverlight アプリを使用して、バック グラウンドでの大きなデータ ファイルを転送する、 **BackgroundTransferService**クラス。</span><span class="sxs-lookup"><span data-stu-id="040c3-123">To transfer large data files in the background, a Windows Phone Silverlight app uses the **BackgroundTransferService** class.</span></span> <span data-ttu-id="040c3-124">UWP アプリは、このために [**Windows.Networking.BackgroundTransfer**](https://docs.microsoft.com/uwp/api/Windows.Networking.BackgroundTransfer) 名前空間の API を使います。</span><span class="sxs-lookup"><span data-stu-id="040c3-124">A UWP app uses APIs in the [**Windows.Networking.BackgroundTransfer**](https://docs.microsoft.com/uwp/api/Windows.Networking.BackgroundTransfer) namespace to do this.</span></span> <span data-ttu-id="040c3-125">機能は同様のパターンを使って転送を開始しますが、新しい API では機能と性能が向上しています。</span><span class="sxs-lookup"><span data-stu-id="040c3-125">The features use a similar pattern to initiate transfers, but the new API has improved capabilities and performance.</span></span> <span data-ttu-id="040c3-126">詳しくは、「[バックグラウンドでのデータの転送](https://docs.microsoft.com/previous-versions/windows/apps/hh452975(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-126">For more info, see [Transferring data in the background](https://docs.microsoft.com/previous-versions/windows/apps/hh452975(v=win.10)).</span></span>

<span data-ttu-id="040c3-127">Windows Phone Silverlight アプリでのマネージ クラスを使用して、 **Microsoft.Phone.BackgroundAudio**フォア グラウンドでアプリの中にオーディオを再生する名前空間がないです。</span><span class="sxs-lookup"><span data-stu-id="040c3-127">A Windows Phone Silverlight app uses the managed classes in the **Microsoft.Phone.BackgroundAudio** namespace to play audio while the app is not in the foreground.</span></span> <span data-ttu-id="040c3-128">UWP は Windows Phone ストア アプリ モデルを使います。詳しくは、「[バックグラウンド オーディオ](https://docs.microsoft.com/windows/uwp/audio-video-camera/background-audio)」および[バックグラウンド オーディオ](https://go.microsoft.com/fwlink/p/?linkid=619997)のサンプルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-128">The UWP uses the Windows Phone Store app model, see [Background Audio](https://docs.microsoft.com/windows/uwp/audio-video-camera/background-audio) and the [Background audio](https://go.microsoft.com/fwlink/p/?linkid=619997) sample.</span></span>

## <a name="cloud-services-networking-and-databases"></a><span data-ttu-id="040c3-129">クラウド サービス、ネットワーク、データベース</span><span class="sxs-lookup"><span data-stu-id="040c3-129">Cloud services, networking, and databases</span></span>

<span data-ttu-id="040c3-130">Azure を使ってクラウドでデータとアプリ サービスをホストできます。</span><span class="sxs-lookup"><span data-stu-id="040c3-130">Hosting data and app services in the cloud is possible using Azure.</span></span> <span data-ttu-id="040c3-131">「[Mobile Services の使用](https://go.microsoft.com/fwlink/p/?LinkID=403138)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-131">See [Getting Started with Mobile Services](https://go.microsoft.com/fwlink/p/?LinkID=403138).</span></span> <span data-ttu-id="040c3-132">オンラインとオフラインの両方のデータを必要とするソリューションを参照してください。[Mobile Services でのオフライン データ同期を使用して](https://azure.microsoft.com/documentation/articles/mobile-services-windows-store-dotnet-get-started-offline-data/)します。</span><span class="sxs-lookup"><span data-stu-id="040c3-132">For solutions that require both online and offline data see: [Using offline data sync in Mobile Services](https://azure.microsoft.com/documentation/articles/mobile-services-windows-store-dotnet-get-started-offline-data/).</span></span>

<span data-ttu-id="040c3-133">UWP は **System.Net.HttpWebRequest** クラスを部分的にサポートしていますが、**System.Net.WebClient** クラスはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="040c3-133">The UWP has partial support for the **System.Net.HttpWebRequest** class, but the **System.Net.WebClient** class is not supported.</span></span> <span data-ttu-id="040c3-134">お勧めできる将来的な代替案は、[**Windows.Web.Http.HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) クラス (または、.NET をサポートする他のプラットフォームにコードを移植可能にする場合は [System.Net.Http.HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.118).aspx)) です。</span><span class="sxs-lookup"><span data-stu-id="040c3-134">The recommended, forward-looking alternative is the [**Windows.Web.Http.HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) class (or [System.Net.Http.HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.118).aspx) if you need your code to be portable to other platforms that support .NET).</span></span> <span data-ttu-id="040c3-135">これらの API では、[System.Net.Http.HttpRequestMessage](https://docs.microsoft.com/previous-versions/visualstudio/hh159020(v=vs.118)) を使って HTTP 要求を表します。</span><span class="sxs-lookup"><span data-stu-id="040c3-135">These APIs use [System.Net.Http.HttpRequestMessage](https://docs.microsoft.com/previous-versions/visualstudio/hh159020(v=vs.118)) to represent an HTTP request.</span></span>

<span data-ttu-id="040c3-136">UWP アプリには、現在、大量のデータ アクセスを実行するシナリオ (基幹業務 (LOB) シナリオなど) を対象としたサポートは組み込まれていません。</span><span class="sxs-lookup"><span data-stu-id="040c3-136">UWP apps do not currently include built-in support for data-intensive scenarios such as line of business (LOB) scenarios.</span></span> <span data-ttu-id="040c3-137">ただし、ローカル トランザクション データベース サービスのために SQLite を使うことができます。</span><span class="sxs-lookup"><span data-stu-id="040c3-137">However, you can make use SQLite for local transactional database services.</span></span> <span data-ttu-id="040c3-138">詳しくは、「[SQLite](https://marketplace.visualstudio.com/vsgallery/4913e7d5-96c9-4dde-a1a1-69820d615936)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-138">For more info, see [SQLite](https://marketplace.visualstudio.com/vsgallery/4913e7d5-96c9-4dde-a1a1-69820d615936).</span></span>

<span data-ttu-id="040c3-139">相対 URI ではなく絶対 URI を Windows ランタイム型に渡します。</span><span class="sxs-lookup"><span data-stu-id="040c3-139">Pass absolute URIs, not relative URIs, to Windows Runtime types.</span></span> <span data-ttu-id="040c3-140">「[Windows ランタイムへの URI の引き渡し](https://docs.microsoft.com/dotnet/standard/cross-platform/passing-a-uri-to-the-windows-runtime)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-140">See [Passing a URI to the Windows Runtime](https://docs.microsoft.com/dotnet/standard/cross-platform/passing-a-uri-to-the-windows-runtime).</span></span>

## <a name="launchers-and-choosers"></a><span data-ttu-id="040c3-141">ランチャーとセレクター</span><span class="sxs-lookup"><span data-stu-id="040c3-141">Launchers and Choosers</span></span>

<span data-ttu-id="040c3-142">ランチャー、チューザーと (で見つかった、 **Microsoft.Phone.Tasks**名前空間)、Windows Phone Silverlight アプリ、写真を選択する、電子メールの構成などの一般的な操作を実行するオペレーティング システムと通信することができますか別のアプリとは、特定の種類のデータを共有します。</span><span class="sxs-lookup"><span data-stu-id="040c3-142">With Launchers and Choosers (found in the **Microsoft.Phone.Tasks** namespace), a Windows Phone Silverlight app can interact with the operating system to perform common operations such as composing an email, choosing a photo, or sharing certain kinds of data with another app.</span></span> <span data-ttu-id="040c3-143">検索**Microsoft.Phone.Tasks** 、トピックの「 [Windows 10 の名前空間とクラス マッピングを Windows Phone Silverlight](wpsl-to-uwp-namespace-and-class-mappings.md) UWP 同等型が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="040c3-143">Search for **Microsoft.Phone.Tasks** in the topic [Windows Phone Silverlight to Windows 10 namespace and class mappings](wpsl-to-uwp-namespace-and-class-mappings.md) to find the equivalent UWP type.</span></span> <span data-ttu-id="040c3-144">これには、ランチャーおよびピッカーと呼ばれる同様のメカニズムから、アプリ間でデータを共有するコントラクトの実装に至るまで、一連の型が含まれます。</span><span class="sxs-lookup"><span data-stu-id="040c3-144">These range from similar mechanisms, called launchers and pickers, to implementing a contract for sharing data between apps.</span></span>

<span data-ttu-id="040c3-145">Windows Phone Silverlight アプリを配置できるに休止状態または廃棄も、たとえば、写真の選択タスクを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="040c3-145">A Windows Phone Silverlight app can be put into a dormant state or even tombstoned when using, for example, the photo Chooser task.</span></span> <span data-ttu-id="040c3-146">UWP アプリは、[**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) クラスの使用中はアクティブで実行中のままになります。</span><span class="sxs-lookup"><span data-stu-id="040c3-146">A UWP app remains active and running while using the [**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) class.</span></span>

## <a name="monetization-trial-mode-and-in-app-purchases"></a><span data-ttu-id="040c3-147">収益化 (試用モードとアプリ内購入)</span><span class="sxs-lookup"><span data-stu-id="040c3-147">Monetization (trial mode and in-app purchases)</span></span>

<span data-ttu-id="040c3-148">Windows Phone Silverlight アプリが、UWP を使用できます [**CurrentApp** ](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Store.CurrentApp)クラスの試用版モードとアプリ内のほとんどは、機能を購入できるように、コードを移植する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="040c3-148">A Windows Phone Silverlight app can use the UWP [**CurrentApp**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Store.CurrentApp) class for most of its trial mode and in-app purchase functionality, so that code doesn't need to be ported.</span></span> <span data-ttu-id="040c3-149">しかし、Windows Phone Silverlight アプリを呼び出す**MarketplaceDetailTask.Show**購入アプリを提供します。</span><span class="sxs-lookup"><span data-stu-id="040c3-149">But, a Windows Phone Silverlight app calls **MarketplaceDetailTask.Show** to offer the app for purchase:</span></span>

```csharp
    private void Buy()
    {
        MarketplaceDetailTask marketplaceDetailTask = new MarketplaceDetailTask();
        marketplaceDetailTask.ContentType = MarketplaceContentType.Applications;
        marketplaceDetailTask.Show();
    }
```

<span data-ttu-id="040c3-150">UWP の  [**RequestAppPurchaseAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.requestapppurchaseasync) メソッドを呼び出すコードを移植します。</span><span class="sxs-lookup"><span data-stu-id="040c3-150">Port that code to call the UWP [**RequestAppPurchaseAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.requestapppurchaseasync) method:</span></span>

```csharp
    private async void Buy()
    {
        await Windows.ApplicationModel.Store.CurrentApp.RequestAppPurchaseAsync(false);
    }
```

<span data-ttu-id="040c3-151">テスト目的のためにアプリ購入機能およびアプリ内購入機能をシミュレートするコードがある場合は、代わりに [**CurrentAppSimulator**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Store.CurrentAppSimulator) クラスを使うようにこのコードを移植できます。</span><span class="sxs-lookup"><span data-stu-id="040c3-151">If you have code that simulates your app purchase and in-app purchase features for testing purposes, then you can port that to use the [**CurrentAppSimulator**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Store.CurrentAppSimulator) class instead.</span></span>

## <a name="notifications-for-tile-or-toast-updates"></a><span data-ttu-id="040c3-152">タイルまたはトーストの更新通知</span><span class="sxs-lookup"><span data-stu-id="040c3-152">Notifications for tile or toast updates</span></span>

<span data-ttu-id="040c3-153">通知は、Windows Phone Silverlight アプリにプッシュ通知のモデルの拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="040c3-153">Notifications are an extension of the push notification model for Windows Phone Silverlight apps.</span></span> <span data-ttu-id="040c3-154">Windows プッシュ通知サービス (WNS) から通知を受信した場合、タイル更新またはトーストにより UI にこの情報を提示できます。</span><span class="sxs-lookup"><span data-stu-id="040c3-154">When you receive a notification from the Windows Push Notification Service (WNS), you can surface the info to the UI with a tile update or with a toast.</span></span> <span data-ttu-id="040c3-155">通知機能の UI 側の移植については、「[タイルとトースト](w8x-to-uwp-porting-xaml-and-ui.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-155">For porting the UI side of your notification features, see [Tiles and toasts](w8x-to-uwp-porting-xaml-and-ui.md).</span></span>

<span data-ttu-id="040c3-156">UWP アプリで通知を使う方法について詳しくは、「[トースト通知の送信](https://docs.microsoft.com/previous-versions/windows/apps/hh868266(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-156">For more details on the use of notifications in a UWP app, see [Sending toast notifications](https://docs.microsoft.com/previous-versions/windows/apps/hh868266(v=win.10)).</span></span>

<span data-ttu-id="040c3-157">C++、C#、または Visual Basic を使った Windows ランタイム アプリでのタイル、トースト、バッジ、バナー、通知の使用についての情報とチュートリアルは、「[タイル、バッジ、トースト通知の操作](https://docs.microsoft.com/previous-versions/windows/apps/hh868259(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-157">For info and tutorials on using tiles, toasts, badges, banners, and notifications in a Windows Runtime app using C++, C#, or Visual Basic, see [Working with tiles, badges, and toast notifications](https://docs.microsoft.com/previous-versions/windows/apps/hh868259(v=win.10)).</span></span>

## <a name="storage-file-access"></a><span data-ttu-id="040c3-158">ストレージ (ファイル アクセス)</span><span class="sxs-lookup"><span data-stu-id="040c3-158">Storage (file access)</span></span>

<span data-ttu-id="040c3-159">分離ストレージ内のキー/値ペアとしてアプリの設定を格納する Windows Phone Silverlight コードは簡単に移植します。</span><span class="sxs-lookup"><span data-stu-id="040c3-159">Windows Phone Silverlight code that stores app settings as key-value pairs in isolated storage is easily ported.</span></span> <span data-ttu-id="040c3-160">ここで例を示します前に、と後、最初に、Windows Phone の Silverlight バージョン。</span><span class="sxs-lookup"><span data-stu-id="040c3-160">Here is a before-and-after example, first the Windows Phone Silverlight version:</span></span>

```csharp
    var propertySet = IsolatedStorageSettings.ApplicationSettings;
    const string key = "favoriteAuthor";
    propertySet[key] = "Charles Dickens";
    propertySet.Save();
    string myFavoriteAuthor = propertySet.Contains(key) ? (string)propertySet[key] : "<none>";
```

<span data-ttu-id="040c3-161">次に相当する UWP の要素を示します。</span><span class="sxs-lookup"><span data-stu-id="040c3-161">And the UWP equivalent:</span></span>

```csharp
    var propertySet = Windows.Storage.ApplicationData.Current.LocalSettings.Values;
    const string key = "favoriteAuthor";
    propertySet[key] = "Charles Dickens";
    string myFavoriteAuthor = propertySet.ContainsKey(key) ? (string)propertySet[key] : "<none>";
```

<span data-ttu-id="040c3-162">サブセットですが、 **Windows.Storage**名前空間が使用できるようにするには、多くの Windows Phone Silverlight アプリの実行ファイルの i/o、 **IsolatedStorageFile**クラスではサポートされているため長くなります。</span><span class="sxs-lookup"><span data-stu-id="040c3-162">Although a subset of the **Windows.Storage** namespace is available to them, many Windows Phone Silverlight apps perform file i/o with the **IsolatedStorageFile** class because it has been supported for longer.</span></span> <span data-ttu-id="040c3-163">仮定**IsolatedStorageFile**が記述して、まず、Windows Phone の Silverlight バージョンのファイルの読み取りの前に、と後例を示します。 使用されています。</span><span class="sxs-lookup"><span data-stu-id="040c3-163">Assuming that **IsolatedStorageFile** is being used, here's a before-and-after example of writing and reading a file, first the Windows Phone Silverlight version:</span></span>

```csharp
    const string filename = "FavoriteAuthor.txt";
    using (var store = IsolatedStorageFile.GetUserStoreForApplication())
    {
        using (var streamWriter = new StreamWriter(store.CreateFile(filename)))
        {
            streamWriter.Write("Charles Dickens");
        }
        using (var StreamReader = new StreamReader(store.OpenFile(filename, FileMode.Open, FileAccess.Read)))
        {
            string myFavoriteAuthor = StreamReader.ReadToEnd();
        }
    }
```

<span data-ttu-id="040c3-164">そして、UWP を使う同じ機能です。</span><span class="sxs-lookup"><span data-stu-id="040c3-164">And the same functionality using the UWP:</span></span>

```csharp
    const string filename = "FavoriteAuthor.txt";
    var store = Windows.Storage.ApplicationData.Current.LocalFolder;
    Windows.Storage.StorageFile file = await store.CreateFileAsync(filename, Windows.Storage.CreationCollisionOption.ReplaceExisting);
    await Windows.Storage.FileIO.WriteTextAsync(file, "Charles Dickens");
    file = await store.GetFileAsync(filename);
    string myFavoriteAuthor = await Windows.Storage.FileIO.ReadTextAsync(file);
```

<span data-ttu-id="040c3-165">Windows Phone Silverlight アプリでは、オプションの SD カードに読み取り専用のアクセスを持ちます。</span><span class="sxs-lookup"><span data-stu-id="040c3-165">A Windows Phone Silverlight app has read-only access to the optional SD card.</span></span> <span data-ttu-id="040c3-166">UWP アプリは、オプションの SD カードに読み取り専用のアクセスを行います。</span><span class="sxs-lookup"><span data-stu-id="040c3-166">A UWP app has read-write access to the SD card.</span></span> <span data-ttu-id="040c3-167">詳しくは、「[SD カードへのアクセス](https://docs.microsoft.com/windows/uwp/files/access-the-sd-card)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-167">For more info, see [Access the SD card](https://docs.microsoft.com/windows/uwp/files/access-the-sd-card).</span></span>

<span data-ttu-id="040c3-168">UWP アプリでの写真、音楽、ビデオ ファイルへのアクセスについて詳しくは、「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](https://docs.microsoft.com/windows/uwp/files/quickstart-managing-folders-in-the-music-pictures-and-videos-libraries)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-168">For info about accessing photos, music, and video files in a UWP app, see [Files and folders in the Music, Pictures, and Videos libraries](https://docs.microsoft.com/windows/uwp/files/quickstart-managing-folders-in-the-music-pictures-and-videos-libraries).</span></span>

<span data-ttu-id="040c3-169">詳しくは、「[ファイル、フォルダー、およびライブラリ](https://docs.microsoft.com/windows/uwp/files/index)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="040c3-169">For more info, see [Files, folders, and libraries](https://docs.microsoft.com/windows/uwp/files/index).</span></span>

<span data-ttu-id="040c3-170">次のトピックは、「[フォーム ファクターと UX の移植](wpsl-to-uwp-form-factors-and-ux.md)」です。</span><span class="sxs-lookup"><span data-stu-id="040c3-170">The next topic is [Porting for form factor and UX](wpsl-to-uwp-form-factors-and-ux.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="040c3-171">関連トピック</span><span class="sxs-lookup"><span data-stu-id="040c3-171">Related topics</span></span>

* [<span data-ttu-id="040c3-172">Namespace およびクラスのマッピング</span><span class="sxs-lookup"><span data-stu-id="040c3-172">Namespace and class mappings</span></span>](wpsl-to-uwp-namespace-and-class-mappings.md)
 

