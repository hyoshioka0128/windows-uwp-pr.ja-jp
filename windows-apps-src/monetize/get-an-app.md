---
ms.assetid: DAF92881-6AF6-44C7-B466-215F5226AE04
description: パートナー センター アカウントに登録されている特定のアプリについての情報を取得するのに、Microsoft Store 送信 API でこのメソッドを使用します。
title: アプリの入手
ms.date: 02/28/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, アプリ
ms.localizationpriority: medium
ms.openlocfilehash: 96efc6145d382d4f6a996e541d638f2a1d896e80
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372660"
---
# <a name="get-an-app"></a><span data-ttu-id="5be51-104">アプリの入手</span><span class="sxs-lookup"><span data-stu-id="5be51-104">Get an app</span></span>

<span data-ttu-id="5be51-105">パートナー センター アカウントに登録されている特定のアプリについての情報を取得するのに、Microsoft Store 送信 API でこのメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="5be51-105">Use this method in the Microsoft Store submission API to retrieve information about a specific app that is registered to your Partner Center account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5be51-106">前提条件</span><span class="sxs-lookup"><span data-stu-id="5be51-106">Prerequisites</span></span>

<span data-ttu-id="5be51-107">このメソッドを使うには、最初に次の作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="5be51-107">To use this method, you need to first do the following:</span></span>

* <span data-ttu-id="5be51-108">Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。</span><span class="sxs-lookup"><span data-stu-id="5be51-108">If you have not done so already, complete all the [prerequisites](create-and-manage-submissions-using-windows-store-services.md#prerequisites) for the Microsoft Store submission API.</span></span>
* <span data-ttu-id="5be51-109">このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。</span><span class="sxs-lookup"><span data-stu-id="5be51-109">[Obtain an Azure AD access token](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token) to use in the request header for this method.</span></span> <span data-ttu-id="5be51-110">アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。</span><span class="sxs-lookup"><span data-stu-id="5be51-110">After you obtain an access token, you have 60 minutes to use it before it expires.</span></span> <span data-ttu-id="5be51-111">トークンの有効期限が切れたら新しいトークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="5be51-111">After the token expires, you can obtain a new one.</span></span>

## <a name="request"></a><span data-ttu-id="5be51-112">要求</span><span class="sxs-lookup"><span data-stu-id="5be51-112">Request</span></span>

<span data-ttu-id="5be51-113">このメソッドの構文は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5be51-113">This method has the following syntax.</span></span> <span data-ttu-id="5be51-114">ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5be51-114">See the following sections for usage examples and descriptions of the header and request body.</span></span>

| <span data-ttu-id="5be51-115">メソッド</span><span class="sxs-lookup"><span data-stu-id="5be51-115">Method</span></span> | <span data-ttu-id="5be51-116">要求 URI</span><span class="sxs-lookup"><span data-stu-id="5be51-116">Request URI</span></span>                                                      |
|--------|------------------------------------------------------------------|
| <span data-ttu-id="5be51-117">GET</span><span class="sxs-lookup"><span data-stu-id="5be51-117">GET</span></span>    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}` |


### <a name="request-header"></a><span data-ttu-id="5be51-118">要求ヘッダー</span><span class="sxs-lookup"><span data-stu-id="5be51-118">Request header</span></span>

| <span data-ttu-id="5be51-119">Header</span><span class="sxs-lookup"><span data-stu-id="5be51-119">Header</span></span>        | <span data-ttu-id="5be51-120">種類</span><span class="sxs-lookup"><span data-stu-id="5be51-120">Type</span></span>   | <span data-ttu-id="5be51-121">説明</span><span class="sxs-lookup"><span data-stu-id="5be51-121">Description</span></span>                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| <span data-ttu-id="5be51-122">Authorization</span><span class="sxs-lookup"><span data-stu-id="5be51-122">Authorization</span></span> | <span data-ttu-id="5be51-123">string</span><span class="sxs-lookup"><span data-stu-id="5be51-123">string</span></span> | <span data-ttu-id="5be51-124">必須。</span><span class="sxs-lookup"><span data-stu-id="5be51-124">Required.</span></span> <span data-ttu-id="5be51-125">**Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。</span><span class="sxs-lookup"><span data-stu-id="5be51-125">The Azure AD access token in the form **Bearer** &lt;*token*&gt;.</span></span> |


### <a name="request-parameters"></a><span data-ttu-id="5be51-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="5be51-126">Request parameters</span></span>

| <span data-ttu-id="5be51-127">名前</span><span class="sxs-lookup"><span data-stu-id="5be51-127">Name</span></span>        | <span data-ttu-id="5be51-128">種類</span><span class="sxs-lookup"><span data-stu-id="5be51-128">Type</span></span>   | <span data-ttu-id="5be51-129">説明</span><span class="sxs-lookup"><span data-stu-id="5be51-129">Description</span></span>                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| <span data-ttu-id="5be51-130">applicationId</span><span class="sxs-lookup"><span data-stu-id="5be51-130">applicationId</span></span> | <span data-ttu-id="5be51-131">string</span><span class="sxs-lookup"><span data-stu-id="5be51-131">string</span></span> | <span data-ttu-id="5be51-132">必須。</span><span class="sxs-lookup"><span data-stu-id="5be51-132">Required.</span></span> <span data-ttu-id="5be51-133">取得するアプリのストア ID。</span><span class="sxs-lookup"><span data-stu-id="5be51-133">The Store ID of the app to retrieve.</span></span> <span data-ttu-id="5be51-134">ストア ID について詳しくは、「[アプリ ID の詳細の表示](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5be51-134">For more information about the Store ID, see [View app identity details](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details).</span></span>  |


### <a name="request-body"></a><span data-ttu-id="5be51-135">要求本文</span><span class="sxs-lookup"><span data-stu-id="5be51-135">Request body</span></span>

<span data-ttu-id="5be51-136">このメソッドでは要求本文を指定しないでください。</span><span class="sxs-lookup"><span data-stu-id="5be51-136">Do not provide a request body for this method.</span></span>

### <a name="request-example"></a><span data-ttu-id="5be51-137">要求の例</span><span class="sxs-lookup"><span data-stu-id="5be51-137">Request example</span></span>

<span data-ttu-id="5be51-138">次の例は、Store ID 値が 9NBLGGH4R315 であるアプリに関する情報を取得する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5be51-138">The following example demonstrates how to retrieve information about an app with the Store ID value 9NBLGGH4R315.</span></span>

```json
GET https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a><span data-ttu-id="5be51-139">応答</span><span class="sxs-lookup"><span data-stu-id="5be51-139">Response</span></span>

<span data-ttu-id="5be51-140">次の例は、このメソッドが正常に呼び出された場合の JSON 応答本文を示しています。</span><span class="sxs-lookup"><span data-stu-id="5be51-140">The following example demonstrates the JSON response body for a successful call to this method.</span></span> <span data-ttu-id="5be51-141">応答の本文内の値について詳しくは、[アプリケーションのリソース](get-app-data.md#application_object)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5be51-141">For more details about the values in the response body, see [Application resource](get-app-data.md#application_object).</span></span>

```json
{
  "id": "9NBLGGH4R315",
  "primaryName": "ApiTestApp",
  "packageFamilyName": "30481DevCenterAPITester.ApiTestAppForDevbox_ng6try80pwt52",
  "packageIdentityName": "30481DevCenterAPITester.ApiTestAppForDevbox",
  "publisherName": "CN=…",
  "firstPublishedDate": "1601-01-01T00:00:00Z",
  "lastPublishedApplicationSubmission": {
    "id": "1152921504621086517",
    "resourceLocation": "applications/9NBLGGH4R315/submissions/1152921504621086517"
  },
  "pendingApplicationSubmission": {
    "id": "1152921504621243487",
    "resourceLocation": "applications/9NBLGGH4R315/submissions/1152921504621243487"
  },
  "hasAdvancedListingPermission": false
}
```

## <a name="error-codes"></a><span data-ttu-id="5be51-142">エラー コード</span><span class="sxs-lookup"><span data-stu-id="5be51-142">Error codes</span></span>

<span data-ttu-id="5be51-143">要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。</span><span class="sxs-lookup"><span data-stu-id="5be51-143">If the request cannot be successfully completed, the response will contain one of the following HTTP error codes.</span></span>

| <span data-ttu-id="5be51-144">エラー コード</span><span class="sxs-lookup"><span data-stu-id="5be51-144">Error code</span></span> |  <span data-ttu-id="5be51-145">説明</span><span class="sxs-lookup"><span data-stu-id="5be51-145">Description</span></span>   |
|--------|------------------|
| <span data-ttu-id="5be51-146">404</span><span class="sxs-lookup"><span data-stu-id="5be51-146">404</span></span>  | <span data-ttu-id="5be51-147">指定したアプリは見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="5be51-147">The specified app could not be found.</span></span> |
| <span data-ttu-id="5be51-148">409</span><span class="sxs-lookup"><span data-stu-id="5be51-148">409</span></span>  | <span data-ttu-id="5be51-149">アプリはパートナー センター機能を使用する[現在サポートされていません、Microsoft Store 送信 API](create-and-manage-submissions-using-windows-store-services.md#not_supported)します。</span><span class="sxs-lookup"><span data-stu-id="5be51-149">The app uses a Partner Center feature that is [currently not supported by the Microsoft Store submission API](create-and-manage-submissions-using-windows-store-services.md#not_supported).</span></span>  |


## <a name="related-topics"></a><span data-ttu-id="5be51-150">関連トピック</span><span class="sxs-lookup"><span data-stu-id="5be51-150">Related topics</span></span>

* [<span data-ttu-id="5be51-151">作成し、Microsoft Store サービスを使用して送信の管理</span><span class="sxs-lookup"><span data-stu-id="5be51-151">Create and manage submissions using Microsoft Store services</span></span>](create-and-manage-submissions-using-windows-store-services.md)
* [<span data-ttu-id="5be51-152">すべてのアプリを入手します。</span><span class="sxs-lookup"><span data-stu-id="5be51-152">Get all apps</span></span>](get-all-apps.md)
* [<span data-ttu-id="5be51-153">アプリのパッケージのフライトを取得します。</span><span class="sxs-lookup"><span data-stu-id="5be51-153">Get package flights for an app</span></span>](get-flights-for-an-app.md)
* [<span data-ttu-id="5be51-154">アプリのアドオンを入手します。</span><span class="sxs-lookup"><span data-stu-id="5be51-154">Get add-ons for an app</span></span>](get-add-ons-for-an-app.md)
