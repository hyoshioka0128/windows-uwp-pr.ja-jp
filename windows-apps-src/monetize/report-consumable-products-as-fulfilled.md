---
ms.assetid: E9BEB2D2-155F-45F6-95F8-6B36C3E81649
description: 特定のユーザーについてコンシューマブルな製品をフルフィルメント完了として報告するには、Microsoft Store コレクション API の以下のメソッドを使います。 ユーザーがコンシューマブルな製品を再購入するには、アプリまたはサービスが、そのユーザーについてコンシューマブルな製品をフルフィルメント完了と報告している必要があります。
title: コンシューマブルな製品をフルフィルメント完了として報告する
ms.date: 03/19/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store コレクション API, フルフィルメント, コンシューマブル
ms.localizationpriority: medium
ms.openlocfilehash: 994113abc34a0a5f7905bff00aa77c6785409927
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372771"
---
# <a name="report-consumable-products-as-fulfilled"></a><span data-ttu-id="8d515-105">コンシューマブルな製品をフルフィルメント完了として報告する</span><span class="sxs-lookup"><span data-stu-id="8d515-105">Report consumable products as fulfilled</span></span>

<span data-ttu-id="8d515-106">特定のユーザーについてコンシューマブルな製品をフルフィルメント完了として報告するには、Microsoft Store コレクション API の以下のメソッドを使います。</span><span class="sxs-lookup"><span data-stu-id="8d515-106">Use this method in the Microsoft Store collection API to report a consumable product as fulfilled for a given customer.</span></span> <span data-ttu-id="8d515-107">ユーザーがコンシューマブルな製品を再購入するには、アプリまたはサービスが、そのユーザーについてコンシューマブルな製品をフルフィルメント完了と報告している必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d515-107">Before a user can repurchase a consumable product, your app or service must report the consumable product as fulfilled for that user.</span></span>

<span data-ttu-id="8d515-108">このメソッドを使用してコンシューマブルな製品をフルフィルメント完了として報告するには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="8d515-108">There are two ways you can use this method to report a consumable product as fulfilled:</span></span>

* <span data-ttu-id="8d515-109">コンシューマブルの項目 ID ([製品の照会](query-for-products.md)で **itemId** パラメーターとして返されるもの)、およびユーザー指定の一意の追跡 ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d515-109">Provide the item ID of the consumable (as returned in the **itemId** parameter of a [query for products](query-for-products.md)), and a unique tracking ID that you provide.</span></span> <span data-ttu-id="8d515-110">複数の試行で同じ追跡 ID が使用される場合、項目が既に消費されている場合でも同じ結果が返されます。</span><span class="sxs-lookup"><span data-stu-id="8d515-110">If the same tracking ID is used for multiple tries, the same result will be returned even if the item is already consumed.</span></span> <span data-ttu-id="8d515-111">消費要求が成功したかどうかがわからない場合は、サービスは同じ追跡 ID を使用して消費要求を再送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d515-111">If you aren't certain if a consume request was successful, your service should resubmit consume requests with the same tracking ID.</span></span> <span data-ttu-id="8d515-112">追跡 ID は常にその消費要求に関連付けられており、無限に再送信できます。</span><span class="sxs-lookup"><span data-stu-id="8d515-112">The tracking ID will always be tied to that consume request and can be resubmitted indefinitely.</span></span>
* <span data-ttu-id="8d515-113">製品 ID ([製品の照会](query-for-products.md)の **productId** パラメーターで返されるもの)、および以下の要求の本文セクションの **transactionId** パラメーターの記述にあるいずれかのソースから取得されるトランザクション ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d515-113">Provide the product ID (as returned in the **productId** parameter of a [query for products](query-for-products.md)) and a transaction ID that is obtained from one of the sources listed in the description for the **transactionId** parameter in the request body section below.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d515-114">前提条件</span><span class="sxs-lookup"><span data-stu-id="8d515-114">Prerequisites</span></span>


<span data-ttu-id="8d515-115">このメソッドを使用するための要件:</span><span class="sxs-lookup"><span data-stu-id="8d515-115">To use this method, you will need:</span></span>

* <span data-ttu-id="8d515-116">対象ユーザー URI の値が `https://onestore.microsoft.com` の Azure AD アクセス トークン。</span><span class="sxs-lookup"><span data-stu-id="8d515-116">An Azure AD access token that has the audience URI value `https://onestore.microsoft.com`.</span></span>
* <span data-ttu-id="8d515-117">コンシューマブルな製品をフルフィルメント完了として報告するユーザーの ID を表す Microsoft Store ID キー。</span><span class="sxs-lookup"><span data-stu-id="8d515-117">A Microsoft Store ID key that represents the identity of the user for whom you want to report a consumable product as fulfilled.</span></span>

<span data-ttu-id="8d515-118">詳しくは、「[サービスによる製品の権利の管理](view-and-grant-products-from-a-service.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="8d515-118">For more information, see [Manage product entitlements from a service](view-and-grant-products-from-a-service.md).</span></span>

## <a name="request"></a><span data-ttu-id="8d515-119">要求</span><span class="sxs-lookup"><span data-stu-id="8d515-119">Request</span></span>


### <a name="request-syntax"></a><span data-ttu-id="8d515-120">要求の構文</span><span class="sxs-lookup"><span data-stu-id="8d515-120">Request syntax</span></span>

| <span data-ttu-id="8d515-121">メソッド</span><span class="sxs-lookup"><span data-stu-id="8d515-121">Method</span></span> | <span data-ttu-id="8d515-122">要求 URI</span><span class="sxs-lookup"><span data-stu-id="8d515-122">Request URI</span></span>                                                   |
|--------|---------------------------------------------------------------|
| <span data-ttu-id="8d515-123">POST</span><span class="sxs-lookup"><span data-stu-id="8d515-123">POST</span></span>   | ```https://collections.mp.microsoft.com/v6.0/collections/consume``` |


### <a name="request-header"></a><span data-ttu-id="8d515-124">要求ヘッダー</span><span class="sxs-lookup"><span data-stu-id="8d515-124">Request header</span></span>

| <span data-ttu-id="8d515-125">Header</span><span class="sxs-lookup"><span data-stu-id="8d515-125">Header</span></span>         | <span data-ttu-id="8d515-126">種類</span><span class="sxs-lookup"><span data-stu-id="8d515-126">Type</span></span>   | <span data-ttu-id="8d515-127">説明</span><span class="sxs-lookup"><span data-stu-id="8d515-127">Description</span></span>                                                                                           |
|----------------|--------|-------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8d515-128">Authorization</span><span class="sxs-lookup"><span data-stu-id="8d515-128">Authorization</span></span>  | <span data-ttu-id="8d515-129">string</span><span class="sxs-lookup"><span data-stu-id="8d515-129">string</span></span> | <span data-ttu-id="8d515-130">必須。</span><span class="sxs-lookup"><span data-stu-id="8d515-130">Required.</span></span> <span data-ttu-id="8d515-131">**Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。</span><span class="sxs-lookup"><span data-stu-id="8d515-131">The Azure AD access token in the form **Bearer** &lt;*token*&gt;.</span></span>                           |
| <span data-ttu-id="8d515-132">Host</span><span class="sxs-lookup"><span data-stu-id="8d515-132">Host</span></span>           | <span data-ttu-id="8d515-133">string</span><span class="sxs-lookup"><span data-stu-id="8d515-133">string</span></span> | <span data-ttu-id="8d515-134">値 **collections.mp.microsoft.com** に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d515-134">Must be set to the value **collections.mp.microsoft.com**.</span></span>                                            |
| <span data-ttu-id="8d515-135">Content-Length</span><span class="sxs-lookup"><span data-stu-id="8d515-135">Content-Length</span></span> | <span data-ttu-id="8d515-136">number</span><span class="sxs-lookup"><span data-stu-id="8d515-136">number</span></span> | <span data-ttu-id="8d515-137">要求の本文の長さ。</span><span class="sxs-lookup"><span data-stu-id="8d515-137">The length of the request body.</span></span>                                                                       |
| <span data-ttu-id="8d515-138">Content-Type</span><span class="sxs-lookup"><span data-stu-id="8d515-138">Content-Type</span></span>   | <span data-ttu-id="8d515-139">string</span><span class="sxs-lookup"><span data-stu-id="8d515-139">string</span></span> | <span data-ttu-id="8d515-140">要求と応答の種類を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d515-140">Specifies the request and response type.</span></span> <span data-ttu-id="8d515-141">現時点では、サポートされている唯一の値は **application/json** です。</span><span class="sxs-lookup"><span data-stu-id="8d515-141">Currently, the only supported value is **application/json**.</span></span> |


### <a name="request-body"></a><span data-ttu-id="8d515-142">要求本文</span><span class="sxs-lookup"><span data-stu-id="8d515-142">Request body</span></span>

| <span data-ttu-id="8d515-143">パラメーター</span><span class="sxs-lookup"><span data-stu-id="8d515-143">Parameter</span></span>     | <span data-ttu-id="8d515-144">種類</span><span class="sxs-lookup"><span data-stu-id="8d515-144">Type</span></span>         | <span data-ttu-id="8d515-145">説明</span><span class="sxs-lookup"><span data-stu-id="8d515-145">Description</span></span>         | <span data-ttu-id="8d515-146">必須</span><span class="sxs-lookup"><span data-stu-id="8d515-146">Required</span></span> |
|---------------|--------------|---------------------|----------|
| <span data-ttu-id="8d515-147">beneficiary</span><span class="sxs-lookup"><span data-stu-id="8d515-147">beneficiary</span></span>   | <span data-ttu-id="8d515-148">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="8d515-148">UserIdentity</span></span> | <span data-ttu-id="8d515-149">この項目が使用されているユーザー。</span><span class="sxs-lookup"><span data-stu-id="8d515-149">The user for which this item is being consumed.</span></span> <span data-ttu-id="8d515-150">詳細については、次の表を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8d515-150">For more information, see the following table.</span></span>        | <span data-ttu-id="8d515-151">〇</span><span class="sxs-lookup"><span data-stu-id="8d515-151">Yes</span></span>      |
| <span data-ttu-id="8d515-152">itemId</span><span class="sxs-lookup"><span data-stu-id="8d515-152">itemId</span></span>        | <span data-ttu-id="8d515-153">string</span><span class="sxs-lookup"><span data-stu-id="8d515-153">string</span></span>       | <span data-ttu-id="8d515-154">[製品の照会](query-for-products.md)で返される *itemId* 値。</span><span class="sxs-lookup"><span data-stu-id="8d515-154">The *itemId* value returned by a [query for products](query-for-products.md).</span></span> <span data-ttu-id="8d515-155">このパラメーターは *trackingId* と共に使用します。</span><span class="sxs-lookup"><span data-stu-id="8d515-155">Use this parameter with *trackingId*</span></span>      | <span data-ttu-id="8d515-156">X</span><span class="sxs-lookup"><span data-stu-id="8d515-156">No</span></span>       |
| <span data-ttu-id="8d515-157">trackingId</span><span class="sxs-lookup"><span data-stu-id="8d515-157">trackingId</span></span>    | <span data-ttu-id="8d515-158">guid</span><span class="sxs-lookup"><span data-stu-id="8d515-158">guid</span></span>         | <span data-ttu-id="8d515-159">開発者により指定される一意の追跡 ID。</span><span class="sxs-lookup"><span data-stu-id="8d515-159">A unique tracking ID provided by developer.</span></span> <span data-ttu-id="8d515-160">このパラメーターは *itemId* と共に使用します。</span><span class="sxs-lookup"><span data-stu-id="8d515-160">Use this parameter with *itemId*.</span></span>         | <span data-ttu-id="8d515-161">X</span><span class="sxs-lookup"><span data-stu-id="8d515-161">No</span></span>       |
| <span data-ttu-id="8d515-162">productId</span><span class="sxs-lookup"><span data-stu-id="8d515-162">productId</span></span>     | <span data-ttu-id="8d515-163">string</span><span class="sxs-lookup"><span data-stu-id="8d515-163">string</span></span>       | <span data-ttu-id="8d515-164">[製品の照会](query-for-products.md)で返される *productId* 値。</span><span class="sxs-lookup"><span data-stu-id="8d515-164">The *productId* value returned by a [query for products](query-for-products.md).</span></span> <span data-ttu-id="8d515-165">このパラメーターは *transactionId* と共に使用します。</span><span class="sxs-lookup"><span data-stu-id="8d515-165">Use this parameter with *transactionId*</span></span>   | <span data-ttu-id="8d515-166">X</span><span class="sxs-lookup"><span data-stu-id="8d515-166">No</span></span>       |
| <span data-ttu-id="8d515-167">transactionId</span><span class="sxs-lookup"><span data-stu-id="8d515-167">transactionId</span></span> | <span data-ttu-id="8d515-168">guid</span><span class="sxs-lookup"><span data-stu-id="8d515-168">guid</span></span>         | <span data-ttu-id="8d515-169">次のいずれかのソースから取得されるトランザクション ID 値。</span><span class="sxs-lookup"><span data-stu-id="8d515-169">A transaction ID value that is obtained from one of the following sources.</span></span> <span data-ttu-id="8d515-170">このパラメーターは *productId* と共に使用します。</span><span class="sxs-lookup"><span data-stu-id="8d515-170">Use this parameter with *productId*.</span></span><ul><li><span data-ttu-id="8d515-171">[PurchaseResults](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Store.PurchaseResults) クラスの [TransactionID](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.purchaseresults.transactionid) プロパティ。</span><span class="sxs-lookup"><span data-stu-id="8d515-171">The [TransactionID](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.purchaseresults.transactionid) property of the [PurchaseResults](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Store.PurchaseResults) class.</span></span></li><li><span data-ttu-id="8d515-172">[RequestProductPurchaseAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.requestproductpurchaseasync)、[RequestAppPurchaseAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.requestapppurchaseasync)、または [GetAppReceiptAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.getappreceiptasync) から返されるアプリまたは製品の通知。</span><span class="sxs-lookup"><span data-stu-id="8d515-172">The app or product receipt that is returned by [RequestProductPurchaseAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.requestproductpurchaseasync), [RequestAppPurchaseAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.requestapppurchaseasync), or [GetAppReceiptAsync](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp.getappreceiptasync).</span></span></li><li><span data-ttu-id="8d515-173">[製品の照会](query-for-products.md)で返される *transactionId* パラメーター。</span><span class="sxs-lookup"><span data-stu-id="8d515-173">The *transactionId* parameter returned by a [query for products](query-for-products.md).</span></span></li></ul>   | <span data-ttu-id="8d515-174">X</span><span class="sxs-lookup"><span data-stu-id="8d515-174">No</span></span>       |


<span data-ttu-id="8d515-175">UserIdentity オブジェクトには以下のパラメーターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d515-175">The UserIdentity object contains the following parameters.</span></span>

| <span data-ttu-id="8d515-176">パラメーター</span><span class="sxs-lookup"><span data-stu-id="8d515-176">Parameter</span></span>            | <span data-ttu-id="8d515-177">種類</span><span class="sxs-lookup"><span data-stu-id="8d515-177">Type</span></span>   | <span data-ttu-id="8d515-178">説明</span><span class="sxs-lookup"><span data-stu-id="8d515-178">Description</span></span>       | <span data-ttu-id="8d515-179">必須</span><span class="sxs-lookup"><span data-stu-id="8d515-179">Required</span></span> |
|----------------------|--------|-------------------|----------|
| <span data-ttu-id="8d515-180">identityType</span><span class="sxs-lookup"><span data-stu-id="8d515-180">identityType</span></span>         | <span data-ttu-id="8d515-181">string</span><span class="sxs-lookup"><span data-stu-id="8d515-181">string</span></span> | <span data-ttu-id="8d515-182">文字列値 **b2b** を指定します。</span><span class="sxs-lookup"><span data-stu-id="8d515-182">Specify the string value **b2b**.</span></span>    | <span data-ttu-id="8d515-183">〇</span><span class="sxs-lookup"><span data-stu-id="8d515-183">Yes</span></span>      |
| <span data-ttu-id="8d515-184">identityValue</span><span class="sxs-lookup"><span data-stu-id="8d515-184">identityValue</span></span>        | <span data-ttu-id="8d515-185">string</span><span class="sxs-lookup"><span data-stu-id="8d515-185">string</span></span> | <span data-ttu-id="8d515-186">コンシューマブルな製品をフルフィルメント完了として報告するユーザーの ID を表す [Microsoft Store ID キー](view-and-grant-products-from-a-service.md#step-4)。</span><span class="sxs-lookup"><span data-stu-id="8d515-186">The [Microsoft Store ID key](view-and-grant-products-from-a-service.md#step-4) that represents the identity of the user for whom you want to report a consumable product as fulfilled.</span></span>      | <span data-ttu-id="8d515-187">〇</span><span class="sxs-lookup"><span data-stu-id="8d515-187">Yes</span></span>      |
| <span data-ttu-id="8d515-188">localTicketReference</span><span class="sxs-lookup"><span data-stu-id="8d515-188">localTicketReference</span></span> | <span data-ttu-id="8d515-189">string</span><span class="sxs-lookup"><span data-stu-id="8d515-189">string</span></span> | <span data-ttu-id="8d515-190">返された応答で必要な識別子。</span><span class="sxs-lookup"><span data-stu-id="8d515-190">The requested identifier for the returned response.</span></span> <span data-ttu-id="8d515-191">同じ値を使用することをお勧め、 *userId*[要求](view-and-grant-products-from-a-service.md#claims-in-a-microsoft-store-id-key)Microsoft Store の ID キー。</span><span class="sxs-lookup"><span data-stu-id="8d515-191">We recommend that you use the same value as the *userId*  [claim](view-and-grant-products-from-a-service.md#claims-in-a-microsoft-store-id-key) in the Microsoft Store ID key.</span></span> | <span data-ttu-id="8d515-192">〇</span><span class="sxs-lookup"><span data-stu-id="8d515-192">Yes</span></span>      |


### <a name="request-examples"></a><span data-ttu-id="8d515-193">要求の例</span><span class="sxs-lookup"><span data-stu-id="8d515-193">Request examples</span></span>

<span data-ttu-id="8d515-194">次の例では、*itemId* と *trackingId* を使用します。</span><span class="sxs-lookup"><span data-stu-id="8d515-194">The following example uses *itemId* and *trackingId*.</span></span>

```syntax
POST https://collections.mp.microsoft.com/v6.0/collections/consume HTTP/1.1
Authorization: Bearer eyJ0eXAiOiJKV1…..
Host: collections.mp.microsoft.com
Content-Length: 2050
Content-Type: application/json

{
    "beneficiary": {
        "localTicketReference": "testreference",
        "identityValue": "eyJ0eXAiOi…..",
        "identityType": "b2b"
    },
    "itemId": "44c26106-4979-457b-af34-609ae97a084f",
    "trackingId": "44db79ca-e31d-49e9-8896-fa5c7f892b40"
}
```

<span data-ttu-id="8d515-195">次の例では、*productId* と *transactionId* を使用します。</span><span class="sxs-lookup"><span data-stu-id="8d515-195">The following example uses *productId* and *transactionId*.</span></span>

```syntax
POST https://collections.mp.microsoft.com/v6.0/collections/consume HTTP/1.1
Authorization: Bearer eyJ0eXAiOiJKV1……
Content-Length: 1880
Content-Type: application/json
Host: collections.md.mp.microsoft.com

{
    "beneficiary" : {
        "localTicketReference" : "testReference",
        "identityValue" : "eyJ0eXAiOiJ…..",
        "identitytype" : "b2b"
    },
    "productId" : "9NBLGGH5WVP6",
    "transactionId" : "08a14c7c-1892-49fc-9135-190ca4f10490"
}
```


## <a name="response"></a><span data-ttu-id="8d515-196">応答</span><span class="sxs-lookup"><span data-stu-id="8d515-196">Response</span></span>

<span data-ttu-id="8d515-197">使用が正常に実行された場合、コンテンツは返されません。</span><span class="sxs-lookup"><span data-stu-id="8d515-197">No content will be returned if the consumption was executed successfully.</span></span>

### <a name="response-example"></a><span data-ttu-id="8d515-198">応答の例</span><span class="sxs-lookup"><span data-stu-id="8d515-198">Response example</span></span>

```syntax
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 386f733d-bc66-4bf9-9b6f-a1ad417f97f0
MS-RequestId: e488cd0a-9fb6-4c2c-bb77-e5100d3c15b1
MS-CV: 5.1
MS-ServerId: 030011326
Date: Tue, 22 Sep 2015 20:40:55 GMT
```

## <a name="error-codes"></a><span data-ttu-id="8d515-199">エラー コード</span><span class="sxs-lookup"><span data-stu-id="8d515-199">Error codes</span></span>


| <span data-ttu-id="8d515-200">コード</span><span class="sxs-lookup"><span data-stu-id="8d515-200">Code</span></span> | <span data-ttu-id="8d515-201">エラー</span><span class="sxs-lookup"><span data-stu-id="8d515-201">Error</span></span>        | <span data-ttu-id="8d515-202">内部エラー コード</span><span class="sxs-lookup"><span data-stu-id="8d515-202">Inner error code</span></span>           | <span data-ttu-id="8d515-203">説明</span><span class="sxs-lookup"><span data-stu-id="8d515-203">Description</span></span>           |
|------|--------------|----------------------------|-----------------------|
| <span data-ttu-id="8d515-204">401</span><span class="sxs-lookup"><span data-stu-id="8d515-204">401</span></span>  | <span data-ttu-id="8d515-205">権限がありません</span><span class="sxs-lookup"><span data-stu-id="8d515-205">Unauthorized</span></span> | <span data-ttu-id="8d515-206">AuthenticationTokenInvalid</span><span class="sxs-lookup"><span data-stu-id="8d515-206">AuthenticationTokenInvalid</span></span> | <span data-ttu-id="8d515-207">Azure AD アクセス トークンが無効です。</span><span class="sxs-lookup"><span data-stu-id="8d515-207">The Azure AD access token is invalid.</span></span> <span data-ttu-id="8d515-208">場合によっては、ServiceError の詳細に追加情報が含まれていることがあります (トークンの有効期限切れや *appid* 要求の欠落など)。</span><span class="sxs-lookup"><span data-stu-id="8d515-208">In some cases the details of the ServiceError will contain more information, such as when the token is expired or the *appid* claim is missing.</span></span> |
| <span data-ttu-id="8d515-209">401</span><span class="sxs-lookup"><span data-stu-id="8d515-209">401</span></span>  | <span data-ttu-id="8d515-210">権限がありません</span><span class="sxs-lookup"><span data-stu-id="8d515-210">Unauthorized</span></span> | <span data-ttu-id="8d515-211">PartnerAadTicketRequired</span><span class="sxs-lookup"><span data-stu-id="8d515-211">PartnerAadTicketRequired</span></span>   | <span data-ttu-id="8d515-212">Azure AD アクセス トークンが承認ヘッダーでサービスに渡されませんでした。</span><span class="sxs-lookup"><span data-stu-id="8d515-212">An Azure AD access token was not passed to the service in the authorization header.</span></span>                                                                                                   |
| <span data-ttu-id="8d515-213">401</span><span class="sxs-lookup"><span data-stu-id="8d515-213">401</span></span>  | <span data-ttu-id="8d515-214">権限がありません</span><span class="sxs-lookup"><span data-stu-id="8d515-214">Unauthorized</span></span> | <span data-ttu-id="8d515-215">InconsistentClientId</span><span class="sxs-lookup"><span data-stu-id="8d515-215">InconsistentClientId</span></span>       | <span data-ttu-id="8d515-216">要求本文の Microsoft Store ID の *clientId* 要求と承認ヘッダーの Azure AD アクセス トークンの *appid* 要求が一致しません。</span><span class="sxs-lookup"><span data-stu-id="8d515-216">The *clientId* claim in the Microsoft Store ID key in the request body and the *appid* claim in the Azure AD access token in the authorization header do not match.</span></span>                     |

<span/> 

## <a name="related-topics"></a><span data-ttu-id="8d515-217">関連トピック</span><span class="sxs-lookup"><span data-stu-id="8d515-217">Related topics</span></span>

* [<span data-ttu-id="8d515-218">サービスからの製品の利用資格を管理します。</span><span class="sxs-lookup"><span data-stu-id="8d515-218">Manage product entitlements from a service</span></span>](view-and-grant-products-from-a-service.md)
* [<span data-ttu-id="8d515-219">製品のクエリ</span><span class="sxs-lookup"><span data-stu-id="8d515-219">Query for products</span></span>](query-for-products.md)
* [<span data-ttu-id="8d515-220">無料の製品を付与します。</span><span class="sxs-lookup"><span data-stu-id="8d515-220">Grant free products</span></span>](grant-free-products.md)
* [<span data-ttu-id="8d515-221">Microsoft Store の ID キーを更新します。</span><span class="sxs-lookup"><span data-stu-id="8d515-221">Renew a Microsoft Store ID key</span></span>](renew-a-windows-store-id-key.md)
