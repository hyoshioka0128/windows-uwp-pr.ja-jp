---
Description: Microsoft Store Services SDK が提供するライブラリとツールを利用すると、収益とユーザーの獲得を図る機能をアプリに追加できます。
title: Microsoft Store Services SDK を使ってユーザーとの関係を深める
ms.assetid: 518516DB-70A7-49C4-B3B6-CD8A98320B9C
ms.date: 08/21/2017
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store Services SDK
ms.localizationpriority: medium
ms.openlocfilehash: 48a19b2fc32733e13cb9a7b730bad7741307c328
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372806"
---
# <a name="engage-customers-with-the-microsoft-store-services-sdk"></a><span data-ttu-id="03a3c-104">Microsoft Store Services SDK を使ってユーザーとの関係を深める</span><span class="sxs-lookup"><span data-stu-id="03a3c-104">Engage customers with the Microsoft Store Services SDK</span></span>

<span data-ttu-id="03a3c-105">Microsoft Store Services SDK の提供する際に役立つ機能など、アプリを対象となる通知を送信して、A を実行して、ユニバーサル Windows プラットフォーム (UWP) アプリでの顧客とかかわります/、B はアプリで実験します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-105">The Microsoft Store Services SDK provides features that help you engage with customers in your Universal Windows Platform (UWP) apps, such as sending targeted notifications to your apps and running A/B experiments in your apps.</span></span> <span data-ttu-id="03a3c-106">この SDK は、Visual Studio 2015 とそれ以降のバージョンの Visual Studio 用の拡張です。</span><span class="sxs-lookup"><span data-stu-id="03a3c-106">This SDK is an extension for Visual Studio 2015 and later versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="03a3c-107">UWP アプリで広告を表示するには、Microsoft Store Services SDK ではなく [Microsoft Advertising SDK](https://aka.ms/ads-sdk-uwp) を使います。</span><span class="sxs-lookup"><span data-stu-id="03a3c-107">To display ads in your UWP apps, use the [Microsoft Advertising SDK](https://aka.ms/ads-sdk-uwp) instead of the Microsoft Store Services SDK.</span></span> <span data-ttu-id="03a3c-108">Advertising ライブラリは、Microsoft Store Services SDK から Microsoft Advertising SDK に移動されました。</span><span class="sxs-lookup"><span data-stu-id="03a3c-108">The advertising libraries have been moved from the Microsoft Store Services SDK to the Microsoft Advertising SDK.</span></span> <span data-ttu-id="03a3c-109">詳しくは、「[アプリでの広告の表示](display-ads-in-your-app.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="03a3c-109">For more information, see [Display ads in your app](display-ads-in-your-app.md).</span></span>



## <a name="scenarios-supported-by-the-microsoft-store-services-sdk"></a><span data-ttu-id="03a3c-110">Microsoft Store Services SDK によりサポートされるシナリオ</span><span class="sxs-lookup"><span data-stu-id="03a3c-110">Scenarios supported by the Microsoft Store Services SDK</span></span>

<span data-ttu-id="03a3c-111">この Microsoft Store Services SDK では現在、UWP アプリ向けに次のシナリオがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="03a3c-111">The Microsoft Store Services SDK currently supports the following scenarios for UWP apps.</span></span> <span data-ttu-id="03a3c-112">API リファレンス ドキュメントについては、「[Microsoft Store Services SDK API リファレンス](https://docs.microsoft.com/uwp/api/overview/engagement)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="03a3c-112">For API reference documentation, see [Microsoft Store Services SDK API reference](https://docs.microsoft.com/uwp/api/overview/engagement).</span></span>

|  <span data-ttu-id="03a3c-113">シナリオ</span><span class="sxs-lookup"><span data-stu-id="03a3c-113">Scenario</span></span>  |  <span data-ttu-id="03a3c-114">説明</span><span class="sxs-lookup"><span data-stu-id="03a3c-114">Description</span></span>   |
|------------|----------------|
|  [<span data-ttu-id="03a3c-115">実験を実行すると、UWP アプリ B のテスト</span><span class="sxs-lookup"><span data-stu-id="03a3c-115">Run experiments in your UWP app with A/B testing</span></span>](run-app-experiments-with-a-b-testing.md)    |  <span data-ttu-id="03a3c-116">ユニバーサル Windows プラットフォーム (UWP) アプリで A/B テストを実施して、すべてのユーザー向けに機能を公開する前に、一部のユーザーに対して機能の有効性を測定することができます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-116">Run A/B tests in your Universal Windows Platform (UWP) app to measure the effectiveness of features on some customers before you release the features to everyone.</span></span> <span data-ttu-id="03a3c-117">使用して、パートナー センターで実験を定義した後、 [StoreServicesExperimentVariation](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesexperimentvariation)アプリでは、実験では、このデータを使用するテストは、機能の動作を変更するは、バリエーションを取得するクラスを使用して、[LogForVariation](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicescustomeventlogger.logforvariation)パートナー センターにイベントを表示し、変換イベントを送信する方法。</span><span class="sxs-lookup"><span data-stu-id="03a3c-117">After you define an experiment in Partner Center, use the [StoreServicesExperimentVariation](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesexperimentvariation) class to get variations for your experiment in your app, use this data to modify the behavior of the feature you are testing, and then use the [LogForVariation](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicescustomeventlogger.logforvariation) method to send view event and conversion events to Partner Center.</span></span> <span data-ttu-id="03a3c-118">最後に、パートナー センターを使用して、結果を表示したり、実験を管理します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-118">Finally, use Partner Center to view the results and manage the experiment.</span></span>  |
|  [<span data-ttu-id="03a3c-119">UWP アプリからのフィードバック ハブを起動します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-119">Launch Feedback Hub from your UWP app</span></span>](launch-feedback-hub-from-your-app.md)    |  <span data-ttu-id="03a3c-120">UWP アプリで [StoreServicesFeedbackLauncher](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesfeedbacklauncher) クラスを使用し、Windows 10 ユーザーをフィードバック Hub に誘導して、ユーザーが問題、提案、賛成票を送信できるようにします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-120">Use the [StoreServicesFeedbackLauncher](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesfeedbacklauncher) class in your UWP app to direct your Windows 10 customers to Feedback Hub, where they can submit problems, suggestions, and upvotes.</span></span> <span data-ttu-id="03a3c-121">次に、パートナー センターの[フィードバック レポート](../publish/feedback-report.md)でこのフィードバックを管理します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-121">Then, manage this feedback in the [Feedback report](../publish/feedback-report.md) in Partner Center.</span></span> |
|  [<span data-ttu-id="03a3c-122">パートナー センターのプッシュ通知を受信する UWP アプリを構成します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-122">Configure your UWP app to receive Partner Center push notifications</span></span>](configure-your-app-to-receive-dev-center-notifications.md)    |  <span data-ttu-id="03a3c-123">使用して、 [StoreServicesEngagementManager](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager)パートナー センターを使用してお客様に送信するターゲットを絞ったプッシュ通知を受信するアプリを登録する UWP アプリでのクラス。</span><span class="sxs-lookup"><span data-stu-id="03a3c-123">Use the [StoreServicesEngagementManager](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicesengagementmanager) class in your UWP app to register your app to receive targeted push notifications that you send to your customers using Partner Center.</span></span>  |
|   [<span data-ttu-id="03a3c-124">パートナー センターでの使用状況レポートの UWP アプリでカスタム イベントを記録します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-124">Log custom events in your UWP app for the Usage report in Partner Center</span></span>](log-custom-events-for-dev-center.md)   |  <span data-ttu-id="03a3c-125">使用して、 [StoreServicesCustomEventLogger](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicescustomeventlogger.log)パートナー センターでアプリに関連付けられているカスタム イベントを記録する UWP アプリでのクラス。</span><span class="sxs-lookup"><span data-stu-id="03a3c-125">Use the [StoreServicesCustomEventLogger](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement.storeservicescustomeventlogger.log) class in your UWP app to log custom events that are associated with your app in Partner Center.</span></span> <span data-ttu-id="03a3c-126">その後、カスタム イベントの合計出現回数を確認、**カスタム イベント**のセクション、[使用状況レポート](https://docs.microsoft.com/windows/uwp/publish/usage-report)パートナー センターでします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-126">Then, review the total occurrences for your custom events in the **Custom events** section of the [Usage report](https://docs.microsoft.com/windows/uwp/publish/usage-report) in Partner Center.</span></span>  |

<span id="prerequisites" />

## <a name="prerequisites"></a><span data-ttu-id="03a3c-127">前提条件</span><span class="sxs-lookup"><span data-stu-id="03a3c-127">Prerequisites</span></span>

<span data-ttu-id="03a3c-128">Microsoft Store Services SDK には以下が必要となります。</span><span class="sxs-lookup"><span data-stu-id="03a3c-128">The Microsoft Store Services SDK requires:</span></span>

* <span data-ttu-id="03a3c-129">Visual Studio 2015 またはそれ以降のバージョン。</span><span class="sxs-lookup"><span data-stu-id="03a3c-129">Visual Studio 2015 or a later version.</span></span>
* <span data-ttu-id="03a3c-130">Visual Studio と共にインストールされている ユニバーサル Windows アプリ用 Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="03a3c-130">Visual Studio Tools for Universal Windows Apps installed with your version of Visual Studio.</span></span>

<span id="install" />

## <a name="install-the-sdk"></a><span data-ttu-id="03a3c-131">SDK のインストール</span><span class="sxs-lookup"><span data-stu-id="03a3c-131">Install the SDK</span></span>

<span data-ttu-id="03a3c-132">開発用コンピューターに Microsoft Store Services SDK をインストールするには、次の 2 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="03a3c-132">There are two options for installing the Microsoft Store Services SDK on your development computer:</span></span>

* <span data-ttu-id="03a3c-133">**MSI インストーラー**&nbsp;&nbsp;[ここ](https://aka.ms/store-em-sdk)から利用できる MSI インストーラーを使って SDK をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-133">**MSI installer**&nbsp;&nbsp;You can install the SDK via the MSI installer available [here](https://aka.ms/store-em-sdk).</span></span>
* <span data-ttu-id="03a3c-134">**NuGet パッケージ**&nbsp;&nbsp;NuGet パッケージとして、SDK をインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-134">**NuGet package**&nbsp;&nbsp;You can install the SDK as a NuGet package.</span></span>

<span data-ttu-id="03a3c-135">マイクロソフトでは定期的に、向上したパフォーマンスと新しい機能を備えた、新しいバージョンの Microsoft Store Services SDK をリリースしています。</span><span class="sxs-lookup"><span data-stu-id="03a3c-135">Microsoft periodically releases new versions of the Microsoft Store Services SDK with performance improvements and new features.</span></span> <span data-ttu-id="03a3c-136">開発用コンピューターに Microsoft Store Services SDK を使っている既存のプロジェクトがあり、そのプロジェクトで最新バージョンを使う場合は、最新バージョンの SDK をダウンロードしてインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="03a3c-136">If you have existing projects that use the SDK and you want to use the latest version, download and install the latest version of the SDK on your development computer.</span></span>

<span id="install-msi" />

### <a name="install-via-msi"></a><span data-ttu-id="03a3c-137">MSI によるインストール</span><span class="sxs-lookup"><span data-stu-id="03a3c-137">Install via MSI</span></span>

<span data-ttu-id="03a3c-138">MSI インストーラーを使って Microsoft Store Services SDK をインストールするには</span><span class="sxs-lookup"><span data-stu-id="03a3c-138">To install the Microsoft Store Services SDK via the MSI installer:</span></span>

1.  <span data-ttu-id="03a3c-139">Visual Studio のすべてのインスタンスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-139">Close all instances of Visual Studio.</span></span>

2. <span data-ttu-id="03a3c-140">Microsoft Store Engagement and Monetization SDK、Universal Ad Client SDK、または Ad Mediator 拡張機能を以前にインストールしていた場合は、それらの SDK をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-140">If you previously installed the Microsoft Store Engagement and Monetization SDK, Universal Ad Client SDK, or Ad Mediator extension, uninstall these SDKs now.</span></span> <span data-ttu-id="03a3c-141">必要に応じて、**コマンド プロンプト** ウィンドウを開き、次のコマンドを実行して、Visual Studio と共にインストールされている可能性があり、コンピューター上のインストールされているプログラムの一覧には表示されない可能性がある、古い SDK のバージョンをすべて削除します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-141">Optionally, open a **Command Prompt** window and run these commands to clean out any older SDK versions that may have been installed with Visual Studio, but which may not appear in the list of installed programs on your computer:</span></span>
    ```console
    MsiExec.exe /x{5C87A4DB-31C7-465E-9356-71B485B69EC8}
    MsiExec.exe /x{6AB13C21-C3EC-46E1-8009-6FD5EBEE515B}
    MsiExec.exe /x{6AC81125-8485-463D-9352-3F35A2508C11}
    ```

3.  <span data-ttu-id="03a3c-142">[Microsoft Store Services SDK](https://aka.ms/store-em-sdk) をダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-142">Download and install the [Microsoft Store Services SDK](https://aka.ms/store-em-sdk).</span></span> <span data-ttu-id="03a3c-143">インストールには数分かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="03a3c-143">It may take a few minutes to install.</span></span> <span data-ttu-id="03a3c-144">確実に処理が完了するまでお待ちください。</span><span class="sxs-lookup"><span data-stu-id="03a3c-144">Be sure and wait until the process has finished.</span></span>

4.  <span data-ttu-id="03a3c-145">Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-145">Restart Visual Studio.</span></span>

5.  <span data-ttu-id="03a3c-146">以前のバージョンの Microsoft Store Services SDK、Microsoft Advertising SDK、Universal Ad Client SDK、Microsoft Store Engagement and Monetization SDK のライブラリを参照する既存のプロジェクトがある場合には、Visual Studio でプロジェクトを開き、プロジェクトをクリーンしてリビルドすることをお勧めします (**ソリューション エクスプ ローラー**でプロジェクト ノードを右クリックして、 **[クリーン]** を選択し、次にもう一度プロジェクト ノードを右クリックして、 **[リビルド]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="03a3c-146">If you have an existing project that references libraries from any earlier version of the Microsoft Store Services SDK, Microsoft Advertising SDK, Universal Ad Client SDK, or Microsoft Store Engagement and Monetization SDK, we recommend that you open your project in Visual Studio and clean and rebuild your project (in **Solution Explorer**, right-click your project node and choose **Clean**, and then right-click your project node again and choose **Rebuild**).</span></span>

  <span data-ttu-id="03a3c-147">または、プロジェクトで初めて SDK を使う場合には、[アセンブリ参照をプロジェクトを追加する](#references)ことができます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-147">Otherwise, if you are using the SDK for the first time in your project, you are now ready to [add the assembly reference to your project](#references).</span></span>

<span id="install-nuget" />

### <a name="install-via-nuget"></a><span data-ttu-id="03a3c-148">NuGet によるインストール</span><span class="sxs-lookup"><span data-stu-id="03a3c-148">Install via NuGet</span></span>

<span data-ttu-id="03a3c-149">NuGet を使って Microsoft Store Services SDK をインストールするには</span><span class="sxs-lookup"><span data-stu-id="03a3c-149">To install the Microsoft Store Services SDK libraries via NuGet:</span></span>

1.  <span data-ttu-id="03a3c-150">Visual Studio のすべてのインスタンスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-150">Close all instances of Visual Studio.</span></span>

2. <span data-ttu-id="03a3c-151">Microsoft Store Engagement and Monetization SDK、Universal Ad Client SDK、または Ad Mediator 拡張機能を以前にインストールしていた場合は、それらの SDK をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-151">If you previously installed the Microsoft Store Engagement and Monetization SDK, Universal Ad Client SDK, or Ad Mediator extension, uninstall these SDKs now.</span></span> <span data-ttu-id="03a3c-152">必要に応じて、**コマンド プロンプト** ウィンドウを開き、次のコマンドを実行して、Visual Studio と共にインストールされている可能性があり、コンピューター上のインストールされているプログラムの一覧には表示されない可能性がある、古い SDK のバージョンをすべて削除します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-152">Optionally, open a **Command Prompt** window and run these commands to clean out any older SDK versions that may have been installed with Visual Studio, but which may not appear in the list of installed programs on your computer:</span></span>
    ```console
    MsiExec.exe /x{5C87A4DB-31C7-465E-9356-71B485B69EC8}
    MsiExec.exe /x{6AB13C21-C3EC-46E1-8009-6FD5EBEE515B}
    MsiExec.exe /x{6AC81125-8485-463D-9352-3F35A2508C11}
    ```

3.  <span data-ttu-id="03a3c-153">Visual Studio を起動し、Microsoft Store Services SDK を使用するプロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-153">Start Visual Studio and open the project in which you want to use the Microsoft Store Services SDK.</span></span>
    > [!NOTE]
    > <span data-ttu-id="03a3c-154">プロジェクトに SDK の以前の MSI インストールからのライブラリの参照が既に含まれている場合は、これらの参照をプロジェクトから削除します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-154">If your project already includes library references from an earlier MSI installation of the SDK, remove these references from your project.</span></span> <span data-ttu-id="03a3c-155">これらの参照は、参照先のライブラリが前の手順で削除されたため、その隣に警告アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-155">These references will have warning icons next to them because the libraries they reference were removed in the previous steps.</span></span>

4. <span data-ttu-id="03a3c-156">Visual Studio で、 **[プロジェクト]** と **[NuGet パッケージの管理]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-156">In Visual Studio, click **Project** and **Manage NuGet Packages**.</span></span>

5. <span data-ttu-id="03a3c-157">検索ボックスに「**Microsoft.Services.Store.Engagement**」と入力し、Microsoft.Services.Store.Engagement パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-157">In the search box, type **Microsoft.Services.Store.Engagement** and install the Microsoft.Services.Store.Engagement package.</span></span> <span data-ttu-id="03a3c-158">パッケージのインストールが完了したら、ソリューションを保存します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-158">When the package is done installing, save your solution.</span></span>
    > [!NOTE]
    > <span data-ttu-id="03a3c-159">**[出力]** ウィンドウに、指定されたパスが長すぎることを示す*インストール パッケージ* エラーが表示されたとき、場合によっては、NuGet を構成して、既定の場所よりも短いパスで示される別の場所にパッケージを展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="03a3c-159">If the **Output** window reports an *Install-Package* error that indicates the specified path is too long, you may need to configure NuGet to extract packages to an alternate location with a shorter path than the default location.</span></span> <span data-ttu-id="03a3c-160">これを行うには、`repositoryPath` 値をコンピューターの nuget.config ファイルに追加し、それを短いフォルダーのパスに割り当て、そこに NuGet パッケージが展開されるようにします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-160">To do this, add the `repositoryPath` value to a nuget.config file on your computer and assign it to a short folder path where NuGet packages can be extracted.</span></span> <span data-ttu-id="03a3c-161">詳しくは、NuGet ドキュメントの[この記事](https://docs.nuget.org/ndocs/consume-packages/configuring-nuget-behavior)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="03a3c-161">For more information, see [this article](https://docs.nuget.org/ndocs/consume-packages/configuring-nuget-behavior) in the NuGet documentation.</span></span> <span data-ttu-id="03a3c-162">または、Visual Studio プロジェクトを短いパスを持つ別のフォルダーに移動してみることができます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-162">Alternatively, you can try moving your Visual Studio project to an alternate folder with a shorter path.</span></span> <span data-ttu-id="03a3c-163">問題が、グローバル パッケージ パスが長すぎるによっても原因。</span><span class="sxs-lookup"><span data-stu-id="03a3c-163">The problem could also be caused by your global packages path being too long.</span></span> <span data-ttu-id="03a3c-164">この場合、追加、 `globalPackagesFolder` nuget.config ファイルに値。</span><span class="sxs-lookup"><span data-stu-id="03a3c-164">In this case, add the `globalPackagesFolder` value into your nuget.config file.</span></span>

6. <span data-ttu-id="03a3c-165">プロジェクトが含まれている Visual Studio ソリューションを閉じ、そのソリューションを再度開きます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-165">Close the Visual Studio solution that contains your project and then reopen the solution.</span></span>

7.  <span data-ttu-id="03a3c-166">プロジェクトが NuGet によりインストールされた以前のバージョンの Microsoft Store Services SDK のライブラリを既に参照している場合で、プロジェクトを SDK の新しいリリースに更新する場合には、プロジェクトをクリーンしてリビルドすることをお勧めします (**ソリューション エクスプローラー**でプロジェクト ノードを右クリックして、 **[クリーン]** を選択し、次にもう一度プロジェクト ノードを右クリックして、 **[リビルド]** を選択します)。</span><span class="sxs-lookup"><span data-stu-id="03a3c-166">If your project already references libraries from an earlier version of the Microsoft Store Services SDK that was installed via NuGet and you have updated your project to a newer release of the SDK, we recommend that you clean and rebuild your project (in **Solution Explorer**, right-click your project node and choose **Clean**, and then right-click your project node again and choose **Rebuild**).</span></span>

  <span data-ttu-id="03a3c-167">または、プロジェクトで初めて SDK を使う場合には、[アセンブリ参照をプロジェクトを追加する](#references)ことができます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-167">Otherwise, if you are using the SDK for the first time in your project, you are now ready to [add the assembly reference to your project](#references).</span></span>

<span id="references" />

## <a name="add-the-assembly-reference-to-your-project"></a><span data-ttu-id="03a3c-168">アセンブリ参照をプロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="03a3c-168">Add the assembly reference to your project</span></span>

<span data-ttu-id="03a3c-169">+MSI インストーラーまたは NuGet により Microsoft Store Services SDK をインストールしたら、次の手順に従って UWP プロジェクトで SDK アセンブリを参照します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-169">After you install the Microsoft Store Services SDK via the MSI installer or NuGet, follow these instructions to reference the SDK assembly in your UWP project.</span></span>

1. <span data-ttu-id="03a3c-170">Visual Studio でプロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-170">Open your project in Visual Studio.</span></span>
    > [!NOTE]
    > <span data-ttu-id="03a3c-171">プロジェクトが JavaScript アプリで、ターゲットが **[任意の CPU]** になっている場合は、アーキテクチャ固有のビルド出力 (たとえば **[x86]** ) を使うようにプロジェクトを更新します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-171">If your project is a JavaScript app that targets **Any CPU**, update your project to use an architecture-specific build output (for example, **x86**).</span></span>

2. <span data-ttu-id="03a3c-172">**ソリューション エクスプローラー**で、 **[参照設定]** を右クリックし、 **[参照の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="03a3c-172">In **Solution Explorer**, right click **References** and select **Add Reference…**</span></span>

3. <span data-ttu-id="03a3c-173">**[参照マネージャー]** で **[ユニバーサル Windows]** を展開し、 **[拡張機能]** をクリックして、 **[Microsoft Engagement Framework]** の横のチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-173">In **Reference Manager**, expand **Universal Windows**, click **Extensions**, and then select the check box next to **Microsoft Engagement Framework**.</span></span> <span data-ttu-id="03a3c-174">これにより、[Microsoft.Services.Store.Engagement](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement) 名前空間の API を使用できます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-174">This enables you to use the APIs in the [Microsoft.Services.Store.Engagement](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement) namespace.</span></span>

3. <span data-ttu-id="03a3c-175">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="03a3c-175">Click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="03a3c-176">NuGet から SDK ライブラリをインストールした場合、プロジェクトには **Microsoft.Services.Store.Engagement** 参照が含められます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-176">If you installed the SDK libraries via NuGet, your project will contain a **Microsoft.Services.Store.Engagement** reference.</span></span> <span data-ttu-id="03a3c-177">**Microsoft.Services.Store.Engagement** の参照は (その中のライブラリではなく) NuGet パッケージを表し、これは無視することができます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-177">The **Microsoft.Services.Store.Engagement** reference represents the NuGet package (rather than the libraries in it), and you can ignore it.</span></span>

<span id="framework" />

## <a name="understanding-framework-packages-in-the-sdk"></a><span data-ttu-id="03a3c-178">SDK のフレームワーク パッケージを理解する</span><span class="sxs-lookup"><span data-stu-id="03a3c-178">Understanding framework packages in the SDK</span></span>

<span data-ttu-id="03a3c-179">Microsoft Store Services SDK の Microsoft.Services.Store.Engagement.dll ライブラリは、*フレームワーク パッケージ*として構成されています。</span><span class="sxs-lookup"><span data-stu-id="03a3c-179">The Microsoft.Services.Store.Engagement.dll library in the Microsoft Store Services SDK is configured as a *framework package*.</span></span> <span data-ttu-id="03a3c-180">このライブラリには、[Microsoft.Services.Store.Engagement](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement) 名前空間の API が含まれています。</span><span class="sxs-lookup"><span data-stu-id="03a3c-180">This library contains the APIs in the [Microsoft.Services.Store.Engagement](https://docs.microsoft.com/uwp/api/microsoft.services.store.engagement) namespace.</span></span>

<span data-ttu-id="03a3c-181">このライブラリはフレームワーク パッケージであるため、このライブラリを使用するバージョンのアプリをユーザーがインストールすると、このライブラリは、修正されてパフォーマンスが向上した新しいバージョンのライブラリが公開されるたびに、ユーザーのデバイスで Windows Update によって自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-181">Because this library is a framework package, this means that after a user installs a version of your app that uses this library, this library is automatically updated on their device through Windows Update whenever we publish a new version of the library with fixes and performance improvements.</span></span> <span data-ttu-id="03a3c-182">これにより、利用できる最新バージョンのライブラリがユーザーのデバイスに確実にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="03a3c-182">This helps to ensure that your customers always have the latest available version of the library installed on their devices.</span></span>

<span data-ttu-id="03a3c-183">このライブラリに新しい API や機能が導入された新しいバージョンの SDK がリリースされた場合は、これらの機能を使用するために最新バージョンの SDK をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="03a3c-183">If we release a new version of the SDK that introduces new APIs or features in this library, you will need to install the latest version of the SDK to use those features.</span></span> <span data-ttu-id="03a3c-184">このシナリオでは、更新されたアプリをストアに公開する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="03a3c-184">In this scenario, you would also need to publish your updated app to the Store.</span></span>

## <a name="related-topics"></a><span data-ttu-id="03a3c-185">関連トピック</span><span class="sxs-lookup"><span data-stu-id="03a3c-185">Related topics</span></span>

* [<span data-ttu-id="03a3c-186">Microsoft Store Services SDK の API リファレンス</span><span class="sxs-lookup"><span data-stu-id="03a3c-186">Microsoft Store Services SDK API reference</span></span>](https://docs.microsoft.com/uwp/api/overview/engagement)
* [<span data-ttu-id="03a3c-187">A/B テストによる実験の実行</span><span class="sxs-lookup"><span data-stu-id="03a3c-187">Run experiments with A/B testing</span></span>](run-app-experiments-with-a-b-testing.md)
* [<span data-ttu-id="03a3c-188">アプリからのフィードバック Hub の起動</span><span class="sxs-lookup"><span data-stu-id="03a3c-188">Launch Feedback Hub from your app</span></span>](launch-feedback-hub-from-your-app.md)
* [<span data-ttu-id="03a3c-189">パートナー センターのプッシュ通知を受信するようにアプリを設定する</span><span class="sxs-lookup"><span data-stu-id="03a3c-189">Configure your app to receive Partner Center push notifications</span></span>](configure-your-app-to-receive-dev-center-notifications.md)
* [<span data-ttu-id="03a3c-190">パートナー センターのカスタム イベントをログに記録する</span><span class="sxs-lookup"><span data-stu-id="03a3c-190">Log custom events for Partner Center</span></span>](log-custom-events-for-dev-center.md)
