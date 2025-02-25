---
ms.assetid: 2f76c520-84a3-4066-8eb3-ecc0ecd198a7
title: Windows デスクトップ ブリッジ アプリのテスト
description: デスクトップ ブリッジの組み込みのテストを使用して、UWP アプリへの変換のため、デスクトップ アプリを最適化することを確認します。
ms.date: 12/18/2017
ms.topic: article
keywords: windows 10 は、uwp アプリの認定
ms.localizationpriority: medium
ms.openlocfilehash: 38c9a40dbe1a46aa125c76cd1fcc88a84685c8cc
ms.sourcegitcommit: 280193dfe5a106fc6b4c85df3ac40535547b855c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67235172"
---
# <a name="windows-desktop-bridge-app-tests"></a>Windows デスクトップ ブリッジ アプリのテスト

[デスクトップ ブリッジ アプリ](https://docs.microsoft.com/en-us/windows/uwp/porting/desktop-to-uwp-root)Windows デスクトップ アプリケーションを使用してユニバーサル Windows プラットフォーム (UWP) アプリに変換されて、[デスクトップ ブリッジ](https://developer.microsoft.com/en-us/windows/bridges/desktop)します。 Windows デスクトップ アプリケーションは、変換後、Windows 10 デスクトップをターゲットとする UWP アプリ パッケージ (.appx または .appxbundle) の形式でパッケージ化され、処理と展開が行われます。

## <a name="required-versus-optional-tests"></a>必須のテストとオプションのテスト
Windows デスクトップ ブリッジ アプリの省略可能なテストは情報提供のみと、Microsoft Store オンボード中に、アプリを評価するには使用されません。 調査をお勧めします。 これらのテスト結果をより適切な品質のアプリを生成します。 ストアの配布準備の全体的な合格/不合格の基準は、これらのオプションのテストではなく、必須のテストで決定されます。

## <a name="current-optional-tests"></a>現在のオプションのテスト

### <a name="1-digitally-signed-file-test"></a>1. ファイルのテストをデジタル署名 
**背景情報**  
このテストでは、すべてのポータブル実行可能ファイル (PE) ファイルに有効な署名が含まれていることを確認します。 デジタル署名されたファイルの存在によって、ユーザーはソフトウェアが正規品であると知ることができます。

**テストの詳細**  
テストでは、パッケージ内のすべてのポータブル実行可能ファイルをスキャンし、そのヘッダーの署名を確認します。 すべての PE ファイルがデジタル署名されていることを推奨します。 PE ファイルのいずれかが署名されていない場合、警告が生成されます。
 
**是正措置**  
ファイルにデジタル署名することを常にお勧めします。 詳しくは、「[コード署名の概要](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537361(v=vs.85))」をご覧ください。

### <a name="2-file-association-verbs"></a>2. ファイルの関連付けの動詞 
**背景情報**  
このテストでは、パッケージのレジストリをスキャンして、任意のファイルの関連付け動詞が登録されているかどうかを確認します。 

**テストの詳細**  
変換されたデスクトップ アプリケーションは、幅広いユニバーサル Windows プラットフォーム API を使用して拡張できます。 このテストでは、アプリ内の UWP バイナリが UWP 以外の API を呼び出していないことを確認します。 UWP バイナリでは、**AppContainer** フラグが設定されています。

**是正措置**  
参照してください[UWP ブリッジにデスクトップ。App エクス テンション](https://docs.microsoft.com/en-us/windows/uwp/porting/desktop-to-uwp-extensions)これらの拡張機能と適切に使用する方法の詳細についてはします。 

### <a name="3-debug-configuration-test"></a>3.デバッグ構成のテスト
このテストでは、appx がデバッグ ビルドではないことを確認します。
 
**背景情報**  
Microsoft Store の認定する場合にアプリする必要がありますがコンパイルされずデバッグ用、いない実行可能ファイルのデバッグ バージョンを参照する必要があります。 また、アプリがこのテストに合格するよう最適化されたコードをビルドする必要もあります。
 
**テストの詳細**  
アプリをテストして、デバッグ用のビルドでないことと、どのデバッグ用のフレームワークにもリンクされていないことを確認します。
 
**是正措置**  
* Microsoft Store に提出する前に、リリース ビルドとして、アプリをビルドします。
* 適切なバージョンの .NET フレームワークがインストールされていることを確認します。
* アプリがフレームワークのデバッグ バージョンにリンクされていないことと、リリース バージョンで構築されたことを確認します。 このアプリに .NET コンポーネントが含まれている場合は、適切なバージョンの .NET Framework がインストールされていることを確認します。

### <a name="4-package-sanity-test"></a>4。パッケージのサニティ テスト
#### <a name="41-archive-files-usage"></a>4.1 アーカイブ ファイルの使用状況

**背景情報**  
このテストは、[Windows 10 S](https://www.microsoft.com/windows/windows-10-s) コンピューターで動作するデスクトップ ブリッジ アプリの質を高めるために役立ちます。

**テストの詳細**  
このテストでは、アーカイブ ファイルや自己展開型コンテンツに含まれている実行可能ファイルをすべてチェックします。 このような種類のコンテンツに格納されている実行可能ファイルは、Windows ストアへのオンボード時に署名されないため、Windows 10 S システムではアプリが期待どおりに動作しない場合があります。
 
**是正措置**
* テストによってフラグ付けされたファイルを評価して、Windows 10 S 環境で実行した場合にアプリに影響がないかどうかを確認します。
* アプリが影響を受ける場合は、アーカイブ ファイルから実行可能ファイルを削除します。また、自己展開型アーカイブを使って実行可能ファイルをディスク上に配置しないようにします。 これにより、アプリの機能が失われることを回避できます。

#### <a name="42-blocked-executables"></a>4.2 ブロックされる実行可能ファイル

**背景情報**  
このテストは、[Windows 10 S](https://www.microsoft.com/windows/windows-10-s) コンピューターで動作するデスクトップ ブリッジ アプリの質を高めるために役立ちます。 

**テストの詳細**  
このテストでは、アプリが実行可能ファイルの起動を試みていないかどうかをチェックします。これは Windows 10 S システムでは制限されます。 この機能に依存するアプリは、Windows 10 S システムでは正しく動作しない可能性があります。 

**是正措置**  
* テストによってフラグ付けされたエントリのうち、アプリの一部ではない実行可能ファイルの起動を呼び出しているものを特定し、それらの呼び出しを削除します。 
* フラグ付けされたファイルがアプリケーションの一部である場合は、この警告を無視できます。


## <a name="current-required-tests"></a>現在の必須のテスト

### <a name="1-app-capabilities-test-special-use-capabilities"></a>1. アプリの機能をテスト (特別な用途の機能)

**背景情報**  
特殊な用途の機能は、特殊なシナリオ向けの機能です。 会社アカウントだけがこれらの機能を使うことができます。 

**テストの詳細**  
アプリが次のいずれかの機能を宣言することを検証します。 
* EnterpriseAuthentication
* SharedUserCertificates
* DocumentsLibrary

これらの機能のいずれかが宣言される場合は、テストにより警告がユーザーに表示されます。 

**是正措置**  
アプリが必要としない場合は、特殊な用途の機能を削除することを検討してください。 さらに、これらの機能は、追加の登録ポリシー レビューの対象となります。

### <a name="2-app-manifest-resources-tests"></a>2. アプリ マニフェスト リソースのテスト 
#### <a name="21-app-resources-validation"></a>2.1 アプリ リソースの検証
アプリのマニフェストで宣言されている文字列や画像に誤りがある場合、そのアプリは正しくインストールされない可能性があります。 これらのエラーがあるアプリをインストールすると、アプリのロゴなどの画像が適切に表示されません。    

**テストの詳細**  
アプリ マニフェストで定義されているリソースを調べて、それらのリソースが存在し有効であることを確認します。

**是正措置**  
次の表をガイドとして使用してください。

エラー メッセージ | コメント
--------------|---------
The image {image name} defines both Scale and TargetSize qualifiers; you can define only one qualifier at a time. (イメージ {image name} には Scale 修飾子と TargetSize 修飾子が定義されていますが、一度に定義可能な修飾子は 1 つだけです。) | さまざまな解像度に合わせて画像をカスタマイズできます。 実際のメッセージでは、{imageName} にエラーの発生した画像の名前が入ります。 各画像で Scale と TargetSize のいずれかが修飾子として定義されていることを確認します。 
The image {image name} failed the size restrictions. (イメージ {image name} がサイズ制限を超えました。)  | すべてのアプリ画像が適切なサイズ制限に従っていることを確認します。 実際のメッセージでは、{imageName} にエラーの発生した画像の名前が入ります。 
The image {image name} is missing from the package. (イメージ {image name} がパッケージ内に見つかりません。)  | 必要な画像がありません。 実際のメッセージでは、{image name} に見つからない画像の名前が入ります。 
The image {image name} is not a valid image file. (イメージ {image name} は有効なイメージ ファイルではありません。)  | すべてのアプリ画像が適切なファイルの種類の制限に従っていることを確認します。 実際のメッセージでは、{image name} に画像の色として無効な値が入ります。 
The image "BadgeLogo" has an ABGR value {value} at position (x, y) that is not valid. (画像 "BadgeLogo" の位置 (x, y) の ABGR 値 {value} が無効です。) The pixel must be white (##FFFFFF) or transparent (00######) (このピクセルは、白 (##FFFFFF) または透明 (00######) である必要があります。)  | バッジ ロゴはロック画面でアプリを識別するためにバッジ通知の横に表示される画像です。 この画像はモノクロである必要があります (含めることができるのは白または透明のピクセルだけです)。 実際のメッセージでは、{value} に画像の色として無効な値が入ります。 
The image “BadgeLogo” has an ABGR value {value} at position (x, y) that is not valid for a high-contrast white image. (画像 "BadgeLogo" の位置 (x, y) にハイコントラストの白い画像には無効な ABGR 値 {value} があります。) The pixel must be (##2A2A2A) or darker, or transparent (00######). (ピクセルは (##2A2A2A) か、それより暗いか、透明 (00######) である必要があります。)  | バッジ ロゴはロック画面でアプリを識別するためにバッジ通知の横に表示される画像です。 "ハイコントラスト 白" ではバッジ ロゴが白い背景に表示されるため、通常のバッジ ロゴの濃いバージョンを使う必要があります。 "ハイコントラスト 白" でバッジ ロゴに含めることができるピクセルは、(##2A2A2A) より濃い色か透明のピクセルだけです。 実際のメッセージでは、{value} に画像の色として無効な値が入ります。 
The image must define at least one variant without a TargetSize qualifier. (画像では、TargetSize 修飾子がないバージョンが少なくとも 1 つ定義されている必要があります。) It must define a Scale qualifier or leave Scale and TargetSize unspecified, which defaults to Scale-100. (Scale 修飾子が定義されているか、または Scale と TargetSize が指定されていないままである必要があり、既定では Scale-100 です。)  | 詳しくは、[レスポンシブ デザイン](https://docs.microsoft.com/windows/uwp/layout/screen-sizes-and-breakpoints-for-responsive-design)と[アプリ リソース](https://docs.microsoft.com/en-us/windows/uwp/app-settings/store-and-retrieve-app-data)に関するガイドをご覧ください。 
The package is missing a "resources.pri" file. (パッケージに "resources.pri" ファイルがありません。)  | アプリ マニフェストにローカライズ可能なコンテンツがある場合は、アプリのパッケージに有効な resources.pri ファイルが含まれていることを確認します。 
The "resources.pri" file must contain a resource map with a name that matches the package name {package full name} ("resources.pri" ファイルには、パッケージ名 {package full name} と名前が一致するリソース マップが含まれている必要があります。)  | このエラーが表示される場合は、マニフェストが変更され、resources.pri 内のリソース マップの名前がマニフェストのパッケージ名と一致しなくなった可能性があります。 実際のメッセージでは、{package full name} には resources.pri に含まれている必要があるパッケージ名が入ります。 この問題を解決するには、resources.pri をリビルドする必要があります。その場合は、アプリのパッケージをリビルドするのが最も簡単です。 
The "resources.pri" file must not have AutoMerge enabled. ("resources.pri" ファイルは AutoMerge を有効にしないでください。)  | MakePRI.exe では、AutoMerge というオプションがサポートされています。 AutoMerge の規定値は "off" です。 オンにすると、AutoMerge が実行時にアプリの言語パックを単一の resources.pri にマージします。 これは、Microsoft Store から配布するアプリをお勧めしません。 Microsoft Store を通じて配布されるアプリの resources.pri は、アプリのパッケージのルート内にあり、アプリをサポートする言語のすべての参照を含めることが必要があります。 
The string {string} failed the max length restriction of {number} characters. (文字列 {string} が {number} 文字の最大文字数の制限を満たしていません。)  | 「[アプリ パッケージの要件](https://docs.microsoft.com/en-us/windows/uwp/publish/app-package-requirements)」をご覧ください。 実際のメッセージでは、{string} が問題の文字列に置き換わり、{number} に最大文字数が入ります。 
The string {string} must not have leading/trailing whitespace. (文字列 {string} の先頭または末尾を空白にすることはできません。)  | アプリ マニフェストの要素のスキーマでは、先頭および末尾の空白は許可されていません。 実際のメッセージでは、{string} が問題の文字列に置き換わります。 resources.pri のマニフェスト フィールドのローカライズされた値において、先頭または末尾にスペースが挿入されていないことを確認します。 
The string must be non-empty (greater than zero in length) (文字列を空にすることはできません (文字数が 0 より大きい必要があります)。)  | 詳しくは、「[アプリ パッケージの要件](https://docs.microsoft.com/en-us/windows/uwp/publish/app-package-requirements)」をご覧ください。 
There is no default resource specified in the "resources.pri" file. ("resources.pri" ファイルで指定された既定のリソースがありません。)  | 詳しくは、[アプリ リソース](https://docs.microsoft.com/en-us/windows/uwp/app-settings/store-and-retrieve-app-data)に関するガイドをご覧ください。 既定のビルド構成では、Visual Studio はバンドル生成時に 200% スケールの画像リソースのみをアプリ パッケージ内に組み込み、その他のリソースはリソース パッケージ内に配置します。 200% スケールの画像リソースを組み込むか、または持っているリソースを組み込むようにプロジェクトを構成してください。 
There is no resource value specified in the "resources.pri" file. ("resources.pri" ファイルに指定されたリソース値がありません。)  | resources.pri でアプリ マニフェストの有効なリソースが定義されていることを確認します。 
The image file {filename} must be smaller than 204800 bytes. (イメージ ファイル {filename} は、204,800 バイト未満である必要があります。)  | 指定の画像のサイズを小さくします。 
The {filename} file must not contain a reverse map section. ({filename} ファイルには、リバース マップ セクションを含めることはできません。)  | 逆マップは Visual Studio の F5 デバッグ時に makepri.exe を呼び出すと生成されますが、pri ファイルの生成時に /m パラメーターなしで makepri.exe を実行すると削除することができます。 



#### <a name="22-branding-validation"></a>2.2 ブランドの検証
**背景情報**  
デスクトップ ブリッジ アプリは、完成していて完全に機能することが期待されます。 既定の画像 (テンプレートまたは SDK サンプルの画像) を使ったアプリは、ユーザー エクスペリエンスが貧弱であることを示しているため、ストア カタログであまり識別されない可能性があります。

**テストの詳細**  
このテストは、アプリで使われている画像が SDK サンプルまたは Visual Studio の既定の画像でないことを検証します。 

**是正措置**  
既定の画像を、もっとアプリを明確に表すものに置き換えます。

### <a name="3-package-compliance-tests"></a>3.パッケージの準拠テスト
#### <a name="31-app-manifest"></a>3.1 アプリ マニフェスト
アプリ マニフェストのコンテンツをテストし、コンテンツが正しいかどうかを確認します。

**背景情報**  
アプリ マニフェストは正しい形式でなければならない

**テストの詳細**  
「[アプリ パッケージの要件](https://docs.microsoft.com/en-us/windows/uwp/publish/app-package-requirements)」の説明に従って、アプリ マニフェストを調べてコンテンツが正しいかどうかを確認します。 このテストでは、次のチェックが行われます。
* **ファイル拡張子とプロトコル**  
アプリは、関連付けることができるファイルの種類を宣言できます。 多くの一般的ではないファイルの種類を宣言すると、ユーザー エクスペリエンスが低下します。 このテストは、アプリに関連付けることができるファイル拡張子の数を制限します。
* **フレームワーク依存関係の規則**  
このテストは、アプリが UWP への適切な依存関係を宣言しているかどうかをチェックします。 不適切な依存関係がある場合は、このテストは失敗します。 アプリがターゲットとする OS のバージョンと依存関係のあるフレームワークとの間に不整合がある場合は、テストは失敗します。 アプリがフレーム ワーク DLL の "Preview" 版を参照している場合にも、テストは失敗します。
* **プロセス間通信 (IPC) 検証**  
このテストでは、デスクトップ ブリッジ アプリがデスクトップ コンポーネントとアプリ コンテナーの外側で通信しないかどうかをチェックします。 プロセス間通信は、サイドローディングが行われたアプリのみを対象としています。 `DesktopApplicationPath` と同じ名前で [**ActivatableClassAttribute**](https://docs.microsoft.com/uwp/schemas/appxpackage/appxmanifestschema/element-activatableclassattribute) を指定しているアプリは、このテストに合格しません。  

**是正措置**  
「[アプリ パッケージの要件](https://docs.microsoft.com/en-us/windows/uwp/publish/app-package-requirements)」で説明されている要件に照らして、アプリのマニフェストを確認します。


#### <a name="32-application-count"></a>3.2 アプリケーション カウント
このテストは、アプリ パッケージ (.appx、アプリ バンドル) に 1 つのアプリケーションが含まれていることを確認します。 

**背景情報**  
このテストは、ストア ポリシーに従って実装されています。 

**テストの詳細**  
このテストでは、バンドル内の .appx パッケージの合計数が 512 未満であり、バンドル内の "main" パッケージが 1 つだけであることを確認します。 また、バンドルのバージョンのリビジョン番号が 0 に設定されているかも確認します。 

**是正措置**  
アプリ パッケージとバンドルが、「**テストの詳細**」に示されている要件を満たしていることを確認します。


#### <a name="33-registry-checks"></a>3.3 レジストリ チェック
**背景情報**  
このテストでは、アプリケーションが新しいサービスやドライバーをインストールまたは更新するかどうかを確認します。

**テストの詳細**  
このテストは、registry.dat ファイル内を調べて、新しいサービスやドライバーが登録されていることを示す特定のレジストリの場所が更新されていないか確認します。 アプリがドライバーまたはサービスをインストールしようとする場合、テストは失敗します。  

**是正措置**  
エラーを確認し、必要はない場合、対象のサービスまたはドライバーを削除します。 アプリがこれらに依存している場合は、ストアに登録するには、アプリを修正する必要があります。


### <a name="4-platform-appropriate-files-test"></a>4。プラットフォーム対応ファイル テスト
混在するバイナリをインストールするアプリは、ユーザーのプロセッサ アーキテクチャによってはクラッシュしたり、正しく動作しない場合があります。 

**背景情報**  
このテストでは、アーキテクチャが競合していないか、アプリ パッケージのバイナリをスキャンします。 アプリ パッケージには、マニフェストに指定されたプロセッサ アーキテクチャで使用できないバイナリを含めることができません。 サポートされていないバイナリが含まれると、アプリがクラッシュしたり、アプリのパッケージ サイズが不必要に大きくなったりする可能性があります。 

**テストの詳細**  
アプリ パッケージのプロセッサ アーキテクチャ宣言と相互参照される場合に、各ファイルの PE ヘッダー内のビット "bitness" が適切かどうかを検証します。 

**是正措置**  
アプリ マニフェストで指定されたアーキテクチャでサポートされるファイルのみをアプリ パッケージが含むことを確認するために、次のガイドラインに従ってください。 
* アプリのターゲット プロセッサ アーキテクチャがニュートラル プロセッサ タイプの場合、アプリ パッケージは、x86、x64、または ARM のバイナリ タイプまたはイメージ タイプのファイルを含むことはできません。
* アプリのターゲット プロセッサ アーキテクチャが x86 プロセッサ タイプの場合、アプリ パッケージは、x86 バイナリ タイプまたはイメージ タイプのファイルのみを含む必要があります。 パッケージが x64 ないし ARM バイナリ形式またはイメージ形式を含む場合は、アプリはテストに合格しません。
* アプリのターゲット プロセッサ アーキテクチャが x64 プロセッサ タイプの場合、アプリ パッケージは、x64 バイナリ タイプまたはイメージ タイプのファイルを含む必要があります。 この場合は、パッケージに x86 ファイルを含めることもできますが、主なアプリ エクスペリエンスでは x64 バイナリを使ってください。 パッケージが ARM バイナリ タイプまたはイメージ タイプのファイルを含む場合、または x86 バイナリ タイプまたはイメージ タイプのファイル*のみ*を含む場合、パッケージはテストに合格しません。
* アプリのターゲット プロセッサ アーキテクチャが ARM プロセッサ タイプの場合、アプリ パッケージは、ARM バイナリ タイプまたはイメージ タイプのファイルのみを含む必要があります。 パッケージが x64 または x86 バイナリ形式またはイメージ形式のファイルを含む場合は、パッケージはテストに合格しません。 

### <a name="5-supported-api-test"></a>5。サポートされる API のテスト
アプリで非標準 API が使われていないかどうかを確認します。 

**背景情報**  
デスクトップ ブリッジ アプリでは、最新の API (UWP コンポーネント) と共に一部の従来の Win32 API を活用できます。 このテストでは、サポートされていない API を使用しているマネージ バイナリを識別します。
 
**テストの詳細**  
このテストでは、アプリ内のすべての UWP コンポーネントを確認します。
* アプリ パッケージ内の各マネージ バイナリがバイナリのインポート アドレス テーブルを調べて、UWP アプリ開発のサポートされていない Win32 API に依存関係がないことを確認します。
* アプリ パッケージ内の管理された各バイナリが承認済みのプロファイル外部の機能に依存していないことを確認します。 

**是正措置**  
この問題を修正するには、アプリが、デバッグ用ビルドとしてではなく、リリース用ビルドとしてコンパイルされていることを確認します。 

> [!NOTE]
> アプリのデバッグ ビルドは、アプリのみ使用する場合でも、このテストは失敗[UWP アプリ用 Api](https://docs.microsoft.com/uwp/)します。 UWP アプリの許可されている API ではない、存在する API を識別するためにエラー メッセージを確認します。 

> [!NOTE]
> C アプリのデバッグ構成で組み込まれている場合でも、構成は、UWP アプリ用 Windows SDK からの Api を使用するのみ、このテストは失敗します。 参照してください[UWP アプリでの Windows Api の代替](https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps)詳細についてはします。

### <a name="6-user-account-control-uac-test"></a>6。ユーザー アカウント制御 (UAC) のテスト  

**背景情報**  
アプリが実行時のユーザー アカウント制御を要求しないことを確認します。

**テストの詳細**  
アプリでは、1 つの Microsoft Store ポリシー管理者の昇格または UIAccess を要求できません。 管理者特権のセキュリティ アクセス許可はサポートされていません。 

**是正措置**  
アプリは、対話ユーザーとして実行する必要があります。 詳しくは、「[UI オートメーション セキュリティの概要](https://go.microsoft.com/fwlink/?linkid=839440)」をご覧ください。

 
### <a name="7-windows-runtime-metadata-validation"></a>7.Windows ランタイム メタデータ検証
**背景情報**  
アプリに付属するコンポーネントが、UWP 型システムに準拠していることを確認します。

**テストの詳細**  
このテストは、適切な型の使用に関連するさまざまなフラグをスローします。

**是正措置**  
* **ExclusiveTo 属性**  
UWP クラスに別の ExclusiveTo クラスとしてマークされたインターフェイスが実装されていないことを確認します。
* **一般的なメタデータの正確性**  
型の生成に使っているコンパイラが UWP の仕様に従って最新の状態になっていることを確認します。
* **[プロパティ]**  
UWP クラスのすべてのプロパティに `get` メソッドがあることを確認します (`set` メソッドは省略可能です)。 すべてのプロパティについて、`get` メソッドによって返される型が `set` メソッドの入力パラメーターの型と一致することを確認します。
* **型の場所**  
UWP のすべての型のメタデータが、アプリ パッケージで最も長い名前空間対応の名前を持つ .winmd ファイルにあることを確認します。
* **型名の大文字小文字の区別**  
すべての UWP 型のアプリ パッケージ内に大文字と小文字が区別されない一意の名前が存在することを確認します。 また、UWP 型名が、アプリ パッケージ内で名前空間名として使われていないことも確認します。
* **型名が正しいこと**  
グローバル名前空間または Windows の最上位名前空間に UWP 型がないことを確認します。
 

### <a name="8-windows-security-features-tests"></a>8.Windows セキュリティ機能のテスト
Windows 既定のセキュリティ保護を変更すると、ユーザーが危険にさらされるリスクが増大します。 

#### <a name="81-banned-file-analyzer"></a>8.1 禁止されたファイルのアナライザー
**背景情報**  
特定のファイルは、重要なセキュリティ、信頼性、その他の改善を提供するように更新されています。 以前のバージョンにはリスクがあるため、Windows デスクトップ ブリッジ アプリには、これらのファイルの最新バージョンを含める必要があります。 すべてのアプリが最新バージョンを使っていることを確実にするために、Windows アプリ認定キットでこれらのファイルをブロックします。

**テストの詳細**  
現在、Windows アプリ認定キットの禁止されたファイルのチェック機能で次のファイルの有無がチェックされます。
* *Bing.Maps.JavaScript\js\veapicore.js*  
このチェックは、通常、アプリでファイルの最新の公式リリースではなく、"Release Preview" バージョンが使われていると失敗します。 

**是正措置**  
これを修正するには、最新バージョンを使用して、 [Bing Maps SDK](https://go.microsoft.com/fwlink/p/?linkid=614880) UWP アプリ用です。

#### <a name="82-private-code-signing"></a>8.2 プライベート コードの署名
アプリ パッケージ内にプライベート コードの署名バイナリが存在するかテストします。 

**背景情報**  
プライベート コードの署名ファイルは、セキュリティが侵害された場合は、悪用される可能性があるため、プライベートにしておく必要があります。 

**テストの詳細**  
アプリ パッケージ内でプライベート署名キーを含むことを示す .pfx または .snk という拡張子を持つファイルについて確認します。 

**是正措置**  
パッケージからプライベート コードの署名キー (.pfx ファイルや .snk ファイルなど) を削除します。


## <a name="related-topics"></a>関連トピック

* [Microsoft Store ポリシー](https://docs.microsoft.com/legal/windows/agreements/store-policies)
