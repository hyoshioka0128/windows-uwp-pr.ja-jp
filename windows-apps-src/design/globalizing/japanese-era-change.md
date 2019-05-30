---
title: アプリケーションの新元号対応
description: 2019 年 5 月に行われる改元と、アプリケーションでの対応方法について説明します。
ms.assetid: 5A945F9A-8632-4038-ADD6-C0568091EF27
ms.date: 4/26/2019
ms.topic: article
keywords: Windows 10, UWP, ローカライズの可否, ローカライズ, 日本, 元号
ms.localizationpriority: high
ms.openlocfilehash: 54d66d0426e5f0c41d48b93ba96781786d6fab92
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66363778"
---
# <a name="prepare-your-application-for-the-japanese-era-change"></a><span data-ttu-id="b02ae-104">アプリケーションの新元号対応</span><span class="sxs-lookup"><span data-stu-id="b02ae-104">Prepare your application for the Japanese era change</span></span>

> [!NOTE]
> <span data-ttu-id="b02ae-105">2019 年 4 月 1日で新しい時代 (年号) の名前が発表されました。Reiwa (令和)。</span><span class="sxs-lookup"><span data-stu-id="b02ae-105">On April 1, 2019, the new era name was announced: Reiwa (令和).</span></span> <span data-ttu-id="b02ae-106">4 月 25 日には、Microsoft は、新しい時代 (年号) の名前で更新されたレジストリ キーを含む別の Windows オペレーティング システムのパッケージをリリースしました。</span><span class="sxs-lookup"><span data-stu-id="b02ae-106">On April 25, Microsoft released packages for different Windows operating systems containing the updated registry key with the new era name.</span></span> <span data-ttu-id="b02ae-107">デバイスを更新し、新しいキーを持っているかどうかに、レジストリを確認し、アプリケーションをテストします。</span><span class="sxs-lookup"><span data-stu-id="b02ae-107">Update your device and check your registry to see if it has the new key, and then test your application.</span></span> <span data-ttu-id="b02ae-108">確認[サポート記事](https://support.microsoft.com/help/4469068/summary-of-new-japanese-era-updates-kb4469068)オペレーティング システムに更新されたレジストリ キーを受信する必要がありますがあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-108">Check [this support article](https://support.microsoft.com/help/4469068/summary-of-new-japanese-era-updates-kb4469068) to make sure your operating system should have received the updated registry key.</span></span>

<span data-ttu-id="b02ae-109">和暦が時代 (年号) に分割され、コンピューティングの最新の有効期間のほとんどは、しました平成時代 (年号)。ただし、2019 年 5 月 1日で新しい時代 (年号) が開始されます。</span><span class="sxs-lookup"><span data-stu-id="b02ae-109">The Japanese calendar is divided into eras, and for most of the modern age of computing, we've been in the Heisei era; however, on May 1, 2019, a new era will begin.</span></span> <span data-ttu-id="b02ae-110">元号が変わるのは約 30 年ぶりであるため、和暦をサポートしているソフトウェアについてはテストを行い、新元号になっても正しく動作するか確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b02ae-110">Because this is the first time in decades for an era to change, software that supports the Japanese calendar will need to be tested to ensure it will function properly when the new era begins.</span></span>

<span data-ttu-id="b02ae-111">以下の各セクションでは、新元号への対応としてアプリケーションの準備とテストを実施する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-111">In the following sections, you will learn what you can do to prepare and test your application for the upcoming new era.</span></span>

> [!NOTE]
> <span data-ttu-id="b02ae-112">テストに使用する変更内容はコンピューター全体の動作に影響するため、テストにはテスト用コンピューターの使用をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b02ae-112">We recommend that you use a test machine for this, because the changes you make will impact the behavior of the entire machine.</span></span>

## <a name="add-a-registry-key-for-the-new-era"></a><span data-ttu-id="b02ae-113">新元号のレジストリ キーを追加する</span><span class="sxs-lookup"><span data-stu-id="b02ae-113">Add a registry key for the new era</span></span>

> [!NOTE]
> <span data-ttu-id="b02ae-114">次の手順については、新しいレジストリ キーで更新されていないデバイスのものです。</span><span class="sxs-lookup"><span data-stu-id="b02ae-114">The following instructions are meant for devices that have not yet been updated with the new registry key.</span></span> <span data-ttu-id="b02ae-115">まず、デバイスに、新しいレジストリ キーが含まれているかどうかを確認し、そうでない場合、次の手順を使用してをテストします。</span><span class="sxs-lookup"><span data-stu-id="b02ae-115">First check if your device contains the new registry key, and if not, test using the following instructions.</span></span>

<span data-ttu-id="b02ae-116">時代 (年号) が変更されていると、これで新しい時代 (年号) の名前を使用して行うことができます前に、互換性の問題のテストは重要です。</span><span class="sxs-lookup"><span data-stu-id="b02ae-116">It is important to test for compatibility problems before the era has changed, and you can do so now using the new era name.</span></span> <span data-ttu-id="b02ae-117">これを行うには、**レジストリ エディター**を使用して、新元号のレジストリ キーを追加します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-117">To do this, add a registry key for the new era using **Registry Editor**:</span></span>

1. <span data-ttu-id="b02ae-118">**Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Nls\Calendars\Japanese\Eras** に移動します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-118">Navigate to **Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Nls\Calendars\Japanese\Eras**.</span></span>
2. <span data-ttu-id="b02ae-119">**[編集] > [新規] > [文字列値]** を選択し、「**2019 05 01**」という名前をつけます。</span><span class="sxs-lookup"><span data-stu-id="b02ae-119">Select **Edit > New > String Value**, and give it the name **2019 05 01**.</span></span>
3. <span data-ttu-id="b02ae-120">キーを右クリックし、 **[修正]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-120">Right-click the key and select **Modify**.</span></span>
4. <span data-ttu-id="b02ae-121">**値データ**フィールドに、入力**令和_令_Reiwa_R** (コピーして簡単にここから貼り付けます)。</span><span class="sxs-lookup"><span data-stu-id="b02ae-121">In the **Value data** field, enter **令和_令_Reiwa_R** (you can copy and paste from here to make it easier).</span></span>

<span data-ttu-id="b02ae-122">これらのレジストリ キーの書式については、「[和暦での元号処理](https://docs.microsoft.com/windows/desktop/Intl/era-handling-for-the-japanese-calendar)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b02ae-122">See [Era Handling for the Japanese Calendar](https://docs.microsoft.com/windows/desktop/Intl/era-handling-for-the-japanese-calendar) to read more about the format for these registry keys.</span></span>

<span data-ttu-id="b02ae-123">2019 年 4 月 1日で新しい時代 (年号) の名前が発表されました。</span><span class="sxs-lookup"><span data-stu-id="b02ae-123">On April 1, 2019, the new era name was announced.</span></span> <span data-ttu-id="b02ae-124">年 4 月 25 日に、名前を含む、サポートされている Windows バージョンの新しいレジストリ キーで更新プログラムがリリースされた、正しく処理アプリケーションを検証することができます。</span><span class="sxs-lookup"><span data-stu-id="b02ae-124">On April 25, an update with a new registry key for supported Windows versions containing the name was released, allowing you to validate that your application handles it properly.</span></span> <span data-ttu-id="b02ae-125">以前のリリースの Windows 8 と Windows 10、および 7 をサポートするには、この更新プログラムを反映中です。</span><span class="sxs-lookup"><span data-stu-id="b02ae-125">This update is being propagated to supported earlier releases of Windows 10, as well as Windows 8 and 7.</span></span>

<span data-ttu-id="b02ae-126">プレースホルダーを使用したレジストリ キーは、アプリケーションのテストが終了したら削除できます。</span><span class="sxs-lookup"><span data-stu-id="b02ae-126">You can delete your placeholder registry key once you're finished testing your application.</span></span> <span data-ttu-id="b02ae-127">削除しておくと、Windows の更新時に追加される新しいレジストリ キーに干渉する心配がなくなります。</span><span class="sxs-lookup"><span data-stu-id="b02ae-127">This will ensure it doesn't interfere with the new registry key that will be added when Windows is updated.</span></span>

## <a name="change-your-devices-calendar-format"></a><span data-ttu-id="b02ae-128">デバイスのカレンダー形式を変更する</span><span class="sxs-lookup"><span data-stu-id="b02ae-128">Change your device's calendar format</span></span>

<span data-ttu-id="b02ae-129">新元号のレジストリ キーを追加したら、和暦が使用されるようにデバイスを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b02ae-129">Once you've added the registry key for the new era, you need to configure your device to use the Japanese calendar.</span></span> <span data-ttu-id="b02ae-130">これを行うために日本語のデバイスは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="b02ae-130">You don't need to have a Japanese-language device to do this.</span></span> <span data-ttu-id="b02ae-131">綿密なテストを行うためには日本語の言語パックをインストールすることもできますが、基本的なテスト用には必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="b02ae-131">For thorough testing, you may want to install the Japanese language pack as well, but it isn't required for basic testing.</span></span>

<span data-ttu-id="b02ae-132">和暦が使用されるようにデバイスを構成するには:</span><span class="sxs-lookup"><span data-stu-id="b02ae-132">To configure your device to use the Japanese calendar:</span></span>

1. <span data-ttu-id="b02ae-133">**intl.cpl** (Windows 検索バーで検索してください) を開きます。</span><span class="sxs-lookup"><span data-stu-id="b02ae-133">Open **intl.cpl** (search for it from the Windows search bar).</span></span>
2. <span data-ttu-id="b02ae-134">**[形式]** ドロップダウンから **[日本語 (日本)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-134">From the **Format** dropdown, select **Japanese (Japan)**.</span></span>
3. <span data-ttu-id="b02ae-135">**[追加の設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-135">Select **Additional settings**.</span></span>
4. <span data-ttu-id="b02ae-136">**[日付]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-136">Select the **Date** tab.</span></span>
5. <span data-ttu-id="b02ae-137">**[カレンダーの種類]** ドロップダウンで、 **[和暦]** ("*和暦*" とは日本のカレンダーの意味) を選択します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-137">From the **Calendar type** dropdown, select **和暦** (*wareki*, the Japanese calendar).</span></span> <span data-ttu-id="b02ae-138">2 番目のオプションが [和暦] です</span><span class="sxs-lookup"><span data-stu-id="b02ae-138">It should be the second option.</span></span>
6. <span data-ttu-id="b02ae-139">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b02ae-139">Click **OK**.</span></span>
7. <span data-ttu-id="b02ae-140">**[地域]** ウィンドウで **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="b02ae-140">Click **OK** in the **Region** window.</span></span>

<span data-ttu-id="b02ae-141">デバイスは和暦を使用するように構成され、レジストリにある元号が反映されます。</span><span class="sxs-lookup"><span data-stu-id="b02ae-141">Your device should now be configured to use the Japanese calendar, and it will reflect whichever eras are in the registry.</span></span> <span data-ttu-id="b02ae-142">以下は、画面の右下に表示される日付形式の例です。</span><span class="sxs-lookup"><span data-stu-id="b02ae-142">Below is an example of what you might see now in the lower-right corner of the screen:</span></span>

![和暦形式の日付と時刻](images/japanese-calendar-format.png)

## <a name="adjust-your-devices-clock"></a><span data-ttu-id="b02ae-144">デバイスのクロックを調整する</span><span class="sxs-lookup"><span data-stu-id="b02ae-144">Adjust your device's clock</span></span>

<span data-ttu-id="b02ae-145">アプリケーションが新元号に対応していることをテストするには、コンピューターのクロックを 2019 年 5 月 1日以降に進める必要があります。</span><span class="sxs-lookup"><span data-stu-id="b02ae-145">To test that your application works with the new era, you must advance your computer's clock to May 1, 2019 or later.</span></span> <span data-ttu-id="b02ae-146">次の手順は Windows 10 用ですが、Windows 8 および 7 でも同様の手順になります。</span><span class="sxs-lookup"><span data-stu-id="b02ae-146">The following instructions are for Windows 10, but Windows 8 and 7 should work similarly:</span></span>

1. <span data-ttu-id="b02ae-147">画面の右下隅にある日付と時刻の領域を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="b02ae-147">Right-click the date and time area in the lower-right corner of the screen.</span></span>
2. <span data-ttu-id="b02ae-148">**[日付と時刻の調整]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-148">Select **Adjust date/time**.</span></span>
3. <span data-ttu-id="b02ae-149">設定アプリの **[日付と時刻を変更する]** で、 **[変更]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-149">In the Settings app, under **Change date and time**, select **Change**.</span></span>
4. <span data-ttu-id="b02ae-150">日付を 2019 年 5 月 1 日以降に変更します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-150">Change the date to on or after May 1, 2019.</span></span>

> [!NOTE]
> <span data-ttu-id="b02ae-151">組織の設定に基づいて日付を変更することはできません。この場合する場合、。 管理者にお問い合わせまたは、既に渡された日付を使用して、プレース ホルダーのレジストリ キーを編集できます。</span><span class="sxs-lookup"><span data-stu-id="b02ae-151">You may not be able to change the date based on organization settings; if this is the case, talk to your admin. Alternatively, you can edit your placeholder registry key to have a date that has already passed.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="b02ae-152">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="b02ae-152">Test your application</span></span>

<span data-ttu-id="b02ae-153">では、アプリケーションで新元号を処理できるかどうかをテストしましょう。</span><span class="sxs-lookup"><span data-stu-id="b02ae-153">Now, test out how your application handles the new era.</span></span> <span data-ttu-id="b02ae-154">タイムスタンプや日付の選択コントロールなど、日付が表示される場所で表示を確認します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-154">Check places where the date is displayed, such as timestamps and date pickers.</span></span> <span data-ttu-id="b02ae-155">(Reiwa 令和) の前後には、2019 年 5 月 1日 (平成平成)、時代 (年号) が正しいことを確認します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-155">Make sure that the era is correct before May 1, 2019 (Heisei, 平成) and after (Reiwa, 令和).</span></span>

### <a name="gannen-"></a><span data-ttu-id="b02ae-156">*元年*</span><span class="sxs-lookup"><span data-stu-id="b02ae-156">*Gannen* (元年)</span></span>

<span data-ttu-id="b02ae-157">日本語のカレンダーの形式は、通常 **&lt;時代 (年号) の名前&gt; &lt;時代 (年号) の年&gt;** します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-157">The format for the Japanese calendar is generally **&lt;Era name&gt; &lt;Year of era&gt;**.</span></span> <span data-ttu-id="b02ae-158">たとえば、2018 年は "**平成 30 年**" です。</span><span class="sxs-lookup"><span data-stu-id="b02ae-158">For example, the year 2018 is **Heisei 30** (平成30年).</span></span>  <span data-ttu-id="b02ae-159">ただし、各元号の最初の年には特殊な表記法を使用し、" **&lt;元号&gt; 1 年**" ではなく " **&lt;元号&gt; 元年**" *と表記します*。</span><span class="sxs-lookup"><span data-stu-id="b02ae-159">However, the first year of an era is special; instead of being **&lt;Era name&gt; 1**, it is **&lt;Era name&gt; 元年** (*gannen*).</span></span> <span data-ttu-id="b02ae-160">このため、平成の最初の年は "*平成元年*" となります。</span><span class="sxs-lookup"><span data-stu-id="b02ae-160">So, the first year of the Heisei era would be 平成元年 (*Heisei gannen*).</span></span> <span data-ttu-id="b02ae-161">アプリケーションが新しい時代 (年号) の最初の年を適切に処理し、正しく令和元年を出力してください。</span><span class="sxs-lookup"><span data-stu-id="b02ae-161">Make sure that your application properly handles the first year of the new era, and correctly outputs 令和元年.</span></span>

## <a name="related-apis"></a><span data-ttu-id="b02ae-162">関連する API</span><span class="sxs-lookup"><span data-stu-id="b02ae-162">Related APIs</span></span>

<span data-ttu-id="b02ae-163">いくつかの WinRT、.NET、Win32 API は、改元を処理できるよう更新されるため、これらを使用する場合にはそれほど心配する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b02ae-163">There are several WinRT, .NET, and Win32 APIs that will be updated to handle the era change, so if you use them, you shouldn't have to worry too much.</span></span> <span data-ttu-id="b02ae-164">ただし、全面的にこれらの API を使用している場合も (解析などの特殊処理を行う場合は特に)、アプリケーションをテストして、動作に問題がないか確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b02ae-164">However, even if you do rely entirely on these APIs, it's still a good idea to test your application and make sure you get the desired behavior, especially if you are doing anything special with them like parsing.</span></span>

<span data-ttu-id="b02ae-165">更新プログラムをに従って OS に Sdk を[用の更新プログラムには、2019 日本の時代 (年号) の変更が可能性があります](https://support.microsoft.com/help/4470918/updates-for-may-2019-japan-era-change)します。</span><span class="sxs-lookup"><span data-stu-id="b02ae-165">You can follow along with updates to the OS and SDKs at [Updates for May 2019 Japan Era Change](https://support.microsoft.com/help/4470918/updates-for-may-2019-japan-era-change).</span></span>

<span data-ttu-id="b02ae-166">影響を受けるのは次の API です。</span><span class="sxs-lookup"><span data-stu-id="b02ae-166">The following APIs will be impacted:</span></span>

### <a name="winrt"></a><span data-ttu-id="b02ae-167">WinRT</span><span class="sxs-lookup"><span data-stu-id="b02ae-167">WinRT</span></span>

* [<span data-ttu-id="b02ae-168">Windows.Globalization Namespace</span><span class="sxs-lookup"><span data-stu-id="b02ae-168">Windows.Globalization Namespace</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization)
  * [<span data-ttu-id="b02ae-169">Calendar クラス</span><span class="sxs-lookup"><span data-stu-id="b02ae-169">Calendar Class</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar)
    * [<span data-ttu-id="b02ae-170">AddDays メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-170">AddDays Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.adddays)
    * [<span data-ttu-id="b02ae-171">AddEras メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-171">AddEras Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.adderas)
    * [<span data-ttu-id="b02ae-172">AddHours メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-172">AddHours Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addhours)
    * [<span data-ttu-id="b02ae-173">AddMinutes メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-173">AddMinutes Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addminutes)
    * [<span data-ttu-id="b02ae-174">AddMonths メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-174">AddMonths Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addmonths)
    * [<span data-ttu-id="b02ae-175">AddNanoseconds メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-175">AddNanoseconds Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addnanoseconds)
    * [<span data-ttu-id="b02ae-176">AddPeriods メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-176">AddPeriods Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addperiods)
    * [<span data-ttu-id="b02ae-177">AddSeconds メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-177">AddSeconds Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addseconds)
    * [<span data-ttu-id="b02ae-178">AddWeeks メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-178">AddWeeks Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addweeks)
    * [<span data-ttu-id="b02ae-179">AddYears メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-179">AddYears Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.addyears)
    * [<span data-ttu-id="b02ae-180">時代 (年号) のプロパティ</span><span class="sxs-lookup"><span data-stu-id="b02ae-180">Era Property</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.era)
    * [<span data-ttu-id="b02ae-181">EraAsString メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-181">EraAsString Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.eraasstring)
    * [<span data-ttu-id="b02ae-182">FirstYearInThisEra プロパティ</span><span class="sxs-lookup"><span data-stu-id="b02ae-182">FirstYearInThisEra Property</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.firstyearinthisera)
    * [<span data-ttu-id="b02ae-183">LastEra プロパティ</span><span class="sxs-lookup"><span data-stu-id="b02ae-183">LastEra Property</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.lastera)
    * [<span data-ttu-id="b02ae-184">LastYearInThisEra プロパティ</span><span class="sxs-lookup"><span data-stu-id="b02ae-184">LastYearInThisEra Property</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.lastyearinthisera)
    * [<span data-ttu-id="b02ae-185">NumberOfYearsInThisEra プロパティ</span><span class="sxs-lookup"><span data-stu-id="b02ae-185">NumberOfYearsInThisEra Property</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.calendar.numberofyearsinthisera)
* [<span data-ttu-id="b02ae-186">Windows.Globalization.DateTimeFormatting Namespace</span><span class="sxs-lookup"><span data-stu-id="b02ae-186">Windows.Globalization.DateTimeFormatting Namespace</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.datetimeformatting)
  * [<span data-ttu-id="b02ae-187">DateTimeFormatter クラス</span><span class="sxs-lookup"><span data-stu-id="b02ae-187">DateTimeFormatter Class</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.datetimeformatting.datetimeformatter)
    * [<span data-ttu-id="b02ae-188">Format メソッド</span><span class="sxs-lookup"><span data-stu-id="b02ae-188">Format Method</span></span>](https://docs.microsoft.com/uwp/api/windows.globalization.datetimeformatting.datetimeformatter.format)

### <a name="net"></a><span data-ttu-id="b02ae-189">.NET</span><span class="sxs-lookup"><span data-stu-id="b02ae-189">.NET</span></span>

* [<span data-ttu-id="b02ae-190">System Namespace</span><span class="sxs-lookup"><span data-stu-id="b02ae-190">System Namespace</span></span>](https://docs.microsoft.com/dotnet/api/system)
  * [<span data-ttu-id="b02ae-191">DateTime 構造体</span><span class="sxs-lookup"><span data-stu-id="b02ae-191">DateTime Struct</span></span>](https://docs.microsoft.com/dotnet/api/system.datetime)
  * [<span data-ttu-id="b02ae-192">DateTimeOffset 構造体</span><span class="sxs-lookup"><span data-stu-id="b02ae-192">DateTimeOffset Struct</span></span>](https://docs.microsoft.com/dotnet/api/system.datetimeoffset)
* [<span data-ttu-id="b02ae-193">System.Globalization Namespace</span><span class="sxs-lookup"><span data-stu-id="b02ae-193">System.Globalization Namespace</span></span>](https://docs.microsoft.com/dotnet/api/system.globalization)
  * [<span data-ttu-id="b02ae-194">Calendar クラス</span><span class="sxs-lookup"><span data-stu-id="b02ae-194">Calendar Class</span></span>](https://docs.microsoft.com/dotnet/api/system.globalization.calendar)
  * [<span data-ttu-id="b02ae-195">DateTimeFormatInfo クラス</span><span class="sxs-lookup"><span data-stu-id="b02ae-195">DateTimeFormatInfo Class</span></span>](https://docs.microsoft.com/dotnet/api/system.globalization.datetimeformatinfo)
  * [<span data-ttu-id="b02ae-196">JapaneseCalendar クラス</span><span class="sxs-lookup"><span data-stu-id="b02ae-196">JapaneseCalendar Class</span></span>](https://docs.microsoft.com/dotnet/api/system.globalization.japanesecalendar)
  * [<span data-ttu-id="b02ae-197">JapaneseLunisolarCalendar クラス</span><span class="sxs-lookup"><span data-stu-id="b02ae-197">JapaneseLunisolarCalendar Class</span></span>](https://docs.microsoft.com/dotnet/api/system.globalization.japaneselunisolarcalendar)

### <a name="win32"></a><span data-ttu-id="b02ae-198">Win32</span><span class="sxs-lookup"><span data-stu-id="b02ae-198">Win32</span></span>

* [<span data-ttu-id="b02ae-199">datetimeapi.h header</span><span class="sxs-lookup"><span data-stu-id="b02ae-199">datetimeapi.h header</span></span>](https://docs.microsoft.com/windows/desktop/api/datetimeapi/)
  * [<span data-ttu-id="b02ae-200">GetDateFormatA 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-200">GetDateFormatA function</span></span>](https://docs.microsoft.com/windows/desktop/api/datetimeapi/nf-datetimeapi-getdateformata)
  * [<span data-ttu-id="b02ae-201">GetDateFormatEx 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-201">GetDateFormatEx function</span></span>](https://docs.microsoft.com/windows/desktop/api/datetimeapi/nf-datetimeapi-getdateformatex)
  * [<span data-ttu-id="b02ae-202">GetDateFormatW 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-202">GetDateFormatW function</span></span>](https://docs.microsoft.com/windows/desktop/api/datetimeapi/nf-datetimeapi-getdateformatw)
* [<span data-ttu-id="b02ae-203">winnls.h ヘッダー</span><span class="sxs-lookup"><span data-stu-id="b02ae-203">winnls.h header</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/)
  * [<span data-ttu-id="b02ae-204">EnumDateFormatsA 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-204">EnumDateFormatsA function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-enumdateformatsa)
  * [<span data-ttu-id="b02ae-205">EnumDateFormatsExA 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-205">EnumDateFormatsExA function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-enumdateformatsexa)
  * [<span data-ttu-id="b02ae-206">EnumDateFormatsExEx 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-206">EnumDateFormatsExEx function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-enumdateformatsexex)
  * [<span data-ttu-id="b02ae-207">EnumDateFormatsExW 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-207">EnumDateFormatsExW function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-enumdateformatsexw)
  * [<span data-ttu-id="b02ae-208">EnumDateFormatsW 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-208">EnumDateFormatsW function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-enumdateformatsw)
  * [<span data-ttu-id="b02ae-209">GetCalendarInfoA 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-209">GetCalendarInfoA function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-getcalendarinfoa)
  * [<span data-ttu-id="b02ae-210">GetCalendarInfoEx 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-210">GetCalendarInfoEx function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-getcalendarinfoex)
  * [<span data-ttu-id="b02ae-211">GetCalendarInfoW 関数</span><span class="sxs-lookup"><span data-stu-id="b02ae-211">GetCalendarInfoW function</span></span>](https://docs.microsoft.com/windows/desktop/api/winnls/nf-winnls-getcalendarinfow)

## <a name="see-also"></a><span data-ttu-id="b02ae-212">関連項目</span><span class="sxs-lookup"><span data-stu-id="b02ae-212">See also</span></span>

* [<span data-ttu-id="b02ae-213">日本語のカレンダーの処理に時代 (年号)。</span><span class="sxs-lookup"><span data-stu-id="b02ae-213">Era Handling for the Japanese Calendar</span></span>](https://docs.microsoft.com/windows/desktop/Intl/era-handling-for-the-japanese-calendar)
* [<span data-ttu-id="b02ae-214">日本語のカレンダーの Y2K 時点</span><span class="sxs-lookup"><span data-stu-id="b02ae-214">The Japanese Calendar’s Y2K Moment</span></span>](https://blogs.msdn.microsoft.com/shawnste/2018/04/12/the-japanese-calendars-y2k-moment/)
* [<span data-ttu-id="b02ae-215">レジストリを使用して、Windows の新しい日本語時代 (年号) をテストするには</span><span class="sxs-lookup"><span data-stu-id="b02ae-215">Using the Registry to Test the New Japanese Era on Windows</span></span>](https://blogs.msdn.microsoft.com/shawnste/2018/08/07/using-the-registry-to-test-the-new-japanese-era-on-windows/)
* [<span data-ttu-id="b02ae-216">元年 vs Ichinen</span><span class="sxs-lookup"><span data-stu-id="b02ae-216">Gannen vs Ichinen</span></span>](https://blogs.msdn.microsoft.com/shawnste/2018/11/12/gannen-vs-ichinen/)
* [<span data-ttu-id="b02ae-217">更新プログラムの可能性があります 2019年日本の時代 (年号) の変更</span><span class="sxs-lookup"><span data-stu-id="b02ae-217">Updates for May 2019 Japan Era Change</span></span>](https://support.microsoft.com/help/4470918/updates-for-may-2019-japan-era-change)
* [<span data-ttu-id="b02ae-218">.NET での日本語のカレンダーで新しい時代 (年号) の処理</span><span class="sxs-lookup"><span data-stu-id="b02ae-218">Handling a new era in the Japanese calendar in .NET</span></span>](https://devblogs.microsoft.com/dotnet/handling-a-new-era-in-the-japanese-calendar-in-net/)
