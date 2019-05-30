---
ms.assetid: B4A550E7-1639-4C9A-A229-31E22B1415E7
title: センサーの向き
description: Accelerometer、Gyrometer、Compass、Inclinometer、および OrientationSensor の各クラスのセンサー データは、基準軸によって定義されます。 これらの軸はデバイスの横長の向きで定義され、ユーザーがデバイスの向きを変えると、デバイスと共に回転します。
ms.date: 05/24/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 8e75ab94c6f1c8c4560854fd4f5264c313657ba9
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369889"
---
# <a name="sensor-orientation"></a><span data-ttu-id="bea77-105">センサーの向き</span><span class="sxs-lookup"><span data-stu-id="bea77-105">Sensor orientation</span></span>


<span data-ttu-id="bea77-106">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="bea77-106">**Important APIs**</span></span>

-   [<span data-ttu-id="bea77-107">**Windows.Devices.Sensors**</span><span class="sxs-lookup"><span data-stu-id="bea77-107">**Windows.Devices.Sensors**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors)
-   [<span data-ttu-id="bea77-108">**Windows.Devices.Sensors.Custom**</span><span class="sxs-lookup"><span data-stu-id="bea77-108">**Windows.Devices.Sensors.Custom**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Custom)

<span data-ttu-id="bea77-109">[  **Accelerometer**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Accelerometer)、[**Gyrometer**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Gyrometer)、[**Compass**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Compass)、[**Inclinometer**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Inclinometer)、および [**OrientationSensor**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.OrientationSensor) の各クラスのセンサー データは、基準軸によって定義されます。</span><span class="sxs-lookup"><span data-stu-id="bea77-109">Sensor data from the [**Accelerometer**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Accelerometer), [**Gyrometer**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Gyrometer), [**Compass**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Compass), [**Inclinometer**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.Inclinometer), and [**OrientationSensor**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.OrientationSensor) classes is defined by their reference axes.</span></span> <span data-ttu-id="bea77-110">これらの軸はデバイスの参照フレームで定義され、ユーザーがデバイスの向きを変えると、デバイスと共に回転します。</span><span class="sxs-lookup"><span data-stu-id="bea77-110">These axes are defined by the device's reference frame and rotate with the device as the user turns it.</span></span> <span data-ttu-id="bea77-111">アプリが自動回転をサポートしており、ユーザーがデバイスを回転させたときに連動して向きが変わる場合、センサー データを使う前に回転に合わせて調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bea77-111">If your app supports automatic rotation and reorients itself to accommodate the device as the user rotates it, you must adjust your sensor data for the rotation before using it.</span></span>

## <a name="display-orientation-vs-device-orientation"></a><span data-ttu-id="bea77-112">表示の向きとデバイスの向き</span><span class="sxs-lookup"><span data-stu-id="bea77-112">Display orientation vs device orientation</span></span>

<span data-ttu-id="bea77-113">センサーの基準軸について理解するために、画面の向きとデバイスの向きを区別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bea77-113">In order to understand the reference axes for sensors, you need to distinguish display orientation from device orientation.</span></span> <span data-ttu-id="bea77-114">画面の向きはテキストの向きであり、画面上に画像が表示されます。それに対してデバイスの向きは、デバイスの実際の配置です。</span><span class="sxs-lookup"><span data-stu-id="bea77-114">Display orientation is the direction text and images are displayed on the screen whereas device orientation is the physical positioning of the device.</span></span> <span data-ttu-id="bea77-115">次の図では、デバイスとディスプレイの向きは共に**横向き**です (示されているセンサー軸は、横向き優先デバイスにのみ適用されることに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="bea77-115">In the following picture, both the device and display orientation are in **Landscape** (note that the sensor axes shown are only applicable to landscape-first devices).</span></span>

![画面とデバイスの向きが横向き](images/sensor-orientation-a.PNG)

<span data-ttu-id="bea77-117">次の図では、画面とデバイスの向きが共に **LandscapeFlipped** です。</span><span class="sxs-lookup"><span data-stu-id="bea77-117">The following picture shows both the display and device orientation in **LandscapeFlipped**.</span></span>

![画面とデバイスの向きが LandscapeFlipped](images/sensor-orientation-b.PNG)

<span data-ttu-id="bea77-119">次の図では、画面の向きが Landscape、デバイスの向きが LandscapeFlipped です。</span><span class="sxs-lookup"><span data-stu-id="bea77-119">The next picture shows the display orientation in Landscape while the device orientation is LandscapeFlipped.</span></span>

![画面の向きが Landscape、デバイスの向きが LandscapeFlipped です。](images/sensor-orientation-c.PNG)

<span data-ttu-id="bea77-121">向きの値は、[**DisplayInformation**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Display.DisplayInformation) クラスの [**GetForCurrentView**](https://docs.microsoft.com/uwp/api/windows.graphics.display.displayinformation.getforcurrentview) メソッドと [**CurrentOrientation**](https://docs.microsoft.com/uwp/api/windows.graphics.display.displayinformation.currentorientation) プロパティを使って照会することができます。</span><span class="sxs-lookup"><span data-stu-id="bea77-121">You can query the orientation values through the [**DisplayInformation**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Display.DisplayInformation) class by using the [**GetForCurrentView**](https://docs.microsoft.com/uwp/api/windows.graphics.display.displayinformation.getforcurrentview) method with the [**CurrentOrientation**](https://docs.microsoft.com/uwp/api/windows.graphics.display.displayinformation.currentorientation) property.</span></span> <span data-ttu-id="bea77-122">次に、[**DisplayOrientations**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Display.DisplayOrientations) 列挙値と比較することによってロジックを作成できます。</span><span class="sxs-lookup"><span data-stu-id="bea77-122">Then you can create logic by comparing against the [**DisplayOrientations**](https://docs.microsoft.com/uwp/api/Windows.Graphics.Display.DisplayOrientations) enumeration.</span></span> <span data-ttu-id="bea77-123">サポートするすべての向きについて、その向きへの基準軸の変換をサポートする必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bea77-123">Remember that for every orientation you support, you have to support a conversion of the reference axes to that orientation.</span></span>

## <a name="landscape-first-vs-portrait-first-devices"></a><span data-ttu-id="bea77-124">横向き優先デバイスと縦向き優先デバイス</span><span class="sxs-lookup"><span data-stu-id="bea77-124">Landscape-first vs portrait-first devices</span></span>

<span data-ttu-id="bea77-125">製造元は、横向き優先および縦向き優先のいずれのデバイスも製造します。</span><span class="sxs-lookup"><span data-stu-id="bea77-125">Manufacturers produce both landscape-first and portrait-first devices.</span></span> <span data-ttu-id="bea77-126">参照フレームは、横向き優先デバイス (デスクトップやノート PC など) と縦向き優先デバイス (電話や一部のタブレットなど) によって異なります。</span><span class="sxs-lookup"><span data-stu-id="bea77-126">The reference frame varies between landscape-first devices (like desktops and laptops) and portrait-first devices (like phones and some tablets).</span></span> <span data-ttu-id="bea77-127">次の表は、横向き優先デバイスと縦向き優先デバイスの両方のセンサー軸を示しています。</span><span class="sxs-lookup"><span data-stu-id="bea77-127">The following table shows the sensor axes for both landscape-first and portrait-first devices.</span></span>

| <span data-ttu-id="bea77-128">方向</span><span class="sxs-lookup"><span data-stu-id="bea77-128">Orientation</span></span> | <span data-ttu-id="bea77-129">横向き優先</span><span class="sxs-lookup"><span data-stu-id="bea77-129">Landscape-first</span></span> | <span data-ttu-id="bea77-130">縦向き優先</span><span class="sxs-lookup"><span data-stu-id="bea77-130">Portrait-first</span></span> |
|-------------|-----------------|----------------|
| <span data-ttu-id="bea77-131">**横**</span><span class="sxs-lookup"><span data-stu-id="bea77-131">**Landscape**</span></span> | ![Landscape の向きの横向き優先デバイス](images/sensor-orientation-0.PNG) | ![Landscape の向きの縦向き優先デバイス](images/sensor-orientation-1.PNG) |
| <span data-ttu-id="bea77-134">**縦向き**</span><span class="sxs-lookup"><span data-stu-id="bea77-134">**Portrait**</span></span> | ![Portrait の向きの横向き優先デバイス](images/sensor-orientation-2.PNG) | ![Portrait の向きの縦向き優先デバイス](images/sensor-orientation-3.PNG) |
| <span data-ttu-id="bea77-137">**LandscapeFlipped**</span><span class="sxs-lookup"><span data-stu-id="bea77-137">**LandscapeFlipped**</span></span> | ![LandscapeFlipped の向きの横向き優先デバイス](images/sensor-orientation-4.PNG) | ![LandscapeFlipped の向きの縦向き優先デバイス](images/sensor-orientation-5.PNG) | 
| <span data-ttu-id="bea77-140">**PortraitFlipped**</span><span class="sxs-lookup"><span data-stu-id="bea77-140">**PortraitFlipped**</span></span> | ![PortraitFlipped の向きの横向き優先デバイス](images/sensor-orientation-6.PNG)| ![PortraitFlipped の向きの縦向き優先デバイス](images/sensor-orientation-7.PNG) |

## <a name="devices-broadcasting-display-and-headless-devices"></a><span data-ttu-id="bea77-143">ディスプレイをブロードキャストするデバイスとヘッドレス デバイス</span><span class="sxs-lookup"><span data-stu-id="bea77-143">Devices broadcasting display and headless devices</span></span>

<span data-ttu-id="bea77-144">一部のデバイスは、別のデバイスにディスプレイをブロードキャストする機能を備えています。</span><span class="sxs-lookup"><span data-stu-id="bea77-144">Some devices have the ability to broadcast the display to another device.</span></span> <span data-ttu-id="bea77-145">たとえば、タブレットで、プロジェクターにディスプレイを横方向にブロードキャストできます。</span><span class="sxs-lookup"><span data-stu-id="bea77-145">For example, you could take a tablet and broadcast the display to a projector that will be in landscape orientation.</span></span> <span data-ttu-id="bea77-146">このシナリオでは、デバイスの向きが、ディスプレイを表示しているものではなく、元のデバイスに基づいていることに留意することが重要です。</span><span class="sxs-lookup"><span data-stu-id="bea77-146">In this scenario, it is important to keep in mind that the device orientation is based on the original device, not the one presenting the display.</span></span> <span data-ttu-id="bea77-147">したがって、加速度計は、タブレットのデータを報告します。</span><span class="sxs-lookup"><span data-stu-id="bea77-147">So an accelerometer would report data for the tablet.</span></span>

<span data-ttu-id="bea77-148">さらに、一部のデバイスにはディスプレイがありません。</span><span class="sxs-lookup"><span data-stu-id="bea77-148">Furthermore, some devices do not have a display.</span></span> <span data-ttu-id="bea77-149">これらのデバイスでは、デバイスの既定の向きは縦です。</span><span class="sxs-lookup"><span data-stu-id="bea77-149">With these devices, the default orientation for these devices is portrait.</span></span>

## <a name="display-orientation-and-compass-heading"></a><span data-ttu-id="bea77-150">表示と向きとコンパスの方位</span><span class="sxs-lookup"><span data-stu-id="bea77-150">Display orientation and compass heading</span></span>


<span data-ttu-id="bea77-151">コンパスの方位は基準軸に依存するため、デバイスの向きと共に変化します。</span><span class="sxs-lookup"><span data-stu-id="bea77-151">Compass heading depends upon the reference axes and so it changes with the device orientation.</span></span> <span data-ttu-id="bea77-152">次の表に基づいて補正します (ユーザーが北を向いていると仮定します)。</span><span class="sxs-lookup"><span data-stu-id="bea77-152">You compensate based on the this table (assume the user is facing north).</span></span>

| <span data-ttu-id="bea77-153">表示の向き</span><span class="sxs-lookup"><span data-stu-id="bea77-153">Display orientation</span></span> | <span data-ttu-id="bea77-154">コンパスの方位の基準軸</span><span class="sxs-lookup"><span data-stu-id="bea77-154">Reference axis for compass heading</span></span> | <span data-ttu-id="bea77-155">北を向いている場合の API によるコンパスの方位 (横向き優先)</span><span class="sxs-lookup"><span data-stu-id="bea77-155">API compass heading when facing north (landscape-first)</span></span> | <span data-ttu-id="bea77-156">北を向いている場合の API によるコンパスの方位 (縦向き優先)</span><span class="sxs-lookup"><span data-stu-id="bea77-156">API compass heading when facing north (portrait-first)</span></span> |<span data-ttu-id="bea77-157">コンパスの方位の補正 (横向き優先)</span><span class="sxs-lookup"><span data-stu-id="bea77-157">Compass heading compensation (landscape-first)</span></span> | <span data-ttu-id="bea77-158">コンパスの方位の補正 (縦向き優先)</span><span class="sxs-lookup"><span data-stu-id="bea77-158">Compass heading compensation (portrait-first)</span></span> |
|---------------------|------------------------------------|---------------------------------------------------------|--------------------------------------------------------|------------------------------------------------|-----------------------------------------------|
| <span data-ttu-id="bea77-159">横向き</span><span class="sxs-lookup"><span data-stu-id="bea77-159">Landscape</span></span>           | <span data-ttu-id="bea77-160">-Z</span><span class="sxs-lookup"><span data-stu-id="bea77-160">-Z</span></span> | <span data-ttu-id="bea77-161">0</span><span class="sxs-lookup"><span data-stu-id="bea77-161">0</span></span>   | <span data-ttu-id="bea77-162">270</span><span class="sxs-lookup"><span data-stu-id="bea77-162">270</span></span> | <span data-ttu-id="bea77-163">見出し</span><span class="sxs-lookup"><span data-stu-id="bea77-163">Heading</span></span>               | <span data-ttu-id="bea77-164">(方位 + 90) % 360</span><span class="sxs-lookup"><span data-stu-id="bea77-164">(Heading + 90) % 360</span></span>  |
| <span data-ttu-id="bea77-165">縦向き</span><span class="sxs-lookup"><span data-stu-id="bea77-165">Portrait</span></span>            |  <span data-ttu-id="bea77-166">Y</span><span class="sxs-lookup"><span data-stu-id="bea77-166">Y</span></span> | <span data-ttu-id="bea77-167">90</span><span class="sxs-lookup"><span data-stu-id="bea77-167">90</span></span>  | <span data-ttu-id="bea77-168">0</span><span class="sxs-lookup"><span data-stu-id="bea77-168">0</span></span>   | <span data-ttu-id="bea77-169">(方位 + 270) % 360</span><span class="sxs-lookup"><span data-stu-id="bea77-169">(Heading + 270) % 360</span></span> |  <span data-ttu-id="bea77-170">見出し</span><span class="sxs-lookup"><span data-stu-id="bea77-170">Heading</span></span>              |
| <span data-ttu-id="bea77-171">LandscapeFlipped</span><span class="sxs-lookup"><span data-stu-id="bea77-171">LandscapeFlipped</span></span>    |  <span data-ttu-id="bea77-172">Z</span><span class="sxs-lookup"><span data-stu-id="bea77-172">Z</span></span> | <span data-ttu-id="bea77-173">180</span><span class="sxs-lookup"><span data-stu-id="bea77-173">180</span></span> | <span data-ttu-id="bea77-174">90</span><span class="sxs-lookup"><span data-stu-id="bea77-174">90</span></span>  | <span data-ttu-id="bea77-175">(方位 + 180) % 360</span><span class="sxs-lookup"><span data-stu-id="bea77-175">(Heading + 180) % 360</span></span> | <span data-ttu-id="bea77-176">(方位 + 270) % 360</span><span class="sxs-lookup"><span data-stu-id="bea77-176">(Heading + 270) % 360</span></span> |
| <span data-ttu-id="bea77-177">PortraitFlipped</span><span class="sxs-lookup"><span data-stu-id="bea77-177">PortraitFlipped</span></span>     |  <span data-ttu-id="bea77-178">Y</span><span class="sxs-lookup"><span data-stu-id="bea77-178">Y</span></span> | <span data-ttu-id="bea77-179">270</span><span class="sxs-lookup"><span data-stu-id="bea77-179">270</span></span> | <span data-ttu-id="bea77-180">180</span><span class="sxs-lookup"><span data-stu-id="bea77-180">180</span></span> | <span data-ttu-id="bea77-181">(方位 + 90) % 360</span><span class="sxs-lookup"><span data-stu-id="bea77-181">(Heading + 90) % 360</span></span>  | <span data-ttu-id="bea77-182">(方位 + 180) % 360</span><span class="sxs-lookup"><span data-stu-id="bea77-182">(Heading + 180) % 360</span></span> |

<span data-ttu-id="bea77-183">正確に方位を表示するために、表に示されているようにコンパスの方位を修正します。</span><span class="sxs-lookup"><span data-stu-id="bea77-183">Modify the compass heading as shown in the table in order to correctly display the heading.</span></span> <span data-ttu-id="bea77-184">次のコード スニペットは、この方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="bea77-184">The following code snippet demonstrates how to do this.</span></span>

```csharp
private void ReadingChanged(object sender, CompassReadingChangedEventArgs e)
{
    double heading = e.Reading.HeadingMagneticNorth;        
    double displayOffset;
    
    // Calculate the compass heading offset based on
    // the current display orientation.
    DisplayInformation displayInfo = DisplayInformation.GetForCurrentView();
    
    switch (displayInfo.CurrentOrientation) 
    { 
        case DisplayOrientations.Landscape: 
            displayOffset = 0; 
            break;
        case DisplayOrientations.Portrait: 
            displayOffset = 270; 
            break; 
        case DisplayOrientations.LandscapeFlipped: 
            displayOffset = 180; 
            break; 
        case DisplayOrientations.PortraitFlipped: 
            displayOffset = 90; 
            break; 
     } 
    

    double displayCompensatedHeading = (heading + displayOffset) % 360;
    
    // Update the UI...
}
```

## <a name="display-orientation-with-the-accelerometer-and-gyrometer"></a><span data-ttu-id="bea77-185">加速度計とジャイロメーターでの表示の向き</span><span class="sxs-lookup"><span data-stu-id="bea77-185">Display orientation with the accelerometer and gyrometer</span></span>

<span data-ttu-id="bea77-186">表示の向きに合わせた加速度計とジャイロメーターのデータの変換を、次の表に示します。</span><span class="sxs-lookup"><span data-stu-id="bea77-186">This table converts accelerometer and gyrometer data for display orientation.</span></span>

| <span data-ttu-id="bea77-187">基準軸</span><span class="sxs-lookup"><span data-stu-id="bea77-187">Reference axes</span></span>        |  <span data-ttu-id="bea77-188">x</span><span class="sxs-lookup"><span data-stu-id="bea77-188">X</span></span> |  <span data-ttu-id="bea77-189">Y</span><span class="sxs-lookup"><span data-stu-id="bea77-189">Y</span></span> | <span data-ttu-id="bea77-190">Z</span><span class="sxs-lookup"><span data-stu-id="bea77-190">Z</span></span> |
|-----------------------|----|----|---|
| <span data-ttu-id="bea77-191">**横**</span><span class="sxs-lookup"><span data-stu-id="bea77-191">**Landscape**</span></span>         |  <span data-ttu-id="bea77-192">x</span><span class="sxs-lookup"><span data-stu-id="bea77-192">X</span></span> |  <span data-ttu-id="bea77-193">Y</span><span class="sxs-lookup"><span data-stu-id="bea77-193">Y</span></span> | <span data-ttu-id="bea77-194">Z</span><span class="sxs-lookup"><span data-stu-id="bea77-194">Z</span></span> |
| <span data-ttu-id="bea77-195">**縦向き**</span><span class="sxs-lookup"><span data-stu-id="bea77-195">**Portrait**</span></span>          |  <span data-ttu-id="bea77-196">Y</span><span class="sxs-lookup"><span data-stu-id="bea77-196">Y</span></span> | <span data-ttu-id="bea77-197">-X</span><span class="sxs-lookup"><span data-stu-id="bea77-197">-X</span></span> | <span data-ttu-id="bea77-198">Z</span><span class="sxs-lookup"><span data-stu-id="bea77-198">Z</span></span> |
| <span data-ttu-id="bea77-199">**LandscapeFlipped**</span><span class="sxs-lookup"><span data-stu-id="bea77-199">**LandscapeFlipped**</span></span>  | <span data-ttu-id="bea77-200">-X</span><span class="sxs-lookup"><span data-stu-id="bea77-200">-X</span></span> | <span data-ttu-id="bea77-201">-Y</span><span class="sxs-lookup"><span data-stu-id="bea77-201">-Y</span></span> | <span data-ttu-id="bea77-202">Z</span><span class="sxs-lookup"><span data-stu-id="bea77-202">Z</span></span> |
| <span data-ttu-id="bea77-203">**PortraitFlipped**</span><span class="sxs-lookup"><span data-stu-id="bea77-203">**PortraitFlipped**</span></span>   | <span data-ttu-id="bea77-204">-Y</span><span class="sxs-lookup"><span data-stu-id="bea77-204">-Y</span></span> |  <span data-ttu-id="bea77-205">x</span><span class="sxs-lookup"><span data-stu-id="bea77-205">X</span></span> | <span data-ttu-id="bea77-206">Z</span><span class="sxs-lookup"><span data-stu-id="bea77-206">Z</span></span> |

<span data-ttu-id="bea77-207">ジャイロメーターにこれらの変換を適用するコード例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="bea77-207">The following code example applies these conversions to the gyrometer.</span></span>

```csharp
private void ReadingChanged(object sender, GyrometerReadingChangedEventArgs e)
{
    double x_Axis;
    double y_Axis;
    double z_Axis;

    GyrometerReading reading = e.Reading;  
    
    // Calculate the gyrometer axes based on
    // the current display orientation.
    DisplayInformation displayInfo = DisplayInformation.GetForCurrentView();
    switch (displayInfo.CurrentOrientation) 
    { 
        case DisplayOrientations.Landscape: 
            x_Axis = reading.AngularVelocityX;
            y_Axis = reading.AngularVelocityY;
            z_Axis = reading.AngularVelocityZ;
            break;
        case DisplayOrientations.Portrait: 
            x_Axis = reading.AngularVelocityY;
            y_Axis = -1 * reading.AngularVelocityX;
            z_Axis = reading.AngularVelocityZ;
            break; 
        case DisplayOrientations.LandscapeFlipped: 
            x_Axis = -1 * reading.AngularVelocityX;
            y_Axis = -1 * reading.AngularVelocityY;
            z_Axis = reading.AngularVelocityZ;
            break; 
        case DisplayOrientations.PortraitFlipped: 
            x_Axis = -1 * reading.AngularVelocityY;
            y_Axis = reading.AngularVelocityX;
            z_Axis = reading.AngularVelocityZ;
            break; 
     } 
    
    
    // Update the UI...
}
```

## <a name="display-orientation-and-device-orientation"></a><span data-ttu-id="bea77-208">表示の向きとデバイスの向き</span><span class="sxs-lookup"><span data-stu-id="bea77-208">Display orientation and device orientation</span></span>

<span data-ttu-id="bea77-209">[  **OrientationSensor**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.OrientationSensor) データは別の方法で変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bea77-209">The [**OrientationSensor**](https://docs.microsoft.com/uwp/api/Windows.Devices.Sensors.OrientationSensor) data must be changed in a different way.</span></span> <span data-ttu-id="bea77-210">複数の向きとして Z 軸に対する反時計回りの回転を考えてみます。この場合、ユーザーの向きを元に戻すには、回転を逆にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bea77-210">Think of these different orientations as rotations counterclockwise to the Z axis, so we need to reverse the rotation to get back the user’s orientation.</span></span> <span data-ttu-id="bea77-211">四元数データの場合、オイラーの公式を使って、基準四元数により回転を定義できます。また、基準回転マトリックスを使うこともできます。</span><span class="sxs-lookup"><span data-stu-id="bea77-211">For quaternion data, we can use Euler’s formula to define a rotation with a reference quaternion, and we can also use a reference rotation matrix.</span></span>

![オイラーの公式](images/eulers-formula.png)

<span data-ttu-id="bea77-213">必要な相対的な向きを得るには、基準オブジェクトと絶対オブジェクトを乗算します。</span><span class="sxs-lookup"><span data-stu-id="bea77-213">To get the relative orientation you want, multiply the reference object against the absolute object.</span></span> <span data-ttu-id="bea77-214">この演算は非可換であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="bea77-214">Note that this math is not commutative.</span></span>

![基準オブジェクトと絶対オブジェクトの乗算](images/orientation-formula.png)

<span data-ttu-id="bea77-216">前の式では、センサー データによって絶対オブジェクトが返されます。</span><span class="sxs-lookup"><span data-stu-id="bea77-216">In the preceding expression, the absolute object is returned by the sensor data.</span></span>


| <span data-ttu-id="bea77-217">表示の向き</span><span class="sxs-lookup"><span data-stu-id="bea77-217">Display orientation</span></span>  | <span data-ttu-id="bea77-218">Z 軸を中心とする反時計回りの回転</span><span class="sxs-lookup"><span data-stu-id="bea77-218">Counterclockwise rotation around Z</span></span> | <span data-ttu-id="bea77-219">基準四元数 (逆回転)</span><span class="sxs-lookup"><span data-stu-id="bea77-219">Reference quaternion (reverse rotation)</span></span> | <span data-ttu-id="bea77-220">基準回転マトリックス (逆回転)</span><span class="sxs-lookup"><span data-stu-id="bea77-220">Reference rotation matrix (reverse rotation)</span></span> | 
|----------------------|------------------------------------|-----------------------------------------|----------------------------------------------|
| <span data-ttu-id="bea77-221">**横**</span><span class="sxs-lookup"><span data-stu-id="bea77-221">**Landscape**</span></span>        | <span data-ttu-id="bea77-222">0</span><span class="sxs-lookup"><span data-stu-id="bea77-222">0</span></span>                                  | <span data-ttu-id="bea77-223">1 + 0i + 0j + 0k</span><span class="sxs-lookup"><span data-stu-id="bea77-223">1 + 0i + 0j + 0k</span></span>                        | <span data-ttu-id="bea77-224">\[1 0 0</span><span class="sxs-lookup"><span data-stu-id="bea77-224">\[1 0 0</span></span><br/> <span data-ttu-id="bea77-225">0 1 0</span><span class="sxs-lookup"><span data-stu-id="bea77-225">0 1 0</span></span><br/> <span data-ttu-id="bea77-226">0 0 1\]</span><span class="sxs-lookup"><span data-stu-id="bea77-226">0 0 1\]</span></span>               |
| <span data-ttu-id="bea77-227">**縦向き**</span><span class="sxs-lookup"><span data-stu-id="bea77-227">**Portrait**</span></span>         | <span data-ttu-id="bea77-228">90</span><span class="sxs-lookup"><span data-stu-id="bea77-228">90</span></span>                                 | <span data-ttu-id="bea77-229">cos(-45⁰) + (i + j + k)\*sin(-45⁰)</span><span class="sxs-lookup"><span data-stu-id="bea77-229">cos(-45⁰) + (i + j + k)\*sin(-45⁰)</span></span>       | <span data-ttu-id="bea77-230">\[0 1 0</span><span class="sxs-lookup"><span data-stu-id="bea77-230">\[0 1 0</span></span><br/><span data-ttu-id="bea77-231">-1 0 0</span><span class="sxs-lookup"><span data-stu-id="bea77-231">-1 0 0</span></span><br/><span data-ttu-id="bea77-232">0 0 1]</span><span class="sxs-lookup"><span data-stu-id="bea77-232">0 0 1]</span></span>              |
| <span data-ttu-id="bea77-233">**LandscapeFlipped**</span><span class="sxs-lookup"><span data-stu-id="bea77-233">**LandscapeFlipped**</span></span> | <span data-ttu-id="bea77-234">180</span><span class="sxs-lookup"><span data-stu-id="bea77-234">180</span></span>                                | <span data-ttu-id="bea77-235">0 - i - j - k</span><span class="sxs-lookup"><span data-stu-id="bea77-235">0 - i - j - k</span></span>                           | <span data-ttu-id="bea77-236">\[1 0 0</span><span class="sxs-lookup"><span data-stu-id="bea77-236">\[1 0 0</span></span><br/> <span data-ttu-id="bea77-237">0 1 0</span><span class="sxs-lookup"><span data-stu-id="bea77-237">0 1 0</span></span><br/> <span data-ttu-id="bea77-238">0 0 1]</span><span class="sxs-lookup"><span data-stu-id="bea77-238">0 0 1]</span></span>               |
| <span data-ttu-id="bea77-239">**PortraitFlipped**</span><span class="sxs-lookup"><span data-stu-id="bea77-239">**PortraitFlipped**</span></span>  | <span data-ttu-id="bea77-240">270</span><span class="sxs-lookup"><span data-stu-id="bea77-240">270</span></span>                                | <span data-ttu-id="bea77-241">cos(-135⁰) + (i + j + k)\*sin(-135⁰)</span><span class="sxs-lookup"><span data-stu-id="bea77-241">cos(-135⁰) + (i + j + k)\*sin(-135⁰)</span></span>     | <span data-ttu-id="bea77-242">\[0 -1 0</span><span class="sxs-lookup"><span data-stu-id="bea77-242">\[0 -1 0</span></span><br/> <span data-ttu-id="bea77-243">1  0 0</span><span class="sxs-lookup"><span data-stu-id="bea77-243">1  0 0</span></span><br/> <span data-ttu-id="bea77-244">0  0 1]</span><span class="sxs-lookup"><span data-stu-id="bea77-244">0  0 1]</span></span>             |

