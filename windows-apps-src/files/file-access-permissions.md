---
ms.assetid: 3A404CC0-A997-45C8-B2E8-44745539759D
title: ファイル アクセス許可
description: アプリは既定でファイル システムの特定の場所にアクセスできます。 また、ファイル ピッカーの使用や機能の宣言によって、その他の場所にアクセスすることもできます。
ms.date: 12/19/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
dev_langs:
- csharp
- cppwinrt
- cpp
- javascript
ms.openlocfilehash: 1473d93bc10f50bf361f92f753adb786e502fc3a
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369435"
---
# <a name="file-access-permissions"></a><span data-ttu-id="41f67-105">ファイル アクセス許可</span><span class="sxs-lookup"><span data-stu-id="41f67-105">File access permissions</span></span>

<span data-ttu-id="41f67-106">ユニバーサル Windows プラットフォーム (UWP) アプリでは、既定では、特定のファイル システムの場所をアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-106">Universal Windows Platform (UWP) apps can access certain file system locations by default.</span></span> <span data-ttu-id="41f67-107">また、ファイル ピッカーの使用や機能の宣言によって、その他の場所にアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-107">Apps can also access additional locations through the file picker, or by declaring capabilities.</span></span>

## <a name="the-locations-that-all-apps-can-access"></a><span data-ttu-id="41f67-108">すべてのアプリからアクセスできる場所</span><span class="sxs-lookup"><span data-stu-id="41f67-108">The locations that all apps can access</span></span>

<span data-ttu-id="41f67-109">新しいアプリを作成すると、既定でファイル システムの次の場所にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-109">When you create a new app, you can access the following file system locations by default:</span></span>

### <a name="application-install-directory"></a><span data-ttu-id="41f67-110">アプリケーションのインストール ディレクトリ</span><span class="sxs-lookup"><span data-stu-id="41f67-110">Application install directory</span></span>
<span data-ttu-id="41f67-111">ユーザーのシステムで、アプリがインストールされているフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="41f67-111">The folder where your app is installed on the user's system.</span></span>

<span data-ttu-id="41f67-112">ファイルにアクセスする 2 つの主な方法があるし、フォルダーが、アプリのインストール ディレクトリ。</span><span class="sxs-lookup"><span data-stu-id="41f67-112">There are two primary ways to access files and folders in your app's install directory:</span></span>

1. <span data-ttu-id="41f67-113">次のように、アプリのインストール ディレクトリを表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) を取得できます。</span><span class="sxs-lookup"><span data-stu-id="41f67-113">You can retrieve a [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) that represents your app's install directory, like this:</span></span>

    ```csharp
    Windows.Storage.StorageFolder installedLocation = Windows.ApplicationModel.Package.Current.InstalledLocation;
    ```
    
    ```javascript
    var installDirectory = Windows.ApplicationModel.Package.current.installedLocation;
    ```
    
    ```cppwinrt
    #include <winrt/Windows.Storage.h>
    ...
    Windows::Storage::StorageFolder installedLocation{ Windows::ApplicationModel::Package::Current().InstalledLocation() };
    ```
    
    ```cpp
    Windows::Storage::StorageFolder^ installedLocation = Windows::ApplicationModel::Package::Current->InstalledLocation;
    ```

    <span data-ttu-id="41f67-114">[  **StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) メソッドを使って、ディレクトリ内のファイルとフォルダーにアクセスすることができます。</span><span class="sxs-lookup"><span data-stu-id="41f67-114">You can then access files and folders in the directory using [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) methods.</span></span> <span data-ttu-id="41f67-115">上の例では、この **StorageFolder** が `installDirectory` 変数に格納されています。</span><span class="sxs-lookup"><span data-stu-id="41f67-115">In the example, this **StorageFolder** is stored in the `installDirectory` variable.</span></span> <span data-ttu-id="41f67-116">アプリ パッケージやインストール ディレクトリの操作について詳しくは、GitHub にある[アプリ パッケージ情報のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Package)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-116">You can learn more about working with your app package and install directory from the [App package information sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Package) on GitHub.</span></span>

2. <span data-ttu-id="41f67-117">次のように、アプリの URI を使って、アプリのインストール ディレクトリからファイルを直接取得できます。</span><span class="sxs-lookup"><span data-stu-id="41f67-117">You can retrieve a file directly from your app's install directory by using an app URI, like this:</span></span>

    ```csharp
    using Windows.Storage;            
    StorageFile file = await StorageFile.GetFileFromApplicationUriAsync(new Uri("ms-appx:///file.txt"));
    ```
    
    ```javascript
    Windows.Storage.StorageFile.getFileFromApplicationUriAsync("ms-appx:///file.txt").done(
        function(file) {
            // Process file
        }
    );
    ```
    
    ```cppwinrt
    Windows::Foundation::IAsyncAction ExampleCoroutineAsync()
    {
        Windows::Storage::StorageFile file{
            co_await Windows::Storage::StorageFile::GetFileFromApplicationUriAsync(Windows::Foundation::Uri{L"ms-appx:///file.txt"})
        };
        // Process file
    }
    ```
    
    ```cpp
    auto getFileTask = create_task(StorageFile::GetFileFromApplicationUriAsync(ref new Uri("ms-appx:///file.txt")));
    getFileTask.then([](StorageFile^ file) 
    {
        // Process file
    });
    ```

    <span data-ttu-id="41f67-118">[  **GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync) が完了すると、アプリのインストール ディレクトリにある `file.txt` ファイル (この例では `file`) を表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) が返されます。</span><span class="sxs-lookup"><span data-stu-id="41f67-118">When [**GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync) completes, it returns a [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) that represents the `file.txt` file in the app's install directory (`file` in the example).</span></span>
    
    <span data-ttu-id="41f67-119">URI の "ms-appx:///" プレフィックスは、アプリのインストール ディレクトリを参照します。</span><span class="sxs-lookup"><span data-stu-id="41f67-119">The "ms-appx:///" prefix in the URI refers to the app's install directory.</span></span> <span data-ttu-id="41f67-120">アプリの URI の使用について詳しくは、「[URI を使ってコンテンツを参照する方法](https://docs.microsoft.com/previous-versions/windows/apps/hh781215(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-120">You can learn more about using app URIs in [How to use URIs to reference content](https://docs.microsoft.com/previous-versions/windows/apps/hh781215(v=win.10)).</span></span>

<span data-ttu-id="41f67-121">さらに、他の場所とは異なり、[ユニバーサル Windows プラットフォーム (UWP) アプリの Win32 と COM](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) や [Microsoft Visual Studio の C/C++ 標準ライブラリ関数](https://docs.microsoft.com/cpp/cpp/c-cpp-language-and-standard-libraries)を使ってアプリのインストール ディレクトリ内のファイルにアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-121">In addition, and unlike other locations, you can also access files in your app install directory by using some [Win32 and COM for Universal Windows Platform (UWP) apps](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) and some [C/C++ Standard Library functions from Microsoft Visual Studio](https://docs.microsoft.com/cpp/cpp/c-cpp-language-and-standard-libraries).</span></span>

<span data-ttu-id="41f67-122">アプリのインストール ディレクトリは読み取り専用です。</span><span class="sxs-lookup"><span data-stu-id="41f67-122">The app's install directory is a read-only location.</span></span> <span data-ttu-id="41f67-123">ファイル ピッカーでは、インストール ディレクトリへのアクセスを得ることはできません。</span><span class="sxs-lookup"><span data-stu-id="41f67-123">You can't gain access to the install directory through the file picker.</span></span>

### <a name="application-data-locations"></a><span data-ttu-id="41f67-124">アプリケーション データの場所</span><span class="sxs-lookup"><span data-stu-id="41f67-124">Application data locations</span></span>
<span data-ttu-id="41f67-125">アプリがデータを保存できるフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="41f67-125">The folders where your app can store data.</span></span> <span data-ttu-id="41f67-126">これらのフォルダー (ローカル、移動、一時) は、アプリのインストール時に作成されます。</span><span class="sxs-lookup"><span data-stu-id="41f67-126">These folders (local, roaming and temporary) are created when your app is installed.</span></span>

<span data-ttu-id="41f67-127">アプリのデータの場所からファイルとフォルダーにアクセスする 2 つの主な方法があります。</span><span class="sxs-lookup"><span data-stu-id="41f67-127">There are two primary ways to access files and folders from your app's data locations:</span></span>

1.  <span data-ttu-id="41f67-128">[  **ApplicationData**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData) プロパティを使ってアプリ データ フォルダーを取得します。</span><span class="sxs-lookup"><span data-stu-id="41f67-128">Use [**ApplicationData**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData) properties to retrieve an app data folder.</span></span>

    <span data-ttu-id="41f67-129">たとえば、次のように、[**ApplicationData**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData).[**LocalFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) を使って、アプリのローカル フォルダーを表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) を取得できます。</span><span class="sxs-lookup"><span data-stu-id="41f67-129">For example, you can use [**ApplicationData**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData).[**LocalFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) to retrieve a [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) that represents your app's local folder like this:</span></span>
    
    ```csharp
    using Windows.Storage;
    StorageFolder localFolder = ApplicationData.Current.LocalFolder;
    ```
    
    ```javascript
    var localFolder = Windows.Storage.ApplicationData.current.localFolder;
    ```
    
    ```cppwinrt
    Windows::Storage::StorageFolder storageFolder{
        Windows::Storage::ApplicationData::Current().LocalFolder()
    };
    ```
    
    ```cpp
    using namespace Windows::Storage;
    StorageFolder^ storageFolder = ApplicationData::Current->LocalFolder;
    ```
    
    <span data-ttu-id="41f67-130">アプリの移動フォルダーまたは一時フォルダーにアクセスする場合は、[**RoamingFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingfolder) プロパティまたは [**TemporaryFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) プロパティを使います。</span><span class="sxs-lookup"><span data-stu-id="41f67-130">If you want to access your app's roaming or temporary folder, use the [**RoamingFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingfolder) or [**TemporaryFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) property instead.</span></span>
    
    <span data-ttu-id="41f67-131">アプリ データの場所を表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) を取得したら、**StorageFolder** メソッドを使って、その場所にあるファイルやフォルダーにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-131">After you retrieve a [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) that represents an app data location, you can access files and folders in that location by using **StorageFolder** methods.</span></span> <span data-ttu-id="41f67-132">上の例では、これらの **StorageFolder** オブジェクトが `localFolder` 変数に格納されています。</span><span class="sxs-lookup"><span data-stu-id="41f67-132">In the example, these **StorageFolder** objects are stored in the `localFolder` variable.</span></span> <span data-ttu-id="41f67-133">アプリ データの場所の使用について詳しくは、[ApplicationData クラス](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata)のページのガイダンスをご覧ください。また、GitHub から[アプリケーション データ サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ApplicationData)をダウンロードしてご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-133">You can learn more about using app data locations from the guidance on the [ApplicationData class](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata) page, and by downloading the [Application data sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ApplicationData) from GitHub.</span></span>

2. <span data-ttu-id="41f67-134">このようなアプリの URI を使用して、アプリのローカル フォルダーから直接ファイルを取得できます。</span><span class="sxs-lookup"><span data-stu-id="41f67-134">You can retrieve a file directly from your app's local folder by using an app URI, like this:</span></span>
    
    ```csharp
    using Windows.Storage;
    StorageFile file = await StorageFile.GetFileFromApplicationUriAsync(new Uri("ms-appdata:///local/file.txt"));
    ```
    
    ```javascript
    Windows.Storage.StorageFile.getFileFromApplicationUriAsync("ms-appdata:///local/file.txt").done(
        function(file) {
            // Process file
        }
    );
    ```
    
    ```cppwinrt
    Windows::Storage::StorageFile file{
        co_await Windows::Storage::StorageFile::GetFileFromApplicationUriAsync(Windows::Foundation::Uri{ L"ms-appdata:///local/file.txt" })
    };
    // Process file
    ```
    
    ```cpp
    using Windows::Storage;
    auto getFileTask = create_task(StorageFile::GetFileFromApplicationUriAsync(ref new Uri("ms-appdata:///local/file.txt")));
    getFileTask.then([](StorageFile^ file) 
    {
        // Process file
    });
    ```
    
    <span data-ttu-id="41f67-135">[  **GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync) が完了すると、アプリのローカル フォルダーにある `file.txt` ファイル (この例では `file`) を表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) が返されます。</span><span class="sxs-lookup"><span data-stu-id="41f67-135">When [**GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync) completes, it returns a [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) that represents the `file.txt` file in the app's local folder (`file` in the example).</span></span>
    
    <span data-ttu-id="41f67-136">URI の "ms-appdata:///local/" プレフィックスは、アプリのローカル フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="41f67-136">The "ms-appdata:///local/" prefix in the URI refers to the app's local folder.</span></span> <span data-ttu-id="41f67-137">アプリの移動フォルダーまたは一時フォルダーにあるファイルにアクセスするには、"ms-appdata:///roaming/" または "ms-appdata:///temporary/" を使います。</span><span class="sxs-lookup"><span data-stu-id="41f67-137">To access files in the app's roaming or temporary folders use "ms-appdata:///roaming/" or "ms-appdata:///temporary/" instead.</span></span> <span data-ttu-id="41f67-138">アプリの URI の使用について詳しくは、「[ファイル リソースを読み込む方法](https://docs.microsoft.com/previous-versions/windows/apps/hh781229(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-138">You can learn more about using app URIs in [How to load file resources](https://docs.microsoft.com/previous-versions/windows/apps/hh781229(v=win.10)).</span></span>

<span data-ttu-id="41f67-139">さらに、他の場所とは異なり、[UWP アプリの Win32 と COM](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) や Visual Studio の C/C++ 標準ライブラリ関数を使ってアプリ データの場所にあるファイルにアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-139">In addition, and unlike other locations, you can also access files in your app data locations by using some [Win32 and COM for UWP apps](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) and some C/C++ Standard Library functions from Visual Studio.</span></span>

<span data-ttu-id="41f67-140">ファイル ピッカーでは、ローカル、移動、または一時フォルダーにアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="41f67-140">You can't access the local, roaming, or temporary folders through the file picker.</span></span>

### <a name="removable-devices"></a><span data-ttu-id="41f67-141">リムーバブル デバイス</span><span class="sxs-lookup"><span data-stu-id="41f67-141">Removable devices</span></span>
<span data-ttu-id="41f67-142">さらに、接続されているデバイス上の一部のファイルに既定でアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-142">Additionally, your app can access some of the files on connected devices by default.</span></span> <span data-ttu-id="41f67-143">これは、[自動再生拡張機能](https://docs.microsoft.com/previous-versions/windows/apps/hh464906(v=win.10))を使って、ユーザーがデバイス (カメラや USB サム ドライブなど) をシステムに接続したときに自動的に起動されるようにする場合に使うことができます。</span><span class="sxs-lookup"><span data-stu-id="41f67-143">This is an option if your app uses the [AutoPlay extension](https://docs.microsoft.com/previous-versions/windows/apps/hh464906(v=win.10)) to launch automatically when users connect a device, like a camera or USB thumb drive, to their system.</span></span> <span data-ttu-id="41f67-144">アプリでアクセスできるファイルの種類は、アプリ マニフェストのファイルの種類の関連付けの宣言で指定されたものだけに制限されます。</span><span class="sxs-lookup"><span data-stu-id="41f67-144">The files your app can access are limited to specific file types that are specified via File Type Association declarations in your app manifest.</span></span>

<span data-ttu-id="41f67-145">もちろん、ファイル ピッカー ([**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) と [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker)) を呼び出して、アプリでアクセスするファイルやフォルダーをユーザーが選べるようにすると、リムーバブル デバイス上のファイルやフォルダーにもアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="41f67-145">Of course, you can also gain access to files and folders on a removable device by calling the file picker (using [**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) and [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker)) and letting the user pick files and folders for your app to access.</span></span> <span data-ttu-id="41f67-146">ファイル ピッカーの使い方については、「[ピッカーでファイルやフォルダーを開く](quickstart-using-file-and-folder-pickers.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-146">Learn how to use the file picker in [Open files and folders with a picker](quickstart-using-file-and-folder-pickers.md).</span></span>

> [!NOTE]
> <span data-ttu-id="41f67-147">SD カードやその他のリムーバブル デバイスにアクセスする方法について詳しくは、「[SD カードへのアクセス](access-the-sd-card.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-147">For more info about accessing an SD card or other removable devices, see [Access the SD card](access-the-sd-card.md).</span></span>

## <a name="locations-that-uwp-apps-can-access"></a><span data-ttu-id="41f67-148">UWP アプリにアクセスできる場所</span><span class="sxs-lookup"><span data-stu-id="41f67-148">Locations that UWP apps can access</span></span>
### <a name="users-downloads-folder"></a><span data-ttu-id="41f67-149">ユーザーの [ダウンロード] フォルダー</span><span class="sxs-lookup"><span data-stu-id="41f67-149">User's Downloads folder</span></span>

<span data-ttu-id="41f67-150">ダウンロードされたファイルが保存される既定のフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="41f67-150">The folder where downloaded files are saved by default.</span></span>

<span data-ttu-id="41f67-151">既定では、ユーザーの "ダウンロード" フォルダーにあるファイルやフォルダーについては、そのアプリで作成したものにしかアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="41f67-151">By default, your app can only access files and folders in the user's Downloads folder that your app created.</span></span> <span data-ttu-id="41f67-152">ただし、ファイル ピッカー ([**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) または [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker)) を呼び出して、アプリでアクセスするファイルやフォルダーをユーザーが参照して選べるようにすると、ユーザーの "ダウンロード" フォルダーにあるファイルやフォルダーにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="41f67-152">However, you can gain access to files and folders in the user's Downloads folder by calling a file picker ([**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) or [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker)) so that users can navigate and pick files or folders for your app to access.</span></span>

- <span data-ttu-id="41f67-153">次のように、ユーザーの "ダウンロード" フォルダーにファイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="41f67-153">You can create a file in the user's Downloads folder like this:</span></span>

    ```csharp
    using Windows.Storage;
    StorageFile newFile = await DownloadsFolder.CreateFileAsync("file.txt");
    ```
    
    ```javascript
    Windows.Storage.DownloadsFolder.createFileAsync("file.txt").done(
        function(newFile) {
            // Process file
        }
    );
    ```
    
    ```cppwinrt
    Windows::Storage::StorageFile newFile{
        co_await Windows::Storage::DownloadsFolder::CreateFileAsync(L"file.txt")
    };
    // Process file
    ```
    
    ```cpp
    using Windows::Storage;
    auto createFileTask = create_task(DownloadsFolder::CreateFileAsync(L"file.txt"));
    createFileTask.then([](StorageFile^ newFile)
    {
        // Process file
    });
    ```

    <span data-ttu-id="41f67-154">[**DownloadsFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.DownloadsFolder).[**CreateFileAsync** ](https://docs.microsoft.com/uwp/api/windows.storage.downloadsfolder.createfileasync)システムで行う必要がありますを指定できるようにオーバー ロードは、同じ名前を持つ Downloads フォルダーが既に既存のファイルがある場合。</span><span class="sxs-lookup"><span data-stu-id="41f67-154">[**DownloadsFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.DownloadsFolder).[**CreateFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.downloadsfolder.createfileasync) is overloaded so that you can specify what the system should do if there is already an existing file in the Downloads folder that has the same name.</span></span> <span data-ttu-id="41f67-155">これらのメソッドが完了すると、作成されたファイルを表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) が返されます。</span><span class="sxs-lookup"><span data-stu-id="41f67-155">When these methods complete, they return a [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) that represents the file that was created.</span></span> <span data-ttu-id="41f67-156">上の例では、このファイルの名前は `newFile` です。</span><span class="sxs-lookup"><span data-stu-id="41f67-156">This file is called `newFile` in the example.</span></span>

- <span data-ttu-id="41f67-157">次のように、ユーザーの "ダウンロード" フォルダーにサブフォルダーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="41f67-157">You can create a subfolder in the user's Downloads folder like this:</span></span>

    ```csharp
    using Windows.Storage;
    StorageFolder newFolder = await DownloadsFolder.CreateFolderAsync("New Folder");
    ```
    
    ```javascript
    Windows.Storage.DownloadsFolder.createFolderAsync("New Folder").done(
        function(newFolder) {
            // Process folder
        }
    );
    ```
    
    ```cppwinrt
    Windows::Storage::StorageFolder newFolder{
        co_await Windows::Storage::DownloadsFolder::CreateFolderAsync(L"New Folder")
    };
    // Process folder
    ```
    
    ```cpp
    using Windows::Storage;
    auto createFolderTask = create_task(DownloadsFolder::CreateFolderAsync(L"New Folder"));
    createFolderTask.then([](StorageFolder^ newFolder)
    {
        // Process folder
    });
    ```

    <span data-ttu-id="41f67-158">[**DownloadsFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.DownloadsFolder).[**CreateFolderAsync** ](https://docs.microsoft.com/uwp/api/windows.storage.downloadsfolder.createfolderasync)システムで行う必要がありますを指定できるようにオーバー ロードは、同じ名前を持つ Downloads フォルダーが既に既存のサブフォルダーがある場合。</span><span class="sxs-lookup"><span data-stu-id="41f67-158">[**DownloadsFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.DownloadsFolder).[**CreateFolderAsync**](https://docs.microsoft.com/uwp/api/windows.storage.downloadsfolder.createfolderasync) is overloaded so that you can specify what the system should do if there is already an existing subfolder in the Downloads folder that has the same name.</span></span> <span data-ttu-id="41f67-159">これらのメソッドが完了すると、作成されたサブフォルダーを表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) が返されます。</span><span class="sxs-lookup"><span data-stu-id="41f67-159">When these methods complete, they return a [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) that represents the subfolder that was created.</span></span> <span data-ttu-id="41f67-160">上の例では、このファイルの名前は `newFolder` です。</span><span class="sxs-lookup"><span data-stu-id="41f67-160">This file is called `newFolder` in the example.</span></span>

<span data-ttu-id="41f67-161">"ダウンロード" フォルダーにファイルやフォルダーを作成する場合は、以降に簡単にアクセスできるように、その項目をアプリの [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) に追加することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="41f67-161">If you create a file or folder in the Downloads folder, we recommend that you add that item to your app's [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) so that your app can readily access that item in the future.</span></span>

## <a name="accessing-additional-locations"></a><span data-ttu-id="41f67-162">その他の場所へのアクセス</span><span class="sxs-lookup"><span data-stu-id="41f67-162">Accessing additional locations</span></span>

<span data-ttu-id="41f67-163">アプリで、既定の場所以外にあるファイルやフォルダーにアクセスするには、アプリ マニフェストで機能を宣言するか、ファイル ピッカーを呼び出してアプリでアクセスするファイルやフォルダーをユーザーが選べるようにします。詳しくは、「[アプリ機能の宣言](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)」または「[ピッカーでファイルやフォルダーを開く](quickstart-using-file-and-folder-pickers.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-163">In addition to the default locations, an app can access additional files and folders by declaring capabilities in the app manifest (see [App capability declarations](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)), or by calling a file picker to let the user pick files and folders for the app to access (see [Open files and folders with a picker](quickstart-using-file-and-folder-pickers.md)).</span></span>

<span data-ttu-id="41f67-164">[AppExecutionAlias](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-appexecutionalias) 拡張機能を宣言したアプリには、コンソール ウィンドウでアプリが起動されたディレクトリおよびその下位レベルのディレクトリに対する、ファイル システムのアクセス許可が与えられます。</span><span class="sxs-lookup"><span data-stu-id="41f67-164">App's that that declare the [AppExecutionAlias](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-appexecutionalias) extension, have file-system permissions from the directory that they are launched from in the console window, and downwards.</span></span>

<span data-ttu-id="41f67-165">次の表に、機能の宣言や関連付けられた [**Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage) API の使用によってアクセスできるその他の場所を示します。</span><span class="sxs-lookup"><span data-stu-id="41f67-165">The following table lists additional locations that you can access by declaring a capability (or capabilities) and using the associated [**Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage) API:</span></span>

| <span data-ttu-id="41f67-166">Location</span><span class="sxs-lookup"><span data-stu-id="41f67-166">Location</span></span> | <span data-ttu-id="41f67-167">機能</span><span class="sxs-lookup"><span data-stu-id="41f67-167">Capability</span></span> | <span data-ttu-id="41f67-168">Windows.Storage API</span><span class="sxs-lookup"><span data-stu-id="41f67-168">Windows.Storage API</span></span> |
|----------|------------|---------------------|
| <span data-ttu-id="41f67-169">ユーザーがアクセス権を持つすべてのファイル。</span><span class="sxs-lookup"><span data-stu-id="41f67-169">All files that the user has access to.</span></span> <span data-ttu-id="41f67-170">例: ドキュメント、画像、写真、ダウンロード、デスクトップ、OneDrive などです。</span><span class="sxs-lookup"><span data-stu-id="41f67-170">For example: documents, pictures, photos, downloads, desktop, OneDrive, etc.</span></span> | <span data-ttu-id="41f67-171">broadFileSystemAccess</span><span class="sxs-lookup"><span data-stu-id="41f67-171">broadFileSystemAccess</span></span><br><br><span data-ttu-id="41f67-172">これは、制限付き機能です。</span><span class="sxs-lookup"><span data-stu-id="41f67-172">This is a restricted capability.</span></span> <span data-ttu-id="41f67-173">アクセス**設定** > **プライバシー** > **ファイル システム**します。</span><span class="sxs-lookup"><span data-stu-id="41f67-173">Access is configurable in **Settings** > **Privacy** > **File system**.</span></span> <span data-ttu-id="41f67-174">ユーザーが許可または拒否でいつでものため**設定**アプリがこれらの変更に回復力のあることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="41f67-174">Because users can grant or deny the permission any time in **Settings**, you should ensure that your app is resilient to those changes.</span></span> <span data-ttu-id="41f67-175">アプリにアクセスがないことを発見した場合へのリンクを提供することで、設定を変更するユーザー入力を求めることができます、 [Windows 10 のファイル システム アクセスとプライバシー](https://privacy.microsoft.com/en-US/windows-10-file-system-access-and-privacy)記事。</span><span class="sxs-lookup"><span data-stu-id="41f67-175">If you find that your app does not have access, you may choose to prompt the user to change the setting by providing a link to the [Windows 10 file system access and privacy](https://privacy.microsoft.com/en-US/windows-10-file-system-access-and-privacy) article.</span></span> <span data-ttu-id="41f67-176">いるユーザー必要があります、アプリを閉じるの設定を切り替えるアプリを再起動します。</span><span class="sxs-lookup"><span data-stu-id="41f67-176">Note that the user must close the app, toggle the setting, and restart the app.</span></span> <span data-ttu-id="41f67-177">場合は、アプリの実行中に、設定を切り替えますが、状態を保存して、新しい設定を適用するために、アプリを強制的に終了するように、プラットフォームは、アプリを中断します。</span><span class="sxs-lookup"><span data-stu-id="41f67-177">If they toggle the setting while the app is running, the platform will suspend your app so that you can save the state, then forcibly terminate the app in order to apply the new setting.</span></span> <span data-ttu-id="41f67-178">2018 年 4 月の更新プログラムでは、アクセス許可の既定値には。</span><span class="sxs-lookup"><span data-stu-id="41f67-178">In the April 2018 update, the default for the permission is On.</span></span> <span data-ttu-id="41f67-179">2018 の年 10 月の更新プログラムでは、既定値は、オフは。</span><span class="sxs-lookup"><span data-stu-id="41f67-179">In the October 2018 update, the default is Off.</span></span><br /><br /><span data-ttu-id="41f67-180">この機能を宣言するアプリを Microsoft Store に提出する場合、アプリでこの機能が必要となる理由およびこの機能の使用目的に関する追加の説明を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="41f67-180">If you submit an app to the Store that declares this capability, you will need to supply additional descriptions of why your app needs this capability, and how it intends to use it.</span></span><br><span data-ttu-id="41f67-181">この機能は、Api での[ **Windows.Storage** ](https://docs.microsoft.com/uwp/api/Windows.Storage)名前空間。</span><span class="sxs-lookup"><span data-stu-id="41f67-181">This capability works for APIs in the [**Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage) namespace.</span></span> <span data-ttu-id="41f67-182">参照してください、**例**アプリでこの機能を有効にする方法の例は、この記事の最後のセクション。</span><span class="sxs-lookup"><span data-stu-id="41f67-182">See the **Example** section at the end of this article for an example of how to enable this capability in your app.</span></span> | <span data-ttu-id="41f67-183">なし</span><span class="sxs-lookup"><span data-stu-id="41f67-183">n/a</span></span> |
| <span data-ttu-id="41f67-184">Documents</span><span class="sxs-lookup"><span data-stu-id="41f67-184">Documents</span></span> | <span data-ttu-id="41f67-185">DocumentsLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-185">DocumentsLibrary</span></span> <br><br><span data-ttu-id="41f67-186">注:この場所で、アプリにアクセスできる特定のファイルの種類を宣言できるアプリケーション マニフェスト ファイルの種類の関連付けを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="41f67-186">Note: You must add File Type Associations to your app manifest that declare specific file types that your app can access in this location.</span></span> <br><br><span data-ttu-id="41f67-187">この機能は、アプリが次の条件を満たす場合に使います。</span><span class="sxs-lookup"><span data-stu-id="41f67-187">Use this capability if your app:</span></span><br><span data-ttu-id="41f67-188">- 有効な OneDrive URL またはリソース ID を使った、特定の OneDrive コンテンツへのクロスプラットフォーム オフライン アクセスを容易にする</span><span class="sxs-lookup"><span data-stu-id="41f67-188">- Facilitates cross-platform offline access to specific OneDrive content using valid OneDrive URLs or Resource IDs</span></span><br><span data-ttu-id="41f67-189">保存中に自動的にユーザーの OneDrive にファイルを開くオフライン</span><span class="sxs-lookup"><span data-stu-id="41f67-189">- Saves open files to the user's OneDrive automatically while offline</span></span> | [<span data-ttu-id="41f67-190">KnownFolders.DocumentsLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-190">KnownFolders.DocumentsLibrary</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.documentslibrary) |
| <span data-ttu-id="41f67-191">音楽</span><span class="sxs-lookup"><span data-stu-id="41f67-191">Music</span></span>     | <span data-ttu-id="41f67-192">MusicLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-192">MusicLibrary</span></span> <br><span data-ttu-id="41f67-193">「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md)」もご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-193">Also see [Files and folders in the Music, Pictures, and Videos libraries](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md).</span></span> | [<span data-ttu-id="41f67-194">KnownFolders.MusicLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-194">KnownFolders.MusicLibrary</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.musiclibrary) |    
| <span data-ttu-id="41f67-195">画像</span><span class="sxs-lookup"><span data-stu-id="41f67-195">Pictures</span></span>  | <span data-ttu-id="41f67-196">PicturesLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-196">PicturesLibrary</span></span><br> <span data-ttu-id="41f67-197">「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md)」もご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-197">Also see [Files and folders in the Music, Pictures, and Videos libraries](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md).</span></span> | [<span data-ttu-id="41f67-198">KnownFolders.PicturesLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-198">KnownFolders.PicturesLibrary</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.pictureslibrary) |  
| <span data-ttu-id="41f67-199">ビデオ</span><span class="sxs-lookup"><span data-stu-id="41f67-199">Videos</span></span>    | <span data-ttu-id="41f67-200">VideosLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-200">VideosLibrary</span></span><br><span data-ttu-id="41f67-201">「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md)」もご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-201">Also see [Files and folders in the Music, Pictures, and Videos libraries](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md).</span></span> | [<span data-ttu-id="41f67-202">KnownFolders.VideosLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-202">KnownFolders.VideosLibrary</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.videoslibrary) |   
| <span data-ttu-id="41f67-203">リムーバブル デバイス</span><span class="sxs-lookup"><span data-stu-id="41f67-203">Removable devices</span></span>  | <span data-ttu-id="41f67-204">RemovableDevices</span><span class="sxs-lookup"><span data-stu-id="41f67-204">RemovableDevices</span></span> <br><br><span data-ttu-id="41f67-205">注  アプリ マニフェストにファイルの種類の関連付けを追加し、この場所でアプリがアクセスできるファイルの種類を具体的に宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="41f67-205">Note  You must add File Type Associations to your app manifest that declare specific file types that your app can access in this location.</span></span> <br><br><span data-ttu-id="41f67-206">「[SD カードへのアクセス](access-the-sd-card.md)」もご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-206">Also see [Access the SD card](access-the-sd-card.md).</span></span> | [<span data-ttu-id="41f67-207">KnownFolders.RemovableDevices</span><span class="sxs-lookup"><span data-stu-id="41f67-207">KnownFolders.RemovableDevices</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.removabledevices) |  
| <span data-ttu-id="41f67-208">ホームグループ ライブラリ</span><span class="sxs-lookup"><span data-stu-id="41f67-208">Homegroup libraries</span></span>  | <span data-ttu-id="41f67-209">次の機能が 1 つ以上必要です。</span><span class="sxs-lookup"><span data-stu-id="41f67-209">At least one of the following capabilities is needed.</span></span> <br><span data-ttu-id="41f67-210">- MusicLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-210">- MusicLibrary</span></span> <br><span data-ttu-id="41f67-211">- PicturesLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-211">- PicturesLibrary</span></span> <br><span data-ttu-id="41f67-212">- VideosLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-212">- VideosLibrary</span></span> | [<span data-ttu-id="41f67-213">KnownFolders.HomeGroup</span><span class="sxs-lookup"><span data-stu-id="41f67-213">KnownFolders.HomeGroup</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.homegroup) |      
| <span data-ttu-id="41f67-214">メディア サーバー デバイス (DLNA)</span><span class="sxs-lookup"><span data-stu-id="41f67-214">Media server devices (DLNA)</span></span> | <span data-ttu-id="41f67-215">次の機能が 1 つ以上必要です。</span><span class="sxs-lookup"><span data-stu-id="41f67-215">At least one of the following capabilities is needed.</span></span> <br><span data-ttu-id="41f67-216">- MusicLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-216">- MusicLibrary</span></span> <br><span data-ttu-id="41f67-217">- PicturesLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-217">- PicturesLibrary</span></span> <br><span data-ttu-id="41f67-218">- VideosLibrary</span><span class="sxs-lookup"><span data-stu-id="41f67-218">- VideosLibrary</span></span> | [<span data-ttu-id="41f67-219">KnownFolders.MediaServerDevices</span><span class="sxs-lookup"><span data-stu-id="41f67-219">KnownFolders.MediaServerDevices</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.mediaserverdevices) |
| <span data-ttu-id="41f67-220">汎用名前付け規則 (UNC) フォルダー</span><span class="sxs-lookup"><span data-stu-id="41f67-220">Universal Naming Convention (UNC) folders</span></span> | <span data-ttu-id="41f67-221">次の機能の組み合わせが必要です。</span><span class="sxs-lookup"><span data-stu-id="41f67-221">A combination of the following capabilities is needed.</span></span> <br><br><span data-ttu-id="41f67-222">ホーム ネットワークと社内ネットワークの機能:</span><span class="sxs-lookup"><span data-stu-id="41f67-222">The home and work networks capability:</span></span> <br><span data-ttu-id="41f67-223">- PrivateNetworkClientServer</span><span class="sxs-lookup"><span data-stu-id="41f67-223">- PrivateNetworkClientServer</span></span> <br><br><span data-ttu-id="41f67-224">インターネットとパブリック ネットワークの 1 つ以上の機能:</span><span class="sxs-lookup"><span data-stu-id="41f67-224">And at least one internet and public networks capability:</span></span> <br><span data-ttu-id="41f67-225">- InternetClient</span><span class="sxs-lookup"><span data-stu-id="41f67-225">- InternetClient</span></span> <br><span data-ttu-id="41f67-226">- InternetClientServer</span><span class="sxs-lookup"><span data-stu-id="41f67-226">- InternetClientServer</span></span> <br><br><span data-ttu-id="41f67-227">ドメイン資格情報の機能 (該当する場合):</span><span class="sxs-lookup"><span data-stu-id="41f67-227">And, if applicable, the domain credentials capability:</span></span><br><span data-ttu-id="41f67-228">- EnterpriseAuthentication</span><span class="sxs-lookup"><span data-stu-id="41f67-228">- EnterpriseAuthentication</span></span> <br><br><span data-ttu-id="41f67-229">注:この場所で、アプリにアクセスできる特定のファイルの種類を宣言できるアプリケーション マニフェスト ファイルの種類の関連付けを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="41f67-229">Note: You must add File Type Associations to your app manifest that declare specific file types that your app can access in this location.</span></span> | <span data-ttu-id="41f67-230">フォルダーを取得する場合:</span><span class="sxs-lookup"><span data-stu-id="41f67-230">Retrieve a folder using:</span></span> <br>[<span data-ttu-id="41f67-231">StorageFolder.GetFolderFromPathAsync</span><span class="sxs-lookup"><span data-stu-id="41f67-231">StorageFolder.GetFolderFromPathAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfolderfrompathasync) <br><br><span data-ttu-id="41f67-232">ファイルを取得する場合:</span><span class="sxs-lookup"><span data-stu-id="41f67-232">Retrieve a file using:</span></span> <br>[<span data-ttu-id="41f67-233">StorageFile.GetFileFromPathAsync</span><span class="sxs-lookup"><span data-stu-id="41f67-233">StorageFile.GetFileFromPathAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefrompathasync) |

<span data-ttu-id="41f67-234">**例**</span><span class="sxs-lookup"><span data-stu-id="41f67-234">**Example**</span></span>

<span data-ttu-id="41f67-235">この例では、制限付きの `broadFileSystemAccess` 機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="41f67-235">This example adds the restricted `broadFileSystemAccess` capability.</span></span> <span data-ttu-id="41f67-236">機能を指定するだけでなく、`rescap` 名前空間を追加し、`IgnorableNamespaces` に追加する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="41f67-236">In addition to specifying the capability, the `rescap` namespace must be added, and is also added to `IgnorableNamespaces`:</span></span>

```xaml
<Package
  ...
  xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
  IgnorableNamespaces="uap mp uap5 rescap">
...
<Capabilities>
    <rescap:Capability Name="broadFileSystemAccess" />
</Capabilities>
```

> [!NOTE]
> <span data-ttu-id="41f67-237">すべてのアプリ機能の一覧については、「[アプリ機能の宣言](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="41f67-237">For a complete list of app capabilities, see [App capability declarations](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations).</span></span>
