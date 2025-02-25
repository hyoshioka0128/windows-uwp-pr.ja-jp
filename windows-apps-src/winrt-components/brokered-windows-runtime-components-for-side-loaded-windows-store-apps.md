---
title: サイド ローディングされた UWP アプリのための Windows ランタイム コンポーネント ブローカー
description: このホワイト ペーパーでは、Windows 10 は、キーのビジネスに不可欠な運用を担う組織の既存のコードを使用するタッチ操作に .NET アプリでサポートされている企業を対象との機能について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 81b3930c-6af9-406d-9d1e-8ee6a13ec38a
ms.localizationpriority: medium
ms.openlocfilehash: a9b6c6fc7a7e3ddfab70fe289a41bb4d436e9722
ms.sourcegitcommit: ea15237291ae3ade0bf22e38bd292c3a23947a03
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66377312"
---
# <a name="brokered-windows-runtime-components-for-a-side-loaded-uwp-app"></a>サイド ローディングされた UWP アプリのための Windows ランタイム コンポーネント ブローカー

この記事では、キーのビジネスに不可欠な運用を担う組織の既存のコードを使用する .NET アプリのタッチ操作には、Windows 10 でサポートされている企業を対象との機能について説明します。

## <a name="introduction"></a>概要

>**注**  のこのホワイト ペーパーに付属するサンプル コードをダウンロードすることが [Visual Studio 2015 および 2017](https://aka.ms/brokeredsample)します。 Windows ランタイム コンポーネントの仲介型の構築に Microsoft Visual Studio テンプレートは、ここでダウンロードできます。[ユニバーサル Windows アプリの Windows 10 を対象とする visual Studio 2015 のテンプレート](https://marketplace.visualstudio.com/vsgallery/10be07b3-67ef-4e02-9243-01b78cd27935)

Windows にはと呼ばれる新しい機能が含まれています *サイドロード アプリケーション用の Windows ランタイム コンポーネントの仲介型*します。 既存のデスクトップ ソフトウェア資産を 1 つのプロセス (デスクトップ コンポーネント) 内で実行しつつ、UWP アプリからこのコードとやり取りできるようにする機能は、IPC (プロセス間通信) と呼ばれます。 これはエンタープライズ開発者には馴染みのあるモデルです。同様のマルチプロセス アーキテクチャは、データベース アプリケーションや、Windows で NT サービスを利用するアプリケーションでも使用されているためです。

アプリのサイドローディングは、この機能を構成する重要な要素です。
エンタープライズ独自のアプリケーションは、一般的なコンシューマー向け Microsoft Store に公開することはできません。各企業には、セキュリティ、プライバシー、配布、セットアップ、サービス提供に関して固有の要件があります。 したがって、サイドローディング モデルは、この機能を使うユーザーの要件であり、重要な実装の構成要素でもあります。

このアプリケーション アーキテクチャが主に対象としているのが、データ中心のアプリケーションです。 たとえば SQL Server に格納されている既存のビジネス ルールは、デスクトップ コンポーネントの共通の構成要素になります。 デスクトップ コンポーネントが提供できるのは、この種類の機能だけではありません。この機能に対する要求のほとんどが既存のデータとビジネス ロジックに関連していることは確かなことです。

.NET ランタイムおよび C の手に負えないものの侵入を最後に、指定された\#エンタープライズ開発では、この機能の言語は、.NET を使用して、UWP アプリとデスクトップ コンポーネント側の両方に重点を置いて開発されました。 付属のサンプルは C のみを示しますが他の言語とランタイムが可能ですが、UWP アプリ用、\#、し、.NET ランタイムに排他的に限定されます。

## <a name="application-components"></a>アプリケーション コンポーネント

>**注**  この機能は、.NET の使用に排他的です。 クライアント アプリとデスクトップ コンポーネントの両方が、.NET を使って作成されている必要があります。

**アプリケーション モデル**

この機能は、MVVM (モデル ビュー ビュー モデル) と呼ばれる一般的なアプリケーション アーキテクチャを中心に構築されています。 また、"モデル" は完全にデスクトップ コンポーネントに含まれると見なされます。 したがって、デスクトップ コンポーネントが "ヘッドレス" になる (UI が含まれない) ことは明らかです。 ビューは、サイドロードされたエンタープライズ アプリケーションに完全に含まれます。 このアプリケーションを "ビュー モデル" 構造で構築しなければならないという要件はありませんが、このパターンを使うのが一般的とされます。

**デスクトップ コンポーネント**

この機能のデスクトップ コンポーネントは、この機能の一部として導入された新しい種類のアプリケーションです。 このデスクトップ コンポーネントは、C でのみ記述できます\#と Windows 10 用 .NET 4.6 以降をターゲットする必要があります。 プロジェクトの種類は、UWP をターゲットとする CLR のハイブリッドで、プロセス間通信の形式は UWP の型とクラスで構成されます。一方、デスクトップ コンポーネントは、.NET ランタイム クラス ライブラリのすべてを呼び出すことができます。 Visual Studio プロジェクトに対する影響については、後で詳しく説明します。 このハイブリッド構成により、デスクトップ コンポーネントに構築されたアプリケーションとの間で UWP の型をマーシャリングしながら、デスクトップ CLR コードをデスクトップ コンポーネントの実装内で呼び出すことができます。

**コントラクト**

サイドロード アプリケーションとデスクトップ コンポーネントの間のコントラクトは、UWP 型システムの観点から記述されます。 1 つ以上の C を宣言する必要があります\#UWP を表すことのできるクラス。 MSDN のトピックを参照してください。 [C での Windows ランタイム コンポーネントの作成\#および Visual Basic](https://docs.microsoft.com/previous-versions/windows/apps/br230301(v=vs.140)) C を使用して Windows ランタイム クラスの作成の特定の要件を\#します。

>**注**  デスクトップ コンポーネントとサイド ロードはアプリケーション間での Windows ランタイム コンポーネントのコントラクトでは、列挙型はサポートされていません。

**アプリケーションのサイドロード**

サイドロード アプリケーションは、Microsoft Store 経由でインストールされるのではなくサイドロードされるという 1 点を除けば、あらゆる点で通常の UWP アプリと変わりません。 インストール メカニズムのほとんどは同じであり、マニフェストとアプリケーションのパッケージも似ています (マニフェストには追加点が 1 つありますが、これについては後で詳しく説明します)。 いったんサイドローディングを有効にしたら、簡単な PowerShell スクリプトで、必要な証明書とアプリケーション自体をインストールできます。 一般的なベスト プラクティスとして、サイドロード アプリケーションでは、Visual Studio の [プロジェクト] メニューの [ストア] に含まれる WACK 認定テストを実行することをお勧めします。

>**注** サイドローディングできますで有効にする設定には、&gt;更新とセキュリティ -&gt;開発者向け。

重要な点として、Windows 10 に搭載されているアプリ ブローカー メカニズムは 32 ビット専用であることに注意が必要です。 デスクトップ コンポーネントは 32 ビットである必要があります。
サイドロード アプリケーションは 64 ビットにできますが (64 ビットと 32 ビットの両方のプロキシが登録されている場合)、これは特殊なアプリケーションになります。 C でのサイド ロード アプリケーションを構築\#自然"neutral"標準的な構成と、「32 ビットを優先」の既定を使用して、32 ビットのサイド ロード アプリケーションを作成します。

**サーバーのインスタンス化および Appdomain**

サイドロードされたアプリケーションはそれぞれ、アプリ ブローカー サーバーの独自のインスタンスを受け取ります (いわゆる "マルチインスタンス化" が行われます)。 サーバー コードは、1 つの AppDomain 内で実行されます。 これにより、複数のバージョンのライブラリを個別のインスタンスで実行できます。 たとえば、アプリケーション A には V1.1 のコンポーネントが必要で、アプリケーション B には V2 が必要であるとします。 これを明確に区別するには、V1.1 コンポーネントと V2 コンポーネントをそれぞれ別のサーバー ディレクトリに分けて、各アプリケーションが、必要なバージョンをサポートするサーバーに接続するように指定します。

サーバー コードの実装を複数のアプリ ブローカー サーバー インスタンスで共有するには、複数のアプリケーションが同じサーバー ディレクトリに接続するように指定します。 それでもアプリ ブローカー サーバーのインスタンスは複数存在することになりますが、各インスタンスでは同じコードが実行されます。 1 つのアプリケーションで使われる実装コンポーネントはすべて、同じパスに存在する必要があります。

## <a name="defining-the-contract"></a>コントラクトの定義

この機能を使ってアプリケーションを作成するには、まず、サイドロード アプリケーションとデスクトップ コンポーネントの間のコントラクトを作成します。 これは、Windows ランタイム型だけを使用して行う必要があります。
さいわい、これらは C を使用して宣言する簡単な\#クラス。 ただし、このような通信を定義するときは、パフォーマンスについて考慮することが重要です。これについては後で説明します。

コントラクトを定義する流れは次のようになります。

**手順 1:** Visual Studio で新しいクラス ライブラリを作成します。 プロジェクトの作成時には、Windows ランタイム コンポーネント テンプレートではなく、クラス ライブラリ テンプレートを使います。

この後には実装が続きますが、このセクションでは、プロセス間のコントラクトの定義についてのみ説明します。 関連するサンプルには次のクラス (EnterpriseServer.cs) が含まれ、先頭部分は次のようになっています。

```csharp
namespace Fabrikam
{
    public sealed class EnterpriseServer
    {

        public ILis<String> TestMethod(String input)
        {
            throw new NotImplementedException();
        }
        
        public IAsyncOperation<int> FindElementAsync(int input)
        {
            throw new NotImplementedException();
        }
        
        public string[] RetrieveData()
        {
            throw new NotImplementedException();
        }
        
        public event EventHandler<string> PeriodicEvent;
    }
}
```

これにより、サイドロード アプリケーションからインスタンス化できる "EnterpriseServer" クラスが定義されます。 このクラスは、RuntimeClass で保障された機能を提供します。 RuntimeClass は、サイドロード アプリケーションに含める参照用の winmd を生成するために使用できます。

**手順 2:** Windows ランタイム コンポーネントにプロジェクトの出力の種類を変更するには、手動でプロジェクト ファイルを編集します。

これを Visual Studio で実行するには、新しく作成されたプロジェクトを右クリックし、[プロジェクトのアンロード] を選択します。もう一度右クリックし、[Edit EnterpriseServer.csproj の編集] を選択して、プロジェクト ファイル (XML ファイル) を編集用に開きます。

ファイルを開いたときに検索、 \<OutputType\>タグし、その値を"winmdobj"に変更します。

**手順 3:** Windows「参照」を作成するビルド規則を作成するメタデータ ファイル (.winmd ファイル)。 つまり、実装は含まれません。

**手順 4:** 「実装」Windows メタデータ ファイルを作成、つまり、同じメタデータ情報も実装が含まれますビルド規則を作成します。

これは次のスクリプトによって実行されます。 プロジェクトの **[プロパティ]**  >  **[ビルド イベント]** で、ビルド後のイベントのコマンド ラインにこれらのスクリプトを追加します。

> **注** このスクリプトは、ターゲットとする Windows のバージョン (Windows 10) と、使用中の Visual Studio のバージョンによって異なります。

**Visual Studio 2015**
```cmd
    call "$(DevEnvDir)..\..\vc\vcvarsall.bat" x86 10.0.14393.0

    md "$(TargetDir)"\impl    md "$(TargetDir)"\reference

    erase "$(TargetDir)\impl\*.winmd"
    erase "$(TargetDir)\impl\*.pdb"
    rem erase "$(TargetDir)\reference\*.winmd"

    xcopy /y "$(TargetPath)" "$(TargetDir)impl"
    xcopy /y "$(TargetDir)*.pdb" "$(TargetDir)impl"

    winmdidl /nosystemdeclares /metadata_dir:C:\Windows\System32\Winmetadata "$(TargetPath)"

    midl /metadata_dir "%WindowsSdkDir%UnionMetadata" /iid "$(SolutionDir)BrokeredProxyStub\$(TargetName)_i.c" /env win32 /x86 /h   "$(SolutionDir)BrokeredProxyStub\$(TargetName).h" /winmd "$(TargetName).winmd" /W1 /char signed /nologo /winrt /dlldata "$(SolutionDir)BrokeredProxyStub\dlldata.c" /proxy "$(SolutionDir)BrokeredProxyStub\$(TargetName)_p.c"  "$(TargetName).idl"
    mdmerge -n 1 -i "$(ProjectDir)bin\$(ConfigurationName)" -o "$(TargetDir)reference" -metadata_dir "%WindowsSdkDir%UnionMetadata" -partial

    rem erase "$(TargetPath)"

```


**Visual Studio 2017**
```cmd
    call "$(DevEnvDir)..\..\vc\auxiliary\build\vcvarsall.bat" x86 10.0.16299.0

    md "$(TargetDir)"\impl
    md "$(TargetDir)"\reference

    erase "$(TargetDir)\impl\*.winmd"
    erase "$(TargetDir)\impl\*.pdb"
    rem erase "$(TargetDir)\reference\*.winmd"

    xcopy /y "$(TargetPath)" "$(TargetDir)impl"
    xcopy /y "$(TargetDir)*.pdb" "$(TargetDir)impl"

    winmdidl /nosystemdeclares /metadata_dir:C:\Windows\System32\Winmetadata "$(TargetPath)"

    midl /metadata_dir "%WindowsSdkDir%UnionMetadata" /iid "$(SolutionDir)BrokeredProxyStub\$(TargetName)_i.c" /env win32 /x86 /h "$(SolutionDir)BrokeredProxyStub\$(TargetName).h" /winmd "$(TargetName).winmd" /W1 /char signed /nologo /winrt /dlldata "$(SolutionDir)BrokeredProxyStub\dlldata.c" /proxy "$(SolutionDir)BrokeredProxyStub\$(TargetName)_p.c"  "$(TargetName).idl"
    mdmerge -n 1 -i "$(ProjectDir)bin\$(ConfigurationName)" -o "$(TargetDir)reference" -metadata_dir "%WindowsSdkDir%UnionMetadata" -partial

    rem erase "$(TargetPath)"
```

参照用の **winmd** が (プロジェクトのターゲット フォルダーの "reference" フォルダーに) 作成されると、それを使用するサイドロード アプリケーションに手動で転送 (コピー) され、参照されます。 これについては、次のセクションで詳しく説明します。 上のビルド規則で使われているプロジェクト構造では、混乱を避けるために、実装用と参照用の **winmd** はビルド階層内の別々のディレクトリに明確に分離されます。

## <a name="side-loaded-applications-in-detail"></a>サイドロード アプリケーションの詳細
既に説明したとおり、サイドロード アプリケーションは他の UWP アプリと同じようにビルドされますが、追加の作業が 1 つあります。つまり、サイドロード アプリケーションのマニフェストで、RuntimeClass の利用を宣言する必要があります。 これにより、アプリケーションでは、new 演算子を記述するだけでデスクトップ コンポーネントの機能にアクセスできるようになります。 <Extension> セクション内の新しいマニフェスト エントリに、デスクトップ コンポーネントで実装される RuntimeClass とその場所に関する情報を記述します。 これらを宣言するアプリケーション マニフェスト内のコンテンツは、Windows 10 をターゲットとするアプリと同じです。 例:

```XML
<Extension Category="windows.activatableClass.inProcessServer">
    <InProcessServer>
        <Path>clrhost.dll</Path>
        <ActivatableClass ActivatableClassId="Fabrikam.EnterpriseServer" ThreadingModel="both">
            <ActivatableClassAttribute Name="DesktopApplicationPath" Type="string" Value="c:\test" />
        </ActivatableClass>
    </InProcessServer>
</Extension>
```

カテゴリは inProcessServer です。outOfProcessServer カテゴリには、このアプリケーション構成に適用できないエントリが複数あるためです。 なお、<Path>コンポーネントは clrhost.dll 常を含める必要が (ただしこれは **いない** 適用され、別の値を指定することは、未定義の方法では失敗)。

<ActivatableClass> セクションは、アプリ パッケージ内の Windows ランタイム コンポーネントによって優先される実際のインプロセス RuntimeClass と同じです。 <ActivatableClassAttribute> 新しい要素と属性名 ="DesktopApplicationPath"、種類 ="string"は必須およびインバリアントします。 Value 属性では、デスクトップ コンポーネントの実装用の winmd の場所を指定します (詳しくは、次のセクションを参照)。 デスクトップ コンポーネントによって優先される各 RuntimeClass には、独自の <ActivatableClass> 要素ツリーが必要です。 ActivatableClassId は、RuntimeClass の完全な名前空間修飾名と一致する必要があります。

「コントラクトの定義」で説明したように、プロジェクトの参照先は、デスクトップ コンポーネントの参照用の winmd にする必要があります。 Visual Studio のプロジェクト システムでは、通常、同じ名前で 2 レベルのディレクトリ構造が作成されます。 サンプルでは EnterpriseIPCApplication\\EnterpriseIPCApplication します。 参照**winmd** この 2 番目のレベルのディレクトリとし、ダイアログ ボックスを使用するプロジェクト参照を手動でコピーされます (をクリックして、 **参照..**  ボタン) を見つけて、この参照**winmd**します。 完了すると、デスクトップ コンポーネントの最上位の名前空間 (たとえば Fabrikam) が、プロジェクトの [参照] 部分の最上位ノードとして表示されます。

>**注**を使用する非常に重要ですが、 **winmd を参照** サイドロード アプリケーションで。 誤って経由で実行する場合、 **実装 winmd** サイド ロード アプリのディレクトリとリファレンスを受け取ることになります「IStringable を見つけることができません」に関連したエラー。 これは、いずれかを確認する署名間違った **winmd** が参照されています。 ビルド後ルールは、IPC サーバー アプリケーション (次のセクションで詳しく説明) 慎重に分離これら 2 つ **winmd** 別々 のディレクトリにします。

環境変数 (特に %programfiles%)使用できる<ActivatableClassAttribute Value="path">します。前述のように、ブローカー アプリのみをサポート 32 ビット %programfiles% は c: を解決するため\\Program Files (x86) 場合は、アプリケーションは 64 ビット OS で実行します。

## <a name="desktop-ipc-server-detail"></a>デスクトップ IPC サーバーの詳細

前の 2 つのセクションは、クラスの宣言と参照を輸送するためのメカニズムについて説明します。 **winmd** サイドロード アプリケーション プロジェクトへです。 デスクトップ コンポーネント側の残りの作業は、ほとんどが実装にかかわるものです。 デスクトップ コンポーネントで肝心なのは、デスクトップ コードを呼び出せるようにするという点です (通常は、既にあるコード資産を再利用するのが目的)。このため、プロジェクトは、特別な方法で構成する必要があります。
通常、.NET を使う Visual Studio プロジェクトでは、2 つの "プロファイル" のいずれかが使われます。
1 つはデスクトップ用プロファイル (".NetFramework")、もう 1 つは CLR の UWP アプリ部分をターゲットとするプロファイル (".NetCore") です。 この機能のデスクトップ コンポーネントは、この 2 つのハイブリッドです。 その結果、参照セクションは、これら 2 つのプロファイルがうまく調和するように注意深く構成されます。

通常の UWP アプリ プロジェクトでは、Windows ランタイム API サーフェス全体が暗黙的に含まれるため、明示的なプロジェクト参照は含まれません。
通常は、他のプロジェクト間でのみ参照が行われます。 これに対してデスクトップ コンポーネント プロジェクトには、きわめて特殊な一連の参照が含まれます。 開始として、"クラシック デスクトップ\\クラス ライブラリ"プロジェクトであるため、デスクトップ プロジェクトをします。 Windows ランタイム API を明示的に参照 (への参照を使用して **winmd** ファイル) できるようにする必要があります。 次に示すように、適切な参照を追加します。

```XML
<ItemGroup>
    <!-- These reference are added by VS automatically when you create a Class Library project-->
    <Reference Include="System" />
    <Reference Include="System.Core" />
    <Reference Include="System.Xml.Linq" />
    <Reference Include="System.Data.DataSetExtensions" />
    <Reference Include="Microsoft.CSharp" />
    <Reference Include="System.Data" />
    <Reference Include="System.Net.Http" />
<Reference Include="System.Xml" />
    <!-- These reference should be added manually by editing .csproj file-->

    <Reference Include="System.Runtime.WindowsRuntime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089, processorArchitecture=MSIL">
      <HintPath>$(MSBuildProgramFiles32)\Microsoft SDKs\NETCoreSDK\System.Runtime.WindowsRuntime\4.0.10\lib\netcore50\System.Runtime.WindowsRuntime.dll</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows">
      <HintPath>$(MSBuildProgramFiles32)\Windows Kits\10\UnionMetadata\Facade\Windows.WinMD</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Foundation.FoundationContract">
      <HintPath>$(MSBuildProgramFiles32)\Windows Kits\10\References\Windows.Foundation.FoundationContract\1.0.0.0\Windows.Foundation.FoundationContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Foundation.UniversalApiContract">
      <HintPath>$(MSBuildProgramFiles32)\Windows Kits\10\References\Windows.Foundation.UniversalApiContract\1.0.0.0\Windows.Foundation.UniversalApiContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Networking.Connectivity.WwanContract">
      <HintPath>$(MSBuildProgramFiles32)\Windows Kits\10\References\Windows.Networking.Connectivity.WwanContract\1.0.0.0\Windows.Networking.Connectivity.WwanContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Activation.ActivatedEventsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Activation.ActivatedEventsContract\1.0.0.0\Windows.ApplicationModel.Activation.ActivatedEventsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Activation.ActivationCameraSettingsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Activation.ActivationCameraSettingsContract\1.0.0.0\Windows.ApplicationModel.Activation.ActivationCameraSettingsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Activation.ContactActivatedEventsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Activation.ContactActivatedEventsContract\1.0.0.0\Windows.ApplicationModel.Activation.ContactActivatedEventsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Activation.WebUISearchActivatedEventsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Activation.WebUISearchActivatedEventsContract\1.0.0.0\Windows.ApplicationModel.Activation.WebUISearchActivatedEventsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Background.BackgroundAlarmApplicationContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Background.BackgroundAlarmApplicationContract\1.0.0.0\Windows.ApplicationModel.Background.BackgroundAlarmApplicationContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Calls.LockScreenCallContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Calls.LockScreenCallContract\1.0.0.0\Windows.ApplicationModel.Calls.LockScreenCallContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Resources.Management.ResourceIndexerContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Resources.Management.ResourceIndexerContract\1.0.0.0\Windows.ApplicationModel.Resources.Management.ResourceIndexerContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Search.Core.SearchCoreContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Search.Core.SearchCoreContract\1.0.0.0\Windows.ApplicationModel.Search.Core.SearchCoreContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Search.SearchContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Search.SearchContract\1.0.0.0\Windows.ApplicationModel.Search.SearchContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.ApplicationModel.Wallet.WalletContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.ApplicationModel.Wallet.WalletContract\1.0.0.0\Windows.ApplicationModel.Wallet.WalletContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Devices.Custom.CustomDeviceContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Devices.Custom.CustomDeviceContract\1.0.0.0\Windows.Devices.Custom.CustomDeviceContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Devices.Portable.PortableDeviceContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Devices.Portable.PortableDeviceContract\1.0.0.0\Windows.Devices.Portable.PortableDeviceContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Devices.Printers.Extensions.ExtensionsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Devices.Printers.Extensions.ExtensionsContract\1.0.0.0\Windows.Devices.Printers.Extensions.ExtensionsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Devices.Printers.PrintersContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Devices.Printers.PrintersContract\1.0.0.0\Windows.Devices.Printers.PrintersContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Devices.Scanners.ScannerDeviceContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Devices.Scanners.ScannerDeviceContract\1.0.0.0\Windows.Devices.Scanners.ScannerDeviceContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Devices.Sms.LegacySmsApiContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Devices.Sms.LegacySmsApiContract\1.0.0.0\Windows.Devices.Sms.LegacySmsApiContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Gaming.Preview.GamesEnumerationContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Gaming.Preview.GamesEnumerationContract\1.0.0.0\Windows.Gaming.Preview.GamesEnumerationContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Globalization.GlobalizationJapanesePhoneticAnalyzerContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Globalization.GlobalizationJapanesePhoneticAnalyzerContract\1.0.0.0\Windows.Globalization.GlobalizationJapanesePhoneticAnalyzerContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Graphics.Printing3D.Printing3DContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Graphics.Printing3D.Printing3DContract\1.0.0.0\Windows.Graphics.Printing3D.Printing3DContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Management.Deployment.Preview.DeploymentPreviewContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Management.Deployment.Preview.DeploymentPreviewContract\1.0.0.0\Windows.Management.Deployment.Preview.DeploymentPreviewContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Management.Workplace.WorkplaceSettingsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Management.Workplace.WorkplaceSettingsContract\1.0.0.0\Windows.Management.Workplace.WorkplaceSettingsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Media.Capture.AppCaptureContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Media.Capture.AppCaptureContract\1.0.0.0\Windows.Media.Capture.AppCaptureContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Media.Capture.CameraCaptureUIContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Media.Capture.CameraCaptureUIContract\1.0.0.0\Windows.Media.Capture.CameraCaptureUIContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Media.Devices.CallControlContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Media.Devices.CallControlContract\1.0.0.0\Windows.Media.Devices.CallControlContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Media.MediaControlContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Media.MediaControlContract\1.0.0.0\Windows.Media.MediaControlContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Media.Playlists.PlaylistsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Media.Playlists.PlaylistsContract\1.0.0.0\Windows.Media.Playlists.PlaylistsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Media.Protection.ProtectionRenewalContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Media.Protection.ProtectionRenewalContract\1.0.0.0\Windows.Media.Protection.ProtectionRenewalContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Networking.NetworkOperators.LegacyNetworkOperatorsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Networking.NetworkOperators.LegacyNetworkOperatorsContract\1.0.0.0\Windows.Networking.NetworkOperators.LegacyNetworkOperatorsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Networking.Sockets.ControlChannelTriggerContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Networking.Sockets.ControlChannelTriggerContract\1.0.0.0\Windows.Networking.Sockets.ControlChannelTriggerContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Security.EnterpriseData.EnterpriseDataContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Security.EnterpriseData.EnterpriseDataContract\1.0.0.0\Windows.Security.EnterpriseData.EnterpriseDataContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Security.ExchangeActiveSyncProvisioning.EasContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Security.ExchangeActiveSyncProvisioning.EasContract\1.0.0.0\Windows.Security.ExchangeActiveSyncProvisioning.EasContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Services.Maps.GuidanceContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Services.Maps.GuidanceContract\1.0.0.0\Windows.Services.Maps.GuidanceContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Services.Maps.LocalSearchContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Services.Maps.LocalSearchContract\1.0.0.0\Windows.Services.Maps.LocalSearchContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.System.Profile.SystemManufacturers.SystemManufacturersContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.System.Profile.SystemManufacturers.SystemManufacturersContract\1.0.0.0\Windows.System.Profile.SystemManufacturers.SystemManufacturersContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.System.Profile.ProfileHardwareTokenContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.System.Profile.ProfileHardwareTokenContract\1.0.0.0\Windows.System.Profile.ProfileHardwareTokenContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.System.Profile.ProfileRetailInfoContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.System.Profile.ProfileRetailInfoContract\1.0.0.0\Windows.System.Profile.ProfileRetailInfoContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.System.UserProfile.UserProfileContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.System.UserProfile.UserProfileContract\1.0.0.0\Windows.System.UserProfile.UserProfileContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.System.UserProfile.UserProfileLockScreenContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.System.UserProfile.UserProfileLockScreenContract\1.0.0.0\Windows.System.UserProfile.UserProfileLockScreenContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.UI.ApplicationSettings.ApplicationsSettingsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.UI.ApplicationSettings.ApplicationsSettingsContract\1.0.0.0\Windows.UI.ApplicationSettings.ApplicationsSettingsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.UI.Core.AnimationMetrics.AnimationMetricsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.UI.Core.AnimationMetrics.AnimationMetricsContract\1.0.0.0\Windows.UI.Core.AnimationMetrics.AnimationMetricsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.UI.Core.CoreWindowDialogsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.UI.Core.CoreWindowDialogsContract\1.0.0.0\Windows.UI.Core.CoreWindowDialogsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.UI.Xaml.Hosting.HostingContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.UI.Xaml.Hosting.HostingContract\1.0.0.0\Windows.UI.Xaml.Hosting.HostingContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
    <Reference Include="Windows.Web.Http.Diagnostics.HttpDiagnosticsContract">
      <HintPath>$(MsBuildProgramFiles32)\Windows Kits\10\References\Windows.Web.Http.Diagnostics.HttpDiagnosticsContract\1.0.0.0\Windows.Web.Http.Diagnostics.HttpDiagnosticsContract.winmd</HintPath>
      <Private>False</Private>
    </Reference>
</ItemGroup>
```

上の参照では、このハイブリッド サーバーを適切に動作させるために欠かせない参照が慎重に組み合わされています。 手順としては、(プロジェクトの OutputType を編集する手順で説明したように) .csproj ファイルを開き、これらの参照を必要に応じて追加します。

参照が適切に構成されたら、次は、サーバーの機能を実装する必要があります。 MSDN のトピックを参照してください。 [Windows ランタイム コンポーネントとの相互運用のためのベスト プラクティス (C を使用して UWP アプリ\##/vb/c C++ および XAML)](https://docs.microsoft.com/previous-versions/windows/apps/hh750311(v=win.10))します。
この作業では、実装の一部として、デスクトップ コードを呼び出すことができる Windows ランタイム コンポーネント dll を作成します。 関連するサンプルには、Windows ランタイムで使われる主なパターンが含まれます。

-   メソッド呼び出し

-   デスクトップ コンポーネントによる Windows ランタイム イベント ソース

-   Windows ランタイムの非同期操作

-   基本的な種類の配列を返す

**インストール**

アプリをインストールするには、実装をコピー **winmd** に関連付けられているサイドロード アプリケーションのマニフェストで指定された適切なディレクトリ:<ActivatableClassAttribute>の値"path"=。 また、関連付けられているすべてのサポート ファイルと、プロキシ/スタブ dll もコピーします (後者については後で詳しく説明します)。 実装のコピーが失敗する **winmd** サーバー ディレクトリの場所は、すべてのサイド ロード、RuntimeClass 上に新しいアプリケーションの呼び出し「クラスは登録されていません」エラーがスローされます。 プロキシ/スタブをインストールできない (または登録できない) 場合は、すべての呼び出しが戻り値なしで失敗します。 この後者のエラーが頻繁に **いない** 表示されている例外に関連付けられています。
この構成エラーが原因で発生する例外は、"無効なキャスト" を参照する可能性があります。

**サーバーの実装に関する考慮事項**

デスクトップ Windows ランタイム サーバーは、"ワーカー" または "タスク" に基づいていると考えることができます。 サーバーへのすべての呼び出しが UI スレッド以外で動作し、すべてのコードがマルチスレッドに対して安全である必要があります。 また、サイドロード アプリケーションのどの部分が、サーバーの機能を呼び出してしているかも重要です。 サイドロード アプリケーションでは、実行に時間のかかるコードを UI スレッドから呼び出すことは必ず避けてください。 それには、主に次の 2 つの方法があります。

1.  UI スレッドからサーバーの機能を呼び出す場合、サーバーの公開サーフェス領域および実装では必ず非同期パターンを使います。

2.  サイドロード アプリケーションのバックグラウンド スレッドからサーバーの機能を呼び出します。

**サーバーで Windows ランタイムの非同期**

アプリケーション モデルのプロセス間通信の特性を考えると、サーバーを呼び出す場合のオーバーヘッドは、イン プロセスで占有的に実行されるコードよりも大きくなります。 一般的に、インメモリの値を返す単純なプロパティを呼び出す操作はすばやく実行できて安全なのは、UI スレッドをブロックする心配がないからです。 ただし、どのような種類でも I/O がかかわる呼び出しは (すべてのファイル処理やデータベース検索を含む)、UI スレッドの呼び出しをブロックする可能性があり、無応答が原因でアプリケーションが停止することがあります。 さらに、オブジェクトに対するプロパティの呼び出しは、パフォーマンス上の理由から、アプリケーション アーキテクチャとしてはお勧めできません。
これについては、次のセクションで詳しく説明します。

適切に実装されたサーバーでは、通常、Windows ランタイム非同期パターンを使って、UI スレッドから直接行われた呼び出しが実装されます。 これは、次のパターンに従って実装できます。 まずは、宣言です (ここでも、関連するサンプルから)。

```csharp
public IAsyncOperation<int> FindElementAsync(int input)
```

これは整数を返す Windows ランタイム非同期操作を宣言します。
非同期操作の実装は、通常、次のような形になります。

```csharp
return Task<int>.Run( () =>
{
    int retval = ...
    // execute some potentially long-running code here 
}).AsAsyncOperation<int>();

```

>**注** この実装では、実行に時間がかかる可能性のある他の操作を待機するのが一般的です。 そうである場合、 **Task.Run** コードを宣言する必要があります。

```csharp
return Task<int>.Run(async () =>
{
    int retval = ...
    // execute some potentially long-running code here 
    await ... // some other WinRT async operation or Task
}).AsAsyncOperation<int>();
```

この非同期メソッドのクライアントは、他の Windows ランタイム非同期操作と同じようにこの操作を待つことができます。

**アプリケーションのバック グラウンド スレッドからサーバー機能を呼び出す**

通常、クライアントとサーバーは両方とも同じ組織によって作成されるため、サーバーへのすべての呼び出しをサイドロード アプリケーションのバックグラウンド スレッドから行うというプログラミング手法を採用できます。 サーバーから 1 つ以上のバッチ データを収集する呼び出しは、バックグラウンド スレッドから直接行うことができます。 結果の取得が完了したら、アプリケーション プロセスのインメモリにあるバッチ データは、一般的に UI スレッドから直接取得できます。 C\#オブジェクトは、当然ながら、バック グラウンドのスレッド間でアジャイルと UI スレッドはため、このような呼び出しパターンに特に便利です。

## <a name="creating-and-deploying-the-windows-runtime-proxy"></a>Windows ランタイム プロキシの作成と展開

IPC アプローチには 2 つのプロセス間の Windows ランタイム インターフェイスのマーシャリングが伴うため、グローバルに登録された Windows ランタイム プロキシとスタブを使う必要があります。

**Visual Studio でのプロキシの作成**

作成および登録プロキシとスタブは、通常の UWP アプリ パッケージ内部で使用するプロセスは、トピックで説明されて [Windows ランタイム コンポーネントのイベントの発生](https://docs.microsoft.com/previous-versions/windows/apps/dn169426(v=vs.140))します。
この記事で説明されている手順には、アプリケーション パッケージ内でのプロキシ/スタブの登録プロセスが含まれているため、次に示すプロセスよりも複雑です (グローバル登録とは異なります)。

**手順 1:** デスクトップ コンポーネント プロジェクトのソリューションを使用して、Visual Studio でプロキシ/スタブ プロジェクトを作成します。

**ソリューション > 追加 > プロジェクト > Visual C > Win32 コンソールの DLL の選択オプション。**

次の手順では、前提としています、サーバー コンポーネントと呼びます **MyWinRTComponent**します。

**手順 3:** プロジェクトからすべての CPP/H ファイルを削除します。

**手順 4:** 前のセクションでは、「コントラクトを定義する」には、実行するビルド後コマンドが含まれています。 **winmdidl.exe**、 **midl.exe**、 **mdmerge.exe**など。 このビルド後のコマンドの midl 手順による出力の 1 つから、次の 4 つの重要な出力が生成されます。

a) Dlldata.c

b) ヘッダー ファイル (例: MyWinRTComponent.h)

c) A \* \_i.c ファイル (例: MyWinRTComponent\_i.c)

d) A \* \_p.c ファイル (例: MyWinRTComponent\_p.c)

**手順 5:** これら 4 つの生成されたファイルを"MyWinRTProxy"プロジェクトに追加します。

**手順 6:** Def ファイルを"MyWinRTProxy"プロジェクトに追加 **(プロジェクト > 新しい項目の追加 > コード > モジュール定義ファイル**) とする内容を更新します。

LIBRARY MyWinRTComponent.Proxies.dll

EXPORTS

DllCanUnloadNow PRIVATE

DllGetClassObject PRIVATE

DllRegisterServer PRIVATE

DllUnregisterServer PRIVATE

**手順 7:** "MyWinRTProxy"プロジェクトのプロパティを開きます。

**構成プロパティ > [全般] > ターゲット名。**

MyWinRTComponent.Proxies

**[C/C++] > プリプロセッサの定義 > の追加**

"WIN32;\_WINDOWS;登録\_プロキシ\_DLL"

**[C/C++] > プリコンパイル済みヘッダー。「プリコンパイル済みヘッダーを使用していない」を選択します。**

**リンカー > [全般] > インポート ライブラリの無視します。[はい] を選択します。**

**リンカー > の入力 > 追加の依存関係。Rpcrt4.lib;runtimeobject.lib を追加します。**

**リンカー > Windows メタデータ > Windows メタデータを生成します。[いいえ] を選択します。**

**手順 8:** "MyWinRTProxy"プロジェクトをビルドします。

**プロキシの展開**

プロキシは、グローバルに登録する必要があります。 最も簡単にこれを行うには、インストール プロセスによってプロキシ dll の DllRegisterServer が呼び出されるようにします。 この機能でサポートされるのは x86 用に構築されたサーバーだけなので (つまり 64 ビットはサポートされません)、最もシンプルな構成は、32 ビットのサーバー、32 ビットのプロキシ、32 ビットのサイドロード アプリケーションを使った構成となります。 プロキシは、通常、デスクトップ コンポーネントの実装用の **winmd** と一緒に設置されます。

追加の構成手順を 1 つ実行する必要があります。 サイドロード プロセスでプロキシを読み込んで実行できるようにうするには、ディレクトリが ALL_APPLICATION_PACKAGES に対して "読み取りと実行" としてマークされている必要があります。 これを行うには、**icacls.exe** コマンド ライン ツールを使います。 次のコマンドを、実装用の **winmd** とプロキシ/スタブ dll が存在するディレクトリで実行する必要があります。

*icacls します。/T/grant \*S-1-15-2-1:RX*

## <a name="patterns-and-performance"></a>パターンとパフォーマンス

プロセス間のトランスポートのパフォーマンスを慎重に監視することは、非常に重要です。 プロセス間の呼び出しのコストは、インプロセスの呼び出しの 2 倍以上です。 プロセス間で "頻繁な" 会話をしたり、ビットマップ イメージなどの大きなオブジェクトを繰り返し転送したりすると、アプリケーションのパフォーマンスが予想外に低下し、問題が生じることがあります。

次の点を考慮してください。

-   アプリケーションの UI スレッドからサーバーへの同期メソッド呼び出しは常に避けます。 メソッドをアプリケーションのバックグラウンド スレッドから呼び出し、必要に応じて CoreWindowDispatcher を使って、結果を UI スレッドに提供します。

-   アプリケーションの UI スレッドからの非同期操作の呼び出しは安全ですが、次に説明するパフォーマンス上の問題を考慮してください。

-   結果のバルク転送により、プロセス間の対話が減ります。 これは通常、Windows ランタイム配列を使って処理されます。

-   返す *一覧<T>*  場所 *T* 非同期操作またはプロパティのフェッチのオブジェクトは、多数のプロセス間の頻繁な通信が発生します。 たとえば、戻る、*一覧&lt;人&gt;*  オブジェクト。 このとき、各反復パスがプロセス間呼び出しになります。 各 *人* 返されるオブジェクトは、プロキシと各メソッドの呼び出しで表されるまたはプロセス間呼び出しでその個々 のオブジェクトのプロパティになります。 ように「無害」 *一覧&lt;人&gt;*  オブジェクト、 *数* が大きい低速な呼び出しの数が多いと。 パフォーマンスを改善するには、コンテンツの構造体を配列に格納してバルク転送します。 次に、例を示します。

```csharp
struct PersonStruct
{
    String LastName;
    String FirstName;
    int Age;
   // etc.
}
```

返された場合 * PersonStruct\[\]* の代わりに*一覧&lt;PersonObject&gt;* します。
これにより、プロセス間の "ホップ" を 1 回に抑えてすべてのデータを取得できます。

パフォーマンスに関する他のあらゆる考慮事項と同様に、ここでも測定とテストが重要になります。 利用統計情報をさまざまな操作に挿入して、所要時間を判断することをお勧めします。 幅広く測定することが重要です。たとえば、サイドロード アプリケーションで、特定のクエリに対してすべての *People* オブジェクトを処理するには実際にどれくらいの時間がかかるかを測定します。

変数読み込みテストという手法もあります。 これを行うには、パフォーマンス テストのフックを、変数遅延の負荷をサーバー処理に組み込むアプリケーションに挿入します。 これによりさまざまな負荷と、さまざまなサーバー パフォーマンスに対するアプリケーションの反応をシミュレートできます。
サンプルは、適切な非同期手法を使って時間の遅延をコードに挿入する方法を示しています。 挿入する正確な遅延時間と、その意図的な負荷に含めるランダム化の範囲は、アプリケーションの設計と、そのアプリケーションが実行される予定の環境によって異なります。

## <a name="development-process"></a>開発プロセス

サーバーを変更するときは、以前に実行されていたインスタンスがいずれも実行されていないことを確認することが必要です。 COM は、最終的にはプロセスを清掃しますが、タイマーによる処理には時間がかかり、反復的な開発では効率的ではありません。 そのため、前に実行されているインスタンスを強制終了することは、開発中に通常の手順です。 これには、どの dllhost のインスタンスがサーバーをホストしているかを開発者が追跡する必要があります。

サーバー プロセスを見つけて強制終了するには、タスク マネージャーやその他のサード パーティ アプリを使うことができます。 コマンド ライン ツール **TaskList.exe **も含まれていて、柔軟な構文は、たとえば。

  
 | **Command** | **操作** |
 | ------------| ---------- |
 | tasklist | 実行中のすべてのプロセスをほぼ作成時刻の順序で一覧表示します。最後に作成されたプロセスは下の方に表示されます。 |
 | tasklist /FI "IMAGENAME eq dllhost.exe" /M | すべての dllhost.exe インスタンスの情報を一覧表示します。 /M スイッチは、読み込み済みのモジュールを一覧表示します。 |
 | tasklist /FI "PID eq 12564" /M | PID がわかっている場合に dllhost.exe を照会するには、このオプションを使用できます。 |

ブローカー サーバーのモジュールの一覧が表示されるはず *clrhost.dll* 読み込まれたモジュールの一覧にします。

## <a name="resources"></a>参考資料

-   [VS 2015 および Windows 10 用のプロジェクト テンプレートの仲介型の WinRT コンポーネント](https://marketplace.visualstudio.com/vsgallery/10be07b3-67ef-4e02-9243-01b78cd27935)

-   [NorthwindRT は、WinRT コンポーネント サンプルの仲介型](https://go.microsoft.com/fwlink/p/?LinkID=397349)

-   [Microsoft Store アプリを信頼できる配信](https://go.microsoft.com/fwlink/p/?LinkID=393644)

-   [アプリ コントラクトと拡張機能 (Windows ストア アプリ)](https://docs.microsoft.com/previous-versions/windows/apps/hh464906(v=win.10))

-   [Windows 10 でアプリをサイドロードする方法](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)

-   [UWP アプリを企業に展開します。](https://go.microsoft.com/fwlink/p/?LinkID=264770)

