---
Description: 既定の InkToolbar をユニバーサル Windows プラットフォーム (UWP) 手描き入力アプリに追加し、カスタム ペン ボタンを InkToolbar に追加して、カスタム ペン ボタンをカスタム ペン定義にバインドします。
title: InkToolbar をユニバーサル Windows プラットフォーム (UWP) アプリに追加する
label: Add an InkToolbar to a Universal Windows Platform (UWP) app
template: detail.hbs
keywords: Windows Ink, Windows の手書き入力, DirectInk, InkPresenter, InkCanvas, InkToolbar, ユニバーサル Windows プラットフォーム, UWP, ユーザー操作, 入力
ms.date: 02/08/2017
ms.topic: article
ms.assetid: d888f75f-c2a0-4134-81db-907b5e24fcc5
ms.localizationpriority: medium
ms.openlocfilehash: 0dd16eac9fe61f292b4f05e1fbd515c0e7255377
ms.sourcegitcommit: d00acf229aa41be2d41ef3e5a7d1f40fa7153acc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65187514"
---
# <a name="add-an-inktoolbar-to-a-universal-windows-platform-uwp-app"></a><span data-ttu-id="20be9-104">InkToolbar をユニバーサル Windows プラットフォーム (UWP) アプリに追加する</span><span class="sxs-lookup"><span data-stu-id="20be9-104">Add an InkToolbar to a Universal Windows Platform (UWP) app</span></span>



<span data-ttu-id="20be9-105">ユニバーサル Windows プラットフォーム (UWP) アプリで手描き入力機能を容易にする 2 つの異なるコントロールがあります。[**InkCanvas** ](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inkcanvas.aspx)と[ **InkToolbar**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="20be9-105">There are two different controls that facilitate inking in Universal Windows Platform (UWP) apps: [**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inkcanvas.aspx) and [**InkToolbar**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx).</span></span>

<span data-ttu-id="20be9-106">[  **InkCanvas**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inkcanvas.aspx) コントロールには、基本的な Windows Ink 機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="20be9-106">The [**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inkcanvas.aspx) control provides basic Windows Ink functionality.</span></span> <span data-ttu-id="20be9-107">このコントロールを使用して、ペン入力をインク ストローク (色と太さの既定の設定を使う) か消去ストロークとしてレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="20be9-107">Use it to render pen input as either an ink stroke (using default settings for color and thickness) or an erase stroke.</span></span>

> <span data-ttu-id="20be9-108">InkCanvas の実装について詳しくは、「[UWP アプリのペン操作とスタイラス操作](pen-and-stylus-interactions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20be9-108">For InkCanvas implementation details, see [Pen and stylus interactions in UWP apps](pen-and-stylus-interactions.md).</span></span>

<span data-ttu-id="20be9-109">InkCanvas は、完全に透明なオーバーレイであるため、インク ストロークのプロパティを設定するための UI は組み込まれていません。</span><span class="sxs-lookup"><span data-stu-id="20be9-109">As a completely transparent overlay, the InkCanvas does not provide any built-in UI for setting ink stroke properties.</span></span> <span data-ttu-id="20be9-110">既定の手書き入力エクスペリエンスを変更する場合、ユーザーがインク ストロークのプロパティを設定し、その他のカスタムの手書き入力機能を使用できるようにします。これには 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="20be9-110">If you want to change the default inking experience, let users set ink stroke properties, and support other custom inking features, you have two options:</span></span>

- <span data-ttu-id="20be9-111">コード ビハインドで、InkCanvas にバインドされている、基になる [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkpresenter.aspx) オブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="20be9-111">In code-behind, use the underlying [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkpresenter.aspx) object bound to the InkCanvas.</span></span>

  <span data-ttu-id="20be9-112">InkPresenter API では、手書き入力エクスペリエンスのさまざまなカスタマイズをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="20be9-112">The InkPresenter APIs support extensive customization of the inking experience.</span></span> <span data-ttu-id="20be9-113">詳しくは、「[UWP アプリのペン操作とスタイラス操作](pen-and-stylus-interactions.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20be9-113">For more detail, see [Pen and stylus interactions in UWP apps](pen-and-stylus-interactions.md).</span></span>

- <span data-ttu-id="20be9-114">[  **InkToolbar**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx) を InkCanvas にバインドします。</span><span class="sxs-lookup"><span data-stu-id="20be9-114">Bind an [**InkToolbar**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx) to the InkCanvas.</span></span> <span data-ttu-id="20be9-115">既定では、InkToolbar には、インク機能をアクティブ化し、ストロークのサイズ、インクの色、ペン先の形状などのインク関連のプロパティを設定できる、カスタマイズ可能で拡張可能なボタンのコレクションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="20be9-115">By default, the InkToolbar provides a customizable and extensible collection of buttons for activating ink-related features such as stroke size, ink color, and pen tip.</span></span>

  <span data-ttu-id="20be9-116">ここでは、InkToolbar について説明します。</span><span class="sxs-lookup"><span data-stu-id="20be9-116">We discuss the InkToolbar in this topic.</span></span>

> <span data-ttu-id="20be9-117">**重要な API**:[**InkCanvas クラス**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inkcanvas.aspx)、 [ **InkToolbar クラス**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx)、 [ **InkPresenter クラス**](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkpresenter.aspx)、 [**Windows.UI.Input.Inking**](https://msdn.microsoft.com/library/windows/apps/br208524)</span><span class="sxs-lookup"><span data-stu-id="20be9-117">**Important APIs**: [**InkCanvas class**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inkcanvas.aspx), [**InkToolbar class**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx), [**InkPresenter class**](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkpresenter.aspx), [**Windows.UI.Input.Inking**](https://msdn.microsoft.com/library/windows/apps/br208524)</span></span>

## <a name="default-inktoolbar"></a><span data-ttu-id="20be9-118">既定の InkToolbar</span><span class="sxs-lookup"><span data-stu-id="20be9-118">Default InkToolbar</span></span>

<span data-ttu-id="20be9-119">既定では、[**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) には、描画、消去、強調表示、ステンシルの表示 (ルーラーまたは分度器) のボタンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="20be9-119">By default, the [**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) includes buttons for drawing, erasing, highlighting, and displaying a stencil (ruler or protractor).</span></span> <span data-ttu-id="20be9-120">機能に応じて、インクの色、ストロークの太さ、すべてのインクの消去など、他の設定やコマンドがポップアップに表示されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-120">Depending on the feature, other settings and commands, such as ink color, stroke thickness, erase all ink, are provided in a flyout.</span></span>

<span data-ttu-id="20be9-121">![InkToolbar](./images/ink/ink-tools-invoked-toolbar-small.png)</span><span class="sxs-lookup"><span data-stu-id="20be9-121">![InkToolbar](./images/ink/ink-tools-invoked-toolbar-small.png)</span></span>  
<span data-ttu-id="20be9-122">*既定の Windows Ink ツールバー*</span><span class="sxs-lookup"><span data-stu-id="20be9-122">*Default Windows Ink toolbar*</span></span>

<span data-ttu-id="20be9-123">既定の [**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) を手描き入力のアプリに追加するには、[**InkCanvas**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas) と同じページに配置して、2 つのコントロールを関連付けます。</span><span class="sxs-lookup"><span data-stu-id="20be9-123">To add a default [**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) to an inking app, just place it on the same page as your [**InkCanvas**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas) and associate the two controls.</span></span>

1. <span data-ttu-id="20be9-124">MainPage.xaml で、手書き入力面のコンテナー オブジェクト (ここでは Grid コントロールを使用します) を宣言します。</span><span class="sxs-lookup"><span data-stu-id="20be9-124">In MainPage.xaml, declare a container object (for this example, we use a Grid control) for the inking surface.</span></span>
2. <span data-ttu-id="20be9-125">コンテナーの子として InkCanvas オブジェクトを宣言します </span><span class="sxs-lookup"><span data-stu-id="20be9-125">Declare an InkCanvas object as a child of the container.</span></span> <span data-ttu-id="20be9-126">(InkCanvas サイズはコンテナーから継承されます)。</span><span class="sxs-lookup"><span data-stu-id="20be9-126">(The InkCanvas size is inherited from the container.)</span></span>
3. <span data-ttu-id="20be9-127">InkToolbar を宣言し、TargetInkCanvas 属性を使用して InkCanvas にバインドします。</span><span class="sxs-lookup"><span data-stu-id="20be9-127">Declare an InkToolbar and use the TargetInkCanvas attribute to bind it to the InkCanvas.</span></span>

> [!NOTE]
> <span data-ttu-id="20be9-128">InkToolbar が InkCanvas の後で宣言されるようにします。</span><span class="sxs-lookup"><span data-stu-id="20be9-128">Ensure the InkToolbar is declared after the InkCanvas.</span></span> <span data-ttu-id="20be9-129">そうでなければ、InkCanvas オーバーレイで InkToolbar にアクセスできなくなります。</span><span class="sxs-lookup"><span data-stu-id="20be9-129">If not, the InkCanvas overlay renders the InkToolbar inaccessible.</span></span>

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header"
                   Text="Basic ink sample"
                   Style="{ThemeResource HeaderTextBlockStyle}"
                   Margin="10,0,0,0" />
    </StackPanel>
    <Grid Grid.Row="1">
        <Image Source="Assets\StoreLogo.png" />
        <InkCanvas x:Name="inkCanvas" />
        <InkToolbar x:Name="inkToolbar"
          VerticalAlignment="Top"
          TargetInkCanvas="{x:Bind inkCanvas}" />
    </Grid>
</Grid>
```

## <a name="basic-customization"></a><span data-ttu-id="20be9-130">基本的なカスタマイズ</span><span class="sxs-lookup"><span data-stu-id="20be9-130">Basic customization</span></span>

<span data-ttu-id="20be9-131">このセクションでは、Windows Ink ツール バーの基本的なカスタマイズに関するシナリオについて説明します。</span><span class="sxs-lookup"><span data-stu-id="20be9-131">In this section, we cover some basic Windows Ink toolbar customization scenarios.</span></span>

### <a name="specify-location-and-orientation"></a><span data-ttu-id="20be9-132">位置と向きの指定</span><span class="sxs-lookup"><span data-stu-id="20be9-132">Specify location and orientation</span></span>

<span data-ttu-id="20be9-133">インク ツール バーをアプリに追加するとき、ツール バーの既定の位置と向きをそのまま使用したり、アプリやユーザーの必要に応じて位置と向きを設定したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="20be9-133">When you add an ink toolbar to your app, you can accept the default location and orientaion of the toolbar or set them as required by your app or user.</span></span>

<span data-ttu-id="20be9-134">**XAML**</span><span class="sxs-lookup"><span data-stu-id="20be9-134">**XAML**</span></span>

<span data-ttu-id="20be9-135">ツール バーの [VerticalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.VerticalAlignment)、[HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.HorizontalAlignment)、[Orientation](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar?branch=rs3.Orientation) の各プロパティを使用して、ツール バーの位置と向きを明示的に指定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-135">Explicitly specify the location and orientation of the toolbar through its [VerticalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.VerticalAlignment), [HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.HorizontalAlignment), and [Orientation](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar?branch=rs3.Orientation) properties.</span></span>

| <span data-ttu-id="20be9-136">Default</span><span class="sxs-lookup"><span data-stu-id="20be9-136">Default</span></span> | <span data-ttu-id="20be9-137">明示的に指定</span><span class="sxs-lookup"><span data-stu-id="20be9-137">Explicit</span></span> |
| --- | --- |
| ![インク ツール バーの既定の位置と向き](./images/ink/location-default-small.png) | ![明示的に指定したインク ツール バーの位置と向き](./images/ink/location-explicit-small.png) |
| <span data-ttu-id="20be9-140">*Windows Ink ツールバーの既定の場所と向き*</span><span class="sxs-lookup"><span data-stu-id="20be9-140">*Windows Ink toolbar default location and orientation*</span></span> | <span data-ttu-id="20be9-141">*Windows Ink ツールバーの明示的な位置と向き*</span><span class="sxs-lookup"><span data-stu-id="20be9-141">*Windows Ink toolbar explicit location and orientation*</span></span> |

<span data-ttu-id="20be9-142">XAML でインク ツール バーの位置と向きを明示的に設定する場合のコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="20be9-142">Here's the code for explicitly setting the location and orientation of the ink toolbar in XAML.</span></span>
```xaml
<InkToolbar x:Name="inkToolbar" 
    VerticalAlignment="Center" 
    HorizontalAlignment="Right" 
    Orientation="Vertical" 
    TargetInkCanvas="{x:Bind inkCanvas}" />
```

<span data-ttu-id="20be9-143">**ユーザーの設定やデバイスの状態に基づいて初期化**</span><span class="sxs-lookup"><span data-stu-id="20be9-143">**Initialize based on user preferences or device state**</span></span>

<span data-ttu-id="20be9-144">場合によっては、ユーザー設定またはデバイスの状態に基づいてインク ツール バーの位置と向きを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20be9-144">In some cases, you might want to set the location and orientation of the ink toolbar based on user preference or device state.</span></span> <span data-ttu-id="20be9-145">次の例は、**[設定] > [デバイス] > [ペンと Windows Ink] > [ペン] > [利き手を選択してください]** で指定されている、左利きや右利きに関する設定に基づいてインク ツール バーの位置と向きを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="20be9-145">The following example demonstrates how to set the location and orientation of the ink toolbar based on the left or right-hand writing preferences specified through **Settings > Devices > Pen & Windows Ink > Pen > Choose which hand you write with**.</span></span>

<span data-ttu-id="20be9-146">![主要な手の形の設定](./images/ink/location-handedness-setting.png)</span><span class="sxs-lookup"><span data-stu-id="20be9-146">![Dominant hand setting](./images/ink/location-handedness-setting.png)</span></span>  
<span data-ttu-id="20be9-147">*主要な手の形の設定*</span><span class="sxs-lookup"><span data-stu-id="20be9-147">*Dominant hand setting*</span></span>

<span data-ttu-id="20be9-148">Windows.UI.ViewManagement の HandPreference プロパティを使用してこの設定を照会し、返された値に基づいて [HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.HorizontalAlignment) を設定できます。</span><span class="sxs-lookup"><span data-stu-id="20be9-148">You can query this setting through the HandPreference property of Windows.UI.ViewManagement and set the [HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.HorizontalAlignment) based on the value returned.</span></span> <span data-ttu-id="20be9-149">この例では、左利きのユーザーに対してはアプリの左側にツール バーを配置し、右利きのユーザーに対しては右側に配置します。</span><span class="sxs-lookup"><span data-stu-id="20be9-149">In this example, we locate the toolbar on the left side of the app for a left-handed person and on the right side for a right-handed person.</span></span>

<span data-ttu-id="20be9-150">**このサンプルをからダウンロード[インクのツールバーの位置や向きサンプルの (basic)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness.zip)**</span><span class="sxs-lookup"><span data-stu-id="20be9-150">**Download this sample from [Ink toolbar location and orientation sample (basic)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness.zip)**</span></span>

```csharp
public MainPage()
{
    this.InitializeComponent();

    Windows.UI.ViewManagement.UISettings settings = 
        new Windows.UI.ViewManagement.UISettings();
    HorizontalAlignment alignment = 
        (settings.HandPreference == 
            Windows.UI.ViewManagement.HandPreference.LeftHanded) ? 
            HorizontalAlignment.Left : HorizontalAlignment.Right;
    inkToolbar.HorizontalAlignment = alignment;
}
```

<span data-ttu-id="20be9-151">**ユーザーまたはデバイスの状態に動的に調整します。**</span><span class="sxs-lookup"><span data-stu-id="20be9-151">**Dynamically adjust to user or device state**</span></span>

<span data-ttu-id="20be9-152">バインドを使用し、ユーザー設定、デバイス設定、デバイスの状態に対する変更に基づいて UI の更新を操作することもできます。</span><span class="sxs-lookup"><span data-stu-id="20be9-152">You can also use binding to look after UI updates based on changes to user preferences, device settings, or device states.</span></span> <span data-ttu-id="20be9-153">次の例では、前の例を拡張し、バインド、ViewMOdel オブジェクト、[INotifyPropertyChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.inotifypropertychanged) インターフェイスを使用して、デバイスの向きに基づいてインク ツール バーを動的に配置する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="20be9-153">In the following example, we expand on the previous example and show how to dynamically position the ink toolbar based on device orientation using binding, a ViewMOdel object, and the [INotifyPropertyChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.inotifypropertychanged) interface.</span></span> 

<span data-ttu-id="20be9-154">**このサンプルをからダウンロード[インクのツールバーの位置や向きサンプルの (動的)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness-dynamic.zip)**</span><span class="sxs-lookup"><span data-stu-id="20be9-154">**Download this sample from [Ink toolbar location and orientation sample (dynamic)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness-dynamic.zip)**</span></span>

1. <span data-ttu-id="20be9-155">最初に、ViewModel を追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="20be9-155">First, let's add our ViewModel.</span></span>
    1. <span data-ttu-id="20be9-156">新しいフォルダーをプロジェクトに追加し、そのフォルダーに **ViewModels** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="20be9-156">Add a new folder to your project and call it **ViewModels**.</span></span>
    1. <span data-ttu-id="20be9-157">新しいクラスを ViewModels フォルダーに追加します (この例では、**InkToolbarSnippetHostViewModel.cs** という名前です)。</span><span class="sxs-lookup"><span data-stu-id="20be9-157">Add a new class to the ViewModels folder (for this example, we called it **InkToolbarSnippetHostViewModel.cs**).</span></span>
        > [!NOTE] 
        > <span data-ttu-id="20be9-158">アプリケーションの有効期間中に必要となるこの種類のオブジェクトは 1 つのみであるため、[シングルトン パターン](https://msdn.microsoft.com/library/ff650849.aspx)を使用しました。</span><span class="sxs-lookup"><span data-stu-id="20be9-158">We used the [Singleton pattern](https://msdn.microsoft.com/library/ff650849.aspx) as we only need one object of this type for the life of the application</span></span>

    1. <span data-ttu-id="20be9-159">`using System.ComponentModel` 名前空間をファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-159">Add `using System.ComponentModel` namespace to the file.</span></span>
    1. <span data-ttu-id="20be9-160">**instance** という静的メンバー変数、および **Instance** という名前の静的な読み取り専用プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-160">Add a static member variable called **instance**, and a static read only property named **Instance**.</span></span> <span data-ttu-id="20be9-161">コンストラクターをプライベートにして、このクラスには Instance プロパティ経由でのみアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="20be9-161">Make the constructor private to ensure this class can only be accessed via the Instance property.</span></span>   
        > [!NOTE] 
        > <span data-ttu-id="20be9-162">このクラスは [INotifyPropertyChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.inotifypropertychanged) インターフェイスを継承します。このインターフェイスは、プロパティの値が変化したことをクライアントに通知するために使用されます (通常、クライアントをバインドします)。</span><span class="sxs-lookup"><span data-stu-id="20be9-162">This class inherits from [INotifyPropertyChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.inotifypropertychanged) interface, which is used to notify clients, typically binding clients, that a property value has changed.</span></span> <span data-ttu-id="20be9-163">これを利用して、デバイスの向きの変化を処理します (後の手順で、このコードを展開して、詳しく説明します)。</span><span class="sxs-lookup"><span data-stu-id="20be9-163">We'll be using this to handle changes to the device orientation (we'll expand this code and explain further in a later step).</span></span>  

        ```csharp
        using System.ComponentModel;

        namespace locationandorientation.ViewModels
        {
            public class InkToolbarSnippetHostViewModel : INotifyPropertyChanged
            {
                private static InkToolbarSnippetHostViewModel instance;
                
                public static InkToolbarSnippetHostViewModel Instance
                {
                    get
                    {
                        if (null == instance)
                        {
                            instance = new InkToolbarSnippetHostViewModel();
                        }
                        return instance;
                    }
                }
            }

            private InkToolbarSnippetHostViewModel() { }
        }
        ```

    1. <span data-ttu-id="20be9-164">InkToolbarSnippetHostViewModel クラスには、2 つのブール型プロパティを追加します。**LeftHandedLayout** (前の XAML 専用の例と同じ機能) と**PortraitLayout** (デバイスの向き)。</span><span class="sxs-lookup"><span data-stu-id="20be9-164">Add two bool properties to the InkToolbarSnippetHostViewModel class: **LeftHandedLayout** (same functionality as the previous XAML-only example) and **PortraitLayout** (orientation of the device).</span></span>
        >[!NOTE] 
        > <span data-ttu-id="20be9-165">PortraitLayout プロパティは設定可能なプロパティであり、[PropertyChanged](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) イベントの定義を含んでいます。</span><span class="sxs-lookup"><span data-stu-id="20be9-165">The PortraitLayout property is settable and includes the defintion for the [PropertyChanged](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) event.</span></span>

        ```csharp
        public bool LeftHandedLayout
        {
            get
            {
                bool leftHandedLayout = false;
                Windows.UI.ViewManagement.UISettings settings =
                    new Windows.UI.ViewManagement.UISettings();
                leftHandedLayout = (settings.HandPreference ==
                    Windows.UI.ViewManagement.HandPreference.LeftHanded);
                return leftHandedLayout;
            }
        }

        public bool portraitLayout = false;
        public bool PortraitLayout
        {
            get
            {
                Windows.UI.ViewManagement.ApplicationViewOrientation winOrientation = 
                    Windows.UI.ViewManagement.ApplicationView.GetForCurrentView().Orientation;
                portraitLayout = 
                    (winOrientation == 
                        Windows.UI.ViewManagement.ApplicationViewOrientation.Portrait);
                return portraitLayout;
            }
            set
            {
                if (value.Equals(portraitLayout)) return;
                portraitLayout = value;
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("PortraitLayout"));
            }
        }
        ```

1. <span data-ttu-id="20be9-166">次に、いくつかのコンバーター クラスをプロジェクトに追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="20be9-166">Now, let's add a couple of converter classes to our project.</span></span> <span data-ttu-id="20be9-167">各クラスには、配置の値 ([HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.horizontalalignment) または [VerticalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.verticalalignment)) を返す Convert オブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="20be9-167">Each class contains a Convert object that returns an alignment value (either [HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.horizontalalignment) or [VerticalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.verticalalignment)).</span></span>
    1. <span data-ttu-id="20be9-168">新しいフォルダーをプロジェクトに追加し、そのフォルダーに **Converters** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="20be9-168">Add a new folder to your project and call it **Converters**.</span></span>
    1. <span data-ttu-id="20be9-169">2 つの新しいクラスを Converters フォルダーに追加します (この例では、これらのクラスは **HorizontalAlignmentFromHandednessConverter.cs** および **VerticalAlignmentFromAppViewConverter.cs** という名前です)。</span><span class="sxs-lookup"><span data-stu-id="20be9-169">Add two new classes to the Converters folder (for this example, we call them **HorizontalAlignmentFromHandednessConverter.cs** and **VerticalAlignmentFromAppViewConverter.cs**).</span></span>
    1. <span data-ttu-id="20be9-170">`using Windows.UI.Xaml` 名前空間と `using Windows.UI.Xaml.Data` 名前空間を各ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-170">Add `using Windows.UI.Xaml` and `using Windows.UI.Xaml.Data` namespaces to each file.</span></span>
    1. <span data-ttu-id="20be9-171">各クラスを `public` に変更し、[IValueConverter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.ivalueconverter) インターフェイスを実装するように指定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-171">Change each class to `public` and specify that it implements the [IValueConverter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.ivalueconverter) interface.</span></span>
    1. <span data-ttu-id="20be9-172">次に示すように、[Convert](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.ivalueconverter.convert) メソッドと [ConvertBack](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.ivalueconverter.convertback) メソッドを各ファイルに追加します (ConvertBack メソッドは実装されない状態のままにしてあります)。</span><span class="sxs-lookup"><span data-stu-id="20be9-172">Add the [Convert](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.ivalueconverter.convert) and [ConvertBack](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.ivalueconverter.convertback) methods to each file, as shown here (we leave the ConvertBack method unimplemented).</span></span>
        - <span data-ttu-id="20be9-173">HorizontalAlignmentFromHandednessConverter によって、右利きのユーザーに対してはアプリの右側にインク ツール バーが配置され、左利きのユーザーに対してはアプリの左側に配置されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-173">HorizontalAlignmentFromHandednessConverter positions the ink toolbar to the right side of the app for right-handed users and to the left side of the app for left-handed users.</span></span>
        ```csharp
        using System;

        using Windows.UI.Xaml;
        using Windows.UI.Xaml.Data;

        namespace locationandorientation.Converters
        {
            public class HorizontalAlignmentFromHandednessConverter : IValueConverter
            {
                public object Convert(object value, Type targetType,
                    object parameter, string language)
                {
                    bool leftHanded = (bool)value;
                    HorizontalAlignment alignment = HorizontalAlignment.Right;
                    if (leftHanded)
                    {
                        alignment = HorizontalAlignment.Left;
                    }
                    return alignment;
                }

                public object ConvertBack(object value, Type targetType,
                    object parameter, string language)
                {
                    throw new NotImplementedException();
                }
            }
        }
        ```

        - <span data-ttu-id="20be9-174">VerticalAlignmentFromAppViewConverter によって、縦長の向きの場合はアプリの中心にインク ツール バーが配置され、横長の向きの場合はアプリの上部にインク ツール バーが配置されます (使いやすさの向上を目的としていますが、これはデモンストレーションを行うために任意に選択した配置です)。</span><span class="sxs-lookup"><span data-stu-id="20be9-174">VerticalAlignmentFromAppViewConverter positions the ink toolbar to the center of the app for portrait orientation and to the top of the app for landscape orientation (while intended to improve usability, this is just an arbitrary choice for demonstration purposes).</span></span>
        ```csharp
        using System;

        using Windows.UI.Xaml;
        using Windows.UI.Xaml.Data;

        namespace locationandorientation.Converters
        {
            public class VerticalAlignmentFromAppViewConverter : IValueConverter
            {
                public object Convert(object value, Type targetType,
                    object parameter, string language)
                {
                    bool portraitOrientation = (bool)value;
                    VerticalAlignment alignment = VerticalAlignment.Top;
                    if (portraitOrientation)
                    {
                        alignment = VerticalAlignment.Center;
                    }
                    return alignment;
                }

                public object ConvertBack(object value, Type targetType,
                    object parameter, string language)
                {
                    throw new NotImplementedException();
                }
            }
        }
        ```

1. <span data-ttu-id="20be9-175">ここで、MainPage.xaml.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="20be9-175">Now, open the MainPage.xaml.cs file.</span></span>
    1. <span data-ttu-id="20be9-176">追加`using using locationandorientation.ViewModels`ViewModel を関連付ける名前空間の一覧にします。</span><span class="sxs-lookup"><span data-stu-id="20be9-176">Add `using using locationandorientation.ViewModels` to the list of namespaces to associate our ViewModel.</span></span>
    1. <span data-ttu-id="20be9-177">追加`using Windows.UI.ViewManagement`デバイスの方向に変更のリッスンを有効にする名前空間の一覧にします。</span><span class="sxs-lookup"><span data-stu-id="20be9-177">Add `using Windows.UI.ViewManagement` to the list of namespaces to enable listening for changes to the device orientation.</span></span>
    1. <span data-ttu-id="20be9-178">追加、 [WindowSizeChangedEventHandler](https://docs.microsoft.com/uwp/api/windows.ui.xaml.windowsizechangedeventhandler)コード。</span><span class="sxs-lookup"><span data-stu-id="20be9-178">Add the [WindowSizeChangedEventHandler](https://docs.microsoft.com/uwp/api/windows.ui.xaml.windowsizechangedeventhandler) code.</span></span>
    1. <span data-ttu-id="20be9-179">設定、 [DataContext](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.FrameworkElement.DataContext) InkToolbarSnippetHostViewModel クラスのシングルトン インスタンスを表示します。</span><span class="sxs-lookup"><span data-stu-id="20be9-179">Set the [DataContext](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.FrameworkElement.DataContext) for the view to the singleton instance of the InkToolbarSnippetHostViewModel class.</span></span> 
    ```csharp
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Controls;

    using locationandorientation.ViewModels;
    using Windows.UI.ViewManagement;

    namespace locationandorientation
    {
        public sealed partial class MainPage : Page
        {
            public MainPage()
            {
                this.InitializeComponent();

                Window.Current.SizeChanged += (sender, args) =>
                {
                    ApplicationView currentView = ApplicationView.GetForCurrentView();

                    if (currentView.Orientation == ApplicationViewOrientation.Landscape)
                    {
                        InkToolbarSnippetHostViewModel.Instance.PortraitLayout = false;
                    }
                    else if (currentView.Orientation == ApplicationViewOrientation.Portrait)
                    {
                        InkToolbarSnippetHostViewModel.Instance.PortraitLayout = true;
                    }
                };

                DataContext = InkToolbarSnippetHostViewModel.Instance;
            }
        }
    }
    ```

1. <span data-ttu-id="20be9-180">次に、MainPage.xaml ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="20be9-180">Next, open the MainPage.xaml file.</span></span>
    1. <span data-ttu-id="20be9-181">追加`xmlns:converters="using:locationandorientation.Converters"`を`Page`コンバーターへのバインド要素。</span><span class="sxs-lookup"><span data-stu-id="20be9-181">Add `xmlns:converters="using:locationandorientation.Converters"` to the `Page` element for binding to our converters.</span></span>
        ```xaml
        <Page
        x:Class="locationandorientation.MainPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:locationandorientation"
        xmlns:converters="using:locationandorientation.Converters"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">
        ```

    1. <span data-ttu-id="20be9-182">追加、`PageResources`要素と、コンバーターへの参照を指定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-182">Add a `PageResources` element and specify references to our converters.</span></span>
        ```xaml
        <Page.Resources>
            <converters:HorizontalAlignmentFromHandednessConverter x:Key="HorizontalAlignmentConverter"/>
            <converters:VerticalAlignmentFromAppViewConverter x:Key="VerticalAlignmentConverter"/>
        </Page.Resources>
        ```

    1. <span data-ttu-id="20be9-183">InkCanvas と InkToolbar 要素を追加し、InkToolbar の verticalalignment と HorizontalAlignment プロパティをバインドします。</span><span class="sxs-lookup"><span data-stu-id="20be9-183">Add the InkCanvas and InkToolbar elements and bind the VerticalAlignment and HorizontalAlignment properties of the InkToolbar.</span></span>
        ```xaml
        <InkCanvas x:Name="inkCanvas" />
        <InkToolbar x:Name="inkToolbar" 
                    VerticalAlignment="{Binding PortraitLayout, Converter={StaticResource VerticalAlignmentConverter} }" 
                    HorizontalAlignment="{Binding LeftHandedLayout, Converter={StaticResource HorizontalAlignmentConverter} }" 
                    Orientation="Vertical" 
                    TargetInkCanvas="{x:Bind inkCanvas}" />
        ```

1. <span data-ttu-id="20be9-184">追加する InkToolbarSnippetHostViewModel.cs ファイルに戻り、`PortraitLayout`と`LeftHandedLayout`にブール型のプロパティ、`InkToolbarSnippetHostViewModel`クラスを再バインドのサポートと共に`PortraitLayout`そのプロパティ値が変更されたとき。</span><span class="sxs-lookup"><span data-stu-id="20be9-184">Return to the InkToolbarSnippetHostViewModel.cs file to add our `PortraitLayout` and `LeftHandedLayout` bool properties to the `InkToolbarSnippetHostViewModel` class, along with support for rebinding `PortraitLayout` when that property value changes.</span></span> 
    ```csharp
    public bool LeftHandedLayout
    {
        get
        {
            bool leftHandedLayout = false;
            Windows.UI.ViewManagement.UISettings settings =
                new Windows.UI.ViewManagement.UISettings();
            leftHandedLayout = (settings.HandPreference ==
                Windows.UI.ViewManagement.HandPreference.LeftHanded);
            return leftHandedLayout;
        }
    }

    public bool portraitLayout = false;
    public bool PortraitLayout
    {
        get
        {
            Windows.UI.ViewManagement.ApplicationViewOrientation winOrientation = 
                Windows.UI.ViewManagement.ApplicationView.GetForCurrentView().Orientation;
            portraitLayout = 
                (winOrientation == 
                    Windows.UI.ViewManagement.ApplicationViewOrientation.Portrait);
            return portraitLayout;
        }
        set
        {
            if (value.Equals(portraitLayout)) return;
            portraitLayout = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("PortraitLayout"));
        }
    }

    #region INotifyPropertyChanged Members

    public event PropertyChangedEventHandler PropertyChanged;

    protected void OnPropertyChanged(string property)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(property));
    }

    #endregion
    ```

<span data-ttu-id="20be9-185">これで、ユーザーの手の主要な設定に適応し、ユーザーのデバイスの向きに動的に応答するインク対応アプリケーションが必要です。</span><span class="sxs-lookup"><span data-stu-id="20be9-185">You should now have an inking app that adapts to both the dominant hand preference of the user and dynamically responds to the orientation of the user's device.</span></span>

### <a name="specify-the-selected-button"></a><span data-ttu-id="20be9-186">選択されるボタンを指定する</span><span class="sxs-lookup"><span data-stu-id="20be9-186">Specify the selected button</span></span>  
<span data-ttu-id="20be9-187">![初期化時に選択した鉛筆ボタン](./images/ink/ink-tools-default-toolbar.png)</span><span class="sxs-lookup"><span data-stu-id="20be9-187">![Pencil button selected at initialization](./images/ink/ink-tools-default-toolbar.png)</span></span>  
<span data-ttu-id="20be9-188">*初期化時に選択した鉛筆ボタンを使用して Windows インク ツールバー*</span><span class="sxs-lookup"><span data-stu-id="20be9-188">*Windows Ink toolbar with pencil button selected at initialization*</span></span>

<span data-ttu-id="20be9-189">既定では、アプリが起動し、ツール バーが初期化されると、最初 (または左端) のボタンが選択されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-189">By default, the first (or leftmost) button is selected when your app is launched and the toolbar is initialized.</span></span> <span data-ttu-id="20be9-190">既定の Windows Ink ツール バーでは、ボールペン ボタンが選択されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-190">In the default Windows Ink toolbar, this is the ballpoint pen button.</span></span>

<span data-ttu-id="20be9-191">フレームワークで組み込みのボタンの順序が定義されるため、最初のボタンが既定でアクティブ化したいペンやツールでない場合があります。</span><span class="sxs-lookup"><span data-stu-id="20be9-191">Because the framework defines the order of the built-in buttons, the first button might not be the pen or tool you want to activate by default.</span></span>

<span data-ttu-id="20be9-192">この既定の動作を上書きし、ツール バーで選択されるボタンを指定できます。</span><span class="sxs-lookup"><span data-stu-id="20be9-192">You can override this default behavior and specify the selected button on the toolbar.</span></span>

<span data-ttu-id="20be9-193">ここでは、(ボールペンではなく) 鉛筆ボタンが選択され、鉛筆がアクティブになるように、既定のツール バーを初期化します。</span><span class="sxs-lookup"><span data-stu-id="20be9-193">For this example, we initialize the default toolbar with the pencil button selected and the pencil activated (instead of the ballpoint pen).</span></span>

1. <span data-ttu-id="20be9-194">前の例から、InkCanvas と InkToolbar の XAML 宣言を使用します。</span><span class="sxs-lookup"><span data-stu-id="20be9-194">Use the XAML declaration for the InkCanvas and InkToolbar from the previous example.</span></span>
2. <span data-ttu-id="20be9-195">コード ビハインドで、[InkToolbar](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx) オブジェクトの [Loaded](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.frameworkelement.loaded.aspx) イベントのハンドラーを設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-195">In code-behind, set up a handler for the [Loaded](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.frameworkelement.loaded.aspx) event of the [InkToolbar](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx) object.</span></span>

  ```csharp
  /// <summary>
  /// An empty page that can be used on its own or navigated to within a Frame.
  /// Here, we set up InkToolbar event listeners.
  /// </summary>
  public MainPage_CodeBehind()
  {
      this.InitializeComponent();
      // Add handlers for InkToolbar events.
      inkToolbar.Loaded += inkToolbar_Loaded;
  }
  ```

3. <span data-ttu-id="20be9-196">[Loaded](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.frameworkelement.loaded.aspx) イベントのハンドラーで次の処理を行います。</span><span class="sxs-lookup"><span data-stu-id="20be9-196">In the handler for the [Loaded](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.frameworkelement.loaded.aspx) event:</span></span>
    1. <span data-ttu-id="20be9-197">組み込みの [InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx) への参照を取得します。</span><span class="sxs-lookup"><span data-stu-id="20be9-197">Get a reference to the built-in [InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx).</span></span>

    <span data-ttu-id="20be9-198">[GetToolButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.gettoolbutton.aspx) メソッドで [InkToolbarTool.Pencil](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbartool.aspx) オブジェクトを渡すことで、[InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx) の [InkToolbarToolButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbartoolbutton.aspx) オブジェクトが返されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-198">Passing an [InkToolbarTool.Pencil](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbartool.aspx) object in the [GetToolButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.gettoolbutton.aspx) method returns an [InkToolbarToolButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbartoolbutton.aspx) object for the [InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx).</span></span>

    2. <span data-ttu-id="20be9-199">前の手順で返されたオブジェクトに [ActiveTool](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.activetool.aspx) を設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-199">Set [ActiveTool](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.activetool.aspx) to the object returned in the previous step.</span></span>

```CSharp
/// <summary>
/// Handle the Loaded event of the InkToolbar.
/// By default, the active tool is set to the first tool on the toolbar.
/// Here, we set the active tool to the pencil button.
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void inkToolbar_Loaded(object sender, RoutedEventArgs e)
{
    InkToolbarToolButton pencilButton = inkToolbar.GetToolButton(InkToolbarTool.Pencil);
    inkToolbar.ActiveTool = pencilButton;
}
```

### <a name="specify-the-built-in-buttons"></a><span data-ttu-id="20be9-200">組み込みのボタンを指定する</span><span class="sxs-lookup"><span data-stu-id="20be9-200">Specify the built-in buttons</span></span>

<span data-ttu-id="20be9-201">![初期化時に含まれる特定のボタン](./images/ink/ink-tools-specific.png)</span><span class="sxs-lookup"><span data-stu-id="20be9-201">![Specific buttons included at initialization](./images/ink/ink-tools-specific.png)</span></span>  
<span data-ttu-id="20be9-202">*初期化時に含まれる特定のボタン*</span><span class="sxs-lookup"><span data-stu-id="20be9-202">*Specific buttons included at initialization*</span></span>

<span data-ttu-id="20be9-203">既に説明したように、Windows Ink ツール バーには既定の組み込みボタンのコレクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="20be9-203">As mentioned, the Windows Ink toolbar includes a collection of default, built-in buttons.</span></span> <span data-ttu-id="20be9-204">これらのボタンは次の順序で (左から右に) 表示されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-204">These buttons are displayed in the following order (from left to right):</span></span>

- [<span data-ttu-id="20be9-205">InkToolbarBallpointPenButton</span><span class="sxs-lookup"><span data-stu-id="20be9-205">InkToolbarBallpointPenButton</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarballpointpenbutton.aspx)
- [<span data-ttu-id="20be9-206">InkToolbarPencilButton</span><span class="sxs-lookup"><span data-stu-id="20be9-206">InkToolbarPencilButton</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx)
- [<span data-ttu-id="20be9-207">InkToolbarHighlighterButton</span><span class="sxs-lookup"><span data-stu-id="20be9-207">InkToolbarHighlighterButton</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarhighlighterbutton.aspx)
- [<span data-ttu-id="20be9-208">InkToolbarEraserButton</span><span class="sxs-lookup"><span data-stu-id="20be9-208">InkToolbarEraserButton</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbareraserbutton.aspx)
- [<span data-ttu-id="20be9-209">InkToolbarRulerButton</span><span class="sxs-lookup"><span data-stu-id="20be9-209">InkToolbarRulerButton</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarrulerbutton.aspx)

<span data-ttu-id="20be9-210">ここでは、組み込みのボールペン、鉛筆、および消しゴムのボタンのみ表示されるようにツール バーを初期化します。</span><span class="sxs-lookup"><span data-stu-id="20be9-210">For this example, we initialize the toolbar with only the built-in ballpoint pen, pencil, and eraser buttons.</span></span>

<span data-ttu-id="20be9-211">これは、XAML またはコード ビハインドを使用して実行できます。</span><span class="sxs-lookup"><span data-stu-id="20be9-211">You can do this using either XAML or code-behind.</span></span>

<span data-ttu-id="20be9-212">**XAML**</span><span class="sxs-lookup"><span data-stu-id="20be9-212">**XAML**</span></span>

<span data-ttu-id="20be9-213">最初の例から、InkCanvas と InkToolbar の XAML 宣言を変更します。</span><span class="sxs-lookup"><span data-stu-id="20be9-213">Modify the XAML declaration for the InkCanvas and InkToolbar from the first example.</span></span>
- <span data-ttu-id="20be9-214">[InitialControls](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.initialcontrols.aspx) 属性を追加し、値を "[None](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarinitialcontrols.aspx)" に設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-214">Add an [InitialControls](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.initialcontrols.aspx) attribute and set its value to "[None](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarinitialcontrols.aspx)".</span></span> <span data-ttu-id="20be9-215">これで組み込みボタンの既定のコレクションがクリアされます。</span><span class="sxs-lookup"><span data-stu-id="20be9-215">This clears the default collection of built-in buttons.</span></span>
- <span data-ttu-id="20be9-216">アプリで必要な特定の InkToolbar ボタンを追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-216">Add the specific InkToolbar buttons required by your app.</span></span> <span data-ttu-id="20be9-217">ここでは、[InkToolbarBallpointPenButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarballpointpenbutton.aspx)、[InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx)、および [InkToolbarEraserButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbareraserbutton.aspx) のみ追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-217">Here, we add [InkToolbarBallpointPenButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarballpointpenbutton.aspx), [InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx), and [InkToolbarEraserButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbareraserbutton.aspx) only.</span></span>
> [!NOTE]
> <span data-ttu-id="20be9-218">ボタンは、ここで指定した順序ではなく、フレームワークで定義されている順序でツール バーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-218">Buttons are added to the toolbar in the order defined by the framework, not the order specified here.</span></span>

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header"
                   Text="Basic ink sample"
                   Style="{ThemeResource HeaderTextBlockStyle}"
                   Margin="10,0,0,0" />
    </StackPanel>
    <Grid Grid.Row="1">
        <Image Source="Assets\StoreLogo.png" />
        <!-- Clear the default InkToolbar buttons by setting InitialControls to None. -->
        <!-- Set the active tool to the pencil button. -->
        <InkCanvas x:Name="inkCanvas" />
        <InkToolbar x:Name="inkToolbar"
                    VerticalAlignment="Top"
                    TargetInkCanvas="{x:Bind inkCanvas}"
                    InitialControls="None">
            <!--
             Add only the ballpoint pen, pencil, and eraser.
             Note that the buttons are added to the toolbar in the order
             defined by the framework, not the order we specify here.
            -->
            <InkToolbarEraserButton />
            <InkToolbarBallpointPenButton />
            <InkToolbarPencilButton/>
        </InkToolbar>
    </Grid>
</Grid>
```

<span data-ttu-id="20be9-219">**分離コード**</span><span class="sxs-lookup"><span data-stu-id="20be9-219">**Code-behind**</span></span>
1. <span data-ttu-id="20be9-220">最初の例から、InkCanvas と InkToolbar の XAML 宣言を使用します。</span><span class="sxs-lookup"><span data-stu-id="20be9-220">Use the XAML declaration for the InkCanvas and InkToolbar from the first example.</span></span>

  ```xaml
  <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
      <Grid.RowDefinitions>
          <RowDefinition Height="Auto"/>
          <RowDefinition Height="*"/>
      </Grid.RowDefinitions>
      <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
          <TextBlock x:Name="Header"
                     Text="Basic ink sample"
                     Style="{ThemeResource HeaderTextBlockStyle}"
                     Margin="10,0,0,0" />
      </StackPanel>
      <Grid Grid.Row="1">
          <Image Source="Assets\StoreLogo.png" />
          <InkCanvas x:Name="inkCanvas" />
          <InkToolbar x:Name="inkToolbar"
          VerticalAlignment="Top"
          TargetInkCanvas="{x:Bind inkCanvas}" />
      </Grid>
  </Grid>
  ```

2. <span data-ttu-id="20be9-221">コード ビハインドで、[InkToolbar](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx) オブジェクトの [Loading](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.frameworkelement.loading.aspx) イベントのハンドラーを設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-221">In code-behind, set up a handler for the [Loading](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.frameworkelement.loading.aspx) event of the [InkToolbar](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx) object.</span></span>

  ```csharp
  /// <summary>
  /// An empty page that can be used on its own or navigated to within a Frame.
  /// Here, we set up InkToolbar event listeners.
  /// </summary>
  public MainPage_CodeBehind()
  {
      this.InitializeComponent();
      // Add handlers for InkToolbar events.
      inkToolbar.Loading += inkToolbar_Loading;
  }
  ```

3. <span data-ttu-id="20be9-222">[InitialControls](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.initialcontrols.aspx) を "[None](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarinitialcontrols.aspx)" に設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-222">Set [InitialControls](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.initialcontrols.aspx) to "[None](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarinitialcontrols.aspx)".</span></span>
4. <span data-ttu-id="20be9-223">アプリで必要なボタンのオブジェクト参照を作成します。</span><span class="sxs-lookup"><span data-stu-id="20be9-223">Create object references for the buttons required by your app.</span></span> <span data-ttu-id="20be9-224">ここでは、[InkToolbarBallpointPenButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarballpointpenbutton.aspx)、[InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx)、および [InkToolbarEraserButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbareraserbutton.aspx) のみ追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-224">Here, we add [InkToolbarBallpointPenButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarballpointpenbutton.aspx), [InkToolbarPencilButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpencilbutton.aspx), and [InkToolbarEraserButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbareraserbutton.aspx) only.</span></span>
  > [!NOTE]
  > <span data-ttu-id="20be9-225">ボタンは、ここで指定した順序ではなく、フレームワークで定義されている順序でツール バーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-225">Buttons are added to the toolbar in the order defined by the framework, not the order specified here.</span></span>

5. <span data-ttu-id="20be9-226">[Add](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.dependencyobjectcollection.add.aspx) メソッドを使用して、ボタンを InkToolbar に追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-226">[Add](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.dependencyobjectcollection.add.aspx) the buttons to the InkToolbar.</span></span>

  ```csharp
  /// <summary>
  /// Handles the Loading event of the InkToolbar.
  /// Here, we identify the buttons to include on the InkToolbar.
  /// </summary>
  /// <param name="sender">The InkToolbar</param>
  /// <param name="args">The InkToolbar event data.
  /// If there is no event data, this parameter is null</param>
  private void inkToolbar_Loading(FrameworkElement sender, object args)
  {
      // Clear all built-in buttons from the InkToolbar.
      inkToolbar.InitialControls = InkToolbarInitialControls.None;

      // Add only the ballpoint pen, pencil, and eraser.
      // Note that the buttons are added to the toolbar in the order
      // defined by the framework, not the order we specify here.
      InkToolbarBallpointPenButton ballpoint = new InkToolbarBallpointPenButton();
      InkToolbarPencilButton pencil = new InkToolbarPencilButton();
      InkToolbarEraserButton eraser = new InkToolbarEraserButton();
      inkToolbar.Children.Add(eraser);
      inkToolbar.Children.Add(ballpoint);
      inkToolbar.Children.Add(pencil);
  }
  ```

<!--
### Support touch input
By default, the InkToolbar supports both pen and mouse input, you have to enable support for touch input.
-->

## <a name="custom-buttons-and-inking-features"></a><span data-ttu-id="20be9-227">カスタム ボタンおよび手書き入力機能</span><span class="sxs-lookup"><span data-stu-id="20be9-227">Custom buttons and inking features</span></span>

<span data-ttu-id="20be9-228">InkToolbar を通じて提供されるボタン (および関連する手書き入力機能) のコレクションをカスタマイズして拡張できます。</span><span class="sxs-lookup"><span data-stu-id="20be9-228">You can customize and extend the collection of buttons (and associated inking features) that are provided through the InkToolbar.</span></span>

<span data-ttu-id="20be9-229">InkToolbar は、次のような 2 つの異なるボタンの種類のグループで構成されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-229">The InkToolbar consists of two distinct groups of button types:</span></span>

1. <span data-ttu-id="20be9-230">"ツール" ボタンのグループ。組み込みの描画ボタン、消去ボタン、強調表示ボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="20be9-230">A group of "tool" buttons containing the built-in drawing, erasing, and highlighting buttons.</span></span> <span data-ttu-id="20be9-231">カスタム ペンとカスタム ツールはここに追加されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-231">Custom pens and tools are added here.</span></span>
> <span data-ttu-id="20be9-232">**注**&nbsp;&nbsp;機能の選択は相互に排他的です。</span><span class="sxs-lookup"><span data-stu-id="20be9-232">**Note**&nbsp;&nbsp;Feature selection is mutually exclusive.</span></span>

2. <span data-ttu-id="20be9-233">"トグル" ボタンのグループ。組み込みのルーラー ボタンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="20be9-233">A group of "toggle" buttons containing the built-in ruler button.</span></span> <span data-ttu-id="20be9-234">カスタム トグルはここに追加されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-234">Custom toggles are added here.</span></span>
> <span data-ttu-id="20be9-235">**注**&nbsp;&nbsp;機能は、相互に排他的でないし、その他のアクティブなツールと同時に使用することができます。</span><span class="sxs-lookup"><span data-stu-id="20be9-235">**Note**&nbsp;&nbsp;Features are not mutually exclusive and can be used concurrently with other active tools.</span></span>

<span data-ttu-id="20be9-236">お使いのアプリケーションと必要なインク機能によって異なりますが、InkToolbar には次のボタン (カスタムの手書き入力機能にバインドされます) を追加できます。</span><span class="sxs-lookup"><span data-stu-id="20be9-236">Depending on your application and the inking functionality required, you can add any of the following buttons (bound to your custom ink features) to the InkToolbar:</span></span>

- <span data-ttu-id="20be9-237">カスタム ペン – インクのカラー パレットやペン先のプロパティ (形状、回転、サイズなど) がホスト アプリで定義されるペン。</span><span class="sxs-lookup"><span data-stu-id="20be9-237">Custom pen – a pen for which the ink color palette and pen tip properties, such as shape, rotation, and size, are defined by the host app.</span></span>
- <span data-ttu-id="20be9-238">カスタム ツール – ホスト アプリで定義されるペン不使用ツール。</span><span class="sxs-lookup"><span data-stu-id="20be9-238">Custom tool – a non-pen tool, defined by the host app.</span></span>
- <span data-ttu-id="20be9-239">カスタム トグル – アプリで定義された機能の状態をオンまたはオフに設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-239">Custom toggle – Sets the state of an app-defined feature to on or off.</span></span> <span data-ttu-id="20be9-240">オンにすると、機能はアクティブなツールと連携して動作します。</span><span class="sxs-lookup"><span data-stu-id="20be9-240">When turned on, the feature works in conjunction with the active tool.</span></span>

> <span data-ttu-id="20be9-241">**注**&nbsp;&nbsp;組み込みのボタンの表示順序を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="20be9-241">**Note**&nbsp;&nbsp;You cannot change the display order of the built-in buttons.</span></span> <span data-ttu-id="20be9-242">既定の表示順序は次のとおりです。ボールペン、鉛筆、蛍光ペン、消しゴムをルーラー。</span><span class="sxs-lookup"><span data-stu-id="20be9-242">The default display order is: Ballpoint pen, pencil, highlighter, eraser, and ruler.</span></span> <span data-ttu-id="20be9-243">カスタム ペンは最後の既定のペンに追加され、カスタム ツール ボタンは最後のペン ボタンと消しゴム ボタンの間に追加され、カスタム トグル ボタンはルーラー ボタンの後に追加されます </span><span class="sxs-lookup"><span data-stu-id="20be9-243">Custom pens are appended to the last default pen, custom tool buttons are added between the last pen button and the eraser button and custom toggle buttons are added after the ruler button.</span></span> <span data-ttu-id="20be9-244">(カスタム ボタンは、指定されている順序で追加されます)。</span><span class="sxs-lookup"><span data-stu-id="20be9-244">(Custom buttons are added in the order they are specified.)</span></span>

### <a name="custom-pen"></a><span data-ttu-id="20be9-245">カスタム ペン</span><span class="sxs-lookup"><span data-stu-id="20be9-245">Custom pen</span></span>

<span data-ttu-id="20be9-246">形状、回転、サイズなどのインク カラー パレットと、ペン先のプロパティを定義するカスタムペン (カスタム ペン ボタンを使用してアクティブ化されます) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="20be9-246">You can create a custom pen (activated through a custom pen button) where you define the ink color palette and pen tip properties, such as shape, rotation, and size.</span></span>

<span data-ttu-id="20be9-247">![カスタム カリグラフィ ペン ボタン](./images/ink/ink-tools-custompen.png)</span><span class="sxs-lookup"><span data-stu-id="20be9-247">![Custom calligraphic pen button](./images/ink/ink-tools-custompen.png)</span></span>  
<span data-ttu-id="20be9-248">*カスタム カリグラフィ ペン ボタン*</span><span class="sxs-lookup"><span data-stu-id="20be9-248">*Custom calligraphic pen button*</span></span>

<span data-ttu-id="20be9-249">ここでは、幅広のペン先で、基本的な筆記体のインク ストロークを可能にするカスタム ペンを定義します。</span><span class="sxs-lookup"><span data-stu-id="20be9-249">For this example, we define a custom pen with a broad tip that enables basic calligraphic ink strokes.</span></span> <span data-ttu-id="20be9-250">また、ボタン ポップアップに表示されるパレットのブラシのコレクションもカスタマイズします。</span><span class="sxs-lookup"><span data-stu-id="20be9-250">We also customize the collection of brushes in the palette displayed on the button flyout.</span></span>

<span data-ttu-id="20be9-251">**分離コード**</span><span class="sxs-lookup"><span data-stu-id="20be9-251">**Code-behind**</span></span>

<span data-ttu-id="20be9-252">まず、コード ビハインドでカスタム ペンを定義し、描画の属性を指定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-252">First, we define our custom pen and specify the drawing attributes in code-behind.</span></span> <span data-ttu-id="20be9-253">このカスタム ペンを後で XAML から参照します。</span><span class="sxs-lookup"><span data-stu-id="20be9-253">We reference this custom pen from XAML later.</span></span>

1. <span data-ttu-id="20be9-254">ソリューション エクスプローラーでプロジェクトを右クリックし、[追加]、[新しい項目] の順に選びます。</span><span class="sxs-lookup"><span data-stu-id="20be9-254">Right click the project in Solution Explorer and select Add -> New item.</span></span>
2. <span data-ttu-id="20be9-255">[Visual C#] の [コード] で、新しいクラス ファイルを追加し、CalligraphicPen.cs という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="20be9-255">Under Visual C# -> Code, add a new Class file and call it CalligraphicPen.cs.</span></span>
3. <span data-ttu-id="20be9-256">Calligraphic.cs で、既定の using ブロックを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="20be9-256">In Calligraphic.cs, replace the default using block with the following:</span></span>
```csharp
using System.Numerics;
using Windows.UI;
using Windows.UI.Input.Inking;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Media;
```

4. <span data-ttu-id="20be9-257">CalligraphicPen クラスが [InkToolbarCustomPen](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarcustompen.aspx) から派生するように指定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-257">Specify that the CalligraphicPen class is derived from [InkToolbarCustomPen](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarcustompen.aspx).</span></span>
```csharp
class CalligraphicPen : InkToolbarCustomPen
{
}
```

5. <span data-ttu-id="20be9-258">[CreateInkDrawingAttributesCore](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarcustompen.createinkdrawingattributescore.aspx) をオーバーライドし、ブラシとストロークのサイズを独自に指定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-258">Override  [CreateInkDrawingAttributesCore](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarcustompen.createinkdrawingattributescore.aspx)  to specify your own brush and stroke size.</span></span>
```csharp
class CalligraphicPen : InkToolbarCustomPen
{
    protected override InkDrawingAttributes
      CreateInkDrawingAttributesCore(Brush brush, double strokeWidth)
    {
    }
}
```

6. <span data-ttu-id="20be9-259">[InkDrawingAttributes](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.aspx) オブジェクトを作成し、[ペン先の形状](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.pentip.aspx)、[ペン先の回転](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.pentiptransform.aspx)、[ストロークのサイズ](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.size.aspx)、および[インクの色](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.color.aspx)を設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-259">Create an [InkDrawingAttributes](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.aspx) object and set the [pen tip shape](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.pentip.aspx), [tip rotation](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.pentiptransform.aspx), [stroke size](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.size.aspx), and [ink color](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.inking.inkdrawingattributes.color.aspx).</span></span>
```csharp
class CalligraphicPen : InkToolbarCustomPen
{
    protected override InkDrawingAttributes
      CreateInkDrawingAttributesCore(Brush brush, double strokeWidth)
    {
        InkDrawingAttributes inkDrawingAttributes =
          new InkDrawingAttributes();
        inkDrawingAttributes.PenTip = PenTipShape.Circle;
        inkDrawingAttributes.Size =
          new Windows.Foundation.Size(strokeWidth, strokeWidth * 20);
        SolidColorBrush solidColorBrush = brush as SolidColorBrush;
        if (solidColorBrush != null)
        {
            inkDrawingAttributes.Color = solidColorBrush.Color;
        }
        else
        {
            inkDrawingAttributes.Color = Colors.Black;
        }

        Matrix3x2 matrix = Matrix3x2.CreateRotation(45);
        inkDrawingAttributes.PenTipTransform = matrix;

        return inkDrawingAttributes;
    }
}
```

<span data-ttu-id="20be9-260">**XAML**</span><span class="sxs-lookup"><span data-stu-id="20be9-260">**XAML**</span></span>

<span data-ttu-id="20be9-261">次に、MainPage.xaml で、カスタム ペンへの必要な参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-261">Next, we add the necessary references to the custom pen in MainPage.xaml.</span></span>

1. <span data-ttu-id="20be9-262">CalligraphicPen.cs で定義したカスタム ペン (`CalligraphicPen`) と、カスタム ペンでサポートされる[ブラシ コレクション](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Media.BrushCollection.aspx) (`CalligraphicPenPalette`) への参照を作成するローカル ページのリソース ディクショナリを宣言します。</span><span class="sxs-lookup"><span data-stu-id="20be9-262">We declare a local page resource dictionary that creates a reference to the custom pen (`CalligraphicPen`) defined in CalligraphicPen.cs, and a [brush collection](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Media.BrushCollection.aspx) supported by the custom pen (`CalligraphicPenPalette`).</span></span>
```xaml
<Page.Resources>
    <!-- Add the custom CalligraphicPen to the page resources. -->
    <local:CalligraphicPen x:Key="CalligraphicPen" />
    <!-- Specify the colors for the palette of the custom pen. -->
    <BrushCollection x:Key="CalligraphicPenPalette">
        <SolidColorBrush Color="Blue" />
        <SolidColorBrush Color="Red" />
    </BrushCollection>
</Page.Resources>
```

2. <span data-ttu-id="20be9-263">次に、InkToolbar と子要素の [InkToolbarCustomPenButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarcustompenbutton.aspx) を追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-263">We then add an InkToolbar with a child [InkToolbarCustomPenButton](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarcustompenbutton.aspx) element.</span></span>

  <span data-ttu-id="20be9-264">カスタム ペン ボタンには、ページ リソースで宣言された `CalligraphicPen` と `CalligraphicPenPalette` の 2 つの静的なリソース参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="20be9-264">The custom pen button includes the two static resource references declared in the page resources: `CalligraphicPen` and `CalligraphicPenPalette`.</span></span>

  <span data-ttu-id="20be9-265">また、ストローク サイズのスライダーの範囲 ([MinStrokeWidth](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.minstrokewidth.aspx)、[MaxStrokeWidth](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.maxstrokewidth.aspx)、および [SelectedStrokeWidth](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.selectedstrokewidthproperty.aspx))、選択されたブラシ ([SelectedBrushIndex](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.selectedbrushindex.aspx))、カスタム ペン ボタンのアイコン ([SymbolIcon](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.symbolicon.aspx)) も指定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-265">We also specify the range for the stroke size slider ([MinStrokeWidth](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.minstrokewidth.aspx), [MaxStrokeWidth](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.maxstrokewidth.aspx), and [SelectedStrokeWidth](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.selectedstrokewidthproperty.aspx)), the selected brush ([SelectedBrushIndex](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbarpenbutton.selectedbrushindex.aspx)), and the icon for the custom pen button ([SymbolIcon](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.symbolicon.aspx)).</span></span>
```xaml
<Grid Grid.Row="1">
    <InkCanvas x:Name="inkCanvas" />
    <InkToolbar x:Name="inkToolbar"
                VerticalAlignment="Top"
                TargetInkCanvas="{x:Bind inkCanvas}">
        <InkToolbarCustomPenButton
            CustomPen="{StaticResource CalligraphicPen}"
            Palette="{StaticResource CalligraphicPenPalette}"
            MinStrokeWidth="1" MaxStrokeWidth="3" SelectedStrokeWidth="2"
            SelectedBrushIndex ="1">
            <SymbolIcon Symbol="Favorite" />
            <InkToolbarCustomPenButton.ConfigurationContent>
                <InkToolbarPenConfigurationControl />
            </InkToolbarCustomPenButton.ConfigurationContent>
        </InkToolbarCustomPenButton>
    </InkToolbar>
</Grid>
```

### <a name="custom-toggle"></a><span data-ttu-id="20be9-266">カスタム トグル</span><span class="sxs-lookup"><span data-stu-id="20be9-266">Custom toggle</span></span>

<span data-ttu-id="20be9-267">カスタム トグル (カスタム トグル ボタンを使用してアクティブ化されます) を作成して、アプリ定義の機能の状態をオンまたはオフに設定できます。</span><span class="sxs-lookup"><span data-stu-id="20be9-267">You can create a custom toggle (activated through a custom toggle button) to set the state of an app-defined feature to on or off.</span></span> <span data-ttu-id="20be9-268">オンにすると、機能はアクティブなツールと連携して動作します。</span><span class="sxs-lookup"><span data-stu-id="20be9-268">When turned on, the feature works in conjunction with the active tool.</span></span>

<span data-ttu-id="20be9-269">この例では、タッチ入力による手書き入力を可能にするカスタム トグル ボタンを定義しています (既定では、タッチの手書き入力は有効化されていません)。</span><span class="sxs-lookup"><span data-stu-id="20be9-269">In this example, we define a custom toggle button that enables inking with touch input (by default, touch inking is not enabled).</span></span>

> [!NOTE]  
> <span data-ttu-id="20be9-270">タッチを使った手書き入力をサポートする必要がある場合は、この例で指定されたアイコンとツールチップを使い、CustomToggleButton を使用して手書き入力を有効化することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="20be9-270">If you need to support inking with touch, we recommended that you enable it using a CustomToggleButton, with the icon and tooltip specified in this example.</span></span>

<span data-ttu-id="20be9-271">通常タッチ入力は、オブジェクトまたはアプリの UI を直接操作するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-271">Typically, touch input is used for direct manipulation of an object or the app UI.</span></span> <span data-ttu-id="20be9-272">タッチによる手書き入力を有効化したときの動作の違いを示すために、InkCanvas を ScrollViewer コンテナ内に配置し、ScrollViewer のサイズを InkCanvas よりも小さく設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-272">To demonstrate the differences in behavior when touch inking is enabled, we place the InkCanvas within a ScrollViewer container and set the dimensions of the ScrollViewer to be smaller than the InkCanvas.</span></span> 

<span data-ttu-id="20be9-273">アプリが起動すると、ペンによる手書き入力のみがサポートされ、タッチは手書き入力の入力面をパンまたはズームするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-273">When the app starts, only pen inking is supported and touch is used to pan or zoom the inking surface.</span></span> <span data-ttu-id="20be9-274">タッチによる手書き入力が有効化されていると、手書き入力の入力面をタッチ入力でパンまたはズームすることはできません。</span><span class="sxs-lookup"><span data-stu-id="20be9-274">When touch inking is enabled, the inking surface cannot be panned or zoomed through touch input.</span></span>

> [!NOTE]
> <span data-ttu-id="20be9-275">[  **InkCanvas**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkCanvas) および [**InkToolbar**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbar) の UX ガイドラインは、「[インク コントロール](../controls-and-patterns/inking-controls.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20be9-275">See [Inking controls](../controls-and-patterns/inking-controls.md) for both [**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkCanvas) and [**InkToolbar**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbar) UX guidelines.</span></span> <span data-ttu-id="20be9-276">次の推奨事項は、この例に関連したものです。</span><span class="sxs-lookup"><span data-stu-id="20be9-276">The following recommendations are relevant to this example:</span></span>
> - <span data-ttu-id="20be9-277">[  **InkToolbar**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbar) と手書き入力全般は、アクティブなペンを通じて最適なエクスペリエンスを実現します。</span><span class="sxs-lookup"><span data-stu-id="20be9-277">The [**InkToolbar**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbar), and inking in general, is best experienced through an active pen.</span></span> <span data-ttu-id="20be9-278">ただし、アプリで必要な場合は、マウスやタッチによる手書き入力をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="20be9-278">However, inking with mouse and touch can be supported if required by your app.</span></span> 
> - <span data-ttu-id="20be9-279">タッチ入力による手書き入力をサポートする場合、トグル ボタンに "Segoe MLD2 アセット" フォントの "ED5F" アイコンを使うと共に、"タッチによる手書き" というヒントを表示することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="20be9-279">If supporting inking with touch input, we recommend using the "ED5F" icon from the "Segoe MLD2 Assets" font for the toggle button, with a "Touch writing" tooltip.</span></span> 

<span data-ttu-id="20be9-280">**XAML**</span><span class="sxs-lookup"><span data-stu-id="20be9-280">**XAML**</span></span>

1. <span data-ttu-id="20be9-281">まず、イベント ハンドラー (Toggle_Custom) を指定する Click イベント リスナーを持つ [**InkToolbarCustomToggleButton**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbarCustomToggleButton) 要素 (toggleButton) を宣言します。</span><span class="sxs-lookup"><span data-stu-id="20be9-281">First, we declare an [**InkToolbarCustomToggleButton**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbarCustomToggleButton) element (toggleButton) with a Click event listener that specifies the event handler (Toggle_Custom).</span></span>

```xaml 
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <StackPanel Grid.Row="0" 
                x:Name="HeaderPanel" 
                Orientation="Horizontal">
        <TextBlock x:Name="Header" 
                   Text="Basic ink sample" 
                   Style="{ThemeResource HeaderTextBlockStyle}" 
                   Margin="10" />
    </StackPanel>

    <ScrollViewer Grid.Row="1" 
                  HorizontalScrollBarVisibility="Auto" 
                  VerticalScrollBarVisibility="Auto">
        
        <Grid HorizontalAlignment="Left" VerticalAlignment="Top">
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
            
            <InkToolbar Grid.Row="0" 
                        Margin="10"
                        x:Name="inkToolbar" 
                        VerticalAlignment="Top"
                        TargetInkCanvas="{x:Bind inkCanvas}">
                <InkToolbarCustomToggleButton 
                x:Name="toggleButton" 
                Click="CustomToggle_Click" 
                ToolTipService.ToolTip="Touch Writing">
                    <SymbolIcon Symbol="{x:Bind TouchWritingIcon}"/>
                </InkToolbarCustomToggleButton>
            </InkToolbar>
            
            <ScrollViewer Grid.Row="1" 
                          Height="500"
                          Width="500"
                          x:Name="scrollViewer" 
                          ZoomMode="Enabled" 
                          MinZoomFactor=".1" 
                          VerticalScrollMode="Enabled" 
                          VerticalScrollBarVisibility="Auto" 
                          HorizontalScrollMode="Enabled" 
                          HorizontalScrollBarVisibility="Auto">
                
                <Grid x:Name="outputGrid" 
                      Height="1000"
                      Width="1000"
                      Background="{ThemeResource SystemControlBackgroundChromeWhiteBrush}">
                    <InkCanvas x:Name="inkCanvas"/>
                </Grid>
                
            </ScrollViewer>
        </Grid>
    </ScrollViewer>
</Grid>
```

<span data-ttu-id="20be9-282">**分離コード**</span><span class="sxs-lookup"><span data-stu-id="20be9-282">**Code-behind**</span></span>

2. <span data-ttu-id="20be9-283">前のスニペットでは、タッチによる手書き入力 (toggleButton) のカスタム トグル ボタンの Click イベント リスナーとハンドラー (Toggle_Custom) を宣言しました。</span><span class="sxs-lookup"><span data-stu-id="20be9-283">In the previous snippet, we declared a Click event listener and handler (Toggle_Custom) on the custom toggle button for touch inking (toggleButton).</span></span> <span data-ttu-id="20be9-284">このハンドラーは、InkPresenter の InputDeviceTypes プロパティを使って、CoreInputDeviceTypes.Touch のサポートを単にトグルします。</span><span class="sxs-lookup"><span data-stu-id="20be9-284">This handler simply toggles support for CoreInputDeviceTypes.Touch through the InputDeviceTypes property of the InkPresenter.</span></span>

   <span data-ttu-id="20be9-285">また、SymbolIcon 要素と、コードビハインド ファイル (TouchWritingIcon) で定義されたフィールドにバインドする {x：Bind} マークアップ拡張を使用して、ボタンのアイコンを指定しました。</span><span class="sxs-lookup"><span data-stu-id="20be9-285">We also specified an icon for the button using the SymbolIcon element and the {x:Bind} markup extension that binds it to a field defined in the code-behind file (TouchWritingIcon).</span></span>

   <span data-ttu-id="20be9-286">次のスニペットには、Click イベント ハンドラーと TouchWritingIcon の定義の両方が含まれています。</span><span class="sxs-lookup"><span data-stu-id="20be9-286">The following snippet includes both the Click event handler and the definition of TouchWritingIcon.</span></span>

```csharp 
namespace Ink_Basic_InkToolbar
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage_AddCustomToggle : Page
    {
        Symbol TouchWritingIcon = (Symbol)0xED5F;

        public MainPage_AddCustomToggle()
        {
            this.InitializeComponent();
        }

        // Handler for the custom toggle button that enables touch inking.
        private void CustomToggle_Click(object sender, RoutedEventArgs e)
        {
            if (toggleButton.IsChecked == true)
            {
                inkCanvas.InkPresenter.InputDeviceTypes |= CoreInputDeviceTypes.Touch;
            }
            else
            {
                inkCanvas.InkPresenter.InputDeviceTypes &= ~CoreInputDeviceTypes.Touch;
            }
        }
    }
}
```

### <a name="custom-tool"></a><span data-ttu-id="20be9-287">カスタム ツール</span><span class="sxs-lookup"><span data-stu-id="20be9-287">Custom tool</span></span>

<span data-ttu-id="20be9-288">カスタム ツール ボタンを作成して、アプリで定義されたペン以外のツールを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="20be9-288">You can create a custom tool button to invoke a non-pen tool that is defined by your app.</span></span>

<span data-ttu-id="20be9-289">既定では、[**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkPresenter) はすべての入力をインク ストロークか消去ストロークとして処理します。</span><span class="sxs-lookup"><span data-stu-id="20be9-289">By default, an [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkPresenter) processes all input as either an ink stroke or an erase stroke.</span></span> <span data-ttu-id="20be9-290">これには、セカンダリ ハードウェア アフォーダンス (ペン バレル ボタン、マウスの右ボタンなど) によって変更された入力も含まれます。</span><span class="sxs-lookup"><span data-stu-id="20be9-290">This includes input modified by a secondary hardware affordance such as a pen barrel button, a right mouse button, or similar.</span></span> <span data-ttu-id="20be9-291">ただし、[**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkPresenter) は、特定の入力を未処理のままにするように設定でき、それをカスタム処理のためにアプリに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="20be9-291">However, [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkPresenter) can be configured to leave specific input unprocessed, which can then be passed through to your app for custom processing.</span></span>

<span data-ttu-id="20be9-292">この例では、カスタム ツール ボタンを定義しており、これを選択すると、後続のストロークはインクではなく、なげなわ選択 (破線) として処理されてレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="20be9-292">In this example, we define a custom tool button that, when selected, causes subsequent strokes to be processed and rendered as a selection lasso (dashed line) instead of ink.</span></span> <span data-ttu-id="20be9-293">選択領域の範囲内のすべてのインク ストロークが [**Selected**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkStroke.Selected) に設定されます。</span><span class="sxs-lookup"><span data-stu-id="20be9-293">All ink strokes within the bounds of the selection area are set to [**Selected**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkStroke.Selected).</span></span>

> [!NOTE]
> <span data-ttu-id="20be9-294">InkCanvas および InkToolbar の UX ガイドラインは、「インク コントロール」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20be9-294">See Inking controls for both InkCanvas and InkToolbar UX guidelines.</span></span> <span data-ttu-id="20be9-295">次の推奨事項は、この例に関連したものです。</span><span class="sxs-lookup"><span data-stu-id="20be9-295">The following recommendation is relevant to this example:</span></span>
> - <span data-ttu-id="20be9-296">ストローク選択を提供する場合は、「選択ツール」ツールチップを使用して、ツール ボタンの "Segoe MLD2 アセット" フォントの "EF20" アイコンを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="20be9-296">If providing stroke selection, we recommend using the "EF20" icon from the "Segoe MLD2 Assets" font for the tool button, with a "Selection tool" tooltip.</span></span> 
 
<span data-ttu-id="20be9-297">**XAML**</span><span class="sxs-lookup"><span data-stu-id="20be9-297">**XAML**</span></span>

1. <span data-ttu-id="20be9-298">まず、ストローク選択が構成されているイベント ハンドラー (customToolButton_Click) を指定する Click イベント リスナーを持つ [**InkToolbarCustomToolButton**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbarCustomToolButton) 要素 (customToolButton) を宣言します。</span><span class="sxs-lookup"><span data-stu-id="20be9-298">First, we declare an [**InkToolbarCustomToolButton**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbarCustomToolButton) element (customToolButton) with a Click event listener that specifies the event handler (customToolButton_Click) where stroke selection is configured.</span></span> <span data-ttu-id="20be9-299">(ストローク選択のコピー、切り取り、貼り付けのための一連のボタンも追加しました。)</span><span class="sxs-lookup"><span data-stu-id="20be9-299">(We've also added a set of buttons for copying, cutting, and pasting the stroke selection.)</span></span>

2. <span data-ttu-id="20be9-300">選択ストロークを描画するための Canvas 要素も追加します。</span><span class="sxs-lookup"><span data-stu-id="20be9-300">We also add a Canvas element for drawing our selection stroke.</span></span> <span data-ttu-id="20be9-301">別のレイヤーを使って選択ストロークを描画すると、[**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkCanvas) とそのコンテンツは影響を受けることがありません。</span><span class="sxs-lookup"><span data-stu-id="20be9-301">Using a separate layer to draw the selection stroke ensures the [**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkCanvas) and its content remain untouched.</span></span> 

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header" 
                   Text="Basic ink sample" 
                   Style="{ThemeResource HeaderTextBlockStyle}" 
                   Margin="10,0,0,0" />
    </StackPanel>
    <StackPanel x:Name="ToolPanel" Orientation="Horizontal" Grid.Row="1">
        <InkToolbar x:Name="inkToolbar" 
                    VerticalAlignment="Top" 
                    TargetInkCanvas="{x:Bind inkCanvas}">
            <InkToolbarCustomToolButton 
                x:Name="customToolButton" 
                Click="customToolButton_Click" 
                ToolTipService.ToolTip="Selection tool">
                <SymbolIcon Symbol="{x:Bind SelectIcon}"/>
            </InkToolbarCustomToolButton>
        </InkToolbar>
        <Button x:Name="cutButton" 
                Content="Cut" 
                Click="cutButton_Click"
                Width="100"
                Margin="5,0,0,0"/>
        <Button x:Name="copyButton" 
                Content="Copy"  
                Click="copyButton_Click"
                Width="100"
                Margin="5,0,0,0"/>
        <Button x:Name="pasteButton" 
                Content="Paste"  
                Click="pasteButton_Click"
                Width="100"
                Margin="5,0,0,0"/>
    </StackPanel>
    <Grid Grid.Row="2" x:Name="outputGrid" 
              Background="{ThemeResource SystemControlBackgroundChromeWhiteBrush}" 
              Height="Auto">
        <!-- Canvas for displaying selection UI. -->
        <Canvas x:Name="selectionCanvas"/>
        <!-- Canvas for displaying ink. -->
        <InkCanvas x:Name="inkCanvas" />
    </Grid>
</Grid>
```

<span data-ttu-id="20be9-302">**分離コード**</span><span class="sxs-lookup"><span data-stu-id="20be9-302">**Code-behind**</span></span>

2. <span data-ttu-id="20be9-303">次に、MainPage.xaml.cs コードビハインド ファイルの [**InkToolbarCustomToolButton**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbarCustomToolButton) の Click イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="20be9-303">We then handle the Click event for the [**InkToolbarCustomToolButton**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Xaml.Controls.InkToolbarCustomToolButton) in the MainPage.xaml.cs code-behind file.</span></span>

   <span data-ttu-id="20be9-304">このハンドラは、未処理の入力をアプリに渡すように [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkPresenter) を設定します。</span><span class="sxs-lookup"><span data-stu-id="20be9-304">This handler configures the [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/Windows.UI.Input.Inking.InkPresenter) to pass unprocessed input through to the app.</span></span> 

   <span data-ttu-id="20be9-305">このコードをより詳細なステップ。パススルーの入力の高度な処理のセクションを参照してください[UWP アプリでの相互作用と Windows の手描き入力をペン](pen-and-stylus-interactions.md)します。</span><span class="sxs-lookup"><span data-stu-id="20be9-305">For a more detailed step through of this code:  See the Pass-through input for advanced processing section of [Pen interactions and Windows Ink in UWP apps](pen-and-stylus-interactions.md).</span></span>

   <span data-ttu-id="20be9-306">また、SymbolIcon 要素と、コードビハインド ファイル (SelectIcon) で定義されたフィールドにバインドする {x：Bind} マークアップ拡張を使用して、ボタンのアイコンを指定しました。</span><span class="sxs-lookup"><span data-stu-id="20be9-306">We also specified an icon for the button using the SymbolIcon element and the {x:Bind} markup extension that binds it to a field defined in the code-behind file (SelectIcon).</span></span>

   <span data-ttu-id="20be9-307">次のスニペットには、Click イベント ハンドラーと SelectIcon の定義の両方が含まれています。</span><span class="sxs-lookup"><span data-stu-id="20be9-307">The following snippet includes both the Click event handler and the definition of SelectIcon.</span></span>

```csharp
namespace Ink_Basic_InkToolbar
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage_AddCustomTool : Page
    {
        // Icon for custom selection tool button.
        Symbol SelectIcon = (Symbol)0xEF20;

        // Stroke selection tool.
        private Polyline lasso;
        // Stroke selection area.
        private Rect boundingRect;

        public MainPage_AddCustomTool()
        {
            this.InitializeComponent();

            // Listen for new ink or erase strokes to clean up selection UI.
            inkCanvas.InkPresenter.StrokeInput.StrokeStarted +=
                StrokeInput_StrokeStarted;
            inkCanvas.InkPresenter.StrokesErased +=
                InkPresenter_StrokesErased;
        }

        private void customToolButton_Click(object sender, RoutedEventArgs e)
        {
            // By default, the InkPresenter processes input modified by 
            // a secondary affordance (pen barrel button, right mouse 
            // button, or similar) as ink.
            // To pass through modified input to the app for custom processing 
            // on the app UI thread instead of the background ink thread, set 
            // InputProcessingConfiguration.RightDragAction to LeaveUnprocessed.
            inkCanvas.InkPresenter.InputProcessingConfiguration.RightDragAction =
                InkInputRightDragAction.LeaveUnprocessed;

            // Listen for unprocessed pointer events from modified input.
            // The input is used to provide selection functionality.
            inkCanvas.InkPresenter.UnprocessedInput.PointerPressed +=
                UnprocessedInput_PointerPressed;
            inkCanvas.InkPresenter.UnprocessedInput.PointerMoved +=
                UnprocessedInput_PointerMoved;
            inkCanvas.InkPresenter.UnprocessedInput.PointerReleased +=
                UnprocessedInput_PointerReleased;
        }

        // Handle new ink or erase strokes to clean up selection UI.
        private void StrokeInput_StrokeStarted(
            InkStrokeInput sender, Windows.UI.Core.PointerEventArgs args)
        {
            ClearSelection();
        }

        private void InkPresenter_StrokesErased(
            InkPresenter sender, InkStrokesErasedEventArgs args)
        {
            ClearSelection();
        }

        private void cutButton_Click(object sender, RoutedEventArgs e)
        {
            inkCanvas.InkPresenter.StrokeContainer.CopySelectedToClipboard();
            inkCanvas.InkPresenter.StrokeContainer.DeleteSelected();
            ClearSelection();
        }

        private void copyButton_Click(object sender, RoutedEventArgs e)
        {
            inkCanvas.InkPresenter.StrokeContainer.CopySelectedToClipboard();
        }

        private void pasteButton_Click(object sender, RoutedEventArgs e)
        {
            if (inkCanvas.InkPresenter.StrokeContainer.CanPasteFromClipboard())
            {
                inkCanvas.InkPresenter.StrokeContainer.PasteFromClipboard(
                    new Point(0, 0));
            }
            else
            {
                // Cannot paste from clipboard.
            }
        }

        // Clean up selection UI.
        private void ClearSelection()
        {
            var strokes = inkCanvas.InkPresenter.StrokeContainer.GetStrokes();
            foreach (var stroke in strokes)
            {
                stroke.Selected = false;
            }
            ClearBoundingRect();
        }

        private void ClearBoundingRect()
        {
            if (selectionCanvas.Children.Any())
            {
                selectionCanvas.Children.Clear();
                boundingRect = Rect.Empty;
            }
        }

        // Handle unprocessed pointer events from modifed input.
        // The input is used to provide selection functionality.
        // Selection UI is drawn on a canvas under the InkCanvas.
        private void UnprocessedInput_PointerPressed(
            InkUnprocessedInput sender, PointerEventArgs args)
        {
            // Initialize a selection lasso.
            lasso = new Polyline()
            {
                Stroke = new SolidColorBrush(Windows.UI.Colors.Blue),
                StrokeThickness = 1,
                StrokeDashArray = new DoubleCollection() { 5, 2 },
            };

            lasso.Points.Add(args.CurrentPoint.RawPosition);

            selectionCanvas.Children.Add(lasso);
        }

        private void UnprocessedInput_PointerMoved(
            InkUnprocessedInput sender, PointerEventArgs args)
        {
            // Add a point to the lasso Polyline object.
            lasso.Points.Add(args.CurrentPoint.RawPosition);
        }

        private void UnprocessedInput_PointerReleased(
            InkUnprocessedInput sender, PointerEventArgs args)
        {
            // Add the final point to the Polyline object and 
            // select strokes within the lasso area.
            // Draw a bounding box on the selection canvas 
            // around the selected ink strokes.
            lasso.Points.Add(args.CurrentPoint.RawPosition);

            boundingRect =
                inkCanvas.InkPresenter.StrokeContainer.SelectWithPolyLine(
                    lasso.Points);

            DrawBoundingRect();
        }

        // Draw a bounding rectangle, on the selection canvas, encompassing 
        // all ink strokes within the lasso area.
        private void DrawBoundingRect()
        {
            // Clear all existing content from the selection canvas.
            selectionCanvas.Children.Clear();

            // Draw a bounding rectangle only if there are ink strokes 
            // within the lasso area.
            if (!((boundingRect.Width == 0) ||
                (boundingRect.Height == 0) ||
                boundingRect.IsEmpty))
            {
                var rectangle = new Rectangle()
                {
                    Stroke = new SolidColorBrush(Windows.UI.Colors.Blue),
                    StrokeThickness = 1,
                    StrokeDashArray = new DoubleCollection() { 5, 2 },
                    Width = boundingRect.Width,
                    Height = boundingRect.Height
                };

                Canvas.SetLeft(rectangle, boundingRect.X);
                Canvas.SetTop(rectangle, boundingRect.Y);

                selectionCanvas.Children.Add(rectangle);
            }
        }
    }
}
```



### <a name="custom-ink-rendering"></a><span data-ttu-id="20be9-308">カスタム インク レンダリング</span><span class="sxs-lookup"><span data-stu-id="20be9-308">Custom ink rendering</span></span>

<span data-ttu-id="20be9-309">既定では、手書き入力は低待機時間のバックグラウンド スレッドで処理され、描画と同時に "ウェット" レンダリングが行われます。</span><span class="sxs-lookup"><span data-stu-id="20be9-309">By default, ink input is processed on a low-latency background thread and rendered "wet" as it is drawn.</span></span> <span data-ttu-id="20be9-310">ストロークが完了すると (ペンまたは指が画面を離れるか、マウスのボタンが離されると)、UI スレッドでストロークが処理されて、[**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/dn858535) レイヤーへの "ドライ" レンダリングが行われます (アプリケーション コンテンツの上にレンダリングされてウェット インクが置き換えられます)。</span><span class="sxs-lookup"><span data-stu-id="20be9-310">When the stroke is completed (pen or finger lifted, or mouse button released), the stroke is processed on the UI thread and rendered "dry" to the [**InkCanvas**](https://msdn.microsoft.com/library/windows/apps/dn858535) layer (above the application content and replacing the wet ink).</span></span>

<span data-ttu-id="20be9-311">インク プラットフォームでは、この動作を上書きして、手書き入力のカスタム ドライ レンダリングによって手書き入力エクスペリエンスを全面的にカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="20be9-311">The ink platform enables you to override this behavior and completely customize the inking experience by custom drying the ink input.</span></span>

<span data-ttu-id="20be9-312">カスタム ドライ レンダリングについて詳しくは、「[UWP アプリでのペン操作と Windows Ink](https://docs.microsoft.com/windows/uwp/design/input/pen-and-stylus-interactions#custom-ink-rendering)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="20be9-312">For more info on custom drying, see [Pen interactions and Windows Ink in UWP apps](https://docs.microsoft.com/windows/uwp/design/input/pen-and-stylus-interactions#custom-ink-rendering).</span></span>

> [!NOTE]
> <span data-ttu-id="20be9-313">カスタム ドライ レンダリングと [**InkToolbar**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx)</span><span class="sxs-lookup"><span data-stu-id="20be9-313">Custom drying and the [**InkToolbar**](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.inktoolbar.aspx)</span></span>  
> <span data-ttu-id="20be9-314">カスタム ドライの実装によって、アプリが [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/dn922011) の既定のインク レンダリング動作を上書きすると、レンダリングされたインク ストロークが InkToolbar で利用できなくなり、InkToolbar の組み込みの消去コマンドが正常に機能しなくなります。</span><span class="sxs-lookup"><span data-stu-id="20be9-314">If your app overrides the default ink rendering behavior of the [**InkPresenter**](https://msdn.microsoft.com/library/windows/apps/dn922011) with a custom drying implementation, the rendered ink strokes are no longer available to the InkToolbar and the built-in erase commands of the InkToolbar do not work as expected.</span></span> <span data-ttu-id="20be9-315">消去機能を提供するには、すべてのポインター イベントを処理し、ストロークごとにヒット テストを実行すると共に、組み込みの [すべてのインクのデータを消去] コマンドをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="20be9-315">To provide erase functionality, you must handle all pointer events, perform hit-testing on each stroke, and override the built-in "Erase all ink" command.</span></span>

## <a name="related-articles"></a><span data-ttu-id="20be9-316">関連記事</span><span class="sxs-lookup"><span data-stu-id="20be9-316">Related articles</span></span>

- [<span data-ttu-id="20be9-317">ペン操作とスタイラス操作</span><span class="sxs-lookup"><span data-stu-id="20be9-317">Pen and stylus interactions</span></span>](pen-and-stylus-interactions.md)

### <a name="topic-samples"></a><span data-ttu-id="20be9-318">トピックのサンプル</span><span class="sxs-lookup"><span data-stu-id="20be9-318">Topic samples</span></span>

- [<span data-ttu-id="20be9-319">インク ツールバー位置や向きのサンプル (基本)</span><span class="sxs-lookup"><span data-stu-id="20be9-319">Ink toolbar location and orientation sample (basic)</span></span>](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness.zip)
- [<span data-ttu-id="20be9-320">インク ツールバー位置や向きのサンプル (動的)</span><span class="sxs-lookup"><span data-stu-id="20be9-320">Ink toolbar location and orientation sample (dynamic)</span></span>](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness-dynamic.zip)

### <a name="other-samples"></a><span data-ttu-id="20be9-321">その他のサンプル</span><span class="sxs-lookup"><span data-stu-id="20be9-321">Other samples</span></span>

- [<span data-ttu-id="20be9-322">単純なインクのサンプル (C#/C++)</span><span class="sxs-lookup"><span data-stu-id="20be9-322">Simple ink sample (C#/C++)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620312)
- [<span data-ttu-id="20be9-323">複雑なインクのサンプル (C++)</span><span class="sxs-lookup"><span data-stu-id="20be9-323">Complex ink sample (C++)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620314)
- [<span data-ttu-id="20be9-324">インクのサンプル (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="20be9-324">Ink sample (JavaScript)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620308)
- [<span data-ttu-id="20be9-325">チュートリアルを開始します。UWP アプリでのインクをサポートします。</span><span class="sxs-lookup"><span data-stu-id="20be9-325">Get Started Tutorial: Support ink in your UWP app</span></span>](https://aka.ms/appsample-ink)
- [<span data-ttu-id="20be9-326">書籍のサンプルを色分け表示</span><span class="sxs-lookup"><span data-stu-id="20be9-326">Coloring book sample</span></span>](https://aka.ms/cpubsample-coloringbook)
- [<span data-ttu-id="20be9-327">ファミリのノートのサンプル</span><span class="sxs-lookup"><span data-stu-id="20be9-327">Family notes sample</span></span>](https://aka.ms/cpubsample-familynotessample)
