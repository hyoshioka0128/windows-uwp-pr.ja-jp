---
Description: この記事では、次の 4 つの通知オプションをについて説明します (& a)\#8212; ローカル、予定、定期的、およびプッシュ (& a)\#8212; タイルおよびバッジの更新プログラムを配信し、トースト通知の内容。
title: 通知配信方法の選択
ms.assetid: FDB43EDE-C5F2-493F-952C-55401EC5172B
label: Choose a notification delivery method
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: b1ea41a509b1673b7c4f5812d34db93dd6b0c93e
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365943"
---
# <a name="choose-a-notification-delivery-method"></a><span data-ttu-id="95518-104">通知配信方法の選択</span><span class="sxs-lookup"><span data-stu-id="95518-104">Choose a notification delivery method</span></span>

 


<span data-ttu-id="95518-105">この記事では、タイルとバッジの更新およびトースト通知のコンテンツを配信するための 4 つの通知オプション (ローカル、スケジュール、定期的、プッシュ) について説明します。</span><span class="sxs-lookup"><span data-stu-id="95518-105">This article covers the four notification options—local, scheduled, periodic, and push—that deliver tile and badge updates and toast notification content.</span></span> <span data-ttu-id="95518-106">タイルやトースト通知では、ユーザーがアプリを直接利用していないときでもユーザーに情報を伝えることができます。</span><span class="sxs-lookup"><span data-stu-id="95518-106">A tile or a toast notification can get information to your user even when the user is not directly engaged with your app.</span></span> <span data-ttu-id="95518-107">アプリおよび配信する情報の性質と内容から、シナリオに最適な通知方法を決めることができます。</span><span class="sxs-lookup"><span data-stu-id="95518-107">The nature and content of your app and the information that you want to deliver can help you determine which notification method or methods is best for your scenario.</span></span>

## <a name="notification-delivery-methods-overview"></a><span data-ttu-id="95518-108">通知配信方法の概要</span><span class="sxs-lookup"><span data-stu-id="95518-108">Notification delivery methods overview</span></span>


<span data-ttu-id="95518-109">通知を配信するためにアプリで使用できるメカニズムには、次の 4 種類があります。</span><span class="sxs-lookup"><span data-stu-id="95518-109">There are four mechanisms that an app can use to deliver a notification:</span></span>

-   <span data-ttu-id="95518-110">**地元の**</span><span class="sxs-lookup"><span data-stu-id="95518-110">**Local**</span></span>
-   <span data-ttu-id="95518-111">**[スケジュール]**</span><span class="sxs-lookup"><span data-stu-id="95518-111">**Scheduled**</span></span>
-   <span data-ttu-id="95518-112">**定期的です**</span><span class="sxs-lookup"><span data-stu-id="95518-112">**Periodic**</span></span>
-   <span data-ttu-id="95518-113">**プッシュ**</span><span class="sxs-lookup"><span data-stu-id="95518-113">**Push**</span></span>

<span data-ttu-id="95518-114">次の表は、通知配信の種類をまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="95518-114">This table summarizes the notification delivery types.</span></span>

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="95518-115">配信方法</span><span class="sxs-lookup"><span data-stu-id="95518-115">Delivery method</span></span></th>
<th align="left"><span data-ttu-id="95518-116">使用対象</span><span class="sxs-lookup"><span data-stu-id="95518-116">Use with</span></span></th>
<th align="left"><span data-ttu-id="95518-117">説明</span><span class="sxs-lookup"><span data-stu-id="95518-117">Description</span></span></th>
<th align="left"><span data-ttu-id="95518-118">例</span><span class="sxs-lookup"><span data-stu-id="95518-118">Examples</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="95518-119">ローカル</span><span class="sxs-lookup"><span data-stu-id="95518-119">Local</span></span></td>
<td align="left"><span data-ttu-id="95518-120">タイル、バッジ、トースト</span><span class="sxs-lookup"><span data-stu-id="95518-120">Tile, Badge, Toast</span></span></td>
<td align="left"><span data-ttu-id="95518-121">アプリが実行されている間、タイルやバッジを直接更新している間、またはトースト通知を送信している間に通知を送信する API 呼び出しのセットです。</span><span class="sxs-lookup"><span data-stu-id="95518-121">A set of API calls that send notifications while your app is running, directly updating the tile or badge, or sending a toast notification.</span></span></td>
<td align="left"><ul>
<li><span data-ttu-id="95518-122">音楽アプリでは、タイルを更新して &quot;再生中&quot; の音楽を表示します。</span><span class="sxs-lookup"><span data-stu-id="95518-122">A music app updates its tile to show what's &quot;Now Playing&quot;.</span></span></li>
<li><span data-ttu-id="95518-123">ゲーム アプリでは、ユーザーがゲームから離れるとタイルを更新してユーザーのハイ スコアを表示します。</span><span class="sxs-lookup"><span data-stu-id="95518-123">A game app updates its tile with the user's high score when the user leaves the game.</span></span></li>
<li><span data-ttu-id="95518-124">グリフでアプリに新しい情報があることが示されたバッジは、アプリがアクティブ化されるとクリアされます。</span><span class="sxs-lookup"><span data-stu-id="95518-124">A badge whose glyph indicates that there's new info int the app is cleared when the app is activated.</span></span></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="95518-125">スケジュール</span><span class="sxs-lookup"><span data-stu-id="95518-125">Scheduled</span></span></td>
<td align="left"><span data-ttu-id="95518-126">タイル、トースト</span><span class="sxs-lookup"><span data-stu-id="95518-126">Tile, Toast</span></span></td>
<td align="left"><span data-ttu-id="95518-127">指定した時間に更新が行われるように事前に通知をスケジュールする API 呼び出しのセットです。</span><span class="sxs-lookup"><span data-stu-id="95518-127">A set of API calls that schedule a notification in advance, to update at the time you specify.</span></span></td>
<td align="left"><ul>
<li><span data-ttu-id="95518-128">カレンダー アプリでは、予定されている会議用のトースト通知のアラームを設定します。</span><span class="sxs-lookup"><span data-stu-id="95518-128">A calendar app sets a toast notification reminder for an upcoming meeting.</span></span></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="95518-129">定期的</span><span class="sxs-lookup"><span data-stu-id="95518-129">Periodic</span></span></td>
<td align="left"><span data-ttu-id="95518-130">タイル、バッジ</span><span class="sxs-lookup"><span data-stu-id="95518-130">Tile, Badge</span></span></td>
<td align="left"><span data-ttu-id="95518-131">クラウド サービスをポーリングして新しいコンテンツの有無を調べて、タイルとバッジを一定の間隔で定期的に更新する通知です。</span><span class="sxs-lookup"><span data-stu-id="95518-131">Notifications that update tiles and badges regularly at a fixed time interval by polling a cloud service for new content.</span></span></td>
<td align="left"><ul>
<li><span data-ttu-id="95518-132">天気予報アプリでは、予報を表示するタイルを 30 分間隔で更新します。</span><span class="sxs-lookup"><span data-stu-id="95518-132">A weather app updates its tile, which shows the forecast, at 30-minute intervals.</span></span></li>
<li><span data-ttu-id="95518-133">&quot;日替わりセール情報&quot; サイトでは、本日のお買い得品を毎朝更新します。</span><span class="sxs-lookup"><span data-stu-id="95518-133">A &quot;daily deals&quot; site updates its deal-of-the-day every morning.</span></span></li>
<li><span data-ttu-id="95518-134">イベントまでの日数を表示するタイルでは、表示される日数のカウントダウンを毎日深夜 0 時に更新します。</span><span class="sxs-lookup"><span data-stu-id="95518-134">A tile that displays the days until an event updates the displayed countdown each day at midnight.</span></span></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="95518-135">プッシュ</span><span class="sxs-lookup"><span data-stu-id="95518-135">Push</span></span></td>
<td align="left"><span data-ttu-id="95518-136">タイル、バッジ、トースト、直接</span><span class="sxs-lookup"><span data-stu-id="95518-136">Tile, Badge, Toast, Raw</span></span></td>
<td align="left"><span data-ttu-id="95518-137">アプリが実行されていなくてもクラウド サーバーから送信される通知です。</span><span class="sxs-lookup"><span data-stu-id="95518-137">Notifications sent from a cloud server, even if your app isn't running.</span></span></td>
<td align="left"><ul>
<li><span data-ttu-id="95518-138">ショッピング アプリでは、トースト通知を送信して、ユーザーが注目している商品のセール情報を知らせます。</span><span class="sxs-lookup"><span data-stu-id="95518-138">A shopping app sends a toast notification to let a user know about a sale on an item that they're watching.</span></span></li>
<li><span data-ttu-id="95518-139">ニュース アプリでは、ニュース速報が発生したときにタイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="95518-139">A news app updates its tile with breaking news as it happens.</span></span></li>
<li><span data-ttu-id="95518-140">スポーツ アプリでは、試合の進行中にタイルを更新し続けます。</span><span class="sxs-lookup"><span data-stu-id="95518-140">A sports app keeps its tile up-to-date during an ongoing game.</span></span></li>
<li><span data-ttu-id="95518-141">通信アプリでは、メッセージや電話の着信をアラートで知らせます。</span><span class="sxs-lookup"><span data-stu-id="95518-141">A communication app provides alerts about incoming messages or phone calls.</span></span></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="local-notifications"></a><span data-ttu-id="95518-142">ローカル通知</span><span class="sxs-lookup"><span data-stu-id="95518-142">Local notifications</span></span>


<span data-ttu-id="95518-143">アプリの実行中に行われるタイルまたはバッジの更新やトースト通知の表示は、ローカルの API 呼び出しのみが必要となる、最もシンプルな通知配信メカニズムです。</span><span class="sxs-lookup"><span data-stu-id="95518-143">Updating the app tile or badge or raising a toast notification while the app is running is the simplest of the notification delivery mechanisms; it only requires local API calls.</span></span> <span data-ttu-id="95518-144">どのアプリでも、役立つ情報や興味を引く情報をタイルに表示することができます。これは、ユーザーがアプリを起動して操作を開始した後でのみコンテンツが変更される場合でも可能です。</span><span class="sxs-lookup"><span data-stu-id="95518-144">Every app can have useful or interesting information to show on the tile, even if that content only changes after the user launches and interacts with the app.</span></span> <span data-ttu-id="95518-145">他の通知メカニズムと併用する場合でも、ローカル通知はアプリのタイルを最新の状態にする手段として適しています。</span><span class="sxs-lookup"><span data-stu-id="95518-145">Local notifications are also a good way to keep the app tile current, even if you also use one of the other notification mechanisms.</span></span> <span data-ttu-id="95518-146">たとえば、フォト アプリのタイルでは、最近追加されたアルバムの写真を表示できます。</span><span class="sxs-lookup"><span data-stu-id="95518-146">For instance, a photo app tile could show photos from a recently added album.</span></span>

<span data-ttu-id="95518-147">アプリによるタイルのローカルな更新は、アプリが最初に起動されたとき、またはアプリによってタイルに反映される変更をユーザーが加えた直後に行うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="95518-147">We recommended that your app update its tile locally on first launch, or at least immediately after the user makes a change that your app would normally reflect on the tile.</span></span> <span data-ttu-id="95518-148">この更新内容は、ユーザーがアプリから離れるまで表示されせんが、アプリが使われている間にタイルを更新することで、ユーザーがアプリから離れたときにタイルは確実に最新の状態になります。</span><span class="sxs-lookup"><span data-stu-id="95518-148">That update isn't seen until the user leaves the app, but by making that change while the app is being used ensures that the tile is already up-to-date when the user departs.</span></span>

<span data-ttu-id="95518-149">API 呼び出しはローカルですが、通知では Web 画像を参照できます。</span><span class="sxs-lookup"><span data-stu-id="95518-149">While the API calls are local, the notifications can reference web images.</span></span> <span data-ttu-id="95518-150">Web 画像が、ダウンロードできない場合、破損している場合、または画像の仕様を満たしていない場合、タイルとトーストでは応答が次のように異なります。</span><span class="sxs-lookup"><span data-stu-id="95518-150">If the web image is not available for download, is corrupted, or doesn't meet the image specifications, tiles and toast respond differently:</span></span>

-   <span data-ttu-id="95518-151">タイル:更新プログラムは表示されません。</span><span class="sxs-lookup"><span data-stu-id="95518-151">Tiles: The update is not shown</span></span>
-   <span data-ttu-id="95518-152">トースト:通知が表示されますが、イメージの削除</span><span class="sxs-lookup"><span data-stu-id="95518-152">Toast: The notification is displayed, but your image is dropped</span></span>

<span data-ttu-id="95518-153">既定では、ローカル トースト通知は 3 日後に有効期限が切れ、ローカル タイル通知には有効期限がありません。</span><span class="sxs-lookup"><span data-stu-id="95518-153">By default, local toast notifications expire in three days, and local tile notifications never expire.</span></span> <span data-ttu-id="95518-154">これらの既定値を、具体的な通知に適した有効期限で上書きすることをお勧めします (トースト通知の有効期限は、最大 3 日間です)。</span><span class="sxs-lookup"><span data-stu-id="95518-154">We recommend overriding these defaults with an explicit expiration time that makes sense for your notifications (toasts have a max of three days).</span></span> 

<span data-ttu-id="95518-155">詳しくは、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="95518-155">For more information, see these topics:</span></span>

-   [<span data-ttu-id="95518-156">ローカル タイル通知の送信</span><span class="sxs-lookup"><span data-stu-id="95518-156">Send a local tile notification</span></span>](sending-a-local-tile-notification.md)
-   [<span data-ttu-id="95518-157">ローカル トースト通知の送信</span><span class="sxs-lookup"><span data-stu-id="95518-157">Send a local toast notification</span></span>](send-local-toast.md)
-   [<span data-ttu-id="95518-158">ユニバーサル Windows プラットフォーム (UWP) 通知コード サンプル</span><span class="sxs-lookup"><span data-stu-id="95518-158">Universal Windows Platform (UWP) notifications code samples</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Notifications)

## <a name="scheduled-notifications"></a><span data-ttu-id="95518-159">スケジュールされた通知</span><span class="sxs-lookup"><span data-stu-id="95518-159">Scheduled notifications</span></span>


<span data-ttu-id="95518-160">スケジュールされた通知は、タイルを更新する時刻またはトースト通知を表示する時刻を正確に指定できるローカル通知のサブセットです。</span><span class="sxs-lookup"><span data-stu-id="95518-160">Scheduled notifications are the subset of local notifications that can specify the precise time when a tile should be updated or a toast notification should be shown.</span></span> <span data-ttu-id="95518-161">スケジュールされた通知は、会議の招集など、更新される内容があらかじめわかっている場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="95518-161">Scheduled notifications are ideal in situations where the content to be updated is known in advance, such as a meeting invitation.</span></span> <span data-ttu-id="95518-162">通知の内容が事前にわからない場合は、プッシュ通知または定期的な通知を使う必要があります。</span><span class="sxs-lookup"><span data-stu-id="95518-162">If you don't have advance knowledge of the notification content, you should use a push or periodic notification.</span></span>

<span data-ttu-id="95518-163">バッジ通知には、スケジュールされた通知を使うことはできません。バッジ通知は、ローカル通知、定期的な通知、プッシュ通知に最も適しています。</span><span class="sxs-lookup"><span data-stu-id="95518-163">Note that scheduled notifications cannot be used for badge notifications; badge notifications are best served by local, periodic, or push notifications.</span></span>

<span data-ttu-id="95518-164">スケジュールされた通知は、既定で配信されたときから 3 日後に有効期限切れになります。</span><span class="sxs-lookup"><span data-stu-id="95518-164">By default, scheduled notifications expire three days from the time they are delivered.</span></span> <span data-ttu-id="95518-165">スケジュールされたタイル通知では、この既定の有効期限を上書きできますが、スケジュールされたトースト通知の有効期限を上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="95518-165">You can override this default expiration time on scheduled tile notifications, but you cannot override the expiration time on scheduled toasts.</span></span>

<span data-ttu-id="95518-166">詳しくは、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="95518-166">For more information, see these topics:</span></span>

-   [<span data-ttu-id="95518-167">ユニバーサル Windows プラットフォーム (UWP) 通知コード サンプル</span><span class="sxs-lookup"><span data-stu-id="95518-167">Universal Windows Platform (UWP) notifications code samples</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Notifications)

## <a name="periodic-notifications"></a><span data-ttu-id="95518-168">定期的な通知</span><span class="sxs-lookup"><span data-stu-id="95518-168">Periodic notifications</span></span>


<span data-ttu-id="95518-169">定期的な通知では、最小限のクラウド サービスとクライアントの投資で、ライブ タイルを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="95518-169">Periodic notifications give you live tile updates with a minimal cloud service and client investment.</span></span> <span data-ttu-id="95518-170">この通知は、同じコンテンツを多数のユーザーに配信する方法としても優れています。</span><span class="sxs-lookup"><span data-stu-id="95518-170">They are also an excellent method of distributing the same content to a wide audience.</span></span> <span data-ttu-id="95518-171">クライアント コードでは、Windows がタイルまたはバッジの更新の有無を確認するためにポーリングするクラウドの場所の URL と、ポーリングの頻度を指定します。</span><span class="sxs-lookup"><span data-stu-id="95518-171">Your client code specifies the URL of a cloud location that Windows polls for tile or badge updates, and how often the location should be polled.</span></span> <span data-ttu-id="95518-172">各ポーリング間隔で、Windows は URL にアクセスして指定された XML コンテンツをダウンロードして、タイルに表示します。</span><span class="sxs-lookup"><span data-stu-id="95518-172">At each polling interval, Windows contacts the URL to download the specified XML content and display it on the tile.</span></span>

<span data-ttu-id="95518-173">定期的な通知では、アプリがクラウド サービスをホストする必要があります。このサービスは、アプリをインストールしたすべてのユーザーから指定した間隔でポーリングされます。</span><span class="sxs-lookup"><span data-stu-id="95518-173">Periodic notifications require the app to host a cloud service, and this service will be polled at the specified interval by all users who have the app installed.</span></span> <span data-ttu-id="95518-174">トースト通知には定期的な更新を使うことができないので注意してください。トースト通知は、スケジュールされた通知またはプッシュ通知で適切に表示されます。</span><span class="sxs-lookup"><span data-stu-id="95518-174">Note that periodic updates cannot be used for toast notifications; toast notifications are best served by scheduled or push notifications.</span></span>

<span data-ttu-id="95518-175">定期的な通知は、既定でポーリングが実行されたときから 3 日後に有効期限切れになります。</span><span class="sxs-lookup"><span data-stu-id="95518-175">By default, periodic notifications expire three days from the time polling occurs.</span></span> <span data-ttu-id="95518-176">必要に応じて、明示的な有効期限を設定してこの既定値を上書きできます。</span><span class="sxs-lookup"><span data-stu-id="95518-176">If needed, you can override this default with an explicit expiration time.</span></span>

<span data-ttu-id="95518-177">詳しくは、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="95518-177">For more information, see these topics:</span></span>

-   [<span data-ttu-id="95518-178">定期的な通知の概要</span><span class="sxs-lookup"><span data-stu-id="95518-178">Periodic notification overview</span></span>](periodic-notification-overview.md)
-   [<span data-ttu-id="95518-179">ユニバーサル Windows プラットフォーム (UWP) 通知コード サンプル</span><span class="sxs-lookup"><span data-stu-id="95518-179">Universal Windows Platform (UWP) notifications code samples</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Notifications)

## <a name="push-notifications"></a><span data-ttu-id="95518-180">プッシュ通知</span><span class="sxs-lookup"><span data-stu-id="95518-180">Push notifications</span></span>


<span data-ttu-id="95518-181">プッシュ通知は、リアルタイム データまたはユーザー向けにカスタマイズされたデータと通信する場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="95518-181">Push notifications are ideal to communicate real-time data or data that is personalized for your user.</span></span> <span data-ttu-id="95518-182">また、ニュース速報、ソーシャル ネットワークの更新、インスタント メッセージなどの予測不可能なタイミングで生成されるコンテンツについても、プッシュ通知が使われます。</span><span class="sxs-lookup"><span data-stu-id="95518-182">Push notifications are used for content that is generated at unpredictable times, such as breaking news, social network updates, or instant messages.</span></span> <span data-ttu-id="95518-183">プッシュ通知は、定期的な通知が適さない即時性を必要とするデータ (スポーツの試合中の得点など) にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="95518-183">Push notifications are also useful in situations where the data is time-sensitive in a way that would not suit periodic notifications, such as sports scores during a game.</span></span>

<span data-ttu-id="95518-184">プッシュ通知を利用するには、プッシュ通知チャネルを管理して、通知を送信するタイミングと送信先のユーザーを判断するクラウド サービスが必要です。</span><span class="sxs-lookup"><span data-stu-id="95518-184">Push notifications require a cloud service that manages push notification channels and chooses when and to whom to send notifications.</span></span>

<span data-ttu-id="95518-185">プッシュ通知は、既定でデバイスで受信されたときから 3 日後に有効期限切れになります。</span><span class="sxs-lookup"><span data-stu-id="95518-185">By default, push notifications expire three days from the time they are received by the device.</span></span> <span data-ttu-id="95518-186">必要に応じて、明示的な有効期限を設定してこの既定値を上書きできます (トースト通知の有効期限は、最大 3 日間です)。</span><span class="sxs-lookup"><span data-stu-id="95518-186">If needed, you can override this default with an explicit expiration time (toasts have a max of three days).</span></span>

<span data-ttu-id="95518-187">詳しくは、次のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="95518-187">For more information, see:</span></span>

-   [<span data-ttu-id="95518-188">Windows プッシュ通知サービス (WNS) の概要</span><span class="sxs-lookup"><span data-stu-id="95518-188">Windows Push Notification Services (WNS) overview</span></span>](windows-push-notification-services--wns--overview.md)
-   [<span data-ttu-id="95518-189">プッシュ通知のガイドライン</span><span class="sxs-lookup"><span data-stu-id="95518-189">Guidelines for push notifications</span></span>](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)
-   [<span data-ttu-id="95518-190">ユニバーサル Windows プラットフォーム (UWP) 通知コード サンプル</span><span class="sxs-lookup"><span data-stu-id="95518-190">Universal Windows Platform (UWP) notifications code samples</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Notifications)


## <a name="related-topics"></a><span data-ttu-id="95518-191">関連トピック</span><span class="sxs-lookup"><span data-stu-id="95518-191">Related topics</span></span>


* [<span data-ttu-id="95518-192">ローカル タイル通知の送信</span><span class="sxs-lookup"><span data-stu-id="95518-192">Send a local tile notification</span></span>](sending-a-local-tile-notification.md)
* [<span data-ttu-id="95518-193">ローカル トースト通知の送信</span><span class="sxs-lookup"><span data-stu-id="95518-193">Send a local toast notification</span></span>](send-local-toast.md)
* [<span data-ttu-id="95518-194">プッシュ通知のガイドライン</span><span class="sxs-lookup"><span data-stu-id="95518-194">Guidelines for push notifications</span></span>](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)
* [<span data-ttu-id="95518-195">トースト通知のガイドライン</span><span class="sxs-lookup"><span data-stu-id="95518-195">Guidelines for toast notifications</span></span>](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-badges-notifications)
* [<span data-ttu-id="95518-196">定期的な通知の概要</span><span class="sxs-lookup"><span data-stu-id="95518-196">Periodic notification overview</span></span>](periodic-notification-overview.md)
* [<span data-ttu-id="95518-197">Windows プッシュ通知サービス (WNS) の概要</span><span class="sxs-lookup"><span data-stu-id="95518-197">Windows Push Notification Services (WNS) overview</span></span>](windows-push-notification-services--wns--overview.md)
* [<span data-ttu-id="95518-198">ユニバーサル Windows プラットフォーム (UWP) の通知は GitHub のサンプルをコードします。</span><span class="sxs-lookup"><span data-stu-id="95518-198">Universal Windows Platform (UWP) notifications code samples on GitHub</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Notifications)
 

 




