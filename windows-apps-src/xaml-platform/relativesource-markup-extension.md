---
description: ランタイム オブジェクト グラフの相対関係に関するバインドのソースを指定する手段を提供します。
title: RelativeSource マークアップ拡張
ms.assetid: B87DEF36-BE1F-4C16-B32E-7A896BD09272
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 716ca61fc9925846377157d215ca3326191915b7
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371145"
---
# <a name="relativesource-markup-extension"></a><span data-ttu-id="28ee5-104">{RelativeSource} マークアップ拡張</span><span class="sxs-lookup"><span data-stu-id="28ee5-104">{RelativeSource} markup extension</span></span>


<span data-ttu-id="28ee5-105">ランタイム オブジェクト グラフの相対関係に関するバインドのソースを指定する手段を提供します。</span><span class="sxs-lookup"><span data-stu-id="28ee5-105">Provides a means to specify the source of a binding in terms of a relative relationship in the run-time object graph.</span></span>

## <a name="xaml-attribute-usage-self-mode"></a><span data-ttu-id="28ee5-106">XAML 属性の使用方法 (Self モード)</span><span class="sxs-lookup"><span data-stu-id="28ee5-106">XAML attribute usage (Self mode)</span></span>

``` syntax
<Binding RelativeSource="{RelativeSource Self}" .../>
-or-
<object property="{Binding RelativeSource={RelativeSource Self} ...}" .../>
```

## <a name="xaml-attribute-usage-templatedparent-mode"></a><span data-ttu-id="28ee5-107">XAML 属性の使用方法 (TemplatedParent モード)</span><span class="sxs-lookup"><span data-stu-id="28ee5-107">XAML attribute usage (TemplatedParent mode)</span></span>

``` syntax
<Binding RelativeSource="{RelativeSource TemplatedParent}" .../>
-or-
<object property="{Binding RelativeSource={RelativeSource TemplatedParent} ...}" .../>
```

## <a name="xaml-values"></a><span data-ttu-id="28ee5-108">XAML 値</span><span class="sxs-lookup"><span data-stu-id="28ee5-108">XAML values</span></span>

| <span data-ttu-id="28ee5-109">用語</span><span class="sxs-lookup"><span data-stu-id="28ee5-109">Term</span></span> | <span data-ttu-id="28ee5-110">説明</span><span class="sxs-lookup"><span data-stu-id="28ee5-110">Description</span></span> |
|------|-------------|
| <span data-ttu-id="28ee5-111">{RelativeSource Self}</span><span class="sxs-lookup"><span data-stu-id="28ee5-111">{RelativeSource Self}</span></span> | <span data-ttu-id="28ee5-112"><strong>Self</strong> の [<strong>Mode</strong>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.relativesource.mode) 値を生成します。</span><span class="sxs-lookup"><span data-stu-id="28ee5-112">Produces a [<strong>Mode</strong>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.relativesource.mode) value of <strong>Self</strong>.</span></span> <span data-ttu-id="28ee5-113">ターゲット要素をこのバインドのソースとして使う必要があります。</span><span class="sxs-lookup"><span data-stu-id="28ee5-113">The target element should be used as the source for this binding.</span></span> <span data-ttu-id="28ee5-114">要素の 1 つのプロパティを同じ要素の別のプロパティにバインドする場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="28ee5-114">This is useful for binding one property of an element to another property on the same element.</span></span> |
| <span data-ttu-id="28ee5-115">{RelativeSource TemplatedParent}</span><span class="sxs-lookup"><span data-stu-id="28ee5-115">{RelativeSource TemplatedParent}</span></span> | <span data-ttu-id="28ee5-116">このバインドのソースとして適用される [<strong>ControlTemplate</strong>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) を生成します。</span><span class="sxs-lookup"><span data-stu-id="28ee5-116">Produces a [<strong>ControlTemplate</strong>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) that is applied as the source for this binding.</span></span> <span data-ttu-id="28ee5-117">ランタイム情報をテンプレート レベルでバインドに適用する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="28ee5-117">This is useful for applying runtime information to bindings at the template level.</span></span> | 

## <a name="remarks"></a><span data-ttu-id="28ee5-118">注釈</span><span class="sxs-lookup"><span data-stu-id="28ee5-118">Remarks</span></span>

<span data-ttu-id="28ee5-119">[  **Binding**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.Binding) では、**Binding** オブジェクト要素の属性または [{Binding} マークアップ拡張](binding-markup-extension.md)内のコンポーネントとして [**Binding.RelativeSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.relativesource) を設定できます。</span><span class="sxs-lookup"><span data-stu-id="28ee5-119">A [**Binding**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.Binding) can set [**Binding.RelativeSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.relativesource) either as an attribute on a **Binding** object element or as a component within a [{Binding} markup extension](binding-markup-extension.md).</span></span> <span data-ttu-id="28ee5-120">これが、2 つの異なる XAML 構文が示されている理由です。</span><span class="sxs-lookup"><span data-stu-id="28ee5-120">This is why two different XAML syntaxes are shown.</span></span>

<span data-ttu-id="28ee5-121">**RelativeSource** は [{Binding} マークアップ拡張](binding-markup-extension.md)に似ています。</span><span class="sxs-lookup"><span data-stu-id="28ee5-121">**RelativeSource** is similar to [{Binding} markup extension](binding-markup-extension.md).</span></span>  <span data-ttu-id="28ee5-122">具体的には、自分自身のインスタンスを返すことができ、基本的に引数をコンストラクターに渡す文字列ベースの構築をサポートできるマークアップ拡張機能であるという点です。</span><span class="sxs-lookup"><span data-stu-id="28ee5-122">It is a markup extension that is capable of returning instances of itself, and supporting a string-based construction that essentially passes an argument to the constructor.</span></span> <span data-ttu-id="28ee5-123">この場合、渡される引数は [**Mode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.relativesource.mode) 値になります。</span><span class="sxs-lookup"><span data-stu-id="28ee5-123">In this case, the argument being passed is the [**Mode**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.relativesource.mode) value.</span></span>

<span data-ttu-id="28ee5-124">**Self** モードは、要素の 1 つのプロパティを同じ要素の別のプロパティにバインドする場合に便利です。これは、要素の名前の指定の後に自己参照を必要としない、[**ElementName**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.elementname) バインドの 1 つのバリエーションです。</span><span class="sxs-lookup"><span data-stu-id="28ee5-124">The **Self** mode is useful for binding one property of an element to another property on the same element, and is a variation on [**ElementName**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.elementname) binding but does not require naming and then self-referencing the element.</span></span> <span data-ttu-id="28ee5-125">要素の 1 つのプロパティを同じ要素の別のプロパティにバインドする場合、プロパティで同じプロパティの型を使うか、またはバインドに対して [**Converter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.converter) を使って値を変換する必要があります。</span><span class="sxs-lookup"><span data-stu-id="28ee5-125">If you bind one property of an element to another property on the same element, either the properties must use the same property type, or you must also use a [**Converter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.converter) on the binding to convert the values.</span></span> <span data-ttu-id="28ee5-126">たとえば、[**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) は変換せずに [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) のソースとして使用できますが、[**Visibility**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.isenabled) のソースとして [**IsEnabled**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Visibility) を使う場合には、コンバーターが必要です。</span><span class="sxs-lookup"><span data-stu-id="28ee5-126">For example, you could use [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) as a source for [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) without conversion, but you'd need a converter to use [**IsEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.isenabled) as a source for [**Visibility**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Visibility).</span></span>

<span data-ttu-id="28ee5-127">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="28ee5-127">Here's an example.</span></span> <span data-ttu-id="28ee5-128">この [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) は [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) と [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) が常に等しく、正方形として表示されるように [{Binding} マークアップ拡張](binding-markup-extension.md) を使います。</span><span class="sxs-lookup"><span data-stu-id="28ee5-128">This [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) uses a [{Binding} markup extension](binding-markup-extension.md) so that its [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) and [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) are always equal and it renders as a square.</span></span> <span data-ttu-id="28ee5-129">Height のみが固定値として設定されます。</span><span class="sxs-lookup"><span data-stu-id="28ee5-129">Only the Height is set as a fixed value.</span></span> <span data-ttu-id="28ee5-130">この **Rectangle** の既定の[**DataContext**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.datacontext) は**これ**ではなく **null** です。</span><span class="sxs-lookup"><span data-stu-id="28ee5-130">For this **Rectangle** its default [**DataContext**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.datacontext) is **null**, not **this**.</span></span> <span data-ttu-id="28ee5-131">そこで、データ コンテキストのソースをオブジェクト自体にするために (そして他のプロパティにバインドできるようにするために)、{Binding} マークアップ拡張の使用時に `RelativeSource={RelativeSource Self}` 引数を使います。</span><span class="sxs-lookup"><span data-stu-id="28ee5-131">So to establish the data context source to be the object itself (and enable binding to its other properties) we use the `RelativeSource={RelativeSource Self}` argument in the {Binding} markup extension usage.</span></span>

```XML
<Rectangle
  Fill="Orange" Width="200"
  Height="{Binding RelativeSource={RelativeSource Self}, Path=Width}"
/>
```

<span data-ttu-id="28ee5-132">オブジェクトの [**DataContext**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.datacontext) を自分自身に設定する方法として `RelativeSource={RelativeSource Self}` を使うこともできます。</span><span class="sxs-lookup"><span data-stu-id="28ee5-132">Another use of `RelativeSource={RelativeSource Self}` is as a way to set an object's [**DataContext**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.datacontext) to itself.</span></span>  <span data-ttu-id="28ee5-133">たとえば、いくつかの SDK の例では、この手法が生じる場所、 [**ページ**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page)クラスは、独自のデータ バインディングのすぐにビュー モデルを既に提供しているカスタム プロパティを使用して拡張されています例を示します。 `<common:LayoutAwarePage ... DataContext="{Binding DefaultViewModel, RelativeSource={RelativeSource Self}}">`</span><span class="sxs-lookup"><span data-stu-id="28ee5-133">For example, you may see this technique in some of the SDK examples where the [**Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) class has been extended with a custom property that's already providing a ready-to-go view model for its own data binding such as: `<common:LayoutAwarePage ... DataContext="{Binding DefaultViewModel, RelativeSource={RelativeSource Self}}">`</span></span>

<span data-ttu-id="28ee5-134">**注**  、XAML の使用状況の**RelativeSource**の対象となる使用量のみを示しています: の値を設定[ **Binding.RelativeSource** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.relativesource)バインディング式の一部としての XAML でします。</span><span class="sxs-lookup"><span data-stu-id="28ee5-134">**Note**  The XAML usage for **RelativeSource** shows only the usage for which it is intended: setting a value for [**Binding.RelativeSource**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.binding.relativesource) in XAML as part of a binding expression.</span></span> <span data-ttu-id="28ee5-135">ただし、値が [**RelativeSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.RelativeSource) のプロパティを設定する場合は、理論的にそれ以外の使用法も可能です。</span><span class="sxs-lookup"><span data-stu-id="28ee5-135">Theoretically, other usages are possible if setting a property where the value is [**RelativeSource**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.RelativeSource).</span></span>

## <a name="related-topics"></a><span data-ttu-id="28ee5-136">関連トピック</span><span class="sxs-lookup"><span data-stu-id="28ee5-136">Related topics</span></span>

* [<span data-ttu-id="28ee5-137">XAML の概要</span><span class="sxs-lookup"><span data-stu-id="28ee5-137">XAML overview</span></span>](xaml-overview.md)
* [<span data-ttu-id="28ee5-138">データ バインディングの詳細</span><span class="sxs-lookup"><span data-stu-id="28ee5-138">Data binding in depth</span></span>](https://docs.microsoft.com/windows/uwp/data-binding/data-binding-in-depth)
* [<span data-ttu-id="28ee5-139">{0} バインド} マークアップ拡張機能</span><span class="sxs-lookup"><span data-stu-id="28ee5-139">{Binding} markup extension</span></span>](binding-markup-extension.md)
* [<span data-ttu-id="28ee5-140">**バインド**</span><span class="sxs-lookup"><span data-stu-id="28ee5-140">**Binding**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.Binding)
* [<span data-ttu-id="28ee5-141">**RelativeSource**</span><span class="sxs-lookup"><span data-stu-id="28ee5-141">**RelativeSource**</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.RelativeSource)

