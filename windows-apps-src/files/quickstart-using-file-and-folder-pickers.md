---
ms.assetid: F87DBE2F-77DB-4573-8172-29E11ABEFD34
title: ピッカーでファイルやフォルダーを開く
description: ユーザーがピッカーを操作してファイルやフォルダーにアクセスできるようにします。 ファイルへのアクセスには FileOpenPicker クラスと FileSavePicker クラス、フォルダーへのアクセスには FolderPicker を使います。
ms.date: 12/19/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 5d45c907215f21977b0a59acede5a8314d6ed168
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369325"
---
# <a name="open-files-and-folders-with-a-picker"></a><span data-ttu-id="c17d7-105">ピッカーでファイルやフォルダーを開く</span><span class="sxs-lookup"><span data-stu-id="c17d7-105">Open files and folders with a picker</span></span>

<span data-ttu-id="c17d7-106">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="c17d7-106">**Important APIs**</span></span>

-   [<span data-ttu-id="c17d7-107">**FileOpenPicker**</span><span class="sxs-lookup"><span data-stu-id="c17d7-107">**FileOpenPicker**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker)
-   [<span data-ttu-id="c17d7-108">**FolderPicker**</span><span class="sxs-lookup"><span data-stu-id="c17d7-108">**FolderPicker**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker)
-   [<span data-ttu-id="c17d7-109">**StorageFile**</span><span class="sxs-lookup"><span data-stu-id="c17d7-109">**StorageFile**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile)

<span data-ttu-id="c17d7-110">ユーザーがピッカーを操作してファイルやフォルダーにアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="c17d7-110">Access files and folders by letting the user interact with a picker.</span></span> <span data-ttu-id="c17d7-111">ファイルへのアクセスには [**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) クラスと [**FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) クラス、フォルダーへのアクセスには [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker) を使います。</span><span class="sxs-lookup"><span data-stu-id="c17d7-111">You can use the [**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) and [**FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) classes to access files, and the [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker) to access a folder.</span></span>

> [!NOTE]
><span data-ttu-id="c17d7-112"> 完全なサンプルを参照してください、[ファイル ピッカー サンプル](https://go.microsoft.com/fwlink/p/?linkid=619994)します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-112"> For a complete sample, see the [File picker sample](https://go.microsoft.com/fwlink/p/?linkid=619994).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c17d7-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="c17d7-113">Prerequisites</span></span>


-   <span data-ttu-id="c17d7-114">**ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングを理解します。**</span><span class="sxs-lookup"><span data-stu-id="c17d7-114">**Understand async programming for Universal Windows Platform (UWP) apps**</span></span>

    <span data-ttu-id="c17d7-115">C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c17d7-115">You can learn how to write asynchronous apps in C# or Visual Basic, see [Call asynchronous APIs in C# or Visual Basic](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic).</span></span> <span data-ttu-id="c17d7-116">C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c17d7-116">To learn how to write asynchronous apps in C++, see [Asynchronous programming in C++](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps).</span></span>

-   <span data-ttu-id="c17d7-117">**場所へのアクセス許可**</span><span class="sxs-lookup"><span data-stu-id="c17d7-117">**Access permissions to the location**</span></span>

    <span data-ttu-id="c17d7-118">「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c17d7-118">See [File access permissions](file-access-permissions.md).</span></span>

## <a name="file-picker-ui"></a><span data-ttu-id="c17d7-119">ファイル ピッカーの UI</span><span class="sxs-lookup"><span data-stu-id="c17d7-119">File picker UI</span></span>


<span data-ttu-id="c17d7-120">ファイル ピッカーには、ユーザーを指示する情報やユーザーがファイルを開くまたは保存するときの一貫したエクスペリエンスを提供する情報が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-120">A file picker displays information to orient users and provide a consistent experience when opening or saving files.</span></span>

<span data-ttu-id="c17d7-121">次の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-121">That information includes:</span></span>

-   <span data-ttu-id="c17d7-122">現在の場所</span><span class="sxs-lookup"><span data-stu-id="c17d7-122">The current location</span></span>
-   <span data-ttu-id="c17d7-123">ユーザーが選んだ項目</span><span class="sxs-lookup"><span data-stu-id="c17d7-123">The item or items that the user picked</span></span>
-   <span data-ttu-id="c17d7-124">ユーザーが参照できる場所のツリー。</span><span class="sxs-lookup"><span data-stu-id="c17d7-124">A tree of locations that the user can browse to.</span></span> <span data-ttu-id="c17d7-125">これらの場所には、ファイル システム上の場所 (音楽フォルダーやダウンロード フォルダーなど) のほか、ファイル ピッカー コントラクトを実装するアプリ (カメラ、フォト、Microsoft OneDrive など) も含まれます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-125">These locations include file system locations—such as the Music or Downloads folder—as well as apps that implement the file picker contract (such as Camera, Photos, and Microsoft OneDrive).</span></span>

<span data-ttu-id="c17d7-126">メール アプリで添付ファイルを選ぶ機能にファイル ピッカーが表示される場合もあります。</span><span class="sxs-lookup"><span data-stu-id="c17d7-126">An email app might display a file picker for the user to pick attachments.</span></span>

![2 つのファイルが開く対象として選ばれているファイル ピッカー。](images/picker-multifile-600px.png)

## <a name="how-pickers-work"></a><span data-ttu-id="c17d7-128">ピッカーのしくみ</span><span class="sxs-lookup"><span data-stu-id="c17d7-128">How pickers work</span></span>


<span data-ttu-id="c17d7-129">アプリでは、ファイル ピッカーを使ってユーザーのシステム上のファイルとフォルダーにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c17d7-129">With a picker your app can access, browse, and save files and folders on the user's system.</span></span> <span data-ttu-id="c17d7-130">アプリではこれらの選択を [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクトと [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) オブジェクトとして受け取ることにより、それらを操作できます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-130">Your app receives those picks as [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) and [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) objects, which you can then operate on.</span></span>

<span data-ttu-id="c17d7-131">ピッカーは単一の統一されたインターフェイスを使用して、ユーザーがファイル システムや他のアプリからファイルやフォルダーを選べるように表示します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-131">The picker uses a single, unified interface to let the user pick files and folders from the file system or from other apps.</span></span> <span data-ttu-id="c17d7-132">他のアプリから選ばれたファイルは、ファイル システムから選ばれたファイルと同様に、[**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクトとして返されます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-132">Files picked from other apps are like files from the file system: they are returned as [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) objects.</span></span> <span data-ttu-id="c17d7-133">通常、アプリはそれらのオブジェクトも、他のオブジェクトと同じ方法で操作できます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-133">In general, your app can operate on them in the same ways as other objects.</span></span> <span data-ttu-id="c17d7-134">他のアプリは、ファイル ピッカー コントラクトに参加することで、ユーザーにファイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-134">Other apps make files available by participating in file picker contracts.</span></span> <span data-ttu-id="c17d7-135">ファイル、保存場所、またはファイルの更新を他のアプリに提供する場合は、「[ファイル ピッカー コントラクトとの統合](https://docs.microsoft.com/previous-versions/windows/apps/hh465192(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c17d7-135">If you want your app to provide files, a save location, or file updates to other apps, see [Integrating with file picker contracts](https://docs.microsoft.com/previous-versions/windows/apps/hh465192(v=win.10)).</span></span>

<span data-ttu-id="c17d7-136">たとえば、ユーザーがファイルを開けるように、アプリでファイル ピッカーを呼び出すとします。</span><span class="sxs-lookup"><span data-stu-id="c17d7-136">For example, you might call the file picker in your app so that your user can open a file.</span></span> <span data-ttu-id="c17d7-137">この場合、アプリは呼び出し元アプリになります。</span><span class="sxs-lookup"><span data-stu-id="c17d7-137">This makes your app the calling app.</span></span> <span data-ttu-id="c17d7-138">ファイル ピッカーは、システムや他のアプリと情報をやり取りして、ユーザーがファイルを探して選べるようにします。</span><span class="sxs-lookup"><span data-stu-id="c17d7-138">The file picker interacts with the system and/or other apps to let the user navigate and pick the file.</span></span> <span data-ttu-id="c17d7-139">ユーザーがファイルを選ぶと、ファイル ピッカーはそのファイルをアプリに返します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-139">When your user chooses a file, the file picker returns that file to your app.</span></span> <span data-ttu-id="c17d7-140">ここでは、ユーザーが OneDrive のような提供元アプリからファイルを選ぶ場合のプロセスを示しています。</span><span class="sxs-lookup"><span data-stu-id="c17d7-140">Here's the process for the case of the user choosing a file from a providing app, such as OneDrive.</span></span>

![ファイル ピッカーを 2 つのアプリの間のインターフェイスとして使って、一方のアプリのファイルをもう一方のアプリから開くプロセスを示す図。](images/app-to-app-diagram-600px.png)

## <a name="pick-a-single-file-complete-code-listing"></a><span data-ttu-id="c17d7-142">1 つのファイルを選ぶ: 完全なコード</span><span class="sxs-lookup"><span data-stu-id="c17d7-142">Pick a single file: complete code listing</span></span>


```cs
var picker = new Windows.Storage.Pickers.FileOpenPicker();
picker.ViewMode = Windows.Storage.Pickers.PickerViewMode.Thumbnail;
picker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.PicturesLibrary;
picker.FileTypeFilter.Add(".jpg");
picker.FileTypeFilter.Add(".jpeg");
picker.FileTypeFilter.Add(".png");

Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();
if (file != null)
{
    // Application now has read/write access to the picked file
    this.textBlock.Text = "Picked photo: " + file.Name;
}
else
{
    this.textBlock.Text = "Operation cancelled.";
}
```

## <a name="pick-a-single-file-step-by-step"></a><span data-ttu-id="c17d7-143">1 つのファイルを選ぶ: ステップ バイ ステップ</span><span class="sxs-lookup"><span data-stu-id="c17d7-143">Pick a single file: step-by-step</span></span>


<span data-ttu-id="c17d7-144">ファイル ピッカーが動作するには、ファイル ピッカー オブジェクトを作成してカスタマイズし、ユーザーが項目を選べるようにそのファイル ピッカーを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c17d7-144">Using a file picker involves creating and customizing a file picker object, and then showing the file picker so the user can pick one or more items.</span></span>

1.  <span data-ttu-id="c17d7-145">**作成し、FileOpenPicker をカスタマイズします。**</span><span class="sxs-lookup"><span data-stu-id="c17d7-145">**Create and customize a FileOpenPicker**</span></span>

    ```cs
    var picker = new Windows.Storage.Pickers.FileOpenPicker();
    picker.ViewMode = Windows.Storage.Pickers.PickerViewMode.Thumbnail;
    picker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.PicturesLibrary;
    picker.FileTypeFilter.Add(".jpg");
    picker.FileTypeFilter.Add(".jpeg");
    picker.FileTypeFilter.Add(".png");
    ```
    <span data-ttu-id="c17d7-146">ファイル ピッカー オブジェクトの、ユーザーとアプリに関連するプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-146">Set properties on the file picker object relevant to your users and app.</span></span>

    <span data-ttu-id="c17d7-147">この例では、次の 3 つのプロパティを設定してから、ユーザーが選択できます便利な場所に画像の豊富なビジュアル表示を作成します。[**ViewMode**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.viewmode)、 [ **SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation)、および[ **FileTypeFilter**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.filetypefilter)します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-147">This example creates a rich, visual display of pictures in a convenient location that the user can pick from by setting three properties: [**ViewMode**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.viewmode), [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation), and [**FileTypeFilter**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.filetypefilter).</span></span>

    -   <span data-ttu-id="c17d7-148">設定[ **ViewMode** ](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.viewmode)を[ **PickerViewMode** ](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerViewMode) **サムネイル**列挙型の値は、豊富なを作成します。ファイル ピッカー内のファイルを表す画像の縮小表示を使用して表示します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-148">Setting [**ViewMode**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.viewmode) to the [**PickerViewMode**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerViewMode) **Thumbnail** enum value creates a rich, visual display by using picture thumbnails to represent files in the file picker.</span></span> <span data-ttu-id="c17d7-149">これは、画像やビデオなどの視覚的なファイルを選ぶ場合に設定します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-149">Do this for picking visual files such as pictures or videos.</span></span> <span data-ttu-id="c17d7-150">それ以外の場合は、[**PickerViewMode.List**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerViewMode) を使います。</span><span class="sxs-lookup"><span data-stu-id="c17d7-150">Otherwise, use [**PickerViewMode.List**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerViewMode).</span></span> <span data-ttu-id="c17d7-151">**画像またはビデオの添付**機能と**ドキュメントの添付**機能がある架空のメール アプリでは、ファイル ピッカーを表示する前に **ViewMode** をそれらの機能に対応させます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-151">A hypothetical email app with **Attach Picture or Video** and **Attach Document** features would set the **ViewMode** appropriate to the feature before showing the file picker.</span></span>

    -   <span data-ttu-id="c17d7-152">[  **PickerLocationId.PicturesLibrary**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerLocationId) を使って [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation) を Pictures に設定すると、画像を見つけられる可能性が高い場所が最初に表示されます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-152">Setting [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation) to Pictures using [**PickerLocationId.PicturesLibrary**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerLocationId) starts the user in a location where they're likely to find pictures.</span></span> <span data-ttu-id="c17d7-153">選ぶファイルの種類 (音楽、画像、ビデオ、ドキュメントなど) に合わせて **SuggestedStartLocation** を設定します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-153">Set **SuggestedStartLocation** to a location appropriate for the type of file being picked, for example Music, Pictures, Videos, or Documents.</span></span> <span data-ttu-id="c17d7-154">ユーザーは、開始場所から別の場所に移動できます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-154">From the start location, the user can navigate to other locations.</span></span>

    -   <span data-ttu-id="c17d7-155">[  **FileTypeFilter**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.filetypefilter) を使うと、関連性の高いファイルの種類に絞ってユーザーがファイルを選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="c17d7-155">Using [**FileTypeFilter**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.filetypefilter) to specify file types keeps the user focused on picking files that are relevant.</span></span> <span data-ttu-id="c17d7-156">**FileTypeFilter** の以前のファイルの種類を新しいエントリに置き換えるには、[**Add**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileextensionvector.append) ではなく [**ReplaceAll**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileextensionvector.replaceall) メソッドを使います。</span><span class="sxs-lookup"><span data-stu-id="c17d7-156">To replace previous file types in the **FileTypeFilter** with new entries, use [**ReplaceAll**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileextensionvector.replaceall) instead of [**Add**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileextensionvector.append).</span></span>

2.  <span data-ttu-id="c17d7-157">**FileOpenPicker を表示します。**</span><span class="sxs-lookup"><span data-stu-id="c17d7-157">**Show the FileOpenPicker**</span></span>

    - <span data-ttu-id="c17d7-158">**1 つのファイルを選択するには**</span><span class="sxs-lookup"><span data-stu-id="c17d7-158">**To pick a single file**</span></span>

        ```cs
        Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();
        if (file != null)
        {
            // Application now has read/write access to the picked file
            this.textBlock.Text = "Picked photo: " + file.Name;
        }
        else
        {
            this.textBlock.Text = "Operation cancelled.";
        }
        ```

    - <span data-ttu-id="c17d7-159">**複数のファイルを選択するには**</span><span class="sxs-lookup"><span data-stu-id="c17d7-159">**To pick multiple files**</span></span>  

        ```cs
        var files = await picker.PickMultipleFilesAsync();
        if (files.Count > 0)
        {
            StringBuilder output = new StringBuilder("Picked files:\n");
    
            // Application now has read/write access to the picked file(s)
            foreach (Windows.Storage.StorageFile file in files)
            {
                output.Append(file.Name + "\n");
            }
            this.textBlock.Text = output.ToString();
        }
        else
        {
            this.textBlock.Text = "Operation cancelled.";
        }
        ```

## <a name="pick-a-folder-complete-code-listing"></a><span data-ttu-id="c17d7-160">フォルダーを選ぶ: 完全なコード</span><span class="sxs-lookup"><span data-stu-id="c17d7-160">Pick a folder: complete code listing</span></span>


```cs
var folderPicker = new Windows.Storage.Pickers.FolderPicker();
folderPicker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.Desktop;
folderPicker.FileTypeFilter.Add("*");

Windows.Storage.StorageFolder folder = await folderPicker.PickSingleFolderAsync();
if (folder != null)
{
    // Application now has read/write access to all contents in the picked folder
    // (including other sub-folder contents)
    Windows.Storage.AccessCache.StorageApplicationPermissions.
    FutureAccessList.AddOrReplace("PickedFolderToken", folder);
    this.textBlock.Text = "Picked folder: " + folder.Name;
}
else
{
    this.textBlock.Text = "Operation cancelled.";
}
```

> [!TIP]
> <span data-ttu-id="c17d7-161">アプリがピッカーでファイルまたはフォルダーにアクセスするたびに、ファイルやフォルダーをアプリの [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) または [**MostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.mostrecentlyusedlist) に追加して、ファイルやフォルダーを追跡します。</span><span class="sxs-lookup"><span data-stu-id="c17d7-161">Whenever your app accesses a file or folder through a picker, add it to your app's [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) or [**MostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.mostrecentlyusedlist) to keep track of it.</span></span> <span data-ttu-id="c17d7-162">これらのリストの使用の詳細については、「[最近使ったファイルやフォルダーを追跡する方法](how-to-track-recently-used-files-and-folders.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c17d7-162">You can learn more about using these lists in [How to track recently-used files and folders](how-to-track-recently-used-files-and-folders.md).</span></span>