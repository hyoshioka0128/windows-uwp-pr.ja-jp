---
ms.assetid: 8BDDE64A-77D2-4F9D-A1A0-E4C634BCD890
title: ピッカーによるファイルの保存
description: FileSavePicker を使って、アプリで保存するファイルの名前とその保存場所をユーザーが指定できるようにします。
ms.date: 12/19/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: c1480c17d97cb8b5e227cc44b384f13095bfd469
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369253"
---
# <a name="save-a-file-with-a-picker"></a><span data-ttu-id="9f033-104">ピッカーによるファイルの保存</span><span class="sxs-lookup"><span data-stu-id="9f033-104">Save a file with a picker</span></span>

<span data-ttu-id="9f033-105">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="9f033-105">**Important APIs**</span></span>

-   [<span data-ttu-id="9f033-106">**FileSavePicker**</span><span class="sxs-lookup"><span data-stu-id="9f033-106">**FileSavePicker**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker)
-   [<span data-ttu-id="9f033-107">**StorageFile**</span><span class="sxs-lookup"><span data-stu-id="9f033-107">**StorageFile**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile)

<span data-ttu-id="9f033-108">[  **FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) を使ってユーザーがアプリで保存するファイルの名前とその保存場所を指定できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9f033-108">Use [**FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) to let users specify the name and location where they want your app to save a file.</span></span>

> [!NOTE]
><span data-ttu-id="9f033-109"> 完全なサンプルを参照してください、[ファイル ピッカー サンプル](https://go.microsoft.com/fwlink/p/?linkid=619994)します。</span><span class="sxs-lookup"><span data-stu-id="9f033-109"> For a complete sample, see the [File picker sample](https://go.microsoft.com/fwlink/p/?linkid=619994).</span></span>

 

## <a name="prerequisites"></a><span data-ttu-id="9f033-110">前提条件</span><span class="sxs-lookup"><span data-stu-id="9f033-110">Prerequisites</span></span>


-   <span data-ttu-id="9f033-111">**ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングを理解します。**</span><span class="sxs-lookup"><span data-stu-id="9f033-111">**Understand async programming for Universal Windows Platform (UWP) apps**</span></span>

    <span data-ttu-id="9f033-112">C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="9f033-112">You can learn how to write asynchronous apps in C# or Visual Basic, see [Call asynchronous APIs in C# or Visual Basic](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic).</span></span> <span data-ttu-id="9f033-113">C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="9f033-113">To learn how to write asynchronous apps in C++, see [Asynchronous programming in C++](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps).</span></span>

-   <span data-ttu-id="9f033-114">**場所へのアクセス許可**</span><span class="sxs-lookup"><span data-stu-id="9f033-114">**Access permissions to the location**</span></span>

    <span data-ttu-id="9f033-115">「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="9f033-115">See [File access permissions](file-access-permissions.md).</span></span>

## <a name="filesavepicker-step-by-step"></a><span data-ttu-id="9f033-116">FileSavePicker: 手順</span><span class="sxs-lookup"><span data-stu-id="9f033-116">FileSavePicker: step-by-step</span></span>

<span data-ttu-id="9f033-117">[  **FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) を使って、ユーザーが保存するファイルの名前、種類、場所を指定できるようにします。</span><span class="sxs-lookup"><span data-stu-id="9f033-117">Use a [**FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) so that your users can specify the name, type, and location of a file to save.</span></span> <span data-ttu-id="9f033-118">ファイル ピッカー オブジェクトを作成、カスタマイズ、および表示し、選ばれたファイルを表す返された [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクトを使ってデータを保存します。</span><span class="sxs-lookup"><span data-stu-id="9f033-118">Create, customize, and show a file picker object, and then save data via the returned [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) object that represents the file picked.</span></span>

1.  <span data-ttu-id="9f033-119">**作成し、FileSavePicker をカスタマイズします。**</span><span class="sxs-lookup"><span data-stu-id="9f033-119">**Create and customize the FileSavePicker**</span></span>

    ```cs
    var savePicker = new Windows.Storage.Pickers.FileSavePicker();
    savePicker.SuggestedStartLocation =
        Windows.Storage.Pickers.PickerLocationId.DocumentsLibrary;
    // Dropdown of file types the user can save the file as
    savePicker.FileTypeChoices.Add("Plain Text", new List<string>() { ".txt" });
    // Default file name if the user does not type one in or select a file to replace
    savePicker.SuggestedFileName = "New Document";
    ```

<span data-ttu-id="9f033-120">ファイル ピッカー オブジェクトの、ユーザーとアプリに関連するプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="9f033-120">Set properties on the file picker object that are relevant to your users and your app.</span></span> <span data-ttu-id="9f033-121">この例は、3 つのプロパティを設定します。[**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedstartlocation)、 [ **FileTypeChoices** ](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.filetypechoices)と[ **SuggestedFileName**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedfilename)します。</span><span class="sxs-lookup"><span data-stu-id="9f033-121">This example sets three properties: [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedstartlocation), [**FileTypeChoices**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.filetypechoices) and [**SuggestedFileName**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedfilename).</span></span>
     
- <span data-ttu-id="9f033-122">このサンプルでは [**LocalFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) を使って、ドキュメントまたはテキスト ファイルを保存する場所として [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedstartlocation) をアプリのローカル フォルダーに設定しています。</span><span class="sxs-lookup"><span data-stu-id="9f033-122">Because our user is saving a document or text file, the sample sets [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedstartlocation) to the app's local folder by using [**LocalFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder).</span></span> <span data-ttu-id="9f033-123">[  **SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation) を保存するファイルの種類 (音楽、画像、ビデオ、ドキュメントなど) に適切な場所に設定します。</span><span class="sxs-lookup"><span data-stu-id="9f033-123">Set [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation) to a location appropriate for the type of file being saved, for example Music, Pictures, Videos, or Documents.</span></span> <span data-ttu-id="9f033-124">ユーザーは、開始場所から別の場所に移動できます。</span><span class="sxs-lookup"><span data-stu-id="9f033-124">From the start location, the user can navigate to other locations.</span></span>

- <span data-ttu-id="9f033-125">サンプルでは、保存したファイルを確実にアプリから開くことができるように、サポートするファイルの種類 (Microsoft Word 文書とテキスト ファイル) を [**FileTypeChoices**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.filetypechoices) を使って指定しています。</span><span class="sxs-lookup"><span data-stu-id="9f033-125">Because we want to make sure our app can open the file after it is saved, we use [**FileTypeChoices**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.filetypechoices) to specify file types that the sample supports (Microsoft Word documents and text files).</span></span> <span data-ttu-id="9f033-126">指定したすべてのファイルの種類をアプリはサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f033-126">Make sure all the file types that you specify are supported by your app.</span></span> <span data-ttu-id="9f033-127">ユーザーは、ファイルの種類を指定して保存できます。</span><span class="sxs-lookup"><span data-stu-id="9f033-127">Users will be able to save their file as any of the file types you specify.</span></span> <span data-ttu-id="9f033-128">また、別のファイルの種類を選んで、ファイルの種類を変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="9f033-128">They can also change the file type by selecting another of the file types that you specified.</span></span> <span data-ttu-id="9f033-129">既定では、リストの先頭にあるファイルの種類が選択されます。これを制御するには、[**DefaultFileExtension**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.defaultfileextension) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="9f033-129">The first file type choice in the list will be selected by default: to control that, set the [**DefaultFileExtension**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.defaultfileextension) property.</span></span>

    > [!NOTE]
    ><span data-ttu-id="9f033-130"> ファイル ピッカーは、選択したファイルの種類に一致するファイルの種類のみがユーザーに表示されるように、表示するファイルをフィルター処理にも、現在選択されているファイルの種類を使用します。</span><span class="sxs-lookup"><span data-stu-id="9f033-130"> The file picker also uses the currently selected file type to filter which files it displays, so that only file types that match the selected files types are displayed to the user.</span></span>

- <span data-ttu-id="9f033-131">ユーザーの入力の手間を多少なりとも軽減するために、この例では [**SuggestedFileName**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedfilename) を設定しています。</span><span class="sxs-lookup"><span data-stu-id="9f033-131">To save the user some typing, the example sets a [**SuggestedFileName**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.suggestedfilename).</span></span> <span data-ttu-id="9f033-132">提示するファイル名は、ユーザーが保存するファイルにできる限り関係のあるものにします。</span><span class="sxs-lookup"><span data-stu-id="9f033-132">Make your suggested file name relevant to the file being saved.</span></span> <span data-ttu-id="9f033-133">たとえば、Word のように、ファイルが既にある場合はその名前を提示し、まだ名前のないファイルを保存している場合はドキュメントの 1 行目を提示します。</span><span class="sxs-lookup"><span data-stu-id="9f033-133">For example, like Word, you can suggest the existing file name if there is one, or the first line of a document if the user is saving a file that does not yet have a name.</span></span>

> [!NOTE]
><span data-ttu-id="9f033-134"> [*\*FileSavePicker** ](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker)オブジェクトを表示、ファイル ピッカーを使用して、 [ *\*PickerViewMode.List** ](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerViewMode)表示モード。</span><span class="sxs-lookup"><span data-stu-id="9f033-134"> [*\*FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) objects display the file picker using the [*\*PickerViewMode.List**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerViewMode) view mode.</span></span>

2.  <span data-ttu-id="9f033-135">**FileSavePicker を表示し、選択されたファイルに保存**</span><span class="sxs-lookup"><span data-stu-id="9f033-135">**Show the FileSavePicker and save to the picked file**</span></span>

    <span data-ttu-id="9f033-136">ファイル ピッカーを表示するには、[**PickSaveFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.picksavefileasync) メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="9f033-136">Display the file picker by calling [**PickSaveFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.filesavepicker.picksavefileasync).</span></span> <span data-ttu-id="9f033-137">ユーザーが名前、ファイルの種類、場所を指定し、ファイルの保存を確定すると、**PickSaveFileAsync** は保存するファイルを表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="9f033-137">After the user specifies the name, file type, and location, and confirms to save the file, **PickSaveFileAsync** returns a [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) object that represents the saved file.</span></span> <span data-ttu-id="9f033-138">これでファイルの読み取りおよび書き込みアクセスが付与されるため、このファイルをキャプチャして処理できます。</span><span class="sxs-lookup"><span data-stu-id="9f033-138">You can capture and process this file now that you have read and write access to it.</span></span>

    ```cs
    Windows.Storage.StorageFile file = await savePicker.PickSaveFileAsync();
        if (file != null)
        {
            // Prevent updates to the remote version of the file until
            // we finish making changes and call CompleteUpdatesAsync.
            Windows.Storage.CachedFileManager.DeferUpdates(file);
            // write to file
            await Windows.Storage.FileIO.WriteTextAsync(file, file.Name);
            // Let Windows know that we're finished changing the file so
            // the other app can update the remote version of the file.
            // Completing updates may require Windows to ask for user input.
            Windows.Storage.Provider.FileUpdateStatus status =
                await Windows.Storage.CachedFileManager.CompleteUpdatesAsync(file);
            if (status == Windows.Storage.Provider.FileUpdateStatus.Complete)
            {
                this.textBlock.Text = "File " + file.Name + " was saved.";
            }
            else
            {
                this.textBlock.Text = "File " + file.Name + " couldn't be saved.";
            }
        }
        else
        {
            this.textBlock.Text = "Operation cancelled.";
        }
    ```

<span data-ttu-id="9f033-139">この例では、ファイルが有効であることをチェックし、ファイルにそのファイル名を書き込みます。</span><span class="sxs-lookup"><span data-stu-id="9f033-139">The example checks that the file is valid and writes its own file name into it.</span></span> <span data-ttu-id="9f033-140">また、「[ファイルの作成、書き込み、および読み取り](quickstart-reading-and-writing-files.md)」もご覧ください。</span><span class="sxs-lookup"><span data-stu-id="9f033-140">Also see [Creating, writing, and reading a file](quickstart-reading-and-writing-files.md).</span></span>

> [!TIP]
><span data-ttu-id="9f033-141"> 確認が有効で、他の処理を実行する前に保存したファイルを常に確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f033-141"> You should always check the saved file to make sure it is valid before you perform any other processing.</span></span> <span data-ttu-id="9f033-142">その後、アプリに適したコンテンツをファイルに保存できるほか、選ばれたファイルが有効でない場合は適切な動作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="9f033-142">Then, you can save content to the file as appropriate for your app, and provide appropriate behavior if the picked file is not valid.</span></span>
