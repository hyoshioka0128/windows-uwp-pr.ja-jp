---
title: DirectX ゲームでのリソースの読み込み
description: ほとんどのゲームは、ある時点で、ローカル ストレージまたは他のデータ ストリームからリソースとアセット (シェーダー、テクスチャ、定義済みメッシュ、その他のグラフィックス データなど) を読み込みます。
ms.assetid: e45186fa-57a3-dc70-2b59-408bff0c0b41
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10、UWP、ゲーム、DirectX、リソースの読み込み
ms.localizationpriority: medium
ms.openlocfilehash: ae3d6bb4b7360119e1b6e3b793380c8270b70688
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368547"
---
# <a name="load-resources-in-your-directx-game"></a><span data-ttu-id="0c45c-104">DirectX ゲームでのリソースの読み込み</span><span class="sxs-lookup"><span data-stu-id="0c45c-104">Load resources in your DirectX game</span></span>



<span data-ttu-id="0c45c-105">ほとんどのゲームは、ある時点で、ローカル ストレージまたは他のデータ ストリームからリソースとアセット (シェーダー、テクスチャ、定義済みメッシュ、その他のグラフィックス データなど) を読み込みます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-105">Most games, at some point, load resources and assets (such as shaders, textures, predefined meshes or other graphics data) from local storage or some other data stream.</span></span> <span data-ttu-id="0c45c-106">ここでは、このようなファイルを読み込んで DirectX C/C++ ユニバーサル Windows プラットフォーム (UWP) ゲームで使う際に考慮すべきことについて、その概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-106">Here, we walk you through a high-level view of what you must consider when loading these files to use in your DirectX C/C++ Universal Windows Platform (UWP) game.</span></span>

<span data-ttu-id="0c45c-107">たとえば、ゲームの多角形オブジェクトのメッシュは、別のツールで作成されて特定の形式にエクスポートされている場合があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-107">For example, the meshes for polygonal objects in your game might have been created with another tool, and exported to a specific format.</span></span> <span data-ttu-id="0c45c-108">テクスチャなどについても同じことが言えます。フラットな非圧縮ビットマップは、ほとんどのツールで普通に作成でき、ほとんどのグラフィックス API で理解されますが、ゲームで使うにはきわめて効率が悪い可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-108">The same is true for textures, and more so: while a flat, uncompressed bitmap can be commonly written by most tools and understood by most graphics APIs, it can be extremely inefficient for use in your game.</span></span> <span data-ttu-id="0c45c-109">ここでは、Direct3D で使うために 3 種類のグラフィック リソース (メッシュ (モデル)、テクスチャ (ビットマップ) と、コンパイル済みシェーダーの各オブジェクト) を読み込む基本的なステップについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-109">Here, we guide you through the basic steps for loading three different types of graphic resources for use with Direct3D: meshes (models), textures (bitmaps), and compiled shader objects.</span></span>

## <a name="what-you-need-to-know"></a><span data-ttu-id="0c45c-110">理解しておく必要があること</span><span class="sxs-lookup"><span data-stu-id="0c45c-110">What you need to know</span></span>


### <a name="technologies"></a><span data-ttu-id="0c45c-111">テクノロジ</span><span class="sxs-lookup"><span data-stu-id="0c45c-111">Technologies</span></span>

-   <span data-ttu-id="0c45c-112">並列パターン ライブラリ (ppltasks.h)</span><span class="sxs-lookup"><span data-stu-id="0c45c-112">Parallel Patterns Library (ppltasks.h)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0c45c-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="0c45c-113">Prerequisites</span></span>

-   <span data-ttu-id="0c45c-114">基本的な Windows ランタイムを理解している。</span><span class="sxs-lookup"><span data-stu-id="0c45c-114">Understand the basic Windows Runtime</span></span>
-   <span data-ttu-id="0c45c-115">非同期タスクを理解している。</span><span class="sxs-lookup"><span data-stu-id="0c45c-115">Understand asynchronous tasks</span></span>
-   <span data-ttu-id="0c45c-116">3-D グラフィックス プログラミングの基本概念を理解している。</span><span class="sxs-lookup"><span data-stu-id="0c45c-116">Understand the basic concepts of 3-D graphics programming.</span></span>

<span data-ttu-id="0c45c-117">また、このサンプルには、リソースの読み込みと管理のためのコード ファイルが 3 つ含まれています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-117">This sample also includes three code files for resource loading and management.</span></span> <span data-ttu-id="0c45c-118">このトピックでは、これらのファイルに定義されているコード オブジェクトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-118">You'll encounter the code objects defined in these files throughout this topic.</span></span>

-   <span data-ttu-id="0c45c-119">BasicLoader.h/.cpp</span><span class="sxs-lookup"><span data-stu-id="0c45c-119">BasicLoader.h/.cpp</span></span>
-   <span data-ttu-id="0c45c-120">BasicReaderWriter.h/.cpp</span><span class="sxs-lookup"><span data-stu-id="0c45c-120">BasicReaderWriter.h/.cpp</span></span>
-   <span data-ttu-id="0c45c-121">DDSTextureLoader.h/.cpp</span><span class="sxs-lookup"><span data-stu-id="0c45c-121">DDSTextureLoader.h/.cpp</span></span>

<span data-ttu-id="0c45c-122">これらのサンプルのコード一式については、次のリンク先をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-122">The complete code for these samples can be found in the following links.</span></span>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="0c45c-123">トピック</span><span class="sxs-lookup"><span data-stu-id="0c45c-123">Topic</span></span></th>
<th align="left"><span data-ttu-id="0c45c-124">説明</span><span class="sxs-lookup"><span data-stu-id="0c45c-124">Description</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span data-ttu-id="0c45c-125"><a href="complete-code-for-basicloader.md">BasicLoader の完全なコード</a></span><span class="sxs-lookup"><span data-stu-id="0c45c-125"><a href="complete-code-for-basicloader.md">Complete code for BasicLoader</a></span></span></p></td>
<td align="left"><p><span data-ttu-id="0c45c-126">グラフィックス メッシュ オブジェクトを変換してメモリに読み込むクラスとメソッドのコード一式です。</span><span class="sxs-lookup"><span data-stu-id="0c45c-126">Complete code for a class and methods that convert and load graphics mesh objects into memory.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="0c45c-127"><a href="complete-code-for-basicreaderwriter.md">BasicReaderWriter の完全なコード</a></span><span class="sxs-lookup"><span data-stu-id="0c45c-127"><a href="complete-code-for-basicreaderwriter.md">Complete code for BasicReaderWriter</a></span></span></p></td>
<td align="left"><p><span data-ttu-id="0c45c-128">バイナリ データ ファイル全般の読み書きを行うクラスとメソッドのコード一式です。</span><span class="sxs-lookup"><span data-stu-id="0c45c-128">Complete code for a class and methods for reading and writing binary data files in general.</span></span> <span data-ttu-id="0c45c-129"><a href="complete-code-for-basicloader.md">BasicLoader</a> クラスで使われます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-129">Used by the <a href="complete-code-for-basicloader.md">BasicLoader</a> class.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="0c45c-130"><a href="complete-code-for-ddstextureloader.md">DDSTextureLoader の完全なコード</a></span><span class="sxs-lookup"><span data-stu-id="0c45c-130"><a href="complete-code-for-ddstextureloader.md">Complete code for DDSTextureLoader</a></span></span></p></td>
<td align="left"><p><span data-ttu-id="0c45c-131">メモリから DDS テクスチャを読み込むクラスとメソッドのコード一式です。</span><span class="sxs-lookup"><span data-stu-id="0c45c-131">Complete code for a class and method that loads a DDS texture from memory.</span></span></p></td>
</tr>
</tbody>
</table>

 

## <a name="instructions"></a><span data-ttu-id="0c45c-132">手順</span><span class="sxs-lookup"><span data-stu-id="0c45c-132">Instructions</span></span>

### <a name="asynchronous-loading"></a><span data-ttu-id="0c45c-133">非同期読み込み</span><span class="sxs-lookup"><span data-stu-id="0c45c-133">Asynchronous loading</span></span>

<span data-ttu-id="0c45c-134">非同期読み込みは、並列パターン ライブラリ (PPL) の **task** テンプレートを使って処理します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-134">Asynchronous loading is handled using the **task** template from the Parallel Patterns Library (PPL).</span></span> <span data-ttu-id="0c45c-135">**task** にはメソッド呼び出しが含まれています。その後に、非同期呼び出しの完了後にその結果を処理するラムダが続きます。通常の形式は次のとおりです: </span><span class="sxs-lookup"><span data-stu-id="0c45c-135">A **task** contains a method call followed by a lambda that processes the results of the async call after it completes, and usually follows the format of:</span></span>

<span data-ttu-id="0c45c-136">`task<generic return type>(async code to execute).then((parameters for lambda){ lambda code contents });` の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-136">`task<generic return type>(async code to execute).then((parameters for lambda){ lambda code contents });`.</span></span>

<span data-ttu-id="0c45c-137">タスクは、 **.then()** 構文を使って連結できます。したがって、ある操作の完了後、その操作の結果に依存する別の非同期操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-137">Tasks can be chained together using the **.then()** syntax, so that when one operation completes, another async operation that depends on the results of the prior operation can be run.</span></span> <span data-ttu-id="0c45c-138">このように、プレイヤーにはほぼ見えない方法で、個別のスレッドで複雑なアセットの読み込み、変換、管理を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-138">In this way, you can load, convert, and manage complex assets on separate threads in a way that appears almost invisible to the player.</span></span>

<span data-ttu-id="0c45c-139">詳しくは、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-139">For more details, read [Asynchronous programming in C++](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps).</span></span>

<span data-ttu-id="0c45c-140">それでは、非同期ファイル読み込みメソッド **ReadDataAsync** の宣言と作成の基本構造を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="0c45c-140">Now, let's look at the basic structure for declaring and creating an async file loading method, **ReadDataAsync**.</span></span>

```cpp
#include <ppltasks.h>

// ...
concurrency::task<Platform::Array<byte>^> ReadDataAsync(
        _In_ Platform::String^ filename);

// ...

using concurrency;

task<Platform::Array<byte>^> BasicReaderWriter::ReadDataAsync(
    _In_ Platform::String^ filename
    )
{
    return task<StorageFile^>(m_location->GetFileAsync(filename)).then([=](StorageFile^ file)
    {
        return FileIO::ReadBufferAsync(file);
    }).then([=](IBuffer^ buffer)
    {
        auto fileData = ref new Platform::Array<byte>(buffer->Length);
        DataReader::FromBuffer(buffer)->ReadBytes(fileData);
        return fileData;
    });
}
```

<span data-ttu-id="0c45c-141">このコードでは、上で定義された **ReadDataAsync** メソッドを呼び出すと、ファイル システムのバッファーを読み取るタスクが作成されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-141">In this code, when your code calls the **ReadDataAsync** method defined above, a task is created to read a buffer from the file system.</span></span> <span data-ttu-id="0c45c-142">このタスクが完了すると、連結されたタスクがバッファーを受け取り、静的な [**DataReader**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader) 型を使ってバッファーから配列にバイトをストリームします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-142">Once it completes, a chained task takes the buffer and streams the bytes from that buffer into an array using the static [**DataReader**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader) type.</span></span>

```cpp
m_basicReaderWriter = ref new BasicReaderWriter();

// ...
return m_basicReaderWriter->ReadDataAsync(filename).then([=](const Platform::Array<byte>^ bytecode)
    {
      // Perform some operation with the data when the async load completes.          
    });
```

<span data-ttu-id="0c45c-143">**ReadDataAsync** の呼び出しはこのとおりです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-143">Here's the call you make to **ReadDataAsync**.</span></span> <span data-ttu-id="0c45c-144">これが完了すると、提供されたファイルから読み取ったバイトの配列が渡されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-144">When it completes, your code receives an array of bytes read from the provided file.</span></span> <span data-ttu-id="0c45c-145">**ReadDataAsync** 自体はタスクとして定義されているため、バイト配列が返されたときにラムダを使って特定の操作 (対応可能な DirectX 関数にバイト データを渡すなど) を実行することができます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-145">Since **ReadDataAsync** itself is defined as a task, you can use a lambda to perform a specific operation when the byte array is returned, such as passing that byte data to a DirectX function that can use it.</span></span>

<span data-ttu-id="0c45c-146">非常にシンプルなゲームの場合は、ユーザーがゲームを開始したときに、このようなメソッドを使ってリソースを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-146">If your game is sufficiently simple, load your resources with a method like this when the user starts the game.</span></span> <span data-ttu-id="0c45c-147">これを実行できるのは、[**IFrameworkView::Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run) 実装の呼び出しシーケンスにおけるあるポイントからメインのゲーム ループを開始する前です。</span><span class="sxs-lookup"><span data-stu-id="0c45c-147">You can do this before you start the main game loop from some point in the call sequence of your [**IFrameworkView::Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run) implementation.</span></span> <span data-ttu-id="0c45c-148">ゲームを速く開始できるように、またプレイヤーが初期段階の対話式操作を行う前に読み込みが完了するまで待機することがないように、もう一度、非同期的にリソース読み込みメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-148">Again, you call your resource loading methods asynchronously so the game can start quicker and so the player doesn't have to wait until the loading completes before engaging in early interactions.</span></span>

<span data-ttu-id="0c45c-149">しかし、すべての非同期読み込みが完了するまではゲーム本体を開始したくありません。</span><span class="sxs-lookup"><span data-stu-id="0c45c-149">However, you don't want to start the game proper until all of the async loading has completed!</span></span> <span data-ttu-id="0c45c-150">そこで、読み込みが完了したら通知するメソッド (特定のフィールドなど) を作成し、読み込みメソッドでラムダを使って、完了時に通知を設定します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-150">Create some method for signaling when loading is complete, such as a specific field, and use the lambdas on your loading method(s) to set that signal when finished.</span></span> <span data-ttu-id="0c45c-151">この読み込まれたリソースを使うコンポーネントを開始する前に、変数を確認します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-151">Check the variable before starting any components that use those loaded resources.</span></span>

<span data-ttu-id="0c45c-152">次に示すのは、BasicLoader.cpp に定義された非同期メソッドを使って、ゲーム起動時にシェーダー、メッシュ、テクスチャを読み込む例です。</span><span class="sxs-lookup"><span data-stu-id="0c45c-152">Here's an example using the async methods defined in BasicLoader.cpp to load shaders, a mesh, and a texture when the game starts up.</span></span> <span data-ttu-id="0c45c-153">ゲームのオブジェクトで、特定のフィールドを設定したことを確認**m\_loadingComplete**、すべての読み込みメソッドが完了します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-153">Notice that it sets a specific field on the game object, **m\_loadingComplete**, when all of the loading methods finish.</span></span>

```cpp
void ResourceLoading::CreateDeviceResources()
{
    // DirectXBase is a common sample class that implements a basic view provider. 
    
    DirectXBase::CreateDeviceResources(); 

    // ...

    // This flag will keep track of whether or not all application
    // resources have been loaded.  Until all resources are loaded,
    // only the sample overlay will be drawn on the screen.
    m_loadingComplete = false;

    // Create a BasicLoader, and use it to asynchronously load all
    // application resources.  When an output value becomes non-null,
    // this indicates that the asynchronous operation has completed.
    BasicLoader^ loader = ref new BasicLoader(m_d3dDevice.Get());

    auto loadVertexShaderTask = loader->LoadShaderAsync(
        "SimpleVertexShader.cso",
        nullptr,
        0,
        &m_vertexShader,
        &m_inputLayout
        );

    auto loadPixelShaderTask = loader->LoadShaderAsync(
        "SimplePixelShader.cso",
        &m_pixelShader
        );

    auto loadTextureTask = loader->LoadTextureAsync(
        "reftexture.dds",
        nullptr,
        &m_textureSRV
        );

    auto loadMeshTask = loader->LoadMeshAsync(
        "refmesh.vbo",
        &m_vertexBuffer,
        &m_indexBuffer,
        nullptr,
        &m_indexCount
        );

    // The && operator can be used to create a single task that represents
    // a group of multiple tasks. The new task's completed handler will only
    // be called once all associated tasks have completed. In this case, the
    // new task represents a task to load various assets from the package.
    (loadVertexShaderTask && loadPixelShaderTask && loadTextureTask && loadMeshTask).then([=]()
    {
        m_loadingComplete = true;
    });

    // Create constant buffers and other graphics device-specific resources here.
}
```

<span data-ttu-id="0c45c-154">すべてのタスクが完了したときにのみ、読み込み完了フラグを設定するラムダがトリガーされるように、&& 演算子を使ってタスクが統合されている点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-154">Note that the tasks have been aggregated using the && operator such that the lambda that sets the loading complete flag is triggered only when all of the tasks complete.</span></span> <span data-ttu-id="0c45c-155">複数のフラグが存在する場合は、競合状態になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-155">Note that if you have multiple flags, you have the possibility of race conditions.</span></span> <span data-ttu-id="0c45c-156">たとえば、ラムダが 2 つのフラグを順次同じ値に設定するとします。2 つ目のフラグが設定される前に別のスレッドがフラグを確認した場合、別のスレッドは 1 つ目のフラグの設定しか認識しません。</span><span class="sxs-lookup"><span data-stu-id="0c45c-156">For example, if the lambda sets two flags sequentially to the same value, another thread may only see the first flag set if it examines them before the second flag is set.</span></span>

<span data-ttu-id="0c45c-157">これまでは、リソース ファイルを非同期的に読み込む方法について確認してきました。</span><span class="sxs-lookup"><span data-stu-id="0c45c-157">You've seen how to load resource files asynchronously.</span></span> <span data-ttu-id="0c45c-158">同期ファイルの読み込みはもっと簡単です。この読み込みの例については、「[BasicReaderWriter のコード一式](complete-code-for-basicreaderwriter.md)」と「[BasicLoader のコード一式](complete-code-for-basicloader.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-158">Synchronous file loads are much simpler, and you can find examples of them in [Complete code for BasicReaderWriter](complete-code-for-basicreaderwriter.md) and [Complete code for BasicLoader](complete-code-for-basicloader.md).</span></span>

<span data-ttu-id="0c45c-159">言うまでもなく、リソースやアセットの種類が異なれば、ほとんどの場合、グラフィックス パイプラインで使う前に追加の処理または変換が必要になります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-159">Of course, different resource and asset types often require additional processing or conversion before they are ready to be used in your graphics pipeline.</span></span> <span data-ttu-id="0c45c-160">次に、3 種類のリソース (メッシュ、テクスチャ、シェーダー) について見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="0c45c-160">Let's take a look at three specific types of resources: meshes, textures, and shaders.</span></span>

### <a name="loading-meshes"></a><span data-ttu-id="0c45c-161">メッシュの読み込み</span><span class="sxs-lookup"><span data-stu-id="0c45c-161">Loading meshes</span></span>

<span data-ttu-id="0c45c-162">メッシュは頂点データです。ゲーム内のコードによって手続き的に生成されるか、他のアプリ (3DStudio MAX や Alias WaveFront など) またはツールからファイルにエクスポートされます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-162">Meshes are vertex data, either generated procedurally by code within your game or exported to a file from another app (like 3DStudio MAX or Alias WaveFront) or tool.</span></span> <span data-ttu-id="0c45c-163">これらのメッシュは、立方体や球体のようなシンプルなプリミティブから自動車、家、人物に及ぶ、ゲーム内のモデルを表します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-163">These meshes represent the models in your game, from simple primitives like cubes and spheres to cars and houses and characters.</span></span> <span data-ttu-id="0c45c-164">形式によっては、色やアニメーションのデータが含まれることも少なくありません。</span><span class="sxs-lookup"><span data-stu-id="0c45c-164">They often contain color and animation data, as well, depending on their format.</span></span> <span data-ttu-id="0c45c-165">ここでは、頂点データのみが含まれるメッシュについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-165">We'll focus on meshes that contain only vertex data.</span></span>

<span data-ttu-id="0c45c-166">メッシュを正しく読み込むには、メッシュのファイルのデータ形式を把握しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-166">To load a mesh correctly, you must know the format of the data in the file for the mesh.</span></span> <span data-ttu-id="0c45c-167">上記のシンプルな **BasicReaderWriter** 型は、データをバイト ストリームとして読み取るだけです。バイト データがメッシュを表していると認識することはできません。言うまでもなく、他のアプリケーションによってエクスポートされた特定のメッシュ形式も認識されません。</span><span class="sxs-lookup"><span data-stu-id="0c45c-167">Our simple **BasicReaderWriter** type above simply reads the data in as a byte stream; it doesn't know that the byte data represents a mesh, much less a specific mesh format as exported by another application!</span></span> <span data-ttu-id="0c45c-168">メッシュ データをメモリに読み込む際に変換を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-168">You must perform the conversion as you bring the mesh data into memory.</span></span>

<span data-ttu-id="0c45c-169">(常に、できるだけ内部表現に近い形式でアセット データをパッケージ化するようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-169">(You should always try to package asset data in a format that's as close to the internal representation as possible.</span></span> <span data-ttu-id="0c45c-170">こうすることでリソースの使用率が下がり、時間が短縮されます。)</span><span class="sxs-lookup"><span data-stu-id="0c45c-170">Doing so will reduce resource utilization and save time.)</span></span>

<span data-ttu-id="0c45c-171">メッシュのファイルからバイト データを取得してみましょう。</span><span class="sxs-lookup"><span data-stu-id="0c45c-171">Let's get the byte data from the mesh's file.</span></span> <span data-ttu-id="0c45c-172">この例では、ファイルの形式がサンプル固有の形式 (名前の最後が .vbo) であるとします</span><span class="sxs-lookup"><span data-stu-id="0c45c-172">The format in the example assumes that the file is a sample-specific format suffixed with .vbo.</span></span> <span data-ttu-id="0c45c-173">(ここでも、この形式は OpenGL の VBO 形式と同じです。)各頂点自体にマップ、 **BasicVertex** obj2vbo コンバーター ツールのコードで定義されている構造体である型。</span><span class="sxs-lookup"><span data-stu-id="0c45c-173">(Again, this format is not the same as OpenGL's VBO format.) Each vertex itself maps to the **BasicVertex** type, which is a struct defined in the code for the obj2vbo converter tool.</span></span> <span data-ttu-id="0c45c-174">.vbo ファイルの頂点データのレイアウトは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-174">The layout of the vertex data in the .vbo file looks like this:</span></span>

-   <span data-ttu-id="0c45c-175">データ ストリームの最初の 32 ビット (4 バイト) には、uint32 値として表されたメッシュの頂点の数 (numVertices) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-175">The first 32 bits (4 bytes) of the data stream contain the number of vertices (numVertices) in the mesh, represented as a uint32 value.</span></span>
-   <span data-ttu-id="0c45c-176">データ ストリームの次の 32 ビット (4 バイト) には、uint32 値として表されたメッシュのインデックスの数 (numIndices) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-176">The next 32 bits (4 bytes) of the data stream contain the number of indices in the mesh (numIndices), represented as a uint32 value.</span></span>
-   <span data-ttu-id="0c45c-177">その後、それに続く (numVertices \* sizeof (**BasicVertex**)) ビットには頂点データが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-177">After that, the subsequent (numVertices \* sizeof(**BasicVertex**)) bits contain the vertex data.</span></span>
-   <span data-ttu-id="0c45c-178">最後の (numIndices \* 16) データのビットに uint16 値のシーケンスとして表される、インデックス データが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-178">The last (numIndices \* 16) bits of data contain the index data, represented as a sequence of uint16 values.</span></span>

<span data-ttu-id="0c45c-179">要するに、読み込んだメッシュ データのビット レベルのレイアウトを把握するということです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-179">The point is this: know the bit-level layout of the mesh data you have loaded.</span></span> <span data-ttu-id="0c45c-180">また、エンディアンが一致するようにします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-180">Also, be sure you are consistent with endian-ness.</span></span> <span data-ttu-id="0c45c-181">すべての Windows 8 プラットフォームは、リトル エンディアンです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-181">All Windows 8 platforms are little-endian.</span></span>

<span data-ttu-id="0c45c-182">この例では、**LoadMeshAsync** メソッドから CreateMesh メソッドを呼び出して、ビット レベルの解釈を行っています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-182">In the example, you call a method, CreateMesh, from the **LoadMeshAsync** method to perform this bit-level interpretation.</span></span>

```cpp
task<void> BasicLoader::LoadMeshAsync(
    _In_ Platform::String^ filename,
    _Out_ ID3D11Buffer** vertexBuffer,
    _Out_ ID3D11Buffer** indexBuffer,
    _Out_opt_ uint32* vertexCount,
    _Out_opt_ uint32* indexCount
    )
{
    return m_basicReaderWriter->ReadDataAsync(filename).then([=](const Platform::Array<byte>^ meshData)
    {
        CreateMesh(
            meshData->Data,
            vertexBuffer,
            indexBuffer,
            vertexCount,
            indexCount,
            filename
            );
    });
}
```

<span data-ttu-id="0c45c-183">**CreateMesh** 、ファイルから読み込まれたバイトのデータを解釈し、頂点およびインデックスのリストを渡すことによって、頂点バッファーとインデックス バッファーのメッシュを作成しますそれぞれ、 [ **ID3D11Device::CreateBuffer**。 ](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11device-createbuffer) D3D11 のいずれかを指定して\_バインド\_頂点\_バッファーまたは D3D11\_バインド\_インデックス\_バッファー。</span><span class="sxs-lookup"><span data-stu-id="0c45c-183">**CreateMesh** interprets the byte data loaded from the file, and creates a vertex buffer and an index buffer for the mesh by passing the vertex and index lists, respectively, to [**ID3D11Device::CreateBuffer**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11device-createbuffer) and specifying either D3D11\_BIND\_VERTEX\_BUFFER or D3D11\_BIND\_INDEX\_BUFFER.</span></span> <span data-ttu-id="0c45c-184">**BasicLoader** で使われるコードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-184">Here's the code used in **BasicLoader**:</span></span>

```cpp
void BasicLoader::CreateMesh(
    _In_ byte* meshData,
    _Out_ ID3D11Buffer** vertexBuffer,
    _Out_ ID3D11Buffer** indexBuffer,
    _Out_opt_ uint32* vertexCount,
    _Out_opt_ uint32* indexCount,
    _In_opt_ Platform::String^ debugName
    )
{
    // The first 4 bytes of the BasicMesh format define the number of vertices in the mesh.
    uint32 numVertices = *reinterpret_cast<uint32*>(meshData);

    // The following 4 bytes define the number of indices in the mesh.
    uint32 numIndices = *reinterpret_cast<uint32*>(meshData + sizeof(uint32));

    // The next segment of the BasicMesh format contains the vertices of the mesh.
    BasicVertex* vertices = reinterpret_cast<BasicVertex*>(meshData + sizeof(uint32) * 2);

    // The last segment of the BasicMesh format contains the indices of the mesh.
    uint16* indices = reinterpret_cast<uint16*>(meshData + sizeof(uint32) * 2 + sizeof(BasicVertex) * numVertices);

    // Create the vertex and index buffers with the mesh data.

    D3D11_SUBRESOURCE_DATA vertexBufferData = {0};
    vertexBufferData.pSysMem = vertices;
    vertexBufferData.SysMemPitch = 0;
    vertexBufferData.SysMemSlicePitch = 0;
    CD3D11_BUFFER_DESC vertexBufferDesc(numVertices * sizeof(BasicVertex), D3D11_BIND_VERTEX_BUFFER);

    m_d3dDevice->CreateBuffer(
            &vertexBufferDesc,
            &vertexBufferData,
            vertexBuffer
            );
    
    D3D11_SUBRESOURCE_DATA indexBufferData = {0};
    indexBufferData.pSysMem = indices;
    indexBufferData.SysMemPitch = 0;
    indexBufferData.SysMemSlicePitch = 0;
    CD3D11_BUFFER_DESC indexBufferDesc(numIndices * sizeof(uint16), D3D11_BIND_INDEX_BUFFER);
    
    m_d3dDevice->CreateBuffer(
            &indexBufferDesc,
            &indexBufferData,
            indexBuffer
            );
  
    if (vertexCount != nullptr)
    {
        *vertexCount = numVertices;
    }
    if (indexCount != nullptr)
    {
        *indexCount = numIndices;
    }
}
```

<span data-ttu-id="0c45c-185">通常は、ゲームで使うメッシュごとに、頂点バッファーとインデックス バッファーのペアを作成します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-185">You typically create a vertex/index buffer pair for every mesh you use in your game.</span></span> <span data-ttu-id="0c45c-186">メッシュをいつ、どこに読み込むかは任意です。</span><span class="sxs-lookup"><span data-stu-id="0c45c-186">Where and when you load the meshes is up to you.</span></span> <span data-ttu-id="0c45c-187">メッシュが多数存在する場合は、ゲームの特定のポイント (定義済みの特定の読み込み状態のときなど) でディスクから一部のメッシュを読み込むことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-187">If you have a lot of meshes, you may only want to load some from the disk at specific points in the game, such as during specific, pre-defined loading states.</span></span> <span data-ttu-id="0c45c-188">地形データのような大きなメッシュの場合は、キャッシュから頂点をストリームすることもできますが、手順はより複雑になります (このトピックでは扱いません)。</span><span class="sxs-lookup"><span data-stu-id="0c45c-188">For large meshes, like terrain data, you can stream the vertices from a cache, but that is a more complex procedure and not in the scope of this topic.</span></span>

<span data-ttu-id="0c45c-189">繰り返しになりますが、頂点データの形式を把握する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-189">Again, know your vertex data format!</span></span> <span data-ttu-id="0c45c-190">モデルの作成に使われるツールで頂点データを表す方法は数多くあります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-190">There are many, many ways to represent vertex data across the tools used to create models.</span></span> <span data-ttu-id="0c45c-191">また、三角形リストや三角形ストリップなど、Direct3D に対して頂点データの入力レイアウトを示す方法もさまざまです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-191">There are also many different ways to represent the input layout of the vertex data to Direct3D, such as triangle lists and strips.</span></span> <span data-ttu-id="0c45c-192">頂点データについて詳しくは、「[Direct3D 11 のバッファーについて](https://docs.microsoft.com/windows/desktop/direct3d11/overviews-direct3d-11-resources-buffers-intro)」と「[プリミティブ](https://docs.microsoft.com/windows/desktop/direct3d9/primitives)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-192">For more information about vertex data, read [Introduction to Buffers in Direct3D 11](https://docs.microsoft.com/windows/desktop/direct3d11/overviews-direct3d-11-resources-buffers-intro) and [Primitives](https://docs.microsoft.com/windows/desktop/direct3d9/primitives).</span></span>

<span data-ttu-id="0c45c-193">次に、テクスチャの読み込みについて見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="0c45c-193">Next, let's look at loading textures.</span></span>

### <a name="loading-textures"></a><span data-ttu-id="0c45c-194">テクスチャの読み込み</span><span class="sxs-lookup"><span data-stu-id="0c45c-194">Loading textures</span></span>

<span data-ttu-id="0c45c-195">ゲームで最も一般的なアセット、そしてディスク上とメモリ内のファイルの大部分を構成するアセットはテクスチャです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-195">The most common asset in a game—and the one that comprises most of the files on disk and in memory—are textures.</span></span> <span data-ttu-id="0c45c-196">メッシュと同様、テクスチャにもさまざまな形式があるため、テクスチャの読み込み時に Direct3D で使うことができる形式に変換します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-196">Like meshes, textures can come in a variety of formats, and you convert them to a format that Direct3D can use when you load them.</span></span> <span data-ttu-id="0c45c-197">また、テクスチャにはさまざまなタイプがあり、種々の効果を作成するのに使われます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-197">Textures also come in a wide variety of types and are used to create different effects.</span></span> <span data-ttu-id="0c45c-198">テクスチャの MIP レベルを使えば、距離オブジェクトの外観とパフォーマンスを向上させることができます。ダート マップとライト マップは、基本テクスチャの上に効果や詳細を重ねるのに使われます。標準マップは、ピクセルあたりの照明の計算で使われます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-198">MIP levels for textures can be used to improve the look and performance of distance objects; dirt and light maps are used to layer effects and detail atop a base texture; and normal maps are used in per-pixel lighting calculations.</span></span> <span data-ttu-id="0c45c-199">最新のゲームでは、標準シーンにそれぞれ異なる何千ものテクスチャが存在する可能性があるため、そのすべてをコードで効果的に管理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-199">In a modern game, a typical scene can potentially have thousands of individual textures, and your code must effectively manage them all!</span></span>

<span data-ttu-id="0c45c-200">また、メッシュと同様、メモリ使用を効率化するのに使われる特殊な形式も数多く存在します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-200">Also like meshes, there are a number of specific formats that are used to make memory usage for efficient.</span></span> <span data-ttu-id="0c45c-201">テクスチャは、GPU (およびシステム) のメモリの大部分をすぐに消費するため、ほとんどの場合何らかの方法で圧縮されています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-201">Since textures can easily consume a large portion of the GPU (and system) memory, they are often compressed in some fashion.</span></span> <span data-ttu-id="0c45c-202">ゲームのテクスチャで圧縮を使う必要はありません。認識できる形式のデータを Direct3D シェーダーに提供する限り、必要な圧縮アルゴリズムと圧縮解除アルゴリズムを使うことができます ([**Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d) ビットマップと同様)。</span><span class="sxs-lookup"><span data-stu-id="0c45c-202">You aren't required to use compression on your game's textures, and you can use any compression/decompression algorithm(s) you want as long as you provide the Direct3D shaders with data in a format it can understand (like a [**Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d) bitmap).</span></span>

<span data-ttu-id="0c45c-203">Direct3D は、DXT テクスチャ圧縮アルゴリズムをサポートしています。ただし、プレイヤーのグラフィックス ハードウェアではサポートされない DXT 形式が存在する可能性もあります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-203">Direct3D provides support for the DXT texture compression algorithms, although every DXT format may not be supported in the player's graphics hardware.</span></span> <span data-ttu-id="0c45c-204">DDS ファイルには DXT テクスチャ (および他のテクスチャ圧縮形式) が含まれています。DDS ファイルの名前は .dds で終わります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-204">DDS files contain DXT textures (and other texture compression formats as well), and are suffixed with .dds.</span></span>

<span data-ttu-id="0c45c-205">DDS ファイルは、次の情報が含まれるバイナリ ファイルです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-205">A DDS file is a binary file that contains the following information:</span></span>

-   <span data-ttu-id="0c45c-206">4 文字コード値 "DDS " (0x20534444) が含まれる DWORD (マジック ナンバー)。</span><span class="sxs-lookup"><span data-stu-id="0c45c-206">A DWORD (magic number) containing the four character code value 'DDS ' (0x20534444).</span></span>

-   <span data-ttu-id="0c45c-207">ファイル内のデータの説明。</span><span class="sxs-lookup"><span data-stu-id="0c45c-207">A description of the data in the file.</span></span>

    <span data-ttu-id="0c45c-208">使用してヘッダーの説明と、データが説明されている[ **DDS\_ヘッダー**](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-header); を使用してピクセル形式を定義[ **DDS\_PIXELFORMAT**](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-pixelformat).</span><span class="sxs-lookup"><span data-stu-id="0c45c-208">The data is described with a header description using [**DDS\_HEADER**](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-header); the pixel format is defined using [**DDS\_PIXELFORMAT**](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-pixelformat).</span></span> <span data-ttu-id="0c45c-209">なお、 **DDS\_ヘッダー**と**DDS\_PIXELFORMAT**構造は非推奨の DDSURFACEDESC2、DDSCAPS2 および DDPIXELFORMAT DirectDraw 7 構造体を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-209">Note that the **DDS\_HEADER** and **DDS\_PIXELFORMAT** structures replace the deprecated DDSURFACEDESC2, DDSCAPS2 and DDPIXELFORMAT DirectDraw 7 structures.</span></span> <span data-ttu-id="0c45c-210">**DDS\_ヘッダー** DDSURFACEDESC2 と DDSCAPS2 のバイナリと同じです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-210">**DDS\_HEADER** is the binary equivalent of DDSURFACEDESC2 and DDSCAPS2.</span></span> <span data-ttu-id="0c45c-211">**DDS\_PIXELFORMAT** DDPIXELFORMAT のバイナリと同じです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-211">**DDS\_PIXELFORMAT** is the binary equivalent of DDPIXELFORMAT.</span></span>

    ```cpp
    DWORD               dwMagic;
    DDS_HEADER          header;
    ```

    <span data-ttu-id="0c45c-212">場合の値**dwFlags**で[ **DDS\_PIXELFORMAT** ](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-pixelformat) DDPF に設定されている\_FOURCC と**dwFourCC**に設定されています。追加するには、"DX10" [ **DDS\_ヘッダー\_DXT10** ](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-header-dxt10)構造体は、テクスチャ配列または RGB として表現できない DXGI 形式に対応するためには浮動小数点の形式、sRGB など形式などのピクセル形式します。ときに、 **DDS\_ヘッダー\_DXT10**構造が存在する、データ全体の説明は次のようです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-212">If the value of **dwFlags** in [**DDS\_PIXELFORMAT**](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-pixelformat) is set to DDPF\_FOURCC and **dwFourCC** is set to "DX10" an additional [**DDS\_HEADER\_DXT10**](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-header-dxt10) structure will be present to accommodate texture arrays or DXGI formats that cannot be expressed as an RGB pixel format such as floating point formats, sRGB formats etc. When the **DDS\_HEADER\_DXT10** structure is present, the entire data description will looks like this.</span></span>

    ```cpp
    DWORD               dwMagic;
    DDS_HEADER          header;
    DDS_HEADER_DXT10    header10;
    ```

-   <span data-ttu-id="0c45c-213">メイン サーフェス データを含むバイトの配列へのポインター。</span><span class="sxs-lookup"><span data-stu-id="0c45c-213">A pointer to an array of bytes that contains the main surface data.</span></span>
    ```cpp
    BYTE bdata[]
    ```

-   <span data-ttu-id="0c45c-214">残りのサーフェス (ミップマップ レベル、キューブ マップの面、ボリューム テクスチャの深度など) を含むバイトの配列へのポインター。</span><span class="sxs-lookup"><span data-stu-id="0c45c-214">A pointer to an array of bytes that contains the remaining surfaces such as; mipmap levels, faces in a cube map, depths in a volume texture.</span></span> <span data-ttu-id="0c45c-215">[テクスチャ](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-file-layout-for-textures)、[キューブ マップ](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-file-layout-for-cubic-environment-maps)、または[ボリューム テクスチャ](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-file-layout-for-volume-textures)の DDS ファイル レイアウトについて詳しくは、ここに挙げたリンク先をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-215">Follow these links for more information about the DDS file layout for a: [texture](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-file-layout-for-textures), a [cube map](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-file-layout-for-cubic-environment-maps), or a [volume texture](https://docs.microsoft.com/windows/desktop/direct3ddds/dds-file-layout-for-volume-textures).</span></span>

    ```cpp
    BYTE bdata2[]
    ```

<span data-ttu-id="0c45c-216">DDS 形式へのエクスポートは、多くのツールで実行可能です。</span><span class="sxs-lookup"><span data-stu-id="0c45c-216">Many tools export to the DDS format.</span></span> <span data-ttu-id="0c45c-217">テクスチャを DDS 形式にエクスポートできるツールがない場合は、作成することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-217">If you don't have a tool to export your texture to this format, consider creating one.</span></span> <span data-ttu-id="0c45c-218">DDS 形式について、また DDS 形式をコードで使う方法について詳しくは、「[DDS 用プログラミング ガイド](https://docs.microsoft.com/windows/desktop/direct3ddds/dx-graphics-dds-pguide)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-218">For more detail on the DDS format and how to work with it in your code, read [Programming Guide for DDS](https://docs.microsoft.com/windows/desktop/direct3ddds/dx-graphics-dds-pguide).</span></span> <span data-ttu-id="0c45c-219">この例では DDS を使います。</span><span class="sxs-lookup"><span data-stu-id="0c45c-219">In our example, we'll use DDS.</span></span>

<span data-ttu-id="0c45c-220">他の種類のリソースと同様に、バイトのストリームとしてファイルからデータを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-220">As with other resource types, you read the data from a file as a stream of bytes.</span></span> <span data-ttu-id="0c45c-221">読み込みタスクが完了すると、ラムダ呼び出しがコード (**CreateTexture** メソッド) を実行し、バイトのストリームを処理して Direct3D で使用できる形式にします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-221">Once your loading task completes, the lambda call runs code (the **CreateTexture** method) to process the stream of bytes into a format that Direct3D can use.</span></span>

```cpp
task<void> BasicLoader::LoadTextureAsync(
    _In_ Platform::String^ filename,
    _Out_opt_ ID3D11Texture2D** texture,
    _Out_opt_ ID3D11ShaderResourceView** textureView
    )
{
    return m_basicReaderWriter->ReadDataAsync(filename).then([=](const Platform::Array<byte>^ textureData)
    {
        CreateTexture(
            GetExtension(filename) == "dds",
            textureData->Data,
            textureData->Length,
            texture,
            textureView,
            filename
            );
    });
}
```

<span data-ttu-id="0c45c-222">上記のスニペットでは、ファイル名に拡張子の "dds" が含まれているかどうかラムダでチェックしています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-222">In the previous snippet, the lambda checks to see if the filename has an extension of "dds".</span></span> <span data-ttu-id="0c45c-223">この拡張子が含まれていれば、DDS テクスチャであると判断できます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-223">If it does, you assume that it is a DDS texture.</span></span> <span data-ttu-id="0c45c-224">含まれていない場合は、Windows Imaging Component (WIC) API を使って形式を検出し、データをビットマップとしてデコードします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-224">If not, well, use the Windows Imaging Component (WIC) APIs to discover the format and decode the data as a bitmap.</span></span> <span data-ttu-id="0c45c-225">いずれにしても、結果は [**Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d) ビットマップ (またはエラー) になります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-225">Either way, the result is a [**Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d) bitmap (or an error).</span></span>

```cpp
void BasicLoader::CreateTexture(
    _In_ bool decodeAsDDS,
    _In_reads_bytes_(dataSize) byte* data,
    _In_ uint32 dataSize,
    _Out_opt_ ID3D11Texture2D** texture,
    _Out_opt_ ID3D11ShaderResourceView** textureView,
    _In_opt_ Platform::String^ debugName
    )
{
    ComPtr<ID3D11ShaderResourceView> shaderResourceView;
    ComPtr<ID3D11Texture2D> texture2D;

    if (decodeAsDDS)
    {
        ComPtr<ID3D11Resource> resource;

        if (textureView == nullptr)
        {
            CreateDDSTextureFromMemory(
                m_d3dDevice.Get(),
                data,
                dataSize,
                &resource,
                nullptr
                );
        }
        else
        {
            CreateDDSTextureFromMemory(
                m_d3dDevice.Get(),
                data,
                dataSize,
                &resource,
                &shaderResourceView
                );
        }

        resource.As(&texture2D);
    }
    else
    {
        if (m_wicFactory.Get() == nullptr)
        {
            // A WIC factory object is required in order to load texture
            // assets stored in non-DDS formats.  If BasicLoader was not
            // initialized with one, create one as needed.
            CoCreateInstance(
                    CLSID_WICImagingFactory,
                    nullptr,
                    CLSCTX_INPROC_SERVER,
                    IID_PPV_ARGS(&m_wicFactory));
        }

        ComPtr<IWICStream> stream;
        m_wicFactory->CreateStream(&stream);

        stream->InitializeFromMemory(
                data,
                dataSize);

        ComPtr<IWICBitmapDecoder> bitmapDecoder;
        m_wicFactory->CreateDecoderFromStream(
                stream.Get(),
                nullptr,
                WICDecodeMetadataCacheOnDemand,
                &bitmapDecoder);

        ComPtr<IWICBitmapFrameDecode> bitmapFrame;
        bitmapDecoder->GetFrame(0, &bitmapFrame);

        ComPtr<IWICFormatConverter> formatConverter;
        m_wicFactory->CreateFormatConverter(&formatConverter);

        formatConverter->Initialize(
                bitmapFrame.Get(),
                GUID_WICPixelFormat32bppPBGRA,
                WICBitmapDitherTypeNone,
                nullptr,
                0.0,
                WICBitmapPaletteTypeCustom);

        uint32 width;
        uint32 height;
        bitmapFrame->GetSize(&width, &height);

        std::unique_ptr<byte[]> bitmapPixels(new byte[width * height * 4]);
        formatConverter->CopyPixels(
                nullptr,
                width * 4,
                width * height * 4,
                bitmapPixels.get());

        D3D11_SUBRESOURCE_DATA initialData;
        ZeroMemory(&initialData, sizeof(initialData));
        initialData.pSysMem = bitmapPixels.get();
        initialData.SysMemPitch = width * 4;
        initialData.SysMemSlicePitch = 0;

        CD3D11_TEXTURE2D_DESC textureDesc(
            DXGI_FORMAT_B8G8R8A8_UNORM,
            width,
            height,
            1,
            1
            );

        m_d3dDevice->CreateTexture2D(
                &textureDesc,
                &initialData,
                &texture2D);

        if (textureView != nullptr)
        {
            CD3D11_SHADER_RESOURCE_VIEW_DESC shaderResourceViewDesc(
                texture2D.Get(),
                D3D11_SRV_DIMENSION_TEXTURE2D
                );

            m_d3dDevice->CreateShaderResourceView(
                    texture2D.Get(),
                    &shaderResourceViewDesc,
                    &shaderResourceView);
        }
    }


    if (texture != nullptr)
    {
        *texture = texture2D.Detach();
    }
    if (textureView != nullptr)
    {
        *textureView = shaderResourceView.Detach();
    }
}
```

<span data-ttu-id="0c45c-226">このコードが完了すると、イメージ ファイルから読み込まれた [**Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d) がメモリ内に格納されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-226">When this code completes, you have a [**Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d) in memory, loaded from an image file.</span></span> <span data-ttu-id="0c45c-227">メッシュと同様に、ゲームにも特定のシーンにもおそらく多数のテクスチャが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-227">As with meshes, you probably have a lot of them in your game and in any given scene.</span></span> <span data-ttu-id="0c45c-228">ゲームまたはレベルの開始時にすべてのテクスチャを読み込むのではなく、シーンごとまたはレベルごとに何度もアクセスされるテクスチャについては、そのためのキャッシュを作成することを検討します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-228">Consider creating caches for regularly accessed textures per-scene or per-level, rather than loading them all when the game or level starts.</span></span>

<span data-ttu-id="0c45c-229">(上記のサンプルで呼び出された **CreateDDSTextureFromMemory** メソッドの全コードについては、「[DDSTextureLoader のコード一式](complete-code-for-ddstextureloader.md)」をご覧ください。)</span><span class="sxs-lookup"><span data-stu-id="0c45c-229">(The **CreateDDSTextureFromMemory** method called in the above sample can be explored in full in [Complete code for DDSTextureLoader](complete-code-for-ddstextureloader.md).)</span></span>

<span data-ttu-id="0c45c-230">また、個々のテクスチャまたはテクスチャの "スキン" は、特定のメッシュ多角形やサーフェスにマップされている場合があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-230">Also, individual textures or texture "skins" may map to specific mesh polygons or surfaces.</span></span> <span data-ttu-id="0c45c-231">このマッピング データは通常、アーティストやデザイナーがモデルとテクスチャを作成するのに使ったツールでエクスポートされます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-231">This mapping data is usually exported by the tool an artist or designer used to create the model and the textures.</span></span> <span data-ttu-id="0c45c-232">フラグメント シェーディングの実行時には、この情報を使って適切なテクスチャを対応サーフェスにマップします。したがって、エクスポートされたデータを読み込む際には、この情報も必ずキャプチャするようにします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-232">Make sure that you capture this information as well when you load the exported data, as you will use it map the correct textures to the corresponding surfaces when you perform fragment shading.</span></span>

### <a name="loading-shaders"></a><span data-ttu-id="0c45c-233">シェーダーの読み込み</span><span class="sxs-lookup"><span data-stu-id="0c45c-233">Loading shaders</span></span>

<span data-ttu-id="0c45c-234">シェーダーは、メモリに読み込まれてグラフィックス パイプラインの特定の段階で呼び出されるコンパイル済み上位レベル シェーダー言語 (HLSL) ファイルです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-234">Shaders are compiled High Level Shader Language (HLSL) files that are loaded into memory and invoked at specific stages of the graphics pipeline.</span></span> <span data-ttu-id="0c45c-235">最も一般的で重要なシェーダーは、頂点シェーダーとピクセル シェーダーです。頂点シェーダーではメッシュの個々の頂点が処理され、ピクセル シェーダーではシーンのビューポートのピクセルが処理されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-235">The most common and essential shaders are the vertex and pixel shaders, which process the individual vertices of your mesh and the pixels in the scene's viewport(s), respectively.</span></span> <span data-ttu-id="0c45c-236">HLSL コードは、ジオメトリの変換、照明効果とテクスチャの適用、レンダリングされたシーンの後処理を行う場合に実行します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-236">The HLSL code is executed to transform the geometry, apply lighting effects and textures, and perform post-processing on the rendered scene.</span></span>

<span data-ttu-id="0c45c-237">Direct3D ゲームには、それぞれが別々の CSO (コンパイル済みシェーダー オブジェクト、.cso) ファイルにコンパイルされた、さまざまなシェーダーが存在している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-237">A Direct3D game can have a number of different shaders, each one compiled into a separate CSO (Compiled Shader Object, .cso) file.</span></span> <span data-ttu-id="0c45c-238">通常、動的に読み込む必要があるシェーダーはそれほど多くありません。ほとんどの場合、ゲームの開始時またはレベルごとに、シェーダーを簡単に読み込むことができます (雨の効果のシェーダーなど)。</span><span class="sxs-lookup"><span data-stu-id="0c45c-238">Normally, you don't have so many that you need to load them dynamically, and in most cases, you can simply load them when the game is starting, or on a per-level basis (such as a shader for rain effects).</span></span>

<span data-ttu-id="0c45c-239">**BasicLoader** クラスのコードは、頂点、ジオメトリ、ピクセル、ハルなどのさまざまなシェーダーに多数のオーバーロードを提供します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-239">The code in the **BasicLoader** class provides a number of overloads for different shaders, including vertex, geometry, pixel, and hull shaders.</span></span> <span data-ttu-id="0c45c-240">次のコードでは、例としてピクセル シェーダーを取り上げています</span><span class="sxs-lookup"><span data-stu-id="0c45c-240">The code below covers pixel shaders as an example.</span></span> <span data-ttu-id="0c45c-241">(すべてのコードについては、「[BasicLoader のコード一式](complete-code-for-basicloader.md)」をご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="0c45c-241">(You can review the complete code in [Complete code for BasicLoader](complete-code-for-basicloader.md).)</span></span>

```cpp
concurrency::task<void> LoadShaderAsync(
    _In_ Platform::String^ filename,
    _Out_ ID3D11PixelShader** shader
    );

// ...

task<void> BasicLoader::LoadShaderAsync(
    _In_ Platform::String^ filename,
    _Out_ ID3D11PixelShader** shader
    )
{
    return m_basicReaderWriter->ReadDataAsync(filename).then([=](const Platform::Array<byte>^ bytecode)
    {
        
       m_d3dDevice->CreatePixelShader(
                bytecode->Data,
                bytecode->Length,
                nullptr,
                shader);
    });
}

```

<span data-ttu-id="0c45c-242">この例では使用して、 **BasicReaderWriter**インスタンス (**m\_basicReaderWriter**) バイト ストリームとして指定されたコンパイル済みシェーダー オブジェクト (.cso) ファイルを読み取るようにします。</span><span class="sxs-lookup"><span data-stu-id="0c45c-242">In this example, you use the **BasicReaderWriter** instance (**m\_basicReaderWriter**) to read in the supplied compiled shader object (.cso) file as a byte stream.</span></span> <span data-ttu-id="0c45c-243">このタスクが完了すると、ラムダは、ファイルから読み込まれたバイト データを使って [**ID3D11Device::CreatePixelShader**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11device-createpixelshader) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-243">Once that task completes, the lambda calls [**ID3D11Device::CreatePixelShader**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11device-createpixelshader) with the byte data loaded from the file.</span></span> <span data-ttu-id="0c45c-244">また、コールバックによって、読み込みの成功を示すフラグを設定する必要があります。コードでは、シェーダーの実行前にこのフラグを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-244">Your callback must set some flag indicating that the load was successful, and your code must check this flag before running the shader.</span></span>

<span data-ttu-id="0c45c-245">頂点シェーダーはもう少し複雑になります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-245">Vertex shaders are bit more complex.</span></span> <span data-ttu-id="0c45c-246">頂点シェーダーの場合は、頂点データを定義する別個の入力レイアウトも読み込みます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-246">For a vertex shader, you also load a separate input layout that defines the vertex data.</span></span> <span data-ttu-id="0c45c-247">次のコードを使うことで、頂点シェーダーと一緒にカスタムの頂点入力レイアウトを非同期的に読み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-247">The following code can be used to asynchronously load a vertex shader along with a custom vertex input layout.</span></span> <span data-ttu-id="0c45c-248">メッシュから読み込まれた頂点情報は、この入力レイアウトによって適切に表せるようになります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-248">Be sure that the vertex information that you load from your meshes can be correctly represented by this input layout!</span></span>

<span data-ttu-id="0c45c-249">頂点シェーダーを読み込む前に入力レイアウトを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="0c45c-249">Let's create the input layout before you load the vertex shader.</span></span>

```cpp
void BasicLoader::CreateInputLayout(
    _In_reads_bytes_(bytecodeSize) byte* bytecode,
    _In_ uint32 bytecodeSize,
    _In_reads_opt_(layoutDescNumElements) D3D11_INPUT_ELEMENT_DESC* layoutDesc,
    _In_ uint32 layoutDescNumElements,
    _Out_ ID3D11InputLayout** layout
    )
{
    if (layoutDesc == nullptr)
    {
        // If no input layout is specified, use the BasicVertex layout.
        const D3D11_INPUT_ELEMENT_DESC basicVertexLayoutDesc[] =
        {
            { "POSITION", 0, DXGI_FORMAT_R32G32B32_FLOAT, 0, 0,  D3D11_INPUT_PER_VERTEX_DATA, 0 },
            { "NORMAL",   0, DXGI_FORMAT_R32G32B32_FLOAT, 0, 12, D3D11_INPUT_PER_VERTEX_DATA, 0 },
            { "TEXCOORD", 0, DXGI_FORMAT_R32G32_FLOAT,    0, 24, D3D11_INPUT_PER_VERTEX_DATA, 0 },
        };

        m_d3dDevice->CreateInputLayout(
                basicVertexLayoutDesc,
                ARRAYSIZE(basicVertexLayoutDesc),
                bytecode,
                bytecodeSize,
                layout);
    }
    else
    {
        m_d3dDevice->CreateInputLayout(
                layoutDesc,
                layoutDescNumElements,
                bytecode,
                bytecodeSize,
                layout);
    }
}
```

<span data-ttu-id="0c45c-250">このレイアウトでは、各頂点に、頂点シェーダーで処理される次のデータが含まれます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-250">In this particular layout, each vertex has the following data processed by the vertex shader:</span></span>

-   <span data-ttu-id="0c45c-251">モデルの座標空間における 3D の座標位置 (x, y, z)。3 つの 32 ビット浮動小数点値で表されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-251">A 3D coordinate position (x, y, z) in the model's coordinate space, represented as a trio of 32-bit floating point values.</span></span>
-   <span data-ttu-id="0c45c-252">頂点の標準ベクター。これも 3 つの 32 ビット浮動小数点値で表されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-252">A normal vector for the vertex, also represented as three 32-bit floating point values.</span></span>
-   <span data-ttu-id="0c45c-253">変換された 2D テクスチャの座標値 (u, v)。2 つの 32 ビット浮動小数点値で表されます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-253">A transformed 2D texture coordinate value (u, v) , represented as a pair of 32-bit floating values.</span></span>

<span data-ttu-id="0c45c-254">頂点ごとのこれらの入力要素は [HLSL セマンティクス](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-semantics)と呼ばれます。これらの入力要素は、コンパイル済みシェーダー オブジェクトとのデータの受け渡しに使われる定義済みレジスタのセットです。</span><span class="sxs-lookup"><span data-stu-id="0c45c-254">These per-vertex input elements are called [HLSL semantics](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-semantics), and they are a set of defined registers used to pass data to and from your compiled shader object.</span></span> <span data-ttu-id="0c45c-255">読み込んだメッシュの頂点ごとに 1 回、パイプラインが頂点シェーダーを実行します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-255">Your pipeline runs the vertex shader once for every vertex in the mesh that you've loaded.</span></span> <span data-ttu-id="0c45c-256">このセマンティクスは、実行時の頂点シェーダーへの入力 (および頂点シェーダーからの出力) を定義し、シェーダーの HLSL コードでの頂点ごとの計算にこのデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="0c45c-256">The semantics define the input to (and output from) the vertex shader as it runs, and provide this data for your per-vertex computations in your shader's HLSL code.</span></span>

<span data-ttu-id="0c45c-257">次に、頂点シェーダー オブジェクトを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="0c45c-257">Now, load the vertex shader object.</span></span>

```cpp
concurrency::task<void> LoadShaderAsync(
        _In_ Platform::String^ filename,
        _In_reads_opt_(layoutDescNumElements) D3D11_INPUT_ELEMENT_DESC layoutDesc[],
        _In_ uint32 layoutDescNumElements,
        _Out_ ID3D11VertexShader** shader,
        _Out_opt_ ID3D11InputLayout** layout
        );

// ...

task<void> BasicLoader::LoadShaderAsync(
    _In_ Platform::String^ filename,
    _In_reads_opt_(layoutDescNumElements) D3D11_INPUT_ELEMENT_DESC layoutDesc[],
    _In_ uint32 layoutDescNumElements,
    _Out_ ID3D11VertexShader** shader,
    _Out_opt_ ID3D11InputLayout** layout
    )
{
    // This method assumes that the lifetime of input arguments may be shorter
    // than the duration of this task.  In order to ensure accurate results, a
    // copy of all arguments passed by pointer must be made.  The method then
    // ensures that the lifetime of the copied data exceeds that of the task.

    // Create copies of the layoutDesc array as well as the SemanticName strings,
    // both of which are pointers to data whose lifetimes may be shorter than that
    // of this method's task.
    shared_ptr<vector<D3D11_INPUT_ELEMENT_DESC>> layoutDescCopy;
    shared_ptr<vector<string>> layoutDescSemanticNamesCopy;
    if (layoutDesc != nullptr)
    {
        layoutDescCopy.reset(
            new vector<D3D11_INPUT_ELEMENT_DESC>(
                layoutDesc,
                layoutDesc + layoutDescNumElements
                )
            );

        layoutDescSemanticNamesCopy.reset(
            new vector<string>(layoutDescNumElements)
            );

        for (uint32 i = 0; i < layoutDescNumElements; i++)
        {
            layoutDescSemanticNamesCopy->at(i).assign(layoutDesc[i].SemanticName);
        }
    }

    return m_basicReaderWriter->ReadDataAsync(filename).then([=](const Platform::Array<byte>^ bytecode)
    {
       m_d3dDevice->CreateVertexShader(
                bytecode->Data,
                bytecode->Length,
                nullptr,
                shader);

        if (layout != nullptr)
        {
            if (layoutDesc != nullptr)
            {
                // Reassign the SemanticName elements of the layoutDesc array copy to point
                // to the corresponding copied strings. Performing the assignment inside the
                // lambda body ensures that the lambda will take a reference to the shared_ptr
                // that holds the data.  This will guarantee that the data is still valid when
                // CreateInputLayout is called.
                for (uint32 i = 0; i < layoutDescNumElements; i++)
                {
                    layoutDescCopy->at(i).SemanticName = layoutDescSemanticNamesCopy->at(i).c_str();
                }
            }

            CreateInputLayout(
                bytecode->Data,
                bytecode->Length,
                layoutDesc == nullptr ? nullptr : layoutDescCopy->data(),
                layoutDescNumElements,
                layout);   
        }
    });
}

```

<span data-ttu-id="0c45c-258">このコードでは、頂点シェーダーの CSO ファイルのバイト データを読み取ってから、[**ID3D11Device::CreateVertexShader**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11device-createvertexshader) を呼び出して頂点シェーダーを作成しています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-258">In this code, once you've read in the byte data for the vertex shader's CSO file, you create the vertex shader by calling [**ID3D11Device::CreateVertexShader**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11device-createvertexshader).</span></span> <span data-ttu-id="0c45c-259">その後で、同じラムダでシェーダーの入力レイアウトを作成しています。</span><span class="sxs-lookup"><span data-stu-id="0c45c-259">After that, you create your input layout for the shader in the same lambda.</span></span>

<span data-ttu-id="0c45c-260">ハル シェーダーやジオメトリ シェーダーなどの他の種類のシェーダーでは、特別な構成が必要になる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="0c45c-260">Other shader types, such as hull and geometry shaders, can also require specific configuration.</span></span> <span data-ttu-id="0c45c-261">さまざまなシェーダー読み込みメソッドのコード一式については、「[BasicLoader のコード一式](complete-code-for-basicloader.md)」と [Direct3D リソース読み込みのサンプル]( https://go.microsoft.com/fwlink/p/?LinkID=265132)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c45c-261">Complete code for a variety of shader loading methods is provided in [Complete code for BasicLoader](complete-code-for-basicloader.md) and in the [Direct3D resource loading sample]( https://go.microsoft.com/fwlink/p/?LinkID=265132).</span></span>

## <a name="remarks"></a><span data-ttu-id="0c45c-262">注釈</span><span class="sxs-lookup"><span data-stu-id="0c45c-262">Remarks</span></span>

<span data-ttu-id="0c45c-263">これで、メッシュ、テクスチャ、コンパイル済みシェーダーなどの一般的なゲームのリソースとアセットを非同期的に読み込むメソッドを理解し、作成と変更をできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0c45c-263">At this point, you should understand and be able to create or modify methods for asynchronously loading common game resources and assets, such as meshes, textures, and compiled shaders.</span></span>

## <a name="related-topics"></a><span data-ttu-id="0c45c-264">関連トピック</span><span class="sxs-lookup"><span data-stu-id="0c45c-264">Related topics</span></span>

* [<span data-ttu-id="0c45c-265">Direct3D リソース読み込みのサンプル</span><span class="sxs-lookup"><span data-stu-id="0c45c-265">Direct3D resource loading sample</span></span>]( https://go.microsoft.com/fwlink/p/?LinkID=265132)
* [<span data-ttu-id="0c45c-266">BasicLoader の完全なコード</span><span class="sxs-lookup"><span data-stu-id="0c45c-266">Complete code for BasicLoader</span></span>](complete-code-for-basicloader.md)
* [<span data-ttu-id="0c45c-267">BasicReaderWriter の完全なコード</span><span class="sxs-lookup"><span data-stu-id="0c45c-267">Complete code for BasicReaderWriter</span></span>](complete-code-for-basicreaderwriter.md)
* [<span data-ttu-id="0c45c-268">DDSTextureLoader の完全なコード</span><span class="sxs-lookup"><span data-stu-id="0c45c-268">Complete code for DDSTextureLoader</span></span>](complete-code-for-ddstextureloader.md)

 

 




