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
# <a name="file-access-permissions"></a>ファイル アクセス許可

ユニバーサル Windows プラットフォーム (UWP) アプリでは、既定では、特定のファイル システムの場所をアクセスできます。 また、ファイル ピッカーの使用や機能の宣言によって、その他の場所にアクセスすることもできます。

## <a name="the-locations-that-all-apps-can-access"></a>すべてのアプリからアクセスできる場所

新しいアプリを作成すると、既定でファイル システムの次の場所にアクセスできます。

### <a name="application-install-directory"></a>アプリケーションのインストール ディレクトリ
ユーザーのシステムで、アプリがインストールされているフォルダーです。

ファイルにアクセスする 2 つの主な方法があるし、フォルダーが、アプリのインストール ディレクトリ。

1. 次のように、アプリのインストール ディレクトリを表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) を取得できます。

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

    [  **StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) メソッドを使って、ディレクトリ内のファイルとフォルダーにアクセスすることができます。 上の例では、この **StorageFolder** が `installDirectory` 変数に格納されています。 アプリ パッケージやインストール ディレクトリの操作について詳しくは、GitHub にある[アプリ パッケージ情報のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Package)をご覧ください。

2. 次のように、アプリの URI を使って、アプリのインストール ディレクトリからファイルを直接取得できます。

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

    [  **GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync) が完了すると、アプリのインストール ディレクトリにある `file.txt` ファイル (この例では `file`) を表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) が返されます。
    
    URI の "ms-appx:///" プレフィックスは、アプリのインストール ディレクトリを参照します。 アプリの URI の使用について詳しくは、「[URI を使ってコンテンツを参照する方法](https://docs.microsoft.com/previous-versions/windows/apps/hh781215(v=win.10))」をご覧ください。

さらに、他の場所とは異なり、[ユニバーサル Windows プラットフォーム (UWP) アプリの Win32 と COM](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) や [Microsoft Visual Studio の C/C++ 標準ライブラリ関数](https://docs.microsoft.com/cpp/cpp/c-cpp-language-and-standard-libraries)を使ってアプリのインストール ディレクトリ内のファイルにアクセスすることもできます。

アプリのインストール ディレクトリは読み取り専用です。 ファイル ピッカーでは、インストール ディレクトリへのアクセスを得ることはできません。

### <a name="application-data-locations"></a>アプリケーション データの場所
アプリがデータを保存できるフォルダーです。 これらのフォルダー (ローカル、移動、一時) は、アプリのインストール時に作成されます。

アプリのデータの場所からファイルとフォルダーにアクセスする 2 つの主な方法があります。

1.  [  **ApplicationData**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData) プロパティを使ってアプリ データ フォルダーを取得します。

    たとえば、次のように、[**ApplicationData**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData).[**LocalFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) を使って、アプリのローカル フォルダーを表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) を取得できます。
    
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
    
    アプリの移動フォルダーまたは一時フォルダーにアクセスする場合は、[**RoamingFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingfolder) プロパティまたは [**TemporaryFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) プロパティを使います。
    
    アプリ データの場所を表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) を取得したら、**StorageFolder** メソッドを使って、その場所にあるファイルやフォルダーにアクセスできます。 上の例では、これらの **StorageFolder** オブジェクトが `localFolder` 変数に格納されています。 アプリ データの場所の使用について詳しくは、[ApplicationData クラス](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata)のページのガイダンスをご覧ください。また、GitHub から[アプリケーション データ サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ApplicationData)をダウンロードしてご覧ください。

2. このようなアプリの URI を使用して、アプリのローカル フォルダーから直接ファイルを取得できます。
    
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
    
    [  **GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync) が完了すると、アプリのローカル フォルダーにある `file.txt` ファイル (この例では `file`) を表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) が返されます。
    
    URI の "ms-appdata:///local/" プレフィックスは、アプリのローカル フォルダーを参照します。 アプリの移動フォルダーまたは一時フォルダーにあるファイルにアクセスするには、"ms-appdata:///roaming/" または "ms-appdata:///temporary/" を使います。 アプリの URI の使用について詳しくは、「[ファイル リソースを読み込む方法](https://docs.microsoft.com/previous-versions/windows/apps/hh781229(v=win.10))」をご覧ください。

さらに、他の場所とは異なり、[UWP アプリの Win32 と COM](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps) や Visual Studio の C/C++ 標準ライブラリ関数を使ってアプリ データの場所にあるファイルにアクセスすることもできます。

ファイル ピッカーでは、ローカル、移動、または一時フォルダーにアクセスできません。

### <a name="removable-devices"></a>リムーバブル デバイス
さらに、接続されているデバイス上の一部のファイルに既定でアクセスできます。 これは、[自動再生拡張機能](https://docs.microsoft.com/previous-versions/windows/apps/hh464906(v=win.10))を使って、ユーザーがデバイス (カメラや USB サム ドライブなど) をシステムに接続したときに自動的に起動されるようにする場合に使うことができます。 アプリでアクセスできるファイルの種類は、アプリ マニフェストのファイルの種類の関連付けの宣言で指定されたものだけに制限されます。

もちろん、ファイル ピッカー ([**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) と [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker)) を呼び出して、アプリでアクセスするファイルやフォルダーをユーザーが選べるようにすると、リムーバブル デバイス上のファイルやフォルダーにもアクセスできます。 ファイル ピッカーの使い方については、「[ピッカーでファイルやフォルダーを開く](quickstart-using-file-and-folder-pickers.md)」をご覧ください。

> [!NOTE]
> SD カードやその他のリムーバブル デバイスにアクセスする方法について詳しくは、「[SD カードへのアクセス](access-the-sd-card.md)」をご覧ください。

## <a name="locations-that-uwp-apps-can-access"></a>UWP アプリにアクセスできる場所
### <a name="users-downloads-folder"></a>ユーザーの [ダウンロード] フォルダー

ダウンロードされたファイルが保存される既定のフォルダーです。

既定では、ユーザーの "ダウンロード" フォルダーにあるファイルやフォルダーについては、そのアプリで作成したものにしかアクセスできません。 ただし、ファイル ピッカー ([**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) または [**FolderPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FolderPicker)) を呼び出して、アプリでアクセスするファイルやフォルダーをユーザーが参照して選べるようにすると、ユーザーの "ダウンロード" フォルダーにあるファイルやフォルダーにアクセスできるようになります。

- 次のように、ユーザーの "ダウンロード" フォルダーにファイルを作成できます。

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

    [**DownloadsFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.DownloadsFolder).[**CreateFileAsync** ](https://docs.microsoft.com/uwp/api/windows.storage.downloadsfolder.createfileasync)システムで行う必要がありますを指定できるようにオーバー ロードは、同じ名前を持つ Downloads フォルダーが既に既存のファイルがある場合。 これらのメソッドが完了すると、作成されたファイルを表す [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) が返されます。 上の例では、このファイルの名前は `newFile` です。

- 次のように、ユーザーの "ダウンロード" フォルダーにサブフォルダーを作成できます。

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

    [**DownloadsFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.DownloadsFolder).[**CreateFolderAsync** ](https://docs.microsoft.com/uwp/api/windows.storage.downloadsfolder.createfolderasync)システムで行う必要がありますを指定できるようにオーバー ロードは、同じ名前を持つ Downloads フォルダーが既に既存のサブフォルダーがある場合。 これらのメソッドが完了すると、作成されたサブフォルダーを表す [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) が返されます。 上の例では、このファイルの名前は `newFolder` です。

"ダウンロード" フォルダーにファイルやフォルダーを作成する場合は、以降に簡単にアクセスできるように、その項目をアプリの [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) に追加することをお勧めします。

## <a name="accessing-additional-locations"></a>その他の場所へのアクセス

アプリで、既定の場所以外にあるファイルやフォルダーにアクセスするには、アプリ マニフェストで機能を宣言するか、ファイル ピッカーを呼び出してアプリでアクセスするファイルやフォルダーをユーザーが選べるようにします。詳しくは、「[アプリ機能の宣言](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)」または「[ピッカーでファイルやフォルダーを開く](quickstart-using-file-and-folder-pickers.md)」をご覧ください。

[AppExecutionAlias](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-appexecutionalias) 拡張機能を宣言したアプリには、コンソール ウィンドウでアプリが起動されたディレクトリおよびその下位レベルのディレクトリに対する、ファイル システムのアクセス許可が与えられます。

次の表に、機能の宣言や関連付けられた [**Windows.Storage**](https://docs.microsoft.com/uwp/api/Windows.Storage) API の使用によってアクセスできるその他の場所を示します。

| Location | 機能 | Windows.Storage API |
|----------|------------|---------------------|
| ユーザーがアクセス権を持つすべてのファイル。 例: ドキュメント、画像、写真、ダウンロード、デスクトップ、OneDrive などです。 | broadFileSystemAccess<br><br>これは、制限付き機能です。 アクセス**設定** > **プライバシー** > **ファイル システム**します。 ユーザーが許可または拒否でいつでものため**設定**アプリがこれらの変更に回復力のあることを確認してください。 アプリにアクセスがないことを発見した場合へのリンクを提供することで、設定を変更するユーザー入力を求めることができます、 [Windows 10 のファイル システム アクセスとプライバシー](https://privacy.microsoft.com/en-US/windows-10-file-system-access-and-privacy)記事。 いるユーザー必要があります、アプリを閉じるの設定を切り替えるアプリを再起動します。 場合は、アプリの実行中に、設定を切り替えますが、状態を保存して、新しい設定を適用するために、アプリを強制的に終了するように、プラットフォームは、アプリを中断します。 2018 年 4 月の更新プログラムでは、アクセス許可の既定値には。 2018 の年 10 月の更新プログラムでは、既定値は、オフは。<br /><br />この機能を宣言するアプリを Microsoft Store に提出する場合、アプリでこの機能が必要となる理由およびこの機能の使用目的に関する追加の説明を提供する必要があります。<br>この機能は、Api での[ **Windows.Storage** ](https://docs.microsoft.com/uwp/api/Windows.Storage)名前空間。 参照してください、**例**アプリでこの機能を有効にする方法の例は、この記事の最後のセクション。 | なし |
| Documents | DocumentsLibrary <br><br>注:この場所で、アプリにアクセスできる特定のファイルの種類を宣言できるアプリケーション マニフェスト ファイルの種類の関連付けを追加する必要があります。 <br><br>この機能は、アプリが次の条件を満たす場合に使います。<br>- 有効な OneDrive URL またはリソース ID を使った、特定の OneDrive コンテンツへのクロスプラットフォーム オフライン アクセスを容易にする<br>保存中に自動的にユーザーの OneDrive にファイルを開くオフライン | [KnownFolders.DocumentsLibrary](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.documentslibrary) |
| 音楽     | MusicLibrary <br>「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md)」もご覧ください。 | [KnownFolders.MusicLibrary](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.musiclibrary) |    
| 画像  | PicturesLibrary<br> 「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md)」もご覧ください。 | [KnownFolders.PicturesLibrary](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.pictureslibrary) |  
| ビデオ    | VideosLibrary<br>「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md)」もご覧ください。 | [KnownFolders.VideosLibrary](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.videoslibrary) |   
| リムーバブル デバイス  | RemovableDevices <br><br>注  アプリ マニフェストにファイルの種類の関連付けを追加し、この場所でアプリがアクセスできるファイルの種類を具体的に宣言する必要があります。 <br><br>「[SD カードへのアクセス](access-the-sd-card.md)」もご覧ください。 | [KnownFolders.RemovableDevices](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.removabledevices) |  
| ホームグループ ライブラリ  | 次の機能が 1 つ以上必要です。 <br>- MusicLibrary <br>- PicturesLibrary <br>- VideosLibrary | [KnownFolders.HomeGroup](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.homegroup) |      
| メディア サーバー デバイス (DLNA) | 次の機能が 1 つ以上必要です。 <br>- MusicLibrary <br>- PicturesLibrary <br>- VideosLibrary | [KnownFolders.MediaServerDevices](https://docs.microsoft.com/uwp/api/windows.storage.knownfolders.mediaserverdevices) |
| 汎用名前付け規則 (UNC) フォルダー | 次の機能の組み合わせが必要です。 <br><br>ホーム ネットワークと社内ネットワークの機能: <br>- PrivateNetworkClientServer <br><br>インターネットとパブリック ネットワークの 1 つ以上の機能: <br>- InternetClient <br>- InternetClientServer <br><br>ドメイン資格情報の機能 (該当する場合):<br>- EnterpriseAuthentication <br><br>注:この場所で、アプリにアクセスできる特定のファイルの種類を宣言できるアプリケーション マニフェスト ファイルの種類の関連付けを追加する必要があります。 | フォルダーを取得する場合: <br>[StorageFolder.GetFolderFromPathAsync](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfolderfrompathasync) <br><br>ファイルを取得する場合: <br>[StorageFile.GetFileFromPathAsync](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefrompathasync) |

**例**

この例では、制限付きの `broadFileSystemAccess` 機能を追加します。 機能を指定するだけでなく、`rescap` 名前空間を追加し、`IgnorableNamespaces` に追加する必要もあります。

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
> すべてのアプリ機能の一覧については、「[アプリ機能の宣言](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations)」をご覧ください。
