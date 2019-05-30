---
title: 2D、3D、Streetside ビューでの地図の表示
description: 地図を表示するには、マップ *プレースカード*と呼ばれる簡易非表示に対応したウィンドウか、フル機能を備えたマップ コントロールを使うことができます。
ms.assetid: 3839E00B-2C1E-4627-A45F-6DDA98D7077F
ms.date: 03/19/2018
ms.topic: article
keywords: Windows 10, UWP, 地図, 位置情報, マップ コントロール, マップ ビュー
ms.localizationpriority: medium
ms.openlocfilehash: 8c026fa0762e25421414ac66fc614625c0df6cd7
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371906"
---
# <a name="display-maps-with-2d-3d-and-streetside-views"></a><span data-ttu-id="3ffbd-104">2D、3D、Streetside ビューでの地図の表示</span><span class="sxs-lookup"><span data-stu-id="3ffbd-104">Display maps with 2D, 3D, and Streetside views</span></span>

<span data-ttu-id="3ffbd-105">地図を表示するには、マップ *プレースカード*と呼ばれる簡易非表示に対応したウィンドウか、フル機能を備えたマップ コントロールを使うことができます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-105">You can show a map in light dismissable window called a map *placecard* or in a full featured map control.</span></span>

<span data-ttu-id="3ffbd-106">[地図サンプル](https://go.microsoft.com/fwlink/p/?LinkId=619977)をダウンロードして、このガイドで説明されている機能のいくつかを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-106">Download the [map sample](https://go.microsoft.com/fwlink/p/?LinkId=619977) to try out some the features described in this guide.</span></span>

<a id="placecard" />

## <a name="display-map-in-a-placecard"></a><span data-ttu-id="3ffbd-107">プレースカードへの地図の表示</span><span class="sxs-lookup"><span data-stu-id="3ffbd-107">Display map in a placecard</span></span>
<span data-ttu-id="3ffbd-108">UI 要素またはユーザーがタッチするアプリの領域の上下左右に軽量なポップアップ ウィンドウを開いて、その内部に地図を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-108">You can show users a map inside of a light-weight pop-up window above, below or to the side of a UI element or an area of an app where the user touches.</span></span> <span data-ttu-id="3ffbd-109">地図には、アプリ内の情報に関連する都市や住所を表示できます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-109">The map can show a city or address that relates to information in your app.</span></span>  

<span data-ttu-id="3ffbd-110">次のプレースカードは、シアトルの街を表示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-110">This placecard shows the city of Seattle.</span></span>

![シアトルの街を表示するプレースカード](images/placecard-city.png)

<span data-ttu-id="3ffbd-112">プレースカードのボタンの下にシアトルを表示するコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-112">Here's the code that makes Seattle appear in a placecard below a button.</span></span>

```csharp
private void Seattle_Click(object sender, RoutedEventArgs e)
{
    Geopoint seattlePoint = new Geopoint
        (new BasicGeoposition { Latitude = 47.6062, Longitude = -122.3321 });

    PlaceInfo spaceNeedlePlace = PlaceInfo.Create(seattlePoint);

    FrameworkElement targetElement = (FrameworkElement)sender;

    GeneralTransform generalTransform =
        targetElement.TransformToVisual((FrameworkElement)targetElement.Parent);

    Rect rectangle = generalTransform.TransformBounds(new Rect(new Point
        (targetElement.Margin.Left, targetElement.Margin.Top), targetElement.RenderSize));

    spaceNeedlePlace.Show(rectangle, Windows.UI.Popups.Placement.Below);
}
```

<span data-ttu-id="3ffbd-113">次のプレースカードは、シアトルにある Space Needle の場所を表示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-113">This placecard shows the location of the Space Needle in Seattle.</span></span>

![Space Needle の場所を表示するプレースカード](images/placecard-needle.png)

<span data-ttu-id="3ffbd-115">プレースカードのボタンの下に Space Needle を表示するコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-115">Here's the code that makes the Space Needle appear in a placecard below a button.</span></span>

```csharp
private void SpaceNeedle_Click(object sender, RoutedEventArgs e)
{
    Geopoint spaceNeedlePoint = new Geopoint
        (new BasicGeoposition { Latitude = 47.6205, Longitude = -122.3493 });

    PlaceInfoCreateOptions options = new PlaceInfoCreateOptions();

    options.DisplayAddress = "400 Broad St, Seattle, WA 98109";
    options.DisplayName = "Seattle Space Needle";

    PlaceInfo spaceNeedlePlace =  PlaceInfo.Create(spaceNeedlePoint, options);

    FrameworkElement targetElement = (FrameworkElement)sender;

    GeneralTransform generalTransform =
        targetElement.TransformToVisual((FrameworkElement)targetElement.Parent);

    Rect rectangle = generalTransform.TransformBounds(new Rect(new Point
        (targetElement.Margin.Left, targetElement.Margin.Top), targetElement.RenderSize));

    spaceNeedlePlace.Show(rectangle, Windows.UI.Popups.Placement.Below);
}
```

<a id="map-control" />

## <a name="display-map-in-a-control"></a><span data-ttu-id="3ffbd-116">コントロールでの地図の表示</span><span class="sxs-lookup"><span data-stu-id="3ffbd-116">Display map in a control</span></span>

<span data-ttu-id="3ffbd-117">機能豊富でカスタマイズ可能なマップ データをアプリに表示するには、マップ コントロールを使います。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-117">Use a map control to show rich and customizable map data in your app.</span></span> <span data-ttu-id="3ffbd-118">マップ コントロールでは、道路地図、航空写真、3D ビュー、ルート案内、検索結果、交通情報を表示できます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-118">A map control can display road maps, aerial, 3D, views, directions, search results, and traffic.</span></span> <span data-ttu-id="3ffbd-119">マップ上には、現在地、ルート、関心のあるポイントを表示できます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-119">On a map, you can display the user's location, directions, and points of interest.</span></span> <span data-ttu-id="3ffbd-120">また、航空写真 3D ビュー、Streetside ビュー、交通情報、乗り換え情報、周辺情報を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-120">A map can also show aerial 3D views, Streetside views, traffic, transit, and local businesses.</span></span>

<span data-ttu-id="3ffbd-121">アプリ固有の地理情報または一般的な地理情報を表示できるアプリ内でマップが必要な場合に、マップ コントロールを使います。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-121">Use a map control when you want a map within your app that allows users to view app-specific or general geographic information.</span></span> <span data-ttu-id="3ffbd-122">アプリにマップ コントロールを含めておくことで、ユーザーはアプリの外部に移動することなく情報を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-122">Having a map control in your app means that users don't have to go outside your app to get that information.</span></span>

> [!NOTE]
><span data-ttu-id="3ffbd-123">その情報を得るためにユーザーがアプリの外部に移動してもかまわない場合は、Windows マップ アプリを利用することも検討してください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-123">If you don't mind users going outside your app, consider using the Windows Maps app to provide that information.</span></span> <span data-ttu-id="3ffbd-124">アプリから Windows マップ アプリを起動し、特定の地図、ルート案内、検索結果を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-124">Your app can launch the Windows Maps app to display specific maps, directions, and search results.</span></span> <span data-ttu-id="3ffbd-125">詳しくは、「[Windows マップ アプリの起動](https://docs.microsoft.com/windows/uwp/launch-resume/launch-maps-app)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-125">For more info, see [Launch the Windows Maps app](https://docs.microsoft.com/windows/uwp/launch-resume/launch-maps-app).</span></span>

### <a name="add-a-map-control-to-your-app"></a><span data-ttu-id="3ffbd-126">アプリへのマップ コントロールの追加</span><span class="sxs-lookup"><span data-stu-id="3ffbd-126">Add a map control to your app</span></span>

<span data-ttu-id="3ffbd-127">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) を追加することによって、XAML ページに地図を表示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-127">Display a map on a XAML page by adding a [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span> <span data-ttu-id="3ffbd-128">**MapControl** を使うには、XAML ページまたはコード内に [**Windows.UI.Xaml.Controls.Maps**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps) 名前空間の宣言が必要です。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-128">To use the **MapControl**, you must declare the [**Windows.UI.Xaml.Controls.Maps**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps) namespace in the XAML page or in your code.</span></span> <span data-ttu-id="3ffbd-129">ツールボックスからコントロールをドラッグすると、この名前空間宣言が自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-129">If you drag the control from the Toolbox, this namespace declaration is added automatically.</span></span> <span data-ttu-id="3ffbd-130">XAML ページに **MapControl** を手動で追加する場合は、ページの上部に名前空間宣言を手動で追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-130">If you add the **MapControl** to the XAML page manually, you must add the namespace declaration manually at the top of the page.</span></span>

<span data-ttu-id="3ffbd-131">次の例では、基本的なマップ コントロールを表示し、タッチ入力を受け付けるだけでなくズーム コントロールとチルト コントロールを表示するように地図を構成しています。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-131">The following example displays a basic map control and configures the map to display the zoom and tilt controls in addition to accepting touch inputs.</span></span>

```xml
<Page
    x:Class="MapsAndLocation1.DisplayMaps"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:MapsAndLocation1"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:Maps="using:Windows.UI.Xaml.Controls.Maps"
    mc:Ignorable="d">

 <Grid x:Name="pageGrid" Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Maps:MapControl
       x:Name="MapControl1"            
       ZoomInteractionMode="GestureAndControl"
       TiltInteractionMode="GestureAndControl"   
       MapServiceToken="EnterYourAuthenticationKeyHere"/>

 </Grid>
</Page>
```

<span data-ttu-id="3ffbd-132">コードにマップ コントロールを追加する場合は、コード ファイルの先頭で手動で名前空間を宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-132">If you add the map control in your code, you must declare the namespace manually at the top of the code file.</span></span>

```csharp
using Windows.UI.Xaml.Controls.Maps;
...

// Add the MapControl and the specify maps authentication key.
MapControl MapControl2 = new MapControl();
MapControl2.ZoomInteractionMode = MapInteractionMode.GestureAndControl;
MapControl2.TiltInteractionMode = MapInteractionMode.GestureAndControl;
MapControl2.MapServiceToken = "EnterYourAuthenticationKeyHere";
pageGrid.Children.Add(MapControl2);
```

### <a name="get-and-set-a-maps-authentication-key"></a><span data-ttu-id="3ffbd-133">マップ認証キーの取得と設定</span><span class="sxs-lookup"><span data-stu-id="3ffbd-133">Get and set a maps authentication key</span></span>

<span data-ttu-id="3ffbd-134">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) やマップ サービスを使用する前に、マップ認証キーを [**MapServiceToken**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapservicetoken) プロパティの値として指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-134">Before you can use [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) and map services, you must specify the maps authentication key as the value of the [**MapServiceToken**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapservicetoken) property.</span></span> <span data-ttu-id="3ffbd-135">前に示した例では、`EnterYourAuthenticationKeyHere` を [Bing Maps Developer Center](https://www.bingmapsportal.com/) から取得したキーで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-135">In the previous examples, replace `EnterYourAuthenticationKeyHere` with the key you get from the [Bing Maps Developer Center](https://www.bingmapsportal.com/).</span></span> <span data-ttu-id="3ffbd-136">テキスト**警告。指定されていない MapServiceToken**マップ認証キーを指定するまでに、コントロールの下に表示され続けます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-136">The text **Warning: MapServiceToken not specified** continues to appear below the control until you specify the maps authentication key.</span></span> <span data-ttu-id="3ffbd-137">マップ認証キーを取得して設定する方法について詳しくは、「[マップ認証キーの要求](authentication-key.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-137">For more info about getting and setting a maps authentication key, see [Request a maps authentication key](authentication-key.md).</span></span>

## <a name="set-the-location-of-a-map"></a><span data-ttu-id="3ffbd-138">地図の場所の設定</span><span class="sxs-lookup"><span data-stu-id="3ffbd-138">Set the location of a map</span></span>
<span data-ttu-id="3ffbd-139">地図を表示するときは、特定の場所を示すように設定することも、ユーザーの現在の場所を使うこともできます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-139">Point the map to any location that you want or use the user's current location.</span></span>  

### <a name="set-a-starting-location-for-the-map"></a><span data-ttu-id="3ffbd-140">地図の開始位置の設定</span><span class="sxs-lookup"><span data-stu-id="3ffbd-140">Set a starting location for the map</span></span>

<span data-ttu-id="3ffbd-141">コードで [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の [**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) プロパティを指定するか、または XAML マークアップでプロパティをバインドすることにより、地図上の表示位置を設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-141">Set the location to display on the map by specifying the [**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) property of the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) in your code or by binding the property in your XAML markup.</span></span> <span data-ttu-id="3ffbd-142">シアトル市を中心とした地図を表示する例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-142">The following example displays a map with the city of Seattle as its center.</span></span>

> [!NOTE]
> <span data-ttu-id="3ffbd-143">文字列は [**Geopoint**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geopoint) に変換できないため、データ バインディングを使わない限り、XAML マークアップで [**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) プロパティに対する値を指定できません。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-143">Since a string can't be converted to a [**Geopoint**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geopoint), you can't specify a value for the [**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) property in XAML markup unless you use data binding.</span></span> <span data-ttu-id="3ffbd-144">(この制限は、[**MapControl.Location**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.setlocation) 添付プロパティにも適用されます)。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-144">(This limitation also applies to the [**MapControl.Location**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.setlocation) attached property.)</span></span>

 
```csharp
protected override void OnNavigatedTo(NavigationEventArgs e)
{
   // Specify a known location.
   BasicGeoposition cityPosition = new BasicGeoposition() { Latitude = 47.604, Longitude = -122.329 };
   Geopoint cityCenter = new Geopoint(cityPosition);

   // Set the map location.
   MapControl1.Center = cityCenter;
   MapControl1.ZoomLevel = 12;
   MapControl1.LandmarksVisible = true;
}
```

![マップ コントロールの例。](images/displaymapsexample1.png)

### <a name="set-the-current-location-of-the-map"></a><span data-ttu-id="3ffbd-146">地図の現在位置の設定</span><span class="sxs-lookup"><span data-stu-id="3ffbd-146">Set the current location of the map</span></span>

<span data-ttu-id="3ffbd-147">ユーザーの位置情報にアクセスするには、先にアプリで [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geolocator.requestaccessasync) メソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-147">Before your app can access the user’s location, your app must call the [**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geolocator.requestaccessasync) method.</span></span> <span data-ttu-id="3ffbd-148">このときに、アプリをフォアグラウンドで実行し、**RequestAccessAsync** を UI スレッドから呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-148">At that time, your app must be in the foreground and **RequestAccessAsync** must be called from the UI thread.</span></span> <span data-ttu-id="3ffbd-149">位置情報に対するアクセス許可をユーザーがアプリに与えるまで、アプリは位置情報にアクセスできません。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-149">Until the user grants your app permission to their location, your app can't access location data.</span></span>

<span data-ttu-id="3ffbd-150">[  **Geolocator**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geolocator) クラスの [**GetGeopositionAsync**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geolocator.getgeopositionasync) メソッドを使って、デバイスの現在の位置情報を取得します (位置情報にアクセスできる場合)。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-150">Get the current location of the device (if location is available) by using the [**GetGeopositionAsync**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geolocator.getgeopositionasync) method of the [**Geolocator**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geolocator) class.</span></span> <span data-ttu-id="3ffbd-151">対応する [**Geopoint**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geopoint) を取得するには、geoposition オブジェクトの geocoordinate の [**Point**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geocoordinate.point) プロパティを使います。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-151">To obtain the corresponding [**Geopoint**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geopoint), use the [**Point**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geocoordinate.point) property of the geoposition's geocoordinate.</span></span> <span data-ttu-id="3ffbd-152">詳しくは、「[現在の位置情報の取得](get-location.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-152">For more info, see [Get current location](get-location.md).</span></span>

```csharp
// Set your current location.
var accessStatus = await Geolocator.RequestAccessAsync();
switch (accessStatus)
{
   case GeolocationAccessStatus.Allowed:

      // Get the current location.
      Geolocator geolocator = new Geolocator();
      Geoposition pos = await geolocator.GetGeopositionAsync();
      Geopoint myLocation = pos.Coordinate.Point;

      // Set the map location.
      MapControl1.Center = myLocation;
      MapControl1.ZoomLevel = 12;
      MapControl1.LandmarksVisible = true;
      break;

   case GeolocationAccessStatus.Denied:
      // Handle the case  if access to location is denied.
      break;

   case GeolocationAccessStatus.Unspecified:
      // Handle the case if  an unspecified error occurs.
      break;
}
```

<span data-ttu-id="3ffbd-153">地図にデバイスの位置を表示するときは、位置情報の精度に基づいてグラフィックスを表示してズーム レベルを設定することを検討します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-153">When you display your device's location on a map, consider displaying graphics and setting the zoom level based on the accuracy of the location data.</span></span> <span data-ttu-id="3ffbd-154">詳しくは、「[位置認識アプリのガイドライン](https://docs.microsoft.com/windows/uwp/maps-and-location/guidelines-and-checklist-for-detecting-location)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-154">For more info, see [Guidelines for location-aware apps](https://docs.microsoft.com/windows/uwp/maps-and-location/guidelines-and-checklist-for-detecting-location).</span></span>

### <a name="change-the-location-of-the-map"></a><span data-ttu-id="3ffbd-155">地図の位置の変更</span><span class="sxs-lookup"><span data-stu-id="3ffbd-155">Change the location of the map</span></span>

<span data-ttu-id="3ffbd-156">2D 地図に表示する位置を変更するには、[**TrySetViewAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync) メソッドのいずれかのオーバーロードを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-156">To change the location that appears in a 2D map, call one of the overloads of the [**TrySetViewAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync) method.</span></span> <span data-ttu-id="3ffbd-157">そのメソッドを使って、[**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center)、[**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel)、[**Heading**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.heading)、[**Pitch**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pitch) の新しい値を指定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-157">Use that method to specify new values for [**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center), [**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel), [**Heading**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.heading), and [**Pitch**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pitch).</span></span> <span data-ttu-id="3ffbd-158">また、ビューが変わるときに使うアニメーションをオプションで指定することもできます。そのためには、[**MapAnimationKind**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapAnimationKind) 列挙値の定数を指定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-158">You can also specify an optional animation to use when the view changes by providing a constant from the [**MapAnimationKind**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapAnimationKind) enumeration.</span></span>

<span data-ttu-id="3ffbd-159">3D 地図の場所を変更するには、代わりに [**TrySetSceneAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync) メソッドを使います。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-159">To change the location of a 3D map, use the [**TrySetSceneAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync) method instead.</span></span> <span data-ttu-id="3ffbd-160">詳しくは、「[航空写真 3D ビューの表示](#3Dviews)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-160">For more info, see [Display aerial 3D views](#3Dviews).</span></span>

<span data-ttu-id="3ffbd-161">地図上に [**GeoboundingBox**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.GeoboundingBox) の内容を表示するには、[**TrySetViewBoundsAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewboundsasync) メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-161">Call the [**TrySetViewBoundsAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewboundsasync) method to display the contents of a [**GeoboundingBox**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.GeoboundingBox) on the map.</span></span> <span data-ttu-id="3ffbd-162">たとえばこのメソッドを使うと、地図上にルートやルートの一部を表示することができます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-162">Use this method, for example, to display a route or a portion of a route on the map.</span></span> <span data-ttu-id="3ffbd-163">詳しくは、「[地図へのルートとルート案内の表示](routes-and-directions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-163">For more info, see [Display routes and directions on a map](routes-and-directions.md).</span></span>

## <a name="change-the-appearance-of-a-map"></a><span data-ttu-id="3ffbd-164">地図の外観の変更</span><span class="sxs-lookup"><span data-stu-id="3ffbd-164">Change the appearance of a map</span></span>

<span data-ttu-id="3ffbd-165">地図の外観をカスタマイズするには、マップ コントロールの [**StyleSheet**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.StyleSheet) プロパティを既存の [**MapStyleSheet**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapstylesheet) オブジェクトに設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-165">To customize the look and feel of the map, set the [**StyleSheet**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.StyleSheet) property of the map control to any of the existing [**MapStyleSheet**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapstylesheet) objects.</span></span>

```csharp
myMap.StyleSheet = MapStyleSheet.RoadDark();
```

![濃色スタイルの地図](images/style-dark.png)

<span data-ttu-id="3ffbd-167">また、JSON を使用してカスタム スタイルを定義し、その JSON を使用して [**MapStyleSheet**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapstylesheet) オブジェクトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-167">You can also use JSON to define custom styles and then use that JSON to create a [**MapStyleSheet**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapstylesheet) object.</span></span>

<span data-ttu-id="3ffbd-168">JSON を使用して対話的に作成できるスタイル シート、[マップ スタイル シート エディター](https://www.microsoft.com/p/map-style-sheet-editor/9nbhtcjt72ft)アプリケーション。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-168">Style sheet JSON can be created interactively using the [Map Style Sheet Editor](https://www.microsoft.com/p/map-style-sheet-editor/9nbhtcjt72ft) application.</span></span>

```csharp
myMap.StyleSheet = MapStyleSheet.ParseFromJson(@"
    {
        ""version"": ""1.0"",
        ""settings"": {
            ""landColor"": ""#FFFFFF"",
            ""spaceColor"": ""#000000""
        },
        ""elements"": {
            ""mapElement"": {
                ""labelColor"": ""#000000"",
                ""labelOutlineColor"": ""#FFFFFF""
            },
            ""water"": {
                ""fillColor"": ""#DDDDDD""
            },
            ""area"": {
                ""fillColor"": ""#EEEEEE""
            },
            ""political"": {
                ""borderStrokeColor"": ""#CCCCCC"",
                ""borderOutlineColor"": ""#00000000""
            }
        }
    }
");
```

![カスタム スタイルの地図](images/style-custom.png)

<span data-ttu-id="3ffbd-170">完全な JSON エントリのリファレンスについては、「[マップ スタイル シート リファレンス](elements-of-map-style-sheet.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-170">For the complete JSON entry reference, see [Map style sheet reference](elements-of-map-style-sheet.md).</span></span>

<span data-ttu-id="3ffbd-171">最初は既存のシートを使用して、次に JSON を使用して要素を上書きできます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-171">You can start with an existing sheet and then use JSON to override any elements that you want.</span></span> <span data-ttu-id="3ffbd-172">この例では、最初は既存のスタイルを使用し、次に JSON を使用して水域の色のみを変更しています。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-172">This example, starts with an existing style and uses JSON to change only the color of water areas.</span></span>

```csharp
 MapStyleSheet \customSheet = MapStyleSheet.ParseFromJson(@"
    {
        ""version"": ""1.0"",
        ""elements"": {
            ""water"": {
                ""fillColor"": ""#DDDDDD""
            }
        }
    }
");

MapStyleSheet builtInSheet = MapStyleSheet.RoadDark();

myMap.StyleSheet = MapStyleSheet.Combine(new List<MapStyleSheet> { builtInSheet, customSheet });
```

![複数のスタイルの地図](images/style-combined.png)

>[!NOTE]
><span data-ttu-id="3ffbd-174">2 番目のスタイル シートで定義するスタイルは、最初のスタイルを上書きします。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-174">Styles that you define in the second style sheet override the styles in the first.</span></span>

## <a name="set-orientation-and-perspective"></a><span data-ttu-id="3ffbd-175">向きと視点の設定</span><span class="sxs-lookup"><span data-stu-id="3ffbd-175">Set orientation and perspective</span></span>

<span data-ttu-id="3ffbd-176">マップ カメラを拡大、縮小、回転、傾けることで、求める効果をもたらす適切な角度に設定できます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-176">Zoom in, zoom out, rotate, and tilt the map's camera to get just the right angle for the effect that you want.</span></span> <span data-ttu-id="3ffbd-177">次のプロパティをお試しください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-177">Try these properties.</span></span>

-   <span data-ttu-id="3ffbd-178">地図の**中心**を地理的位置に設定するには、[**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-178">Set the **center** of the map to a geographic point by setting the [**Center**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) property.</span></span>
-   <span data-ttu-id="3ffbd-179">[  **ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel) プロパティに 1 ～ 20 度の値を設定することにより、地図の**ズーム レベル**を設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-179">Set the **zoom level** of the map by setting the [**ZoomLevel**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel) property to a value between 1 and 20.</span></span>
-   <span data-ttu-id="3ffbd-180">[  **Heading**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.heading) プロパティを設定することにより地図の**回転**を設定します。ここでは 0 度または 360 度 = 北、90 度 = 東、180 度 = 南、270 度 = 西です。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-180">Set the **rotation** of the map by setting the [**Heading**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.heading) property, where 0 or 360 degrees = North, 90 = East, 180 = South, and 270 = West.</span></span>
-   <span data-ttu-id="3ffbd-181">[  **DesiredPitch**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.desiredpitch) プロパティに 0 ～ 65 度の値を設定することにより、地図の**傾き**を設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-181">Set the **tilt** of the map by setting the [**DesiredPitch**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.desiredpitch) property to a value between 0 and 65 degrees.</span></span>

## <a name="show-and-hide-map-features"></a><span data-ttu-id="3ffbd-182">地図機能を表示または非表示にする</span><span class="sxs-lookup"><span data-stu-id="3ffbd-182">Show and hide map features</span></span>

<span data-ttu-id="3ffbd-183">道路やランドマークなどの地図機能を表示または非表示にするには、[**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の次のプロパティの値を設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-183">Show or hide map features such as roads and landmarks by setting the values of the following properties of the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span>

* <span data-ttu-id="3ffbd-184">地図に**建物やランドマーク**を表示するには、[**LandmarksVisible**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.landmarksvisible) プロパティを有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-184">Display **buildings and landmarks** on the map by enabling or disabling the [**LandmarksVisible**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.landmarksvisible) property.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3ffbd-185">建物の表示と非表示を切り替えることはできますが、3 次元表示を無効にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-185">You can show or hide buildings, but you can't prevent them from appearing 3 dimensions.</span></span>  

* <span data-ttu-id="3ffbd-186">地図に公共階段などの**歩行者用の施設**を表示するには、[**PedestrianFeaturesVisible**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pedestrianfeaturesvisible) プロパティを有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-186">Display **pedestrian features** such as public stairs on the map by enabling or disabling the [**PedestrianFeaturesVisible**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pedestrianfeaturesvisible) property.</span></span>
* <span data-ttu-id="3ffbd-187">地図に**交通情報**を表示するには、[**TrafficFlowVisible**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trafficflowvisible) プロパティを有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-187">Display **traffic** on the map by enabling or disabling the [**TrafficFlowVisible**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trafficflowvisible) property.</span></span>
* <span data-ttu-id="3ffbd-188">地図に**透かし**を表示するかどうかを指定するには、[**WatermarkMode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.watermarkmode) プロパティを [**MapWatermarkMode**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapWatermarkMode) 定数のいずれかに設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-188">Specify whether the **watermark** is displayed on the map by setting the [**WatermarkMode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.watermarkmode) property to one of the [**MapWatermarkMode**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapWatermarkMode) constants.</span></span>
* <span data-ttu-id="3ffbd-189">地図に**自動車ルートや徒歩ルート**を表示するには、マップ コントロールの [**Routes**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.routes) コレクションに [**MapRouteView**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapRouteView) を追加します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-189">Display a **driving or walking route** on the map by adding a [**MapRouteView**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapRouteView) to the [**Routes**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.routes) collection of the Map control.</span></span> <span data-ttu-id="3ffbd-190">詳しい情報と例については、「[地図へのルートとルート案内の表示](routes-and-directions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-190">For more info and an example, see [Display routes and directions on a map](routes-and-directions.md).</span></span>

<span data-ttu-id="3ffbd-191">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) でプッシュピン、図形、XAML コントロールを表示する方法については、「[関心のあるポイント (POI) の地図への表示](display-poi.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-191">For info about how to display pushpins, shapes, and XAML controls in the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl), see [Display points of interest (POI) on a map](display-poi.md).</span></span>

## <a name="display-streetside-views"></a><span data-ttu-id="3ffbd-192">Streetside ビューの表示</span><span class="sxs-lookup"><span data-stu-id="3ffbd-192">Display Streetside views</span></span>


<span data-ttu-id="3ffbd-193">Streetside ビューは、視点がストリート レベルにある場合の場所の見え方を示すもので、マップ コントロールの上に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-193">A Streetside view is a street-level perspective of a location that appears on top of the map control.</span></span>

![マップ コントロールの Streetside ビューの例。](images/onlystreetside-730width.png)

<span data-ttu-id="3ffbd-195">Streetside ビューの「内部」での操作は、マップ コントロールにもともと表示されている地図とは独立していることを考慮します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-195">Consider the experience "inside" the Streetside view separate from the map originally displayed in the map control.</span></span> <span data-ttu-id="3ffbd-196">たとえば、Streetside ビューで場所を変更しても、Streetside ビューの「下」にある地図の場所や外観は変わりません。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-196">For example, changing the location in the Streetside view does not change the location or appearance of the map "under" the Streetside view.</span></span> <span data-ttu-id="3ffbd-197">コントロールの右上隅にある **[X]** をクリックして Streetside ビューを閉じると、元の地図は Streetside ビューが表示される前のままです。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-197">After you close the Streetside view (by clicking the **X** in the upper right corner of the control), the original map remains unchanged.</span></span>

<span data-ttu-id="3ffbd-198">Streetside ビューを表示するには</span><span class="sxs-lookup"><span data-stu-id="3ffbd-198">To display a Streetside view</span></span>

1.  <span data-ttu-id="3ffbd-199">[  **IsStreetsideSupported**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.isstreetsidesupported) を確認して、Streetside ビューがデバイスでサポートされているかどうかを調べます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-199">Determine if Streetside views are supported on the device by checking [**IsStreetsideSupported**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.isstreetsidesupported).</span></span>
2.  <span data-ttu-id="3ffbd-200">Streetside ビューがサポートされている場合は、[**FindNearbyAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.streetsidepanorama.findnearbyasync) を呼び出し、指定した位置の近くに [**StreetsidePanorama**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.StreetsidePanorama) を作成します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-200">If Streetside view is supported, create a [**StreetsidePanorama**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.StreetsidePanorama) near the specified location by calling [**FindNearbyAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.streetsidepanorama.findnearbyasync).</span></span>
3.  <span data-ttu-id="3ffbd-201">[  **StreetsidePanorama**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.StreetsidePanorama) が null でないかどうかを確認し、近隣のパノラマ写真があるかどうかを調べます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-201">Determine if a nearby panorama was found by checking if the [**StreetsidePanorama**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.StreetsidePanorama) is not null</span></span>
4.  <span data-ttu-id="3ffbd-202">近隣のパノラマ写真があった場合、[**StreetsideExperience**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.streetsideexperience.) を作成し、マップ コントロールの [**CustomExperience**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.customexperience) プロパティに設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-202">If a nearby panorama was found, create a [**StreetsideExperience**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.streetsideexperience.) for the map control's [**CustomExperience**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.customexperience) property.</span></span>

<span data-ttu-id="3ffbd-203">次の例は、前掲の画像に似た Streetside ビューを表示する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-203">This example shows how to display a Streetside view similar to the previous image.</span></span>

<span data-ttu-id="3ffbd-204">**注**  概要マップは、マップ コントロールのサイズが小さすぎる場合は表示されません。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-204">**Note**  The overview map will not appear if the map control is sized too small.</span></span>

 

```csharp
private async void showStreetsideView()
{
   // Check if Streetside is supported.
   if (MapControl1.IsStreetsideSupported)
   {
      // Find a panorama near Avenue Gustave Eiffel.
      BasicGeoposition cityPosition = new BasicGeoposition() { Latitude = 48.858, Longitude = 2.295};
      Geopoint cityCenter = new Geopoint(cityPosition);
      StreetsidePanorama panoramaNearCity = await StreetsidePanorama.FindNearbyAsync(cityCenter);

      // Set the Streetside view if a panorama exists.
      if (panoramaNearCity != null)
      {
         // Create the Streetside view.
         StreetsideExperience ssView = new StreetsideExperience(panoramaNearCity);
         ssView.OverviewMapVisible = true;
         MapControl1.CustomExperience = ssView;
      }
   }
   else
   {
      // If Streetside is not supported
      ContentDialog viewNotSupportedDialog = new ContentDialog()
      {
         Title = "Streetside is not supported",
         Content ="\nStreetside views are not supported on this device.",
         PrimaryButtonText = "OK"
      };
      await viewNotSupportedDialog.ShowAsync();            
   }
}
```

<a id="3Dviews" />
## <a name="display-aerial-3d-views"></a><span data-ttu-id="3ffbd-205">航空写真 3D ビューの表示</span><span class="sxs-lookup"><span data-stu-id="3ffbd-205">Display aerial 3D views</span></span>


<span data-ttu-id="3ffbd-206">[  **MapScene**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapScene) クラスを使って、地図の 3D 視点を指定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-206">Specify a 3D perspective of the map by using the [**MapScene**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapScene) class.</span></span> <span data-ttu-id="3ffbd-207">マップ シーンは、地図に表示される 3D ビューを表します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-207">The map scene represents the 3D view that appears in the map.</span></span> <span data-ttu-id="3ffbd-208">[  **MapCamera**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapCamera) クラスは、このようなビューが表示されるカメラの位置を表します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-208">The [**MapCamera**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapCamera) class represents the position of the camera that would display such a view.</span></span>

![マップ シーンの場所と MapCamera の場所を示す図](images/mapcontrol-techdiagram.png)

<span data-ttu-id="3ffbd-210">建物などの地物を地図表面に 3D 表示するには、マップ コントロールの [**Style**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) プロパティを [**MapStyle.Aerial3DWithRoads**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapStyle) に設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-210">To make buildings and other features on the map surface appear in 3D, set the map control's [**Style**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) property to [**MapStyle.Aerial3DWithRoads**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapStyle).</span></span> <span data-ttu-id="3ffbd-211">**Aerial3DWithRoads** スタイルの 3D ビューの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-211">This is an example of a 3D view with the **Aerial3DWithRoads** style.</span></span>

![3D 地図ビューの例。](images/only3d-730width.png)

<span data-ttu-id="3ffbd-213">3D ビューを表示するには</span><span class="sxs-lookup"><span data-stu-id="3ffbd-213">To display a 3D view</span></span>

1.  <span data-ttu-id="3ffbd-214">[  **Is3DSupported**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.is3dsupported) を確認して、3D ビューがデバイスでサポートされているかどうかを調べます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-214">Determine if 3D views are supported on the device by checking [**Is3DSupported**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.is3dsupported).</span></span>
2.  <span data-ttu-id="3ffbd-215">3D ビューがサポートされている場合は、マップ コントロールの [**Style**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) プロパティを [**MapStyle.Aerial3DWithRoads**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapStyle) に設定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-215">If 3D views is supported, set the map control's [**Style**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) property to [**MapStyle.Aerial3DWithRoads**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapStyle).</span></span>
3.  <span data-ttu-id="3ffbd-216">[  **CreateFromLocationAndRadius**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapscene.createfromlocationandradius)、[**CreateFromCamera**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapscene.createfromcamera) などの多数の **CreateFrom** メソッドの中から [**MapScene**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapScene) オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-216">Create a [**MapScene**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapScene) object using one of the many **CreateFrom** methods, such as [**CreateFromLocationAndRadius**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapscene.createfromlocationandradius) and [**CreateFromCamera**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapscene.createfromcamera).</span></span>
4.  <span data-ttu-id="3ffbd-217">[  **TrySetSceneAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync) を呼び出して、3D ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-217">Call [**TrySetSceneAsync**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync) to display the 3D view.</span></span> <span data-ttu-id="3ffbd-218">また、ビューが変わるときに使うアニメーションをオプションで指定することもできます。そのためには、[**MapAnimationKind**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapAnimationKind) 列挙値の定数を指定します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-218">You can also specify an optional animation to use when the view changes by providing a constant from the [**MapAnimationKind**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapAnimationKind) enumeration.</span></span>

<span data-ttu-id="3ffbd-219">次の例は、3D ビューを表示する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-219">This example shows how to display a 3D view.</span></span>

```csharp
private async void display3DLocation()
{
   if (MapControl1.Is3DSupported)
   {
      // Set the aerial 3D view.
      MapControl1.Style = MapStyle.Aerial3DWithRoads;

      // Specify the location.
      BasicGeoposition hwGeoposition = new BasicGeoposition() { Latitude = 43.773251, Longitude = 11.255474};
      Geopoint hwPoint = new Geopoint(hwGeoposition);

      // Create the map scene.
      MapScene hwScene = MapScene.CreateFromLocationAndRadius(hwPoint,
                                                                           80, /* show this many meters around */
                                                                           0, /* looking at it to the North*/
                                                                           60 /* degrees pitch */);
      // Set the 3D view with animation.
      await MapControl1.TrySetSceneAsync(hwScene,MapAnimationKind.Bow);
   }
   else
   {
      // If 3D views are not supported, display dialog.
      ContentDialog viewNotSupportedDialog = new ContentDialog()
      {
         Title = "3D is not supported",
         Content = "\n3D views are not supported on this device.",
         PrimaryButtonText = "OK"
      };
      await viewNotSupportedDialog.ShowAsync();
   }
}
```

## <a name="get-info-about-locations"></a><span data-ttu-id="3ffbd-220">位置に関する情報の取得</span><span class="sxs-lookup"><span data-stu-id="3ffbd-220">Get info about locations</span></span>


<span data-ttu-id="3ffbd-221">地図上の位置に関する情報を取得するには、[**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の次のメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-221">Get info about locations on the map by calling the following methods of the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span>

-   <span data-ttu-id="3ffbd-222">[**TryGetLocationFromOffset** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getlocationfromoffset)メソッド - マップ コントロールのビューポートに指定したポイントに対応する地理的な場所を取得します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-222">[**TryGetLocationFromOffset**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getlocationfromoffset) method - Get the geographic location that corresponds to the specified point in the viewport of the Map control.</span></span>
-   <span data-ttu-id="3ffbd-223">[**GetOffsetFromLocation** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getoffsetfromlocation)メソッド - 指定した地理的な場所に対応するマップ コントロールのビューポート内のポイントを取得します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-223">[**GetOffsetFromLocation**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getoffsetfromlocation) method - Get the point in the viewport of the Map control that corresponds to the specified geographic location.</span></span>
-   <span data-ttu-id="3ffbd-224">[**IsLocationInView** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.islocationinview)メソッド - 指定した地理的な場所が、マップ コントロールのビューポートに表示されているかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-224">[**IsLocationInView**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.islocationinview) method - Determine whether the specified geographic location is currently visible in the viewport of the Map control.</span></span>
-   <span data-ttu-id="3ffbd-225">[**FindMapElementsAtOffset** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.findmapelementsatoffset)メソッド - マップ コントロールのビューポートに指定したポイントにある、マップ上の要素を取得します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-225">[**FindMapElementsAtOffset**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.findmapelementsatoffset) method - Get the elements on the map located at the specified point in the viewport of the Map control.</span></span>

## <a name="handle-interaction-and-changes"></a><span data-ttu-id="3ffbd-226">操作と変更の処理</span><span class="sxs-lookup"><span data-stu-id="3ffbd-226">Handle interaction and changes</span></span>


<span data-ttu-id="3ffbd-227">地図上でのユーザー入力ジェスチャを処理するには、[**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の次のイベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-227">Handle user input gestures on the map by handling the following events of the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span> <span data-ttu-id="3ffbd-228">地図上の地理的な位置、およびジェスチャが行われたビューポート内の実際の位置に関する情報を取得するには、[**MapInputEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapInputEventArgs) の [**Location**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapinputeventargs.location) プロパティと [**Position**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapinputeventargs.position) プロパティの値を確認します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-228">Get info about the geographic location on the map and the physical position in the viewport where the gesture occurred by checking the values of the [**Location**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapinputeventargs.location) and [**Position**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapinputeventargs.position) properties of the [**MapInputEventArgs**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapInputEventArgs).</span></span>

-   [<span data-ttu-id="3ffbd-229">**MapTapped**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-229">**MapTapped**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.maptapped)
-   [<span data-ttu-id="3ffbd-230">**MapDoubleTapped**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-230">**MapDoubleTapped**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapdoubletapped)
-   [<span data-ttu-id="3ffbd-231">**MapHolding**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-231">**MapHolding**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapholding)

<span data-ttu-id="3ffbd-232">地図が読み込まれている最中であるか、完全に読み込まれたかどうかを判断するには、コントロールの [**LoadingStatusChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.loadingstatuschanged) イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-232">Determine whether the map is loading or completely loaded by handling the control's [**LoadingStatusChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.loadingstatuschanged) event.</span></span>

<span data-ttu-id="3ffbd-233">ユーザーやアプリによる地図の設定変更に対応するには、[**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の次のイベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-233">Handle changes that happen when the user or the app changes the settings of the map by handling the following events of the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl).</span></span> [<span data-ttu-id="3ffbd-234">マップのガイドライン</span><span class="sxs-lookup"><span data-stu-id="3ffbd-234">Guidelines for maps</span></span>](https://docs.microsoft.com/windows/uwp/maps-and-location/controls-map)

-   [<span data-ttu-id="3ffbd-235">**CenterChanged**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-235">**CenterChanged**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.centerchanged)
-   [<span data-ttu-id="3ffbd-236">**HeadingChanged**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-236">**HeadingChanged**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.headingchanged)
-   [<span data-ttu-id="3ffbd-237">**PitchChanged**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-237">**PitchChanged**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pitchchanged)
-   [<span data-ttu-id="3ffbd-238">**ZoomLevelChanged**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-238">**ZoomLevelChanged**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevelchanged)

## <a name="best-practice-recommendations"></a><span data-ttu-id="3ffbd-239">推奨される運用方法</span><span class="sxs-lookup"><span data-stu-id="3ffbd-239">Best practice recommendations</span></span>

-   <span data-ttu-id="3ffbd-240">ユーザーが地理情報を表示するためにパンとズームを過度に使用しなくて済むように、十分な画面領域 (または画面全体) を使用してマップを表示します。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-240">Use ample screen space (or the entire screen) to display the map so that users don't have to pan and zoom excessively to view geographical information.</span></span>

-   <span data-ttu-id="3ffbd-241">静的な情報ビューの提示をするためにのみマップを使う場合、小さなマップを使う方が適している場合があります。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-241">If the map is only used to present a static, informational view, then using a smaller map might be more appropriate.</span></span> <span data-ttu-id="3ffbd-242">小さく静的なマップを使う場合は、使いやすさを考えてサイズを決めます。画面上の領域を十分節約できる程度に小さく、判読しにくくならない程度に大きくします。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-242">If you go with a smaller, static map, base its dimensions on usability—small enough to conserve enough screen real estate, but large enough to remain legible.</span></span>

-   <span data-ttu-id="3ffbd-243">マップ シーンに関心のあるポイントを埋め込むには、[**MapElements**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementsproperty) を使います。その他の情報も、マップ シーンのオーバーレイとして表示される一時的な UI に表示できます。</span><span class="sxs-lookup"><span data-stu-id="3ffbd-243">Embed the points of interest in the map scene using [**map elements**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementsproperty); any additional information can be displayed as transient UI that overlays the map scene.</span></span>

## <a name="related-topics"></a><span data-ttu-id="3ffbd-244">関連トピック</span><span class="sxs-lookup"><span data-stu-id="3ffbd-244">Related topics</span></span>

* [<span data-ttu-id="3ffbd-245">Bing Maps Developer Center</span><span class="sxs-lookup"><span data-stu-id="3ffbd-245">Bing Maps Developer Center</span></span>](https://www.bingmapsportal.com/)
* [<span data-ttu-id="3ffbd-246">UWP の地図のサンプル</span><span class="sxs-lookup"><span data-stu-id="3ffbd-246">UWP map sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619977)
* [<span data-ttu-id="3ffbd-247">現在の場所を取得します</span><span class="sxs-lookup"><span data-stu-id="3ffbd-247">Get current location</span></span>](get-location.md)
* [<span data-ttu-id="3ffbd-248">位置認識アプリの設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="3ffbd-248">Design guidelines for location-aware apps</span></span>](https://docs.microsoft.com/windows/uwp/maps-and-location/guidelines-and-checklist-for-detecting-location)
* [<span data-ttu-id="3ffbd-249">地図の設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="3ffbd-249">Design guidelines for maps</span></span>](https://docs.microsoft.com/windows/uwp/maps-and-location/controls-map)
* [<span data-ttu-id="3ffbd-250">Build 2015 のビデオ:Windows アプリでの電話、タブレット、PC で使用できるマップと位置情報の活用</span><span class="sxs-lookup"><span data-stu-id="3ffbd-250">Build 2015 video: Leveraging Maps and Location Across Phone, Tablet, and PC in Your Windows Apps</span></span>](https://channel9.msdn.com/Events/Build/2015/2-757)
* [<span data-ttu-id="3ffbd-251">UWP の交通情報アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="3ffbd-251">UWP traffic app sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619982)
* [<span data-ttu-id="3ffbd-252">**MapControl**</span><span class="sxs-lookup"><span data-stu-id="3ffbd-252">**MapControl**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl)
