---
ms.assetid: 66400066-24BF-4AF2-B52A-577F5C3CA474
description: Microsoft Store 送信 API でこれらのメソッドを使用すると、パートナー センター アカウントに登録されているアプリ用のサブミッションをアドオンを管理できます。
title: アドオンの申請の管理
ms.date: 04/17/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, アドオンの申請, アプリ内製品, IAP
ms.localizationpriority: medium
ms.openlocfilehash: e6e75483ca6c01958a4b8bda2c5c3bb60e764eff
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372479"
---
# <a name="manage-add-on-submissions"></a>アドオンの申請の管理

Microsoft Store 申請 API には、アプリのアドオン (アプリ内製品または IAP とも呼ばれます) 申請を管理するために使用できるメソッドが用意されています。 Microsoft Store 申請 API の概要については、「[Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)」をご覧ください。この API を使用するための前提条件などの情報があります。

> [!IMPORTANT]
> Microsoft Store 送信 API を使用して、アドオンの提出を作成すると、必ず変更を加える、送信するだけで、パートナー センターで変更を行うのではなく、API を使用してください。 パートナー センターを使用して API を使用して作成した元の送信を変更する場合は、変更、または API を使用して送信をコミットすることはできなくなります。 場合によっては、申請がエラー状態のままになり、申請プロセスを進めることができなくなります。 この場合、申請を削除して新しい申請を作成する必要があります。

<span id="methods-for-add-on-submissions" />

## <a name="methods-for-managing-add-on-submissions"></a>アドオンの申請を管理するためのメソッド

アドオンの申請を取得、作成、更新、コミット、または削除するには、次のメソッドを使用します。 これらのメソッドを使用する前に、アドオンはする必要があります、パートナー センター アカウントに既に存在します。 アドオンを作成するには、パートナー センターで[製品の種類と製品 ID を定義する](../publish/set-your-add-on-product-id.md)で説明されている Microsoft Store の送信 API メソッドを使用してまたは[アドオンを管理する](manage-add-ons.md)します。

<table>
<colgroup>
<col width="10%" />
<col width="30%" />
<col width="60%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メソッド</th>
<th align="left">URI</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}</td>
<td align="left"><a href="get-an-add-on-submission.md">既存のアドオンの送信を取得します。</a></td>
</tr>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}/status</td>
<td align="left"><a href="get-status-for-an-add-on-submission.md">既存のアドオンの送信の状態を取得します。</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions</td>
<td align="left"><a href="create-an-add-on-submission.md">新しいアドオンの提出を作成します。</a></td>
</tr>
<tr>
<td align="left">PUT</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}</td>
<td align="left"><a href="update-an-add-on-submission.md">既存のアドオンの申請を更新します。</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}/commit</td>
<td align="left"><a href="commit-an-add-on-submission.md">コミットを新規または更新済みのアドオンの送信</a></td>
</tr>
<tr>
<td align="left">Del</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}</td>
<td align="left"><a href="delete-an-add-on-submission.md">削除するアドオンの送信</a></td>
</tr>
</tbody>
</table>

<span id="create-an-add-on-submission">

## <a name="create-an-add-on-submission"></a>アドオンの申請の作成

アドオンの申請を作成するには、次のプロセスに従います。

1. まだ行っていないため、完全な前提条件に記載されている[作成 Microsoft Store サービスを使用して送信の管理と](create-and-manage-submissions-using-windows-store-services.md)(パートナー センター アカウントと Azure AD アプリケーションの関連付けを取得するなど)、クライアント ID とキー。 この作業は 1 度行うだけでよく、クライアント ID とキーを入手したら、新しい Azure AD アクセス トークンの作成が必要になったときに、いつでもそれらを再利用できます。  

2. [Azure AD のアクセス トークンを取得します](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)。 このアクセス トークンを Microsoft Store 申請 API のメソッドに渡す必要があります。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

3. Microsoft Store 申請 API の次のメソッドを実行します。 このメソッドによって、新しい申請が作成され、審査中になります。これは、前回発行した申請のコピーです。 詳しくは、「[アドオンの申請の作成](create-an-add-on-submission.md)」をご覧ください。

    ```json
    POST https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions
    ```

    応答本文には、新しい申請の ID、申請用のアドオン アイコンを Azure Blob Storage にアップロードするための共有アクセス署名 (SAS) URI、および新しい申請のためのすべてのデータ (登録情報や料金情報など) を含む[アドオンの申請](#add-on-submission-object) リソースが含まれます。

    > [!NOTE]
    > SAS URI では、アカウント キーを必要とせずに、Azure Storage 内のセキュリティで保護されたリソースにアクセスできます。 SAS URI の背景情報と Azure Blob Storage での SAS URI の使用については、[Shared Access Signature 第 1 部: SAS モデルについて](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1)と[Shared Access Signature、第 2 部。作成し、Blob storage では、SAS を使用して](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/)します。

4. 申請用に新しいアイコンを追加する場合は、[アイコンを準備](https://docs.microsoft.com/windows/uwp/publish/create-iap-descriptions)して、ZIP アーカイブに追加します。

5. 新しい申請用に必要な変更を行って[アドオンの申請](#add-on-submission-object)データを更新し、次のメソッドを実行して申請を更新します。 詳しくは、「[アドオンの申請の更新](update-an-add-on-submission.md)」をご覧ください。

    ```json
    PUT https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}
    ```
      > [!NOTE]
      > 申請用に新しいアイコンを追加する場合、ZIP アーカイブ内のアイコンのファイルの名前と相対パスを参照するように、申請データを更新してください。

4. 申請用に新しいアイコンを追加する場合は、上記で呼び出した POST メソッドの応答本文に含まれていた SAS URI を使用して、ZIP アーカイブを [Azure Blob Storage](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage) にアップロードします。 さまざまなプラットフォームでこれを行うために使用できる、次のようなさまざまな Azure ライブラリがあります。

    * [.NET 用 azure Storage クライアント ライブラリ](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-blobs)
    * [Azure Storage SDK for Java](https://docs.microsoft.com/azure/storage/storage-java-how-to-use-blob-storage)
    * [Azure Storage SDK for Python](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage)

    次の C# コード例は、.NET 用 Azure Storage クライアント ライブラリの [CloudBlockBlob](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?redirectedfrom=MSDN) クラスを使用して ZIP アーカイブを Azure Blob Storage にアップロードする方法を示しています。 この例では、ZIP アーカイブが既にストリーム オブジェクトに書き込まれていることを前提としています。

    ```csharp
    string sasUrl = "https://productingestionbin1.blob.core.windows.net/ingestion/26920f66-b592-4439-9a9d-fb0f014902ec?sv=2014-02-14&sr=b&sig=usAN0kNFNnYE2tGQBI%2BARQWejX1Guiz7hdFtRhyK%2Bog%3D&se=2016-06-17T20:45:51Z&sp=rwl";
    Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob blockBob =
      new Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob(new System.Uri(sasUrl));
    await blockBob.UploadFromStreamAsync(stream);
    ```

5. 次のメソッドを実行して、申請をコミットします。 お客様の提出を終了することと、自分のアカウントに、更新プログラムが適用されるようになりましたことは、パートナー センターが警告されます。 詳しくは、「[アドオンの申請のコミット](commit-an-add-on-submission.md)」をご覧ください。

    ```json
    POST https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}/commit
    ```

6. 次のメソッドを実行して、コミットの状態を確認します。 詳しくは、「[アドオンの申請の状態の取得](get-status-for-an-add-on-submission.md)」をご覧ください。

    ```json
    GET https://manage.devcenter.microsoft.com/v1.0/my/inappproducts/{id}/submissions/{submissionId}/status
    ```

    申請の状態を確認するには、応答本文の *status* の値を確認します。 この値が **CommitStarted** から **PreProcessing** (要求が成功した場合) または **CommitFailed** (要求でエラーが発生した場合) に変わっています。 エラーがある場合は、*statusDetails* フィールドにエラーについての詳細情報が含まれています。

7. コミットが正常に処理されると、インジェストのために申請がストアに送信されます。 前のメソッドを使用するか、パートナー センターにアクセスして、送信進行状況を監視できます。

<span/>

## <a name="code-examples"></a>コード例

次の記事では、さまざまなプログラミング言語でアドオンの申請を作成する方法を説明する詳しいコード例を紹介します。

* [C#コード例](csharp-code-examples-for-the-windows-store-submission-api.md)
* [Java のコード例](java-code-examples-for-the-windows-store-submission-api.md)
* [Python のコード例](python-code-examples-for-the-windows-store-submission-api.md)

## <a name="storebroker-powershell-module"></a>StoreBroker PowerShell モジュール

Microsoft Store 申請 API を直接呼び出す代わりに、API の上にコマンド ライン インターフェイスを実装するオープンソースの PowerShell モジュールも用意されています。 このモジュールは、[StoreBroker](https://aka.ms/storebroker) と呼ばれています。 このモジュールを使うと、Microsoft Store 申請 API を直接呼び出さずに、コマンド ラインからアプリ、フライト、アドオンの申請を管理できます。また、ソースを参照して、この API を呼び出す方法の例を確認することもできます。 StoreBroker モジュールは、多くのファースト パーティ アプリケーションをストアに申請する主要な方法として Microsoft 内で積極的に使っています。

詳しくは、[GitHub の StoreBroker に関するページ](https://aka.ms/storebroker)をご覧ください。

<span/>

## <a name="data-resources"></a>データ リソース

アドオンの申請を管理するための Microsoft Store 申請 API のメソッドでは、次の JSON データ リソースが使われます。

<span id="add-on-submission-object" />

### <a name="add-on-submission-resource"></a>アドオンの申請のリソース

このリソースは、アドオンの申請を記述しています。

```json
{
  "id": "1152921504621243680",
  "contentType": "EMagazine",
  "keywords": [
    "books"
  ],
  "lifetime": "FiveDays",
  "listings": {
    "en": {
      "description": "English add-on description",
      "icon": {
        "fileName": "add-on-en-us-listing2.png",
        "fileStatus": "Uploaded"
      },
      "title": "Add-on Title (English)"
    },
    "ru": {
      "description": "Russian add-on description",
      "icon": {
        "fileName": "add-on-ru-listing.png",
        "fileStatus": "Uploaded"
      },
      "title": "Add-on Title (Russian)"
    }
  },
  "pricing": {
    "marketSpecificPricings": {
      "RU": "Tier3",
      "US": "Tier4",
    },
    "sales": [],
    "priceId": "Free",
    "isAdvancedPricingModel": true
  },
  "targetPublishDate": "2016-03-15T05:10:58.047Z",
  "targetPublishMode": "Immediate",
  "tag": "SampleTag",
  "visibility": "Public",
  "status": "PendingCommit",
  "statusDetails": {
    "errors": [
      {
        "code": "None",
        "details": "string"
      }
    ],
    "warnings": [
      {
        "code": "ListingOptOutWarning",
        "details": "You have removed listing language(s): []"
      }
    ],
    "certificationReports": [
      {
      }
    ]
  },
  "fileUploadUrl": "https://productingestionbin1.blob.core.windows.net/ingestion/26920f66-b592-4439-9a9d-fb0f014902ec?sv=2014-02-14&sr=b&sig=usAN0kNFNnYE2tGQBI%2BARQWejX1Guiz7hdFtRhyK%2Bog%3D&se=2016-06-17T20:45:51Z&sp=rwl",
  "friendlyName": "Submission 2"
}
```

このリソースには、次の値があります。

| Value      | 種類   | 説明        |
|------------|--------|----------------------|
| id            | string  | 申請 ID。 この ID は、[アドオンの申請の作成](create-an-add-on-submission.md)要求、[すべてのアドオンの取得](get-all-add-ons.md)要求、[アドオンの取得](get-an-add-on.md)要求に対する応答データで確認できます。 パートナー センターで作成された送信、この ID はパートナー センターでの送信 ページの URL で使用できるも。  |
| contentType           | string  |  アドオンで提供されている[コンテンツの種類](../publish/enter-add-on-properties.md#content-type)です。 次のいずれかの値を使用できます。 <ul><li>NotSet</li><li>BookDownload</li><li>EMagazine</li><li>ENewspaper</li><li>MusicDownload</li><li>MusicStream</li><li>OnlineDataStorage</li><li>VideoDownload</li><li>VideoStream</li><li>Asp</li><li>OnlineDownload</li></ul> |  
| keywords           | array  | アドオンの[キーワード](../publish/enter-add-on-properties.md#keywords)の文字列を最大 10 個含む配列です。 アプリでは、これらのキーワードを使ってアドオンを照会できます。   |
| lifetime           | string  |  アドオンの有効期間です。 次のいずれかの値を使用できます。 <ul><li>Forever</li><li>OneDay</li><li>ThreeDays</li><li>FiveDays</li><li>OneWeek</li><li>TwoWeeks</li><li>OneMonth</li><li>TwoMonths</li><li>ThreeMonths</li><li>SixMonths</li><li>OneYear</li></ul> |
| listings           | オブジェクト  |  キーと値のペアのディクショナリです。各キーは 2 文字の ISO 3166-1 alpha-2 の国コードで、各値はアドオンの登録情報が保持される[登録情報リソース](#listing-object)です。  |
| pricing           | オブジェクト  | アドオンの価格設定情報が保持される[価格リソース](#pricing-object)です。   |
| targetPublishMode           | string  | 申請の公開モードです。 次のいずれかの値を使用できます。 <ul><li>即時</li><li>Manual</li><li>SpecificDate</li></ul> |
| targetPublishDate           | string  | *targetPublishMode* が SpecificDate に設定されている場合、ISO 8601 形式での申請の公開日です。  |
| tag           | string  |  アドオンの[カスタムの開発者データ](../publish/enter-add-on-properties.md#custom-developer-data)(この情報は従来*タグ*と呼ばれていました)。   |
| visibility  | string  |  アドオンの可視性です。 次のいずれかの値を使用できます。 <ul><li>Hidden</li><li>パブリック</li><li>Private</li><li>NotSet</li></ul>  |
| status  | string  |  申請の状態。 次のいずれかの値を使用できます。 <ul><li>なし</li><li>Canceled</li><li>PendingCommit</li><li>CommitStarted</li><li>CommitFailed</li><li>PendingPublication</li><li>公開</li><li>公開済み</li><li>PublishFailed</li><li>PreProcessing</li><li>PreProcessingFailed</li><li>認定</li><li>CertificationFailed</li><li>リリース</li><li>ReleaseFailed</li></ul>   |
| statusDetails           | オブジェクト  |  エラーに関する情報など、申請のステータスに関する追加情報が保持される[ステータスの詳細に関するリソース](#status-details-object)です。 |
| fileUploadUrl           | string  | 申請のパッケージのアップロードに使用する共有アクセス署名 (SAS) URI です。 申請用に新しいパッケージを追加する場合は、パッケージを含む ZIP アーカイブをこの URI にアップロードします。 詳しくは、「[アドオンの申請の作成](#create-an-add-on-submission)」をご覧ください。  |
| friendlyName  | string  |  パートナー センターで示すように、送信のフレンドリ名。 この値は、申請を作成するときに生成されます。  |

<span id="listing-object" />

### <a name="listing-resource"></a>登録情報リソース

このリソースには[アドオンの登録情報](../publish/create-add-on-store-listings.md)が保持されます。 このリソースには、次の値があります。

| Value           | 種類    | 説明       |
|-----------------|---------|------|
|  description               |    string     |   アドオンの登録情報についての説明です。   |     
|  アイコン●あいこん○               |   オブジェクト      |アドオンの登録情報に使用されるアイコンのデータが保持される[アイコン リソース](#icon-object)です。    |
|  title               |     string    |   アドオンの登録情報のタイトルです。   |  

<span id="icon-object" />

### <a name="icon-resource"></a>アイコン リソース

このリソースにはアドオンの登録情報のアイコン データが保持されます。 このリソースには、次の値があります。

| Value           | 種類    | 説明     |
|-----------------|---------|------|
|  fileName               |    string     |   申請用にアップロードした ZIP アーカイブに含まれているアイコン ファイルの名前です。 このアイコンには、300 x 300 ピクセルの .png ファイルを使用する必要があります。   |     
|  fileStatus               |   string      |  アイコン ファイルの状態です。 次のいずれかの値を使用できます。 <ul><li>なし</li><li>PendingUpload</li><li>Uploaded</li><li>PendingDelete</li></ul>   |

<span id="pricing-object" />

### <a name="pricing-resource"></a>価格リソース

このリソースにはアドオンの価格設定情報が保持されます。 このリソースには、次の値があります。

| Value           | 種類    | 説明    |
|-----------------|---------|------|
|  marketSpecificPricings               |    オブジェクト     |  キーと値のペアのディクショナリです。各キーは 2 文字の ISO 3166-1 alpha-2 の国コードで、各値は[価格帯](#price-tiers)です。 これらの項目は、[特定の市場でのアドオンのカスタム価格](https://docs.microsoft.com/windows/uwp/publish/set-iap-pricing-and-availability)を表します。 このディクショナリに含まれる項目は、指定された市場の *priceId* の値によって指定されている基本価格を上書きします。     |     
|  sales               |   array      |  **推奨されなくなった値**です。 アドオンの販売情報が保持される[セール リソース](#sale-object)の配列です。     |     
|  priceId               |   string      |  アドオンの[基本価格](https://docs.microsoft.com/windows/uwp/publish/set-iap-pricing-and-availability)を規定する[価格帯](#price-tiers)です。    |    
|  isAdvancedPricingModel               |   boolean      |  **true** の場合、開発者アカウントは 0.99 USD ～ 1999.99 USD の拡張された価格セットにアクセスできます。 **false** の場合、開発者アカウントは 0.99 USD ～ 999.99 USD の元の価格帯セットにアクセスできます。 各種価格帯について詳しくは、「[価格帯](#price-tiers)」をご覧ください。<br/><br/>**注**&nbsp;&nbsp;このフィールドは読み取り専用です。   |


<span id="sale-object" />

### <a name="sale-resource"></a>セール リソース

このリソースにはアドオンのセール情報が保持されます。

> [!IMPORTANT]
> **セール** リソースはサポートを終了しました。現在、Microsoft Store 申請 API を使ってアドオンの申請の販売データを取得または変更することはできません。 将来的には、Microsoft Store 申請 API を更新して、アドオンの申請のセール情報にプログラムでアクセスする新しい方法を導入する予定です。
>    * [アドオンの申請を取得する GET メソッド](get-an-add-on-submission.md)を呼び出すと、*セール* リソースは空になります。 パートナー センターを使用して、アドオンの提出の販売データを取得する続行することができます。
>    * [アドオンの申請を更新する PUT メソッド](update-an-add-on-submission.md)を呼び出すとき、*セール*の値に含まれた情報は無視されます。 パートナー センターを使用して、アドオンの提出の販売データを変更する続行することができます。

このリソースには、次の値があります。

| Value           | 種類    | 説明           |
|-----------------|---------|------|
|  name               |    string     |   セールの名前です。    |     
|  basePriceId               |   string      |  セールの基本価格として使用する[価格帯](#price-tiers)です。    |     
|  startDate               |   string      |   ISO 8601 形式で表したセールの開始日です。  |     
|  endDate               |   string      |  ISO 8601 形式で表したセールの終了日です。      |     
|  marketSpecificPricings               |   オブジェクト      |   キーと値のペアのディクショナリです。各キーは 2 文字の ISO 3166-1 alpha-2 の国コードで、各値は[価格帯](#price-tiers)です。 これらの項目は、[特定の市場でのアドオンのカスタム価格](https://docs.microsoft.com/windows/uwp/publish/set-iap-pricing-and-availability)を表します。 このディクショナリに含まれる項目は、指定された市場の *basePriceId* の値によって指定されている基本価格を上書きします。    |

<span id="status-details-object" />

### <a name="status-details-resource"></a>ステータスの詳細に関するリソース

このリソースには、申請の状態についての追加情報が保持されます。 このリソースには、次の値があります。

| Value           | 種類    | 説明       |
|-----------------|---------|------|
|  errors               |    オブジェクト     |   申請のエラーの詳細が保持される[ステータスの詳細リソース](#status-detail-object)の配列です。   |     
|  warnings               |   オブジェクト      | 申請の警告の詳細が保持される[ステータスの詳細リソース](#status-detail-object)の配列です。     |
|  certificationReports               |     オブジェクト    |   申請の認定レポート データへのアクセスを提供する[認定レポート リソース](#certification-report-object)です。 認定されなかった場合に、これらのレポートから詳しい情報を知ることができます。    |  

<span id="status-detail-object" />

### <a name="status-detail-resource"></a>ステータスの詳細に関するリソース

このリソースには、申請に関連するエラーや警告についての追加情報が保持されます。 このリソースには、次の値があります。

| Value           | 種類    | 説明    |
|-----------------|---------|------|
|  code               |    string     |   エラーや警告の種類を説明する[申請ステータス コード](#submission-status-code)です。   |     
|  details               |     string    |  問題についての詳細が含まれるメッセージです。     |

<span id="certification-report-object" />

### <a name="certification-report-resource"></a>認定レポート リソース

このリソースは、申請の認定レポート データへのアクセスを提供します。 このリソースには、次の値があります。

| Value           | 種類    | 説明               |
|-----------------|---------|------|
|     date            |    string     |  日付と ISO 8601 形式でレポートが生成された時刻。    |
|     reportUrl            |    string     |  レポートにアクセスできる URL です。    |

## <a name="enums"></a>列挙型

これらのメソッドでは、次の列挙型が使用されます。

<span id="price-tiers" />

### <a name="price-tiers"></a>価格帯

次の値は、[価格リソース](#pricing-object)における、アドオンの申請に利用できる価格帯を表します。

| Value           | 説明       |
|-----------------|------|
|  基本               |   価格帯が設定されていない場合、アドオンの基本価格が使用されます。      |     
|  NotAvailable              |   アドオンは指定された地域で提供されていません。    |     
|  Free              |   アドオンは無償です。    |    
|  Tier*xxxx*               |   アドオンの価格帯を指定する文字列 (**Tier<em>xxxx</em>** の形式)。 現在のところ、次の範囲の価格帯がサポートされています。<br/><br/><ul><li>[価格リソース](#pricing-object)の *isAdvancedPricingModel* 値が **true** の場合、アカウントで利用可能な価格帯値は **Tier1012** - **Tier1424** です。</li><li>[価格リソース](#pricing-object)の *isAdvancedPricingModel* 値が **false** の場合、アカウントで利用可能な価格帯値は **Tier2** - **Tier96** です。</li></ul>各レベルに関連付けられている市場固有の価格を含む、開発者アカウントの利用できる価格レベルの完全なテーブルを確認する、**価格と可用性**でアプリを送信する、いずれかのページパートナー センターと、をクリックして、**ビュー テーブル**のリンクを**市場やカスタムの価格**セクション (このリンクは一部の開発者アカウントで、**価格**セクション)。     |

<span id="submission-status-code" />

### <a name="submission-status-code"></a>申請の状態コード

次の値は、申請の状態コードを表します。

| Value           |  説明      |
|-----------------|---------------|
|  なし            |     コードが指定されていません。         |     
|      InvalidArchive        |     パッケージが含まれる ZIP アーカイブは無効であるか、認識できないアーカイブ形式です。  |
| MissingFiles | ZIP アーカイブに、申請データで指定されているすべてのファイルが含まれていないか、ファイルのアーカイブ内の場所が正しくありません。 |
| PackageValidationFailed | 申請の 1 つ以上のパッケージを検証できませんでした。 |
| InvalidParameterValue | 要求本文に含まれるパラメーターの 1 つが無効です。 |
| InvalidOperation | 実行された操作は無効です。 |
| InvalidState | 実行された操作は、パッケージ フライトの現在の状態では無効です。 |
| ResourceNotFound | 指定されたパッケージ フライトは見つかりませんでした。 |
| ServiceError | 内部サービス エラーのため、要求を処理できませんでした。 もう一度要求を行ってください。 |
| ListingOptOutWarning | 開発者が以前の申請の登録情報を削除しているか、パッケージによってサポートされる登録情報を含めていませんでした。 |
| ListingOptInWarning  | 開発者が登録情報を追加しました。 |
| UpdateOnlyWarning | 開発者が、更新サポートしかないものを挿入しようとしています。 |
| その他  | 申請が非認識または未分類の状態です。 |
| PackageValidationWarning | パッケージ検証プロセスの結果、警告が生成されました。 |

<span/>

## <a name="related-topics"></a>関連トピック

* [作成し、Microsoft Store サービスを使用して送信の管理](create-and-manage-submissions-using-windows-store-services.md)
* [Microsoft Store 送信 API を使用してアドオンを管理します。](manage-add-ons.md)
* [パートナー センターで申請をアドオン](https://docs.microsoft.com/windows/uwp/publish/iap-submissions)
