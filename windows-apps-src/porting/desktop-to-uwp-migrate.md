---
Description: デスクトップ アプリケーションおよび UWP アプリ間で共有コード
title: デスクトップ アプリケーションおよび UWP アプリ間で共有コード
ms.date: 10/03/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 16b75226d6b79b19978ddf7e37231b15ac7a4e3e
ms.sourcegitcommit: f0f933d5cf0be734373a7b03e338e65000cc3d80
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65984167"
---
# <a name="move-from-a-desktop-application-to-uwp"></a><span data-ttu-id="16c0d-104">UWP へのデスクトップ アプリケーションからの移動します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-104">Move from a desktop application to UWP</span></span>

<span data-ttu-id="16c0d-105">.NET Framework (WPF と Windows フォームを含む) を使用して構築された既存のデスクトップ アプリケーションがある場合またはC++Win32 Api では、Windows 10 とユニバーサル Windows プラットフォーム (UWP) に移動するためのいくつかのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-105">If you have an existing desktop application that was built using the .NET Framework (including WPF and Windows Forms) or C++ Win32 APIs, you have several options for moving to the Universal Windows Platform (UWP) and Windows 10.</span></span>

## <a name="package-your-desktop-application-in-an-msix-package"></a><span data-ttu-id="16c0d-106">MSIX パッケージ内のデスクトップ、アプリケーションをパッケージ化します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-106">Package your desktop application in an MSIX package</span></span>

<span data-ttu-id="16c0d-107">Windows 10 の多数の機能へのアクセスを取得する MSIX パッケージをデスクトップ アプリケーションをパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-107">You can package your desktop application in an MSIX package to get access to many more Windows 10 features.</span></span> <span data-ttu-id="16c0d-108">MSIX には、UWP、WPF、Windows フォーム、Win32 アプリを含む、すべてのアプリの Windows ユニバーサルのパッケージ化エクスペリエンスを提供する最新 Windows アプリ パッケージ形式です。</span><span class="sxs-lookup"><span data-stu-id="16c0d-108">MSIX is a modern Windows app package format that provides a universal packaging experience for all Windows apps, including UWP, WPF, Windows Forms and Win32 apps.</span></span> <span data-ttu-id="16c0d-109">堅牢なインストールへのアクセスを取得する MSIX パッケージで、デスクトップの Windows アプリをパッケージ化し、Microsoft Store、エンタープライズ管理、および多くのカスタムのサポート、機能の柔軟性の高いシステムでの管理セキュリティ モデルのエクスペリエンスを更新するには、配布モデル。</span><span class="sxs-lookup"><span data-stu-id="16c0d-109">Packaging your desktop Windows apps in MSIX packages gets you access to a robust installation and updating experience, a managed security model with a flexible capability system, support for the Microsoft Store, enterprise management, and many custom distribution models.</span></span> <span data-ttu-id="16c0d-110">ソース コードがあるかどうか、またはのみ (MSI、または、APP-V のインストーラー) などの既存のインストーラー ファイルがあるかどうか、アプリケーションをパッケージ化することができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-110">You can package your application whether you have the source code or if you only have an existing installer file (such as an MSI or App-V installer).</span></span> <span data-ttu-id="16c0d-111">アプリケーションをパッケージ化したら、パッケージの拡張機能とその他の UWP コンポーネントなどの UWP 機能を統合できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-111">After you package your application, you can integrate UWP features such as package extensions and other UWP components.</span></span>

<span data-ttu-id="16c0d-112">詳細については、次を参照してください。[デスクトップ アプリケーション (デスクトップ ブリッジ) パッケージ](/windows/msix/desktop/desktop-to-uwp-root)と[パッケージ id が必要な機能](/windows/apps/desktop/modernize/modernize-packaged-apps)します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-112">For more information, see [Package desktop applications (Desktop Bridge)](/windows/msix/desktop/desktop-to-uwp-root) and [Features that require package identity](/windows/apps/desktop/modernize/modernize-packaged-apps).</span></span>

## <a name="use-uwp-apis"></a><span data-ttu-id="16c0d-113">UWP Api を使用して、</span><span class="sxs-lookup"><span data-stu-id="16c0d-113">Use UWP APIs</span></span>

<span data-ttu-id="16c0d-114">UWP Api の多くは、Windows フォーム、WPF で直接呼び出すことができますかC++Win32 デスクトップ アプリに Windows 10 のユーザー用に光を最新のエクスペリエンスを統合します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-114">You can call many UWP APIs directly in your WPF, Windows Forms, or C++ Win32 desktop app to integrate modern experiences that light up for Windows 10 users.</span></span> <span data-ttu-id="16c0d-115">たとえば、デスクトップ アプリにトースト通知を追加する UWP Api を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-115">For example, you can call UWP APIs to add toast notifications to your desktop app.</span></span>

<span data-ttu-id="16c0d-116">詳細については、次を参照してください。[デスクトップ アプリでの UWP Api を使用して](/windows/apps/desktop/modernize/desktop-to-uwp-enhance)します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-116">For more information, see [Use UWP APIs in desktop apps](/windows/apps/desktop/modernize/desktop-to-uwp-enhance).</span></span>

## <a name="migrate-a-net-framework-app-to-a-uwp-app"></a><span data-ttu-id="16c0d-117">移行、.NET Framework アプリを UWP アプリ</span><span class="sxs-lookup"><span data-stu-id="16c0d-117">Migrate a .NET Framework app to a UWP app</span></span>

<span data-ttu-id="16c0d-118">アプリケーションを .NET Framework で実行する場合は、.NET Standard 2.0 を利用して UWP アプリに移行することができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-118">If your application runs on the .NET Framework, you can migrate it to a UWP app by leveraging .NET Standard 2.0.</span></span> <span data-ttu-id="16c0d-119">.NET Standard 2.0 クラス ライブラリにことができますし、.NET Standard 2.0 ライブラリを参照する UWP アプリを作成すると、多くのコードに移動します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-119">Move as much code as you can into .NET Standard 2.0 class libraries, and then create a UWP app that references your .NET Standard 2.0 libraries.</span></span> 

### <a name="share-code-in-a-net-standard-20-library"></a><span data-ttu-id="16c0d-120">.NET Standard 2.0 ライブラリでコードを共有する</span><span class="sxs-lookup"><span data-stu-id="16c0d-120">Share code in a .NET Standard 2.0 library</span></span>

<span data-ttu-id="16c0d-121">.NET Framework でアプリケーションを実行する場合は、することができますに .NET Standard 2.0 クラス ライブラリのコードを配置します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-121">If your application runs on the .NET Framework, place as much code as you can into .NET Standard 2.0 class libraries.</span></span> <span data-ttu-id="16c0d-122">標準で定義されている API を使用しているコードは、UWP アプリで再利用できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-122">As long as your code uses APIs that are defined in the standard, you can reuse it in a UWP app.</span></span> <span data-ttu-id="16c0d-123">.NET Standard 2.0 に含まれる API が大幅に増えたため、.NET Standard ライブラリでのコード共有は、従来よりずっと簡単になっています。</span><span class="sxs-lookup"><span data-stu-id="16c0d-123">It's easier than it's ever been to share code in a .NET Standard library because so many more APIs are included in the .NET Standard 2.0.</span></span>

<span data-ttu-id="16c0d-124">詳細については、通知するビデオを次に示します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-124">Here's a video that tells you more about it.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/YI4MurjfMn8?list=PLRAdsfhKI4OWx321A_pr-7HhRNk7wOLLY&amp;ecver=1]

#### <a name="add-net-standard-libraries"></a><span data-ttu-id="16c0d-125">.NET Standard ライブラリを追加する</span><span class="sxs-lookup"><span data-stu-id="16c0d-125">Add .NET Standard libraries</span></span>

<span data-ttu-id="16c0d-126">まず、1 つ以上の .NET Standard クラス ライブラリをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-126">First, add one or more .NET Standard class libraries to your solution.</span></span>  

![.NET Standard プロジェクトの追加](images/desktop-to-uwp/dot-net-standard-project-template.png)

<span data-ttu-id="16c0d-128">ソリューションに追加するライブラリの数は、計画しているコード編成によって異なります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-128">The number of libraries that you add to your solution depends on how you plan to organize your code.</span></span>

<span data-ttu-id="16c0d-129">各クラス ライブラリのターゲットが **.NET Standard 2.0** になっていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-129">Make sure that each class library targets the **.NET Standard 2.0**.</span></span>

![.NET Standard 2.0 をターゲットにする](images/desktop-to-uwp/target-standard-20.png)

<span data-ttu-id="16c0d-131">この設定には、クラス ライブラリ プロジェクトのプロパティ ページからアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-131">You can find this setting in the property pages of the class library project.</span></span>

<span data-ttu-id="16c0d-132">デスクトップ アプリケーション プロジェクトから、クラス ライブラリ プロジェクトへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-132">From your desktop application project, add a reference to the class library project.</span></span>

![クラス ライブラリ参照](images/desktop-to-uwp/class-library-reference.png)

<span data-ttu-id="16c0d-134">次に、ツールを使用して、どの程度のコードが標準に準拠しているか調べます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-134">Next, use tools to determine how much of your code conforms to the standard.</span></span> <span data-ttu-id="16c0d-135">これにより、コードをライブラリに移行する前に、どの部分を再利用でき、どの部分で最小限の変更が必要になり、どの部分がアプリケーション固有にしておくのかを決定できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-135">That way, before you move code into the library, you can decide which parts you can reuse, which parts require minimal modification, and which parts will remain application-specific.</span></span>

#### <a name="check-library-and-code-compatibility"></a><span data-ttu-id="16c0d-136">ライブラリとコードの互換性を確認する</span><span class="sxs-lookup"><span data-stu-id="16c0d-136">Check library and code compatibility</span></span>

<span data-ttu-id="16c0d-137">まず Nuget パッケージと、サード パーティから取得したその他の dll ファイルから始めます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-137">We'll start with Nuget Packages and other dll files that you obtained from a third party.</span></span>

<span data-ttu-id="16c0d-138">アプリケーションでこれらを使用する場合は、.NET Standard 2.0 と互換性があるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-138">If your application uses any of them, determine if they are compatible with the .NET Standard 2.0.</span></span> <span data-ttu-id="16c0d-139">そのためには、Visual Studio 拡張機能またはコマンド ライン ユーティリティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-139">You can use a Visual Studio extension or a command-line utility to do that.</span></span>

<span data-ttu-id="16c0d-140">これらの同じツールを使用して、コードを分析します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-140">Use these same tools to analyze your code.</span></span> <span data-ttu-id="16c0d-141">ここでツール ([dotnet apiport](https://github.com/Microsoft/dotnet-apiport/releases)) をダウンロードし、使用方法に関するビデオをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-141">Download the tools here ([dotnet-apiport](https://github.com/Microsoft/dotnet-apiport/releases)) and then watch this video to learn how to use them.</span></span>
<span data-ttu-id="16c0d-142">&nbsp;</span><span class="sxs-lookup"><span data-stu-id="16c0d-142">&nbsp;</span></span>
> [!VIDEO https://www.youtube-nocookie.com/embed/rzs_FGPyAlY?list=PLRAdsfhKI4OWx321A_pr-7HhRNk7wOLLY&amp;ecver=2]

<span data-ttu-id="16c0d-143">コードに標準との互換性がない場合は、そのコードを実装するための他の方法を検討してください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-143">If your code isn't compatible with the standard, consider other ways that you could implement that code.</span></span> <span data-ttu-id="16c0d-144">まず [.NET API ブラウザー](https://docs.microsoft.com/dotnet/api/?view=netstandard-2.0)を開きます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-144">Start by opening the [.NET API Browser](https://docs.microsoft.com/dotnet/api/?view=netstandard-2.0).</span></span> <span data-ttu-id="16c0d-145">このブラウザーを使用して、.NET Standard 2.0 に含まれている API を確認します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-145">You can use that browser to review the API's that are available in the .NET Standard 2.0.</span></span> <span data-ttu-id="16c0d-146">一覧の範囲として .NET Standard 2.0 を指定してください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-146">Make sure to scope the list to the .NET Standard 2.0.</span></span>

![.NET オプション](images/desktop-to-uwp/dot-net-option.png)

<span data-ttu-id="16c0d-148">コードの一部はプラットフォーム固有でありデスクトップ アプリケーション プロジェクト内に残す必要があります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-148">Some of your code will be platform-specific and will need to remain in your desktop application project.</span></span>

#### <a name="example-migrating-data-access-code-to-a-net-standard-20-library"></a><span data-ttu-id="16c0d-149">以下に例を示します.NET Standard 2.0 ライブラリへのデータ アクセス コードの移行</span><span class="sxs-lookup"><span data-stu-id="16c0d-149">Example: Migrating data access code to a .NET Standard 2.0 library</span></span>

<span data-ttu-id="16c0d-150">Northwind サンプル データベースから顧客を表示する非常に基本的な Windows フォーム アプリケーションがあると仮定します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-150">Let's assume that we have a very basic Windows Forms application that shows customers from our Northwind sample database.</span></span>

![Windows フォーム アプリ](images/desktop-to-uwp/win-forms-app.png)

<span data-ttu-id="16c0d-152">このプロジェクトには、.NET Standard 2.0 クラス ライブラリおよび **Northwind** という静的クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="16c0d-152">The project contains a .NET Standard 2.0 class library with a static class named **Northwind**.</span></span> <span data-ttu-id="16c0d-153">このコードでは ``SQLConnection`` クラス、``SqlCommand`` クラス、``SqlDataReader`` クラスが使用されており、これらのクラスが .NET Standard 2.0 にないため、**Northwind** クラスに移行してもコンパイルできません。</span><span class="sxs-lookup"><span data-stu-id="16c0d-153">If we move this code into the **Northwind** class, it won't compile because it uses the ``SQLConnection``, ``SqlCommand``, and ``SqlDataReader`` classes, and those classes that are not available in the .NET Standard 2.0.</span></span>

```csharp
public static ArrayList GetCustomerNames()
{
    ArrayList customers = new ArrayList();

    using (SqlConnection conn = new SqlConnection())
    {
        conn.ConnectionString =
            @"Data Source=" +
            @"<Your Server Name>\SQLEXPRESS;Initial Catalog=NORTHWIND;Integrated Security=SSPI";

        conn.Open();

        SqlCommand command = new SqlCommand("select ContactName from customers order by ContactName asc", conn);

        using (SqlDataReader reader = command.ExecuteReader())
        {
            while (reader.Read())
            {
                customers.Add(reader[0]);
            }
        }
    }

    return customers;
}

```
<span data-ttu-id="16c0d-154">ただし、[.NET API ブラウザー](https://docs.microsoft.com/dotnet/api/?view=netstandard-2.0)を使用して代わりのクラスを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-154">We can use the [.NET API Browser](https://docs.microsoft.com/dotnet/api/?view=netstandard-2.0) to find an alternative though.</span></span> <span data-ttu-id="16c0d-155">``DbConnection``、``DbCommand``、``DbDataReader`` の各クラスはすべて .NET Standard 2.0 で利用可能であるため、それらを代わりに使用することができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-155">The ``DbConnection``, ``DbCommand``, and ``DbDataReader`` classes are all available in the .NET Standard 2.0 so we can use them instead.</span></span>  

<span data-ttu-id="16c0d-156">この改訂バージョンではこれらのクラスを使用して顧客の一覧を取得しますが、``DbConnection`` クラスを作成するには、クライアント アプリケーションで作成するファクトリ オブジェクトを渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-156">This revised version uses those classes to get a list of customers, but to create a ``DbConnection`` class, we'll need to pass in a factory object that we create in the client application.</span></span>

```csharp
public static ArrayList GetCustomerNames(DbProviderFactory factory)
{
    ArrayList customers = new ArrayList();

    using (DbConnection conn = factory.CreateConnection())
    {
        conn.ConnectionString = @"Data Source=" +
                        @"<Your Server Name>\SQLEXPRESS;Initial Catalog=NORTHWIND;Integrated Security=SSPI";

        conn.Open();

        DbCommand command = factory.CreateCommand();
        command.Connection = conn;
        command.CommandText = "select ContactName from customers order by ContactName asc";

        using (DbDataReader reader = command.ExecuteReader())
        {
            while (reader.Read())
            {
                customers.Add(reader[0]);
            }
        }
    }

    return customers;
}
```  

<span data-ttu-id="16c0d-157">Windows フォームの分離コード ページでは、ファクトリ インスタンスを作成しメソッドに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-157">In the code-behind page of the Windows Form, we can just create factory instance and pass it into our method.</span></span>

```csharp
public partial class Customers : Form
{
    public Customers()
    {
        InitializeComponent();

        dataGridView1.Rows.Clear();

        SqlClientFactory factory = SqlClientFactory.Instance;

        foreach (string customer in Northwind.GetCustomerNames(factory))
        {
            dataGridView1.Rows.Add(customer);
        }
    }
}
```

### <a name="create-a-uwp-app"></a><span data-ttu-id="16c0d-158">UWP アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-158">Create a UWP app</span></span>

<span data-ttu-id="16c0d-159">これで、ソリューションに UWP アプリを追加する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="16c0d-159">Now you're ready to add a UWP app to your solution.</span></span>

![Desktop to UWP Bridge のイメージ](images/desktop-to-uwp/adaptive-ui.png)

<span data-ttu-id="16c0d-161">UI ページは XAML で設計し、デバイス固有またはプラットフォーム固有のコードも記述する必要がありますが、完了すると、すべての Windows 10 デバイスをターゲットにすることができます。アプリ ページはさまざまな画面サイズや解像度に合わせて調整されるモダンな使用感になります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-161">You'll still have to design UI pages in XAML and write any device or platform-specific code, but when you are done, you'll be able to reach the full breadth of Windows 10 devices and your app pages will have a modern feel that adapts well to different screen sizes and resolutions.</span></span>

<span data-ttu-id="16c0d-162">アプリはキーボードとマウスだけではなく、他の入力メカニズムにも応答し、さまざまなデバイスで直感的に機能や設定を使用できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-162">Your app will respond to input mechanisms other than just a keyboard and mouse, and features and settings will be intuitive across devices.</span></span> <span data-ttu-id="16c0d-163">つまり、ユーザーが操作方法を 1 回だけ学習すると、デバイスに関係なく慣れた方法で操作できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-163">This means that users learn how to do things one time, and then it works in a very familiar way no matter the device.</span></span>

<span data-ttu-id="16c0d-164">これらは、UWP による利点のごく一部です。</span><span class="sxs-lookup"><span data-stu-id="16c0d-164">These are just a few of the goodies that come with UWP.</span></span> <span data-ttu-id="16c0d-165">詳しくは、「[Windowsで優れたエクスペリエンスを実現](https://developer.microsoft.com/windows/why-build-for-uwp)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-165">To learn more, see [Build great experiences with Windows](https://developer.microsoft.com/windows/why-build-for-uwp).</span></span>

#### <a name="add-a-uwp-project"></a><span data-ttu-id="16c0d-166">UWP プロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="16c0d-166">Add a UWP project</span></span>

<span data-ttu-id="16c0d-167">まず、UWP プロジェクトをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-167">First, add a UWP project to your solution.</span></span>

![UWP プロジェクト](images/desktop-to-uwp/new-uwp-app.png)

<span data-ttu-id="16c0d-169">次に、UWP プロジェクトから、.NET Standard 2.0 ライブラリ プロジェクトへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-169">Then, from your UWP project, add a reference the .NET Standard 2.0 library project.</span></span>

![クラス ライブラリ参照](images/desktop-to-uwp/class-library-reference2.png)

#### <a name="build-your-pages"></a><span data-ttu-id="16c0d-171">ページをビルドする</span><span class="sxs-lookup"><span data-stu-id="16c0d-171">Build your pages</span></span>

<span data-ttu-id="16c0d-172">XAML ページを追加し、.NET Standard 2.0 ライブラリ内のコードを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-172">Add XAML pages and call the code in your .NET Standard 2.0 library.</span></span>

![UWP アプリ](images/desktop-to-uwp/uwp-app.png)

```xml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <StackPanel x:Name="customerStackPanel">
        <ListView x:Name="customerList"/>
    </StackPanel>
</Grid>
```

```csharp
public sealed partial class MainPage : Page
{
    public MainPage()
    {
        this.InitializeComponent();

        SqlClientFactory factory = SqlClientFactory.Instance;

        customerList.ItemsSource = Northwind.GetCustomerNames(factory);
    }
}
```

<span data-ttu-id="16c0d-174">UWP を使い始めるには、「[UWP アプリとは](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-174">To get started with UWP, see [What's a UWP app](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide).</span></span>

### <a name="reach-ios-and-android-devices"></a><span data-ttu-id="16c0d-175">iOS および Android デバイスへのリーチ</span><span class="sxs-lookup"><span data-stu-id="16c0d-175">Reach iOS and Android devices</span></span>

<span data-ttu-id="16c0d-176">Xamarin プロジェクトを追加することにより、Android デバイスと iOS デバイスをターゲットにすることができます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-176">You can reach Android and iOS devices by adding Xamarin projects.</span></span>  

![Xamarin アプリ](images/desktop-to-uwp/xamarin-apps.png)

<span data-ttu-id="16c0d-178">これらのプロジェクトでは、C# でプラットフォーム固有およびデバイスに固有の API へのフル アクセスを使用して、Android アプリと iOS アプリを構築できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-178">These projects let you use C# to build Android and iOS apps with full access to platform-specific and device-specific APIs.</span></span> <span data-ttu-id="16c0d-179">これらのアプリはプラットフォーム固有のハードウェア アクセラレーションを利用し、ネイティブ パフォーマンス用にコンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-179">These apps leverage platform-specific hardware acceleration, and are compiled for native performance.</span></span>

<span data-ttu-id="16c0d-180">これらのアプリでは、iBeacons や Android フラグメントなどのプラットフォーム固有機能を含めて、基盤となるプラットフォームおよびデバイスによって公開される機能に全面的にアクセスできます。標準のネイティブ ユーザー インターフェイス コントロールを使用すると、ユーザーが期待する外観と操作感の UI を構築できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-180">They have access to the full spectrum of functionality exposed by the underlying platform and device, including platform-specific capabilities like iBeacons and Android Fragments and you'll use standard native user interface controls to build UIs that look and feel the way that users expect them to.</span></span>

<span data-ttu-id="16c0d-181">UWP の場合と同様、.NET Standard 2.0 クラス ライブラリに用意されているビジネス ロジックを再利用できるため、Android アプリまたは iOS アプリを追加するコストが低くなります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-181">Just like UWPs, the cost to add an Android or iOS app is lower because you can reuse business logic in a .NET Standard 2.0 class library.</span></span> <span data-ttu-id="16c0d-182">UI ページは XAML で設計し、デバイス固有またはプラットフォーム固有のコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-182">You'll have to design your UI pages in XAML and write any device or platform-specific code.</span></span>

#### <a name="add-a-xamarin-project"></a><span data-ttu-id="16c0d-183">Xamarin プロジェクトを追加する</span><span class="sxs-lookup"><span data-stu-id="16c0d-183">Add a Xamarin project</span></span>

<span data-ttu-id="16c0d-184">まず、**Android**、**iOS**、または**クロス プラットフォーム**のプロジェクトをソリューションに追加します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-184">First, add an **Android**, **iOS**, or **Cross-Platform** project to your solution.</span></span>

<span data-ttu-id="16c0d-185">これらのテンプレートは、**[新しいプロジェクトの追加]** ダイアログ ボックスの **[Visual C#]** グループにあります。</span><span class="sxs-lookup"><span data-stu-id="16c0d-185">You can find these templates in the **Add New Project** dialog box under the **Visual C#** group.</span></span>

![Xamarin アプリ](images/desktop-to-uwp/xamarin-projects.png)

>[!NOTE]
><span data-ttu-id="16c0d-187">クロスプラット フォーム プロジェクトは、プラットフォーム固有の機能がほとんどないアプリに最適です。</span><span class="sxs-lookup"><span data-stu-id="16c0d-187">Cross-platform projects are great for apps with little platform-specific functionality.</span></span> <span data-ttu-id="16c0d-188">これらを使用して、iOS、Android、および Windows で実行されるネイティブの XAML ベース UI を 1 つ構築できます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-188">You can use them to build one native XAML-based UI that runs on iOS, Android, and Windows.</span></span> <span data-ttu-id="16c0d-189">[こちら](https://www.xamarin.com/forms)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-189">Learn more [here](https://www.xamarin.com/forms).</span></span>

<span data-ttu-id="16c0d-190">次に、Android、iOS、またはクロスプラットフォーム プロジェクトから、クラス ライブラリ プロジェクトの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="16c0d-190">Then, from your Android, iOS, or cross-platform project, add a reference the class library project.</span></span>

![クラス ライブラリ参照](images/desktop-to-uwp/class-library-reference3.png)

#### <a name="build-your-pages"></a><span data-ttu-id="16c0d-192">ページをビルドする</span><span class="sxs-lookup"><span data-stu-id="16c0d-192">Build your pages</span></span>

<span data-ttu-id="16c0d-193">この例では、Android アプリに顧客の一覧が示されます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-193">Our example shows a list of customers in an Android app.</span></span>

![Android アプリ](images/desktop-to-uwp/android-app.png)

```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:padding="10dp" android:textSize="16sp"
    android:id="@android:id/list">
</TextView>
```

```csharp
[Activity(Label = "MyAndroidApp", MainLauncher = true)]
public class MainActivity : ListActivity
{
    protected override void OnCreate(Bundle savedInstanceState)
    {
        base.OnCreate(savedInstanceState);

        SqlClientFactory factory = SqlClientFactory.Instance;

        var customers = (string[])Northwind.GetCustomerNames(factory).ToArray(typeof(string));

        ListAdapter = new ArrayAdapter<string>(this, Resource.Layout.list_item, customers);
    }
}
```

<span data-ttu-id="16c0d-195">Android プロジェクト、iOS プロジェクト、およびクロスプラットフォーム プロジェクトの概要については、[Xamarin 開発者ポータル](https://developer.xamarin.com/)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-195">To get started with Android, iOS, and cross-platform projects, see the [Xamarin developer portal](https://developer.xamarin.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c0d-196">次のステップ</span><span class="sxs-lookup"><span data-stu-id="16c0d-196">Next steps</span></span>

<span data-ttu-id="16c0d-197">**質問の回答を検索**</span><span class="sxs-lookup"><span data-stu-id="16c0d-197">**Find answers to your questions**</span></span>

<span data-ttu-id="16c0d-198">ご質問がある場合は、</span><span class="sxs-lookup"><span data-stu-id="16c0d-198">Have questions?</span></span> <span data-ttu-id="16c0d-199">Stack Overflow でお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-199">Ask us on Stack Overflow.</span></span> <span data-ttu-id="16c0d-200">Microsoft のチームでは、これらの[タグ](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge)をチェックしています。</span><span class="sxs-lookup"><span data-stu-id="16c0d-200">Our team monitors these [tags](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge).</span></span> <span data-ttu-id="16c0d-201">[こちら](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D)から質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="16c0d-201">You can also ask us [here](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D).</span></span>

<span data-ttu-id="16c0d-202">**ご意見や機能を提案します。**</span><span class="sxs-lookup"><span data-stu-id="16c0d-202">**Give feedback or make feature suggestions**</span></span>

<span data-ttu-id="16c0d-203">[UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial) のページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="16c0d-203">See [UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial).</span></span>
