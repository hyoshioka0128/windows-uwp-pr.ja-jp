---
description: C++/WinRT は、Windows Runtime クラスを作成するのに役立つのと同様に、従来の COM コンポーネントを作成するのに役立ちます。
title: C++/WinRT での COM コンポーネントの作成
ms.date: 04/24/2019
ms.topic: article
keywords: windows 10、uwp、standard、c++、cpp、winrt、プロジェクション、作成者は、COM、コンポーネント
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 3badcd59155bc4bb5ef8d9e29271b853c245c24e
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66360323"
---
# <a name="author-com-components-with-cwinrt"></a><span data-ttu-id="4938f-104">C++/WinRT での COM コンポーネントの作成</span><span class="sxs-lookup"><span data-stu-id="4938f-104">Author COM components with C++/WinRT</span></span>

<span data-ttu-id="4938f-105">[C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt) Windows ランタイム クラスの作成に利用すると同様に、クラシック コンポーネント オブジェクト モデル (COM) コンポーネント (またはコクラス) を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="4938f-105">[C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt) can help you to author classic Component Object Model (COM) components (or coclasses), just as it helps you to author Windows Runtime classes.</span></span> <span data-ttu-id="4938f-106">ここでは、単純な図にコードを貼り付ける場合をテストすることができます、`pch.h`と`main.cpp`新しい**Windows コンソール アプリケーション (C +/cli WinRT)** プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="4938f-106">Here's a simple illustration, which you can test out if you paste the code into the `pch.h` and `main.cpp` of a new **Windows Console Application (C++/WinRT)** project.</span></span>

```cppwinrt
// pch.h
#pragma once
#include <unknwn.h>
#include <winrt/Windows.Foundation.h>

// main.cpp : Defines the entry point for the console application.
#include "pch.h"

struct __declspec(uuid("ddc36e02-18ac-47c4-ae17-d420eece2281")) IMyComInterface : ::IUnknown
{
    virtual HRESULT __stdcall Call() = 0;
};

using namespace winrt;
using namespace Windows::Foundation;

int main()
{
    winrt::init_apartment();

    struct MyCoclass : winrt::implements<MyCoclass, IPersist, IStringable, IMyComInterface>
    {
        HRESULT __stdcall Call() noexcept override
        {
            return S_OK;
        }

        HRESULT __stdcall GetClassID(CLSID* id) noexcept override
        {
            *id = IID_IPersist; // Doesn't matter what we return, for this example.
            return S_OK;
        }

        winrt::hstring ToString()
        {
            return L"MyCoclass as a string";
        }
    };

    auto mycoclass_instance{ winrt::make<MyCoclass>() };
    CLSID id{};
    winrt::check_hresult(mycoclass_instance->GetClassID(&id));
    winrt::check_hresult(mycoclass_instance.as<IMyComInterface>()->Call());
}
```

<span data-ttu-id="4938f-107">参照してください[C + での使用の COM コンポーネント/cli WinRT](consume-com.md)します。</span><span class="sxs-lookup"><span data-stu-id="4938f-107">Also see [Consume COM components with C++/WinRT](consume-com.md).</span></span>

## <a name="a-more-realistic-and-interesting-example"></a><span data-ttu-id="4938f-108">現実的で興味深い例</span><span class="sxs-lookup"><span data-stu-id="4938f-108">A more realistic and interesting example</span></span>

<span data-ttu-id="4938f-109">このトピックの残りの部分は、C + を使用して最小限のコンソール アプリケーション プロジェクトを作成する手順について説明します/cli WinRT (COM コンポーネントまたは COM クラス) の基本的なコクラスとクラス ファクトリを実装します。</span><span class="sxs-lookup"><span data-stu-id="4938f-109">The remainder of this topic walks through creating a minimal console application project that uses C++/WinRT to implement a basic coclass (COM component, or COM class) and class factory.</span></span> <span data-ttu-id="4938f-110">アプリケーションの例は、コールバック ボタンと、コクラスのトースト通知を配信する方法を示します (実装する、 **INotificationActivationCallback** COM インターフェイス) により、アプリケーションが起動され、呼び出されますユーザーは、トーストでそのボタンをクリックしたときにバックアップします。</span><span class="sxs-lookup"><span data-stu-id="4938f-110">The example application shows how to deliver a toast notification with a callback button on it, and the coclass (which implements the **INotificationActivationCallback** COM interface) allows the application to be launched and called back when the user clicks that button on the toast.</span></span>

<span data-ttu-id="4938f-111">さらに詳しく知り、トースト通知の機能領域をご覧[ローカル トースト通知を送信](/windows/uwp/design/shell/tiles-and-notifications/send-local-toast)します。</span><span class="sxs-lookup"><span data-stu-id="4938f-111">More background about the toast notification feature area can be found at [Send a local toast notification](/windows/uwp/design/shell/tiles-and-notifications/send-local-toast).</span></span> <span data-ttu-id="4938f-112">ドキュメントのセクションのコード例のいずれを使用して、C +/cli WinRT、ただし、これをお勧めこのトピックに示すようにコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="4938f-112">None of the code examples in that section of the documentation use C++/WinRT, though, so we recommend that you prefer the code shown in this topic.</span></span>

## <a name="create-a-windows-console-application-project-toastandcallback"></a><span data-ttu-id="4938f-113">Windows コンソール アプリケーション プロジェクト (ToastAndCallback) を作成します。</span><span class="sxs-lookup"><span data-stu-id="4938f-113">Create a Windows Console Application project (ToastAndCallback)</span></span>

<span data-ttu-id="4938f-114">まず、Microsoft Visual Studio で、新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="4938f-114">Begin by creating a new project in Microsoft Visual Studio.</span></span> <span data-ttu-id="4938f-115">作成、 **Windows コンソール アプリケーション (C++/WinRT)** プロジェクト、および名前を付けます*ToastAndCallback*します。</span><span class="sxs-lookup"><span data-stu-id="4938f-115">Create a **Windows Console Application (C++/WinRT)** project, and name it *ToastAndCallback*.</span></span>

<span data-ttu-id="4938f-116">オープン`pch.h`、し、追加`#include <unknwn.h>`する前が含まれますすべて C +/cli WinRT ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="4938f-116">Open `pch.h`, and add `#include <unknwn.h>` before the includes for any C++/WinRT headers.</span></span> <span data-ttu-id="4938f-117">結果を次に示します内容を置き換えることができます、`pch.h`この一覧にします。</span><span class="sxs-lookup"><span data-stu-id="4938f-117">Here's the result; you can replace the contents of your `pch.h` with this listing.</span></span>

```cppwinrt
// pch.h
#pragma once
#include <unknwn.h>
#include <winrt/Windows.Foundation.h>
```

<span data-ttu-id="4938f-118">開いている`main.cpp`ディレクティブを削除を使用して、プロジェクト テンプレートを生成するとします。</span><span class="sxs-lookup"><span data-stu-id="4938f-118">Open `main.cpp`, and remove the using-directives that the project template generates.</span></span> <span data-ttu-id="4938f-119">代わりに、(ライブラリ、ヘッダー、および必要な型名により) 次のコードを挿入します。</span><span class="sxs-lookup"><span data-stu-id="4938f-119">In their place, insert the following code (which gives us the libs, headers, and type names that we need).</span></span> <span data-ttu-id="4938f-120">結果を次に示します内容を置き換えることができます、`main.cpp`この一覧に (からコードを削除しましたも`main`、下の一覧で置き換える関数後であるため)。</span><span class="sxs-lookup"><span data-stu-id="4938f-120">Here's the result; you can replace the contents of your `main.cpp` with this listing (we've also removed the code from `main` in the listing below, because we'll be replacing that function later).</span></span>

```cppwinrt
// main.cpp : Defines the entry point for the console application.

#include "pch.h"

#pragma comment(lib, "advapi32")
#pragma comment(lib, "ole32")
#pragma comment(lib, "shell32")

#include <iomanip>
#include <iostream>
#include <notificationactivationcallback.h>
#include <propkey.h>
#include <propvarutil.h>
#include <shlobj.h>
#include <winrt/Windows.UI.Notifications.h>
#include <winrt/Windows.Data.Xml.Dom.h>

using namespace winrt;
using namespace Windows::Data::Xml::Dom;
using namespace Windows::UI::Notifications;

int main() { }
```

<span data-ttu-id="4938f-121">プロジェクトがまだビルドはありません。コードの追加が完了したら、ビルドおよび実行を求め。</span><span class="sxs-lookup"><span data-stu-id="4938f-121">The project won't build yet; after we've finished adding code, you'll be prompted to build and run.</span></span>

## <a name="implement-the-coclass-and-class-factory"></a><span data-ttu-id="4938f-122">コクラスとクラス ファクトリを実装します。</span><span class="sxs-lookup"><span data-stu-id="4938f-122">Implement the coclass and class factory</span></span>

<span data-ttu-id="4938f-123">C++/cli WinRT、実装するコクラス、およびクラスのファクトリから派生することによって、 [ **winrt::implements** ](/uwp/cpp-ref-for-winrt/implements)基底構造体。</span><span class="sxs-lookup"><span data-stu-id="4938f-123">In C++/WinRT, you implement coclasses, and class factories, by deriving from the [**winrt::implements**](/uwp/cpp-ref-for-winrt/implements) base struct.</span></span> <span data-ttu-id="4938f-124">次の 3 つを使用して、ディレクティブは、上記の直後に (前に`main`)、トースト通知 COM のアクティベーター コンポーネントを実装するには、このコードを貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="4938f-124">Immediately after the three using-directives shown above (and before `main`), paste this code to implement your toast notification COM activator component.</span></span>

```cppwinrt
static constexpr GUID callback_guid // BAF2FA85-E121-4CC9-A942-CE335B6F917F
{
    0xBAF2FA85, 0xE121, 0x4CC9, {0xA9, 0x42, 0xCE, 0x33, 0x5B, 0x6F, 0x91, 0x7F}
};

std::wstring const this_app_name{ L"ToastAndCallback" };

struct callback : winrt::implements<callback, INotificationActivationCallback>
{
    HRESULT __stdcall Activate(
        LPCWSTR app,
        LPCWSTR args,
        [[maybe_unused]] NOTIFICATION_USER_INPUT_DATA const* data,
        [[maybe_unused]] ULONG count) noexcept final
    {
        try
        {
            std::wcout << this_app_name << L" has been called back from a notification." << std::endl;
            std::wcout << L"Value of the 'app' parameter is '" << app << L"'." << std::endl;
            std::wcout << L"Value of the 'args' parameter is '" << args << L"'." << std::endl;
            return S_OK;
        }
        catch (...)
        {
            return winrt::to_hresult();
        }
    }
};

struct callback_factory : implements<callback_factory, IClassFactory>
{
    HRESULT __stdcall CreateInstance(
        IUnknown* outer,
        GUID const& iid,
        void** result) noexcept final
    {
        *result = nullptr;

        if (outer)
        {
            return CLASS_E_NOAGGREGATION;
        }

        return make<callback>()->QueryInterface(iid, result);
    }

    HRESULT __stdcall LockServer(BOOL) noexcept final
    {
        return S_OK;
    }
};
```

<span data-ttu-id="4938f-125">上記のコクラスの実装は」に示したのと同じパターンに従います[作成者 Api c++/cli WinRT](/windows/uwp/cpp-and-winrt-apis/author-apis#if-youre-not-authoring-a-runtime-class)します。</span><span class="sxs-lookup"><span data-stu-id="4938f-125">The implementation of the coclass above follows the same pattern that's demonstrated in [Author APIs with C++/WinRT](/windows/uwp/cpp-and-winrt-apis/author-apis#if-youre-not-authoring-a-runtime-class).</span></span> <span data-ttu-id="4938f-126">そのため、COM インターフェイスと Windows ランタイム インターフェイスを実装するために、同じ手法を使用できます。</span><span class="sxs-lookup"><span data-stu-id="4938f-126">So, you can use the same technique to implement COM interfaces as well as Windows Runtime interfaces.</span></span> <span data-ttu-id="4938f-127">COM コンポーネントと Windows ランタイム クラス、インターフェイスを使用してその機能を公開します。</span><span class="sxs-lookup"><span data-stu-id="4938f-127">COM components and Windows Runtime classes expose their features via interfaces.</span></span> <span data-ttu-id="4938f-128">すべての COM インターフェイスが最終的に派生、 [ **IUnknown インターフェイス**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="4938f-128">Every COM interface ultimately derives from the [**IUnknown interface**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown) interface.</span></span> <span data-ttu-id="4938f-129">Windows ランタイムは COM に基づいて&mdash;から派生している Windows ランタイムが最終的にインターフェイス 1 つの違い、 [ **IInspectable インターフェイス**](/windows/desktop/api/inspectable/nn-inspectable-iinspectable) (と**IInspectable**から派生した**IUnknown**)。</span><span class="sxs-lookup"><span data-stu-id="4938f-129">The Windows Runtime is based on COM&mdash;one distinction being that Windows Runtime interfaces ultimately derive from the [**IInspectable interface**](/windows/desktop/api/inspectable/nn-inspectable-iinspectable) (and **IInspectable** derives from **IUnknown**).</span></span>

<span data-ttu-id="4938f-130">上記のコードでは、コクラスの実装、 **INotificationActivationCallback::Activate**メソッドは、ユーザーがトースト通知のコールバックのボタンをクリックしたときに呼び出される関数。</span><span class="sxs-lookup"><span data-stu-id="4938f-130">In the coclass in the code above, we implement the **INotificationActivationCallback::Activate** method, which is the function that's called when the user clicks the callback button on a toast notification.</span></span> <span data-ttu-id="4938f-131">その関数を呼び出すことができます、前に、コクラスのインスタンスを作成する必要がありますの仕事です。 この、 **IClassFactory::CreateInstance**関数。</span><span class="sxs-lookup"><span data-stu-id="4938f-131">But before that function can be called, an instance of the coclass needs to be created, and that's the job of the **IClassFactory::CreateInstance** function.</span></span>

<span data-ttu-id="4938f-132">実装しましたコクラスと呼ばれる、 *COM アクティベーター*の通知、およびそれがの形式でクラス id (CLSID) がある、`callback_guid`識別子 (型の**GUID**) を上記を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4938f-132">The coclass that we just implemented is known as the *COM activator* for notifications, and it has its class id (CLSID) in the form of the `callback_guid` identifier (of type **GUID**) that you see above.</span></span> <span data-ttu-id="4938f-133">使用する識別子後で、[スタート] メニューのショートカットと Windows レジストリ エントリの形式でします。</span><span class="sxs-lookup"><span data-stu-id="4938f-133">We'll be using that identifier later, in the form of a Start menu shortcut and a Windows Registry entry.</span></span> <span data-ttu-id="4938f-134">COM アクティベーター CLSID、およびその関連付けられている COM サーバー (つまりここで作成している実行可能ファイルへのパス) へのパスは、コールバックのボタンがクリックされたときのインスタンスを作成するクラスをトースト通知が認識するメカニズム (かどうか、通知がクリックされたアクション センターか)。</span><span class="sxs-lookup"><span data-stu-id="4938f-134">The COM activator CLSID, and the path to its associated COM server (which is the path to the executable that we're building here) is the mechanism by which a toast notification knows what class to create an instance of when its callback button is clicked (whether the notification is clicked in Action Center or not).</span></span>

## <a name="best-practices-for-implementing-com-methods"></a><span data-ttu-id="4938f-135">COM メソッドを実装するためのベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="4938f-135">Best practices for implementing COM methods</span></span>

<span data-ttu-id="4938f-136">エラー処理とリソースの管理手法では、手の形に密接に連携を移動できます。</span><span class="sxs-lookup"><span data-stu-id="4938f-136">Techniques for error handling and for resource management can go hand-in-hand.</span></span> <span data-ttu-id="4938f-137">便利でエラー コードよりも例外を使用するは実用的になります。</span><span class="sxs-lookup"><span data-stu-id="4938f-137">It's more convenient and practical to use exceptions than error codes.</span></span> <span data-ttu-id="4938f-138">リソースの取得-がの初期化 (RAII) の表現形式を使用する場合を回避できますエラー コードの明示的に確認し、リソースを明示的に解放します。</span><span class="sxs-lookup"><span data-stu-id="4938f-138">And if you employ the resource-acquisition-is-initialization (RAII) idiom, then you can avoid explicitly checking for error codes and then explicitly releasing resources.</span></span> <span data-ttu-id="4938f-139">このような明示的なチェックは必要に応じてよりもより複雑ですが、コードを行い、場所を非表示にはたくさんのバグを提供します。</span><span class="sxs-lookup"><span data-stu-id="4938f-139">Such explicit checks make your code more convoluted than necessary, and it gives bugs plenty of places to hide.</span></span> <span data-ttu-id="4938f-140">代わりに、RAII を使用して、例外のスローと catch</span><span class="sxs-lookup"><span data-stu-id="4938f-140">Instead, use RAII, and throw/catch exceptions.</span></span> <span data-ttu-id="4938f-141">これにより、リソースの割り当ては例外セーフと、コードは単純です。</span><span class="sxs-lookup"><span data-stu-id="4938f-141">That way, your resource allocations are exception-safe, and your code is simple.</span></span>

<span data-ttu-id="4938f-142">ただし、COM メソッドの実装をエスケープする例外を許可しないでください。</span><span class="sxs-lookup"><span data-stu-id="4938f-142">However, you mustn't allow exceptions to escape your COM method implementations.</span></span> <span data-ttu-id="4938f-143">使用して行うことができます、 `noexcept` COM メソッドの指定子。</span><span class="sxs-lookup"><span data-stu-id="4938f-143">You can ensure that by using the `noexcept` specifier on your COM methods.</span></span> <span data-ttu-id="4938f-144">メソッドが終了する前にそれらを処理する限り、メソッドの呼び出しグラフで任意の場所がスローされる例外では問題が。</span><span class="sxs-lookup"><span data-stu-id="4938f-144">It's ok for exceptions to be thrown anywhere in the call graph of your method, as long as you handle them before your method exits.</span></span> <span data-ttu-id="4938f-145">使用する場合`noexcept`が、メソッドをエスケープするための例外を許可し、アプリケーションは終了します。</span><span class="sxs-lookup"><span data-stu-id="4938f-145">If you use `noexcept`, but you then allow an exception to escape your method, then your application will terminate.</span></span>

## <a name="add-helper-types-and-functions"></a><span data-ttu-id="4938f-146">ヘルパー型および関数を追加します。</span><span class="sxs-lookup"><span data-stu-id="4938f-146">Add helper types and functions</span></span>

<span data-ttu-id="4938f-147">このステップでのコードの残りの部分は、いくつかヘルパー型および関数を使用して追加します。</span><span class="sxs-lookup"><span data-stu-id="4938f-147">In this step, we'll add some helper types and functions that the rest of the code makes use of.</span></span> <span data-ttu-id="4938f-148">直前に`main`以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="4938f-148">So, immediately before `main`, add the following.</span></span>

```cppwinrt
struct prop_variant : PROPVARIANT
{
    prop_variant() noexcept : PROPVARIANT{}
    {
    }

    ~prop_variant() noexcept
    {
        clear();
    }

    void clear() noexcept
    {
        WINRT_VERIFY_(S_OK, ::PropVariantClear(this));
    }
};

struct registry_traits
{
    using type = HKEY;

    static void close(type value) noexcept
    {
        WINRT_VERIFY_(ERROR_SUCCESS, ::RegCloseKey(value));
    }

    static constexpr type invalid() noexcept
    {
        return nullptr;
    }
};

using registry_key = winrt::handle_type<registry_traits>;

std::wstring get_module_path()
{
    std::wstring path(100, L'?');
    uint32_t path_size{};
    DWORD actual_size{};

    do
    {
        path_size = static_cast<uint32_t>(path.size());
        actual_size = ::GetModuleFileName(nullptr, path.data(), path_size);

        if (actual_size + 1 > path_size)
        {
            path.resize(path_size * 2, L'?');
        }
    } while (actual_size + 1 > path_size);

    path.resize(actual_size);
    return path;
}

std::wstring get_shortcut_path()
{
    std::wstring format{ LR"(%ProgramData%\Microsoft\Windows\Start Menu\Programs\)" };
    format += (this_app_name + L".lnk");

    auto required{ ::ExpandEnvironmentStrings(format.c_str(), nullptr, 0) };
    std::wstring path(required - 1, L'?');
    ::ExpandEnvironmentStrings(format.c_str(), path.data(), required);
    return path;
}
```

## <a name="implement-the-remaining-functions-and-the-wmain-entry-point-function"></a><span data-ttu-id="4938f-149">残りの関数では、および wmain のエントリ ポイント関数を実装します。</span><span class="sxs-lookup"><span data-stu-id="4938f-149">Implement the remaining functions, and the wmain entry point function</span></span>

<span data-ttu-id="4938f-150">削除、`main`関数、およびその場所に貼り付け、コクラスを登録するコードが含まれている一覧から、このコードをクリックし、トースト、アプリケーションのコールバックの対応を配信します。</span><span class="sxs-lookup"><span data-stu-id="4938f-150">Delete your `main` function, and in its place paste this code listing, which includes code to register your coclass, and then to deliver a toast capable of calling back your application.</span></span>

```cppwinrt
void register_callback()
{
    DWORD registration{};

    winrt::check_hresult(::CoRegisterClassObject(
        callback_guid,
        make<callback_factory>().get(),
        CLSCTX_LOCAL_SERVER,
        REGCLS_SINGLEUSE,
        &registration));
}

void create_shortcut()
{
    auto link{ winrt::create_instance<IShellLink>(CLSID_ShellLink) };
    std::wstring module_path{ get_module_path() };
    winrt::check_hresult(link->SetPath(module_path.c_str()));

    auto store = link.as<IPropertyStore>();
    prop_variant value;
    winrt::check_hresult(::InitPropVariantFromString(this_app_name.c_str(), &value));
    winrt::check_hresult(store->SetValue(PKEY_AppUserModel_ID, value));
    value.clear();
    winrt::check_hresult(::InitPropVariantFromCLSID(callback_guid, &value));
    winrt::check_hresult(store->SetValue(PKEY_AppUserModel_ToastActivatorCLSID, value));

    auto file{ store.as<IPersistFile>() };
    std::wstring shortcut_path{ get_shortcut_path() };
    winrt::check_hresult(file->Save(shortcut_path.c_str(), TRUE));

    std::wcout << L"In " << shortcut_path << L", created a shortcut to " << module_path << std::endl;
}

void update_registry()
{
    std::wstring key_path{ LR"(SOFTWARE\Classes\CLSID\{????????-????-????-????-????????????})" };
    ::StringFromGUID2(callback_guid, key_path.data() + 23, 39);
    key_path += LR"(\LocalServer32)";
    registry_key key;

    winrt::check_win32(::RegCreateKeyEx(
        HKEY_CURRENT_USER,
        key_path.c_str(),
        0,
        nullptr,
        0,
        KEY_WRITE,
        nullptr,
        key.put(),
        nullptr));
    ::RegDeleteValue(key.get(), nullptr);

    std::wstring path{ get_module_path() };

    winrt::check_win32(::RegSetValueEx(
        key.get(),
        nullptr,
        0,
        REG_SZ,
        reinterpret_cast<BYTE const*>(path.c_str()),
        static_cast<uint32_t>((path.size() + 1) * sizeof(wchar_t))));

    std::wcout << L"In " << key_path << L", registered local server at " << path << std::endl;
}

void create_toast()
{
    XmlDocument xml;

    std::wstring toastPayload
    {
        LR"(
<toast>
  <visual>
    <binding template='ToastGeneric'>
      <text>)"
    };
    toastPayload += this_app_name;
    toastPayload += LR"(
      </text>
    </binding>
  </visual>
  <actions>
    <action content='Call back )";
    toastPayload += this_app_name;
    toastPayload += LR"(
' arguments='the_args' activationKind='Foreground' />
  </actions>
</toast>)";
    xml.LoadXml(toastPayload);

    ToastNotification toast{ xml };
    ToastNotifier notifier{ ToastNotificationManager::CreateToastNotifier(this_app_name) };
    notifier.Show(toast);
    ::Sleep(50); // Give the callback chance to display.
}

void LaunchedNormally(HANDLE, INPUT_RECORD &, DWORD &);
void LaunchedFromNotification(HANDLE, INPUT_RECORD &, DWORD &);

int wmain(int argc, wchar_t * argv[], wchar_t * /* envp */[])
{
    winrt::init_apartment();

    register_callback();

    HANDLE consoleHandle{ ::GetStdHandle(STD_INPUT_HANDLE) };
    INPUT_RECORD buffer{};
    DWORD events{};
    ::FlushConsoleInputBuffer(consoleHandle);

    if (argc == 1)
    {
        LaunchedNormally(consoleHandle, buffer, events);
    }
    else if (argc == 2 && wcscmp(argv[1], L"-Embedding") == 0)
    {
        LaunchedFromNotification(consoleHandle, buffer, events);
    }
}

void LaunchedNormally(HANDLE consoleHandle, INPUT_RECORD & buffer, DWORD & events)
{
    try
    {
        bool runningAsAdmin{ ::IsUserAnAdmin() == TRUE };
        std::wcout << this_app_name << L" is running" << (runningAsAdmin ? L" (administrator)." : L" (NOT as administrator).") << std::endl;

        if (runningAsAdmin)
        {
            create_shortcut();
            update_registry();
        }

        std::wcout << std::endl << L"Press 'T' to display a toast notification (press any other key to exit)." << std::endl;

        ::ReadConsoleInput(consoleHandle, &buffer, 1, &events);
        if (towupper(buffer.Event.KeyEvent.uChar.UnicodeChar) == L'T')
        {
            create_toast();
        }
    }
    catch (winrt::hresult_error const& e)
    {
        std::wcout << L"Error: " << e.message().c_str() << L" (" << std::hex << std::showbase << std::setw(8) << static_cast<uint32_t>(e.code()) << L")" << std::endl;
    }
}

void LaunchedFromNotification(HANDLE consoleHandle, INPUT_RECORD & buffer, DWORD & events)
{
    ::Sleep(50); // Give the callback chance to display its message.
    std::wcout << std::endl << L"Press any key to exit." << std::endl;
    ::ReadConsoleInput(consoleHandle, &buffer, 1, &events);
}
```

## <a name="how-to-test-the-example-application"></a><span data-ttu-id="4938f-151">サンプル アプリケーションをテストする方法</span><span class="sxs-lookup"><span data-stu-id="4938f-151">How to test the example application</span></span>

<span data-ttu-id="4938f-152">アプリケーションをビルドし、少なくとも 1 回の登録、およびその他のセットアップでは、コードを実行させるに管理者として実行します。</span><span class="sxs-lookup"><span data-stu-id="4938f-152">Build the application, and then run it at least once as an administrator to cause the registration, and other setup, code to run.</span></span> <span data-ttu-id="4938f-153">1 つの簡単な方法では、管理者として Visual Studio を実行し、Visual Studio からアプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="4938f-153">One way to do that is to run Visual Studio as an administrator, and then run the app from Visual Studio.</span></span> <span data-ttu-id="4938f-154">ジャンプ リストを表示、ジャンプ リストで、Visual Studio を右クリックし、クリックして、タスク バーで、Visual Studio を右クリックして**管理者として実行**します。</span><span class="sxs-lookup"><span data-stu-id="4938f-154">Right-click Visual Studio in the taskbar to display the jump list, right-click Visual Studio on the jump list, and then click **Run as administrator**.</span></span> <span data-ttu-id="4938f-155">プロンプトに同意し、プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="4938f-155">Agree to the prompt, and then open the project.</span></span> <span data-ttu-id="4938f-156">アプリケーションを実行すると、アプリケーションが管理者として実行されているかどうかを示すメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4938f-156">When you run the application, a message is displayed indicating whether or not the application is running as an administrator.</span></span> <span data-ttu-id="4938f-157">いない場合は、登録とその他のセットアップは実行されません。</span><span class="sxs-lookup"><span data-stu-id="4938f-157">If it isn't, then the registration and other setup won't run.</span></span> <span data-ttu-id="4938f-158">その登録とその他のセットアップは正常に動作するアプリケーションの順序で少なくとも 1 回実行するがあります。</span><span class="sxs-lookup"><span data-stu-id="4938f-158">That registration and other setup has to run at least once in order for the application to work correctly.</span></span>

<span data-ttu-id="4938f-159">管理者としてアプリケーションを実行しているかどうかを押して 'T' に表示されるトーストを発生します。</span><span class="sxs-lookup"><span data-stu-id="4938f-159">Whether or not you're running the application as an administrator, press 'T' to cause a toast to be displayed.</span></span> <span data-ttu-id="4938f-160">クリックすることができます、 **ToastAndCallback コールバック**ボタン、トースト通知が表示されたら、またはアクション センター、およびアプリケーションから直接起動する、インスタンス化すると、コクラスと**INotificationActivationCallback::Activate**メソッドを実行します。</span><span class="sxs-lookup"><span data-stu-id="4938f-160">You can then click the **Call back ToastAndCallback** button either directly from the toast notification that pops up, or from the Action Center, and your application will be launched, the coclass instantiated, and the **INotificationActivationCallback::Activate** method executed.</span></span>

## <a name="in-process-com-server"></a><span data-ttu-id="4938f-161">インプロセス COM サーバー</span><span class="sxs-lookup"><span data-stu-id="4938f-161">In-process COM server</span></span>

<span data-ttu-id="4938f-162">*ToastAndCallback*上記の例のアプリはローカル (または、プロセス外の) COM サーバーとして機能します。</span><span class="sxs-lookup"><span data-stu-id="4938f-162">The *ToastAndCallback* example app above functions as a local (or out-of-process) COM server.</span></span> <span data-ttu-id="4938f-163">これにより、表示、 [LocalServer32](/windows/desktop/com/localserver32) Windows レジストリ キーのコクラスの CLSID を登録するために使用します。</span><span class="sxs-lookup"><span data-stu-id="4938f-163">This is indicated by the [LocalServer32](/windows/desktop/com/localserver32) Windows Registry key that you use to register the CLSID of its coclass.</span></span> <span data-ttu-id="4938f-164">ローカル COM サーバーのホスト実行可能ファイルのバイナリ内の coclass(es) (、 `.exe`)。</span><span class="sxs-lookup"><span data-stu-id="4938f-164">A local COM server hosts its coclass(es) inside an executable binary (an `.exe`).</span></span>

<span data-ttu-id="4938f-165">または (と可能性の高いほぼ間違いなく)、ダイナミック リンク ライブラリ内で、coclass(es) をホストすることもできます (、 `.dll`)。</span><span class="sxs-lookup"><span data-stu-id="4938f-165">Alternatively (and arguably more likely), you can choose to host your coclass(es) inside a dynamic-link library (a `.dll`).</span></span> <span data-ttu-id="4938f-166">DLL の形式での COM サーバーは、インプロセス COM サーバーと呼ばれ、Clsid を使用して登録されているで示された、 [InprocServer32](/windows/desktop/com/inprocserver32) Windows レジストリ キー。</span><span class="sxs-lookup"><span data-stu-id="4938f-166">A COM server in the form of a DLL is known as an in-process COM server, and it's indicated by CLSIDs being registered by using the [InprocServer32](/windows/desktop/com/inprocserver32) Windows Registry key.</span></span>

### <a name="create-a-dynamic-link-library-dll-project"></a><span data-ttu-id="4938f-167">ダイナミック リンク ライブラリ (DLL) プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="4938f-167">Create a Dynamic-Link Library (DLL) project</span></span>

<span data-ttu-id="4938f-168">Microsoft Visual Studio で新しいプロジェクトを作成して、インプロセス COM サーバーを作成するタスクを開始することができます。</span><span class="sxs-lookup"><span data-stu-id="4938f-168">You can begin the task of creating an in-process COM server by creating a new project in Microsoft Visual Studio.</span></span> <span data-ttu-id="4938f-169">作成、 **Visual C** > **Windows デスクトップ** > **ダイナミック リンク ライブラリ (DLL)** プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="4938f-169">Create a **Visual C++** > **Windows Desktop** > **Dynamic-Link Library (DLL)** project.</span></span>

<span data-ttu-id="4938f-170">追加 C +/cli WinRT サポート、新しいプロジェクトに次の記載された手順[C + を追加する Windows デスクトップ アプリケーション プロジェクトを変更する/cli WinRT サポート](/windows/uwp/cpp-and-winrt-apis/get-started#modify-a-windows-desktop-application-project-to-add-cwinrt-support)します。</span><span class="sxs-lookup"><span data-stu-id="4938f-170">To add C++/WinRT support to the new project, follow the steps described in [Modify a Windows Desktop application project to add C++/WinRT support](/windows/uwp/cpp-and-winrt-apis/get-started#modify-a-windows-desktop-application-project-to-add-cwinrt-support).</span></span>

### <a name="implement-the-coclass-class-factory-and-in-proc-server-exports"></a><span data-ttu-id="4938f-171">コクラス、クラス ファクトリ、および、インプロセス サーバーのエクスポートを実装します。</span><span class="sxs-lookup"><span data-stu-id="4938f-171">Implement the coclass, class factory, and in-proc server exports</span></span>

<span data-ttu-id="4938f-172">開いている`dllmain.cpp`、し、次に示すコード リストを追加します。</span><span class="sxs-lookup"><span data-stu-id="4938f-172">Open `dllmain.cpp`, and add to it the code listing shown below.</span></span>

<span data-ttu-id="4938f-173">C + を実装する DLL があれば/cli WinRT Windows ランタイム クラスを既にがある得られます、 **DllCanUnloadNow**次に示す関数。</span><span class="sxs-lookup"><span data-stu-id="4938f-173">If you already have a DLL that implements C++/WinRT Windows Runtime classes, then you'll already have the **DllCanUnloadNow** function shown below.</span></span> <span data-ttu-id="4938f-174">コクラスをその DLL に追加するかどうかは、追加することができます、 **DllGetClassObject**関数。</span><span class="sxs-lookup"><span data-stu-id="4938f-174">If you want to add coclasses to that DLL, then you can add the **DllGetClassObject** function.</span></span>

<span data-ttu-id="4938f-175">場合は既存の必要はありません[Windows ランタイム C++ テンプレート ライブラリ (WRL)](/cpp/windows/windows-runtime-cpp-template-library-wrl)に示すコードからパーツのコードを使用すると、互換性を維持するその、WRL を削除することができます。</span><span class="sxs-lookup"><span data-stu-id="4938f-175">If don't have existing [Windows Runtime C++ Template Library (WRL)](/cpp/windows/windows-runtime-cpp-template-library-wrl) code that you want to stay compatible with, then you can remove the WRL parts from the code shown.</span></span>

```cppwinrt
// dllmain.cpp

struct MyCoclass : winrt::implements<MyCoclass, IPersist>
{
    HRESULT STDMETHODCALLTYPE GetClassID(CLSID* id) noexcept override
    {
        *id = IID_IPersist; // Doesn't matter what we return, for this example.
        return S_OK;
    }
};

struct __declspec(uuid("85d6672d-0606-4389-a50a-356ce7bded09"))
    MyCoclassFactory : winrt::implements<MyCoclassFactory, IClassFactory>
{
    HRESULT STDMETHODCALLTYPE CreateInstance(IUnknown *pUnkOuter, REFIID riid, void **ppvObject) noexcept override
    {
        try
        {
            *ppvObject = winrt::make<MyCoclass>().get();
            return S_OK;
        }
        catch (...)
        {
            return winrt::to_hresult();
        }
    }

    HRESULT STDMETHODCALLTYPE LockServer(BOOL fLock) noexcept override
    {
        // ...
        return S_OK;
    }

    // ...
};

HRESULT __stdcall DllCanUnloadNow()
{
#ifdef _WRL_MODULE_H_
    if (!::Microsoft::WRL::Module<::Microsoft::WRL::InProc>::GetModule().Terminate())
    {
        return S_FALSE;
    }
#endif

    if (winrt::get_module_lock())
    {
        return S_FALSE;
    }

    winrt::clear_factory_cache();
    return S_OK;
}

HRESULT __stdcall DllGetClassObject(GUID const& clsid, GUID const& iid, void** result)
{
    try
    {
        *result = nullptr;

        if (clsid == __uuidof(MyCoclassFactory))
        {
            return winrt::make<MyCoclassFactory>()->QueryInterface(iid, result);
        }

#ifdef _WRL_MODULE_H_
        return ::Microsoft::WRL::Module<::Microsoft::WRL::InProc>::GetModule().GetClassObject(clsid, iid, result);
#else
        return winrt::hresult_class_not_available().to_abi();
#endif
    }
    catch (...)
    {
        return winrt::to_hresult();
    }
}
```

### <a name="support-for-weak-references"></a><span data-ttu-id="4938f-176">弱い参照のサポート</span><span class="sxs-lookup"><span data-stu-id="4938f-176">Support for weak references</span></span>

<span data-ttu-id="4938f-177">参照してください[c++ の弱い参照/cli WinRT](weak-references.md#weak-references-in-cwinrt)します。</span><span class="sxs-lookup"><span data-stu-id="4938f-177">Also see [Weak references in C++/WinRT](weak-references.md#weak-references-in-cwinrt).</span></span>

<span data-ttu-id="4938f-178">C +/cli WinRT (具体的には、 [ **winrt::implements** ](/uwp/cpp-ref-for-winrt/implements)基底構造体のテンプレート) を実装して[ **IWeakReferenceSource** ](/windows/desktop/api/weakreference/nn-weakreference-iweakreferencesource)の場合、実装の入力[ **IInspectable** ](/windows/desktop/api/inspectable/nn-inspectable-iinspectable) (または任意のインターフェイスから派生した**IInspectable**)。</span><span class="sxs-lookup"><span data-stu-id="4938f-178">C++/WinRT (specifically, the [**winrt::implements**](/uwp/cpp-ref-for-winrt/implements) base struct template) implements [**IWeakReferenceSource**](/windows/desktop/api/weakreference/nn-weakreference-iweakreferencesource) for you if your type implements [**IInspectable**](/windows/desktop/api/inspectable/nn-inspectable-iinspectable) (or any interface that derives from **IInspectable**).</span></span>

<span data-ttu-id="4938f-179">これは、ため**IWeakReferenceSource**と[ **IWeakReference** ](/windows/desktop/api/weakreference/nn-weakreference-iweakreference) Windows ランタイム型用に設計されています。</span><span class="sxs-lookup"><span data-stu-id="4938f-179">This is because **IWeakReferenceSource** and [**IWeakReference**](/windows/desktop/api/weakreference/nn-weakreference-iweakreference) are designed for Windows Runtime types.</span></span> <span data-ttu-id="4938f-180">そのため、できるサポートを有効に弱い参照、コクラスを追加するだけで**winrt::Windows::Foundation::IInspectable** (またはインターフェイスから派生した**IInspectable**) 実装にします。</span><span class="sxs-lookup"><span data-stu-id="4938f-180">So, you can turn on weak reference support for your coclass simply by adding **winrt::Windows::Foundation::IInspectable** (or an interface that derives from **IInspectable**) to your implementation.</span></span>

```cppwinrt
struct MyCoclass : winrt::implements<MyCoclass, IMyComInterface, winrt::Windows::Foundation::IInspectable>
{
    //  ...
};
```

## <a name="important-apis"></a><span data-ttu-id="4938f-181">重要な API</span><span class="sxs-lookup"><span data-stu-id="4938f-181">Important APIs</span></span>
* [<span data-ttu-id="4938f-182">IInspectable インターフェイス</span><span class="sxs-lookup"><span data-stu-id="4938f-182">IInspectable interface</span></span>](/windows/desktop/api/inspectable/nn-inspectable-iinspectable)
* [<span data-ttu-id="4938f-183">IUnknown インターフェイス</span><span class="sxs-lookup"><span data-stu-id="4938f-183">IUnknown interface</span></span>](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)
* [<span data-ttu-id="4938f-184">winrt::implements 構造体のテンプレート</span><span class="sxs-lookup"><span data-stu-id="4938f-184">winrt::implements struct template</span></span>](/uwp/cpp-ref-for-winrt/implements)

## <a name="related-topics"></a><span data-ttu-id="4938f-185">関連トピック</span><span class="sxs-lookup"><span data-stu-id="4938f-185">Related topics</span></span>
* [<span data-ttu-id="4938f-186">C++/WinRT で API を作成する</span><span class="sxs-lookup"><span data-stu-id="4938f-186">Author APIs with C++/WinRT</span></span>](/windows/uwp/cpp-and-winrt-apis/author-apis)
* [<span data-ttu-id="4938f-187">C++/WinRT での COM コンポーネントの使用</span><span class="sxs-lookup"><span data-stu-id="4938f-187">Consume COM components with C++/WinRT</span></span>](consume-com.md)
* [<span data-ttu-id="4938f-188">ローカル トースト通知の送信</span><span class="sxs-lookup"><span data-stu-id="4938f-188">Send a local toast notification</span></span>](/windows/uwp/design/shell/tiles-and-notifications/send-local-toast)
