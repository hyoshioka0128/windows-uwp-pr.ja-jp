---
ms.assetid: 3b75d881-bdcf-402b-a330-23cd29d68e53
description: この記事では、オーディオ デバイスに関連する DeviceInformation プロパティを示します。
title: オーディオ デバイス情報プロパティ
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 97b6bd0c3567c00902a9528d54e6417f41ac66ed
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66359095"
---
# <a name="audio-device-information-properties"></a><span data-ttu-id="edf0f-104">オーディオ デバイス情報プロパティ</span><span class="sxs-lookup"><span data-stu-id="edf0f-104">Audio device information properties</span></span>

<span data-ttu-id="edf0f-105">この記事では、オーディオ デバイスに関連するデバイス情報プロパティを示します。</span><span class="sxs-lookup"><span data-stu-id="edf0f-105">This article lists the device information properties related to audio devices.</span></span> <span data-ttu-id="edf0f-106">Windows では、ハードウェア デバイスにはそれぞれ [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) プロパティが関連付けられており、デバイスについての特定の情報が必要な場合やデバイス セレクターを作成する場合に使うことができる、デバイスに関する詳細情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="edf0f-106">On Windows, each hardware device has associated [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) properties providing detailed information about a device that you can use when you need specific information about the device or when you are building a device selector.</span></span> <span data-ttu-id="edf0f-107">Windows でのデバイスの列挙に関する一般的な情報については、「[デバイスの列挙](../devices-sensors/enumerate-devices.md)」と「[デバイス情報プロパティ](../devices-sensors/device-information-properties.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="edf0f-107">For general information about enumerating devices on Windows, see [Enumerate devices](../devices-sensors/enumerate-devices.md) and [Device information properties](../devices-sensors/device-information-properties.md).</span></span>


|<span data-ttu-id="edf0f-108">名前</span><span class="sxs-lookup"><span data-stu-id="edf0f-108">Name</span></span>|<span data-ttu-id="edf0f-109">種類</span><span class="sxs-lookup"><span data-stu-id="edf0f-109">Type</span></span>|<span data-ttu-id="edf0f-110">説明</span><span class="sxs-lookup"><span data-stu-id="edf0f-110">Description</span></span>|
|------------------------------------------------------------|------------|------------------------------------------------------|
|<span data-ttu-id="edf0f-111">**System.Devices.AudioDevice.Microphone.SensitivityInDbfs**</span><span class="sxs-lookup"><span data-stu-id="edf0f-111">**System.Devices.AudioDevice.Microphone.SensitivityInDbfs**</span></span>|<span data-ttu-id="edf0f-112">Double</span><span class="sxs-lookup"><span data-stu-id="edf0f-112">Double</span></span>|<span data-ttu-id="edf0f-113">フルスケール (dBFS) 単位を基準としてマイクの感度を指定します。</span><span class="sxs-lookup"><span data-stu-id="edf0f-113">Specifies the microphone sensitivity in decibels relative to full scale (dBFS) units.</span></span>|
|<span data-ttu-id="edf0f-114">**System.Devices.AudioDevice.Microphone.SignalToNoiseRatioInDb**</span><span class="sxs-lookup"><span data-stu-id="edf0f-114">**System.Devices.AudioDevice.Microphone.SignalToNoiseRatioInDb**</span></span>|<span data-ttu-id="edf0f-115">Double</span><span class="sxs-lookup"><span data-stu-id="edf0f-115">Double</span></span>|<span data-ttu-id="edf0f-116">デシベル (dB) 単位で測定されたマイクの信号雑音比 (SNR) を指定します。</span><span class="sxs-lookup"><span data-stu-id="edf0f-116">Specifies the microphone signal to noise ratio (SNR) measured in decibel (dB) units.</span></span>|
|<span data-ttu-id="edf0f-117">**System.Devices.AudioDevice.SpeechProcessingSupported**</span><span class="sxs-lookup"><span data-stu-id="edf0f-117">**System.Devices.AudioDevice.SpeechProcessingSupported**</span></span>|<span data-ttu-id="edf0f-118">ブール値</span><span class="sxs-lookup"><span data-stu-id="edf0f-118">Boolean</span></span>|<span data-ttu-id="edf0f-119">オーディオ デバイスが、音声処理をサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="edf0f-119">Indicates whether the audio device supports speech processing.</span></span>|
|<span data-ttu-id="edf0f-120">**System.Devices.AudioDevice.RawProcessingSupported**</span><span class="sxs-lookup"><span data-stu-id="edf0f-120">**System.Devices.AudioDevice.RawProcessingSupported**</span></span>|<span data-ttu-id="edf0f-121">ブール値</span><span class="sxs-lookup"><span data-stu-id="edf0f-121">Boolean</span></span>|<span data-ttu-id="edf0f-122">オーディオ デバイスが、raw 処理をサポートするかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="edf0f-122">Indicates whether the audio device supports raw processing.</span></span>|
|<span data-ttu-id="edf0f-123">**System.Devices.MicrophoneArray.Geometry**</span><span class="sxs-lookup"><span data-stu-id="edf0f-123">**System.Devices.MicrophoneArray.Geometry**</span></span>|<span data-ttu-id="edf0f-124">unsigned char[]</span><span class="sxs-lookup"><span data-stu-id="edf0f-124">unsigned char[]</span></span>|<span data-ttu-id="edf0f-125">マイク配列のジオメトリ データです。</span><span class="sxs-lookup"><span data-stu-id="edf0f-125">Geometry data for a microphone array.</span></span>|

## <a name="related-topics"></a><span data-ttu-id="edf0f-126">関連トピック</span><span class="sxs-lookup"><span data-stu-id="edf0f-126">Related topics</span></span>

* [<span data-ttu-id="edf0f-127">デバイスの列挙</span><span class="sxs-lookup"><span data-stu-id="edf0f-127">Enumerate devices</span></span>](../devices-sensors/enumerate-devices.md)
* [<span data-ttu-id="edf0f-128">デバイス情報のプロパティ</span><span class="sxs-lookup"><span data-stu-id="edf0f-128">Device information properties</span></span>](../devices-sensors/device-information-properties.md)
* [<span data-ttu-id="edf0f-129">デバイス セレクターをビルドします。</span><span class="sxs-lookup"><span data-stu-id="edf0f-129">Build a device selector</span></span>](../devices-sensors/build-a-device-selector.md)
* [<span data-ttu-id="edf0f-130">メディア再生</span><span class="sxs-lookup"><span data-stu-id="edf0f-130">Media playback</span></span>](media-playback.md)




