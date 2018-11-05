---
author: mijacobs
Description: In a Universal Windows Platform (UWP) app, command elements are the interactive UI elements that enable the user to perform actions, such as sending an email, deleting an item, or submitting a form.
title: ユニバーサル Windows プラットフォーム (UWP) アプリのコマンド設計の基本
ms.assetid: 1DB48285-07B7-4952-80EF-02B57D4469F2
label: Command design basics
template: detail.hbs
op-migration-status: ready
ms.author: mijacobs
ms.date: 10/01/2018
ms.topic: article
keywords: Windows 10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: 028cc9586180f2d94337282c3ed0cd58317b539b
ms.sourcegitcommit: e814a13978f33654d8e995584f4b047cb53e0aef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6044795"
---
# <a name="command-design-basics-for-uwp-apps"></a><span data-ttu-id="01d55-103">UWP アプリのコマンド設計の基本</span><span class="sxs-lookup"><span data-stu-id="01d55-103">Command design basics for UWP apps</span></span>

<span data-ttu-id="01d55-104">ユニバーサル Windows プラットフォーム (UWP) アプリでは、*コマンド要素*は、ユーザーがメールの送信、項目の削除、フォームの送信などの操作を実行できる対話型の UI 要素をします。</span><span class="sxs-lookup"><span data-stu-id="01d55-104">In a Universal Windows Platform (UWP) app, *command elements* are interactive UI elements that let users perform actions such as sending an email, deleting an item, or submitting a form.</span></span> <span data-ttu-id="01d55-105">*コマンド インターフェイス*は、一般的なコマンド要素、それらをホストするコマンド サーフェス、サポートされる操作、および提供するエクスペリエンスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="01d55-105">*Command interfaces* are composed of common command elements, the command surfaces that host them, the interactions they support, and the experiences they provide.</span></span>

## <a name="provide-the-best-command-experience"></a><span data-ttu-id="01d55-106">最適なコマンド エクスペリエンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="01d55-106">Provide the best command experience</span></span>

<span data-ttu-id="01d55-107">コマンド インターフェイスの最も重要な側面は、どのようなしようとしたユーザーが行うようにします。</span><span class="sxs-lookup"><span data-stu-id="01d55-107">The most important aspect of a command interface is what your trying to let a user accomplish.</span></span> <span data-ttu-id="01d55-108">アプリの機能を計画する際は、これらのタスクと有効にするユーザー エクスペリエンスを実現するための手順を検討してください。</span><span class="sxs-lookup"><span data-stu-id="01d55-108">As you plan the functionality of your app, consider the steps required to accomplish those tasks and the user experiences you want to enable.</span></span> <span data-ttu-id="01d55-109">これらのエクスペリエンスの最初の下書きが完了したら、それらを実装するツールと対話式操作の決定事項を作成できます。</span><span class="sxs-lookup"><span data-stu-id="01d55-109">Once you've completed an initial draft of these experiences, then you can make decisions on the tools and interactions to implement them.</span></span>

<span data-ttu-id="01d55-110">いくつかの一般的なアプリケーション エクスペリエンスを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="01d55-110">Here are some common application experiences:</span></span>

- <span data-ttu-id="01d55-111">情報の送信または提出</span><span class="sxs-lookup"><span data-stu-id="01d55-111">Sending or submiting information</span></span>
- <span data-ttu-id="01d55-112">設定とオプションの選択</span><span class="sxs-lookup"><span data-stu-id="01d55-112">Selecting settings and choices</span></span>
- <span data-ttu-id="01d55-113">コンテンツの検索とフィルター処理</span><span class="sxs-lookup"><span data-stu-id="01d55-113">Searching and filtering content</span></span>
- <span data-ttu-id="01d55-114">ファイルを開く、保存する、削除する</span><span class="sxs-lookup"><span data-stu-id="01d55-114">Opening, saving, and deleting files</span></span>
- <span data-ttu-id="01d55-115">コンテンツの編集または作成</span><span class="sxs-lookup"><span data-stu-id="01d55-115">Editing or creating content</span></span>

<span data-ttu-id="01d55-116">コマンド エクスペリエンスの設計と創造的なあります。</span><span class="sxs-lookup"><span data-stu-id="01d55-116">Be creative with the design of your command experiences.</span></span> <span data-ttu-id="01d55-117">選択する入力デバイス、アプリをサポートし、各デバイスにアプリがどのように対応するか。</span><span class="sxs-lookup"><span data-stu-id="01d55-117">Choose which input devices your app supports, and how your app responds to each device.</span></span> <span data-ttu-id="01d55-118">広範な機能や基本設定をサポートすることによって、使用可能な移植性および可能なアクセシビリティ対応として、アプリを行います。</span><span class="sxs-lookup"><span data-stu-id="01d55-118">By supporting the broadest range of capabilities and preferences you make your app as usable, portable, and accessible as possible.</span></span>



<!--
When designing a command interface, the most important decision is choosing what a user can do. To plan the right type of interactions, focus on your app - consider the user experiences you want to enable, and what steps users will need to take. Once you decide what you want users to accomplish, then you can provide them the tools to do so.
-->

## <a name="choose-the-right-command-elements"></a><span data-ttu-id="01d55-119">適切なコマンド要素を選択します。</span><span class="sxs-lookup"><span data-stu-id="01d55-119">Choose the right command elements</span></span>

<span data-ttu-id="01d55-120">コマンド インターフェイスで適切な要素を使うことを直感的で使いやすいアプリと困難、混乱を招くアプリの違いことができます。</span><span class="sxs-lookup"><span data-stu-id="01d55-120">Using the right elements in a command interface can make the difference between an intuitive, easy-to-use app and a difficult, confusing app.</span></span> <span data-ttu-id="01d55-121">包括的な一連のコマンド要素は、ユニバーサル Windows プラットフォーム (UWP) で使用できます。</span><span class="sxs-lookup"><span data-stu-id="01d55-121">A comprehensive set of command elements are available in the Universal Windows Platform (UWP).</span></span> <span data-ttu-id="01d55-122">次に、最も一般的な UWP コマンド要素の一部の一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="01d55-122">Here's a list of some of the most common UWP command elements.</span></span>

:::row:::
    :::column:::
        ![button image](images/commanding/thumbnail-button.svg)
    :::column-end:::
    :::column span="2":::
        <b>Buttons</b>

        <a href="../controls-and-patterns/buttons.md" style="text-decoration:none">Buttons</a> trigger an immediate action. Examples include sending an email, submitting form data, or confirming an action in a dialog.
:::row-end:::

:::row:::
    :::column:::
        ![list image](images/commanding/thumbnail-list.svg)
    :::column-end:::
    :::column span="2":::
        <b>Lists</b>

        <a href="../controls-and-patterns/lists.md" style="text-decoration:none">Lists</a> present items in a interactive list or a grid. Usually used for many options or display items. Examples include drop-down list, list box, list view and grid view.
:::row-end:::

:::row:::
    :::column:::
        ![selection control image](images/commanding/thumbnail-selection.svg)
    :::column-end:::
    :::column span="2":::
        <b>Selection controls</b>

        Lets users choose from a few options, such as when completing a survey or configuring app settings. Examples include <a href="../controls-and-patterns/checkbox.md">check box</a>, <a href="../controls-and-patterns/radio-button.md">radio button</a>, and <a href="../controls-and-patterns/toggles.md">toggle switch</a>.
:::row-end:::

:::row:::
    :::column:::
        ![Calendar  image](images/commanding/thumbnail-calendar.svg)
    :::column-end:::
    :::column span="2":::
        <b>Calendar, date and time pickers</b>

        <a href="../controls-and-patterns/date-and-time.md">Calendar, date and time pickers</a> enable users to view and modify date and time info, such as when creating an event or setting an alarm. Examples include calendar date picker, calendar view, date picker, time picker.
:::row-end:::

:::row:::
    :::column:::
        ![Predictive text entry image](images/commanding/thumbnail-autosuggest.svg)
    :::column-end:::
    :::column span="2":::
        <b>Predictive text entry</b>

        Provides suggestions as users type, such as when entering data or performing queries. Examples include <a href="../controls-and-patterns/auto-suggest-box.md">auto-suggest box</a>.<br>
:::row-end:::

<span data-ttu-id="01d55-123">全一覧については、「[コントロールと UI 要素](../controls-and-patterns/index.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="01d55-123">For a complete list, see [Controls and UI elements](../controls-and-patterns/index.md)</span></span>

## <a name="place-commands-on-the-right-surface"></a><span data-ttu-id="01d55-124">適切なサーフェスへのコマンドの配置</span><span class="sxs-lookup"><span data-stu-id="01d55-124">Place commands on the right surface</span></span>

<span data-ttu-id="01d55-125">アプリのキャンバスやコマンド バー、コマンド バーのポップアップ、メニュー バーでは、ダイアログなどの特殊なコマンド コンテナーを含む、アプリでの多くのサーフェスにコマンド要素を配置できます。</span><span class="sxs-lookup"><span data-stu-id="01d55-125">You can place command elements on a number of surfaces in your app, including the app canvas or special command containers, such as a command bar, command bar flyout, menu bar, or dialog.</span></span>

<span data-ttu-id="01d55-126">常にユーザーが直接コンテンツを操作できるようにするではなくを通じてコマンド、コンテンツを上下に移動するコマンド ボタンではなく、ドラッグ アンド ドロップ リスト項目を配置し直すなどの動作を表します。</span><span class="sxs-lookup"><span data-stu-id="01d55-126">Always try to let users manipulate content directly rather than through commands that act on the content, such as dragging and dropping to rearrange list items rather than up and down command buttons.</span></span> 

<span data-ttu-id="01d55-127">ただし、このできない可能性があります、特定の入力デバイスまたは特定のユーザーの機能と設定に対応している場合。</span><span class="sxs-lookup"><span data-stu-id="01d55-127">However, this might not be possible with certain input devices, or when accommodating specific user abilities and preferences.</span></span> <span data-ttu-id="01d55-128">このような場合は、できるだけ多くのコマンド実行アフォー ダンスを提供し、これらのコマンド要素をアプリでのコマンド サーフェスに配置します。</span><span class="sxs-lookup"><span data-stu-id="01d55-128">In these cases, provide as many commanding affordances as possible, and place these command elements on a command surface in your app.</span></span>

<span data-ttu-id="01d55-129">最も一般的ないくつかのコマンド サーフェスの一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="01d55-129">Here's a list of some of the most common command surfaces.</span></span>

:::row:::
    :::column:::
        ![app canvas image](images/commanding/thumbnail-canvas.svg)
    :::column-end:::
    :::column span="2":::
        <b>App canvas (content area)</b>

        If a command is constantly needed for users to complete core scenarios, put it on the canvas. Because you can put commands near (or on) the objects they affect, putting commands on the canvas makes them easy and obvious to use. However, choose the commands you put on the canvas carefully. Too many commands on the app canvas take up valuable screen space and can overwhelm the user. If the command won't be frequently used, consider putting it in another command surface.
:::row-end:::

:::row:::
    :::column:::
        ![commandbar image](images/commanding/thumbnail-commandbar.svg)
    :::column-end:::
    :::column span="2":::
        <b>Command bars and menu bars</b>

        <a href="../controls-and-patterns/app-bars.md">Command bars</a> help organize commands and make them easy to access. Command bars can be placed at the top of the screen, at the bottom of the screen, or at both the top and bottom of the screen (a <a href="../controls-and-patterns/menus.md#create-a-menu-bar">MenuBar</a> can also be used when the functionality in your app is too complex for a command bar).
:::row-end:::

:::row:::
    :::column:::
        ![context menu image](images/commanding/thumbnail-contextmenu.svg)
    :::column-end:::
    :::column span="2":::
        <b>Menus and context menus</b>

        <p>Menus and context menus save space by organizing commands and hiding them until the user needs them. Users typically access a menu or context menu by clicking a button or right-clicking a control.</p> 

        <p>The <a href="../controls-and-patterns/command-bar-flyout.md">command bar flyout </a> is a type of contextual menu that combines the benefits of a command bar and a context menu into a single control. It can provide shortcuts to commonly-used actions and provide access to secondary commands that are only relevant in certain contexts, such as clipboard or custom commands.</p>

        <p>UWP also provides a set of traditional menus and context menus; for more info, see the <a href="../controls-and-patterns/menus.md">menus and context menus overview</a>.</p>
:::row-end:::

## <a name="provide-command-feedback"></a><span data-ttu-id="01d55-130">コマンドのフィードバックを提供します。</span><span class="sxs-lookup"><span data-stu-id="01d55-130">Provide command feedback</span></span> 

<span data-ttu-id="01d55-131">コマンドのフィードバックは、操作やコマンドが検出された、どのように解釈および処理された、かどうかが成功したかに、ユーザーと通信します。</span><span class="sxs-lookup"><span data-stu-id="01d55-131">Command feedback communicates to users that an interaction or command was detected, how it was interpreted and handled, and whether it was successful or not.</span></span> <span data-ttu-id="01d55-132">これにより、実行したこと、および次に実行できる機能を把握することができます。</span><span class="sxs-lookup"><span data-stu-id="01d55-132">This helps users understand what they've done, and what they can do next.</span></span> <span data-ttu-id="01d55-133">フィードバックが UI に自然に統合されていて、ユーザーの介在が不要であるか、どうしても必要な場合以外は他の操作が不要であることが理想的です。</span><span class="sxs-lookup"><span data-stu-id="01d55-133">Ideally, feedback should be integrated naturally in your UI, so users don't have to be interrupted, or take additional action unless absolutely necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="01d55-134">どうしても必要なフィードバックは他の場所でない限り、フィードバックを提供しません。</span><span class="sxs-lookup"><span data-stu-id="01d55-134">Don't provide feedback unless it is absolutely necessary and the feedback is not available elsewhere.</span></span> <span data-ttu-id="01d55-135">値を追加する場合を除き、簡潔、アプリの UI を維持します。</span><span class="sxs-lookup"><span data-stu-id="01d55-135">Keep your application UI clean and uncluttered unless you are adding value.</span></span>

<span data-ttu-id="01d55-136">アプリでフィードバックを提供する方法をいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="01d55-136">Here are some ways to provide feedback in your app.</span></span>

:::row:::
    :::column:::
        ![commandbar content area image](images/commanding/thumbnail-commandbar2.svg)
    :::column-end:::
    :::column span="2":::
        <b>Command bar</b>

        The content area of the <a href="../controls-and-patterns/app-bars.md">command bar</a> is an intuitive place to communicate status to users if they'd like to see feedback.
:::row-end:::

:::row:::
    :::column:::
        ![Flyout image](images/commanding/thumbnail-flyout.svg)
    :::column-end:::
    :::column span="2":::
        <b>Flyouts</b>

       <span data-ttu-id="01d55-137"><a href="../controls-and-patterns/dialogs-and-flyouts/index.md">ポップアップ</a>は、軽量のコンテキストに沿ったポップアップをタップするか、どこかクリックすると、ポップアップの外側で閉じることができます。</span><span class="sxs-lookup"><span data-stu-id="01d55-137"><a href="../controls-and-patterns/dialogs-and-flyouts/index.md">Flyouts</a> are lightweight contextual popups that can be dismissed by tapping or clicking somewhere outside the flyout.</span></span>
:::row-end:::

:::row:::
    :::column:::
        ![Dialog image](images/commanding/thumbnail-dialog.svg)
    :::column-end:::
    :::column span="2":::
        <b>Dialog controls</b>

        <a href="../controls-and-patterns/dialogs-and-flyouts/index.md">Dialog controls</a> are modal UI overlays that provide contextual app information. In most cases, dialogs block interactions with the app window until being explicitly dismissed, and often request some kind of action from the user. Dialogs can be disruptive and should only be used in certain situations. For more info, see the [When to confirm or undo actions](#when-to-confirm-or-undo-actions) section.
    :::column-end:::
:::row-end:::

> [!TIP]
> <span data-ttu-id="01d55-138">アプリで使う確認ダイアログの量に注意してください。ユーザーが間違えたときはとても役に立ちますが、ユーザーが意図的にアクションを実行しようとしているときは邪魔になります。</span><span class="sxs-lookup"><span data-stu-id="01d55-138">Be careful of how much your app uses confirmation dialogs; they can be very helpful when the user makes a mistake, but they are a hindrance whenever the user is trying to perform an action intentionally.</span></span>

### <a name="when-to-confirm-or-undo-actions"></a><span data-ttu-id="01d55-139">アクションを確認または元に戻すタイミング</span><span class="sxs-lookup"><span data-stu-id="01d55-139">When to confirm or undo actions</span></span>

<span data-ttu-id="01d55-140">適切に設計された、アプリケーションの UI は、すべてのユーザーであってアクションを実行します。</span><span class="sxs-lookup"><span data-stu-id="01d55-140">No matter how well-designed your application's UI is, all users perform an action they wish they hadn't.</span></span> <span data-ttu-id="01d55-141">最近の操作を元に戻す方法を提供するや、アクションの確認を求めるによってこれらの状況で、アプリが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="01d55-141">Your app can help in these situations by requiring confirmation of an action, or by providing a way to undo recent actions.</span></span>

:::row:::
    :::column:::
        ![do image](images/do.svg)

        For actions that can't be undone and have major consequences, we recommend using a confirmation dialog. Examples of such actions include:
        -   Overwriting a file
        -   Not saving a file before closing
        -   Confirming permanent deletion of a file or data
        -   Making a purchase (unless the user opts out of requiring a confirmation)
        -   Submitting a form, such as signing up for something
    :::column-end:::
    :::column:::
        ![do image](images/do.svg)

        For actions that can be undone, offering a simple undo command is usually enough. Examples of such actions include:
        -   Deleting a file
        -   Deleting an email (not permanently)
        -   Modifying content or editing text
        -   Renaming a file
:::row-end:::

##  <a name="optimize-for-specific-input-types"></a><span data-ttu-id="01d55-142">特定の入力タイプの最適化</span><span class="sxs-lookup"><span data-stu-id="01d55-142">Optimize for specific input types</span></span>

<span data-ttu-id="01d55-143">特定の入力の種類やデバイスを中心としたユーザー エクスペリエンスの最適化について詳しくは、「[操作の基本情報](../input/index.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="01d55-143">See the [Interaction primer](../input/index.md) for more detail on optimizing user experiences around a specific input type or device.</span></span>

