---
Description: ローカル アプリ データ、ローミング アプリ データ、一時アプリ データの保存方法と取得方法について説明します。
title: 設定と他のアプリ データを保存して取得する
ms.assetid: 41676A02-325A-455E-8565-C9EC0BC3A8FE
label: App settings and data
template: detail.hbs
ms.date: 11/14/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 2848b22c69960075297546d401689d4c51c637aa
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66361927"
---
# <a name="store-and-retrieve-settings-and-other-app-data"></a><span data-ttu-id="85cb3-104">設定と他のアプリ データを保存して取得する</span><span class="sxs-lookup"><span data-stu-id="85cb3-104">Store and retrieve settings and other app data</span></span>

<span data-ttu-id="85cb3-105">*アプリ データ*とは、特定のアプリに固有の実行可能データです。</span><span class="sxs-lookup"><span data-stu-id="85cb3-105">*App data* is mutable data that is specific to a particular app.</span></span> <span data-ttu-id="85cb3-106">ランタイム状態、ユーザー設定、その他の設定などがあります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-106">It includes runtime state, user preferences, and other settings.</span></span> <span data-ttu-id="85cb3-107">アプリ データは*ユーザー データ*とは異なり、アプリを使用しているときに、ユーザーが作成、管理するデータです。</span><span class="sxs-lookup"><span data-stu-id="85cb3-107">App data is different from *user data*, data that the user creates and manages when using an app.</span></span> <span data-ttu-id="85cb3-108">ユーザー データには、ドキュメント ファイル、メディア ファイル、メール トランスクリプト、通信トランスクリプト、ユーザーが作成したコンテンツを保持するデータベース レコードなどがあります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-108">User data includes document or media files, email or communication transcripts, or database records holding content created by the user.</span></span> <span data-ttu-id="85cb3-109">ユーザー データは複数のアプリで有効な場合があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-109">User data may be useful or meaningful to more than one app.</span></span> <span data-ttu-id="85cb3-110">多くの場合、ユーザー データは、ユーザーがアプリ自体とは無関係にエンティティとして操作または転送するデータ (ドキュメントなど) です。</span><span class="sxs-lookup"><span data-stu-id="85cb3-110">Often, this is data that the user wants to manipulate or transmit as an entity independent of the app itself, such as a document.</span></span>

<span data-ttu-id="85cb3-111">**アプリのデータについての重要な注意事項:** アプリ データの有効期間はアプリの有効期間に依存します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-111">**Important note about app data:** The lifetime of the app data is tied to the lifetime of the app.</span></span> <span data-ttu-id="85cb3-112">アプリが削除されると、すべてのアプリ データが失われます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-112">If the app is removed, all of the app data will be lost as a consequence.</span></span> <span data-ttu-id="85cb3-113">ユーザー データや、ユーザーにとって欠かすことができない重要なデータの保存には、アプリ データを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-113">Don't use app data to store user data or anything that users might perceive as valuable and irreplaceable.</span></span> <span data-ttu-id="85cb3-114">そのような情報の保存には、ユーザーのライブラリや Microsoft OneDrive を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-114">We recommend that the user's libraries and Microsoft OneDrive be used to store this sort of information.</span></span> <span data-ttu-id="85cb3-115">アプリ データは、アプリ固有のユーザー設定、設定、お気に入りを保存するのに適しています。</span><span class="sxs-lookup"><span data-stu-id="85cb3-115">App data is ideal for storing app-specific user preferences, settings, and favorites.</span></span>

## <a name="types-of-app-data"></a><span data-ttu-id="85cb3-116">アプリ データの種類</span><span class="sxs-lookup"><span data-stu-id="85cb3-116">Types of app data</span></span>


<span data-ttu-id="85cb3-117">アプリ データには、設定とファイルの 2 種類があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-117">There are two types of app data: settings and files.</span></span>

-   <span data-ttu-id="85cb3-118">**設定**</span><span class="sxs-lookup"><span data-stu-id="85cb3-118">**Settings**</span></span>

    <span data-ttu-id="85cb3-119">設定を使用して、ユーザー設定やとアプリケーションの状態情報を保存します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-119">Use settings to store user preferences and application state info.</span></span> <span data-ttu-id="85cb3-120">アプリ データ API を使用して、設定をを簡単に作成して取得できます (この記事の後半でいくつかの例を紹介します)。</span><span class="sxs-lookup"><span data-stu-id="85cb3-120">The app data API enables you to easily create and retrieve settings (we'll show you some examples later in this article).</span></span>

    <span data-ttu-id="85cb3-121">アプリの設定に使用できるデータ型を次に示します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-121">Here are data types you can use for app settings:</span></span>

    -   <span data-ttu-id="85cb3-122">**UInt8**、**Int16**、**UInt16**、**Int32**、**UInt32**、**Int64**、**UInt64**、**Single**、**Double**</span><span class="sxs-lookup"><span data-stu-id="85cb3-122">**UInt8**, **Int16**, **UInt16**, **Int32**, **UInt32**, **Int64**, **UInt64**, **Single**, **Double**</span></span>
    -   <span data-ttu-id="85cb3-123">**ブール値**</span><span class="sxs-lookup"><span data-stu-id="85cb3-123">**Boolean**</span></span>
    -   <span data-ttu-id="85cb3-124">**Char16**、**String**</span><span class="sxs-lookup"><span data-stu-id="85cb3-124">**Char16**, **String**</span></span>
    -   <span data-ttu-id="85cb3-125">[**DateTime**](https://docs.microsoft.com/uwp/api/Windows.Foundation.DateTime)、 [ **TimeSpan**](https://docs.microsoft.com/uwp/api/Windows.Foundation.TimeSpan)</span><span class="sxs-lookup"><span data-stu-id="85cb3-125">[**DateTime**](https://docs.microsoft.com/uwp/api/Windows.Foundation.DateTime), [**TimeSpan**](https://docs.microsoft.com/uwp/api/Windows.Foundation.TimeSpan)</span></span>
    -   <span data-ttu-id="85cb3-126">**GUID**、[**Point**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Point)、[**Size**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Size)、[**Rect**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Rect)</span><span class="sxs-lookup"><span data-stu-id="85cb3-126">**GUID**, [**Point**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Point), [**Size**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Size), [**Rect**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Rect)</span></span>
    -   <span data-ttu-id="85cb3-127">[**ApplicationDataCompositeValue**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataCompositeValue):一連の関連アプリ設定をシリアル化し、アトミックに逆シリアル化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-127">[**ApplicationDataCompositeValue**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataCompositeValue): A set of related app settings that must be serialized and deserialized atomically.</span></span> <span data-ttu-id="85cb3-128">コンポジット設定を使うと、相互に依存する設定のアトミックな更新が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-128">Use composite settings to easily handle atomic updates of interdependent settings.</span></span> <span data-ttu-id="85cb3-129">同時アクセスとローミング時は、システムによってコンポジット設定の整合性が保たれます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-129">The system ensures the integrity of composite settings during concurrent access and roaming.</span></span> <span data-ttu-id="85cb3-130">コンポジット設定は少量のデータに適しており、大きなデータ セットに使うとパフォーマンスが低下する場合があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-130">Composite settings are optimized for small amounts of data, and performance can be poor if you use them for large data sets.</span></span>
-   <span data-ttu-id="85cb3-131">**ファイル**</span><span class="sxs-lookup"><span data-stu-id="85cb3-131">**Files**</span></span>

    <span data-ttu-id="85cb3-132">ファイルを使うと、バイナリ データを保存したり、独自にカスタマイズされ、シリアル化された型を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-132">Use files to store binary data or to enable your own, customized serialized types.</span></span>

## <a name="storing-app-data-in-the-app-data-stores"></a><span data-ttu-id="85cb3-133">アプリのデータ ストアにアプリ データを保存する</span><span class="sxs-lookup"><span data-stu-id="85cb3-133">Storing app data in the app data stores</span></span>


<span data-ttu-id="85cb3-134">アプリのインストール時には、設定やファイル用に、ユーザーごとの固有のデータ ストアが設定されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-134">When an app is installed, the system gives it its own per-user data stores for settings and files.</span></span> <span data-ttu-id="85cb3-135">物理的ストレージはシステムによって管理されるため、このデータの場所や形式を意識することなく、データは他のアプリやユーザーから確実に分離されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-135">You don't need to know where or how this data exists, because the system is responsible for managing the physical storage, ensuring that the data is kept isolated from other apps and other users.</span></span> <span data-ttu-id="85cb3-136">また、アプリに更新プログラムをインストールするときはデータ ストアの内容が保持され、アプリのアンインストール時にはデータ ストアの内容が完全に削除されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-136">The system also preserves the contents of these data stores when the user installs an update to your app and removes the contents of these data stores completely and cleanly when your app is uninstalled.</span></span>

<span data-ttu-id="85cb3-137">各アプリのデータ ストア内には、ローカル ファイル用、ローミング ファイル用、一時ファイル用に 1 つずつ、システム定義のルート ディレクトリがあります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-137">Within its app data store, each app has system-defined root directories: one for local files, one for roaming files, and one for temporary files.</span></span> <span data-ttu-id="85cb3-138">それぞれのルート ディレクトリに新しいファイルや新しいコンテナーをアプリで追加できます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-138">Your app can add new files and new containers to each of these root directories.</span></span>

## <a name="local-app-data"></a><span data-ttu-id="85cb3-139">ローカル アプリ データ</span><span class="sxs-lookup"><span data-stu-id="85cb3-139">Local app data</span></span>


<span data-ttu-id="85cb3-140">ローカル アプリ データは、アプリ セッション間で保持する必要がある情報のうち、ローミング アプリ データには適していないものに使用されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-140">Local app data should be used for any information that needs to be preserved between app sessions and is not suitable for roaming app data.</span></span> <span data-ttu-id="85cb3-141">また、他のデバイスには適さないデータもここに格納します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-141">Data that is not applicable on other devices should be stored here as well.</span></span> <span data-ttu-id="85cb3-142">ローカルに格納されるデータには、一般的なサイズの制限はありません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-142">There is no general size restriction on local data stored.</span></span> <span data-ttu-id="85cb3-143">ローカル アプリ データ ストアは、ローミングに適さないデータや、大きなデータ セットに使用してください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-143">Use the local app data store for data that it does not make sense to roam and for large data sets.</span></span>

### <a name="retrieve-the-local-app-data-store"></a><span data-ttu-id="85cb3-144">ローカル アプリ データ ストアを取得する</span><span class="sxs-lookup"><span data-stu-id="85cb3-144">Retrieve the local app data store</span></span>

<span data-ttu-id="85cb3-145">ローカル アプリ データを読み書きする前に、ローカル アプリ データ ストアを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-145">Before you can read or write local app data, you must retrieve the local app data store.</span></span> <span data-ttu-id="85cb3-146">ローカル アプリ データ ストアを取得するには、[**ApplicationData.LocalSettings**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localsettings) プロパティを使用して、アプリのローカル設定を [**ApplicationDataContainer**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataContainer) オブジェクトとして取得します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-146">To retrieve the local app data store, use the [**ApplicationData.LocalSettings**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localsettings) property to get the app's local settings as an [**ApplicationDataContainer**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataContainer) object.</span></span> <span data-ttu-id="85cb3-147">[  **StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) オブジェクト内のファイルを取得するには、[**ApplicationData.LocalFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-147">Use the [**ApplicationData.LocalFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) property to get the files in a [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) object.</span></span> <span data-ttu-id="85cb3-148">バックアップや復元に含まれていないファイルを保存できるローカル アプリ データ ストア内のフォルダーを取得するには、[**ApplicationData.LocalCacheFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localcachefolder) プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-148">Use the [**ApplicationData.LocalCacheFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localcachefolder) property to get the folder in the local app data store where you can save files that are not included in backup and restore.</span></span>

```CSharp
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;
```

### <a name="create-and-retrieve-a-simple-local-setting"></a><span data-ttu-id="85cb3-149">簡易ローカル設定を作成して取得する</span><span class="sxs-lookup"><span data-stu-id="85cb3-149">Create and retrieve a simple local setting</span></span>

<span data-ttu-id="85cb3-150">設定を作成または書き込むには、[**ApplicationDataContainer.Values**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.values) プロパティを使用して、前の手順で取得した `localSettings` コンテナー内の設定にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-150">To create or write a setting, use the [**ApplicationDataContainer.Values**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.values) property to access the settings in the `localSettings` container we got in the previous step.</span></span> <span data-ttu-id="85cb3-151">次の例では、`exampleSetting` という名前の設定を作成します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-151">This example creates a setting named `exampleSetting`.</span></span>

```CSharp
// Simple setting

localSettings.Values["exampleSetting"] = "Hello Windows";
```

<span data-ttu-id="85cb3-152">設定を取得するには、設定を作成したときに使ったものと同じ [**ApplicationDataContainer.Values**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.values) プロパティを使います。</span><span class="sxs-lookup"><span data-stu-id="85cb3-152">To retrieve the setting, you use the same [**ApplicationDataContainer.Values**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.values) property that you used to create the setting.</span></span> <span data-ttu-id="85cb3-153">この例では作成した設定を取得する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="85cb3-153">This example shows how to retrieve the setting we just created.</span></span>

```CSharp
// Simple setting
Object value = localSettings.Values["exampleSetting"];
```

### <a name="create-and-retrieve-a-local-composite-value"></a><span data-ttu-id="85cb3-154">ローカル コンポジット値を作成して取得する</span><span class="sxs-lookup"><span data-stu-id="85cb3-154">Create and retrieve a local composite value</span></span>

<span data-ttu-id="85cb3-155">コンポジット値を作成または書き込むには、[**ApplicationDataCompositeValue**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataCompositeValue) オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-155">To create or write a composite value, create an [**ApplicationDataCompositeValue**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataCompositeValue) object.</span></span> <span data-ttu-id="85cb3-156">次の例では、`exampleCompositeSetting` という名前のコンポジット設定を作成し、`localSettings` コンテナーに追加します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-156">This example creates a composite setting named `exampleCompositeSetting` and adds it to the `localSettings` container.</span></span>

```CSharp
// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
    new Windows.Storage.ApplicationDataCompositeValue();
composite["intVal"] = 1;
composite["strVal"] = "string";

localSettings.Values["exampleCompositeSetting"] = composite;
```

<span data-ttu-id="85cb3-157">この例では作成したコンポジット値を取得する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="85cb3-157">This example shows how to retrieve the composite value we just created.</span></span>

```CSharp
// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
   (Windows.Storage.ApplicationDataCompositeValue)localSettings.Values["exampleCompositeSetting"];

if (composite == null)
{
   // No data
}
else
{
   // Access data in composite["intVal"] and composite["strVal"]
}
```

### <a name="create-and-read-a-local-file"></a><span data-ttu-id="85cb3-158">ローカル ファイルを作成して読み取る</span><span class="sxs-lookup"><span data-stu-id="85cb3-158">Create and read a local file</span></span>

<span data-ttu-id="85cb3-159">ローカル アプリ データ ストアにファイルを作成して更新するには、[**Windows.Storage.StorageFolder.CreateFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfileasync) や [**Windows.Storage.FileIO.WriteTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.writetextasync) などのファイル API を使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-159">To create and update a file in the local app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.CreateFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfileasync) and [**Windows.Storage.FileIO.WriteTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.writetextasync).</span></span> <span data-ttu-id="85cb3-160">次の例では、`localFolder` コンテナーに `dataFile.txt` という名前のファイルを作成し、現在の日付と時刻をファイルに書き込みます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-160">This example creates a file named `dataFile.txt` in the `localFolder` container and writes the current date and time to the file.</span></span> <span data-ttu-id="85cb3-161">[  **CreationCollisionOption**](https://docs.microsoft.com/uwp/api/Windows.Storage.CreationCollisionOption) 列挙体の **ReplaceExisting** 値は、ファイルが既にある場合にファイルを置き換えることを示します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-161">The **ReplaceExisting** value from the [**CreationCollisionOption**](https://docs.microsoft.com/uwp/api/Windows.Storage.CreationCollisionOption) enumeration indicates to replace the file if it already exists.</span></span>

```csharp
async void WriteTimestamp()
{
   Windows.Globalization.DateTimeFormatting.DateTimeFormatter formatter = 
       new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("longtime");

   StorageFile sampleFile = await localFolder.CreateFileAsync("dataFile.txt", 
       CreationCollisionOption.ReplaceExisting);
   await FileIO.WriteTextAsync(sampleFile, formatter.Format(DateTimeOffset.Now));
}
```

<span data-ttu-id="85cb3-162">ローカル アプリ データ ストアのファイルを開いて読み取るには、[**Windows.Storage.StorageFolder.GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfileasync)、[**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync)、[**Windows.Storage.FileIO.ReadTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.readtextasync) などのファイル API を使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-162">To open and read a file in the local app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfileasync), [**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync), and [**Windows.Storage.FileIO.ReadTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.readtextasync).</span></span> <span data-ttu-id="85cb3-163">この例では、前の手順で作成した `dataFile.txt` ファイルを開き、ファイルから日付を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-163">This example opens the `dataFile.txt` file created in the previous step and reads the date from the file.</span></span> <span data-ttu-id="85cb3-164">さまざまな場所からファイル リソースを読み込む方法について詳しくは、「[ファイル リソースを読み込む方法](https://docs.microsoft.com/previous-versions/windows/apps/hh965322(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-164">For details on loading file resources from various locations, see [How to load file resources](https://docs.microsoft.com/previous-versions/windows/apps/hh965322(v=win.10)).</span></span>

```csharp
async void ReadTimestamp()
{
   try
   {
      StorageFile sampleFile = await localFolder.GetFileAsync("dataFile.txt");
      String timestamp = await FileIO.ReadTextAsync(sampleFile);
      // Data is contained in timestamp
   }
   catch (Exception)
   {
      // Timestamp not found
   }
}
```

## <a name="roaming-data"></a><span data-ttu-id="85cb3-165">ローミング データ</span><span class="sxs-lookup"><span data-stu-id="85cb3-165">Roaming data</span></span>


<span data-ttu-id="85cb3-166">アプリでローミング データを使用すると、複数のデバイス間でアプリ データを簡単に同期することができます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-166">If you use roaming data in your app, your users can easily keep your app's app data in sync across multiple devices.</span></span> <span data-ttu-id="85cb3-167">アプリを複数のデバイス上にインストールすると、OS によってアプリ データの同期が維持されるため、2 つ目のデバイス上でユーザーが行うアプリのセットアップ作業が軽減されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-167">If a user installs your app on multiple devices, the OS keeps the app data in sync, reducing the amount of setup work that the user needs to do for your app on their second device.</span></span> <span data-ttu-id="85cb3-168">またローミングを使うと、異なるデバイス上でも、一覧の作成などの作業を中断したときの状態から再開することができます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-168">Roaming also enables your users to continue a task, such as composing a list, right where they left off even on a different device.</span></span> <span data-ttu-id="85cb3-169">ローミング データが更新されると、OS によってクラウドにレプリケートされ、アプリがインストールされている別のデバイスに同期されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-169">The OS replicates roaming data to the cloud when it is updated, and synchronizes the data to the other devices on which the app is installed.</span></span>

<span data-ttu-id="85cb3-170">各アプリでローミングできるアプリ データのサイズには OS による制限があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-170">The OS limits the size of the app data that each app may roam.</span></span> <span data-ttu-id="85cb3-171">「[**ApplicationData.RoamingStorageQuota**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingstoragequota)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-171">See [**ApplicationData.RoamingStorageQuota**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingstoragequota).</span></span> <span data-ttu-id="85cb3-172">この制限に達した場合、アプリでローミングされたアプリ データの合計が制限値未満に戻るまで、そのアプリのアプリ データはクラウドにまったくレプリケートされません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-172">If the app hits this limit, none of the app's app data will be replicated to the cloud until the app's total roamed app data is less than the limit again.</span></span> <span data-ttu-id="85cb3-173">このため、ローミング データは、ユーザー設定、リンク、小さなデータ ファイルのみに使うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-173">For this reason, it is a best practice to use roaming data only for user preferences, links, and small data files.</span></span>

<span data-ttu-id="85cb3-174">アプリのローミング データは、一定の時間間隔内にユーザーがいずれかのデバイスからアクセスしている限り、クラウドに保持されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-174">Roaming data for an app is available in the cloud as long as it is accessed by the user from some device within the required time interval.</span></span> <span data-ttu-id="85cb3-175">この時間間隔内にアプリが実行されないと、そのローミング データはクラウドから削除されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-175">If the user does not run an app for longer than this time interval, its roaming data is removed from the cloud.</span></span> <span data-ttu-id="85cb3-176">ユーザーがアプリをアンインストールしても、そのローミング データがクラウドから自動的に削除されることはなく、保持されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-176">If a user uninstalls an app, its roaming data isn't automatically removed from the cloud, it's preserved.</span></span> <span data-ttu-id="85cb3-177">時間間隔内にユーザーがアプリを再インストールすると、ローミング データがクラウドから同期されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-177">If the user reinstalls the app within the time interval, the roaming data is synchronized from the cloud.</span></span>

### <a name="roaming-data-dos-and-donts"></a><span data-ttu-id="85cb3-178">データのローミングの推奨事項と非推奨事項</span><span class="sxs-lookup"><span data-stu-id="85cb3-178">Roaming data do's and don'ts</span></span>

-   <span data-ttu-id="85cb3-179">ユーザーの基本設定やカスタマイズ、リンク、小さなデータ ファイルにローミングを使います。</span><span class="sxs-lookup"><span data-stu-id="85cb3-179">Use roaming for user preferences and customizations, links, and small data files.</span></span> <span data-ttu-id="85cb3-180">たとえば、ローミングを使って、ユーザーの背景色の基本設定をすべてのデバイスで保持します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-180">For example, use roaming to preserve a user's background color preference across all devices.</span></span>
-   <span data-ttu-id="85cb3-181">ユーザーがデバイス間で作業を続けられるようにローミングを使います。</span><span class="sxs-lookup"><span data-stu-id="85cb3-181">Use roaming to let users continue a task across devices.</span></span> <span data-ttu-id="85cb3-182">たとえば、下書きしたメールの内容やリーダー アプリで最近表示したページなどのアプリ データをローミングします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-182">For example, roam app data like the contents of an drafted email or the most recently viewed page in a reader app.</span></span>
-   <span data-ttu-id="85cb3-183">アプリ データを更新して、[**DataChanged**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.datachanged) イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-183">Handle the [**DataChanged**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.datachanged) event by updating app data.</span></span> <span data-ttu-id="85cb3-184">このイベントは、クラウドからのアプリ データの同期が完了したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-184">This event occurs when app data has just finished syncing from the cloud.</span></span>
-   <span data-ttu-id="85cb3-185">生データではなくコンテンツへの参照をローミングします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-185">Roam references to content rather than raw data.</span></span> <span data-ttu-id="85cb3-186">たとえば、オンライン記事のコンテンツではなく URL をローミングします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-186">For example, roam a URL rather than the content of an online article.</span></span>
-   <span data-ttu-id="85cb3-187">タイム クリティカルな重要な設定に対しては、[**RoamingSettings**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingsettings) に関連付けられた *HighPriority* 設定を使います。</span><span class="sxs-lookup"><span data-stu-id="85cb3-187">For important, time critical settings, use the *HighPriority* setting associated with [**RoamingSettings**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingsettings).</span></span>
-   <span data-ttu-id="85cb3-188">デバイス固有のアプリ データをローミングしないでください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-188">Don't roam app data that is specific to a device.</span></span> <span data-ttu-id="85cb3-189">ローカルにあるファイル リソースのパス名など、ローカルのみに関連した情報もあります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-189">Some info is only pertinent locally, such as a path name to a local file resource.</span></span> <span data-ttu-id="85cb3-190">ローカル情報をローミングする場合は、その情報が別のデバイスで無効なときにアプリを回復できることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-190">If you do decide to roam local information, make sure that the app can recover if the info isn't valid on the secondary device.</span></span>
-   <span data-ttu-id="85cb3-191">大量のアプリ データをローミングしないでください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-191">Don't roam large sets of app data.</span></span> <span data-ttu-id="85cb3-192">アプリでローミングできるアプリ データの量には制限があります。この最大値を取得するには、[**RoamingStorageQuota**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingstoragequota) プロパティを使ってください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-192">There's a limit to the amount of app data an app may roam; use [**RoamingStorageQuota**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingstoragequota) property to get this maximum.</span></span> <span data-ttu-id="85cb3-193">この制限に達した場合、アプリ データのサイズが制限を下回るまで、データはローミングできません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-193">If an app hits this limit, no data can roam until the size of the app data store no longer exceeds the limit.</span></span> <span data-ttu-id="85cb3-194">アプリを設計する際は、この制限を超えないようにサイズの大きいデータをどのように制限するかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-194">When you design your app, consider how to put a bound on larger data so as to not exceed the limit.</span></span> <span data-ttu-id="85cb3-195">たとえば、ゲームの状態を保存するのにそれぞれ 10 KB 必要になる場合は、ユーザーによる保存を 10 ゲームまでに制限したりすると効果的です。</span><span class="sxs-lookup"><span data-stu-id="85cb3-195">For example, if saving a game state requires 10KB each, the app might only allow the user store up to 10 games.</span></span>
-   <span data-ttu-id="85cb3-196">即時同期に依存するデータにローミングを使わないでください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-196">Don't use roaming for data that relies on instant syncing.</span></span> <span data-ttu-id="85cb3-197">Windows では即時同期が保証されません。ユーザーがオフラインであったり、待ち時間の長いネットワークを使っている場合、ローミングはかなり遅れる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-197">Windows doesn't guarantee an instant sync; roaming could be significantly delayed if a user is offline or on a high latency network.</span></span> <span data-ttu-id="85cb3-198">UI が即時同期に依存しないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-198">Ensure that your UI doesn't depend on instant syncing.</span></span>
-   <span data-ttu-id="85cb3-199">頻繁に変更されるデータのローミングを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-199">Don't use roaming for frequently changing data.</span></span> <span data-ttu-id="85cb3-200">たとえば、再生中の曲の秒刻みの位置など、頻繁に変更される情報を追跡する場合は、この情報をローミング アプリ データとして保存しないでください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-200">For example, if your app tracks frequently changing info, such as the position in a song by second, don't store this as roaming app data.</span></span> <span data-ttu-id="85cb3-201">代わりに、現在再生中の曲など、変更の頻度が少なく、ユーザー エクスペリエンスも損なわないような情報を利用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-201">Instead, pick a less frequent representation that still provides a good user experience, like the currently playing song.</span></span>

### <a name="roaming-pre-requisites"></a><span data-ttu-id="85cb3-202">ローミングの前提条件</span><span class="sxs-lookup"><span data-stu-id="85cb3-202">Roaming pre-requisites</span></span>

<span data-ttu-id="85cb3-203">アプリ データのローミングは、Microsoft アカウントを使ってデバイスにログインするすべてのユーザーに利点をもたらします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-203">Any user can benefit from roaming app data if they use a Microsoft account to log on to their device.</span></span> <span data-ttu-id="85cb3-204">ただし、いつでもデバイスでアプリ データのローミングを切り替えることができるのは、ユーザーとグループ ポリシーの管理者です。</span><span class="sxs-lookup"><span data-stu-id="85cb3-204">However, users and group policy administrators can switch off roaming app data on a device at any time.</span></span> <span data-ttu-id="85cb3-205">ユーザーは、Microsoft アカウントを使用しないように選択またはローミング データの機能を無効にします。、アプリを使用して、彼女はできますが、アプリ データは、各デバイスにローカルになります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-205">If a user chooses not to use a Microsoft account or disables roaming data capabilities, she will still be able to use your app, but app data will be local to each device.</span></span>

<span data-ttu-id="85cb3-206">[  **PasswordVault**](https://docs.microsoft.com/uwp/api/Windows.Security.Credentials.PasswordVault) に格納されているデータは、ユーザーが "信頼" しているデバイスにしか移行されません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-206">Data stored in the [**PasswordVault**](https://docs.microsoft.com/uwp/api/Windows.Security.Credentials.PasswordVault) will only transition if a user has made a device “trusted”.</span></span> <span data-ttu-id="85cb3-207">デバイスが信頼されていない場合、この資格情報コンテナーのセキュリティで確保されているデータはローミングされません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-207">If a device isn't trusted, data secured in this vault will not roam.</span></span>

### <a name="conflict-resolution"></a><span data-ttu-id="85cb3-208">競合の解決</span><span class="sxs-lookup"><span data-stu-id="85cb3-208">Conflict resolution</span></span>

<span data-ttu-id="85cb3-209">アプリ データのローミングは、複数のデバイスでの同時使用を想定していません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-209">Roaming app data is not intended for simultaneous use on more than one device at a time.</span></span> <span data-ttu-id="85cb3-210">2 台のデバイスで特定のデータ単位が変更されたことが原因で同期中に競合が発生した場合、最後に書き込まれた値が常に優先されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-210">If a conflict arises during synchronization because a particular data unit was changed on two devices, the system will always favor the value that was written last.</span></span> <span data-ttu-id="85cb3-211">これにより、アプリで最新の情報が利用されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-211">This ensures that the app utilizes the most up-to-date information.</span></span> <span data-ttu-id="85cb3-212">データ単位が設定コンポジットの場合、競合の解決は設定の単位で行われ、最新の変更を含むコンポジットが同期されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-212">If the data unit is a setting composite, conflict resolution will still occur on the level of the setting unit, which means that the composite with the latest change will be synchronized.</span></span>

### <a name="when-to-write-data"></a><span data-ttu-id="85cb3-213">データを書き込むタイミング</span><span class="sxs-lookup"><span data-stu-id="85cb3-213">When to write data</span></span>

<span data-ttu-id="85cb3-214">想定される設定の有効期間に応じて、データを書き込むタイミングを変える必要があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-214">Depending on the expected lifetime of the setting, data should be written at different times.</span></span> <span data-ttu-id="85cb3-215">変更の頻度が低いアプリ データや変更間隔の長いアプリ データは、変更されたらすぐに書き込むようにします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-215">Infrequently or slowly changing app data should be written immediately.</span></span> <span data-ttu-id="85cb3-216">ただし、頻繁に変更されるアプリ データは、アプリが中断されたとき以外は、一定の間隔 (5 分に 1 回など) でのみ書き込むようにします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-216">However, app data that changes frequently should only be written periodically at regular intervals (such as once every 5 minutes), as well as when the app is suspended.</span></span> <span data-ttu-id="85cb3-217">たとえば、音楽アプリでは、"現在の曲" の設定は新しい曲の再生が始まるたびに書き込みますが、曲の途中の実際の位置は中断したときにのみ書き込みます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-217">For example, a music app might write the “current song” settings whenever a new song starts to play, however, the actual position in the song should only be written on suspend.</span></span>

### <a name="excessive-usage-protection"></a><span data-ttu-id="85cb3-218">使いすぎに対する保護</span><span class="sxs-lookup"><span data-stu-id="85cb3-218">Excessive usage protection</span></span>

<span data-ttu-id="85cb3-219">リソースの不適切な使用を防止するために、システムにはさまざまな保護メカニズムが備わっています。</span><span class="sxs-lookup"><span data-stu-id="85cb3-219">The system has various protection mechanisms in place to avoid inappropriate use of resources.</span></span> <span data-ttu-id="85cb3-220">アプリ データが想定どおりに移行されない場合は、デバイスが一時的に制限されていることが考えられます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-220">If app data does not transition as expected, it is likely that the device has been temporarily restricted.</span></span> <span data-ttu-id="85cb3-221">通常、この状況はしばらくすると自動的に解決されるため、操作は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-221">Waiting for some time will usually resolve this situation automatically and no action is required.</span></span>

### <a name="versioning"></a><span data-ttu-id="85cb3-222">バージョン</span><span class="sxs-lookup"><span data-stu-id="85cb3-222">Versioning</span></span>

<span data-ttu-id="85cb3-223">アプリ データは、バージョンに基づいてデータ構造をアップグレードできます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-223">App data can utilize versioning to upgrade from one data structure to another.</span></span> <span data-ttu-id="85cb3-224">バージョン番号は、アプリのバージョンとは別の番号で、自由に設定することができます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-224">The version number is different from the app version and can be set at will.</span></span> <span data-ttu-id="85cb3-225">強制ではありませんが、バージョン番号は新しいデータほど大きくすることを強くお勧めします。新しいデータを表すバージョン番号が小さくなると、データ損失などの望ましくない問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-225">Although not enforced, it is highly recommended that you use increasing version numbers, since undesirable complications (including data loss)could occur if you try to transition to a lower data version number that represents newer data.</span></span>

<span data-ttu-id="85cb3-226">アプリ データのローミングは、バージョン番号が同じインストールされたアプリの間でしか行われません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-226">App data only roams between installed apps with the same version number.</span></span> <span data-ttu-id="85cb3-227">たとえば、どちらもバージョン 2 のデバイスの間やどちらもバージョン 3 のデバイスの間ではデータが移行されますが、バージョン 2 を実行中のデバイスとバージョン 3 を実行中のデバイスの間ではローミングは行われません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-227">For example, devices on version 2 will transition data between each other and devices on version 3 will do the same, but no roaming will occur between a device running version 2 and a device running version 3.</span></span> <span data-ttu-id="85cb3-228">他のデバイスでさまざまなバージョン番号を利用していたアプリを新たにインストールする場合、新たにインストールしたアプリは、最も大きいバージョン番号と関連付けられているアプリ データを同期します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-228">If you install a new app that utilized various version numbers on other devices, the newly installed app will sync the app data associated with the highest version number.</span></span>

### <a name="testing-and-tools"></a><span data-ttu-id="85cb3-229">テストとツール</span><span class="sxs-lookup"><span data-stu-id="85cb3-229">Testing and tools</span></span>

<span data-ttu-id="85cb3-230">開発者は、ローミング アプリ データの同期をトリガーするためにデバイスをロックできます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-230">Developers can lock their device in order to trigger a synchronization of roaming app data.</span></span> <span data-ttu-id="85cb3-231">一定の期間にわたってアプリ データが移行されていない場合は、次の点を確認してください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-231">If it seems that the app data does not transition within a certain time frame, please check the following items and make sure that:</span></span>

-   <span data-ttu-id="85cb3-232">ローミング データが最大サイズを超えていないこと (詳しくは、「[**RoamingStorageQuota**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingstoragequota)」をご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="85cb3-232">Your roaming data does not exceed the maximum size (see [**RoamingStorageQuota**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingstoragequota) for details).</span></span>
-   <span data-ttu-id="85cb3-233">ファイルが閉じていて、適切に解放されていること。</span><span class="sxs-lookup"><span data-stu-id="85cb3-233">Your files are closed and released properly.</span></span>
-   <span data-ttu-id="85cb3-234">同じバージョンのアプリを実行しているデバイスが 2 台以上あること。</span><span class="sxs-lookup"><span data-stu-id="85cb3-234">There are at least two devices running the same version of the app.</span></span>


### <a name="register-to-receive-notification-when-roaming-data-changes"></a><span data-ttu-id="85cb3-235">ローミング データが変更された場合に通知を受け取るように登録する</span><span class="sxs-lookup"><span data-stu-id="85cb3-235">Register to receive notification when roaming data changes</span></span>

<span data-ttu-id="85cb3-236">アプリのローミング データを使用するには、ローミング データの変更に備えて登録し、設定を読み書きできるように、ローミング データのコンテナーを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-236">To use roaming app data, you need to register for roaming data changes and retrieve the roaming data containers so you can read and write settings.</span></span>

1.  <span data-ttu-id="85cb3-237">ローミング データが変更されたときに通知を受け取るように登録します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-237">Register to receive notification when roaming data changes.</span></span>

    <span data-ttu-id="85cb3-238">[  **DataChanged**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.datachanged) イベントで、ローミング データが変更されたときに通知します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-238">The [**DataChanged**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.datachanged) event notifies you when roaming data changes.</span></span> <span data-ttu-id="85cb3-239">この例では、ローミング データの変更のハンドラーとして `DataChangeHandler` を設定します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-239">This example sets `DataChangeHandler` as the handler for roaming data changes.</span></span>

```csharp
void InitHandlers()
    {
       Windows.Storage.ApplicationData.Current.DataChanged += 
          new TypedEventHandler<ApplicationData, object>(DataChangeHandler);
    }

    void DataChangeHandler(Windows.Storage.ApplicationData appData, object o)
    {
       // TODO: Refresh your data
    }
```

2.  <span data-ttu-id="85cb3-240">アプリの設定とファイルのコンテナーを取得します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-240">Get the containers for the app's settings and files.</span></span>

    <span data-ttu-id="85cb3-241">設定を取得するには [**ApplicationData.RoamingSettings**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingsettings) プロパティを、ファイルを取得するには [**ApplicationData.RoamingFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingfolder) プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-241">Use the [**ApplicationData.RoamingSettings**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingsettings) property to get the settings and the [**ApplicationData.RoamingFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingfolder) property to get the files.</span></span>

```csharp
Windows.Storage.ApplicationDataContainer roamingSettings = 
        Windows.Storage.ApplicationData.Current.RoamingSettings;
    Windows.Storage.StorageFolder roamingFolder = 
        Windows.Storage.ApplicationData.Current.RoamingFolder;
```

### <a name="create-and-retrieve-roaming-settings"></a><span data-ttu-id="85cb3-242">ローミング設定を作成して取得する</span><span class="sxs-lookup"><span data-stu-id="85cb3-242">Create and retrieve roaming settings</span></span>

<span data-ttu-id="85cb3-243">前のセクションで取得した `roamingSettings` コンテナー内の設定にアクセスするには、[**ApplicationDataContainer.Values**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.values) プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-243">Use the [**ApplicationDataContainer.Values**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.values) property to access the settings in the `roamingSettings` container we got in the previous section.</span></span> <span data-ttu-id="85cb3-244">次の例では、`exampleSetting` という名前の簡易設定と、`composite` という名前のコンポジット値を作成します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-244">This example creates a simple setting named `exampleSetting` and a composite value named `composite`.</span></span>

```csharp
// Simple setting

roamingSettings.Values["exampleSetting"] = "Hello World";
// High Priority setting, for example, last page position in book reader app
roamingSettings.values["HighPriority"] = "65";

// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
    new Windows.Storage.ApplicationDataCompositeValue();
composite["intVal"] = 1;
composite["strVal"] = "string";

roamingSettings.Values["exampleCompositeSetting"] = composite;

```

<span data-ttu-id="85cb3-245">この例では作成した設定を取得します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-245">This example retrieves the settings we just created.</span></span>

```csharp
// Simple setting

Object value = roamingSettings.Values["exampleSetting"];

// Composite setting

Windows.Storage.ApplicationDataCompositeValue composite = 
   (Windows.Storage.ApplicationDataCompositeValue)roamingSettings.Values["exampleCompositeSetting"];

if (composite == null)
{
   // No data
}
else
{
   // Access data in composite["intVal"] and composite["strVal"]
}
```

### <a name="create-and-retrieve-roaming-files"></a><span data-ttu-id="85cb3-246">ローミング ファイルを作成して取得する</span><span class="sxs-lookup"><span data-stu-id="85cb3-246">Create and retrieve roaming files</span></span>

<span data-ttu-id="85cb3-247">ローミング アプリ データ ストアでファイルを作成して更新するには、[**Windows.Storage.StorageFolder.CreateFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfileasync) や [**Windows.Storage.FileIO.WriteTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.writetextasync) などのファイル API を使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-247">To create and update a file in the roaming app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.CreateFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfileasync) and [**Windows.Storage.FileIO.WriteTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.writetextasync).</span></span> <span data-ttu-id="85cb3-248">次の例では、`roamingFolder` コンテナーに `dataFile.txt` という名前のファイルを作成し、現在の日付と時刻をファイルに書き込みます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-248">This example creates a file named `dataFile.txt` in the `roamingFolder` container and writes the current date and time to the file.</span></span> <span data-ttu-id="85cb3-249">[  **CreationCollisionOption**](https://docs.microsoft.com/uwp/api/Windows.Storage.CreationCollisionOption) 列挙体の **ReplaceExisting** 値は、ファイルが既にある場合にファイルを置き換えることを示します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-249">The **ReplaceExisting** value from the [**CreationCollisionOption**](https://docs.microsoft.com/uwp/api/Windows.Storage.CreationCollisionOption) enumeration indicates to replace the file if it already exists.</span></span>

```csharp
async void WriteTimestamp()
{
   Windows.Globalization.DateTimeFormatting.DateTimeFormatter formatter = 
       new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("longtime");

   StorageFile sampleFile = await roamingFolder.CreateFileAsync("dataFile.txt", 
       CreationCollisionOption.ReplaceExisting);
   await FileIO.WriteTextAsync(sampleFile, formatter.Format(DateTimeOffset.Now));
}
```

<span data-ttu-id="85cb3-250">ローミング アプリ データ ストアのファイルを開いて読み取るには、[**Windows.Storage.StorageFolder.GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfileasync)、[**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync)、[**Windows.Storage.FileIO.ReadTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.readtextasync) などのファイル API を使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-250">To open and read a file in the roaming app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfileasync), [**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync), and [**Windows.Storage.FileIO.ReadTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.readtextasync).</span></span> <span data-ttu-id="85cb3-251">この例では、前のセクションで作成した `dataFile.txt` ファイルを開き、ファイルから日付を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-251">This example opens the `dataFile.txt` file created in the previous section and reads the date from the file.</span></span> <span data-ttu-id="85cb3-252">さまざまな場所からファイル リソースを読み込む方法について詳しくは、「[ファイル リソースを読み込む方法](https://docs.microsoft.com/previous-versions/windows/apps/hh965322(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-252">For details on loading file resources from various locations, see [How to load file resources](https://docs.microsoft.com/previous-versions/windows/apps/hh965322(v=win.10)).</span></span>

```csharp
async void ReadTimestamp()
{
   try
   {
      StorageFile sampleFile = await roamingFolder.GetFileAsync("dataFile.txt");
      String timestamp = await FileIO.ReadTextAsync(sampleFile);
      // Data is contained in timestamp
   }
   catch (Exception)
   {
      // Timestamp not found
   }
}
```


## <a name="temporary-app-data"></a><span data-ttu-id="85cb3-253">一時アプリ データ</span><span class="sxs-lookup"><span data-stu-id="85cb3-253">Temporary app data</span></span>


<span data-ttu-id="85cb3-254">一時アプリ データ ストアは、キャッシュのような働きをします。</span><span class="sxs-lookup"><span data-stu-id="85cb3-254">The temporary app data store works like a cache.</span></span> <span data-ttu-id="85cb3-255">ファイルはローミングされず、任意の時点で削除されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-255">Its files do not roam and could be removed at any time.</span></span> <span data-ttu-id="85cb3-256">システム メンテナンス タスクを使うと、この場所に格納されているデータをいつでも自動的に削除できます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-256">The System Maintenance task can automatically delete data stored at this location at any time.</span></span> <span data-ttu-id="85cb3-257">ディスク クリーンアップを使って、一時データ ストアからファイルを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-257">The user can also clear files from the temporary data store using Disk Cleanup.</span></span> <span data-ttu-id="85cb3-258">一時アプリ データは、アプリ セッションの一時的な情報の格納に使うことができます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-258">Temporary app data can be used for storing temporary information during an app session.</span></span> <span data-ttu-id="85cb3-259">このデータは、アプリ セッションの終了後に保持されるという保証はありません。必要に応じて使用領域が再利用されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-259">There is no guarantee that this data will persist beyond the end of the app session as the system might reclaim the used space if needed.</span></span> <span data-ttu-id="85cb3-260">この場所には、[**temporaryFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) プロパティを使ってアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-260">The location is available via the [**temporaryFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) property.</span></span>

### <a name="retrieve-the-temporary-data-container"></a><span data-ttu-id="85cb3-261">一時データコンテナーを取得する</span><span class="sxs-lookup"><span data-stu-id="85cb3-261">Retrieve the temporary data container</span></span>

<span data-ttu-id="85cb3-262">ファイルを取得するには [**ApplicationData.TemporaryFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-262">Use the [**ApplicationData.TemporaryFolder**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) property to get the files.</span></span> <span data-ttu-id="85cb3-263">以降の手順では、この手順の `temporaryFolder` 変数を使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-263">The next steps use the `temporaryFolder` variable from this step.</span></span>

```csharp
Windows.Storage.StorageFolder temporaryFolder = ApplicationData.Current.TemporaryFolder;
```

### <a name="create-and-read-temporary-files"></a><span data-ttu-id="85cb3-264">一時ファイルを作成して読み取る</span><span class="sxs-lookup"><span data-stu-id="85cb3-264">Create and read temporary files</span></span>

<span data-ttu-id="85cb3-265">一時アプリ データ ストアにファイルを作成して更新するには、[**Windows.Storage.StorageFolder.CreateFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfileasync) や [**Windows.Storage.FileIO.WriteTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.writetextasync) などのファイル API を使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-265">To create and update a file in the temporary app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.CreateFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.createfileasync) and [**Windows.Storage.FileIO.WriteTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.writetextasync).</span></span> <span data-ttu-id="85cb3-266">次の例では、`temporaryFolder` コンテナーに `dataFile.txt` という名前のファイルを作成し、現在の日付と時刻をファイルに書き込みます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-266">This example creates a file named `dataFile.txt` in the `temporaryFolder` container and writes the current date and time to the file.</span></span> <span data-ttu-id="85cb3-267">[  **CreationCollisionOption**](https://docs.microsoft.com/uwp/api/Windows.Storage.CreationCollisionOption) 列挙体の **ReplaceExisting** 値は、ファイルが既にある場合にファイルを置き換えることを示します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-267">The **ReplaceExisting** value from the [**CreationCollisionOption**](https://docs.microsoft.com/uwp/api/Windows.Storage.CreationCollisionOption) enumeration indicates to replace the file if it already exists.</span></span>


```csharp
async void WriteTimestamp()
{
   Windows.Globalization.DateTimeFormatting.DateTimeFormatter formatter = 
       new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("longtime");

   StorageFile sampleFile = await temporaryFolder.CreateFileAsync("dataFile.txt", 
       CreateCollisionOption.ReplaceExisting);
   await FileIO.WriteTextAsync(sampleFile, formatter.Format(DateTimeOffset.Now));
}
```

<span data-ttu-id="85cb3-268">一時アプリ データ ストアのファイルを開いて読み取るには、[**Windows.Storage.StorageFolder.GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfileasync)、[**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync)、[**Windows.Storage.FileIO.ReadTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.readtextasync) などのファイル API を使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-268">To open and read a file in the temporary app data store, use the file APIs, such as [**Windows.Storage.StorageFolder.GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfileasync), [**Windows.Storage.StorageFile.GetFileFromApplicationUriAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefile.getfilefromapplicationuriasync), and [**Windows.Storage.FileIO.ReadTextAsync**](https://docs.microsoft.com/uwp/api/windows.storage.fileio.readtextasync).</span></span> <span data-ttu-id="85cb3-269">この例では、前の手順で作成した `dataFile.txt` ファイルを開き、ファイルから日付を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="85cb3-269">This example opens the `dataFile.txt` file created in the previous step and reads the date from the file.</span></span> <span data-ttu-id="85cb3-270">さまざまな場所からファイル リソースを読み込む方法について詳しくは、「[ファイル リソースを読み込む方法](https://docs.microsoft.com/previous-versions/windows/apps/hh965322(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-270">For details on loading file resources from various locations, see [How to load file resources](https://docs.microsoft.com/previous-versions/windows/apps/hh965322(v=win.10)).</span></span>

```csharp
async void ReadTimestamp()
{
   try
   {
      StorageFile sampleFile = await temporaryFolder.GetFileAsync("dataFile.txt");
      String timestamp = await FileIO.ReadTextAsync(sampleFile);
      // Data is contained in timestamp
   }
   catch (Exception)
   {
      // Timestamp not found
   }
}
```

## <a name="organize-app-data-with-containers"></a><span data-ttu-id="85cb3-271">コンテナーでアプリ データを整理する</span><span class="sxs-lookup"><span data-stu-id="85cb3-271">Organize app data with containers</span></span>


<span data-ttu-id="85cb3-272">アプリ データの設定とファイルを整理するには、ディレクトリで直接作業するのではなく、コンテナー ([**ApplicationDataContainer**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataContainer) オブジェクトで表されます) を作成します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-272">To help you organize your app data settings and files, you create containers (represented by [**ApplicationDataContainer**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataContainer) objects) instead of working directly with directories.</span></span> <span data-ttu-id="85cb3-273">コンテナーは、ローカル アプリ データ ストア、ローミング アプリ データ ストア、一時アプリ データ ストアに追加できます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-273">You can add containers to the local, roaming, and temporary app data stores.</span></span> <span data-ttu-id="85cb3-274">コンテナーは 32 階層まで入れ子にすることができます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-274">Containers can be nested up to 32 levels deep.</span></span>

<span data-ttu-id="85cb3-275">設定コンテナーを作成するには、[**ApplicationDataContainer.CreateContainer**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.createcontainer) メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-275">To create a settings container, call the [**ApplicationDataContainer.CreateContainer**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.createcontainer) method.</span></span> <span data-ttu-id="85cb3-276">次の例では、`exampleContainer` という名前のローカル設定コンテナーを作成し、`exampleSetting` という名前の設定を追加します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-276">This example creates a local settings container named `exampleContainer` and adds a setting named `exampleSetting`.</span></span> <span data-ttu-id="85cb3-277">[  **ApplicationDataCreateDisposition**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataCreateDisposition) 列挙体の **Always** 値は、コンテナーがまだない場合に作成されることを示します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-277">The **Always** value from the [**ApplicationDataCreateDisposition**](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataCreateDisposition) enumeration indicates that the container is created if it doesn't already exist.</span></span>

```csharp
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Setting in a container
Windows.Storage.ApplicationDataContainer container = 
   localSettings.CreateContainer("exampleContainer", Windows.Storage.ApplicationDataCreateDisposition.Always);

if (localSettings.Containers.ContainsKey("exampleContainer"))
{
   localSettings.Containers["exampleContainer"].Values["exampleSetting"] = "Hello Windows";
}
```

## <a name="delete-app-settings-and-containers"></a><span data-ttu-id="85cb3-278">アプリの設定とコンテナーを削除する</span><span class="sxs-lookup"><span data-stu-id="85cb3-278">Delete app settings and containers</span></span>


<span data-ttu-id="85cb3-279">アプリでもう必要のない簡易設定を削除するには、[**ApplicationDataContainerSettings.Remove**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainersettings.remove) メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-279">To delete a simple setting that your app no longer needs, use the [**ApplicationDataContainerSettings.Remove**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainersettings.remove) method.</span></span> <span data-ttu-id="85cb3-280">この例では、前の手順で作成した `exampleSetting` ローカル設定を削除します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-280">This example deletesthe `exampleSetting` local setting that we created earlier.</span></span>

```csharp
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Delete simple setting

localSettings.Values.Remove("exampleSetting");
```

<span data-ttu-id="85cb3-281">コンポジット設定を削除するには、[**ApplicationDataCompositeValue.Remove**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacompositevalue.remove) メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-281">To delete a composite setting, use the [**ApplicationDataCompositeValue.Remove**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacompositevalue.remove) method.</span></span> <span data-ttu-id="85cb3-282">この例では、前の例で作成したローカルの `exampleCompositeSetting` コンポジット設定を削除します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-282">This example deletes the local `exampleCompositeSetting` composite setting we created in an earlier example.</span></span>

```csharp
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Delete composite setting

localSettings.Values.Remove("exampleCompositeSetting");
```

<span data-ttu-id="85cb3-283">コンテナーを削除するには、[**ApplicationDataContainer.DeleteContainer**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.deletecontainer) メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-283">To delete a container, call the [**ApplicationDataContainer.DeleteContainer**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdatacontainer.deletecontainer) method.</span></span> <span data-ttu-id="85cb3-284">この例では、前の手順で作成したローカルの `exampleContainer` 設定コンテナーを削除します。</span><span class="sxs-lookup"><span data-stu-id="85cb3-284">This example deletes the local `exampleContainer` settings container we created earlier.</span></span>

```csharp
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
Windows.Storage.StorageFolder localFolder = 
    Windows.Storage.ApplicationData.Current.LocalFolder;

// Delete container

localSettings.DeleteContainer("exampleContainer");
```

## <a name="versioning-your-app-data"></a><span data-ttu-id="85cb3-285">アプリ データのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="85cb3-285">Versioning your app data</span></span>


<span data-ttu-id="85cb3-286">必要に応じて、アプリのアプリ データをバージョン管理することもできます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-286">You can optionally version the app data for your app.</span></span> <span data-ttu-id="85cb3-287">これにより、将来作成するアプリのバージョンでアプリ データの形式を変更しても、以前のバージョンとの互換性に問題が起こりません。</span><span class="sxs-lookup"><span data-stu-id="85cb3-287">This would enable you to create a future version of your app that changes the format of its app data without causing compatibility problems with the previous version of your app.</span></span> <span data-ttu-id="85cb3-288">データ ストア内のアプリ データのバージョンをアプリが確認し、以前のバージョンであった場合、アプリ データは新しい形式に更新され、バージョンも更新されます。</span><span class="sxs-lookup"><span data-stu-id="85cb3-288">The app checks the version of the app data in the data store, and if the version is less than the version the app expects, the app should update the app data to the new format and update the version.</span></span> <span data-ttu-id="85cb3-289">詳しくは、「[**Application.Version**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.version) プロパティ」と「[**ApplicationData.SetVersionAsync**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.) メソッド」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="85cb3-289">For more info, see the[**Application.Version**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.version) property and the [**ApplicationData.SetVersionAsync**](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.) method.</span></span>

## <a name="related-articles"></a><span data-ttu-id="85cb3-290">関連記事</span><span class="sxs-lookup"><span data-stu-id="85cb3-290">Related articles</span></span>

* [<span data-ttu-id="85cb3-291">**Windows.Storage.ApplicationData**</span><span class="sxs-lookup"><span data-stu-id="85cb3-291">**Windows.Storage.ApplicationData**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationData)
* [<span data-ttu-id="85cb3-292">**Windows.Storage.ApplicationData.RoamingSettings**</span><span class="sxs-lookup"><span data-stu-id="85cb3-292">**Windows.Storage.ApplicationData.RoamingSettings**</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingsettings)
* [<span data-ttu-id="85cb3-293">**Windows.Storage.ApplicationData.RoamingFolder**</span><span class="sxs-lookup"><span data-stu-id="85cb3-293">**Windows.Storage.ApplicationData.RoamingFolder**</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingfolder)
* [<span data-ttu-id="85cb3-294">**Windows.Storage.ApplicationData.RoamingStorageQuota**</span><span class="sxs-lookup"><span data-stu-id="85cb3-294">**Windows.Storage.ApplicationData.RoamingStorageQuota**</span></span>](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.roamingstoragequota)
* [<span data-ttu-id="85cb3-295">**Windows.Storage.ApplicationDataCompositeValue**</span><span class="sxs-lookup"><span data-stu-id="85cb3-295">**Windows.Storage.ApplicationDataCompositeValue**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.ApplicationDataCompositeValue)
