---
title: Microsoft Store アプリの起動
description: このトピックでは、ms-windows-store URI スキームについて説明します。 アプリは、この URI スキームを使用して、Microsoft Store アプリ、ストアの特定のページを起動することができます。
ms.assetid: 9A9C6576-1637-47D1-AC3B-D1A20D49E0FF
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: fd0e7137f31a8f1620f7937b52efe1ca84a6b99a
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370782"
---
# <a name="launch-the-microsoft-store-app"></a><span data-ttu-id="925b9-105">Microsoft Store アプリの起動</span><span class="sxs-lookup"><span data-stu-id="925b9-105">Launch the Microsoft Store app</span></span>



<span data-ttu-id="925b9-106">このトピックで説明します、 **ms-windows ストア。** URI スキーム。</span><span class="sxs-lookup"><span data-stu-id="925b9-106">This topic describes the **ms-windows-store:** URI scheme.</span></span> <span data-ttu-id="925b9-107">アプリは、この URI スキームを使用して、使用して、ストア内の特定のページに、Microsoft Store アプリを起動する、 [ **LaunchUriAsync** ](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync)メソッド。</span><span class="sxs-lookup"><span data-stu-id="925b9-107">Your app can use this URI scheme to launch the Microsoft Store app to specific pages in the store by using the [**LaunchUriAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync) method.</span></span>

<span data-ttu-id="925b9-108">この例では、Microsoft Store のゲームのページを開く方法を示します。</span><span class="sxs-lookup"><span data-stu-id="925b9-108">This example shows how to open the Store to the Games page:</span></span>

```cs
bool result = await Windows.System.Launcher.LaunchUriAsync(new Uri("ms-windows-store://navigatetopage/?Id=Games"));
```

## <a name="ms-windows-store-uri-scheme-reference"></a><span data-ttu-id="925b9-109">ms-windows ストア:URI スキームの参照</span><span class="sxs-lookup"><span data-stu-id="925b9-109">ms-windows-store: URI scheme reference</span></span>

<table>
<tr><th><span data-ttu-id="925b9-110">説明</span><span class="sxs-lookup"><span data-stu-id="925b9-110">Description</span></span></th><th></th><th><span data-ttu-id="925b9-111">URI スキーム</span><span class="sxs-lookup"><span data-stu-id="925b9-111">URI scheme</span></span></th></tr>
<tr><td><span data-ttu-id="925b9-112">ストアのホーム ページを起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-112">Launches the home page of the Store.</span></span></td><td /><td><span data-ttu-id="925b9-113">ms-windows-store://home</span><span class="sxs-lookup"><span data-stu-id="925b9-113">ms-windows-store://home</span></span></td></tr>
<tr><td><span data-ttu-id="925b9-114">ストア内の最上位レベルのカテゴリを起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-114">Launches a top-level vertical in the Store.</span></span><p><span data-ttu-id="925b9-115">注:すべてのユーザーでは、すべての業種にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="925b9-115">Note: Not all users have access to all verticals.</span></span></p>
</td><td /><td>
<p><span data-ttu-id="925b9-116">ms-windows-store://navigatetopage/?Id=Apps</span><span class="sxs-lookup"><span data-stu-id="925b9-116">ms-windows-store://navigatetopage/?Id=Apps</span></span> </p>
<p><span data-ttu-id="925b9-117">ms-windows-store://navigatetopage/?Id=Games</span><span class="sxs-lookup"><span data-stu-id="925b9-117">ms-windows-store://navigatetopage/?Id=Games</span></span></p>
<p><span data-ttu-id="925b9-118">ms-windows-store://navigatetopage/?Id=Music</span><span class="sxs-lookup"><span data-stu-id="925b9-118">ms-windows-store://navigatetopage/?Id=Music</span></span></p>
<p><span data-ttu-id="925b9-119">ms-windows-store://navigatetopage/?Id=Video</span><span class="sxs-lookup"><span data-stu-id="925b9-119">ms-windows-store://navigatetopage/?Id=Video</span></span></p>
<p><span data-ttu-id="925b9-120">ms-windows-store://navigatetopage/?Id=LOB</span><span class="sxs-lookup"><span data-stu-id="925b9-120">ms-windows-store://navigatetopage/?Id=LOB</span></span></p>
</td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="925b9-121">製品の詳細ページ (PDP) を起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-121">Launches the product details page (PDP) for a product.</span></span> <p><span data-ttu-id="925b9-122">Store ID は、Windows 10 でのお客様をお勧めし、協力してこれ以前の方法がすべての OS バージョン (例。PFN) はまだサポートされています。</span><span class="sxs-lookup"><span data-stu-id="925b9-122">Store ID is recommended for customers on Windows 10, and will work on all OS versions, but the earlier ways of doing it (ex: PFN) are still supported.</span></span></p>
<p><span data-ttu-id="925b9-123">これらの値を確認できる<a href="https://partner.microsoft.com/dashboard">パートナー センター</a>上、<a href="https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details">アプリ id</a>  ページの各アプリのアプリの管理セクション。</span><span class="sxs-lookup"><span data-stu-id="925b9-123">These values can be found in <a href="https://partner.microsoft.com/dashboard">Partner Center</a> on the <a href="https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details">App identity</a> page in the App management section for each app.</span></span></p>
</td>
<td>
<span data-ttu-id="925b9-124">Store ID</span><span class="sxs-lookup"><span data-stu-id="925b9-124">Store ID</span></span> <p><span data-ttu-id="925b9-125">(推奨)</span><span class="sxs-lookup"><span data-stu-id="925b9-125">(Recommended)</span></span></p>
</td>
<td>
<p><span data-ttu-id="925b9-126">ms-windows-store://pdp/?ProductId=9WZDNCRFHVJL</span><span class="sxs-lookup"><span data-stu-id="925b9-126">ms-windows-store://pdp/?ProductId=9WZDNCRFHVJL</span></span></p>
</td>
</tr>
<tr>
<td><span data-ttu-id="925b9-127">パッケージ ファミリ名 (PFN)</span><span class="sxs-lookup"><span data-stu-id="925b9-127">Package Family Name (PFN)</span></span></td>
<td><span data-ttu-id="925b9-128">ms-windows-store://pdp/?PFN= Microsoft.Office.OneNote_8wekyb3d8bbwe</span><span class="sxs-lookup"><span data-stu-id="925b9-128">ms-windows-store://pdp/?PFN= Microsoft.Office.OneNote_8wekyb3d8bbwe</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="925b9-129">製品 ID (Windows Phone 7.x/8.x)</span><span class="sxs-lookup"><span data-stu-id="925b9-129">Product ID (Windows Phone 7.x/8.x)</span></span></td>
<td><span data-ttu-id="925b9-130">ms-windows-store://pdp/?PhoneAppId=ca05b3ab-f157-450c-8c49-a1f127f5e71d</span><span class="sxs-lookup"><span data-stu-id="925b9-130">ms-windows-store://pdp/?PhoneAppId=ca05b3ab-f157-450c-8c49-a1f127f5e71d</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="925b9-131">製品 ID (Windows 8.x)</span><span class="sxs-lookup"><span data-stu-id="925b9-131">Product ID (Windows 8.x)</span></span></td>
<td><span data-ttu-id="925b9-132">ms-windows-store://pdp/?AppId=f022389f-f3a6-417e-ad23-704fbdf57117</span><span class="sxs-lookup"><span data-stu-id="925b9-132">ms-windows-store://pdp/?AppId=f022389f-f3a6-417e-ad23-704fbdf57117</span></span>
</td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="925b9-133">製品のレビューを書くエクスペリエンスを起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-133">Launches the write a review experience for a product.</span></span></td>
<td><span data-ttu-id="925b9-134">Store ID</span><span class="sxs-lookup"><span data-stu-id="925b9-134">Store ID</span></span> <p><span data-ttu-id="925b9-135">(推奨)</span><span class="sxs-lookup"><span data-stu-id="925b9-135">(Recommended)</span></span></p></td>
<td><span data-ttu-id="925b9-136">ms-windows-store://review/?ProductId=9WZDNCRFHVJL</span><span class="sxs-lookup"><span data-stu-id="925b9-136">ms-windows-store://review/?ProductId=9WZDNCRFHVJL</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="925b9-137">パッケージ ファミリ名 (PFN)</span><span class="sxs-lookup"><span data-stu-id="925b9-137">Package Family Name (PFN)</span></span></td>
<td><span data-ttu-id="925b9-138">ms-windows-store://review/?PFN= Microsoft.Office.OneNote_8wekyb3d8bbwe</span><span class="sxs-lookup"><span data-stu-id="925b9-138">ms-windows-store://review/?PFN= Microsoft.Office.OneNote_8wekyb3d8bbwe</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="925b9-139">製品 ID (Windows Phone 7.x/8.x)</span><span class="sxs-lookup"><span data-stu-id="925b9-139">Product ID (Windows Phone 7.x/8.x)</span></span></td>
<td><span data-ttu-id="925b9-140">ms-windows-store://reviewapp/?AppId=ca05b3ab-f157-450c-8c49-a1f127f5e71d</span><span class="sxs-lookup"><span data-stu-id="925b9-140">ms-windows-store://reviewapp/?AppId=ca05b3ab-f157-450c-8c49-a1f127f5e71d</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="925b9-141">製品 ID (Windows 8.x)</span><span class="sxs-lookup"><span data-stu-id="925b9-141">Product ID (Windows 8.x)</span></span></td>
<td><span data-ttu-id="925b9-142">ms-windows-store://review/?AppId=f022389f-f3a6-417e-ad23-704fbdf57117</span><span class="sxs-lookup"><span data-stu-id="925b9-142">ms-windows-store://review/?AppId=f022389f-f3a6-417e-ad23-704fbdf57117</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="925b9-143">ファイル拡張子に関連付けられた製品の検索を起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-143">Launches a search for products associated with a file extension.</span></span> </td>
<td />
<td><span data-ttu-id="925b9-144">ms-windows-store://assoc/?FileExt=pdf</span><span class="sxs-lookup"><span data-stu-id="925b9-144">ms-windows-store://assoc/?FileExt=pdf</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="925b9-145">プロトコルに関連付けられた製品の検索を起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-145">Launches a search for products associated with a protocol.</span></span></td>
<td />
<td><span data-ttu-id="925b9-146">ms-windows-store://assoc/?Protocol=ms-word</span><span class="sxs-lookup"><span data-stu-id="925b9-146">ms-windows-store://assoc/?Protocol=ms-word</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="925b9-147">1 つまたは複数のタグに関連付けられた製品の検索を起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-147">Launches a search for products associated with one or more tags.</span></span> <span data-ttu-id="925b9-148">タグはコンマで区切る必要があります。</span><span class="sxs-lookup"><span data-stu-id="925b9-148">Tags should be separated by commas.</span></span>
</td>
<td />
<td>
<p><span data-ttu-id="925b9-149">ms-windows-store://assoc/?Tags=Photos_Rich_Media_Edit</span><span class="sxs-lookup"><span data-stu-id="925b9-149">ms-windows-store://assoc/?Tags=Photos_Rich_Media_Edit</span></span> </p>
<p><span data-ttu-id="925b9-150">ms-windows-store://assoc/?Tags=Photos_Rich_Media_Edit, Camera_Capture_App</span><span class="sxs-lookup"><span data-stu-id="925b9-150">ms-windows-store://assoc/?Tags=Photos_Rich_Media_Edit, Camera_Capture_App</span></span></p>
</td>
</tr>
<tr>
<td>
<span data-ttu-id="925b9-151">指定されたクエリの検索を起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-151">Launches a search for the specified query.</span></span> <span data-ttu-id="925b9-152">クエリ内で空白文字を使うことができます。</span><span class="sxs-lookup"><span data-stu-id="925b9-152">Spaces in the query are allowed.</span></span>
</td>
<td />
<td><span data-ttu-id="925b9-153">ms-windows-store://search/?query=OneNote</span><span class="sxs-lookup"><span data-stu-id="925b9-153">ms-windows-store://search/?query=OneNote</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="925b9-154">カテゴリ内で製品の検索を起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-154">Launches a search for products in a category.</span></span></td>
<td />
<td>
<p><span data-ttu-id="925b9-155">ms-windows-store://browse/?type=Apps&amp;cat=Productivity</span><span class="sxs-lookup"><span data-stu-id="925b9-155">ms-windows-store://browse/?type=Apps&amp;cat=Productivity</span></span></p>
<p><span data-ttu-id="925b9-156">ms-windows-store://browse/?type=Apps&amp;cat=Health+%26+fitness</span><span class="sxs-lookup"><span data-stu-id="925b9-156">ms-windows-store://browse/?type=Apps&amp;cat=Health+%26+fitness</span></span> </p>
</td>
</tr>
<tr>
<td><span data-ttu-id="925b9-157">指定した発行元からの製品の検索を起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-157">Launches a search for products from the specified publisher.</span></span> <span data-ttu-id="925b9-158">名前には空白文字を使うことができます。</span><span class="sxs-lookup"><span data-stu-id="925b9-158">Spaces in the name are allowed.</span></span>
</td>
<td />
<td><span data-ttu-id="925b9-159">ms-windows-store://publisher/?name=Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="925b9-159">ms-windows-store://publisher/?name=Microsoft Corporation</span></span>
</td>
</tr>
<tr><td><span data-ttu-id="925b9-160">ダウンロードと更新プログラムに関するページを起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-160">Launches the downloads and updates page.</span></span></td>
<td />
<td><span data-ttu-id="925b9-161">ms-windows-store://downloadsandupdates</span><span class="sxs-lookup"><span data-stu-id="925b9-161">ms-windows-store://downloadsandupdates</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="925b9-162">ストアの設定ページを起動します。</span><span class="sxs-lookup"><span data-stu-id="925b9-162">Launches the Store settings page.</span></span></td>
<td />
<td><span data-ttu-id="925b9-163">ms-windows-store://settings</span><span class="sxs-lookup"><span data-stu-id="925b9-163">ms-windows-store://settings</span></span> </td>
</tr>
</table>

 

 
