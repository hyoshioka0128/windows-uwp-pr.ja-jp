---
title: ジオコーディングと逆ジオコーディングの実行
description: このガイドでは、住所を地理的な場所 (ジオコーディング) に変換し、Windows.Services.Maps 名前空間に MapLocationFinder クラスのメソッドを呼び出すことによって (逆ジオコーディング) の住所を地理的な場所に変換する方法を示します。
ms.assetid: B912BE80-3E1D-43BB-918F-7A43327597D2
ms.date: 07/02/2018
ms.topic: article
keywords: Windows 10, UWP, ジオコーディング, 地図, 位置情報
ms.localizationpriority: medium
ms.openlocfilehash: 88687f6e7074ff7c914927a81a08720336b3c60c
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371871"
---
# <a name="perform-geocoding-and-reverse-geocoding"></a><span data-ttu-id="3052a-104">ジオコーディングと逆ジオコーディングの実行</span><span class="sxs-lookup"><span data-stu-id="3052a-104">Perform geocoding and reverse geocoding</span></span>

<span data-ttu-id="3052a-105">このガイドは、住所を地理的な場所 (ジオコーディング) に変換しのメソッドを呼び出して、地理的な場所を住所 (逆ジオコーディング) に変換する方法を示します、 [ **MapLocationFinder**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder)クラス、 [ **Windows.Services.Maps** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps)名前空間。</span><span class="sxs-lookup"><span data-stu-id="3052a-105">This guide shows you how to convert street addresses to geographic locations (geocoding) and convert geographic locations to street addresses (reverse geocoding) by calling the methods of the [**MapLocationFinder**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder) class in the [**Windows.Services.Maps**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps) namespace.</span></span>

> [!TIP]
> <span data-ttu-id="3052a-106">詳細については、アプリでマップを使用して、ダウンロード、 [MapControl](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl)サンプルから、 [Windows ユニバーサル サンプル リポジトリ](h https://github.com/Microsoft/Windows-universal-samples)GitHub で。</span><span class="sxs-lookup"><span data-stu-id="3052a-106">To learn more about using maps in your app, download the [MapControl](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl) sample from the [Windows universal samples repo](hhttps://github.com/Microsoft/Windows-universal-samples) on GitHub.</span></span>

<span data-ttu-id="3052a-107">ジオコーディングと逆ジオコーディングに関連するクラスは、次のように編成されます。</span><span class="sxs-lookup"><span data-stu-id="3052a-107">The classes involved in geocoding and reverse geocoding are organized as follows.</span></span>

-   <span data-ttu-id="3052a-108">[ **MapLocationFinder** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder)クラスには、ジオコーディングを処理するメソッドが含まれています ([**FindLocationsAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsasync)) とリバース ジオコーディング ([**FindLocationsAtAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsatasync))。</span><span class="sxs-lookup"><span data-stu-id="3052a-108">The [**MapLocationFinder**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder) class contains methods that handle geocoding ([**FindLocationsAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsasync)) and reverse geocoding ([**FindLocationsAtAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsatasync)).</span></span>
-   <span data-ttu-id="3052a-109">これらのメソッドは両方を返す、 [ **MapLocationFinderResult** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult)インスタンス。</span><span class="sxs-lookup"><span data-stu-id="3052a-109">These methods both return a [**MapLocationFinderResult**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult) instance.</span></span>
-   <span data-ttu-id="3052a-110">[**場所**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinderresult.locations)のプロパティ、 [ **MapLocationFinderResult** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult)のコレクションを公開[ **MapLocation** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="3052a-110">The [**Locations**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinderresult.locations) property of the [**MapLocationFinderResult**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult) exposes a collection of [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) objects.</span></span> 
-   <span data-ttu-id="3052a-111">[**MapLocation** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation)両方のオブジェクトがある、 [**アドレス**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocation.address)プロパティを公開する、 [ **MapAddress** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapAddress)、番地を表すオブジェクト、 [**ポイント**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocation.point)プロパティを公開する、 [ **Geopoint** ](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geopoint)オブジェクト地理的な場所を表すです。</span><span class="sxs-lookup"><span data-stu-id="3052a-111">[**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) objects have both an [**Address**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocation.address) property, which exposes a [**MapAddress**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapAddress) object representing a street address, and a [**Point**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocation.point) property, which exposes a [**Geopoint**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geopoint) object representing a geographic location.</span></span>

> [!IMPORTANT]
><span data-ttu-id="3052a-112"> マップ サービスを使用する前に、マップの認証キーを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3052a-112"> You must specify a maps authentication key before you can use map services.</span></span> <span data-ttu-id="3052a-113">詳しくは、「[マップ認証キーの要求](authentication-key.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="3052a-113">For more info, see [Request a maps authentication key](authentication-key.md).</span></span>

## <a name="get-a-location-geocode"></a><span data-ttu-id="3052a-114">位置情報の取得 (ジオコーディング)</span><span class="sxs-lookup"><span data-stu-id="3052a-114">Get a location (Geocode)</span></span>

<span data-ttu-id="3052a-115">このセクションでは、住所や場所名を地理的な場所 (ジオコーディング) に変換する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="3052a-115">This section shows how to convert a street address or a place name to a geographic location (geocoding).</span></span>

1.  <span data-ttu-id="3052a-116">オーバー ロードの 1 つを呼び出して、 [ **FindLocationsAsync** ](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsasync)のメソッド、 [ **MapLocationFinder** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder)スポット名または住所を持つクラスアドレス。</span><span class="sxs-lookup"><span data-stu-id="3052a-116">Call one of the overloads of the [**FindLocationsAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsasync) method of the [**MapLocationFinder**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder) class with a place name or street address.</span></span>
2.  <span data-ttu-id="3052a-117">[ **FindLocationsAsync** ](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsasync)メソッドを返します。 を[ **MapLocationFinderResult** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="3052a-117">The [**FindLocationsAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsasync) method returns a [**MapLocationFinderResult**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult) object.</span></span>
3.  <span data-ttu-id="3052a-118">使用して、 [**場所**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinderresult.locations)のプロパティ、 [ **MapLocationFinderResult** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult)コレクションを公開する[ **MapLocation** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="3052a-118">Use the [**Locations**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinderresult.locations) property of the [**MapLocationFinderResult**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult) to expose a collection [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) objects.</span></span> <span data-ttu-id="3052a-119">複数存在する可能性があります[ **MapLocation** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation)オブジェクトをシステムが複数ありますので、指定された入力に対応する場所。</span><span class="sxs-lookup"><span data-stu-id="3052a-119">There may be multiple [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) objects because the system may find multiple locations that correspond to the given input.</span></span>

```csharp
using Windows.Services.Maps;
using Windows.Devices.Geolocation;
...
private async void geocodeButton_Click(object sender, RoutedEventArgs e)
{
   // The address or business to geocode.
   string addressToGeocode = "Microsoft";

   // The nearby location to use as a query hint.
   BasicGeoposition queryHint = new BasicGeoposition();
   queryHint.Latitude = 47.643;
   queryHint.Longitude = -122.131;
   Geopoint hintPoint = new Geopoint(queryHint);

   // Geocode the specified address, using the specified reference point
   // as a query hint. Return no more than 3 results.
   MapLocationFinderResult result =
         await MapLocationFinder.FindLocationsAsync(
                           addressToGeocode,
                           hintPoint,
                           3);

   // If the query returns results, display the coordinates
   // of the first result.
   if (result.Status == MapLocationFinderStatus.Success)
   {
      tbOutputText.Text = "result = (" +
            result.Locations[0].Point.Position.Latitude.ToString() + "," +
            result.Locations[0].Point.Position.Longitude.ToString() + ")";
   }
}
```

<span data-ttu-id="3052a-120">このコードでは、`tbOutputText` テキスト ボックスに次の結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3052a-120">This code displays the following results to the `tbOutputText` textbox.</span></span>

``` syntax
result = (47.6406099647284,-122.129339994863)
```

## <a name="get-an-address-reverse-geocode"></a><span data-ttu-id="3052a-121">住所の取得 (逆ジオコーディング)</span><span class="sxs-lookup"><span data-stu-id="3052a-121">Get an address (reverse geocode)</span></span>

<span data-ttu-id="3052a-122">このセクションでは、地理的な場所を (逆ジオコーディング) アドレスに変換する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="3052a-122">This section shows how to convert a geographic location to an address (reverse geocoding).</span></span>

1.  <span data-ttu-id="3052a-123">[  **MapLocationFinder**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder) クラスの [**FindLocationsAtAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsatasync) メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="3052a-123">Call the [**FindLocationsAtAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsatasync) method of the [**MapLocationFinder**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder) class.</span></span>
2.  <span data-ttu-id="3052a-124">[  **FindLocationsAtAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsatasync) メソッドは、一致する [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) オブジェクトのコレクションを含む [**MapLocationFinderResult**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult) オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="3052a-124">The [**FindLocationsAtAsync**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsatasync) method returns a [**MapLocationFinderResult**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult) object that contains a collection of matching [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) objects.</span></span>
3.  <span data-ttu-id="3052a-125">使用して、 [**場所**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinderresult.locations)のプロパティ、 [ **MapLocationFinderResult** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult)コレクションを公開する[ **MapLocation** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="3052a-125">Use the [**Locations**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinderresult.locations) property of the [**MapLocationFinderResult**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinderResult) to expose a collection [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) objects.</span></span> <span data-ttu-id="3052a-126">複数存在する可能性があります[ **MapLocation** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation)オブジェクトをシステムが複数ありますので、指定された入力に対応する場所。</span><span class="sxs-lookup"><span data-stu-id="3052a-126">There may be multiple [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation) objects because the system may find multiple locations that correspond to the given input.</span></span>
4.  <span data-ttu-id="3052a-127">アクセス[ **MapAddress** ](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapAddress)オブジェクトを通じて、 [**アドレス**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocation.address)の各プロパティ[ **MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation).</span><span class="sxs-lookup"><span data-stu-id="3052a-127">Access [**MapAddress**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapAddress) objects through the [**Address**](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocation.address) property of each [**MapLocation**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocation).</span></span>

```csharp
using Windows.Services.Maps;
using Windows.Devices.Geolocation;
...
private async void reverseGeocodeButton_Click(object sender, RoutedEventArgs e)
{
   // The location to reverse geocode.
   BasicGeoposition location = new BasicGeoposition();
   location.Latitude = 47.643;
   location.Longitude = -122.131;
   Geopoint pointToReverseGeocode = new Geopoint(location);

   // Reverse geocode the specified geographic location.
   MapLocationFinderResult result =
         await MapLocationFinder.FindLocationsAtAsync(pointToReverseGeocode);

   // If the query returns results, display the name of the town
   // contained in the address of the first result.
   if (result.Status == MapLocationFinderStatus.Success)
   {
      tbOutputText.Text = "town = " +
            result.Locations[0].Address.Town;
   }
}
```

<span data-ttu-id="3052a-128">このコードでは、`tbOutputText` テキスト ボックスに次の結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="3052a-128">This code displays the following results to the `tbOutputText` textbox.</span></span>

``` syntax
town = Redmond
```

## <a name="related-topics"></a><span data-ttu-id="3052a-129">関連トピック</span><span class="sxs-lookup"><span data-stu-id="3052a-129">Related topics</span></span>

* [<span data-ttu-id="3052a-130">UWP の地図のサンプル</span><span class="sxs-lookup"><span data-stu-id="3052a-130">UWP map sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619977)
* [<span data-ttu-id="3052a-131">UWP の交通情報アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="3052a-131">UWP traffic app sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619982)
* [<span data-ttu-id="3052a-132">地図の設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="3052a-132">Design guidelines for maps</span></span>](https://docs.microsoft.com/windows/uwp/maps-and-location/controls-map)
* [<span data-ttu-id="3052a-133">ビデオ:Windows アプリでの電話、タブレット、PC で使用できるマップと位置情報の活用</span><span class="sxs-lookup"><span data-stu-id="3052a-133">Video: Leveraging Maps and Location Across Phone, Tablet, and PC in Your Windows Apps</span></span>](https://channel9.msdn.com/Events/Build/2015/2-757)
* [<span data-ttu-id="3052a-134">Bing Maps Developer Center</span><span class="sxs-lookup"><span data-stu-id="3052a-134">Bing Maps Developer Center</span></span>](https://www.bingmapsportal.com/)
* [<span data-ttu-id="3052a-135">**MapLocationFinder**クラス</span><span class="sxs-lookup"><span data-stu-id="3052a-135">**MapLocationFinder** class</span></span>](https://docs.microsoft.com/uwp/api/Windows.Services.Maps.MapLocationFinder)
* [<span data-ttu-id="3052a-136">**FindLocationsAsync**メソッド</span><span class="sxs-lookup"><span data-stu-id="3052a-136">**FindLocationsAsync** method</span></span>](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsasync)
* [<span data-ttu-id="3052a-137">**FindLocationsAtAsync**メソッド</span><span class="sxs-lookup"><span data-stu-id="3052a-137">**FindLocationsAtAsync** method</span></span>](https://docs.microsoft.com/uwp/api/windows.services.maps.maplocationfinder.findlocationsatasync)
