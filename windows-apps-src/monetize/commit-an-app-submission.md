---
ms.assetid: 934F2DBF-2C7E-4B77-997D-17B9B0535D51
description: Microsoft Store 送信 API でこのメソッドを使用して、パートナー センターに新しいまたは更新されたアプリの提出をコミットします。
title: アプリの申請のコミット
ms.date: 04/17/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, アプリの申請のコミット
ms.localizationpriority: medium
ms.openlocfilehash: 36c645303a86bc28f12fa8e31b8a83653c167664
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371995"
---
# <a name="commit-an-app-submission"></a><span data-ttu-id="979d0-104">アプリの申請のコミット</span><span class="sxs-lookup"><span data-stu-id="979d0-104">Commit an app submission</span></span>

<span data-ttu-id="979d0-105">Microsoft Store 送信 API でこのメソッドを使用して、パートナー センターに新しいまたは更新されたアプリの提出をコミットします。</span><span class="sxs-lookup"><span data-stu-id="979d0-105">Use this method in the Microsoft Store submission API to commit a new or updated app submission to  Partner Center.</span></span> <span data-ttu-id="979d0-106">コミット アクション アラート パートナー センター (すべての関連するパッケージとイメージを含む) の送信データがアップロードされています。</span><span class="sxs-lookup"><span data-stu-id="979d0-106">The commit action alerts Partner Center that the submission data has been uploaded (including any related packages and images).</span></span> <span data-ttu-id="979d0-107">応答では、パートナー センターは、送信データの取り込みおよび発行に変更をコミットします。</span><span class="sxs-lookup"><span data-stu-id="979d0-107">In response, Partner Center commits the changes to the submission data for ingestion and publishing.</span></span> <span data-ttu-id="979d0-108">コミット操作が成功すると、パートナー センターで、送信への変更が表示されます。</span><span class="sxs-lookup"><span data-stu-id="979d0-108">After the commit operation succeeds, the changes to the submission are shown in Partner Center.</span></span>

<span data-ttu-id="979d0-109">コミット操作が Microsoft Store 申請 API を使ったアプリ申請プロセスにどのように適合するかについては、「[アプリの申請の管理](manage-app-submissions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="979d0-109">For more information about how the commit operation fits into the process of submitting an app by using the Microsoft Store submission API, see [Manage app submissions](manage-app-submissions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="979d0-110">前提条件</span><span class="sxs-lookup"><span data-stu-id="979d0-110">Prerequisites</span></span>

<span data-ttu-id="979d0-111">このメソッドを使うには、最初に次の作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="979d0-111">To use this method, you need to first do the following:</span></span>

* <span data-ttu-id="979d0-112">Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。</span><span class="sxs-lookup"><span data-stu-id="979d0-112">If you have not done so already, complete all the [prerequisites](create-and-manage-submissions-using-windows-store-services.md#prerequisites) for the Microsoft Store submission API.</span></span>
* <span data-ttu-id="979d0-113">このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。</span><span class="sxs-lookup"><span data-stu-id="979d0-113">[Obtain an Azure AD access token](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token) to use in the request header for this method.</span></span> <span data-ttu-id="979d0-114">アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。</span><span class="sxs-lookup"><span data-stu-id="979d0-114">After you obtain an access token, you have 60 minutes to use it before it expires.</span></span> <span data-ttu-id="979d0-115">トークンの有効期限が切れたら新しいトークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="979d0-115">After the token expires, you can obtain a new one.</span></span>
* <span data-ttu-id="979d0-116">[アプリの申請を作成](create-an-app-submission.md)し、申請データを必要に応じて変更して[申請を更新](update-an-app-submission.md)します。</span><span class="sxs-lookup"><span data-stu-id="979d0-116">[Create an app submission](create-an-app-submission.md) and then [update the submission](update-an-app-submission.md) with any necessary changes to the submission data.</span></span>

## <a name="request"></a><span data-ttu-id="979d0-117">要求</span><span class="sxs-lookup"><span data-stu-id="979d0-117">Request</span></span>

<span data-ttu-id="979d0-118">このメソッドの構文は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="979d0-118">This method has the following syntax.</span></span> <span data-ttu-id="979d0-119">ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="979d0-119">See the following sections for usage examples and descriptions of the header and request body.</span></span>

| <span data-ttu-id="979d0-120">メソッド</span><span class="sxs-lookup"><span data-stu-id="979d0-120">Method</span></span> | <span data-ttu-id="979d0-121">要求 URI</span><span class="sxs-lookup"><span data-stu-id="979d0-121">Request URI</span></span>                                                      |
|--------|------------------------------------------------------------------|
| <span data-ttu-id="979d0-122">POST</span><span class="sxs-lookup"><span data-stu-id="979d0-122">POST</span></span>    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/commit` |


### <a name="request-header"></a><span data-ttu-id="979d0-123">要求ヘッダー</span><span class="sxs-lookup"><span data-stu-id="979d0-123">Request header</span></span>

| <span data-ttu-id="979d0-124">Header</span><span class="sxs-lookup"><span data-stu-id="979d0-124">Header</span></span>        | <span data-ttu-id="979d0-125">種類</span><span class="sxs-lookup"><span data-stu-id="979d0-125">Type</span></span>   | <span data-ttu-id="979d0-126">説明</span><span class="sxs-lookup"><span data-stu-id="979d0-126">Description</span></span>                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| <span data-ttu-id="979d0-127">Authorization</span><span class="sxs-lookup"><span data-stu-id="979d0-127">Authorization</span></span> | <span data-ttu-id="979d0-128">string</span><span class="sxs-lookup"><span data-stu-id="979d0-128">string</span></span> | <span data-ttu-id="979d0-129">必須。</span><span class="sxs-lookup"><span data-stu-id="979d0-129">Required.</span></span> <span data-ttu-id="979d0-130">**Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。</span><span class="sxs-lookup"><span data-stu-id="979d0-130">The Azure AD access token in the form **Bearer** &lt;*token*&gt;.</span></span> |


### <a name="request-parameters"></a><span data-ttu-id="979d0-131">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="979d0-131">Request parameters</span></span>

| <span data-ttu-id="979d0-132">名前</span><span class="sxs-lookup"><span data-stu-id="979d0-132">Name</span></span>        | <span data-ttu-id="979d0-133">種類</span><span class="sxs-lookup"><span data-stu-id="979d0-133">Type</span></span>   | <span data-ttu-id="979d0-134">説明</span><span class="sxs-lookup"><span data-stu-id="979d0-134">Description</span></span>                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| <span data-ttu-id="979d0-135">applicationId</span><span class="sxs-lookup"><span data-stu-id="979d0-135">applicationId</span></span> | <span data-ttu-id="979d0-136">string</span><span class="sxs-lookup"><span data-stu-id="979d0-136">string</span></span> | <span data-ttu-id="979d0-137">必須。</span><span class="sxs-lookup"><span data-stu-id="979d0-137">Required.</span></span> <span data-ttu-id="979d0-138">コミットする申請が含まれるアプリのストア ID です。</span><span class="sxs-lookup"><span data-stu-id="979d0-138">The Store ID of the app that contains the submission you want to commit.</span></span> <span data-ttu-id="979d0-139">ストア ID について詳しくは、「[アプリ ID の詳細の表示](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="979d0-139">For more information about the Store ID, see [View app identity details](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details).</span></span>  |
| <span data-ttu-id="979d0-140">submissionId</span><span class="sxs-lookup"><span data-stu-id="979d0-140">submissionId</span></span> | <span data-ttu-id="979d0-141">string</span><span class="sxs-lookup"><span data-stu-id="979d0-141">string</span></span> | <span data-ttu-id="979d0-142">必須。</span><span class="sxs-lookup"><span data-stu-id="979d0-142">Required.</span></span> <span data-ttu-id="979d0-143">コミットする申請の ID です。</span><span class="sxs-lookup"><span data-stu-id="979d0-143">The ID of the submission you want to commit.</span></span> <span data-ttu-id="979d0-144">この ID は、[アプリの申請の作成](create-an-app-submission.md)要求に対する応答データで確認できます。</span><span class="sxs-lookup"><span data-stu-id="979d0-144">This ID is available in the response data for requests to [create an app submission](create-an-app-submission.md).</span></span> <span data-ttu-id="979d0-145">パートナー センターで作成された送信、この ID はパートナー センターでの送信 ページの URL で使用できるも。</span><span class="sxs-lookup"><span data-stu-id="979d0-145">For a submission that was created in Partner Center, this ID is also available in the URL for the submission page in Partner Center.</span></span>  |

### <a name="request-body"></a><span data-ttu-id="979d0-146">要求本文</span><span class="sxs-lookup"><span data-stu-id="979d0-146">Request body</span></span>

<span data-ttu-id="979d0-147">このメソッドでは要求本文を指定しないでください。</span><span class="sxs-lookup"><span data-stu-id="979d0-147">Do not provide a request body for this method.</span></span>

### <a name="request-example"></a><span data-ttu-id="979d0-148">要求の例</span><span class="sxs-lookup"><span data-stu-id="979d0-148">Request example</span></span>

<span data-ttu-id="979d0-149">次の例は、アプリの申請をコミットする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="979d0-149">The following example demonstrates how to commit an app submission.</span></span>

```json
POST https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/submissions/1152921504621243610/commit HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a><span data-ttu-id="979d0-150">応答</span><span class="sxs-lookup"><span data-stu-id="979d0-150">Response</span></span>

<span data-ttu-id="979d0-151">次の例は、このメソッドが正常に呼び出された場合の JSON 応答本文を示しています。</span><span class="sxs-lookup"><span data-stu-id="979d0-151">The following example demonstrates the JSON response body for a successful call to this method.</span></span> <span data-ttu-id="979d0-152">応答本文の値について詳しくは、次のセクションをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="979d0-152">For more details about the values in the response body, see the following sections.</span></span>

```json
{
  "status": "CommitStarted"
}
```

### <a name="response-body"></a><span data-ttu-id="979d0-153">応答本文</span><span class="sxs-lookup"><span data-stu-id="979d0-153">Response body</span></span>

| <span data-ttu-id="979d0-154">Value</span><span class="sxs-lookup"><span data-stu-id="979d0-154">Value</span></span>      | <span data-ttu-id="979d0-155">種類</span><span class="sxs-lookup"><span data-stu-id="979d0-155">Type</span></span>   | <span data-ttu-id="979d0-156">説明</span><span class="sxs-lookup"><span data-stu-id="979d0-156">Description</span></span>                                                                                                                                                                                                                                                                         |
|------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="979d0-157">status</span><span class="sxs-lookup"><span data-stu-id="979d0-157">status</span></span>           | <span data-ttu-id="979d0-158">string</span><span class="sxs-lookup"><span data-stu-id="979d0-158">string</span></span>  | <span data-ttu-id="979d0-159">申請の状態。</span><span class="sxs-lookup"><span data-stu-id="979d0-159">The status of the submission.</span></span> <span data-ttu-id="979d0-160">次のいずれかの値を使用できます。</span><span class="sxs-lookup"><span data-stu-id="979d0-160">This can be one of the following values:</span></span> <ul><li><span data-ttu-id="979d0-161">なし</span><span class="sxs-lookup"><span data-stu-id="979d0-161">None</span></span></li><li><span data-ttu-id="979d0-162">Canceled</span><span class="sxs-lookup"><span data-stu-id="979d0-162">Canceled</span></span></li><li><span data-ttu-id="979d0-163">PendingCommit</span><span class="sxs-lookup"><span data-stu-id="979d0-163">PendingCommit</span></span></li><li><span data-ttu-id="979d0-164">CommitStarted</span><span class="sxs-lookup"><span data-stu-id="979d0-164">CommitStarted</span></span></li><li><span data-ttu-id="979d0-165">CommitFailed</span><span class="sxs-lookup"><span data-stu-id="979d0-165">CommitFailed</span></span></li><li><span data-ttu-id="979d0-166">PendingPublication</span><span class="sxs-lookup"><span data-stu-id="979d0-166">PendingPublication</span></span></li><li><span data-ttu-id="979d0-167">公開</span><span class="sxs-lookup"><span data-stu-id="979d0-167">Publishing</span></span></li><li><span data-ttu-id="979d0-168">公開済み</span><span class="sxs-lookup"><span data-stu-id="979d0-168">Published</span></span></li><li><span data-ttu-id="979d0-169">PublishFailed</span><span class="sxs-lookup"><span data-stu-id="979d0-169">PublishFailed</span></span></li><li><span data-ttu-id="979d0-170">PreProcessing</span><span class="sxs-lookup"><span data-stu-id="979d0-170">PreProcessing</span></span></li><li><span data-ttu-id="979d0-171">PreProcessingFailed</span><span class="sxs-lookup"><span data-stu-id="979d0-171">PreProcessingFailed</span></span></li><li><span data-ttu-id="979d0-172">認定</span><span class="sxs-lookup"><span data-stu-id="979d0-172">Certification</span></span></li><li><span data-ttu-id="979d0-173">CertificationFailed</span><span class="sxs-lookup"><span data-stu-id="979d0-173">CertificationFailed</span></span></li><li><span data-ttu-id="979d0-174">リリース</span><span class="sxs-lookup"><span data-stu-id="979d0-174">Release</span></span></li><li><span data-ttu-id="979d0-175">ReleaseFailed</span><span class="sxs-lookup"><span data-stu-id="979d0-175">ReleaseFailed</span></span></li></ul>  |

## <a name="error-codes"></a><span data-ttu-id="979d0-176">エラー コード</span><span class="sxs-lookup"><span data-stu-id="979d0-176">Error codes</span></span>

<span data-ttu-id="979d0-177">要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。</span><span class="sxs-lookup"><span data-stu-id="979d0-177">If the request cannot be successfully completed, the response will contain one of the following HTTP error codes.</span></span>

| <span data-ttu-id="979d0-178">エラー コード</span><span class="sxs-lookup"><span data-stu-id="979d0-178">Error code</span></span> |  <span data-ttu-id="979d0-179">説明</span><span class="sxs-lookup"><span data-stu-id="979d0-179">Description</span></span>   |
|--------|------------------|
| <span data-ttu-id="979d0-180">400</span><span class="sxs-lookup"><span data-stu-id="979d0-180">400</span></span>  | <span data-ttu-id="979d0-181">要求パラメーターが有効ではありません。</span><span class="sxs-lookup"><span data-stu-id="979d0-181">The request parameters are invalid.</span></span> |
| <span data-ttu-id="979d0-182">404</span><span class="sxs-lookup"><span data-stu-id="979d0-182">404</span></span>  | <span data-ttu-id="979d0-183">指定した申請は見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="979d0-183">The specified submission could not be found.</span></span> |
| <span data-ttu-id="979d0-184">409</span><span class="sxs-lookup"><span data-stu-id="979d0-184">409</span></span>  | <span data-ttu-id="979d0-185">指定した送信が見つかりましたが、現在の状態で、コミットできなかったまたは、アプリはパートナー センター機能を使用する[現在サポートされていません、Microsoft Store 送信 API](create-and-manage-submissions-using-windows-store-services.md#not_supported)します。</span><span class="sxs-lookup"><span data-stu-id="979d0-185">The specified submission was found but it could not be committed in its current state, or the app uses a Partner Center feature that is [currently not supported by the Microsoft Store submission API](create-and-manage-submissions-using-windows-store-services.md#not_supported).</span></span> |

## <a name="related-topics"></a><span data-ttu-id="979d0-186">関連トピック</span><span class="sxs-lookup"><span data-stu-id="979d0-186">Related topics</span></span>

* [<span data-ttu-id="979d0-187">作成し、Microsoft Store サービスを使用して送信の管理</span><span class="sxs-lookup"><span data-stu-id="979d0-187">Create and manage submissions using Microsoft Store services</span></span>](create-and-manage-submissions-using-windows-store-services.md)
* [<span data-ttu-id="979d0-188">アプリの提出を取得します。</span><span class="sxs-lookup"><span data-stu-id="979d0-188">Get an app submission</span></span>](get-an-app-submission.md)
* [<span data-ttu-id="979d0-189">アプリの提出を作成します。</span><span class="sxs-lookup"><span data-stu-id="979d0-189">Create an app submission</span></span>](create-an-app-submission.md)
* [<span data-ttu-id="979d0-190">アプリの提出を更新します。</span><span class="sxs-lookup"><span data-stu-id="979d0-190">Update an app submission</span></span>](update-an-app-submission.md)
* [<span data-ttu-id="979d0-191">アプリの提出を削除します。</span><span class="sxs-lookup"><span data-stu-id="979d0-191">Delete an app submission</span></span>](delete-an-app-submission.md)
* [<span data-ttu-id="979d0-192">アプリの送信の状態を取得します。</span><span class="sxs-lookup"><span data-stu-id="979d0-192">Get the status of an app submission</span></span>](get-status-for-an-app-submission.md)
