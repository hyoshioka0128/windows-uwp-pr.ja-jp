---
Description: 拡張機能を使用すると、あらかじめ定義された方法で Windows 10 にパッケージ デスクトップ アプリを統合できます。
title: Windows 10 と UWP (デスクトップ ブリッジ) のパッケージ化されたデスクトップ アプリケーションを統合します。
ms.date: 04/18/2018
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 0a8cedac-172a-4efd-8b6b-67fd3667df34
ms.author: mcleans
author: mcleanbyron
ms.localizationpriority: medium
ms.openlocfilehash: 814d8c04943e32ff4d2f0c81bd847e78becd5ebb
ms.sourcegitcommit: a4fe508e62827a10471e2359e81e82132dc2ac5a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2019
ms.locfileid: "66468324"
---
# <a name="integrate-your-packaged-desktop-app-with-windows-10-and-uwp"></a><span data-ttu-id="870c8-104">Windows 10 と UWP パッケージ化されたデスクトップ アプリに統合します。</span><span class="sxs-lookup"><span data-stu-id="870c8-104">Integrate your packaged desktop app with Windows 10 and UWP</span></span>

<span data-ttu-id="870c8-105">場合する[MSIX コンテナーでデスクトップ アプリケーションをパッケージ化](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)、定義済みの拡張機能を使用して Windows 10 では、パッケージ化されたデスクトップ アプリケーションを統合する拡張機能を使用することができます、[アプリ パッケージ マニフェスト](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/schema-root).</span><span class="sxs-lookup"><span data-stu-id="870c8-105">If you [package your desktop application in an MSIX container](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root), you can use extensions to integrate your packaged desktop application with Windows 10 by using predefined extensions in the [app package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/schema-root).</span></span>

<span data-ttu-id="870c8-106">たとえば、拡張機能を使用して、ファイアウォールの例外を作成、ファイルの種類の既定のアプリケーション、アプリケーションを作成またはスタート タイルをポイントして、アプリのパッケージ化されたバージョン。</span><span class="sxs-lookup"><span data-stu-id="870c8-106">For example, use an extension to create a firewall exception, make your application the default application for a file type, or point start tiles to the packaged version of your app.</span></span> <span data-ttu-id="870c8-107">拡張機能は、アプリのパッケージ マニフェスト ファイルに XML を追加するだけで使用できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-107">To use an extension, just add some XML to your app's package manifest file.</span></span> <span data-ttu-id="870c8-108">コードは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="870c8-108">No code is required.</span></span>

<span data-ttu-id="870c8-109">この記事では、これらの拡張機能とそれらを使用して実行できるタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="870c8-109">This article describes these extensions and the tasks that you can perform by using them.</span></span>

> [!NOTE]
> <span data-ttu-id="870c8-110">この記事で説明されている機能では、お客様のデスクトップ アプリケーションの Windows アプリ パッケージを作成することが必要です。</span><span class="sxs-lookup"><span data-stu-id="870c8-110">The features described in this article require that you create a Windows app package for your desktop application.</span></span> <span data-ttu-id="870c8-111">これはまだ完了していない場合を参照してください。[デスクトップ アプリケーションをパッケージ化](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)します。</span><span class="sxs-lookup"><span data-stu-id="870c8-111">If you haven't yet done this, see [Package desktop applications](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root).</span></span>

## <a name="transition-users-to-your-app"></a><span data-ttu-id="870c8-112">ユーザーをアプリに移行する</span><span class="sxs-lookup"><span data-stu-id="870c8-112">Transition users to your app</span></span>

<span data-ttu-id="870c8-113">ユーザーによってパッケージ アプリが使用されるように、移行を促します。</span><span class="sxs-lookup"><span data-stu-id="870c8-113">Help users transition to your packaged app.</span></span>

* [<span data-ttu-id="870c8-114">既存のスタート タイルとタスク バー ボタンをポイントして、パッケージ アプリ</span><span class="sxs-lookup"><span data-stu-id="870c8-114">Point existing Start tiles and taskbar buttons to your packaged app</span></span>](#point)
* [<span data-ttu-id="870c8-115">デスクトップ アプリではなくファイルを開き、パッケージ化されたアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="870c8-115">Make your packaged application open files instead of your desktop app</span></span>](#make)
* [<span data-ttu-id="870c8-116">ファイルの種類のセット、パッケージ化されたアプリケーションに関連付ける</span><span class="sxs-lookup"><span data-stu-id="870c8-116">Associate your packaged application with a set of file types</span></span>](#associate)
* [<span data-ttu-id="870c8-117">特定のファイルの種類のファイルのコンテキスト メニューにオプションを追加します。</span><span class="sxs-lookup"><span data-stu-id="870c8-117">Add options to the context menus of files that have a certain file type</span></span>](#add)
* [<span data-ttu-id="870c8-118">URL を使用して直接特定の種類のファイルを開く</span><span class="sxs-lookup"><span data-stu-id="870c8-118">Open certain types of files directly by using a URL</span></span>](#open)

<a id="point" />

### <a name="point-existing-start-tiles-and-taskbar-buttons-to-your-packaged-app"></a><span data-ttu-id="870c8-119">既存のスタート タイルとタスク バー ボタンの参照先をパッケージ アプリに設定する</span><span class="sxs-lookup"><span data-stu-id="870c8-119">Point existing Start tiles and taskbar buttons to your packaged app</span></span>

<span data-ttu-id="870c8-120">ユーザーによって、デスクトップ アプリがタスク バーまたはスタート メニューにピン留めされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="870c8-120">Your users might have pinned your desktop application to the taskbar or the Start menu.</span></span> <span data-ttu-id="870c8-121">これらのショートカットの参照先を新しいパッケージ アプリに変更できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-121">You can point those shortcuts to your new packaged app.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-122">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-122">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-123">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-123">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.desktopAppMigration">
    <DesktopAppMigration>
        <DesktopApp AumId="[your_app_aumid]" />
        <DesktopApp ShortcutPath="[path]" />
    </DesktopAppMigration>
</Extension>

```

<span data-ttu-id="870c8-124">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-rescap3-desktopappmigration)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-124">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-rescap3-desktopappmigration).</span></span>

|<span data-ttu-id="870c8-125">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-125">Name</span></span> | <span data-ttu-id="870c8-126">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-126">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-127">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-127">Category</span></span> |<span data-ttu-id="870c8-128">常に ``windows.desktopAppMigration`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-128">Always ``windows.desktopAppMigration``.</span></span>
|<span data-ttu-id="870c8-129">AumID</span><span class="sxs-lookup"><span data-stu-id="870c8-129">AumID</span></span> |<span data-ttu-id="870c8-130">パッケージ アプリのアプリケーション ユーザー モデル ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-130">The Application User Model ID of your packaged app.</span></span> |
|<span data-ttu-id="870c8-131">ShortcutPath</span><span class="sxs-lookup"><span data-stu-id="870c8-131">ShortcutPath</span></span> |<span data-ttu-id="870c8-132">アプリのデスクトップ バージョンを起動する .lnk ファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="870c8-132">The path to .lnk files that start the desktop version of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-133">例</span><span class="sxs-lookup"><span data-stu-id="870c8-133">Example</span></span>

```XML
<Package
  xmlns:rescap3="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3"
  IgnorableNamespaces="rescap3">
  <Applications>
    <Application>
      <Extensions>
        <rescap3:Extension Category="windows.desktopAppMigration">
          <rescap3:DesktopAppMigration>
            <rescap3:DesktopApp AumId="[your_app_aumid]" />
            <rescap3:DesktopApp ShortcutPath="%USERPROFILE%\Desktop\[my_app].lnk" />
            <rescap3:DesktopApp ShortcutPath="%APPDATA%\Microsoft\Windows\Start Menu\Programs\[my_app].lnk" />
            <rescap3:DesktopApp ShortcutPath="%PROGRAMDATA%\Microsoft\Windows\Start Menu\Programs\[my_app_folder]\[my_app].lnk"/>
         </rescap3:DesktopAppMigration>
        </rescap3:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a><span data-ttu-id="870c8-134">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="870c8-134">Related sample</span></span>

[<span data-ttu-id="870c8-135">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="870c8-135">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="make" />

### <a name="make-your-packaged-application-open-files-instead-of-your-desktop-app"></a><span data-ttu-id="870c8-136">デスクトップ アプリではなくファイルを開き、パッケージ化されたアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="870c8-136">Make your packaged application open files instead of your desktop app</span></span>

<span data-ttu-id="870c8-137">ユーザーが特定の種類のデスクトップ バージョンのアプリを開く代わりにファイルの既定で、新しいパッケージ化されたアプリケーションを開くことを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-137">You can make sure that users open your new packaged application by default for specific types of files instead of opening the desktop version of your app.</span></span>

<span data-ttu-id="870c8-138">これを行うには、ファイルの関連付けを継承するために、関連付けされている各アプリケーションの[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) を指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-138">To do that, you'll specify the [programmatic identifier (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) of each application from which you want to inherit file associations.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-139">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-139">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-140">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-140">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
<FileTypeAssociation Name="[AppID]">
         <MigrationProgIds>
            <MigrationProgId>"[ProgID]"</MigrationProgId>
        </MigrationProgIds>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="870c8-141">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-141">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-142">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-142">Name</span></span> |<span data-ttu-id="870c8-143">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-143">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-144">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-144">Category</span></span> |<span data-ttu-id="870c8-145">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-145">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-146">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-146">Name</span></span> |<span data-ttu-id="870c8-147">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-147">A unique Id for your app.</span></span> <span data-ttu-id="870c8-148">この ID は、ファイルの種類の関連付けによって関連付けられたハッシュ対象の[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) を生成するために内部で使用されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-148">This Id is used internally to generate a hashed [programmatic identifier (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) associated with your file type association.</span></span> <span data-ttu-id="870c8-149">この ID を使って、アプリの今後のバージョンで変更を管理することができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-149">You can use this Id to manage changes in future versions of your app.</span></span> |
|<span data-ttu-id="870c8-150">MigrationProgId</span><span class="sxs-lookup"><span data-stu-id="870c8-150">MigrationProgId</span></span> |<span data-ttu-id="870c8-151">[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids)アプリケーション、コンポーネント、およびファイルの関連付けを継承するデスクトップ アプリケーションのバージョンをについて説明します。</span><span class="sxs-lookup"><span data-stu-id="870c8-151">The [programmatic identifier (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) that describes the application, component, and version of the desktop application from which you want to inherit file associations.</span></span>|

#### <a name="example"></a><span data-ttu-id="870c8-152">例</span><span class="sxs-lookup"><span data-stu-id="870c8-152">Example</span></span>

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:rescap3="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3"
  IgnorableNamespaces="uap3, rescap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <rescap3:MigrationProgIds>
              <rescap3:MigrationProgId>Foo.Bar.1</rescap3:MigrationProgId>
              <rescap3:MigrationProgId>Foo.Bar.2</rescap3:MigrationProgId>
            </rescap3:MigrationProgIds>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a><span data-ttu-id="870c8-153">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="870c8-153">Related sample</span></span>

[<span data-ttu-id="870c8-154">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="870c8-154">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="associate" />

### <a name="associate-your-packaged-application-with-a-set-of-file-types"></a><span data-ttu-id="870c8-155">ファイルの種類のセット、パッケージ化されたアプリケーションに関連付ける</span><span class="sxs-lookup"><span data-stu-id="870c8-155">Associate your packaged application with a set of file types</span></span>

<span data-ttu-id="870c8-156">パッケージ化されたアプリケーションは、ファイル拡張子に関連付けられていることができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-156">You can associated your packaged application with file type extensions.</span></span> <span data-ttu-id="870c8-157">ユーザーがファイルを右クリックし、選択した場合、**プログラムから開く**オプション、推奨事項の一覧で、アプリケーションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-157">If a user right-clicks a file and then selects the **Open with** option, your application appears in the list of suggestions.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-158">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-158">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-159">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-159">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[file extension]"</FileType>
        </SupportedFileTypes>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="870c8-160">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-160">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-161">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-161">Name</span></span> |<span data-ttu-id="870c8-162">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-162">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-163">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-163">Category</span></span> |<span data-ttu-id="870c8-164">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-164">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-165">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-165">Name</span></span> |<span data-ttu-id="870c8-166">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-166">A unique Id for your app.</span></span> <span data-ttu-id="870c8-167">この ID は、ファイルの種類の関連付けによって関連付けられたハッシュ対象の[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) を生成するために内部で使用されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-167">This Id is used internally to generate a hashed [programmatic identifier (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) associated with your file type association.</span></span> <span data-ttu-id="870c8-168">この ID を使って、アプリの今後のバージョンで変更を管理することができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-168">You can use this Id to manage changes in future versions of your app.</span></span>   |
|<span data-ttu-id="870c8-169">FileType</span><span class="sxs-lookup"><span data-stu-id="870c8-169">FileType</span></span> |<span data-ttu-id="870c8-170">アプリでサポートされているファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="870c8-170">The file extension supported by your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-171">例</span><span class="sxs-lookup"><span data-stu-id="870c8-171">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap, uap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap:SupportedFileTypes>
            <uap:FileType>.txt</uap:FileType>
            <uap:FileType>.avi</uap:FileType>
            </uap:SupportedFileTypes>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a><span data-ttu-id="870c8-172">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="870c8-172">Related sample</span></span>

[<span data-ttu-id="870c8-173">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="870c8-173">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="add" />

### <a name="add-options-to-the-context-menus-of-files-that-have-a-certain-file-type"></a><span data-ttu-id="870c8-174">特定の種類のファイルのコンテキスト メニューにオプションを追加する</span><span class="sxs-lookup"><span data-stu-id="870c8-174">Add options to the context menus of files that have a certain file type</span></span>

<span data-ttu-id="870c8-175">ほとんどの場合、ユーザーはファイルをダブルクリックして開きます。</span><span class="sxs-lookup"><span data-stu-id="870c8-175">In most cases, users double-click files to open them.</span></span> <span data-ttu-id="870c8-176">ユーザーがファイルを右クリックすると、さまざまなオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-176">If users, right click a file, various options appear.</span></span>

<span data-ttu-id="870c8-177">このメニューには、オプションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-177">You can add options to that menu.</span></span> <span data-ttu-id="870c8-178">これらのオプションを使用すると、ファイルの印刷、編集、プレビューなど、ファイルの操作を別の方法で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-178">These options give users other ways to interact with your file such as print, edit, or preview the file.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-179">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-179">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-180">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-180">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedVerbs>
           <Verb Id="[ID]" Extended="[Extended]" Parameters="[parameters]">"[verb label]"</Verb>
        </SupportedVerbs>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="870c8-181">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-181">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-182">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-182">Name</span></span> |<span data-ttu-id="870c8-183">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-183">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-184">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-184">Category</span></span> | <span data-ttu-id="870c8-185">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-185">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-186">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-186">Name</span></span> |<span data-ttu-id="870c8-187">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-187">A unique Id for your app.</span></span> |
|<span data-ttu-id="870c8-188">動詞</span><span class="sxs-lookup"><span data-stu-id="870c8-188">Verb</span></span> |<span data-ttu-id="870c8-189">エクスプローラーのコンテキスト メニューに表示される名前です。</span><span class="sxs-lookup"><span data-stu-id="870c8-189">The name that appears in the File Explorer context menu.</span></span> <span data-ttu-id="870c8-190">この文字列は、```ms-resource``` を使用してローカライズできます。</span><span class="sxs-lookup"><span data-stu-id="870c8-190">This string is localizable that uses ```ms-resource```.</span></span>|
|<span data-ttu-id="870c8-191">ID</span><span class="sxs-lookup"><span data-stu-id="870c8-191">Id</span></span> |<span data-ttu-id="870c8-192">動詞の一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-192">The unique Id of the verb.</span></span> <span data-ttu-id="870c8-193">アプリケーションが UWP アプリの場合、ユーザーの選択を適切に処理できるように、アクティブ化イベントの引数の一部としてアプリに渡されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-193">If your application is a UWP app, this is passed to your app as part of its activation event args so it can handle the user’s selection appropriately.</span></span> <span data-ttu-id="870c8-194">アプリケーションが完全に信頼されているパッケージ アプリの場合は、パラメーターを受け取った代わりに (次の箇条書きを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="870c8-194">If your application is a full-trust packaged app, it receives parameters instead (see the next bullet).</span></span> |
|<span data-ttu-id="870c8-195">パラメーター</span><span class="sxs-lookup"><span data-stu-id="870c8-195">Parameters</span></span> |<span data-ttu-id="870c8-196">動詞に関連付けられている引数のパラメーターと値のリスト。</span><span class="sxs-lookup"><span data-stu-id="870c8-196">The list of argument parameters and values associated with the verb.</span></span> <span data-ttu-id="870c8-197">アプリケーションが完全に信頼されているパッケージ アプリの場合は、これらのパラメーターは、アプリケーションがアクティブになるイベント引数としてアプリケーションに渡されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-197">If your application is a full-trust packaged app, these parameters are passed to the application as event args when the application is activated.</span></span> <span data-ttu-id="870c8-198">複数のアクティブ化の動詞に基づくアプリケーションの動作をカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-198">You can customize the behavior of your application based on different activation verbs.</span></span> <span data-ttu-id="870c8-199">変数にファイル パスが含まれる可能性がある場合は、パラメーター値を引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="870c8-199">If a variable can contain a file path, wrap the parameter value in quotes.</span></span> <span data-ttu-id="870c8-200">これにより、パスにスペースが含まれている場合に発生する問題を回避できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-200">That will avoid any issues that happen in cases where the path includes spaces.</span></span> <span data-ttu-id="870c8-201">アプリケーションが UWP アプリの場合は、パラメーターを渡すことはできません。</span><span class="sxs-lookup"><span data-stu-id="870c8-201">If your application is a UWP app, you can’t pass parameters.</span></span> <span data-ttu-id="870c8-202">アプリは、代わりに ID を受け取ります (前の項目を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="870c8-202">The app receives the Id instead (see the previous bullet).</span></span>|
|<span data-ttu-id="870c8-203">Extended</span><span class="sxs-lookup"><span data-stu-id="870c8-203">Extended</span></span> |<span data-ttu-id="870c8-204">ユーザーが **Shift** キーを押しながらファイルを右クリックすることでコンテキスト メニューを表示した場合にのみ表示される動詞を指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-204">Specifies that the verb appears only if the user shows the context menu by holding the **Shift** key before right-clicking the file.</span></span> <span data-ttu-id="870c8-205">この属性は省略可能であり、指定されていない場合の既定値は **False** (常に動詞を表示する) です。</span><span class="sxs-lookup"><span data-stu-id="870c8-205">This attribute is optional and defaults to a value of **False** (e.g., always show the verb) if not listed.</span></span> <span data-ttu-id="870c8-206">この動作は各動詞について個別に指定します ("開く" は例外で、常に **False**)。</span><span class="sxs-lookup"><span data-stu-id="870c8-206">You specify this behavior individually for each verb (except for "Open," which is always **False**).</span></span>|

#### <a name="example"></a><span data-ttu-id="870c8-207">例</span><span class="sxs-lookup"><span data-stu-id="870c8-207">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"

  IgnorableNamespaces="uap, uap2, uap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap2:SupportedVerbs>
              <uap3:Verb Id="Edit" Parameters="/e &quot;%1&quot;">Edit</uap3:Verb>
              <uap3:Verb Id="Print" Extended="true" Parameters="/p &quot;%1&quot;">Print</uap3:Verb>
            </uap2:SupportedVerbs>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a><span data-ttu-id="870c8-208">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="870c8-208">Related sample</span></span>

[<span data-ttu-id="870c8-209">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="870c8-209">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="open" />

### <a name="open-certain-types-of-files-directly-by-using-a-url"></a><span data-ttu-id="870c8-210">URL を使用して特定の種類のファイルを直接開く</span><span class="sxs-lookup"><span data-stu-id="870c8-210">Open certain types of files directly by using a URL</span></span>

<span data-ttu-id="870c8-211">ユーザーが特定の種類のデスクトップ バージョンのアプリを開く代わりにファイルの既定で、新しいパッケージ化されたアプリケーションを開くことを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-211">You can make sure that users open your new packaged application by default for specific types of files instead of opening the desktop version of your app.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-212">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-212">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* <span data-ttu-id="870c8-213">http://schemas.microsoft.com/appx/manifest/uap/windows10/3"</span><span class="sxs-lookup"><span data-stu-id="870c8-213">http://schemas.microsoft.com/appx/manifest/uap/windows10/3"</span></span>

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-214">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-214">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]" UseUrl="true" Parameters="%1">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="870c8-215">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-215">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-216">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-216">Name</span></span> |<span data-ttu-id="870c8-217">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-217">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-218">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-218">Category</span></span> |<span data-ttu-id="870c8-219">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-219">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-220">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-220">Name</span></span> |<span data-ttu-id="870c8-221">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-221">A unique Id for your app.</span></span> |
|<span data-ttu-id="870c8-222">UseUrl</span><span class="sxs-lookup"><span data-stu-id="870c8-222">UseUrl</span></span> |<span data-ttu-id="870c8-223">URL ターゲットから直接ファイルを開くかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="870c8-223">Indicates whether to open files directly from a URL target.</span></span> <span data-ttu-id="870c8-224">この値を設定しない場合は、システムを使用して URL 原因、最初のダウンロード ファイルをローカル ファイルを開くアプリケーションでしようとします。</span><span class="sxs-lookup"><span data-stu-id="870c8-224">If you do not set this value, attempts by your application to open a file by using a URL cause the system to first download the file locally.</span></span> |
|<span data-ttu-id="870c8-225">パラメーター</span><span class="sxs-lookup"><span data-stu-id="870c8-225">Parameters</span></span> |<span data-ttu-id="870c8-226">省略可能なパラメーター。</span><span class="sxs-lookup"><span data-stu-id="870c8-226">optional parameters.</span></span> |
|<span data-ttu-id="870c8-227">FileType</span><span class="sxs-lookup"><span data-stu-id="870c8-227">FileType</span></span> |<span data-ttu-id="870c8-228">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="870c8-228">The relevant file extensions.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-229">例</span><span class="sxs-lookup"><span data-stu-id="870c8-229">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap, uap3">
  <Applications>
      <Application>
        <Extensions>
          <uap:Extension Category="windows.fileTypeAssociation">
            <uap3:FileTypeAssociation Name="documenttypes" UseUrl="true" Parameters="%1">
              <uap:SupportedFileTypes>
                <uap:FileType>.txt</uap:FileType>
                <uap:FileType>.doc</uap:FileType>
              </uap:SupportedFileTypes>
            </uap3:FileTypeAssociation>
          </uap:Extension>
        </Extensions>
      </Application>
    </Applications>
</Package>
```

## <a name="perform-setup-tasks"></a><span data-ttu-id="870c8-230">セットアップ タスクを実行する</span><span class="sxs-lookup"><span data-stu-id="870c8-230">Perform setup tasks</span></span>

* [<span data-ttu-id="870c8-231">アプリがファイアウォールの例外を作成します。</span><span class="sxs-lookup"><span data-stu-id="870c8-231">Create firewall exception for your app</span></span>](#rules)
* [<span data-ttu-id="870c8-232">パッケージの任意のフォルダーに、DLL ファイルに配置します。</span><span class="sxs-lookup"><span data-stu-id="870c8-232">Place your DLL files into any folder of the package</span></span>](#load-paths)

<a id="rules" />

### <a name="create-firewall-exception-for-your-app"></a><span data-ttu-id="870c8-233">アプリのファイアウォール例外を作成する</span><span class="sxs-lookup"><span data-stu-id="870c8-233">Create firewall exception for your app</span></span>

<span data-ttu-id="870c8-234">アプリケーションは、ポート経由の通信を必要とする場合は、ファイアウォールの例外の一覧にアプリケーションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-234">If your application requires communication through a port, you can add your application to the list of firewall exceptions.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-235">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-235">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-236">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-236">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.firewallRules">
  <FirewallRules Executable="[executable file name]">
    <Rule
      Direction="[Direction]"
      IPProtocol="[Protocol]"
      LocalPortMin="[LocalPortMin]"
      LocalPortMax="LocalPortMax"
      RemotePortMin="RemotePortMin"
      RemotePortMax="RemotePortMax"
      Profile="[Profile]"/>
  </FirewallRules>
</Extension>
```

<span data-ttu-id="870c8-237">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-firewallrules)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-237">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-firewallrules).</span></span>

|<span data-ttu-id="870c8-238">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-238">Name</span></span> |<span data-ttu-id="870c8-239">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-239">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-240">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-240">Category</span></span> |<span data-ttu-id="870c8-241">いつも ``windows.firewallRules``</span><span class="sxs-lookup"><span data-stu-id="870c8-241">Always ``windows.firewallRules``</span></span>|
|<span data-ttu-id="870c8-242">実行可能ファイル</span><span class="sxs-lookup"><span data-stu-id="870c8-242">Executable</span></span> |<span data-ttu-id="870c8-243">ファイアウォールの例外の一覧に追加する実行可能ファイルの名前。</span><span class="sxs-lookup"><span data-stu-id="870c8-243">The name of the executable file that you want to add to the list of firewall exceptions</span></span> |
|<span data-ttu-id="870c8-244">Direction</span><span class="sxs-lookup"><span data-stu-id="870c8-244">Direction</span></span> |<span data-ttu-id="870c8-245">規則が受信規則か送信規則かを示します。</span><span class="sxs-lookup"><span data-stu-id="870c8-245">Indicates whether the rule is an inbound or outbound rule</span></span> |
|<span data-ttu-id="870c8-246">IPProtocol</span><span class="sxs-lookup"><span data-stu-id="870c8-246">IPProtocol</span></span> |<span data-ttu-id="870c8-247">通信プロトコル。</span><span class="sxs-lookup"><span data-stu-id="870c8-247">The communication protocol</span></span> |
|<span data-ttu-id="870c8-248">LocalPortMin</span><span class="sxs-lookup"><span data-stu-id="870c8-248">LocalPortMin</span></span> |<span data-ttu-id="870c8-249">ローカル ポート番号の範囲を示すポート番号の下限。</span><span class="sxs-lookup"><span data-stu-id="870c8-249">The lower port number in a range of local port numbers.</span></span> |
|<span data-ttu-id="870c8-250">LocalPortMax</span><span class="sxs-lookup"><span data-stu-id="870c8-250">LocalPortMax</span></span> |<span data-ttu-id="870c8-251">ローカル ポート番号の範囲を示すポート番号の上限。</span><span class="sxs-lookup"><span data-stu-id="870c8-251">The highest port number of a range of local port numbers.</span></span> |
|<span data-ttu-id="870c8-252">RemotePortMax</span><span class="sxs-lookup"><span data-stu-id="870c8-252">RemotePortMax</span></span> |<span data-ttu-id="870c8-253">リモート ポート番号の範囲を示すポート番号の下限。</span><span class="sxs-lookup"><span data-stu-id="870c8-253">The lower port number in a range of remote port numbers.</span></span> |
|<span data-ttu-id="870c8-254">RemotePortMax</span><span class="sxs-lookup"><span data-stu-id="870c8-254">RemotePortMax</span></span> |<span data-ttu-id="870c8-255">リモート ポート番号の範囲を示すポート番号の上限。</span><span class="sxs-lookup"><span data-stu-id="870c8-255">The highest port number of a range of remote port numbers.</span></span> |
|<span data-ttu-id="870c8-256">Profile</span><span class="sxs-lookup"><span data-stu-id="870c8-256">Profile</span></span> |<span data-ttu-id="870c8-257">ネットワークの種類。</span><span class="sxs-lookup"><span data-stu-id="870c8-257">The network type</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-258">例</span><span class="sxs-lookup"><span data-stu-id="870c8-258">Example</span></span>

```XML
<Package
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="desktop2">
  <Extensions>
    <desktop2:Extension Category="windows.firewallRules">
      <desktop2:FirewallRules Executable="Contoso.exe">
          <desktop2:Rule Direction="in" IPProtocol="TCP" Profile="all"/>
          <desktop2:Rule Direction="in" IPProtocol="UDP" LocalPortMin="1337" LocalPortMax="1338" Profile="domain"/>
          <desktop2:Rule Direction="in" IPProtocol="UDP" LocalPortMin="1337" LocalPortMax="1338" Profile="public"/>
          <desktop2:Rule Direction="out" IPProtocol="UDP" LocalPortMin="1339" LocalPortMax="1340" RemotePortMin="15"
                         RemotePortMax="19" Profile="domainAndPrivate"/>
          <desktop2:Rule Direction="out" IPProtocol="GRE" Profile="private"/>
      </desktop2:FirewallRules>
  </desktop2:Extension>
</Extensions>
</Package>
```

<a id="load-paths" />

### <a name="place-your-dll-files-into-any-folder-of-the-package"></a><span data-ttu-id="870c8-259">DLL ファイルをパッケージの任意のフォルダーに配置します。</span><span class="sxs-lookup"><span data-stu-id="870c8-259">Place your DLL files into any folder of the package</span></span>

<span data-ttu-id="870c8-260">拡張機能を使ってそれらのフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-260">Use an extension to identify those folders.</span></span> <span data-ttu-id="870c8-261">これにより、システムは配置したファイルを見つけて読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-261">That way, the system can find and load the files that you place in them.</span></span> <span data-ttu-id="870c8-262">この拡張機能は、 _%PATH%_ 環境変数の置き換えと考えてください。</span><span class="sxs-lookup"><span data-stu-id="870c8-262">Think of this extension as a replacement of the _%PATH%_ environment variable.</span></span>

<span data-ttu-id="870c8-263">この拡張機能を使わない場合、システムはプロセスのパッケージの依存関係グラフ、パッケージ ルート フォルダー、システム ディレクトリ ( _%SystemRoot%\system32_) の順で検索します。</span><span class="sxs-lookup"><span data-stu-id="870c8-263">If you don't use this extension, the system searches the package dependency graph of the process, the package root folder, and then the system directory (_%SystemRoot%\system32_) in that order.</span></span> <span data-ttu-id="870c8-264">詳しくは、[Windows アプリの検索順序に関するページ](https://docs.microsoft.com/windows/desktop/Dlls/dynamic-link-library-search-order)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-264">To learn more, see [Search order of Windows apps](https://docs.microsoft.com/windows/desktop/Dlls/dynamic-link-library-search-order).</span></span>

<span data-ttu-id="870c8-265">各パッケージには、これらの拡張機能を 1 つだけ含めることができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-265">Each package can contain only one of these extensions.</span></span> <span data-ttu-id="870c8-266">つまり、1 つをメイン パッケージに追加し、他の拡張機能は[オプション パッケージと関連するセット](https://docs.microsoft.com/windows/uwp/packaging/optional-packages)それぞれに 1 つずつ追加できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-266">That means that you can add one of them to your main package, and then add one to each of your [optional packages, and related sets](https://docs.microsoft.com/windows/uwp/packaging/optional-packages).</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-267">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-267">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/uap/windows10/6

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-268">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-268">Elements and attributes of this extension</span></span>

<span data-ttu-id="870c8-269">アプリケーション マニフェストのパッケージ レベルでこの拡張機能を宣言します。</span><span class="sxs-lookup"><span data-stu-id="870c8-269">Declare this extension at the package-level of your app manifest.</span></span>

```XML
<Extension Category="windows.loaderSearchPathOverride">
  <LoaderSearchPathOverride>
    <LoaderSearchPathEntry FolderPath="[path]"/>
  </LoaderSearchPathOverride>
</Extension>

```

|<span data-ttu-id="870c8-270">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-270">Name</span></span> | <span data-ttu-id="870c8-271">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-271">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-272">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-272">Category</span></span> |<span data-ttu-id="870c8-273">常に ``windows.loaderSearchPathOverride`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-273">Always ``windows.loaderSearchPathOverride``.</span></span>
|<span data-ttu-id="870c8-274">FolderPath</span><span class="sxs-lookup"><span data-stu-id="870c8-274">FolderPath</span></span> | <span data-ttu-id="870c8-275">dll ファイルが含まれているフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="870c8-275">The path of the folder that contains your dll files.</span></span> <span data-ttu-id="870c8-276">パッケージのルート フォルダーの相対パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-276">Specify a path that is relative to the root folder of the package.</span></span> <span data-ttu-id="870c8-277">1 つの拡張機能で最大 5 つのパスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-277">You can specify up to five paths in one extension.</span></span> <span data-ttu-id="870c8-278">システムがパッケージのルート フォルダーにあるファイルを検索するようにする場合、これらのパスのいずれかに空の文字列を使用します。</span><span class="sxs-lookup"><span data-stu-id="870c8-278">If you want the system to search for files in the root folder of the package, use an empty string for one of these paths.</span></span> <span data-ttu-id="870c8-279">重複するパスを含めないでください。パスの先頭と末尾にスラッシュや円記号を使わないでください。</span><span class="sxs-lookup"><span data-stu-id="870c8-279">Don't included duplicate paths and make sure that your paths don't contain leading and trailing slashes or backslashes.</span></span> <br><br> <span data-ttu-id="870c8-280">システムはサブフォルダーを検索しないため、システムが読み込む DLL ファイルが含まれている各フォルダーを明示的に一覧表示してください。</span><span class="sxs-lookup"><span data-stu-id="870c8-280">The system won't search subfolders, so make sure to explicitly list each folder that contains DLL files that you want the system to load.</span></span>|

#### <a name="example"></a><span data-ttu-id="870c8-281">例</span><span class="sxs-lookup"><span data-stu-id="870c8-281">Example</span></span>

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/6"
  IgnorableNamespaces="uap6">
  ...
    <Extensions>
      <uap6:Extension Category="windows.loaderSearchPathOverride">
        <uap6:LoaderSearchPathOverride>
          <uap6:LoaderSearchPathEntry FolderPath=""/>
          <uap6:LoaderSearchPathEntry FolderPath="folder1/subfolder1"/>
          <uap6:LoaderSearchPathEntry FolderPath="folder2/subfolder2"/>
        </uap6:LoaderSearchPathOverride>
      </uap6:Extension>
    </Extensions>
...
</Package>
```

## <a name="integrate-with-file-explorer"></a><span data-ttu-id="870c8-282">エクスプローラーに統合する</span><span class="sxs-lookup"><span data-stu-id="870c8-282">Integrate with File Explorer</span></span>

<span data-ttu-id="870c8-283">ユーザーが慣れた方法でファイルを整理し操作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="870c8-283">Help users organize your files and interact with them in familiar ways.</span></span>

* [<span data-ttu-id="870c8-284">ユーザーの選択し、同時に複数のファイルを開くときに、アプリケーションの動作を定義します。</span><span class="sxs-lookup"><span data-stu-id="870c8-284">Define how your application behaves when users select and open multiple files at the same time</span></span>](#define)
* [<span data-ttu-id="870c8-285">ファイル エクスプ ローラー内でサムネイル画像のファイルの内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="870c8-285">Show file contents in a thumbnail image within File Explorer</span></span>](#show)
* [<span data-ttu-id="870c8-286">ファイル エクスプ ローラーのプレビュー ウィンドウにファイルの内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="870c8-286">Show file contents in a Preview pane of File Explorer</span></span>](#preview)
* <span data-ttu-id="870c8-287">[ファイル エクスプ ローラーで、[種類] 列を使用して、ユーザーがファイルをグループ化を有効にします。](#enable)</span><span class="sxs-lookup"><span data-stu-id="870c8-287">[Enable users to group files by using the Kind column in File Explorer](#enable)</span></span>
* [<span data-ttu-id="870c8-288">検索、インデックス、プロパティ ダイアログ ボックス、および詳細ウィンドウにファイルのプロパティを使用できるように</span><span class="sxs-lookup"><span data-stu-id="870c8-288">Make file properties available to search, index, property dialogs, and the details pane</span></span>](#make-file-properties)
* [<span data-ttu-id="870c8-289">ファイルの種類のコンテキスト メニュー ハンドラーを指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-289">Specify a context menu handler for a file type</span></span>](#context-menu)
* [<span data-ttu-id="870c8-290">クラウド サービスからのファイルをファイル エクスプ ローラーに表示</span><span class="sxs-lookup"><span data-stu-id="870c8-290">Make files from your cloud service appear in File Explorer</span></span>](#cloud-files)

<a id="define" />

### <a name="define-how-your-application-behaves-when-users-select-and-open-multiple-files-at-the-same-time"></a><span data-ttu-id="870c8-291">ユーザーの選択し、同時に複数のファイルを開くときに、アプリケーションの動作を定義します。</span><span class="sxs-lookup"><span data-stu-id="870c8-291">Define how your application behaves when users select and open multiple files at the same time</span></span>

<span data-ttu-id="870c8-292">ユーザーが同時に複数のファイルを開いたときに、アプリケーションの動作を指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-292">Specify how your application behaves when a user opens multiple files simultaneously.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-293">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-293">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-294">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-294">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]" MultiSelectModel="[SelectionModel]">
        <SupportedVerbs>
            <Verb Id="Edit" MultiSelectModel="[SelectionModel]">Edit</Verb>
        </SupportedVerbs>
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
</Extension>
```

<span data-ttu-id="870c8-295">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-295">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-296">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-296">Name</span></span> |<span data-ttu-id="870c8-297">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-297">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-298">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-298">Category</span></span> |<span data-ttu-id="870c8-299">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-299">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-300">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-300">Name</span></span> |<span data-ttu-id="870c8-301">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-301">A unique Id for your app.</span></span> |
|<span data-ttu-id="870c8-302">MultiSelectModel</span><span class="sxs-lookup"><span data-stu-id="870c8-302">MultiSelectModel</span></span> |<span data-ttu-id="870c8-303">下を参照</span><span class="sxs-lookup"><span data-stu-id="870c8-303">See below</span></span> |
|<span data-ttu-id="870c8-304">FileType</span><span class="sxs-lookup"><span data-stu-id="870c8-304">FileType</span></span> |<span data-ttu-id="870c8-305">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="870c8-305">The relevant file extensions.</span></span> |

<span data-ttu-id="870c8-306">**MultSelectModel**</span><span class="sxs-lookup"><span data-stu-id="870c8-306">**MultSelectModel**</span></span>

<span data-ttu-id="870c8-307">パッケージ デスクトップ アプリには、通常のデスクトップ アプリと同じ 3 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="870c8-307">packaged desktop apps have the same three options as regular desktop apps.</span></span>

* <span data-ttu-id="870c8-308">``Player`` :アプリケーションは、1 回をアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-308">``Player``: Your application is activated one time.</span></span> <span data-ttu-id="870c8-309">すべての選択したファイルは、引数のパラメーターとしてアプリケーションに渡されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-309">All of the selected files are passed to your application as argument parameters.</span></span>
* <span data-ttu-id="870c8-310">``Single`` :アプリケーションは、選択した最初のファイルの 1 つの時間をアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-310">``Single``: Your application is activated one time for the first selected file.</span></span> <span data-ttu-id="870c8-311">その他のファイルは無視されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-311">Other files are ignored.</span></span>
* <span data-ttu-id="870c8-312">``Document`` :選択したファイルごとに、アプリケーションの新しい、個別のインスタンスがアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-312">``Document``: A new, separate instance of your application is activated for each selected file.</span></span>

 <span data-ttu-id="870c8-313">ファイルの種類やアクションごとに、さまざまな環境設定項目を設定できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-313">You can set different preferences for different file types and actions.</span></span> <span data-ttu-id="870c8-314">たとえば、*Documents* は *Document* モードで開き、*Images* は *Player* モードで開くことができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-314">For example, you may wish to open *Documents* in *Document* mode and *Images* in *Player* mode.</span></span>

#### <a name="example"></a><span data-ttu-id="870c8-315">例</span><span class="sxs-lookup"><span data-stu-id="870c8-315">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap, uap2, uap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="myapp" MultiSelectModel="Document">
            <uap2:SupportedVerbs>
              <uap3:Verb Id="Edit" MultiSelectModel="Player">Edit</uap3:Verb>
              <uap3:Verb Id="Preview" MultiSelectModel="Document">Preview</uap3:Verb>
            </uap2:SupportedVerbs>
            <uap:SupportedFileTypes>
              <uap:FileType>.txt</uap:FileType>
            </uap:SupportedFileTypes>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<span data-ttu-id="870c8-316">ユーザーが 15 個以下のファイルを開いた場合、**MultiSelectModel** 属性の既定値は *Player* になります。</span><span class="sxs-lookup"><span data-stu-id="870c8-316">If the user opens 15 or fewer files, the default choice for the **MultiSelectModel** attribute is *Player*.</span></span> <span data-ttu-id="870c8-317">それ以外の場合、既定値は *Document* です。</span><span class="sxs-lookup"><span data-stu-id="870c8-317">Otherwise, the default is *Document*.</span></span> <span data-ttu-id="870c8-318">UWP アプリは常に *Player* として起動されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-318">UWP apps are always started as *Player*.</span></span>

<a id="show" />

### <a name="show-file-contents-in-a-thumbnail-image-within-file-explorer"></a><span data-ttu-id="870c8-319">エクスプ ローラーでサムネイル画像のファイル内容を表示する</span><span class="sxs-lookup"><span data-stu-id="870c8-319">Show file contents in a thumbnail image within File Explorer</span></span>

<span data-ttu-id="870c8-320">ファイルが中アイコン、大アイコン、特大アイコンで表示された場合に、ファイル内容のサムネイル画像をユーザーが確認できるようにします。</span><span class="sxs-lookup"><span data-stu-id="870c8-320">Enable users to view a thumbnail image of the file's contents when the icon of the file appears in the medium, large, or extra large size.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-321">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-321">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-322">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-322">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
        <ThumbnailHandler
            Clsid  ="[Clsid  ]" />
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="870c8-323">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-323">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-324">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-324">Name</span></span> |<span data-ttu-id="870c8-325">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-325">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-326">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-326">Category</span></span> |<span data-ttu-id="870c8-327">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-327">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-328">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-328">Name</span></span> |<span data-ttu-id="870c8-329">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-329">A unique Id for your app.</span></span> |
|<span data-ttu-id="870c8-330">FileType</span><span class="sxs-lookup"><span data-stu-id="870c8-330">FileType</span></span> |<span data-ttu-id="870c8-331">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="870c8-331">The relevant file extensions.</span></span> |
|<span data-ttu-id="870c8-332">Clsid</span><span class="sxs-lookup"><span data-stu-id="870c8-332">Clsid</span></span>   |<span data-ttu-id="870c8-333">アプリのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-333">The class ID of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-334">例</span><span class="sxs-lookup"><span data-stu-id="870c8-334">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="uap, uap2, uap3, desktop2">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap2:SupportedFileTypes>
              <uap:FileType>.bar</uap:FileType>
            </uap2:SupportedFileTypes>
            <desktop2:ThumbnailHandler
              Clsid  ="20000000-0000-0000-0000-000000000001"  />
            </uap3:FileTypeAssociation>
         </uap::Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="preview" />

### <a name="show-file-contents-in-the-preview-pane-of-file-explorer"></a><span data-ttu-id="870c8-335">エクスプローラーのプレビュー ウィンドウにファイル内容を表示する</span><span class="sxs-lookup"><span data-stu-id="870c8-335">Show file contents in the Preview pane of File Explorer</span></span>

<span data-ttu-id="870c8-336">エクスプローラーのプレビュー ウィンドウで、ユーザーがファイルの内容をプレビューできるようにします。</span><span class="sxs-lookup"><span data-stu-id="870c8-336">Enable users to preview a file's contents in the Preview pane of File Explorer.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-337">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-337">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-338">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-338">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
        <DesktopPreviewHandler Clsid  ="[Clsid  ]" />
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="870c8-339">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-339">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-340">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-340">Name</span></span> |<span data-ttu-id="870c8-341">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-341">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-342">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-342">Category</span></span> |<span data-ttu-id="870c8-343">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-343">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-344">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-344">Name</span></span> |<span data-ttu-id="870c8-345">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-345">A unique Id for your app.</span></span> |
|<span data-ttu-id="870c8-346">FileType</span><span class="sxs-lookup"><span data-stu-id="870c8-346">FileType</span></span> |<span data-ttu-id="870c8-347">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="870c8-347">The relevant file extensions.</span></span> |
|<span data-ttu-id="870c8-348">Clsid</span><span class="sxs-lookup"><span data-stu-id="870c8-348">Clsid</span></span>   |<span data-ttu-id="870c8-349">アプリのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-349">The class ID of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-350">例</span><span class="sxs-lookup"><span data-stu-id="870c8-350">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="uap, uap2, uap3, desktop2">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap2SupportedFileTypes>
              <uap:FileType>.bar</uap:FileType>
                </uap2SupportedFileTypes>
              <desktop2:DesktopPreviewHandler Clsid ="20000000-0000-0000-0000-000000000001" />
           </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="enable" />

### <a name="enable-users-to-group-files-by-using-the-kind-column-in-file-explorer"></a><span data-ttu-id="870c8-351">ユーザーがエクスプローラーの [種類] 列を使用してファイルをグループ化できるようにする</span><span class="sxs-lookup"><span data-stu-id="870c8-351">Enable users to group files by using the Kind column in File Explorer</span></span>

<span data-ttu-id="870c8-352">ファイルの種類に関する 1 つまたは複数の定義済みの値を **Kind** フィールドに関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-352">You can associate one or more predefined values for your file types with the **Kind** field.</span></span>

<span data-ttu-id="870c8-353">ユーザーはエクスプローラーでこのフィールドを使用して、ファイルをグループ化できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-353">In File Explorer, users can group those files by using that field.</span></span> <span data-ttu-id="870c8-354">また、このフィールドは、システム コンポーネントによって、インデックス作成などのさまざまな目的にも使用されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-354">System components also use this field for various purposes such as indexing.</span></span>

<span data-ttu-id="870c8-355">**Kind** フィールドの詳細と、このフィールドに使用できる値については、「[種類名の使用](https://docs.microsoft.com/windows/desktop/properties/building-property-handlers-user-friendly-kind-names)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-355">For more information about the **Kind** field and the values that you can use for this field, see [Using Kind Names](https://docs.microsoft.com/windows/desktop/properties/building-property-handlers-user-friendly-kind-names).</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-356">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-356">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-357">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-357">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
        <KindMap>
            <Kind value="[KindValue]">
        </KindMap>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="870c8-358">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-358">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-359">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-359">Name</span></span> |<span data-ttu-id="870c8-360">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-360">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-361">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-361">Category</span></span> |<span data-ttu-id="870c8-362">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-362">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-363">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-363">Name</span></span> |<span data-ttu-id="870c8-364">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-364">A unique Id for your app.</span></span> |
|<span data-ttu-id="870c8-365">FileType</span><span class="sxs-lookup"><span data-stu-id="870c8-365">FileType</span></span> |<span data-ttu-id="870c8-366">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="870c8-366">The relevant file extensions.</span></span> |
|<span data-ttu-id="870c8-367">value</span><span class="sxs-lookup"><span data-stu-id="870c8-367">value</span></span> |<span data-ttu-id="870c8-368">有効な [Kind 値](https://docs.microsoft.com/windows/desktop/properties/building-property-handlers-user-friendly-kind-names)。</span><span class="sxs-lookup"><span data-stu-id="870c8-368">A valid [Kind value](https://docs.microsoft.com/windows/desktop/properties/building-property-handlers-user-friendly-kind-names)</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-369">例</span><span class="sxs-lookup"><span data-stu-id="870c8-369">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3"
  IgnorableNamespaces="uap, rescap">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
           <uap:FileTypeAssociation Name="Contoso">
             <uap:SupportedFileTypes>
               <uap:FileType>.m4a</uap:FileType>
               <uap:FileType>.mta</uap:FileType>
             </uap:SupportedFileTypes>
             <rescap:KindMap>
               <rescap:Kind value="Item">
               <rescap:Kind value="Communications">
               <rescap:Kind value="Task">
             </rescap:KindMap>
          </uap:FileTypeAssociation>
      </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="make-file-properties" />

### <a name="make-file-properties-available-to-search-index-property-dialogs-and-the-details-pane"></a><span data-ttu-id="870c8-370">ファイルのプロパティを検索、インデックス、プロパティ ダイアログ、詳細ウィンドウに利用できるようにする</span><span class="sxs-lookup"><span data-stu-id="870c8-370">Make file properties available to search, index, property dialogs, and the details pane</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-371">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-371">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-372">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-372">Elements and attributes of this extension</span></span>

```XML
<uap:Extension Category="windows.fileTypeAssociation">
    <uap:FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>.bar</FileType>
        </SupportedFileTypes>
        <DesktopPropertyHandler Clsid ="[Clsid]"/>
    </uap:FileTypeAssociation>
</uap:Extension>
```

<span data-ttu-id="870c8-373">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-373">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="870c8-374">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-374">Name</span></span> |<span data-ttu-id="870c8-375">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-375">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-376">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-376">Category</span></span> |<span data-ttu-id="870c8-377">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-377">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="870c8-378">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-378">Name</span></span> |<span data-ttu-id="870c8-379">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-379">A unique Id for your app.</span></span> |
|<span data-ttu-id="870c8-380">FileType</span><span class="sxs-lookup"><span data-stu-id="870c8-380">FileType</span></span> |<span data-ttu-id="870c8-381">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="870c8-381">The relevant file extensions.</span></span> |
|<span data-ttu-id="870c8-382">Clsid</span><span class="sxs-lookup"><span data-stu-id="870c8-382">Clsid</span></span>  |<span data-ttu-id="870c8-383">アプリのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-383">The class ID of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-384">例</span><span class="sxs-lookup"><span data-stu-id="870c8-384">Example</span></span>

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="uap, uap3, desktop2">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap:SupportedFileTypes>
              <uap:FileType>.bar</uap:FileType>
            </uap:SupportedFileTypes>
            <desktop2:DesktopPropertyHandler Clsid ="20000000-0000-0000-0000-000000000001"/>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="context-menu" />

### <a name="specify-a-context-menu-handler-for-a-file-type"></a><span data-ttu-id="870c8-385">ファイルの種類のコンテキスト メニュー ハンドラーを指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-385">Specify a context menu handler for a file type</span></span>

<span data-ttu-id="870c8-386">お客様のデスクトップ アプリケーションが定義されている場合、[コンテキスト メニュー ハンドラー](https://docs.microsoft.com/windows/desktop/shell/context-menu-handlers)、メニュー ハンドラーを登録するこの拡張機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="870c8-386">If your desktop application defines a [context menu handler](https://docs.microsoft.com/windows/desktop/shell/context-menu-handlers), use this extension to register the menu handler.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-387">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-387">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/foundation/windows10
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/4

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-388">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-388">Elements and attributes of this extension</span></span>

```XML
<Extensions>
    <com:Extension Category="windows.comServer">
        <com:ComServer>
            <com:SurrogateServer AppId="[AppID]" DisplayName="[DisplayName]">
                <com:Class Id="[Clsid]" Path="[Path]" ThreadingModel="[Model]"/>
            </com:SurrogateServer>
        </com:ComServer>
    </com:Extension>
    <desktop4:Extension Category="windows.fileExplorerContextMenus">
        <desktop4:FileExplorerContextMenus>
            <desktop4:ItemType Type="[Type]">
                <desktop4:Verb Id="[ID]" Clsid="[Clsid]" />
            </desktop4:ItemType>
        </desktop4:FileExplorerContextMenus>
    </desktop4:Extension>
</Extensions>
```

<span data-ttu-id="870c8-389">ここで、完全なスキーマの参照を検索: [com:ComServer](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-com-comserver)と[desktop4:FileExplorerContextMenus](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop4-fileexplorercontextmenus)します。</span><span class="sxs-lookup"><span data-stu-id="870c8-389">Find the complete schema reference here: [com:ComServer](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-com-comserver) and [desktop4:FileExplorerContextMenus](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop4-fileexplorercontextmenus).</span></span>

#### <a name="instructions"></a><span data-ttu-id="870c8-390">手順</span><span class="sxs-lookup"><span data-stu-id="870c8-390">Instructions</span></span>

<span data-ttu-id="870c8-391">コンテキスト メニュー ハンドラーを登録するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="870c8-391">To register your context menu handler, follow these instructions.</span></span>

1. <span data-ttu-id="870c8-392">デスクトップ アプリケーションでは、実装、[コンテキスト メニュー ハンドラー](https://docs.microsoft.com/windows/desktop/shell/context-menu-handlers)実装することによって、 [IExplorerCommand](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommand)または[IExplorerCommandState](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommandstate)インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="870c8-392">In your desktop application, implement a [context menu handler](https://docs.microsoft.com/windows/desktop/shell/context-menu-handlers) by implementing the [IExplorerCommand](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommand) or [IExplorerCommandState](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommandstate) interface.</span></span> <span data-ttu-id="870c8-393">サンプルについては、次を参照してください。、 [ExplorerCommandVerb](https://github.com/microsoft/Windows-classic-samples/tree/master/Samples/Win7Samples/winui/shell/appshellintegration/ExplorerCommandVerb)コード サンプル。</span><span class="sxs-lookup"><span data-stu-id="870c8-393">For a sample, see the [ExplorerCommandVerb](https://github.com/microsoft/Windows-classic-samples/tree/master/Samples/Win7Samples/winui/shell/appshellintegration/ExplorerCommandVerb) code sample.</span></span> <span data-ttu-id="870c8-394">実装オブジェクトのそれぞれのクラス GUID を定義することを確認します。</span><span class="sxs-lookup"><span data-stu-id="870c8-394">Make sure that you define a class GUID for each of your implementation objects.</span></span> <span data-ttu-id="870c8-395">たとえば、次のコードは実装のクラス ID を定義します。 [IExplorerCommand](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommand)します。</span><span class="sxs-lookup"><span data-stu-id="870c8-395">For example, the following code defines a class ID for an implementation of [IExplorerCommand](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommand).</span></span>

    ```cpp
    class __declspec(uuid("d0c8bceb-28eb-49ae-bc68-454ae84d6264")) CExplorerCommandVerb;
    ```

2. <span data-ttu-id="870c8-396">パッケージ マニフェストで指定、 [com:ComServer](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-com-comserver)コンテキスト メニュー ハンドラーの実装のクラス ID を持つサロゲートの COM サーバーを登録するアプリケーションの拡張機能。</span><span class="sxs-lookup"><span data-stu-id="870c8-396">In your package manifest, specify a [com:ComServer](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-com-comserver) application extension that registers a COM surrogate server with the class ID of your context menu handler implementation.</span></span>

    ```xml
    <com:Extension Category="windows.comServer">
        <com:ComServer>
            <com:SurrogateServer AppId="d0c8bceb-28eb-49ae-bc68-454ae84d6264" DisplayName="ContosoHandler">
                <com:Class Id="d0c8bceb-28eb-49ae-bc68-454ae84d6264" Path="ExplorerCommandVerb.dll" ThreadingModel="STA"/>
            </com:SurrogateServer>
        </com:ComServer>
    </com:Extension>
    ```

2. <span data-ttu-id="870c8-397">パッケージ マニフェストで指定、 [desktop4:FileExplorerContextMenus](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop4-fileexplorercontextmenus)コンテキスト メニュー ハンドラーの実装を登録するアプリケーションの拡張機能。</span><span class="sxs-lookup"><span data-stu-id="870c8-397">In your package manifest, specify a [desktop4:FileExplorerContextMenus](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop4-fileexplorercontextmenus) application extension that registers your context menu handler implementation.</span></span>

    ```xml
    <desktop4:Extension Category="windows.fileExplorerContextMenus">
        <desktop4:FileExplorerContextMenus>
            <desktop4:ItemType Type=".rar">
                <desktop4:Verb Id="Command1" Clsid="d0c8bceb-28eb-49ae-bc68-454ae84d6264" />
            </desktop4:ItemType>
        </desktop4:FileExplorerContextMenus>
    </desktop4:Extension>
    ```

#### <a name="example"></a><span data-ttu-id="870c8-398">例</span><span class="sxs-lookup"><span data-stu-id="870c8-398">Example</span></span>

```XML
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:desktop4="http://schemas.microsoft.com/appx/manifest/desktop/windows10/4"
  IgnorableNamespaces="desktop4">
  <Applications>
    <Application>
      <Extensions>
        <com:Extension Category="windows.comServer">
          <com:ComServer>
            <com:SurrogateServer AppId="d0c8bceb-28eb-49ae-bc68-454ae84d6264" DisplayName="ContosoHandler"">
              <com:Class Id="Id="d0c8bceb-28eb-49ae-bc68-454ae84d6264" Path="ExplorerCommandVerb.dll" ThreadingModel="STA"/>
            </com:SurrogateServer>
          </com:ComServer>
        </com:Extension>
        <desktop4:Extension Category="windows.fileExplorerContextMenus">
          <desktop4:FileExplorerContextMenus>
            <desktop4:ItemType Type=".contoso">
              <desktop4:Verb Id="Command1" Clsid="d0c8bceb-28eb-49ae-bc68-454ae84d6264" />
            </desktop4:ItemType>
          </desktop4:FileExplorerContextMenus>
        </desktop4:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="cloud-files" />

### <a name="make-files-from-your-cloud-service-appear-in-file-explorer"></a><span data-ttu-id="870c8-399">クラウド サービスのファイルがエクスプローラーに表示されるようにする</span><span class="sxs-lookup"><span data-stu-id="870c8-399">Make files from your cloud service appear in File Explorer</span></span>

<span data-ttu-id="870c8-400">アプリに実装するハンドラーを登録する</span><span class="sxs-lookup"><span data-stu-id="870c8-400">Register the handlers that you implement in your application.</span></span> <span data-ttu-id="870c8-401">ユーザーがエクスプローラーでクラウド ベースのファイルを右クリックしたときに表示されるコンテキスト メニュー オプションを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="870c8-401">You can also add context menu options that appear when you users right-click your cloud-based files in File Explorer.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-402">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-402">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-403">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-403">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.cloudfiles" >
    <CloudFiles IconResource="[Icon]">
        <CustomStateHandler Clsid ="[Clsid]"/>
        <ThumbnailProviderHandler Clsid ="[Clsid]"/>
        <ExtendedPropertyhandler Clsid ="[Clsid]"/>
        <CloudFilesContextMenus>
            <Verb Id ="Command3" Clsid= "[GUID]">[Verb Label]</Verb>
        </CloudFilesContextMenus>
    </CloudFiles>
</Extension>

```

|<span data-ttu-id="870c8-404">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-404">Name</span></span> |<span data-ttu-id="870c8-405">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-405">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-406">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-406">Category</span></span> |<span data-ttu-id="870c8-407">常に ``windows.cloudfiles`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-407">Always ``windows.cloudfiles``.</span></span>
|<span data-ttu-id="870c8-408">iconResource</span><span class="sxs-lookup"><span data-stu-id="870c8-408">iconResource</span></span> |<span data-ttu-id="870c8-409">クラウド ファイル プロバイダー サービスを表すアイコン。</span><span class="sxs-lookup"><span data-stu-id="870c8-409">The icon that represents your cloud file provider service.</span></span> <span data-ttu-id="870c8-410">このアイコンは、エクスプローラーのナビゲーション ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-410">This icon appears in the Navigation pane of File Explorer.</span></span>  <span data-ttu-id="870c8-411">ユーザーは、このアイコンを選んでクラウド サービスのファイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="870c8-411">Users choose this icon to show files from your cloud service.</span></span> |
|<span data-ttu-id="870c8-412">CustomStateHandler Clsid</span><span class="sxs-lookup"><span data-stu-id="870c8-412">CustomStateHandler Clsid</span></span> |<span data-ttu-id="870c8-413">CustomStateHandler を実装するアプリケーションのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-413">The class ID of the application that implements the CustomStateHandler.</span></span> <span data-ttu-id="870c8-414">システムは、このクラス ID を使ってクラウド ファイルのカスタム状態と列を要求します。</span><span class="sxs-lookup"><span data-stu-id="870c8-414">The system uses this Class ID to request custom states and columns for cloud files.</span></span> |
|<span data-ttu-id="870c8-415">ThumbnailProviderHandler Clsid</span><span class="sxs-lookup"><span data-stu-id="870c8-415">ThumbnailProviderHandler Clsid</span></span> |<span data-ttu-id="870c8-416">ThumbnailProviderHandler を実装するアプリケーションのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-416">The class ID of the application that implements the ThumbnailProviderHandler.</span></span> <span data-ttu-id="870c8-417">システムは、このクラス ID を使ってクラウド ファイルの縮小版イメージを要求します。</span><span class="sxs-lookup"><span data-stu-id="870c8-417">The system uses this Class ID to request thumbnail images for cloud files.</span></span> |
|<span data-ttu-id="870c8-418">ExtendedPropertyHandler Clsid</span><span class="sxs-lookup"><span data-stu-id="870c8-418">ExtendedPropertyHandler Clsid</span></span> |<span data-ttu-id="870c8-419">ExtendedPropertyHandler を実装するアプリケーションのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-419">The class ID of the application that implements the ExtendedPropertyHandler.</span></span>  <span data-ttu-id="870c8-420">システムは、このクラス ID を使ってクラウド ファイルの拡張プロパティを要求します。</span><span class="sxs-lookup"><span data-stu-id="870c8-420">The system uses this Class ID to request extended properties for a cloud file.</span></span> |
|<span data-ttu-id="870c8-421">動詞</span><span class="sxs-lookup"><span data-stu-id="870c8-421">Verb</span></span> |<span data-ttu-id="870c8-422">クラウド サービスによって提供されるファイルのエクスプローラー コンテキスト メニューに表示される名前です。</span><span class="sxs-lookup"><span data-stu-id="870c8-422">The name that appears in the File Explorer context menu for files provided by your cloud service.</span></span> |
|<span data-ttu-id="870c8-423">ID</span><span class="sxs-lookup"><span data-stu-id="870c8-423">Id</span></span> |<span data-ttu-id="870c8-424">動詞の一意の ID。</span><span class="sxs-lookup"><span data-stu-id="870c8-424">The unique ID of the verb.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-425">例</span><span class="sxs-lookup"><span data-stu-id="870c8-425">Example</span></span>

```XML
<Package
    xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
    IgnorableNamespaces="desktop">
  <Applications>
    <Application>
      <Extensions>
        <Extension Category="windows.cloudfiles" >
            <CloudFiles IconResource="images\Wide310x150Logo.png">
                <CustomStateHandler Clsid ="20000000-0000-0000-0000-000000000001"/>
                <ThumbnailProviderHandler Clsid ="20000000-0000-0000-0000-000000000001"/>
                <ExtendedPropertyhandler Clsid ="20000000-0000-0000-0000-000000000001"/>
                <desktop:CloudFilesContextMenus>
                    <desktop:Verb Id ="keep" Clsid=
                       "20000000-0000-0000-0000-000000000001">
                       Always keep on this device</desktop:Verb>
                </desktop:CloudFilesContextMenus>
            </CloudFiles>
          </Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="start" />

## <a name="start-your-application-in-different-ways"></a><span data-ttu-id="870c8-426">さまざまな方法でアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="870c8-426">Start your application in different ways</span></span>

* [<span data-ttu-id="870c8-427">プロトコルを使用して、アプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="870c8-427">Start your application by using a protocol</span></span>](#protocol)
* [<span data-ttu-id="870c8-428">エイリアスを使用して、アプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="870c8-428">Start your application by using an alias</span></span>](#alias)
* [<span data-ttu-id="870c8-429">ユーザーが Windows にログインすると、実行可能ファイルを開始します。</span><span class="sxs-lookup"><span data-stu-id="870c8-429">Start an executable file when users log into Windows</span></span>](#executable)
* [<span data-ttu-id="870c8-430">ユーザーが各自の PC にデバイスを接続するときのアプリケーションの起動を有効にします。</span><span class="sxs-lookup"><span data-stu-id="870c8-430">Enable users to start your application when they connect a device to their PC</span></span>](#autoplay)
* [<span data-ttu-id="870c8-431">Microsoft Store から更新プログラムを受信した後に自動的に再起動します。</span><span class="sxs-lookup"><span data-stu-id="870c8-431">Restart automatically after receiving an update from the Microsoft Store</span></span>](#updates)

<a id="protocol" />

### <a name="start-your-application-by-using-a-protocol"></a><span data-ttu-id="870c8-432">プロトコルを使用して、アプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="870c8-432">Start your application by using a protocol</span></span>

<span data-ttu-id="870c8-433">プロトコルの関連付けによって、他のプログラムやシステム コンポーネントがパッケージ アプリと相互運用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="870c8-433">Protocol associations can enable other programs and system components to interoperate with your packaged app.</span></span> <span data-ttu-id="870c8-434">プロトコルを使用して、パッケージ化されたアプリケーションが開始されると、それに従って動作できるように、アクティブ化イベントの引数を渡す特定のパラメーターを指定できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-434">When your packaged application is started by using a protocol, you can specify specific parameters to pass to its activation event arguments so it can behave accordingly.</span></span> <span data-ttu-id="870c8-435">パラメーターは、完全に信頼できるパッケージ アプリでのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="870c8-435">Parameters are supported only for packaged, full-trust apps.</span></span> <span data-ttu-id="870c8-436">UWP アプリでは、パラメーターを使用できません。</span><span class="sxs-lookup"><span data-stu-id="870c8-436">UWP apps can't use parameters.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-437">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-437">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-438">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-438">Elements and attributes of this extension</span></span>

```XML
<Extension
    Category="windows.protocol">
  <Protocol
      Name="[Protocol name]"
      Parameters="[Parameters]" />
</Extension>
```

<span data-ttu-id="870c8-439">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-protocol)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-439">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-protocol).</span></span>

|<span data-ttu-id="870c8-440">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-440">Name</span></span> |<span data-ttu-id="870c8-441">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-441">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-442">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-442">Category</span></span> |<span data-ttu-id="870c8-443">常に ``windows.protocol`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-443">Always ``windows.protocol``.</span></span>
|<span data-ttu-id="870c8-444">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-444">Name</span></span> |<span data-ttu-id="870c8-445">プロトコルの名前。</span><span class="sxs-lookup"><span data-stu-id="870c8-445">The name of the protocol.</span></span> |
|<span data-ttu-id="870c8-446">パラメーター</span><span class="sxs-lookup"><span data-stu-id="870c8-446">Parameters</span></span> |<span data-ttu-id="870c8-447">パラメーターと、アプリケーションがアクティブになるイベントの引数として、アプリケーションに渡す値の一覧。</span><span class="sxs-lookup"><span data-stu-id="870c8-447">The list of parameters and values to pass to your application as event arguments when the application is activated.</span></span> <span data-ttu-id="870c8-448">変数にファイル パスが含まれる可能性がある場合は、パラメーター値を引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="870c8-448">If a variable can contain a file path, wrap the parameter value in quotes.</span></span> <span data-ttu-id="870c8-449">これにより、パスにスペースが含まれている場合に発生する問題を回避できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-449">That will avoid any issues that happen in cases where the path includes spaces.</span></span> |

### <a name="example"></a><span data-ttu-id="870c8-450">例</span><span class="sxs-lookup"><span data-stu-id="870c8-450">Example</span></span>

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap3">
  <Applications>
    <Application>
      <Extensions>
         <uap3:Extension
                Category="windows.appExecutionAlias"
                Executable="exes\launcher.exe"
                EntryPoint="Windows.FullTrustApplication">
            <uap3:AppExecutionAlias>
                <desktop:ExecutionAlias Alias="Contoso.exe" />
            </uap3:AppExecutionAlias>
        </uap3:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="alias" />

### <a name="start-your-application-by-using-an-alias"></a><span data-ttu-id="870c8-451">エイリアスを使用して、アプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="870c8-451">Start your application by using an alias</span></span>

<span data-ttu-id="870c8-452">ユーザーおよびその他のプロセスは、アプリへの完全パスを指定するのにことがなく、アプリケーションを開始するのにエイリアスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-452">Users and other processes can use an alias to start your application without having to specify the full path to your app.</span></span> <span data-ttu-id="870c8-453">そのエイリアス名を指定できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-453">You can specify that alias name.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-454">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-454">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-455">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-455">Elements and attributes of this extension</span></span>

```XML
<Extension
    Category="windows.appExecutionAlias"
    Executable="[ExecutableName]"
    EntryPoint="Windows.FullTrustApplication">
    <AppExecutionAlias>
        <desktop:ExecutionAlias Alias="[AliasName]" />
    </AppExecutionAlias>
</Extension>
```

|<span data-ttu-id="870c8-456">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-456">Name</span></span> |<span data-ttu-id="870c8-457">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-457">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-458">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-458">Category</span></span> |<span data-ttu-id="870c8-459">常に ``windows.appExecutionAlias`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-459">Always ``windows.appExecutionAlias``.</span></span>
|<span data-ttu-id="870c8-460">実行可能ファイル</span><span class="sxs-lookup"><span data-stu-id="870c8-460">Executable</span></span> |<span data-ttu-id="870c8-461">エイリアスが呼び出されたときに起動する実行可能ファイルの相対パス。</span><span class="sxs-lookup"><span data-stu-id="870c8-461">The relative path to the executable to start when the alias is invoked.</span></span> |
|<span data-ttu-id="870c8-462">Alias</span><span class="sxs-lookup"><span data-stu-id="870c8-462">Alias</span></span> |<span data-ttu-id="870c8-463">アプリの短い名前。</span><span class="sxs-lookup"><span data-stu-id="870c8-463">The short name for your app.</span></span> <span data-ttu-id="870c8-464">常に、拡張子 ".exe" で終わっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="870c8-464">It must always end with the ".exe" extension.</span></span> <span data-ttu-id="870c8-465">パッケージ内のアプリケーションごとにアプリの実行エイリアスは 1 つだけ指定できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-465">You can only specify a single app execution alias for each application in the package.</span></span> <span data-ttu-id="870c8-466">複数のアプリで同じエイリアスが登録されている場合、システムは最後に登録されたアプリを呼び出します。したがって、他のアプリが上書きする可能性が低い一意のエイリアスを選んでください。</span><span class="sxs-lookup"><span data-stu-id="870c8-466">If multiple apps register for the same alias, the system will invoke the last one that was registered, so make sure to choose a unique alias other apps are unlikely to override.</span></span>
|

#### <a name="example"></a><span data-ttu-id="870c8-467">例</span><span class="sxs-lookup"><span data-stu-id="870c8-467">Example</span></span>

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
  IgnorableNamespaces="uap3, desktop">
  <Applications>
    <Application>
      <Extensions>
        <uap3:Extension
          Category="windows.protocol">
          <uap3:Protocol
            Name="myapp-cmd"
            Parameters="/p &quot;%1&quot;" />
        </uap3:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
 
...
</Package>
```

<span data-ttu-id="870c8-468">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-468">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

<a id="executable" />

### <a name="start-an-executable-file-when-users-log-into-windows"></a><span data-ttu-id="870c8-469">ユーザーが Windows にログオンしたときに実行可能ファイルを起動する</span><span class="sxs-lookup"><span data-stu-id="870c8-469">Start an executable file when users log into Windows</span></span>

<span data-ttu-id="870c8-470">スタートアップ タスクでは、ユーザーがログオンするたびに自動的に実行可能ファイルを実行するアプリケーションを許可します。</span><span class="sxs-lookup"><span data-stu-id="870c8-470">Startup tasks allow your application to run an executable automatically whenever a user logs on.</span></span>

> [!NOTE]
> <span data-ttu-id="870c8-471">ユーザーは、このスタートアップ タスクを登録するには少なくとも 1 回のアプリケーションの起動を持ちます。</span><span class="sxs-lookup"><span data-stu-id="870c8-471">The user has to start your application at least one time to register this startup task.</span></span>

<span data-ttu-id="870c8-472">アプリケーションでは、複数のスタートアップ タスクを宣言できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-472">Your application can declare multiple startup tasks.</span></span> <span data-ttu-id="870c8-473">各タスクは独立して起動されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-473">Each task starts independently.</span></span> <span data-ttu-id="870c8-474">すべてのスタートアップ タスクは、タスク マネージャーの **[スタートアップ]** タブに、アプリのマニフェストで指定した名前とアプリのアイコンを使って表示されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-474">All startup tasks will appear in Task Manager under the **Startup** tab with the name that you specify in your app's manifest and your app's icon.</span></span> <span data-ttu-id="870c8-475">タスク マネージャーによって、タスクの起動への影響が自動的に分析されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-475">Task Manager will automatically analyze the startup impact of your tasks.</span></span>

<span data-ttu-id="870c8-476">ユーザーは、タスク マネージャーを使用して、アプリのスタートアップ タスクを手動で無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-476">Users can manually disable your app's startup task by using Task Manager.</span></span> <span data-ttu-id="870c8-477">ユーザーがタスクを無効にした場合、プログラムでタスクを再度有効にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="870c8-477">If a user disables a task, you can't programmatically re-enable it.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-478">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-478">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-479">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-479">Elements and attributes of this extension</span></span>

```XML
<Extension
    Category="windows.startupTask"
    Executable="[ExecutableName]"
    EntryPoint="Windows.FullTrustApplication">
  <StartupTask
      TaskId="[TaskID]"
      Enabled="true"
      DisplayName="[DisplayName]" />
</Extension>
```

|<span data-ttu-id="870c8-480">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-480">Name</span></span> |<span data-ttu-id="870c8-481">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-481">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-482">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-482">Category</span></span> |<span data-ttu-id="870c8-483">常に ``windows.startupTask`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-483">Always ``windows.startupTask``.</span></span>|
|<span data-ttu-id="870c8-484">実行可能ファイル</span><span class="sxs-lookup"><span data-stu-id="870c8-484">Executable</span></span> |<span data-ttu-id="870c8-485">起動する実行可能ファイルへの相対パス。</span><span class="sxs-lookup"><span data-stu-id="870c8-485">The relative path to the executable file to start.</span></span> |
|<span data-ttu-id="870c8-486">TaskId</span><span class="sxs-lookup"><span data-stu-id="870c8-486">TaskId</span></span> |<span data-ttu-id="870c8-487">タスクの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="870c8-487">A unique identifier for your task.</span></span> <span data-ttu-id="870c8-488">この識別子を使用して、アプリケーション Api を呼び出すこと、 [Windows.ApplicationModel.StartupTask](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.StartupTask)クラスをプログラムで有効または、スタートアップ タスクを無効にします。</span><span class="sxs-lookup"><span data-stu-id="870c8-488">Using this identifier, your application can call the APIs in the [Windows.ApplicationModel.StartupTask](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.StartupTask) class to programmatically enable or disable a startup task.</span></span> |
|<span data-ttu-id="870c8-489">有効</span><span class="sxs-lookup"><span data-stu-id="870c8-489">Enabled</span></span> |<span data-ttu-id="870c8-490">初めて起動したタスクを有効にするか、無効にするかを指定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-490">Indicates whether the task first starts enabled or disabled.</span></span> <span data-ttu-id="870c8-491">有効になっているタスクは、(ユーザーが無効にしていない限り) 次回ユーザーがログオンするときに実行されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-491">Enabled tasks will run the next time the user logs on (unless the user disables it).</span></span> |
|<span data-ttu-id="870c8-492">DisplayName</span><span class="sxs-lookup"><span data-stu-id="870c8-492">DisplayName</span></span> |<span data-ttu-id="870c8-493">タスク マネージャーに表示されるタスクの名前。</span><span class="sxs-lookup"><span data-stu-id="870c8-493">The name of the task that appears in Task Manager.</span></span> <span data-ttu-id="870c8-494">この文字列は、```ms-resource``` を使用してローカライズできます。</span><span class="sxs-lookup"><span data-stu-id="870c8-494">You can localize this string by using ```ms-resource```.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-495">例</span><span class="sxs-lookup"><span data-stu-id="870c8-495">Example</span></span>

```XML
<Package
  xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
  IgnorableNamespaces="desktop">
  <Applications>
    <Application>
      <Extensions>
        <desktop:Extension
          Category="windows.startupTask"
          Executable="bin\MyStartupTask.exe"
          EntryPoint="Windows.FullTrustApplication">
        <desktop:StartupTask
          TaskId="MyStartupTask"
          Enabled="true"
          DisplayName="My App Service" />
        </desktop:Extension>
      </Extensions>
    </Application>
  </Applications>
 </Package>
```

<a id="autoplay" />

### <a name="enable-users-to-start-your-application-when-they-connect-a-device-to-their-pc"></a><span data-ttu-id="870c8-496">ユーザーが各自の PC にデバイスを接続するときのアプリケーションの起動を有効にします。</span><span class="sxs-lookup"><span data-stu-id="870c8-496">Enable users to start your application when they connect a device to their PC</span></span>

<span data-ttu-id="870c8-497">自動再生は、ユーザーが各自の PC にデバイスを接続するときに、オプションとして、アプリケーションを表示できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-497">AutoPlay can present your application as an option when a user connects a device to their PC.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="870c8-498">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-498">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-499">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-499">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.autoPlayHandler">
  <AutoPlayHandler>
    <InvokeAction ActionDisplayName="[action string]" ProviderDisplayName="[name of your app/service]">
      <Content ContentEvent="[Content event]" Verb="[any string]" DropTargetHandler="[Clsid]" />
      <Content ContentEvent="[Content event]" Verb="[any string]" Parameters="[Initialization parameter]"/>
      <Device DeviceEvent="[Device event]" HWEventHandler="[Clsid]" InitCmdLine="[Initialization parameter]"/>
    </InvokeAction>
  </AutoPlayHandler>
```

|<span data-ttu-id="870c8-500">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-500">Name</span></span> |<span data-ttu-id="870c8-501">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-501">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-502">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-502">Category</span></span> |<span data-ttu-id="870c8-503">常に ``windows.autoPlayHandler`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-503">Always ``windows.autoPlayHandler``.</span></span>
|<span data-ttu-id="870c8-504">ActionDisplayName</span><span class="sxs-lookup"><span data-stu-id="870c8-504">ActionDisplayName</span></span> |<span data-ttu-id="870c8-505">ユーザーが PC に接続するデバイスで実行できるアクションを表す文字列です (例。「ファイルのインポート」または「ビデオを再生」)。</span><span class="sxs-lookup"><span data-stu-id="870c8-505">A string that represents the action that users can take with a device that they connect to a PC (For example: "Import files", or "Play video").</span></span> |
|<span data-ttu-id="870c8-506">ProviderDisplayName</span><span class="sxs-lookup"><span data-stu-id="870c8-506">ProviderDisplayName</span></span> | <span data-ttu-id="870c8-507">アプリケーションまたはサービスを表す文字列です (例。「Contoso ビデオ プレーヤー」)。</span><span class="sxs-lookup"><span data-stu-id="870c8-507">A string that represents your application or service (For example: "Contoso video player").</span></span> |
|<span data-ttu-id="870c8-508">ContentEvent</span><span class="sxs-lookup"><span data-stu-id="870c8-508">ContentEvent</span></span> |<span data-ttu-id="870c8-509">ユーザーに ``ActionDisplayName`` と ``ProviderDisplayName`` をプロンプト表示する原因となるコンテンツ イベントの名前。</span><span class="sxs-lookup"><span data-stu-id="870c8-509">The name of a content event that causes users to be prompted with your ``ActionDisplayName`` and ``ProviderDisplayName``.</span></span> <span data-ttu-id="870c8-510">コンテンツ イベントは、カメラのメモリ カード、サム ドライブ、DVD などのボリューム デバイスが PC に挿入されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="870c8-510">A content event is raised when a volume device such as a camera memory card, thumb drive, or DVD is inserted into the PC.</span></span> <span data-ttu-id="870c8-511">これらのイベントの詳しい一覧については、[ここ](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-511">You can find the full list of those events [here](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference).</span></span>  |
|<span data-ttu-id="870c8-512">動詞</span><span class="sxs-lookup"><span data-stu-id="870c8-512">Verb</span></span> |<span data-ttu-id="870c8-513">動詞の設定は、選択したオプションのアプリケーションに渡される値を識別します。</span><span class="sxs-lookup"><span data-stu-id="870c8-513">The Verb setting identifies a value that is passed to your application for the selected option.</span></span> <span data-ttu-id="870c8-514">自動再生のイベントの起動アクションは複数指定できます。また、[動詞] 設定を使って、ユーザーがアプリで選んだアクションを確認できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-514">You can specify multiple launch actions for an AutoPlay event and use the Verb setting to determine which option a user has selected for your app.</span></span> <span data-ttu-id="870c8-515">アプリに渡される起動イベント引数の verb プロパティを調べることでユーザーが選んだオプションを確認できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-515">You can tell which option the user selected by checking the verb property of the startup event arguments passed to your app.</span></span> <span data-ttu-id="870c8-516">[動詞] 設定には任意の値を使うことができます。ただし、予約されている open を除きます。</span><span class="sxs-lookup"><span data-stu-id="870c8-516">You can use any value for the Verb setting except, open, which is reserved.</span></span> |
|<span data-ttu-id="870c8-517">DropTargetHandler</span><span class="sxs-lookup"><span data-stu-id="870c8-517">DropTargetHandler</span></span> |<span data-ttu-id="870c8-518">実装するアプリケーションのクラス ID、 [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017)インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="870c8-518">The class ID of the application that implements the [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) interface.</span></span> <span data-ttu-id="870c8-519">リムーバブル メディアのファイルは、[IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) 実装の [Drop](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget.drop?view=visualstudiosdk-2017#Microsoft_VisualStudio_OLE_Interop_IDropTarget_Drop_Microsoft_VisualStudio_OLE_Interop_IDataObject_System_UInt32_Microsoft_VisualStudio_OLE_Interop_POINTL_System_UInt32__) メソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="870c8-519">Files from the removable media are passed to the [Drop](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget.drop?view=visualstudiosdk-2017#Microsoft_VisualStudio_OLE_Interop_IDropTarget_Drop_Microsoft_VisualStudio_OLE_Interop_IDataObject_System_UInt32_Microsoft_VisualStudio_OLE_Interop_POINTL_System_UInt32__) method of your [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) implementation.</span></span>  |
|<span data-ttu-id="870c8-520">パラメーター</span><span class="sxs-lookup"><span data-stu-id="870c8-520">Parameters</span></span> |<span data-ttu-id="870c8-521">すべてのコンテンツ イベントで [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) インターフェイスを実装する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="870c8-521">You don't have to implement the [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) interface for all content events.</span></span> <span data-ttu-id="870c8-522">どのコンテンツ イベントにも、[IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) インターフェイスを実装する代わりにコマンド ライン パラメーターを指定することができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-522">For any of the content events, you could provide command line parameters instead of implementing the [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) interface.</span></span> <span data-ttu-id="870c8-523">これらのイベントでは、自動再生がこれらのコマンド ライン パラメーターを使用してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="870c8-523">For those events, AutoPlay will start your application by using those command line parameters.</span></span> <span data-ttu-id="870c8-524">アプリの初期化コードでそれらのパラメーターを解析して、自動再生によって起動したかどうかを判断し、カスタム実装を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-524">You can parse those parameters in your app's initialization code to determine if it was started by AutoPlay and then provide your custom implementation.</span></span> |
|<span data-ttu-id="870c8-525">DeviceEvent</span><span class="sxs-lookup"><span data-stu-id="870c8-525">DeviceEvent</span></span> |<span data-ttu-id="870c8-526">ユーザーに ``ActionDisplayName`` と ``ProviderDisplayName`` をプロンプト表示する原因となるデバイス イベントの名前。</span><span class="sxs-lookup"><span data-stu-id="870c8-526">The name of a device event that causes users to be prompted with your ``ActionDisplayName`` and ``ProviderDisplayName``.</span></span> <span data-ttu-id="870c8-527">デバイス イベントは、デバイスが PC に接続されると発生します。</span><span class="sxs-lookup"><span data-stu-id="870c8-527">A device event is raised when a device is connected to the PC.</span></span> <span data-ttu-id="870c8-528">デバイス イベントの先頭は文字列 ``WPD`` です。一覧については[ここ](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-528">Device events begin with the string ``WPD`` and you can find them listed [here](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference).</span></span> |
|<span data-ttu-id="870c8-529">HWEventHandler</span><span class="sxs-lookup"><span data-stu-id="870c8-529">HWEventHandler</span></span> |<span data-ttu-id="870c8-530">実装するアプリケーションのクラス ID、 [IHWEventHandler](https://docs.microsoft.com/windows/desktop/api/shobjidl/nn-shobjidl-ihweventhandler)インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="870c8-530">The Class ID of the application that implements the [IHWEventHandler](https://docs.microsoft.com/windows/desktop/api/shobjidl/nn-shobjidl-ihweventhandler) interface.</span></span> |
|<span data-ttu-id="870c8-531">InitCmdLine</span><span class="sxs-lookup"><span data-stu-id="870c8-531">InitCmdLine</span></span> |<span data-ttu-id="870c8-532">[IHWEventHandler](https://docs.microsoft.com/windows/desktop/api/shobjidl/nn-shobjidl-ihweventhandler) インターフェイスの [Initialize](https://docs.microsoft.com/windows/desktop/api/shobjidl/nf-shobjidl-ihweventhandler-initialize) メソッドに渡す文字列パラメーター。</span><span class="sxs-lookup"><span data-stu-id="870c8-532">The string parameter that you want to pass into the [Initialize](https://docs.microsoft.com/windows/desktop/api/shobjidl/nf-shobjidl-ihweventhandler-initialize) method of the [IHWEventHandler](https://docs.microsoft.com/windows/desktop/api/shobjidl/nn-shobjidl-ihweventhandler) interface.</span></span> |

### <a name="example"></a><span data-ttu-id="870c8-533">例</span><span class="sxs-lookup"><span data-stu-id="870c8-533">Example</span></span>

```XML
<Package
  xmlns:desktop3="http://schemas.microsoft.com/appx/manifest/desktop/windows10/3"
  IgnorableNamespaces="desktop3">
  <Applications>
    <Application>
      <Extensions>
        <desktop3:Extension Category="windows.autoPlayHandler">
          <desktop3:AutoPlayHandler>
            <desktop3:InvokeAction ActionDisplayName="Import my files" ProviderDisplayName="ms-resource:AutoPlayDisplayName">
              <desktop3:Content ContentEvent="ShowPicturesOnArrival" Verb="show" DropTargetHandler="CD041BAE-0DEA-4472-9B7B-C98043D26EA8"/>
              <desktop3:Content ContentEvent="PlayVideoFilesOnArrival" Verb="play" Parameters="%1" />
              <desktop3:Device DeviceEvent="WPD\ImageSource" HWEventHandler="CD041BAE-0DEA-4472-9B7B-C98043D26EA8" InitCmdLine="/autoplay"/>
            </desktop3:InvokeAction>
          </desktop3:AutoPlayHandler>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="updates" />

### <a name="restart-automatically-after-receiving-an-update-from-the-microsoft-store"></a><span data-ttu-id="870c8-534">Microsoft Store から更新プログラムを受信した後、自動的に再起動する</span><span class="sxs-lookup"><span data-stu-id="870c8-534">Restart automatically after receiving an update from the Microsoft Store</span></span>

<span data-ttu-id="870c8-535">ユーザーに更新プログラムをインストールするときに、アプリケーションが開いている場合、アプリケーションを閉じます。</span><span class="sxs-lookup"><span data-stu-id="870c8-535">If your application is open when users install an update to it, the application closes.</span></span>

<span data-ttu-id="870c8-536">そのアプリケーションの場合、更新された後で再起動が完了すると、呼び出し、 [RegisterApplicationRestart](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-registerapplicationrestart)を再起動するすべてのプロセス内の関数。</span><span class="sxs-lookup"><span data-stu-id="870c8-536">If you want that application to restart after the update completes, call the  [RegisterApplicationRestart](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-registerapplicationrestart) function in every process that you want to restart.</span></span>

<span data-ttu-id="870c8-537">各アクティブなウィンドウ、アプリケーションでの受信、 [WM_QUERYENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-queryendsession)メッセージ。</span><span class="sxs-lookup"><span data-stu-id="870c8-537">Each active window in your application receives a [WM_QUERYENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-queryendsession) message.</span></span> <span data-ttu-id="870c8-538">この時点で、アプリケーションを呼び出すことができます、 [RegisterApplicationRestart](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-registerapplicationrestart)必要な場合は、コマンドラインを更新するには、もう一度関数。</span><span class="sxs-lookup"><span data-stu-id="870c8-538">At this point, your application can call the [RegisterApplicationRestart](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-registerapplicationrestart) function again to update the command line if necessary.</span></span>

<span data-ttu-id="870c8-539">アプリケーション内のアクティブな各ウィンドウが受信すると、 [WM_ENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-endsession)メッセージ、アプリケーションがデータを保存およびシャット ダウンします。</span><span class="sxs-lookup"><span data-stu-id="870c8-539">When each active window in your application receives the [WM_ENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-endsession) message, your application should save data and shut down.</span></span>

>[!NOTE]
<span data-ttu-id="870c8-540">また、アクティブなウィンドウが表示される、 [WM_CLOSE](https://docs.microsoft.com/windows/desktop/winmsg/wm-close)メッセージ、アプリケーションが処理しない場合、 [WM_ENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-endsession)メッセージ。</span><span class="sxs-lookup"><span data-stu-id="870c8-540">Your active windows also receive the [WM_CLOSE](https://docs.microsoft.com/windows/desktop/winmsg/wm-close) message in case the application doesn't handle the [WM_ENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-endsession) message.</span></span>

<span data-ttu-id="870c8-541">この時点で、アプリケーションが、独自のプロセスを終了する 30 秒を持っているか、プラットフォームは、これらを強制的に終了します。</span><span class="sxs-lookup"><span data-stu-id="870c8-541">At this point, your application has 30 seconds to close it's own processes or the platform terminates them forcefully.</span></span>

<span data-ttu-id="870c8-542">更新プログラムが完了した後、アプリケーションを再起動します。</span><span class="sxs-lookup"><span data-stu-id="870c8-542">After the update is complete, your application restarts.</span></span>

## <a name="work-with-other-applications"></a><span data-ttu-id="870c8-543">他のアプリケーションと連携する</span><span class="sxs-lookup"><span data-stu-id="870c8-543">Work with other applications</span></span>

<span data-ttu-id="870c8-544">他のアプリとの統合、他のプロセスの開始、情報の共有が可能です。</span><span class="sxs-lookup"><span data-stu-id="870c8-544">Integrate with other apps, start other processes or share information.</span></span>

* [<span data-ttu-id="870c8-545">印刷をサポートするアプリケーションで印刷のターゲットとして表示される、アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="870c8-545">Make your application appear as the print target in applications that support printing</span></span>](#printing)
* [<span data-ttu-id="870c8-546">その他の Windows アプリケーションでのフォントの共有</span><span class="sxs-lookup"><span data-stu-id="870c8-546">Share fonts with other Windows applications</span></span>](#fonts)
* [<span data-ttu-id="870c8-547">ユニバーサル Windows プラットフォーム (UWP) アプリからの Win32 プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="870c8-547">Start a Win32 process from a Universal Windows Platform (UWP) app</span></span>](#win32-process)

<a id="printing" />

### <a name="make-your-application-appear-as-the-print-target-in-applications-that-support-printing"></a><span data-ttu-id="870c8-548">印刷をサポートするアプリケーションで印刷のターゲットとして表示される、アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="870c8-548">Make your application appear as the print target in applications that support printing</span></span>

<span data-ttu-id="870c8-549">ユーザーは、メモ帳などの別のアプリケーションからデータを印刷する場合、アプリケーションの利用可能な印刷ターゲット アプリの一覧で印刷のターゲットとして表示を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="870c8-549">When users want to print data from another application such as Notepad, you can make your application appear as a print target in the app's list of available print targets.</span></span>

<span data-ttu-id="870c8-550">XML Paper Specification (XPS) 形式で印刷データを受信するようにアプリケーションを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="870c8-550">You'll have to modify your application so that it receives print data in XML Paper Specification (XPS) format.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-551">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-551">XML namespaces</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-552">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-552">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.appPrinter">
    <AppPrinter
        DisplayName="[DisplayName]"
        Parameters="[Parameters]" />
</Extension>
```

<span data-ttu-id="870c8-553">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-appprinter)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-553">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-appprinter).</span></span>

|<span data-ttu-id="870c8-554">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-554">Name</span></span> |<span data-ttu-id="870c8-555">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-555">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-556">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-556">Category</span></span> |<span data-ttu-id="870c8-557">常に ``windows.appPrinter`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-557">Always ``windows.appPrinter``.</span></span>
|<span data-ttu-id="870c8-558">DisplayName</span><span class="sxs-lookup"><span data-stu-id="870c8-558">DisplayName</span></span> |<span data-ttu-id="870c8-559">アプリの印刷先一覧に表示する名前。</span><span class="sxs-lookup"><span data-stu-id="870c8-559">The name that you want to appear in the list of print targets for an app.</span></span> |
|<span data-ttu-id="870c8-560">パラメーター</span><span class="sxs-lookup"><span data-stu-id="870c8-560">Parameters</span></span> |<span data-ttu-id="870c8-561">アプリケーションに要求を正しく処理するために必要な任意のパラメーター。</span><span class="sxs-lookup"><span data-stu-id="870c8-561">Any parameters that your application requires to properly handle the request.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-562">例</span><span class="sxs-lookup"><span data-stu-id="870c8-562">Example</span></span>

```XML
<Package
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="desktop2">
  <Applications>
  <Application>
    <Extensions>
      <desktop2:Extension Category="windows.appPrinter">
        <desktop2:AppPrinter
          DisplayName="Send to Contoso"
          Parameters="/insertdoc %1" />
      </desktop2:Extension>
    </Extensions>
  </Application>
</Applications>
</Package>
```

<span data-ttu-id="870c8-563">この拡張機能を使用するサンプルについては、[こちら](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/PrintToPDF)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-563">Find a sample that uses this extension [Here](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/PrintToPDF)</span></span>

<a id="fonts" />

### <a name="share-fonts-with-other-windows-applications"></a><span data-ttu-id="870c8-564">他の Windows アプリケーションとフォントを共有する</span><span class="sxs-lookup"><span data-stu-id="870c8-564">Share fonts with other Windows applications</span></span>

<span data-ttu-id="870c8-565">他の Windows アプリケーションとカスタム フォントを共有できます。</span><span class="sxs-lookup"><span data-stu-id="870c8-565">Share your custom fonts with other Windows applications.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-566">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-566">XML namespaces</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-567">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-567">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.sharedFonts">
    <SharedFonts>
      <Font File="[FontFile]" />
    </SharedFonts>
  </Extension>
```

<span data-ttu-id="870c8-568">完全なスキーマ リファレンスについては、[こちら](/uwp/schemas/appxpackage/uapmanifestschema/element-uap4-sharedfonts)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-568">Find the complete schema reference [here](/uwp/schemas/appxpackage/uapmanifestschema/element-uap4-sharedfonts).</span></span>

|<span data-ttu-id="870c8-569">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-569">Name</span></span> |<span data-ttu-id="870c8-570">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-570">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-571">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-571">Category</span></span> |<span data-ttu-id="870c8-572">常に ``windows.sharedFonts`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-572">Always ``windows.sharedFonts``.</span></span>
|<span data-ttu-id="870c8-573">ファイル</span><span class="sxs-lookup"><span data-stu-id="870c8-573">File</span></span> |<span data-ttu-id="870c8-574">共有するフォントが格納されたファイル。</span><span class="sxs-lookup"><span data-stu-id="870c8-574">The file that contains the fonts that you want to share.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-575">例</span><span class="sxs-lookup"><span data-stu-id="870c8-575">Example</span></span>

```XML
<Package
  xmlns:uap4="http://schemas.microsoft.com/appx/manifest/uap/windows10/4"
  IgnorableNamespaces="uap4">
  <Applications>
    <Application>
      <Extensions>
        <uap4:Extension Category="windows.sharedFonts">
          <uap4:SharedFonts>
            <uap4:Font File="Fonts\JustRealize.ttf" />
            <uap4:Font File="Fonts\JustRealizeBold.ttf" />
          </uap4:SharedFonts>
        </uap4:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="win32-process" />

### <a name="start-a-win32-process-from-a-universal-windows-platform-uwp-app"></a><span data-ttu-id="870c8-576">ユニバーサル Windows プラットフォーム (UWP) アプリから Win32 プロセスを開始する</span><span class="sxs-lookup"><span data-stu-id="870c8-576">Start a Win32 process from a Universal Windows Platform (UWP) app</span></span>

<span data-ttu-id="870c8-577">完全信頼で実行される Win32 プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="870c8-577">Start a Win32 process that runs in full-trust.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="870c8-578">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="870c8-578">XML namespaces</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="870c8-579">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="870c8-579">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fullTrustProcess" Executable="[executable file]">
  <FullTrustProcess>
    <ParameterGroup GroupId="[GroupID]" Parameters="[Parameters]"/>
  </FullTrustProcess>
</Extension>
```

|<span data-ttu-id="870c8-580">名前</span><span class="sxs-lookup"><span data-stu-id="870c8-580">Name</span></span> |<span data-ttu-id="870c8-581">説明</span><span class="sxs-lookup"><span data-stu-id="870c8-581">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="870c8-582">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="870c8-582">Category</span></span> |<span data-ttu-id="870c8-583">常に ``windows.fullTrustProcess`` です。</span><span class="sxs-lookup"><span data-stu-id="870c8-583">Always ``windows.fullTrustProcess``.</span></span>
|<span data-ttu-id="870c8-584">GroupID</span><span class="sxs-lookup"><span data-stu-id="870c8-584">GroupID</span></span> |<span data-ttu-id="870c8-585">実行可能ファイルに渡すパラメーターのセットを識別するための文字列。</span><span class="sxs-lookup"><span data-stu-id="870c8-585">A string that identifies a set of parameters that you want to pass to the executable.</span></span> |
|<span data-ttu-id="870c8-586">パラメーター</span><span class="sxs-lookup"><span data-stu-id="870c8-586">Parameters</span></span> |<span data-ttu-id="870c8-587">実行可能ファイルに渡すパラメーター。</span><span class="sxs-lookup"><span data-stu-id="870c8-587">Parameters that you want to pass to the executable.</span></span> |

#### <a name="example"></a><span data-ttu-id="870c8-588">例</span><span class="sxs-lookup"><span data-stu-id="870c8-588">Example</span></span>

```XML
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
         xmlns:rescap=
"http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
         xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10">
  ...
  <Capabilities>
      <rescap:Capability Name="runFullTrust"/>
  </Capabilities>
  <Applications>
    <Application>
      <Extensions>
          <desktop:Extension Category="windows.fullTrustProcess" Executable="fulltrustprocess.exe">
              <desktop:FullTrustProcess>
                  <desktop:ParameterGroup GroupId="SyncGroup" Parameters="/Sync"/>
                  <desktop:ParameterGroup GroupId="OtherGroup" Parameters="/Other"/>
              </desktop:FullTrustProcess>
           </desktop:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<span data-ttu-id="870c8-589">この拡張機能をすべてのデバイスで動作するユニバーサル Windows プラットフォームのユーザー インターフェイスを作成する場合に便利ですが完全信頼で実行を継続する Win32 アプリケーションのコンポーネントをします。</span><span class="sxs-lookup"><span data-stu-id="870c8-589">This extension might be useful if you want to create a Universal Windows Platform User interface that runs on all devices, but you want components of your Win32 application to continue running in full-trust.</span></span>

<span data-ttu-id="870c8-590">Win32 アプリの Windows アプリ パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="870c8-590">Just create a Windows app package for your Win32 app.</span></span> <span data-ttu-id="870c8-591">そのうえで、この拡張機能を UWP アプリのパッケージ ファイルに追加してください。</span><span class="sxs-lookup"><span data-stu-id="870c8-591">Then, add this extension to the package file of your UWP app.</span></span> <span data-ttu-id="870c8-592">この拡張機能では、Windows アプリ パッケージの実行可能ファイルを起動することを示します。</span><span class="sxs-lookup"><span data-stu-id="870c8-592">This extensions indicates that you want to start an executable file in the Windows app package.</span></span>  <span data-ttu-id="870c8-593">UWP アプリと Win32 アプリの間でやり取りを行うには、1 つまたは複数の[アプリ サービス](/windows/uwp/launch-resume/app-services.md)を設定します。</span><span class="sxs-lookup"><span data-stu-id="870c8-593">If you want to communicate between your UWP app and your Win32 app, you can set up one or more [app services](/windows/uwp/launch-resume/app-services.md) to do that.</span></span> <span data-ttu-id="870c8-594">このシナリオについては詳しくは、[こちら](https://blogs.msdn.microsoft.com/appconsult/2016/12/19/desktop-bridge-the-migrate-phase-invoking-a-win32-process-from-a-uwp-app/)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-594">You can read more about this scenario [here](https://blogs.msdn.microsoft.com/appconsult/2016/12/19/desktop-bridge-the-migrate-phase-invoking-a-win32-process-from-a-uwp-app/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="870c8-595">次のステップ</span><span class="sxs-lookup"><span data-stu-id="870c8-595">Next steps</span></span>

<span data-ttu-id="870c8-596">**質問の回答を検索**</span><span class="sxs-lookup"><span data-stu-id="870c8-596">**Find answers to your questions**</span></span>

<span data-ttu-id="870c8-597">ご質問がある場合は、</span><span class="sxs-lookup"><span data-stu-id="870c8-597">Have questions?</span></span> <span data-ttu-id="870c8-598">Stack Overflow でお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="870c8-598">Ask us on Stack Overflow.</span></span> <span data-ttu-id="870c8-599">Microsoft のチームでは、これらの[タグ](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge)をチェックしています。</span><span class="sxs-lookup"><span data-stu-id="870c8-599">Our team monitors these [tags](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge).</span></span> <span data-ttu-id="870c8-600">[こちら](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D)から質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="870c8-600">You can also ask us [here](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D).</span></span>

<span data-ttu-id="870c8-601">**ご意見や機能を提案します。**</span><span class="sxs-lookup"><span data-stu-id="870c8-601">**Give feedback or make feature suggestions**</span></span>

<span data-ttu-id="870c8-602">[UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial) のページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="870c8-602">See [UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial).</span></span>
