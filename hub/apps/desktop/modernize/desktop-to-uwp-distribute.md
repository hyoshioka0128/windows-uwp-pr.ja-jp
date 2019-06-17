---
Description: 配布パッケージのデスクトップ アプリケーション (デスクトップ ブリッジ)
title: Microsoft Store またはサイドロードにパッケージ化されたデスクトップ アプリケーションを発行して 1 つまたは複数のデバイスにします。
ms.date: 05/18/2018
ms.topic: article
keywords: windows 10, uwp
ms.assetid: edff3787-cecb-4054-9a2d-1fbefa79efc4
ms.author: mcleans
author: mcleanbyron
ms.localizationpriority: medium
ms.openlocfilehash: 45d298aca60155915900f494654dce8e89fb1ee0
ms.sourcegitcommit: b9e2cd5232ad98f4ef367881b92000a3ae610844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "67131906"
---
# <a name="distribute-your-packaged-desktop-app"></a><span data-ttu-id="5efbb-104">パッケージ化されたデスクトップ アプリを配布します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-104">Distribute your packaged desktop app</span></span>

<span data-ttu-id="5efbb-105">場合[MSIX パッケージでデスクトップ アプリをパッケージ化](/windows/msix/desktop/desktop-to-uwp-root)、サイドローディングを行う、Microsoft Store にパッケージ化されたアプリケーションを発行する 1 つまたは複数のデバイスにします。</span><span class="sxs-lookup"><span data-stu-id="5efbb-105">If you decide to [package your desktop app in an MSIX package](/windows/msix/desktop/desktop-to-uwp-root), you can publish your packaged application to the Microsoft Store or sideload it onto one or more devices.</span></span>

> [!NOTE]
> <span data-ttu-id="5efbb-106">ユーザーをパッケージ化されたアプリケーションに移行する方法を計画していますか。</span><span class="sxs-lookup"><span data-stu-id="5efbb-106">Do you have a plan for how you might transition users to your packaged application?</span></span> <span data-ttu-id="5efbb-107">アプリを配布する前に、このガイドの「[パッケージ アプリにユーザーを移行する](#transition-users)」セクションを参照して、アイデアを得てください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-107">Before you distribute your app, see the [Transition users to your packaged app](#transition-users) section of this guide to get some ideas.</span></span>

## <a name="distribute-your-application-by-publishing-it-to-the-microsoft-store"></a><span data-ttu-id="5efbb-108">Microsoft Store に公開することによって、アプリケーションを配布します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-108">Distribute your application by publishing it to the Microsoft Store</span></span>

<span data-ttu-id="5efbb-109">[Microsoft Store](https://www.microsoft.com/store/apps) は、お客様がアプリを取得する場合に最も便利な方法です。</span><span class="sxs-lookup"><span data-stu-id="5efbb-109">The [Microsoft Store](https://www.microsoft.com/store/apps) is a convenient way for customers to get your app.</span></span>

<span data-ttu-id="5efbb-110">広範な対象ユーザーに到達する Microsoft Store にアプリケーションを発行します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-110">Publish your application to the Microsoft Store to reach the broadest audience.</span></span> <span data-ttu-id="5efbb-111">組織の顧客がを通じて、組織に内部的に配布するアプリケーションを取得することも、[ビジネス向け Microsoft Store](https://www.microsoft.com/business-store)します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-111">Also, organizational customers can acquire your application to distribute internally to their organizations through the [Microsoft Store for Business](https://www.microsoft.com/business-store).</span></span>

<span data-ttu-id="5efbb-112">Microsoft Store への公開を計画している場合は、申請プロセスの一部としていくつかの追加の質問をされます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-112">If you plan to publish to the Microsoft Store, you'll be asked a few extra questions as part of the submission process.</span></span> <span data-ttu-id="5efbb-113">これは、パッケージ マニフェストが **runFullTrust** という名前の制限付き機能を宣言し、弊社でアプリケーションによるその機能の使用を承認する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="5efbb-113">That's because your package manifest declares a restricted capability named **runFullTrust**, and we need to approve your application's use of that capability.</span></span> <span data-ttu-id="5efbb-114">詳細については、ここで、この要件。[機能が制限されている](/windows/uwp/packaging/app-capability-declarations#restricted-capabilities)します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-114">You can read more about this requirement here: [Restricted capabilities](/windows/uwp/packaging/app-capability-declarations#restricted-capabilities).</span></span>

<span data-ttu-id="5efbb-115">ストアに送信する前に、アプリケーションに署名する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5efbb-115">You don't have to sign your application before you submit it to the Store.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="5efbb-116">Microsoft Store にアプリケーションを発行する場合は、Windows 10 s. を実行するデバイスで、アプリケーションが正しく動作確認します。これは、ストアの要件です。</span><span class="sxs-lookup"><span data-stu-id="5efbb-116">If you plan to publish your application to the Microsoft Store, make sure that your application operates correctly on devices that run Windows 10 S. This is a Store requirement.</span></span> <span data-ttu-id="5efbb-117">「[Windows アプリの Windows 10 S 対応をテストする](/windows/msix/desktop/desktop-to-uwp-test-windows-s)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-117">See [Test your Windows app for Windows 10  S](/windows/msix/desktop/desktop-to-uwp-test-windows-s).</span></span>

<a id="side-load" />

## <a name="distribute-your-application-without-placing-it-onto-the-microsoft-store"></a><span data-ttu-id="5efbb-118">Microsoft Store に配置することがなく、アプリケーションを配布します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-118">Distribute your application without placing it onto the Microsoft Store</span></span>

<span data-ttu-id="5efbb-119">ストアを使用せず、アプリケーション配布ではなく場合、は、1 つまたは複数のデバイスにアプリを手動で配布できます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-119">If you'd rather distribute your application without using the Store, you can manually distribute apps to one or more devices.</span></span>

<span data-ttu-id="5efbb-120">この方法は、配布エクスペリエンスをきめ細かく制御する必要がある場合や、Microsoft Store の認定プロセスへの関与が望ましくない場合などに有効です。</span><span class="sxs-lookup"><span data-stu-id="5efbb-120">This might make sense if you want greater control over the distribution experience or you don't want to get involved with the Microsoft Store certification process.</span></span>

<span data-ttu-id="5efbb-121">ストアに配置することがなく、他のデバイスにアプリケーションを配布するには、証明書を取得するには、アプリケーションをそれらのデバイスにその証明書、および、サイドローディングを使用して、アプリケーションの署名があります。</span><span class="sxs-lookup"><span data-stu-id="5efbb-121">To distribute your application to other devices without placing it in the Store, you have to obtain a certificate, sign your application by using that certificate, and then sideload your application onto those devices.</span></span>

<span data-ttu-id="5efbb-122">[証明書を作成](/windows/uwp/packaging/create-certificate-package-signing)することも、[Verisign](https://www.verisign.com/) などのポピュラーなベンダーから取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-122">You can [create a certificate](/windows/uwp/packaging/create-certificate-package-signing) or obtain one from a popular vendor such as [Verisign](https://www.verisign.com/).</span></span>

<span data-ttu-id="5efbb-123">Windows 10 S を実行しているデバイスにアプリケーションを配布する場合は、これらのデバイスにアプリケーションを配布する前に、ストア提出プロセスを経由する必要があるありますので、Microsoft Store で署名するアプリケーションを持ちます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-123">If you plan to distribute your application onto devices that run Windows 10 S, your application has to be signed by the Microsoft Store so you'll have to go through the Store submission process before you can distribute your application onto those devices.</span></span>

<span data-ttu-id="5efbb-124">証明書を作成する場合は、アプリを実行する各デバイスの証明書ストア ("**信頼されたルート**" または "**信頼されたユーザー**") にインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5efbb-124">If you create a certificate, you have to install it into the **Trusted Root** or **Trusted People** certificate store on each device that runs your app.</span></span> <span data-ttu-id="5efbb-125">ポピュラーなベンダーから証明書を取得する場合、システムにはアプリの他に何もインストールする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5efbb-125">If you get a certificate from a popular vendor, you won't have to install anything onto other systems besides your app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="5efbb-126">証明書の発行元名がアプリの発行者名と一致することを確認してください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-126">Make sure that the publisher name on your certificate matches the publisher name of your app.</span></span>

<span data-ttu-id="5efbb-127">アプリケーションへの署名証明書を使用してを参照してください。 [SignTool を使用して、アプリケーション パッケージに署名](/windows/uwp/packaging/sign-app-package-using-signtool)します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-127">To sign your application by using a certificate, see [Sign an application package using SignTool](/windows/uwp/packaging/sign-app-package-using-signtool).</span></span>

<span data-ttu-id="5efbb-128">サイドローディングを行う他のデバイスにアプリケーションを参照してください[サイドローディングを行う基幹業務アプリと Windows 10 で](/windows/application-management/sideload-apps-in-windows-10)します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-128">To sideload your application onto other devices, see [Sideload LOB apps in Windows 10](/windows/application-management/sideload-apps-in-windows-10).</span></span>

<a id="transition-users" />

## <a name="transition-users-to-your-packaged-app"></a><span data-ttu-id="5efbb-129">パッケージ アプリへのユーザーの移行</span><span class="sxs-lookup"><span data-stu-id="5efbb-129">Transition users to your packaged app</span></span>

<span data-ttu-id="5efbb-130">ユーザーによってパッケージ アプリが使用されるようにするには、アプリを配布する前に、パッケージ マニフェストにいくつかの拡張機能を追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-130">Before you distribute your app, consider adding a few extensions to your package manifest to help users get into the habit of using your packaged app.</span></span> <span data-ttu-id="5efbb-131">次のようなことができます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-131">Here's a few things you can do.</span></span>

* <span data-ttu-id="5efbb-132">既存のスタート タイルとタスク バー ボタンの参照先をパッケージ アプリに設定する。</span><span class="sxs-lookup"><span data-stu-id="5efbb-132">Point existing Start tiles and taskbar buttons to your packaged app.</span></span>
* <span data-ttu-id="5efbb-133">パッケージ化されたアプリケーションをファイルの種類のセットに関連付けます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-133">Associate your packaged application with a set of file types.</span></span>
* <span data-ttu-id="5efbb-134">既定で特定の種類のファイルを開き、パッケージ化されたアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-134">Make your packaged application open certain types of files by default.</span></span>

<span data-ttu-id="5efbb-135">拡張機能の完全な一覧と使用方法のガイダンスについては、「[アプリにユーザーを移行する](desktop-to-uwp-extensions.md#transition-users-to-your-app)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-135">For the complete list of extensions and the guidance for how to use them, see [Transition users to your app](desktop-to-uwp-extensions.md#transition-users-to-your-app).</span></span>

<span data-ttu-id="5efbb-136">また、これらのタスクが実行されるパッケージ化されたアプリケーションにコードを追加することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-136">Also, consider adding code to your packaged application that accomplishes these tasks:</span></span>

* <span data-ttu-id="5efbb-137">デスクトップ アプリケーションをパッケージ化されたアプリの適切なフォルダーの場所に関連付けられているユーザー データを移行します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-137">Migrates user data associated with your desktop application to the appropriate folder locations of your packaged app.</span></span>
* <span data-ttu-id="5efbb-138">アプリのデスクトップ バージョンをアンインストールするためのオプションをユーザーに示します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-138">Gives users the option to uninstall the desktop version of your app.</span></span>

<span data-ttu-id="5efbb-139">これらのタスクについて、それぞれ説明します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-139">Let's talk about each one of these tasks.</span></span> <span data-ttu-id="5efbb-140">ユーザー データの移行から開始します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-140">We'll start with user data migration.</span></span>

### <a name="migrate-user-data"></a><span data-ttu-id="5efbb-141">ユーザー データの移行</span><span class="sxs-lookup"><span data-stu-id="5efbb-141">Migrate user data</span></span>

<span data-ttu-id="5efbb-142">ユーザー データを移行するコードを追加しようとしている場合は、アプリケーションが初めて起動した場合にのみ、そのコードを実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5efbb-142">If you're going to add code that migrates user data, it's best to run that code only when the application is first started.</span></span> <span data-ttu-id="5efbb-143">ユーザー データを移行する前に、ユーザーに対してダイアログ ボックスを表示して、何が起こっているか、なぜ移行が推奨されるのか、既存のデータにどのような影響があるかを説明します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-143">Before you migrate the users data, display a dialog box to the user that explains what is happening, why it is recommended, and what's going to happen to their existing data.</span></span>

<span data-ttu-id="5efbb-144">例として、.NET ベースのパッケージ アプリでの方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-144">Here's an example of how you could do this in a .NET-based packaged app.</span></span>

```csharp
private void MigrateUserData()
{
    String sourceDir = Environment.GetFolderPath
        (Environment.SpecialFolder.ApplicationData) + "\\AppName";

    if (sourceDir != null)
    {
        DialogResult migrateResult = MessageBox.Show
            ("Would you like to migrate your data from the previous version of this app?",
             "Data Migration", MessageBoxButtons.YesNo);

        if (migrateResult.Equals(DialogResult.Yes))
        {
            String destinationDir =
                Windows.Storage.ApplicationData.Current.LocalFolder.Path + "\\AppName";

            Process process = new Process();
            process.StartInfo.FileName = "robocopy.exe";
            process.StartInfo.Arguments = "%LOCALAPPDATA%\\AppName " + destinationDir + " /move";
            process.StartInfo.CreateNoWindow = true;
            process.Start();
            process.WaitForExit();

            if (process.ExitCode > 1)
            {
                //Migration was unsuccessful -- you can choose to block/retry/other action
            }
        }
    }
}
```

### <a name="uninstall-the-desktop-version-of-your-app"></a><span data-ttu-id="5efbb-145">アプリのデスクトップ バージョンをアンインストールする</span><span class="sxs-lookup"><span data-stu-id="5efbb-145">Uninstall the desktop version of your app</span></span>

<span data-ttu-id="5efbb-146">最初に許可を求めることがなく、ユーザーのデスクトップ アプリケーションをアンインストールすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5efbb-146">It is better not to uninstall the users desktop application without first asking them for permission.</span></span> <span data-ttu-id="5efbb-147">ユーザーに許可を求めるには、そのためのダイアログ ボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-147">Display a dialog box that asks the user for that permission.</span></span> <span data-ttu-id="5efbb-148">ユーザーによって、アプリのデスクトップ バージョンをアンインストールしないように指定されることも考えられます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-148">Users might decide not to uninstall the desktop version of your app.</span></span> <span data-ttu-id="5efbb-149">このような場合は、デスクトップ アプリケーションの使用状況をブロックまたは両方のアプリのサイド バイ サイドでの使用をサポートするかどうかを決定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5efbb-149">If that happens, you'll have to decide whether you want to block usage of the desktop application or support the side-by-side use of both apps.</span></span>

<span data-ttu-id="5efbb-150">例として、.NET ベースのパッケージ アプリでの方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5efbb-150">Here's an example of how you could do this in a .NET-based packaged app.</span></span>

<span data-ttu-id="5efbb-151">このスニペットの完全なコンテキストを確認するには、「[WPF picture viewer with transition/migration/uninstallation](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)」というサンプルの **MainWindow.cs** ファイルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-151">To view the complete context of this snippet, see the **MainWindow.cs** file of this sample [WPF picture viewer with transition/migration/uninstallation](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition).</span></span>

```csharp
private void RemoveDesktopApp()
{              
    //Typically, you can find your uninstall string at this location.
    String uninstallString = (String)Microsoft.Win32.Registry.GetValue
        (@"HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion" +
         @"\Uninstall\{7AD02FB8-B85E-44BC-8998-F4803BA5A0E3}\", "UninstallString", null);

    //Detect if the previous version of the Desktop application is installed.
    if (uninstallString != null)
    {
        DialogResult uninstallResult = MessageBox.Show
            ("To have the best experience, consider uninstalling the "
              + " previous version of this app. Would you like to do that now?",
              "Uninstall the previous version", MessageBoxButtons.YesNo);

        if (uninstallResult.Equals(DialogResult.Yes))
        {
                    string[] uninstallArgs = uninstallString.Split(' ');

            Process process = new Process();
            process.StartInfo.FileName = uninstallArgs[0];
            process.StartInfo.Arguments = uninstallArgs[1];
            process.StartInfo.CreateNoWindow = true;

            process.Start();
            process.WaitForExit();

            if (process.ExitCode != 0)
            {
                //Uninstallation was unsuccessful - You can choose to block the application here.
            }
        }
    }

}
```

## <a name="next-steps"></a><span data-ttu-id="5efbb-152">次のステップ</span><span class="sxs-lookup"><span data-stu-id="5efbb-152">Next steps</span></span>

<span data-ttu-id="5efbb-153">**質問の回答を検索**</span><span class="sxs-lookup"><span data-stu-id="5efbb-153">**Find answers to your questions**</span></span>

<span data-ttu-id="5efbb-154">ご質問がある場合は、</span><span class="sxs-lookup"><span data-stu-id="5efbb-154">Have questions?</span></span> <span data-ttu-id="5efbb-155">Stack Overflow でお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-155">Ask us on Stack Overflow.</span></span> <span data-ttu-id="5efbb-156">Microsoft のチームでは、これらの[タグ](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge)をチェックしています。</span><span class="sxs-lookup"><span data-stu-id="5efbb-156">Our team monitors these [tags](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge).</span></span> <span data-ttu-id="5efbb-157">[こちら](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D)から質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-157">You can also ask us [here](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D).</span></span>

<span data-ttu-id="5efbb-158">Microsoft Store へのアプリの公開で問題が発生した場合は、この[ブログ投稿](https://blogs.msdn.microsoft.com/appconsult/2017/09/25/preparing-a-desktop-bridge-application-for-the-store-submission/)で役に立つヒントを参照できます。</span><span class="sxs-lookup"><span data-stu-id="5efbb-158">If you encounter issues publishing your application to the Store, this [blog post](https://blogs.msdn.microsoft.com/appconsult/2017/09/25/preparing-a-desktop-bridge-application-for-the-store-submission/) contains some useful tips.</span></span>

<span data-ttu-id="5efbb-159">**ご意見や機能を提案します。**</span><span class="sxs-lookup"><span data-stu-id="5efbb-159">**Give feedback or make feature suggestions**</span></span>

<span data-ttu-id="5efbb-160">[UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial) のページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5efbb-160">See [UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial).</span></span>
