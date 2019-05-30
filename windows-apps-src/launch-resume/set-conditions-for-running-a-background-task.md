---
title: バックグラウンド タスクを実行するための条件の設定
description: バックグラウンド タスクをいつ実行するかを制御する条件の設定方法について説明します。
ms.assetid: 10ABAC9F-AA8C-41AC-A29D-871CD9AD9471
ms.date: 07/06/2018
ms.topic: article
keywords: windows 10、uwp、バック グラウンド タスク
ms.localizationpriority: medium
dev_langs:
- csharp
- cppwinrt
- cpp
ms.openlocfilehash: 88836ac0363001e86c17486e1527b96a4eac0faa
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371844"
---
# <a name="set-conditions-for-running-a-background-task"></a><span data-ttu-id="949aa-104">バックグラウンド タスクを実行するための条件の設定</span><span class="sxs-lookup"><span data-stu-id="949aa-104">Set conditions for running a background task</span></span>

<span data-ttu-id="949aa-105">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="949aa-105">**Important APIs**</span></span>

- [<span data-ttu-id="949aa-106">**SystemCondition**</span><span class="sxs-lookup"><span data-stu-id="949aa-106">**SystemCondition**</span></span>](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemCondition)
- [<span data-ttu-id="949aa-107">**SystemConditionType**</span><span class="sxs-lookup"><span data-stu-id="949aa-107">**SystemConditionType**</span></span>](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType)
- [<span data-ttu-id="949aa-108">**BackgroundTaskBuilder**</span><span class="sxs-lookup"><span data-stu-id="949aa-108">**BackgroundTaskBuilder**</span></span>](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder)

<span data-ttu-id="949aa-109">バックグラウンド タスクをいつ実行するかを制御する条件の設定方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="949aa-109">Learn how to set conditions that control when your background task will run.</span></span>

<span data-ttu-id="949aa-110">場合によっては、バックグラウンド タスクを正しく実行するために、特定の条件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="949aa-110">Sometimes, background tasks require certain conditions to be met for the background task to succeed.</span></span> <span data-ttu-id="949aa-111">バックグラウンド タスクを登録するときに、[**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType) で指定される条件を 1 つ以上指定することができます。</span><span class="sxs-lookup"><span data-stu-id="949aa-111">You can specify one or more of the conditions specified by [**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType) when registering your background task.</span></span> <span data-ttu-id="949aa-112">条件がチェックされるのは、トリガーが発生した後です。</span><span class="sxs-lookup"><span data-stu-id="949aa-112">The condition will be checked after the trigger has been fired.</span></span> <span data-ttu-id="949aa-113">バックグラウンド タスクは、キューに入れられますが、必要な条件がすべて満たされるまでは実行されません。</span><span class="sxs-lookup"><span data-stu-id="949aa-113">The background task will then be queued, but it will not run until all the required conditions are satisfied.</span></span>

<span data-ttu-id="949aa-114">バックグラウンド タスクに条件を設定すると、タスクが不必要に実行されなくなるため、バッテリー残量と CPU 実行時間が節約できます。</span><span class="sxs-lookup"><span data-stu-id="949aa-114">Putting conditions on background tasks saves battery life and CPU by preventing tasks from running unnecessarily.</span></span> <span data-ttu-id="949aa-115">たとえば、バックグラウンド タスクがタイマーで実行され、インターネット接続が必要な場合は、タスクを登録する前に、**InternetAvailable** 条件を [**TaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) に追加します。</span><span class="sxs-lookup"><span data-stu-id="949aa-115">For example, if your background task runs on a timer and requires Internet connectivity, add the **InternetAvailable** condition to the [**TaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) before registering the task.</span></span> <span data-ttu-id="949aa-116">これにより、タイマーの設定時間が経過し、*かつ*インターネットが利用可能な場合にのみバックグラウンド タスクが実行されるため、タスクがシステム リソースやバッテリー残量を無駄に消費することはなくなります。</span><span class="sxs-lookup"><span data-stu-id="949aa-116">This will help prevent the task from using system resources and battery life unnecessarily by only running the background task when the timer has elapsed *and* the Internet is available.</span></span>

<span data-ttu-id="949aa-117">同じ [**TaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) で **AddCondition** を複数回呼び出すことで、複数の条件を組み合わせることもできます。</span><span class="sxs-lookup"><span data-stu-id="949aa-117">It is also possible to combine multiple conditions by calling **AddCondition** multiple times on the same [**TaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder).</span></span> <span data-ttu-id="949aa-118">**UserPresent** や **UserNotPresent** など競合する条件を追加しないように注意してください。</span><span class="sxs-lookup"><span data-stu-id="949aa-118">Take care not to add conflicting conditions, such as **UserPresent** and **UserNotPresent**.</span></span>

## <a name="create-a-systemcondition-object"></a><span data-ttu-id="949aa-119">SystemCondition オブジェクトを作る</span><span class="sxs-lookup"><span data-stu-id="949aa-119">Create a SystemCondition object</span></span>

<span data-ttu-id="949aa-120">ここでは、既にバックグラウンド タスクがアプリと関連付けられており、アプリでは、**taskBuilder** という [**BackgroundTaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) オブジェクトを作るためのコードが記述済みであることを前提とします。</span><span class="sxs-lookup"><span data-stu-id="949aa-120">This topic assumes that you have a background task already associated with your app, and that your app already includes code that creates a [**BackgroundTaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) object named **taskBuilder**.</span></span>  <span data-ttu-id="949aa-121">最初にバックグラウンド タスクを作成する必要がある場合は、「[インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)」または「[アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="949aa-121">See [Create and register an in-process background task](create-and-register-an-inproc-background-task.md) or [Create and register an out-of-process background task](create-and-register-a-background-task.md) if you need to create a background task first.</span></span>

<span data-ttu-id="949aa-122">このトピックの内容は、アウトプロセスで実行されるバックグラウンド タスク、およびフォアグラウンド アプリと同じプロセスで実行されるバックグラウンド タスクに適用されます。</span><span class="sxs-lookup"><span data-stu-id="949aa-122">This topic applies to background tasks that run out-of-process as well as those that run in the same process as the foreground app.</span></span>

<span data-ttu-id="949aa-123">条件を追加する前に、バックグラウンド タスクを実行するために有効にする必要のある条件を表す [**SystemCondition**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemCondition) オブジェクトを作ります。</span><span class="sxs-lookup"><span data-stu-id="949aa-123">Before adding the condition, create a [**SystemCondition**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemCondition) object to represent the condition that must be in effect for a background task to run.</span></span> <span data-ttu-id="949aa-124">コンストラクターで、[**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType) 列挙値を渡して、必要な条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="949aa-124">In the constructor, specify the condition that must be met with a [**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType) enumeration value.</span></span>

<span data-ttu-id="949aa-125">次のコードでは、**InternetAvailable** 条件を指定する [**SystemCondition**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemCondition) オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="949aa-125">The following code creates a [**SystemCondition**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemCondition) object that specifies the **InternetAvailable** condition:</span></span>

```csharp
SystemCondition internetCondition = new SystemCondition(SystemConditionType.InternetAvailable);
```

```cppwinrt
Windows::ApplicationModel::Background::SystemCondition internetCondition{
    Windows::ApplicationModel::Background::SystemConditionType::InternetAvailable };
```

```cpp
SystemCondition ^ internetCondition = ref new SystemCondition(SystemConditionType::InternetAvailable);
```

## <a name="add-the-systemcondition-object-to-your-background-task"></a><span data-ttu-id="949aa-126">SystemCondition オブジェクトをバックグラウンド タスクに追加する</span><span class="sxs-lookup"><span data-stu-id="949aa-126">Add the SystemCondition object to your background task</span></span>

<span data-ttu-id="949aa-127">条件を追加するには、[**BackgroundTaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) オブジェクトで [**AddCondition**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.addcondition) メソッドを呼び出して、[**SystemCondition**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemCondition) オブジェクトに渡します。</span><span class="sxs-lookup"><span data-stu-id="949aa-127">To add the condition, call the [**AddCondition**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.addcondition) method on the [**BackgroundTaskBuilder**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) object, and pass it the [**SystemCondition**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemCondition) object.</span></span>

<span data-ttu-id="949aa-128">次のコードは、**taskBuilder** を使用して **InternetAvailable** 条件を追加します。</span><span class="sxs-lookup"><span data-stu-id="949aa-128">The following code uses **taskBuilder** to add the **InternetAvailable** condition.</span></span>

```csharp
taskBuilder.AddCondition(internetCondition);
```

```cppwinrt
taskBuilder.AddCondition(internetCondition);
```

```cpp
taskBuilder->AddCondition(internetCondition);
```

## <a name="register-your-background-task"></a><span data-ttu-id="949aa-129">バックグラウンド タスクを登録する</span><span class="sxs-lookup"><span data-stu-id="949aa-129">Register your background task</span></span>

<span data-ttu-id="949aa-130">これで、バックグラウンド タスクを [**Register**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.register) メソッドに登録できます。このバックグラウンド タスクは、指定した条件が満たされるまで、開始されません。</span><span class="sxs-lookup"><span data-stu-id="949aa-130">Now you can register your background task with the [**Register**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.register) method, and the background task will not start until the specified condition is met.</span></span>

<span data-ttu-id="949aa-131">次のコードでは、タスクを登録し、生成される BackgroundTaskRegistration オブジェクトを保存します。</span><span class="sxs-lookup"><span data-stu-id="949aa-131">The following code registers the task and stores the resulting BackgroundTaskRegistration object:</span></span>

```csharp
BackgroundTaskRegistration task = taskBuilder.Register();
```

```cppwinrt
Windows::ApplicationModel::Background::BackgroundTaskRegistration task{ recurringTaskBuilder.Register() };
```

```cpp
BackgroundTaskRegistration ^ task = taskBuilder->Register();
```

> [!NOTE]
> <span data-ttu-id="949aa-132">ユニバーサル Windows アプリは、どの種類のバックグラウンド トリガーを登録する場合でも、先に [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="949aa-132">Universal Windows apps must call [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) before registering any of the background trigger types.</span></span>

<span data-ttu-id="949aa-133">更新プログラムのリリース後にユニバーサル Windows アプリが引き続き適切に実行されるようにするには、更新後にアプリが起動する際に、[**RemoveAccess**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess)、[**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) の順に呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="949aa-133">To ensure that your Universal Windows app continues to run properly after you release an update, you must call [**RemoveAccess**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess) and then call [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) when your app launches after being updated.</span></span> <span data-ttu-id="949aa-134">詳しくは、「[バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="949aa-134">For more information, see [Guidelines for background tasks](guidelines-for-background-tasks.md).</span></span>

> [!NOTE]
> <span data-ttu-id="949aa-135">バックグラウンド タスクの登録パラメーターは登録時に検証されます。</span><span class="sxs-lookup"><span data-stu-id="949aa-135">Background task registration parameters are validated at the time of registration.</span></span> <span data-ttu-id="949aa-136">いずれかの登録パラメーターが有効でない場合は、エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="949aa-136">An error is returned if any of the registration parameters are invalid.</span></span> <span data-ttu-id="949aa-137">バックグラウンド タスクの登録が失敗するシナリオをアプリが適切に処理するようにします。タスクを登録しようとした後で、有効な登録オブジェクトを持っていることを前提として動作するアプリは、クラッシュする場合があります。</span><span class="sxs-lookup"><span data-stu-id="949aa-137">Ensure that your app gracefully handles scenarios where background task registration fails - if instead your app depends on having a valid registration object after attempting to register a task, it may crash.</span></span>

## <a name="place-multiple-conditions-on-your-background-task"></a><span data-ttu-id="949aa-138">バックグラウンド タスクに複数の条件を設定する</span><span class="sxs-lookup"><span data-stu-id="949aa-138">Place multiple conditions on your background task</span></span>

<span data-ttu-id="949aa-139">複数の条件を追加するには、アプリから [**で**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.addcondition) メソッドを複数回呼び出します。</span><span class="sxs-lookup"><span data-stu-id="949aa-139">To add multiple conditions, your app makes multiple calls to the [**AddCondition**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.addcondition) method.</span></span> <span data-ttu-id="949aa-140">呼び出しは必ず、タスクの登録が有効になる前に行います。</span><span class="sxs-lookup"><span data-stu-id="949aa-140">These calls must come before task registration to be effective.</span></span>

> [!NOTE]
> <span data-ttu-id="949aa-141">バック グラウンド タスクに競合する条件を追加しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="949aa-141">Take care not to add conflicting conditions to a background task.</span></span>

<span data-ttu-id="949aa-142">次のスニペットでは、作成して、バック グラウンド タスクの登録のコンテキストで複数の条件を示します。</span><span class="sxs-lookup"><span data-stu-id="949aa-142">The following snippet shows multiple conditions in the context of creating and registering a background task.</span></span>

```csharp
// Set up the background task.
TimeTrigger hourlyTrigger = new TimeTrigger(60, false);

var recurringTaskBuilder = new BackgroundTaskBuilder();

recurringTaskBuilder.Name           = "Hourly background task";
recurringTaskBuilder.TaskEntryPoint = "Tasks.ExampleBackgroundTaskClass";
recurringTaskBuilder.SetTrigger(hourlyTrigger);

// Begin adding conditions.
SystemCondition userCondition     = new SystemCondition(SystemConditionType.UserPresent);
SystemCondition internetCondition = new SystemCondition(SystemConditionType.InternetAvailable);

recurringTaskBuilder.AddCondition(userCondition);
recurringTaskBuilder.AddCondition(internetCondition);

// Done adding conditions, now register the background task.

BackgroundTaskRegistration task = recurringTaskBuilder.Register();
```

```cppwinrt
// Set up the background task.
Windows::ApplicationModel::Background::TimeTrigger hourlyTrigger{ 60, false };

Windows::ApplicationModel::Background::BackgroundTaskBuilder recurringTaskBuilder;

recurringTaskBuilder.Name(L"Hourly background task");
recurringTaskBuilder.TaskEntryPoint(L"Tasks.ExampleBackgroundTaskClass");
recurringTaskBuilder.SetTrigger(hourlyTrigger);

// Begin adding conditions.
Windows::ApplicationModel::Background::SystemCondition userCondition{
    Windows::ApplicationModel::Background::SystemConditionType::UserPresent };
Windows::ApplicationModel::Background::SystemCondition internetCondition{
    Windows::ApplicationModel::Background::SystemConditionType::InternetAvailable };

recurringTaskBuilder.AddCondition(userCondition);
recurringTaskBuilder.AddCondition(internetCondition);

// Done adding conditions, now register the background task.
Windows::ApplicationModel::Background::BackgroundTaskRegistration task{ recurringTaskBuilder.Register() };
```

```cpp
// Set up the background task.
TimeTrigger ^ hourlyTrigger = ref new TimeTrigger(60, false);

auto recurringTaskBuilder = ref new BackgroundTaskBuilder();

recurringTaskBuilder->Name           = "Hourly background task";
recurringTaskBuilder->TaskEntryPoint = "Tasks.ExampleBackgroundTaskClass";
recurringTaskBuilder->SetTrigger(hourlyTrigger);

// Begin adding conditions.
SystemCondition ^ userCondition     = ref new SystemCondition(SystemConditionType::UserPresent);
SystemCondition ^ internetCondition = ref new SystemCondition(SystemConditionType::InternetAvailable);

recurringTaskBuilder->AddCondition(userCondition);
recurringTaskBuilder->AddCondition(internetCondition);

// Done adding conditions, now register the background task.
BackgroundTaskRegistration ^ task = recurringTaskBuilder->Register();
```

## <a name="remarks"></a><span data-ttu-id="949aa-143">注釈</span><span class="sxs-lookup"><span data-stu-id="949aa-143">Remarks</span></span>

> [!NOTE]
> <span data-ttu-id="949aa-144">これが必要であり、そうでないときに実行されない場合にのみ実行されるように、バック グラウンド タスクの条件を選択します。</span><span class="sxs-lookup"><span data-stu-id="949aa-144">Choose conditions for your background task so that it only runs when it's needed, and doesn't run when it shouldn't.</span></span> <span data-ttu-id="949aa-145">バックグラウンド タスクの各条件については、「[**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="949aa-145">See [**SystemConditionType**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.SystemConditionType) for descriptions of the different background task conditions.</span></span>

## <a name="related-topics"></a><span data-ttu-id="949aa-146">関連トピック</span><span class="sxs-lookup"><span data-stu-id="949aa-146">Related topics</span></span>

* [<span data-ttu-id="949aa-147">アウトプロセス バックグラウンド タスクの作成と登録</span><span class="sxs-lookup"><span data-stu-id="949aa-147">Create and register an out-of-process background task</span></span>](create-and-register-a-background-task.md)
* [<span data-ttu-id="949aa-148">インプロセス バックグラウンド タスクの作成と登録</span><span class="sxs-lookup"><span data-stu-id="949aa-148">Create and register an in-process background task</span></span>](create-and-register-an-inproc-background-task.md)
* [<span data-ttu-id="949aa-149">アプリケーション マニフェストでのバックグラウンド タスクの宣言</span><span class="sxs-lookup"><span data-stu-id="949aa-149">Declare background tasks in the application manifest</span></span>](declare-background-tasks-in-the-application-manifest.md)
* [<span data-ttu-id="949aa-150">取り消されたバックグラウンド タスクの処理</span><span class="sxs-lookup"><span data-stu-id="949aa-150">Handle a cancelled background task</span></span>](handle-a-cancelled-background-task.md)
* [<span data-ttu-id="949aa-151">バックグラウンド タスクの進捗状況と完了の監視</span><span class="sxs-lookup"><span data-stu-id="949aa-151">Monitor background task progress and completion</span></span>](monitor-background-task-progress-and-completion.md)
* [<span data-ttu-id="949aa-152">バックグラウンド タスクの登録</span><span class="sxs-lookup"><span data-stu-id="949aa-152">Register a background task</span></span>](register-a-background-task.md)
* [<span data-ttu-id="949aa-153">バックグラウンド タスクによるシステム イベントへの応答</span><span class="sxs-lookup"><span data-stu-id="949aa-153">Respond to system events with background tasks</span></span>](respond-to-system-events-with-background-tasks.md)
* [<span data-ttu-id="949aa-154">バックグラウンド タスクのライブ タイルの更新</span><span class="sxs-lookup"><span data-stu-id="949aa-154">Update a live tile from a background task</span></span>](update-a-live-tile-from-a-background-task.md)
* [<span data-ttu-id="949aa-155">メンテナンス トリガーの使用</span><span class="sxs-lookup"><span data-stu-id="949aa-155">Use a maintenance trigger</span></span>](use-a-maintenance-trigger.md)
* [<span data-ttu-id="949aa-156">タイマーでのバックグラウンド タスクの実行</span><span class="sxs-lookup"><span data-stu-id="949aa-156">Run a background task on a timer</span></span>](run-a-background-task-on-a-timer-.md)
* [<span data-ttu-id="949aa-157">バックグラウンド タスクのガイドライン</span><span class="sxs-lookup"><span data-stu-id="949aa-157">Guidelines for background tasks</span></span>](guidelines-for-background-tasks.md)
* [<span data-ttu-id="949aa-158">バックグラウンド タスクのデバッグ</span><span class="sxs-lookup"><span data-stu-id="949aa-158">Debug a background task</span></span>](debug-a-background-task.md)
* [<span data-ttu-id="949aa-159">トリガーする方法を中断、再開、および (デバッグ) 場合は、UWP アプリでイベントをバック グラウンド</span><span class="sxs-lookup"><span data-stu-id="949aa-159">How to trigger suspend, resume, and background events in UWP apps (when debugging)</span></span>](https://go.microsoft.com/fwlink/p/?linkid=254345)
