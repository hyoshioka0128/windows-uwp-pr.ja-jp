---
ms.assetid: D20C8E01-4E78-4115-A2E8-07BB3E67DDDC
description: この記事では、デバイスのライトにアクセスして使う方法を説明します (存在する場合)。 ライト機能は、デバイスのカメラやカメラのフラッシュ機能とは別に管理されます。
title: カメラに依存しない懐中電灯
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ddc7ad87a883c3512c719167975428b6c7746031
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66359054"
---
# <a name="camera-independent-flashlight"></a><span data-ttu-id="e154e-105">カメラに依存しない懐中電灯</span><span class="sxs-lookup"><span data-stu-id="e154e-105">Camera-independent Flashlight</span></span>



<span data-ttu-id="e154e-106">この記事では、デバイスのライトにアクセスして使う方法を説明します (存在する場合)。</span><span class="sxs-lookup"><span data-stu-id="e154e-106">This article shows how to access and use a device's lamp, if one is present.</span></span> <span data-ttu-id="e154e-107">ライト機能は、デバイスのカメラやカメラのフラッシュ機能とは別に管理されます。</span><span class="sxs-lookup"><span data-stu-id="e154e-107">Lamp functionality is managed separately from the device's camera and camera flash functionality.</span></span> <span data-ttu-id="e154e-108">この記事では、ライトへの参照の取得および設定の調整に加えて、使用されていないときにライトのリソースを正しく解放する方法と、ライトが別のアプリで使用されている場合に利用状況の変化を検出する方法も説明します。</span><span class="sxs-lookup"><span data-stu-id="e154e-108">In addition to acquiring a reference to the lamp and adjusting its settings, this article also shows you how to properly free up the lamp resource when it's not in use, and how to detect when the lamp's availability changes in case it is being used by another app.</span></span>

## <a name="get-the-devices-default-lamp"></a><span data-ttu-id="e154e-109">デバイスの既定のライトを取得する</span><span class="sxs-lookup"><span data-stu-id="e154e-109">Get the device's default lamp</span></span>

<span data-ttu-id="e154e-110">デバイスの既定のライトを取得するには、[**Lamp.GetDefaultAsync**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.getdefaultasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e154e-110">To get a device's default lamp device, call [**Lamp.GetDefaultAsync**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.getdefaultasync).</span></span> <span data-ttu-id="e154e-111">ライト関連 API は、[**Windows.Devices.Lights**](https://docs.microsoft.com/uwp/api/Windows.Devices.Lights) 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="e154e-111">The lamp APIs are found in the [**Windows.Devices.Lights**](https://docs.microsoft.com/uwp/api/Windows.Devices.Lights) namespace.</span></span> <span data-ttu-id="e154e-112">これらの API にアクセスするには、この名前空間の using ディレクティブをあらかじめ追加しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="e154e-112">Be sure to add a using directive for this namespace before attempting to access these APIs.</span></span>

[!code-cs[LightsNamespace](./code/Lamp/cs/MainPage.xaml.cs#SnippetLightsNamespace)]


[!code-cs[DeclareLamp](./code/Lamp/cs/MainPage.xaml.cs#SnippetDeclareLamp)]


[!code-cs[GetDefaultLamp](./code/Lamp/cs/MainPage.xaml.cs#SnippetGetDefaultLamp)]

<span data-ttu-id="e154e-113">返されたオブジェクトが **null** の場合、そのデバイスでは **Lamp** API がサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="e154e-113">If the returned object is **null**, the **Lamp** API is unsupported on the device.</span></span> <span data-ttu-id="e154e-114">一部のデバイスでは、ライトが物理的には存在していても、**Lamp** API がサポートされていないことがあります。</span><span class="sxs-lookup"><span data-stu-id="e154e-114">Some devices may not support the **Lamp** API even if there is a lamp physically present on the device.</span></span>

## <a name="get-a-specific-lamp-using-the-lamp-selector-string"></a><span data-ttu-id="e154e-115">ライト セレクター文字列を使って特定のランプを取得する</span><span class="sxs-lookup"><span data-stu-id="e154e-115">Get a specific lamp using the lamp selector string</span></span>

<span data-ttu-id="e154e-116">デバイスによっては、複数のライトが組み込まれている場合があります。</span><span class="sxs-lookup"><span data-stu-id="e154e-116">Some devices may have more than one lamp.</span></span> <span data-ttu-id="e154e-117">デバイスで利用可能なライトの一覧を取得するには、[**GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.getdeviceselector) を呼び出すことによってデバイスのセレクター文字列を取得します。</span><span class="sxs-lookup"><span data-stu-id="e154e-117">To obtain a list of lamps available on the device, get the device selector string by calling [**GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.getdeviceselector).</span></span> <span data-ttu-id="e154e-118">このセレクター文字列は、[**DeviceInformation.FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="e154e-118">This selector string can then be passed into [**DeviceInformation.FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync).</span></span> <span data-ttu-id="e154e-119">これは、さまざまな種類の多数のデバイスを列挙するために使うメソッドです。セレクター文字列はこのメソッドに対し、ライト デバイスのみを返すように伝えます。</span><span class="sxs-lookup"><span data-stu-id="e154e-119">This method is used to enumerate many different kinds of devices and the selector string lets the method know to return only lamp devices.</span></span> <span data-ttu-id="e154e-120">**FindAllAsync** から返される [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) オブジェクトは、デバイスで利用可能なライトを表す [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトのコレクションになります。</span><span class="sxs-lookup"><span data-stu-id="e154e-120">The [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) object returned from **FindAllAsync** is a collection of [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) objects representing the lamps available on the device.</span></span> <span data-ttu-id="e154e-121">一覧からいずれかのオブジェクトを選択し、[**Id**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.id) プロパティを [**Lamp.FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.fromidasync) に渡すと、要求されたライトへの参照を取得できます。</span><span class="sxs-lookup"><span data-stu-id="e154e-121">Select one of the objects in the list and then pass the [**Id**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.id) property to [**Lamp.FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.fromidasync) to get a reference to the requested lamp.</span></span> <span data-ttu-id="e154e-122">この例では、**System.Linq** 名前空間の **GetFirstOrDefault** 拡張メソッドを使って、[**EnclosureLocation.Panel**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.enclosurelocation.panel) プロパティの値が **Back** である **DeviceInformation** オブジェクトを選択しています。これにより、デバイス エンクロージャの背面にあるライトが選択されます (存在する場合)。</span><span class="sxs-lookup"><span data-stu-id="e154e-122">This example uses the **GetFirstOrDefault** extension method from the **System.Linq** namespace to select the **DeviceInformation** object where the [**EnclosureLocation.Panel**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.enclosurelocation.panel) property has a value of **Back**, which selects a lamp that is on the back of the device's enclosure, if one exists.</span></span>

<span data-ttu-id="e154e-123">[  **DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) API は [**Windows.Devices.Enumeration**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="e154e-123">Note that the [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) APIs are found in the [**Windows.Devices.Enumeration**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) namespace.</span></span>

[!code-cs[EnumerationNamespace](./code/Lamp/cs/MainPage.xaml.cs#SnippetEnumerationNamespace)]

[!code-cs[GetLampWithSelectionString](./code/Lamp/cs/MainPage.xaml.cs#SnippetGetLampWithSelectionString)]

## <a name="adjust-lamp-settings"></a><span data-ttu-id="e154e-124">ライトの設定を調整する</span><span class="sxs-lookup"><span data-stu-id="e154e-124">Adjust lamp settings</span></span>

<span data-ttu-id="e154e-125">[  **Lamp**](https://docs.microsoft.com/uwp/api/Windows.Devices.Lights.Lamp) クラスのインスタンスを作成した後、[**IsEnabled**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.isenabled) プロパティを **true** に設定することで、ライトをオンにします。</span><span class="sxs-lookup"><span data-stu-id="e154e-125">After you have an instance of the [**Lamp**](https://docs.microsoft.com/uwp/api/Windows.Devices.Lights.Lamp) class, turn the lamp on by setting the [**IsEnabled**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.isenabled) property to **true**.</span></span>

[!code-cs[LampSettingsOn](./code/Lamp/cs/MainPage.xaml.cs#SnippetLampSettingsOn)]

<span data-ttu-id="e154e-126">ライトをオフにするには、[**IsEnabled**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.isenabled) プロパティを **false** に設定します。</span><span class="sxs-lookup"><span data-stu-id="e154e-126">Turn the lamp off by setting the [**IsEnabled**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.isenabled) property to **false**.</span></span>

[!code-cs[LampSettingsOff](./code/Lamp/cs/MainPage.xaml.cs#SnippetLampSettingsOff)]

<span data-ttu-id="e154e-127">デバイスによっては、ライトで色の値がサポートされていることがあります。</span><span class="sxs-lookup"><span data-stu-id="e154e-127">Some devices have lamps that support color values.</span></span> <span data-ttu-id="e154e-128">ライトで色がサポートされているかどうかを確認するには、[**IsColorSettable**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.iscolorsettable) プロパティをチェックします。</span><span class="sxs-lookup"><span data-stu-id="e154e-128">Check if a lamp supports color by checking the [**IsColorSettable**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.iscolorsettable) property.</span></span> <span data-ttu-id="e154e-129">この値が **true** であれば、[**Color**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.color) プロパティを使ってライトの色を設定できます。</span><span class="sxs-lookup"><span data-stu-id="e154e-129">If this value is **true**, you can set the color of the lamp with the [**Color**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.color) property.</span></span>

[!code-cs[LampSettingsColor](./code/Lamp/cs/MainPage.xaml.cs#SnippetLampSettingsColor)]

## <a name="register-to-be-notified-if-the-lamp-availability-changes"></a><span data-ttu-id="e154e-130">ライトの利用状況が変化したら通知されるよう登録する</span><span class="sxs-lookup"><span data-stu-id="e154e-130">Register to be notified if the lamp availability changes</span></span>

<span data-ttu-id="e154e-131">ライトへのアクセス権は、アクセスを要求した最新のアプリに付与されます。</span><span class="sxs-lookup"><span data-stu-id="e154e-131">Lamp access is granted to the most recent app to request access.</span></span> <span data-ttu-id="e154e-132">このため、別のアプリが起動され、現在のアプリで使用中のライト リソースが要求された場合は、別のアプリからリソースが解放されるまで、現在のアプリではライトを制御できなくなります。</span><span class="sxs-lookup"><span data-stu-id="e154e-132">So, if another app is launched and requests a lamp resource that your app is currently using, your app will no longer be able to control the lamp until the other app has released the resource.</span></span> <span data-ttu-id="e154e-133">ライトの利用状況が変化したときに通知を受け取るには、[**Lamp.AvailabilityChanged**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.availabilitychanged) イベントに対するハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="e154e-133">To receive a notification when the availability of the lamp changes, register a handler for the [**Lamp.AvailabilityChanged**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.availabilitychanged) event.</span></span>

[!code-cs[AvailabilityChanged](./code/Lamp/cs/MainPage.xaml.cs#SnippetAvailabilityChanged)]

<span data-ttu-id="e154e-134">このイベントのハンドラーでは、[**LampAvailabilityChanged.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lampavailabilitychangedeventargs.isavailable) プロパティをチェックして、ライトを使用できるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="e154e-134">In the handler for the event, check the [**LampAvailabilityChanged.IsAvailable**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lampavailabilitychangedeventargs.isavailable) property to determine if the lamp is available.</span></span> <span data-ttu-id="e154e-135">この例では、ライトの利用可能性に基づいて、ライトをオンまたはオフにするトグル スイッチが有効または無効になります。</span><span class="sxs-lookup"><span data-stu-id="e154e-135">In this example, a toggle switch for turning the lamp on and off is enabled or disabled based on the lamp availability.</span></span>

[!code-cs[AvailabilityChangedHandler](./code/Lamp/cs/MainPage.xaml.cs#SnippetAvailabilityChangedHandler)]

## <a name="properly-dispose-of-the-lamp-resource-when-not-in-use"></a><span data-ttu-id="e154e-136">使用していないライト リソースを適切に破棄する</span><span class="sxs-lookup"><span data-stu-id="e154e-136">Properly dispose of the lamp resource when not in use</span></span>

<span data-ttu-id="e154e-137">ライトの使用が終わったら、ライトを無効にして [**Lamp.Close**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.close) を呼び出すことにより、他のアプリがライトにアクセスできるようリソースを解放する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e154e-137">When you are no longer using the lamp, you should disable it and call [**Lamp.Close**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.close) to release the resource and allow other apps to access the lamp.</span></span> <span data-ttu-id="e154e-138">C# を使用している場合、このプロパティは **Dispose** メソッドにマップされています。</span><span class="sxs-lookup"><span data-stu-id="e154e-138">This property is mapped to the **Dispose** method if you are using C#.</span></span> <span data-ttu-id="e154e-139">[  **AvailabilityChanged**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.availabilitychanged) に登録した場合は、ライト リソースを破棄するときにハンドラーの登録を解除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e154e-139">If you registered for the [**AvailabilityChanged**](https://docs.microsoft.com/uwp/api/windows.devices.lights.lamp.availabilitychanged), you should unregister the handler when you dispose of the lamp resource.</span></span> <span data-ttu-id="e154e-140">ライト リソースを破棄するコードの適切な場所は、アプリによって異なります。</span><span class="sxs-lookup"><span data-stu-id="e154e-140">The right place in your code to dispose of the lamp resource depends on your app.</span></span> <span data-ttu-id="e154e-141">ライト アクセスのスコープを単一のページに限定するには、リソースを [**OnNavigatingFrom**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatingfrom) イベントで解放します。</span><span class="sxs-lookup"><span data-stu-id="e154e-141">To scope lamp access to a single page, release the resource in the [**OnNavigatingFrom**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page.onnavigatingfrom) event.</span></span>

[!code-cs[DisposeLamp](./code/Lamp/cs/MainPage.xaml.cs#SnippetDisposeLamp)]

## <a name="related-topics"></a><span data-ttu-id="e154e-142">関連トピック</span><span class="sxs-lookup"><span data-stu-id="e154e-142">Related topics</span></span>
- [<span data-ttu-id="e154e-143">メディア再生</span><span class="sxs-lookup"><span data-stu-id="e154e-143">Media playback</span></span>](media-playback.md)

 




