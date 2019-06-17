---
Description: ユニバーサル Windows プラットフォーム (UWP) Api を使用して、Windows 10 ユーザー向けのデスクトップ アプリケーションを強化します。
title: デスクトップ アプリでの UWP Api を使用します。
ms.date: 04/19/2019
ms.topic: article
keywords: windows 10, uwp
ms.author: mcleans
author: mcleanbyron
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4846a29e914ffed15e4c3dea938cc51cefd566e0
ms.sourcegitcommit: b9e2cd5232ad98f4ef367881b92000a3ae610844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "67131944"
---
# <a name="call-uwp-apis-in-desktop-apps"></a><span data-ttu-id="a7ac6-104">デスクトップ アプリでの UWP Api を呼び出す</span><span class="sxs-lookup"><span data-stu-id="a7ac6-104">Call UWP APIs in desktop apps</span></span>

<span data-ttu-id="a7ac6-105">ユニバーサル Windows プラットフォーム (UWP) Api を使用すると、最新のエクスペリエンスを Windows 10 ユーザー向けに磨きをかける、デスクトップ アプリに追加します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-105">You can use Universal Windows Platform (UWP) APIs to add modern experiences to your desktop apps that light up for Windows 10 users.</span></span>

<span data-ttu-id="a7ac6-106">最初に、必要な参照を使用してプロジェクトを設定します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-106">First, set up your project with the required references.</span></span> <span data-ttu-id="a7ac6-107">次に、Windows 10 のエクスペリエンスをデスクトップ アプリに追加するコードから UWP Api を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-107">Then, call UWP APIs from your code to add Windows 10 experiences to your desktop app.</span></span> <span data-ttu-id="a7ac6-108">Windows 10 のユーザーを個別にビルドまたは実行する Windows のバージョンに関係なくすべてのユーザーに同じバイナリを配布できます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-108">You can build separately for Windows 10 users or distribute the same binaries to all users regardless of which version of Windows they run.</span></span>

<span data-ttu-id="a7ac6-109">一部の UWP Api はパッケージ化されているデスクトップ アプリでのみサポートされている、 [MSIX パッケージ](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-109">Some UWP APIs are supported only in desktop apps that are packaged in an [MSIX package](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root).</span></span> <span data-ttu-id="a7ac6-110">詳細については、次を参照してください。[利用可能な UWP Api](desktop-to-uwp-supported-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-110">For more information, see [Available UWP APIs](desktop-to-uwp-supported-api.md).</span></span>

## <a name="set-up-your-project"></a><span data-ttu-id="a7ac6-111">プロジェクトを設定します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-111">Set up your project</span></span>

<span data-ttu-id="a7ac6-112">UWP API を使用するには、プロジェクトにいくつかの変更を加える必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-112">You'll have to make a few changes to your project to use UWP APIs.</span></span>

### <a name="modify-a-net-project-to-use-windows-runtime-apis"></a><span data-ttu-id="a7ac6-113">Windows ランタイム Api を使用する .NET プロジェクトを変更します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-113">Modify a .NET project to use Windows Runtime APIs</span></span>

1. <span data-ttu-id="a7ac6-114">**[参照マネージャー]** ダイアログ ボックスを開き、 **[参照]** ボタンを選択して、 **[すべてのファイル]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-114">Open the **Reference Manager** dialog box, choose the **Browse** button, and then select  **All Files**.</span></span>

    ![[参照の追加] ダイアログ ボックス](images/desktop-to-uwp/browse-references.png)

2. <span data-ttu-id="a7ac6-116">これらのファイルへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-116">Add a reference to these files.</span></span>

  |<span data-ttu-id="a7ac6-117">ファイル</span><span class="sxs-lookup"><span data-stu-id="a7ac6-117">File</span></span>|<span data-ttu-id="a7ac6-118">Location</span><span class="sxs-lookup"><span data-stu-id="a7ac6-118">Location</span></span>|
  |--|--|
  |<span data-ttu-id="a7ac6-119">System.Runtime.WindowsRuntime</span><span class="sxs-lookup"><span data-stu-id="a7ac6-119">System.Runtime.WindowsRuntime</span></span>|<span data-ttu-id="a7ac6-120">C:\Windows\Microsoft.NET\Framework\v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="a7ac6-120">C:\Windows\Microsoft.NET\Framework\v4.0.30319</span></span>|
  |<span data-ttu-id="a7ac6-121">System.Runtime.WindowsRuntime.UI.Xaml</span><span class="sxs-lookup"><span data-stu-id="a7ac6-121">System.Runtime.WindowsRuntime.UI.Xaml</span></span>|<span data-ttu-id="a7ac6-122">C:\Windows\Microsoft.NET\Framework\v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="a7ac6-122">C:\Windows\Microsoft.NET\Framework\v4.0.30319</span></span>|
  |<span data-ttu-id="a7ac6-123">System.Runtime.InteropServices.WindowsRuntime</span><span class="sxs-lookup"><span data-stu-id="a7ac6-123">System.Runtime.InteropServices.WindowsRuntime</span></span>|<span data-ttu-id="a7ac6-124">C:\Windows\Microsoft.NET\Framework\v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="a7ac6-124">C:\Windows\Microsoft.NET\Framework\v4.0.30319</span></span>|
  |<span data-ttu-id="a7ac6-125">windows.winmd</span><span class="sxs-lookup"><span data-stu-id="a7ac6-125">windows.winmd</span></span>|<span data-ttu-id="a7ac6-126">C:\Program Files (x86)\Windows Kits\10\UnionMetadata\\<*sdk version*>\Facade</span><span class="sxs-lookup"><span data-stu-id="a7ac6-126">C:\Program Files (x86)\Windows Kits\10\UnionMetadata\\<*sdk version*>\Facade</span></span>|
  |<span data-ttu-id="a7ac6-127">Windows.Foundation.UniversalApiContract.winmd</span><span class="sxs-lookup"><span data-stu-id="a7ac6-127">Windows.Foundation.UniversalApiContract.winmd</span></span>|<span data-ttu-id="a7ac6-128">C:\Program Files (x86)\Windows Kits\10\References\\<*sdk version*>\Windows.Foundation.UniversalApiContract\<*version*></span><span class="sxs-lookup"><span data-stu-id="a7ac6-128">C:\Program Files (x86)\Windows Kits\10\References\\<*sdk version*>\Windows.Foundation.UniversalApiContract\<*version*></span></span>|
  |<span data-ttu-id="a7ac6-129">Windows.Foundation.FoundationContract.winmd</span><span class="sxs-lookup"><span data-stu-id="a7ac6-129">Windows.Foundation.FoundationContract.winmd</span></span>|<span data-ttu-id="a7ac6-130">C:\Program Files (x86)\Windows Kits\10\References\\<*sdk version*>\Windows.Foundation.FoundationContract\<*version*></span><span class="sxs-lookup"><span data-stu-id="a7ac6-130">C:\Program Files (x86)\Windows Kits\10\References\\<*sdk version*>\Windows.Foundation.FoundationContract\<*version*></span></span>|

3. <span data-ttu-id="a7ac6-131">**[プロパティ]** ウィンドウで、各 *.winmd* ファイルの **[ローカルにコピー]** フィールドを **[False]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-131">In the **Properties** window, set the **Copy Local** field of each *.winmd* file to **False**.</span></span>

    ![[ローカルにコピー] フィールド](images/desktop-to-uwp/copy-local-field.png)

### <a name="modify-a-c-project-to-use-windows-runtime-apis"></a><span data-ttu-id="a7ac6-133">Windows ランタイム Api を使用する C++ プロジェクトを変更します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-133">Modify a C++ project to use Windows Runtime APIs</span></span>

<span data-ttu-id="a7ac6-134">使用[C +/cli WinRT](https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/) Windows ランタイム Api を使用します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-134">Use [C++/WinRT](https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/) to consume Windows Runtime APIs.</span></span> <span data-ttu-id="a7ac6-135">C++/WinRT は Windows ランタイム (WinRT) API の標準的な最新の C++17 言語プロジェクションで、ヘッダー ファイル ベースのライブラリとして実装され、最新の Windows API への最上位アクセス権を提供するように設計されています。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-135">C++/WinRT is an entirely standard modern C++17 language projection for Windows Runtime (WinRT) APIs, implemented as a header-file-based library, and designed to provide you with first-class access to the modern Windows API.</span></span>

<span data-ttu-id="a7ac6-136">C++ プロジェクトを構成する/cli WinRT を参照してください[C + を追加する Windows デスクトップ アプリケーション プロジェクトを変更する/cli WinRT サポート](https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/get-started#modify-a-windows-desktop-application-project-to-add-cwinrt-support)します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-136">To configure your project for C++/WinRT, See [Modify a Windows Desktop application project to add C++/WinRT support](https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/get-started#modify-a-windows-desktop-application-project-to-add-cwinrt-support).</span></span>

## <a name="add-windows-10-experiences"></a><span data-ttu-id="a7ac6-137">Windows 10 エクスペリエンスの追加</span><span class="sxs-lookup"><span data-stu-id="a7ac6-137">Add Windows 10 experiences</span></span>

<span data-ttu-id="a7ac6-138">これで、Windows 10 でアプリケーションをユーザーが実行する際に便利になる最新のエクスペリエンスを追加する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-138">Now you're ready to add modern experiences that light up when users run your application on Windows 10.</span></span> <span data-ttu-id="a7ac6-139">次の設計フローを使用します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-139">Use this design flow.</span></span>

<span data-ttu-id="a7ac6-140">:white_check_mark:**最初に、追加するどのようなエクスペリエンスを決定します。**</span><span class="sxs-lookup"><span data-stu-id="a7ac6-140">:white_check_mark: **First, decide what experiences you want to add**</span></span>

<span data-ttu-id="a7ac6-141">選択肢はたくさんあります。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-141">There's lots to choose from.</span></span> <span data-ttu-id="a7ac6-142">たとえば、購買注文の流れを簡略化を使用してできます[Api を収益化](/windows/uwp/monetize)、または[アプリケーションに向ける](/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts)を共有する興味深いものがある場合など、新しい画像を別のユーザーが投稿します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-142">For example, you can simplify your purchase order flow by using [monetization APIs](/windows/uwp/monetize), or [direct attention to your application](/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts) when you have something interesting to share, such as a new picture that another user has posted.</span></span>

![トースト](images/desktop-to-uwp/toast.png)

<span data-ttu-id="a7ac6-144">ユーザーがメッセージを無視したり、非表示にした場合でも、ユーザーはアクション センターで再度メッセージを表示し、クリックすることで、アプリを開くことができます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-144">Even if users ignore or dismiss your message, they can see it again in the action center, and then click on the message to open your app.</span></span> <span data-ttu-id="a7ac6-145">これにより、アプリケーションで engagement を向上し、アプリケーションをオペレーティング システムに深く統合表示の追加されたボーナスが。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-145">This increases engagement with your application and has the added bonus of making your application appear deeply integrated with the operating system.</span></span> <span data-ttu-id="a7ac6-146">見せ経験があることのコードは、この記事で後で説明します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-146">We'll show you the code for that experience a bit later in this article.</span></span>

<span data-ttu-id="a7ac6-147">参照してください、 [UWP ドキュメント](/windows/uwp/get-started/)他のアイデア。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-147">Visit the [UWP documentation](/windows/uwp/get-started/) for more ideas.</span></span>

<span data-ttu-id="a7ac6-148">:white_check_mark:**強化または拡張するかどうかを決定します。**</span><span class="sxs-lookup"><span data-stu-id="a7ac6-148">:white_check_mark: **Decide whether to enhance or extend**</span></span>

<span data-ttu-id="a7ac6-149">使用条件をよく耳を*強化*と*拡張*、平均値を正確にどのようなこれらの各用語の説明には少しご説明しましょう。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-149">You'll often hear us use the terms *enhance* and *extend*, so we'll take a moment to explain exactly what each of these terms mean.</span></span>

<span data-ttu-id="a7ac6-150">という用語*強化*(かどうかを選択した MSIX パッケージ内のアプリケーションをパッケージ化) デスクトップ アプリから直接呼び出すことができる Windows ランタイム Api を記述します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-150">We use the term *enhance* to describe Windows Runtime APIs that you can call directly from your desktop app (whether or not you have chosen to package your application in an MSIX package).</span></span> <span data-ttu-id="a7ac6-151">Windows 10 エクスペリエンスを選択したら、識別を作成し、かどうか、その API に表示されます。 表示する必要のある Api[このリスト](desktop-to-uwp-supported-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-151">When you've chosen a Windows 10 experience, identify the APIs that you need to create it, and then see if that API appears in [this list](desktop-to-uwp-supported-api.md).</span></span> <span data-ttu-id="a7ac6-152">これは、デスクトップ アプリから直接呼び出すことができる Api の一覧です。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-152">This is a list of APIs that you can call directly from your desktop app.</span></span> <span data-ttu-id="a7ac6-153">API がこの一覧に表示されていない場合、その API に関連付けられている機能が UWP プロセス内でしか実行できないことが理由です。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-153">If your API does not appear in this list, that's because the functionality associated with that API can run only within a UWP process.</span></span> <span data-ttu-id="a7ac6-154">多くの場合、UWP のマップ コントロールや Windows こんにちはセキュリティの確認など、UWP XAML をレンダリングする Api が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-154">Often times, these include APIs that render UWP XAML such as a UWP map control or a Windows Hello security prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="a7ac6-155">通常 UWP XAML をレンダリングする Api は、デスクトップから直接呼び出すことはできませんの代替アプローチを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-155">Although APIs that render UWP XAML typically cannot be called directly from your desktop, you might be able to use alternative approaches.</span></span> <span data-ttu-id="a7ac6-156">UWP XAML コントロールまたはその他のカスタム ビジュアル エクスペリエンスをホストする場合は、使用[XAML 諸島](xaml-islands.md)(Windows 10、バージョンが 1903 以降) および[ビジュアル層](visual-layer-in-desktop-apps.md)(Windows 10、バージョン 1803 以降)。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-156">If you want to host UWP XAML controls or other custom visual experiences, you can use [XAML Islands](xaml-islands.md) (starting in Windows 10, version 1903) and the [Visual layer](visual-layer-in-desktop-apps.md) (starting in Windows 10, version 1803).</span></span> <span data-ttu-id="a7ac6-157">これらの機能は、パッケージまたはパッケージ化されていないデスクトップ アプリで使用できます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-157">These features can be used in packaged or unpackaged desktop apps.</span></span>

<span data-ttu-id="a7ac6-158">MSIX パッケージでデスクトップ アプリをパッケージ化することを選択した場合に、別のオプションが、*拡張*UWP プロジェクトをソリューションに追加することで、アプリケーション。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-158">If you have chosen to package your desktop app in an MSIX package, another option is to *extend* the application by adding a UWP project to your solution.</span></span> <span data-ttu-id="a7ac6-159">デスクトップ プロジェクトは、アプリケーションのエントリ ポイントですが、UWP プロジェクトにアクセスできるすべての Api で表示されない[このリスト](desktop-to-uwp-supported-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-159">The desktop project is still the entry point of your application, but the UWP project gives you access to all of the APIs that do not appear in [this list](desktop-to-uwp-supported-api.md).</span></span> <span data-ttu-id="a7ac6-160">デスクトップ アプリが UWP のプロセスを使用して通信を app service とそれらをセットアップする方法のガイダンスの多くがあります。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-160">The desktop app can communicate with the UWP process by using a an app service and we have lots of guidance on how to set that up.</span></span> <span data-ttu-id="a7ac6-161">UWP プロジェクトを必要とするエクスペリエンスを追加する場合を参照してください[UWP コンポーネントを持つ拡張](desktop-to-uwp-extend.md)します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-161">If you want to add an experience that requires a UWP project, see [Extend with UWP components](desktop-to-uwp-extend.md).</span></span>

<span data-ttu-id="a7ac6-162">:white_check_mark:**参照 API コントラクト**</span><span class="sxs-lookup"><span data-stu-id="a7ac6-162">:white_check_mark: **Reference API contracts**</span></span>

<span data-ttu-id="a7ac6-163">デスクトップ アプリから直接 API を呼び出すことができる場合、ブラウザーとその API のリファレンス トピックの検索を開きます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-163">If you can call the API directly from your desktop app, open a browser and search for the reference topic for that API.</span></span>
<span data-ttu-id="a7ac6-164">API の概要の下に、その API の API コントラクトを説明する表があります。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-164">Beneath the summary of the API, you'll find a table that describes the API contract for that API.</span></span> <span data-ttu-id="a7ac6-165">以下に表の例を示します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-165">Here's an example of that table:</span></span>

![API コントラクト表](images/desktop-to-uwp/contract-table.png)

<span data-ttu-id="a7ac6-167">.NET ベースのデスクトップ アプリの場合、その API コントラクトへの参照を追加します。その後、そのファイルの **[ローカルにコピー]** プロパティを **[False]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-167">If you have a .NET-based desktop app, add a reference to that API contract, and then set the **Copy Local** property of that file to **False**.</span></span> <span data-ttu-id="a7ac6-168">C++ ベースのプロジェクトの場合、 **[追加のインクルード ディレクトリ]** に、このコントラクトを含むフォルダーのパスを追加します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-168">If you have a C++-based project, add to your **Additional Include Directories**, a path to the folder that contains this contract.</span></span>

<span data-ttu-id="a7ac6-169">:white_check_mark:**お客様のエクスペリエンスを追加する Api を呼び出す**</span><span class="sxs-lookup"><span data-stu-id="a7ac6-169">:white_check_mark: **Call the APIs to add your experience**</span></span>

<span data-ttu-id="a7ac6-170">以下に、前述の通知ウィンドウの表示に使用するコードを示します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-170">Here's the code that you'd use to show the notification window that we looked at earlier.</span></span> <span data-ttu-id="a7ac6-171">これでこれらの Api が表示される[一覧](desktop-to-uwp-supported-api.md)デスクトップ アプリに次のコードを追加して、すぐに実行できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-171">These APIs appear in this [list](desktop-to-uwp-supported-api.md) so you can add this code to your desktop app and run it right now.</span></span>

```csharp
using Windows.Foundation;
using Windows.System;
using Windows.UI.Notifications;
using Windows.Data.Xml.Dom;
...

private void ShowToast()
{
    string title = "featured picture of the day";
    string content = "beautiful scenery";
    string image = "https://picsum.photos/360/180?image=104";
    string logo = "https://picsum.photos/64?image=883";

    string xmlString =
    $@"<toast><visual>
       <binding template='ToastGeneric'>
       <text>{title}</text>
       <text>{content}</text>
       <image src='{image}'/>
       <image src='{logo}' placement='appLogoOverride' hint-crop='circle'/>
       </binding>
      </visual></toast>";

    XmlDocument toastXml = new XmlDocument();
    toastXml.LoadXml(xmlString);

    ToastNotification toast = new ToastNotification(toastXml);

    ToastNotificationManager.CreateToastNotifier().Show(toast);
}
```

```C++
using namespace Windows::Foundation;
using namespace Windows::System;
using namespace Windows::UI::Notifications;
using namespace Windows::Data::Xml::Dom;

void UWP::ShowToast()
{
    Platform::String ^title = "featured picture of the day";
    Platform::String ^content = "beautiful scenery";
    Platform::String ^image = "https://picsum.photos/360/180?image=104";
    Platform::String ^logo = "https://picsum.photos/64?image=883";

    Platform::String ^xmlString =
        L"<toast><visual><binding template='ToastGeneric'>" +
        L"<text>" + title + "</text>" +
        L"<text>"+ content + "</text>" +
        L"<image src='" + image + "'/>" +
        L"<image src='" + logo + "'" +
        L" placement='appLogoOverride' hint-crop='circle'/>" +
        L"</binding></visual></toast>";

    XmlDocument ^toastXml = ref new XmlDocument();

    toastXml->LoadXml(xmlString);

    ToastNotificationManager::CreateToastNotifier()->Show(ref new ToastNotification(toastXml));
}
```

<span data-ttu-id="a7ac6-172">通知の詳細については、「[アダプティブ トースト通知と対話型トースト通知](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-172">To learn more about notifications, see [Adaptive and Interactive toast notifications](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts).</span></span>

## <a name="support-windows-xp-windows-vista-and-windows-78-install-bases"></a><span data-ttu-id="a7ac6-173">Windows XP、Windows Vista、および Windows 7/8 インストール ベースのサポート</span><span class="sxs-lookup"><span data-stu-id="a7ac6-173">Support Windows XP, Windows Vista, and Windows 7/8 install bases</span></span>

<span data-ttu-id="a7ac6-174">新しいブランチを作成し、別のコード ベースを管理することがなく、Windows 10 用のアプリケーションを最新化することができます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-174">You can modernize your application for Windows 10 without having to create a new branch and maintain separate code bases.</span></span>

<span data-ttu-id="a7ac6-175">Windows 10 ユーザー向けに個別のバイナリをビルドする場合は、条件付きコンパイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-175">If you want to build separate binaries for Windows 10 users, use conditional compilation.</span></span> <span data-ttu-id="a7ac6-176">すべての Windows ユーザーに対して 1 組のバイナリをビルドして展開する場合は、ランタイム チェックを使用します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-176">If you'd prefer to build one set of binaries that you deploy to all Windows users, use runtime checks.</span></span>

<span data-ttu-id="a7ac6-177">各オプションを簡単に見ていきましょう。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-177">Let's take a quick look at each option.</span></span>

### <a name="conditional-compilation"></a><span data-ttu-id="a7ac6-178">条件付きコンパイル</span><span class="sxs-lookup"><span data-stu-id="a7ac6-178">Conditional compilation</span></span>

<span data-ttu-id="a7ac6-179">1 つのコードベースを維持して、Windows 10 ユーザー向けだけに一連のバイナリをコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-179">You can keep one code base and compile a set of binaries just for Windows 10 users.</span></span>

<span data-ttu-id="a7ac6-180">最初に、新しいビルド構成をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-180">First, add a new build configuration to your project.</span></span>

![ビルド構成](images/desktop-to-uwp/build-config.png)

<span data-ttu-id="a7ac6-182">そのビルド構成の定数を作成する Windows ランタイム Api を呼び出すコードを識別するためにします。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-182">For that build configuration, create a constant that to identify code that calls Windows Runtime APIs.</span></span>  

<span data-ttu-id="a7ac6-183">.NET ベースのプロジェクトの場合、この定数は**条件付きコンパイル定数**と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-183">For .NET-based projects, the constant is called a **Conditional Compilation Constant**.</span></span>

![プリプロセッサ](images/desktop-to-uwp/compilation-constants.png)

<span data-ttu-id="a7ac6-185">C++ ベースのプロジェクトの場合、この定数は**プリプロセッサ定義**と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-185">For C++-based projects, the constant is called a **Preprocessor Definition**.</span></span>

![プリプロセッサ](images/desktop-to-uwp/pre-processor.png)

<span data-ttu-id="a7ac6-187">この定数を、任意の UWP コードのブロックの前に追加します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-187">Add that constant before any block of UWP code.</span></span>

```csharp

[System.Diagnostics.Conditional("_UWP")]
private void ShowToast()
{
 ...
}

```

```C++

#if _UWP
void UWP::ShowToast()
{
 ...
}
#endif

```

<span data-ttu-id="a7ac6-188">この定数がアクティブなビルド構成で定義されている場合のみ、コンパイラでこのコードがビルドされます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-188">The compiler builds that code only if that constant is defined in your active build configuration.</span></span>

### <a name="runtime-checks"></a><span data-ttu-id="a7ac6-189">ランタイム チェック</span><span class="sxs-lookup"><span data-stu-id="a7ac6-189">Runtime checks</span></span>

<span data-ttu-id="a7ac6-190">ユーザーが実行する Windows のバージョンに関係なく、1 組のバイナリをすべての Windows ユーザー向けにコンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-190">You can compile one set of binaries for all of your Windows users regardless of which version of Windows they run.</span></span> <span data-ttu-id="a7ac6-191">アプリケーションは Windows ランタイム Api、ユーザーが実行する場合にのみアプリケーションをパッケージ化されたアプリケーションとして Windows 10</span><span class="sxs-lookup"><span data-stu-id="a7ac6-191">Your application calls Windows Runtime APIs only if the user is runs your application as a packaged application on Windows 10.</span></span>

<span data-ttu-id="a7ac6-192">ランタイム チェックをコードに追加する最も簡単な方法では、この Nuget パッケージをインストールします。[デスクトップ ブリッジ ヘルパー](https://www.nuget.org/packages/DesktopBridge.Helpers/)しを使用して、``IsRunningAsUWP()``メソッド ゲートを Windows ランタイム Api を呼び出すコードをすべてオフにします。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-192">The easiest way to add runtime checks to your code is to install this Nuget package: [Desktop Bridge Helpers](https://www.nuget.org/packages/DesktopBridge.Helpers/) and then use the ``IsRunningAsUWP()`` method to gate off all code that calls Windows Runtime APIs.</span></span> <span data-ttu-id="a7ac6-193">このブログの詳細については投稿を参照してください。[デスクトップ ブリッジ - アプリケーションのコンテキストを識別する](https://blogs.msdn.microsoft.com/appconsult/2016/11/03/desktop-bridge-identify-the-applications-context/)します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-193">see this blog post for more details: [Desktop Bridge - Identify the application's context](https://blogs.msdn.microsoft.com/appconsult/2016/11/03/desktop-bridge-identify-the-applications-context/).</span></span>

## <a name="related-samples"></a><span data-ttu-id="a7ac6-194">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="a7ac6-194">Related Samples</span></span>

* [<span data-ttu-id="a7ac6-195">Hello World サンプル</span><span class="sxs-lookup"><span data-stu-id="a7ac6-195">Hello World Sample</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/HelloWorldSample)
* [<span data-ttu-id="a7ac6-196">セカンダリ タイル</span><span class="sxs-lookup"><span data-stu-id="a7ac6-196">Secondary Tile</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/SecondaryTileSample)
* [<span data-ttu-id="a7ac6-197">ストア API サンプル</span><span class="sxs-lookup"><span data-stu-id="a7ac6-197">Store API Sample</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/StoreSample)
* [<span data-ttu-id="a7ac6-198">WinForms アプリケーション UWP UpdateTask を実装します。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-198">WinForms application that implements a UWP UpdateTask</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/WinFormsUpdateTaskSample)
* [<span data-ttu-id="a7ac6-199">UWP サンプルへのブリッジのデスクトップ アプリ</span><span class="sxs-lookup"><span data-stu-id="a7ac6-199">Desktop app bridge to UWP Samples</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples)

## <a name="support-and-feedback"></a><span data-ttu-id="a7ac6-200">サポートとフィードバック</span><span class="sxs-lookup"><span data-stu-id="a7ac6-200">Support and feedback</span></span>

<span data-ttu-id="a7ac6-201">**質問の回答を検索**</span><span class="sxs-lookup"><span data-stu-id="a7ac6-201">**Find answers to your questions**</span></span>

<span data-ttu-id="a7ac6-202">ご質問がある場合は、</span><span class="sxs-lookup"><span data-stu-id="a7ac6-202">Have questions?</span></span> <span data-ttu-id="a7ac6-203">Stack Overflow でお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-203">Ask us on Stack Overflow.</span></span> <span data-ttu-id="a7ac6-204">Microsoft のチームでは、これらの[タグ](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge)をチェックしています。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-204">Our team monitors these [tags](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge).</span></span> <span data-ttu-id="a7ac6-205">[こちら](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D)から質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-205">You can also ask us [here](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D).</span></span>

<span data-ttu-id="a7ac6-206">**ご意見や機能を提案します。**</span><span class="sxs-lookup"><span data-stu-id="a7ac6-206">**Give feedback or make feature suggestions**</span></span>

<span data-ttu-id="a7ac6-207">[UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial) のページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a7ac6-207">See [UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial).</span></span>
