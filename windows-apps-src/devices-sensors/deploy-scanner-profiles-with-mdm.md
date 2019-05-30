---
title: MDM によるバーコード スキャナー プロファイルの展開
description: バーコード スキャナー プロファイルは、MDM サーバーを使って展開できます。
ms.assetid: 99ED3BD8-022C-40C2-9C65-F599186548FE
ms.date: 09/26/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: e92c4c715608f9ae36adb3a67beec8002083542f
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370286"
---
# <a name="deploy-barcode-scanner-profiles-with-mdm"></a><span data-ttu-id="cb2e2-104">MDM によるバーコード スキャナー プロファイルの展開</span><span class="sxs-lookup"><span data-stu-id="cb2e2-104">Deploy barcode scanner profiles with MDM</span></span>

<span data-ttu-id="cb2e2-105">**注**  この機能では Windows 10 Mobile 以降。</span><span class="sxs-lookup"><span data-stu-id="cb2e2-105">**Note**  This feature requires Windows 10 Mobile or later.</span></span>

<span data-ttu-id="cb2e2-106">バーコード スキャナー プロファイルは、MDM サーバーを使って展開できます。</span><span class="sxs-lookup"><span data-stu-id="cb2e2-106">Barcode scanner profiles can be deployed with an MDM server.</span></span> <span data-ttu-id="cb2e2-107">使用して、プロファイルを展開する*OemProfile*で、 [EnterpriseExtFileSystem CSP](https://docs.microsoft.com/windows/client-management/mdm/enterpriseextfilessystem-csp)に配置することに、\\データ\\SharedData\\OEM\\パブリック\\プロファイル フォルダー。</span><span class="sxs-lookup"><span data-stu-id="cb2e2-107">To deploy the profiles, use *OemProfile* in the [EnterpriseExtFileSystem CSP](https://docs.microsoft.com/windows/client-management/mdm/enterpriseextfilessystem-csp) to place them into the \\Data\\SharedData\\OEM\\Public\\Profile folder.</span></span> <span data-ttu-id="cb2e2-108">ドライバーの製造元では、これらのスキャナー プロファイルを使用して、API サーフェスを通じて公開されていない設定を構成できます。</span><span class="sxs-lookup"><span data-stu-id="cb2e2-108">These scanner profiles can then be used by driver manufacturers to configure settings that are not exposed through the API surface.</span></span>

<span data-ttu-id="cb2e2-109">Microsoft では、スキャナーのプロファイルやそれらを実装する方法の詳細を定義していません。</span><span class="sxs-lookup"><span data-stu-id="cb2e2-109">Microsoft does not define the specifics of a scanner profile or how to implement them.</span></span>

## <a name="related-topics"></a><span data-ttu-id="cb2e2-110">関連トピック</span><span class="sxs-lookup"><span data-stu-id="cb2e2-110">Related topics</span></span>
- [<span data-ttu-id="cb2e2-111">EnterpriseExtFileSystem CSP</span><span class="sxs-lookup"><span data-stu-id="cb2e2-111">EnterpriseExtFileSystem CSP</span></span>](https://docs.microsoft.com/windows/client-management/mdm/enterpriseextfilessystem-csp)
- [<span data-ttu-id="cb2e2-112">バーコード スキャナのデバイスのサポート</span><span class="sxs-lookup"><span data-stu-id="cb2e2-112">Barcode scanner device support</span></span>](https://docs.microsoft.com/en-us/windows/uwp/devices-sensors/pos-device-support#barcode-scanner)