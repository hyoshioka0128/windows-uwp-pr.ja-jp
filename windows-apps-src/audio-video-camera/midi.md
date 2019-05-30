---
ms.assetid: 9146212C-8480-4C16-B74C-D7F08C7086AF
description: この記事では、MIDI (Musical Instrument Digital Interface) デバイスを列挙する方法と、ユニバーサル Windows アプリとの間で MIDI メッセージを送受信する方法について説明します。
title: MIDI
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 2737713030d68dbc19aaad3df767cea103b53f35
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66361597"
---
# <a name="midi"></a><span data-ttu-id="6fe33-104">MIDI</span><span class="sxs-lookup"><span data-stu-id="6fe33-104">MIDI</span></span>



<span data-ttu-id="6fe33-105">この記事では、MIDI (Musical Instrument Digital Interface) デバイスを列挙する方法と、ユニバーサル Windows アプリとの間で MIDI メッセージを送受信する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-105">This article shows you how to enumerate MIDI (Musical Instrument Digital Interface) devices and send and receive MIDI messages from a Universal Windows app.</span></span> <span data-ttu-id="6fe33-106">Windows 10 (クラスに準拠していませんし、最も独自ドライバー)、MIDI Bluetooth LE 経由での USB 経由で MIDI をサポートしています (Windows 10 Anniversary Edition 以降)、および over Ethernet MIDI とルーティング MIDI、自由に利用できるサード パーティ製品を使用します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-106">Windows 10 supports MIDI over USB (class-compliant and most proprietary drivers), MIDI over Bluetooth LE (Windows 10 Anniversary Edition and later), and through freely-available third-party products, MIDI over Ethernet and routed MIDI.</span></span>

## <a name="enumerate-midi-devices"></a><span data-ttu-id="6fe33-107">MIDI デバイスの列挙</span><span class="sxs-lookup"><span data-stu-id="6fe33-107">Enumerate MIDI devices</span></span>

<span data-ttu-id="6fe33-108">MIDI デバイスを列挙して使う前に、次の名前空間をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-108">Before enumerating and using MIDI devices, add the following namespaces to your project.</span></span>

[!code-cs[Using](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetUsing)]

<span data-ttu-id="6fe33-109">XAML ページに [**ListBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox) コントロールを追加して、システムに接続されている MIDI 入力デバイスのいずれかをユーザーが選択できるようにします。</span><span class="sxs-lookup"><span data-stu-id="6fe33-109">Add a [**ListBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox) control to your XAML page that will allow the user to select one of the MIDI input devices attached to the system.</span></span> <span data-ttu-id="6fe33-110">また、MIDI 出力の一覧を表示する別のコントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-110">Add another one to list the MIDI output devices.</span></span>

[!code-xml[MidiListBoxes](./code/MIDIWin10/cs/MainPage.xaml#SnippetMidiListBoxes)]

<span data-ttu-id="6fe33-111">[  **FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) メソッドの [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) クラスは、Windows によって認識される多くの異なる種類のデバイスを列挙するのに使われます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-111">The [**FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) method [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) class is used to enumerate many different types of devices that are recognized by Windows.</span></span> <span data-ttu-id="6fe33-112">メソッドで MIDI 入力デバイスだけを検索するよう指定するには、[**MidiInPort.GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.getdeviceselector) によって返されるセレクター文字列を使います。</span><span class="sxs-lookup"><span data-stu-id="6fe33-112">To specify that you only want the method to find MIDI input devices, use the selector string returned by [**MidiInPort.GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.getdeviceselector).</span></span> <span data-ttu-id="6fe33-113">**FindAllAsync** は、システムに登録されている各 MIDI 入力デバイスの **DeviceInformation** が格納された [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) を返します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-113">**FindAllAsync** returns a [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) that contains a **DeviceInformation** for each MIDI input device registered with the system.</span></span> <span data-ttu-id="6fe33-114">返されたコレクションに項目が含まれていない場合、利用可能な MIDI 入力デバイスはありません。</span><span class="sxs-lookup"><span data-stu-id="6fe33-114">If the returned collection contains no items, then there are no available MIDI input devices.</span></span> <span data-ttu-id="6fe33-115">コレクションに項目が含まれる場合は、**DeviceInformation** オブジェクトのループ処理を行い、各デバイスの名前を MIDI 入力デバイスの **ListBox** に追加します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-115">If there are items in the collection, loop through the **DeviceInformation** objects and add the name of each device to the MIDI input device **ListBox**.</span></span>

[!code-cs[EnumerateMidiInputDevices](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetEnumerateMidiInputDevices)]

<span data-ttu-id="6fe33-116">MIDI 出力デバイスの列挙も入力デバイスの列挙とまったく同じように動作しますが、**FindAllAsync** を呼び出すときに、[**MidiOutPort.GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midioutport.getdeviceselector) によって返されるセレクター文字列を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fe33-116">Enumerating MIDI output devices works the exact same way as enumerating input devices, except that you should specify the selector string returned by [**MidiOutPort.GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midioutport.getdeviceselector) when calling **FindAllAsync**.</span></span>

[!code-cs[EnumerateMidiOutputDevices](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetEnumerateMidiOutputDevices)]



## <a name="create-a-device-watcher-helper-class"></a><span data-ttu-id="6fe33-117">デバイス ウォッチャーのヘルパー クラスを作成する</span><span class="sxs-lookup"><span data-stu-id="6fe33-117">Create a device watcher helper class</span></span>

<span data-ttu-id="6fe33-118">[  **Windows.Devices.Enumeration**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) 名前空間の [**DeviceWatcher**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) は、システムにデバイスが追加されるか削除された場合、またはデバイスの情報が更新された場合に、アプリに通知を送信できます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-118">The [**Windows.Devices.Enumeration**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) namespace provides the [**DeviceWatcher**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) which can notify your app if devices are added or removed from the system, or if the information for a device is updated.</span></span> <span data-ttu-id="6fe33-119">MIDI 対応アプリでは通常、入力デバイスと出力デバイスの両方に関心があるため、この例では、**DeviceWatcher** パターンを実装するヘルパー クラスを作成して、同じコードを複製することなく MIDI 入力デバイスと MIDI 出力デバイスの両方に使えるようにします。</span><span class="sxs-lookup"><span data-stu-id="6fe33-119">Since MIDI-enabled apps typically are interested in both input and output devices, this example creates a helper class that implements the **DeviceWatcher** pattern, so that the same code can be used for both MIDI input and MIDI output devices, without the need for duplication.</span></span>

<span data-ttu-id="6fe33-120">デバイス ウォッチャーとして機能する新しいクラスをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-120">Add a new class to your project to serve as your device watcher.</span></span> <span data-ttu-id="6fe33-121">この例では、クラスの名前は **MyMidiDeviceWatcher** です。</span><span class="sxs-lookup"><span data-stu-id="6fe33-121">In this example the class is named **MyMidiDeviceWatcher**.</span></span> <span data-ttu-id="6fe33-122">このセクションのコードの残りの部分は、ヘルパー クラスの実装に使われます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-122">The rest of the code in this section is used to implement the helper class.</span></span>

<span data-ttu-id="6fe33-123">クラスにいくつかのメンバー変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-123">Add some member variables to the class:</span></span>

-   <span data-ttu-id="6fe33-124">デバイスの変更を監視する [**DeviceWatcher**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="6fe33-124">A [**DeviceWatcher**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) object that will monitor for device changes.</span></span>
-   <span data-ttu-id="6fe33-125">1 つのインスタンスには MIDI 入力ポートのセレクター文字列、もう 1 つのインスタンスには MIDI 出力ポートのセレクター文字列が格納される、デバイス セレクター文字列。</span><span class="sxs-lookup"><span data-stu-id="6fe33-125">A device selector string that will contain the MIDI in port selector string for one instance and the MIDI out port selector string for another instance.</span></span>
-   <span data-ttu-id="6fe33-126">利用可能なデバイスの名前が格納される [**ListBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox) コントロール。</span><span class="sxs-lookup"><span data-stu-id="6fe33-126">A [**ListBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox) control that will be populated with the names of the available devices.</span></span>
-   <span data-ttu-id="6fe33-127">UI スレッド以外のスレッドから UI を更新するために必要な [**CoreDispatcher**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreDispatcher)。</span><span class="sxs-lookup"><span data-stu-id="6fe33-127">A [**CoreDispatcher**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreDispatcher) that is required to update the UI from a thread other than the UI thread.</span></span>

[!code-cs[WatcherVariables](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherVariables)]

<span data-ttu-id="6fe33-128">ヘルパー クラスの外部からのデバイスの現在の一覧にアクセスするために使用される [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) プロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-128">Add a [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) property that is used to access the current list of devices from outside the helper class.</span></span>

[!code-cs[DeclareDeviceInformationCollection](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetDeclareDeviceInformationCollection)]

<span data-ttu-id="6fe33-129">クラスのコンストラクターで、呼び出し元は MIDI デバイスのセレクター文字列、デバイスの一覧を表示する **ListBox**、および UI の更新に必要な **Dispatcher** を渡します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-129">In class constructor, the caller passes in the MIDI device selector string, the **ListBox** for listing the devices, and the **Dispatcher** needed to update the UI.</span></span>

<span data-ttu-id="6fe33-130">MIDI デバイスのセレクター文字列を渡して [**DeviceInformation.CreateWatcher**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.createwatcher) を呼び出し、**DeviceWatcher** クラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-130">Call [**DeviceInformation.CreateWatcher**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.createwatcher) to create a new instance of the **DeviceWatcher** class, passing in the MIDI device selector string.</span></span>

<span data-ttu-id="6fe33-131">ウォッチャーのイベント ハンドラーに対してハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-131">Register handlers for the watcher's event handlers.</span></span>

[!code-cs[WatcherConstructor](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherConstructor)]

<span data-ttu-id="6fe33-132">**DeviceWatcher** には次のイベントがあります。</span><span class="sxs-lookup"><span data-stu-id="6fe33-132">The **DeviceWatcher** has the following events:</span></span>

-   <span data-ttu-id="6fe33-133">[**追加**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.added) -新しいデバイスがシステムに追加されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-133">[**Added**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.added) - Raised when a new device is added to the system.</span></span>
-   <span data-ttu-id="6fe33-134">[**削除**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.removed) -デバイスがシステムから削除されるときに発生します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-134">[**Removed**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.removed) - Raised when a device is removed from the system.</span></span>
-   <span data-ttu-id="6fe33-135">[**更新**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.updated) -既存のデバイスに関連付けられている情報が更新されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-135">[**Updated**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.updated) - Raised when the information associated with an existing device is updated.</span></span>
-   <span data-ttu-id="6fe33-136">[**EnumerationCompleted** ](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) -ウォッチャーには、要求されたデバイスの種類の列挙が完了したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-136">[**EnumerationCompleted**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) - Raised when the watcher has completed its enumeration of the requested device type.</span></span>

<span data-ttu-id="6fe33-137">これらの各イベントのイベント ハンドラーで、ヘルパー メソッド **UpdateDevices** が呼び出され、現在のデバイスの一覧で **ListBox** が更新されます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-137">In the event handler for each of these events, a helper method, **UpdateDevices**, is called to update the **ListBox** with the current list of devices.</span></span> <span data-ttu-id="6fe33-138">**UpdateDevices** は UI 要素を更新し、これらのイベント ハンドラーは UI スレッドでは呼び出されないため、各呼び出しを [**RunAsync**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows) の呼び出しにラップすることで、指定したコードが UI スレッドで実行されるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6fe33-138">Because **UpdateDevices** updates UI elements and these event handlers are not called on the UI thread, each call must be wrapped in a call to [**RunAsync**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows), which causes the specified code to be run on the UI thread.</span></span>

[!code-cs[WatcherEventHandlers](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherEventHandlers)]

<span data-ttu-id="6fe33-139">**UpdateDevices** ヘルパー メソッドは、[**DeviceInformation.FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) を呼び出し、この記事の前半で説明したように、返されたデバイスの名前で **ListBox** を更新します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-139">The **UpdateDevices** helper method calls [**DeviceInformation.FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) and updates the **ListBox** with the names of the returned devices as described previously in this article.</span></span>

[!code-cs[WatcherUpdateDevices](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherUpdateDevices)]

<span data-ttu-id="6fe33-140">**DeviceWatcher** オブジェクトの [**Start**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.start) メソッドを使って、ウォッチャーを起動するメソッドを追加し、[**Stop**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.stop) メソッドを使ってウォッチャーを停止するメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-140">Add methods to start the watcher, using the **DeviceWatcher** object's [**Start**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.start) method, and to stop the watcher, using the [**Stop**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.stop) method.</span></span>

[!code-cs[WatcherStopStart](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherStopStart)]

<span data-ttu-id="6fe33-141">ウォッチャーのイベント ハンドラーの登録を解除し、デバイス ウォッチャーを null に設定する、デストラクターを用意します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-141">Provide a destructor to unregister the watcher event handlers and set the device watcher to null.</span></span>

[!code-cs[WatcherDestructor](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherDestructor)]

## <a name="create-midi-ports-to-send-and-receive-messages"></a><span data-ttu-id="6fe33-142">メッセージを送受信する MIDI ポートを作成する</span><span class="sxs-lookup"><span data-stu-id="6fe33-142">Create MIDI ports to send and receive messages</span></span>

<span data-ttu-id="6fe33-143">ページの分離コードで、**MyMidiDeviceWatcher** ヘルパー クラスの 2 つのインスタンスを保持するメンバー変数を宣言します。1 つは入力デバイス用、もう 1 つは出力デバイス用です。</span><span class="sxs-lookup"><span data-stu-id="6fe33-143">In the code behind for your page, declare member variables to hold two instances of the **MyMidiDeviceWatcher** helper class, one for input devices and one for output devices.</span></span>

[!code-cs[DeclareDeviceWatchers](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetDeclareDeviceWatchers)]

<span data-ttu-id="6fe33-144">ウォッチャー ヘルパー クラスの新しいインスタンスを作成し、デバイスのセレクター文字列、格納する **ListBox**、およびページの **Dispatcher** プロパティでアクセスできる **CoreDispatcher** オブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-144">Create a new instance of the watcher helper classes, passing in the device selector string, the **ListBox** to be populated, and the **CoreDispatcher** object that can be accessed through the page's **Dispatcher** property.</span></span> <span data-ttu-id="6fe33-145">次に、各オブジェクトの **DeviceWatcher** を起動するメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-145">Then, call the method to start each object's **DeviceWatcher**.</span></span>

<span data-ttu-id="6fe33-146">各 **DeviceWatcher** は起動するとすぐに、現在システムに接続されているデバイスの列挙を完了し、[**EnumerationCompleted**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) イベントを発生させます。これにより、各 **ListBox** が現在の MIDI デバイスで更新されます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-146">Shortly after each **DeviceWatcher** is started, it will finish enumerating the current devices connected to the system and raise its [**EnumerationCompleted**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) event, which will cause each **ListBox** to be updated with the current MIDI devices.</span></span>

[!code-cs[StartWatchers](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetStartWatchers)]

<span data-ttu-id="6fe33-147">ユーザーが MIDI 入力 **ListBox** の項目を選択すると、[**SelectionChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) イベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-147">When the user selects an item in the MIDI input **ListBox**, the [**SelectionChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) event is raised.</span></span> <span data-ttu-id="6fe33-148">このイベントのハンドラーで、ヘルパー クラスの **DeviceInformationCollection** プロパティにアクセスして、デバイスの現在の一覧を取得します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-148">In the handler for this event, access the **DeviceInformationCollection** property of the helper class to get the current list of devices.</span></span> <span data-ttu-id="6fe33-149">一覧にエントリが含まれている場合は、**ListBox** コントロールの [**SelectedIndex**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectedindex) に対応するインデックスを持つ **DeviceInformation** オブジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-149">If there are entries in the list, select the **DeviceInformation** object with the index corresponding to the **ListBox** control's [**SelectedIndex**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectedindex).</span></span>

<span data-ttu-id="6fe33-150">選択したデバイスの [**Id**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.id) プロパティを渡して [**MidiInPort.FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.fromidasync) を呼び出すことにより、選択した入力デバイスを表す [**MidiInPort**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiInPort) オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-150">Create the [**MidiInPort**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiInPort) object representing the selected input device by calling [**MidiInPort.FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.fromidasync), passing in the [**Id**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.id) property of the selected device.</span></span>

<span data-ttu-id="6fe33-151">指定されたデバイスで MIDI メッセージが受信されるたびに発生する [**MessageReceived**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.messagereceived) イベントのハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-151">Register a handler for the [**MessageReceived**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.messagereceived) event, which is raised whenever a MIDI message is received through the specified device.</span></span>

[!code-cs[DeclareMidiPorts](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetDeclareMidiPorts)]

[!code-cs[InPortSelectionChanged](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetInPortSelectionChanged)]

<span data-ttu-id="6fe33-152">**MessageReceived** ハンドラーが呼び出されると、**MidiMessageReceivedEventArgs** の [**Message**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiMessageReceivedEventArgs) プロパティにメッセージが格納されます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-152">When the **MessageReceived** handler is called, the message is contained in the [**Message**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiMessageReceivedEventArgs) property of the **MidiMessageReceivedEventArgs**.</span></span> <span data-ttu-id="6fe33-153">メッセージ オブジェクトの [**Type**](https://docs.microsoft.com/uwp/api/windows.devices.midi.imidimessage.type) は、受信したメッセージの種類を示す [**MidiMessageType**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiMessageType) 列挙体の値です。</span><span class="sxs-lookup"><span data-stu-id="6fe33-153">The [**Type**](https://docs.microsoft.com/uwp/api/windows.devices.midi.imidimessage.type) of the message object is a value from the [**MidiMessageType**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiMessageType) enumeration indicating the type of message that was received.</span></span> <span data-ttu-id="6fe33-154">メッセージのデータは、メッセージの種類によって異なります。</span><span class="sxs-lookup"><span data-stu-id="6fe33-154">The data of the message depends on the type of the message.</span></span> <span data-ttu-id="6fe33-155">この例では、メッセージがノートオン メッセージであるかどうかを確認し、そうである場合は、メッセージの MIDI チャネル、ノート、およびベロシティを出力します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-155">This example checks to see if the message is a note on message and, if so, outputs the midi channel, note, and velocity of the message.</span></span>

[!code-cs[MessageReceived](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetMessageReceived)]

<span data-ttu-id="6fe33-156">出力デバイス **ListBox** の [**SelectionChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) ハンドラーは、入力デバイスのハンドラーと同じように動作しますが、イベント ハンドラーは登録されません。</span><span class="sxs-lookup"><span data-stu-id="6fe33-156">The [**SelectionChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) handler for the output device **ListBox** works the same as the handler for input devices, except no event handler is registered.</span></span>

[!code-cs[OutPortSelectionChanged](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetOutPortSelectionChanged)]

<span data-ttu-id="6fe33-157">出力デバイスが作成されたら、送信するメッセージの種類に対する新しい [**IMidiMessage**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.IMidiMessage) を作成して、メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-157">Once the output device is created, you can send a message by creating a new [**IMidiMessage**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.IMidiMessage) for the type of message you want to send.</span></span> <span data-ttu-id="6fe33-158">この例では、メッセージは [**NoteOnMessage**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiNoteOnMessage) です。</span><span class="sxs-lookup"><span data-stu-id="6fe33-158">In this example, the message is a [**NoteOnMessage**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiNoteOnMessage).</span></span> <span data-ttu-id="6fe33-159">[  **IMidiOutPort**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.IMidiOutPort) オブジェクトの [**SendMessage**](https://docs.microsoft.com/uwp/api/windows.devices.midi.imidioutport.sendmessage) メソッドが呼び出されて、メッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-159">The [**SendMessage**](https://docs.microsoft.com/uwp/api/windows.devices.midi.imidioutport.sendmessage) method of the [**IMidiOutPort**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.IMidiOutPort) object is called to send the message.</span></span>

[!code-cs[SendMessage](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetSendMessage)]

<span data-ttu-id="6fe33-160">アプリが非アクティブ化になったときは、必ずアプリのリソースをクリーンアップしてください。</span><span class="sxs-lookup"><span data-stu-id="6fe33-160">When your app is deactivated, be sure to clean up your apps resources.</span></span> <span data-ttu-id="6fe33-161">イベント ハンドラーの登録を解除し、MIDI の入力ポート オブジェクトと出力ポート オブジェクトを null に設定します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-161">Unregister your event handlers and set the MIDI in port and out port objects to null.</span></span> <span data-ttu-id="6fe33-162">デバイス ウォッチャーを停止し、null に設定します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-162">Stop the device watchers and set them to null.</span></span>

[!code-cs[CleanUp](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetCleanUp)]

## <a name="using-the-built-in-windows-general-midi-synth"></a><span data-ttu-id="6fe33-163">組み込みの Windows General MIDI シンセサイザーを使用する</span><span class="sxs-lookup"><span data-stu-id="6fe33-163">Using the built-in Windows General MIDI synth</span></span>

<span data-ttu-id="6fe33-164">上記で説明した手法を使用して MIDI 出力デバイスを列挙すると、アプリは、"Microsoft GS Wavetable Synth" という MIDI デバイスを検出します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-164">When you enumerate output MIDI devices using the technique described above, your app will discover a MIDI device called "Microsoft GS Wavetable Synth".</span></span> <span data-ttu-id="6fe33-165">このデバイスは、アプリから使用できる組み込みの General MIDI シンセサイザーです。</span><span class="sxs-lookup"><span data-stu-id="6fe33-165">This is a built-in General MIDI synthesizer that you can play from your app.</span></span> <span data-ttu-id="6fe33-166">ただし、組み込みのシンセサイザーの SDK 拡張機能をプロジェクトに含めていない限り、このデバイスへの MIDI アウトポートを作成しようとすると失敗します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-166">However, attempting to create a MIDI outport to this device will fail unless you have included the SDK extension for the built-in synth in your project.</span></span>

<span data-ttu-id="6fe33-167">**汎用 MIDI シンセサイザー SDK 拡張機能をアプリ プロジェクトに含める**</span><span class="sxs-lookup"><span data-stu-id="6fe33-167">**To include the General MIDI Synth SDK extension in your app project**</span></span>

1.  <span data-ttu-id="6fe33-168">**ソリューション エクスプローラー**で、プロジェクトの下にある **[参照設定]** を右クリックし、 **[参照の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-168">In **Solution Explorer**, under your project, right-click **References** and select **Add reference...**</span></span>
2.  <span data-ttu-id="6fe33-169">**[Universal Windows]** ノードを展開します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-169">Expand the **Universal Windows** node.</span></span>
3.  <span data-ttu-id="6fe33-170">**[拡張機能]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-170">Select **Extensions**.</span></span>
4.  <span data-ttu-id="6fe33-171">拡張機能の一覧から **[Microsoft General MIDI DLS for Universal Windows Apps]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="6fe33-171">From the list of extensions, select **Microsoft General MIDI DLS for Universal Windows Apps**.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="6fe33-172">複数のバージョンの拡張機能がある場合、アプリのターゲットと一致するバージョンを選んでください。</span><span class="sxs-lookup"><span data-stu-id="6fe33-172">If there are multiple versions of the extension, be sure to select the version that matches the target for your app.</span></span> <span data-ttu-id="6fe33-173">プロジェクトのプロパティの **[アプリケーション]** タブで、アプリがターゲットとしている SDK バージョンを確認できます。</span><span class="sxs-lookup"><span data-stu-id="6fe33-173">You can see which SDK version your app is targeting on the **Application** tab of the project Properties.</span></span>

 

 




