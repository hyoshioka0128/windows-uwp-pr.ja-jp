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
# <a name="midi"></a>MIDI



この記事では、MIDI (Musical Instrument Digital Interface) デバイスを列挙する方法と、ユニバーサル Windows アプリとの間で MIDI メッセージを送受信する方法について説明します。 Windows 10 (クラスに準拠していませんし、最も独自ドライバー)、MIDI Bluetooth LE 経由での USB 経由で MIDI をサポートしています (Windows 10 Anniversary Edition 以降)、および over Ethernet MIDI とルーティング MIDI、自由に利用できるサード パーティ製品を使用します。

## <a name="enumerate-midi-devices"></a>MIDI デバイスの列挙

MIDI デバイスを列挙して使う前に、次の名前空間をプロジェクトに追加します。

[!code-cs[Using](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetUsing)]

XAML ページに [**ListBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox) コントロールを追加して、システムに接続されている MIDI 入力デバイスのいずれかをユーザーが選択できるようにします。 また、MIDI 出力の一覧を表示する別のコントロールを追加します。

[!code-xml[MidiListBoxes](./code/MIDIWin10/cs/MainPage.xaml#SnippetMidiListBoxes)]

[  **FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) メソッドの [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) クラスは、Windows によって認識される多くの異なる種類のデバイスを列挙するのに使われます。 メソッドで MIDI 入力デバイスだけを検索するよう指定するには、[**MidiInPort.GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.getdeviceselector) によって返されるセレクター文字列を使います。 **FindAllAsync** は、システムに登録されている各 MIDI 入力デバイスの **DeviceInformation** が格納された [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) を返します。 返されたコレクションに項目が含まれていない場合、利用可能な MIDI 入力デバイスはありません。 コレクションに項目が含まれる場合は、**DeviceInformation** オブジェクトのループ処理を行い、各デバイスの名前を MIDI 入力デバイスの **ListBox** に追加します。

[!code-cs[EnumerateMidiInputDevices](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetEnumerateMidiInputDevices)]

MIDI 出力デバイスの列挙も入力デバイスの列挙とまったく同じように動作しますが、**FindAllAsync** を呼び出すときに、[**MidiOutPort.GetDeviceSelector**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midioutport.getdeviceselector) によって返されるセレクター文字列を指定する必要があります。

[!code-cs[EnumerateMidiOutputDevices](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetEnumerateMidiOutputDevices)]



## <a name="create-a-device-watcher-helper-class"></a>デバイス ウォッチャーのヘルパー クラスを作成する

[  **Windows.Devices.Enumeration**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration) 名前空間の [**DeviceWatcher**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) は、システムにデバイスが追加されるか削除された場合、またはデバイスの情報が更新された場合に、アプリに通知を送信できます。 MIDI 対応アプリでは通常、入力デバイスと出力デバイスの両方に関心があるため、この例では、**DeviceWatcher** パターンを実装するヘルパー クラスを作成して、同じコードを複製することなく MIDI 入力デバイスと MIDI 出力デバイスの両方に使えるようにします。

デバイス ウォッチャーとして機能する新しいクラスをプロジェクトに追加します。 この例では、クラスの名前は **MyMidiDeviceWatcher** です。 このセクションのコードの残りの部分は、ヘルパー クラスの実装に使われます。

クラスにいくつかのメンバー変数を追加します。

-   デバイスの変更を監視する [**DeviceWatcher**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) オブジェクト。
-   1 つのインスタンスには MIDI 入力ポートのセレクター文字列、もう 1 つのインスタンスには MIDI 出力ポートのセレクター文字列が格納される、デバイス セレクター文字列。
-   利用可能なデバイスの名前が格納される [**ListBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListBox) コントロール。
-   UI スレッド以外のスレッドから UI を更新するために必要な [**CoreDispatcher**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreDispatcher)。

[!code-cs[WatcherVariables](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherVariables)]

ヘルパー クラスの外部からのデバイスの現在の一覧にアクセスするために使用される [**DeviceInformationCollection**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) プロパティを追加します。

[!code-cs[DeclareDeviceInformationCollection](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetDeclareDeviceInformationCollection)]

クラスのコンストラクターで、呼び出し元は MIDI デバイスのセレクター文字列、デバイスの一覧を表示する **ListBox**、および UI の更新に必要な **Dispatcher** を渡します。

MIDI デバイスのセレクター文字列を渡して [**DeviceInformation.CreateWatcher**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.createwatcher) を呼び出し、**DeviceWatcher** クラスの新しいインスタンスを作成します。

ウォッチャーのイベント ハンドラーに対してハンドラーを登録します。

[!code-cs[WatcherConstructor](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherConstructor)]

**DeviceWatcher** には次のイベントがあります。

-   [**追加**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.added) -新しいデバイスがシステムに追加されたときに発生します。
-   [**削除**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.removed) -デバイスがシステムから削除されるときに発生します。
-   [**更新**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.updated) -既存のデバイスに関連付けられている情報が更新されたときに発生します。
-   [**EnumerationCompleted** ](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) -ウォッチャーには、要求されたデバイスの種類の列挙が完了したときに発生します。

これらの各イベントのイベント ハンドラーで、ヘルパー メソッド **UpdateDevices** が呼び出され、現在のデバイスの一覧で **ListBox** が更新されます。 **UpdateDevices** は UI 要素を更新し、これらのイベント ハンドラーは UI スレッドでは呼び出されないため、各呼び出しを [**RunAsync**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.windows) の呼び出しにラップすることで、指定したコードが UI スレッドで実行されるようにする必要があります。

[!code-cs[WatcherEventHandlers](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherEventHandlers)]

**UpdateDevices** ヘルパー メソッドは、[**DeviceInformation.FindAllAsync**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) を呼び出し、この記事の前半で説明したように、返されたデバイスの名前で **ListBox** を更新します。

[!code-cs[WatcherUpdateDevices](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherUpdateDevices)]

**DeviceWatcher** オブジェクトの [**Start**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.start) メソッドを使って、ウォッチャーを起動するメソッドを追加し、[**Stop**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.stop) メソッドを使ってウォッチャーを停止するメソッドを追加します。

[!code-cs[WatcherStopStart](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherStopStart)]

ウォッチャーのイベント ハンドラーの登録を解除し、デバイス ウォッチャーを null に設定する、デストラクターを用意します。

[!code-cs[WatcherDestructor](./code/MIDIWin10/cs/MyMidiDeviceWatcher.cs#SnippetWatcherDestructor)]

## <a name="create-midi-ports-to-send-and-receive-messages"></a>メッセージを送受信する MIDI ポートを作成する

ページの分離コードで、**MyMidiDeviceWatcher** ヘルパー クラスの 2 つのインスタンスを保持するメンバー変数を宣言します。1 つは入力デバイス用、もう 1 つは出力デバイス用です。

[!code-cs[DeclareDeviceWatchers](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetDeclareDeviceWatchers)]

ウォッチャー ヘルパー クラスの新しいインスタンスを作成し、デバイスのセレクター文字列、格納する **ListBox**、およびページの **Dispatcher** プロパティでアクセスできる **CoreDispatcher** オブジェクトを渡します。 次に、各オブジェクトの **DeviceWatcher** を起動するメソッドを呼び出します。

各 **DeviceWatcher** は起動するとすぐに、現在システムに接続されているデバイスの列挙を完了し、[**EnumerationCompleted**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) イベントを発生させます。これにより、各 **ListBox** が現在の MIDI デバイスで更新されます。

[!code-cs[StartWatchers](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetStartWatchers)]

ユーザーが MIDI 入力 **ListBox** の項目を選択すると、[**SelectionChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) イベントが発生します。 このイベントのハンドラーで、ヘルパー クラスの **DeviceInformationCollection** プロパティにアクセスして、デバイスの現在の一覧を取得します。 一覧にエントリが含まれている場合は、**ListBox** コントロールの [**SelectedIndex**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectedindex) に対応するインデックスを持つ **DeviceInformation** オブジェクトを選択します。

選択したデバイスの [**Id**](https://docs.microsoft.com/uwp/api/windows.devices.enumeration.deviceinformation.id) プロパティを渡して [**MidiInPort.FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.fromidasync) を呼び出すことにより、選択した入力デバイスを表す [**MidiInPort**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiInPort) オブジェクトを作成します。

指定されたデバイスで MIDI メッセージが受信されるたびに発生する [**MessageReceived**](https://docs.microsoft.com/uwp/api/windows.devices.midi.midiinport.messagereceived) イベントのハンドラーを登録します。

[!code-cs[DeclareMidiPorts](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetDeclareMidiPorts)]

[!code-cs[InPortSelectionChanged](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetInPortSelectionChanged)]

**MessageReceived** ハンドラーが呼び出されると、**MidiMessageReceivedEventArgs** の [**Message**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiMessageReceivedEventArgs) プロパティにメッセージが格納されます。 メッセージ オブジェクトの [**Type**](https://docs.microsoft.com/uwp/api/windows.devices.midi.imidimessage.type) は、受信したメッセージの種類を示す [**MidiMessageType**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiMessageType) 列挙体の値です。 メッセージのデータは、メッセージの種類によって異なります。 この例では、メッセージがノートオン メッセージであるかどうかを確認し、そうである場合は、メッセージの MIDI チャネル、ノート、およびベロシティを出力します。

[!code-cs[MessageReceived](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetMessageReceived)]

出力デバイス **ListBox** の [**SelectionChanged**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.selector.selectionchanged) ハンドラーは、入力デバイスのハンドラーと同じように動作しますが、イベント ハンドラーは登録されません。

[!code-cs[OutPortSelectionChanged](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetOutPortSelectionChanged)]

出力デバイスが作成されたら、送信するメッセージの種類に対する新しい [**IMidiMessage**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.IMidiMessage) を作成して、メッセージを送信できます。 この例では、メッセージは [**NoteOnMessage**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.MidiNoteOnMessage) です。 [  **IMidiOutPort**](https://docs.microsoft.com/uwp/api/Windows.Devices.Midi.IMidiOutPort) オブジェクトの [**SendMessage**](https://docs.microsoft.com/uwp/api/windows.devices.midi.imidioutport.sendmessage) メソッドが呼び出されて、メッセージを送信します。

[!code-cs[SendMessage](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetSendMessage)]

アプリが非アクティブ化になったときは、必ずアプリのリソースをクリーンアップしてください。 イベント ハンドラーの登録を解除し、MIDI の入力ポート オブジェクトと出力ポート オブジェクトを null に設定します。 デバイス ウォッチャーを停止し、null に設定します。

[!code-cs[CleanUp](./code/MIDIWin10/cs/MainPage.xaml.cs#SnippetCleanUp)]

## <a name="using-the-built-in-windows-general-midi-synth"></a>組み込みの Windows General MIDI シンセサイザーを使用する

上記で説明した手法を使用して MIDI 出力デバイスを列挙すると、アプリは、"Microsoft GS Wavetable Synth" という MIDI デバイスを検出します。 このデバイスは、アプリから使用できる組み込みの General MIDI シンセサイザーです。 ただし、組み込みのシンセサイザーの SDK 拡張機能をプロジェクトに含めていない限り、このデバイスへの MIDI アウトポートを作成しようとすると失敗します。

**汎用 MIDI シンセサイザー SDK 拡張機能をアプリ プロジェクトに含める**

1.  **ソリューション エクスプローラー**で、プロジェクトの下にある **[参照設定]** を右クリックし、 **[参照の追加]** を選択します。
2.  **[Universal Windows]** ノードを展開します。
3.  **[拡張機能]** を選択します。
4.  拡張機能の一覧から **[Microsoft General MIDI DLS for Universal Windows Apps]** を選択します。
    > [!NOTE] 
    > 複数のバージョンの拡張機能がある場合、アプリのターゲットと一致するバージョンを選んでください。 プロジェクトのプロパティの **[アプリケーション]** タブで、アプリがターゲットとしている SDK バージョンを確認できます。

 

 




