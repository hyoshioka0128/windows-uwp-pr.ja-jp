---
Description: Windows Ink をサポートしている UWP アプリでは、インク ストロークを Ink Serialized Format (ISF) ファイルにシリアル化および逆シリアル化することができます。 ISF ファイルは、すべてのインク ストロークのプロパティと動作に関する追加のメタデータを含む GIF 画像です。 インク対応ではないアプリでは、アルファ チャンネルの背景色の透明度を含めて、静的な GIF 画像を表示できます。
title: Windows Ink ストローク データの保存と取得
ms.assetid: C96C9D2F-DB69-4883-9809-4A0DF7CEC506
label: Store and retrieve Windows Ink stroke data
template: detail.hbs
keywords: Windows Ink, Windows の手書き入力, DirectInk, InkPresenter, InkCanvas, ISF, Ink Serialized Format, ユーザー操作, 入力
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 7eb7f085c5e4daa46cfa6c256ec3938be3c13d82
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365346"
---
# <a name="store-and-retrieve-windows-ink-stroke-data"></a><span data-ttu-id="8fab6-106">Windows Ink ストローク データの保存と取得</span><span class="sxs-lookup"><span data-stu-id="8fab6-106">Store and retrieve Windows Ink stroke data</span></span>


<span data-ttu-id="8fab6-107">Windows Ink をサポートしている UWP アプリでは、インク ストロークを Ink Serialized Format (ISF) ファイルにシリアル化および逆シリアル化することができます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-107">UWP apps that support Windows Ink can serialize and deserialize ink strokes to an Ink Serialized Format (ISF) file.</span></span> <span data-ttu-id="8fab6-108">ISF ファイルは、すべてのインク ストロークのプロパティと動作に関する追加のメタデータを含む GIF 画像です。</span><span class="sxs-lookup"><span data-stu-id="8fab6-108">The ISF file is a GIF image with additional metadata for all ink stroke properties and behaviors.</span></span> <span data-ttu-id="8fab6-109">インク対応ではないアプリでは、アルファ チャンネルの背景色の透明度を含めて、静的な GIF 画像を表示できます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-109">Apps that are not ink-enabled, can view the static GIF image, including alpha-channel background transparency.</span></span>

> [!NOTE]
> <span data-ttu-id="8fab6-110">ISF は、最もコンパクトなインクの永続表現です。</span><span class="sxs-lookup"><span data-stu-id="8fab6-110">ISF is the most compact persistent representation of ink.</span></span> <span data-ttu-id="8fab6-111">バイナリ ドキュメント形式 (GIF ファイルなど) に埋め込むことも、クリップボードに直接配置することもできます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-111">It can be embedded within a binary document format, such as a GIF file, or placed directly on the Clipboard.</span></span>

> <span data-ttu-id="8fab6-112">**重要な API**:[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)、 [ **Windows.UI.Input.Inking**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking)</span><span class="sxs-lookup"><span data-stu-id="8fab6-112">**Important APIs**: [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas), [**Windows.UI.Input.Inking**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking)</span></span>

## <a name="save-ink-strokes-to-a-file"></a><span data-ttu-id="8fab6-113">インク ストロークをファイルに保存する</span><span class="sxs-lookup"><span data-stu-id="8fab6-113">Save ink strokes to a file</span></span>

<span data-ttu-id="8fab6-114">ここでは、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールに描画されたインク ストロークの保存方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-114">Here, we demonstrate how to save ink strokes drawn on an [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control.</span></span>

<span data-ttu-id="8fab6-115">**このサンプルをからダウンロード[を保存し、インク ストロークを形式 ISF (Ink Serialized) ファイルから読み込む](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store.zip)**</span><span class="sxs-lookup"><span data-stu-id="8fab6-115">**Download this sample from [Save and load ink strokes from an Ink Serialized Format (ISF) file](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store.zip)**</span></span>

1.  <span data-ttu-id="8fab6-116">まず、UI を設定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-116">First, we set up the UI.</span></span>

    <span data-ttu-id="8fab6-117">UI には [Save]、[Load]、[Clear] の各ボタンと、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-117">The UI includes "Save", "Load", and "Clear" buttons, and the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas).</span></span>
```    XAML
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
        <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
            <TextBlock x:Name="Header" 
                       Text="Basic ink store sample" 
                       Style="{ThemeResource HeaderTextBlockStyle}" 
                       Margin="10,0,0,0" />
            <Button x:Name="btnSave" 
                    Content="Save" 
                    Margin="50,0,10,0"/>
            <Button x:Name="btnLoad" 
                    Content="Load" 
                    Margin="50,0,10,0"/>
            <Button x:Name="btnClear" 
                    Content="Clear" 
                    Margin="50,0,10,0"/>
        </StackPanel>
        <Grid Grid.Row="1">
            <InkCanvas x:Name="inkCanvas" />
        </Grid>
    </Grid>
```

2.  <span data-ttu-id="8fab6-118">次に、基本的なインク入力の動作をいくつか設定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-118">We then set some basic ink input behaviors.</span></span>

    <span data-ttu-id="8fab6-119">[  **InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) は、ペンとマウスのいずれからの入力データもインク ストローク ([**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputdevicetypes)) として解釈するように構成します。各ボタンのイベントに対するリスナーも宣言します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-119">The [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) is configured to interpret input data from both pen and mouse as ink strokes ([**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputdevicetypes)), and listeners for the click events on the buttons are declared.</span></span>
```csharp
public MainPage()
    {
        this.InitializeComponent();

        // Set supported inking device types.
        inkCanvas.InkPresenter.InputDeviceTypes =
            Windows.UI.Core.CoreInputDeviceTypes.Mouse |
            Windows.UI.Core.CoreInputDeviceTypes.Pen;

        // Listen for button click to initiate save.
        btnSave.Click += btnSave_Click;
        // Listen for button click to initiate load.
        btnLoad.Click += btnLoad_Click;
        // Listen for button click to clear ink canvas.
        btnClear.Click += btnClear_Click;
    }
```

3.  <span data-ttu-id="8fab6-120">最後に、 **[Save]** ボタンのクリック イベント ハンドラーで、インクを保存します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-120">Finally, we save the ink in the click event handler of the **Save** button.</span></span>

    <span data-ttu-id="8fab6-121">[  **FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) を使用すると、インク データの保存先としてファイルと場所の両方をユーザーが選択できます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-121">A [**FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) lets the user select both the file and the location where the ink data is saved.</span></span>

    <span data-ttu-id="8fab6-122">ファイルが選択されたら、[**ReadWrite**](https://docs.microsoft.com/uwp/api/Windows.Storage.FileAccessMode) に設定された [**IRandomAccessStream**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.IRandomAccessStream) ストリームを開きます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-122">Once a file is selected, we open an [**IRandomAccessStream**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.IRandomAccessStream) stream set to [**ReadWrite**](https://docs.microsoft.com/uwp/api/Windows.Storage.FileAccessMode).</span></span>

    <span data-ttu-id="8fab6-123">次に [**SaveAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.iinkstrokecontainer.saveasync) を呼び出して、[**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) によって管理されているインク ストロークをストリームにシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-123">We then call [**SaveAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.iinkstrokecontainer.saveasync) to serialize the ink strokes managed by the [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) to the stream.</span></span>

```csharp
// Save ink data to a file.
    private async void btnSave_Click(object sender, RoutedEventArgs e)
    {
        // Get all strokes on the InkCanvas.
        IReadOnlyList<InkStroke> currentStrokes = inkCanvas.InkPresenter.StrokeContainer.GetStrokes();

        // Strokes present on ink canvas.
        if (currentStrokes.Count > 0)
        {
            // Let users choose their ink file using a file picker.
            // Initialize the picker.
            Windows.Storage.Pickers.FileSavePicker savePicker = 
                new Windows.Storage.Pickers.FileSavePicker();
            savePicker.SuggestedStartLocation = 
                Windows.Storage.Pickers.PickerLocationId.DocumentsLibrary;
            savePicker.FileTypeChoices.Add(
                "GIF with embedded ISF", 
                new List<string>() { ".gif" });
            savePicker.DefaultFileExtension = ".gif";
            savePicker.SuggestedFileName = "InkSample";

            // Show the file picker.
            Windows.Storage.StorageFile file = 
                await savePicker.PickSaveFileAsync();
            // When chosen, picker returns a reference to the selected file.
            if (file != null)
            {
                // Prevent updates to the file until updates are 
                // finalized with call to CompleteUpdatesAsync.
                Windows.Storage.CachedFileManager.DeferUpdates(file);
                // Open a file stream for writing.
                IRandomAccessStream stream = await file.OpenAsync(Windows.Storage.FileAccessMode.ReadWrite);
                // Write the ink strokes to the output stream.
                using (IOutputStream outputStream = stream.GetOutputStreamAt(0))
                {
                    await inkCanvas.InkPresenter.StrokeContainer.SaveAsync(outputStream);
                    await outputStream.FlushAsync();
                }
                stream.Dispose();

                // Finalize write so other apps can update file.
                Windows.Storage.Provider.FileUpdateStatus status =
                    await Windows.Storage.CachedFileManager.CompleteUpdatesAsync(file);

                if (status == Windows.Storage.Provider.FileUpdateStatus.Complete)
                {
                    // File saved.
                }
                else
                {
                    // File couldn't be saved.
                }
            }
            // User selects Cancel and picker returns null.
            else
            {
                // Operation cancelled.
            }
        }
    }
```

> [!NOTE]
> <span data-ttu-id="8fab6-124">インク データの保存用にサポートされるファイル形式は GIF のみです。</span><span class="sxs-lookup"><span data-stu-id="8fab6-124">GIF is the only file format supported for saving ink data.</span></span> <span data-ttu-id="8fab6-125">ただし、[**LoadAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkmanager.loadasync) メソッド (次のセクションで説明します) では、下位互換性のためにその他の形式もサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-125">However, the [**LoadAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkmanager.loadasync) method (demonstrated in the next section) does support additional formats for backward compatibility.</span></span>

## <a name="load-ink-strokes-from-a-file"></a><span data-ttu-id="8fab6-126">インク ストロークをファイルから読み込む</span><span class="sxs-lookup"><span data-stu-id="8fab6-126">Load ink strokes from a file</span></span>

<span data-ttu-id="8fab6-127">ここでは、ファイルからインク ストロークを読み込んで [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールにレンダリングする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-127">Here, we demonstrate how to load ink strokes from a file and render them on an [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control.</span></span>

<span data-ttu-id="8fab6-128">**このサンプルをからダウンロード[を保存し、インク ストロークを形式 ISF (Ink Serialized) ファイルから読み込む](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store.zip)**</span><span class="sxs-lookup"><span data-stu-id="8fab6-128">**Download this sample from [Save and load ink strokes from an Ink Serialized Format (ISF) file](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store.zip)**</span></span>

1.  <span data-ttu-id="8fab6-129">まず、UI を設定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-129">First, we set up the UI.</span></span>

    <span data-ttu-id="8fab6-130">UI には [Save]、[Load]、[Clear] の各ボタンと、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-130">The UI includes "Save", "Load", and "Clear" buttons, and the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas).</span></span>
```    XAML
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
        <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
            <TextBlock x:Name="Header" 
                       Text="Basic ink store sample" 
                       Style="{ThemeResource HeaderTextBlockStyle}" 
                       Margin="10,0,0,0" />
            <Button x:Name="btnSave" 
                    Content="Save" 
                    Margin="50,0,10,0"/>
            <Button x:Name="btnLoad" 
                    Content="Load" 
                    Margin="50,0,10,0"/>
            <Button x:Name="btnClear" 
                    Content="Clear" 
                    Margin="50,0,10,0"/>
        </StackPanel>
        <Grid Grid.Row="1">
            <InkCanvas x:Name="inkCanvas" />
        </Grid>
    </Grid>
```

2.  <span data-ttu-id="8fab6-131">次に、基本的なインク入力の動作をいくつか設定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-131">We then set some basic ink input behaviors.</span></span>

    <span data-ttu-id="8fab6-132">[  **InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) は、ペンとマウスのいずれからの入力データもインク ストローク ([**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputdevicetypes)) として解釈するように構成します。各ボタンのイベントに対するリスナーも宣言します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-132">The [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) is configured to interpret input data from both pen and mouse as ink strokes ([**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputdevicetypes)), and listeners for the click events on the buttons are declared.</span></span>
```csharp
public MainPage()
    {
        this.InitializeComponent();

        // Set supported inking device types.
        inkCanvas.InkPresenter.InputDeviceTypes =
            Windows.UI.Core.CoreInputDeviceTypes.Mouse |
            Windows.UI.Core.CoreInputDeviceTypes.Pen;

        // Listen for button click to initiate save.
        btnSave.Click += btnSave_Click;
        // Listen for button click to initiate load.
        btnLoad.Click += btnLoad_Click;
        // Listen for button click to clear ink canvas.
        btnClear.Click += btnClear_Click;
    }
```

3.  <span data-ttu-id="8fab6-133">最後に、 **[Load]** ボタンのクリック イベント ハンドラーで、インクを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-133">Finally, we load the ink in the click event handler of the **Load** button.</span></span>

    <span data-ttu-id="8fab6-134">[  **FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) を使用すると、保存済みインク データを取得するためのファイルと場所の両方をユーザーが選択できます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-134">A [**FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) lets the user select both the file and the location from where to retrieve the saved ink data.</span></span>

    <span data-ttu-id="8fab6-135">ファイルが選択されたら、[**Read**](https://docs.microsoft.com/uwp/api/Windows.Storage.FileAccessMode) に設定された [**IRandomAccessStream**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.IRandomAccessStream) ストリームを開きます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-135">Once a file is selected, we open an [**IRandomAccessStream**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.IRandomAccessStream) stream set to [**Read**](https://docs.microsoft.com/uwp/api/Windows.Storage.FileAccessMode).</span></span>

    <span data-ttu-id="8fab6-136">次に [**LoadAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkmanager.loadasync) を呼び出して、保存済みのインク ストロークの読み取りと逆シリアル化を行い、[**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-136">We then call [**LoadAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkmanager.loadasync) to read, de-serialize, and load the saved ink strokes into the [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer).</span></span> <span data-ttu-id="8fab6-137">ストロークを **InkStrokeContainer** に読み込むと、[**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) は直ちにストロークを [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="8fab6-137">Loading the strokes into the **InkStrokeContainer** causes the [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) to immediately render them to the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas).</span></span>

    > [!NOTE]
    > <span data-ttu-id="8fab6-138">新しいストロークが読み込まれる前には、InkStrokeContainer 内の既存のストロークがすべて消去されます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-138">All existing strokes in the InkStrokeContainer are cleared before new strokes are loaded.</span></span>

``` csharp
// Load ink data from a file.
private async void btnLoad_Click(object sender, RoutedEventArgs e)
{
    // Let users choose their ink file using a file picker.
    // Initialize the picker.
    Windows.Storage.Pickers.FileOpenPicker openPicker =
        new Windows.Storage.Pickers.FileOpenPicker();
    openPicker.SuggestedStartLocation =
        Windows.Storage.Pickers.PickerLocationId.DocumentsLibrary;
    openPicker.FileTypeFilter.Add(".gif");
    // Show the file picker.
    Windows.Storage.StorageFile file = await openPicker.PickSingleFileAsync();
    // User selects a file and picker returns a reference to the selected file.
    if (file != null)
    {
        // Open a file stream for reading.
        IRandomAccessStream stream = await file.OpenAsync(Windows.Storage.FileAccessMode.Read);
        // Read from file.
        using (var inputStream = stream.GetInputStreamAt(0))
        {
            await inkCanvas.InkPresenter.StrokeContainer.LoadAsync(inputStream);
        }
        stream.Dispose();
    }
    // User selects Cancel and picker returns null.
    else
    {
        // Operation cancelled.
    }
}
```

> [!NOTE]
> <span data-ttu-id="8fab6-139">インク データの保存用にサポートされるファイル形式は GIF のみです。</span><span class="sxs-lookup"><span data-stu-id="8fab6-139">GIF is the only file format supported for saving ink data.</span></span> <span data-ttu-id="8fab6-140">ただし、[**LoadAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkmanager.loadasync) メソッドでは、下位互換性のために次の形式もサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-140">However, the [**LoadAsync**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkmanager.loadasync) method does support the following formats for backward compatibility.</span></span>

| <span data-ttu-id="8fab6-141">表記</span><span class="sxs-lookup"><span data-stu-id="8fab6-141">Format</span></span>                    | <span data-ttu-id="8fab6-142">説明</span><span class="sxs-lookup"><span data-stu-id="8fab6-142">Description</span></span> |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8fab6-143">InkSerializedFormat</span><span class="sxs-lookup"><span data-stu-id="8fab6-143">InkSerializedFormat</span></span>       | <span data-ttu-id="8fab6-144">ISF で永続化されたインクを指定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-144">Specifies ink that is persisted using ISF.</span></span> <span data-ttu-id="8fab6-145">これは最もコンパクトなインクの永続表現です。</span><span class="sxs-lookup"><span data-stu-id="8fab6-145">This is the most compact persistent representation of ink.</span></span> <span data-ttu-id="8fab6-146">バイナリ ドキュメント形式への埋め込みまたはクリップボードへの直接配置を実行できます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-146">It can be embedded within a binary document format or placed directly on the Clipboard.</span></span>                                                                                                                                                                                                         |
| <span data-ttu-id="8fab6-147">Base64InkSerializedFormat</span><span class="sxs-lookup"><span data-stu-id="8fab6-147">Base64InkSerializedFormat</span></span> | <span data-ttu-id="8fab6-148">base64 ストリームとして ISF をエンコードすることで永続化されたインクを指定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-148">Specifies ink that is persisted by encoding the ISF as a base64 stream.</span></span> <span data-ttu-id="8fab6-149">この形式を指定すると、インクを XML ファイルや HTML ファイルで直接エンコードできます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-149">This format is provided so ink can be encoded directly in an XML or HTML file.</span></span>                                                                                                                                                                                                                                                |
| <span data-ttu-id="8fab6-150">Gif</span><span class="sxs-lookup"><span data-stu-id="8fab6-150">Gif</span></span>                       | <span data-ttu-id="8fab6-151">ファイル内に ISF がメタデータとして埋め込まれた GIF ファイルで永続化されたインクを指定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-151">Specifies ink that is persisted by using a GIF file that contains ISF as metadata embedded within the file.</span></span> <span data-ttu-id="8fab6-152">この形式では、インクに対応していないアプリケーションでインクを表示でき、インク対応のアプリケーションに返されたときもまったく同じように再現できます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-152">This enables ink to be viewed in applications that are not ink-enabled and maintain its full ink fidelity when it returns to an ink-enabled application.</span></span> <span data-ttu-id="8fab6-153">この形式は、HTML ファイル内のインクのコンテンツを転送して、インク アプリとインク対応でないアプリで使えるようにする場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-153">This format is ideal when transporting ink content within an HTML file and for making it usable by ink and non-ink applications.</span></span> |
| <span data-ttu-id="8fab6-154">Base64Gif</span><span class="sxs-lookup"><span data-stu-id="8fab6-154">Base64Gif</span></span>                 | <span data-ttu-id="8fab6-155">base64 エンコードの拡張 GIF で永続化されたインクを指定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-155">Specifies ink that is persisted by using a base64-encoded fortified GIF.</span></span> <span data-ttu-id="8fab6-156">この形式は、後で画像に変換するために、インクを XML ファイルや HTML ファイルで直接エンコードする場合に指定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-156">This format is provided when ink is to be encoded directly in an XML or HTML file for later conversion into an image.</span></span> <span data-ttu-id="8fab6-157">すべてのインク情報を格納するために生成された XML 形式で、Extensible Stylesheet Language Transformations (XSLT) を介して HTML を生成するために使うことができます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-157">A possible use of this is in an XML format generated to contain all ink information and used to generate HTML through Extensible Stylesheet Language Transformations (XSLT).</span></span> 

## <a name="copy-and-paste-ink-strokes-with-the-clipboard"></a><span data-ttu-id="8fab6-158">クリップボードを使ってインク ストロークのコピーと貼り付けを行う</span><span class="sxs-lookup"><span data-stu-id="8fab6-158">Copy and paste ink strokes with the clipboard</span></span>

<span data-ttu-id="8fab6-159">ここでは、クリップボードを使って、アプリ間でインク ストロークを転送する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-159">Here, we demonstrate how to use the clipboard to transfer ink strokes between apps.</span></span>

<span data-ttu-id="8fab6-160">クリップボード機能をサポートするために、組み込みの [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) の切り取り/コピー コマンドでは、1 つまたは複数のインク ストロークの選択が求められます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-160">To support clipboard functionality, the built-in [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) cut and copy commands require one or more ink strokes be selected.</span></span>

<span data-ttu-id="8fab6-161">次の例では、ペン バレル ボタン (またはマウスの右ボタン) で入力が変更された場合にストロークを選べるようにする手順を示しています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-161">For this example, we enable stroke selection when input is modified with a pen barrel button (or right mouse button).</span></span> <span data-ttu-id="8fab6-162">ストローク選択の実装方法を示す詳しい例については、「[ペン操作とスタイラス操作](pen-and-stylus-interactions.md)」の「高度な処理のための入力のパススルー」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="8fab6-162">For a complete example of how to implement stroke selection, see Pass-through input for advanced processing in [Pen and stylus interactions](pen-and-stylus-interactions.md).</span></span>

<span data-ttu-id="8fab6-163">**このサンプルをからダウンロード[保存し、クリップボードからインク ストロークを読み込む](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store-clipboard.zip)**</span><span class="sxs-lookup"><span data-stu-id="8fab6-163">**Download this sample from [Save and load ink strokes from the clipboard](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store-clipboard.zip)**</span></span>

1.  <span data-ttu-id="8fab6-164">まず、UI を設定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-164">First, we set up the UI.</span></span>

    <span data-ttu-id="8fab6-165">UI には、[Cut]、[Copy]、[Paste]、[Clear] の各ボタン、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)、選択キャンバスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-165">The UI includes "Cut", "Copy", "Paste", and "Clear" buttons, along with the [**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) and a selection canvas.</span></span>
```    XAML
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
        <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
            <TextBlock x:Name="tbHeader" 
                       Text="Basic ink store sample" 
                       Style="{ThemeResource HeaderTextBlockStyle}" 
                       Margin="10,0,0,0" />
            <Button x:Name="btnCut" 
                    Content="Cut" 
                    Margin="20,0,10,0"/>
            <Button x:Name="btnCopy" 
                    Content="Copy" 
                    Margin="20,0,10,0"/>
            <Button x:Name="btnPaste" 
                    Content="Paste" 
                    Margin="20,0,10,0"/>
            <Button x:Name="btnClear" 
                    Content="Clear" 
                    Margin="20,0,10,0"/>
        </StackPanel>
        <Grid x:Name="gridCanvas" Grid.Row="1">
            <!-- Canvas for displaying selection UI. -->
            <Canvas x:Name="selectionCanvas"/>
            <!-- Inking area -->
            <InkCanvas x:Name="inkCanvas"/>
        </Grid>
    </Grid>
```

2.  <span data-ttu-id="8fab6-166">次に、基本的なインク入力の動作をいくつか設定します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-166">We then set some basic ink input behaviors.</span></span>

    <span data-ttu-id="8fab6-167">[  **InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) は、ペンとマウスのいずれからの入力データもインク ストローク ([**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputdevicetypes)) として解釈するように構成します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-167">The [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) is configured to interpret input data from both pen and mouse as ink strokes ([**InputDeviceTypes**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter.inputdevicetypes)).</span></span> <span data-ttu-id="8fab6-168">ここでは、ボタンのクリック イベント、選択機能のポインター イベントおよびストローク イベントに対するリスナーも宣言されています。</span><span class="sxs-lookup"><span data-stu-id="8fab6-168">Listeners for the click events on the buttons as well as pointer and stroke events for selection functionality are also declared here.</span></span>

    <span data-ttu-id="8fab6-169">ストローク選択の実装方法を示す詳しい例については、「[ペン操作とスタイラス操作](pen-and-stylus-interactions.md)」の「高度な処理のための入力のパススルー」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="8fab6-169">For a complete example of how to implement stroke selection, see Pass-through input for advanced processing in [Pen and stylus interactions](pen-and-stylus-interactions.md).</span></span>
```csharp
public MainPage()
    {
        this.InitializeComponent();

        // Set supported inking device types.
        inkCanvas.InkPresenter.InputDeviceTypes =
            Windows.UI.Core.CoreInputDeviceTypes.Mouse |
            Windows.UI.Core.CoreInputDeviceTypes.Pen;

        // Listen for button click to cut ink strokes.
        btnCut.Click += btnCut_Click;
        // Listen for button click to copy ink strokes.
        btnCopy.Click += btnCopy_Click;
        // Listen for button click to paste ink strokes.
        btnPaste.Click += btnPaste_Click;
        // Listen for button click to clear ink canvas.
        btnClear.Click += btnClear_Click;

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

        // Listen for new ink or erase strokes to clean up selection UI.
        inkCanvas.InkPresenter.StrokeInput.StrokeStarted +=
            StrokeInput_StrokeStarted;
        inkCanvas.InkPresenter.StrokesErased +=
            InkPresenter_StrokesErased;
    }
```

3.  <span data-ttu-id="8fab6-170">最後に、ストローク選択サポートを追加した後で、 **[Cut]** ボタン、 **[Copy]** ボタン、 **[Paste]** ボタンのクリック イベント ハンドラーにクリップボード機能を実装します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-170">Finally, after adding stroke selection support, we implement clipboard functionality in the click event handlers of the **Cut**, **Copy**, and **Paste** buttons.</span></span>

    <span data-ttu-id="8fab6-171">切り取りの場合は、まず [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) の [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) で [**CopySelectedToClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.copyselectedtoclipboard) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-171">For cut, we first call [**CopySelectedToClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.copyselectedtoclipboard) on the [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) of the [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter).</span></span>

    <span data-ttu-id="8fab6-172">次に [**DeleteSelected**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.deleteselected) を呼び出して、インク キャンバスからストロークを削除します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-172">We then call [**DeleteSelected**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.deleteselected) to remove the strokes from the ink canvas.</span></span>

    <span data-ttu-id="8fab6-173">最後に、選択キャンバスからすべてのストローク選択を削除します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-173">Finally, we delete all selection strokes from the selection canvas.</span></span>
    
```csharp
private void btnCut_Click(object sender, RoutedEventArgs e)
    {
        inkCanvas.InkPresenter.StrokeContainer.CopySelectedToClipboard();
        inkCanvas.InkPresenter.StrokeContainer.DeleteSelected();
        ClearSelection();
    }
```
```csharp
// Clean up selection UI.
    private void ClearSelection()
    {
        var strokes = inkCanvas.InkPresenter.StrokeContainer.GetStrokes();
        foreach (var stroke in strokes)
        {
            stroke.Selected = false;
        }
        ClearDrawnBoundingRect();
    }

    private void ClearDrawnBoundingRect()
    {
        if (selectionCanvas.Children.Any())
        {
            selectionCanvas.Children.Clear();
            boundingRect = Rect.Empty;
        }
    }
```

<span data-ttu-id="8fab6-174">コピーの場合は、[**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) の [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) で [**CopySelectedToClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.copyselectedtoclipboard) を呼び出すだけです。</span><span class="sxs-lookup"><span data-stu-id="8fab6-174">For copy, we simply call [**CopySelectedToClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.copyselectedtoclipboard) on the [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) of the [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter).</span></span>


```csharp
private void btnCopy_Click(object sender, RoutedEventArgs e)
    {
        inkCanvas.InkPresenter.StrokeContainer.CopySelectedToClipboard();
    }
```

<span data-ttu-id="8fab6-175">貼り付けの場合は、クリップボードのコンテンツをインク キャンバスに貼り付けることができるように、[**CanPasteFromClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.canpastefromclipboard) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8fab6-175">For paste, we call [**CanPasteFromClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.canpastefromclipboard) to ensure that the content on the clipboard can be pasted to the ink canvas.</span></span>

<span data-ttu-id="8fab6-176">その場合は、[**PasteFromClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.pastefromclipboard) を呼び出して、クリップボード内のインク ストロークを [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) の [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) に挿入します。これにより、ストロークがインク キャンバスにレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="8fab6-176">If so, we call [**PasteFromClipboard**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstrokecontainer.pastefromclipboard) to insert the clipboard ink strokes into the [**InkStrokeContainer**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkStrokeContainer) of the [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter), which then renders the strokes to the ink canvas.</span></span>

```csharp
private void btnPaste_Click(object sender, RoutedEventArgs e)
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
```

## <a name="related-articles"></a><span data-ttu-id="8fab6-177">関連記事</span><span class="sxs-lookup"><span data-stu-id="8fab6-177">Related articles</span></span>

* [<span data-ttu-id="8fab6-178">ペン操作とスタイラス操作</span><span class="sxs-lookup"><span data-stu-id="8fab6-178">Pen and stylus interactions</span></span>](pen-and-stylus-interactions.md)

<span data-ttu-id="8fab6-179">**トピックのサンプル**</span><span class="sxs-lookup"><span data-stu-id="8fab6-179">**Topic samples**</span></span>
* [<span data-ttu-id="8fab6-180">保存し、インク ストロークを形式 ISF (Ink Serialized) ファイルから読み込む</span><span class="sxs-lookup"><span data-stu-id="8fab6-180">Save and load ink strokes from an Ink Serialized Format (ISF) file</span></span>](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store.zip)
* [<span data-ttu-id="8fab6-181">保存し、クリップボードからインク ストロークを読み込む</span><span class="sxs-lookup"><span data-stu-id="8fab6-181">Save and load ink strokes from the clipboard</span></span>](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store-clipboard.zip)

<span data-ttu-id="8fab6-182">**その他のサンプル**</span><span class="sxs-lookup"><span data-stu-id="8fab6-182">**Other samples**</span></span>
* [<span data-ttu-id="8fab6-183">単純なインクのサンプル (C#/C++)</span><span class="sxs-lookup"><span data-stu-id="8fab6-183">Simple ink sample (C#/C++)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620312)
* [<span data-ttu-id="8fab6-184">複雑なインクのサンプル (C++)</span><span class="sxs-lookup"><span data-stu-id="8fab6-184">Complex ink sample (C++)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620314)
* [<span data-ttu-id="8fab6-185">インクのサンプル (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="8fab6-185">Ink sample (JavaScript)</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=620308)
* [<span data-ttu-id="8fab6-186">チュートリアルを開始します。UWP アプリでのインクをサポートします。</span><span class="sxs-lookup"><span data-stu-id="8fab6-186">Get Started Tutorial: Support ink in your UWP app</span></span>](https://aka.ms/appsample-ink)
* [<span data-ttu-id="8fab6-187">書籍のサンプルを色分け表示</span><span class="sxs-lookup"><span data-stu-id="8fab6-187">Coloring book sample</span></span>](https://aka.ms/cpubsample-coloringbook)
* [<span data-ttu-id="8fab6-188">ファミリのノートのサンプル</span><span class="sxs-lookup"><span data-stu-id="8fab6-188">Family notes sample</span></span>](https://aka.ms/cpubsample-familynotessample)



