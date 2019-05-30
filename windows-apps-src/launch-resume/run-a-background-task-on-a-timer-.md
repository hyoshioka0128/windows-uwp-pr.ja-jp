---
title: タイマーでのバックグラウンド タスクの実行
description: 1 回限りのバックグラウンド タスクをスケジュールする方法、または定期的なバックグラウンド タスクを実行する方法について説明します。
ms.assetid: 0B7F0BFF-535A-471E-AC87-783C740A61E9
ms.date: 07/06/2018
ms.topic: article
keywords: windows 10、uwp、バック グラウンド タスク
ms.localizationpriority: medium
ms.openlocfilehash: 08f163fb660ad158694f925467711e4d62bf8217
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371453"
---
# <a name="run-a-background-task-on-a-timer"></a><span data-ttu-id="29041-104">タイマーでのバックグラウンド タスクの実行</span><span class="sxs-lookup"><span data-stu-id="29041-104">Run a background task on a timer</span></span>

<span data-ttu-id="29041-105">[  **TimeTrigger**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.TimeTrigger) を使用して 1 回限りのバックグラウンド タスクをスケジュールする方法、または定期的なバックグラウンド タスクを実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="29041-105">Learn how to use the [**TimeTrigger**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.TimeTrigger) to schedule a one-time background task, or run a periodic background task.</span></span>

<span data-ttu-id="29041-106">このトピックで説明する、時間でトリガーされるバックグラウンド タスクを実装する方法の例については、[バックグラウンドのアクティブ化のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BackgroundActivation)の **Scenario4** を参照してください。</span><span class="sxs-lookup"><span data-stu-id="29041-106">See **Scenario4** in the [Background activation sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BackgroundActivation) to see an example of how to implement the time triggered background task described in this topic.</span></span>

<span data-ttu-id="29041-107">このトピックは、定期的に、または特定の時刻に実行する必要があるバックグラウンド タスクがあることを前提にしています。</span><span class="sxs-lookup"><span data-stu-id="29041-107">This topic assumes that you have a background task that needs to run periodically, or at a specific time.</span></span> <span data-ttu-id="29041-108">まだバックグラウンド タスクがない場合は、[BackgroundActivity.cs](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/BackgroundActivation/cs/BackgroundActivity.cs) にサンプルのバックグラウンド タスクがあります。</span><span class="sxs-lookup"><span data-stu-id="29041-108">If you don't already have a background task, there is a sample background task at [BackgroundActivity.cs](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/BackgroundActivation/cs/BackgroundActivity.cs).</span></span> <span data-ttu-id="29041-109">または、「[インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)」または「[アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)」の手順に従って作成してください。</span><span class="sxs-lookup"><span data-stu-id="29041-109">Or, follow the steps in [Create and register an in-process background task](create-and-register-an-inproc-background-task.md) or [Create and register an out-of-process background task](create-and-register-a-background-task.md) to create one.</span></span>

## <a name="create-a-time-trigger"></a><span data-ttu-id="29041-110">時刻のトリガーを作る</span><span class="sxs-lookup"><span data-stu-id="29041-110">Create a time trigger</span></span>

<span data-ttu-id="29041-111">新しい [**TimeTrigger**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.TimeTrigger) を作ります。</span><span class="sxs-lookup"><span data-stu-id="29041-111">Create a new [**TimeTrigger**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.TimeTrigger).</span></span> <span data-ttu-id="29041-112">2 つ目のパラメーター (*OneShot*) では、バックグラウンド タスクを一度だけ実行するか、または定期的に実行を続けるかを指定します。</span><span class="sxs-lookup"><span data-stu-id="29041-112">The second parameter, *OneShot*, specifies whether the background task will run only once or keep running periodically.</span></span> <span data-ttu-id="29041-113">*OneShot* を true に設定する場合は、1 つ目のパラメーター (*FreshnessTime*) に、バックグラウンド タスクをスケジュールするまで待機する時間 (分単位) を指定します。</span><span class="sxs-lookup"><span data-stu-id="29041-113">If *OneShot* is set to true, the first parameter (*FreshnessTime*) specifies the number of minutes to wait before scheduling the background task.</span></span> <span data-ttu-id="29041-114">*OneShot* を false に設定する場合は、*FreshnessTime* に、バックグラウンド タスクを実行する間隔を指定します。</span><span class="sxs-lookup"><span data-stu-id="29041-114">If *OneShot* is set to false, *FreshnessTime* specifies the frequency at which the background task will run.</span></span>

<span data-ttu-id="29041-115">デスクトップかモバイル デバイス ファミリを対象とするユニバーサル Windows プラットフォーム (UWP) アプリの組み込みタイマーは、15 分間隔でバックグラウンド タスクを実行します。</span><span class="sxs-lookup"><span data-stu-id="29041-115">The built-in timer for Universal Windows Platform (UWP) apps that target the desktop or mobile device family runs background tasks in 15-minute intervals.</span></span> <span data-ttu-id="29041-116">(要求された TimerTrigger を持つアプリを起動するためにシステムが 15 分に 1 回だけ起動すればよいように、タイマーは 15 分間隔で実行されます。これにより、電力が節約されます)。</span><span class="sxs-lookup"><span data-stu-id="29041-116">(The timer runs in 15-minute intervals so that the system only needs to wake once every 15 minutes to wake up the apps that have requested TimerTriggers--which saves power.)</span></span>

- <span data-ttu-id="29041-117">*FreshnessTime* が 15 分に設定され、*OneShot* が true の場合、タスクは登録された時点から 15 ～ 30 分の間に一度実行されるようにスケジュールされます。</span><span class="sxs-lookup"><span data-stu-id="29041-117">If *FreshnessTime* is set to 15 minutes and *OneShot* is true, the task will be scheduled to run once starting between 15 and 30 minutes from the time it is registered.</span></span> <span data-ttu-id="29041-118">これが 25 分に設定され、*OneShot* が true の場合、タスクは登録された時点から 25 ～ 40 分の間に一度実行されるようにスケジュールされます。</span><span class="sxs-lookup"><span data-stu-id="29041-118">If it is set to 25 minutes and *OneShot* is true, the task will be scheduled to run once starting between 25 and 40 minutes from the time it is registered.</span></span>

- <span data-ttu-id="29041-119">*FreshnessTime* が 15 分に設定され、*OneShot* が false の場合、タスクは登録された時点から 15 ～ 15 分の間に実行され、その後 30 分ごとに実行されるようにスケジュールされます。</span><span class="sxs-lookup"><span data-stu-id="29041-119">If *FreshnessTime* is set to 15 minutes and *OneShot* is false, the task will be scheduled to run every 15 minutes starting between 15 and 30 minutes from the time it is registered.</span></span> <span data-ttu-id="29041-120">これが n 分に設定され、*OneShot* が false の場合、タスクは登録された時点から n ～ n + 15 分の間に実行され、その後 n 分ごとに実行されるようにスケジュールされます。</span><span class="sxs-lookup"><span data-stu-id="29041-120">If it is set to n minutes and *OneShot* is false, the task will be scheduled to run every n minutes starting between n and n + 15 minutes after it is registered.</span></span>

> [!NOTE]
> <span data-ttu-id="29041-121">場合*FreshnessTime*がバック グラウンド タスクの登録を試みているときに例外がスローに未満、15 分に設定します。</span><span class="sxs-lookup"><span data-stu-id="29041-121">If *FreshnessTime* is set to less than 15 minutes, an exception is thrown when attempting to register the background task.</span></span>
 
<span data-ttu-id="29041-122">たとえば、このトリガーでは、1 時間に 1 回実行するバック グラウンド タスクが発生します。</span><span class="sxs-lookup"><span data-stu-id="29041-122">For example, this trigger will cause a background task to run once an hour.</span></span>

```cs
TimeTrigger hourlyTrigger = new TimeTrigger(60, false);
```

```cppwinrt
Windows::ApplicationModel::Background::TimeTrigger hourlyTrigger{ 60, false };
```

```cpp
TimeTrigger ^ hourlyTrigger = ref new TimeTrigger(60, false);
```

## <a name="optional-add-a-condition"></a><span data-ttu-id="29041-123">(省略可能) 条件の追加</span><span class="sxs-lookup"><span data-stu-id="29041-123">(Optional) Add a condition</span></span>

<span data-ttu-id="29041-124">いつタスクを実行するかを制御するバックグラウンド タスクの条件を作成できます。</span><span class="sxs-lookup"><span data-stu-id="29041-124">You can create a background task condition to control when the task runs.</span></span> <span data-ttu-id="29041-125">条件を指定すると、条件が満たされるまではバックグラウンド タスクが実行されないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="29041-125">A condition prevents the background task from running until the condition is met.</span></span> <span data-ttu-id="29041-126">詳しくは、「[バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29041-126">For more information, see [Set conditions for running a background task](set-conditions-for-running-a-background-task.md).</span></span>

<span data-ttu-id="29041-127">この例では、条件が **UserPresent** に設定されているため、トリガー後、ユーザーがアクティブになった場合にタスクが 1 回だけ実行されます。</span><span class="sxs-lookup"><span data-stu-id="29041-127">In this example the condition is set to **UserPresent** so that, once triggered, the task only runs once the user is active.</span></span> <span data-ttu-id="29041-128">指定できる条件の一覧については、「[**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29041-128">For a list of possible conditions, see [**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType).</span></span>

```cs
SystemCondition userCondition = new SystemCondition(SystemConditionType.UserPresent);
```

```cppwinrt
Windows::ApplicationModel::Background::SystemCondition userCondition{
    Windows::ApplicationModel::Background::SystemConditionType::UserPresent };
```

```cpp
SystemCondition ^ userCondition = ref new SystemCondition(SystemConditionType::UserPresent);
```

<span data-ttu-id="29041-129">バックグラウンド トリガーの条件と種類について詳しくは、「[バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29041-129">For more in-depth information on conditions and types of background triggers, see [Support your app with background tasks](support-your-app-with-background-tasks.md).</span></span>

##  <a name="call-requestaccessasync"></a><span data-ttu-id="29041-130">RequestAccessAsync() の呼び出し</span><span class="sxs-lookup"><span data-stu-id="29041-130">Call RequestAccessAsync()</span></span>

<span data-ttu-id="29041-131">**ApplicationTrigger** バックグラウンド タスクを登録する前に、[**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出して、ユーザーが許可しているバックグラウンド アクティビティのレベルを判断します。これは、ユーザーがアプリのバックグラウンド アクティビティを無効にしている可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="29041-131">Before registering the **ApplicationTrigger** background task, call [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) to determine the level of background activity the user allows because the user may have disabled background activity for your app.</span></span> <span data-ttu-id="29041-132">ユーザーがバックグラウンド アクティビティの設定を制御する方法について詳しくは、「[バックグラウンド アクティビティの最適化](https://docs.microsoft.com/windows/uwp/debug-test-perf/optimize-background-activity)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="29041-132">See [Optimize background activity](https://docs.microsoft.com/windows/uwp/debug-test-perf/optimize-background-activity) for more information about the ways users can control the settings for background activity.</span></span>

```cs
var requestStatus = await Windows.ApplicationModel.Background.BackgroundExecutionManager.RequestAccessAsync();
if (requestStatus != BackgroundAccessStatus.AlwaysAllowed)
{
    // Depending on the value of requestStatus, provide an appropriate response
    // such as notifying the user which functionality won't work as expected
}
```

## <a name="register-the-background-task"></a><span data-ttu-id="29041-133">バックグラウンド タスクの登録</span><span class="sxs-lookup"><span data-stu-id="29041-133">Register the background task</span></span>

<span data-ttu-id="29041-134">バックグラウンド タスクの登録関数を呼び出してバックグラウンド タスクを登録します。</span><span class="sxs-lookup"><span data-stu-id="29041-134">Register the background task by calling your background task registration function.</span></span> <span data-ttu-id="29041-135">バックグラウンド タスクの登録と、以下のコード サンプルの **RegisterBackgroundTask()** メソッドの定義について詳しくは、「[バックグラウンド タスクの登録](register-a-background-task.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="29041-135">For more information on registering background tasks, and to see the definition of the **RegisterBackgroundTask()** method in the sample code below, see [Register a background task](register-a-background-task.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29041-136">バック グラウンド タスクをアプリと同じプロセスで実行されるは設定しないでください`entryPoint`します。</span><span class="sxs-lookup"><span data-stu-id="29041-136">For background tasks that run in the same process as your app, do not set `entryPoint`.</span></span> <span data-ttu-id="29041-137">バック グラウンド タスクをアプリから別のプロセスで実行している設定`entryPoint`を名前空間 '.'、およびバック グラウンド タスクの実装を含むクラスの名前。</span><span class="sxs-lookup"><span data-stu-id="29041-137">For background tasks that run in a separate process from your app, set `entryPoint` to be the namespace, '.', and the name of the class that contains your background task implementation.</span></span>

```cs
string entryPoint = "Tasks.ExampleBackgroundTaskClass";
string taskName   = "Example hourly background task";

BackgroundTaskRegistration task = RegisterBackgroundTask(entryPoint, taskName, hourlyTrigger, userCondition);
```

```cppwinrt
std::wstring entryPoint{ L"Tasks.ExampleBackgroundTaskClass" };
std::wstring taskName{ L"Example hourly background task" };

Windows::ApplicationModel::Background::BackgroundTaskRegistration task{
    RegisterBackgroundTask(entryPoint, taskName, hourlyTrigger, userCondition) };
```

```cpp
String ^ entryPoint = "Tasks.ExampleBackgroundTaskClass";
String ^ taskName   = "Example hourly background task";

BackgroundTaskRegistration ^ task = RegisterBackgroundTask(entryPoint, taskName, hourlyTrigger, userCondition);
```

<span data-ttu-id="29041-138">バックグラウンド タスクの登録パラメーターは登録時に検証されます。</span><span class="sxs-lookup"><span data-stu-id="29041-138">Background task registration parameters are validated at the time of registration.</span></span> <span data-ttu-id="29041-139">いずれかの登録パラメーターが有効でない場合は、エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="29041-139">An error is returned if any of the registration parameters are invalid.</span></span> <span data-ttu-id="29041-140">バックグラウンド タスクの登録が失敗するシナリオをアプリが適切に処理するようにします。タスクを登録しようとした後で、有効な登録オブジェクトを持っていることを前提として動作するアプリは、クラッシュする場合があります。</span><span class="sxs-lookup"><span data-stu-id="29041-140">Ensure that your app gracefully handles scenarios where background task registration fails - if instead your app depends on having a valid registration object after attempting to register a task, it may crash.</span></span>

## <a name="manage-resources-for-your-background-task"></a><span data-ttu-id="29041-141">バックグラウンド タスクのリソースの管理</span><span class="sxs-lookup"><span data-stu-id="29041-141">Manage resources for your background task</span></span>

<span data-ttu-id="29041-142">[BackgroundExecutionManager.RequestAccessAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager) を使用して、アプリのバックグラウンド アクティビティを制限するようにユーザーが設定しているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="29041-142">Use [BackgroundExecutionManager.RequestAccessAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager) to determine if the user has decided that your app’s background activity should be limited.</span></span> <span data-ttu-id="29041-143">バッテリー使用量を注意し、ユーザーが望む操作を完了するために必要な場合にのみ、バックグラウンドで実行するようにしてください。</span><span class="sxs-lookup"><span data-stu-id="29041-143">Be aware of your battery usage and only run in the background when it is necessary to complete an action that the user wants.</span></span> <span data-ttu-id="29041-144">ユーザーがバックグラウンド アクティビティの設定を制御する方法について詳しくは、「[バックグラウンド アクティビティの最適化](https://docs.microsoft.com/windows/uwp/debug-test-perf/optimize-background-activity)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="29041-144">See [Optimize background activity](https://docs.microsoft.com/windows/uwp/debug-test-perf/optimize-background-activity) for more information about the ways users can control the settings for background activity.</span></span>

- <span data-ttu-id="29041-145">メモリ:チューニングにアプリのメモリとエネルギーの使用は、オペレーティング システムで、バック グラウンド タスクを実行を許可することを保証するキーです。</span><span class="sxs-lookup"><span data-stu-id="29041-145">Memory: Tuning your app's memory and energy use is key to ensuring that the operating system will allow your background task to run.</span></span> <span data-ttu-id="29041-146">[メモリ管理 API](https://docs.microsoft.com/uwp/api/windows.system.memorymanager) を使用して、バックグラウンド タスクが使用しているメモリ量を確認します。</span><span class="sxs-lookup"><span data-stu-id="29041-146">Use the [Memory Management APIs](https://docs.microsoft.com/uwp/api/windows.system.memorymanager) to see how much memory your background task is using.</span></span> <span data-ttu-id="29041-147">バックグラウンド タスクが使用するメモリ量が多くなるほど、別のアプリがフォアグラウンドのときに、バックグラウンド タスクの実行を OS が維持することは難しくなります。</span><span class="sxs-lookup"><span data-stu-id="29041-147">The more memory your background task uses, the harder it is for the OS to keep it running when another app is in the foreground.</span></span> <span data-ttu-id="29041-148">アプリが実行できるすべてのバックグラウンド アクティビティについて、最終的に管理できるのはユーザーです。また、ユーザーは、アプリがどの程度バッテリー消費に影響しているかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="29041-148">The user is ultimately in control of all background activity that your app can perform and has visibility on the impact your app has on battery use.</span></span>  
- <span data-ttu-id="29041-149">CPU 時間:バック グラウンド タスクは、トリガーの種類に基づいて、取得、ウォール クロック使用時間の量によって制限されます。</span><span class="sxs-lookup"><span data-stu-id="29041-149">CPU time: Background tasks are limited by the amount of wall-clock usage time they get based on trigger type.</span></span>

<span data-ttu-id="29041-150">バックグラウンド タスクに適用されるリソースの制約については、「[バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="29041-150">See [Support your app with background tasks](support-your-app-with-background-tasks.md) for the resource constraints applied to background tasks.</span></span>

## <a name="remarks"></a><span data-ttu-id="29041-151">注釈</span><span class="sxs-lookup"><span data-stu-id="29041-151">Remarks</span></span>

<span data-ttu-id="29041-152">Windows 10 以降の場合は、バック グラウンド タスクを利用するには、ロック画面にアプリを追加するユーザーのために必要な不要になった。</span><span class="sxs-lookup"><span data-stu-id="29041-152">Starting with Windows 10, it is no longer necessary for the user to add your app to the lock screen in order to utilize background tasks.</span></span>

<span data-ttu-id="29041-153">バックグラウンド タスクが **TimeTrigger** を使って実行されるのは、先に[**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出した場合のみです。</span><span class="sxs-lookup"><span data-stu-id="29041-153">A background task will only run using a **TimeTrigger** if you have called [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) first.</span></span>

## <a name="related-topics"></a><span data-ttu-id="29041-154">関連トピック</span><span class="sxs-lookup"><span data-stu-id="29041-154">Related topics</span></span>

* [<span data-ttu-id="29041-155">バックグラウンド タスクのガイドライン</span><span class="sxs-lookup"><span data-stu-id="29041-155">Guidelines for background tasks</span></span>](guidelines-for-background-tasks.md)
* [<span data-ttu-id="29041-156">バック グラウンド タスクのコード サンプル</span><span class="sxs-lookup"><span data-stu-id="29041-156">Background task code sample</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BackgroundTask)
* [<span data-ttu-id="29041-157">インプロセス バックグラウンド タスクの作成と登録</span><span class="sxs-lookup"><span data-stu-id="29041-157">Create and register an in-process background task</span></span>](create-and-register-an-inproc-background-task.md)
* [<span data-ttu-id="29041-158">アウトプロセス バックグラウンド タスクの作成と登録</span><span class="sxs-lookup"><span data-stu-id="29041-158">Create and register an out-of-process background task</span></span>](create-and-register-a-background-task.md)
* [<span data-ttu-id="29041-159">バックグラウンド タスクのデバッグ</span><span class="sxs-lookup"><span data-stu-id="29041-159">Debug a background task</span></span>](debug-a-background-task.md)
* [<span data-ttu-id="29041-160">アプリケーション マニフェストでのバックグラウンド タスクの宣言</span><span class="sxs-lookup"><span data-stu-id="29041-160">Declare background tasks in the application manifest</span></span>](declare-background-tasks-in-the-application-manifest.md)
* [<span data-ttu-id="29041-161">アプリがバックグラウンドに移動したときのメモリの解放</span><span class="sxs-lookup"><span data-stu-id="29041-161">Free memory when your app moves to the background</span></span>](reduce-memory-usage.md)
* [<span data-ttu-id="29041-162">取り消されたバックグラウンド タスクの処理</span><span class="sxs-lookup"><span data-stu-id="29041-162">Handle a cancelled background task</span></span>](handle-a-cancelled-background-task.md)
* [<span data-ttu-id="29041-163">トリガーする方法を中断、再開、および (デバッグ) 場合は、UWP アプリでイベントをバック グラウンド</span><span class="sxs-lookup"><span data-stu-id="29041-163">How to trigger suspend, resume, and background events in UWP apps (when debugging)</span></span>](https://go.microsoft.com/fwlink/p/?linkid=254345)
* [<span data-ttu-id="29041-164">バックグラウンド タスクの進捗状況と完了の監視</span><span class="sxs-lookup"><span data-stu-id="29041-164">Monitor background task progress and completion</span></span>](monitor-background-task-progress-and-completion.md)
* [<span data-ttu-id="29041-165">延長実行を使ってアプリの中断を延期する</span><span class="sxs-lookup"><span data-stu-id="29041-165">Postpone app suspension with extended execution</span></span>](run-minimized-with-extended-execution.md)
* [<span data-ttu-id="29041-166">バックグラウンド タスクの登録</span><span class="sxs-lookup"><span data-stu-id="29041-166">Register a background task</span></span>](register-a-background-task.md)
* [<span data-ttu-id="29041-167">バックグラウンド タスクによるシステム イベントへの応答</span><span class="sxs-lookup"><span data-stu-id="29041-167">Respond to system events with background tasks</span></span>](respond-to-system-events-with-background-tasks.md)
* [<span data-ttu-id="29041-168">バックグラウンド タスクを実行するための条件の設定</span><span class="sxs-lookup"><span data-stu-id="29041-168">Set conditions for running a background task</span></span>](set-conditions-for-running-a-background-task.md)
* [<span data-ttu-id="29041-169">バックグラウンド タスクのライブ タイルの更新</span><span class="sxs-lookup"><span data-stu-id="29041-169">Update a live tile from a background task</span></span>](update-a-live-tile-from-a-background-task.md)
* [<span data-ttu-id="29041-170">メンテナンス トリガーの使用</span><span class="sxs-lookup"><span data-stu-id="29041-170">Use a maintenance trigger</span></span>](use-a-maintenance-trigger.md)
