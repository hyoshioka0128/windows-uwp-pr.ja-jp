---
author: mijacobs
Description: 多くの企業では、不要なトラフィックをブロックするのにファイアウォールを使用します。 このドキュメントでは、ファイアウォールを通過する WNS トラフィックを許可する方法について説明します。
title: WNS のトラフィックをファイアウォールの許可リストに追加します。
ms.assetid: 2125B09F-DB90-4515-9AA6-516C7E9ACCCD
template: detail.hbs
ms.author: mijacobs
ms.date: 05/20/2019
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10、uwp、WNS の場合、windows 通知サービス、通知、windows ファイアウォール、トラブルシューティング、IP、トラフィック、enterprise、ネットワーク、パブリック IP アドレス、IPv4、VIP、FQDN
ms.localizationpriority: medium
ms.openlocfilehash: 9ed4ad6ed828abda9d487ef96beca9b655c92421
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366677"
---
# <a name="allowing-windows-notification-traffic-through-enterprise-firewalls"></a><span data-ttu-id="2d84e-105">エンタープライズ ファイアウォールを介した Windows の通知のトラフィックを許可します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-105">Allowing Windows Notification traffic through enterprise firewalls</span></span>

## <a name="background"></a><span data-ttu-id="2d84e-106">背景</span><span class="sxs-lookup"><span data-stu-id="2d84e-106">Background</span></span>
<span data-ttu-id="2d84e-107">多くの企業では、ファイアウォールを使用して、不要なネットワーク トラフィックをブロックするには残念ながら、Windows 通知サービスの通信などの重要なブロックこれこともできます。</span><span class="sxs-lookup"><span data-stu-id="2d84e-107">Many enterprises use firewalls to block unwanted network traffic; unfortunately, this can also block important things like Windows Notification Service communications.</span></span> <span data-ttu-id="2d84e-108">つまり、WNS から送信されるすべての通知は破棄されます。</span><span class="sxs-lookup"><span data-stu-id="2d84e-108">This means all notifications sent through WNS will be dropped.</span></span> <span data-ttu-id="2d84e-109">これを回避するには、ネットワーク管理者は、ファイアウォールを通過する WNS トラフィックを許可するには、その除外リストに承認済みの WNS チャネルの一覧を追加できます。</span><span class="sxs-lookup"><span data-stu-id="2d84e-109">To avoid this, network admins can add the list of approved WNS channels to their exemption list to allow the WNS traffic to pass through the firewall.</span></span> <span data-ttu-id="2d84e-110">方法の詳細および追加するものを次に示します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-110">Below are more details on how and what to add.</span></span> 


## <a name="what-information-should-be-added-to-the-allowlist"></a><span data-ttu-id="2d84e-111">どのような情報は、許可リストに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d84e-111">What information should be added to the allowlist</span></span>
<span data-ttu-id="2d84e-112">以下は、Fqdn、Vip、および IP を含むリスト アドレス範囲、Windows 通知サービスで使用します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-112">Below is a list that contains the FQDNs, VIPs, and IP address ranges used by the Windows Notification Service.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2d84e-113">強くお勧め fqdn を一覧できるようにすることため、これらは変更されません。</span><span class="sxs-lookup"><span data-stu-id="2d84e-113">We strongly suggest that you allow list by FQDN, because these will not change.</span></span> <span data-ttu-id="2d84e-114">Fqdn ボックスの一覧を許可する場合も IP アドレスの範囲を許可する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="2d84e-114">If you allow list by FQDN, you do not need to also allow the IP address ranges.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d84e-115">IP アドレスの範囲が定期的に変更されます。このため、このページは含まれません。</span><span class="sxs-lookup"><span data-stu-id="2d84e-115">The IP address ranges will change periodically; because of this, they are not included on this page.</span></span> <span data-ttu-id="2d84e-116">IP 範囲の一覧を表示する場合は、ダウンロード センターからファイルをダウンロードできます。[Windows 通知サービス (WNS) の VIP と IP の範囲は](https://www.microsoft.com/download/details.aspx?id=44238)します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-116">If you want to see the list of IP ranges, you can download the file from Download Center: [Windows Notification Service (WNS) VIP and IP Ranges](https://www.microsoft.com/download/details.aspx?id=44238).</span></span> <span data-ttu-id="2d84e-117">確認してください、最新の情報があるかどうかを確認するには、定期的にバックアップします。</span><span class="sxs-lookup"><span data-stu-id="2d84e-117">Please check back regularly to make sure you have the most up-to-date information.</span></span> 


### <a name="fqdns-vips-and-ips"></a><span data-ttu-id="2d84e-118">Fqdn、Vip、および ip アドレス</span><span class="sxs-lookup"><span data-stu-id="2d84e-118">FQDNs, VIPs, and IPs</span></span>
<span data-ttu-id="2d84e-119">それに続くテーブルで各次の XML ドキュメント内の要素の説明 (で[用語と表記](#terms-and-notations)します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-119">Each of the elements in the following XML document is explained in the table that follows it (in [Terms and Notations](#terms-and-notations).</span></span> <span data-ttu-id="2d84e-120">IP の範囲は、Fqdn を一定に保たれます Fqdn のみを使用することを促すには、このドキュメントから意図的にありました。</span><span class="sxs-lookup"><span data-stu-id="2d84e-120">The IP ranges were intentionally left out of this document to encourage you to use only the FQDNs as the FQDNs will remain constant.</span></span> <span data-ttu-id="2d84e-121">ただし、ダウンロード センターから完全な一覧を含む XML ファイルをダウンロードすることができます。[Windows 通知サービス (WNS) の VIP と IP の範囲は](https://www.microsoft.com/download/details.aspx?id=44238)します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-121">However, you can download the XML file containing the complete list from Download Center: [Windows Notification Service (WNS) VIP and IP Ranges](https://www.microsoft.com/download/details.aspx?id=44238).</span></span> <span data-ttu-id="2d84e-122">新しい Vip または IP 範囲がある**1 つの日の週はアップロード後**します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-122">New VIPs or IP ranges will be **effective one week after they are uploaded**.</span></span>

```XML
<?xml version="1.0" encoding="UTF-8"?>
<WNSPublicIpAddresses xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <!-- This file contains the FQDNs, VIPs, and IP address ranges used by the Windows Notification Service. A new text file will be uploaded every time a new VIP or IP range is released in production.  Please copy the below information and perform the necessary changes on your site. Endpoints in CloudService nodes are used for cloud services to send notifications to WNS. Endpoints in Client nodes are used by devices to receive notifications from WNS. --> 
    <CloudServiceDNS>
    <DNS FQDN="*.notify.windows.com"/>
    </CloudServiceDNS>
    <ClientDNS>
        <DNS FQDN="*.wns.windows.com"/>
        <DNS FQDN="*.notify.live.net"/>
    </ClientDNS>
    <CloudServiceIPs>
        <IpRange Subnet=""/>
        <!-- See the file in Download Center for the complete list of IP ranges -->
    </CloudServiceIPs>
    <ClientIPsIPv4>
        <IpRange Subnet=""/>
        <!-- See the file in Download Center for the complete list of IP ranges -->
    </ClientIPsIPv4>
</WNSPublicIpAddresses>

```

### <a name="terms-and-notations"></a><span data-ttu-id="2d84e-123">用語との表記</span><span class="sxs-lookup"><span data-stu-id="2d84e-123">Terms and notations</span></span>
<span data-ttu-id="2d84e-124">表記と上記の XML スニペットで使用される要素の説明を次に示します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-124">Below are explanations on the notations and elements used in the above XML snippet.</span></span>

| <span data-ttu-id="2d84e-125">用語</span><span class="sxs-lookup"><span data-stu-id="2d84e-125">Term</span></span> | <span data-ttu-id="2d84e-126">説明</span><span class="sxs-lookup"><span data-stu-id="2d84e-126">Explanation</span></span> |
|---|---|
| <span data-ttu-id="2d84e-127">**ドット数値記法 (つまり 64.4.28.0/26)**</span><span class="sxs-lookup"><span data-stu-id="2d84e-127">**Dot-decimal notation (i.e. 64.4.28.0/26)**</span></span> | <span data-ttu-id="2d84e-128">ドット数値記法は、範囲の IP アドレスを記述する方法です。</span><span class="sxs-lookup"><span data-stu-id="2d84e-128">Dot-decimal notation is a way to describe the range of IP addresses.</span></span> <span data-ttu-id="2d84e-129">たとえば、64.4.28.0/26 64.4.28.0 の最初の 26 のビットは定数、最後の 6 ビットは変数を意味します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-129">For example, 64.4.28.0/26 means the first 26 bits of 64.4.28.0 are constant, while the last 6 bits are variable.</span></span>  <span data-ttu-id="2d84e-130">この場合は、IPv4 の範囲は、64.4.28.0 - 64.4.28.63 します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-130">In this case, the IPv4 range is 64.4.28.0 - 64.4.28.63.</span></span> |
| <span data-ttu-id="2d84e-131">**ClientDNS**</span><span class="sxs-lookup"><span data-stu-id="2d84e-131">**ClientDNS**</span></span> | <span data-ttu-id="2d84e-132">これらのクライアント デバイス (Windows Pc、デスクトップ) の完全修飾ドメイン名 (FQDN) フィルターは、WNS から通知を受信します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-132">These are the Fully-Qualified Domain Name (FQDN) filters for the client devices (Windows PCs, desktops) receiving notifications from WNS.</span></span> <span data-ttu-id="2d84e-133">これらは、WNS クライアント WNS 機能を使用するためにファイアウォールで許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d84e-133">These must be allowed through the firewall in order for WNS clients to use the WNS Functionality.</span></span>  <span data-ttu-id="2d84e-134">お勧め許可一覧に IP/VIP の範囲ではなく Fqdn によってこれらが変更されないためです。</span><span class="sxs-lookup"><span data-stu-id="2d84e-134">It is recommended to allow-list by the FQDNs instead of the IP/VIP ranges, since these will never change.</span></span> |
| <span data-ttu-id="2d84e-135">**ClientIPsIPv4**</span><span class="sxs-lookup"><span data-stu-id="2d84e-135">**ClientIPsIPv4**</span></span> | <span data-ttu-id="2d84e-136">これらは、クライアント デバイス (Windows Pc、デスクトップ) からアクセスされるサーバーの IPv4 アドレス WNS から通知を受信します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-136">These are the IPv4 addresses of the servers accessed by client devices (Windows PCs, desktops) receiving notifications from WNS.</span></span> |
| <span data-ttu-id="2d84e-137">**CloudServiceDNS**</span><span class="sxs-lookup"><span data-stu-id="2d84e-137">**CloudServiceDNS**</span></span> | <span data-ttu-id="2d84e-138">これらは、WNS に notificatios を送信する、クラウド サービスと対話する WNS サーバーの完全修飾ドメイン名 (FQDN) のフィルターです。</span><span class="sxs-lookup"><span data-stu-id="2d84e-138">These are the Fully-Qualified Domain Name (FQDN) filters for the WNS servers your cloud service will talk to to send notificatios to WNS.</span></span> <span data-ttu-id="2d84e-139">これらは、WNS 通知を送信するサービスのためにファイアウォールで許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2d84e-139">These must be allowed through the firewall in order for services to send WNS notifications.</span></span>  <span data-ttu-id="2d84e-140">お勧め許可一覧に IP/VIP の範囲ではなく Fqdn によってこれらが変更されないためです。</span><span class="sxs-lookup"><span data-stu-id="2d84e-140">It is recommended to allow-list by the FQDNs instead of the IP/VIP ranges, since these will never change.</span></span>|
| <span data-ttu-id="2d84e-141">**CloudServiceIPs**</span><span class="sxs-lookup"><span data-stu-id="2d84e-141">**CloudServiceIPs**</span></span> | <span data-ttu-id="2d84e-142">CloudServiceIPs は cloud services に WNS 通知を送信するために使用するサーバーの IPv4 アドレスです。</span><span class="sxs-lookup"><span data-stu-id="2d84e-142">CloudServiceIPs are the IPv4 addresses of the servers used for cloud services to send notifications to WNS</span></span>  |


## <a name="microsoft-push-notifications-service-mpns-public-ip-ranges"></a><span data-ttu-id="2d84e-143">Microsoft プッシュ通知サービス (MPNS) パブリック IP 範囲</span><span class="sxs-lookup"><span data-stu-id="2d84e-143">Microsoft Push Notifications Service (MPNS) public IP ranges</span></span>
<span data-ttu-id="2d84e-144">MPNS、従来の通知サービスを使用している場合は、許可一覧に追加する必要があります IP アドレスの範囲は使用可能なダウンロード センターから。[Microsoft プッシュ通知サービス (MPNS) のパブリック IP の範囲は](https://www.microsoft.com/download/details.aspx?id=44535)します。</span><span class="sxs-lookup"><span data-stu-id="2d84e-144">If you are using the legacy notification service, MPNS, the IP address ranges that you will need to add to the allow list are available from Download Center: [Microsoft Push Notifications Service (MPNS) Public IP ranges](https://www.microsoft.com/download/details.aspx?id=44535).</span></span>


## <a name="related-topics"></a><span data-ttu-id="2d84e-145">関連トピック</span><span class="sxs-lookup"><span data-stu-id="2d84e-145">Related topics</span></span>

* <span data-ttu-id="2d84e-146">[クイック スタート:プッシュ通知を送信します。](https://docs.microsoft.com/previous-versions/windows/apps/hh868252(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="2d84e-146">[Quickstart: Sending a push notification](https://docs.microsoft.com/previous-versions/windows/apps/hh868252(v=win.10))</span></span>
* <span data-ttu-id="2d84e-147">[要求、作成、および通知チャネルを保存する方法](https://docs.microsoft.com/previous-versions/windows/apps/hh465412(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="2d84e-147">[How to request, create, and save a notification channel](https://docs.microsoft.com/previous-versions/windows/apps/hh465412(v=win.10))</span></span>
* <span data-ttu-id="2d84e-148">[アプリケーションを実行するための通知をインターセプトする方法](https://docs.microsoft.com/previous-versions/windows/apps/jj709907(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="2d84e-148">[How to intercept notifications for running applications](https://docs.microsoft.com/previous-versions/windows/apps/jj709907(v=win.10))</span></span>
* <span data-ttu-id="2d84e-149">[Windows プッシュ通知サービス (WNS) とを認証する方法](https://docs.microsoft.com/previous-versions/windows/apps/hh465407(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="2d84e-149">[How to authenticate with the Windows Push Notification Service (WNS)](https://docs.microsoft.com/previous-versions/windows/apps/hh465407(v=win.10))</span></span>
* <span data-ttu-id="2d84e-150">[プッシュ通知サービスの要求および応答ヘッダー](https://docs.microsoft.com/previous-versions/windows/apps/hh465435(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="2d84e-150">[Push notification service request and response headers](https://docs.microsoft.com/previous-versions/windows/apps/hh465435(v=win.10))</span></span>
* [<span data-ttu-id="2d84e-151">プッシュ通知のガイドラインとチェックリスト</span><span class="sxs-lookup"><span data-stu-id="2d84e-151">Guidelines and checklist for push notifications</span></span>](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)
 
