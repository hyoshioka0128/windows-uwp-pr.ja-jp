---
title: インプロセス バックグラウンド タスクの作成と登録
description: フォアグラウンド アプリと同じプロセスで実行されるインプロセスのタスクを作成して登録します。
ms.date: 11/03/2017
ms.topic: article
keywords: windows 10、uwp、バック グラウンド タスク
ms.assetid: d99de93b-e33b-45a9-b19f-31417f1e9354
ms.localizationpriority: medium
ms.openlocfilehash: f37ffe21795fc68ff72b4e6f1de591c96d2f8b90
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366213"
---
# <a name="create-and-register-an-in-process-background-task"></a><span data-ttu-id="660af-104">インプロセス バックグラウンド タスクの作成と登録</span><span class="sxs-lookup"><span data-stu-id="660af-104">Create and register an in-process background task</span></span>

<span data-ttu-id="660af-105">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="660af-105">**Important APIs**</span></span>

-   [<span data-ttu-id="660af-106">**IBackgroundTask**</span><span class="sxs-lookup"><span data-stu-id="660af-106">**IBackgroundTask**</span></span>](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask)
-   [<span data-ttu-id="660af-107">**BackgroundTaskBuilder**</span><span class="sxs-lookup"><span data-stu-id="660af-107">**BackgroundTaskBuilder**</span></span>](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder)
-   [<span data-ttu-id="660af-108">**BackgroundTaskCompletedEventHandler**</span><span class="sxs-lookup"><span data-stu-id="660af-108">**BackgroundTaskCompletedEventHandler**</span></span>](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskcompletedeventhandler)

<span data-ttu-id="660af-109">このトピックでは、アプリと同じプロセスで実行されるバックグラウンド タスクを作成して登録する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="660af-109">This topic demonstrates how to create and register a background task that runs in the same process as your app.</span></span>

<span data-ttu-id="660af-110">インプロセスのバック グラウンド タスクはアウトプロセスのバック グラウンド タスクよりも実装が簡単です。</span><span class="sxs-lookup"><span data-stu-id="660af-110">In-process background tasks are simpler to implement than out-of-process background tasks.</span></span> <span data-ttu-id="660af-111">ただし、インプロセスのバックグラウンド タスクでは回復力が低下します。</span><span class="sxs-lookup"><span data-stu-id="660af-111">However, they are less resilient.</span></span> <span data-ttu-id="660af-112">インプロセスのバックグラウンド タスクで実行中のコードがクラッシュすると、アプリがダウンします。</span><span class="sxs-lookup"><span data-stu-id="660af-112">If the code running in an in-process background task crashes, it will take down your app.</span></span> <span data-ttu-id="660af-113">また、[DeviceUseTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.deviceusetrigger)、[DeviceServicingTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.deviceservicingtrigger)、**IoTStartupTask** はインプロセス モデルで使用できないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="660af-113">Also note that [DeviceUseTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.deviceusetrigger), [DeviceServicingTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.deviceservicingtrigger) and **IoTStartupTask** cannot be used with the in-process model.</span></span> <span data-ttu-id="660af-114">アプリケーション内で VoIP バックグラウンド タスクをアクティブ化することもできません。</span><span class="sxs-lookup"><span data-stu-id="660af-114">Activating a VoIP background task within your application is also not possible.</span></span> <span data-ttu-id="660af-115">これらのトリガーとタスクは、アウトプロセスのバックグラウンド タスク モデルを使用してサポートされています。</span><span class="sxs-lookup"><span data-stu-id="660af-115">These triggers and tasks are still supported using the out-of-process background task model.</span></span>

<span data-ttu-id="660af-116">バックグラウンド アクティビティは、実行時間制限を超えて実行された場合に、アプリのフォアグラウンド プロセス内で実行されているときでも終了できます。</span><span class="sxs-lookup"><span data-stu-id="660af-116">Be aware that background activity can be terminated even when running inside the app's foreground process if it runs past execution time limits.</span></span> <span data-ttu-id="660af-117">特定の目的では、別のプロセスで実行するバックグラウンド タスクに作業を分離した場合の回復性が有用です。</span><span class="sxs-lookup"><span data-stu-id="660af-117">For some purposes the resiliency of separating work into a background task that runs in a separate process is still useful.</span></span> <span data-ttu-id="660af-118">バックグラウンドの作業をフォアグラウンド アプリケーションとは別のタスクとして保持することは、フォアグラウンド アプリケーションとの通信を必要としない作業にとって最適なオプションである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="660af-118">Keeping background work as a task separate from the foreground application may be the best option for work that does not require communication with the foreground application.</span></span>

## <a name="fundamentals"></a><span data-ttu-id="660af-119">基本事項</span><span class="sxs-lookup"><span data-stu-id="660af-119">Fundamentals</span></span>

<span data-ttu-id="660af-120">インプロセス モデルでは、アプリがフォアグラウンドまたはバックグラウンドで実行されるときの改善された通知によってアプリケーションのライフサイクルが強化されます。</span><span class="sxs-lookup"><span data-stu-id="660af-120">The in-process model enhances the application lifecycle with improved notifications for when your app is in the foreground or in the background.</span></span> <span data-ttu-id="660af-121">2 つの新しいイベントはこれらの遷移のアプリケーション オブジェクトから使用できます。[**EnteredBackground** ](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication.enteredbackground)と[ **LeavingBackground**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication.leavingbackground)します。</span><span class="sxs-lookup"><span data-stu-id="660af-121">Two new events are available from the Application object for these transitions: [**EnteredBackground**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication.enteredbackground) and [**LeavingBackground**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication.leavingbackground).</span></span> <span data-ttu-id="660af-122">これらのイベントは、アプリケーションの表示状態に基づくアプリケーションのライフサイクルに適合します。これらのイベントの詳細とアプリケーションのライフサイクルに与える影響については、[アプリのライフサイクル](app-lifecycle.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="660af-122">These events fit into the application lifecycle based on the visibility state of your application Read more about these events and how they affect the application lifecycle at [App lifecycle](app-lifecycle.md).</span></span>

<span data-ttu-id="660af-123">大まかに言うと、**EnteredBackground** イベントは、アプリがバックグラウンドで実行されている間に実行されるコードを実行します。また、**LeavingBackground** イベントは、アプリがフォアグラウンドに移動したことを知るために処理します。</span><span class="sxs-lookup"><span data-stu-id="660af-123">At a high level, you will handle the **EnteredBackground** event to run your code that will execute while your app is running in the background, and handle **LeavingBackground** to know when your app has moved to the foreground.</span></span>

## <a name="register-your-background-task-trigger"></a><span data-ttu-id="660af-124">バックグラウンド タスク トリガーを登録する</span><span class="sxs-lookup"><span data-stu-id="660af-124">Register your background task trigger</span></span>

<span data-ttu-id="660af-125">インプロセスのバックグラウンド アクティビティの登録は、アウトプロセスのバックグラウンド アクティビティを登録する方法とほぼ同じです。</span><span class="sxs-lookup"><span data-stu-id="660af-125">In-process background activity is registered much the same as out-of-process background activity.</span></span> <span data-ttu-id="660af-126">すべてのバックグラウンド トリガーは、[BackgroundTaskBuilder](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder?f=255&MSPPError=-2147217396) を使用した登録から始まります。</span><span class="sxs-lookup"><span data-stu-id="660af-126">All background triggers start with registration using the [BackgroundTaskBuilder](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="660af-127">ビルダーを使用すると、必要なすべての値を 1 か所で設定できるため、簡単にバックグラウンド タスクを登録できます。</span><span class="sxs-lookup"><span data-stu-id="660af-127">The builder makes it easy to register a background task by setting all required values in one place:</span></span>

> [!div class="tabbedCodeSnippets"]
> ```cs
> var builder = new BackgroundTaskBuilder();
> builder.Name = "My Background Trigger";
> builder.SetTrigger(new TimeTrigger(15, true));
> // Do not set builder.TaskEntryPoint for in-process background tasks
> // Here we register the task and work will start based on the time trigger.
> BackgroundTaskRegistration task = builder.Register();
> ```

> [!NOTE]
> <span data-ttu-id="660af-128">ユニバーサル Windows アプリは、どの種類のバックグラウンド トリガーを登録する場合でも、先に [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="660af-128">Universal Windows apps must call [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) before registering any of the background trigger types.</span></span>
> <span data-ttu-id="660af-129">更新プログラムのリリース後にユニバーサル Windows アプリが引き続き適切に実行されるようにするには、更新後にアプリが起動する際に、[**RemoveAccess**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess)、[**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) の順に呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="660af-129">To ensure that your Universal Windows app continues to run properly after you release an update, you must call [**RemoveAccess**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess) and then call [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) when your app launches after being updated.</span></span> <span data-ttu-id="660af-130">詳しくは、「[バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="660af-130">For more information, see [Guidelines for background tasks](guidelines-for-background-tasks.md).</span></span>

<span data-ttu-id="660af-131">インプロセスのバックグラウンド アクティビティの場合は `TaskEntryPoint.` を設定しません。この値を設定しないと、[OnBackgroundActivated()](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onbackgroundactivated) と呼ばれる、Application オブジェクトの新しい保護されたメソッドが既定のエントリ ポイントとして有効になります。</span><span class="sxs-lookup"><span data-stu-id="660af-131">For in-process background activities you do not set `TaskEntryPoint.` Leaving it blank enables the default entry point, a new protected method on the Application object called [OnBackgroundActivated()](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onbackgroundactivated).</span></span>

<span data-ttu-id="660af-132">登録したトリガーは、[SetTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.settrigger) メソッドで設定されたトリガーの種類に基づいて発生します。</span><span class="sxs-lookup"><span data-stu-id="660af-132">Once a trigger is registered, it will fire based on the type of trigger set in the [SetTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.settrigger) method.</span></span> <span data-ttu-id="660af-133">上記の例では、[TimeTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.timetrigger) が使用されています。これは、登録された時点から 15 分後に発生します。</span><span class="sxs-lookup"><span data-stu-id="660af-133">In the example above a [TimeTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.timetrigger) is used, which will fire fifteen minutes from the time it was registered.</span></span>

## <a name="add-a-condition-to-control-when-your-task-will-run-optional"></a><span data-ttu-id="660af-134">どのようなときにタスクを実行するかという条件を追加する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="660af-134">Add a condition to control when your task will run (optional)</span></span>

<span data-ttu-id="660af-135">トリガー イベントの発生後、どのようなときにタスクを実行するかという条件を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="660af-135">You can add a condition to control when your task will run after the trigger event occurs.</span></span> <span data-ttu-id="660af-136">たとえば、ユーザーが存在するときにだけタスクを実行する場合、**UserPresent** という条件を使います。</span><span class="sxs-lookup"><span data-stu-id="660af-136">For example, if you don't want the task to run until the user is present, use the condition **UserPresent**.</span></span> <span data-ttu-id="660af-137">指定できる条件の一覧については、「[**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="660af-137">For a list of possible conditions, see [**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType).</span></span>

<span data-ttu-id="660af-138">次のサンプル コードでは、"ユーザーの存在" を条件として割り当てています。</span><span class="sxs-lookup"><span data-stu-id="660af-138">The following sample code assigns a condition requiring the user to be present:</span></span>

> [!div class="tabbedCodeSnippets"]
> ```cs
> builder.AddCondition(new SystemCondition(SystemConditionType.UserPresent));
> ```

## <a name="place-your-background-activity-code-in-onbackgroundactivated"></a><span data-ttu-id="660af-139">バックグラウンド アクティビティのコードを OnBackgroundActivated() に配置する</span><span class="sxs-lookup"><span data-stu-id="660af-139">Place your background activity code in OnBackgroundActivated()</span></span>

<span data-ttu-id="660af-140">バック グラウンド アクティビティ コードを配置[OnBackgroundActivated](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onbackgroundactivated)を発生させるときに、バック グラウンドのトリガーに応答します。</span><span class="sxs-lookup"><span data-stu-id="660af-140">Put your background activity code in [OnBackgroundActivated](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.onbackgroundactivated) to respond to your background trigger when it fires.</span></span> <span data-ttu-id="660af-141">**OnBackgroundActivated** は、[IBackgroundTask.Run](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.ibackgroundtask.run?f=255&MSPPError=-2147217396) と同様に処理することができます。</span><span class="sxs-lookup"><span data-stu-id="660af-141">**OnBackgroundActivated** can be treated just like [IBackgroundTask.Run](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.ibackgroundtask.run?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="660af-142">メソッドには、 [BackgroundActivatedEventArgs](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.backgroundactivatedeventargs)パラメーターで、すべてのものが含まれていますが、**実行**メソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="660af-142">The method has a [BackgroundActivatedEventArgs](https://docs.microsoft.com/uwp/api/windows.applicationmodel.activation.backgroundactivatedeventargs) parameter, which contains everything that the **Run** method delivers.</span></span> <span data-ttu-id="660af-143">たとえば、App.xaml.cs: で</span><span class="sxs-lookup"><span data-stu-id="660af-143">For example, in App.xaml.cs:</span></span>

``` cs
using Windows.ApplicationModel.Background;

...

sealed partial class App : Application
{
  ...

  protected override void OnBackgroundActivated(BackgroundActivatedEventArgs args)
  {
      base.OnBackgroundActivated(args);
      IBackgroundTaskInstance taskInstance = args.TaskInstance;
      DoYourBackgroundWork(taskInstance);  
  }
}
```

<span data-ttu-id="660af-144">豊富な**OnBackgroundActivated**例を参照してください[ホスト アプリケーションと同じプロセスで実行する app service の変換](convert-app-service-in-process.md)します。</span><span class="sxs-lookup"><span data-stu-id="660af-144">For a richer **OnBackgroundActivated** example, see [Convert an app service to run in the same process as its host app](convert-app-service-in-process.md).</span></span>

## <a name="handle-background-task-progress-and-completion"></a><span data-ttu-id="660af-145">バックグラウンド タスクの進捗状況と完了を処理する</span><span class="sxs-lookup"><span data-stu-id="660af-145">Handle background task progress and completion</span></span>

<span data-ttu-id="660af-146">タスクの進捗状況と完了は、マルチプロセスのバックグラウンド タスクの場合と同じ方法で監視できます (「[バックグラウンド タスクの進捗状況と完了の監視](monitor-background-task-progress-and-completion.md)」をご覧ください)。ただし、変数を使うと、より簡単にアプリで進捗状況または完了状態を追跡できます。</span><span class="sxs-lookup"><span data-stu-id="660af-146">Task progress and completion can be monitored the same way as for multi-process background tasks (see [Monitor background task progress and completion](monitor-background-task-progress-and-completion.md)) but you will likely find that you can more easily track them by using variables to track progress or completion status in your app.</span></span> <span data-ttu-id="660af-147">これは、アプリと同じプロセスでバックグラウンド アクティビティのコードを実行する利点の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="660af-147">This is one of the advantages of having your background activity code running in the same process as your app.</span></span>

## <a name="handle-background-task-cancellation"></a><span data-ttu-id="660af-148">バックグラウンド タスクの取り消しを処理する</span><span class="sxs-lookup"><span data-stu-id="660af-148">Handle background task cancellation</span></span>

<span data-ttu-id="660af-149">インプロセスのバックグラウンド タスクは、アウトプロセスのバックグラウンド タスクの場合と同じ方法で取り消すことができます (「[取り消されたバックグラウンド タスクの処理](handle-a-cancelled-background-task.md)」をご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="660af-149">In-process background tasks are cancelled the same way as out-of-process background tasks are (see [Handle a cancelled background task](handle-a-cancelled-background-task.md)).</span></span> <span data-ttu-id="660af-150">取り消しが発生する前に **BackgroundActivated** イベント ハンドラーを終了する必要があります。そうでないと、プロセス全体が終了します。</span><span class="sxs-lookup"><span data-stu-id="660af-150">Be aware that your **BackgroundActivated** event handler must exit before the cancellation occurs, or the whole process will be terminated.</span></span> <span data-ttu-id="660af-151">バックグラウンド タスクを取り消したときにフォアグラウンド アプリが予期せずに終了する場合は、取り消しが発生する前にハンドラーが終了していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="660af-151">If your foreground app closes unexpectedly when you cancel the background task, verify that your handler exited before the cancellation occured.</span></span>

## <a name="the-manifest"></a><span data-ttu-id="660af-152">マニフェスト</span><span class="sxs-lookup"><span data-stu-id="660af-152">The manifest</span></span>

<span data-ttu-id="660af-153">アウトプロセスのバックグラウンド タスクとは異なり、インプロセスのバックグラウンド タスクを実行するためにパッケージ マニフェストにバックグラウンド タスクの情報を追加する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="660af-153">Unlike out-of-process background tasks, you are not required to add background task information to the package manifest in order to run in-process background tasks.</span></span>

## <a name="summary-and-next-steps"></a><span data-ttu-id="660af-154">要約と次のステップ</span><span class="sxs-lookup"><span data-stu-id="660af-154">Summary and next steps</span></span>

<span data-ttu-id="660af-155">インプロセスのバックグラウンド タスクを作成する方法の基本を説明しました。</span><span class="sxs-lookup"><span data-stu-id="660af-155">You should now understand the basics of how to write a in-process background task.</span></span>

<span data-ttu-id="660af-156">API リファレンス、バックグラウンド タスクの概念的ガイダンス、バックグラウンド タスクを使ったアプリの作成に関する詳しい説明については、次の関連するトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="660af-156">See the following related topics for API reference, background task conceptual guidance, and more detailed instructions for writing apps that use background tasks.</span></span>

## <a name="related-topics"></a><span data-ttu-id="660af-157">関連トピック</span><span class="sxs-lookup"><span data-stu-id="660af-157">Related topics</span></span>

<span data-ttu-id="660af-158">**詳細なバック グラウンド タスクの説明のトピック**</span><span class="sxs-lookup"><span data-stu-id="660af-158">**Detailed background task instructional topics**</span></span>

* [<span data-ttu-id="660af-159">プロセス内のバック グラウンド タスクに、プロセス外のバック グラウンド タスクを変換します。</span><span class="sxs-lookup"><span data-stu-id="660af-159">Convert an out-of-process background task to an in-process background task</span></span>](convert-out-of-process-background-task.md)
* [<span data-ttu-id="660af-160">アウトプロセス バックグラウンド タスクの作成と登録</span><span class="sxs-lookup"><span data-stu-id="660af-160">Create and register an out-of-process background task</span></span>](create-and-register-a-background-task.md)
* [<span data-ttu-id="660af-161">バック グラウンドでメディアを再生します。</span><span class="sxs-lookup"><span data-stu-id="660af-161">Play media in the background</span></span>](https://docs.microsoft.com/windows/uwp/audio-video-camera/background-audio)
* [<span data-ttu-id="660af-162">バックグラウンド タスクによるシステム イベントへの応答</span><span class="sxs-lookup"><span data-stu-id="660af-162">Respond to system events with background tasks</span></span>](respond-to-system-events-with-background-tasks.md)
* [<span data-ttu-id="660af-163">バックグラウンド タスクの登録</span><span class="sxs-lookup"><span data-stu-id="660af-163">Register a background task</span></span>](register-a-background-task.md)
* [<span data-ttu-id="660af-164">バックグラウンド タスクを実行するための条件の設定</span><span class="sxs-lookup"><span data-stu-id="660af-164">Set conditions for running a background task</span></span>](set-conditions-for-running-a-background-task.md)
* [<span data-ttu-id="660af-165">メンテナンス トリガーの使用</span><span class="sxs-lookup"><span data-stu-id="660af-165">Use a maintenance trigger</span></span>](use-a-maintenance-trigger.md)
* [<span data-ttu-id="660af-166">取り消されたバックグラウンド タスクの処理</span><span class="sxs-lookup"><span data-stu-id="660af-166">Handle a cancelled background task</span></span>](handle-a-cancelled-background-task.md)
* [<span data-ttu-id="660af-167">バックグラウンド タスクの進捗状況と完了の監視</span><span class="sxs-lookup"><span data-stu-id="660af-167">Monitor background task progress and completion</span></span>](monitor-background-task-progress-and-completion.md)
* [<span data-ttu-id="660af-168">タイマーでのバックグラウンド タスクの実行</span><span class="sxs-lookup"><span data-stu-id="660af-168">Run a background task on a timer</span></span>](run-a-background-task-on-a-timer-.md)

<span data-ttu-id="660af-169">**バック グラウンド タスクのガイダンス**</span><span class="sxs-lookup"><span data-stu-id="660af-169">**Background task guidance**</span></span>

* [<span data-ttu-id="660af-170">バックグラウンド タスクのガイドライン</span><span class="sxs-lookup"><span data-stu-id="660af-170">Guidelines for background tasks</span></span>](guidelines-for-background-tasks.md)
* [<span data-ttu-id="660af-171">バックグラウンド タスクのデバッグ</span><span class="sxs-lookup"><span data-stu-id="660af-171">Debug a background task</span></span>](debug-a-background-task.md)
* [<span data-ttu-id="660af-172">トリガーする方法を中断、再開、および (デバッグ) 場合は、UWP アプリでイベントをバック グラウンド</span><span class="sxs-lookup"><span data-stu-id="660af-172">How to trigger suspend, resume, and background events in UWP apps (when debugging)</span></span>](https://go.microsoft.com/fwlink/p/?linkid=254345)

<span data-ttu-id="660af-173">**バック グラウンド タスクの API リファレンス**</span><span class="sxs-lookup"><span data-stu-id="660af-173">**Background Task API Reference**</span></span>

* [<span data-ttu-id="660af-174">**Windows.ApplicationModel.Background**</span><span class="sxs-lookup"><span data-stu-id="660af-174">**Windows.ApplicationModel.Background**</span></span>](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background)
