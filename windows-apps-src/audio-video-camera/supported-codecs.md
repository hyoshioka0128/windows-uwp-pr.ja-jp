---
ms.assetid: 9347AD7C-3A90-4073-BFF4-9E8237398343
description: この記事では、UWP アプリ用のオーディオとビデオのコーデックおよび形式のサポートを示します。
title: サポートされるコーデック
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 92511c1f5b7ad8991900d80d4ec52659d6e74f88
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66361411"
---
# <a name="supported-codecs"></a><span data-ttu-id="71219-104">サポートされるコーデック</span><span class="sxs-lookup"><span data-stu-id="71219-104">Supported codecs</span></span>

<span data-ttu-id="71219-105">この記事では、各デバイス ファミリの既定で、UWP アプリで利用可能なオーディオ、ビデオ、イメージのコーデックと形式を示します。</span><span class="sxs-lookup"><span data-stu-id="71219-105">This article lists the audio, video, and image codec and format availability for UWP apps by default for each device family.</span></span> <span data-ttu-id="71219-106">これらの表では、指定のデバイス ファミリの Windows 10 のインストールに含まれているコーデックを示していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="71219-106">Note that these tables list the codecs that are included with the Windows 10 installation for the specified device family.</span></span> <span data-ttu-id="71219-107">ユーザーやアプリが、利用可能な追加のコーデックをインストールする場合があります。</span><span class="sxs-lookup"><span data-stu-id="71219-107">Users and apps can install additional codecs that may be available to use.</span></span> <span data-ttu-id="71219-108">実行時に、特定のデバイスで現在利用可能なコーデックのセットを照会できます。</span><span class="sxs-lookup"><span data-stu-id="71219-108">You can query at runtime for the set of codecs that are currently available for a specific device.</span></span> <span data-ttu-id="71219-109">詳しくは、「[デバイスにインストールされているコーデックの照会](codec-query.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="71219-109">For more information, see [Query for codecs installed on a device](codec-query.md).</span></span>

<span data-ttu-id="71219-110">以下の表では、"D" はデコーダーのサポートを示し、"E" はエンコーダーのサポートを示します。</span><span class="sxs-lookup"><span data-stu-id="71219-110">In the tables below "D" indicates decoder support and "E" indicates encoder support.</span></span>

## <a name="audio-codec--format-support"></a><span data-ttu-id="71219-111">オーディオのコーデックおよび形式のサポート</span><span class="sxs-lookup"><span data-stu-id="71219-111">Audio codec & format support</span></span>

<span data-ttu-id="71219-112">次の表は、各デバイス ファミリのオーディオのコーデックと形式のサポートを示しています。</span><span class="sxs-lookup"><span data-stu-id="71219-112">The following tables show the audio codec and format support for each device family.</span></span>

> [!NOTE] 
> <span data-ttu-id="71219-113">AMR-NB のサポートが示されている場合、Server SKU ではこのコーデックがサポートされません。</span><span class="sxs-lookup"><span data-stu-id="71219-113">Where AMR-NB support is indicated, this codec is not supported on Server SKUs.</span></span>

 

### <a name="desktop"></a><span data-ttu-id="71219-114">Desktop</span><span class="sxs-lookup"><span data-stu-id="71219-114">Desktop</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-115">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-115">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-116">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-116">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-117">MPEG-3</span><span class="sxs-lookup"><span data-stu-id="71219-117">MPEG-3</span></span></th>
<th align="left"><span data-ttu-id="71219-118">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-118">MPEG-2</span></span></th>
<th align="left"><span data-ttu-id="71219-119">ADTS</span><span class="sxs-lookup"><span data-stu-id="71219-119">ADTS</span></span></th>
<th align="left"><span data-ttu-id="71219-120">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-120">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-121">RIFF</span><span class="sxs-lookup"><span data-stu-id="71219-121">RIFF</span></span></th>
<th align="left"><span data-ttu-id="71219-122">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-122">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-123">AC-3</span><span class="sxs-lookup"><span data-stu-id="71219-123">AC-3</span></span></th>
<th align="left"><span data-ttu-id="71219-124">AMR</span><span class="sxs-lookup"><span data-stu-id="71219-124">AMR</span></span></th>
<th align="left"><span data-ttu-id="71219-125">3GP</span><span class="sxs-lookup"><span data-stu-id="71219-125">3GP</span></span></th>
<th align="left"><span data-ttu-id="71219-126">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-126">FLAC</span></span></th>
<th align="left"><span data-ttu-id="71219-127">WAV</span><span class="sxs-lookup"><span data-stu-id="71219-127">WAV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-128">HE-AAC v1/AAC+</span><span class="sxs-lookup"><span data-stu-id="71219-128">HE-AAC v1 / AAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-129">D</span><span class="sxs-lookup"><span data-stu-id="71219-129">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-130">D</span><span class="sxs-lookup"><span data-stu-id="71219-130">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-131">HE-AAC v2/eAAC+</span><span class="sxs-lookup"><span data-stu-id="71219-131">HE-AAC v2 / eAAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-132">D</span><span class="sxs-lookup"><span data-stu-id="71219-132">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-133">D</span><span class="sxs-lookup"><span data-stu-id="71219-133">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-134">AAC-LC</span><span class="sxs-lookup"><span data-stu-id="71219-134">AAC-LC</span></span></td>
<td align="left"><span data-ttu-id="71219-135">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-135">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-136">D</span><span class="sxs-lookup"><span data-stu-id="71219-136">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-137">AC3</span><span class="sxs-lookup"><span data-stu-id="71219-137">AC3</span></span></td>
<td align="left"><span data-ttu-id="71219-138">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-138">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-139">D</span><span class="sxs-lookup"><span data-stu-id="71219-139">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-140">D</span><span class="sxs-lookup"><span data-stu-id="71219-140">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-141">EAC3/EC3</span><span class="sxs-lookup"><span data-stu-id="71219-141">EAC3 / EC3</span></span></td>
<td align="left"><span data-ttu-id="71219-142">D</span><span class="sxs-lookup"><span data-stu-id="71219-142">D</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-143">D</span><span class="sxs-lookup"><span data-stu-id="71219-143">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-144">D</span><span class="sxs-lookup"><span data-stu-id="71219-144">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-145">ALAC</span><span class="sxs-lookup"><span data-stu-id="71219-145">ALAC</span></span></td>
<td align="left"><span data-ttu-id="71219-146">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-146">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-147">AMR-NB</span><span class="sxs-lookup"><span data-stu-id="71219-147">AMR-NB</span></span></td>
<td align="left"><span data-ttu-id="71219-148">D</span><span class="sxs-lookup"><span data-stu-id="71219-148">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-149">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-149">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-150">D</span><span class="sxs-lookup"><span data-stu-id="71219-150">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-151">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-151">FLAC</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-152">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-152">D/E</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-153">G.711 (A-Law、µ-law)</span><span class="sxs-lookup"><span data-stu-id="71219-153">G.711 (A-Law, µ-law)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-154">D</span><span class="sxs-lookup"><span data-stu-id="71219-154">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-155">GSM 6.10</span><span class="sxs-lookup"><span data-stu-id="71219-155">GSM 6.10</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-156">D</span><span class="sxs-lookup"><span data-stu-id="71219-156">D</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-157">IMA ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-157">IMA ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-158">D</span><span class="sxs-lookup"><span data-stu-id="71219-158">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-159">LPCM</span><span class="sxs-lookup"><span data-stu-id="71219-159">LPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-160">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-160">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-161">MP3</span><span class="sxs-lookup"><span data-stu-id="71219-161">MP3</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-162">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-162">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-163">MPEG-1/2</span><span class="sxs-lookup"><span data-stu-id="71219-163">MPEG-1/2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-164">D</span><span class="sxs-lookup"><span data-stu-id="71219-164">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-165">MS ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-165">MS ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-166">D</span><span class="sxs-lookup"><span data-stu-id="71219-166">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-167">WMA 1/2/3</span><span class="sxs-lookup"><span data-stu-id="71219-167">WMA 1/2/3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-168">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-168">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-169">WMA Pro</span><span class="sxs-lookup"><span data-stu-id="71219-169">WMA Pro</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-170">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-170">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-171">WMA Voice</span><span class="sxs-lookup"><span data-stu-id="71219-171">WMA Voice</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-172">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-172">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="mobile"></a><span data-ttu-id="71219-173">モバイル</span><span class="sxs-lookup"><span data-stu-id="71219-173">Mobile</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-174">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-174">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-175">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-175">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-176">MPEG-3</span><span class="sxs-lookup"><span data-stu-id="71219-176">MPEG-3</span></span></th>
<th align="left"><span data-ttu-id="71219-177">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-177">MPEG-2</span></span></th>
<th align="left"><span data-ttu-id="71219-178">ADTS</span><span class="sxs-lookup"><span data-stu-id="71219-178">ADTS</span></span></th>
<th align="left"><span data-ttu-id="71219-179">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-179">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-180">RIFF</span><span class="sxs-lookup"><span data-stu-id="71219-180">RIFF</span></span></th>
<th align="left"><span data-ttu-id="71219-181">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-181">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-182">AC-3</span><span class="sxs-lookup"><span data-stu-id="71219-182">AC-3</span></span></th>
<th align="left"><span data-ttu-id="71219-183">AMR</span><span class="sxs-lookup"><span data-stu-id="71219-183">AMR</span></span></th>
<th align="left"><span data-ttu-id="71219-184">3GP</span><span class="sxs-lookup"><span data-stu-id="71219-184">3GP</span></span></th>
<th align="left"><span data-ttu-id="71219-185">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-185">FLAC</span></span></th>
<th align="left"><span data-ttu-id="71219-186">WAV</span><span class="sxs-lookup"><span data-stu-id="71219-186">WAV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-187">HE-AAC v1/AAC+</span><span class="sxs-lookup"><span data-stu-id="71219-187">HE-AAC v1 / AAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-188">D</span><span class="sxs-lookup"><span data-stu-id="71219-188">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-189">D</span><span class="sxs-lookup"><span data-stu-id="71219-189">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-190">HE-AAC v2/eAAC+</span><span class="sxs-lookup"><span data-stu-id="71219-190">HE-AAC v2 / eAAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-191">D</span><span class="sxs-lookup"><span data-stu-id="71219-191">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-192">D</span><span class="sxs-lookup"><span data-stu-id="71219-192">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-193">AAC-LC</span><span class="sxs-lookup"><span data-stu-id="71219-193">AAC-LC</span></span></td>
<td align="left"><span data-ttu-id="71219-194">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-194">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-195">D</span><span class="sxs-lookup"><span data-stu-id="71219-195">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-196">AC3</span><span class="sxs-lookup"><span data-stu-id="71219-196">AC3</span></span></td>
<td align="left"><span data-ttu-id="71219-197">D (Lumia Icon、830、930、1520 のみ)</span><span class="sxs-lookup"><span data-stu-id="71219-197">D, Only on Lumia Icon, 830, 930, 1520</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-198">D (Lumia Icon、830、930、1520 のみ)</span><span class="sxs-lookup"><span data-stu-id="71219-198">D, Only on Lumia Icon, 830, 930, 1520</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-199">D (Lumia Icon、830、930、1520 のみ)</span><span class="sxs-lookup"><span data-stu-id="71219-199">D, Only on Lumia Icon, 830, 930, 1520</span></span></td>
<td align="left"><span data-ttu-id="71219-200">D (Lumia Icon、830、930、1520 のみ)</span><span class="sxs-lookup"><span data-stu-id="71219-200">D, Only on Lumia Icon, 830, 930, 1520</span></span></td>
<td align="left"><span data-ttu-id="71219-201">D (Lumia Icon、830、930、1520 のみ)</span><span class="sxs-lookup"><span data-stu-id="71219-201">D, Only on Lumia Icon, 830, 930, 1520</span></span></td>
<td align="left"><span data-ttu-id="71219-202">D (Lumia Icon、830、930、1520 のみ)</span><span class="sxs-lookup"><span data-stu-id="71219-202">D, Only on Lumia Icon, 830, 930, 1520</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-203">EAC3/EC3</span><span class="sxs-lookup"><span data-stu-id="71219-203">EAC3 / EC3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-204">ALAC</span><span class="sxs-lookup"><span data-stu-id="71219-204">ALAC</span></span></td>
<td align="left"><span data-ttu-id="71219-205">D</span><span class="sxs-lookup"><span data-stu-id="71219-205">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-206">AMR-NB</span><span class="sxs-lookup"><span data-stu-id="71219-206">AMR-NB</span></span></td>
<td align="left"><span data-ttu-id="71219-207">D</span><span class="sxs-lookup"><span data-stu-id="71219-207">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-208">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-208">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-209">D</span><span class="sxs-lookup"><span data-stu-id="71219-209">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-210">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-210">FLAC</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-211">D</span><span class="sxs-lookup"><span data-stu-id="71219-211">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-212">G.711 (A-Law、µ-law)</span><span class="sxs-lookup"><span data-stu-id="71219-212">G.711 (A-Law, µ-law)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-213">D</span><span class="sxs-lookup"><span data-stu-id="71219-213">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-214">GSM 6.10</span><span class="sxs-lookup"><span data-stu-id="71219-214">GSM 6.10</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-215">D</span><span class="sxs-lookup"><span data-stu-id="71219-215">D</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-216">IMA ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-216">IMA ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-217">D</span><span class="sxs-lookup"><span data-stu-id="71219-217">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-218">LPCM</span><span class="sxs-lookup"><span data-stu-id="71219-218">LPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-219">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-219">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-220">MP3</span><span class="sxs-lookup"><span data-stu-id="71219-220">MP3</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-221">D</span><span class="sxs-lookup"><span data-stu-id="71219-221">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-222">MPEG-1/2</span><span class="sxs-lookup"><span data-stu-id="71219-222">MPEG-1/2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-223">MS ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-223">MS ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-224">D</span><span class="sxs-lookup"><span data-stu-id="71219-224">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-225">WMA 1/2/3</span><span class="sxs-lookup"><span data-stu-id="71219-225">WMA 1/2/3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-226">D</span><span class="sxs-lookup"><span data-stu-id="71219-226">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-227">WMA Pro</span><span class="sxs-lookup"><span data-stu-id="71219-227">WMA Pro</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-228">D</span><span class="sxs-lookup"><span data-stu-id="71219-228">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-229">WMA Voice</span><span class="sxs-lookup"><span data-stu-id="71219-229">WMA Voice</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="iot-core-x86"></a><span data-ttu-id="71219-230">IoT Core (x86)</span><span class="sxs-lookup"><span data-stu-id="71219-230">IoT Core (x86)</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-231">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-231">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-232">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-232">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-233">MPEG-3</span><span class="sxs-lookup"><span data-stu-id="71219-233">MPEG-3</span></span></th>
<th align="left"><span data-ttu-id="71219-234">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-234">MPEG-2</span></span></th>
<th align="left"><span data-ttu-id="71219-235">ADTS</span><span class="sxs-lookup"><span data-stu-id="71219-235">ADTS</span></span></th>
<th align="left"><span data-ttu-id="71219-236">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-236">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-237">RIFF</span><span class="sxs-lookup"><span data-stu-id="71219-237">RIFF</span></span></th>
<th align="left"><span data-ttu-id="71219-238">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-238">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-239">AC-3</span><span class="sxs-lookup"><span data-stu-id="71219-239">AC-3</span></span></th>
<th align="left"><span data-ttu-id="71219-240">AMR</span><span class="sxs-lookup"><span data-stu-id="71219-240">AMR</span></span></th>
<th align="left"><span data-ttu-id="71219-241">3GP</span><span class="sxs-lookup"><span data-stu-id="71219-241">3GP</span></span></th>
<th align="left"><span data-ttu-id="71219-242">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-242">FLAC</span></span></th>
<th align="left"><span data-ttu-id="71219-243">WAV</span><span class="sxs-lookup"><span data-stu-id="71219-243">WAV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-244">HE-AAC v1/AAC+</span><span class="sxs-lookup"><span data-stu-id="71219-244">HE-AAC v1 / AAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-245">D</span><span class="sxs-lookup"><span data-stu-id="71219-245">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-246">D</span><span class="sxs-lookup"><span data-stu-id="71219-246">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-247">HE-AAC v2/eAAC+</span><span class="sxs-lookup"><span data-stu-id="71219-247">HE-AAC v2 / eAAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-248">D</span><span class="sxs-lookup"><span data-stu-id="71219-248">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-249">D</span><span class="sxs-lookup"><span data-stu-id="71219-249">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-250">AAC-LC</span><span class="sxs-lookup"><span data-stu-id="71219-250">AAC-LC</span></span></td>
<td align="left"><span data-ttu-id="71219-251">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-251">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-252">D</span><span class="sxs-lookup"><span data-stu-id="71219-252">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-253">AC3</span><span class="sxs-lookup"><span data-stu-id="71219-253">AC3</span></span></td>
<td align="left"><span data-ttu-id="71219-254">D</span><span class="sxs-lookup"><span data-stu-id="71219-254">D</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-255">D</span><span class="sxs-lookup"><span data-stu-id="71219-255">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-256">D</span><span class="sxs-lookup"><span data-stu-id="71219-256">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-257">EAC3/EC3</span><span class="sxs-lookup"><span data-stu-id="71219-257">EAC3 / EC3</span></span></td>
<td align="left"><span data-ttu-id="71219-258">D</span><span class="sxs-lookup"><span data-stu-id="71219-258">D</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-259">D</span><span class="sxs-lookup"><span data-stu-id="71219-259">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-260">D</span><span class="sxs-lookup"><span data-stu-id="71219-260">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-261">ALAC</span><span class="sxs-lookup"><span data-stu-id="71219-261">ALAC</span></span></td>
<td align="left"><span data-ttu-id="71219-262">D</span><span class="sxs-lookup"><span data-stu-id="71219-262">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-263">AMR-NB</span><span class="sxs-lookup"><span data-stu-id="71219-263">AMR-NB</span></span></td>
<td align="left"><span data-ttu-id="71219-264">D</span><span class="sxs-lookup"><span data-stu-id="71219-264">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-265">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-265">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-266">D</span><span class="sxs-lookup"><span data-stu-id="71219-266">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-267">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-267">FLAC</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-268">D</span><span class="sxs-lookup"><span data-stu-id="71219-268">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-269">G.711 (A-Law、µ-law)</span><span class="sxs-lookup"><span data-stu-id="71219-269">G.711 (A-Law, µ-law)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-270">D</span><span class="sxs-lookup"><span data-stu-id="71219-270">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-271">GSM 6.10</span><span class="sxs-lookup"><span data-stu-id="71219-271">GSM 6.10</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-272">D</span><span class="sxs-lookup"><span data-stu-id="71219-272">D</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-273">IMA ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-273">IMA ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-274">D</span><span class="sxs-lookup"><span data-stu-id="71219-274">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-275">LPCM</span><span class="sxs-lookup"><span data-stu-id="71219-275">LPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-276">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-276">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-277">MP3</span><span class="sxs-lookup"><span data-stu-id="71219-277">MP3</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-278">D</span><span class="sxs-lookup"><span data-stu-id="71219-278">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-279">MPEG-1/2</span><span class="sxs-lookup"><span data-stu-id="71219-279">MPEG-1/2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-280">D</span><span class="sxs-lookup"><span data-stu-id="71219-280">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-281">MS ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-281">MS ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-282">D</span><span class="sxs-lookup"><span data-stu-id="71219-282">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-283">WMA 1/2/3</span><span class="sxs-lookup"><span data-stu-id="71219-283">WMA 1/2/3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-284">D</span><span class="sxs-lookup"><span data-stu-id="71219-284">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-285">WMA Pro</span><span class="sxs-lookup"><span data-stu-id="71219-285">WMA Pro</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-286">D</span><span class="sxs-lookup"><span data-stu-id="71219-286">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-287">WMA Voice</span><span class="sxs-lookup"><span data-stu-id="71219-287">WMA Voice</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-288">D</span><span class="sxs-lookup"><span data-stu-id="71219-288">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="iot-core-arm"></a><span data-ttu-id="71219-289">IoT Core (ARM)</span><span class="sxs-lookup"><span data-stu-id="71219-289">IoT Core (ARM)</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-290">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-290">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-291">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-291">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-292">MPEG-3</span><span class="sxs-lookup"><span data-stu-id="71219-292">MPEG-3</span></span></th>
<th align="left"><span data-ttu-id="71219-293">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-293">MPEG-2</span></span></th>
<th align="left"><span data-ttu-id="71219-294">ADTS</span><span class="sxs-lookup"><span data-stu-id="71219-294">ADTS</span></span></th>
<th align="left"><span data-ttu-id="71219-295">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-295">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-296">RIFF</span><span class="sxs-lookup"><span data-stu-id="71219-296">RIFF</span></span></th>
<th align="left"><span data-ttu-id="71219-297">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-297">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-298">AC-3</span><span class="sxs-lookup"><span data-stu-id="71219-298">AC-3</span></span></th>
<th align="left"><span data-ttu-id="71219-299">AMR</span><span class="sxs-lookup"><span data-stu-id="71219-299">AMR</span></span></th>
<th align="left"><span data-ttu-id="71219-300">3GP</span><span class="sxs-lookup"><span data-stu-id="71219-300">3GP</span></span></th>
<th align="left"><span data-ttu-id="71219-301">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-301">FLAC</span></span></th>
<th align="left"><span data-ttu-id="71219-302">WAV</span><span class="sxs-lookup"><span data-stu-id="71219-302">WAV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-303">HE-AAC v1/AAC+</span><span class="sxs-lookup"><span data-stu-id="71219-303">HE-AAC v1 / AAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-304">D</span><span class="sxs-lookup"><span data-stu-id="71219-304">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-305">D</span><span class="sxs-lookup"><span data-stu-id="71219-305">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-306">HE-AAC v2/eAAC+</span><span class="sxs-lookup"><span data-stu-id="71219-306">HE-AAC v2 / eAAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-307">D</span><span class="sxs-lookup"><span data-stu-id="71219-307">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-308">D</span><span class="sxs-lookup"><span data-stu-id="71219-308">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-309">AAC-LC</span><span class="sxs-lookup"><span data-stu-id="71219-309">AAC-LC</span></span></td>
<td align="left"><span data-ttu-id="71219-310">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-310">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-311">D</span><span class="sxs-lookup"><span data-stu-id="71219-311">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-312">AC3</span><span class="sxs-lookup"><span data-stu-id="71219-312">AC3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-313">EAC3/EC3</span><span class="sxs-lookup"><span data-stu-id="71219-313">EAC3 / EC3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-314">ALAC</span><span class="sxs-lookup"><span data-stu-id="71219-314">ALAC</span></span></td>
<td align="left"><span data-ttu-id="71219-315">D</span><span class="sxs-lookup"><span data-stu-id="71219-315">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-316">AMR-NB</span><span class="sxs-lookup"><span data-stu-id="71219-316">AMR-NB</span></span></td>
<td align="left"><span data-ttu-id="71219-317">D</span><span class="sxs-lookup"><span data-stu-id="71219-317">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-318">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-318">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-319">D</span><span class="sxs-lookup"><span data-stu-id="71219-319">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-320">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-320">FLAC</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-321">D</span><span class="sxs-lookup"><span data-stu-id="71219-321">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-322">G.711 (A-Law、µ-law)</span><span class="sxs-lookup"><span data-stu-id="71219-322">G.711 (A-Law, µ-law)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-323">D</span><span class="sxs-lookup"><span data-stu-id="71219-323">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-324">GSM 6.10</span><span class="sxs-lookup"><span data-stu-id="71219-324">GSM 6.10</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-325">D</span><span class="sxs-lookup"><span data-stu-id="71219-325">D</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-326">IMA ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-326">IMA ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-327">D</span><span class="sxs-lookup"><span data-stu-id="71219-327">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-328">LPCM</span><span class="sxs-lookup"><span data-stu-id="71219-328">LPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-329">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-329">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-330">MP3</span><span class="sxs-lookup"><span data-stu-id="71219-330">MP3</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-331">D</span><span class="sxs-lookup"><span data-stu-id="71219-331">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-332">MPEG-1/2</span><span class="sxs-lookup"><span data-stu-id="71219-332">MPEG-1/2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-333">D</span><span class="sxs-lookup"><span data-stu-id="71219-333">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-334">MS ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-334">MS ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-335">D</span><span class="sxs-lookup"><span data-stu-id="71219-335">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-336">WMA 1/2/3</span><span class="sxs-lookup"><span data-stu-id="71219-336">WMA 1/2/3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-337">D</span><span class="sxs-lookup"><span data-stu-id="71219-337">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-338">WMA Pro</span><span class="sxs-lookup"><span data-stu-id="71219-338">WMA Pro</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-339">D</span><span class="sxs-lookup"><span data-stu-id="71219-339">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-340">WMA Voice</span><span class="sxs-lookup"><span data-stu-id="71219-340">WMA Voice</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-341">D</span><span class="sxs-lookup"><span data-stu-id="71219-341">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="xbox"></a><span data-ttu-id="71219-342">XBox</span><span class="sxs-lookup"><span data-stu-id="71219-342">XBox</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-343">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-343">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-344">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-344">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-345">MPEG-3</span><span class="sxs-lookup"><span data-stu-id="71219-345">MPEG-3</span></span></th>
<th align="left"><span data-ttu-id="71219-346">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-346">MPEG-2</span></span></th>
<th align="left"><span data-ttu-id="71219-347">ADTS</span><span class="sxs-lookup"><span data-stu-id="71219-347">ADTS</span></span></th>
<th align="left"><span data-ttu-id="71219-348">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-348">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-349">RIFF</span><span class="sxs-lookup"><span data-stu-id="71219-349">RIFF</span></span></th>
<th align="left"><span data-ttu-id="71219-350">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-350">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-351">AC-3</span><span class="sxs-lookup"><span data-stu-id="71219-351">AC-3</span></span></th>
<th align="left"><span data-ttu-id="71219-352">AMR</span><span class="sxs-lookup"><span data-stu-id="71219-352">AMR</span></span></th>
<th align="left"><span data-ttu-id="71219-353">3GP</span><span class="sxs-lookup"><span data-stu-id="71219-353">3GP</span></span></th>
<th align="left"><span data-ttu-id="71219-354">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-354">FLAC</span></span></th>
<th align="left"><span data-ttu-id="71219-355">WAV</span><span class="sxs-lookup"><span data-stu-id="71219-355">WAV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-356">HE-AAC v1/AAC+</span><span class="sxs-lookup"><span data-stu-id="71219-356">HE-AAC v1 / AAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-357">D</span><span class="sxs-lookup"><span data-stu-id="71219-357">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-358">D</span><span class="sxs-lookup"><span data-stu-id="71219-358">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-359">HE-AAC v2/eAAC+</span><span class="sxs-lookup"><span data-stu-id="71219-359">HE-AAC v2 / eAAC+</span></span></td>
<td align="left"><span data-ttu-id="71219-360">D</span><span class="sxs-lookup"><span data-stu-id="71219-360">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-361">D</span><span class="sxs-lookup"><span data-stu-id="71219-361">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-362">AAC-LC</span><span class="sxs-lookup"><span data-stu-id="71219-362">AAC-LC</span></span></td>
<td align="left"><span data-ttu-id="71219-363">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-363">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-364">D</span><span class="sxs-lookup"><span data-stu-id="71219-364">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-365">AC3</span><span class="sxs-lookup"><span data-stu-id="71219-365">AC3</span></span></td>
<td align="left"><span data-ttu-id="71219-366">D</span><span class="sxs-lookup"><span data-stu-id="71219-366">D</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-367">D</span><span class="sxs-lookup"><span data-stu-id="71219-367">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-368">D</span><span class="sxs-lookup"><span data-stu-id="71219-368">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-369">EAC3/EC3</span><span class="sxs-lookup"><span data-stu-id="71219-369">EAC3 / EC3</span></span></td>
<td align="left"><span data-ttu-id="71219-370">D</span><span class="sxs-lookup"><span data-stu-id="71219-370">D</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-371">D</span><span class="sxs-lookup"><span data-stu-id="71219-371">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-372">D</span><span class="sxs-lookup"><span data-stu-id="71219-372">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-373">ALAC</span><span class="sxs-lookup"><span data-stu-id="71219-373">ALAC</span></span></td>
<td align="left"><span data-ttu-id="71219-374">D</span><span class="sxs-lookup"><span data-stu-id="71219-374">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-375">AMR-NB</span><span class="sxs-lookup"><span data-stu-id="71219-375">AMR-NB</span></span></td>
<td align="left"><span data-ttu-id="71219-376">D</span><span class="sxs-lookup"><span data-stu-id="71219-376">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-377">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-377">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-378">D</span><span class="sxs-lookup"><span data-stu-id="71219-378">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-379">FLAC</span><span class="sxs-lookup"><span data-stu-id="71219-379">FLAC</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-380">D</span><span class="sxs-lookup"><span data-stu-id="71219-380">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-381">G.711 (A-Law、µ-law)</span><span class="sxs-lookup"><span data-stu-id="71219-381">G.711 (A-Law, µ-law)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-382">D</span><span class="sxs-lookup"><span data-stu-id="71219-382">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-383">GSM 6.10</span><span class="sxs-lookup"><span data-stu-id="71219-383">GSM 6.10</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-384">D</span><span class="sxs-lookup"><span data-stu-id="71219-384">D</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-385">IMA ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-385">IMA ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-386">D</span><span class="sxs-lookup"><span data-stu-id="71219-386">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-387">LPCM</span><span class="sxs-lookup"><span data-stu-id="71219-387">LPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-388">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-388">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-389">MP3</span><span class="sxs-lookup"><span data-stu-id="71219-389">MP3</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-390">D</span><span class="sxs-lookup"><span data-stu-id="71219-390">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-391">MPEG-1/2</span><span class="sxs-lookup"><span data-stu-id="71219-391">MPEG-1/2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-392">D</span><span class="sxs-lookup"><span data-stu-id="71219-392">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-393">MS ADPCM</span><span class="sxs-lookup"><span data-stu-id="71219-393">MS ADPCM</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-394">D</span><span class="sxs-lookup"><span data-stu-id="71219-394">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-395">WMA 1/2/3</span><span class="sxs-lookup"><span data-stu-id="71219-395">WMA 1/2/3</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-396">D</span><span class="sxs-lookup"><span data-stu-id="71219-396">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-397">WMA Pro</span><span class="sxs-lookup"><span data-stu-id="71219-397">WMA Pro</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-398">D</span><span class="sxs-lookup"><span data-stu-id="71219-398">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-399">WMA Voice</span><span class="sxs-lookup"><span data-stu-id="71219-399">WMA Voice</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-400">D</span><span class="sxs-lookup"><span data-stu-id="71219-400">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="video-codec--format-support"></a><span data-ttu-id="71219-401">ビデオのコーデックおよび形式のサポート</span><span class="sxs-lookup"><span data-stu-id="71219-401">Video codec & format support</span></span>

<span data-ttu-id="71219-402">次の表は、各デバイス ファミリのビデオのコーデックと形式のサポートを示しています。</span><span class="sxs-lookup"><span data-stu-id="71219-402">The following tables show the video codec and format support for each device family.</span></span>

> [!NOTE] 
> <span data-ttu-id="71219-403">H.265 のサポートが示されている場合、必ずしもデバイス ファミリ内のすべてのデバイスでサポートされるわけではありません。</span><span class="sxs-lookup"><span data-stu-id="71219-403">Where H.265 support is indicated, it is not necessarily supported by all devices within the device family.</span></span>
> <span data-ttu-id="71219-404">MPEG-2/MPEG-1 のサポートが示されている場合、オプションの Microsoft DVD ユニバーサル Windows アプリのインストールでのみサポートされます。</span><span class="sxs-lookup"><span data-stu-id="71219-404">Where MPEG-2/MPEG-1 support is indicated, it is only supported with the installation of the optional Microsoft DVD Universal Windows app.</span></span>

 

### <a name="desktop"></a><span data-ttu-id="71219-405">Desktop</span><span class="sxs-lookup"><span data-stu-id="71219-405">Desktop</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-406">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-406">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-407">FOURCC</span><span class="sxs-lookup"><span data-stu-id="71219-407">FOURCC</span></span></th>
<th align="left"><span data-ttu-id="71219-408">fMP4</span><span class="sxs-lookup"><span data-stu-id="71219-408">fMP4</span></span></th>
<th align="left"><span data-ttu-id="71219-409">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-409">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-410">MPEG-2 PS</span><span class="sxs-lookup"><span data-stu-id="71219-410">MPEG-2 PS</span></span></th>
<th align="left"><span data-ttu-id="71219-411">MPEG-2 TS</span><span class="sxs-lookup"><span data-stu-id="71219-411">MPEG-2 TS</span></span></th>
<th align="left"><span data-ttu-id="71219-412">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-412">MPEG-1</span></span></th>
<th align="left"><span data-ttu-id="71219-413">3GPP</span><span class="sxs-lookup"><span data-stu-id="71219-413">3GPP</span></span></th>
<th align="left"><span data-ttu-id="71219-414">3GPP2</span><span class="sxs-lookup"><span data-stu-id="71219-414">3GPP2</span></span></th>
<th align="left"><span data-ttu-id="71219-415">AVCHD</span><span class="sxs-lookup"><span data-stu-id="71219-415">AVCHD</span></span></th>
<th align="left"><span data-ttu-id="71219-416">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-416">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-417">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-417">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-418">MKV</span><span class="sxs-lookup"><span data-stu-id="71219-418">MKV</span></span></th>
<th align="left"><span data-ttu-id="71219-419">DV</span><span class="sxs-lookup"><span data-stu-id="71219-419">DV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-420">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-420">MPEG-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-421">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-421">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-422">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-422">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-423">D</span><span class="sxs-lookup"><span data-stu-id="71219-423">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-424">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-424">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-425">D</span><span class="sxs-lookup"><span data-stu-id="71219-425">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-426">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-426">MPEG-2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-427">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-427">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-428">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-428">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-429">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-429">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-430">D</span><span class="sxs-lookup"><span data-stu-id="71219-430">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-431">MPEG-4 (Part 2)</span><span class="sxs-lookup"><span data-stu-id="71219-431">MPEG-4 (Part 2)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-432">D</span><span class="sxs-lookup"><span data-stu-id="71219-432">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-433">D</span><span class="sxs-lookup"><span data-stu-id="71219-433">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-434">D</span><span class="sxs-lookup"><span data-stu-id="71219-434">D</span></span></td>
<td align="left"><span data-ttu-id="71219-435">D</span><span class="sxs-lookup"><span data-stu-id="71219-435">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-436">H.265</span><span class="sxs-lookup"><span data-stu-id="71219-436">H.265</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-437">D</span><span class="sxs-lookup"><span data-stu-id="71219-437">D</span></span></td>
<td align="left"><span data-ttu-id="71219-438">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-438">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-439">D</span><span class="sxs-lookup"><span data-stu-id="71219-439">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-440">H.264</span><span class="sxs-lookup"><span data-stu-id="71219-440">H.264</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-441">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-441">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-442">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-442">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-443">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-443">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-444">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-444">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-445">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-445">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-446">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-446">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-447">D</span><span class="sxs-lookup"><span data-stu-id="71219-447">D</span></span></td>
<td align="left"><span data-ttu-id="71219-448">D</span><span class="sxs-lookup"><span data-stu-id="71219-448">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-449">H.263</span><span class="sxs-lookup"><span data-stu-id="71219-449">H.263</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-450">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-450">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-451">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-451">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-452">D</span><span class="sxs-lookup"><span data-stu-id="71219-452">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-453">VC-1</span><span class="sxs-lookup"><span data-stu-id="71219-453">VC-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-454">D</span><span class="sxs-lookup"><span data-stu-id="71219-454">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-455">D</span><span class="sxs-lookup"><span data-stu-id="71219-455">D</span></span></td>
<td align="left"><span data-ttu-id="71219-456">D</span><span class="sxs-lookup"><span data-stu-id="71219-456">D</span></span></td>
<td align="left"><span data-ttu-id="71219-457">D</span><span class="sxs-lookup"><span data-stu-id="71219-457">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-458">WMV7/8/9</span><span class="sxs-lookup"><span data-stu-id="71219-458">WMV7/8/9</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-459">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-459">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-460">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-460">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-461">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-461">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-462">WMV9 Screen</span><span class="sxs-lookup"><span data-stu-id="71219-462">WMV9 Screen</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-463">D</span><span class="sxs-lookup"><span data-stu-id="71219-463">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-464">D</span><span class="sxs-lookup"><span data-stu-id="71219-464">D</span></span></td>
<td align="left"><span data-ttu-id="71219-465">D</span><span class="sxs-lookup"><span data-stu-id="71219-465">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-466">DV</span><span class="sxs-lookup"><span data-stu-id="71219-466">DV</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-467">D</span><span class="sxs-lookup"><span data-stu-id="71219-467">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-468">D</span><span class="sxs-lookup"><span data-stu-id="71219-468">D</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-469">D</span><span class="sxs-lookup"><span data-stu-id="71219-469">D</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-470">モーション JPEG</span><span class="sxs-lookup"><span data-stu-id="71219-470">Motion JPEG</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-471">D</span><span class="sxs-lookup"><span data-stu-id="71219-471">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-472">D</span><span class="sxs-lookup"><span data-stu-id="71219-472">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="mobile"></a><span data-ttu-id="71219-473">モバイル</span><span class="sxs-lookup"><span data-stu-id="71219-473">Mobile</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-474">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-474">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-475">FOURCC</span><span class="sxs-lookup"><span data-stu-id="71219-475">FOURCC</span></span></th>
<th align="left"><span data-ttu-id="71219-476">fMP4</span><span class="sxs-lookup"><span data-stu-id="71219-476">fMP4</span></span></th>
<th align="left"><span data-ttu-id="71219-477">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-477">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-478">MPEG-2 PS</span><span class="sxs-lookup"><span data-stu-id="71219-478">MPEG-2 PS</span></span></th>
<th align="left"><span data-ttu-id="71219-479">MPEG-2 TS</span><span class="sxs-lookup"><span data-stu-id="71219-479">MPEG-2 TS</span></span></th>
<th align="left"><span data-ttu-id="71219-480">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-480">MPEG-1</span></span></th>
<th align="left"><span data-ttu-id="71219-481">3GPP</span><span class="sxs-lookup"><span data-stu-id="71219-481">3GPP</span></span></th>
<th align="left"><span data-ttu-id="71219-482">3GPP2</span><span class="sxs-lookup"><span data-stu-id="71219-482">3GPP2</span></span></th>
<th align="left"><span data-ttu-id="71219-483">AVCHD</span><span class="sxs-lookup"><span data-stu-id="71219-483">AVCHD</span></span></th>
<th align="left"><span data-ttu-id="71219-484">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-484">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-485">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-485">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-486">MKV</span><span class="sxs-lookup"><span data-stu-id="71219-486">MKV</span></span></th>
<th align="left"><span data-ttu-id="71219-487">DV</span><span class="sxs-lookup"><span data-stu-id="71219-487">DV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-488">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-488">MPEG-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-489">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-489">MPEG-2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-490">MPEG-4 (Part 2)</span><span class="sxs-lookup"><span data-stu-id="71219-490">MPEG-4 (Part 2)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-491">D</span><span class="sxs-lookup"><span data-stu-id="71219-491">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-492">D</span><span class="sxs-lookup"><span data-stu-id="71219-492">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-493">D</span><span class="sxs-lookup"><span data-stu-id="71219-493">D</span></span></td>
<td align="left"><span data-ttu-id="71219-494">D</span><span class="sxs-lookup"><span data-stu-id="71219-494">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-495">H.265</span><span class="sxs-lookup"><span data-stu-id="71219-495">H.265</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-496">D</span><span class="sxs-lookup"><span data-stu-id="71219-496">D</span></span></td>
<td align="left"><span data-ttu-id="71219-497">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-497">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-498">D</span><span class="sxs-lookup"><span data-stu-id="71219-498">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-499">H.264</span><span class="sxs-lookup"><span data-stu-id="71219-499">H.264</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-500">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-500">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-501">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-501">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-502">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-502">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-503">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-503">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-504">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-504">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-505">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-505">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-506">D</span><span class="sxs-lookup"><span data-stu-id="71219-506">D</span></span></td>
<td align="left"><span data-ttu-id="71219-507">D</span><span class="sxs-lookup"><span data-stu-id="71219-507">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-508">H.263</span><span class="sxs-lookup"><span data-stu-id="71219-508">H.263</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-509">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-509">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-510">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-510">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-511">D</span><span class="sxs-lookup"><span data-stu-id="71219-511">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-512">VC-1</span><span class="sxs-lookup"><span data-stu-id="71219-512">VC-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-513">D</span><span class="sxs-lookup"><span data-stu-id="71219-513">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-514">D</span><span class="sxs-lookup"><span data-stu-id="71219-514">D</span></span></td>
<td align="left"><span data-ttu-id="71219-515">D</span><span class="sxs-lookup"><span data-stu-id="71219-515">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-516">WMV7/8/9</span><span class="sxs-lookup"><span data-stu-id="71219-516">WMV7/8/9</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-517">WMV9 Screen</span><span class="sxs-lookup"><span data-stu-id="71219-517">WMV9 Screen</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-518">DV</span><span class="sxs-lookup"><span data-stu-id="71219-518">DV</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-519">モーション JPEG</span><span class="sxs-lookup"><span data-stu-id="71219-519">Motion JPEG</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-520">D</span><span class="sxs-lookup"><span data-stu-id="71219-520">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-521">D</span><span class="sxs-lookup"><span data-stu-id="71219-521">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="iot-core-x86"></a><span data-ttu-id="71219-522">IoT Core (x86)</span><span class="sxs-lookup"><span data-stu-id="71219-522">IoT Core (x86)</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-523">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-523">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-524">FOURCC</span><span class="sxs-lookup"><span data-stu-id="71219-524">FOURCC</span></span></th>
<th align="left"><span data-ttu-id="71219-525">fMP4</span><span class="sxs-lookup"><span data-stu-id="71219-525">fMP4</span></span></th>
<th align="left"><span data-ttu-id="71219-526">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-526">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-527">MPEG-2 PS</span><span class="sxs-lookup"><span data-stu-id="71219-527">MPEG-2 PS</span></span></th>
<th align="left"><span data-ttu-id="71219-528">MPEG-2 TS</span><span class="sxs-lookup"><span data-stu-id="71219-528">MPEG-2 TS</span></span></th>
<th align="left"><span data-ttu-id="71219-529">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-529">MPEG-1</span></span></th>
<th align="left"><span data-ttu-id="71219-530">3GPP</span><span class="sxs-lookup"><span data-stu-id="71219-530">3GPP</span></span></th>
<th align="left"><span data-ttu-id="71219-531">3GPP2</span><span class="sxs-lookup"><span data-stu-id="71219-531">3GPP2</span></span></th>
<th align="left"><span data-ttu-id="71219-532">AVCHD</span><span class="sxs-lookup"><span data-stu-id="71219-532">AVCHD</span></span></th>
<th align="left"><span data-ttu-id="71219-533">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-533">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-534">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-534">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-535">MKV</span><span class="sxs-lookup"><span data-stu-id="71219-535">MKV</span></span></th>
<th align="left"><span data-ttu-id="71219-536">DV</span><span class="sxs-lookup"><span data-stu-id="71219-536">DV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-537">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-537">MPEG-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-538">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-538">MPEG-2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-539">MPEG-4 (Part 2)</span><span class="sxs-lookup"><span data-stu-id="71219-539">MPEG-4 (Part 2)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-540">D</span><span class="sxs-lookup"><span data-stu-id="71219-540">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-541">D</span><span class="sxs-lookup"><span data-stu-id="71219-541">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-542">D</span><span class="sxs-lookup"><span data-stu-id="71219-542">D</span></span></td>
<td align="left"><span data-ttu-id="71219-543">D</span><span class="sxs-lookup"><span data-stu-id="71219-543">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-544">H.265</span><span class="sxs-lookup"><span data-stu-id="71219-544">H.265</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-545">D</span><span class="sxs-lookup"><span data-stu-id="71219-545">D</span></span></td>
<td align="left"><span data-ttu-id="71219-546">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-546">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-547">D</span><span class="sxs-lookup"><span data-stu-id="71219-547">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-548">H.264</span><span class="sxs-lookup"><span data-stu-id="71219-548">H.264</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-549">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-549">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-550">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-550">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-551">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-551">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-552">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-552">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-553">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-553">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-554">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-554">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-555">D</span><span class="sxs-lookup"><span data-stu-id="71219-555">D</span></span></td>
<td align="left"><span data-ttu-id="71219-556">D</span><span class="sxs-lookup"><span data-stu-id="71219-556">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-557">H.263</span><span class="sxs-lookup"><span data-stu-id="71219-557">H.263</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-558">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-558">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-559">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-559">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-560">D</span><span class="sxs-lookup"><span data-stu-id="71219-560">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-561">VC-1</span><span class="sxs-lookup"><span data-stu-id="71219-561">VC-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-562">D</span><span class="sxs-lookup"><span data-stu-id="71219-562">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-563">D</span><span class="sxs-lookup"><span data-stu-id="71219-563">D</span></span></td>
<td align="left"><span data-ttu-id="71219-564">D</span><span class="sxs-lookup"><span data-stu-id="71219-564">D</span></span></td>
<td align="left"><span data-ttu-id="71219-565">D</span><span class="sxs-lookup"><span data-stu-id="71219-565">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-566">WMV7/8/9</span><span class="sxs-lookup"><span data-stu-id="71219-566">WMV7/8/9</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-567">D</span><span class="sxs-lookup"><span data-stu-id="71219-567">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-568">D</span><span class="sxs-lookup"><span data-stu-id="71219-568">D</span></span></td>
<td align="left"><span data-ttu-id="71219-569">D</span><span class="sxs-lookup"><span data-stu-id="71219-569">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-570">WMV9 Screen</span><span class="sxs-lookup"><span data-stu-id="71219-570">WMV9 Screen</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-571">D</span><span class="sxs-lookup"><span data-stu-id="71219-571">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-572">D</span><span class="sxs-lookup"><span data-stu-id="71219-572">D</span></span></td>
<td align="left"><span data-ttu-id="71219-573">D</span><span class="sxs-lookup"><span data-stu-id="71219-573">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-574">DV</span><span class="sxs-lookup"><span data-stu-id="71219-574">DV</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-575">モーション JPEG</span><span class="sxs-lookup"><span data-stu-id="71219-575">Motion JPEG</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-576">D</span><span class="sxs-lookup"><span data-stu-id="71219-576">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-577">D</span><span class="sxs-lookup"><span data-stu-id="71219-577">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="iot-arm"></a><span data-ttu-id="71219-578">IoT (ARM)</span><span class="sxs-lookup"><span data-stu-id="71219-578">IoT (ARM)</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-579">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-579">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-580">FOURCC</span><span class="sxs-lookup"><span data-stu-id="71219-580">FOURCC</span></span></th>
<th align="left"><span data-ttu-id="71219-581">fMP4</span><span class="sxs-lookup"><span data-stu-id="71219-581">fMP4</span></span></th>
<th align="left"><span data-ttu-id="71219-582">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-582">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-583">MPEG-2 PS</span><span class="sxs-lookup"><span data-stu-id="71219-583">MPEG-2 PS</span></span></th>
<th align="left"><span data-ttu-id="71219-584">MPEG-2 TS</span><span class="sxs-lookup"><span data-stu-id="71219-584">MPEG-2 TS</span></span></th>
<th align="left"><span data-ttu-id="71219-585">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-585">MPEG-1</span></span></th>
<th align="left"><span data-ttu-id="71219-586">3GPP</span><span class="sxs-lookup"><span data-stu-id="71219-586">3GPP</span></span></th>
<th align="left"><span data-ttu-id="71219-587">3GPP2</span><span class="sxs-lookup"><span data-stu-id="71219-587">3GPP2</span></span></th>
<th align="left"><span data-ttu-id="71219-588">AVCHD</span><span class="sxs-lookup"><span data-stu-id="71219-588">AVCHD</span></span></th>
<th align="left"><span data-ttu-id="71219-589">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-589">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-590">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-590">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-591">MKV</span><span class="sxs-lookup"><span data-stu-id="71219-591">MKV</span></span></th>
<th align="left"><span data-ttu-id="71219-592">DV</span><span class="sxs-lookup"><span data-stu-id="71219-592">DV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-593">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-593">MPEG-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-594">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-594">MPEG-2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-595">MPEG-4 (Part 2)</span><span class="sxs-lookup"><span data-stu-id="71219-595">MPEG-4 (Part 2)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-596">H.265</span><span class="sxs-lookup"><span data-stu-id="71219-596">H.265</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-597">D</span><span class="sxs-lookup"><span data-stu-id="71219-597">D</span></span></td>
<td align="left"><span data-ttu-id="71219-598">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-598">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-599">D</span><span class="sxs-lookup"><span data-stu-id="71219-599">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-600">H.264</span><span class="sxs-lookup"><span data-stu-id="71219-600">H.264</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-601">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-601">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-602">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-602">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-603">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-603">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-604">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-604">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-605">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-605">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-606">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-606">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-607">D</span><span class="sxs-lookup"><span data-stu-id="71219-607">D</span></span></td>
<td align="left"><span data-ttu-id="71219-608">D</span><span class="sxs-lookup"><span data-stu-id="71219-608">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-609">H.263</span><span class="sxs-lookup"><span data-stu-id="71219-609">H.263</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-610">VC-1</span><span class="sxs-lookup"><span data-stu-id="71219-610">VC-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-611">D</span><span class="sxs-lookup"><span data-stu-id="71219-611">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-612">D</span><span class="sxs-lookup"><span data-stu-id="71219-612">D</span></span></td>
<td align="left"><span data-ttu-id="71219-613">D</span><span class="sxs-lookup"><span data-stu-id="71219-613">D</span></span></td>
<td align="left"><span data-ttu-id="71219-614">D</span><span class="sxs-lookup"><span data-stu-id="71219-614">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-615">WMV7/8/9</span><span class="sxs-lookup"><span data-stu-id="71219-615">WMV7/8/9</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-616">D</span><span class="sxs-lookup"><span data-stu-id="71219-616">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-617">D</span><span class="sxs-lookup"><span data-stu-id="71219-617">D</span></span></td>
<td align="left"><span data-ttu-id="71219-618">D</span><span class="sxs-lookup"><span data-stu-id="71219-618">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-619">WMV9 Screen</span><span class="sxs-lookup"><span data-stu-id="71219-619">WMV9 Screen</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-620">DV</span><span class="sxs-lookup"><span data-stu-id="71219-620">DV</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-621">モーション JPEG</span><span class="sxs-lookup"><span data-stu-id="71219-621">Motion JPEG</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-622">D</span><span class="sxs-lookup"><span data-stu-id="71219-622">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-623">D</span><span class="sxs-lookup"><span data-stu-id="71219-623">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="xbox"></a><span data-ttu-id="71219-624">XBox</span><span class="sxs-lookup"><span data-stu-id="71219-624">XBox</span></span>

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-625">コーデック/コンテナー</span><span class="sxs-lookup"><span data-stu-id="71219-625">Codec/Container</span></span></th>
<th align="left"><span data-ttu-id="71219-626">FOURCC</span><span class="sxs-lookup"><span data-stu-id="71219-626">FOURCC</span></span></th>
<th align="left"><span data-ttu-id="71219-627">fMP4</span><span class="sxs-lookup"><span data-stu-id="71219-627">fMP4</span></span></th>
<th align="left"><span data-ttu-id="71219-628">MPEG-4</span><span class="sxs-lookup"><span data-stu-id="71219-628">MPEG-4</span></span></th>
<th align="left"><span data-ttu-id="71219-629">MPEG-2 PS</span><span class="sxs-lookup"><span data-stu-id="71219-629">MPEG-2 PS</span></span></th>
<th align="left"><span data-ttu-id="71219-630">MPEG-2 TS</span><span class="sxs-lookup"><span data-stu-id="71219-630">MPEG-2 TS</span></span></th>
<th align="left"><span data-ttu-id="71219-631">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-631">MPEG-1</span></span></th>
<th align="left"><span data-ttu-id="71219-632">3GPP</span><span class="sxs-lookup"><span data-stu-id="71219-632">3GPP</span></span></th>
<th align="left"><span data-ttu-id="71219-633">3GPP2</span><span class="sxs-lookup"><span data-stu-id="71219-633">3GPP2</span></span></th>
<th align="left"><span data-ttu-id="71219-634">AVCHD</span><span class="sxs-lookup"><span data-stu-id="71219-634">AVCHD</span></span></th>
<th align="left"><span data-ttu-id="71219-635">ASF</span><span class="sxs-lookup"><span data-stu-id="71219-635">ASF</span></span></th>
<th align="left"><span data-ttu-id="71219-636">AVI</span><span class="sxs-lookup"><span data-stu-id="71219-636">AVI</span></span></th>
<th align="left"><span data-ttu-id="71219-637">MKV</span><span class="sxs-lookup"><span data-stu-id="71219-637">MKV</span></span></th>
<th align="left"><span data-ttu-id="71219-638">DV</span><span class="sxs-lookup"><span data-stu-id="71219-638">DV</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-639">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="71219-639">MPEG-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-640">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-640">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-641">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-641">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-642">D</span><span class="sxs-lookup"><span data-stu-id="71219-642">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-643">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-643">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-644">D</span><span class="sxs-lookup"><span data-stu-id="71219-644">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-645">MPEG-2</span><span class="sxs-lookup"><span data-stu-id="71219-645">MPEG-2</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-646">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-646">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-647">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-647">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-648">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-648">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-649">D</span><span class="sxs-lookup"><span data-stu-id="71219-649">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-650">MPEG-4 (Part 2)</span><span class="sxs-lookup"><span data-stu-id="71219-650">MPEG-4 (Part 2)</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-651">D</span><span class="sxs-lookup"><span data-stu-id="71219-651">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-652">D</span><span class="sxs-lookup"><span data-stu-id="71219-652">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-653">D</span><span class="sxs-lookup"><span data-stu-id="71219-653">D</span></span></td>
<td align="left"><span data-ttu-id="71219-654">D</span><span class="sxs-lookup"><span data-stu-id="71219-654">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-655">H.265</span><span class="sxs-lookup"><span data-stu-id="71219-655">H.265</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-656">D</span><span class="sxs-lookup"><span data-stu-id="71219-656">D</span></span></td>
<td align="left"><span data-ttu-id="71219-657">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-657">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-658">D</span><span class="sxs-lookup"><span data-stu-id="71219-658">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-659">H.264</span><span class="sxs-lookup"><span data-stu-id="71219-659">H.264</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-660">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-660">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-661">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-661">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-662">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-662">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-663">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-663">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-664">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-664">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-665">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-665">D/E</span></span></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-666">D</span><span class="sxs-lookup"><span data-stu-id="71219-666">D</span></span></td>
<td align="left"><span data-ttu-id="71219-667">D</span><span class="sxs-lookup"><span data-stu-id="71219-667">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-668">H.263</span><span class="sxs-lookup"><span data-stu-id="71219-668">H.263</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-669">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-669">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-670">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-670">D/E</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-671">D</span><span class="sxs-lookup"><span data-stu-id="71219-671">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-672">VC-1</span><span class="sxs-lookup"><span data-stu-id="71219-672">VC-1</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-673">D</span><span class="sxs-lookup"><span data-stu-id="71219-673">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-674">D</span><span class="sxs-lookup"><span data-stu-id="71219-674">D</span></span></td>
<td align="left"><span data-ttu-id="71219-675">D</span><span class="sxs-lookup"><span data-stu-id="71219-675">D</span></span></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-676">WMV7/8/9</span><span class="sxs-lookup"><span data-stu-id="71219-676">WMV7/8/9</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-677">WMV9 Screen</span><span class="sxs-lookup"><span data-stu-id="71219-677">WMV9 Screen</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-678">DV</span><span class="sxs-lookup"><span data-stu-id="71219-678">DV</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-679">モーション JPEG</span><span class="sxs-lookup"><span data-stu-id="71219-679">Motion JPEG</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-680">D</span><span class="sxs-lookup"><span data-stu-id="71219-680">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><span data-ttu-id="71219-681">D</span><span class="sxs-lookup"><span data-stu-id="71219-681">D</span></span></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

## <a name="image-codec--format-support"></a><span data-ttu-id="71219-682">イメージのコーデックおよび形式のサポート</span><span class="sxs-lookup"><span data-stu-id="71219-682">Image codec & format support</span></span> 

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="71219-683">コーデック</span><span class="sxs-lookup"><span data-stu-id="71219-683">Codec</span></span></th>
<th align="left"><span data-ttu-id="71219-684">Desktop</span><span class="sxs-lookup"><span data-stu-id="71219-684">Desktop</span></span></th>
<th align="left"><span data-ttu-id="71219-685">他のデバイス ファミリ</span><span class="sxs-lookup"><span data-stu-id="71219-685">Other device families</span></span></th>
</tr>
</thead>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-686">BMP</span><span class="sxs-lookup"><span data-stu-id="71219-686">BMP</span></span></td>
<td align="left"><span data-ttu-id="71219-687">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-687">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-688">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-688">D/E</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-689">DDS</span><span class="sxs-lookup"><span data-stu-id="71219-689">DDS</span></span></td>
<td align="left"><span data-ttu-id="71219-690">D/E<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="71219-690">D/E<sup>1</sup></span></span></td>
<td align="left"><span data-ttu-id="71219-691">D/E<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="71219-691">D/E<sup>1</sup></span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-692">DNG</span><span class="sxs-lookup"><span data-stu-id="71219-692">DNG</span></span></td>
<td align="left"><span data-ttu-id="71219-693">D<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="71219-693">D<sup>2</sup></span></span></td>
<td align="left"><span data-ttu-id="71219-694">D<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="71219-694">D<sup>2</sup></span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-695">GIF</span><span class="sxs-lookup"><span data-stu-id="71219-695">GIF</span></span></td>
<td align="left"><span data-ttu-id="71219-696">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-696">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-697">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-697">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-698">ICO</span><span class="sxs-lookup"><span data-stu-id="71219-698">ICO</span></span></td>
<td align="left"><span data-ttu-id="71219-699">D</span><span class="sxs-lookup"><span data-stu-id="71219-699">D</span></span></td>
<td align="left"><span data-ttu-id="71219-700">D</span><span class="sxs-lookup"><span data-stu-id="71219-700">D</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-701">JPEG</span><span class="sxs-lookup"><span data-stu-id="71219-701">JPEG</span></span></td>
<td align="left"><span data-ttu-id="71219-702">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-702">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-703">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-703">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-704">JPEG-XR</span><span class="sxs-lookup"><span data-stu-id="71219-704">JPEG-XR</span></span></td>
<td align="left"><span data-ttu-id="71219-705">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-705">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-706">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-706">D/E</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-707">PNG</span><span class="sxs-lookup"><span data-stu-id="71219-707">PNG</span></span></td>
<td align="left"><span data-ttu-id="71219-708">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-708">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-709">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-709">D/E</span></span></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="71219-710">TIFF</span><span class="sxs-lookup"><span data-stu-id="71219-710">TIFF</span></span></td>
<td align="left"><span data-ttu-id="71219-711">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-711">D/E</span></span></td>
<td align="left"><span data-ttu-id="71219-712">D/E</span><span class="sxs-lookup"><span data-stu-id="71219-712">D/E</span></span></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="71219-713">RAW 形式のカメラ</span><span class="sxs-lookup"><span data-stu-id="71219-713">Camera RAW</span></span></td>
<td align="left"><span data-ttu-id="71219-714">D<sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="71219-714">D<sup>3</sup></span></span></td>
<td align="left"><span data-ttu-id="71219-715">X</span><span class="sxs-lookup"><span data-stu-id="71219-715">No</span></span></td>
</tr>
</table>

<span data-ttu-id="71219-716"><sup>1</sup> BC5 圧縮による BC1 を使用した DDS イメージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="71219-716"><sup>1</sup> DDS images using BC1 through BC5 compression are supported.</span></span>  
<span data-ttu-id="71219-717"><sup>2</sup> 非 RAW 形式の埋め込みプレビューを含む DNG イメージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="71219-717"><sup>2</sup> DNG images with a non-RAW embedded preview are supported.</span></span>  
<span data-ttu-id="71219-718"><sup>3</sup> 特定のカメラの RAW 形式のみがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="71219-718"><sup>3</sup> Only certain camera RAW formats are supported.</span></span>  

<span data-ttu-id="71219-719">イメージ コーデックの詳細については、「[ネイティブ WIC コーデック](https://docs.microsoft.com/windows/desktop/wic/native-wic-codecs)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="71219-719">For more information on image codecs, see [Native WIC Codecs](https://docs.microsoft.com/windows/desktop/wic/native-wic-codecs).</span></span>