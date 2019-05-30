---
ms.assetid: 12ECEA89-59D2-4BCE-B24C-5A4DD525E0C7
title: ホームグループ コンテンツへのアクセス
description: ユーザーのホームグループ フォルダーに格納されているコンテンツ (画像、音楽、ビデオなど) にアクセスします。
ms.date: 12/19/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 07d94f5b11acfe14bf55392c5cbf2c1b7bcfbeef
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369396"
---
# <a name="accessing-homegroup-content"></a><span data-ttu-id="0ee80-104">ホームグループ コンテンツへのアクセス</span><span class="sxs-lookup"><span data-stu-id="0ee80-104">Accessing HomeGroup content</span></span>



<span data-ttu-id="0ee80-105">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="0ee80-105">**Important APIs**</span></span>

-   [<span data-ttu-id="0ee80-106">**Windows.Storage.KnownFolders クラス**</span><span class="sxs-lookup"><span data-stu-id="0ee80-106">**Windows.Storage.KnownFolders class**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders)

<span data-ttu-id="0ee80-107">ユーザーのホームグループ フォルダーに格納されているコンテンツ (画像、音楽、ビデオなど) にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="0ee80-107">Access content stored in the user's HomeGroup folder, including pictures, music, and videos.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ee80-108">前提条件</span><span class="sxs-lookup"><span data-stu-id="0ee80-108">Prerequisites</span></span>

-   <span data-ttu-id="0ee80-109">**ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングを理解します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-109">**Understand async programming for Universal Windows Platform (UWP) apps**</span></span>

    <span data-ttu-id="0ee80-110">C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ee80-110">You can learn how to write asynchronous apps in C# or Visual Basic, see [Call asynchronous APIs in C# or Visual Basic](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic).</span></span> <span data-ttu-id="0ee80-111">C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ee80-111">To learn how to write asynchronous apps in C++, see [Asynchronous programming in C++](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps).</span></span>

-   <span data-ttu-id="0ee80-112">**アプリの capabilty 宣言**</span><span class="sxs-lookup"><span data-stu-id="0ee80-112">**App capabilty declarations**</span></span>

    <span data-ttu-id="0ee80-113">ホームグループ コンテンツにアクセスするには、ユーザーのコンピューターにホームグループがセットアップされ、アプリに **picturesLibrary**、**musicLibrary**、**videosLibrary** のうちの少なくとも 1 つの機能が備わっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="0ee80-113">To access HomeGroup content, the user's machine must have a HomeGroup set up and your app must have at least one of the following capabilities: **picturesLibrary**, **musicLibrary**, or **videosLibrary**.</span></span> <span data-ttu-id="0ee80-114">アプリは、ホームグループ フォルダーにアクセスすると、アプリのマニフェストで宣言されている機能に対応するライブラリだけを参照します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-114">When your app accesses the HomeGroup folder, it will see only the libraries that correspond to the capabilities declared in your app's manifest.</span></span> <span data-ttu-id="0ee80-115">詳しくは、「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ee80-115">To learn more, see [File access permissions](file-access-permissions.md).</span></span>

    > [!NOTE]
    ><span data-ttu-id="0ee80-116"> ホーム グループのドキュメント ライブラリ内のコンテンツは、アプリのマニフェストで宣言されている機能に関係なく、ユーザーの共有設定に関係なく、アプリに表示されません。</span><span class="sxs-lookup"><span data-stu-id="0ee80-116"> Content in the Documents library of a HomeGroup isn't visible to your app regardless of the capabilities declared in your app's manifest and regardless of the user's sharing settings.</span></span>     

-   <span data-ttu-id="0ee80-117">**ファイル ピッカーを使用する方法を理解します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-117">**Understand how to use file pickers**</span></span>

    <span data-ttu-id="0ee80-118">ホームグループのファイルやフォルダーにアクセスするには、通常、ファイル ピッカーを使います。</span><span class="sxs-lookup"><span data-stu-id="0ee80-118">You typically use the file picker to access files and folders in the HomeGroup.</span></span> <span data-ttu-id="0ee80-119">ファイル ピッカーの使い方については、「[ピッカーでファイルやフォルダーを開く](quickstart-using-file-and-folder-pickers.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ee80-119">To learn how to use the file picker, see [Open files and folders with a picker](quickstart-using-file-and-folder-pickers.md).</span></span>

-   <span data-ttu-id="0ee80-120">**ファイルとフォルダーのクエリを理解します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-120">**Understand file and folder queries**</span></span>

    <span data-ttu-id="0ee80-121">ホームグループのファイルやフォルダーを列挙するには、クエリを使うことができます。</span><span class="sxs-lookup"><span data-stu-id="0ee80-121">You can use queries to enumerate files and folders in the HomeGroup.</span></span> <span data-ttu-id="0ee80-122">ファイルとフォルダーのクエリについて詳しくは、「[ファイルとフォルダーの列挙と照会](quickstart-listing-files-and-folders.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ee80-122">To learn about file and folder queries, see [Enumerating and querying files and folders](quickstart-listing-files-and-folders.md).</span></span>

## <a name="open-the-file-picker-at-the-homegroup"></a><span data-ttu-id="0ee80-123">ホームグループでファイル ピッカーを開く</span><span class="sxs-lookup"><span data-stu-id="0ee80-123">Open the file picker at the HomeGroup</span></span>

<span data-ttu-id="0ee80-124">以下の手順に従って、ユーザーがホームグループのファイルとフォルダーを選ぶことができるファイル ピッカーのインスタンスを開きます。</span><span class="sxs-lookup"><span data-stu-id="0ee80-124">Follow these steps to open an instance of the file picker that lets the user pick files and folders from the HomeGroup:</span></span>

1.  <span data-ttu-id="0ee80-125">**作成し、ファイル ピッカーをカスタマイズします。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-125">**Create and customize the file picker**</span></span>

    <span data-ttu-id="0ee80-126">[  **FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) を使ってファイル ピッカーを作成し、ピッカーの [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation) を [**PickerLocationId.HomeGroup**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerLocationId) に設定します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-126">Use [**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) to create the file picker, and then set the picker's [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation) to [**PickerLocationId.HomeGroup**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerLocationId).</span></span> <span data-ttu-id="0ee80-127">または、ユーザーとアプリに関連するその他のプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-127">Or, set other properties that are relevant to your users and your app.</span></span> <span data-ttu-id="0ee80-128">ファイル ピッカーのカスタマイズ方法を判断するためのガイドラインについては、「[ファイル ピッカーのガイドラインとチェック リスト](https://docs.microsoft.com/windows/uwp/files/quickstart-using-file-and-folder-pickers)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ee80-128">For guidelines to help you decide how to customize the file picker, see [Guidelines and checklist for file pickers](https://docs.microsoft.com/windows/uwp/files/quickstart-using-file-and-folder-pickers)</span></span>

    <span data-ttu-id="0ee80-129">次の例では、ホームグループで開かれ、すべての種類のファイルを含み、ファイルをサムネイル画像として表示するファイル ピッカーを作成しています。</span><span class="sxs-lookup"><span data-stu-id="0ee80-129">This example creates a file picker that opens at the HomeGroup, includes files of any type, and displays the files as thumbnail images:</span></span>
    ```cs
    Windows.Storage.Pickers.FileOpenPicker picker = new Windows.Storage.Pickers.FileOpenPicker();
    picker.ViewMode = Windows.Storage.Pickers.PickerViewMode.Thumbnail;
    picker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.HomeGroup;
    picker.FileTypeFilter.Clear();
    picker.FileTypeFilter.Add("*");
    ```

2.  <span data-ttu-id="0ee80-130">**ファイル ピッカーを表示し、選択されたファイルを処理します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-130">**Show the file picker and process the picked file.**</span></span>

    <span data-ttu-id="0ee80-131">ファイル ピッカーを作成してカスタマイズしたら、ユーザーが 1 つのファイルを選べるように [**FileOpenPicker.PickSingleFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync) を呼び出すか、複数のファイルを選べるように [**FileOpenPicker.PickMultipleFilesAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.pickmultiplefilesasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-131">After you create and customize the file picker, let the user pick one file by calling [**FileOpenPicker.PickSingleFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync), or multiple files by calling [**FileOpenPicker.PickMultipleFilesAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.pickmultiplefilesasync).</span></span>

    <span data-ttu-id="0ee80-132">次の例では、ファイル ピッカーを表示して、ユーザーが 1 つのファイルを選べるようにしています。</span><span class="sxs-lookup"><span data-stu-id="0ee80-132">This example displays the file picker to let the user pick one file:</span></span>
    ```cs
    Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();

    if (file != null)
    {
        // Do something with the file.
    }
    else
    {
        // No file returned. Handle the error.
    }   
    ```

## <a name="search-the-homegroup-for-files"></a><span data-ttu-id="0ee80-133">ホームグループでファイルを検索する</span><span class="sxs-lookup"><span data-stu-id="0ee80-133">Search the HomeGroup for files</span></span>

<span data-ttu-id="0ee80-134">このセクションでは、ユーザーが指定したクエリ語句に一致するホームグループ項目を見つける方法を示します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-134">This section shows how to find HomeGroup items that match a query term provided by the user.</span></span>

1.  <span data-ttu-id="0ee80-135">**ユーザーから、クエリ用語を取得します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-135">**Get the query term from the user.**</span></span>

    <span data-ttu-id="0ee80-136">ここでは、ユーザーが `searchQueryTextBox` という名前の [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) コントロールに入力したクエリ語句を取得します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-136">Here we get a query term that the user has entered into a [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) control called `searchQueryTextBox`:</span></span>
    ```cs
    string queryTerm = this.searchQueryTextBox.Text;    
    ```

2.  <span data-ttu-id="0ee80-137">**検索フィルター クエリ オプションを設定します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-137">**Set the query options and search filter.**</span></span>

    <span data-ttu-id="0ee80-138">クエリ オプションは、検索結果をどのように並べ替えるかを決めます。検索フィルターは、どの項目が検索結果に含まれるかを決めます。</span><span class="sxs-lookup"><span data-stu-id="0ee80-138">Query options determine how the search results are sorted, while the search filter determines which items are included in the search results.</span></span>

    <span data-ttu-id="0ee80-139">次の例は、検索結果をまず関連性で、次に更新日で並べ替えるクエリ オプションを設定します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-139">This example sets query options that sort the search results by relevance and then the date modified.</span></span> <span data-ttu-id="0ee80-140">検索フィルターは、ユーザーが前の手順で入力したクエリ語句です。</span><span class="sxs-lookup"><span data-stu-id="0ee80-140">The search filter is the query term that the user entered in the previous step:</span></span>
    ```cs
    Windows.Storage.Search.QueryOptions queryOptions =
            new Windows.Storage.Search.QueryOptions
                (Windows.Storage.Search.CommonFileQuery.OrderBySearchRank, null);
    queryOptions.UserSearchFilter = queryTerm.Text;
    Windows.Storage.Search.StorageFileQueryResult queryResults =
            Windows.Storage.KnownFolders.HomeGroup.CreateFileQueryWithOptions(queryOptions);    
    ```

3.  <span data-ttu-id="0ee80-141">**クエリを実行し、結果を処理します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-141">**Run the query and process the results.**</span></span>

    <span data-ttu-id="0ee80-142">次の例は、ホームグループで検索クエリを実行し、一致するファイルの名前を文字列の一覧として保存します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-142">The following example runs the search query in the HomeGroup and saves the names of any matching files as a list of strings.</span></span>
    ```cs
    System.Collections.Generic.IReadOnlyList<Windows.Storage.StorageFile> files =
        await queryResults.GetFilesAsync();

    if (files.Count > 0)
    {
        outputString += (files.Count == 1) ? "One file found\n" : files.Count.ToString() + " files found\n";
        foreach (Windows.Storage.StorageFile file in files)
        {
            outputString += file.Name + "\n";
        }
    }    
    ```


## <a name="search-the-homegroup-for-a-particular-users-shared-files"></a><span data-ttu-id="0ee80-143">ホームグループで特定のユーザーの共有ファイルを検索する</span><span class="sxs-lookup"><span data-stu-id="0ee80-143">Search the HomeGroup for a particular user's shared files</span></span>

<span data-ttu-id="0ee80-144">このセクションでは、特定のユーザーによって共有されているホームグループ ファイルを見つける方法を示します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-144">This section shows you how to find HomeGroup files that are shared by a particular user.</span></span>

1.  <span data-ttu-id="0ee80-145">**ホーム グループのユーザーのコレクションを取得します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-145">**Get a collection of HomeGroup users.**</span></span>

    <span data-ttu-id="0ee80-146">ホームグループの第 1 レベルのフォルダーは、それぞれが個々のホームグループ ユーザーを表しています。</span><span class="sxs-lookup"><span data-stu-id="0ee80-146">Each of the first-level folders in the HomeGroup represents an individual HomeGroup user.</span></span> <span data-ttu-id="0ee80-147">そのため、ホームグループ ユーザーのコレクションを取得するには、[**GetFoldersAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfoldersasync) を呼び出し、第 1 レベルのホームグループ フォルダーを取得します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-147">So, to get the collection of HomeGroup users, call [**GetFoldersAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfoldersasync) retrieve the top-level HomeGroup folders.</span></span>
    ```cs
    System.Collections.Generic.IReadOnlyList<Windows.Storage.StorageFolder> hgFolders =
        await Windows.Storage.KnownFolders.HomeGroup.GetFoldersAsync();    
    ```

2.  <span data-ttu-id="0ee80-148">**ターゲット ユーザーのフォルダーを見つけて、そのユーザーのフォルダーにスコープ設定ファイルのクエリを作成します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-148">**Find the target user's folder, and then create a file query scoped to that user's folder.**</span></span>

    <span data-ttu-id="0ee80-149">次の例は、取得したフォルダーを反復処理して、目的のユーザーのフォルダーを見つけます。</span><span class="sxs-lookup"><span data-stu-id="0ee80-149">The following example iterates through the retrieved folders to find the target user's folder.</span></span> <span data-ttu-id="0ee80-150">次に、クエリ オプションを設定して、フォルダー内のすべてのファイルを検索し、まずは関連性で、次に更新日で並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="0ee80-150">Then, it sets query options to find all files in the folder, sorted first by relevance and then by the date modified.</span></span> <span data-ttu-id="0ee80-151">この例では、見つかったファイルの数とファイルの名前を報告する文字列を作成します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-151">The example builds a string that reports the number of files found, along with the names of the files.</span></span>
    ```cs
    bool userFound = false;
    foreach (Windows.Storage.StorageFolder folder in hgFolders)
    {
        if (folder.DisplayName == targetUserName)
        {
            // Found the target user's folder, now find all files in the folder.
            userFound = true;
            Windows.Storage.Search.QueryOptions queryOptions =
                new Windows.Storage.Search.QueryOptions
                    (Windows.Storage.Search.CommonFileQuery.OrderBySearchRank, null);
            queryOptions.UserSearchFilter = "*";
            Windows.Storage.Search.StorageFileQueryResult queryResults =
                folder.CreateFileQueryWithOptions(queryOptions);
            System.Collections.Generic.IReadOnlyList<Windows.Storage.StorageFile> files =
                await queryResults.GetFilesAsync();

            if (files.Count > 0)
            {
                string outputString = "Searched for files belonging to " + targetUserName + "'\n";
                outputString += (files.Count == 1) ? "One file found\n" : files.Count.ToString() + " files found\n";
                foreach (Windows.Storage.StorageFile file in files)
                {
                    outputString += file.Name + "\n";
                }
            }
        }
    }    
    ```

## <a name="stream-video-from-the-homegroup"></a><span data-ttu-id="0ee80-152">ホームグループからビデオをストリーミングする</span><span class="sxs-lookup"><span data-stu-id="0ee80-152">Stream video from the HomeGroup</span></span>

<span data-ttu-id="0ee80-153">ホームグループからビデオ コンテンツをストリーミングするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-153">Follow these steps to stream video content from the HomeGroup:</span></span>

1.  <span data-ttu-id="0ee80-154">**アプリ内に MediaElement を含めます。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-154">**Include a MediaElement in your app.**</span></span>

    <span data-ttu-id="0ee80-155">[  **MediaElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement) は、アプリのオーディオ コンテンツとビデオ コンテンツを再生します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-155">A [**MediaElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement) lets you play back audio and video content in your app.</span></span> <span data-ttu-id="0ee80-156">オーディオとビデオの再生について詳しくは、「[カスタム トランスポート コントロールを作成する](https://docs.microsoft.com/windows/uwp/controls-and-patterns/custom-transport-controls)」と「[オーディオ、ビデオ、およびカメラ](https://docs.microsoft.com/windows/uwp/audio-video-camera/index)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0ee80-156">For more information on audio and video playback, see [Create custom transport controls](https://docs.microsoft.com/windows/uwp/controls-and-patterns/custom-transport-controls) and [Audio, video, and camera](https://docs.microsoft.com/windows/uwp/audio-video-camera/index).</span></span>
    ```HTML
    <Grid x:Name="Output" HorizontalAlignment="Left" VerticalAlignment="Top" Grid.Row="1">
        <MediaElement x:Name="VideoBox" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0" Width="400" Height="300"/>
    </Grid>    
    ```

2.  <span data-ttu-id="0ee80-157">**ホーム グループにファイル ピッカーを開き、アプリでサポートされる形式でビデオ ファイルを含むフィルターを適用します。**</span><span class="sxs-lookup"><span data-stu-id="0ee80-157">**Open a file picker at the HomeGroup and apply a filter that includes video files in the formats that your app supports.**</span></span>

    <span data-ttu-id="0ee80-158">次の例では、ファイル オープン ピッカーに .mp4 ファイルと .wmv ファイルが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0ee80-158">This example includes .mp4 and .wmv files in the file open picker.</span></span>
    ```cs
    Windows.Storage.Pickers.FileOpenPicker picker = new Windows.Storage.Pickers.FileOpenPicker();
    picker.ViewMode = Windows.Storage.Pickers.PickerViewMode.Thumbnail;
    picker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.HomeGroup;
    picker.FileTypeFilter.Clear();
    picker.FileTypeFilter.Add(".mp4");
    picker.FileTypeFilter.Add(".wmv");
    Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();   
    ```

3.  <span data-ttu-id="0ee80-159">**読み取りアクセス権をユーザーのファイルの選択を開いてのソースとしてファイル ストリームを設定して、** [ **MediaElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement)、し、ファイルを再生します。</span><span class="sxs-lookup"><span data-stu-id="0ee80-159">**Open the user's file selection for read access, and set the file stream as the source for the** [**MediaElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement), and then play the file.</span></span>
    ```cs
    if (file != null)
    {
        var stream = await file.OpenAsync(Windows.Storage.FileAccessMode.Read);
        VideoBox.SetSource(stream, file.ContentType);
        VideoBox.Stop();
        VideoBox.Play();
    }
    else
    {
        // No file selected. Handle the error here.
    }    
    ```
