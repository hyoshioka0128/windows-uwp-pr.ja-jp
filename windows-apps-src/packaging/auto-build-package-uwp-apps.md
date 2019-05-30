---
title: UWP アプリの自動ビルドを設定する
description: サイドロード パッケージやストア パッケージを生成する自動ビルドを構成する方法について説明します。
ms.date: 09/30/2018
ms.topic: article
keywords: windows 10, uwp
ms.assetid: f9b0d6bd-af12-4237-bc66-0c218859d2fd
ms.localizationpriority: medium
ms.openlocfilehash: cb21573dac0c4cc4fc2d6aa2e2345c56631fde87
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372760"
---
# <a name="set-up-automated-builds-for-your-uwp-app"></a><span data-ttu-id="6e430-104">UWP アプリの自動ビルドを設定する</span><span class="sxs-lookup"><span data-stu-id="6e430-104">Set up automated builds for your UWP app</span></span>

<span data-ttu-id="6e430-105">Azure のパイプラインを使用すると、UWP プロジェクトに対して自動ビルドを作成します。</span><span class="sxs-lookup"><span data-stu-id="6e430-105">You can use Azure Pipelines to create automated builds for UWP projects.</span></span> <span data-ttu-id="6e430-106">この記事では、これを行うさまざまな方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="6e430-106">In this article, we’ll look at different ways to do this.</span></span> <span data-ttu-id="6e430-107">紹介しますが、他のビルド システムと統合できるように、コマンドラインを使用して、これらのタスクを実行する方法。</span><span class="sxs-lookup"><span data-stu-id="6e430-107">We’ll also show you how to perform these tasks by using the command line so that you can integrate with any other build system.</span></span>

## <a name="create-a-new-azure-pipeline"></a><span data-ttu-id="6e430-108">新しい Azure パイプラインを作成します。</span><span class="sxs-lookup"><span data-stu-id="6e430-108">Create a new Azure Pipeline</span></span>

<span data-ttu-id="6e430-109">まず[パイプラインを Azure にサインアップ](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up)をまだ行っていない場合。</span><span class="sxs-lookup"><span data-stu-id="6e430-109">Begin by [signing up for Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up) if you haven't done so already.</span></span>

<span data-ttu-id="6e430-110">次に、ソース コードをビルドするのに使用できるパイプラインを作成します。</span><span class="sxs-lookup"><span data-stu-id="6e430-110">Next, create a pipeline that you can use to build your source code.</span></span> <span data-ttu-id="6e430-111">GitHub リポジトリを構築するためのパイプラインの構築に関するチュートリアルについては、次を参照してください。[最初のパイプラインを作成する](https://docs.microsoft.com/azure/devops/pipelines/get-started-yaml)します。</span><span class="sxs-lookup"><span data-stu-id="6e430-111">For a tutorial about building a pipeline to build a GitHub repository, see [Create your first pipeline](https://docs.microsoft.com/azure/devops/pipelines/get-started-yaml).</span></span> <span data-ttu-id="6e430-112">Azure のパイプラインが表示されているリポジトリの種類をサポートしています[今回](https://docs.microsoft.com/azure/devops/pipelines/repos)します。</span><span class="sxs-lookup"><span data-stu-id="6e430-112">Azure Pipelines supports the repository types listed [in this article](https://docs.microsoft.com/azure/devops/pipelines/repos).</span></span>

## <a name="set-up-an-automated-build"></a><span data-ttu-id="6e430-113">自動ビルドを設定する</span><span class="sxs-lookup"><span data-stu-id="6e430-113">Set up an automated build</span></span>

<span data-ttu-id="6e430-114">まず、既定値は、UWP は、Azure の開発運用で使用可能な定義を作成し、パイプラインを構成する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="6e430-114">We’ll start with the default UWP build definition that’s available in Azure Dev Ops and then show you how to configure the pipeline.</span></span>

<span data-ttu-id="6e430-115">ビルド定義テンプレートの一覧で、 **[ユニバーサル Windows プラットフォーム]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="6e430-115">In the list of build definition templates, choose the **Universal Windows Platform** template.</span></span>

![UWP テンプレートを選択します。](images/select-yaml-template.png)

<span data-ttu-id="6e430-117">このテンプレートには、UWP プロジェクトをビルドする基本的な構成が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6e430-117">This template includes the basic configuration to build your UWP project:</span></span>

```yml
trigger:
- master

pool:
  vmImage: 'VS2017-Win2016'

variables:
  solution: '**/*.sln'
  buildPlatform: 'x86|x64|ARM'
  buildConfiguration: 'Release'
  appxPackageDir: '$(build.artifactStagingDirectory)\AppxPackages\\'

steps:
- task: NuGetToolInstaller@0

- task: NuGetCommand@2
  inputs:
    restoreSolution: '$(solution)'

- task: VSBuild@1
  inputs:
    platform: 'x86'
    solution: '$(solution)'
    configuration: '$(buildConfiguration)'
    msbuildArgs: '/p:AppxBundlePlatforms="$(buildPlatform)" /p:AppxPackageDir="$(appxPackageDir)" /p:AppxBundle=Always /p:UapAppxPackageBuildMode=StoreUpload'

```

<span data-ttu-id="6e430-118">既定のテンプレートは、.csproj ファイルで指定された証明書でパッケージに署名しようとします。</span><span class="sxs-lookup"><span data-stu-id="6e430-118">The default template tries to sign the package with the certificate specified in the .csproj file.</span></span> <span data-ttu-id="6e430-119">ビルド中に、パッケージに署名する場合は、秘密キーへのアクセスが必要です。</span><span class="sxs-lookup"><span data-stu-id="6e430-119">If you want to sign your package during the build you must have access to the private key.</span></span> <span data-ttu-id="6e430-120">署名パラメーターを追加して無効にした場合は、`/p:AppxPackageSigningEnabled=false`を`msbuildArgs`YAML ファイルのセクション。</span><span class="sxs-lookup"><span data-stu-id="6e430-120">Otherwise, you can disable signing by adding the parameter `/p:AppxPackageSigningEnabled=false` to the `msbuildArgs` section in the YAML file.</span></span>

## <a name="add-your-project-certificate-to-a-repository"></a><span data-ttu-id="6e430-121">リポジトリに、プロジェクトの証明書を追加します。</span><span class="sxs-lookup"><span data-stu-id="6e430-121">Add your project certificate to a repository</span></span>

<span data-ttu-id="6e430-122">パイプラインは、Azure リポジトリの Git と TFVC の両方のリポジトリで動作します。</span><span class="sxs-lookup"><span data-stu-id="6e430-122">Pipelines works with both Azure Repos Git and TFVC repositories.</span></span> <span data-ttu-id="6e430-123">Git リポジトリを使用する場合は、ビルド エージェントがアプリ パッケージに署名できるように、リポジトリにプロジェクトの証明書ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="6e430-123">If you use a Git repository, add the certificate file of your project to the repository so that the build agent can sign the app package.</span></span> <span data-ttu-id="6e430-124">これを行わない場合、Git リポジトリは証明書ファイルを無視します。</span><span class="sxs-lookup"><span data-stu-id="6e430-124">If you don’t do this, the Git repository will ignore the certificate file.</span></span> <span data-ttu-id="6e430-125">証明書ファイルを右クリックし、リポジトリには、証明書ファイルを追加するに**ソリューション エクスプ ローラー**、ショートカット メニューの 、**無視ファイルをソース管理に追加**コマンド。</span><span class="sxs-lookup"><span data-stu-id="6e430-125">To add the certificate file to your repository, right-click the certificate file in **Solution Explorer**, and then in the shortcut menu, choose the **Add Ignored File to Source Control** command.</span></span>

![証明書を含める方法](images/building-screen1.png)

## <a name="configure-the-build-solution-build-task"></a><span data-ttu-id="6e430-127">ソリューションのビルドのビルド タスクを構成する</span><span class="sxs-lookup"><span data-stu-id="6e430-127">Configure the Build solution build task</span></span>

<span data-ttu-id="6e430-128">このタスクは、バイナリを作業フォルダーにあり、出力アプリのパッケージ ファイルを生成するソリューションをコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="6e430-128">This task compiles any solution that’s in the working folder to binaries and produces the output app package file.</span></span>
<span data-ttu-id="6e430-129">このタスクは、MSBuild 引数を使用します。</span><span class="sxs-lookup"><span data-stu-id="6e430-129">This task uses MSBuild arguments.</span></span> <span data-ttu-id="6e430-130">これらの引数の値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6e430-130">You’ll have to specify the value of those arguments.</span></span> <span data-ttu-id="6e430-131">次の表をガイドとして使用してください。</span><span class="sxs-lookup"><span data-stu-id="6e430-131">Use the following table as a guide.</span></span>

|<span data-ttu-id="6e430-132">**MSBuild 引数**</span><span class="sxs-lookup"><span data-stu-id="6e430-132">**MSBuild argument**</span></span>|<span data-ttu-id="6e430-133">**値**</span><span class="sxs-lookup"><span data-stu-id="6e430-133">**Value**</span></span>|<span data-ttu-id="6e430-134">**説明**</span><span class="sxs-lookup"><span data-stu-id="6e430-134">**Description**</span></span>|
|--------------------|---------|---------------|
| <span data-ttu-id="6e430-135">AppxPackageDir</span><span class="sxs-lookup"><span data-stu-id="6e430-135">AppxPackageDir</span></span> | <span data-ttu-id="6e430-136">$(Build.ArtifactStagingDirectory)\AppxPackages</span><span class="sxs-lookup"><span data-stu-id="6e430-136">$(Build.ArtifactStagingDirectory)\AppxPackages</span></span> | <span data-ttu-id="6e430-137">生成された成果物を格納するフォルダーを定義します。</span><span class="sxs-lookup"><span data-stu-id="6e430-137">Defines the folder to store the generated artifacts.</span></span> |
| <span data-ttu-id="6e430-138">AppxBundlePlatforms</span><span class="sxs-lookup"><span data-stu-id="6e430-138">AppxBundlePlatforms</span></span> | <span data-ttu-id="6e430-139">$(Build.BuildPlatform)</span><span class="sxs-lookup"><span data-stu-id="6e430-139">$(Build.BuildPlatform)</span></span> | <span data-ttu-id="6e430-140">バンドルに含めるプラットフォームを定義できます。</span><span class="sxs-lookup"><span data-stu-id="6e430-140">Enables you to define the platforms to include in the bundle.</span></span> |
| <span data-ttu-id="6e430-141">AppxBundle</span><span class="sxs-lookup"><span data-stu-id="6e430-141">AppxBundle</span></span> | <span data-ttu-id="6e430-142">常に </span><span class="sxs-lookup"><span data-stu-id="6e430-142">Always</span></span> | <span data-ttu-id="6e430-143">指定されたプラットフォームの.msix/.appx ファイルで、.msixbundle/.appxbundle を作成します。</span><span class="sxs-lookup"><span data-stu-id="6e430-143">Creates an .msixbundle/.appxbundle with the .msix/.appx files for the platform specified.</span></span> |
| <span data-ttu-id="6e430-144">UapAppxPackageBuildMode</span><span class="sxs-lookup"><span data-stu-id="6e430-144">UapAppxPackageBuildMode</span></span> | <span data-ttu-id="6e430-145">StoreUpload</span><span class="sxs-lookup"><span data-stu-id="6e430-145">StoreUpload</span></span> | <span data-ttu-id="6e430-146">.Msixupload/.appxupload ファイルを生成し、**テスト (_t)** サイドローディング用のフォルダー。</span><span class="sxs-lookup"><span data-stu-id="6e430-146">Generates the .msixupload/.appxupload file and the **_Test** folder for sideloading.</span></span> |
| <span data-ttu-id="6e430-147">UapAppxPackageBuildMode</span><span class="sxs-lookup"><span data-stu-id="6e430-147">UapAppxPackageBuildMode</span></span> | <span data-ttu-id="6e430-148">CI</span><span class="sxs-lookup"><span data-stu-id="6e430-148">CI</span></span> | <span data-ttu-id="6e430-149">.Msixupload/.appxupload ファイルのみを生成します。</span><span class="sxs-lookup"><span data-stu-id="6e430-149">Generates the .msixupload/.appxupload file only.</span></span> |
| <span data-ttu-id="6e430-150">UapAppxPackageBuildMode</span><span class="sxs-lookup"><span data-stu-id="6e430-150">UapAppxPackageBuildMode</span></span> | <span data-ttu-id="6e430-151">SideloadOnly</span><span class="sxs-lookup"><span data-stu-id="6e430-151">SideloadOnly</span></span> | <span data-ttu-id="6e430-152">生成、**テスト (_t)** のみサイドローディング用のフォルダー</span><span class="sxs-lookup"><span data-stu-id="6e430-152">Generates the **_Test** folder for sideloading only</span></span> |

<span data-ttu-id="6e430-153">またはその他のビルド システムを使用して、コマンドラインを使用して、ソリューションをビルドする場合は、これらの引数で MSBuild を実行します。</span><span class="sxs-lookup"><span data-stu-id="6e430-153">If you want to build your solution by using the command line, or by using any other build system, run MSBuild with these arguments.</span></span>

```powershell
/p:AppxPackageDir="$(Build.ArtifactStagingDirectory)\AppxPackages\\"
/p:UapAppxPackageBuildMode=StoreUpload
/p:AppxBundlePlatforms="$(Build.BuildPlatform)"
/p:AppxBundle=Always
```

<span data-ttu-id="6e430-154">定義されているパラメーター、`$()`構文は、ビルド定義で定義された変数とその他の変更がシステムを構築します。</span><span class="sxs-lookup"><span data-stu-id="6e430-154">The parameters defined with the `$()` syntax are variables defined in the build definition, and will change in other build systems.</span></span>

![既定の変数](images/building-screen5.png)

<span data-ttu-id="6e430-156">定義済みのすべての変数を表示するを参照してください。[ビルド変数の定義済み](https://docs.microsoft.com/azure/devops/pipelines/build/variables)します。</span><span class="sxs-lookup"><span data-stu-id="6e430-156">To view all predefined variables, see [Predefined build variables](https://docs.microsoft.com/azure/devops/pipelines/build/variables).</span></span>

## <a name="configure-the-publish-build-artifacts-task"></a><span data-ttu-id="6e430-157">ビルド成果物の発行タスクを構成します。</span><span class="sxs-lookup"><span data-stu-id="6e430-157">Configure the Publish Build Artifacts task</span></span>

<span data-ttu-id="6e430-158">既定の UWP パイプラインは、生成された成果物を保存できません。</span><span class="sxs-lookup"><span data-stu-id="6e430-158">The default UWP pipeline does not save the generated artifacts.</span></span> <span data-ttu-id="6e430-159">YAML 定義には、発行機能を追加するには、次のタスクを追加します。</span><span class="sxs-lookup"><span data-stu-id="6e430-159">To add the publish capabilities to your YAML definition, add the following tasks.</span></span>

```yml
- task: CopyFiles@2
  displayName: 'Copy Files to: $(build.artifactstagingdirectory)'
  inputs:
    SourceFolder: '$(system.defaultworkingdirectory)'
    Contents: '**\bin\$(BuildConfiguration)\**'
    TargetFolder: '$(build.artifactstagingdirectory)'

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact: drop'
  inputs:
    PathtoPublish: '$(build.artifactstagingdirectory)'
```

<span data-ttu-id="6e430-160">生成された成果物を表示できます、**成果物**オプション、ビルドの結果 ページ。</span><span class="sxs-lookup"><span data-stu-id="6e430-160">You can see the generated artifacts in the **Artifacts** option of the build results page.</span></span>

![成果物](images/building-screen6.png)

<span data-ttu-id="6e430-162">ご用意しましたので、`UapAppxPackageBuildMode`引数`StoreUpload`、成果物フォルダーには (.msixupload/.appxupload) ストアに送信するパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="6e430-162">Because we’ve set the `UapAppxPackageBuildMode` argument to `StoreUpload`, the artifacts folder includes the package for submission to the Store (.msixupload/.appxupload).</span></span> <span data-ttu-id="6e430-163">送信する通常のアプリ パッケージ (.msix/.appx) またはアプリ バンドル (.msixbundle/.appxbundle/) ストアに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6e430-163">Note that you can also submit a regular app pacakge (.msix/.appx) or an app bundle (.msixbundle/.appxbundle/) to the Store.</span></span> <span data-ttu-id="6e430-164">この資料の目的上、.appxupload ファイルを使います。</span><span class="sxs-lookup"><span data-stu-id="6e430-164">For the purposes of this article, we'll use the .appxupload file.</span></span>

## <a name="address-bundle-errors"></a><span data-ttu-id="6e430-165">アドレスのバンドルのエラー</span><span class="sxs-lookup"><span data-stu-id="6e430-165">Address bundle errors</span></span>

<span data-ttu-id="6e430-166">1 つ以上の UWP プロジェクトをソリューションに追加してバンドルを作成しようとしは、次のようなエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="6e430-166">If you add more than one UWP project to your solution and then try to create a bundle, you might receive an error like this one.</span></span>

  `MakeAppx(0,0): Error : Error info: error 80080204: The package with file name "AppOne.UnitTests_0.1.2595.0_x86.appx" and package full name "8ef641d1-4557-4e33-957f-6895b122f1e6_0.1.2595.0_x86__scrj5wvaadcy6" is not valid in the bundle because it has a different package family name than other packages in the bundle`

<span data-ttu-id="6e430-167">このエラーが表示されるのは、ソリューション レベルで、バンドルに含めるアプリが明確ではないためです。</span><span class="sxs-lookup"><span data-stu-id="6e430-167">This error appears because at the solution level, it’s not clear which app should appear in the bundle.</span></span> <span data-ttu-id="6e430-168">この問題を解決するには、各プロジェクト ファイルを開くし、次のプロパティを 1 つ目の末尾に追加`<PropertyGroup>`要素。</span><span class="sxs-lookup"><span data-stu-id="6e430-168">To resolve this issue, open each project file and add the following properties at the end of the first `<PropertyGroup>` element.</span></span>

|<span data-ttu-id="6e430-169">**プロジェクト**</span><span class="sxs-lookup"><span data-stu-id="6e430-169">**Project**</span></span>|<span data-ttu-id="6e430-170">**[プロパティ]**</span><span class="sxs-lookup"><span data-stu-id="6e430-170">**Properties**</span></span>|
|-------|----------|
|<span data-ttu-id="6e430-171">App</span><span class="sxs-lookup"><span data-stu-id="6e430-171">App</span></span>|`<AppxBundle>Always</AppxBundle>`|
|<span data-ttu-id="6e430-172">UnitTests</span><span class="sxs-lookup"><span data-stu-id="6e430-172">UnitTests</span></span>|`<AppxBundle>Never</AppxBundle>`|

<span data-ttu-id="6e430-173">次に、削除、`AppxBundle`ビルド ステップの MSBuild 引数。</span><span class="sxs-lookup"><span data-stu-id="6e430-173">Then, remove the `AppxBundle` MSBuild argument from the build step.</span></span>

## <a name="related-topics"></a><span data-ttu-id="6e430-174">関連トピック</span><span class="sxs-lookup"><span data-stu-id="6e430-174">Related topics</span></span>

- [<span data-ttu-id="6e430-175">Windows の .NET アプリを構築します。</span><span class="sxs-lookup"><span data-stu-id="6e430-175">Build your .NET app for Windows</span></span>](https://www.visualstudio.com/docs/build/get-started/dot-net)
- [<span data-ttu-id="6e430-176">UWP アプリのパッケージ化</span><span class="sxs-lookup"><span data-stu-id="6e430-176">Packaging UWP apps</span></span>](https://docs.microsoft.com/windows/uwp/packaging/packaging-uwp-apps)
- [<span data-ttu-id="6e430-177">Windows 10 で LOB アプリのサイドロード</span><span class="sxs-lookup"><span data-stu-id="6e430-177">Sideload LOB apps in Windows 10</span></span>](https://technet.microsoft.com/itpro/windows/deploy/sideload-apps-in-windows-10)
- [<span data-ttu-id="6e430-178">パッケージに署名するための証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="6e430-178">Create a certificate for package signing</span></span>](https://docs.microsoft.com/windows/uwp/packaging/create-certificate-package-signing)
