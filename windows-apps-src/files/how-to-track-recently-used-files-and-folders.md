---
ms.assetid: BF929A68-9C82-4866-BC13-A32B3A550005
title: 最近使ったファイルやフォルダーの追跡
description: ユーザーが頻繁にアクセスするファイルを追跡するには、そのファイルを最近使ったアプリの一覧 (MRU) に追加します。
ms.date: 12/19/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 97ad2485abab0bd4733699bc4ffcf29e17a22844
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369447"
---
# <a name="track-recently-used-files-and-folders"></a><span data-ttu-id="a1324-104">最近使ったファイルやフォルダーの追跡</span><span class="sxs-lookup"><span data-stu-id="a1324-104">Track recently used files and folders</span></span>

<span data-ttu-id="a1324-105">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="a1324-105">**Important APIs**</span></span>

- [<span data-ttu-id="a1324-106">**MostRecentlyUsedList**</span><span class="sxs-lookup"><span data-stu-id="a1324-106">**MostRecentlyUsedList**</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.mostrecentlyusedlist)
- [<span data-ttu-id="a1324-107">**FileOpenPicker**</span><span class="sxs-lookup"><span data-stu-id="a1324-107">**FileOpenPicker**</span></span>](https://docs.microsoft.com/uwp/schemas/appxpackage/appxmanifestschema/element-fileopenpicker)

<span data-ttu-id="a1324-108">ユーザーが頻繁にアクセスするファイルを追跡するには、そのファイルを最近使ったアプリの一覧 (MRU) に追加します。</span><span class="sxs-lookup"><span data-stu-id="a1324-108">Track files that your user accesses frequently by adding them to your app's most recently used list (MRU).</span></span> <span data-ttu-id="a1324-109">MRU はプラットフォームが管理し、最後にアクセスした日時に基づいて項目を並べ替えたり、一覧の上限である 25 項目に達したら最も古い項目を削除したりします。</span><span class="sxs-lookup"><span data-stu-id="a1324-109">The platform manages the MRU for you by sorting items based on when they were last accessed, and by removing the oldest item when the list's 25-item limit is reached.</span></span> <span data-ttu-id="a1324-110">すべてのアプリにはそれぞれに専用の MRU があります。</span><span class="sxs-lookup"><span data-stu-id="a1324-110">All apps have their own MRU.</span></span>

<span data-ttu-id="a1324-111">お使いのアプリの MRU は、静的な [**StorageApplicationPermissions.MostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.mostrecentlyusedlist) プロパティから取得する [**StorageItemMostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageItemMostRecentlyUsedList) クラスによって表されます。</span><span class="sxs-lookup"><span data-stu-id="a1324-111">Your app's MRU is represented by the [**StorageItemMostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageItemMostRecentlyUsedList) class, which you obtain from the static [**StorageApplicationPermissions.MostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.mostrecentlyusedlist) property.</span></span> <span data-ttu-id="a1324-112">MRU の項目は [**IStorageItem**](https://docs.microsoft.com/uwp/api/Windows.Storage.IStorageItem) オブジェクトとして格納されます。つまり、[**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクト (ファイルを表すオブジェクト) と [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) オブジェクト (フォルダーを表すオブジェクト) は、どちらも MRU に追加できます。</span><span class="sxs-lookup"><span data-stu-id="a1324-112">MRU items are stored as [**IStorageItem**](https://docs.microsoft.com/uwp/api/Windows.Storage.IStorageItem) objects, so both [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) objects (which represent files) and [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) objects (which represent folders) can be added to the MRU.</span></span>

> [!NOTE]
><span data-ttu-id="a1324-113"> 完全なサンプルは、次を参照してください。、[ファイル ピッカー サンプル](https://go.microsoft.com/fwlink/p/?linkid=619994)と[ファイル アクセス サンプル](https://go.microsoft.com/fwlink/p/?linkid=619995)します。</span><span class="sxs-lookup"><span data-stu-id="a1324-113"> For complete samples, see the [File picker sample](https://go.microsoft.com/fwlink/p/?linkid=619994) and the [File access sample](https://go.microsoft.com/fwlink/p/?linkid=619995).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1324-114">前提条件</span><span class="sxs-lookup"><span data-stu-id="a1324-114">Prerequisites</span></span>

-   <span data-ttu-id="a1324-115">**ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングを理解します。**</span><span class="sxs-lookup"><span data-stu-id="a1324-115">**Understand async programming for Universal Windows Platform (UWP) apps**</span></span>

    <span data-ttu-id="a1324-116">C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a1324-116">You can learn how to write asynchronous apps in C# or Visual Basic, see [Call asynchronous APIs in C# or Visual Basic](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic).</span></span> <span data-ttu-id="a1324-117">C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a1324-117">To learn how to write asynchronous apps in C++, see [Asynchronous programming in C++](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps).</span></span>

-   <span data-ttu-id="a1324-118">**場所へのアクセス許可**</span><span class="sxs-lookup"><span data-stu-id="a1324-118">**Access permissions to the location**</span></span>

    <span data-ttu-id="a1324-119">「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a1324-119">See [File access permissions](file-access-permissions.md).</span></span>

-   [<span data-ttu-id="a1324-120">ピッカーでファイルやフォルダーを開く</span><span class="sxs-lookup"><span data-stu-id="a1324-120">Open files and folders with a picker</span></span>](quickstart-using-file-and-folder-pickers.md)

    <span data-ttu-id="a1324-121">ユーザーは同じファイルを何度も選ぶ傾向にあります。</span><span class="sxs-lookup"><span data-stu-id="a1324-121">Picked files are often the same files that users return to again and again.</span></span>

 ## <a name="add-a-picked-file-to-the-mru"></a><span data-ttu-id="a1324-122">MRU に選んだファイルを追加する</span><span class="sxs-lookup"><span data-stu-id="a1324-122">Add a picked file to the MRU</span></span>

-   <span data-ttu-id="a1324-123">ユーザーは同じファイルを繰り返し選ぶ傾向にあります。</span><span class="sxs-lookup"><span data-stu-id="a1324-123">The files that your user picks are often files that they return to repeatedly.</span></span> <span data-ttu-id="a1324-124">そのため、選んだファイルはできるだけ早くアプリの MRU に追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a1324-124">So consider adding picked files to your app's MRU as soon as they are picked.</span></span> <span data-ttu-id="a1324-125">以下にその方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a1324-125">Here's how.</span></span>

    ```cs
    Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();

    var mru = Windows.Storage.AccessCache.StorageApplicationPermissions.MostRecentlyUsedList;
    string mruToken = mru.Add(file, "profile pic");
    ```

    <span data-ttu-id="a1324-126">[**StorageItemMostRecentlyUsedList.Add** ](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add)はオーバー ロードされます。</span><span class="sxs-lookup"><span data-stu-id="a1324-126">[**StorageItemMostRecentlyUsedList.Add**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add) is overloaded.</span></span> <span data-ttu-id="a1324-127">この例では [**Add(IStorageItem, String)** ](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add) を使って、メタデータをファイルに関連付けられるようにしています。</span><span class="sxs-lookup"><span data-stu-id="a1324-127">In the example, we use [**Add(IStorageItem, String)**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add) so that we can associate metadata with the file.</span></span> <span data-ttu-id="a1324-128">メタデータを設定すると、その項目の目的 ("プロファイル画像" など) を記録できます。</span><span class="sxs-lookup"><span data-stu-id="a1324-128">Setting metadata lets you record the item's purpose, for example "profile pic".</span></span> <span data-ttu-id="a1324-129">メタデータなしで MRU にファイルを追加するには、[**Add(IStorageItem)** ](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a1324-129">You can also add the file to the MRU without metadata by calling [**Add(IStorageItem)**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add).</span></span> <span data-ttu-id="a1324-130">MRU に項目を追加すると、項目を取得するときに使われる一意に識別するための文字列であるトークンが返されます。</span><span class="sxs-lookup"><span data-stu-id="a1324-130">When you add an item to the MRU, the method returns a uniquely identifying string, called a token, which is used to retrieve the item.</span></span>

> [!TIP]
> <span data-ttu-id="a1324-131">項目を MRU から取得するにはそのトークンが必要であるため、どこかに保存しておいてください。</span><span class="sxs-lookup"><span data-stu-id="a1324-131">You'll need the token to retrieve an item from the MRU, so persist it somewhere.</span></span> <span data-ttu-id="a1324-132">アプリ データの詳細については、「[アプリケーション データの管理](https://docs.microsoft.com/previous-versions/windows/apps/hh465109(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a1324-132">For more info about app data, see [Managing application data](https://docs.microsoft.com/previous-versions/windows/apps/hh465109(v=win.10)).</span></span>

## <a name="use-a-token-to-retrieve-an-item-from-the-mru"></a><span data-ttu-id="a1324-133">トークンを使って MRU から項目を取得する</span><span class="sxs-lookup"><span data-stu-id="a1324-133">Use a token to retrieve an item from the MRU</span></span>

<span data-ttu-id="a1324-134">取得する項目に最適な取得メソッドを使います。</span><span class="sxs-lookup"><span data-stu-id="a1324-134">Use the retrieval method most appropriate for the item you want to retrieve.</span></span>

-   <span data-ttu-id="a1324-135">ファイルを [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) として取得するには [**GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getfileasync) を使います。</span><span class="sxs-lookup"><span data-stu-id="a1324-135">Retrieve a file as a [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) by using [**GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getfileasync).</span></span>
-   <span data-ttu-id="a1324-136">フォルダーを [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) として取得するには [**GetFolderAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getfolderasync) を使います。</span><span class="sxs-lookup"><span data-stu-id="a1324-136">Retrieve a folder as a [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) by using [**GetFolderAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getfolderasync).</span></span>
-   <span data-ttu-id="a1324-137">ファイルかフォルダーを表す汎用の [**IStorageItem**](https://docs.microsoft.com/uwp/api/Windows.Storage.IStorageItem) を取得するには [**GetItemAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getitemasync) を使います。</span><span class="sxs-lookup"><span data-stu-id="a1324-137">Retrieve a generic [**IStorageItem**](https://docs.microsoft.com/uwp/api/Windows.Storage.IStorageItem), which can represent either a file or folder, by using [**GetItemAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getitemasync).</span></span>

<span data-ttu-id="a1324-138">先ほど追加したファイルを取得する方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a1324-138">Here's how to get back the file we just added.</span></span>

```cs
StorageFile retrievedFile = await mru.GetFileAsync(mruToken);
```

<span data-ttu-id="a1324-139">すべてのエントリを反復処理してトークンを取得した後に項目を取得する方法は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a1324-139">Here's how to iterate all the entries to get tokens and then items.</span></span>

```cs
foreach (Windows.Storage.AccessCache.AccessListEntry entry in mru.Entries)
{
    string mruToken = entry.Token;
    string mruMetadata = entry.Metadata;
    Windows.Storage.IStorageItem item = await mru.GetItemAsync(mruToken);
    // The type of item will tell you whether it's a file or a folder.
}
```

<span data-ttu-id="a1324-140">[  **AccessListEntryView**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.AccessListEntryView) を使うと MRU 内のエントリを反復処理できます。</span><span class="sxs-lookup"><span data-stu-id="a1324-140">The [**AccessListEntryView**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.AccessListEntryView) lets you iterate entries in the MRU.</span></span> <span data-ttu-id="a1324-141">これらのエントリは、項目のトークンとメタデータが格納された [**AccessListEntry**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.AccessListEntry) 構造体です。</span><span class="sxs-lookup"><span data-stu-id="a1324-141">These entries are [**AccessListEntry**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.AccessListEntry) structures that contain the token and metadata for an item.</span></span>

## <a name="removing-items-from-the-mru-when-its-full"></a><span data-ttu-id="a1324-142">空きのない MRU から項目を削除する</span><span class="sxs-lookup"><span data-stu-id="a1324-142">Removing items from the MRU when it's full</span></span>

<span data-ttu-id="a1324-143">MRU の上限である 25 項目に達している場合、新しい項目を追加しようとすると、最後にアクセスしてからの経過時間が最も長い項目が自動的に削除されます。</span><span class="sxs-lookup"><span data-stu-id="a1324-143">When the MRU's 25-item limit is reached and you try to add a new item, the item that was accessed the longest time ago is automatically removed.</span></span> <span data-ttu-id="a1324-144">そのため、新しい項目を追加する前に項目を削除する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a1324-144">So, you never need to remove an item before you add a new one.</span></span>

## <a name="future-access-list"></a><span data-ttu-id="a1324-145">後でアクセスする一覧</span><span class="sxs-lookup"><span data-stu-id="a1324-145">Future-access list</span></span>

<span data-ttu-id="a1324-146">アプリには MRU のほか、後でアクセスする一覧もあります。</span><span class="sxs-lookup"><span data-stu-id="a1324-146">As well as an MRU, your app also has a future-access list.</span></span> <span data-ttu-id="a1324-147">ファイルやフォルダーを選ぶことで、ユーザーはアプリがアクセスできない可能性がある項目にアクセス許可を付与します。</span><span class="sxs-lookup"><span data-stu-id="a1324-147">By picking files and folders, your user grants your app permission to access items that might not be accessible otherwise.</span></span> <span data-ttu-id="a1324-148">これらの項目を後でアクセスする一覧に追加すると、後にそれらの項目にアプリがアクセスする場合に備えてアクセス許可が保持されます。</span><span class="sxs-lookup"><span data-stu-id="a1324-148">If you add these items to your future-access list then you'll retain that permission when your app wants to access those items again later.</span></span> <span data-ttu-id="a1324-149">お使いのアプリの、後でアクセスする一覧は、静的な [**StorageApplicationPermissions.FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) プロパティから取得する [**StorageItemAccessList**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageItemAccessList) クラスによって表されます。</span><span class="sxs-lookup"><span data-stu-id="a1324-149">Your app's future-access list is represented by the [**StorageItemAccessList**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageItemAccessList) class, which you obtain from the static [**StorageApplicationPermissions.FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) property.</span></span>

<span data-ttu-id="a1324-150">ユーザーが項目を選ぶ際には、MRU のほか、後でアクセスする一覧にも追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a1324-150">When a user picks an item, consider adding it to your future-access list as well as your MRU.</span></span>

-   <span data-ttu-id="a1324-151">[  **FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) は最大 1,000 項目を保持できます。</span><span class="sxs-lookup"><span data-stu-id="a1324-151">The [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) can hold up to 1000 items.</span></span> <span data-ttu-id="a1324-152">ファイル以外にもフォルダーを保持できるため、大量のフォルダーがあることにご注意ください。</span><span class="sxs-lookup"><span data-stu-id="a1324-152">Remember: it can hold folders as well as files, so that's a lot of folders.</span></span>
-   <span data-ttu-id="a1324-153">プラットフォームによって [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) から項目が削除されることはありません。</span><span class="sxs-lookup"><span data-stu-id="a1324-153">The platform never removes items from the [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) for you.</span></span> <span data-ttu-id="a1324-154">項目の数が上限の 1,000 に到達した場合、[**Remove**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.remove) メソッドで空きを確保するまで項目を追加できません。</span><span class="sxs-lookup"><span data-stu-id="a1324-154">When you reach the 1000-item limit, you can't add another until you make room with the [**Remove**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.remove) method.</span></span>
