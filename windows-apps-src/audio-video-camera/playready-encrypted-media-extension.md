---
ms.assetid: 79C284CA-C53A-4C24-807E-6D4CE1A29BFA
description: このセクションでは、以前のバージョンの Windows 8.1、Windows 10 バージョンに加えられた変更をサポートするために、PlayReady の web アプリを変更する方法について説明します。
title: PlayReady の Encrypted Media Extension
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ad304d22fd1c519f7364ac69882eeaac9fa1a5c7
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66360708"
---
# <a name="playready-encrypted-media-extension"></a><span data-ttu-id="4cd36-104">PlayReady の Encrypted Media Extension</span><span class="sxs-lookup"><span data-stu-id="4cd36-104">PlayReady Encrypted Media Extension</span></span>



<span data-ttu-id="4cd36-105">このセクションでは、以前のバージョンの Windows 8.1、Windows 10 バージョンに加えられた変更をサポートするために、PlayReady の web アプリを変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-105">This section describes how to modify your PlayReady web app to support the changes made from the previous Windows 8.1 version to the Windows 10 version.</span></span>

<span data-ttu-id="4cd36-106">Internet Explorer で PlayReady メディア要素を使うと、開発者はコンテンツ プロバイダーが定義したアクセス ルールを適用しながら、ユーザーに PlayReady コンテンツを提供することのできる Web アプリを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-106">Using PlayReady media elements in Internet Explorer enables developers to create web apps capable of providing PlayReady content to the user while enforcing the access rules defined by the content provider.</span></span> <span data-ttu-id="4cd36-107">ここでは、HTML5 と JavaScript のみを使って、既存の Web アプリに PlayReady メディア要素を追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-107">This section describes how to add PlayReady media elements to your existing web apps by using only HTML5 and JavaScript.</span></span>

## <a name="whats-new-in-playready-encrypted-media-extension"></a><span data-ttu-id="4cd36-108">PlayReady の Encrypted Media Extension の新機能</span><span class="sxs-lookup"><span data-stu-id="4cd36-108">What's new in PlayReady Encrypted Media Extension</span></span>

<span data-ttu-id="4cd36-109">このセクションでは、Windows 10 で PlayReady コンテンツ保護を有効にする PlayReady Encrypted Media Extension (EME) に加えられた変更の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-109">This section provides a list of changes made to the PlayReady Encrypted Media Extension (EME) to enable PlayReady content protection on Windows 10.</span></span>

<span data-ttu-id="4cd36-110">次の一覧には、PlayReady 暗号化されたメディア拡張機能の Windows 10 への変更、新しい機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-110">The following list describes the new features and changes made to PlayReady Encrypted Media Extension for Windows 10:</span></span>

-   <span data-ttu-id="4cd36-111">追加されたハードウェア デジタル著作権管理 (DRM)。</span><span class="sxs-lookup"><span data-stu-id="4cd36-111">Added hardware digital rights management (DRM).</span></span>

    <span data-ttu-id="4cd36-112">ハードウェア ベースのコンテンツ保護により、複数のデバイス プラットフォーム上で、高解像度 (HD) と超高解像度 (UHD) のコンテンツを安全に再生できます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-112">Hardware-based content protection support enables secure playback of high definition (HD) and ultra-high definition (UHD) content on multiple device platforms.</span></span> <span data-ttu-id="4cd36-113">キー マテリアル (秘密キー、コンテンツ キー、これらのキーを派生またはロック解除するために使われるその他のキー マテリアルを含みます)、および暗号化解除された圧縮および非圧縮ビデオ サンプルは、ハードウェア セキュリティを利用して保護されます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-113">Key material (including private keys, content keys, and any other key material used to derive or unlock said keys), and decrypted compressed and uncompressed video samples are protected by leveraging hardware security.</span></span>

-   <span data-ttu-id="4cd36-114">永続的でないライセンスの事前の取得を提供します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-114">Provides proactive acquisition of non-persistent licenses.</span></span>
-   <span data-ttu-id="4cd36-115">1 つのメッセージで複数のライセンスを取得できるようにします。</span><span class="sxs-lookup"><span data-stu-id="4cd36-115">Provides acquisition of multiple licenses in one message.</span></span>

    <span data-ttu-id="4cd36-116">Windows 8.1 では、ように複数のキー識別子 (KeyIDs) と PlayReady オブジェクトを使用するかを使用して、[コンテンツ モデル データの復号化 (CDMData)](https://go.microsoft.com/fwlink/p/?LinkID=626819)複数 KeyIDs とします。</span><span class="sxs-lookup"><span data-stu-id="4cd36-116">You can either use a PlayReady object with multiple key identifiers (KeyIDs) as in Windows 8.1, or use [content decryption model data (CDMData)](https://go.microsoft.com/fwlink/p/?LinkID=626819) with multiple KeyIDs.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4cd36-117">Windows 10 で複数のキー識別子がサポートされている&lt;KeyID&gt; CDMData でします。</span><span class="sxs-lookup"><span data-stu-id="4cd36-117">In Windows 10, multiple key identifiers are supported under &lt;KeyID&gt; in CDMData.</span></span>

-   <span data-ttu-id="4cd36-118">リアルタイムの有効期限のサポートや期間限定ライセンス (LDL) が追加されました。</span><span class="sxs-lookup"><span data-stu-id="4cd36-118">Added real time expiration support, or limited duration license (LDL).</span></span>

    <span data-ttu-id="4cd36-119">ライセンスに対してリアルタイムの有効期限を設定することができます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-119">Provides the ability to set real-time expiration on licenses.</span></span>

-   <span data-ttu-id="4cd36-120">HDCP Type 1 (バージョン 2.2) ポリシーのサポートを追加しました。</span><span class="sxs-lookup"><span data-stu-id="4cd36-120">Added HDCP Type 1 (version 2.2) policy support.</span></span>
-   <span data-ttu-id="4cd36-121">Miracast が暗黙的な出力となりました。</span><span class="sxs-lookup"><span data-stu-id="4cd36-121">Miracast is now implicit as an output.</span></span>
-   <span data-ttu-id="4cd36-122">セキュア ストップが追加されました。</span><span class="sxs-lookup"><span data-stu-id="4cd36-122">Added secure stop.</span></span>

    <span data-ttu-id="4cd36-123">セキュア ストップによって、特定のコンテンツについてのメディア再生が停止したメディア ストリーミング サービスに対して、PlayReady デバイスが確実にアサートするための手段が提供されます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-123">Secure stop provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content.</span></span>

-   <span data-ttu-id="4cd36-124">オーディオとビデオに関するライセンスの分離が追加されました。</span><span class="sxs-lookup"><span data-stu-id="4cd36-124">Added audio and video license separation.</span></span>

    <span data-ttu-id="4cd36-125">トラックを分離することによって、ビデオがオーディオにデコードされるのを防ぐことができます。これにより、さらに強力なコンテンツ保護が可能になります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-125">Separate tracks prevent video from being decoded as audio; enabling more robust content protection.</span></span> <span data-ttu-id="4cd36-126">最新の標準では、オーディオ トラックと映像トラックに対して別々のキーが必要になります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-126">Emerging standards are requiring separate keys for audio and visual tracks.</span></span>

-   <span data-ttu-id="4cd36-127">MaxResDecode が追加されました。</span><span class="sxs-lookup"><span data-stu-id="4cd36-127">Added MaxResDecode.</span></span>

    <span data-ttu-id="4cd36-128">この機能は、コンテンツの再生を最大解像度に制限するために追加されました (ライセンスではなく、より強力なキーを所有している場合にも制限を受けます)。</span><span class="sxs-lookup"><span data-stu-id="4cd36-128">This feature was added to limit playback of content to a maximum resolution even when in possession of a more capable key (but not a license).</span></span> <span data-ttu-id="4cd36-129">これは、複数のストリーム サイズが 1 つのキーでエンコードされる状況をサポートします。</span><span class="sxs-lookup"><span data-stu-id="4cd36-129">It supports cases where multiple stream sizes are encoded with a single key.</span></span>

## <a name="encrypted-media-extension-support-in-playready"></a><span data-ttu-id="4cd36-130">PlayReady の Encrypted Media Extension のサポート</span><span class="sxs-lookup"><span data-stu-id="4cd36-130">Encrypted Media Extension support in PlayReady</span></span>

<span data-ttu-id="4cd36-131">このセクションでは、PlayReady でサポートされている W3C 暗号化メディア拡張機能のバージョンについて説明します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-131">This section describes the version of the W3C Encrypted Media Extension supported by PlayReady.</span></span>

<span data-ttu-id="4cd36-132">Web アプリ用の PlayReady は、現在 [2013 年 5 月 10 日付けの W3C Encrypted Media Extension (EME) 草案](https://www.w3.org/TR/2013/WD-encrypted-media-20130510/)に準拠しています。</span><span class="sxs-lookup"><span data-stu-id="4cd36-132">PlayReady for Web Apps is currently bound to the [W3C Encrypted Media Extension (EME) draft of May 10, 2013](https://www.w3.org/TR/2013/WD-encrypted-media-20130510/).</span></span> <span data-ttu-id="4cd36-133">このサポートは、将来のバージョンの Windows では更新された EME 仕様に合わせて変更されます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-133">This support will be changed to the updated EME specification in future versions of Windows.</span></span>

## <a name="use-hardware-drm"></a><span data-ttu-id="4cd36-134">ハードウェア DRM の使用</span><span class="sxs-lookup"><span data-stu-id="4cd36-134">Use hardware DRM</span></span>

<span data-ttu-id="4cd36-135">このセクションでは、Web アプリで PlayReady ハードウェア DRM を使う方法と、保護されたコンテンツがハードウェア DRM をサポートしていない場合にそれを無効にする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-135">This section describes how your web app can use PlayReady hardware DRM, and how to disable hardware DRM if the protected content does not support it.</span></span>

<span data-ttu-id="4cd36-136">PlayReady ハードウェア DRM を使うには、JavaScript Web アプリは、キー システム識別子 `com.microsoft.playready.hardware` と共に **isTypeSupported** EME メソッドを使って、ブラウザーから PlayReady ハードウェア DRM のサポートを照会する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-136">To use PlayReady hardware DRM, your JavaScript web app should use the **isTypeSupported** EME method with a key system identifier of `com.microsoft.playready.hardware` to query for PlayReady hardware DRM support from the browser.</span></span>

<span data-ttu-id="4cd36-137">一部のコンテンツは、ハードウェア DRM ではサポートされない場合があります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-137">Occasionally, some content is not supported in hardware DRM.</span></span> <span data-ttu-id="4cd36-138">Cocktail コンテンツがハードウェア DRM でサポートされることはありません。Cocktail コンテンツを再生する場合は、ハードウェア DRM を除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-138">Cocktail content is never supported in hardware DRM; if you want to play cocktail content, you must opt out of hardware DRM.</span></span> <span data-ttu-id="4cd36-139">一部のハードウェア DRM は HEVC をサポートしますが、サポートしないものもあります。HEVC コンテンツを再生したいが、ハードウェア DRM がサポートしていない場合も、これを除外してください。</span><span class="sxs-lookup"><span data-stu-id="4cd36-139">Some hardware DRM will support HEVC and some will not; if you want to play HEVC content and hardware DRM doesn’t support it, you will want to opt out as well.</span></span>

> [!NOTE]
> <span data-ttu-id="4cd36-140">HEVC コンテンツがサポートされているかどうかを判断するには、`com.microsoft.playready` をインスタンス化した後で、[**PlayReadyStatics.CheckSupportedHardware**](https://docs.microsoft.com/uwp/api/windows.media.protection.playready.playreadystatics.checksupportedhardware) メソッドを使います。</span><span class="sxs-lookup"><span data-stu-id="4cd36-140">To determine whether HEVC content is supported, after instantiating `com.microsoft.playready`, use the [**PlayReadyStatics.CheckSupportedHardware**](https://docs.microsoft.com/uwp/api/windows.media.protection.playready.playreadystatics.checksupportedhardware) method.</span></span>

## <a name="add-secure-stop-to-your-web-app"></a><span data-ttu-id="4cd36-141">Web アプリにセキュア ストップを追加する</span><span class="sxs-lookup"><span data-stu-id="4cd36-141">Add secure stop to your web app</span></span>

<span data-ttu-id="4cd36-142">このセクションでは、Web アプリにセキュア ストップを追加する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-142">This section describes how to add secure stop to your web app.</span></span>

<span data-ttu-id="4cd36-143">セキュア ストップによって、特定のコンテンツについてのメディア再生が停止したメディア ストリーミング サービスに対して、PlayReady デバイスが確実にアサートするための手段が提供されます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-143">Secure stop provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content.</span></span> <span data-ttu-id="4cd36-144">この機能により、メディア ストリーミング サービスは、特定のアカウントのさまざまなデバイスに対する使用制限を正しく適用し報告することができるようになります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-144">This capability ensures your media streaming services provide accurate enforcement and reporting of usage limitations on different devices for a given account.</span></span>

<span data-ttu-id="4cd36-145">セキュア ストップのチャレンジを送信する主なシナリオが 2 つあります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-145">There are two primary scenarios for sending a secure stop challenge:</span></span>

-   <span data-ttu-id="4cd36-146">コンテンツの最後に達したか、ユーザーがメディア プレゼンテーションを途中で停止したため、メディア プレゼンテーションが停止した場合。</span><span class="sxs-lookup"><span data-stu-id="4cd36-146">When the media presentation stops because end of content was reached or when the user stopped the media presentation somewhere in the middle.</span></span>
-   <span data-ttu-id="4cd36-147">(システムまたはアプリのクラッシュなどにより) 前回のセッションが予期せずに終了した場合。</span><span class="sxs-lookup"><span data-stu-id="4cd36-147">When the previous session ends unexpectedly (for example, due to a system or app crash).</span></span> <span data-ttu-id="4cd36-148">アプリは、起動時またはシャットダウン時に、未処理のセキュア ストップ セッションについて照会し、その他のメディア再生とは別にチャレンジを送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-148">The app will need to query, either at startup or shutdown, for any outstanding secure stop sessions and send challenge(s) separate from any other media playback.</span></span>

<span data-ttu-id="4cd36-149">次の手順は、さまざまなシナリオでセキュア ストップを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-149">The following procedures describe how to set up secure stop for various scenarios.</span></span>

<span data-ttu-id="4cd36-150">プレゼンテーションの通常の終了時にセキュア ストップを設定するには</span><span class="sxs-lookup"><span data-stu-id="4cd36-150">To set up secure stop for a normal end of a presentation:</span></span>

1.  <span data-ttu-id="4cd36-151">再生が開始する前に **onEnded** イベントを登録します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-151">Register the **onEnded** event before playback starts.</span></span>
2.  <span data-ttu-id="4cd36-152">**onEnded** イベント ハンドラーは、ビデオ/オーディオ要素のオブジェクトから `removeAttribute(“src”)` を呼び出し、ソースを **NULL** に設定する必要があります。これにより、メディア ファンデーションをトリガーしてトポロジを終了し、暗号化解除機能を破棄して、停止状態を設定します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-152">The **onEnded** event handler needs to call `removeAttribute(“src”)` from the video/audio element object to set the source to **NULL** which will trigger the media foundation to tear down the topology, destroy the decryptor(s), and set the stop state.</span></span>
3.  <span data-ttu-id="4cd36-153">ハンドラー内の CDM セッションのセキュア ストップを開始し、セキュア ストップ チャレンジをサーバーに送信して、現在は再生が停止したが、後でも実行できることを通知できます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-153">You can start the secure stop CDM session inside the handler to send the secure stop challenge to the server to notify the playback has stopped at this time, but it can be done later as well.</span></span>

<span data-ttu-id="4cd36-154">ユーザーがページから移動したか、タブまたはブラウザーを閉じた場合にセキュア ストップを設定するには</span><span class="sxs-lookup"><span data-stu-id="4cd36-154">To set up secure stop if the user navigates away from the page or closes down the tab or browser:</span></span>

-   <span data-ttu-id="4cd36-155">停止状態を記録するためにアプリの操作は必要ありません。自動的に記録されます。</span><span class="sxs-lookup"><span data-stu-id="4cd36-155">No app action is required to record the stop state; it will be recorded for you.</span></span>

<span data-ttu-id="4cd36-156">カスタム ページ コントロールまたはユーザーの操作 (カスタム ナビゲーション ボタンや、現在のプレゼンテーションを完了する前に新しいプレゼンテーションを開始するなど) のセキュア ストップを設定するには</span><span class="sxs-lookup"><span data-stu-id="4cd36-156">To set up secure stop for custom page controls or user actions (such as custom navigation buttons or starting a new presentation before the current presentation completed):</span></span>

-   <span data-ttu-id="4cd36-157">カスタム ユーザー アクションが発生すると、アプリは、ソースを **NULL** に設定する必要があります。これにより、メディア ファンデーションをトリガーして、トポロジを終了し、暗号化解除機能を破棄して、停止状態を設定します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-157">When custom user action occurs, the app needs to set the source to **NULL** which will trigger the media foundation to tear down the topology, destroy the decryptor(s), and set the stop state.</span></span>

<span data-ttu-id="4cd36-158">次の例は、Web アプリでのセキュア ストップの使い方を示しています。</span><span class="sxs-lookup"><span data-stu-id="4cd36-158">The following example demonstrates how to use secure stop in your web app:</span></span>

```JavaScript
// JavaScript source code

var g_prkey = null;
var g_keySession = null;
var g_fUseSpecificSecureStopSessionID = false;
var g_encodedMeteringCert = 'Base64 encoded of your metering cert (aka publisher cert)';

// Note: g_encodedLASessionId is the CDM session ID of the proactive or reactive license acquisition 
//       that we want to initiate the secure stop process.
var g_encodedLASessionId = null;

function main()
{
    ...

    g_prkey = new MSMediaKeys("com.microsoft.playready");

    ...

    // add 'onended' event handler to the video element
    // Assume 'myvideo' is the ID of the video element
    var videoElement = document.getElementById("myvideo");
    videoElement.onended = function (e) { 

        //
        // Calling removeAttribute("src") will set the source to null
        // which will trigger the MF to tear down the topology, destroy the
        // decryptor(s) and set the stop state.  This is required in order
        // to set the stop state.
        //
        videoElement.removeAttribute("src");
        videoElement.load();

        onEndOfStream();
    };
}

function onEndOfStream()
{
    ...

    createSecureStopCDMSession();

    ...    
}

function createSecureStopCDMSession()
{
    try{    
        var targetMediaCodec = "video/mp4";
        var customData = "my custom data";

        var encodedSessionId = g_encodedLASessionId;
        if( !g_fUseSpecificSecureStopSessionID )
        {
            // Use "*" (wildcard) as the session ID to include all secure stop sessions
            // TODO: base64 encode "*" and place encoded result to encodedSessionId
        }

        var int8ArrayCDMdata = formatSecureStopCDMData( encodedSessionId, customData,  g_encodedMeteringCert );
        var emptyArrayofInitData = new Uint8Array();

        g_keySession = g_prkey.createSession(targetMediaCodec, emptyArrayofInitData, int8ArrayCDMdata);

        addPlayreadyKeyEventHandler();

    } catch( e )
    {
        // TODO: Handle exception
    }
}

function addPlayreadyKeyEventHandler()
{
    // add 'keymessage' eventhandler   
    g_keySession.addEventListener('mskeymessage', function (event) {

        // TODO: Get the keyMessage from event.message.buffer which contains the secure stop challenge
        //       The keyMessage format for the secure stop is similar to LA as below:
        //
        //            <PlayReadyKeyMessage type="SecureStop" >
        //              <SecureStop version="1.0" >
        //                <Challenge encoding="base64encoded">
        //                    secure stop challenge
        //                </Challenge>
        //                <HttpHeaders>
        //                    <HttpHeader>
        //                      <name>Content-Type</name>
        //                         <value>"content type data"</value>
        //                    </HttpHeader>
        //                    <HttpHeader>
        //                         <name>SOAPAction</name>
        //                         <value>soap action</value>
        //                     </HttpHeader>
        //                    ....
        //                </HttpHeaders>
        //              </SecureStop>
        //            </PlayReadyKeyMessage>
                
        // TODO: send the secure stop challenge to a server that handles the secure stop challenge

        // TODO: Receive and response and call event.target.Update() to proecess the response
    });
    
    // add 'keyerror' eventhandler
    g_keySession.addEventListener('mskeyerror', function (event) {
        var session = event.target;
        
        ...

        session.close();
    });
    
    // add 'keyadded' eventhandler
    g_keySession.addEventListener('mskeyadded', function (event) {
        
        var session = event.target;

        ...

        session.close();             
    });
}

/**
* desc@ formatSecureStopCDMData
*   generate playready CDMData
*   CDMData is in xml format:
*   <PlayReadyCDMData type="SecureStop">
*     <SecureStop version="1.0">
*       <SessionID>B64 encoded session ID</SessionID>
*       <CustomData>B64 encoded custom data</CustomData>
*       <ServerCert>B64 encoded server cert</ServerCert>
*     </SecureCert>
* </PlayReadyCDMData>        
*/
function formatSecureStopCDMData(encodedSessionId, customData, encodedPublisherCert) 
{
    var encodedCustomData = null;

    // TODO: base64 encode the custom data and place the encoded result to encodedCustomData

    var CDMDataStr = "<PlayReadyCDMData type=\"SecureStop\">" +
                     "<SecureStop version=\"1.0\" >" +
                     "<SessionID>" + encodedSessionId + "</SessionID>" +
                     "<CustomData>" + encodedCustomData + "</CustomData>" +
                     "<ServerCert>" + encodedPublisherCert + "</ServerCert>" +
                     "</SecureStop></PlayReadyCDMData>";
    
    var int8ArrayCDMdata = null

    // TODO: Convert CDMDataStr to Uint8 byte array and palce the converted result to int8ArrayCDMdata

    return int8ArrayCDMdata;
}
```

> [!NOTE]
> <span data-ttu-id="4cd36-159">データのセキュリティで保護された停止の`<SessionID>B64 encoded session ID</SessionID>`上の例では、アスタリスクを指定できます (\*)、記録されたすべての停止をセキュリティで保護されたセッションはワイルド カード。</span><span class="sxs-lookup"><span data-stu-id="4cd36-159">The secure stop data’s `<SessionID>B64 encoded session ID</SessionID>` in the sample above can be an asterisk (\*), which is a wild card for all the secure stop sessions recorded.</span></span> <span data-ttu-id="4cd36-160">つまり、 **SessionID**タグは、特定のセッションまたはワイルドカード (\*) をセキュリティで保護された停止のすべてのセッションを選択します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-160">That is, the **SessionID** tag can be a specific session, or a wild card (\*) to select all the secure stop sessions.</span></span>

## <a name="programming-considerations-for-encrypted-media-extension"></a><span data-ttu-id="4cd36-161">Encrypted Media Extension のプログラミングについての考慮事項</span><span class="sxs-lookup"><span data-stu-id="4cd36-161">Programming considerations for Encrypted Media Extension</span></span>

<span data-ttu-id="4cd36-162">このセクションでは、Windows 10 用の PlayReady 対応の web アプリを作成するときに考慮するプログラミングの考慮事項を示します。</span><span class="sxs-lookup"><span data-stu-id="4cd36-162">This section lists the programming considerations that you should take into account when creating your PlayReady-enabled web app for Windows 10.</span></span>

<span data-ttu-id="4cd36-163">アプリで作成した **MSMediaKeys** オブジェクトと **MSMediaKeySession** オブジェクトは、アプリが終了するまで有効なままである必要があります。</span><span class="sxs-lookup"><span data-stu-id="4cd36-163">The **MSMediaKeys** and **MSMediaKeySession** objects created by your app must be kept alive until your app closes.</span></span> <span data-ttu-id="4cd36-164">これらのオブジェクトが必ず有効な状態にとどまるようにする方法の 1 つは、それらをグローバル変数として割り当てることです (関数内でローカル変数宣言された場合、変数はスコープ外になり、ガベージ コレクションの対象になります)。</span><span class="sxs-lookup"><span data-stu-id="4cd36-164">One way of ensuring these objects stay alive is to assign them as global variables (the variables would become out of scope and subject to garbage collection if declared as a local variable inside of a function).</span></span> <span data-ttu-id="4cd36-165">たとえば、次の例は、変数を割り当てられます*g\_msMediaKeys*と*g\_mediaKeySession*グローバル変数は、次に割り当てられる、 **。MSMediaKeys**と**MSMediaKeySession**関数内のオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="4cd36-165">For example, the following sample assigns the variables *g\_msMediaKeys* and *g\_mediaKeySession* as global variables, which are then assigned to the **MSMediaKeys** and **MSMediaKeySession** objects in the function.</span></span>

``` syntax
var g_msMediaKeys;
var g_mediaKeySession;

function foo() {
  ...
  g_msMediaKeys = new MSMediaKeys("com.microsoft.playready");
  ...
  g_mediaKeySession = g_msMediaKeys.createSession("video/mp4", intiData, null);
  g_mediaKeySession.addEventListener(this.KEYMESSAGE_EVENT, function (e) 
  {
    ...
    downloadPlayReadyKey(url, keyMessage, function (data) 
    {
      g_mediaKeySession.update(data);
    });
  });
  g_mediaKeySession.addEventListener(this.KEYADDED_EVENT, function () 
  {
    ...
    g_mediaKeySession.close();
    g_mediaKeySession = null;
  });
}
```

<span data-ttu-id="4cd36-166">詳しくは、[サンプル アプリケーション](https://code.msdn.microsoft.com/windowsapps/PlayReady-samples-for-124a3738)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4cd36-166">For more information, see the [sample applications](https://code.msdn.microsoft.com/windowsapps/PlayReady-samples-for-124a3738).</span></span>

## <a name="see-also"></a><span data-ttu-id="4cd36-167">関連項目</span><span class="sxs-lookup"><span data-stu-id="4cd36-167">See also</span></span>
- [<span data-ttu-id="4cd36-168">PlayReady DRM</span><span class="sxs-lookup"><span data-stu-id="4cd36-168">PlayReady DRM</span></span>](playready-client-sdk.md)




