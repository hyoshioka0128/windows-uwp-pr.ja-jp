---
description: リソースとして作成されて参照される、ResourceDictionary 内に存在する要素を一意に識別します。
title: xKey 属性
ms.assetid: 141FC5AF-80EE-4401-8A1B-17CB22C2277A
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: cb42fcb17cfcad76989732b1a1482d9fbc85be5e
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372326"
---
# <a name="xkey-attribute"></a><span data-ttu-id="4624b-104">x:Key 属性</span><span class="sxs-lookup"><span data-stu-id="4624b-104">x:Key attribute</span></span>


<span data-ttu-id="4624b-105">リソースとして作成されて参照される、[**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) 内に存在する要素を一意に識別します。</span><span class="sxs-lookup"><span data-stu-id="4624b-105">Uniquely identifies elements that are created and referenced as resources, and which exist within a [**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary).</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="4624b-106">XAML 属性の使用方法</span><span class="sxs-lookup"><span data-stu-id="4624b-106">XAML attribute usage</span></span>

``` syntax
<ResourceDictionary>
  <object x:Key="stringKeyValue".../>
</ResourceDictionary>
```

## <a name="xaml-attribute-usage-implicit-resourcedictionary"></a><span data-ttu-id="4624b-107">XAML 属性の使用方法 (暗黙的な **ResourceDictionary**)</span><span class="sxs-lookup"><span data-stu-id="4624b-107">XAML attribute usage (implicit **ResourceDictionary**)</span></span>

``` syntax
<object.Resources>
  <object x:Key="stringKeyValue".../>
</object.Resources>
```

## <a name="xaml-values"></a><span data-ttu-id="4624b-108">XAML 値</span><span class="sxs-lookup"><span data-stu-id="4624b-108">XAML values</span></span>

| <span data-ttu-id="4624b-109">用語</span><span class="sxs-lookup"><span data-stu-id="4624b-109">Term</span></span> | <span data-ttu-id="4624b-110">説明</span><span class="sxs-lookup"><span data-stu-id="4624b-110">Description</span></span> |
|------|-------------|
| <span data-ttu-id="4624b-111">オブジェクト</span><span class="sxs-lookup"><span data-stu-id="4624b-111">object</span></span> | <span data-ttu-id="4624b-112">共有可能な任意のオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="4624b-112">Any object that is shareable.</span></span> <span data-ttu-id="4624b-113">「[ResourceDictionary と XAML リソースの参照](https://docs.microsoft.com/windows/uwp/controls-and-patterns/resourcedictionary-and-xaml-resource-references)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4624b-113">See [ResourceDictionary and XAML resource references](https://docs.microsoft.com/windows/uwp/controls-and-patterns/resourcedictionary-and-xaml-resource-references).</span></span> |
| <span data-ttu-id="4624b-114">stringKeyValue</span><span class="sxs-lookup"><span data-stu-id="4624b-114">stringKeyValue</span></span> | <span data-ttu-id="4624b-115">_XamlName_> の文法に準拠する必要がある、キーとして使われる実際の文字列。</span><span class="sxs-lookup"><span data-stu-id="4624b-115">A true string used as a key, which must conform to the _XamlName_> grammar.</span></span> <span data-ttu-id="4624b-116">以下の「XamlName の文法」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4624b-116">See "XamlName grammar" below.</span></span> | 

##  <a name="xamlname-grammar"></a><span data-ttu-id="4624b-117">XamlName の文法</span><span class="sxs-lookup"><span data-stu-id="4624b-117">XamlName grammar</span></span>

<span data-ttu-id="4624b-118">ユニバーサル Windows プラットフォーム (UWP) の XAML 実装でキーとして使われる文字列の規範となる文法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4624b-118">The following is the normative grammar for a string that is used as a key in the Universal Windows Platform (UWP) XAML implementation:</span></span>

``` syntax
XamlName ::= NameStartChar (NameChar)*
NameStartChar ::= LetterCharacter | '_'
NameChar ::= NameStartChar | DecimalDigit
LetterCharacter ::= ('a'-'z') | ('A'-'Z')
DecimalDigit ::= '0'-'9'
CombiningCharacter::= none
```

-   <span data-ttu-id="4624b-119">文字が ASCII の下の範囲はローマ字の大文字と小文字の英字、数字、およびアンダー スコアを具体的には制限されている (\_) 文字。</span><span class="sxs-lookup"><span data-stu-id="4624b-119">Characters are restricted to the lower ASCII range, and more specifically to Roman alphabet uppercase and lowercase letters, digits, and the underscore (\_) character.</span></span>
-   <span data-ttu-id="4624b-120">Unicode 文字範囲はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="4624b-120">The Unicode character range is not supported.</span></span>
-   <span data-ttu-id="4624b-121">名前の先頭を数字にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4624b-121">A name cannot begin with a digit.</span></span>

## <a name="remarks"></a><span data-ttu-id="4624b-122">注釈</span><span class="sxs-lookup"><span data-stu-id="4624b-122">Remarks</span></span>

<span data-ttu-id="4624b-123">通常、[**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) の子要素は、そのディクショナリ内の一意のキー値を指定する **x:Key** 属性を含みます。</span><span class="sxs-lookup"><span data-stu-id="4624b-123">Child elements of a [**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) generally include an **x:Key** attribute that specifies a unique key value within that dictionary.</span></span> <span data-ttu-id="4624b-124">キーは、読み込み時に XAML プロセッサによって一意であることが要求されます。</span><span class="sxs-lookup"><span data-stu-id="4624b-124">Key uniqueness is enforced at load time by the XAML processor.</span></span> <span data-ttu-id="4624b-125">**x:Key** 値が一意でない場合は、XAML の解析で例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="4624b-125">Non-unique **x:Key** values will result in XAML parse exceptions.</span></span> <span data-ttu-id="4624b-126">[{StaticResource} マークアップ拡張](staticresource-markup-extension.md)によって要求された場合、解決されていないキーも XAML の解析での例外の原因になります。</span><span class="sxs-lookup"><span data-stu-id="4624b-126">If requested by [{StaticResource} markup extension](staticresource-markup-extension.md), a non-resolved key will also result in XAML parse exceptions.</span></span>

<span data-ttu-id="4624b-127">**x:Key** と [x:Name](x-name-attribute.md) は同じ概念ではありません。</span><span class="sxs-lookup"><span data-stu-id="4624b-127">**x:Key** and [x:Name](x-name-attribute.md) are not identical concepts.</span></span> <span data-ttu-id="4624b-128">**x:Key** はリソース ディクショナリだけで使われます。</span><span class="sxs-lookup"><span data-stu-id="4624b-128">**x:Key** is used exclusively in resource dictionaries.</span></span> <span data-ttu-id="4624b-129">x:Name は、すべての XAML 領域で使われます。</span><span class="sxs-lookup"><span data-stu-id="4624b-129">x:Name is used for all areas of XAML.</span></span> <span data-ttu-id="4624b-130">キー値を使って [**FindName**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.findname) を呼び出した場合、キーを持つリソースは取得されません。</span><span class="sxs-lookup"><span data-stu-id="4624b-130">A [**FindName**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.findname) call using a key value will not retrieve a keyed resource.</span></span> <span data-ttu-id="4624b-131">リソース ディクショナリで定義されているオブジェクトは、**x:Key** と **x:Name** のどちらか一方または両方を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="4624b-131">Objects defined in a resource dictionary may have an **x:Key**, an **x:Name** or both.</span></span> <span data-ttu-id="4624b-132">キーと名前が一致する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4624b-132">The key and name are not required to match.</span></span>

<span data-ttu-id="4624b-133">ここに示す暗黙的な構文において、[**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) オブジェクトは XAML プロセッサが [**Resources**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.resources) コレクションを取得するための新しいオブジェクトを生成する方法を暗黙的に決定することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4624b-133">Note that in the implicit syntax shown, the [**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) object is implicit in how the XAML processor produces a new object to populate a [**Resources**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.resources) collection.</span></span>

<span data-ttu-id="4624b-134">**x:Key** の指定に相当するコードは、基になる [**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) でキーを使う任意の操作です。</span><span class="sxs-lookup"><span data-stu-id="4624b-134">The code equivalent of specifying **x:Key** is any operation that uses a key with the underlying [**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary).</span></span> <span data-ttu-id="4624b-135">たとえば、あるリソースのマークアップで適用される **x:Key** は、リソースを **ResourceDictionary** に追加するときの **Insert** の *key* パラメーターの値と同じです。</span><span class="sxs-lookup"><span data-stu-id="4624b-135">For example, an **x:Key** applied in markup for a resource is equivalent to the value of the *key* parameter of **Insert** when you add the resource to a **ResourceDictionary**.</span></span>

<span data-ttu-id="4624b-136">リソース ディクショナリ内の項目は、ターゲットとなる [**Style**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) または [**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) である場合、**x:Key** の値を省略できます。どちらの場合も、リソース項目の暗黙的なキーは、文字列として解釈される **TargetType** 値です。</span><span class="sxs-lookup"><span data-stu-id="4624b-136">An item in a resource dictionary can omit a value for **x:Key** if it is a targeted [**Style**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) or [**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate); in each of these cases the implicit key of the resource item is the **TargetType** value interpreted as a string.</span></span> <span data-ttu-id="4624b-137">詳しくは、「[クイック スタート: コントロールのスタイル (JavaScript と HTML を使った Windows ストア アプリ)](https://docs.microsoft.com/previous-versions/windows/apps/hh465498(v=win.10))」と「[ResourceDictionary と XAML リソースの参照](https://docs.microsoft.com/windows/uwp/controls-and-patterns/resourcedictionary-and-xaml-resource-references)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4624b-137">For more info, see [Quickstart: styling controls](https://docs.microsoft.com/previous-versions/windows/apps/hh465498(v=win.10)) and [ResourceDictionary and XAML resource references](https://docs.microsoft.com/windows/uwp/controls-and-patterns/resourcedictionary-and-xaml-resource-references).</span></span>

