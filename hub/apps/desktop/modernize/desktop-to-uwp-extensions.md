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
ms.openlocfilehash: 063106362a36aa32d0874be15dd589b5fb573409
ms.sourcegitcommit: d1c3e13de3da3f7dce878b3735ee53765d0df240
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66214945"
---
# <a name="integrate-your-packaged-desktop-app-with-windows-10-and-uwp"></a><span data-ttu-id="f8837-104">Windows 10 と UWP パッケージ化されたデスクトップ アプリに統合します。</span><span class="sxs-lookup"><span data-stu-id="f8837-104">Integrate your packaged desktop app with Windows 10 and UWP</span></span>

<span data-ttu-id="f8837-105">場合する[MSIX コンテナーでデスクトップ アプリケーションをパッケージ化](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)、定義済みの拡張機能を使用して Windows 10 では、パッケージ化されたデスクトップ アプリケーションを統合する拡張機能を使用することができます、[アプリ パッケージ マニフェスト](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/schema-root).</span><span class="sxs-lookup"><span data-stu-id="f8837-105">If you [package your desktop application in an MSIX container](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root), you can use extensions to integrate your packaged desktop application with Windows 10 by using predefined extensions in the [app package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/schema-root).</span></span>

<span data-ttu-id="f8837-106">たとえば、拡張機能を使用して、ファイアウォールの例外を作成、ファイルの種類の既定のアプリケーション、アプリケーションを作成またはスタート タイルをポイントして、アプリのパッケージ化されたバージョン。</span><span class="sxs-lookup"><span data-stu-id="f8837-106">For example, use an extension to create a firewall exception, make your application the default application for a file type, or point start tiles to the packaged version of your app.</span></span> <span data-ttu-id="f8837-107">拡張機能は、アプリのパッケージ マニフェスト ファイルに XML を追加するだけで使用できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-107">To use an extension, just add some XML to your app's package manifest file.</span></span> <span data-ttu-id="f8837-108">コードは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="f8837-108">No code is required.</span></span>

<span data-ttu-id="f8837-109">この記事では、これらの拡張機能とそれらを使用して実行できるタスクについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f8837-109">This article describes these extensions and the tasks that you can perform by using them.</span></span>

> [!NOTE]
> <span data-ttu-id="f8837-110">この記事で説明されている機能では、お客様のデスクトップ アプリケーションの Windows アプリ パッケージを作成することが必要です。</span><span class="sxs-lookup"><span data-stu-id="f8837-110">The features described in this article require that you create a Windows app package for your desktop application.</span></span> <span data-ttu-id="f8837-111">これはまだ完了していない場合を参照してください。[デスクトップ アプリケーションをパッケージ化](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)します。</span><span class="sxs-lookup"><span data-stu-id="f8837-111">If you haven't yet done this, see [Package desktop applications](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root).</span></span>

## <a name="transition-users-to-your-app"></a><span data-ttu-id="f8837-112">ユーザーをアプリに移行する</span><span class="sxs-lookup"><span data-stu-id="f8837-112">Transition users to your app</span></span>

<span data-ttu-id="f8837-113">ユーザーによってパッケージ アプリが使用されるように、移行を促します。</span><span class="sxs-lookup"><span data-stu-id="f8837-113">Help users transition to your packaged app.</span></span>

* [<span data-ttu-id="f8837-114">既存のスタート タイルとタスク バー ボタンをポイントして、パッケージ アプリ</span><span class="sxs-lookup"><span data-stu-id="f8837-114">Point existing Start tiles and taskbar buttons to your packaged app</span></span>](#point)
* [<span data-ttu-id="f8837-115">デスクトップ アプリではなくファイルを開き、パッケージ化されたアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="f8837-115">Make your packaged application open files instead of your desktop app</span></span>](#make)
* [<span data-ttu-id="f8837-116">ファイルの種類のセット、パッケージ化されたアプリケーションに関連付ける</span><span class="sxs-lookup"><span data-stu-id="f8837-116">Associate your packaged application with a set of file types</span></span>](#associate)
* [<span data-ttu-id="f8837-117">特定のファイルの種類のファイルのコンテキスト メニューにオプションを追加します。</span><span class="sxs-lookup"><span data-stu-id="f8837-117">Add options to the context menus of files that have a certain file type</span></span>](#add)
* [<span data-ttu-id="f8837-118">URL を使用して直接特定の種類のファイルを開く</span><span class="sxs-lookup"><span data-stu-id="f8837-118">Open certain types of files directly by using a URL</span></span>](#open)

<a id="point" />

### <a name="point-existing-start-tiles-and-taskbar-buttons-to-your-packaged-app"></a><span data-ttu-id="f8837-119">既存のスタート タイルとタスク バー ボタンの参照先をパッケージ アプリに設定する</span><span class="sxs-lookup"><span data-stu-id="f8837-119">Point existing Start tiles and taskbar buttons to your packaged app</span></span>

<span data-ttu-id="f8837-120">ユーザーによって、デスクトップ アプリがタスク バーまたはスタート メニューにピン留めされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f8837-120">Your users might have pinned your desktop application to the taskbar or the Start menu.</span></span> <span data-ttu-id="f8837-121">これらのショートカットの参照先を新しいパッケージ アプリに変更できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-121">You can point those shortcuts to your new packaged app.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-122">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-122">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-123">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-123">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.desktopAppMigration">
    <DesktopAppMigration>
        <DesktopApp AumId="[your_app_aumid]" />
        <DesktopApp ShortcutPath="[path]" />
    </DesktopAppMigration>
</Extension>

```

<span data-ttu-id="f8837-124">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-rescap3-desktopappmigration)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-124">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-rescap3-desktopappmigration).</span></span>

|<span data-ttu-id="f8837-125">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-125">Name</span></span> | <span data-ttu-id="f8837-126">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-126">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-127">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-127">Category</span></span> |<span data-ttu-id="f8837-128">常に ``windows.desktopAppMigration`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-128">Always ``windows.desktopAppMigration``.</span></span>
|<span data-ttu-id="f8837-129">AumID</span><span class="sxs-lookup"><span data-stu-id="f8837-129">AumID</span></span> |<span data-ttu-id="f8837-130">パッケージ アプリのアプリケーション ユーザー モデル ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-130">The Application User Model ID of your packaged app.</span></span> |
|<span data-ttu-id="f8837-131">ShortcutPath</span><span class="sxs-lookup"><span data-stu-id="f8837-131">ShortcutPath</span></span> |<span data-ttu-id="f8837-132">アプリのデスクトップ バージョンを起動する .lnk ファイルへのパス。</span><span class="sxs-lookup"><span data-stu-id="f8837-132">The path to .lnk files that start the desktop version of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-133">例</span><span class="sxs-lookup"><span data-stu-id="f8837-133">Example</span></span>

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

#### <a name="related-sample"></a><span data-ttu-id="f8837-134">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="f8837-134">Related sample</span></span>

[<span data-ttu-id="f8837-135">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="f8837-135">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="make" />

### <a name="make-your-packaged-application-open-files-instead-of-your-desktop-app"></a><span data-ttu-id="f8837-136">デスクトップ アプリではなくファイルを開き、パッケージ化されたアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="f8837-136">Make your packaged application open files instead of your desktop app</span></span>

<span data-ttu-id="f8837-137">ユーザーが特定の種類のデスクトップ バージョンのアプリを開く代わりにファイルの既定で、新しいパッケージ化されたアプリケーションを開くことを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-137">You can make sure that users open your new packaged application by default for specific types of files instead of opening the desktop version of your app.</span></span>

<span data-ttu-id="f8837-138">これを行うには、ファイルの関連付けを継承するために、関連付けされている各アプリケーションの[プログラム識別子 (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx) を指定します。</span><span class="sxs-lookup"><span data-stu-id="f8837-138">To do that, you'll specify the [programmatic identifier (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx) of each application from which you want to inherit file associations.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-139">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-139">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-140">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-140">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
<FileTypeAssociation Name="[AppID]">
         <MigrationProgIds>
            <MigrationProgId>"[ProgID]"</MigrationProgId>
        </MigrationProgIds>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="f8837-141">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-141">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-142">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-142">Name</span></span> |<span data-ttu-id="f8837-143">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-143">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-144">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-144">Category</span></span> |<span data-ttu-id="f8837-145">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-145">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-146">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-146">Name</span></span> |<span data-ttu-id="f8837-147">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-147">A unique Id for your app.</span></span> <span data-ttu-id="f8837-148">この ID は、ファイルの種類の関連付けによって関連付けられたハッシュ対象の[プログラム識別子 (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx) を生成するために内部で使用されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-148">This Id is used internally to generate a hashed [programmatic identifier (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx) associated with your file type association.</span></span> <span data-ttu-id="f8837-149">この ID を使って、アプリの今後のバージョンで変更を管理することができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-149">You can use this Id to manage changes in future versions of your app.</span></span> |
|<span data-ttu-id="f8837-150">MigrationProgId</span><span class="sxs-lookup"><span data-stu-id="f8837-150">MigrationProgId</span></span> |<span data-ttu-id="f8837-151">[プログラム識別子 (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx)アプリケーション、コンポーネント、およびファイルの関連付けを継承するデスクトップ アプリケーションのバージョンをについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f8837-151">The [programmatic identifier (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx) that describes the application, component, and version of the desktop application from which you want to inherit file associations.</span></span>|

#### <a name="example"></a><span data-ttu-id="f8837-152">例</span><span class="sxs-lookup"><span data-stu-id="f8837-152">Example</span></span>

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

#### <a name="related-sample"></a><span data-ttu-id="f8837-153">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="f8837-153">Related sample</span></span>

[<span data-ttu-id="f8837-154">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="f8837-154">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="associate" />

### <a name="associate-your-packaged-application-with-a-set-of-file-types"></a><span data-ttu-id="f8837-155">ファイルの種類のセット、パッケージ化されたアプリケーションに関連付ける</span><span class="sxs-lookup"><span data-stu-id="f8837-155">Associate your packaged application with a set of file types</span></span>

<span data-ttu-id="f8837-156">パッケージ化されたアプリケーションは、ファイル拡張子に関連付けられていることができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-156">You can associated your packaged application with file type extensions.</span></span> <span data-ttu-id="f8837-157">ユーザーがファイルを右クリックし、選択した場合、**プログラムから開く**オプション、推奨事項の一覧で、アプリケーションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-157">If a user right-clicks a file and then selects the **Open with** option, your application appears in the list of suggestions.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-158">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-158">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-159">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-159">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[file extension]"</FileType>
        </SupportedFileTypes>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="f8837-160">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-160">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-161">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-161">Name</span></span> |<span data-ttu-id="f8837-162">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-162">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-163">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-163">Category</span></span> |<span data-ttu-id="f8837-164">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-164">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-165">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-165">Name</span></span> |<span data-ttu-id="f8837-166">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-166">A unique Id for your app.</span></span> <span data-ttu-id="f8837-167">この ID は、ファイルの種類の関連付けによって関連付けられたハッシュ対象の[プログラム識別子 (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx) を生成するために内部で使用されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-167">This Id is used internally to generate a hashed [programmatic identifier (ProgID)](https://msdn.microsoft.com/library/windows/desktop/cc144152.aspx) associated with your file type association.</span></span> <span data-ttu-id="f8837-168">この ID を使って、アプリの今後のバージョンで変更を管理することができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-168">You can use this Id to manage changes in future versions of your app.</span></span>   |
|<span data-ttu-id="f8837-169">FileType</span><span class="sxs-lookup"><span data-stu-id="f8837-169">FileType</span></span> |<span data-ttu-id="f8837-170">アプリでサポートされているファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="f8837-170">The file extension supported by your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-171">例</span><span class="sxs-lookup"><span data-stu-id="f8837-171">Example</span></span>

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

#### <a name="related-sample"></a><span data-ttu-id="f8837-172">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="f8837-172">Related sample</span></span>

[<span data-ttu-id="f8837-173">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="f8837-173">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="add" />

### <a name="add-options-to-the-context-menus-of-files-that-have-a-certain-file-type"></a><span data-ttu-id="f8837-174">特定の種類のファイルのコンテキスト メニューにオプションを追加する</span><span class="sxs-lookup"><span data-stu-id="f8837-174">Add options to the context menus of files that have a certain file type</span></span>

<span data-ttu-id="f8837-175">ほとんどの場合、ユーザーはファイルをダブルクリックして開きます。</span><span class="sxs-lookup"><span data-stu-id="f8837-175">In most cases, users double-click files to open them.</span></span> <span data-ttu-id="f8837-176">ユーザーがファイルを右クリックすると、さまざまなオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-176">If users, right click a file, various options appear.</span></span>

<span data-ttu-id="f8837-177">このメニューには、オプションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-177">You can add options to that menu.</span></span> <span data-ttu-id="f8837-178">これらのオプションを使用すると、ファイルの印刷、編集、プレビューなど、ファイルの操作を別の方法で行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-178">These options give users other ways to interact with your file such as print, edit, or preview the file.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-179">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-179">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-180">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-180">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedVerbs>
           <Verb Id="[ID]" Extended="[Extended]" Parameters="[parameters]">"[verb label]"</Verb>
        </SupportedVerbs>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="f8837-181">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-181">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-182">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-182">Name</span></span> |<span data-ttu-id="f8837-183">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-183">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-184">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-184">Category</span></span> | <span data-ttu-id="f8837-185">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-185">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-186">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-186">Name</span></span> |<span data-ttu-id="f8837-187">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-187">A unique Id for your app.</span></span> |
|<span data-ttu-id="f8837-188">動詞</span><span class="sxs-lookup"><span data-stu-id="f8837-188">Verb</span></span> |<span data-ttu-id="f8837-189">エクスプローラーのコンテキスト メニューに表示される名前です。</span><span class="sxs-lookup"><span data-stu-id="f8837-189">The name that appears in the File Explorer context menu.</span></span> <span data-ttu-id="f8837-190">この文字列は、```ms-resource``` を使用してローカライズできます。</span><span class="sxs-lookup"><span data-stu-id="f8837-190">This string is localizable that uses ```ms-resource```.</span></span>|
|<span data-ttu-id="f8837-191">ID</span><span class="sxs-lookup"><span data-stu-id="f8837-191">Id</span></span> |<span data-ttu-id="f8837-192">動詞の一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-192">The unique Id of the verb.</span></span> <span data-ttu-id="f8837-193">アプリケーションが UWP アプリの場合、ユーザーの選択を適切に処理できるように、アクティブ化イベントの引数の一部としてアプリに渡されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-193">If your application is a UWP app, this is passed to your app as part of its activation event args so it can handle the user’s selection appropriately.</span></span> <span data-ttu-id="f8837-194">アプリケーションが完全に信頼されているパッケージ アプリの場合は、パラメーターを受け取った代わりに (次の箇条書きを参照してください)。</span><span class="sxs-lookup"><span data-stu-id="f8837-194">If your application is a full-trust packaged app, it receives parameters instead (see the next bullet).</span></span> |
|<span data-ttu-id="f8837-195">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f8837-195">Parameters</span></span> |<span data-ttu-id="f8837-196">動詞に関連付けられている引数のパラメーターと値のリスト。</span><span class="sxs-lookup"><span data-stu-id="f8837-196">The list of argument parameters and values associated with the verb.</span></span> <span data-ttu-id="f8837-197">アプリケーションが完全に信頼されているパッケージ アプリの場合は、これらのパラメーターは、アプリケーションがアクティブになるイベント引数としてアプリケーションに渡されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-197">If your application is a full-trust packaged app, these parameters are passed to the application as event args when the application is activated.</span></span> <span data-ttu-id="f8837-198">複数のアクティブ化の動詞に基づくアプリケーションの動作をカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-198">You can customize the behavior of your application based on different activation verbs.</span></span> <span data-ttu-id="f8837-199">変数にファイル パスが含まれる可能性がある場合は、パラメーター値を引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="f8837-199">If a variable can contain a file path, wrap the parameter value in quotes.</span></span> <span data-ttu-id="f8837-200">これにより、パスにスペースが含まれている場合に発生する問題を回避できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-200">That will avoid any issues that happen in cases where the path includes spaces.</span></span> <span data-ttu-id="f8837-201">アプリケーションが UWP アプリの場合は、パラメーターを渡すことはできません。</span><span class="sxs-lookup"><span data-stu-id="f8837-201">If your application is a UWP app, you can’t pass parameters.</span></span> <span data-ttu-id="f8837-202">アプリは、代わりに ID を受け取ります (前の項目を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="f8837-202">The app receives the Id instead (see the previous bullet).</span></span>|
|<span data-ttu-id="f8837-203">Extended</span><span class="sxs-lookup"><span data-stu-id="f8837-203">Extended</span></span> |<span data-ttu-id="f8837-204">ユーザーが **Shift** キーを押しながらファイルを右クリックすることでコンテキスト メニューを表示した場合にのみ表示される動詞を指定します。</span><span class="sxs-lookup"><span data-stu-id="f8837-204">Specifies that the verb appears only if the user shows the context menu by holding the **Shift** key before right-clicking the file.</span></span> <span data-ttu-id="f8837-205">この属性は省略可能であり、指定されていない場合の既定値は **False** (常に動詞を表示する) です。</span><span class="sxs-lookup"><span data-stu-id="f8837-205">This attribute is optional and defaults to a value of **False** (e.g., always show the verb) if not listed.</span></span> <span data-ttu-id="f8837-206">この動作は各動詞について個別に指定します ("開く" は例外で、常に **False**)。</span><span class="sxs-lookup"><span data-stu-id="f8837-206">You specify this behavior individually for each verb (except for "Open," which is always **False**).</span></span>|

#### <a name="example"></a><span data-ttu-id="f8837-207">例</span><span class="sxs-lookup"><span data-stu-id="f8837-207">Example</span></span>

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

#### <a name="related-sample"></a><span data-ttu-id="f8837-208">関連するサンプル</span><span class="sxs-lookup"><span data-stu-id="f8837-208">Related sample</span></span>

[<span data-ttu-id="f8837-209">WPF ピクチャ ビューアーの移行/移行/アンインストール</span><span class="sxs-lookup"><span data-stu-id="f8837-209">WPF picture viewer with transition/migration/uninstallation</span></span>](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="open" />

### <a name="open-certain-types-of-files-directly-by-using-a-url"></a><span data-ttu-id="f8837-210">URL を使用して特定の種類のファイルを直接開く</span><span class="sxs-lookup"><span data-stu-id="f8837-210">Open certain types of files directly by using a URL</span></span>

<span data-ttu-id="f8837-211">ユーザーが特定の種類のデスクトップ バージョンのアプリを開く代わりにファイルの既定で、新しいパッケージ化されたアプリケーションを開くことを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-211">You can make sure that users open your new packaged application by default for specific types of files instead of opening the desktop version of your app.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-212">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-212">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* <span data-ttu-id="f8837-213">http://schemas.microsoft.com/appx/manifest/uap/windows10/3"</span><span class="sxs-lookup"><span data-stu-id="f8837-213">http://schemas.microsoft.com/appx/manifest/uap/windows10/3"</span></span>

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-214">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-214">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]" UseUrl="true" Parameters="%1">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
    </FileTypeAssociation>
</Extension>
```

<span data-ttu-id="f8837-215">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-215">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-216">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-216">Name</span></span> |<span data-ttu-id="f8837-217">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-217">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-218">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-218">Category</span></span> |<span data-ttu-id="f8837-219">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-219">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-220">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-220">Name</span></span> |<span data-ttu-id="f8837-221">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-221">A unique Id for your app.</span></span> |
|<span data-ttu-id="f8837-222">UseUrl</span><span class="sxs-lookup"><span data-stu-id="f8837-222">UseUrl</span></span> |<span data-ttu-id="f8837-223">URL ターゲットから直接ファイルを開くかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="f8837-223">Indicates whether to open files directly from a URL target.</span></span> <span data-ttu-id="f8837-224">この値を設定しない場合は、システムを使用して URL 原因、最初のダウンロード ファイルをローカル ファイルを開くアプリケーションでしようとします。</span><span class="sxs-lookup"><span data-stu-id="f8837-224">If you do not set this value, attempts by your application to open a file by using a URL cause the system to first download the file locally.</span></span> |
|<span data-ttu-id="f8837-225">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f8837-225">Parameters</span></span> |<span data-ttu-id="f8837-226">省略可能なパラメーター。</span><span class="sxs-lookup"><span data-stu-id="f8837-226">optional parameters.</span></span> |
|<span data-ttu-id="f8837-227">FileType</span><span class="sxs-lookup"><span data-stu-id="f8837-227">FileType</span></span> |<span data-ttu-id="f8837-228">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="f8837-228">The relevant file extensions.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-229">例</span><span class="sxs-lookup"><span data-stu-id="f8837-229">Example</span></span>

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

## <a name="perform-setup-tasks"></a><span data-ttu-id="f8837-230">セットアップ タスクを実行する</span><span class="sxs-lookup"><span data-stu-id="f8837-230">Perform setup tasks</span></span>

* [<span data-ttu-id="f8837-231">アプリがファイアウォールの例外を作成します。</span><span class="sxs-lookup"><span data-stu-id="f8837-231">Create firewall exception for your app</span></span>](#rules)
* [<span data-ttu-id="f8837-232">パッケージの任意のフォルダーに、DLL ファイルに配置します。</span><span class="sxs-lookup"><span data-stu-id="f8837-232">Place your DLL files into any folder of the package</span></span>](#load-paths)

<a id="rules" />

### <a name="create-firewall-exception-for-your-app"></a><span data-ttu-id="f8837-233">アプリのファイアウォール例外を作成する</span><span class="sxs-lookup"><span data-stu-id="f8837-233">Create firewall exception for your app</span></span>

<span data-ttu-id="f8837-234">アプリケーションは、ポート経由の通信を必要とする場合は、ファイアウォールの例外の一覧にアプリケーションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-234">If your application requires communication through a port, you can add your application to the list of firewall exceptions.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-235">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-235">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-236">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-236">Elements and attributes of this extension</span></span>

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

<span data-ttu-id="f8837-237">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-firewallrules)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-237">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-firewallrules).</span></span>

|<span data-ttu-id="f8837-238">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-238">Name</span></span> |<span data-ttu-id="f8837-239">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-239">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-240">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-240">Category</span></span> |<span data-ttu-id="f8837-241">いつも ``windows.firewallRules``</span><span class="sxs-lookup"><span data-stu-id="f8837-241">Always ``windows.firewallRules``</span></span>|
|<span data-ttu-id="f8837-242">実行可能ファイル</span><span class="sxs-lookup"><span data-stu-id="f8837-242">Executable</span></span> |<span data-ttu-id="f8837-243">ファイアウォールの例外の一覧に追加する実行可能ファイルの名前。</span><span class="sxs-lookup"><span data-stu-id="f8837-243">The name of the executable file that you want to add to the list of firewall exceptions</span></span> |
|<span data-ttu-id="f8837-244">Direction</span><span class="sxs-lookup"><span data-stu-id="f8837-244">Direction</span></span> |<span data-ttu-id="f8837-245">規則が受信規則か送信規則かを示します。</span><span class="sxs-lookup"><span data-stu-id="f8837-245">Indicates whether the rule is an inbound or outbound rule</span></span> |
|<span data-ttu-id="f8837-246">IPProtocol</span><span class="sxs-lookup"><span data-stu-id="f8837-246">IPProtocol</span></span> |<span data-ttu-id="f8837-247">通信プロトコル。</span><span class="sxs-lookup"><span data-stu-id="f8837-247">The communication protocol</span></span> |
|<span data-ttu-id="f8837-248">LocalPortMin</span><span class="sxs-lookup"><span data-stu-id="f8837-248">LocalPortMin</span></span> |<span data-ttu-id="f8837-249">ローカル ポート番号の範囲を示すポート番号の下限。</span><span class="sxs-lookup"><span data-stu-id="f8837-249">The lower port number in a range of local port numbers.</span></span> |
|<span data-ttu-id="f8837-250">LocalPortMax</span><span class="sxs-lookup"><span data-stu-id="f8837-250">LocalPortMax</span></span> |<span data-ttu-id="f8837-251">ローカル ポート番号の範囲を示すポート番号の上限。</span><span class="sxs-lookup"><span data-stu-id="f8837-251">The highest port number of a range of local port numbers.</span></span> |
|<span data-ttu-id="f8837-252">RemotePortMax</span><span class="sxs-lookup"><span data-stu-id="f8837-252">RemotePortMax</span></span> |<span data-ttu-id="f8837-253">リモート ポート番号の範囲を示すポート番号の下限。</span><span class="sxs-lookup"><span data-stu-id="f8837-253">The lower port number in a range of remote port numbers.</span></span> |
|<span data-ttu-id="f8837-254">RemotePortMax</span><span class="sxs-lookup"><span data-stu-id="f8837-254">RemotePortMax</span></span> |<span data-ttu-id="f8837-255">リモート ポート番号の範囲を示すポート番号の上限。</span><span class="sxs-lookup"><span data-stu-id="f8837-255">The highest port number of a range of remote port numbers.</span></span> |
|<span data-ttu-id="f8837-256">Profile</span><span class="sxs-lookup"><span data-stu-id="f8837-256">Profile</span></span> |<span data-ttu-id="f8837-257">ネットワークの種類。</span><span class="sxs-lookup"><span data-stu-id="f8837-257">The network type</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-258">例</span><span class="sxs-lookup"><span data-stu-id="f8837-258">Example</span></span>

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

### <a name="place-your-dll-files-into-any-folder-of-the-package"></a><span data-ttu-id="f8837-259">DLL ファイルをパッケージの任意のフォルダーに配置します。</span><span class="sxs-lookup"><span data-stu-id="f8837-259">Place your DLL files into any folder of the package</span></span>

<span data-ttu-id="f8837-260">拡張機能を使ってそれらのフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f8837-260">Use an extension to identify those folders.</span></span> <span data-ttu-id="f8837-261">これにより、システムは配置したファイルを見つけて読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-261">That way, the system can find and load the files that you place in them.</span></span> <span data-ttu-id="f8837-262">この拡張機能は、 _%PATH%_ 環境変数の置き換えと考えてください。</span><span class="sxs-lookup"><span data-stu-id="f8837-262">Think of this extension as a replacement of the _%PATH%_ environment variable.</span></span>

<span data-ttu-id="f8837-263">この拡張機能を使わない場合、システムはプロセスのパッケージの依存関係グラフ、パッケージ ルート フォルダー、システム ディレクトリ ( _%SystemRoot%\system32_) の順で検索します。</span><span class="sxs-lookup"><span data-stu-id="f8837-263">If you don't use this extension, the system searches the package dependency graph of the process, the package root folder, and then the system directory (_%SystemRoot%\system32_) in that order.</span></span> <span data-ttu-id="f8837-264">詳しくは、[Windows アプリの検索順序に関するページ](https://msdn.microsoft.com/library/windows/desktop/ms682586.aspx#_search_order_for_windows_store_apps)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-264">To learn more, see [Search order of Windows apps](https://msdn.microsoft.com/library/windows/desktop/ms682586.aspx#_search_order_for_windows_store_apps).</span></span>

<span data-ttu-id="f8837-265">各パッケージには、これらの拡張機能を 1 つだけ含めることができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-265">Each package can contain only one of these extensions.</span></span> <span data-ttu-id="f8837-266">つまり、1 つをメイン パッケージに追加し、他の拡張機能は[オプション パッケージと関連するセット](https://docs.microsoft.com/windows/uwp/packaging/optional-packages)それぞれに 1 つずつ追加できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-266">That means that you can add one of them to your main package, and then add one to each of your [optional packages, and related sets](https://docs.microsoft.com/windows/uwp/packaging/optional-packages).</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-267">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-267">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/uap/windows10/6

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-268">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-268">Elements and attributes of this extension</span></span>

<span data-ttu-id="f8837-269">アプリケーション マニフェストのパッケージ レベルでこの拡張機能を宣言します。</span><span class="sxs-lookup"><span data-stu-id="f8837-269">Declare this extension at the package-level of your app manifest.</span></span>

```XML
<Extension Category="windows.loaderSearchPathOverride">
  <LoaderSearchPathOverride>
    <LoaderSearchPathEntry FolderPath="[path]"/>
  </LoaderSearchPathOverride>
</Extension>

```

|<span data-ttu-id="f8837-270">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-270">Name</span></span> | <span data-ttu-id="f8837-271">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-271">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-272">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-272">Category</span></span> |<span data-ttu-id="f8837-273">常に ``windows.loaderSearchPathOverride`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-273">Always ``windows.loaderSearchPathOverride``.</span></span>
|<span data-ttu-id="f8837-274">FolderPath</span><span class="sxs-lookup"><span data-stu-id="f8837-274">FolderPath</span></span> | <span data-ttu-id="f8837-275">dll ファイルが含まれているフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="f8837-275">The path of the folder that contains your dll files.</span></span> <span data-ttu-id="f8837-276">パッケージのルート フォルダーの相対パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="f8837-276">Specify a path that is relative to the root folder of the package.</span></span> <span data-ttu-id="f8837-277">1 つの拡張機能で最大 5 つのパスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-277">You can specify up to five paths in one extension.</span></span> <span data-ttu-id="f8837-278">システムがパッケージのルート フォルダーにあるファイルを検索するようにする場合、これらのパスのいずれかに空の文字列を使用します。</span><span class="sxs-lookup"><span data-stu-id="f8837-278">If you want the system to search for files in the root folder of the package, use an empty string for one of these paths.</span></span> <span data-ttu-id="f8837-279">重複するパスを含めないでください。パスの先頭と末尾にスラッシュや円記号を使わないでください。</span><span class="sxs-lookup"><span data-stu-id="f8837-279">Don't included duplicate paths and make sure that your paths don't contain leading and trailing slashes or backslashes.</span></span> <br><br> <span data-ttu-id="f8837-280">システムはサブフォルダーを検索しないため、システムが読み込む DLL ファイルが含まれている各フォルダーを明示的に一覧表示してください。</span><span class="sxs-lookup"><span data-stu-id="f8837-280">The system won't search subfolders, so make sure to explicitly list each folder that contains DLL files that you want the system to load.</span></span>|

#### <a name="example"></a><span data-ttu-id="f8837-281">例</span><span class="sxs-lookup"><span data-stu-id="f8837-281">Example</span></span>

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

## <a name="integrate-with-file-explorer"></a><span data-ttu-id="f8837-282">エクスプローラーに統合する</span><span class="sxs-lookup"><span data-stu-id="f8837-282">Integrate with File Explorer</span></span>

<span data-ttu-id="f8837-283">ユーザーが慣れた方法でファイルを整理し操作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f8837-283">Help users organize your files and interact with them in familiar ways.</span></span>

* [<span data-ttu-id="f8837-284">ユーザーの選択し、同時に複数のファイルを開くときに、アプリケーションの動作を定義します。</span><span class="sxs-lookup"><span data-stu-id="f8837-284">Define how your application behaves when users select and open multiple files at the same time</span></span>](#define)
* [<span data-ttu-id="f8837-285">ファイル エクスプ ローラー内でサムネイル画像のファイルの内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="f8837-285">Show file contents in a thumbnail image within File Explorer</span></span>](#show)
* [<span data-ttu-id="f8837-286">ファイル エクスプ ローラーのプレビュー ウィンドウにファイルの内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="f8837-286">Show file contents in a Preview pane of File Explorer</span></span>](#preview)
* <span data-ttu-id="f8837-287">[ファイル エクスプ ローラーで、[種類] 列を使用して、ユーザーがファイルをグループ化を有効にします。](#enable)</span><span class="sxs-lookup"><span data-stu-id="f8837-287">[Enable users to group files by using the Kind column in File Explorer](#enable)</span></span>
* [<span data-ttu-id="f8837-288">検索、インデックス、プロパティ ダイアログ ボックス、および詳細ウィンドウにファイルのプロパティを使用できるように</span><span class="sxs-lookup"><span data-stu-id="f8837-288">Make file properties available to search, index, property dialogs, and the details pane</span></span>](#make-file-properties)
* [<span data-ttu-id="f8837-289">クラウド サービスからのファイルをファイル エクスプ ローラーに表示</span><span class="sxs-lookup"><span data-stu-id="f8837-289">Make files from your cloud service appear in File Explorer</span></span>](#cloud-files)

<a id="define" />

### <a name="define-how-your-application-behaves-when-users-select-and-open-multiple-files-at-the-same-time"></a><span data-ttu-id="f8837-290">ユーザーの選択し、同時に複数のファイルを開くときに、アプリケーションの動作を定義します。</span><span class="sxs-lookup"><span data-stu-id="f8837-290">Define how your application behaves when users select and open multiple files at the same time</span></span>

<span data-ttu-id="f8837-291">ユーザーが同時に複数のファイルを開いたときに、アプリケーションの動作を指定します。</span><span class="sxs-lookup"><span data-stu-id="f8837-291">Specify how your application behaves when a user opens multiple files simultaneously.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-292">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-292">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-293">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-293">Elements and attributes of this extension</span></span>

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

<span data-ttu-id="f8837-294">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-294">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-295">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-295">Name</span></span> |<span data-ttu-id="f8837-296">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-296">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-297">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-297">Category</span></span> |<span data-ttu-id="f8837-298">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-298">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-299">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-299">Name</span></span> |<span data-ttu-id="f8837-300">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-300">A unique Id for your app.</span></span> |
|<span data-ttu-id="f8837-301">MultiSelectModel</span><span class="sxs-lookup"><span data-stu-id="f8837-301">MultiSelectModel</span></span> |<span data-ttu-id="f8837-302">下を参照</span><span class="sxs-lookup"><span data-stu-id="f8837-302">See below</span></span> |
|<span data-ttu-id="f8837-303">FileType</span><span class="sxs-lookup"><span data-stu-id="f8837-303">FileType</span></span> |<span data-ttu-id="f8837-304">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="f8837-304">The relevant file extensions.</span></span> |

<span data-ttu-id="f8837-305">**MultSelectModel**</span><span class="sxs-lookup"><span data-stu-id="f8837-305">**MultSelectModel**</span></span>

<span data-ttu-id="f8837-306">パッケージ デスクトップ アプリには、通常のデスクトップ アプリと同じ 3 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="f8837-306">packaged desktop apps have the same three options as regular desktop apps.</span></span>

* <span data-ttu-id="f8837-307">``Player`` :アプリケーションは、1 回をアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-307">``Player``: Your application is activated one time.</span></span> <span data-ttu-id="f8837-308">すべての選択したファイルは、引数のパラメーターとしてアプリケーションに渡されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-308">All of the selected files are passed to your application as argument parameters.</span></span>
* <span data-ttu-id="f8837-309">``Single`` :アプリケーションは、選択した最初のファイルの 1 つの時間をアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-309">``Single``: Your application is activated one time for the first selected file.</span></span> <span data-ttu-id="f8837-310">その他のファイルは無視されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-310">Other files are ignored.</span></span>
* <span data-ttu-id="f8837-311">``Document`` :選択したファイルごとに、アプリケーションの新しい、個別のインスタンスがアクティブ化されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-311">``Document``: A new, separate instance of your application is activated for each selected file.</span></span>

 <span data-ttu-id="f8837-312">ファイルの種類やアクションごとに、さまざまな環境設定項目を設定できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-312">You can set different preferences for different file types and actions.</span></span> <span data-ttu-id="f8837-313">たとえば、*Documents* は *Document* モードで開き、*Images* は *Player* モードで開くことができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-313">For example, you may wish to open *Documents* in *Document* mode and *Images* in *Player* mode.</span></span>

#### <a name="example"></a><span data-ttu-id="f8837-314">例</span><span class="sxs-lookup"><span data-stu-id="f8837-314">Example</span></span>

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

<span data-ttu-id="f8837-315">ユーザーが 15 個以下のファイルを開いた場合、**MultiSelectModel** 属性の既定値は *Player* になります。</span><span class="sxs-lookup"><span data-stu-id="f8837-315">If the user opens 15 or fewer files, the default choice for the **MultiSelectModel** attribute is *Player*.</span></span> <span data-ttu-id="f8837-316">それ以外の場合、既定値は *Document* です。</span><span class="sxs-lookup"><span data-stu-id="f8837-316">Otherwise, the default is *Document*.</span></span> <span data-ttu-id="f8837-317">UWP アプリは常に *Player* として起動されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-317">UWP apps are always started as *Player*.</span></span>

<a id="show" />

### <a name="show-file-contents-in-a-thumbnail-image-within-file-explorer"></a><span data-ttu-id="f8837-318">エクスプ ローラーでサムネイル画像のファイル内容を表示する</span><span class="sxs-lookup"><span data-stu-id="f8837-318">Show file contents in a thumbnail image within File Explorer</span></span>

<span data-ttu-id="f8837-319">ファイルが中アイコン、大アイコン、特大アイコンで表示された場合に、ファイル内容のサムネイル画像をユーザーが確認できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f8837-319">Enable users to view a thumbnail image of the file's contents when the icon of the file appears in the medium, large, or extra large size.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-320">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-320">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-321">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-321">Elements and attributes of this extension</span></span>

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

<span data-ttu-id="f8837-322">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-322">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-323">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-323">Name</span></span> |<span data-ttu-id="f8837-324">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-324">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-325">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-325">Category</span></span> |<span data-ttu-id="f8837-326">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-326">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-327">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-327">Name</span></span> |<span data-ttu-id="f8837-328">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-328">A unique Id for your app.</span></span> |
|<span data-ttu-id="f8837-329">FileType</span><span class="sxs-lookup"><span data-stu-id="f8837-329">FileType</span></span> |<span data-ttu-id="f8837-330">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="f8837-330">The relevant file extensions.</span></span> |
|<span data-ttu-id="f8837-331">Clsid</span><span class="sxs-lookup"><span data-stu-id="f8837-331">Clsid</span></span>   |<span data-ttu-id="f8837-332">アプリのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-332">The class ID of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-333">例</span><span class="sxs-lookup"><span data-stu-id="f8837-333">Example</span></span>

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

### <a name="show-file-contents-in-the-preview-pane-of-file-explorer"></a><span data-ttu-id="f8837-334">エクスプローラーのプレビュー ウィンドウにファイル内容を表示する</span><span class="sxs-lookup"><span data-stu-id="f8837-334">Show file contents in the Preview pane of File Explorer</span></span>

<span data-ttu-id="f8837-335">エクスプローラーのプレビュー ウィンドウで、ユーザーがファイルの内容をプレビューできるようにします。</span><span class="sxs-lookup"><span data-stu-id="f8837-335">Enable users to preview a file's contents in the Preview pane of File Explorer.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-336">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-336">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-337">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-337">Elements and attributes of this extension</span></span>

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

<span data-ttu-id="f8837-338">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-338">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-339">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-339">Name</span></span> |<span data-ttu-id="f8837-340">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-340">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-341">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-341">Category</span></span> |<span data-ttu-id="f8837-342">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-342">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-343">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-343">Name</span></span> |<span data-ttu-id="f8837-344">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-344">A unique Id for your app.</span></span> |
|<span data-ttu-id="f8837-345">FileType</span><span class="sxs-lookup"><span data-stu-id="f8837-345">FileType</span></span> |<span data-ttu-id="f8837-346">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="f8837-346">The relevant file extensions.</span></span> |
|<span data-ttu-id="f8837-347">Clsid</span><span class="sxs-lookup"><span data-stu-id="f8837-347">Clsid</span></span>   |<span data-ttu-id="f8837-348">アプリのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-348">The class ID of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-349">例</span><span class="sxs-lookup"><span data-stu-id="f8837-349">Example</span></span>

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

### <a name="enable-users-to-group-files-by-using-the-kind-column-in-file-explorer"></a><span data-ttu-id="f8837-350">ユーザーがエクスプローラーの [種類] 列を使用してファイルをグループ化できるようにする</span><span class="sxs-lookup"><span data-stu-id="f8837-350">Enable users to group files by using the Kind column in File Explorer</span></span>

<span data-ttu-id="f8837-351">ファイルの種類に関する 1 つまたは複数の定義済みの値を **Kind** フィールドに関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-351">You can associate one or more predefined values for your file types with the **Kind** field.</span></span>

<span data-ttu-id="f8837-352">ユーザーはエクスプローラーでこのフィールドを使用して、ファイルをグループ化できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-352">In File Explorer, users can group those files by using that field.</span></span> <span data-ttu-id="f8837-353">また、このフィールドは、システム コンポーネントによって、インデックス作成などのさまざまな目的にも使用されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-353">System components also use this field for various purposes such as indexing.</span></span>

<span data-ttu-id="f8837-354">**Kind** フィールドの詳細と、このフィールドに使用できる値については、「[種類名の使用](https://msdn.microsoft.com/library/windows/desktop/cc144136.aspx)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-354">For more information about the **Kind** field and the values that you can use for this field, see [Using Kind Names](https://msdn.microsoft.com/library/windows/desktop/cc144136.aspx).</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-355">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-355">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-356">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-356">Elements and attributes of this extension</span></span>

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

<span data-ttu-id="f8837-357">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-357">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-358">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-358">Name</span></span> |<span data-ttu-id="f8837-359">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-359">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-360">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-360">Category</span></span> |<span data-ttu-id="f8837-361">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-361">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-362">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-362">Name</span></span> |<span data-ttu-id="f8837-363">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-363">A unique Id for your app.</span></span> |
|<span data-ttu-id="f8837-364">FileType</span><span class="sxs-lookup"><span data-stu-id="f8837-364">FileType</span></span> |<span data-ttu-id="f8837-365">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="f8837-365">The relevant file extensions.</span></span> |
|<span data-ttu-id="f8837-366">value</span><span class="sxs-lookup"><span data-stu-id="f8837-366">value</span></span> |<span data-ttu-id="f8837-367">有効な [Kind 値](https://msdn.microsoft.com/en-us/library/windows/desktop/cc144136.aspx#kind_hierarchy)。</span><span class="sxs-lookup"><span data-stu-id="f8837-367">A valid [Kind value](https://msdn.microsoft.com/en-us/library/windows/desktop/cc144136.aspx#kind_hierarchy)</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-368">例</span><span class="sxs-lookup"><span data-stu-id="f8837-368">Example</span></span>

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

### <a name="make-file-properties-available-to-search-index-property-dialogs-and-the-details-pane"></a><span data-ttu-id="f8837-369">ファイルのプロパティを検索、インデックス、プロパティ ダイアログ、詳細ウィンドウに利用できるようにする</span><span class="sxs-lookup"><span data-stu-id="f8837-369">Make file properties available to search, index, property dialogs, and the details pane</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-370">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-370">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-371">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-371">Elements and attributes of this extension</span></span>

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

<span data-ttu-id="f8837-372">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-372">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

|<span data-ttu-id="f8837-373">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-373">Name</span></span> |<span data-ttu-id="f8837-374">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-374">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-375">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-375">Category</span></span> |<span data-ttu-id="f8837-376">常に ``windows.fileTypeAssociation`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-376">Always ``windows.fileTypeAssociation``.</span></span>
|<span data-ttu-id="f8837-377">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-377">Name</span></span> |<span data-ttu-id="f8837-378">アプリの一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-378">A unique Id for your app.</span></span> |
|<span data-ttu-id="f8837-379">FileType</span><span class="sxs-lookup"><span data-stu-id="f8837-379">FileType</span></span> |<span data-ttu-id="f8837-380">関連するファイル拡張子。</span><span class="sxs-lookup"><span data-stu-id="f8837-380">The relevant file extensions.</span></span> |
|<span data-ttu-id="f8837-381">Clsid</span><span class="sxs-lookup"><span data-stu-id="f8837-381">Clsid</span></span>  |<span data-ttu-id="f8837-382">アプリのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-382">The class ID of your app.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-383">例</span><span class="sxs-lookup"><span data-stu-id="f8837-383">Example</span></span>

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

<a id="cloud-files" />

### <a name="make-files-from-your-cloud-service-appear-in-file-explorer"></a><span data-ttu-id="f8837-384">クラウド サービスのファイルがエクスプローラーに表示されるようにする</span><span class="sxs-lookup"><span data-stu-id="f8837-384">Make files from your cloud service appear in File Explorer</span></span>

<span data-ttu-id="f8837-385">アプリに実装するハンドラーを登録する</span><span class="sxs-lookup"><span data-stu-id="f8837-385">Register the handlers that you implement in your application.</span></span> <span data-ttu-id="f8837-386">ユーザーがエクスプローラーでクラウド ベースのファイルを右クリックしたときに表示されるコンテキスト メニュー オプションを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="f8837-386">You can also add context menu options that appear when you users right-click your cloud-based files in File Explorer.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-387">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-387">XML namespace</span></span>

* http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-388">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-388">Elements and attributes of this extension</span></span>

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

|<span data-ttu-id="f8837-389">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-389">Name</span></span> |<span data-ttu-id="f8837-390">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-390">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-391">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-391">Category</span></span> |<span data-ttu-id="f8837-392">常に ``windows.cloudfiles`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-392">Always ``windows.cloudfiles``.</span></span>
|<span data-ttu-id="f8837-393">iconResource</span><span class="sxs-lookup"><span data-stu-id="f8837-393">iconResource</span></span> |<span data-ttu-id="f8837-394">クラウド ファイル プロバイダー サービスを表すアイコン。</span><span class="sxs-lookup"><span data-stu-id="f8837-394">The icon that represents your cloud file provider service.</span></span> <span data-ttu-id="f8837-395">このアイコンは、エクスプローラーのナビゲーション ウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-395">This icon appears in the Navigation pane of File Explorer.</span></span>  <span data-ttu-id="f8837-396">ユーザーは、このアイコンを選んでクラウド サービスのファイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="f8837-396">Users choose this icon to show files from your cloud service.</span></span> |
|<span data-ttu-id="f8837-397">CustomStateHandler Clsid</span><span class="sxs-lookup"><span data-stu-id="f8837-397">CustomStateHandler Clsid</span></span> |<span data-ttu-id="f8837-398">CustomStateHandler を実装するアプリケーションのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-398">The class ID of the application that implements the CustomStateHandler.</span></span> <span data-ttu-id="f8837-399">システムは、このクラス ID を使ってクラウド ファイルのカスタム状態と列を要求します。</span><span class="sxs-lookup"><span data-stu-id="f8837-399">The system uses this Class ID to request custom states and columns for cloud files.</span></span> |
|<span data-ttu-id="f8837-400">ThumbnailProviderHandler Clsid</span><span class="sxs-lookup"><span data-stu-id="f8837-400">ThumbnailProviderHandler Clsid</span></span> |<span data-ttu-id="f8837-401">ThumbnailProviderHandler を実装するアプリケーションのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-401">The class ID of the application that implements the ThumbnailProviderHandler.</span></span> <span data-ttu-id="f8837-402">システムは、このクラス ID を使ってクラウド ファイルの縮小版イメージを要求します。</span><span class="sxs-lookup"><span data-stu-id="f8837-402">The system uses this Class ID to request thumbnail images for cloud files.</span></span> |
|<span data-ttu-id="f8837-403">ExtendedPropertyHandler Clsid</span><span class="sxs-lookup"><span data-stu-id="f8837-403">ExtendedPropertyHandler Clsid</span></span> |<span data-ttu-id="f8837-404">ExtendedPropertyHandler を実装するアプリケーションのクラス ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-404">The class ID of the application that implements the ExtendedPropertyHandler.</span></span>  <span data-ttu-id="f8837-405">システムは、このクラス ID を使ってクラウド ファイルの拡張プロパティを要求します。</span><span class="sxs-lookup"><span data-stu-id="f8837-405">The system uses this Class ID to request extended properties for a cloud file.</span></span> |
|<span data-ttu-id="f8837-406">動詞</span><span class="sxs-lookup"><span data-stu-id="f8837-406">Verb</span></span> |<span data-ttu-id="f8837-407">クラウド サービスによって提供されるファイルのエクスプローラー コンテキスト メニューに表示される名前です。</span><span class="sxs-lookup"><span data-stu-id="f8837-407">The name that appears in the File Explorer context menu for files provided by your cloud service.</span></span> |
|<span data-ttu-id="f8837-408">ID</span><span class="sxs-lookup"><span data-stu-id="f8837-408">Id</span></span> |<span data-ttu-id="f8837-409">動詞の一意の ID。</span><span class="sxs-lookup"><span data-stu-id="f8837-409">The unique ID of the verb.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-410">例</span><span class="sxs-lookup"><span data-stu-id="f8837-410">Example</span></span>

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

## <a name="start-your-application-in-different-ways"></a><span data-ttu-id="f8837-411">さまざまな方法でアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="f8837-411">Start your application in different ways</span></span>

* [<span data-ttu-id="f8837-412">プロトコルを使用して、アプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="f8837-412">Start your application by using a protocol</span></span>](#protocol)
* [<span data-ttu-id="f8837-413">エイリアスを使用して、アプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="f8837-413">Start your application by using an alias</span></span>](#alias)
* [<span data-ttu-id="f8837-414">ユーザーが Windows にログインすると、実行可能ファイルを開始します。</span><span class="sxs-lookup"><span data-stu-id="f8837-414">Start an executable file when users log into Windows</span></span>](#executable)
* [<span data-ttu-id="f8837-415">ユーザーが各自の PC にデバイスを接続するときのアプリケーションの起動を有効にします。</span><span class="sxs-lookup"><span data-stu-id="f8837-415">Enable users to start your application when they connect a device to their PC</span></span>](#autoplay)
* [<span data-ttu-id="f8837-416">Microsoft Store から更新プログラムを受信した後に自動的に再起動します。</span><span class="sxs-lookup"><span data-stu-id="f8837-416">Restart automatically after receiving an update from the Microsoft Store</span></span>](#updates)

<a id="protocol" />

### <a name="start-your-application-by-using-a-protocol"></a><span data-ttu-id="f8837-417">プロトコルを使用して、アプリケーションを開始します。</span><span class="sxs-lookup"><span data-stu-id="f8837-417">Start your application by using a protocol</span></span>

<span data-ttu-id="f8837-418">プロトコルの関連付けによって、他のプログラムやシステム コンポーネントがパッケージ アプリと相互運用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f8837-418">Protocol associations can enable other programs and system components to interoperate with your packaged app.</span></span> <span data-ttu-id="f8837-419">プロトコルを使用して、パッケージ化されたアプリケーションが開始されると、それに従って動作できるように、アクティブ化イベントの引数を渡す特定のパラメーターを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-419">When your packaged application is started by using a protocol, you can specify specific parameters to pass to its activation event arguments so it can behave accordingly.</span></span> <span data-ttu-id="f8837-420">パラメーターは、完全に信頼できるパッケージ アプリでのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f8837-420">Parameters are supported only for packaged, full-trust apps.</span></span> <span data-ttu-id="f8837-421">UWP アプリでは、パラメーターを使用できません。</span><span class="sxs-lookup"><span data-stu-id="f8837-421">UWP apps can't use parameters.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-422">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-422">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-423">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-423">Elements and attributes of this extension</span></span>

```XML
<Extension
    Category="windows.protocol">
  <Protocol
      Name="[Protocol name]"
      Parameters="[Parameters]" />
</Extension>
```

<span data-ttu-id="f8837-424">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-protocol)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-424">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-protocol).</span></span>

|<span data-ttu-id="f8837-425">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-425">Name</span></span> |<span data-ttu-id="f8837-426">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-426">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-427">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-427">Category</span></span> |<span data-ttu-id="f8837-428">常に ``windows.protocol`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-428">Always ``windows.protocol``.</span></span>
|<span data-ttu-id="f8837-429">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-429">Name</span></span> |<span data-ttu-id="f8837-430">プロトコルの名前。</span><span class="sxs-lookup"><span data-stu-id="f8837-430">The name of the protocol.</span></span> |
|<span data-ttu-id="f8837-431">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f8837-431">Parameters</span></span> |<span data-ttu-id="f8837-432">パラメーターと、アプリケーションがアクティブになるイベントの引数として、アプリケーションに渡す値の一覧。</span><span class="sxs-lookup"><span data-stu-id="f8837-432">The list of parameters and values to pass to your application as event arguments when the application is activated.</span></span> <span data-ttu-id="f8837-433">変数にファイル パスが含まれる可能性がある場合は、パラメーター値を引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="f8837-433">If a variable can contain a file path, wrap the parameter value in quotes.</span></span> <span data-ttu-id="f8837-434">これにより、パスにスペースが含まれている場合に発生する問題を回避できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-434">That will avoid any issues that happen in cases where the path includes spaces.</span></span> |

### <a name="example"></a><span data-ttu-id="f8837-435">例</span><span class="sxs-lookup"><span data-stu-id="f8837-435">Example</span></span>

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

### <a name="start-your-application-by-using-an-alias"></a><span data-ttu-id="f8837-436">エイリアスを使用して、アプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="f8837-436">Start your application by using an alias</span></span>

<span data-ttu-id="f8837-437">ユーザーおよびその他のプロセスは、アプリへの完全パスを指定するのにことがなく、アプリケーションを開始するのにエイリアスを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-437">Users and other processes can use an alias to start your application without having to specify the full path to your app.</span></span> <span data-ttu-id="f8837-438">そのエイリアス名を指定できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-438">You can specify that alias name.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-439">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-439">XML namespaces</span></span>

* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-440">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-440">Elements and attributes of this extension</span></span>

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

|<span data-ttu-id="f8837-441">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-441">Name</span></span> |<span data-ttu-id="f8837-442">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-442">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-443">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-443">Category</span></span> |<span data-ttu-id="f8837-444">常に ``windows.appExecutionAlias`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-444">Always ``windows.appExecutionAlias``.</span></span>
|<span data-ttu-id="f8837-445">実行可能ファイル</span><span class="sxs-lookup"><span data-stu-id="f8837-445">Executable</span></span> |<span data-ttu-id="f8837-446">エイリアスが呼び出されたときに起動する実行可能ファイルの相対パス。</span><span class="sxs-lookup"><span data-stu-id="f8837-446">The relative path to the executable to start when the alias is invoked.</span></span> |
|<span data-ttu-id="f8837-447">Alias</span><span class="sxs-lookup"><span data-stu-id="f8837-447">Alias</span></span> |<span data-ttu-id="f8837-448">アプリの短い名前。</span><span class="sxs-lookup"><span data-stu-id="f8837-448">The short name for your app.</span></span> <span data-ttu-id="f8837-449">常に、拡張子 ".exe" で終わっている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f8837-449">It must always end with the ".exe" extension.</span></span> <span data-ttu-id="f8837-450">パッケージ内のアプリケーションごとにアプリの実行エイリアスは 1 つだけ指定できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-450">You can only specify a single app execution alias for each application in the package.</span></span> <span data-ttu-id="f8837-451">複数のアプリで同じエイリアスが登録されている場合、システムは最後に登録されたアプリを呼び出します。したがって、他のアプリが上書きする可能性が低い一意のエイリアスを選んでください。</span><span class="sxs-lookup"><span data-stu-id="f8837-451">If multiple apps register for the same alias, the system will invoke the last one that was registered, so make sure to choose a unique alias other apps are unlikely to override.</span></span>
|

#### <a name="example"></a><span data-ttu-id="f8837-452">例</span><span class="sxs-lookup"><span data-stu-id="f8837-452">Example</span></span>

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

<span data-ttu-id="f8837-453">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-453">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation).</span></span>

<a id="executable" />

### <a name="start-an-executable-file-when-users-log-into-windows"></a><span data-ttu-id="f8837-454">ユーザーが Windows にログオンしたときに実行可能ファイルを起動する</span><span class="sxs-lookup"><span data-stu-id="f8837-454">Start an executable file when users log into Windows</span></span>

<span data-ttu-id="f8837-455">スタートアップ タスクでは、ユーザーがログオンするたびに自動的に実行可能ファイルを実行するアプリケーションを許可します。</span><span class="sxs-lookup"><span data-stu-id="f8837-455">Startup tasks allow your application to run an executable automatically whenever a user logs on.</span></span>

> [!NOTE]
> <span data-ttu-id="f8837-456">ユーザーは、このスタートアップ タスクを登録するには少なくとも 1 回のアプリケーションの起動を持ちます。</span><span class="sxs-lookup"><span data-stu-id="f8837-456">The user has to start your application at least one time to register this startup task.</span></span>

<span data-ttu-id="f8837-457">アプリケーションでは、複数のスタートアップ タスクを宣言できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-457">Your application can declare multiple startup tasks.</span></span> <span data-ttu-id="f8837-458">各タスクは独立して起動されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-458">Each task starts independently.</span></span> <span data-ttu-id="f8837-459">すべてのスタートアップ タスクは、タスク マネージャーの **[スタートアップ]** タブに、アプリのマニフェストで指定した名前とアプリのアイコンを使って表示されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-459">All startup tasks will appear in Task Manager under the **Startup** tab with the name that you specify in your app's manifest and your app's icon.</span></span> <span data-ttu-id="f8837-460">タスク マネージャーによって、タスクの起動への影響が自動的に分析されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-460">Task Manager will automatically analyze the startup impact of your tasks.</span></span>

<span data-ttu-id="f8837-461">ユーザーは、タスク マネージャーを使用して、アプリのスタートアップ タスクを手動で無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-461">Users can manually disable your app's startup task by using Task Manager.</span></span> <span data-ttu-id="f8837-462">ユーザーがタスクを無効にした場合、プログラムでタスクを再度有効にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="f8837-462">If a user disables a task, you can't programmatically re-enable it.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-463">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-463">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-464">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-464">Elements and attributes of this extension</span></span>

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

|<span data-ttu-id="f8837-465">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-465">Name</span></span> |<span data-ttu-id="f8837-466">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-466">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-467">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-467">Category</span></span> |<span data-ttu-id="f8837-468">常に ``windows.startupTask`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-468">Always ``windows.startupTask``.</span></span>|
|<span data-ttu-id="f8837-469">実行可能ファイル</span><span class="sxs-lookup"><span data-stu-id="f8837-469">Executable</span></span> |<span data-ttu-id="f8837-470">起動する実行可能ファイルへの相対パス。</span><span class="sxs-lookup"><span data-stu-id="f8837-470">The relative path to the executable file to start.</span></span> |
|<span data-ttu-id="f8837-471">TaskId</span><span class="sxs-lookup"><span data-stu-id="f8837-471">TaskId</span></span> |<span data-ttu-id="f8837-472">タスクの一意の識別子。</span><span class="sxs-lookup"><span data-stu-id="f8837-472">A unique identifier for your task.</span></span> <span data-ttu-id="f8837-473">この識別子を使用して、アプリケーション Api を呼び出すこと、 [Windows.ApplicationModel.StartupTask](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.StartupTask)クラスをプログラムで有効または、スタートアップ タスクを無効にします。</span><span class="sxs-lookup"><span data-stu-id="f8837-473">Using this identifier, your application can call the APIs in the [Windows.ApplicationModel.StartupTask](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.StartupTask) class to programmatically enable or disable a startup task.</span></span> |
|<span data-ttu-id="f8837-474">有効</span><span class="sxs-lookup"><span data-stu-id="f8837-474">Enabled</span></span> |<span data-ttu-id="f8837-475">初めて起動したタスクを有効にするか、無効にするかを指定します。</span><span class="sxs-lookup"><span data-stu-id="f8837-475">Indicates whether the task first starts enabled or disabled.</span></span> <span data-ttu-id="f8837-476">有効になっているタスクは、(ユーザーが無効にしていない限り) 次回ユーザーがログオンするときに実行されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-476">Enabled tasks will run the next time the user logs on (unless the user disables it).</span></span> |
|<span data-ttu-id="f8837-477">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f8837-477">DisplayName</span></span> |<span data-ttu-id="f8837-478">タスク マネージャーに表示されるタスクの名前。</span><span class="sxs-lookup"><span data-stu-id="f8837-478">The name of the task that appears in Task Manager.</span></span> <span data-ttu-id="f8837-479">この文字列は、```ms-resource``` を使用してローカライズできます。</span><span class="sxs-lookup"><span data-stu-id="f8837-479">You can localize this string by using ```ms-resource```.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-480">例</span><span class="sxs-lookup"><span data-stu-id="f8837-480">Example</span></span>

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

### <a name="enable-users-to-start-your-application-when-they-connect-a-device-to-their-pc"></a><span data-ttu-id="f8837-481">ユーザーが各自の PC にデバイスを接続するときのアプリケーションの起動を有効にします。</span><span class="sxs-lookup"><span data-stu-id="f8837-481">Enable users to start your application when they connect a device to their PC</span></span>

<span data-ttu-id="f8837-482">自動再生は、ユーザーが各自の PC にデバイスを接続するときに、オプションとして、アプリケーションを表示できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-482">AutoPlay can present your application as an option when a user connects a device to their PC.</span></span>

#### <a name="xml-namespace"></a><span data-ttu-id="f8837-483">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-483">XML namespace</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-484">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-484">Elements and attributes of this extension</span></span>

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

|<span data-ttu-id="f8837-485">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-485">Name</span></span> |<span data-ttu-id="f8837-486">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-486">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-487">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-487">Category</span></span> |<span data-ttu-id="f8837-488">常に ``windows.autoPlayHandler`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-488">Always ``windows.autoPlayHandler``.</span></span>
|<span data-ttu-id="f8837-489">ActionDisplayName</span><span class="sxs-lookup"><span data-stu-id="f8837-489">ActionDisplayName</span></span> |<span data-ttu-id="f8837-490">ユーザーが PC に接続するデバイスで実行できるアクションを表す文字列です (例。「ファイルのインポート」または「ビデオを再生」)。</span><span class="sxs-lookup"><span data-stu-id="f8837-490">A string that represents the action that users can take with a device that they connect to a PC (For example: "Import files", or "Play video").</span></span> |
|<span data-ttu-id="f8837-491">ProviderDisplayName</span><span class="sxs-lookup"><span data-stu-id="f8837-491">ProviderDisplayName</span></span> | <span data-ttu-id="f8837-492">アプリケーションまたはサービスを表す文字列です (例。「Contoso ビデオ プレーヤー」)。</span><span class="sxs-lookup"><span data-stu-id="f8837-492">A string that represents your application or service (For example: "Contoso video player").</span></span> |
|<span data-ttu-id="f8837-493">ContentEvent</span><span class="sxs-lookup"><span data-stu-id="f8837-493">ContentEvent</span></span> |<span data-ttu-id="f8837-494">ユーザーに ``ActionDisplayName`` と ``ProviderDisplayName`` をプロンプト表示する原因となるコンテンツ イベントの名前。</span><span class="sxs-lookup"><span data-stu-id="f8837-494">The name of a content event that causes users to be prompted with your ``ActionDisplayName`` and ``ProviderDisplayName``.</span></span> <span data-ttu-id="f8837-495">コンテンツ イベントは、カメラのメモリ カード、サム ドライブ、DVD などのボリューム デバイスが PC に挿入されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="f8837-495">A content event is raised when a volume device such as a camera memory card, thumb drive, or DVD is inserted into the PC.</span></span> <span data-ttu-id="f8837-496">これらのイベントの詳しい一覧については、[ここ](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-496">You can find the full list of those events [here](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference).</span></span>  |
|<span data-ttu-id="f8837-497">動詞</span><span class="sxs-lookup"><span data-stu-id="f8837-497">Verb</span></span> |<span data-ttu-id="f8837-498">動詞の設定は、選択したオプションのアプリケーションに渡される値を識別します。</span><span class="sxs-lookup"><span data-stu-id="f8837-498">The Verb setting identifies a value that is passed to your application for the selected option.</span></span> <span data-ttu-id="f8837-499">自動再生のイベントの起動アクションは複数指定できます。また、[動詞] 設定を使って、ユーザーがアプリで選んだアクションを確認できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-499">You can specify multiple launch actions for an AutoPlay event and use the Verb setting to determine which option a user has selected for your app.</span></span> <span data-ttu-id="f8837-500">アプリに渡される起動イベント引数の verb プロパティを調べることでユーザーが選んだオプションを確認できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-500">You can tell which option the user selected by checking the verb property of the startup event arguments passed to your app.</span></span> <span data-ttu-id="f8837-501">[動詞] 設定には任意の値を使うことができます。ただし、予約されている open を除きます。</span><span class="sxs-lookup"><span data-stu-id="f8837-501">You can use any value for the Verb setting except, open, which is reserved.</span></span> |
|<span data-ttu-id="f8837-502">DropTargetHandler</span><span class="sxs-lookup"><span data-stu-id="f8837-502">DropTargetHandler</span></span> |<span data-ttu-id="f8837-503">実装するアプリケーションのクラス ID、 [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017)インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="f8837-503">The class ID of the application that implements the [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) interface.</span></span> <span data-ttu-id="f8837-504">リムーバブル メディアのファイルは、[IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) 実装の [Drop](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget.drop?view=visualstudiosdk-2017#Microsoft_VisualStudio_OLE_Interop_IDropTarget_Drop_Microsoft_VisualStudio_OLE_Interop_IDataObject_System_UInt32_Microsoft_VisualStudio_OLE_Interop_POINTL_System_UInt32__) メソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="f8837-504">Files from the removable media are passed to the [Drop](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget.drop?view=visualstudiosdk-2017#Microsoft_VisualStudio_OLE_Interop_IDropTarget_Drop_Microsoft_VisualStudio_OLE_Interop_IDataObject_System_UInt32_Microsoft_VisualStudio_OLE_Interop_POINTL_System_UInt32__) method of your [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) implementation.</span></span>  |
|<span data-ttu-id="f8837-505">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f8837-505">Parameters</span></span> |<span data-ttu-id="f8837-506">すべてのコンテンツ イベントで [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) インターフェイスを実装する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f8837-506">You don't have to implement the [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) interface for all content events.</span></span> <span data-ttu-id="f8837-507">どのコンテンツ イベントにも、[IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) インターフェイスを実装する代わりにコマンド ライン パラメーターを指定することができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-507">For any of the content events, you could provide command line parameters instead of implementing the [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) interface.</span></span> <span data-ttu-id="f8837-508">これらのイベントでは、自動再生がこれらのコマンド ライン パラメーターを使用してアプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="f8837-508">For those events, AutoPlay will start your application by using those command line parameters.</span></span> <span data-ttu-id="f8837-509">アプリの初期化コードでそれらのパラメーターを解析して、自動再生によって起動したかどうかを判断し、カスタム実装を提供することができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-509">You can parse those parameters in your app's initialization code to determine if it was started by AutoPlay and then provide your custom implementation.</span></span> |
|<span data-ttu-id="f8837-510">DeviceEvent</span><span class="sxs-lookup"><span data-stu-id="f8837-510">DeviceEvent</span></span> |<span data-ttu-id="f8837-511">ユーザーに ``ActionDisplayName`` と ``ProviderDisplayName`` をプロンプト表示する原因となるデバイス イベントの名前。</span><span class="sxs-lookup"><span data-stu-id="f8837-511">The name of a device event that causes users to be prompted with your ``ActionDisplayName`` and ``ProviderDisplayName``.</span></span> <span data-ttu-id="f8837-512">デバイス イベントは、デバイスが PC に接続されると発生します。</span><span class="sxs-lookup"><span data-stu-id="f8837-512">A device event is raised when a device is connected to the PC.</span></span> <span data-ttu-id="f8837-513">デバイス イベントの先頭は文字列 ``WPD`` です。一覧については[ここ](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-513">Device events begin with the string ``WPD`` and you can find them listed [here](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference).</span></span> |
|<span data-ttu-id="f8837-514">HWEventHandler</span><span class="sxs-lookup"><span data-stu-id="f8837-514">HWEventHandler</span></span> |<span data-ttu-id="f8837-515">実装するアプリケーションのクラス ID、 [IHWEventHandler](https://msdn.microsoft.com/library/windows/desktop/bb775492.aspx)インターフェイス。</span><span class="sxs-lookup"><span data-stu-id="f8837-515">The Class ID of the application that implements the [IHWEventHandler](https://msdn.microsoft.com/library/windows/desktop/bb775492.aspx) interface.</span></span> |
|<span data-ttu-id="f8837-516">InitCmdLine</span><span class="sxs-lookup"><span data-stu-id="f8837-516">InitCmdLine</span></span> |<span data-ttu-id="f8837-517">[IHWEventHandler](https://msdn.microsoft.com/library/windows/desktop/bb775492.aspx) インターフェイスの [Initialize](https://msdn.microsoft.com/en-us/library/windows/desktop/bb775495.aspx) メソッドに渡す文字列パラメーター。</span><span class="sxs-lookup"><span data-stu-id="f8837-517">The string parameter that you want to pass into the [Initialize](https://msdn.microsoft.com/en-us/library/windows/desktop/bb775495.aspx) method of the [IHWEventHandler](https://msdn.microsoft.com/library/windows/desktop/bb775492.aspx) interface.</span></span> |

### <a name="example"></a><span data-ttu-id="f8837-518">例</span><span class="sxs-lookup"><span data-stu-id="f8837-518">Example</span></span>

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

### <a name="restart-automatically-after-receiving-an-update-from-the-microsoft-store"></a><span data-ttu-id="f8837-519">Microsoft Store から更新プログラムを受信した後、自動的に再起動する</span><span class="sxs-lookup"><span data-stu-id="f8837-519">Restart automatically after receiving an update from the Microsoft Store</span></span>

<span data-ttu-id="f8837-520">ユーザーに更新プログラムをインストールするときに、アプリケーションが開いている場合、アプリケーションを閉じます。</span><span class="sxs-lookup"><span data-stu-id="f8837-520">If your application is open when users install an update to it, the application closes.</span></span>

<span data-ttu-id="f8837-521">そのアプリケーションの場合、更新された後で再起動が完了すると、呼び出し、 [RegisterApplicationRestart](https://msdn.microsoft.com/library/windows/desktop/aa373347.aspx)を再起動するすべてのプロセス内の関数。</span><span class="sxs-lookup"><span data-stu-id="f8837-521">If you want that application to restart after the update completes, call the  [RegisterApplicationRestart](https://msdn.microsoft.com/library/windows/desktop/aa373347.aspx) function in every process that you want to restart.</span></span>

<span data-ttu-id="f8837-522">各アクティブなウィンドウ、アプリケーションでの受信、 [WM_QUERYENDSESSION](https://msdn.microsoft.com/library/windows/desktop/aa376890.aspx)メッセージ。</span><span class="sxs-lookup"><span data-stu-id="f8837-522">Each active window in your application receives a [WM_QUERYENDSESSION](https://msdn.microsoft.com/library/windows/desktop/aa376890.aspx) message.</span></span> <span data-ttu-id="f8837-523">この時点で、アプリケーションを呼び出すことができます、 [RegisterApplicationRestart](https://msdn.microsoft.com/library/windows/desktop/aa373347.aspx)必要な場合は、コマンドラインを更新するには、もう一度関数。</span><span class="sxs-lookup"><span data-stu-id="f8837-523">At this point, your application can call the [RegisterApplicationRestart](https://msdn.microsoft.com/library/windows/desktop/aa373347.aspx) function again to update the command line if necessary.</span></span>

<span data-ttu-id="f8837-524">アプリケーション内のアクティブな各ウィンドウが受信すると、 [WM_ENDSESSION](https://msdn.microsoft.com/library/windows/desktop/aa376889.aspx)メッセージ、アプリケーションがデータを保存およびシャット ダウンします。</span><span class="sxs-lookup"><span data-stu-id="f8837-524">When each active window in your application receives the [WM_ENDSESSION](https://msdn.microsoft.com/library/windows/desktop/aa376889.aspx) message, your application should save data and shut down.</span></span>

>[!NOTE]
<span data-ttu-id="f8837-525">また、アクティブなウィンドウが表示される、 [WM_CLOSE](https://msdn.microsoft.com/library/windows/desktop/ms632617.aspx)メッセージ、アプリケーションが処理しない場合、 [WM_ENDSESSION](https://msdn.microsoft.com/library/windows/desktop/aa376889.aspx)メッセージ。</span><span class="sxs-lookup"><span data-stu-id="f8837-525">Your active windows also receive the [WM_CLOSE](https://msdn.microsoft.com/library/windows/desktop/ms632617.aspx) message in case the application doesn't handle the [WM_ENDSESSION](https://msdn.microsoft.com/library/windows/desktop/aa376889.aspx) message.</span></span>

<span data-ttu-id="f8837-526">この時点で、アプリケーションが、独自のプロセスを終了する 30 秒を持っているか、プラットフォームは、これらを強制的に終了します。</span><span class="sxs-lookup"><span data-stu-id="f8837-526">At this point, your application has 30 seconds to close it's own processes or the platform terminates them forcefully.</span></span>

<span data-ttu-id="f8837-527">更新プログラムが完了した後、アプリケーションを再起動します。</span><span class="sxs-lookup"><span data-stu-id="f8837-527">After the update is complete, your application restarts.</span></span>

## <a name="work-with-other-applications"></a><span data-ttu-id="f8837-528">他のアプリケーションと連携する</span><span class="sxs-lookup"><span data-stu-id="f8837-528">Work with other applications</span></span>

<span data-ttu-id="f8837-529">他のアプリとの統合、他のプロセスの開始、情報の共有が可能です。</span><span class="sxs-lookup"><span data-stu-id="f8837-529">Integrate with other apps, start other processes or share information.</span></span>

* [<span data-ttu-id="f8837-530">印刷をサポートするアプリケーションで印刷のターゲットとして表示される、アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="f8837-530">Make your application appear as the print target in applications that support printing</span></span>](#printing)
* [<span data-ttu-id="f8837-531">その他の Windows アプリケーションでのフォントの共有</span><span class="sxs-lookup"><span data-stu-id="f8837-531">Share fonts with other Windows applications</span></span>](#fonts)
* [<span data-ttu-id="f8837-532">ユニバーサル Windows プラットフォーム (UWP) アプリからの Win32 プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="f8837-532">Start a Win32 process from a Universal Windows Platform (UWP) app</span></span>](#win32-process)

<a id="printing" />

### <a name="make-your-application-appear-as-the-print-target-in-applications-that-support-printing"></a><span data-ttu-id="f8837-533">印刷をサポートするアプリケーションで印刷のターゲットとして表示される、アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="f8837-533">Make your application appear as the print target in applications that support printing</span></span>

<span data-ttu-id="f8837-534">ユーザーは、メモ帳などの別のアプリケーションからデータを印刷する場合、アプリケーションの利用可能な印刷ターゲット アプリの一覧で印刷のターゲットとして表示を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f8837-534">When users want to print data from another application such as Notepad, you can make your application appear as a print target in the app's list of available print targets.</span></span>

<span data-ttu-id="f8837-535">XML Paper Specification (XPS) 形式で印刷データを受信するようにアプリケーションを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f8837-535">You'll have to modify your application so that it receives print data in XML Paper Specification (XPS) format.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-536">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-536">XML namespaces</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-537">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-537">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.appPrinter">
    <AppPrinter
        DisplayName="[DisplayName]"
        Parameters="[Parameters]" />
</Extension>
```

<span data-ttu-id="f8837-538">完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-appprinter)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-538">Find the complete schema reference [here](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-appprinter).</span></span>

|<span data-ttu-id="f8837-539">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-539">Name</span></span> |<span data-ttu-id="f8837-540">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-540">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-541">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-541">Category</span></span> |<span data-ttu-id="f8837-542">常に ``windows.appPrinter`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-542">Always ``windows.appPrinter``.</span></span>
|<span data-ttu-id="f8837-543">DisplayName</span><span class="sxs-lookup"><span data-stu-id="f8837-543">DisplayName</span></span> |<span data-ttu-id="f8837-544">アプリの印刷先一覧に表示する名前。</span><span class="sxs-lookup"><span data-stu-id="f8837-544">The name that you want to appear in the list of print targets for an app.</span></span> |
|<span data-ttu-id="f8837-545">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f8837-545">Parameters</span></span> |<span data-ttu-id="f8837-546">アプリケーションに要求を正しく処理するために必要な任意のパラメーター。</span><span class="sxs-lookup"><span data-stu-id="f8837-546">Any parameters that your application requires to properly handle the request.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-547">例</span><span class="sxs-lookup"><span data-stu-id="f8837-547">Example</span></span>

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

<span data-ttu-id="f8837-548">この拡張機能を使用するサンプルについては、[こちら](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/PrintToPDF)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-548">Find a sample that uses this extension [Here](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/PrintToPDF)</span></span>

<a id="fonts" />

### <a name="share-fonts-with-other-windows-applications"></a><span data-ttu-id="f8837-549">他の Windows アプリケーションとフォントを共有する</span><span class="sxs-lookup"><span data-stu-id="f8837-549">Share fonts with other Windows applications</span></span>

<span data-ttu-id="f8837-550">他の Windows アプリケーションとカスタム フォントを共有できます。</span><span class="sxs-lookup"><span data-stu-id="f8837-550">Share your custom fonts with other Windows applications.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-551">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-551">XML namespaces</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-552">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-552">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.sharedFonts">
    <SharedFonts>
      <Font File="[FontFile]" />
    </SharedFonts>
  </Extension>
```

<span data-ttu-id="f8837-553">完全なスキーマ リファレンスについては、[こちら](/uwp/schemas/appxpackage/uapmanifestschema/element-uap4-sharedfonts)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-553">Find the complete schema reference [here](/uwp/schemas/appxpackage/uapmanifestschema/element-uap4-sharedfonts).</span></span>

|<span data-ttu-id="f8837-554">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-554">Name</span></span> |<span data-ttu-id="f8837-555">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-555">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-556">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-556">Category</span></span> |<span data-ttu-id="f8837-557">常に ``windows.sharedFonts`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-557">Always ``windows.sharedFonts``.</span></span>
|<span data-ttu-id="f8837-558">ファイル</span><span class="sxs-lookup"><span data-stu-id="f8837-558">File</span></span> |<span data-ttu-id="f8837-559">共有するフォントが格納されたファイル。</span><span class="sxs-lookup"><span data-stu-id="f8837-559">The file that contains the fonts that you want to share.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-560">例</span><span class="sxs-lookup"><span data-stu-id="f8837-560">Example</span></span>

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

### <a name="start-a-win32-process-from-a-universal-windows-platform-uwp-app"></a><span data-ttu-id="f8837-561">ユニバーサル Windows プラットフォーム (UWP) アプリから Win32 プロセスを開始する</span><span class="sxs-lookup"><span data-stu-id="f8837-561">Start a Win32 process from a Universal Windows Platform (UWP) app</span></span>

<span data-ttu-id="f8837-562">完全信頼で実行される Win32 プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="f8837-562">Start a Win32 process that runs in full-trust.</span></span>

#### <a name="xml-namespaces"></a><span data-ttu-id="f8837-563">XML 名前空間</span><span class="sxs-lookup"><span data-stu-id="f8837-563">XML namespaces</span></span>

http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a><span data-ttu-id="f8837-564">この拡張機能の要素と属性</span><span class="sxs-lookup"><span data-stu-id="f8837-564">Elements and attributes of this extension</span></span>

```XML
<Extension Category="windows.fullTrustProcess" Executable="[executable file]">
  <FullTrustProcess>
    <ParameterGroup GroupId="[GroupID]" Parameters="[Parameters]"/>
  </FullTrustProcess>
</Extension>
```

|<span data-ttu-id="f8837-565">名前</span><span class="sxs-lookup"><span data-stu-id="f8837-565">Name</span></span> |<span data-ttu-id="f8837-566">説明</span><span class="sxs-lookup"><span data-stu-id="f8837-566">Description</span></span> |
|-------|-------------|
|<span data-ttu-id="f8837-567">カテゴリ</span><span class="sxs-lookup"><span data-stu-id="f8837-567">Category</span></span> |<span data-ttu-id="f8837-568">常に ``windows.fullTrustProcess`` です。</span><span class="sxs-lookup"><span data-stu-id="f8837-568">Always ``windows.fullTrustProcess``.</span></span>
|<span data-ttu-id="f8837-569">GroupID</span><span class="sxs-lookup"><span data-stu-id="f8837-569">GroupID</span></span> |<span data-ttu-id="f8837-570">実行可能ファイルに渡すパラメーターのセットを識別するための文字列。</span><span class="sxs-lookup"><span data-stu-id="f8837-570">A string that identifies a set of parameters that you want to pass to the executable.</span></span> |
|<span data-ttu-id="f8837-571">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f8837-571">Parameters</span></span> |<span data-ttu-id="f8837-572">実行可能ファイルに渡すパラメーター。</span><span class="sxs-lookup"><span data-stu-id="f8837-572">Parameters that you want to pass to the executable.</span></span> |

#### <a name="example"></a><span data-ttu-id="f8837-573">例</span><span class="sxs-lookup"><span data-stu-id="f8837-573">Example</span></span>

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

<span data-ttu-id="f8837-574">この拡張機能をすべてのデバイスで動作するユニバーサル Windows プラットフォームのユーザー インターフェイスを作成する場合に便利ですが完全信頼で実行を継続する Win32 アプリケーションのコンポーネントをします。</span><span class="sxs-lookup"><span data-stu-id="f8837-574">This extension might be useful if you want to create a Universal Windows Platform User interface that runs on all devices, but you want components of your Win32 application to continue running in full-trust.</span></span>

<span data-ttu-id="f8837-575">Win32 アプリの Windows アプリ パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="f8837-575">Just create a Windows app package for your Win32 app.</span></span> <span data-ttu-id="f8837-576">そのうえで、この拡張機能を UWP アプリのパッケージ ファイルに追加してください。</span><span class="sxs-lookup"><span data-stu-id="f8837-576">Then, add this extension to the package file of your UWP app.</span></span> <span data-ttu-id="f8837-577">この拡張機能では、Windows アプリ パッケージの実行可能ファイルを起動することを示します。</span><span class="sxs-lookup"><span data-stu-id="f8837-577">This extensions indicates that you want to start an executable file in the Windows app package.</span></span>  <span data-ttu-id="f8837-578">UWP アプリと Win32 アプリの間でやり取りを行うには、1 つまたは複数の[アプリ サービス](/windows/uwp/launch-resume/app-services.md)を設定します。</span><span class="sxs-lookup"><span data-stu-id="f8837-578">If you want to communicate between your UWP app and your Win32 app, you can set up one or more [app services](/windows/uwp/launch-resume/app-services.md) to do that.</span></span> <span data-ttu-id="f8837-579">このシナリオについては詳しくは、[こちら](https://blogs.msdn.microsoft.com/appconsult/2016/12/19/desktop-bridge-the-migrate-phase-invoking-a-win32-process-from-a-uwp-app/)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-579">You can read more about this scenario [here](https://blogs.msdn.microsoft.com/appconsult/2016/12/19/desktop-bridge-the-migrate-phase-invoking-a-win32-process-from-a-uwp-app/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8837-580">次のステップ</span><span class="sxs-lookup"><span data-stu-id="f8837-580">Next steps</span></span>

<span data-ttu-id="f8837-581">**質問の回答を検索**</span><span class="sxs-lookup"><span data-stu-id="f8837-581">**Find answers to your questions**</span></span>

<span data-ttu-id="f8837-582">ご質問がある場合は、</span><span class="sxs-lookup"><span data-stu-id="f8837-582">Have questions?</span></span> <span data-ttu-id="f8837-583">Stack Overflow でお問い合わせください。</span><span class="sxs-lookup"><span data-stu-id="f8837-583">Ask us on Stack Overflow.</span></span> <span data-ttu-id="f8837-584">Microsoft のチームでは、これらの[タグ](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge)をチェックしています。</span><span class="sxs-lookup"><span data-stu-id="f8837-584">Our team monitors these [tags](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge).</span></span> <span data-ttu-id="f8837-585">[こちら](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D)から質問することもできます。</span><span class="sxs-lookup"><span data-stu-id="f8837-585">You can also ask us [here](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D).</span></span>

<span data-ttu-id="f8837-586">**ご意見や機能を提案します。**</span><span class="sxs-lookup"><span data-stu-id="f8837-586">**Give feedback or make feature suggestions**</span></span>

<span data-ttu-id="f8837-587">[UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial) のページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f8837-587">See [UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial).</span></span>
