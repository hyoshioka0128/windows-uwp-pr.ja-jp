---
title: ゲームのムーブ/ルック コントロール
description: ここでは、マウスとキーボードの従来のムーブ/ルック コントロール (マウスルック コントロールとも呼ばれます) を DirectX ゲームに追加する方法について説明します。
ms.assetid: 4b4d967c-3de9-8a97-ae68-0327f00cc933
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, ムーブ/ルック, コントロール
ms.localizationpriority: medium
ms.openlocfilehash: f1516ada043ac5e9d5c059f7cd2b91cb69a5eab1
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66367854"
---
# <a name="span-iddevgamingtutorialaddingmove-lookcontrolstoyourdirectxgamespanmove-look-controls-for-games"></a><span data-ttu-id="4d356-104"><span id="dev_gaming.tutorial__adding_move-look_controls_to_your_directx_game"></span>ゲームの移動検索コントロール</span><span class="sxs-lookup"><span data-stu-id="4d356-104"><span id="dev_gaming.tutorial__adding_move-look_controls_to_your_directx_game"></span>Move-look controls for games</span></span>



<span data-ttu-id="4d356-105">ここでは、マウスとキーボードの従来のムーブ/ルック コントロール (マウスルック コントロールとも呼ばれます) を DirectX ゲームに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4d356-105">Learn how to add traditional mouse and keyboard move-look controls (also known as mouselook controls) to your DirectX game.</span></span>

<span data-ttu-id="4d356-106">さらに、タッチ デバイスでのムーブ/ルックのサポートについても説明します。タッチ デバイスでは、ムーブ コントローラーは画面の左下の部分として定義され、方向入力と同じように動作します。ルック コントローラーは、画面の残りの部分に対して定義されます。カメラは、中心をプレイヤーがその領域内で最後にタッチした場所に合わせます。</span><span class="sxs-lookup"><span data-stu-id="4d356-106">We also discuss move-look support for touch devices, with the move controller defined as the lower-left section of the screen that behaves like a directional input, and the look controller defined for the remainder of the screen, with the camera centering on the last place the player touched in that area.</span></span>

<span data-ttu-id="4d356-107">このコントロールの概念に詳しくない場合は、キーボード (またはタッチ ベースの方向入力ボックス) は、この 3D 空間内で足を制御し、足が前後または左右にしか動けないかのように機能するものと考えてください。</span><span class="sxs-lookup"><span data-stu-id="4d356-107">If this is an unfamiliar control concept to you, think of it this way: the keyboard (or the touch-based directional input box) controls your legs in this 3D space, and behaves as if your legs were only capable of moving forward or backward, or strafing left and right.</span></span> <span data-ttu-id="4d356-108">マウス (またはタッチ ポインター) は、頭を制御します。</span><span class="sxs-lookup"><span data-stu-id="4d356-108">The mouse (or touch pointer) controls your head.</span></span> <span data-ttu-id="4d356-109">頭を動かして、ある方向 (左、右、上、下、またはその平面のどこか) を見ます。</span><span class="sxs-lookup"><span data-stu-id="4d356-109">You use your head to look in a direction -- left or right, up or down, or somewhere in that plane.</span></span> <span data-ttu-id="4d356-110">視界の中にターゲットがある場合、マウスを使ってカメラ ビューの中心をそのターゲットに合わせてから、前進キーを押してターゲットに向かって前進するか、後退キーを押してターゲットから後退します。</span><span class="sxs-lookup"><span data-stu-id="4d356-110">If there is a target in your view, you would use the mouse to center your camera view on that target, and then press the forward key to move towards it, or back to move away from it.</span></span> <span data-ttu-id="4d356-111">ターゲットの周りを旋回するには、カメラ ビューの中心をターゲットに合わせたまま、左右に動きます。</span><span class="sxs-lookup"><span data-stu-id="4d356-111">To circle the target, you would keep the camera view centered on the target, and move left or right at the same time.</span></span> <span data-ttu-id="4d356-112">このように、この制御方法は 3D 環境のナビゲートに非常に有効です。</span><span class="sxs-lookup"><span data-stu-id="4d356-112">You can see how this is a very effective control method for navigating 3D environments!</span></span>

<span data-ttu-id="4d356-113">これらのコントロールは、ゲームでは一般的に WASD コントロールと呼ばれます。WASD コントロールでは、x-z 平面に固定されたカメラを動かすのに W、A、S、D のキーを使用し、x 軸と y 軸を中心としたカメラの回転を制御するのにマウスを使用します。</span><span class="sxs-lookup"><span data-stu-id="4d356-113">These controls are commonly known as WASD controls in gaming, where the W, A, S, and D keys are used for x-z plane fixed camera movement, and the mouse is used to control camera rotation around the x and y axes.</span></span>

## <a name="objectives"></a><span data-ttu-id="4d356-114">目標</span><span class="sxs-lookup"><span data-stu-id="4d356-114">Objectives</span></span>


-   <span data-ttu-id="4d356-115">マウス/キーボード用とタッチ スクリーン用の両方の基本的なムーブ/ルック コントロールを DirectX ゲームに追加する。</span><span class="sxs-lookup"><span data-stu-id="4d356-115">Add basic move-look controls to your DirectX game for both mouse and keyboard, and touch screens.</span></span>
-   <span data-ttu-id="4d356-116">3D 環境のナビゲートに使う主観カメラを実装する。</span><span class="sxs-lookup"><span data-stu-id="4d356-116">Implement a first-person camera used to navigate a 3D environment.</span></span>

## <a name="a-note-on-touch-control-implementations"></a><span data-ttu-id="4d356-117">タッチ コントロールの実装に関する注意</span><span class="sxs-lookup"><span data-stu-id="4d356-117">A note on touch control implementations</span></span>


<span data-ttu-id="4d356-118">タッチ コントロールには、2 つのコントローラーを実装します。1 つはカメラの視点に相対的な x-z 平面の動きを扱うムーブ コントローラー、もう 1 つはカメラの視点を合わせるためのルック コントローラーです。</span><span class="sxs-lookup"><span data-stu-id="4d356-118">For touch controls, we implement two controllers: the move controller, which handles movement in the x-z plane relative to the camera's look point; and the look controller, which aims the camera's look point.</span></span> <span data-ttu-id="4d356-119">ムーブ コントローラーはキーボードの WASD ボタンに相当し、ルック コントローラーはマウスに相当します。</span><span class="sxs-lookup"><span data-stu-id="4d356-119">Our move controller maps to the keyboard WASD buttons, and the look controller maps to the mouse.</span></span> <span data-ttu-id="4d356-120">ただし、タッチ コントロールでは、方向入力、または仮想的な WASD ボタンとして機能する画面の領域を定義する必要があります。画面の残りの部分は、ルック コントロール用の入力領域として機能します。</span><span class="sxs-lookup"><span data-stu-id="4d356-120">But for touch controls, we need to define a region of the screen that serves as the directional inputs, or the virtual WASD buttons, with the remainder of the screen serving as the input space for the look controls.</span></span>

<span data-ttu-id="4d356-121">画面は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="4d356-121">Our screen looks like this.</span></span>

![ムーブ/ルック コントローラーのレイアウト](images/movelook-touch.png)

<span data-ttu-id="4d356-123">タッチ ポインター (マウスではなく) を画面の左下で動かす場合、上方向に動かすとカメラは前方に動きます。</span><span class="sxs-lookup"><span data-stu-id="4d356-123">When you move the touch pointer (not the mouse!) in the lower left of the screen, any movement upwards will make the camera move forward.</span></span> <span data-ttu-id="4d356-124">下方向に動かすとカメラは後方に動きます。</span><span class="sxs-lookup"><span data-stu-id="4d356-124">Any movement downwards will make the camera move backwards.</span></span> <span data-ttu-id="4d356-125">ムーブ コントローラーのポインター領域内でポインターを左右に動かす場合にも同じことが当てはまります。</span><span class="sxs-lookup"><span data-stu-id="4d356-125">The same holds for left and right movement inside the move controller's pointer space.</span></span> <span data-ttu-id="4d356-126">この領域外ではルック コントローラーになるため、カメラを単にタッチまたはドラッグして、希望の向きにします。</span><span class="sxs-lookup"><span data-stu-id="4d356-126">Outside of that space, and it becomes a look controller -- you just touch or drag the camera to where you'd like it to face.</span></span>

## <a name="set-up-the-basic-input-event-infrastructure"></a><span data-ttu-id="4d356-127">基本的な入力イベントのインフラストラクチャのセットアップ</span><span class="sxs-lookup"><span data-stu-id="4d356-127">Set up the basic input event infrastructure</span></span>


<span data-ttu-id="4d356-128">まず、マウスとキーボードからの入力イベントの処理と、その入力に基づいたカメラの視点の更新を行うコントロール クラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d356-128">First, we must create our control class that we use to handle input events from the mouse and keyboard, and update the camera perspective based on that input.</span></span> <span data-ttu-id="4d356-129">実装するのはムーブ/ルック コントロールであるため、**MoveLookController** という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="4d356-129">Because we're implementing move-look controls, we call it **MoveLookController**.</span></span>

```cpp
using namespace Windows::UI::Core;
using namespace Windows::System;
using namespace Windows::Foundation;
using namespace Windows::Devices::Input;
#include <DirectXMath.h>

// Methods to get input from the UI pointers
ref class MoveLookController
{
};  // class MoveLookController
```

<span data-ttu-id="4d356-130">次に、ムーブ/ルック コントローラーの状態とその主観カメラを定義するヘッダーと、コントロールを実装してカメラの状態を更新する基本的なメソッドとイベント ハンドラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="4d356-130">Now, let's create a header that defines the state of the move-look controller and its first-person camera, plus the basic methods and event handlers that implement the controls and that update the state of the camera.</span></span>

```cpp
#define ROTATION_GAIN 0.004f    // Sensitivity adjustment for the look controller
#define MOVEMENT_GAIN 0.1f      // Sensitivity adjustment for the move controller

ref class MoveLookController
{
private:
    // Properties of the controller object
    DirectX::XMFLOAT3 m_position;               // The position of the controller
    float m_pitch, m_yaw;           // Orientation euler angles in radians

    // Properties of the Move control
    bool m_moveInUse;               // Specifies whether the move control is in use
    uint32 m_movePointerID;         // Id of the pointer in this control
    DirectX::XMFLOAT2 m_moveFirstDown;          // Point where initial contact occurred
    DirectX::XMFLOAT2 m_movePointerPosition;   // Point where the move pointer is currently located
    DirectX::XMFLOAT3 m_moveCommand;            // The net command from the move control

    // Properties of the Look control
    bool m_lookInUse;               // Specifies whether the look control is in use
    uint32 m_lookPointerID;         // Id of the pointer in this control
    DirectX::XMFLOAT2 m_lookLastPoint;          // Last point (from last frame)
    DirectX::XMFLOAT2 m_lookLastDelta;          // For smoothing

    bool m_forward, m_back;         // States for movement
    bool m_left, m_right;
    bool m_up, m_down;


public:

    // Methods to get input from the UI pointers
    void OnPointerPressed(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::PointerEventArgs^ args
        );

    void OnPointerMoved(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::PointerEventArgs^ args
        );

    void OnPointerReleased(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::PointerEventArgs^ args
        );

    void OnKeyDown(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::KeyEventArgs^ args
        );

    void OnKeyUp(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::KeyEventArgs^ args
        );

    // Set up the Controls that this controller supports
    void Initialize( _In_ Windows::UI::Core::CoreWindow^ window );

    void Update( Windows::UI::Core::CoreWindow ^window );
    
internal:
    // Accessor to set position of controller
    void SetPosition( _In_ DirectX::XMFLOAT3 pos );

    // Accessor to set position of controller
    void SetOrientation( _In_ float pitch, _In_ float yaw );

    // Returns the position of the controller object
    DirectX::XMFLOAT3 get_Position();

    // Returns the point  which the controller is facing
    DirectX::XMFLOAT3 get_LookPoint();


};  // class MoveLookController
```

<span data-ttu-id="4d356-131">このコードには、プライベート フィールドのグループが 4 つ含まれています。</span><span class="sxs-lookup"><span data-stu-id="4d356-131">Our code contains 4 groups of private fields.</span></span> <span data-ttu-id="4d356-132">それぞれの目的を確認してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4d356-132">Let's review the purpose of each one.</span></span>

<span data-ttu-id="4d356-133">まず、カメラ ビューに関する更新情報を保持する、便利なフィールドをいくつか定義します。</span><span class="sxs-lookup"><span data-stu-id="4d356-133">First, we define some useful fields that hold our updated info about our camera view.</span></span>

-   <span data-ttu-id="4d356-134">**m\_位置**カメラ (およびそのため、viewplane) 3 D のシーンでシーンの座標を使用しての位置です。</span><span class="sxs-lookup"><span data-stu-id="4d356-134">**m\_position** is the position of the camera (and therefore the viewplane) in the 3D scene, using scene coordinates.</span></span>
-   <span data-ttu-id="4d356-135">**m\_ピッチ**カメラまたは上下回転 (ラジアン単位)、viewplane の x 軸の周りのピッチします。</span><span class="sxs-lookup"><span data-stu-id="4d356-135">**m\_pitch** is the pitch of the camera, or its up-down rotation around the viewplane's x-axis, in radians.</span></span>
-   <span data-ttu-id="4d356-136">**m\_ヨー**カメラまたは左から右回転 (ラジアン単位)、viewplane の y 軸の周りのヨーです。</span><span class="sxs-lookup"><span data-stu-id="4d356-136">**m\_yaw** is the yaw of the camera, or its left-right rotation around the viewplane's y-axis, in radians.</span></span>

<span data-ttu-id="4d356-137">次に、コントローラーの状態と位置に関する情報を格納するフィールドを定義してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4d356-137">Now, let's define the fields that we use to store info about the status and position of our controllers.</span></span> <span data-ttu-id="4d356-138">まず、タッチ ベースのムーブ コントローラーに必要なフィールドを定義します。</span><span class="sxs-lookup"><span data-stu-id="4d356-138">First, we'll define the fields we need for our touch-based move controller.</span></span> <span data-ttu-id="4d356-139">(ムーブ コントローラーのキーボード実装に関して特別必要なことはありません。</span><span class="sxs-lookup"><span data-stu-id="4d356-139">(There's nothing special needed for the keyboard implementation of the move controller.</span></span> <span data-ttu-id="4d356-140">キーボードのイベントと具体的なハンドラーについては先ほど説明しました。)</span><span class="sxs-lookup"><span data-stu-id="4d356-140">We just read keyboard events with specific handlers.)</span></span>

-   <span data-ttu-id="4d356-141">**m\_moveInUse**移動コント ローラーが使用中かどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="4d356-141">**m\_moveInUse** indicates whether the move controller is in use.</span></span>
-   <span data-ttu-id="4d356-142">**m\_movePointerID**現在移動ポインターの一意の ID です。</span><span class="sxs-lookup"><span data-stu-id="4d356-142">**m\_movePointerID** is the unique ID for the current move pointer.</span></span> <span data-ttu-id="4d356-143">これは、ポインターの ID 値を確認するときにルック ポインターとムーブ ポインターを区別するために使います。</span><span class="sxs-lookup"><span data-stu-id="4d356-143">We use it to differentiate between the look pointer and the move pointer when we check the pointer ID value.</span></span>
-   <span data-ttu-id="4d356-144">**m\_moveFirstDown** player コント ローラーのポインターの移動 領域がタッチされた最初の画面上のポイントです。</span><span class="sxs-lookup"><span data-stu-id="4d356-144">**m\_moveFirstDown** is the point on the screen where the player first touched the move controller pointer area.</span></span> <span data-ttu-id="4d356-145">この値は、小さな動きによってビューが不安定にならないようデッド ゾーンを設定するために後で使います。</span><span class="sxs-lookup"><span data-stu-id="4d356-145">We use this value later to set a dead zone to keep tiny movements from jittering the view.</span></span>
-   <span data-ttu-id="4d356-146">**m\_movePointerPosition**は、プレーヤーがへのポインターを移動して現在の画面上のポイント。</span><span class="sxs-lookup"><span data-stu-id="4d356-146">**m\_movePointerPosition** is the point on the screen the player has currently moved the pointer to.</span></span> <span data-ttu-id="4d356-147">プレーヤーを基準とすることを調べることで移行したい方向を判断するために使用**m\_moveFirstDown**します。</span><span class="sxs-lookup"><span data-stu-id="4d356-147">We use it to determine what direction the player wanted to move by examining it relative to **m\_moveFirstDown**.</span></span>
-   <span data-ttu-id="4d356-148">**m\_moveCommand**移動コント ローラーの計算された最後のコマンドは、: (進む)、上下 (戻る)、left または right。</span><span class="sxs-lookup"><span data-stu-id="4d356-148">**m\_moveCommand** is the final computed command for the move controller: up (forward), down (back), left, or right.</span></span>

<span data-ttu-id="4d356-149">次に、ルック コントローラーに使うフィールドを、マウス実装とタッチ実装の両方に対して定義します。</span><span class="sxs-lookup"><span data-stu-id="4d356-149">Now, we define the fields we use for our look controller, both the mouse and touch implementations.</span></span>

-   <span data-ttu-id="4d356-150">**m\_lookInUse**検索コントロールが使用中かどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="4d356-150">**m\_lookInUse** indicates whether the look control is in use.</span></span>
-   <span data-ttu-id="4d356-151">**m\_lookPointerID**現在参照ポインターの一意の ID です。</span><span class="sxs-lookup"><span data-stu-id="4d356-151">**m\_lookPointerID** is the unique ID for the current look pointer.</span></span> <span data-ttu-id="4d356-152">これは、ポインターの ID 値を確認するときにルック ポインターとムーブ ポインターを区別するために使います。</span><span class="sxs-lookup"><span data-stu-id="4d356-152">We use it to differentiate between the look pointer and the move pointer when we check the pointer ID value.</span></span>
-   <span data-ttu-id="4d356-153">**m\_lookLastPoint**は最後のポイント、シーンの座標の前のフレームのキャプチャされました。</span><span class="sxs-lookup"><span data-stu-id="4d356-153">**m\_lookLastPoint** is the last point, in scene coordinates, that was captured in the previous frame.</span></span>
-   <span data-ttu-id="4d356-154">**m\_lookLastDelta**計算の現在の違いは、 **m\_位置**と**m\_lookLastPoint**します。</span><span class="sxs-lookup"><span data-stu-id="4d356-154">**m\_lookLastDelta** is the computed difference between the current **m\_position** and **m\_lookLastPoint**.</span></span>

<span data-ttu-id="4d356-155">最後に、6 段階の動きに対して次の 6 つのブール値を定義します。これらの値は、それぞれの方向移動操作の現在の状態 (オンまたはオフ) を示すために使います。</span><span class="sxs-lookup"><span data-stu-id="4d356-155">Finally, we define 6 Boolean values for the 6 degrees of movement, which we use to indicate the current state of each directional move action (on or off):</span></span>

-   <span data-ttu-id="4d356-156">**m\_フォワード**、 **m\_戻る**、 **m\_左**、 **m\_右**、 **m\_を**と**m\_ダウン**します。</span><span class="sxs-lookup"><span data-stu-id="4d356-156">**m\_forward**, **m\_back**, **m\_left**, **m\_right**, **m\_up** and **m\_down**.</span></span>

<span data-ttu-id="4d356-157">これら 6 つのイベント ハンドラーを使って、次のコントローラーの状態を更新するための入力データをキャプチャします。</span><span class="sxs-lookup"><span data-stu-id="4d356-157">We use the 6 event handlers to capture the input data we use to update the state of our controllers:</span></span>

-   <span data-ttu-id="4d356-158">**OnPointerPressed**。</span><span class="sxs-lookup"><span data-stu-id="4d356-158">**OnPointerPressed**.</span></span> <span data-ttu-id="4d356-159">プレイヤーが、ポインターがゲーム画面にある状態でマウスの左ボタンを押したか、画面にタッチしました。</span><span class="sxs-lookup"><span data-stu-id="4d356-159">The player pressed the left mouse button with the pointer in our game screen, or touched the screen.</span></span>
-   <span data-ttu-id="4d356-160">**OnPointerMoved**。</span><span class="sxs-lookup"><span data-stu-id="4d356-160">**OnPointerMoved**.</span></span> <span data-ttu-id="4d356-161">プレイヤーが、ポインターがゲーム画面にある状態でマウスを動かしたか、画面上でタッチ ポインターをドラッグしました。</span><span class="sxs-lookup"><span data-stu-id="4d356-161">The player moved the mouse with the pointer in our game screen, or dragged the touch pointer on the screen.</span></span>
-   <span data-ttu-id="4d356-162">**OnPointerReleased**。</span><span class="sxs-lookup"><span data-stu-id="4d356-162">**OnPointerReleased**.</span></span> <span data-ttu-id="4d356-163">プレイヤーが、ポインターがゲーム画面にある状態でマウスの左ボタンを離したか、画面から手を離しました。</span><span class="sxs-lookup"><span data-stu-id="4d356-163">The player released the left mouse button with the pointer in our game screen, or stopped touching the screen.</span></span>
-   <span data-ttu-id="4d356-164">**OnKeyDown**。</span><span class="sxs-lookup"><span data-stu-id="4d356-164">**OnKeyDown**.</span></span> <span data-ttu-id="4d356-165">プレイヤーがキーを押しました。</span><span class="sxs-lookup"><span data-stu-id="4d356-165">The player pressed a key.</span></span>
-   <span data-ttu-id="4d356-166">**OnKeyUp**。</span><span class="sxs-lookup"><span data-stu-id="4d356-166">**OnKeyUp**.</span></span> <span data-ttu-id="4d356-167">プレイヤーがキーを離しました。</span><span class="sxs-lookup"><span data-stu-id="4d356-167">The player released a key.</span></span>

<span data-ttu-id="4d356-168">最後に、次のメソッドとプロパティを使って、コントローラーの状態情報の初期化、アクセス、更新を行います。</span><span class="sxs-lookup"><span data-stu-id="4d356-168">And finally, we use these methods and properties to initialize, access, and update the controllers' state info.</span></span>

-   <span data-ttu-id="4d356-169">**Initialize**。</span><span class="sxs-lookup"><span data-stu-id="4d356-169">**Initialize**.</span></span> <span data-ttu-id="4d356-170">Windows ストア アプリは、コントロールを初期化して、表示ウィンドウを定義する [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) オブジェクトにそれらのコントロールを適用するときに、このイベント ハンドラーを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4d356-170">Our app calls this event handler to initialize the controls and attach them to the [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) object that describes our display window.</span></span>
-   <span data-ttu-id="4d356-171">**SetPosition**。</span><span class="sxs-lookup"><span data-stu-id="4d356-171">**SetPosition**.</span></span> <span data-ttu-id="4d356-172">Windows ストア アプリは、シーン空間内のコントロールの (x、y、z) 座標を設定するときに、このメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4d356-172">Our app calls this method to set the (x, y, and z) coordinates of our controls in the scene space.</span></span>
-   <span data-ttu-id="4d356-173">**SetOrientation**。</span><span class="sxs-lookup"><span data-stu-id="4d356-173">**SetOrientation**.</span></span> <span data-ttu-id="4d356-174">Windows ストア アプリは、カメラのピッチとヨーを設定するときに、このメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4d356-174">Our app calls this method to set the pitch and yaw of the camera.</span></span>
-   <span data-ttu-id="4d356-175">**取得\_位置**します。</span><span class="sxs-lookup"><span data-stu-id="4d356-175">**get\_Position**.</span></span> <span data-ttu-id="4d356-176">Windows ストア アプリは、シーン空間内のカメラの現在の位置を取得するときに、このプロパティにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="4d356-176">Our app accesses this property to get the current position of the camera in the scene space.</span></span> <span data-ttu-id="4d356-177">このプロパティは、カメラの現在の位置をアプリに伝える手段として使います。</span><span class="sxs-lookup"><span data-stu-id="4d356-177">You use this property as the method of communicating the current camera position to the app.</span></span>
-   <span data-ttu-id="4d356-178">**取得\_LookPoint**します。</span><span class="sxs-lookup"><span data-stu-id="4d356-178">**get\_LookPoint**.</span></span> <span data-ttu-id="4d356-179">Windows ストア アプリは、現在コントローラーのカメラが向いている点を取得するときに、このプロパティにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="4d356-179">Our app accesses this property to get the current point toward which the controller camera is facing.</span></span>
-   <span data-ttu-id="4d356-180">**更新プログラム**。</span><span class="sxs-lookup"><span data-stu-id="4d356-180">**Update**.</span></span> <span data-ttu-id="4d356-181">ムーブ コントローラーとルック コントローラーの状態を読み取り、カメラの位置を更新します。</span><span class="sxs-lookup"><span data-stu-id="4d356-181">Reads the state of the move and look controllers and updates the camera position.</span></span> <span data-ttu-id="4d356-182">このメソッドをアプリのメイン ループから継続的に呼び出して、カメラ コントローラーのデータとシーン空間内のカメラの位置を更新します。</span><span class="sxs-lookup"><span data-stu-id="4d356-182">You continually call this method from the app's main loop to refresh the camera controller data and the camera position in the scene space.</span></span>

<span data-ttu-id="4d356-183">これで、ムーブ/ルック コントロールの実装に必要なコンポーネントがすべて揃いました。</span><span class="sxs-lookup"><span data-stu-id="4d356-183">Now, you have here all the components you need to implement your move-look controls.</span></span> <span data-ttu-id="4d356-184">次は、これらのコンポーネントどうしを接続してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4d356-184">So, let's connect these pieces together.</span></span>

## <a name="create-the-basic-input-events"></a><span data-ttu-id="4d356-185">基本的な入力イベントを作成する</span><span class="sxs-lookup"><span data-stu-id="4d356-185">Create the basic input events</span></span>


<span data-ttu-id="4d356-186">Windows ランタイムのイベント ディスパッチャーは、**MoveLookController** クラスのインスタンスで処理するイベントを 5 つ提供します。</span><span class="sxs-lookup"><span data-stu-id="4d356-186">The Windows Runtime event dispatcher provides 5 events we want instances of the **MoveLookController** class to handle:</span></span>

-   [<span data-ttu-id="4d356-187">**PointerPressed**</span><span class="sxs-lookup"><span data-stu-id="4d356-187">**PointerPressed**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.pointerpressed)
-   [<span data-ttu-id="4d356-188">**PointerMoved**</span><span class="sxs-lookup"><span data-stu-id="4d356-188">**PointerMoved**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.pointermoved)
-   [<span data-ttu-id="4d356-189">**PointerReleased**</span><span class="sxs-lookup"><span data-stu-id="4d356-189">**PointerReleased**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.pointerreleased)
-   [<span data-ttu-id="4d356-190">**KeyUp**</span><span class="sxs-lookup"><span data-stu-id="4d356-190">**KeyUp**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.keyup)
-   [<span data-ttu-id="4d356-191">**KeyDown**</span><span class="sxs-lookup"><span data-stu-id="4d356-191">**KeyDown**</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.keydown)

<span data-ttu-id="4d356-192">これらのイベントは、[**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) 型に実装されています。</span><span class="sxs-lookup"><span data-stu-id="4d356-192">These events are implemented on the [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) type.</span></span> <span data-ttu-id="4d356-193">ここでは、操作する **CoreWindow** オブジェクトが既にあると想定しています。</span><span class="sxs-lookup"><span data-stu-id="4d356-193">We assume that you have a **CoreWindow** object to work with.</span></span> <span data-ttu-id="4d356-194">取得方法が不明な場合は、「[ユニバーサル Windows プラットフォーム (UWP) C++ アプリで DirectX ビューを表示するための設定方法](https://docs.microsoft.com/previous-versions/windows/apps/hh465077(v=win.10))」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4d356-194">If you don't know how to obtain one, see [How to set up your Universal Windows Platform (UWP) C++ app to display a DirectX view](https://docs.microsoft.com/previous-versions/windows/apps/hh465077(v=win.10)).</span></span>

<span data-ttu-id="4d356-195">これらのイベントは Windows ストア アプリの実行中に起動するため、ハンドラーはプライベート フィールドに定義されているコントローラーの状態情報を更新します。</span><span class="sxs-lookup"><span data-stu-id="4d356-195">As these events fire while our app is running, the handlers update the controllers' state info defined in our private fields.</span></span>

<span data-ttu-id="4d356-196">まず、マウス ポインターとタッチ ポインターのイベント ハンドラーを設定します。</span><span class="sxs-lookup"><span data-stu-id="4d356-196">First, let's populate the mouse and touch pointer event handlers.</span></span> <span data-ttu-id="4d356-197">最初のイベント ハンドラーである **OnPointerPressed()** では、ユーザーがルック コントローラー領域でマウスをクリックまたは画面をタッチすると、表示を管理する [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) からポインターの x-y 座標を取得します。</span><span class="sxs-lookup"><span data-stu-id="4d356-197">In the first event handler, **OnPointerPressed()**, we get the x-y coordinates of the pointer from the [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) that manages our display when the user clicks the mouse or touches the screen in the look controller region.</span></span>

<span data-ttu-id="4d356-198">**OnPointerPressed**</span><span class="sxs-lookup"><span data-stu-id="4d356-198">**OnPointerPressed**</span></span>

```cpp
void MoveLookController::OnPointerPressed(
_In_ CoreWindow^ sender,
_In_ PointerEventArgs^ args)
{
    // Get the current pointer position.
    uint32 pointerID = args->CurrentPoint->PointerId;
    DirectX::XMFLOAT2 position = DirectX::XMFLOAT2( args->CurrentPoint->Position.X, args->CurrentPoint->Position.Y );

    auto device = args->CurrentPoint->PointerDevice;
    auto deviceType = device->PointerDeviceType;
    if ( deviceType == PointerDeviceType::Mouse )
    {
        // Action, Jump, or Fire
    }

    // Check  if this pointer is in the move control.
    // Change the values  to percentages of the preferred screen resolution.
    // You can set the x value to <preferred resolution> * <percentage of width>
    // for example, ( position.x < (screenResolution.x * 0.15) ).

    if (( position.x < 300 && position.y > 380 ) && ( deviceType != PointerDeviceType::Mouse ))
    {
        if ( !m_moveInUse ) // if no pointer is in this control yet
        {
            // Process a DPad touch down event.
            m_moveFirstDown = position;                 // Save the location of the initial contact.
            m_movePointerPosition = position;
            m_movePointerID = pointerID;                // Store the id of the pointer using this control.
            m_moveInUse = TRUE;
        }
    }
    else // This pointer must be in the look control.
    {
        if ( !m_lookInUse ) // If no pointer is in this control yet...
        {
            m_lookLastPoint = position;                         // save the point for later move
            m_lookPointerID = args->CurrentPoint->PointerId;  // store the id of pointer using this control
            m_lookLastDelta.x = m_lookLastDelta.y = 0;          // these are for smoothing
            m_lookInUse = TRUE;
        }
    }
}
```

<span data-ttu-id="4d356-199">このイベント ハンドラーは、ポインターがマウスでないかどうか (このサンプルではマウスとタッチの両方をサポートするため) と、ムーブ コントローラー領域内にあるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="4d356-199">This event handler checks whether the pointer is not the mouse (for the purposes of this sample, which supports both mouse and touch) and if it is in the move controller area.</span></span> <span data-ttu-id="4d356-200">両方の条件が true の場合、チェックするかどうか、ポインターだけ、押された具体的には、これが関連付けられていないかどうかがある場合、前に移動または場合をテストして、入力、確認**m\_moveInUse**は false です。</span><span class="sxs-lookup"><span data-stu-id="4d356-200">If both criteria are true, it checks whether the pointer was just pressed, specifically, whether this click is unrelated to a previous move or look input, by testing if **m\_moveInUse** is false.</span></span> <span data-ttu-id="4d356-201">ハンドラーが、キーを押してが発生し、設定は、移動コント ローラーの領域内のポイントをキャプチャするため場合、 **m\_moveInUse** true、このハンドラーが再度呼び出されると、移動の開始位置が上書きされないようにするコント ローラーの入力対話します。</span><span class="sxs-lookup"><span data-stu-id="4d356-201">If so, the handler captures the point in the move controller area where the press happened and sets **m\_moveInUse** to true, so that when this handler is called again, it won't overwrite the start position of the move controller input interaction.</span></span> <span data-ttu-id="4d356-202">さらに、ムーブ コントローラーのポインター ID を現在のポインターの ID に更新します。</span><span class="sxs-lookup"><span data-stu-id="4d356-202">It also updates the move controller pointer ID to the current pointer's ID.</span></span>

<span data-ttu-id="4d356-203">ポインターがマウスの場合、またはタッチ ポインターがムーブ コントローラー領域内にない場合は、ルック コントローラー領域内にある必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d356-203">If the pointer is the mouse or if the touch pointer isn't in the move controller area, it must be in the look controller area.</span></span> <span data-ttu-id="4d356-204">設定**m\_lookLastPoint**を現在の位置、ユーザーの押されたマウス ボタンまたは操作された、押された、リセット、デルタと外観のコント ローラーのポインター ID をポインターの現在の ID に更新します。</span><span class="sxs-lookup"><span data-stu-id="4d356-204">It sets **m\_lookLastPoint** to the current position where the user pressed the mouse button or touched and pressed, resets the delta, and updates the look controller's pointer ID to the current pointer ID.</span></span> <span data-ttu-id="4d356-205">また、ルック コントローラーの状態をアクティブに設定します。</span><span class="sxs-lookup"><span data-stu-id="4d356-205">It also sets the state of the look controller to active.</span></span>

<span data-ttu-id="4d356-206">**OnPointerMoved**</span><span class="sxs-lookup"><span data-stu-id="4d356-206">**OnPointerMoved**</span></span>

```cpp
void MoveLookController::OnPointerMoved(
    _In_ CoreWindow ^sender,
    _In_ PointerEventArgs ^args)
{
    uint32 pointerID = args->CurrentPoint->PointerId;
    DirectX::XMFLOAT2 position = DirectX::XMFLOAT2(args->CurrentPoint->Position.X, args->CurrentPoint->Position.Y);

    // Decide which control this pointer is operating.
    if (pointerID == m_movePointerID)           // This is the move pointer.
    {
        // Move control
        m_movePointerPosition = position;       // Save the current position.

    }
    else if (pointerID == m_lookPointerID)      // This is the look pointer.
    {
        // Look control

        DirectX::XMFLOAT2 pointerDelta;
        pointerDelta.x = position.x - m_lookLastPoint.x;        // How far did pointer move
        pointerDelta.y = position.y - m_lookLastPoint.y;

        DirectX::XMFLOAT2 rotationDelta;
        rotationDelta.x = pointerDelta.x * ROTATION_GAIN;   // Scale for control sensitivity.
        rotationDelta.y = pointerDelta.y * ROTATION_GAIN;

        m_lookLastPoint = position;                     // Save for the next time through.

                                                        // Update our orientation based on the command.
        m_pitch -= rotationDelta.y;                     // Mouse y increases down, but pitch increases up.
        m_yaw -= rotationDelta.x;                       // Yaw is defined as CCW around the y-axis.

                                                        // Limit the pitch to straight up or straight down.
        m_pitch = (float)__max(-DirectX::XM_PI / 2.0f, m_pitch);
        m_pitch = (float)__min(+DirectX::XM_PI / 2.0f, m_pitch);
    }
}
```

<span data-ttu-id="4d356-207">**OnPointerMoved** イベント ハンドラーは、ポインターが動くたび起動します (この場合、タッチ スクリーンのポインターがドラッグされているとき、またはマウスの左ボタンを押しながらマウス ポインターが動かされているとき)。</span><span class="sxs-lookup"><span data-stu-id="4d356-207">The **OnPointerMoved** event handler fires whenever the pointer moves (in this case, if a touch screen pointer is being dragged, or if the mouse pointer is being moved while the left button is pressed).</span></span> <span data-ttu-id="4d356-208">ポインター ID がムーブ コントローラーのポインターの ID と同じ場合は、ムーブ ポインターになります。違う場合は、アクティブなポインターであるルック コントローラーかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="4d356-208">If the pointer ID is the same as the move controller pointer's ID, then it's the move pointer; otherwise, we check if it's the look controller that's the active pointer.</span></span>

<span data-ttu-id="4d356-209">ムーブ コントローラーの場合は、単にポインターの位置を更新します。</span><span class="sxs-lookup"><span data-stu-id="4d356-209">If it's the move controller, we just update the pointer position.</span></span> <span data-ttu-id="4d356-210">**OnPointerPressed** イベント ハンドラーでキャプチャした最初の位置と最後の位置を比較するため、[**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.pointermoved) イベントが起動を続ける限りポインターの位置を更新し続けます。</span><span class="sxs-lookup"><span data-stu-id="4d356-210">We keep updating it as long the [**PointerMoved**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.pointermoved) event keeps firing, because we want to compare the final position with the first one we captured with the **OnPointerPressed** event handler.</span></span>

<span data-ttu-id="4d356-211">ルック コントローラーの場合は、やや複雑になります。</span><span class="sxs-lookup"><span data-stu-id="4d356-211">If it's the look controller, things are a little more complicated.</span></span> <span data-ttu-id="4d356-212">新しい視点を計算してカメラの中心をそこに合わせ、前の視点と現在の画面の位置との差分を計算する必要があります。その後、倍率を乗算します。倍率を調整すると、画面移動の距離に比例して動きが小さくまたは大きく見えるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="4d356-212">We need to calculate a new look point and center the camera on it, so we calculate the delta between the last look point and the current screen position, and then we multiply versus our scale factor, which we can tweak to make the look movements smaller or larger relative to the distance of the screen movement.</span></span> <span data-ttu-id="4d356-213">その値を使って、ピッチとヨーを計算します。</span><span class="sxs-lookup"><span data-stu-id="4d356-213">Using that value, we calculate the pitch and the yaw.</span></span>

<span data-ttu-id="4d356-214">最後に、プレイヤーがマウスの移動を停止したとき、または画面から手を離したときに、ムーブ コントローラーまたはルック コントローラーの動作を非アクティブにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d356-214">Finally, we need to deactivate the move or look controller behaviors when the player stops moving the mouse or touching the screen.</span></span> <span data-ttu-id="4d356-215">使用して**OnPointerReleased**、ときと呼ばれる[ **PointerReleased** ](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.pointerreleased)を設定する発生した**m\_moveInUse**または**m\_lookInUse**を FALSE にカメラのパンの動きをオフにして、ポインター ID をゼロにする</span><span class="sxs-lookup"><span data-stu-id="4d356-215">We use **OnPointerReleased**, which we call when [**PointerReleased**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.pointerreleased) is fired, to set **m\_moveInUse** or **m\_lookInUse** to FALSE and turn off the camera pan movement, and to zero out the pointer ID.</span></span>

<span data-ttu-id="4d356-216">**OnPointerReleased**</span><span class="sxs-lookup"><span data-stu-id="4d356-216">**OnPointerReleased**</span></span>

```cpp
void MoveLookController::OnPointerReleased(
_In_ CoreWindow ^sender,
_In_ PointerEventArgs ^args)
{
    uint32 pointerID = args->CurrentPoint->PointerId;
    DirectX::XMFLOAT2 position = DirectX::XMFLOAT2( args->CurrentPoint->Position.X, args->CurrentPoint->Position.Y );


    if ( pointerID == m_movePointerID )    // This was the move pointer.
    {
        m_moveInUse = FALSE;
        m_movePointerID = 0;
    }
    else if (pointerID == m_lookPointerID ) // This was the look pointer.
    {
        m_lookInUse = FALSE;
        m_lookPointerID = 0;
    }
}
```

<span data-ttu-id="4d356-217">今まで処理したのは、すべてタッチ スクリーン イベントでした。</span><span class="sxs-lookup"><span data-stu-id="4d356-217">So far, we handled all the touch screen events.</span></span> <span data-ttu-id="4d356-218">次は、キーボード ベースのムーブ コントローラー用のキー入力イベントを処理しましょう。</span><span class="sxs-lookup"><span data-stu-id="4d356-218">Now, let's handle the key input events for a keyboard-based move controller.</span></span>

<span data-ttu-id="4d356-219">**OnKeyDown**</span><span class="sxs-lookup"><span data-stu-id="4d356-219">**OnKeyDown**</span></span>

```cpp
void MoveLookController::OnKeyDown(
                                   __in CoreWindow^ sender,
                                   __in KeyEventArgs^ args )
{
    Windows::System::VirtualKey Key;
    Key = args->VirtualKey;

    // Figure out the command from the keyboard.
    if ( Key == VirtualKey::W )     // Forward
        m_forward = true;
    if ( Key == VirtualKey::S )     // Back
        m_back = true;
    if ( Key == VirtualKey::A )     // Left
        m_left = true;
    if ( Key == VirtualKey::D )     // Right
        m_right = true;
}
```

<span data-ttu-id="4d356-220">これらのキーのいずれかが押されている限り、このイベント ハンドラーは対応する方向移動状態を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="4d356-220">As long as one of these keys is pressed, this event handler sets the corresponding directional move state to true.</span></span>

<span data-ttu-id="4d356-221">**OnKeyUp**</span><span class="sxs-lookup"><span data-stu-id="4d356-221">**OnKeyUp**</span></span>

```cpp
void MoveLookController::OnKeyUp(
                                 __in CoreWindow^ sender,
                                 __in KeyEventArgs^ args)
{
    Windows::System::VirtualKey Key;
    Key = args->VirtualKey;

    // Figure out the command from the keyboard.
    if ( Key == VirtualKey::W )     // forward
        m_forward = false;
    if ( Key == VirtualKey::S )     // back
        m_back = false;
    if ( Key == VirtualKey::A )     // left
        m_left = false;
    if ( Key == VirtualKey::D )     // right
        m_right = false;
}
```

<span data-ttu-id="4d356-222">キーが離されると、状態を false にリセットします。</span><span class="sxs-lookup"><span data-stu-id="4d356-222">And when the key is released, this event handler sets it back to false.</span></span> <span data-ttu-id="4d356-223">**Update** を呼び出すと、これらの方向移動状態が確認され、それに従ってカメラが動きます。</span><span class="sxs-lookup"><span data-stu-id="4d356-223">When we call **Update**, it checks these directional move states, and move the camera accordingly.</span></span> <span data-ttu-id="4d356-224">これは、タッチ実装より少し簡単です。</span><span class="sxs-lookup"><span data-stu-id="4d356-224">This is a bit simpler than the touch implementation!</span></span>

## <a name="initialize-the-touch-controls-and-the-controller-state"></a><span data-ttu-id="4d356-225">タッチ コントロールとコントローラーの状態の初期化</span><span class="sxs-lookup"><span data-stu-id="4d356-225">Initialize the touch controls and the controller state</span></span>


<span data-ttu-id="4d356-226">次は、イベントをフックして、コントローラー状態の全フィールドを初期化しましょう。</span><span class="sxs-lookup"><span data-stu-id="4d356-226">Let's hook up the events now, and initialize all the controller state fields.</span></span>

<span data-ttu-id="4d356-227">**初期化します。**</span><span class="sxs-lookup"><span data-stu-id="4d356-227">**Initialize**</span></span>

```cpp
void MoveLookController::Initialize( _In_ CoreWindow^ window )
{

    // Opt in to receive touch/mouse events.
    window->PointerPressed += 
    ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &MoveLookController::OnPointerPressed);

    window->PointerMoved += 
    ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &MoveLookController::OnPointerMoved);

    window->PointerReleased += 
    ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &MoveLookController::OnPointerReleased);

    window->CharacterReceived +=
    ref new TypedEventHandler<CoreWindow^, CharacterReceivedEventArgs^>(this, &MoveLookController::OnCharacterReceived);

    window->KeyDown += 
    ref new TypedEventHandler<CoreWindow^, KeyEventArgs^>(this, &MoveLookController::OnKeyDown);

    window->KeyUp += 
    ref new TypedEventHandler<CoreWindow^, KeyEventArgs^>(this, &MoveLookController::OnKeyUp);

    // Initialize the state of the controller.
    m_moveInUse = FALSE;                // No pointer is in the Move control.
    m_movePointerID = 0;

    m_lookInUse = FALSE;                // No pointer is in the Look control.
    m_lookPointerID = 0;

    //  Need to init this as it is reset every frame.
    m_moveCommand = DirectX::XMFLOAT3( 0.0f, 0.0f, 0.0f );

    SetOrientation( 0, 0 );             // Look straight ahead when the app starts.

}
```

<span data-ttu-id="4d356-228">**Initialize** は、アプリの [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) インスタンスへの参照をパラメーターとして使い、先ほど作成したイベント ハンドラーをその **CoreWindow** の適切なイベントに登録します。</span><span class="sxs-lookup"><span data-stu-id="4d356-228">**Initialize** takes a reference to the app's [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) instance as a parameter and registers the event handlers we developed to the appropriate events on that **CoreWindow**.</span></span> <span data-ttu-id="4d356-229">このハンドラーは、ムーブ ポインターとルック ポインターの ID を初期化し、タッチ スクリーンのムーブ コントローラー実装用のコマンド ベクターをゼロに設定して、アプリの起動時にカメラが正面を向くように設定します。</span><span class="sxs-lookup"><span data-stu-id="4d356-229">It initializes the move and look pointer's IDs, sets the command vector for our touch screen move controller implementation to zero, and sets the camera looking straight ahead when the app starts.</span></span>

## <a name="getting-and-setting-the-position-and-orientation-of-the-camera"></a><span data-ttu-id="4d356-230">カメラの位置と向きの取得と設定</span><span class="sxs-lookup"><span data-stu-id="4d356-230">Getting and setting the position and orientation of the camera</span></span>


<span data-ttu-id="4d356-231">ビューポートに対してカメラの位置の取得と設定を行うメソッドをいくつか定義してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4d356-231">Let's define some methods to get and set the position of the camera with respect to the viewport.</span></span>

```cpp
void MoveLookController::SetPosition( _In_ DirectX::XMFLOAT3 pos )
{
    m_position = pos;
}

// Accessor to set the position of the controller.
void MoveLookController::SetOrientation( _In_ float pitch, _In_ float yaw )
{
    m_pitch = pitch;
    m_yaw = yaw;
}

// Returns the position of the controller object.
DirectX::XMFLOAT3 MoveLookController::get_Position()
{
    return m_position;
}

// Returns the point at which the camera controller is facing.
DirectX::XMFLOAT3 MoveLookController::get_LookPoint()
{
    float y = sinf(m_pitch);        // Vertical
    float r = cosf(m_pitch);        // In the plane
    float z = r*cosf(m_yaw);        // Fwd-back
    float x = r*sinf(m_yaw);        // Left-right
    DirectX::XMFLOAT3 result(x,y,z);
    result.x += m_position.x;
    result.y += m_position.y;
    result.z += m_position.z;

    // Return m_position + DirectX::XMFLOAT3(x, y, z);
    return result;
}
```

## <a name="updating-the-controller-state-info"></a><span data-ttu-id="4d356-232">コントローラーの状態情報の更新</span><span class="sxs-lookup"><span data-stu-id="4d356-232">Updating the controller state info</span></span>


<span data-ttu-id="4d356-233">追跡するポインターの座標情報に変換する計算は、実行、 **m\_movePointerPosition**新しい座標それぞれの情報、ワールド座標系にします。</span><span class="sxs-lookup"><span data-stu-id="4d356-233">Now, we perform our calculations that convert the pointer coordinate info tracked in **m\_movePointerPosition** into new coordinate information respective of our world coordinate system.</span></span> <span data-ttu-id="4d356-234">Windows ストア アプリは、アプリのメイン ループが更新されるたびに、このメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="4d356-234">Our app calls this method every time we refresh the main app loop.</span></span> <span data-ttu-id="4d356-235">このため、ビュー マトリックスをビューポートへのプロジェクションの前に更新するためにアプリに渡す新しい視点位置情報は、ここで計算します。</span><span class="sxs-lookup"><span data-stu-id="4d356-235">So, it is here that we compute the new look point position info we want to pass to the app for updating the view matrix before projection into the viewport.</span></span>

```cpp
void MoveLookController::Update(CoreWindow ^window)
{
    // Check for input from the Move control.
    if (m_moveInUse)
    {
        DirectX::XMFLOAT2 pointerDelta(m_movePointerPosition);
        pointerDelta.x -= m_moveFirstDown.x;
        pointerDelta.y -= m_moveFirstDown.y;

        // Figure out the command from the touch-based virtual joystick.
        if (pointerDelta.x > 16.0f)      // Leave 32 pixel-wide dead spot for being still.
            m_moveCommand.x = 1.0f;
        else
            if (pointerDelta.x < -16.0f)
            m_moveCommand.x = -1.0f;

        if (pointerDelta.y > 16.0f)      // Joystick y is up, so change sign.
            m_moveCommand.y = -1.0f;
        else
            if (pointerDelta.y < -16.0f)
            m_moveCommand.y = 1.0f;
    }

    // Poll our state bits that are set by the keyboard input events.
    if (m_forward)
        m_moveCommand.y += 1.0f;
    if (m_back)
        m_moveCommand.y -= 1.0f;

    if (m_left)
        m_moveCommand.x -= 1.0f;
    if (m_right)
        m_moveCommand.x += 1.0f;

    if (m_up)
        m_moveCommand.z += 1.0f;
    if (m_down)
        m_moveCommand.z -= 1.0f;

    // Make sure that 45 degree cases are not faster.
    DirectX::XMFLOAT3 command = m_moveCommand;
    DirectX::XMVECTOR vector;
    vector = DirectX::XMLoadFloat3(&command);

    if (fabsf(command.x) > 0.1f || fabsf(command.y) > 0.1f || fabsf(command.z) > 0.1f)
    {
        vector = DirectX::XMVector3Normalize(vector);
        DirectX::XMStoreFloat3(&command, vector);
    }
    

    // Rotate command to align with our direction (world coordinates).
    DirectX::XMFLOAT3 wCommand;
    wCommand.x = command.x*cosf(m_yaw) - command.y*sinf(m_yaw);
    wCommand.y = command.x*sinf(m_yaw) + command.y*cosf(m_yaw);
    wCommand.z = command.z;

    // Scale for sensitivity adjustment.
    wCommand.x = wCommand.x * MOVEMENT_GAIN;
    wCommand.y = wCommand.y * MOVEMENT_GAIN;
    wCommand.z = wCommand.z * MOVEMENT_GAIN;

    // Our velocity is based on the command.
    // Also note that y is the up-down axis. 
    DirectX::XMFLOAT3 Velocity;
    Velocity.x = -wCommand.x;
    Velocity.z = wCommand.y;
    Velocity.y = wCommand.z;

    // Integrate
    m_position.x += Velocity.x;
    m_position.y += Velocity.y;
    m_position.z += Velocity.z;

    // Clear movement input accumulator for use during the next frame.
    m_moveCommand = DirectX::XMFLOAT3(0.0f, 0.0f, 0.0f);

}
```

<span data-ttu-id="4d356-236">プレイヤーがタッチ ベースのムーブ コントローラーを使う場合に動きが不安定にならないように、ポインターの周りに直径 32 ピクセルの仮想デッド ゾーンを設定します。</span><span class="sxs-lookup"><span data-stu-id="4d356-236">Because we don't want jittery movement when the player uses our touch-based move controller, we set a virtual dead zone around the pointer with a diameter of 32 pixels.</span></span> <span data-ttu-id="4d356-237">また、コマンド値に移動ゲイン速度を加えた速度も追加します </span><span class="sxs-lookup"><span data-stu-id="4d356-237">We also add velocity, which is the command value plus a movement gain rate.</span></span> <span data-ttu-id="4d356-238">(この動作は、ポインターがムーブ コントローラー領域内で動く距離に基づいて移動速度を低下または上昇させることができるように、任意に調整できます。)</span><span class="sxs-lookup"><span data-stu-id="4d356-238">(You can adjust this behavior to your liking, to slow down or speed up the rate of movement based on the distance the pointer moves in the move controller area.)</span></span>

<span data-ttu-id="4d356-239">速度を計算するときは、さらに、ムーブ コントローラーとルック コントローラーから受け取った座標を、シーンのビュー マトリックスを計算するメソッドに送信する実際の視点の動きに変換します。</span><span class="sxs-lookup"><span data-stu-id="4d356-239">When we compute the velocity, we also translate the coordinates received from the move and look controllers into the movement of the actual look point we send to the method that computes our view matrix for the scene.</span></span> <span data-ttu-id="4d356-240">まず、x 座標を反転します。これは、ルック コントローラーで、クリックしてから左または右方向への移動またはドラッグを行うと、カメラがその中心軸の周囲でスイングするように視点がシーン内で反対方向に回転するためです。</span><span class="sxs-lookup"><span data-stu-id="4d356-240">First, we invert the x coordinate, because if we click-move or drag left or right with the look controller, the look point rotates in the opposite direction in the scene, as a camera might swing about its central axis.</span></span> <span data-ttu-id="4d356-241">次に、y 軸と z 軸を入れ替えます。これは、ムーブ コントローラーで、上/下方向キーを押す、またはタッチ ドラッグ動作 (y 軸動作として読み取られます) を行うと、視点を画面 (z 軸) の中に、または外へ動かすカメラ操作が行われるためです。</span><span class="sxs-lookup"><span data-stu-id="4d356-241">Then, we swap the y and z axes, because an up/down key press or touch drag motion (read as a y-axis behavior) on the move controller should translate into a camera action that moves the look point into or out of the screen (the z-axis).</span></span>

<span data-ttu-id="4d356-242">プレーヤーの外観のポイントの最後の位置は最後の位置と計算速度、あり、これを呼び出すときに、レンダラーによって読み取り対象、**取得\_位置**(多くの場合のそれぞれのセットアップ中にメソッドフレーム)。</span><span class="sxs-lookup"><span data-stu-id="4d356-242">The final position of the look point for the player is the last position plus the calculated velocity, and this is what is read by the renderer when it calls the **get\_Position** method (most likely during the setup for each frame).</span></span> <span data-ttu-id="4d356-243">その後、移動コマンドをゼロにリセットします。</span><span class="sxs-lookup"><span data-stu-id="4d356-243">After that, we reset the move command to zero.</span></span>

## <a name="updating-the-view-matrix-with-the-new-camera-position"></a><span data-ttu-id="4d356-244">カメラの新しい位置によるビュー マトリックスの更新</span><span class="sxs-lookup"><span data-stu-id="4d356-244">Updating the view matrix with the new camera position</span></span>


<span data-ttu-id="4d356-245">カメラのフォーカスが合っているシーン空間の座標を取得できます。この座標は、アプリに指定した時間ごとに更新されます (たとえばアプリのメイン ループでは 60 秒ごと)。</span><span class="sxs-lookup"><span data-stu-id="4d356-245">We can obtain a scene space coordinate that our camera is focused on, and which is updated whenever you tell your app to do so (every 60 seconds in the main app loop, for example).</span></span> <span data-ttu-id="4d356-246">次の疑似コードは、実装できる呼び出し動作を示しています。</span><span class="sxs-lookup"><span data-stu-id="4d356-246">This pseudocode suggests the calling behavior you can implement:</span></span>

```cpp
myMoveLookController->Update( m_window );   

// Update the view matrix based on the camera position.
myFirstPersonCamera->SetViewParameters(
                 myMoveLookController->get_Position(),       // Point we are at
                 myMoveLookController->get_LookPoint(),      // Point to look towards
                 DirectX::XMFLOAT3( 0, 1, 0 )                   // Up-vector
                 ); 
```

<span data-ttu-id="4d356-247">これで終了です。</span><span class="sxs-lookup"><span data-stu-id="4d356-247">Congratulations!</span></span> <span data-ttu-id="4d356-248">タッチ スクリーン用とキーボード/マウス用の入力タッチ コントロールの両方の基本的なムーブ/ルック コントロールがゲームで実装されました。</span><span class="sxs-lookup"><span data-stu-id="4d356-248">You've implemented basic move-look controls for both touch screens and keyboard/mouse input touch controls in your game!</span></span>



 

 




