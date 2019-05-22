---
Description: Windows アプリのパッケージにパッケージ化したデスクトップ アプリケーションで Windows 10 ユーザー向けの最新のエクスペリエンスを追加する方法について説明します。
title: パッケージのデスクトップ アプリを最新化します。
ms.date: 04/22/2019
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 6d71233bc7b96af9d9b261406d6b149f36f65f29
ms.sourcegitcommit: f0f933d5cf0be734373a7b03e338e65000cc3d80
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65985292"
---
# <a name="features-that-require-package-identity"></a><span data-ttu-id="51d3a-104">パッケージ id が必要な機能</span><span class="sxs-lookup"><span data-stu-id="51d3a-104">Features that require package identity</span></span>

<span data-ttu-id="51d3a-105">使用してデスクトップ アプリを更新する場合[最新の Windows 10 エクスペリエンス](index.md)、多くの機能が MSIX パッケージにパッケージ化、デスクトップ アプリでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="51d3a-105">If you want to update your desktop app with [modern Windows 10 experiences](index.md), many features are available only in desktop apps that are packaged in an MSIX package.</span></span>

<span data-ttu-id="51d3a-106">MSIX には、すべての Windows アプリ、WPF、Windows フォーム、Win32 アプリのユニバーサル パッケージ化エクスペリエンスを提供する最新 Windows アプリ パッケージ形式です。</span><span class="sxs-lookup"><span data-stu-id="51d3a-106">MSIX is a modern Windows app package format that provides a universal packaging experience for all Windows apps, WPF, Windows Forms and Win32 apps.</span></span> <span data-ttu-id="51d3a-107">デスクトップの Windows アプリをパッケージ化するには、ライブ タイルや通知などの最新の Windows 10 エクスペリエンスをアプリに統合することができます。</span><span class="sxs-lookup"><span data-stu-id="51d3a-107">Packaging your desktop Windows apps enables you to integrate modern Windows 10 experiences such as live tiles and notifications into your apps.</span></span> <span data-ttu-id="51d3a-108">また、堅牢なインストールと更新エクスペリエンス、機能の柔軟性の高いシステムでは、Microsoft Store、エンタープライズ管理、および多くのカスタムの配布モデルのサポートで管理セキュリティ モデルへのアクセスを取得します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-108">It also gets you access to a robust installation and updating experience, a managed security model with a flexible capability system, support for the Microsoft Store, enterprise management, and many custom distribution models.</span></span> <span data-ttu-id="51d3a-109">詳細については、次を参照してください。[デスクトップ アプリケーションをパッケージ化](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)MSIX ドキュメント。</span><span class="sxs-lookup"><span data-stu-id="51d3a-109">For more information, see [Package desktop applications](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root) in the MSIX documentation.</span></span>

<span data-ttu-id="51d3a-110">デスクトップ アプリをパッケージ化する場合は、パッケージ id、パッケージの拡張機能、およびパッケージ化されたアプリでの UWP コンポーネントを必要とする UWP Api を使用できます。</span><span class="sxs-lookup"><span data-stu-id="51d3a-110">If you package your desktop app, you can then use UWP APIs that require package identity, package extensions, and UWP components in your packaged app.</span></span> <span data-ttu-id="51d3a-111">詳細については、次の記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="51d3a-111">For more information, see these articles.</span></span>

## <a name="use-uwp-apis-that-require-package-identity"></a><span data-ttu-id="51d3a-112">パッケージ id を必要とする UWP Api を使用して、</span><span class="sxs-lookup"><span data-stu-id="51d3a-112">Use UWP APIs that require package identity</span></span>

<span data-ttu-id="51d3a-113">一部の UWP Api を必要と[パッケージ identity](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-identity)デスクトップ アプリで使用します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-113">Some UWP APIs require [package identity](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-identity) to be used in a desktop app.</span></span> <span data-ttu-id="51d3a-114">(パッケージ マニフェストを含む) MSIX パッケージは、この id を提供します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-114">The MSIX package (including the package manifest) provides this identity.</span></span>

<span data-ttu-id="51d3a-115">詳細については、次を参照してください。 [Api の一覧はこの](desktop-to-uwp-supported-api.md#list-of-apis)します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-115">For more information, see [this list of APIs](desktop-to-uwp-supported-api.md#list-of-apis).</span></span>

## <a name="integrate-with-package-extensions"></a><span data-ttu-id="51d3a-116">パッケージの拡張機能との統合します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-116">Integrate with package extensions</span></span>

<span data-ttu-id="51d3a-117">アプリケーションは、システムと統合する必要がある場合 (例: ファイアウォール規則の確立) と、アプリケーションのパッケージ マニフェストではこの記述、システムが処理してくれます。</span><span class="sxs-lookup"><span data-stu-id="51d3a-117">If your application needs to integrate with the system (For example: establish firewall rules), describe those things in the package manifest of your application and the system will do the rest.</span></span> <span data-ttu-id="51d3a-118">これらのタスクのほとんどは、まったくコードを記述する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="51d3a-118">For most of these tasks, you won't have to write any code at all.</span></span> <span data-ttu-id="51d3a-119">Xml マニフェスト内のビットを使用して操作を実行できます、ユーザーがログオンしたときにプロセスを開始、ファイル エクスプ ローラーで、アプリケーションに統合およびアプリケーションを追加するように他のアプリに表示される印刷のターゲットの一覧。</span><span class="sxs-lookup"><span data-stu-id="51d3a-119">With a bit of XML in the manifest, you can do things like start a process when the user logs on, integrate your application into File Explorer, and add your application a list of print targets that appear in other apps.</span></span>

<span data-ttu-id="51d3a-120">詳細については、次を参照してください。[パッケージ拡張機能とデスクトップ アプリを統合](desktop-to-uwp-extensions.md)します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-120">For more information, see [Integrate your desktop app with package extensions](desktop-to-uwp-extensions.md).</span></span>

## <a name="extend-with-uwp-components"></a><span data-ttu-id="51d3a-121">UWP コンポーネントを拡張します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-121">Extend with UWP components</span></span>

<span data-ttu-id="51d3a-122">一部の Windows 10 エクスペリエンス (タッチ対応 UI ページなど) は、最新のアプリ コンテナー内で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="51d3a-122">Some Windows 10 experiences (For example: a touch-enabled UI page) must run inside of a modern app container.</span></span> <span data-ttu-id="51d3a-123">一般に、最初に決定する必要あるかどうかによって、エクスペリエンスを追加することができます[強化](desktop-to-uwp-enhance.md)UWP Api を使用した既存のデスクトップ アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="51d3a-123">In general, you should first determine whether you can add your experience by [enhancing](desktop-to-uwp-enhance.md) your existing desktop application with UWP APIs.</span></span> <span data-ttu-id="51d3a-124">コード型の場合は、エクスペリエンスを実現するために、UWP コンポーネントを使用する必要が UWP プロジェクトをソリューションに追加するアプリ サービスを使用して、お客様のデスクトップ アプリケーションと UWP コンポーネント間の通信し、ことができます。</span><span class="sxs-lookup"><span data-stu-id="51d3a-124">If you have to use a UWP component, to achieve the experience, then you can add a UWP project to your solution and use app services to communicate between your desktop application and the UWP component.</span></span>

<span data-ttu-id="51d3a-125">詳細については、次を参照してください。 [UWP コンポーネントを使ってデスクトップ アプリを拡張](desktop-to-uwp-extend.md)します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-125">For more information, see [Extend your desktop app with UWP components](desktop-to-uwp-extend.md).</span></span>

## <a name="distribute"></a><span data-ttu-id="51d3a-126">配布</span><span class="sxs-lookup"><span data-stu-id="51d3a-126">Distribute</span></span>

<span data-ttu-id="51d3a-127">アプリケーションを配布するには、Microsoft Store を発行すること、またはサイドローディングによって他のシステムにします。</span><span class="sxs-lookup"><span data-stu-id="51d3a-127">You can distribute your application by publishing it the Microsoft Store or by sideloading it onto other systems.</span></span>

<span data-ttu-id="51d3a-128">参照してください[パッケージ化されたデスクトップ アプリを配布](desktop-to-uwp-distribute.md)します。</span><span class="sxs-lookup"><span data-stu-id="51d3a-128">See [Distribute your packaged desktop app](desktop-to-uwp-distribute.md).</span></span>
