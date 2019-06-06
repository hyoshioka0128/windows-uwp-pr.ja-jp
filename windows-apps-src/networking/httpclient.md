---
description: HTTP 2.0 プロトコルと HTTP 1.1 プロトコルを使って情報を送受信するには、HttpClient とその他の Windows.Web.Http 名前空間 API を使います。
title: HttpClient
ms.assetid: EC9820D3-3A46-474F-8A01-AE1C27442750
ms.date: 6/5/2019
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: bb098aae346c7a81771262793f5f6a042d62d5a3
ms.sourcegitcommit: 1f39b67f2711b96c6b4e7ed7107a9a47127d4e8f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2019
ms.locfileid: "66721610"
---
# <a name="httpclient"></a><span data-ttu-id="35099-104">HttpClient</span><span class="sxs-lookup"><span data-stu-id="35099-104">HttpClient</span></span>

<span data-ttu-id="35099-105">**重要な API**</span><span class="sxs-lookup"><span data-stu-id="35099-105">**Important APIs**</span></span>

-   [<span data-ttu-id="35099-106">**HttpClient**</span><span class="sxs-lookup"><span data-stu-id="35099-106">**HttpClient**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient)
-   [<span data-ttu-id="35099-107">**Windows.Web.Http**</span><span class="sxs-lookup"><span data-stu-id="35099-107">**Windows.Web.Http**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Web.Http)
-   [<span data-ttu-id="35099-108">**Windows.Web.Http.HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="35099-108">**Windows.Web.Http.HttpResponseMessage**</span></span>](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpResponseMessage)

<span data-ttu-id="35099-109">HTTP 2.0 プロトコルと HTTP 1.1 プロトコルを使って情報を送受信するには、[**HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) とその他の [**Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) 名前空間 API を使います。</span><span class="sxs-lookup"><span data-stu-id="35099-109">Use [**HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) and the rest of the [**Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) namespace API to send and receive information using the HTTP 2.0 and HTTP 1.1 protocols.</span></span>

## <a name="overview-of-httpclient-and-the-windowswebhttp-namespace"></a><span data-ttu-id="35099-110">HttpClient と Windows.Web.Http 名前空間の概要</span><span class="sxs-lookup"><span data-stu-id="35099-110">Overview of HttpClient and the Windows.Web.Http namespace</span></span>

<span data-ttu-id="35099-111">[  **Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) 名前空間、関連する [**Windows.Web.Http.Headers**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.Headers) 名前空間、[**Windows.Web.Http.Filters**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.Filters) 名前空間のクラスには、基本的な GET 要求を実行したり、次のようなさらに高度な HTTP 機能を実装したりするための HTTP クライアントとして動作する、ユニバーサル Windows プラットフォーム (UWP) アプリ用のプログラミング インターフェイスが用意されています。</span><span class="sxs-lookup"><span data-stu-id="35099-111">The classes in the [**Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) namespace and the related [**Windows.Web.Http.Headers**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.Headers) and [**Windows.Web.Http.Filters**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.Filters) namespaces provide a programming interface for Universal Windows Platform (UWP) apps that act as an HTTP client to perform basic GET requests or implement more advanced HTTP functionality listed below.</span></span>

-   <span data-ttu-id="35099-112">一般的な動詞 (**DELETE**、**GET**、**PUT**、**POST**) に対応するメソッド。</span><span class="sxs-lookup"><span data-stu-id="35099-112">Methods for common verbs (**DELETE**, **GET**, **PUT**, and **POST**).</span></span> <span data-ttu-id="35099-113">これらの各要求は、非同期操作として送られます。</span><span class="sxs-lookup"><span data-stu-id="35099-113">Each of these requests are sent as an asynchronous operation.</span></span>

-   <span data-ttu-id="35099-114">一般的な認証設定とパターンのサポート。</span><span class="sxs-lookup"><span data-stu-id="35099-114">Support for common authentication settings and patterns.</span></span>

-   <span data-ttu-id="35099-115">トランスポートに関する Secure Sockets Layer (SSL) 詳細へのアクセス。</span><span class="sxs-lookup"><span data-stu-id="35099-115">Access to Secure Sockets Layer (SSL) details on the transport.</span></span>

-   <span data-ttu-id="35099-116">カスタマイズされたフィルターを高度なアプリに含める機能。</span><span class="sxs-lookup"><span data-stu-id="35099-116">Ability to include customized filters in advanced apps.</span></span>

-   <span data-ttu-id="35099-117">Cookie を取得、設定、削除する機能。</span><span class="sxs-lookup"><span data-stu-id="35099-117">Ability to get, set, and delete cookies.</span></span>

-   <span data-ttu-id="35099-118">非同期メソッドで利用可能な HTTP 要求の進行状況情報。</span><span class="sxs-lookup"><span data-stu-id="35099-118">HTTP Request progress info available on asynchronous methods.</span></span>

<span data-ttu-id="35099-119">[  **Windows.Web.Http.HttpRequestMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpRequestMessage) クラスは、[**Windows.Web.Http.HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) から送られた HTTP 要求メッセージを表します。</span><span class="sxs-lookup"><span data-stu-id="35099-119">The [**Windows.Web.Http.HttpRequestMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpRequestMessage) class represents an HTTP request message sent by [**Windows.Web.Http.HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient).</span></span> <span data-ttu-id="35099-120">[  **Windows.Web.Http.HttpResponseMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpResponseMessage) クラスは、HTTP 要求から受け取った HTTP 応答メッセージを表します。</span><span class="sxs-lookup"><span data-stu-id="35099-120">The [**Windows.Web.Http.HttpResponseMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpResponseMessage) class represents an HTTP response message received from an HTTP request.</span></span> <span data-ttu-id="35099-121">HTTP メッセージは、IETF によって [RFC 2616](https://go.microsoft.com/fwlink/p/?linkid=241642) で規定されています。</span><span class="sxs-lookup"><span data-stu-id="35099-121">HTTP messages are defined in [RFC 2616](https://go.microsoft.com/fwlink/p/?linkid=241642) by the IETF.</span></span>

<span data-ttu-id="35099-122">[  **Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) 名前空間は、クッキーを含む HTTP エンティティ ボディおよびヘッダーとして HTTP コンテンツを表します。</span><span class="sxs-lookup"><span data-stu-id="35099-122">The [**Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) namespace represents HTTP content as the HTTP entity body and headers including cookies.</span></span> <span data-ttu-id="35099-123">HTTP コンテンツは、HTTP 要求または HTTP 応答に関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="35099-123">HTTP content can be associated with an HTTP request or an HTTP response.</span></span> <span data-ttu-id="35099-124">**Windows.Web.Http** 名前空間には、HTTP コンテンツを表す多数のさまざまなクラスが用意されています。</span><span class="sxs-lookup"><span data-stu-id="35099-124">The **Windows.Web.Http** namespace provides a number of different classes to represent HTTP content.</span></span>

-   <span data-ttu-id="35099-125">[**HttpBufferContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpBufferContent)します。</span><span class="sxs-lookup"><span data-stu-id="35099-125">[**HttpBufferContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpBufferContent).</span></span> <span data-ttu-id="35099-126">バッファーとしてのコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="35099-126">Content as a buffer</span></span>
-   <span data-ttu-id="35099-127">[**HttpFormUrlEncodedContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpFormUrlEncodedContent)します。</span><span class="sxs-lookup"><span data-stu-id="35099-127">[**HttpFormUrlEncodedContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpFormUrlEncodedContent).</span></span> <span data-ttu-id="35099-128">**application/x-www-form-urlencoded** MIME タイプでエンコードされた名前と値の組としてのコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="35099-128">Content as name and value tuples encoded with the **application/x-www-form-urlencoded** MIME type</span></span>
-   <span data-ttu-id="35099-129">[**HttpMultipartContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpMultipartContent)します。</span><span class="sxs-lookup"><span data-stu-id="35099-129">[**HttpMultipartContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpMultipartContent).</span></span> <span data-ttu-id="35099-130">コンテンツの形式で、**マルチパート/\***  MIME の種類。</span><span class="sxs-lookup"><span data-stu-id="35099-130">Content in the form of the **multipart/\*** MIME type.</span></span>
-   <span data-ttu-id="35099-131">[**HttpMultipartFormDataContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpMultipartFormDataContent)します。</span><span class="sxs-lookup"><span data-stu-id="35099-131">[**HttpMultipartFormDataContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpMultipartFormDataContent).</span></span> <span data-ttu-id="35099-132">**multipart/form-data** MIME タイプとしてエンコードされているコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="35099-132">Content that is encoded as the **multipart/form-data** MIME type.</span></span>
-   <span data-ttu-id="35099-133">[**HttpStreamContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpStreamContent)します。</span><span class="sxs-lookup"><span data-stu-id="35099-133">[**HttpStreamContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpStreamContent).</span></span> <span data-ttu-id="35099-134">ストリームとしてのコンテンツ (この内部タイプは、HTTP GET メソッドでのデータの受信、および HTTP POST メソッドでのデータのアップロードに使われます)。</span><span class="sxs-lookup"><span data-stu-id="35099-134">Content as a stream (the internal type is used by the HTTP GET method to receive data and the HTTP POST method to upload data)</span></span>
-   <span data-ttu-id="35099-135">[**HttpStringContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpStringContent)します。</span><span class="sxs-lookup"><span data-stu-id="35099-135">[**HttpStringContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpStringContent).</span></span> <span data-ttu-id="35099-136">文字列としてのコンテンツ。</span><span class="sxs-lookup"><span data-stu-id="35099-136">Content as a string.</span></span>
-   <span data-ttu-id="35099-137">[**IHttpContent** ](https://docs.microsoft.com/uwp/api/Windows.Web.Http.IHttpContent) -独自のコンテンツ オブジェクトを作成する開発者向けの基本インターフェイス</span><span class="sxs-lookup"><span data-stu-id="35099-137">[**IHttpContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.IHttpContent) - A base interface for developers to create their own content objects</span></span>

<span data-ttu-id="35099-138">「HTTP 経由でシンプルな GET 要求を送信する」セクションのコード スニペットでは、[**HttpStringContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpStringContent) クラスを使って、HTTP GET 要求からの HTTP 応答を文字列として表しています。</span><span class="sxs-lookup"><span data-stu-id="35099-138">The code snippet in the "Send a simple GET request over HTTP" section uses the [**HttpStringContent**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpStringContent) class to represent the HTTP response from an HTTP GET request as a string.</span></span>

<span data-ttu-id="35099-139">[  **Windows.Web.Http.Headers**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.Headers) 名前空間では、HTTP ヘッダーと Cookie の作成がサポートされます。これらはプロパティとして、[**HttpRequestMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpRequestMessage) オブジェクトと [**HttpResponseMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpResponseMessage) オブジェクトに関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="35099-139">The [**Windows.Web.Http.Headers**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.Headers) namespace supports creation of HTTP headers and cookies, which are then associated as properties with [**HttpRequestMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpRequestMessage) and [**HttpResponseMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpResponseMessage) objects.</span></span>

## <a name="send-a-simple-get-request-over-http"></a><span data-ttu-id="35099-140">HTTP 経由でシンプルな GET 要求を送信する</span><span class="sxs-lookup"><span data-stu-id="35099-140">Send a simple GET request over HTTP</span></span>

<span data-ttu-id="35099-141">この記事の中で既に説明したように、[**Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) 名前空間は、UWP アプリで GET 要求を送信できるようにします。</span><span class="sxs-lookup"><span data-stu-id="35099-141">As mentioned earlier in this article, the [**Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) namespace allows UWP apps to send GET requests.</span></span> <span data-ttu-id="35099-142">次のコード スニペットは、GET 要求を送信する方法を示します http://www.contoso.comを使用して、 [ **Windows.Web.Http.HttpClient** ](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient)クラスおよび[ **Windows.Web.Http.HttpResponseMessage** ](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpResponseMessage) GET 要求から応答を読み取るクラス。</span><span class="sxs-lookup"><span data-stu-id="35099-142">The following code snippet demonstrates how to send a GET request to http://www.contoso.com using the [**Windows.Web.Http.HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) class and the [**Windows.Web.Http.HttpResponseMessage**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpResponseMessage) class to read the response from the GET request.</span></span>

```csharp
//Create an HTTP client object
Windows.Web.Http.HttpClient httpClient = new Windows.Web.Http.HttpClient();

//Add a user-agent header to the GET request. 
var headers = httpClient.DefaultRequestHeaders;

//The safe way to add a header value is to use the TryParseAdd method and verify the return value is true,
//especially if the header value is coming from user input.
string header = "ie";
if (!headers.UserAgent.TryParseAdd(header))
{
    throw new Exception("Invalid header value: " + header);
}

header = "Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)";
if (!headers.UserAgent.TryParseAdd(header))
{
    throw new Exception("Invalid header value: " + header);
}

Uri requestUri = new Uri("http://www.contoso.com");

//Send the GET request asynchronously and retrieve the response as a string.
Windows.Web.Http.HttpResponseMessage httpResponse = new Windows.Web.Http.HttpResponseMessage();
string httpResponseBody = "";

try
{
    //Send the GET request
    httpResponse = await httpClient.GetAsync(requestUri);
    httpResponse.EnsureSuccessStatusCode();
    httpResponseBody = await httpResponse.Content.ReadAsStringAsync();
}
catch (Exception ex)
{
    httpResponseBody = "Error: " + ex.HResult.ToString("X") + " Message: " + ex.Message;
}
```

```cppwinrt
// pch.h
#pragma once
#include <winrt/Windows.Foundation.h>
#include <winrt/Windows.Web.Http.Headers.h>

// main.cpp : Defines the entry point for the console application.
#include "pch.h"
#include <iostream>
using namespace winrt;
using namespace Windows::Foundation;

int main()
{
    init_apartment();

    // Create an HttpClient object.
    Windows::Web::Http::HttpClient httpClient;

    // Add a user-agent header to the GET request.
    auto headers{ httpClient.DefaultRequestHeaders() };

    // The safe way to add a header value is to use the TryParseAdd method, and verify the return value is true.
    // This is especially important if the header value is coming from user input.
    std::wstring header{ L"ie" };
    if (!headers.UserAgent().TryParseAdd(header))
    {
        throw L"Invalid header value: " + header;
    }

    header = L"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)";
    if (!headers.UserAgent().TryParseAdd(header))
    {
        throw L"Invalid header value: " + header;
    }

    Uri requestUri{ L"http://www.contoso.com" };

    // Send the GET request asynchronously, and retrieve the response as a string.
    Windows::Web::Http::HttpResponseMessage httpResponseMessage;
    std::wstring httpResponseBody;

    try
    {
        // Send the GET request.
        httpResponseMessage = httpClient.GetAsync(requestUri).get();
        httpResponseMessage.EnsureSuccessStatusCode();
        httpResponseBody = httpResponseMessage.Content().ReadAsStringAsync().get();
    }
    catch (winrt::hresult_error const& ex)
    {
        httpResponseBody = ex.message();
    }
    std::wcout << httpResponseBody;
}
```

## <a name="post-binary-data-over-http"></a><span data-ttu-id="35099-143">HTTP 経由で投稿のバイナリ データ</span><span class="sxs-lookup"><span data-stu-id="35099-143">POST binary data over HTTP</span></span>

<span data-ttu-id="35099-144">[C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis)フォーム データと POST 要求を使用して、web サーバーにファイルのアップロードと少量のバイナリ データを送信する次のコード例を示しています。</span><span class="sxs-lookup"><span data-stu-id="35099-144">The [C++/WinRT](/windows/uwp/cpp-and-winrt-apis) code example below illustrates using form data and a POST request to send a small amount of binary data as a file upload to a web server.</span></span> <span data-ttu-id="35099-145">コードを使用して、 [ **HttpBufferContent** ](/uwp/api/windows.web.http.httpbuffercontent)バイナリのデータを表すクラスと[ **HttpMultipartFormDataContent** ](/uwp/api/windows.web.http.httpmultipartformdatacontent)クラスマルチパート フォーム データを表します。</span><span class="sxs-lookup"><span data-stu-id="35099-145">The code uses the [**HttpBufferContent**](/uwp/api/windows.web.http.httpbuffercontent) class to represent the binary data, and the [**HttpMultipartFormDataContent**](/uwp/api/windows.web.http.httpmultipartformdatacontent) class to represent the multi-part form data.</span></span>

> [!NOTE]
> <span data-ttu-id="35099-146">呼び出す**取得**(として次のコード例でわかる) が適切でない UI スレッドにします。</span><span class="sxs-lookup"><span data-stu-id="35099-146">Calling **get** (as seen in the code example below) isn't appropriate for a UI thread.</span></span> <span data-ttu-id="35099-147">その場合に使用する正しい方法を参照してください。[同時実行と非同期操作を C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis/concurrency)します。</span><span class="sxs-lookup"><span data-stu-id="35099-147">For the correct technique to use in that case, see [Concurrency and asynchronous operations with C++/WinRT](/windows/uwp/cpp-and-winrt-apis/concurrency).</span></span>

```cppwinrt
// pch.h
#pragma once
#include <winrt/Windows.Foundation.h>
#include <winrt/Windows.Security.Cryptography.h>
#include <winrt/Windows.Storage.Streams.h>
#include <winrt/Windows.Web.Http.Headers.h>

// main.cpp : Defines the entry point for the console application.
#include "pch.h"
#include <iostream>
#include <sstream>
using namespace winrt;
using namespace Windows::Foundation;
using namespace Windows::Storage::Streams;

int main()
{
    init_apartment();

    auto buffer{
        Windows::Security::Cryptography::CryptographicBuffer::ConvertStringToBinary(
            L"A sentence of text to encode into binary to serve as sample data.",
            Windows::Security::Cryptography::BinaryStringEncoding::Utf8
        )
    };
    Windows::Web::Http::HttpBufferContent binaryContent{ buffer };
    // You can use the 'image/jpeg' content type to represent any binary data;
    // it's not necessarily an image file.
    binaryContent.Headers().Append(L"Content-Type", L"image/jpeg");

    Windows::Web::Http::Headers::HttpContentDispositionHeaderValue disposition{ L"form-data" };
    binaryContent.Headers().ContentDisposition(disposition);
    // The 'name' directive contains the name of the form field representing the data.
    disposition.Name(L"fileForUpload");
    // Here, the 'filename' directive is used to indicate to the server a file name
    // to use to save the uploaded data.
    disposition.FileName(L"file.dat");

    Windows::Web::Http::HttpMultipartFormDataContent postContent;
    postContent.Add(binaryContent); // Add the binary data content as a part of the form data content.

    // Send the POST request asynchronously, and retrieve the response as a string.
    Windows::Web::Http::HttpResponseMessage httpResponseMessage;
    std::wstring httpResponseBody;

    try
    {
        // Send the POST request.
        Uri requestUri{ L"https://www.contoso.com/post" };
        Windows::Web::Http::HttpClient httpClient;
        httpResponseMessage = httpClient.PostAsync(requestUri, postContent).get();
        httpResponseMessage.EnsureSuccessStatusCode();
        httpResponseBody = httpResponseMessage.Content().ReadAsStringAsync().get();
    }
    catch (winrt::hresult_error const& ex)
    {
        httpResponseBody = ex.message();
    }
    std::wcout << httpResponseBody;
}
```

<span data-ttu-id="35099-148">(上記で使用する明示的なバイナリ データではなく) 実際のバイナリ ファイルの内容を投稿することがわかりますが使いやすく、 [HttpStreamContent](/uwp/api/windows.web.http.httpstreamcontent)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="35099-148">To POST the contents of an actual binary file (rather than the explicit binary data used above), you'll find it easier to use an [HttpStreamContent](/uwp/api/windows.web.http.httpstreamcontent) object.</span></span> <span data-ttu-id="35099-149">構築して、そのコンス トラクターに引数として渡す呼び出しから返される値[StorageFile.OpenReadAsync](/uwp/api/windows.storage.storagefile.openreadasync)します。</span><span class="sxs-lookup"><span data-stu-id="35099-149">Construct one and, as the argument to its constructor, pass the value returned from a call to [StorageFile.OpenReadAsync](/uwp/api/windows.storage.storagefile.openreadasync).</span></span> <span data-ttu-id="35099-150">そのメソッドは、バイナリ ファイル内のデータのストリームを返します。</span><span class="sxs-lookup"><span data-stu-id="35099-150">That method returns a stream for the data inside your binary file.</span></span>

<span data-ttu-id="35099-151">また、大きなファイル (約 10 MB より大きい) をアップロードしている場合をお勧め、Windows ランタイムを使用すること[バック グラウンド転送](/uwp/api/windows.networking.backgroundtransfer)Api。</span><span class="sxs-lookup"><span data-stu-id="35099-151">Also, if you're uploading a large file (larger than about 10MB), then we recommend that you use the Windows Runtime [Background Transfer](/uwp/api/windows.networking.backgroundtransfer) APIs.</span></span>

## <a name="post-json-data-over-http"></a><span data-ttu-id="35099-152">HTTP 経由での POST JSON データ</span><span class="sxs-lookup"><span data-stu-id="35099-152">POST JSON data over HTTP</span></span>

<span data-ttu-id="35099-153">次の例は、エンドポイントをいくつかの JSON を投稿し、応答本文を書き込みます。</span><span class="sxs-lookup"><span data-stu-id="35099-153">The following example posts some JSON to an endpoint, then writes out the response body.</span></span>

```cs
using System;
using System.Diagnostics;
using System.Threading.Tasks;
using Windows.Storage.Streams;
using Windows.Web.Http;

private async Task TryPostJsonAsync()
{
    try
    {
        // Construct the HttpClient and Uri. This endpoint is for test purposes only.
        HttpClient httpClient = new HttpClient();
        Uri uri = new Uri("https://www.contoso.com/post");

        // Construct the JSON to post.
        HttpStringContent content = new HttpStringContent(
            "{ \"firstName\": \"Eliot\" }",
            UnicodeEncoding.Utf8,
            "application/json");

        // Post the JSON and wait for a response.
        HttpResponseMessage httpResponseMessage = await httpClient.PostAsync(
            uri,
            content);

        // Make sure the post succeeded, and write out the response.
        httpResponseMessage.EnsureSuccessStatusCode();
        var httpResponseBody = await httpResponseMessage.Content.ReadAsStringAsync();
        Debug.WriteLine(httpResponseBody);
    }
    catch (Exception ex)
    {
        // Write out any exceptions.
        Debug.WriteLine(ex);
    }
}
```

## <a name="exceptions-in-windowswebhttp"></a><span data-ttu-id="35099-154">Windows.Web.Http の例外</span><span class="sxs-lookup"><span data-stu-id="35099-154">Exceptions in Windows.Web.Http</span></span>

<span data-ttu-id="35099-155">Uniform Resource Identifier (URI) として無効な文字列が、[**Windows.Foundation.Uri**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Uri) オブジェクトのコンストラクターに渡されると、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="35099-155">An exception is thrown when an invalid string for a the Uniform Resource Identifier (URI) is passed to the constructor for the [**Windows.Foundation.Uri**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Uri) object.</span></span>

<span data-ttu-id="35099-156">**.NET:**   、 [ **Windows.Foundation.Uri** ](https://docs.microsoft.com/uwp/api/Windows.Foundation.Uri)種類[ **System.Uri** ](https://docs.microsoft.com/dotnet/api/system.uri?redirectedfrom=MSDN)でC#とVB.</span><span class="sxs-lookup"><span data-stu-id="35099-156">**.NET:**  The [**Windows.Foundation.Uri**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Uri) type appears as [**System.Uri**](https://docs.microsoft.com/dotnet/api/system.uri?redirectedfrom=MSDN) in C# and VB.</span></span>

<span data-ttu-id="35099-157">C# や Visual Basic では、.NET 4.5 の [**System.Uri**](https://docs.microsoft.com/dotnet/api/system.uri?redirectedfrom=MSDN) クラスと、[**System.Uri.TryCreate**](https://docs.microsoft.com/dotnet/api/system.uri.trycreate?redirectedfrom=MSDN#overloads) メソッドの 1 つを使って、URI が作成される前にユーザーから受け取った文字列をテストすることによって、このエラーを回避できます。</span><span class="sxs-lookup"><span data-stu-id="35099-157">In C# and Visual Basic, this error can be avoided by using the [**System.Uri**](https://docs.microsoft.com/dotnet/api/system.uri?redirectedfrom=MSDN) class in the .NET 4.5 and one of the [**System.Uri.TryCreate**](https://docs.microsoft.com/dotnet/api/system.uri.trycreate?redirectedfrom=MSDN#overloads) methods to test the string received from a user before the URI is constructed.</span></span>

<span data-ttu-id="35099-158">C++ では、URI として渡される文字列を試行して解析するメソッドはありません。</span><span class="sxs-lookup"><span data-stu-id="35099-158">In C++, there is no method to try and parse a string to a URI.</span></span> <span data-ttu-id="35099-159">アプリがユーザーから [**Windows.Foundation.Uri**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Uri) の入力を取得する場合、このコンストラクターを try/catch ブロックに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="35099-159">If an app gets input from the user for the [**Windows.Foundation.Uri**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Uri), the constructor should be in a try/catch block.</span></span> <span data-ttu-id="35099-160">例外がスローされた場合、アプリは、ユーザーに通知し、新しいホスト名を要求することができます。</span><span class="sxs-lookup"><span data-stu-id="35099-160">If an exception is thrown, the app can notify the user and request a new hostname.</span></span>

<span data-ttu-id="35099-161">[  **Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) には便利な関数がありません。</span><span class="sxs-lookup"><span data-stu-id="35099-161">The [**Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http) lacks a convenience function.</span></span> <span data-ttu-id="35099-162">そのため、この名前空間の [**HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) と他のクラスを使うアプリは、**HRESULT** 値を使う必要があります。</span><span class="sxs-lookup"><span data-stu-id="35099-162">So an app using [**HttpClient**](https://docs.microsoft.com/uwp/api/Windows.Web.Http.HttpClient) and other classes in this namespace needs to use the **HRESULT** value.</span></span>

<span data-ttu-id="35099-163">.NET Framework 4.5 を使用してアプリC#、VB.NET、 [System.Exception](https://docs.microsoft.com/dotnet/api/system.exception?redirectedfrom=MSDN)例外が発生したときに、アプリの実行中にエラーを表します。</span><span class="sxs-lookup"><span data-stu-id="35099-163">In apps using the .NET Framework 4.5 in C#, VB.NET, the [System.Exception](https://docs.microsoft.com/dotnet/api/system.exception?redirectedfrom=MSDN) represents an error during app execution when an exception occurs.</span></span> <span data-ttu-id="35099-164">[System.Exception.HResult](https://docs.microsoft.com/dotnet/api/system.exception.hresult?redirectedfrom=MSDN#System_Exception_HResult) プロパティは、特定の例外に割り当てられた **HRESULT** を返します。</span><span class="sxs-lookup"><span data-stu-id="35099-164">The [System.Exception.HResult](https://docs.microsoft.com/dotnet/api/system.exception.hresult?redirectedfrom=MSDN#System_Exception_HResult) property returns the **HRESULT** assigned to the specific exception.</span></span> <span data-ttu-id="35099-165">[System.Exception.Message](https://docs.microsoft.com/dotnet/api/system.exception.message?redirectedfrom=MSDN#System_Exception_Message) プロパティは、例外を説明するメッセージを返します。</span><span class="sxs-lookup"><span data-stu-id="35099-165">The [System.Exception.Message](https://docs.microsoft.com/dotnet/api/system.exception.message?redirectedfrom=MSDN#System_Exception_Message) property returns the message that describes the exception.</span></span> <span data-ttu-id="35099-166">使うことができる **HRESULT** 値は、*Winerror.h* ヘッダー ファイルに記載されています。</span><span class="sxs-lookup"><span data-stu-id="35099-166">Possible **HRESULT** values are listed in the *Winerror.h* header file.</span></span> <span data-ttu-id="35099-167">アプリは特定の **HRESULT** 値に対するフィルター処理を行い、例外の原因に応じてアプリの動作を変更できます。</span><span class="sxs-lookup"><span data-stu-id="35099-167">An app can filter on specific **HRESULT** values to modify app behavior depending on the cause of the exception.</span></span>

<span data-ttu-id="35099-168">Managed C++ を使うアプリでは、アプリの実行中に例外が発生したときに、[Platform::Exception](https://docs.microsoft.com/cpp/cppcx/platform-exception-class) がエラーを表します。</span><span class="sxs-lookup"><span data-stu-id="35099-168">In apps using managed C++, the [Platform::Exception](https://docs.microsoft.com/cpp/cppcx/platform-exception-class) represents an error during app execution when an exception occurs.</span></span> <span data-ttu-id="35099-169">[Platform::Exception::HResult](https://docs.microsoft.com/cpp/cppcx/platform-exception-class#hresult) プロパティは、特定の例外に割り当てられた **HRESULT** を返します。</span><span class="sxs-lookup"><span data-stu-id="35099-169">The [Platform::Exception::HResult](https://docs.microsoft.com/cpp/cppcx/platform-exception-class#hresult) property returns the **HRESULT** assigned to the specific exception.</span></span> <span data-ttu-id="35099-170">[Platform::Exception::Message](https://docs.microsoft.com/cpp/cppcx/platform-exception-class#message) プロパティは、**HRESULT** 値に関連付けられた、システムが提供する文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="35099-170">The [Platform::Exception::Message](https://docs.microsoft.com/cpp/cppcx/platform-exception-class#message) property returns the system-provided string that is associated with the **HRESULT** value.</span></span> <span data-ttu-id="35099-171">使うことができる **HRESULT** 値は、*Winerror.h* ヘッダー ファイルに記載されています。</span><span class="sxs-lookup"><span data-stu-id="35099-171">Possible **HRESULT** values are listed in the *Winerror.h* header file.</span></span> <span data-ttu-id="35099-172">アプリは特定の **HRESULT** 値に対するフィルター処理を行い、例外の原因に応じてアプリの動作を変更できます。</span><span class="sxs-lookup"><span data-stu-id="35099-172">An app can filter on specific **HRESULT** values to modify app behavior depending on the cause of the exception.</span></span>

<span data-ttu-id="35099-173">ほとんどのパラメーター検証エラー、 **HRESULT**が返される**E\_INVALIDARG**します。</span><span class="sxs-lookup"><span data-stu-id="35099-173">For most parameter validation errors, the **HRESULT** returned is **E\_INVALIDARG**.</span></span> <span data-ttu-id="35099-174">一部の無効なメソッド呼び出しの**HRESULT**が返される**E\_不正な\_メソッド\_呼び出す**。</span><span class="sxs-lookup"><span data-stu-id="35099-174">For some illegal method calls, the **HRESULT** returned is **E\_ILLEGAL\_METHOD\_CALL**.</span></span>

