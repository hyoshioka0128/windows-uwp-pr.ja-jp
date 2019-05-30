---
description: スタイルを使うと、コントロールのプロパティに値を設定し、その設定を再利用することで、複数のコントロールの外観を統一できます。
MS-HAID: dev\_ctrl\_layout\_txt.styling\_controls
MSHAttr: PreferredLib:/library/windows/apps
Search.Product: eADQiWindows 10XVcnh
ms.date: 01/03/2019
title: XAML スタイル
ms.assetid: AB469A46-FAF5-42D0-9340-948D0EDF4150
label: XAML styles
template: detail.hbs
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: cd11427ed1b53641a25c32742ca114b121efcfe8
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66363963"
---
# <a name="xaml-styles"></a><span data-ttu-id="66e01-103">XAML スタイル</span><span class="sxs-lookup"><span data-stu-id="66e01-103">XAML styles</span></span>





<span data-ttu-id="66e01-104">XAML フレームワークを使って、さまざまな方法でアプリの外観をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="66e01-104">You can customize the appearance of your apps in many ways by using the XAML framework.</span></span> <span data-ttu-id="66e01-105">スタイルを使うと、コントロールのプロパティに値を設定し、その設定を再利用することで、複数のコントロールの外観を統一できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-105">Styles let you set control properties and reuse those settings for a consistent appearance across multiple controls.</span></span>

## <a name="style-basics"></a><span data-ttu-id="66e01-106">スタイルの基本</span><span class="sxs-lookup"><span data-stu-id="66e01-106">Style basics</span></span>

<span data-ttu-id="66e01-107">スタイルを使うと、視覚的なプロパティの設定を、再利用可能なリソースとして抽出できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-107">Use styles to extract visual property settings into reusable resources.</span></span> <span data-ttu-id="66e01-108">次の例は、[BorderBrush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderbrush)、[BorderThickness](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderthickness)、および [Foreground](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.foreground) プロパティを設定するスタイルを適用した 3 つのボタンを示しています。</span><span class="sxs-lookup"><span data-stu-id="66e01-108">Here's an example that shows 3 buttons with a style that sets the [BorderBrush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderbrush), [BorderThickness](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderthickness) and [Foreground](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.foreground) properties.</span></span> <span data-ttu-id="66e01-109">スタイルを適用することで、これらのプロパティを各コントロールで個別に設定しなくて済み、また、コントロールに同じ外観を持たせることができます。</span><span class="sxs-lookup"><span data-stu-id="66e01-109">By applying a style, you can make the controls appear the same without having to set these properties on each control separately.</span></span>

![スタイルを適用したボタン](images/styles-rainbow-buttons.png)

<span data-ttu-id="66e01-111">スタイルは、XAML を使ってコントロールに対してインラインで定義するか、再利用可能なリソースとして定義できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-111">You can define a style inline in the XAML for a control, or as a reusable resource.</span></span> <span data-ttu-id="66e01-112">リソースは、個々のページの XAML ファイル、App.xaml ファイル、別個のリソース ディクショナリ XAML ファイルのいずれかに定義します。</span><span class="sxs-lookup"><span data-stu-id="66e01-112">Define resources in an individual page's XAML file, in the App.xaml file, or in a separate resource dictionary XAML file.</span></span> <span data-ttu-id="66e01-113">リソース ディクショナリ XAML ファイルはアプリ間で共有できます。また、単一のアプリで複数のリソース ディクショナリをマージすることも可能です。</span><span class="sxs-lookup"><span data-stu-id="66e01-113">A resource dictionary XAML file can be shared across apps, and more than one resource dictionary can be merged in a single app.</span></span> <span data-ttu-id="66e01-114">リソースを定義する場所は、リソースが使われる範囲によって決まります。</span><span class="sxs-lookup"><span data-stu-id="66e01-114">Where the resource is defined determines the scope in which it can be used.</span></span> <span data-ttu-id="66e01-115">ページ レベルのリソースは定義元のページでしか利用できません。</span><span class="sxs-lookup"><span data-stu-id="66e01-115">Page-level resources are available only in the page where they are defined.</span></span> <span data-ttu-id="66e01-116">App.xaml とページ内の両方で同じキーが定義されている場合、ページ内のリソースが App.xaml 内のリソースよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="66e01-116">If resources with the same key are defined in both App.xaml and in a page, the resource in the page overrides the resource in App.xaml.</span></span> <span data-ttu-id="66e01-117">リソースが別個のリソース ディクショナリ ファイルで定義されている場合、そのスコープはリソース ディクショナリが参照される場所によって決まります。</span><span class="sxs-lookup"><span data-stu-id="66e01-117">If a resource is defined in a separate resource dictionary file, it's scope is determined by where the resource dictionary is referenced.</span></span>

<span data-ttu-id="66e01-118">[Style](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) の定義では、1 つの [TargetType](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.targettype) 属性と、1 つ以上の [Setter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) 要素が必要になります。</span><span class="sxs-lookup"><span data-stu-id="66e01-118">In the [Style](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) definition, you need a [TargetType](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.targettype) attribute and a collection of one or more [Setter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) elements.</span></span> <span data-ttu-id="66e01-119">**TargetType** 属性は、スタイルを適用する [FrameworkElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.FrameworkElement) 型を指定する文字列です。</span><span class="sxs-lookup"><span data-stu-id="66e01-119">The **TargetType** attribute is a string that specifies a [FrameworkElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.FrameworkElement) type to apply the style to.</span></span> <span data-ttu-id="66e01-120">**TargetType** の値では、Windows ランタイムか、参照先アセンブリ内で使用できるカスタム型で定義される **FrameworkElement** から派生した型を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66e01-120">The **TargetType** value must specify a **FrameworkElement**-derived type that's defined by the Windows Runtime or a custom type that's available in a referenced assembly.</span></span> <span data-ttu-id="66e01-121">適用しようとしているスタイルの **TargetType** 属性の指定内容と異なるコントロールやコントロールの型にスタイルを適用しようとすると、例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="66e01-121">If you try to apply a style to a control and the control's type doesn't match the **TargetType** attribute of the style you're trying to apply, an exception occurs.</span></span>

<span data-ttu-id="66e01-122">それぞれの [Setter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) 要素に、[Property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.setter.property) と [Value](https://docs.microsoft.com/uwp/api/windows.ui.xaml.setter.value) が必要です。</span><span class="sxs-lookup"><span data-stu-id="66e01-122">Each [Setter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) element requires a [Property](https://docs.microsoft.com/uwp/api/windows.ui.xaml.setter.property) and a [Value](https://docs.microsoft.com/uwp/api/windows.ui.xaml.setter.value).</span></span> <span data-ttu-id="66e01-123">この 2 つのプロパティは、それぞれ、その設定が適用されるコントロールのプロパティと、そのプロパティに対して設定される値を指定します。</span><span class="sxs-lookup"><span data-stu-id="66e01-123">These property settings indicate what control property the setting applies to, and the value to set for that property.</span></span> <span data-ttu-id="66e01-124">**Setter.Value** は、属性構文またはプロパティ要素構文を使って設定できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-124">You can set the **Setter.Value** with either attribute or property element syntax.</span></span> <span data-ttu-id="66e01-125">次の XAML は前に示したボタンに適用されたスタイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="66e01-125">The XAML here shows the style applied to the buttons shown previously.</span></span> <span data-ttu-id="66e01-126">この XAML では、最初の 2 つの **Setter** 要素に属性構文を使っていますが、[BorderBrush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderbrush) プロパティ用の最後の**Setter** にはプロパティ要素構文を使っています。</span><span class="sxs-lookup"><span data-stu-id="66e01-126">In this XAML, the first two **Setter** elements use attribute syntax, but the last **Setter**, for the [BorderBrush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderbrush) property, uses property element syntax.</span></span> <span data-ttu-id="66e01-127">この例では [x:Key attribute](../../xaml-platform/x-key-attribute.md) 属性を使っていないため、スタイルはボタンに対して暗黙的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="66e01-127">The example doesn't use the [x:Key attribute](../../xaml-platform/x-key-attribute.md) attribute, so the style is implicitly applied to the buttons.</span></span> <span data-ttu-id="66e01-128">スタイルの暗黙的または明示的な適用については、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="66e01-128">Applying styles implicitly or explicitly is explained in the next section.</span></span>

```XAML
<Page.Resources>
    <Style TargetType="Button">
        <Setter Property="BorderThickness" Value="5" />
        <Setter Property="Foreground" Value="Black" />
        <Setter Property="BorderBrush" >
            <Setter.Value>
                <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
                    <GradientStop Color="Yellow" Offset="0.0" />
                    <GradientStop Color="Red" Offset="0.25" />
                    <GradientStop Color="Blue" Offset="0.75" />
                    <GradientStop Color="LimeGreen" Offset="1.0" />
                </LinearGradientBrush>
            </Setter.Value>
        </Setter>
    </Style>
</Page.Resources>

<StackPanel Orientation="Horizontal">
    <Button Content="Button"/>
    <Button Content="Button"/>
    <Button Content="Button"/>
</StackPanel>
```

## <a name="apply-an-implicit-or-explicit-style"></a><span data-ttu-id="66e01-129">暗黙的または明示的なスタイルの適用</span><span class="sxs-lookup"><span data-stu-id="66e01-129">Apply an implicit or explicit style</span></span>

<span data-ttu-id="66e01-130">スタイルをリソースとして定義した場合、それをコントロールに適用するには 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="66e01-130">If you define a style as a resource, there are two ways to apply it to your controls:</span></span>

-   <span data-ttu-id="66e01-131">暗黙的な適用。[Style](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) に対して [TargetType](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.targettype) のみを指定します。</span><span class="sxs-lookup"><span data-stu-id="66e01-131">Implicitly, by specifying only a [TargetType](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.targettype) for the [Style](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style).</span></span>
-   <span data-ttu-id="66e01-132">明示的な適用。[Style](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) に対して [TargetType](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.targettype) と [x:Key](../../xaml-platform/x-key-attribute.md) 属性を設定した後、ターゲット コントロールの [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) プロパティに、明示的キーを使う [{StaticResource} markup extension](https://docs.microsoft.com/windows/uwp/xaml-platform/staticresource-markup-extension) 参照を設定します。</span><span class="sxs-lookup"><span data-stu-id="66e01-132">Explicitly, by specifying a [TargetType](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.targettype) and an [x:Key attribute](../../xaml-platform/x-key-attribute.md) attribute for the [Style](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) and then by setting the target control's [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) property with a [{StaticResource} markup extension](https://docs.microsoft.com/windows/uwp/xaml-platform/staticresource-markup-extension) reference that uses the explicit key.</span></span>

<span data-ttu-id="66e01-133">スタイルに [x:Key](../../xaml-platform/x-key-attribute.md) 属性が含まれる場合、そのスタイルをコントロールに適用するには、コントロールの [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) プロパティをキーで指定されたスタイルに設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66e01-133">If a style contains the [x:Key attribute](../../xaml-platform/x-key-attribute.md), you can only apply it to a control by setting the [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) property of the control to the keyed style.</span></span> <span data-ttu-id="66e01-134">一方、x:Key attribute 属性を含まないスタイルは、ターゲットとなる型のすべてのコントロールに自動的に適用されます。それ以外の場合、これには明示的なスタイル設定がありません。</span><span class="sxs-lookup"><span data-stu-id="66e01-134">In contrast, a style without an x:Key attribute is automatically applied to every control of its target type, that doesn't otherwise have an explicit style setting.</span></span>

<span data-ttu-id="66e01-135">次の 2 つのボタンは、暗黙的なスタイルと明示的なスタイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="66e01-135">Here are two buttons that demonstrate implicit and explicit styles.</span></span>

![暗黙的および明示的にスタイルが適用されたボタン。](images/styles-buttons-implicit-explicit.png)

<span data-ttu-id="66e01-137">この例では、最初のスタイルには [x:Key](../../xaml-platform/x-key-attribute.md) 属性が含まれ、ターゲットとなる型は [Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button) です。</span><span class="sxs-lookup"><span data-stu-id="66e01-137">In this example, the first style has an [x:Key attribute](../../xaml-platform/x-key-attribute.md) and its target type is [Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button).</span></span> <span data-ttu-id="66e01-138">最初のボタンの [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) プロパティはこのキーに設定されているため、このスタイルは明示的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="66e01-138">The first button's [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.style) property is set to this key, so this style is applied explicitly.</span></span> <span data-ttu-id="66e01-139">2 番目のスタイルは、ターゲットとなる型が **Button** で、スタイルに x:Key 属性が含まれないため、2 番目のボタンに暗黙的に適用されます。</span><span class="sxs-lookup"><span data-stu-id="66e01-139">The second style is applied implicitly to the second button because its target type is **Button** and the style doesn't have an x:Key attribute.</span></span>

```XAML
<Page.Resources>
    <Style x:Key="PurpleStyle" TargetType="Button">
        <Setter Property="FontFamily" Value="Segoe UI"/>
        <Setter Property="FontSize" Value="14"/>
        <Setter Property="Foreground" Value="Purple"/>
    </Style>

    <Style TargetType="Button">
        <Setter Property="FontFamily" Value="Segoe UI"/>
        <Setter Property="FontSize" Value="14"/>
        <Setter Property="RenderTransform">
            <Setter.Value>
                <RotateTransform Angle="25"/>
            </Setter.Value>
        </Setter>
        <Setter Property="BorderBrush" Value="Green"/>
        <Setter Property="BorderThickness" Value="2"/>
        <Setter Property="Foreground" Value="Green"/>
    </Style>
</Page.Resources>

<Grid x:Name="LayoutRoot">
    <Button Content="Button" Style="{StaticResource PurpleStyle}"/>
    <Button Content="Button"/>
</Grid>
```

## <a name="use-based-on-styles"></a><span data-ttu-id="66e01-140">継承スタイルの使用</span><span class="sxs-lookup"><span data-stu-id="66e01-140">Use based-on styles</span></span>

<span data-ttu-id="66e01-141">スタイルを管理しやすくし、スタイルの再利用を最適化するために、他のスタイルから継承するスタイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-141">To make styles easier to maintain and to optimize style reuse, you can create styles that inherit from other styles.</span></span> <span data-ttu-id="66e01-142">継承したスタイルを作成するには、[BasedOn](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.basedon) プロパティを使います。</span><span class="sxs-lookup"><span data-stu-id="66e01-142">You use the [BasedOn](https://docs.microsoft.com/uwp/api/windows.ui.xaml.style.basedon) property to create inherited styles.</span></span> <span data-ttu-id="66e01-143">他のスタイルから継承するスタイルは、同じ型のコントロール、または基本スタイルのターゲットとなる型から派生したコントロールをターゲットとする必要があります。</span><span class="sxs-lookup"><span data-stu-id="66e01-143">Styles that inherit from other styles must target the same type of control or a control that derives from the type targeted by the base style.</span></span> <span data-ttu-id="66e01-144">たとえば、基本スタイルのターゲットが [ContentControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ContentControl) である場合、このスタイルに基づくスタイルは、**ContentControl**、または **ContentControl** から派生した型 ([Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button)、[ScrollViewer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer) など) をターゲットにできます。</span><span class="sxs-lookup"><span data-stu-id="66e01-144">For example, if a base style targets [ContentControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ContentControl), styles that are based on this style can target **ContentControl** or types that derive from **ContentControl** such as [Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button) and [ScrollViewer](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer).</span></span> <span data-ttu-id="66e01-145">継承スタイルに対して設定しない値は、基本スタイルから継承されます。</span><span class="sxs-lookup"><span data-stu-id="66e01-145">If a value is not set in the based-on style, it's inherited from the base style.</span></span> <span data-ttu-id="66e01-146">基本スタイルから値を変更するには、継承スタイルに値を設定して上書きします。</span><span class="sxs-lookup"><span data-stu-id="66e01-146">To change a value from the base style, the based-on style overrides that value.</span></span> <span data-ttu-id="66e01-147">次の例は、同じ基本スタイルから継承したスタイルを持つ **Button** と [CheckBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) を示しています。</span><span class="sxs-lookup"><span data-stu-id="66e01-147">The next example shows a **Button** and a [CheckBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) with styles that inherit from the same base style.</span></span>

![継承スタイルを使ってスタイルを適用したボタン。](images/styles-buttons-based-on.png)

<span data-ttu-id="66e01-149">基本スタイルは [ContentControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ContentControl) をターゲットとし、[Height](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) プロパティと [Width](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="66e01-149">The base style targets [ContentControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ContentControl), and sets the [Height](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height), and [Width](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) properties.</span></span> <span data-ttu-id="66e01-150">このスタイルに基づくスタイルは、**ContentControl** から派生した [CheckBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) と [Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button) をターゲットとします。</span><span class="sxs-lookup"><span data-stu-id="66e01-150">The styles based on this style target [CheckBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) and [Button](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Button), which derive from **ContentControl**.</span></span> <span data-ttu-id="66e01-151">各継承スタイルでは、[BorderBrush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderbrush) プロパティと [Foreground](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.foreground) プロパティに異なる色を設定しています </span><span class="sxs-lookup"><span data-stu-id="66e01-151">The based-on styles set different colors for the [BorderBrush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.borderbrush) and [Foreground](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.foreground) properties.</span></span> <span data-ttu-id="66e01-152">(通常、**CheckBox** の周囲には境界線を配置しません。</span><span class="sxs-lookup"><span data-stu-id="66e01-152">(You don't typically put a border around a **CheckBox**.</span></span> <span data-ttu-id="66e01-153">ここでは、スタイルの効果を示すためにこのように設定しています)。</span><span class="sxs-lookup"><span data-stu-id="66e01-153">We do it here to show the effects of the style.)</span></span>

```XAML
<Page.Resources>
    <Style x:Key="BasicStyle" TargetType="ContentControl">
        <Setter Property="Width" Value="130" />
        <Setter Property="Height" Value="30" />
    </Style>

    <Style x:Key="ButtonStyle" TargetType="Button"
           BasedOn="{StaticResource BasicStyle}">
        <Setter Property="BorderBrush" Value="Orange" />
        <Setter Property="BorderThickness" Value="2" />
        <Setter Property="Foreground" Value="Red" />
    </Style>

    <Style x:Key="CheckBoxStyle" TargetType="CheckBox"
           BasedOn="{StaticResource BasicStyle}">
        <Setter Property="BorderBrush" Value="Blue" />
        <Setter Property="BorderThickness" Value="2" />
        <Setter Property="Foreground" Value="Green" />
    </Style>
</Page.Resources>

<StackPanel>
    <Button Content="Button" Style="{StaticResource ButtonStyle}" Margin="0,10"/>
    <CheckBox Content="CheckBox" Style="{StaticResource CheckBoxStyle}"/>
</StackPanel>
```

## <a name="use-tools-to-work-with-styles-easily"></a><span data-ttu-id="66e01-154">ツールを使ってスタイルを簡単に操作</span><span class="sxs-lookup"><span data-stu-id="66e01-154">Use tools to work with styles easily</span></span>

<span data-ttu-id="66e01-155">コントロールにスタイルをすばやく適用する方法の 1 つは、Microsoft Visual Studio の XAML デザイン サーフェイスでコントロールを右クリックし、 **[スタイルの編集]** または **[テンプレートの編集]** (右クリックしたコントロールによって異なる) をクリックすることです。</span><span class="sxs-lookup"><span data-stu-id="66e01-155">A fast way to apply styles to your controls is to right-click on a control on the Microsoft Visual Studio XAML design surface and select **Edit Style** or **Edit Template** (depending on the control you are right-clicking on).</span></span> <span data-ttu-id="66e01-156">その後、 **[リソースの適用]** をクリックして既にあるスタイルを適用するか、または **[空アイテムの作成]** をクリックして新しいスタイルを定義できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-156">You can then apply an existing style by selecting **Apply Resource** or define a new style by selecting **Create Empty**.</span></span> <span data-ttu-id="66e01-157">空のスタイルを作成する場合は、ページ、App.xaml ファイル、または別のリソース ディクショナリにそのスタイルを定義できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-157">If you create an empty style, you are given the option to define it in the page, in the App.xaml file, or in a separate resource dictionary.</span></span>

## <a name="lightweight-styling"></a><span data-ttu-id="66e01-158">軽量なスタイル設定</span><span class="sxs-lookup"><span data-stu-id="66e01-158">Lightweight styling</span></span>

<span data-ttu-id="66e01-159">システム ブラシのオーバーライドは一般にアプリ レベルまたはページ レベルで行われます。いずれの場合も、色のオーバーライドはそのブラシを参照するすべてのコントロールに影響します。また、XAML では多くのコントロールが同じシステム ブラシを参照できます。</span><span class="sxs-lookup"><span data-stu-id="66e01-159">Overriding the system brushes is generally done at the App or Page level, and in either case the color override will affect all controls that reference that brush – and in XAML many controls can reference the same system brush.</span></span>

![スタイルを適用したボタン](images/LightweightStyling_ButtonStatesExample.png)

```XAML
<Page.Resources>
    <ResourceDictionary>
        <ResourceDictionary.ThemeDictionaries>
            <ResourceDictionary x:Key="Light">
                 <SolidColorBrush x:Key="ButtonBackground" Color="Transparent"/>
                 <SolidColorBrush x:Key="ButtonForeground" Color="MediumSlateBlue"/>
                 <SolidColorBrush x:Key="ButtonBorderBrush" Color="MediumSlateBlue"/>
            </ResourceDictionary>
        </ResourceDictionary.ThemeDictionaries>
    </ResourceDictionary>
</Page.Resources>
```

<span data-ttu-id="66e01-161">PointerOver (マウスがボタンの上に置かれている)、**PointerPressed** (ボタンが押された)、Disabled (ボタンが有効でない) などの状態に使用します。</span><span class="sxs-lookup"><span data-stu-id="66e01-161">For states like PointerOver (mouse is hovered over the button), **PointerPressed** (button has been invoked), or Disabled (button is not interactable).</span></span> <span data-ttu-id="66e01-162">元の簡易スタイル名には、これらの終わりが追加されます。**ButtonBackgroundPointerOver**、 **ButtonForegroundPointerPressed**、 **ButtonBorderBrushDisabled**など。それらの変更ブラシ同様に、確認コントロールは、アプリのテーマに一貫して表示します。</span><span class="sxs-lookup"><span data-stu-id="66e01-162">These endings are appended onto the original Lightweight styling names: **ButtonBackgroundPointerOver**, **ButtonForegroundPointerPressed**, **ButtonBorderBrushDisabled**, etc. Modifying those brushes as well, will make sure that your controls are colored consistently to your app's theme.</span></span>

<span data-ttu-id="66e01-163">これらのブラシを配置すると、**App.Resources** レベルでオーバーライドし、(単一ページではなく) アプリ全体のすべてのボタンを変更します。</span><span class="sxs-lookup"><span data-stu-id="66e01-163">Placing these brush overrides at the **App.Resources** level, will alter all the buttons within the entire app, instead of on a single page.</span></span>

### <a name="per-control-styling"></a><span data-ttu-id="66e01-164">コントロールごとのスタイル設定</span><span class="sxs-lookup"><span data-stu-id="66e01-164">Per-control styling</span></span>

<span data-ttu-id="66e01-165">他のケースでは、コントロールの他のバージョンを変更することなく、1 つのページ上の単一のコントロールを特定の方法で表示するように変更することが望ましい方法です。</span><span class="sxs-lookup"><span data-stu-id="66e01-165">In other cases, changing a single control on one page only to look a certain way, without altering any other versions of that control, is desired:</span></span>

![スタイルを適用したボタン](images/LightweightStyling_CheckboxExample.png)

```XAML
<CheckBox Content="Normal CheckBox" Margin="5"/>
    <CheckBox Content="Special CheckBox" Margin="5">
        <CheckBox.Resources>
            <ResourceDictionary>
                <ResourceDictionary.ThemeDictionaries>
                    <ResourceDictionary x:Key="Light">
                        <SolidColorBrush x:Key="CheckBoxForegroundUnchecked"
                            Color="Purple"/>
                        <SolidColorBrush x:Key="CheckBoxForegroundChecked"
                            Color="Purple"/>
                        <SolidColorBrush x:Key="CheckBoxCheckGlyphForegroundChecked"
                            Color="White"/>
                        <SolidColorBrush x:Key="CheckBoxCheckBackgroundStrokeChecked"  
                            Color="Purple"/>
                        <SolidColorBrush x:Key="CheckBoxCheckBackgroundFillChecked"
                            Color="Purple"/>
                    </ResourceDictionary>
                </ResourceDictionary.ThemeDictionaries>
            </ResourceDictionary>
        </CheckBox.Resources>
    </CheckBox>
<CheckBox Content="Normal CheckBox" Margin="5"/>
```

<span data-ttu-id="66e01-167">これは、そのコントロールが存在していたページ上の 1 つの「特別なチェック ボックス」にのみ影響します。</span><span class="sxs-lookup"><span data-stu-id="66e01-167">This would only effect that one “Special CheckBox” on the page where that control existed.</span></span>

## <a name="modify-the-default-system-styles"></a><span data-ttu-id="66e01-168">既定のシステム スタイルの変更</span><span class="sxs-lookup"><span data-stu-id="66e01-168">Modify the default system styles</span></span>

<span data-ttu-id="66e01-169">可能であれば、Windows ランタイムの既定の XAML リソースからのスタイルを使う必要があります。</span><span class="sxs-lookup"><span data-stu-id="66e01-169">You should use the styles that come from the Windows Runtime default XAML resources when you can.</span></span> <span data-ttu-id="66e01-170">独自のスタイルを定義する必要がある場合は、できるだけこれらの既定のスタイルから継承したスタイルを作成します (このクイック スタートで既に説明したように継承スタイルを使います。元の既定のスタイルのコピーを編集することから始めます)。</span><span class="sxs-lookup"><span data-stu-id="66e01-170">When you have to define your own styles, try to base your styles on the default ones when possible (using based-on styles as explained earlier, or start by editing a copy of the original default style).</span></span>

## <a name="the-template-property"></a><span data-ttu-id="66e01-171">テンプレート プロパティ</span><span class="sxs-lookup"><span data-stu-id="66e01-171">The template property</span></span>

<span data-ttu-id="66e01-172">スタイル setter は、[Control](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Control) の [Template](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.template) プロパティに使うことができ、実際に、一般的な XAML スタイルとアプリの XAML リソースの主要な部分を構成しています。</span><span class="sxs-lookup"><span data-stu-id="66e01-172">A style setter can be used for the [Template](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.template) property of a [Control](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Control), and in fact this makes up the majority of a typical XAML style and an app's XAML resources.</span></span> <span data-ttu-id="66e01-173">詳しくは、「[コントロール テンプレート](control-templates.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="66e01-173">This is discussed in more detail in the topic [Control templates](control-templates.md).</span></span>
