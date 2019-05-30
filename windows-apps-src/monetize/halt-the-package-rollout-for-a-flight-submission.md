---
description: パッケージ フライトに関するパッケージのロールアウトを停止するには、Microsoft Store 申請 API の以下のメソッドを使います。
title: フライトに関するロールアウトを停止する
ms.date: 04/17/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, パッケージのロールアウト, フライトの申請, 停止
ms.assetid: f8ee0687-a421-48e7-a6eb-3fd5633c352b
ms.localizationpriority: medium
ms.openlocfilehash: 43b721a608996b904d6c68b7db350490d77755dc
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372698"
---
# <a name="halt-the-rollout-for-a-flight"></a><span data-ttu-id="15df9-104">フライトに関するロールアウトを停止する</span><span class="sxs-lookup"><span data-stu-id="15df9-104">Halt the rollout for a flight</span></span>

<span data-ttu-id="15df9-105">パッケージ フライトの申請に関する[ロールアウトを停止する](../publish/gradual-package-rollout.md#completing-the-rollout)には、Microsoft Store 申請 API に含まれる以下のメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="15df9-105">Use this method in the Microsoft Store submission API to [halt the rollout](../publish/gradual-package-rollout.md#completing-the-rollout) for a package flight submission.</span></span> <span data-ttu-id="15df9-106">Microsoft Store 申請 API を使ったパッケージ フライトの申請の作成プロセスについて詳しくは、「[パッケージ フライトの申請の管理](manage-flight-submissions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="15df9-106">For more information about the process of process of creating a package flight submission by using the Microsoft Store submission API, see [Manage package flight submissions](manage-flight-submissions.md).</span></span>

> [!NOTE]
> <span data-ttu-id="15df9-107">パッケージ フライトの申請に関するロールアウトを停止してから、[新しいパッケージ フライトの申請を作成する](create-a-flight-submission.md)場合、新しい申請は停止した申請を複製したものになります。</span><span class="sxs-lookup"><span data-stu-id="15df9-107">If you halt the rollout for a package flight submission and then [create a new package flight submission](create-a-flight-submission.md), the new submission is a clone of the halted submission.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15df9-108">前提条件</span><span class="sxs-lookup"><span data-stu-id="15df9-108">Prerequisites</span></span>

<span data-ttu-id="15df9-109">このメソッドを使うには、最初に次の作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="15df9-109">To use this method, you need to first do the following:</span></span>

* <span data-ttu-id="15df9-110">Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。</span><span class="sxs-lookup"><span data-stu-id="15df9-110">If you have not done so already, complete all the [prerequisites](create-and-manage-submissions-using-windows-store-services.md#prerequisites) for the Microsoft Store submission API.</span></span>
* <span data-ttu-id="15df9-111">このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。</span><span class="sxs-lookup"><span data-stu-id="15df9-111">[Obtain an Azure AD access token](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token) to use in the request header for this method.</span></span> <span data-ttu-id="15df9-112">アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。</span><span class="sxs-lookup"><span data-stu-id="15df9-112">After you obtain an access token, you have 60 minutes to use it before it expires.</span></span> <span data-ttu-id="15df9-113">トークンの有効期限が切れたら新しいトークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="15df9-113">After the token expires, you can obtain a new one.</span></span>
* <span data-ttu-id="15df9-114">アプリのいずれかの提出を作成します。</span><span class="sxs-lookup"><span data-stu-id="15df9-114">Create a submission for one of your apps.</span></span> <span data-ttu-id="15df9-115">パートナー センターでこれを行うかを使用してこれを行う、[アプリの提出を作成](create-an-app-submission.md)メソッド。</span><span class="sxs-lookup"><span data-stu-id="15df9-115">You can do this in Partner Center, or you can do this by using the [create an app submission](create-an-app-submission.md) method.</span></span>
* <span data-ttu-id="15df9-116">申請に関する段階的なパッケージのロールアウトを有効にします。</span><span class="sxs-lookup"><span data-stu-id="15df9-116">Enable a gradual package rollout for the submission.</span></span> <span data-ttu-id="15df9-117">これを行うことができます[パートナー センターで](../publish/gradual-package-rollout.md)、これを行うまたは[Microsoft Store 送信 API を使用して](manage-flight-submissions.md#manage-gradual-package-rollout)します。</span><span class="sxs-lookup"><span data-stu-id="15df9-117">You can do this [in Partner Center](../publish/gradual-package-rollout.md), or you can do this by [using the Microsoft Store submission API](manage-flight-submissions.md#manage-gradual-package-rollout).</span></span>

## <a name="request"></a><span data-ttu-id="15df9-118">要求</span><span class="sxs-lookup"><span data-stu-id="15df9-118">Request</span></span>

<span data-ttu-id="15df9-119">このメソッドの構文は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="15df9-119">This method has the following syntax.</span></span> <span data-ttu-id="15df9-120">ヘッダーと要求のパラメーターの使用例と説明については、以下のセクションをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="15df9-120">See the following sections for usage examples and descriptions of the header and request parameters.</span></span>

| <span data-ttu-id="15df9-121">メソッド</span><span class="sxs-lookup"><span data-stu-id="15df9-121">Method</span></span> | <span data-ttu-id="15df9-122">要求 URI</span><span class="sxs-lookup"><span data-stu-id="15df9-122">Request URI</span></span>                                                      |
|--------|------------------------------------------------------------------|
| <span data-ttu-id="15df9-123">POST</span><span class="sxs-lookup"><span data-stu-id="15df9-123">POST</span></span>   | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/flights/{flightId}/submissions/{submissionId}/haltpackagerollout` |


### <a name="request-header"></a><span data-ttu-id="15df9-124">要求ヘッダー</span><span class="sxs-lookup"><span data-stu-id="15df9-124">Request header</span></span>

| <span data-ttu-id="15df9-125">Header</span><span class="sxs-lookup"><span data-stu-id="15df9-125">Header</span></span>        | <span data-ttu-id="15df9-126">種類</span><span class="sxs-lookup"><span data-stu-id="15df9-126">Type</span></span>   | <span data-ttu-id="15df9-127">説明</span><span class="sxs-lookup"><span data-stu-id="15df9-127">Description</span></span>                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| <span data-ttu-id="15df9-128">Authorization</span><span class="sxs-lookup"><span data-stu-id="15df9-128">Authorization</span></span> | <span data-ttu-id="15df9-129">string</span><span class="sxs-lookup"><span data-stu-id="15df9-129">string</span></span> | <span data-ttu-id="15df9-130">必須。</span><span class="sxs-lookup"><span data-stu-id="15df9-130">Required.</span></span> <span data-ttu-id="15df9-131">**Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。</span><span class="sxs-lookup"><span data-stu-id="15df9-131">The Azure AD access token in the form **Bearer** &lt;*token*&gt;.</span></span> |


### <a name="request-parameters"></a><span data-ttu-id="15df9-132">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="15df9-132">Request parameters</span></span>

| <span data-ttu-id="15df9-133">名前</span><span class="sxs-lookup"><span data-stu-id="15df9-133">Name</span></span>        | <span data-ttu-id="15df9-134">種類</span><span class="sxs-lookup"><span data-stu-id="15df9-134">Type</span></span>   | <span data-ttu-id="15df9-135">説明</span><span class="sxs-lookup"><span data-stu-id="15df9-135">Description</span></span>                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| <span data-ttu-id="15df9-136">applicationId</span><span class="sxs-lookup"><span data-stu-id="15df9-136">applicationId</span></span> | <span data-ttu-id="15df9-137">string</span><span class="sxs-lookup"><span data-stu-id="15df9-137">string</span></span> | <span data-ttu-id="15df9-138">必須。</span><span class="sxs-lookup"><span data-stu-id="15df9-138">Required.</span></span> <span data-ttu-id="15df9-139">停止するパッケージのロールアウトの対象となるパッケージ フライトの申請が含まれているアプリのストア ID です。</span><span class="sxs-lookup"><span data-stu-id="15df9-139">The Store ID of the app that contains the package flight submission with the package rollout you want to halt.</span></span> <span data-ttu-id="15df9-140">ストア ID について詳しくは、「[アプリ ID の詳細の表示](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="15df9-140">For more information about the Store ID, see [View app identity details](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details).</span></span>  |
| <span data-ttu-id="15df9-141">flightId</span><span class="sxs-lookup"><span data-stu-id="15df9-141">flightId</span></span> | <span data-ttu-id="15df9-142">string</span><span class="sxs-lookup"><span data-stu-id="15df9-142">string</span></span> | <span data-ttu-id="15df9-143">必須。</span><span class="sxs-lookup"><span data-stu-id="15df9-143">Required.</span></span> <span data-ttu-id="15df9-144">停止するパッケージのロールアウトの対象となる申請が含まれているパッケージ フライトの ID です。</span><span class="sxs-lookup"><span data-stu-id="15df9-144">The ID of the package flight that contains the submission with the package rollout you want to halt.</span></span> <span data-ttu-id="15df9-145">この ID は、[パッケージ フライトの作成](create-a-flight.md)要求と[アプリのパッケージ フライトの取得](get-flights-for-an-app.md)要求の応答データで確認できます。</span><span class="sxs-lookup"><span data-stu-id="15df9-145">This ID is available in the response data for requests to [create a package flight](create-a-flight.md) and [get package flights for an app](get-flights-for-an-app.md).</span></span> <span data-ttu-id="15df9-146">パートナー センターで作成されたフライトはこの ID はパートナー センターでのフライトのページの URL で使用できるも。</span><span class="sxs-lookup"><span data-stu-id="15df9-146">For a flight that was created in Partner Center, this ID is also available in the URL for the flight page in Partner Center.</span></span>   |
| <span data-ttu-id="15df9-147">submissionId</span><span class="sxs-lookup"><span data-stu-id="15df9-147">submissionId</span></span> | <span data-ttu-id="15df9-148">string</span><span class="sxs-lookup"><span data-stu-id="15df9-148">string</span></span> | <span data-ttu-id="15df9-149">必須。</span><span class="sxs-lookup"><span data-stu-id="15df9-149">Required.</span></span> <span data-ttu-id="15df9-150">停止するパッケージのロールアウトの対象となる申請の ID です。</span><span class="sxs-lookup"><span data-stu-id="15df9-150">The ID of the submission with the package rollout to halt.</span></span> <span data-ttu-id="15df9-151">この ID は、[パッケージ フライトの申請の作成](create-a-flight-submission.md)要求に対する応答データで確認できます。</span><span class="sxs-lookup"><span data-stu-id="15df9-151">This ID is available in the response data for requests to [create a package flight submission](create-a-flight-submission.md).</span></span> <span data-ttu-id="15df9-152">パートナー センターで作成された送信、この ID はパートナー センターでの送信 ページの URL で使用できるも。</span><span class="sxs-lookup"><span data-stu-id="15df9-152">For a submission that was created in Partner Center, this ID is also available in the URL for the submission page in Partner Center.</span></span>  |


### <a name="request-body"></a><span data-ttu-id="15df9-153">要求本文</span><span class="sxs-lookup"><span data-stu-id="15df9-153">Request body</span></span>

<span data-ttu-id="15df9-154">このメソッドでは要求本文を指定しないでください。</span><span class="sxs-lookup"><span data-stu-id="15df9-154">Do not provide a request body for this method.</span></span>

### <a name="request-example"></a><span data-ttu-id="15df9-155">要求の例</span><span class="sxs-lookup"><span data-stu-id="15df9-155">Request example</span></span>

<span data-ttu-id="15df9-156">パッケージ フライトの申請に関するパッケージのロールアウトを停止する方法の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="15df9-156">The following example demonstrates how to halt the package rollout for a package flight submission.</span></span>

```json
POST https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/flights/43e448df-97c9-4a43-a0bc-2a445e736bcd/submissions/1152921504621243680/haltpackagerollout HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a><span data-ttu-id="15df9-157">応答</span><span class="sxs-lookup"><span data-stu-id="15df9-157">Response</span></span>

<span data-ttu-id="15df9-158">次の例は、このメソッドが正常に呼び出された場合の JSON 応答本文を示しています。</span><span class="sxs-lookup"><span data-stu-id="15df9-158">The following example demonstrates the JSON response body for a successful call to this method.</span></span> <span data-ttu-id="15df9-159">応答本文の値について詳しくは、「[パッケージのロールアウトのリソース](manage-flight-submissions.md#package-rollout-object)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="15df9-159">For more details about the values in the response body, see [Package rollout resource](manage-flight-submissions.md#package-rollout-object).</span></span>

```json
{
    "isPackageRollout": true,
    "packageRolloutPercentage": 0.0,
    "packageRolloutStatus": "PackageRolloutStopped",
    "fallbackSubmissionId": "1212922684621243058"
}
```

## <a name="error-codes"></a><span data-ttu-id="15df9-160">エラー コード</span><span class="sxs-lookup"><span data-stu-id="15df9-160">Error codes</span></span>

<span data-ttu-id="15df9-161">要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。</span><span class="sxs-lookup"><span data-stu-id="15df9-161">If the request cannot be successfully completed, the response will contain one of the following HTTP error codes.</span></span>

| <span data-ttu-id="15df9-162">エラー コード</span><span class="sxs-lookup"><span data-stu-id="15df9-162">Error code</span></span> |  <span data-ttu-id="15df9-163">説明</span><span class="sxs-lookup"><span data-stu-id="15df9-163">Description</span></span>   |
|--------|------------------|
| <span data-ttu-id="15df9-164">404</span><span class="sxs-lookup"><span data-stu-id="15df9-164">404</span></span>  | <span data-ttu-id="15df9-165">パッケージ フライトの申請は見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="15df9-165">The package flight submission could not be found.</span></span> |
| <span data-ttu-id="15df9-166">409</span><span class="sxs-lookup"><span data-stu-id="15df9-166">409</span></span>  | <span data-ttu-id="15df9-167">このコードは、次のエラーのいずれかを示します。</span><span class="sxs-lookup"><span data-stu-id="15df9-167">This code indicates one of the following errors:</span></span><br/><br/><ul><li><span data-ttu-id="15df9-168">申請が、段階的なロールアウト操作に対して有効な状態になっていません (このメソッドを呼び出す前に、申請を公開し、[packageRolloutStatus](manage-flight-submissions.md#package-rollout-object) の値を **PackageRolloutInProgress** に設定する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="15df9-168">The submission is not in a valid state for the gradual rollout operation (before calling this method, the submission must be published and the [packageRolloutStatus](manage-flight-submissions.md#package-rollout-object) value must be set to **PackageRolloutInProgress**).</span></span></li><li><span data-ttu-id="15df9-169">申請が、指定されたアプリに属していません。</span><span class="sxs-lookup"><span data-stu-id="15df9-169">The submission does not belong to the specified app.</span></span></li><li><span data-ttu-id="15df9-170">アプリはパートナー センター機能を使用する[現在サポートされていません、Microsoft Store 送信 API](create-and-manage-submissions-using-windows-store-services.md#not_supported)します。</span><span class="sxs-lookup"><span data-stu-id="15df9-170">The app uses a Partner Center feature that is [currently not supported by the Microsoft Store submission API](create-and-manage-submissions-using-windows-store-services.md#not_supported).</span></span></li></ul> |   


## <a name="related-topics"></a><span data-ttu-id="15df9-171">関連トピック</span><span class="sxs-lookup"><span data-stu-id="15df9-171">Related topics</span></span>

* [<span data-ttu-id="15df9-172">パッケージの段階的なロールアウト</span><span class="sxs-lookup"><span data-stu-id="15df9-172">Gradual package rollout</span></span>](../publish/gradual-package-rollout.md)
* [<span data-ttu-id="15df9-173">Microsoft Store 送信 API を使用してパッケージのフライトの送信を管理します。</span><span class="sxs-lookup"><span data-stu-id="15df9-173">Manage package flight submissions using the Microsoft Store submission API</span></span>](manage-flight-submissions.md)
* [<span data-ttu-id="15df9-174">作成し、Microsoft Store サービスを使用して送信の管理</span><span class="sxs-lookup"><span data-stu-id="15df9-174">Create and manage submissions using Microsoft Store services</span></span>](create-and-manage-submissions-using-windows-store-services.md)
