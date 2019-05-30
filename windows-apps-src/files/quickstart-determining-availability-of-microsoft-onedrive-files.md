---
ms.assetid: 3604524F-112A-474F-B0CA-0726DC8DB885
title: Microsoft OneDrive ファイルが利用可能かどうかの確認
description: StorageFile.IsAvailable プロパティを使って、Microsoft OneDrive ファイルが利用可能かどうかを確認します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: effb28fa453ec884152dbc404245f00f4893ef5a
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369422"
---
# <a name="determining-availability-of-microsoft-onedrive-files"></a><span data-ttu-id="f3c84-104">Microsoft OneDrive ファイルが利用可能かどうかの確認</span><span class="sxs-lookup"><span data-stu-id="f3c84-104">Determining availability of Microsoft OneDrive files</span></span>


<span data-ttu-id="f3c84-105">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="f3c84-105">**Important APIs**</span></span>

-   [<span data-ttu-id="f3c84-106">**FileIO クラス**</span><span class="sxs-lookup"><span data-stu-id="f3c84-106">**FileIO class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.FileIO)
-   [<span data-ttu-id="f3c84-107">**StorageFile クラス**</span><span class="sxs-lookup"><span data-stu-id="f3c84-107">**StorageFile class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile)
-   [<span data-ttu-id="f3c84-108">**StorageFile.IsAvailable property**</span><span class="sxs-lookup"><span data-stu-id="f3c84-108">**StorageFile.IsAvailable property**</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable)

<span data-ttu-id="f3c84-109">[  **StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable) プロパティを使って、Microsoft OneDrive ファイルが利用可能かどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-109">Determine if a Microsoft OneDrive file is available using the [**StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable) property.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3c84-110">前提条件</span><span class="sxs-lookup"><span data-stu-id="f3c84-110">Prerequisites</span></span>

-   <span data-ttu-id="f3c84-111">**ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングを理解します。**</span><span class="sxs-lookup"><span data-stu-id="f3c84-111">**Understand async programming for Universal Windows Platform (UWP) apps**</span></span>

    <span data-ttu-id="f3c84-112">C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f3c84-112">You can learn how to write asynchronous apps in C# or Visual Basic, see [Call asynchronous APIs in C# or Visual Basic](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic).</span></span> <span data-ttu-id="f3c84-113">C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f3c84-113">To learn how to write asynchronous apps in C++, see [Asynchronous programming in C++](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps).</span></span>

-   <span data-ttu-id="f3c84-114">**アプリの capabilty 宣言**</span><span class="sxs-lookup"><span data-stu-id="f3c84-114">**App capabilty declarations**</span></span>

    <span data-ttu-id="f3c84-115">「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f3c84-115">See [File access permissions](file-access-permissions.md).</span></span>

## <a name="using-the-storagefileisavailable-property"></a><span data-ttu-id="f3c84-116">StorageFile.IsAvailable プロパティの使用</span><span class="sxs-lookup"><span data-stu-id="f3c84-116">Using the StorageFile.IsAvailable property</span></span>

<span data-ttu-id="f3c84-117">ユーザーは、OneDrive ファイルを "オフラインで利用可能" (既定) または "オンラインのみ" とマークできます。</span><span class="sxs-lookup"><span data-stu-id="f3c84-117">Users are able to mark OneDrive files as either available-offline (default) or online-only.</span></span> <span data-ttu-id="f3c84-118">この機能を使うと、大容量のファイル (写真やビデオなど) を自分の OneDrive に移動し、オンラインのみとマークすることで、ディスク領域を節約できます (ローカルに保存されるのはメタデータ ファイルのみです)。</span><span class="sxs-lookup"><span data-stu-id="f3c84-118">This capability enables users to move large files (such as pictures and videos) to their OneDrive, mark them as online-only, and save disk space (the only thing kept locally is a metadata file).</span></span>

<span data-ttu-id="f3c84-119">[**StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable)ファイルが現在使用できるかを判断するために使用します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-119">[**StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable), is used to determine if a file is currently available.</span></span> <span data-ttu-id="f3c84-120">次の表に、さまざまなシナリオでの **StorageFile.IsAvailable** プロパティの値を示します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-120">The following table shows the value of the **StorageFile.IsAvailable** property in various scenarios.</span></span>

| <span data-ttu-id="f3c84-121">ファイルの種類</span><span class="sxs-lookup"><span data-stu-id="f3c84-121">Type of file</span></span>                              | <span data-ttu-id="f3c84-122">オンライン</span><span class="sxs-lookup"><span data-stu-id="f3c84-122">Online</span></span> | <span data-ttu-id="f3c84-123">従量制課金接続</span><span class="sxs-lookup"><span data-stu-id="f3c84-123">Metered network</span></span>        | <span data-ttu-id="f3c84-124">オフライン</span><span class="sxs-lookup"><span data-stu-id="f3c84-124">Offline</span></span> |
|-------------------------------------------|--------|------------------------|---------|
| <span data-ttu-id="f3c84-125">ローカル ファイル</span><span class="sxs-lookup"><span data-stu-id="f3c84-125">Local file</span></span>                                | <span data-ttu-id="f3c84-126">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-126">True</span></span>   | <span data-ttu-id="f3c84-127">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-127">True</span></span>                   | <span data-ttu-id="f3c84-128">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-128">True</span></span>    |
| <span data-ttu-id="f3c84-129">オフラインで利用可能とマークされている OneDrive ファイル</span><span class="sxs-lookup"><span data-stu-id="f3c84-129">OneDrive file marked as available-offline</span></span> | <span data-ttu-id="f3c84-130">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-130">True</span></span>   | <span data-ttu-id="f3c84-131">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-131">True</span></span>                   | <span data-ttu-id="f3c84-132">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-132">True</span></span>    |
| <span data-ttu-id="f3c84-133">オンラインのみとマークされている OneDrive ファイル</span><span class="sxs-lookup"><span data-stu-id="f3c84-133">OneDrive file marked as online-only</span></span>       | <span data-ttu-id="f3c84-134">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-134">True</span></span>   | <span data-ttu-id="f3c84-135">ユーザー設定に基づく</span><span class="sxs-lookup"><span data-stu-id="f3c84-135">Based on user settings</span></span> | <span data-ttu-id="f3c84-136">False</span><span class="sxs-lookup"><span data-stu-id="f3c84-136">False</span></span>   |
| <span data-ttu-id="f3c84-137">ネットワーク ファイル</span><span class="sxs-lookup"><span data-stu-id="f3c84-137">Network file</span></span>                              | <span data-ttu-id="f3c84-138">True</span><span class="sxs-lookup"><span data-stu-id="f3c84-138">True</span></span>   | <span data-ttu-id="f3c84-139">ユーザー設定に基づく</span><span class="sxs-lookup"><span data-stu-id="f3c84-139">Based on user settings</span></span> | <span data-ttu-id="f3c84-140">False</span><span class="sxs-lookup"><span data-stu-id="f3c84-140">False</span></span>   |

 

<span data-ttu-id="f3c84-141">次の手順では、ファイルが現在利用できるかどうかを判別する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="f3c84-141">The following steps illustrate how to determine if a file is currently available.</span></span>

1.  <span data-ttu-id="f3c84-142">アクセスするライブラリに適した機能を宣言します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-142">Declare a capability appropriate for the library you want to access.</span></span>
2.  <span data-ttu-id="f3c84-143">[  **Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage) 名前空間を含めます。</span><span class="sxs-lookup"><span data-stu-id="f3c84-143">Include the [**Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage) namespace.</span></span> <span data-ttu-id="f3c84-144">この名前空間には、ファイル、フォルダー、アプリケーション設定を管理するための型が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c84-144">This namespace includes the types for managing files, folders, and application settings.</span></span> <span data-ttu-id="f3c84-145">また、必要な [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) 型も含まれています。</span><span class="sxs-lookup"><span data-stu-id="f3c84-145">It also includes the needed [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) type.</span></span>
3.  <span data-ttu-id="f3c84-146">必要なファイルの [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-146">Acquire a [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) object for the desired file(s).</span></span> <span data-ttu-id="f3c84-147">ライブラリを列挙する場合、通常、この手順は [**StorageFolder.CreateFileQuery**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfilequery) メソッドを呼び出し、結果の [**StorageFileQueryResult**](https://docs.microsoft.com/uwp/api/Windows.Storage.Search.StorageFileQueryResult) オブジェクトの [**GetFilesAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfilesasync) メソッドを呼び出して行います。</span><span class="sxs-lookup"><span data-stu-id="f3c84-147">If you are enumerating a library, this step is usually accomplished by calling the [**StorageFolder.CreateFileQuery**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfilequery) method and then calling the resulting [**StorageFileQueryResult**](https://docs.microsoft.com/uwp/api/Windows.Storage.Search.StorageFileQueryResult) object's [**GetFilesAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfilesasync) method.</span></span> <span data-ttu-id="f3c84-148">**GetFilesAsync** メソッドは、**StorageFile** オブジェクトの [IReadOnlyList](https://go.microsoft.com/fwlink/p/?LinkId=324970) コレクションを返します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-148">The **GetFilesAsync** method returns an [IReadOnlyList](https://go.microsoft.com/fwlink/p/?LinkId=324970) collection of **StorageFile** objects.</span></span>
4.  <span data-ttu-id="f3c84-149">目的のファイルを表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクトにアクセスできるようになると、[**StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable) プロパティの値は、ファイルが利用できるかどうかを表します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-149">Once you have the access to a [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) object representing the desired file(s), the value of the [**StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable) property reflects whether or not the file is available.</span></span>

<span data-ttu-id="f3c84-150">次の汎用的なメソッドは、フォルダーを列挙し、そのフォルダーの [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクトのコレクションを返す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="f3c84-150">The following generic method illustrates how to enumerate any folder and return the collection of [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) objects for that folder.</span></span> <span data-ttu-id="f3c84-151">その後、呼び出し元メソッドで、各ファイルの [**StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable) プロパティを参照する返されたコレクションを反復処理します。</span><span class="sxs-lookup"><span data-stu-id="f3c84-151">The calling method then iterates over the returned collection referencing the [**StorageFile.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.isavailable) property for each file.</span></span>

```cs
/// <summary>
/// Generic function that retrieves all files from the specified folder.
/// </summary>
/// <param name="folder">The folder to be searched.</param>
/// <returns>An IReadOnlyList collection containing the file objects.</returns>
async Task<System.Collections.Generic.IReadOnlyList<StorageFile>> GetLibraryFilesAsync(StorageFolder folder)
{
    var query = folder.CreateFileQuery();
    return await query.GetFilesAsync();
}

private async void CheckAvailabilityOfFilesInPicturesLibrary()
{
    // Determine availability of all files within Pictures library.
    var files = await GetLibraryFilesAsync(KnownFolders.PicturesLibrary);
    for (int i = 0; i < files.Count; i++)
    {
        StorageFile file = files[i];

        StringBuilder fileInfo = new StringBuilder();
        fileInfo.AppendFormat("{0} (on {1}) is {2}",
                    file.Name,
                    file.Provider.DisplayName,
                    file.IsAvailable ? "available" : "not available");
    }
}
```
