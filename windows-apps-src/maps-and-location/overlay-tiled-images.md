---
title: 地図へのタイル画像のオーバーレイ
description: タイル ソースを使って、地図上にサード パーティ製タイルまたはカスタム タイル画像をオーバーレイします。 タイル ソースを使って、気象データ、人口データ、地質データなどの特殊な情報をオーバーレイすることや、既定の地図を完全に置き換えることができます。
ms.assetid: 066BD6E2-C22B-4F5B-AA94-5D6C86A09BDF
ms.date: 07/19/2018
ms.topic: article
keywords: Windows 10、UWP、地図、位置情報、画像、オーバーレイ
ms.localizationpriority: medium
ms.openlocfilehash: e9b4d439958e6cfbf0845aaf5bcd31644ff39432
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371683"
---
# <a name="overlay-tiled-images-on-a-map"></a><span data-ttu-id="7ec0f-105">地図へのタイル画像のオーバーレイ</span><span class="sxs-lookup"><span data-stu-id="7ec0f-105">Overlay tiled images on a map</span></span>

<span data-ttu-id="7ec0f-106">タイル ソースを使って、地図上にサード パーティ製タイルまたはカスタム タイル画像をオーバーレイします。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-106">Overlay third-party or custom tiled images on a map by using tile sources.</span></span> <span data-ttu-id="7ec0f-107">タイル ソースを使って、気象データ、人口データ、地質データなどの特殊な情報をオーバーレイすることや、既定の地図を完全に置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-107">Use tile sources to overlay specialized information such as weather data, population data, or seismic data; or use tile sources to replace the default map entirely.</span></span>

<span data-ttu-id="7ec0f-108">**ヒント** アプリでの地図の使用について詳しくは、Github で[ユニバーサル Windows プラットフォーム (UWP) の地図サンプル](https://go.microsoft.com/fwlink/p/?LinkId=619977)をダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-108">**Tip** To learn more about using maps in your app, download the [Universal Windows Platform (UWP) map sample](https://go.microsoft.com/fwlink/p/?LinkId=619977) on Github.</span></span>

<a id="tileintro" />

## <a name="tiled-image-overview"></a><span data-ttu-id="7ec0f-109">タイル画像の概要</span><span class="sxs-lookup"><span data-stu-id="7ec0f-109">Tiled image overview</span></span>

<span data-ttu-id="7ec0f-110">Nokia Maps や Bing Maps などのマップ サービスでは、迅速な取得と表示のために正方形タイルに地図を切り取ります。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-110">Map services such as Nokia Maps and Bing Maps cut maps into square tiles for quick retrieval and display.</span></span> <span data-ttu-id="7ec0f-111">こうしたタイルは 256 ピクセル x 256 ピクセル サイズであり、いくつかの詳細レベルで事前にレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-111">These tiles are 256 pixels by 256 pixels in size, and are pre-rendered at multiple levels of detail.</span></span> <span data-ttu-id="7ec0f-112">また、多くのサード パーティ サービスがタイルに切り取られた地図ベースのデータを提供しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-112">Many third-party services also provide map-based data that's cut into tiles.</span></span> <span data-ttu-id="7ec0f-113">タイル ソースを使ってサード パーティ製タイルを取得するか、独自のカスタム タイルを作成してそれを [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) に表示された地図上にオーバーレイできます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-113">Use tile sources to retrieve third-party tiles, or to create your own custom tiles, and overlay them on the map displayed in the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span>

<span data-ttu-id="7ec0f-114">**重要な**  タイル ソースを使用する場合を要求する、または個々 のタイルの位置にコードを記述する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-114">**Important**   When you use tile sources, you don't have to write code to request or to position individual tiles.</span></span> <span data-ttu-id="7ec0f-115">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) が必要時にタイルを要求します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-115">The [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) requests tiles as it needs them.</span></span> <span data-ttu-id="7ec0f-116">各要求では、個々のタイルについて X 座標と Y 座標、ズーム レベルを指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-116">Each request specifies the X and Y coordinates and the zoom level for the individual tile.</span></span> <span data-ttu-id="7ec0f-117">タイルを取得するために使う URI またはファイル名の形式を **UriFormatString** プロパティに指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-117">You simply specify the format of the Uri or filename to use to retrieve the tiles in the **UriFormatString** property.</span></span> <span data-ttu-id="7ec0f-118">つまり、各タイルの X 座標、Y 座標、ズーム レベルを渡す場所を示すベース URI またはファイル名に、置き換え可能なパラメーターを挿入します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-118">That is, you insert replaceable parameters in the base Uri or filename to indicate where to pass the X and Y coordinates and the zoom level for each tile.</span></span>

<span data-ttu-id="7ec0f-119">次に、X 座標、Y 座標、ズーム レベルの置き換え可能なパラメーターを示す [**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) の [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) プロパティの例を示します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-119">Here's an example of the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) property for an [**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) that shows the replaceable parameters for the X and Y coordinates and the zoom level.</span></span>

```syntax
http://www.<web service name>.com/z={zoomlevel}&x={x}&y={y}
```

<span data-ttu-id="7ec0f-120">X 座標と Y 座標は、指定された詳細レベルで世界地図内の個々のタイルの場所を表します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-120">(The X and Y coordinates represent the location of the individual tile within the map of the world at the specified level of detail.</span></span> <span data-ttu-id="7ec0f-121">タイルの番号付けは、地図の左上端の {0, 0} から開始します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-121">The tile numbering system starts from {0, 0} in the upper left corner of the map.</span></span> <span data-ttu-id="7ec0f-122">たとえば、{1, 2} のタイルは、タイル グリッドの第 1 行の第 2 列にあります。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-122">For example, the tile at {1, 2} is in the second column of the third row of the grid of tiles.)</span></span>

<span data-ttu-id="7ec0f-123">マッピング サービスにより使用されるタイル システムについては、[Bing Maps タイル システムに関するページ (英語) ](https://go.microsoft.com/fwlink/p/?LinkId=626692)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-123">For more info about the tile system used by mapping services, see [Bing Maps Tile System](https://go.microsoft.com/fwlink/p/?LinkId=626692).</span></span>

### <a name="overlay-tiles-from-a-tile-source"></a><span data-ttu-id="7ec0f-124">タイル ソースからのタイルのオーバーレイ</span><span class="sxs-lookup"><span data-stu-id="7ec0f-124">Overlay tiles from a tile source</span></span>

<span data-ttu-id="7ec0f-125">[  **MapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileDataSource) を使って、タイル ソースからのタイル画像を地図にオーバーレイします。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-125">Overlay tiled images from a tile source on a map by using the [**MapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileDataSource).</span></span>

1.  <span data-ttu-id="7ec0f-126">[  **MapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileDataSource) から継承する 3 つのタイル データ ソース クラスのいずれかをインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-126">Instantiate one of the three tile data source classes that inherit from [**MapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileDataSource).</span></span>

    -   [<span data-ttu-id="7ec0f-127">**HttpMapTileDataSource**</span><span class="sxs-lookup"><span data-stu-id="7ec0f-127">**HttpMapTileDataSource**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource)
    -   [<span data-ttu-id="7ec0f-128">**LocalMapTileDataSource**</span><span class="sxs-lookup"><span data-stu-id="7ec0f-128">**LocalMapTileDataSource**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource)
    -   [<span data-ttu-id="7ec0f-129">**CustomMapTileDataSource**</span><span class="sxs-lookup"><span data-stu-id="7ec0f-129">**CustomMapTileDataSource**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.CustomMapTileDataSource)

    <span data-ttu-id="7ec0f-130">ベース URI またはファイル名に置き換え可能なパラメーターを挿入することにより、タイルの要求に使う **UriFormatString** を構成します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-130">Configure the **UriFormatString** to use to request the tiles by inserting replaceable parameters in the base Uri or filename.</span></span>

    <span data-ttu-id="7ec0f-131">次の例では、[**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) をインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-131">The following example instantiates an [**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource).</span></span> <span data-ttu-id="7ec0f-132">次の例では、**HttpMapTileDataSource** のコンストラクターで [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) の値を指定しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-132">This example specifies the value of the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) in the constructor of the **HttpMapTileDataSource**.</span></span>

    ```csharp
        HttpMapTileDataSource dataSource = new HttpMapTileDataSource(
          "http://www.<web service name>.com/z={zoomlevel}&x={x}&y={y}");
    ```

2.  <span data-ttu-id="7ec0f-133">[  **MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) をインスタンス化および構成します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-133">Instantiate and configure a [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource).</span></span> <span data-ttu-id="7ec0f-134">以前の手順で **MapTileSource** の [**DataSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.datasource) として構成した [**MapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileDataSource) を指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-134">Specify the [**MapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileDataSource) that you configured in the previous step as the [**DataSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.datasource) of the **MapTileSource**.</span></span>

    <span data-ttu-id="7ec0f-135">次の例では、[**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) のコンストラクターで [**DataSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.datasource) を指定しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-135">The following example specifies the [**DataSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.datasource) in the constructor of the [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource).</span></span>

    ```csharp
        MapTileSource tileSource = new MapTileSource(dataSource);
    ```

    <span data-ttu-id="7ec0f-136">[  **MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) のプロパティを使うことにより、タイルが表示される条件を制限できます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-136">You can restrict the conditions in which the tiles are displayed by using properties of the [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource).</span></span>

    -   <span data-ttu-id="7ec0f-137">[  **Bounds**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.bounds) プロパティの値を指定することにより、特定地域内にのみタイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-137">Display tiles only within a specific geographic area by providing a value for the [**Bounds**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.bounds) property.</span></span>
    -   <span data-ttu-id="7ec0f-138">[  **ZoomLevelRange**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.zoomlevelrange) プロパティの値を指定することにより、特定の詳細レベルでのみタイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-138">Display tiles only at certain levels of detail by providing a value for the [**ZoomLevelRange**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.zoomlevelrange) property.</span></span>

    <span data-ttu-id="7ec0f-139">オプションで、[**Layer**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.layer)、[**AllowOverstretch**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.allowoverstretch)、[**IsRetryEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.isretryenabled)、[**IsTransparencyEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.istransparencyenabled) など、タイルの読み込みまたは表示に影響する [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) の他のプロパティを構成します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-139">Optionally, configure other properties of the [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) that affect the loading or the display of the tiles, such as [**Layer**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.layer), [**AllowOverstretch**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.allowoverstretch), [**IsRetryEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.isretryenabled), and [**IsTransparencyEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.istransparencyenabled).</span></span>

3.  <span data-ttu-id="7ec0f-140">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の [**TileSources**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tilesources) コレクションに [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) を追加します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-140">Add the [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) to the [**TileSources**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tilesources) collection of the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span>

    ```csharp
         MapControl1.TileSources.Add(tileSource);
    ```

## <a name="overlay-tiles-from-a-web-service"></a><span data-ttu-id="7ec0f-141">Web サービスからのタイルのオーバーレイ</span><span class="sxs-lookup"><span data-stu-id="7ec0f-141">Overlay tiles from a web service</span></span>


<span data-ttu-id="7ec0f-142">[  **HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) を使って、Web サービスから取得したタイル画像をオーバーレイします。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-142">Overlay tiled images retrieved from a web service by using the [**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource).</span></span>

1.  <span data-ttu-id="7ec0f-143">[  **HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) をインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-143">Instantiate an [**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource).</span></span>
2.  <span data-ttu-id="7ec0f-144">Web サービスで [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) プロパティの値として想定される URI の形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-144">Specify the format of the Uri that the web service expects as the value of the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) property.</span></span> <span data-ttu-id="7ec0f-145">この値を作成するには、ベース URI に置き換え可能なパラメーターを挿入します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-145">To create this value, insert replaceable parameters in the base Uri.</span></span> <span data-ttu-id="7ec0f-146">たとえば次のコード サンプルでは、**UriFormatString** の値は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-146">For example, in the following code sample, the value of the **UriFormatString** is:</span></span>

    ``` syntax
    http://www.<web service name>.com/z={zoomlevel}&x={x}&y={y}
    ```

    <span data-ttu-id="7ec0f-147">この Web サービスでは、置き換え可能なパラメーター {x}、{y}、{zoomlevel} を含む URI をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-147">The web service has to support a Uri that contains the replaceable parameters {x}, {y}, and {zoomlevel}.</span></span> <span data-ttu-id="7ec0f-148">大半の Web サービス (たとえば Nokia、Bing、Google など) で、この形式の URI がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-148">Most web services (for example, Nokia, Bing, and Google) support Uris in this format.</span></span> <span data-ttu-id="7ec0f-149">[  **UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) プロパティで使用できない追加引数が Web サービスで必要な場合は、カスタム URI を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-149">If the web service requires additional arguments that aren't available with the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) property, then you have to create a custom Uri.</span></span> <span data-ttu-id="7ec0f-150">[  **UriRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.urirequested) イベントを処理することにより、カスタム URI を作成して返します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-150">Create and return a custom Uri by handling the [**UriRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.urirequested) event.</span></span> <span data-ttu-id="7ec0f-151">詳しくは、このトピックで後述する「[カスタム URI の指定](#customuri)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-151">For more info, see the [Provide a custom URI](#customuri) section later in this topic.</span></span>

3.  <span data-ttu-id="7ec0f-152">次に、「[タイル画像の概要](#tileintro)」で説明した残りの手順に従います。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-152">Then, follow the remaining steps described previously in the [Tiled image overview](#tileintro).</span></span>

<span data-ttu-id="7ec0f-153">次の例では、北米のマップに架空の Web サービスからのタイルをオーバーレイしています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-153">The following example overlays tiles from a fictitious web service on a map of North America.</span></span> <span data-ttu-id="7ec0f-154">[  **HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) のコンストラクターで [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) の値を指定しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-154">The value of the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) is specified in the constructor of the [**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource).</span></span> <span data-ttu-id="7ec0f-155">この例では、省略可能な [**Bounds**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.bounds) プロパティによって指定した地理的境界内にのみタイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-155">In this example, tiles are only displayed within the geographic boundaries specified by the optional [**Bounds**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.bounds) property.</span></span>

```csharp
private void AddHttpMapTileSource()
{
    // Create the bounding box in which the tiles are displayed.
    // This example represents North America.
    BasicGeoposition northWestCorner =
        new BasicGeoposition() { Latitude = 48.38544, Longitude = -124.667360 };
    BasicGeoposition southEastCorner =
        new BasicGeoposition() { Latitude = 25.26954, Longitude = -80.30182 };
    GeoboundingBox boundingBox = new GeoboundingBox(northWestCorner, southEastCorner);

    // Create an HTTP data source.
    // This example retrieves tiles from a fictitious web service.
    HttpMapTileDataSource dataSource = new HttpMapTileDataSource(
        "http://www.<web service name>.com/z={zoomlevel}&x={x}&y={y}");

    // Optionally, add custom HTTP headers if the web service requires them.
    dataSource.AdditionalRequestHeaders.Add("header name", "header value");

    // Create a tile source and add it to the Map control.
    MapTileSource tileSource = new MapTileSource(dataSource);
    tileSource.Bounds = boundingBox;
    MapControl1.TileSources.Add(tileSource);
}
```

```cppwinrt
...
#include <winrt/Windows.Devices.Geolocation.h>
#include <winrt/Windows.UI.Xaml.Controls.Maps.h>
...
void MainPage::AddHttpMapTileSource()
{
    Windows::Devices::Geolocation::BasicGeoposition northWest{ 48.38544, -124.667360 };
    Windows::Devices::Geolocation::BasicGeoposition southEast{ 25.26954, -80.30182 };
    Windows::Devices::Geolocation::GeoboundingBox boundingBox{ northWest, southEast };

    Windows::UI::Xaml::Controls::Maps::HttpMapTileDataSource dataSource{
        L"http://www.<web service name>.com/z={zoomlevel}&x={x}&y={y}" };

    dataSource.AdditionalRequestHeaders().Insert(L"header name", L"header value");

    Windows::UI::Xaml::Controls::Maps::MapTileSource tileSource{ dataSource };
    tileSource.Bounds(boundingBox);

    MapControl1().TileSources().Append(tileSource);
}
...
```

```cpp
void MainPage::AddHttpMapTileSource()
{
    BasicGeoposition northWest = { 48.38544, -124.667360 };
    BasicGeoposition southEast = { 25.26954, -80.30182 };
    GeoboundingBox^ boundingBox = ref new GeoboundingBox(northWest, southEast);

    auto dataSource = ref new Windows::UI::Xaml::Controls::Maps::HttpMapTileDataSource(
        "http://www.<web service name>.com/z={zoomlevel}&x={x}&y={y}");

    dataSource->AdditionalRequestHeaders->Insert("header name", "header value");

    auto tileSource = ref new Windows::UI::Xaml::Controls::Maps::MapTileSource(dataSource);
    tileSource->Bounds = boundingBox;

    this->MapControl1->TileSources->Append(tileSource);
}
```

## <a name="overlay-tiles-from-local-storage"></a><span data-ttu-id="7ec0f-156">ローカル記憶域からのタイルのオーバーレイ</span><span class="sxs-lookup"><span data-stu-id="7ec0f-156">Overlay tiles from local storage</span></span>


<span data-ttu-id="7ec0f-157">[  **LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource) を使って、ローカル ストレージにファイルとして格納されたタイル画像をオーバーレイします。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-157">Overlay tiled images stored as files in local storage by using the [**LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource).</span></span> <span data-ttu-id="7ec0f-158">通常、こうしたファイルはアプリと共にパッケージ化して配布します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-158">Typically, you package and distribute these files with your app.</span></span>

1.  <span data-ttu-id="7ec0f-159">[  **LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource) をインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-159">Instantiate a [**LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource).</span></span>
2.  <span data-ttu-id="7ec0f-160">[  **UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) プロパティの値としてファイル名の形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-160">Specify the format of the file names as the value of the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) property.</span></span> <span data-ttu-id="7ec0f-161">この値を作成するには、ベース ファイル名に置き換え可能なパラメーターを挿入します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-161">To create this value, insert replaceable parameters in the base filename.</span></span> <span data-ttu-id="7ec0f-162">たとえば次のコード サンプルでは、[**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) の値は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-162">For example, in the following code sample, the value of the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) is:</span></span>

    ``` syntax
        Tile_{zoomlevel}_{x}_{y}.png
    ```

    <span data-ttu-id="7ec0f-163">[  **UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) プロパティで使用できない追加引数がファイル名の形式で必要な場合は、カスタム URI を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-163">If the format of the file names requires additional arguments that aren't available with the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) property, then you have to create a custom Uri.</span></span> <span data-ttu-id="7ec0f-164">[  **UriRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.urirequested) イベントを処理することにより、カスタム URI を作成して返します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-164">Create and return a custom Uri by handling the [**UriRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.urirequested) event.</span></span> <span data-ttu-id="7ec0f-165">詳しくは、このトピックで後述する「[カスタム URI の指定](#customuri)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-165">For more info, see the [Provide a custom URI](#customuri) section later in this topic.</span></span>

3.  <span data-ttu-id="7ec0f-166">次に、「[タイル画像の概要](#tileintro)」で説明した残りの手順に従います。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-166">Then, follow the remaining steps described previously in the [Tiled image overview](#tileintro).</span></span>

<span data-ttu-id="7ec0f-167">ローカル ストレージからタイルを読み込むために、次のプロトコルと場所を使用できます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-167">You can use the following protocols and locations to load tiles from local storage:</span></span>

| <span data-ttu-id="7ec0f-168">Uri</span><span class="sxs-lookup"><span data-stu-id="7ec0f-168">Uri</span></span> | <span data-ttu-id="7ec0f-169">詳細情報</span><span class="sxs-lookup"><span data-stu-id="7ec0f-169">More info</span></span> |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7ec0f-170">ms-appx:///</span><span class="sxs-lookup"><span data-stu-id="7ec0f-170">ms-appx:///</span></span> | <span data-ttu-id="7ec0f-171">アプリのインストール フォルダーのルートを参照します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-171">Points to the root of the app's installation folder.</span></span> |
|  | <span data-ttu-id="7ec0f-172">これは、[Package.InstalledLocation](https://docs.microsoft.com/uwp/api/windows.applicationmodel.package.installedlocation) プロパティによって参照される場所です。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-172">This is the location referenced by the [Package.InstalledLocation](https://docs.microsoft.com/uwp/api/windows.applicationmodel.package.installedlocation) property.</span></span> |
| <span data-ttu-id="7ec0f-173">ms-appdata:///local</span><span class="sxs-lookup"><span data-stu-id="7ec0f-173">ms-appdata:///local</span></span> | <span data-ttu-id="7ec0f-174">アプリのローカル ストレージのルートを参照します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-174">Points to the root of the app's local storage.</span></span> |
|  | <span data-ttu-id="7ec0f-175">これは、[ApplicationData.LocalFolder](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) プロパティによって参照される場所です。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-175">This is the location referenced by the [ApplicationData.LocalFolder](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.localfolder) property.</span></span> |
| <span data-ttu-id="7ec0f-176">ms-appdata:///temp</span><span class="sxs-lookup"><span data-stu-id="7ec0f-176">ms-appdata:///temp</span></span> | <span data-ttu-id="7ec0f-177">アプリの一時フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-177">Points to the app's temp folder.</span></span> |
|  | <span data-ttu-id="7ec0f-178">これは、[ApplicationData.TemporaryFolder](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) プロパティによって参照される場所です。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-178">This is the location referenced by the [ApplicationData.TemporaryFolder](https://docs.microsoft.com/uwp/api/windows.storage.applicationdata.temporaryfolder) property.</span></span> |

 

<span data-ttu-id="7ec0f-179">次の例では、`ms-appx:///` プロトコルを使って、アプリのインストール フォルダーにファイルとして格納されたタイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-179">The following example loads tiles that are stored as files in the app's installation folder by using the `ms-appx:///` protocol.</span></span> <span data-ttu-id="7ec0f-180">[  **LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource) のコンストラクターで [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) の値を指定しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-180">The value for the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) is specified in the constructor of the [**LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource).</span></span> <span data-ttu-id="7ec0f-181">この例では、省略可能な [**ZoomLevelRange**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.zoomlevelrange) プロパティによって指定された範囲内に地図のズーム レベルがある場合にのみ、タイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-181">In this example, tiles are only displayed when the zoom level of the map is within the range specified by the optional [**ZoomLevelRange**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.zoomlevelrange) property.</span></span>

```csharp
        void AddLocalMapTileSource()
        {
            // Specify the range of zoom levels
            // at which the overlaid tiles are displayed.
            MapZoomLevelRange range;
            range.Min = 11;
            range.Max = 20;

            // Create a local data source.
            LocalMapTileDataSource dataSource = new LocalMapTileDataSource(
                "ms-appx:///TileSourceAssets/Tile_{zoomlevel}_{x}_{y}.png");

            // Create a tile source and add it to the Map control.
            MapTileSource tileSource = new MapTileSource(dataSource);
            tileSource.ZoomLevelRange = range;
            MapControl1.TileSources.Add(tileSource);
        }
```

<a id="customuri" />

## <a name="provide-a-custom-uri"></a><span data-ttu-id="7ec0f-182">カスタム URI の指定</span><span class="sxs-lookup"><span data-stu-id="7ec0f-182">Provide a custom URI</span></span>

<span data-ttu-id="7ec0f-183">[  **HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) の [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) プロパティまたは [**LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource) の [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) プロパティにより使用できる置き換え可能なパラメーターがタイルの取得に十分でない場合は、カスタム URI を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-183">If the replaceable parameters available with the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.httpmaptiledatasource.uriformatstring) property of the [**HttpMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.HttpMapTileDataSource) or the [**UriFormatString**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.localmaptiledatasource.uriformatstring) property of the [**LocalMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.LocalMapTileDataSource) aren't sufficient to retrieve your tiles, then you have to create a custom Uri.</span></span> <span data-ttu-id="7ec0f-184">**UriRequested** イベントのカスタム ハンドラーを指定することによりカスタム URI を作成して返します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-184">Create and return a custom Uri by providing a custom handler for the **UriRequested** event.</span></span> <span data-ttu-id="7ec0f-185">**UriRequested** イベントは、個々のタイルについて発生します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-185">The **UriRequested** event is raised for each individual tile.</span></span>

1.  <span data-ttu-id="7ec0f-186">カスタム URI を作成するために、**UriRequested** イベントのカスタム ハンドラーで、[**MapTileUriRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileUriRequestedEventArgs) の [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.x) プロパティ、[**Y**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.y) プロパティ、[**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.zoomlevel) プロパティにより必要なカスタム引数を組み合わせます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-186">In your custom handler for the **UriRequested** event, combine the required custom arguments with the [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.x), [**Y**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.y), and [**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.zoomlevel) properties of the [**MapTileUriRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileUriRequestedEventArgs) to create the custom Uri.</span></span>
2.  <span data-ttu-id="7ec0f-187">[  **MapTileUriRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileUriRequestedEventArgs) の [**Request**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.request) プロパティに含まれている [**MapTileUriRequest**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileUriRequest) の [**Uri**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequest.uri) プロパティにカスタム URI を返します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-187">Return the custom Uri in the [**Uri**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequest.uri) property of the [**MapTileUriRequest**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileUriRequest), which is contained in the [**Request**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptileurirequestedeventargs.request) property of the [**MapTileUriRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileUriRequestedEventArgs).</span></span>

<span data-ttu-id="7ec0f-188">次の例では、**UriRequested** イベントのカスタム ハンドラーを作成することによりカスタム URI を指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-188">The following example shows how to provide a custom Uri by creating a custom handler for the **UriRequested** event.</span></span> <span data-ttu-id="7ec0f-189">また、カスタム URI を作成するために非同期処理が必要な場合に、保留パターンを実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-189">It also shows how to implement the deferral pattern if you have to do something asynchronously to create the custom Uri.</span></span>

```csharp
using Windows.UI.Xaml.Controls.Maps;
using System.Threading.Tasks;
...
            var httpTileDataSource = new HttpMapTileDataSource();
            // Attach a handler for the UriRequested event.
            httpTileDataSource.UriRequested += HandleUriRequestAsync;
            MapTileSource httpTileSource = new MapTileSource(httpTileDataSource);
            MapControl1.TileSources.Add(httpTileSource);
...
        // Handle the UriRequested event.
        private async void HandleUriRequestAsync(HttpMapTileDataSource sender,
            MapTileUriRequestedEventArgs args)
        {
            // Get a deferral to do something asynchronously.
            // Omit this line if you don't have to do something asynchronously.
            var deferral = args.Request.GetDeferral();

            // Get the custom Uri.
            var uri = await GetCustomUriAsync(args.X, args.Y, args.ZoomLevel);

            // Specify the Uri in the Uri property of the MapTileUriRequest.
            args.Request.Uri = uri;

            // Notify the app that the custom Uri is ready.
            // Omit this line also if you don't have to do something asynchronously.
            deferral.Complete();
        }

        // Create the custom Uri.
        private async Task<Uri> GetCustomUriAsync(int x, int y, int zoomLevel)
        {
            // Do something asynchronously to create and return the custom Uri.        }
        }
```

## <a name="overlay-tiles-from-a-custom-source"></a><span data-ttu-id="7ec0f-190">カスタム ソースからのタイルのオーバーレイ</span><span class="sxs-lookup"><span data-stu-id="7ec0f-190">Overlay tiles from a custom source</span></span>

<span data-ttu-id="7ec0f-191">[  **CustomMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.CustomMapTileDataSource) を使って、カスタム タイルをオーバーレイします。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-191">Overlay custom tiles by using the [**CustomMapTileDataSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.CustomMapTileDataSource).</span></span> <span data-ttu-id="7ec0f-192">プログラムによってメモリ内で随時にタイルを作成するか、または別のソースから既存のタイルを読み込むために独自のコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-192">Create tiles programmatically in memory on the fly, or write your own code to load existing tiles from another source.</span></span>

<span data-ttu-id="7ec0f-193">カスタム タイルを作成するか読み込むには、[**BitmapRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.custommaptiledatasource.bitmaprequested) イベントのカスタム ハンドラーを指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-193">To create or load custom tiles, provide a custom handler for the [**BitmapRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.custommaptiledatasource.bitmaprequested) event.</span></span> <span data-ttu-id="7ec0f-194">**BitmapRequested** イベントは、個々のタイルについて発生します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-194">The **BitmapRequested** event is raised for each individual tile.</span></span>

1.  <span data-ttu-id="7ec0f-195">カスタム タイルを作成または取得するために、[**BitmapRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.custommaptiledatasource.bitmaprequested) イベントのカスタム ハンドラーで、[**MapTileBitmapRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequestedEventArgs) の [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.x) プロパティ、[**Y**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.y) プロパティ、[**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.zoomlevel) プロパティにより必要なカスタム引数を組み合わせます。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-195">In your custom handler for the [**BitmapRequested**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.custommaptiledatasource.bitmaprequested) event, combine the required custom arguments with the [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.x), [**Y**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.y), and [**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.zoomlevel) properties of the [**MapTileBitmapRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequestedEventArgs) to create or retrieve a custom tile.</span></span>
2.  <span data-ttu-id="7ec0f-196">[  **MapTileBitmapRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequestedEventArgs) の [**Request**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.request) プロパティに含まれている [**MapTileBitmapRequest**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequest) の [**PixelData**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequest.pixeldata) プロパティにカスタム タイルを返します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-196">Return the custom tile in the [**PixelData**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequest.pixeldata) property of the [**MapTileBitmapRequest**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequest), which is contained in the [**Request**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.request) property of the [**MapTileBitmapRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequestedEventArgs).</span></span> <span data-ttu-id="7ec0f-197">**PixelData** プロパティの型は [**IRandomAccessStreamReference**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.IRandomAccessStreamReference) です。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-197">The **PixelData** property is of type [**IRandomAccessStreamReference**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.IRandomAccessStreamReference).</span></span>

<span data-ttu-id="7ec0f-198">次の例では、**BitmapRequested** イベントのカスタム ハンドラーを作成することによりカスタム タイルを指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-198">The following example shows how to provide custom tiles by creating a custom handler for the **BitmapRequested** event.</span></span> <span data-ttu-id="7ec0f-199">この例では、一部が不透明な赤の同じタイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-199">This example creates identical red tiles that are partially opaque.</span></span> <span data-ttu-id="7ec0f-200">この例では、[**MapTileBitmapRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequestedEventArgs) の [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.x) プロパティ、[**Y**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.y) プロパティ、[**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.zoomlevel) プロパティを無視します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-200">The example ignores the [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.x), [**Y**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.y), and [**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilebitmaprequestedeventargs.zoomlevel) properties of the [**MapTileBitmapRequestedEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileBitmapRequestedEventArgs).</span></span> <span data-ttu-id="7ec0f-201">これは実際の例ではありませんが、メモリ内で随時にカスタム タイルを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-201">Although this is not a real world example, the example demonstrates how you can create in-memory custom tiles on the fly.</span></span> <span data-ttu-id="7ec0f-202">この例ではまた、カスタム タイルを作成するために非同期処理が必要な場合に、保留パターンを実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-202">The example also shows how to implement the deferral pattern if you have to do something asynchronously to create the custom tiles.</span></span>

```csharp
using Windows.UI.Xaml.Controls.Maps;
using Windows.Storage.Streams;
using System.Threading.Tasks;
...
        CustomMapTileDataSource customDataSource = new CustomMapTileDataSource();
        // Attach a handler for the BitmapRequested event.
        customDataSource.BitmapRequested += customDataSource_BitmapRequestedAsync;
        customTileSource = new MapTileSource(customDataSource);
        MapControl1.TileSources.Add(customTileSource);
...
        // Handle the BitmapRequested event.
        private async void customDataSource_BitmapRequestedAsync(
            CustomMapTileDataSource sender,
            MapTileBitmapRequestedEventArgs args)
        {
            var deferral = args.Request.GetDeferral();
            args.Request.PixelData = await CreateBitmapAsStreamAsync();
            deferral.Complete();
        }

        // Create the custom tiles.
        // This example creates red tiles that are partially opaque.
        private async Task<RandomAccessStreamReference> CreateBitmapAsStreamAsync()
        {
            int pixelHeight = 256;
            int pixelWidth = 256;
            int bpp = 4;

            byte[] bytes = new byte[pixelHeight * pixelWidth * bpp];

            for (int y = 0; y < pixelHeight; y++)
            {
                for (int x = 0; x < pixelWidth; x++)
                {
                    int pixelIndex = y * pixelWidth + x;
                    int byteIndex = pixelIndex * bpp;

                    // Set the current pixel bytes.
                    bytes[byteIndex] = 0xff;        // Red
                    bytes[byteIndex + 1] = 0x00;    // Green
                    bytes[byteIndex + 2] = 0x00;    // Blue
                    bytes[byteIndex + 3] = 0x80;    // Alpha (0xff = fully opaque)
                }
            }

            // Create RandomAccessStream from byte array.
            InMemoryRandomAccessStream randomAccessStream =
                new InMemoryRandomAccessStream();
            IOutputStream outputStream = randomAccessStream.GetOutputStreamAt(0);
            DataWriter writer = new DataWriter(outputStream);
            writer.WriteBytes(bytes);
            await writer.StoreAsync();
            await writer.FlushAsync();
            return RandomAccessStreamReference.CreateFromStream(randomAccessStream);
        }
```

```cppwinrt
...
#include <winrt/Windows.Storage.Streams.h>
...
Windows::Foundation::IAsyncOperation<Windows::Storage::Streams::InMemoryRandomAccessStream> MainPage::CustomRandomAccessStream()
{
    constexpr int pixelHeight{ 256 };
    constexpr int pixelWidth{ 256 };
    constexpr int bpp{ 4 };

    std::array<uint8_t, pixelHeight * pixelWidth * bpp> bytes;

    for (int y = 0; y < pixelHeight; y++)
    {
        for (int x = 0; x < pixelWidth; x++)
        {
            int pixelIndex{ y * pixelWidth + x };
            int byteIndex{ pixelIndex * bpp };

            // Set the current pixel bytes.
            bytes[byteIndex] = (byte)(std::rand() % 256);        // Red
            bytes[byteIndex + 1] = (byte)(std::rand() % 256);    // Green
            bytes[byteIndex + 2] = (byte)(std::rand() % 256);    // Blue
            bytes[byteIndex + 3] = (byte)((std::rand() % 56) + 200);    // Alpha (0xff = fully opaque)
        }
    }

    // Create RandomAccessStream from byte array.
    Windows::Storage::Streams::InMemoryRandomAccessStream randomAccessStream;
    Windows::Storage::Streams::IOutputStream outputStream{ randomAccessStream.GetOutputStreamAt(0) };
    Windows::Storage::Streams::DataWriter writer{ outputStream };
    writer.WriteBytes(bytes);

    co_await writer.StoreAsync();
    co_await writer.FlushAsync();

    co_return randomAccessStream;
}
...
```

```cpp
InMemoryRandomAccessStream^ TileSources::CustomRandomAccessStream::get()
{
    int pixelHeight = 256;
    int pixelWidth = 256;
    int bpp = 4;

    Array<byte>^ bytes = ref new Array<byte>(pixelHeight * pixelWidth * bpp);

    for (int y = 0; y < pixelHeight; y++)
    {
        for (int x = 0; x < pixelWidth; x++)
        {
            int pixelIndex = y * pixelWidth + x;
            int byteIndex = pixelIndex * bpp;

            // Set the current pixel bytes.
            bytes[byteIndex] = (byte)(std::rand() % 256);        // Red
            bytes[byteIndex + 1] = (byte)(std::rand() % 256);    // Green
            bytes[byteIndex + 2] = (byte)(std::rand() % 256);    // Blue
            bytes[byteIndex + 3] = (byte)((std::rand() % 56) + 200);    // Alpha (0xff = fully opaque)
        }
    }

    // Create RandomAccessStream from byte array.
    InMemoryRandomAccessStream^ randomAccessStream = ref new InMemoryRandomAccessStream();
    IOutputStream^ outputStream = randomAccessStream->GetOutputStreamAt(0);
    DataWriter^ writer = ref new DataWriter(outputStream);
    writer->WriteBytes(bytes);

    create_task(writer->StoreAsync()).then([writer](unsigned int)
    {
        create_task(writer->FlushAsync());
    });

    return randomAccessStream;
}
```

## <a name="replace-the-default-map"></a><span data-ttu-id="7ec0f-203">既定の地図の置き換え</span><span class="sxs-lookup"><span data-stu-id="7ec0f-203">Replace the default map</span></span>

<span data-ttu-id="7ec0f-204">既定の地図をサード パーティ製タイルまたはカスタム タイルに完全に置き換えるには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-204">To replace the default map entirely with third-party or custom tiles:</span></span>

-   <span data-ttu-id="7ec0f-205">[  **MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource) の [**Layer**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.layer) プロパティ値として [**MapTileLayer**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileLayer).**BackgroundReplacement** を指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-205">Specify [**MapTileLayer**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileLayer).**BackgroundReplacement** as the value of the [**Layer**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.maptilesource.layer) property of the [**MapTileSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapTileSource).</span></span>
-   <span data-ttu-id="7ec0f-206">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の [**Style**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) プロパティ値として [**MapStyle**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapStyle).**None** を指定します。</span><span class="sxs-lookup"><span data-stu-id="7ec0f-206">Specify [**MapStyle**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapStyle).**None** as the value of the [**Style**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) property of the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span>

## <a name="related-topics"></a><span data-ttu-id="7ec0f-207">関連トピック</span><span class="sxs-lookup"><span data-stu-id="7ec0f-207">Related topics</span></span>

* [<span data-ttu-id="7ec0f-208">Bing Maps Developer Center</span><span class="sxs-lookup"><span data-stu-id="7ec0f-208">Bing Maps Developer Center</span></span>](https://www.bingmapsportal.com/)
* [<span data-ttu-id="7ec0f-209">UWP の地図のサンプル</span><span class="sxs-lookup"><span data-stu-id="7ec0f-209">UWP map sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619977)
* [<span data-ttu-id="7ec0f-210">地図の設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="7ec0f-210">Design guidelines for maps</span></span>](https://docs.microsoft.com/windows/uwp/maps-and-location/controls-map)
* [<span data-ttu-id="7ec0f-211">Build 2015 のビデオ:Windows アプリでの電話、タブレット、PC で使用できるマップと位置情報の活用</span><span class="sxs-lookup"><span data-stu-id="7ec0f-211">Build 2015 video: Leveraging Maps and Location Across Phone, Tablet, and PC in Your Windows Apps</span></span>](https://channel9.msdn.com/Events/Build/2015/2-757)
* [<span data-ttu-id="7ec0f-212">UWP の交通情報アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="7ec0f-212">UWP traffic app sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619982)
