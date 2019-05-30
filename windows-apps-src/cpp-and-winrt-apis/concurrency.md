---
description: このトピックでは、C++/WinRT を使用した Windows ランタイムの非同期オブジェクトの作成方法と利用方法について説明します。
title: C++/WinRT を使用した同時実行操作と非同期操作
ms.date: 04/24/2019
ms.topic: article
keywords: Windows 10、uwp、標準、c++、cpp、winrt、プロジェクション、同時実行、非同期、非同期、非同期操作
ms.localizationpriority: medium
ms.openlocfilehash: 5dba97ede63b1bcb85c4ee1807d5558f4c93834a
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66361211"
---
# <a name="concurrency-and-asynchronous-operations-with-cwinrt"></a><span data-ttu-id="054da-104">C++/WinRT を使用した同時実行操作と非同期操作</span><span class="sxs-lookup"><span data-stu-id="054da-104">Concurrency and asynchronous operations with C++/WinRT</span></span>

<span data-ttu-id="054da-105">このトピックではどちらもできる方法を作成およびと Windows ランタイムの非同期オブジェクトを使用[C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)します。</span><span class="sxs-lookup"><span data-stu-id="054da-105">This topic shows the ways in which you can both create and consume Windows Runtime asynchronous objects with [C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt).</span></span>

## <a name="asynchronous-operations-and-windows-runtime-async-functions"></a><span data-ttu-id="054da-106">非同期操作と Windows ランタイムの "非同期" 関数</span><span class="sxs-lookup"><span data-stu-id="054da-106">Asynchronous operations and Windows Runtime "Async" functions</span></span>

<span data-ttu-id="054da-107">完了までの時間が 50 ミリ秒を超える可能性がある Windows ランタイム API は、非同期の関数 (末尾が "Async") として実装されます。</span><span class="sxs-lookup"><span data-stu-id="054da-107">Any Windows Runtime API that has the potential to take more than 50 milliseconds to complete is implemented as an asynchronous function (with a name ending in "Async").</span></span> <span data-ttu-id="054da-108">非同期関数を実装すると、別のスレッドの作業が開始され、非同期操作を表すオブジェクトがすぐに返されます。</span><span class="sxs-lookup"><span data-stu-id="054da-108">The implementation of an asynchronous function initiates the work on another thread and returns immediately with an object that represents the asynchronous operation.</span></span> <span data-ttu-id="054da-109">非同期操作が完了すると、作業結果が含まれるオブジェクトが返されます。</span><span class="sxs-lookup"><span data-stu-id="054da-109">When the asynchronous operation completes, that returned object contains any value that resulted from the work.</span></span> <span data-ttu-id="054da-110">**Windows::Foundation** Windows ランタイムの名前空間には 4 種類の非同期操作オブジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="054da-110">The **Windows::Foundation** Windows Runtime namespace contains four types of asynchronous operation object.</span></span>

- <span data-ttu-id="054da-111">[**IAsyncAction**](/uwp/api/windows.foundation.iasyncaction),</span><span class="sxs-lookup"><span data-stu-id="054da-111">[**IAsyncAction**](/uwp/api/windows.foundation.iasyncaction),</span></span>
- <span data-ttu-id="054da-112">[**IAsyncActionWithProgress&lt;TProgress&gt;** ](/uwp/api/windows.foundation.iasyncactionwithprogress_tprogress_)、</span><span class="sxs-lookup"><span data-stu-id="054da-112">[**IAsyncActionWithProgress&lt;TProgress&gt;**](/uwp/api/windows.foundation.iasyncactionwithprogress_tprogress_),</span></span>
- <span data-ttu-id="054da-113">[**IAsyncOperation&lt;TResult&gt;** ](/uwp/api/windows.foundation.iasyncoperation_tresult_)と</span><span class="sxs-lookup"><span data-stu-id="054da-113">[**IAsyncOperation&lt;TResult&gt;**](/uwp/api/windows.foundation.iasyncoperation_tresult_), and</span></span>
- <span data-ttu-id="054da-114">[**IAsyncOperationWithProgress&lt;TResult, TProgress&gt;** ](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_)します。</span><span class="sxs-lookup"><span data-stu-id="054da-114">[**IAsyncOperationWithProgress&lt;TResult, TProgress&gt;**](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_).</span></span>

<span data-ttu-id="054da-115">各非同期操作は、**winrt::Windows::Foundation** C++/WinRT の名前空間で対応する型に投影されます。</span><span class="sxs-lookup"><span data-stu-id="054da-115">Each of these asynchronous operation types is projected into a corresponding type in the **winrt::Windows::Foundation** C++/WinRT namespace.</span></span> <span data-ttu-id="054da-116">また、C++/WinRT には内部 await アダプター構造体も含まれます。</span><span class="sxs-lookup"><span data-stu-id="054da-116">C++/WinRT also contains an internal await adapter struct.</span></span> <span data-ttu-id="054da-117">記述できますを使用しないことを直接が、その構造体に協力してくれた、`co_await`協調的にこれらの非同期操作の種類のいずれかを返す任意の関数の結果を待機するステートメント。</span><span class="sxs-lookup"><span data-stu-id="054da-117">You don't use it directly but, thanks to that struct, you can write a `co_await` statement to cooperatively await the result of any function that returns one of these asychronous operation types.</span></span> <span data-ttu-id="054da-118">その後、これらの型を返す独自のコルーチンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="054da-118">And you can author your own coroutines that return these types.</span></span>

<span data-ttu-id="054da-119">たとえば、非同期の Windows 関数である [**SyndicationClient::RetrieveFeedAsync**](https://docs.microsoft.com/uwp/api/windows.web.syndication.syndicationclient.retrievefeedasync) は、[**IAsyncOperationWithProgress&lt;TResult, TProgress&gt;** ](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_) 型の非同期操作オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="054da-119">An example of an asynchronous Windows function is [**SyndicationClient::RetrieveFeedAsync**](https://docs.microsoft.com/uwp/api/windows.web.syndication.syndicationclient.retrievefeedasync), which returns an asynchronous operation object of type [**IAsyncOperationWithProgress&lt;TResult, TProgress&gt;**](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_).</span></span> <span data-ttu-id="054da-120">いくつかの方法を見てみましょう&mdash;、最初のブロックとし、非ブロッキング&mdash;使用する C +/cli WinRT をなどの API を呼び出す。</span><span class="sxs-lookup"><span data-stu-id="054da-120">Let's look at some ways&mdash;first blocking, and then non-blocking&mdash;of using C++/WinRT to call an API such as that.</span></span>

## <a name="block-the-calling-thread"></a><span data-ttu-id="054da-121">呼び出しスレッドのブロック</span><span class="sxs-lookup"><span data-stu-id="054da-121">Block the calling thread</span></span>

<span data-ttu-id="054da-122">次のコード例では、**RetrieveFeedAsync** から非同期操作オブジェクトを受け取り、非同期操作の結果が利用可能になるまで呼び出しスレッドをブロックするようにこのオブジェクトで **get** を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="054da-122">The code example below receives an asynchronous operation object from **RetrieveFeedAsync**, and it calls **get** on that object to block the calling thread until the results of the asynchronous operation are available.</span></span>

<span data-ttu-id="054da-123">メイン ソース コード ファイルに直接この例をコピー アンド ペーストする場合、 **Windows コンソール アプリケーション (C++/WinRT)** プロジェクト、その最初のセット**プリコンパイル済みヘッダーを使用しない**プロジェクトプロパティ。</span><span class="sxs-lookup"><span data-stu-id="054da-123">If you want to copy-paste this example directly into the main source code file of a **Windows Console Application (C++/WinRT)** project, then first set **Not Using Precompiled Headers** in project properties.</span></span>

```cppwinrt
// main.cpp
#include <winrt/Windows.Foundation.h>
#include <winrt/Windows.Web.Syndication.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace Windows::Web::Syndication;

void ProcessFeed()
{
    Uri rssFeedUri{ L"https://blogs.windows.com/feed" };
    SyndicationClient syndicationClient;
    SyndicationFeed syndicationFeed{ syndicationClient.RetrieveFeedAsync(rssFeedUri).get() };
    // use syndicationFeed.
}

int main()
{
    winrt::init_apartment();
    ProcessFeed();
}
```

<span data-ttu-id="054da-124">**get** を呼び出すとコーディングが簡単になり、何らかの理由でコルーチンを使用しないコンソール アプリやバックグラウンド スレッドに最適です。</span><span class="sxs-lookup"><span data-stu-id="054da-124">Calling **get** makes for convenient coding, and it's ideal for console apps or background threads where you may not want to use a coroutine for whatever reason.</span></span> <span data-ttu-id="054da-125">ただし、同時実行でも非同期でもないため、UI スレッドには適していません (UI スレッドで使用しようとすると、最適化されないビルドでアサーションが発生します)。</span><span class="sxs-lookup"><span data-stu-id="054da-125">But it's not concurrent nor asynchronous, so it's not appropriate for a UI thread (and an assertion will fire in unoptimized builds if you attempt to use it on one).</span></span> <span data-ttu-id="054da-126">OS スレッドの他の有用な作業を妨げないように、さまざまな方法が必要です。</span><span class="sxs-lookup"><span data-stu-id="054da-126">To avoid holding up OS threads from doing other useful work, we need a different technique.</span></span>

## <a name="write-a-coroutine"></a><span data-ttu-id="054da-127">コルーチンの作成</span><span class="sxs-lookup"><span data-stu-id="054da-127">Write a coroutine</span></span>

> [!IMPORTANT]
> <span data-ttu-id="054da-128">としての[ C++WinRT 2.0](news.md#news-and-changes-in-cwinrt-20)、必ず`#include <winrt/coroutine.h>`たびに作成または、コルーチンを使用します。</span><span class="sxs-lookup"><span data-stu-id="054da-128">As of [C++/WinRT 2.0](news.md#news-and-changes-in-cwinrt-20), be sure to `#include <winrt/coroutine.h>` whenever you author or consume a coroutine.</span></span>

<span data-ttu-id="054da-129">C++/WinRT は C++ コルーチンをプログラミング モデルに統合し、結果を連携して待機するための自然な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="054da-129">C++/WinRT integrates C++ coroutines into the programming model to provide a natural way to cooperatively wait for a result.</span></span> <span data-ttu-id="054da-130">コルーチンを作成すると、独自の Windows ランタイム非同期操作を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="054da-130">You can produce your own Windows Runtime asynchronous operation by writing a coroutine.</span></span> <span data-ttu-id="054da-131">次のコード例で、**ProcessFeedAsync** はコルーチンします。</span><span class="sxs-lookup"><span data-stu-id="054da-131">In the code example below, **ProcessFeedAsync** is the coroutine.</span></span>

> [!NOTE]
> <span data-ttu-id="054da-132">**取得**関数が c++ に存在する/cli WinRT プロジェクション型**winrt::Windows::Foundation::IAsyncAction**すべて C + 内から関数を呼び出すことができますので、/cli WinRT プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="054da-132">The **get** function exists on the C++/WinRT projection type **winrt::Windows::Foundation::IAsyncAction**, so you can call the function from within any C++/WinRT project.</span></span> <span data-ttu-id="054da-133">メンバーとして記載されている関数は見つかりません、 [ **IAsyncAction** ](/uwp/api/windows.foundation.iasyncaction)で**取得**アプリケーション バイナリ インターフェイス (ABI) の表面の一部でない、実際の Windows ランタイム型**IAsyncAction**します。</span><span class="sxs-lookup"><span data-stu-id="054da-133">You will not find the function listed as a member of the [**IAsyncAction**](/uwp/api/windows.foundation.iasyncaction) interface, because **get** is not part of the application binary interface (ABI) surface of the actual Windows Runtime type **IAsyncAction**.</span></span>

```cppwinrt
// main.cpp
#include <iostream>
#include <winrt/coroutine.h>
#include <winrt/Windows.Foundation.Collections.h>
#include <winrt/Windows.Web.Syndication.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace Windows::Web::Syndication;

void PrintFeed(SyndicationFeed const& syndicationFeed)
{
    for (SyndicationItem const& syndicationItem : syndicationFeed.Items())
    {
        std::wcout << syndicationItem.Title().Text().c_str() << std::endl;
    }
}

IAsyncAction ProcessFeedAsync()
{
    Uri rssFeedUri{ L"https://blogs.windows.com/feed" };
    SyndicationClient syndicationClient;
    SyndicationFeed syndicationFeed{ co_await syndicationClient.RetrieveFeedAsync(rssFeedUri) };
    PrintFeed(syndicationFeed);
}

int main()
{
    winrt::init_apartment();

    auto processOp{ ProcessFeedAsync() };
    // do other work while the feed is being printed.
    processOp.get(); // no more work to do; call get() so that we see the printout before the application exits.
}
```

<span data-ttu-id="054da-134">コルーチンは中断して再開できる関数です。</span><span class="sxs-lookup"><span data-stu-id="054da-134">A coroutine is a function that can be suspended and resumed.</span></span> <span data-ttu-id="054da-135">上記の **ProcessFeedAsync** コルーチンでは、`co_await` ステートメントに到達すると、コルーチンは **RetrieveFeedAsync** 呼び出しを非同期的に起動してからすぐに自身を中断し、呼び出し元 (上記の例の **main**) に戻ります。</span><span class="sxs-lookup"><span data-stu-id="054da-135">In the **ProcessFeedAsync** coroutine above, when the `co_await` statement is reached, the coroutine asynchronously initiates the **RetrieveFeedAsync** call and then it immediately suspends itself and returns control back to the caller (which is **main** in the example above).</span></span> <span data-ttu-id="054da-136">次に、フィードが取得および印刷されるまで、**main** は作業を続けます。</span><span class="sxs-lookup"><span data-stu-id="054da-136">**main** can then continue to do work while the feed is being retrieved and printed.</span></span> <span data-ttu-id="054da-137">完了すると (**RetrieveFeedAsync** 呼び出しが完了すると)、**ProcessFeedAsync** コルーチンは次のステートメントを再開します。</span><span class="sxs-lookup"><span data-stu-id="054da-137">When that's done (when the **RetrieveFeedAsync** call completes), the **ProcessFeedAsync** coroutine resumes at the next statement.</span></span>

<span data-ttu-id="054da-138">コルーチンは別のコルーチンに集約することができます。</span><span class="sxs-lookup"><span data-stu-id="054da-138">You can aggregate a coroutine into other coroutines.</span></span> <span data-ttu-id="054da-139">または、**get** を呼び出してブロックするか、完了するまで待機します (結果が存在する場合には取得します)。</span><span class="sxs-lookup"><span data-stu-id="054da-139">Or you can call **get** to block and wait for it to complete (and get the result if there is one).</span></span> <span data-ttu-id="054da-140">または、Windows ランタイムをサポートする別のプログラミング言語に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="054da-140">Or you can pass it to another programming language that supports the Windows Runtime.</span></span>

<span data-ttu-id="054da-141">また、デリゲートを使用して、非同期アクションおよび操作の完了イベントと進行状況イベントを処理することもできます。</span><span class="sxs-lookup"><span data-stu-id="054da-141">It's also possible to handle the completed and/or progress events of asynchronous actions and operations by using delegates.</span></span> <span data-ttu-id="054da-142">詳細とコード例については、「[非同期アクションと操作のデリゲート型](handle-events.md#delegate-types-for-asynchronous-actions-and-operations)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="054da-142">For details, and code examples, see [Delegate types for asynchronous actions and operations](handle-events.md#delegate-types-for-asynchronous-actions-and-operations).</span></span>

## <a name="asychronously-return-a-windows-runtime-type"></a><span data-ttu-id="054da-143">Windows ランタイム型を非同期的に返す</span><span class="sxs-lookup"><span data-stu-id="054da-143">Asychronously return a Windows Runtime type</span></span>

<span data-ttu-id="054da-144">次の例では、特定の URI で呼び出しを **RetrieveFeedAsync** にラップして、[**SyndicationFeed**](/uwp/api/windows.web.syndication.syndicationfeed) を非同期的に返す **RetrieveBlogFeedAsync** 関数を示します。</span><span class="sxs-lookup"><span data-stu-id="054da-144">In this next example we wrap a call to **RetrieveFeedAsync**, for a specific URI, to give us a **RetrieveBlogFeedAsync** function that asynchronously returns a [**SyndicationFeed**](/uwp/api/windows.web.syndication.syndicationfeed).</span></span>

```cppwinrt
// main.cpp
#include <iostream>
#include <winrt/coroutine.h>
#include <winrt/Windows.Foundation.Collections.h>
#include <winrt/Windows.Web.Syndication.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace Windows::Web::Syndication;

void PrintFeed(SyndicationFeed const& syndicationFeed)
{
    for (SyndicationItem const& syndicationItem : syndicationFeed.Items())
    {
        std::wcout << syndicationItem.Title().Text().c_str() << std::endl;
    }
}

IAsyncOperationWithProgress<SyndicationFeed, RetrievalProgress> RetrieveBlogFeedAsync()
{
    Uri rssFeedUri{ L"https://blogs.windows.com/feed" };
    SyndicationClient syndicationClient;
    return syndicationClient.RetrieveFeedAsync(rssFeedUri);
}

int main()
{
    winrt::init_apartment();

    auto feedOp{ RetrieveBlogFeedAsync() };
    // do other work.
    PrintFeed(feedOp.get());
}
```

<span data-ttu-id="054da-145">次の例では、**RetrieveBlogFeedAsync** は進捗状況と戻り値の両方が含まれる **IAsyncOperationWithProgress** を返します。</span><span class="sxs-lookup"><span data-stu-id="054da-145">In the example above, **RetrieveBlogFeedAsync** returns an **IAsyncOperationWithProgress**, which has both progress and a return value.</span></span> <span data-ttu-id="054da-146">**RetrieveBlogFeedAsync** が自分の処理を行い、フィードを取得している間は、他の作業を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="054da-146">We can do other work while **RetrieveBlogFeedAsync** is doing its thing and retrieving the feed.</span></span> <span data-ttu-id="054da-147">次に、非同期操作オブジェクトで **get** を呼び出し、ブロックするか完了まで待機して、操作結果を取得します。</span><span class="sxs-lookup"><span data-stu-id="054da-147">Then, we call **get** on that asynchronous operation object to block, wait for it to complete, and then obtain the results of the operation.</span></span>

<span data-ttu-id="054da-148">Windows ランタイム型を非同期的に返す場合は、[**IAsyncOperation&lt;TResult&gt;** ](/uwp/api/windows.foundation.iasyncoperation_tresult_) または [**IAsyncOperationWithProgress&lt;TResult, TProgress&gt;** ](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_) を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="054da-148">If you're asynchronously returning a Windows Runtime type, then you should return an [**IAsyncOperation&lt;TResult&gt;**](/uwp/api/windows.foundation.iasyncoperation_tresult_) or an [**IAsyncOperationWithProgress&lt;TResult, TProgress&gt;**](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_).</span></span> <span data-ttu-id="054da-149">ファースト パーティ製またはサード パーティ製のランタイム クラス、または Windows ランタイム関数との間で受け渡しできる任意の型 (例、`int` または **winrt::hstring**) がこれに適合します。</span><span class="sxs-lookup"><span data-stu-id="054da-149">Any first- or third-party runtime class qualifies, or any type that can be passed to or from a Windows Runtime function (for example, `int`, or **winrt::hstring**).</span></span> <span data-ttu-id="054da-150">コンパイラは、Windows ランタイム型以外でこれらの非同期操作型のいずれかを使用しようとすると表示される "*WinRT 型である必要があります*" というエラーをサポートします。</span><span class="sxs-lookup"><span data-stu-id="054da-150">The compiler will help you with a "*must be WinRT type*" error if you try to use one of these asychronous operation types with a non-Windows Runtime type.</span></span>

<span data-ttu-id="054da-151">コルーチンに 1 つ以上の `co_await` ステートメントがない場合、コルーチンであると認められるために、1 つ以上の `co_return` または 1 つの `co_yield` ステートメントが必要です。</span><span class="sxs-lookup"><span data-stu-id="054da-151">If a coroutine doesn't have at least one `co_await` statement then, in order to qualify as a coroutine, it must have at least one `co_return` or one `co_yield` statement.</span></span> <span data-ttu-id="054da-152">非同期操作を必要とせず、そのためにコンテキストのブロックや切り替えを行わずに、コルーチンが値を返すことができる場合があります。</span><span class="sxs-lookup"><span data-stu-id="054da-152">There will be cases where your coroutine can return a value without introducing any asynchrony, and therefore without blocking nor switching context.</span></span> <span data-ttu-id="054da-153">値をキャッシュすることでそれを行う例を次に示します (2 回目以降は呼び出されます)。</span><span class="sxs-lookup"><span data-stu-id="054da-153">Here's an example that does that (the second and subsequent times it's called) by caching a value.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
winrt::hstring m_cache;

IAsyncOperation<winrt::hstring> ReadAsync()
{
    if (m_cache.empty())
    {
        // Asynchronously download and cache the string.
    }
    co_return m_cache;
}
``` 

## <a name="asychronously-return-a-non-windows-runtime-type"></a><span data-ttu-id="054da-154">Windows ランタイム型以外を非同期的に返す</span><span class="sxs-lookup"><span data-stu-id="054da-154">Asychronously return a non-Windows-Runtime type</span></span>

<span data-ttu-id="054da-155">Windows ランタイム型*以外*の型を非同期的に返す場合は、並列パターン ライブラリ (PPL) [**concurrency::task**](/cpp/parallel/concrt/reference/task-class) を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="054da-155">If you're asynchronously returning a type that's *not* a Windows Runtime type, then you should return a Parallel Patterns Library (PPL) [**concurrency::task**](/cpp/parallel/concrt/reference/task-class).</span></span> <span data-ttu-id="054da-156">**std::future**よりもパフォーマンスに優れているため (また、今後の互換性の向上により)、**concurrency::task** をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="054da-156">We recommend **concurrency::task** because it gives you better performance (and better compatibility going forward) than **std::future** does.</span></span>

> [!TIP]
> <span data-ttu-id="054da-157">`<pplawait.h>` を含めると、コルーチンの型として **concurrency::task** を使用できます。</span><span class="sxs-lookup"><span data-stu-id="054da-157">If you include `<pplawait.h>`, then you can use **concurrency::task** as a coroutine type.</span></span>

```cppwinrt
// main.cpp
#include <iostream>
#include <ppltasks.h>
#include <winrt/Windows.Foundation.Collections.h>
#include <winrt/Windows.Web.Syndication.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace Windows::Web::Syndication;

concurrency::task<std::wstring> RetrieveFirstTitleAsync()
{
    return concurrency::create_task([]
        {
            Uri rssFeedUri{ L"https://blogs.windows.com/feed" };
            SyndicationClient syndicationClient;
            SyndicationFeed syndicationFeed{ syndicationClient.RetrieveFeedAsync(rssFeedUri).get() };
            return std::wstring{ syndicationFeed.Items().GetAt(0).Title().Text() };
        });
}

int main()
{
    winrt::init_apartment();

    auto firstTitleOp{ RetrieveFirstTitleAsync() };
    // Do other work here.
    std::wcout << firstTitleOp.get() << std::endl;
}
```

## <a name="parameter-passing"></a><span data-ttu-id="054da-158">パラメーターの引き渡し</span><span class="sxs-lookup"><span data-stu-id="054da-158">Parameter-passing</span></span>

<span data-ttu-id="054da-159">同期関数では、既定で `const&` パラメーターを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="054da-159">For synchronous functions, you should use `const&` parameters by default.</span></span> <span data-ttu-id="054da-160">これにより、コピーのオーバーヘッドが回避されます (参照カウント、つまりインタロックされたインクリメントとデクリメントが含まれます)。</span><span class="sxs-lookup"><span data-stu-id="054da-160">That will avoid the overhead of copies (which involve reference counting, and that means interlocked increments and decrements).</span></span>

```cppwinrt
// Synchronous function.
void DoWork(Param const& value);
```

<span data-ttu-id="054da-161">ただし、コルーチンに参照パラメーターを渡した場合、問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="054da-161">But you can run into problems if you pass a reference parameter to a coroutine.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
// NOT the recommended way to pass a value to a coroutine!
IASyncAction DoWorkAsync(Param const& value)
{
    // While it's ok to access value here...

    co_await DoOtherWorkAsync();

    // ...accessing value here carries no guarantees of safety.
}
```

<span data-ttu-id="054da-162">コルーチンでは、最初の一時停止ポイントまで実行は同期であり、ここでは、コントロールは呼び出し元に返されます。</span><span class="sxs-lookup"><span data-stu-id="054da-162">In a coroutine, execution is synchronous up until the first suspension point, where control is returned to the caller.</span></span> <span data-ttu-id="054da-163">コルーチンが再開するまで、参照パラメーターが参照するソース値に何かが発生している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="054da-163">By the time the coroutine resumes, anything might have happened to the source value that a reference parameter references.</span></span> <span data-ttu-id="054da-164">コルーチンの観点からは、参照パラメーターには管理されていない有効期間があります。</span><span class="sxs-lookup"><span data-stu-id="054da-164">From the coroutine's perspective, a reference parameter has uncontrolled lifetime.</span></span> <span data-ttu-id="054da-165">そのため、上記の例では、`co_await` まで*値*に安全にアクセスできますが、それ以降は安全ではありません。</span><span class="sxs-lookup"><span data-stu-id="054da-165">So, in the example above, we're safe to access *value* up until the `co_await`, but not after it.</span></span> <span data-ttu-id="054da-166">また、その後その関数が中断し、再開した後で*値*を使用しようとするリスクがある場合、**DoOtherWorkAsync** に安全に*値*を渡すこともできません。</span><span class="sxs-lookup"><span data-stu-id="054da-166">Nor can we safely pass *value* to **DoOtherWorkAsync** if there's any risk that that function will in turn suspend and then try to use *value* after it resumes.</span></span> <span data-ttu-id="054da-167">中断して再開した後で、パラメーターを安全に使用できるようにするには、コルーチンは既定で値渡しを使用し、値でキャプチャして有効期間の問題を回避できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="054da-167">To make parameters safe to use after suspending and resuming, your coroutines should use pass-by-value by default to ensure that they capture by value and avoid lifetime issues.</span></span> <span data-ttu-id="054da-168">それを行うことが安全であると確信できるためにそのガイダンスから逸脱できる場合は稀です。</span><span class="sxs-lookup"><span data-stu-id="054da-168">Cases when you can deviate from that guidance because you're certain that it's safe to do so are going to be rare.</span></span>

```cppwinrt
// Coroutine
IASyncAction DoWorkAsync(Param value);
```

<span data-ttu-id="054da-169">(値を移動しない限り) 定数値を渡すことが良い方法であるということにも議論の余地があります。</span><span class="sxs-lookup"><span data-stu-id="054da-169">It's also arguable that (unless you want to move the value) passing by const value is good practice.</span></span> <span data-ttu-id="054da-170">コピー元のソース値に影響はありませんが、意図が明確になり、誤ってコピーを変更した場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="054da-170">It won't have any effect on the source value from which you're making a copy, but it makes the intent clear, and helps if you inadvertently modify the copy.</span></span>

```cppwinrt
// coroutine with strictly unnecessary const (but arguably good practice).
IASyncAction DoWorkAsync(Param const value);
```

<span data-ttu-id="054da-171">非同期の呼び出し先に標準ベクターを渡す方法について説明した「[標準的な配列とベクトル](std-cpp-data-types.md#standard-arrays-and-vectors)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="054da-171">Also see [Standard arrays and vectors](std-cpp-data-types.md#standard-arrays-and-vectors), which deals with how to pass a standard vector into an asynchronous callee.</span></span>

## <a name="offloading-work-onto-the-windows-thread-pool"></a><span data-ttu-id="054da-172">Windows スレッド プールへの処理のオフロード</span><span class="sxs-lookup"><span data-stu-id="054da-172">Offloading work onto the Windows thread pool</span></span>

<span data-ttu-id="054da-173">コルーチンは、関数に実行を返すまで、呼び出し元がブロックされていることなどの他の機能です。</span><span class="sxs-lookup"><span data-stu-id="054da-173">A coroutine is a function like any other in that a caller is blocked until a function returns execution to it.</span></span> <span data-ttu-id="054da-174">返すコルーチンの最初のチャンスが 1 つ目とは、 `co_await`、 `co_return`、または`co_yield`します。</span><span class="sxs-lookup"><span data-stu-id="054da-174">And, the first opportunity for a coroutine to return is the first `co_await`, `co_return`, or `co_yield`.</span></span>

<span data-ttu-id="054da-175">そのため、実行する前にコルーチンでの作業を計算主体、実行を返す、呼び出し元にする必要があります (つまり、中断ポイントを導入する) 呼び出し元がブロックされないようにします。</span><span class="sxs-lookup"><span data-stu-id="054da-175">So, before you do compute-bound work in a coroutine, you need to return execution to the caller (in other words, introduce a suspension point) so that the caller isn't blocked.</span></span> <span data-ttu-id="054da-176">をまだ行っている場合`co_await`- その他のいくつか操作してかまいません ing `co_await` 、 [ **winrt::resume_background** ](/uwp/cpp-ref-for-winrt/resume-background)関数。</span><span class="sxs-lookup"><span data-stu-id="054da-176">If you're not already doing that by `co_await`-ing some other operation, then you can `co_await` the [**winrt::resume_background**](/uwp/cpp-ref-for-winrt/resume-background) function.</span></span> <span data-ttu-id="054da-177">これにより、呼び出し元に制御が返され、スレッド プールのスレッドですぐに実行が再開されます。</span><span class="sxs-lookup"><span data-stu-id="054da-177">That returns control to the caller, and then immediately resumes execution on a thread pool thread.</span></span>

<span data-ttu-id="054da-178">実装で使用されているスレッド プールは低レベルの [Windows スレッド プール](https://docs.microsoft.com/windows/desktop/ProcThread/thread-pool-api)であるため、最適に効率化されます。</span><span class="sxs-lookup"><span data-stu-id="054da-178">The thread pool being used in the implementation is the low-level [Windows thread pool](https://docs.microsoft.com/windows/desktop/ProcThread/thread-pool-api), so it's optimially efficient.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncOperation<uint32_t> DoWorkOnThreadPoolAsync()
{
    co_await winrt::resume_background(); // Return control; resume on thread pool.

    uint32_t result;
    for (uint32_t y = 0; y < height; ++y)
    for (uint32_t x = 0; x < width; ++x)
    {
        // Do compute-bound work here.
    }
    co_return result;
}
```

## <a name="programming-with-thread-affinity-in-mind"></a><span data-ttu-id="054da-179">スレッドの関係を考慮したプログラミング</span><span class="sxs-lookup"><span data-stu-id="054da-179">Programming with thread affinity in mind</span></span>

<span data-ttu-id="054da-180">このシナリオは、前のシナリオをさらに詳しく説明しています。</span><span class="sxs-lookup"><span data-stu-id="054da-180">This scenario expands on the previous one.</span></span> <span data-ttu-id="054da-181">一部の処理をスレッド プールにオフロードするが、ユーザー インターフェイス (UI) で進行状況を表示したいとします。</span><span class="sxs-lookup"><span data-stu-id="054da-181">You offload some work onto the thread pool, but then you want to display progress in the user interface (UI).</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction DoWorkAsync(TextBlock textblock)
{
    co_await winrt::resume_background();
    // Do compute-bound work here.

    textblock.Text(L"Done!"); // Error: TextBlock has thread affinity.
}
```

<span data-ttu-id="054da-182">上のコードは、[**winrt::hresult_wrong_thread**](/uwp/cpp-ref-for-winrt/error-handling/hresult-wrong-thread) 例外をスローします。これは、**TextBlock** がそれを作成したスレッド (UI スレッド) から更新する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="054da-182">The code above throws a [**winrt::hresult_wrong_thread**](/uwp/cpp-ref-for-winrt/error-handling/hresult-wrong-thread) exception, because a **TextBlock** must be updated from the thread that created it, which is the UI thread.</span></span> <span data-ttu-id="054da-183">1 つの解決方法は、コルーチンが最初に呼び出されたスレッド コンテキストをキャプチャする方法です。</span><span class="sxs-lookup"><span data-stu-id="054da-183">One solution is to capture the thread context within which our coroutine was originally called.</span></span> <span data-ttu-id="054da-184">インスタンス化、 [ **winrt::apartment_context** ](/uwp/cpp-ref-for-winrt/apartment-context)オブジェクト、バック グラウンド作業をし`co_await`、 **apartment_context**呼び出し元に戻すコンテキスト。</span><span class="sxs-lookup"><span data-stu-id="054da-184">To do that, instantiate a [**winrt::apartment_context**](/uwp/cpp-ref-for-winrt/apartment-context) object, do background work, and then `co_await` the **apartment_context** to switch back to the calling context.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction DoWorkAsync(TextBlock textblock)
{
    winrt::apartment_context ui_thread; // Capture calling context.

    co_await winrt::resume_background();
    // Do compute-bound work here.

    co_await ui_thread; // Switch back to calling context.

    textblock.Text(L"Done!"); // Ok if we really were called from the UI thread.
}
```

<span data-ttu-id="054da-185">上のコルーチンが **TextBlock** を作成した UI スレッドから呼び出される限り、この手法は機能します。</span><span class="sxs-lookup"><span data-stu-id="054da-185">As long as the coroutine above is called from the UI thread that created the **TextBlock**, then this technique works.</span></span> <span data-ttu-id="054da-186">アプリで多くの場合にそれを確信できます。</span><span class="sxs-lookup"><span data-stu-id="054da-186">There will be many cases in your app where you're certain of that.</span></span>

<span data-ttu-id="054da-187">一般的なソリューションは、呼び出し元のスレッドが不明確していない場合を対象とする、UI を更新することができます`co_await`、 [ **winrt::resume_foreground** ](/uwp/cpp-ref-for-winrt/resume-foreground)スイッチを特定する関数フォア グラウンド スレッドです。</span><span class="sxs-lookup"><span data-stu-id="054da-187">For a more general solution to updating UI, which covers cases where you're uncertain about the calling thread, you can `co_await` the [**winrt::resume_foreground**](/uwp/cpp-ref-for-winrt/resume-foreground) function to switch to a specific foreground thread.</span></span> <span data-ttu-id="054da-188">次のコード例では、([**Dispatcher**](/uwp/api/windows.ui.xaml.dependencyobject.dispatcher#Windows_UI_Xaml_DependencyObject_Dispatcher) プロパティにアクセスして) **TextBlock** に関連するディスパッチャー オブジェクトを渡すことでフォアグラウンド スレッドを指定しています。</span><span class="sxs-lookup"><span data-stu-id="054da-188">In the code example below, we specify the foreground thread by passing the dispatcher object associated with the **TextBlock** (by accessing its [**Dispatcher**](/uwp/api/windows.ui.xaml.dependencyobject.dispatcher#Windows_UI_Xaml_DependencyObject_Dispatcher) property).</span></span> <span data-ttu-id="054da-189">**winrt::resume_foreground** の実装では、そのディスパッチャー オブジェクトで [**CoreDispatcher.RunAsync**](/uwp/api/windows.ui.core.coredispatcher.runasync) を呼び出し、コルーチンでその後に続く処理を実行しています。</span><span class="sxs-lookup"><span data-stu-id="054da-189">The implementation of **winrt::resume_foreground** calls [**CoreDispatcher.RunAsync**](/uwp/api/windows.ui.core.coredispatcher.runasync) on that dispatcher object to execute the work that comes after it in the coroutine.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction DoWorkAsync(TextBlock textblock)
{
    co_await winrt::resume_background();
    // Do compute-bound work here.

    co_await winrt::resume_foreground(textblock.Dispatcher()); // Switch to the foreground thread associated with textblock.

    textblock.Text(L"Done!"); // Guaranteed to work.
}
```

## <a name="execution-contexts-resuming-and-switching-in-a-coroutine"></a><span data-ttu-id="054da-190">実行コンテキスト、再開、およびコルーチンでの切り替え</span><span class="sxs-lookup"><span data-stu-id="054da-190">Execution contexts, resuming, and switching in a coroutine</span></span>

<span data-ttu-id="054da-191">大まかに言えば、コルーチンでの中断ポイントした後、元のスレッドの実行の終了してもよいし、再開に任意のスレッドで発生する可能性があります (つまり、任意のスレッドを呼び出すことができます、**完了**非同期操作のメソッド)。</span><span class="sxs-lookup"><span data-stu-id="054da-191">Broadly speaking, after a suspension point in a coroutine, the original thread of execution may go away and resumption may occur on any thread (in other words, any thread may call the **Completed** method for the async operation).</span></span>

<span data-ttu-id="054da-192">場合する`co_await`4 つの Windows ランタイムの非同期操作の種類のいずれか (**IAsyncXxx**)、し、C++/cli WinRT はポイントで呼び出し元のコンテキストをキャプチャする`co_await`します。</span><span class="sxs-lookup"><span data-stu-id="054da-192">But if you `co_await` any of the four Windows Runtime asynchronous operation types (**IAsyncXxx**), then C++/WinRT captures the calling context at the point you `co_await`.</span></span> <span data-ttu-id="054da-193">および継続タスクを再開したとき、そのコンテキストにまだ残っていることになります。</span><span class="sxs-lookup"><span data-stu-id="054da-193">And it ensures that you're still on that context when the continuation resumes.</span></span> <span data-ttu-id="054da-194">C +/cli WinRT は呼び出し元のコンテキストに既にいるかどうかをチェックし、そうでない場合は、これに切り替えることによって。</span><span class="sxs-lookup"><span data-stu-id="054da-194">C++/WinRT does this by checking whether you're already on the calling context and, if not, switching to it.</span></span> <span data-ttu-id="054da-195">したかどうかは、前に、シングル スレッド アパートメント (STA) スレッドで`co_await`、ことと同じものに後で; したかどうかは、前に、マルチ スレッド アパートメント (MTA) スレッドで`co_await`、後でいずれかにあります。</span><span class="sxs-lookup"><span data-stu-id="054da-195">If you were on a single-threaded apartment (STA) thread before `co_await`, then you'll be on the same one afterward; if you were on a multi-threaded apartment (MTA) thread before `co_await`, then you'll be on one afterward.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction ProcessFeedAsync()
{
    Uri rssFeedUri{ L"https://blogs.windows.com/feed" };
    SyndicationClient syndicationClient;

    // The thread context at this point is captured...
    SyndicationFeed syndicationFeed{ co_await syndicationClient.RetrieveFeedAsync(rssFeedUri) };
    // ...and is restored at this point.
}
```

<span data-ttu-id="054da-196">この動作に依存できる理由は、ためには C +/cli WinRT C++ コルーチンの言語サポート (これらのコードは待機のアダプターで呼ばれます) に、Windows ランタイム非同期操作の種類を調整するためのコードを提供します。</span><span class="sxs-lookup"><span data-stu-id="054da-196">The reason you can rely on this behavior is because C++/WinRT provides code to adapt those Windows Runtime asynchronous operation types to the C++ coroutine language support (these pieces of code are called wait adapters).</span></span> <span data-ttu-id="054da-197">残りの待機可能な型に C +/cli WinRT はスレッド プール ラッパーやヘルパー。そのため、スレッド プールで完了します。</span><span class="sxs-lookup"><span data-stu-id="054da-197">The remaining awaitable types in C++/WinRT are simply thread pool wrappers and/or helpers; so they complete on the thread pool.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
using namespace std::chrono;
IAsyncOperation<int> return_123_after_5s()
{
    // No matter what the thread context is at this point...
    co_await 5s;
    // ...we're on the thread pool at this point.
    co_return 123;
}
```

<span data-ttu-id="054da-198">場合する`co_await`他の何らかの種類&mdash;C + 内でも/cli WinRT コルーチンの実装&mdash;別のライブラリは、アダプターを提供し、再開とコンテキストの観点からこれらのアダプターが行う操作を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="054da-198">If you `co_await` some other type&mdash;even within a C++/WinRT coroutine implementation&mdash;then another library provides the adapters, and you'll need to understand what those adapters do in terms of resumption and contexts.</span></span>

<span data-ttu-id="054da-199">コンテキストの切り替えを最小値までを保持するには、このトピックで前述したよう手法の一部を使用できます。</span><span class="sxs-lookup"><span data-stu-id="054da-199">To keep context switches down to a minimum, you can use some of the techniques that we've already seen in this topic.</span></span> <span data-ttu-id="054da-200">これを行うのいくつかの図を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="054da-200">Let's see some illustrations of doing that.</span></span> <span data-ttu-id="054da-201">この次の擬似コードの例では、イベント ハンドラー、イメージを読み込むための Windows ランタイム API を呼び出すし、そのイメージを処理するバック グラウンド スレッドにドロップし、UI でイメージを表示する UI スレッドに戻りますのアウトラインを説明します。</span><span class="sxs-lookup"><span data-stu-id="054da-201">In this next pseudo-code example, we show the outline of an event handler that calls a Windows Runtime API to load an image, drops onto a background thread to process that image, and then returns to the UI thread to display the image in the UI.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction MainPage::ClickHandler(IInspectable /* sender */, RoutedEventArgs /* args */)
{
    // We begin in the UI context.

    // Call StorageFile::OpenAsync to load an image file.

    // The call to OpenAsync occurred on a background thread, but C++/WinRT has restored us to the UI thread by this point.

    co_await winrt::resume_background();

    // We're now on a background thread.

    // Process the image.

    co_await winrt::resume_foreground(this->Dispatcher());

    // We're back on MainPage's UI thread.

    // Display the image in the UI.
}
```

<span data-ttu-id="054da-202">このシナリオでは、少し呼び出しの周囲の ineffiency **StorageFile::OpenAsync**します。</span><span class="sxs-lookup"><span data-stu-id="054da-202">For this scenario, there's a little bit of ineffiency around the call to **StorageFile::OpenAsync**.</span></span> <span data-ttu-id="054da-203">背景に必要なコンテキスト スイッチがある (そのハンドラーは、実行を呼び出し元に戻すことができる) スレッド、再開後にどの C +/cli WinRT が UI スレッドのコンテキストを復元します。</span><span class="sxs-lookup"><span data-stu-id="054da-203">There's a necessary context switch to a background thread (so that the handler can return execution to the caller), on resumption after which C++/WinRT restores the UI thread context.</span></span> <span data-ttu-id="054da-204">しかし、ここでは、UI を更新しようとしていることになるまで、UI スレッド上に存在する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="054da-204">But, in this case, it's not necessary to be on the UI thread until we're about to update the UI.</span></span> <span data-ttu-id="054da-205">いわゆる複数の Windows ランタイム Api*する前に*への呼び出しを**winrt::resume_background**より不要な - 前後のコンテキスト スイッチが発生しています。</span><span class="sxs-lookup"><span data-stu-id="054da-205">The more Windows Runtime APIs we call *before* our call to **winrt::resume_background**, the more unnecessary back-and-forth context switches we incur.</span></span> <span data-ttu-id="054da-206">ソリューションは呼び出す*任意*その前に、Windows ランタイム Api です。</span><span class="sxs-lookup"><span data-stu-id="054da-206">The solution is not to call *any* Windows Runtime APIs before then.</span></span> <span data-ttu-id="054da-207">すべての後に移動、 **winrt::resume_background**します。</span><span class="sxs-lookup"><span data-stu-id="054da-207">Move them all after the **winrt::resume_background**.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction MainPage::ClickHandler(IInspectable /* sender */, RoutedEventArgs /* args */)
{
    // We begin in the UI context.

    co_await winrt::resume_background();

    // We're now on a background thread.

    // Call StorageFile::OpenAsync to load an image file.

    // Process the image.

    co_await winrt::resume_foreground(this->Dispatcher());

    // We're back on MainPage's UI thread.

    // Display the image in the UI.
}
```

<span data-ttu-id="054da-208">独自に記述する可能性がありより高度なものを行いたい場合は、アダプターを待機します。</span><span class="sxs-lookup"><span data-stu-id="054da-208">If you want to do something more advanced, then you could write your own await adapters.</span></span> <span data-ttu-id="054da-209">たい場合など、`co_await`で非同期操作が完了するのと同じスレッドで再開する (そのためがないコンテキストの切り替え) を記述して開始する可能性がありますし、await の次に示すようなアダプター。</span><span class="sxs-lookup"><span data-stu-id="054da-209">For example, if you want a `co_await` to resume on the same thread that the async action completes on (so, there's no context switch), then you could begin by writing await adapters similar to the ones shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="054da-210">教育目的のみで、次のコード例が提供されます。作業を開始するのには理解がどのアダプターの連携を待機します。</span><span class="sxs-lookup"><span data-stu-id="054da-210">The code example below is provided for educational purposes only; it's to get you started understanding how await adapters work.</span></span> <span data-ttu-id="054da-211">開発および、独自にテストすることをお勧めし、独自のコードベースでは、この手法を使用する場合は、アダプター struct(s) を待機します。</span><span class="sxs-lookup"><span data-stu-id="054da-211">If you want to use this technique in your own codebase, then we recommend that you develop and test your own await adapter struct(s).</span></span> <span data-ttu-id="054da-212">たとえば、作成する**complete_on_any**、 **complete_on_current**、および**complete_on(dispatcher)** します。</span><span class="sxs-lookup"><span data-stu-id="054da-212">For example, you could write **complete_on_any**, **complete_on_current**, and **complete_on(dispatcher)**.</span></span> <span data-ttu-id="054da-213">受け取るテンプレートにすることも検討、 **IAsyncXxx**型テンプレート パラメーターとして。</span><span class="sxs-lookup"><span data-stu-id="054da-213">Also consider making them templates that take the **IAsyncXxx** type as a template parameter.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
struct no_switch
{
    no_switch(Windows::Foundation::IAsyncAction const& async) : m_async(async)
    {
    }

    bool await_ready() const
    {
        return m_async.Status() == Windows::Foundation::AsyncStatus::Completed;
    }

    void await_suspend(std::experimental::coroutine_handle<> handle) const
    {
        m_async.Completed([handle](Windows::Foundation::IAsyncAction const& /* asyncInfo */, Windows::Foundation::AsyncStatus const& /* asyncStatus */)
        {
            handle();
        });
    }

    auto await_resume() const
    {
        return m_async.GetResults();
    }

private:
    Windows::Foundation::IAsyncAction const& m_async;
};
```

<span data-ttu-id="054da-214">使用する方法を理解する、**切り替え**await アダプター、することを確認する必要がありますのではまず、C++コンパイラが検出、`co_await`呼び出された関数が検索式**await_ready**、**await_suspend**、および**await_resume**します。</span><span class="sxs-lookup"><span data-stu-id="054da-214">To understand how to use the **no_switch** await adapters, you'll first need to know that when the C++ compiler encounters a `co_await` expression it looks for functions called **await_ready**, **await_suspend**, and **await_resume**.</span></span> <span data-ttu-id="054da-215">C++/cli WinRT ライブラリは、既定では、このような適切な動作を取得するためにこれらの関数を提供します。</span><span class="sxs-lookup"><span data-stu-id="054da-215">The C++/WinRT library provides those functions so that you get reasonable behavior by default, like this.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction async{ ProcessFeedAsync() };
co_await async;
```

<span data-ttu-id="054da-216">使用する、**切り替え**await アダプター、その型を変更するだけ`co_await`から式**IAsyncXxx**に**切り替え**、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="054da-216">To use the **no_switch** await adapters, just change the type of that `co_await` expression from **IAsyncXxx** to **no_switch**, like this.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction async{ ProcessFeedAsync() };
co_await static_cast<no_switch>(async);
```

<span data-ttu-id="054da-217">次の 3 つの検索ではなく、 **await_xxx**関数と一致する**IAsyncXxx**、C++コンパイラと一致する関数を探します**切り替え**します。</span><span class="sxs-lookup"><span data-stu-id="054da-217">Then, instead of looking for the three **await_xxx** functions that match **IAsyncXxx**, the C++ compiler looks for functions that match **no_switch**.</span></span>

## <a name="canceling-an-asychronous-operation-and-cancellation-callbacks"></a><span data-ttu-id="054da-218">非同期操作、および取り消しのコールバックをキャンセル</span><span class="sxs-lookup"><span data-stu-id="054da-218">Canceling an asychronous operation, and cancellation callbacks</span></span>

<span data-ttu-id="054da-219">非同期プログラミング向けの Windows ランタイムの機能を使用すると、実行中の非同期アクションまたは操作をキャンセルできます。</span><span class="sxs-lookup"><span data-stu-id="054da-219">The Windows Runtime's features for asynchronous programming allow you to cancel an in-flight asynchronous action or operation.</span></span> <span data-ttu-id="054da-220">呼び出す例を次に示します[ **StorageFolder::GetFilesAsync** ](/uwp/api/windows.storage.storagefolder.getfilesasync)が大きくなる可能性、ファイルのコレクションを取得するには、データ メンバーの非同期操作の結果のオブジェクトを格納します。</span><span class="sxs-lookup"><span data-stu-id="054da-220">Here's an example that calls [**StorageFolder::GetFilesAsync**](/uwp/api/windows.storage.storagefolder.getfilesasync) to retrieve a potentially large collection of files, and it stores the resulting asynchronous operation object in a data member.</span></span> <span data-ttu-id="054da-221">ユーザーには、操作をキャンセルするオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="054da-221">The user has the option to cancel the operation.</span></span>

```cppwinrt
// MainPage.xaml
...
<Button x:Name="workButton" Click="OnWork">Work</Button>
<Button x:Name="cancelButton" Click="OnCancel">Cancel</Button>
...

// MainPage.h
...
#include <winrt/coroutine.h>
#include <winrt/Windows.Foundation.Collections.h>
#include <winrt/Windows.Storage.Search.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace Windows::Foundation::Collections;
using namespace Windows::Storage;
using namespace Windows::Storage::Search;
using namespace Windows::UI::Xaml;
...
struct MainPage : MainPageT<MainPage>
{
    MainPage()
    {
        InitializeComponent();
    }

    IAsyncAction OnWork(IInspectable /* sender */, RoutedEventArgs /* args */)
    {
        workButton().Content(winrt::box_value(L"Working..."));

        // Enable the Pictures Library capability in the app manifest file.
        StorageFolder picturesLibrary{ KnownFolders::PicturesLibrary() };

        m_async = picturesLibrary.GetFilesAsync(CommonFileQuery::OrderByDate, 0, 1000);

        IVectorView<StorageFile> filesInFolder{ co_await m_async };

        workButton().Content(box_value(L"Done!"));

        // Process the files in some way.
    }

    void OnCancel(IInspectable const& /* sender */, RoutedEventArgs const& /* args */)
    {
        if (m_async.Status() != AsyncStatus::Completed)
        {
            m_async.Cancel();
            workButton().Content(winrt::box_value(L"Canceled"));
        }
    }

private:
    IAsyncOperation<::IVectorView<StorageFile>> m_async;
};
...
```

<span data-ttu-id="054da-222">キャンセルの実装側では、簡単な例から始めましょう。</span><span class="sxs-lookup"><span data-stu-id="054da-222">For the implementation side of cancellation, let's begin with a simple example.</span></span>

```cppwinrt
// main.cpp
#include <iostream>
#include <winrt/coroutine.h>
#include <winrt/Windows.Foundation.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace std::chrono_literals;

IAsyncAction ImplicitCancellationAsync()
{
    while (true)
    {
        std::cout << "ImplicitCancellationAsync: do some work for 1 second" << std::endl;
        co_await 1s;
    }
}

IAsyncAction MainCoroutineAsync()
{
    auto implicit_cancellation{ ImplicitCancellationAsync() };
    co_await 3s;
    implicit_cancellation.Cancel();
}

int main()
{
    winrt::init_apartment();
    MainCoroutineAsync().get();
}
```

<span data-ttu-id="054da-223">上記の例を実行するかどうかは、表示**ImplicitCancellationAsync** 3 秒間、その後に自動的に終了しますその結果れるキャンセルの 1 秒あたりの 1 つのメッセージを出力します。</span><span class="sxs-lookup"><span data-stu-id="054da-223">If you run the example above, then you'll see **ImplicitCancellationAsync** print one message per second for three seconds, after which time it automatically terminates as a result of being canceled.</span></span> <span data-ttu-id="054da-224">発生したため、これは、機能、`co_await`が取り消されましたかどうか、式、コルーチンを確認します。</span><span class="sxs-lookup"><span data-stu-id="054da-224">This works because, on encountering a `co_await` expression, a coroutine checks whether it has been cancelled.</span></span> <span data-ttu-id="054da-225">場合は、し、それを実行せずにアウトしてください。これに該当しない場合は、これを中断し、通常どおりです。</span><span class="sxs-lookup"><span data-stu-id="054da-225">If it has, then it short-circuits out; and if it hasn't, then it suspends as normal.</span></span>

<span data-ttu-id="054da-226">キャンセルは、コルーチンを中断している間、発生します。</span><span class="sxs-lookup"><span data-stu-id="054da-226">Cancellation can, of course, happen while the coroutine is suspended.</span></span> <span data-ttu-id="054da-227">コルーチンの再開時にのみヒット別または`co_await`、これは取り消し状態をチェックします。</span><span class="sxs-lookup"><span data-stu-id="054da-227">Only when the coroutine resumes, or hits another `co_await`, will it check for cancellation.</span></span> <span data-ttu-id="054da-228">問題では、キャンセルに応答する可能性のあるすぎる粗い-詳細の待機時間の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="054da-228">The issue is one of potentially too-coarse-grained latency in responding to cancellation.</span></span>

<span data-ttu-id="054da-229">そのため、別のオプションは、コルーチン内からのキャンセルを明示的にポーリングします。</span><span class="sxs-lookup"><span data-stu-id="054da-229">So, another option is to explicitly poll for cancellation from within your coroutine.</span></span> <span data-ttu-id="054da-230">以下のリスト内のコードでは、上記の例を更新します。</span><span class="sxs-lookup"><span data-stu-id="054da-230">Update the example above with the code in the listing below.</span></span> <span data-ttu-id="054da-231">この新しい例では**ExplicitCancellationAsync**によって返されるオブジェクトを取得、 [ **winrt::get_cancellation_token** ](/uwp/cpp-ref-for-winrt/get-cancellation-token)関数は、オブジェクトを定期的に使用してコルーチンが取り消されたかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="054da-231">In this new example, **ExplicitCancellationAsync** retrieves the object returned by the [**winrt::get_cancellation_token**](/uwp/cpp-ref-for-winrt/get-cancellation-token) function, and uses it to periodically check whether the coroutine has been canceled.</span></span> <span data-ttu-id="054da-232">コルーチンが無制限にループ処理が取り消されない限り、キャンセルすると、ループ、関数は、通常どおりに終了します。</span><span class="sxs-lookup"><span data-stu-id="054da-232">As long as it's not canceled, the coroutine loops indefinitely; once it is canceled, the loop and the function exit normally.</span></span> <span data-ttu-id="054da-233">結果は、ここで終了するが、前の例では、明示的が行われるため、管理下にある同じです。</span><span class="sxs-lookup"><span data-stu-id="054da-233">The outcome is the same as the previous example, but here exiting happens explicitly, and under control.</span></span>

```cppwinrt
...
#include <winrt/coroutine.h>
...
IAsyncAction ExplicitCancellationAsync()
{
    auto cancellation_token{ co_await winrt::get_cancellation_token() };

    while (!cancellation_token())
    {
        std::cout << "ExplicitCancellationAsync: do some work for 1 second" << std::endl;
        co_await 1s;
    }
}

IAsyncAction MainCoroutineAsync()
{
    auto explicit_cancellation{ ExplicitCancellationAsync() };
    co_await 3s;
    explicit_cancellation.Cancel();
}
...
```

<span data-ttu-id="054da-234">待機している**winrt::get_cancellation_token**の知識があるキャンセル トークンを取得、 **IAsyncAction**コルーチンが自動的に生成します。</span><span class="sxs-lookup"><span data-stu-id="054da-234">Waiting on **winrt::get_cancellation_token** retrieves a cancellation token with knowledge of the **IAsyncAction** that the coroutine is producing on your behalf.</span></span> <span data-ttu-id="054da-235">そのトークンに関数呼び出し演算子を使用するにはキャンセル状態を照会する&mdash;本質的に取り消し状態をポーリングします。</span><span class="sxs-lookup"><span data-stu-id="054da-235">You can use the function call operator on that token to query the cancellation state&mdash;essentially polling for cancellation.</span></span> <span data-ttu-id="054da-236">大規模なコレクションを反復し、これは、適切な手法によって計算バウンドの操作を実行している場合。</span><span class="sxs-lookup"><span data-stu-id="054da-236">If you're performing some compute-bound operation, or iterating through a large collection, then this is a reasonable technique.</span></span>

### <a name="register-a-cancellation-callback"></a><span data-ttu-id="054da-237">キャンセル コールバックを登録します。</span><span class="sxs-lookup"><span data-stu-id="054da-237">Register a cancellation callback</span></span>

<span data-ttu-id="054da-238">Windows ランタイムの取り消しは、その他の非同期オブジェクトを自動的に流れません。</span><span class="sxs-lookup"><span data-stu-id="054da-238">The Windows Runtime's cancellation doesn't automatically flow to other asynchronous objects.</span></span> <span data-ttu-id="054da-239">&mdash;10.0.17763.0 (Windows 10、バージョンは 1809) のバージョンの Windows SDK で導入された&mdash;取り消しのコールバックを登録することができます。</span><span class="sxs-lookup"><span data-stu-id="054da-239">But&mdash;introduced in version 10.0.17763.0 (Windows 10, version 1809) of the Windows SDK&mdash;you can register a cancellation callback.</span></span> <span data-ttu-id="054da-240">これは、プリエンプティブなフックをキャンセルを伝えることができるし、同時実行の既存のライブラリと統合することになります。</span><span class="sxs-lookup"><span data-stu-id="054da-240">This is a pre-emptive hook by which cancellation can be propagated, and makes it possible to integrate with existing concurrency libraries.</span></span>

<span data-ttu-id="054da-241">この次のコード例では**NestedCoroutineAsync**作業が特別な取り消しロジックがありません。</span><span class="sxs-lookup"><span data-stu-id="054da-241">In this next code example, **NestedCoroutineAsync** does the work, but it has no special cancellation logic in it.</span></span> <span data-ttu-id="054da-242">**CancellationPropagatorAsync** ; 入れ子になったコルーチンのラッパーでは基本的には、ラッパーがにわかキャンセルを転送します。</span><span class="sxs-lookup"><span data-stu-id="054da-242">**CancellationPropagatorAsync** is essentially a wrapper on the nested coroutine; the wrapper forwards cancellation pre-emptively.</span></span>

```cppwinrt
// main.cpp
#include <iostream>
#include <winrt/coroutine.h>
#include <winrt/Windows.Foundation.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace std::chrono_literals;

IAsyncAction NestedCoroutineAsync()
{
    while (true)
    {
        std::cout << "NestedCoroutineAsync: do some work for 1 second" << std::endl;
        co_await 1s;
    }
}

IAsyncAction CancellationPropagatorAsync()
{
    auto cancellation_token{ co_await winrt::get_cancellation_token() };
    auto nested_coroutine{ NestedCoroutineAsync() };

    cancellation_token.callback([=]
    {
        nested_coroutine.Cancel();
    });

    co_await nested_coroutine;
}

IAsyncAction MainCoroutineAsync()
{
    auto cancellation_propagator{ CancellationPropagatorAsync() };
    co_await 3s;
    cancellation_propagator.Cancel();
}

int main()
{
    winrt::init_apartment();
    MainCoroutineAsync().get();
}
```

<span data-ttu-id="054da-243">**CancellationPropagatorAsync**レジスタの独自のキャンセル コールバックし、ラムダ関数を待機 (が中断されます)、入れ子になった作業が完了するまでです。</span><span class="sxs-lookup"><span data-stu-id="054da-243">**CancellationPropagatorAsync** registers a lambda function for its own cancellation callback, and then it awaits (it suspends) until the nested work completes.</span></span> <span data-ttu-id="054da-244">場合、または**CancellationPropagatorAsync**が取り消されると、入れ子になったコルーチンにキャンセルを伝達します。</span><span class="sxs-lookup"><span data-stu-id="054da-244">When or if **CancellationPropagatorAsync** is canceled, it propagates the cancellation to the nested coroutine.</span></span> <span data-ttu-id="054da-245">キャンセル; をポーリングする必要はありません。キャンセルは無限にブロックします。</span><span class="sxs-lookup"><span data-stu-id="054da-245">There's no need to poll for cancellation; nor is cancellation blocked indefinitely.</span></span> <span data-ttu-id="054da-246">このメカニズムはコルーチンまたは同時実行の何も認識しているライブラリとの相互運用に使用するための十分な柔軟性/cli WinRT します。</span><span class="sxs-lookup"><span data-stu-id="054da-246">This mechanism is flexible enough for you to use it to interop with a coroutine or concurrency library that knows nothing of C++/WinRT.</span></span>

## <a name="reporting-progress"></a><span data-ttu-id="054da-247">進行状況の報告</span><span class="sxs-lookup"><span data-stu-id="054da-247">Reporting progress</span></span>

<span data-ttu-id="054da-248">場合は、コルーチンでは、どちらかを返します[ **IAsyncActionWithProgress**](/uwp/api/windows.foundation.iasyncactionwithprogress_tprogress_)、または[ **IAsyncOperationWithProgress**](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_)、取得することができ、によって返されるオブジェクト、 [ **winrt::get_progress_token** ](/uwp/cpp-ref-for-winrt/get-progress-token)関数、および進行状況のハンドラーに進行状況の報告に使用します。</span><span class="sxs-lookup"><span data-stu-id="054da-248">If your coroutine returns either [**IAsyncActionWithProgress**](/uwp/api/windows.foundation.iasyncactionwithprogress_tprogress_), or [**IAsyncOperationWithProgress**](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_), then you can retrieve the object returned by the [**winrt::get_progress_token**](/uwp/cpp-ref-for-winrt/get-progress-token) function, and use it to report progress back to a progress handler.</span></span> <span data-ttu-id="054da-249">次にコード例を示します。</span><span class="sxs-lookup"><span data-stu-id="054da-249">Here's a code example.</span></span>

```cppwinrt
// main.cpp
#include <iostream>
#include <winrt/coroutine.h>
#include <winrt/Windows.Foundation.h>

using namespace winrt;
using namespace Windows::Foundation;
using namespace std::chrono_literals;

IAsyncOperationWithProgress<double, double> CalcPiTo5DPs()
{
    auto progress{ co_await winrt::get_progress_token() };

    co_await 1s;
    double pi_so_far{ 3.1 };
    progress(0.2);

    co_await 1s;
    pi_so_far += 4.e-2;
    progress(0.4);

    co_await 1s;
    pi_so_far += 1.e-3;
    progress(0.6);

    co_await 1s;
    pi_so_far += 5.e-4;
    progress(0.8);

    co_await 1s;
    pi_so_far += 9.e-5;
    progress(1.0);
    co_return pi_so_far;
}

IAsyncAction DoMath()
{
    auto async_op_with_progress{ CalcPiTo5DPs() };
    async_op_with_progress.Progress([](auto const& /* sender */, double progress)
    {
        std::wcout << L"CalcPiTo5DPs() reports progress: " << progress << std::endl;
    });
    double pi{ co_await async_op_with_progress };
    std::wcout << L"CalcPiTo5DPs() is complete !" << std::endl;
    std::wcout << L"Pi is approx.: " << pi << std::endl;
}

int main()
{
    winrt::init_apartment();
    DoMath().get();
}
```

> [!NOTE]
> <span data-ttu-id="054da-250">1 つ以上実装するために正しくない*完了ハンドラー*非同期アクションまたは操作します。</span><span class="sxs-lookup"><span data-stu-id="054da-250">It's not correct to implement more than one *completion handler* for an asynchronous action or operation.</span></span> <span data-ttu-id="054da-251">、Completed イベントの 1 つのデリゲートがあることもできます`co_await`こと。</span><span class="sxs-lookup"><span data-stu-id="054da-251">You can have either a single delegate for its completed event, or you can `co_await` it.</span></span> <span data-ttu-id="054da-252">両方がある場合は、2 つ目は失敗します。</span><span class="sxs-lookup"><span data-stu-id="054da-252">If you have both, then the second will fail.</span></span> <span data-ttu-id="054da-253">いずれか適切な; 次の 2 種類の完了ハンドラーの 1 つです両方ではなく、同じ非同期オブジェクトの。</span><span class="sxs-lookup"><span data-stu-id="054da-253">Either one of the following two kinds of completion handlers is appropriate; not both for the same async object.</span></span>

```cppwinrt
auto async_op_with_progress{ CalcPiTo5DPs() };
async_op_with_progress.Completed([](auto const& sender, AsyncStatus /* status */)
{
    double pi{ sender.GetResults() };
});
```

```cppwinrt
auto async_op_with_progress{ CalcPiTo5DPs() };
double pi{ co_await async_op_with_progress };
```

<span data-ttu-id="054da-254">完了ハンドラーの詳細については、次を参照してください。[非同期アクションおよび操作の種類をデリゲート](handle-events.md#delegate-types-for-asynchronous-actions-and-operations)します。</span><span class="sxs-lookup"><span data-stu-id="054da-254">For more info about completion handlers, see [Delegate types for asynchronous actions and operations](handle-events.md#delegate-types-for-asynchronous-actions-and-operations).</span></span>

## <a name="fire-and-forget"></a><span data-ttu-id="054da-255">ファイア アンド フォーゲット</span><span class="sxs-lookup"><span data-stu-id="054da-255">Fire and forget</span></span>

<span data-ttu-id="054da-256">場合によっては、他の作業と同時に実行できるタスクがあるし、そのタスクを完了するまで待機する必要はありません (その他の作業なしに依存)、その値を返す必要があるとします。</span><span class="sxs-lookup"><span data-stu-id="054da-256">Sometimes, you have a task that can be done concurrently with other work, and you don't need to wait for that task to complete (no other work depends on it), nor do you need it to return a value.</span></span> <span data-ttu-id="054da-257">その場合は、タスクを起動し、忘れたできます。</span><span class="sxs-lookup"><span data-stu-id="054da-257">In that case, you can fire off the task and forget it.</span></span> <span data-ttu-id="054da-258">コルーチンの戻り値の型を記述することができます[ **winrt::fire_and_forget** ](/uwp/cpp-ref-for-winrt/fire-and-forget) (Windows ランタイムの非同期操作の種類のいずれかではなくまたは**concurrency::task**).</span><span class="sxs-lookup"><span data-stu-id="054da-258">You can do that by writing a coroutine whose return type is [**winrt::fire_and_forget**](/uwp/cpp-ref-for-winrt/fire-and-forget) (instead of one of the Windows Runtime asynchronous operation types, or **concurrency::task**).</span></span>

```cppwinrt
// main.cpp
#include <winrt/coroutine.h>
#include <winrt/Windows.Foundation.h>

using namespace winrt;
using namespace std::chrono_literals;

winrt::fire_and_forget CompleteInFiveSeconds()
{
    co_await 5s;
}

int main()
{
    winrt::init_apartment();
    CompleteInFiveSeconds();
    // Do other work here.
}
```

## <a name="important-apis"></a><span data-ttu-id="054da-259">重要な API</span><span class="sxs-lookup"><span data-stu-id="054da-259">Important APIs</span></span>
* [<span data-ttu-id="054da-260">concurrency::task クラス</span><span class="sxs-lookup"><span data-stu-id="054da-260">concurrency::task class</span></span>](/cpp/parallel/concrt/reference/task-class)
* [<span data-ttu-id="054da-261">IAsyncAction インターフェイス</span><span class="sxs-lookup"><span data-stu-id="054da-261">IAsyncAction interface</span></span>](/uwp/api/windows.foundation.iasyncaction)
* [<span data-ttu-id="054da-262">IAsyncActionWithProgress&lt;TProgress&gt;インターフェイス</span><span class="sxs-lookup"><span data-stu-id="054da-262">IAsyncActionWithProgress&lt;TProgress&gt; interface</span></span>](/uwp/api/windows.foundation.iasyncactionwithprogress_tprogress_)
* [<span data-ttu-id="054da-263">IAsyncOperation&lt;TResult&gt;インターフェイス</span><span class="sxs-lookup"><span data-stu-id="054da-263">IAsyncOperation&lt;TResult&gt; interface</span></span>](/uwp/api/windows.foundation.iasyncoperation_tresult_)
* [<span data-ttu-id="054da-264">IAsyncOperationWithProgress&lt;TResult, TProgress&gt;インターフェイス</span><span class="sxs-lookup"><span data-stu-id="054da-264">IAsyncOperationWithProgress&lt;TResult, TProgress&gt; interface</span></span>](/uwp/api/windows.foundation.iasyncoperationwithprogress_tresult_tprogress_)
* [<span data-ttu-id="054da-265">SyndicationClient::RetrieveFeedAsync メソッド</span><span class="sxs-lookup"><span data-stu-id="054da-265">SyndicationClient::RetrieveFeedAsync method</span></span>](/uwp/api/windows.web.syndication.syndicationclient.retrievefeedasync)
* [<span data-ttu-id="054da-266">SyndicationFeed クラス</span><span class="sxs-lookup"><span data-stu-id="054da-266">SyndicationFeed class</span></span>](/uwp/api/windows.web.syndication.syndicationfeed)
* [<span data-ttu-id="054da-267">winrt::get_cancellation_token</span><span class="sxs-lookup"><span data-stu-id="054da-267">winrt::get_cancellation_token</span></span>](/uwp/cpp-ref-for-winrt/get-cancellation-token)
* [<span data-ttu-id="054da-268">winrt::get_progress_token</span><span class="sxs-lookup"><span data-stu-id="054da-268">winrt::get_progress_token</span></span>](/uwp/cpp-ref-for-winrt/get-progress-token)
* [<span data-ttu-id="054da-269">winrt::fire_and_forget</span><span class="sxs-lookup"><span data-stu-id="054da-269">winrt::fire_and_forget</span></span>](/uwp/cpp-ref-for-winrt/fire-and-forget)

## <a name="related-topics"></a><span data-ttu-id="054da-270">関連トピック</span><span class="sxs-lookup"><span data-stu-id="054da-270">Related topics</span></span>
* [<span data-ttu-id="054da-271">C + でデリゲートを使用してイベントを処理/cli WinRT</span><span class="sxs-lookup"><span data-stu-id="054da-271">Handle events by using delegates in C++/WinRT</span></span>](handle-events.md)
* [<span data-ttu-id="054da-272">標準的な C++ のデータ型と C++/WinRT</span><span class="sxs-lookup"><span data-stu-id="054da-272">Standard C++ data types and C++/WinRT</span></span>](std-cpp-data-types.md)
