---
Description: ユーザーがタッチ キーボード、つまりソフト入力パネル (SIP) でデータを入力できるように、ユーザーが入力すると予想されるデータの種類に合わせてテキスト コントロールの入力値の種類を設定できます。
MS-HAID: dev\_ctrl\_layout\_txt.use\_input\_scope\_to\_change\_the\_touch\_keyboard
MSHAttr: PreferredLib:/library/windows/apps
Search.Product: eADQiWindows 10XVcnh
title: 入力値の種類を使ったタッチ キーボードの変更
ms.assetid: 6E5F55D7-24D6-47CC-B457-B6231EDE2A71
template: detail.hbs
keywords: キーボード, アクセシビリティ, ナビゲーション, フォーカス, テキスト, 入力, ユーザーの操作
ms.date: 02/08/2017
ms.topic: article
ms.openlocfilehash: c522e21c45a3edd08a14b081cc227a83f19a3ea0
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365363"
---
# <a name="use-input-scope-to-change-the-touch-keyboard"></a><span data-ttu-id="06dd1-104">入力値の種類を使ったタッチ キーボードの変更</span><span class="sxs-lookup"><span data-stu-id="06dd1-104">Use input scope to change the touch keyboard</span></span>

<span data-ttu-id="06dd1-105">ユーザーがタッチ キーボード、つまりソフト入力パネル (SIP) でデータを入力できるように、ユーザーが入力すると予想されるデータの種類に合わせてテキスト コントロールの入力値の種類を設定できます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-105">To help users to enter data using the touch keyboard, or Soft Input Panel (SIP), you can set the input scope of the text control to match the kind of data the user is expected to enter.</span></span>

### <a name="important-apis"></a><span data-ttu-id="06dd1-106">重要な API</span><span class="sxs-lookup"><span data-stu-id="06dd1-106">Important APIs</span></span>
- [<span data-ttu-id="06dd1-107">InputScope</span><span class="sxs-lookup"><span data-stu-id="06dd1-107">InputScope</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope)
- [<span data-ttu-id="06dd1-108">inputScopeNameValue</span><span class="sxs-lookup"><span data-stu-id="06dd1-108">InputScopeNameValue</span></span>](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeNameValue)


<span data-ttu-id="06dd1-109">タッチ キーボードは、アプリがタッチ スクリーン付きのデバイスで実行されているときにテキスト入力に使うことができます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-109">The touch keyboard can be used for text entry when your app runs on a device with a touch screen.</span></span> <span data-ttu-id="06dd1-110">タッチ キーボードは、 **[TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox)** または **[RichEditBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox)** などの編集可能な入力フィールドをユーザーがタップしたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-110">The touch keyboard is invoked when the user taps on an editable input field, such as a **[TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox)** or **[RichEditBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox)**.</span></span> <span data-ttu-id="06dd1-111">ユーザーが入力すると予想されるデータの種類と一致するようにテキスト コントロールの*入力値の種類*を設定することで、ユーザーはより速く簡単にアプリでデータを入力できるようになります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-111">You can make it much faster and easier for users to enter data in your app by setting the *input scope* of the text control to match the kind of data you expect the user to enter.</span></span> <span data-ttu-id="06dd1-112">入力値の種類は、システムに対してコントロールが予期しているテキスト入力の種類のヒントとなるため、システムはその入力の種類用の特殊なタッチ キーボード レイアウトを提供できます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-112">The input scope provides a hint to the system about the type of text input expected by the control so the system can provide a specialized touch keyboard layout for the input type.</span></span>

<span data-ttu-id="06dd1-113">たとえば、テキスト ボックスが 4 桁の PIN の入力専用である場合は、[**InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) プロパティを **Number** に設定します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-113">For example, if a text box is used only to enter a 4-digit PIN, set the [**InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) property to **Number**.</span></span> <span data-ttu-id="06dd1-114">これにより、システムに数字キーパッド レイアウトの表示が指示されるため、ユーザーは簡単に PIN を入力できます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-114">This tells the system to show the number keypad layout, which makes it easier for the user to enter the PIN.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="06dd1-115">この情報は、SIP にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-115">This info applies only to the SIP.</span></span> <span data-ttu-id="06dd1-116">ハードウェア キーボードにも、Windows の簡単操作オプションで使用できるスクリーン キーボードにも適用されません。</span><span class="sxs-lookup"><span data-stu-id="06dd1-116">It does not apply to hardware keyboards or the On-Screen Keyboard available in the Windows Ease of Access options.</span></span>
> - <span data-ttu-id="06dd1-117">入力スコープの設定によって、入力の検証が実行されるわけではありません。また、ユーザーが、ハードウェア キーボードやその他の入力デバイスから入力できなくなることもありません。</span><span class="sxs-lookup"><span data-stu-id="06dd1-117">The input scope does not cause any input validation to be performed, and does not prevent the user from providing any input through a hardware keyboard or other input device.</span></span> <span data-ttu-id="06dd1-118">必要に応じて、コードで入力を検証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-118">You are still responsible for validating the input in your code as needed.</span></span>

## <a name="changing-the-input-scope-of-a-text-control"></a><span data-ttu-id="06dd1-119">テキスト コントロールの入力値の種類を変更する</span><span class="sxs-lookup"><span data-stu-id="06dd1-119">Changing the input scope of a text control</span></span>

<span data-ttu-id="06dd1-120">アプリで使用可能な入力値の種類は、 **[InputScopeNameValue](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeNameValue)** 列挙体のメンバーです。</span><span class="sxs-lookup"><span data-stu-id="06dd1-120">The input scopes that are available to your app are members of the **[InputScopeNameValue](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeNameValue)** enumeration.</span></span> <span data-ttu-id="06dd1-121"> **[TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox)** または **[RichEditBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox)** の *\*InputScope** プロパティを、これらの値のいずれかに設定できます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-121">You can set the **InputScope** property of a **[TextBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox)** or **[RichEditBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox)** to one of these values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06dd1-122">**[InputScope](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.passwordbox.inputscope)** プロパティ **[PasswordBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.PasswordBox)** のみをサポート、 **パスワード** と **NumericPin** 値。</span><span class="sxs-lookup"><span data-stu-id="06dd1-122">The **[InputScope](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.passwordbox.inputscope)** property on **[PasswordBox](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.PasswordBox)** supports only the **Password** and **NumericPin** values.</span></span> <span data-ttu-id="06dd1-123">それ以外の値はすべて無視されます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-123">Any other value is ignored.</span></span>

<span data-ttu-id="06dd1-124">ここでは、各テキスト ボックスで予期されるデータと一致するように、いくつかのテキスト ボックスの入力値の種類を変更します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-124">Here, you change the input scope of several text boxes to match the expected data for each text box.</span></span>

<span data-ttu-id="06dd1-125">**入力 XAML にスコープを変更するには**</span><span class="sxs-lookup"><span data-stu-id="06dd1-125">**To change the input scope in XAML**</span></span>

1.  <span data-ttu-id="06dd1-126">ページの XAML ファイルで、変更するテキスト コントロールのタグを見つけます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-126">In the XAML file for your page, locate the tag for the text control that you want to change.</span></span>
2.  <span data-ttu-id="06dd1-127">[  **InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) 属性をタグに追加し、予期される入力に一致する [**InputScopeNameValue**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeNameValue) 値を指定します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-127">Add the [**InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) attribute to the tag and specify the [**InputScopeNameValue**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeNameValue) value that matches the expected input.</span></span>

    <span data-ttu-id="06dd1-128">次に示すのは、一般的な顧客の連絡先フォームに表示されるテキスト ボックスです。</span><span class="sxs-lookup"><span data-stu-id="06dd1-128">Here are some text boxes that might appear on a common customer-contact form.</span></span> <span data-ttu-id="06dd1-129">[  **InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) を設定すると、各テキスト ボックスに、データに適切なレイアウトのタッチ キーボードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-129">With the [**InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) set, a touch keyboard with a suitable layout for the data shows for each text box.</span></span>

    ```xaml
    <StackPanel Width="300">
        <TextBox Header="Name" InputScope="Default"/>
        <TextBox Header="Email Address" InputScope="EmailSmtpAddress"/>
        <TextBox Header="Telephone Number" InputScope="TelephoneNumber"/>
        <TextBox Header="Web site" InputScope="Url"/>
    </StackPanel>
    ```

<span data-ttu-id="06dd1-130">**コードの入力スコープを変更するには**</span><span class="sxs-lookup"><span data-stu-id="06dd1-130">**To change the input scope in code**</span></span>

1.  <span data-ttu-id="06dd1-131">ページの XAML ファイルで、変更するテキスト コントロールのタグを見つけます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-131">In the XAML file for your page, locate the tag for the text control that you want to change.</span></span> <span data-ttu-id="06dd1-132">設定されていない場合は、[x: Name 属性](https://docs.microsoft.com/windows/uwp/xaml-platform/x-name-attribute) を設定します。これで、コード内でコントロールを参照できます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-132">If it's not set, set the [x:Name attribute](https://docs.microsoft.com/windows/uwp/xaml-platform/x-name-attribute) so you can reference the control in your code.</span></span>

    ```csharp
    <TextBox Header="Telephone Number" x:Name="phoneNumberTextBox"/>
    ```

2.  <span data-ttu-id="06dd1-133">新しい [**InputScope**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScope) オブジェクトをインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-133">Instantiate a new [**InputScope**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScope) object.</span></span>

    ```csharp
    InputScope scope = new InputScope();
    ```

3.  <span data-ttu-id="06dd1-134">新しい [**InputScopeName**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeName) オブジェクトをインスタンス化します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-134">Instantiate a new [**InputScopeName**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeName) object.</span></span>
    
    ```csharp
    InputScopeName scopeName = new InputScopeName();
    ```

4.  <span data-ttu-id="06dd1-135">[  **InputScopeName**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeName) オブジェクトの [**NameValue**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.input.inputscopename.namevalue) プロパティを [**InputScopeNameValue**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeNameValue) 列挙体の値に設定します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-135">Set the [**NameValue**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.input.inputscopename.namevalue) property of the [**InputScopeName**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeName) object to a value of the [**InputScopeNameValue**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeNameValue) enumeration.</span></span>

    ```csharp
    scopeName.NameValue = InputScopeNameValue.TelephoneNumber;
    ```

5.  <span data-ttu-id="06dd1-136">[  **InputScope**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScope) オブジェクトの [**Names**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.input.inputscope.names) コレクションに [**InputScopeName**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeName) オブジェクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-136">Add the [**InputScopeName**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScopeName) object to the [**Names**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.input.inputscope.names) collection of the [**InputScope**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScope) object.</span></span>

    ```csharp
    scope.Names.Add(scopeName);
    ```

6.  <span data-ttu-id="06dd1-137">[  **InputScope**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScope) オブジェクトを、テキスト コントロールの [**InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) プロパティの値として設定します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-137">Set the [**InputScope**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.InputScope) object as the value of the text control's [**InputScope**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.inputscope) property.</span></span>

    ```csharp
    phoneNumberTextBox.InputScope = scope;
    ```

<span data-ttu-id="06dd1-138">コード全体を次に示します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-138">Here's the code all together.</span></span>

```CSharp
InputScope scope = new InputScope();
InputScopeName scopeName = new InputScopeName();
scopeName.NameValue = InputScopeNameValue.TelephoneNumber;
scope.Names.Add(scopeName);
phoneNumberTextBox.InputScope = scope;
```

<span data-ttu-id="06dd1-139">同じ手順を、次の短縮形のコードにまとめることもできます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-139">The same steps can be condensed into this shorthand code.</span></span>

```CSharp
phoneNumberTextBox.InputScope = new InputScope() 
{
    Names = {new InputScopeName(InputScopeNameValue.TelephoneNumber)}
};
```

## <a name="text-prediction-spell-checking-and-auto-correction"></a><span data-ttu-id="06dd1-140">予測入力、スペル チェック、および自動修正</span><span class="sxs-lookup"><span data-stu-id="06dd1-140">Text prediction, spell checking, and auto-correction</span></span>

<span data-ttu-id="06dd1-141">[  **TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) コントロールと [**RichEditBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox) コントロールには、SIP の動作に影響を与えるプロパティがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-141">The [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) and [**RichEditBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.RichEditBox) controls have several properties that influence the behavior of the SIP.</span></span> <span data-ttu-id="06dd1-142">ユーザーに最適なエクスペリエンスを提供するには、これらのプロパティが、タッチ操作を使用したテキスト入力に与える影響を理解しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-142">To provide the best experience for your users, it's important to understand how these properties affect text input using touch.</span></span>

-   <span data-ttu-id="06dd1-143">[**IsSpellCheckEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.isspellcheckenabled): コントロールが、認識されない語をマークする、システムのスペル チェック エンジンと対話とき、テキスト コントロールでスペル チェックを有効にします。</span><span class="sxs-lookup"><span data-stu-id="06dd1-143">[**IsSpellCheckEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.isspellcheckenabled)—When spell check is enabled for a text control, the control interacts with the system's spell-check engine to mark words that are not recognized.</span></span> <span data-ttu-id="06dd1-144">単語をタップすると、修正候補の一覧を表示できます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-144">You can tap a word to see a list of suggested corrections.</span></span> <span data-ttu-id="06dd1-145">スペル チェック オプションは既定で有効になっています。</span><span class="sxs-lookup"><span data-stu-id="06dd1-145">Spell checking is enabled by default.</span></span>

    <span data-ttu-id="06dd1-146">入力値の種類が **Default** である場合、このプロパティを使用すると、文字列を入力するときに、文の最初の単語に対する大文字の自動設定および単語の自動修正が有効になります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-146">For the **Default** input scope, this property also enables automatic capitalization of the first word in a sentence and auto-correction of words as you type.</span></span> <span data-ttu-id="06dd1-147">これらの自動修正機能は、他の入力値の種類では無効である場合があります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-147">These auto-correction features might be disabled in other input scopes.</span></span> <span data-ttu-id="06dd1-148">詳しくは、このトピックの後半にある表をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="06dd1-148">For more info, see the tables later in this topic.</span></span>

-   <span data-ttu-id="06dd1-149">[**IsTextPredictionEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.istextpredictionenabled)-システムが単語入力を開始する可能性があることの一覧を表示するテキスト コントロールのテキストの予測を有効にします。</span><span class="sxs-lookup"><span data-stu-id="06dd1-149">[**IsTextPredictionEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.istextpredictionenabled)—When text prediction is enabled for a text control, the system shows a list of words that you might be beginning to type.</span></span> <span data-ttu-id="06dd1-150">一覧から選択できるため、単語全体を入力しなくても済みます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-150">You can select from the list so you don't have to type the whole word.</span></span> <span data-ttu-id="06dd1-151">予測入力は既定で有効になっています。</span><span class="sxs-lookup"><span data-stu-id="06dd1-151">Text prediction is enabled by default.</span></span>

    <span data-ttu-id="06dd1-152">入力値の種類が **Default** 以外のとき、[**IsTextPredictionEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.istextpredictionenabled) プロパティが **true** であっても、予測入力が無効になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-152">Text prediction might be disabled if the input scope is other than **Default**, even if the [**IsTextPredictionEnabled**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.istextpredictionenabled) property is **true**.</span></span> <span data-ttu-id="06dd1-153">詳しくは、このトピックの後半にある表をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="06dd1-153">For more info, see the tables later in this topic.</span></span>

-   <span data-ttu-id="06dd1-154">[**PreventKeyboardDisplayOnProgrammaticFocus**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.preventkeyboarddisplayonprogrammaticfocus): このプロパティが**true**が原因でシステムのテキスト コントロールにフォーカスをプログラムで設定すると、SIP を表示します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-154">[**PreventKeyboardDisplayOnProgrammaticFocus**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textbox.preventkeyboarddisplayonprogrammaticfocus)—When this property is **true**, it prevents the system from showing the SIP when focus is programmatically set on a text control.</span></span> <span data-ttu-id="06dd1-155">代わりに、ユーザーがコントロールで操作するときにだけ、キーボードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06dd1-155">Instead, the keyboard is shown only when the user interacts with the control.</span></span>

## <a name="touch-keyboard-index-for-windows"></a><span data-ttu-id="06dd1-156">Windows のタッチ キーボードのインデックス</span><span class="sxs-lookup"><span data-stu-id="06dd1-156">Touch keyboard index for Windows</span></span>

<span data-ttu-id="06dd1-157">これらのテーブルでは、一般的な入力スコープの値を Windows のソフト入力パネル (SIP) のレイアウトを表示します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-157">These tables show the Windows Soft Input Panel (SIP) layouts for common input scope values.</span></span> <span data-ttu-id="06dd1-158">**IsSpellCheckEnabled** プロパティや **IsTextPredictionEnabled** プロパティによって有効になっている機能に対する入力値の種類の影響が、入力値の種類ごとに説明されています。</span><span class="sxs-lookup"><span data-stu-id="06dd1-158">The effect of the input scope on the features enabled by the **IsSpellCheckEnabled** and **IsTextPredictionEnabled** properties is listed for each input scope.</span></span> <span data-ttu-id="06dd1-159">これは、利用できる入力値の種類をすべて示したものではありません。</span><span class="sxs-lookup"><span data-stu-id="06dd1-159">This is not a comprehensive list of available input scopes.</span></span>

> [!Tip] 
> <span data-ttu-id="06dd1-160">キーを押して、アルファベットのレイアウトと数字と記号のレイアウトの間のほとんどのタッチ キーボードを切り替えることができます、 **123 &** に数字と記号のレイアウトとキーを押して変更をキー、 **abcd**キーアルファベット順のレイアウトに変更します。</span><span class="sxs-lookup"><span data-stu-id="06dd1-160">You can toggle most touch keyboards between an alphabetic layout and a numbers-and-symbols layout by pressing the **&123** key to change to the numbers-and-symbols layout, and press the **abcd** key to change to the alphabetic layout.</span></span>

### <a name="default"></a><span data-ttu-id="06dd1-161">Default</span><span class="sxs-lookup"><span data-stu-id="06dd1-161">Default</span></span>

`<TextBox InputScope="Default"/>`

<span data-ttu-id="06dd1-162">既定の Windows はタッチ キーボードです。</span><span class="sxs-lookup"><span data-stu-id="06dd1-162">The default Windows touch keyboard.</span></span>

![既定の Windows タッチ キーボード](images/input-scopes/default.png)
- <span data-ttu-id="06dd1-164">スペル チェック: **IsSpellCheckEnabled** = **true** の場合は有効、**IsSpellCheckEnabled** = **false** の場合は無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-164">Spell check: enabled if **IsSpellCheckEnabled** = **true**, disabled if **IsSpellCheckEnabled** = **false**</span></span>
- <span data-ttu-id="06dd1-165">自動修正: **IsSpellCheckEnabled** = **true** の場合は有効、**IsSpellCheckEnabled** = **false** の場合は無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-165">Auto-correction: enabled if **IsSpellCheckEnabled** = **true**, disabled if **IsSpellCheckEnabled** = **false**</span></span>
- <span data-ttu-id="06dd1-166">大文字の自動設定: **IsSpellCheckEnabled** = **true** の場合は有効、**IsSpellCheckEnabled** = **false** の場合は無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-166">Automatic capitalization: enabled if **IsSpellCheckEnabled** = **true**, disabled if **IsSpellCheckEnabled** = **false**</span></span>
- <span data-ttu-id="06dd1-167">予測入力: **IsTextPredictionEnabled** = **true** の場合は有効、**IsTextPredictionEnabled** = **false** の場合は無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-167">Text prediction: enabled if **IsTextPredictionEnabled** = **true**, disabled if **IsTextPredictionEnabled** = **false**</span></span>

### <a name="currencyamountandsymbol"></a><span data-ttu-id="06dd1-168">CurrencyAmountAndSymbol</span><span class="sxs-lookup"><span data-stu-id="06dd1-168">CurrencyAmountAndSymbol</span></span>

`<TextBox InputScope="CurrencyAmountAndSymbol"/>`

<span data-ttu-id="06dd1-169">既定の数字と記号のキーボード レイアウト。</span><span class="sxs-lookup"><span data-stu-id="06dd1-169">The default numbers and symbols keyboard layout.</span></span>

![通貨用 Windows タッチ キーボード](images/input-scopes/currencyamountandsymbol.png)

- <span data-ttu-id="06dd1-171">複数のシンボルを表示するページの左/右キーが含まれています</span><span class="sxs-lookup"><span data-stu-id="06dd1-171">Includes page left/right keys to show more symbols</span></span>
- <span data-ttu-id="06dd1-172">スペル チェック: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-172">Spell check: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-173">自動修正: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-173">Auto-correction: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-174">大文字の自動設定: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-174">Automatic capitalization: always disabled</span></span>
- <span data-ttu-id="06dd1-175">予測入力: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-175">Text prediction: on by default, can be disabled</span></span>
 
### <a name="url"></a><span data-ttu-id="06dd1-176">Url</span><span class="sxs-lookup"><span data-stu-id="06dd1-176">Url</span></span>

`<TextBox InputScope="Url"/>`

![URL 用 Windows タッチ キーボード](images/input-scopes/url.png)

- <span data-ttu-id="06dd1-178">**.com** キーと ![Go キー](images/input-scopes/kbdgokey.png) (Go) キーがあります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-178">Includes the **.com** and ![go key](images/input-scopes/kbdgokey.png) (Go) keys.</span></span> <span data-ttu-id="06dd1-179">長押しし、 **.com**追加のオプションを表示するキー ( **.org**、 **.net**、およびリージョン固有のサフィックスを)</span><span class="sxs-lookup"><span data-stu-id="06dd1-179">Press and hold the **.com** key to display additional options (**.org**, **.net**, and region-specific suffixes)</span></span>
- <span data-ttu-id="06dd1-180">含まれています、 **:** 、 **-** 、および **/** キー</span><span class="sxs-lookup"><span data-stu-id="06dd1-180">Includes the **:**, **-**, and **/** keys</span></span>
- <span data-ttu-id="06dd1-181">スペル チェック: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-181">Spell check: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-182">自動修正: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-182">Auto-correction: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-183">大文字の自動設定: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-183">Automatic capitalization: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-184">予測入力: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-184">Text prediction: off by default, can be enabled</span></span>


### <a name="emailsmtpaddress"></a><span data-ttu-id="06dd1-185">EmailSmtpAddress</span><span class="sxs-lookup"><span data-stu-id="06dd1-185">EmailSmtpAddress</span></span>

`<TextBox InputScope="EmailSmtpAddress"/>`

![メール アドレス用の Windows タッチ キーボード](images/input-scopes/emailsmtpaddress.png)
- <span data-ttu-id="06dd1-187">**@**  キーと **.com** キーがあります。</span><span class="sxs-lookup"><span data-stu-id="06dd1-187">Includes the **@** and **.com** keys.</span></span> <span data-ttu-id="06dd1-188">長押しし、 **.com**追加のオプションを表示するキー ( **.org**、 **.net**、およびリージョン固有のサフィックスを)</span><span class="sxs-lookup"><span data-stu-id="06dd1-188">Press and hold the **.com** key to display additional options (**.org**, **.net**, and region-specific suffixes)</span></span>
- <span data-ttu-id="06dd1-189">含まれています、 **_** と **-** キー</span><span class="sxs-lookup"><span data-stu-id="06dd1-189">Includes the **_** and **-** keys</span></span>
- <span data-ttu-id="06dd1-190">スペル チェック: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-190">Spell check: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-191">自動修正: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-191">Auto-correction: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-192">大文字の自動設定: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-192">Automatic capitalization: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-193">予測入力: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-193">Text prediction: off by default, can be enabled</span></span>


### <a name="number"></a><span data-ttu-id="06dd1-194">数値</span><span class="sxs-lookup"><span data-stu-id="06dd1-194">Number</span></span>

`<TextBox InputScope="Number"/>`

![電話番号用 Windows タッチ キーボード](images/input-scopes/number.png)
- <span data-ttu-id="06dd1-196">スペル チェック: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-196">Spell check: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-197">自動修正: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-197">Auto-correction: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-198">大文字の自動設定: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-198">Automatic capitalization: always disabled</span></span>
- <span data-ttu-id="06dd1-199">予測入力: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-199">Text prediction: on by default, can be disabled</span></span>

### <a name="telephonenumber"></a><span data-ttu-id="06dd1-200">TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="06dd1-200">TelephoneNumber</span></span>

`<TextBox InputScope="TelephoneNumber"/>`

![電話番号用 Windows タッチ キーボード](images/input-scopes/telephonenumber.png)
- <span data-ttu-id="06dd1-202">スペル チェック: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-202">Spell check: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-203">自動修正: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-203">Auto-correction: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-204">大文字の自動設定: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-204">Automatic capitalization: always disabled</span></span>
- <span data-ttu-id="06dd1-205">予測入力: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-205">Text prediction: on by default, can be disabled</span></span>

### <a name="search"></a><span data-ttu-id="06dd1-206">検索</span><span class="sxs-lookup"><span data-stu-id="06dd1-206">Search</span></span>

`<TextBox InputScope="Search"/>`

![検索用 Windows タッチ キーボード](images/input-scopes/search.png)
- <span data-ttu-id="06dd1-208">含まれています、**検索**キーの代わりに、 **Enter**キー</span><span class="sxs-lookup"><span data-stu-id="06dd1-208">Includes the **Search** key instead of the **Enter** key</span></span>
- <span data-ttu-id="06dd1-209">スペル チェック: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-209">Spell check: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-210">自動修正: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-210">Auto-correction: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-211">大文字の自動設定: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-211">Auto-capitalization: always disabled</span></span>
- <span data-ttu-id="06dd1-212">予測入力: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-212">Text prediction: on by default, can be disabled</span></span>

### <a name="searchincremental"></a><span data-ttu-id="06dd1-213">SearchIncremental</span><span class="sxs-lookup"><span data-stu-id="06dd1-213">SearchIncremental</span></span>

`<TextBox InputScope="SearchIncremental"/>`

![インクリメンタル検索を Windows タッチ キーボード](images/input-scopes/searchincremental.png)
- <span data-ttu-id="06dd1-215">同じレイアウト**既定**</span><span class="sxs-lookup"><span data-stu-id="06dd1-215">Same layout as **Default**</span></span>
- <span data-ttu-id="06dd1-216">スペル チェック: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-216">Spell check: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-217">自動修正: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-217">Auto-correction: always disabled</span></span>
- <span data-ttu-id="06dd1-218">大文字の自動設定: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-218">Automatic capitalization: always disabled</span></span>
- <span data-ttu-id="06dd1-219">予測入力: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-219">Text prediction: always disabled</span></span>

### <a name="formula"></a><span data-ttu-id="06dd1-220">[数式]</span><span class="sxs-lookup"><span data-stu-id="06dd1-220">Formula</span></span>

`<TextBox InputScope="Formula"/>`

![式の Windows のタッチ キーボード](images/input-scopes/formula.png)
- <span data-ttu-id="06dd1-222">含まれています、 **=** キー</span><span class="sxs-lookup"><span data-stu-id="06dd1-222">Includes the **=** key</span></span>
- <span data-ttu-id="06dd1-223">含まれています、 **%** 、 **$** 、および **+** キー</span><span class="sxs-lookup"><span data-stu-id="06dd1-223">Also includes the **%**, **$**, and **+** keys</span></span>
- <span data-ttu-id="06dd1-224">スペル チェック: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-224">Spell check: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-225">自動修正: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-225">Auto-correction: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-226">大文字の自動設定: 常に無効</span><span class="sxs-lookup"><span data-stu-id="06dd1-226">Automatic capitalization: always disabled</span></span>
- <span data-ttu-id="06dd1-227">予測入力: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-227">Text prediction: on by default, can be disabled</span></span>

### <a name="chat"></a><span data-ttu-id="06dd1-228">Chat</span><span class="sxs-lookup"><span data-stu-id="06dd1-228">Chat</span></span>

`<TextBox InputScope="Chat"/>`

![既定の Windows タッチ キーボード](images/input-scopes/default.png)
- <span data-ttu-id="06dd1-230">同じレイアウト**既定**</span><span class="sxs-lookup"><span data-stu-id="06dd1-230">Same layout as **Default**</span></span>
- <span data-ttu-id="06dd1-231">スペル チェック: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-231">Spell check: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-232">自動修正: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-232">Auto-correction: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-233">大文字の自動設定: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-233">Automatic capitalization: on by default, can be disabled</span></span>
- <span data-ttu-id="06dd1-234">予測入力: 既定では有効だが、無効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-234">Text prediction: on by default, can be disabled</span></span>

### <a name="nameorphonenumber"></a><span data-ttu-id="06dd1-235">NameOrPhoneNumber</span><span class="sxs-lookup"><span data-stu-id="06dd1-235">NameOrPhoneNumber</span></span>

`<TextBox InputScope="NameOrPhoneNumber"/>`

![既定の Windows タッチ キーボード](images/input-scopes/default.png)
- <span data-ttu-id="06dd1-237">同じレイアウト**既定**</span><span class="sxs-lookup"><span data-stu-id="06dd1-237">Same layout as **Default**</span></span>
- <span data-ttu-id="06dd1-238">スペル チェック: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-238">Spell check: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-239">自動修正: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-239">Auto-correction: off by default, can be enabled</span></span>
- <span data-ttu-id="06dd1-240">大文字の自動: オフ、既定で有効にできます (各単語の最初の文字が大文字で入力)</span><span class="sxs-lookup"><span data-stu-id="06dd1-240">Automatic capitalization: off by default, can be enabled (first letter of each word is capitalized)</span></span>
- <span data-ttu-id="06dd1-241">予測入力: 既定では無効だが、有効にすることも可能</span><span class="sxs-lookup"><span data-stu-id="06dd1-241">Text prediction: off by default, can be enabled</span></span>
