---
description: Microsoft Store analytics API でこのメソッドを使用すると、お客様のデスクトップ アプリケーションの insights のデータを取得できます。
title: デスクトップ アプリケーションのインサイト データの取得
ms.date: 07/31/2018
ms.topic: article
keywords: windows 10、uwp、Store services、Microsoft Store analytics API、insights
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 8f6f4b2df1cda14bc1f363a1f9100e416f26489b
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372463"
---
# <a name="get-insights-data-for-your-desktop-application"></a><span data-ttu-id="f86b9-104">デスクトップ アプリケーションのインサイト データの取得</span><span class="sxs-lookup"><span data-stu-id="f86b9-104">Get insights data for your desktop application</span></span>

<span data-ttu-id="f86b9-105">Insights データを取得するには、Microsoft Store analytics API では、このメソッドに関連する正常性メトリックを追加したデスクトップ アプリケーションを使用して、 [Windows デスクトップ アプリケーション プログラム](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-105">Use this method in the Microsoft Store analytics API to get insights data related to health metrics for a desktop application that you have added to the [Windows Desktop Application program](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program).</span></span> <span data-ttu-id="f86b9-106">このデータも記載されて、[正常性レポート](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program#health-report)パートナー センターでのデスクトップ アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="f86b9-106">This data is also available in the [Health report](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program#health-report) for desktop applications in Partner Center.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f86b9-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="f86b9-107">Prerequisites</span></span>

<span data-ttu-id="f86b9-108">このメソッドを使うには、最初に次の作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f86b9-108">To use this method, you need to first do the following:</span></span>

* <span data-ttu-id="f86b9-109">Microsoft Store 分析 API に関するすべての[前提条件](access-analytics-data-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。</span><span class="sxs-lookup"><span data-stu-id="f86b9-109">If you have not done so already, complete all the [prerequisites](access-analytics-data-using-windows-store-services.md#prerequisites) for the Microsoft Store analytics API.</span></span>
* <span data-ttu-id="f86b9-110">このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-110">[Obtain an Azure AD access token](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token) to use in the request header for this method.</span></span> <span data-ttu-id="f86b9-111">アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。</span><span class="sxs-lookup"><span data-stu-id="f86b9-111">After you obtain an access token, you have 60 minutes to use it before it expires.</span></span> <span data-ttu-id="f86b9-112">トークンの有効期限が切れたら新しいトークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="f86b9-112">After the token expires, you can obtain a new one.</span></span>

## <a name="request"></a><span data-ttu-id="f86b9-113">要求</span><span class="sxs-lookup"><span data-stu-id="f86b9-113">Request</span></span>


### <a name="request-syntax"></a><span data-ttu-id="f86b9-114">要求の構文</span><span class="sxs-lookup"><span data-stu-id="f86b9-114">Request syntax</span></span>

| <span data-ttu-id="f86b9-115">メソッド</span><span class="sxs-lookup"><span data-stu-id="f86b9-115">Method</span></span> | <span data-ttu-id="f86b9-116">要求 URI</span><span class="sxs-lookup"><span data-stu-id="f86b9-116">Request URI</span></span>       |
|--------|----------------------|
| <span data-ttu-id="f86b9-117">GET</span><span class="sxs-lookup"><span data-stu-id="f86b9-117">GET</span></span>    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/insights``` |


### <a name="request-header"></a><span data-ttu-id="f86b9-118">要求ヘッダー</span><span class="sxs-lookup"><span data-stu-id="f86b9-118">Request header</span></span>

| <span data-ttu-id="f86b9-119">Header</span><span class="sxs-lookup"><span data-stu-id="f86b9-119">Header</span></span>        | <span data-ttu-id="f86b9-120">種類</span><span class="sxs-lookup"><span data-stu-id="f86b9-120">Type</span></span>   | <span data-ttu-id="f86b9-121">説明</span><span class="sxs-lookup"><span data-stu-id="f86b9-121">Description</span></span>                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| <span data-ttu-id="f86b9-122">Authorization</span><span class="sxs-lookup"><span data-stu-id="f86b9-122">Authorization</span></span> | <span data-ttu-id="f86b9-123">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-123">string</span></span> | <span data-ttu-id="f86b9-124">必須。</span><span class="sxs-lookup"><span data-stu-id="f86b9-124">Required.</span></span> <span data-ttu-id="f86b9-125">**Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。</span><span class="sxs-lookup"><span data-stu-id="f86b9-125">The Azure AD access token in the form **Bearer** &lt;*token*&gt;.</span></span> |


### <a name="request-parameters"></a><span data-ttu-id="f86b9-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="f86b9-126">Request parameters</span></span>

| <span data-ttu-id="f86b9-127">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f86b9-127">Parameter</span></span>        | <span data-ttu-id="f86b9-128">種類</span><span class="sxs-lookup"><span data-stu-id="f86b9-128">Type</span></span>   |  <span data-ttu-id="f86b9-129">説明</span><span class="sxs-lookup"><span data-stu-id="f86b9-129">Description</span></span>      |  <span data-ttu-id="f86b9-130">必須</span><span class="sxs-lookup"><span data-stu-id="f86b9-130">Required</span></span>  
|---------------|--------|---------------|------|
| <span data-ttu-id="f86b9-131">applicationId</span><span class="sxs-lookup"><span data-stu-id="f86b9-131">applicationId</span></span> | <span data-ttu-id="f86b9-132">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-132">string</span></span> | <span data-ttu-id="f86b9-133">Insights のデータを取得するデスクトップ アプリケーションの製品の ID。</span><span class="sxs-lookup"><span data-stu-id="f86b9-133">The product ID of the desktop application for which you want to get insights data.</span></span> <span data-ttu-id="f86b9-134">デスクトップ アプリケーションの製品 ID を取得するには、いずれかを開く[analytics は、パートナー センターでデスクトップ アプリケーションのレポート](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)(など、**正常性レポート**) し、URL から、製品 ID を取得します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-134">To get the product ID of a desktop application, open any [analytics report for your desktop application in Partner Center](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program) (such as the **Health report**) and retrieve the product ID from the URL.</span></span> <span data-ttu-id="f86b9-135">このパラメーターを指定しないと、応答本文は、自分のアカウントに登録されているすべてのアプリの insights のデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f86b9-135">If you do not specify this parameter, the response body will contain insights data for all apps registered to your account.</span></span>  |  <span data-ttu-id="f86b9-136">X</span><span class="sxs-lookup"><span data-stu-id="f86b9-136">No</span></span>  |
| <span data-ttu-id="f86b9-137">startDate</span><span class="sxs-lookup"><span data-stu-id="f86b9-137">startDate</span></span> | <span data-ttu-id="f86b9-138">date</span><span class="sxs-lookup"><span data-stu-id="f86b9-138">date</span></span> | <span data-ttu-id="f86b9-139">取得する insights データの日付範囲の開始日。</span><span class="sxs-lookup"><span data-stu-id="f86b9-139">The start date in the date range of insights data to retrieve.</span></span> <span data-ttu-id="f86b9-140">既定値は、現在の日付の 30 日前です。</span><span class="sxs-lookup"><span data-stu-id="f86b9-140">The default is 30 days before the current date.</span></span> |  <span data-ttu-id="f86b9-141">X</span><span class="sxs-lookup"><span data-stu-id="f86b9-141">No</span></span>  |
| <span data-ttu-id="f86b9-142">endDate</span><span class="sxs-lookup"><span data-stu-id="f86b9-142">endDate</span></span> | <span data-ttu-id="f86b9-143">date</span><span class="sxs-lookup"><span data-stu-id="f86b9-143">date</span></span> | <span data-ttu-id="f86b9-144">取得する insights データの日付範囲の終了日。</span><span class="sxs-lookup"><span data-stu-id="f86b9-144">The end date in the date range of insights data to retrieve.</span></span> <span data-ttu-id="f86b9-145">既定値は現在の日付です。</span><span class="sxs-lookup"><span data-stu-id="f86b9-145">The default is the current date.</span></span> |  <span data-ttu-id="f86b9-146">X</span><span class="sxs-lookup"><span data-stu-id="f86b9-146">No</span></span>  |
| <span data-ttu-id="f86b9-147">filter</span><span class="sxs-lookup"><span data-stu-id="f86b9-147">filter</span></span> | <span data-ttu-id="f86b9-148">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-148">string</span></span>  | <span data-ttu-id="f86b9-149">応答内の行をフィルター処理する 1 つまたは複数のステートメントです。</span><span class="sxs-lookup"><span data-stu-id="f86b9-149">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="f86b9-150">各ステートメントには、応答本文からのフィールド名、および **eq** 演算子または **ne** 演算子と関連付けられる値が含まれており、**and** や **or** を使用してステートメントを組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="f86b9-150">Each statement contains a field name from the response body and value that are associated with the **eq** or **ne** operators, and statements can be combined using **and** or **or**.</span></span> <span data-ttu-id="f86b9-151">*filter* パラメーターでは、文字列値を単一引用符で囲む必要があります。</span><span class="sxs-lookup"><span data-stu-id="f86b9-151">String values must be surrounded by single quotes in the *filter* parameter.</span></span> <span data-ttu-id="f86b9-152">たとえば、*フィルター = データ型 eq '買収'* します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-152">For example, *filter=dataType eq 'acquisition'*.</span></span> <p/><p/><span data-ttu-id="f86b9-153">現在このメソッドは、フィルターのみをサポート**ヘルス**します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-153">Currently this method only supports the filter **health**.</span></span>  | <span data-ttu-id="f86b9-154">X</span><span class="sxs-lookup"><span data-stu-id="f86b9-154">No</span></span>   |

### <a name="request-example"></a><span data-ttu-id="f86b9-155">要求の例</span><span class="sxs-lookup"><span data-stu-id="f86b9-155">Request example</span></span>

<span data-ttu-id="f86b9-156">次の例では、insights データを取得するための要求を示します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-156">The following example demonstrates a request for getting insights data.</span></span> <span data-ttu-id="f86b9-157">置換、 *applicationId*デスクトップ アプリケーションの適切な値を持つ値。</span><span class="sxs-lookup"><span data-stu-id="f86b9-157">Replace the *applicationId* value with the appropriate value for your desktop application.</span></span>

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/insights?applicationId=10238467886765136388&startDate=6/1/2018&endDate=6/15/2018&filter=dataType eq 'health' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a><span data-ttu-id="f86b9-158">応答</span><span class="sxs-lookup"><span data-stu-id="f86b9-158">Response</span></span>

### <a name="response-body"></a><span data-ttu-id="f86b9-159">応答本文</span><span class="sxs-lookup"><span data-stu-id="f86b9-159">Response body</span></span>

| <span data-ttu-id="f86b9-160">Value</span><span class="sxs-lookup"><span data-stu-id="f86b9-160">Value</span></span>      | <span data-ttu-id="f86b9-161">種類</span><span class="sxs-lookup"><span data-stu-id="f86b9-161">Type</span></span>   | <span data-ttu-id="f86b9-162">説明</span><span class="sxs-lookup"><span data-stu-id="f86b9-162">Description</span></span>                  |
|------------|--------|-------------------------------------------------------|
| <span data-ttu-id="f86b9-163">Value</span><span class="sxs-lookup"><span data-stu-id="f86b9-163">Value</span></span>      | <span data-ttu-id="f86b9-164">array</span><span class="sxs-lookup"><span data-stu-id="f86b9-164">array</span></span>  | <span data-ttu-id="f86b9-165">アプリの insights のデータを格納するオブジェクトの配列。</span><span class="sxs-lookup"><span data-stu-id="f86b9-165">An array of objects that contain insights data for the app.</span></span> <span data-ttu-id="f86b9-166">各オブジェクトのデータの詳細については、次を参照してください。、 [Insight 値](#insight-values)以下のセクション。</span><span class="sxs-lookup"><span data-stu-id="f86b9-166">For more information about the data in each object, see the [Insight values](#insight-values) section below.</span></span>                                                                                                                      |
| <span data-ttu-id="f86b9-167">TotalCount</span><span class="sxs-lookup"><span data-stu-id="f86b9-167">TotalCount</span></span> | <span data-ttu-id="f86b9-168">int</span><span class="sxs-lookup"><span data-stu-id="f86b9-168">int</span></span>    | <span data-ttu-id="f86b9-169">クエリの結果データ内の行の総数です。</span><span class="sxs-lookup"><span data-stu-id="f86b9-169">The total number of rows in the data result for the query.</span></span>                 |


### <a name="insight-values"></a><span data-ttu-id="f86b9-170">Insight 値</span><span class="sxs-lookup"><span data-stu-id="f86b9-170">Insight values</span></span>

<span data-ttu-id="f86b9-171">*Value* 配列の要素には、次の値が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f86b9-171">Elements in the *Value* array contain the following values.</span></span>

| <span data-ttu-id="f86b9-172">Value</span><span class="sxs-lookup"><span data-stu-id="f86b9-172">Value</span></span>               | <span data-ttu-id="f86b9-173">種類</span><span class="sxs-lookup"><span data-stu-id="f86b9-173">Type</span></span>   | <span data-ttu-id="f86b9-174">説明</span><span class="sxs-lookup"><span data-stu-id="f86b9-174">Description</span></span>                           |
|---------------------|--------|-------------------------------------------|
| <span data-ttu-id="f86b9-175">applicationId</span><span class="sxs-lookup"><span data-stu-id="f86b9-175">applicationId</span></span>       | <span data-ttu-id="f86b9-176">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-176">string</span></span> | <span data-ttu-id="f86b9-177">Insights のデータを取得し、デスクトップ アプリケーションの製品の ID。</span><span class="sxs-lookup"><span data-stu-id="f86b9-177">The product ID of the desktop application for which you retrieved insights data.</span></span>     |
| <span data-ttu-id="f86b9-178">insightDate</span><span class="sxs-lookup"><span data-stu-id="f86b9-178">insightDate</span></span>                | <span data-ttu-id="f86b9-179">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-179">string</span></span> | <span data-ttu-id="f86b9-180">日付が特定のメトリックの変化を特定しました。</span><span class="sxs-lookup"><span data-stu-id="f86b9-180">The date on which we identified the change in a specific metric.</span></span> <span data-ttu-id="f86b9-181">この日付は、大幅な増加を検出しました週の終わりを表すと比較する前に、その週とメトリックに増減します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-181">This date represents the end of the week in which we detected a significant increase or decrease in a metric compared to the week before that.</span></span> |
| <span data-ttu-id="f86b9-182">データ型</span><span class="sxs-lookup"><span data-stu-id="f86b9-182">dataType</span></span>     | <span data-ttu-id="f86b9-183">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-183">string</span></span> | <span data-ttu-id="f86b9-184">この情報に通知する一般的な分析の領域を指定する文字列。</span><span class="sxs-lookup"><span data-stu-id="f86b9-184">A string that specifies the general analytics area that this insight informs.</span></span> <span data-ttu-id="f86b9-185">現時点では、このメソッドは**ヘルス**します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-185">Currently, this method only supports **health**.</span></span>    |
| <span data-ttu-id="f86b9-186">insightDetail</span><span class="sxs-lookup"><span data-stu-id="f86b9-186">insightDetail</span></span>          | <span data-ttu-id="f86b9-187">array</span><span class="sxs-lookup"><span data-stu-id="f86b9-187">array</span></span> | <span data-ttu-id="f86b9-188">1 つまたは複数[InsightDetail 値](#insightdetail-values)現在インサイトの詳細を表します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-188">One or more [InsightDetail values](#insightdetail-values) that represent the details for current insight.</span></span>    |


### <a name="insightdetail-values"></a><span data-ttu-id="f86b9-189">InsightDetail 値</span><span class="sxs-lookup"><span data-stu-id="f86b9-189">InsightDetail values</span></span>

| <span data-ttu-id="f86b9-190">Value</span><span class="sxs-lookup"><span data-stu-id="f86b9-190">Value</span></span>               | <span data-ttu-id="f86b9-191">種類</span><span class="sxs-lookup"><span data-stu-id="f86b9-191">Type</span></span>   | <span data-ttu-id="f86b9-192">説明</span><span class="sxs-lookup"><span data-stu-id="f86b9-192">Description</span></span>                           |
|---------------------|--------|-------------------------------------------|
| <span data-ttu-id="f86b9-193">FactName</span><span class="sxs-lookup"><span data-stu-id="f86b9-193">FactName</span></span>           | <span data-ttu-id="f86b9-194">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-194">string</span></span> | <span data-ttu-id="f86b9-195">現在 insight または現在のディメンションについて説明するメトリックを示す文字列。</span><span class="sxs-lookup"><span data-stu-id="f86b9-195">A string that indicates the metric that the current insight or current dimension describes.</span></span> <span data-ttu-id="f86b9-196">現時点では、このメソッドは、値のみをサポート**ヒット カウント**します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-196">Currently, this method only supports the value **HitCount**.</span></span>  |
| <span data-ttu-id="f86b9-197">SubDimensions</span><span class="sxs-lookup"><span data-stu-id="f86b9-197">SubDimensions</span></span>         | <span data-ttu-id="f86b9-198">array</span><span class="sxs-lookup"><span data-stu-id="f86b9-198">array</span></span> |  <span data-ttu-id="f86b9-199">情報を得ることの 1 つのメトリックを記述する 1 つまたは複数のオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="f86b9-199">One or more objects that describe a single metric for the insight.</span></span>   |
| <span data-ttu-id="f86b9-200">PercentChange</span><span class="sxs-lookup"><span data-stu-id="f86b9-200">PercentChange</span></span>            | <span data-ttu-id="f86b9-201">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-201">string</span></span> |  <span data-ttu-id="f86b9-202">この割合は、全体の顧客ベースでメトリックを変更しました。</span><span class="sxs-lookup"><span data-stu-id="f86b9-202">The percentage that the metric changed across your entire customer base.</span></span>  |
| <span data-ttu-id="f86b9-203">DimensionName</span><span class="sxs-lookup"><span data-stu-id="f86b9-203">DimensionName</span></span>           | <span data-ttu-id="f86b9-204">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-204">string</span></span> |  <span data-ttu-id="f86b9-205">現在のディメンションで説明されているメトリックの名前。</span><span class="sxs-lookup"><span data-stu-id="f86b9-205">The name of the metric described in the current dimension.</span></span> <span data-ttu-id="f86b9-206">例としては、 **EventType**、**市場**、 **DeviceType**、および**PackageVersion**します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-206">Examples include **EventType**, **Market**, **DeviceType**, and **PackageVersion**.</span></span>   |
| <span data-ttu-id="f86b9-207">DimensionValue</span><span class="sxs-lookup"><span data-stu-id="f86b9-207">DimensionValue</span></span>              | <span data-ttu-id="f86b9-208">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-208">string</span></span> | <span data-ttu-id="f86b9-209">現在のディメンションで説明されているメトリックの値。</span><span class="sxs-lookup"><span data-stu-id="f86b9-209">The value of the metric that is described in the current dimension.</span></span> <span data-ttu-id="f86b9-210">たとえば場合、 **DimensionName**は**EventType**、 **DimensionValue**可能性があります**クラッシュ**または**ハング**.</span><span class="sxs-lookup"><span data-stu-id="f86b9-210">For example, if **DimensionName** is **EventType**, **DimensionValue** might be **crash** or **hang**.</span></span>   |
| <span data-ttu-id="f86b9-211">FactValue</span><span class="sxs-lookup"><span data-stu-id="f86b9-211">FactValue</span></span>     | <span data-ttu-id="f86b9-212">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-212">string</span></span> | <span data-ttu-id="f86b9-213">情報を得ることが検出された日付のメトリックの絶対値。</span><span class="sxs-lookup"><span data-stu-id="f86b9-213">The absolute value of the metric on the date the insight was detected.</span></span>  |
| <span data-ttu-id="f86b9-214">Direction</span><span class="sxs-lookup"><span data-stu-id="f86b9-214">Direction</span></span> | <span data-ttu-id="f86b9-215">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-215">string</span></span> |  <span data-ttu-id="f86b9-216">変更の方向 (**正**または**負**)。</span><span class="sxs-lookup"><span data-stu-id="f86b9-216">The direction of the change (**Positive** or **Negative**).</span></span>   |
| <span data-ttu-id="f86b9-217">日付</span><span class="sxs-lookup"><span data-stu-id="f86b9-217">Date</span></span>              | <span data-ttu-id="f86b9-218">string</span><span class="sxs-lookup"><span data-stu-id="f86b9-218">string</span></span> |  <span data-ttu-id="f86b9-219">日付、現在の情報または現在のディメンションに関連する変更を特定しました。</span><span class="sxs-lookup"><span data-stu-id="f86b9-219">The date on which we identified the change related to the current insight or the current dimension.</span></span>   |

### <a name="response-example"></a><span data-ttu-id="f86b9-220">応答の例</span><span class="sxs-lookup"><span data-stu-id="f86b9-220">Response example</span></span>

<span data-ttu-id="f86b9-221">この要求の JSON 返信の本文の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="f86b9-221">The following example demonstrates an example JSON response body for this request.</span></span>

```json
{
  "Value": [
    {
      "applicationId": "9NBLGGGZ5QDR",
      "insightDate": "2018-06-03T00:00:00",
      "dataType": "health",
      "insightDetail": [
        {
          "FactName": "HitCount",
          "SubDimensions": [
            {
              "FactName:": "HitCount",
              "PercentChange": "21",
              "DimensionValue:": "DE",
              "FactValue": "109",
              "Direction": "Positive",
              "Date": "6/3/2018 12:00:00 AM",
              "DimensionName": "Market"
            }
          ],
          "DimensionValue": "crash",
          "Date": "6/3/2018 12:00:00 AM",
          "DimensionName": "EventType"
        },
        {
          "FactName": "HitCount",
          "SubDimensions": [
            {
              "FactName:": "HitCount",
              "PercentChange": "71",
              "DimensionValue:": "JP",
              "FactValue": "112",
              "Direction": "Positive",
              "Date": "6/3/2018 12:00:00 AM",
              "DimensionName": "Market"
            }
          ],
          "DimensionValue": "hang",
          "Date": "6/3/2018 12:00:00 AM",
          "DimensionName": "EventType"
        },
      ],
      "insightId": "9CY0F3VBT1AS942AFQaeyO0k2zUKfyOhrOHc0036Iwc="
    }
  ],
  "@nextLink": null,
  "TotalCount": 2
}
```

## <a name="related-topics"></a><span data-ttu-id="f86b9-222">関連トピック</span><span class="sxs-lookup"><span data-stu-id="f86b9-222">Related topics</span></span>

* [<span data-ttu-id="f86b9-223">Windows デスクトップ アプリケーション プログラム</span><span class="sxs-lookup"><span data-stu-id="f86b9-223">Windows Desktop Application program</span></span>](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
* [<span data-ttu-id="f86b9-224">正常性レポート</span><span class="sxs-lookup"><span data-stu-id="f86b9-224">Health report</span></span>](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program#health-report)
* [<span data-ttu-id="f86b9-225">Microsoft Store サービスを使用して分析データにアクセス</span><span class="sxs-lookup"><span data-stu-id="f86b9-225">Access analytics data using Microsoft Store services</span></span>](access-analytics-data-using-windows-store-services.md)
