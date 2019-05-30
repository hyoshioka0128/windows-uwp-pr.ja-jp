---
title: スマート カード
description: このトピックでは、ユニバーサル Windows プラットフォーム (UWP) アプリでスマート カードを使ってユーザーをセキュリティで保護されたネットワーク サービスに接続する方法のほか、物理スマート カード リーダーにアクセスする方法、仮想スマート カードの作成方法、スマート カードとの通信方法、ユーザーの認証方法、ユーザーの PIN のリセット方法、スマート カードの取り外しや切断の方法などについて説明します。
ms.assetid: 86524267-50A0-4567-AE17-35C4B6D24745
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp, セキュリティ
ms.localizationpriority: medium
ms.openlocfilehash: 5498480e0dbe2c8be96d92df766b15676a3e6b7b
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371934"
---
# <a name="smart-cards"></a><span data-ttu-id="e9230-104">スマート カード</span><span class="sxs-lookup"><span data-stu-id="e9230-104">Smart cards</span></span>




<span data-ttu-id="e9230-105">このトピックでは、ユニバーサル Windows プラットフォーム (UWP) アプリでスマート カードを使ってユーザーをセキュリティで保護されたネットワーク サービスに接続する方法のほか、物理スマート カード リーダーにアクセスする方法、仮想スマート カードの作成方法、スマート カードとの通信方法、ユーザーの認証方法、ユーザーの PIN のリセット方法、スマート カードの取り外しや切断の方法などについて説明します。</span><span class="sxs-lookup"><span data-stu-id="e9230-105">This topic explains how Universal Windows Platform (UWP) apps can use smart cards to connect users to secure network services, including how to access physical smart card readers, create virtual smart cards, communicate with smart cards, authenticate users, reset user PINs, and remove or disconnect smart cards.</span></span> 

## <a name="configure-the-app-manifest"></a><span data-ttu-id="e9230-106">アプリ マニフェストの構成</span><span class="sxs-lookup"><span data-stu-id="e9230-106">Configure the app manifest</span></span>


<span data-ttu-id="e9230-107">アプリでスマート カードや仮想スマート カードを使ってユーザーを認証するには、あらかじめプロジェクトの Package.appxmanifest ファイルで、**共有ユーザー証明書**機能を設定しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9230-107">Before your app can authenticate users using smart cards or virtual smart cards, you must set the **Shared User Certificates** capability in the project Package.appxmanifest file.</span></span>

## <a name="access-connected-card-readers-and-smart-cards"></a><span data-ttu-id="e9230-108">接続されているカード リーダーとスマート カードへのアクセス</span><span class="sxs-lookup"><span data-stu-id="e9230-108">Access connected card readers and smart cards</span></span>


<span data-ttu-id="e9230-109">[  **DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation) に指定されているデバイス ID を [**SmartCardReader.FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.fromidasync) メソッドに渡すと、リーダーや装着されているスマート カードを照会することができます。</span><span class="sxs-lookup"><span data-stu-id="e9230-109">You can query for readers and attached smart cards by passing the device ID (specified in [**DeviceInformation**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation)) to the [**SmartCardReader.FromIdAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.fromidasync) method.</span></span> <span data-ttu-id="e9230-110">返されたリーダー デバイスに現在装着されているスマート カードにアクセスするには、[**SmartCardReader.FindAllCardsAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.findallcardsasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e9230-110">To access the smart cards currently attached to the returned reader device, call [**SmartCardReader.FindAllCardsAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.findallcardsasync).</span></span>

```cs
string selector = SmartCardReader.GetDeviceSelector();
DeviceInformationCollection devices =
    await DeviceInformation.FindAllAsync(selector);

foreach (DeviceInformation device in devices)
{
    SmartCardReader reader =
        await SmartCardReader.FromIdAsync(device.Id);

    // For each reader, we want to find all the cards associated
    // with it.  Then we will create a SmartCardListItem for
    // each (reader, card) pair.
    IReadOnlyList<SmartCard> cards =
        await reader.FindAllCardsAsync();
}
```

<span data-ttu-id="e9230-111">また、カードが挿入されたときのアプリの動作を処理するメソッドを実装して、アプリによる [**CardAdded**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.cardadded) イベントの監視を有効にする必要もあります。</span><span class="sxs-lookup"><span data-stu-id="e9230-111">You should also enable your app to observe for [**CardAdded**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.cardadded) events by implementing a method to handle app behavior on card insertion.</span></span>

```cs
private void reader_CardAdded(SmartCardReader sender, CardAddedEventArgs args)
{
  // A card has been inserted into the sender SmartCardReader.
}
```

<span data-ttu-id="e9230-112">その後、返された各 [**SmartCard**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCard) オブジェクトを [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) に渡すことで、その構成へのアクセスやカスタマイズを行うメソッドを使えるようになります。</span><span class="sxs-lookup"><span data-stu-id="e9230-112">You can then pass each returned [**SmartCard**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCard) object to [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) to access the methods that allow your app to access and customize its configuration.</span></span>

## <a name="create-a-virtual-smart-card"></a><span data-ttu-id="e9230-113">仮想スマート カードの作成</span><span class="sxs-lookup"><span data-stu-id="e9230-113">Create a virtual smart card</span></span>


<span data-ttu-id="e9230-114">アプリで [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) を使って仮想スマート カードを作成するには、まずフレンドリ名、管理者キー、[**SmartCardPinPolicy**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardPinPolicy) を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9230-114">To create a virtual smart card using [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning), your app will first need to provide a friendly name, an admin key, and a [**SmartCardPinPolicy**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardPinPolicy).</span></span> <span data-ttu-id="e9230-115">通常、フレンドリ名は既にアプリに用意されている可能性がありますが、アプリではさらに、管理者キーを提供し、現在の **SmartCardPinPolicy** のインスタンスを生成する必要があります。その後、これらの 3 つの値をすべて [**RequestVirtualSmartCardCreationAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcardcreationasync) に渡します。</span><span class="sxs-lookup"><span data-stu-id="e9230-115">The friendly name is generally something provided to the app, but your app will still need to provide an admin key and generate an instance of the current **SmartCardPinPolicy** before passing all three values to [**RequestVirtualSmartCardCreationAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcardcreationasync).</span></span>

1.  <span data-ttu-id="e9230-116">[  **SmartCardPinPolicy**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardPinPolicy) の新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e9230-116">Create a new instance of a [**SmartCardPinPolicy**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardPinPolicy)</span></span>
2.  <span data-ttu-id="e9230-117">サービスまたは管理ツールから提供された管理者キーの値に対して [**CryptographicBuffer.GenerateRandom**](https://docs.microsoft.com/uwp/api/windows.security.cryptography.cryptographicbuffer.generaterandom) を呼び出して、管理者キーの値を生成します。</span><span class="sxs-lookup"><span data-stu-id="e9230-117">Generate the admin key value by calling [**CryptographicBuffer.GenerateRandom**](https://docs.microsoft.com/uwp/api/windows.security.cryptography.cryptographicbuffer.generaterandom) on the admin key value provided by the service or management tool.</span></span>
3.  <span data-ttu-id="e9230-118">これらの値と *FriendlyNameText* 文字列を [**RequestVirtualSmartCardCreationAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcardcreationasync) に渡します。</span><span class="sxs-lookup"><span data-stu-id="e9230-118">Pass these values along with the *FriendlyNameText* string to [**RequestVirtualSmartCardCreationAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcardcreationasync).</span></span>

```cs
SmartCardPinPolicy pinPolicy = new SmartCardPinPolicy();
pinPolicy.MinLength = 6;

IBuffer adminkey = CryptographicBuffer.GenerateRandom(24);

SmartCardProvisioning provisioning = await
     SmartCardProvisioning.RequestVirtualSmartCardCreationAsync(
          "Card friendly name",
          adminkey,
          pinPolicy);
```

<span data-ttu-id="e9230-119">関連付けられた [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) オブジェクトが [**RequestVirtualSmartCardCreationAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcardcreationasync) から返されたら、仮想スマート カードのプロビジョニングが完了し、使う準備ができたことになります。</span><span class="sxs-lookup"><span data-stu-id="e9230-119">Once [**RequestVirtualSmartCardCreationAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcardcreationasync) has returned the associated [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) object, the virtual smart card is provisioned and ready for use.</span></span>

## <a name="handle-authentication-challenges"></a><span data-ttu-id="e9230-120">認証チャレンジの処理</span><span class="sxs-lookup"><span data-stu-id="e9230-120">Handle authentication challenges</span></span>


<span data-ttu-id="e9230-121">スマート カードや仮想スマート カードを使って認証するには、カードに格納されている管理者キーのデータと、認証サーバーまたは管理ツールによって管理されている管理者キーのデータとの間で、チャレンジを完了する動作をアプリに実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e9230-121">To authenticate with smart cards or virtual smart cards, your app must provide the behavior to complete challenges between the admin key data stored on the card, and the admin key data maintained by the authentication server or management tool.</span></span>

<span data-ttu-id="e9230-122">次のコードは、サービスのスマート カード認証をサポートする方法、または物理カードや仮想カードの詳細を変更する方法の例を示します。</span><span class="sxs-lookup"><span data-stu-id="e9230-122">The following code shows how to support smart card authentication for services or modification of physical or virtual card details.</span></span> <span data-ttu-id="e9230-123">カードの管理者キーを使って生成されたデータ ("challenge") が、サーバーまたは管理者ツールから提供された管理者キーのデータ ("adminkey") と一致すれば、認証は成功します。</span><span class="sxs-lookup"><span data-stu-id="e9230-123">If the data generated using the admin key on the card ("challenge") is the same as the admin key data provided by the server or management tool ("adminkey"), authentication is successful.</span></span>

```cs
static class ChallengeResponseAlgorithm
{
    public static IBuffer CalculateResponse(IBuffer challenge, IBuffer adminkey)
    {
        if (challenge == null)
            throw new ArgumentNullException("challenge");
        if (adminkey == null)
            throw new ArgumentNullException("adminkey");

        SymmetricKeyAlgorithmProvider objAlg = SymmetricKeyAlgorithmProvider.OpenAlgorithm(SymmetricAlgorithmNames.TripleDesCbc);
        var symmetricKey = objAlg.CreateSymmetricKey(adminkey);
        var buffEncrypted = CryptographicEngine.Encrypt(symmetricKey, challenge, null);
        return buffEncrypted;
    }
}
```

<span data-ttu-id="e9230-124">このコードは、このトピックの残りの部分で説明する、認証操作を完了する方法や、スマート カードまたは仮想スマート カードの情報に変更を適用する方法の中で使われます。</span><span class="sxs-lookup"><span data-stu-id="e9230-124">You will see this code referenced throughout the remainder of this topic was we review how to complete an authentication action, and how to apply changes to smart card and virtual smart card information.</span></span>

## <a name="verify-smart-card-or-virtual-smart-card-authentication-response"></a><span data-ttu-id="e9230-125">スマート カードまたは仮想スマート カード認証の応答の確認</span><span class="sxs-lookup"><span data-stu-id="e9230-125">Verify smart card or virtual smart card authentication response</span></span>


<span data-ttu-id="e9230-126">これで認証チャレンジのロジックが定義されたので、リーダーと通信してスマート カードにアクセスするか、その代わりに仮想スマート カードにアクセスして、認証を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e9230-126">Now that we have the logic for authentication challenges defined, we can communicate with the reader to access the smart card, or alternatively, access a virtual smart card for authentication.</span></span>

1.  <span data-ttu-id="e9230-127">チャレンジを始めるには、スマート カードに関連付けられた [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) オブジェクトから [**GetChallengeContextAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.getchallengecontextasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e9230-127">To begin the challenge, call [**GetChallengeContextAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.getchallengecontextasync) from the [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) object associated with the smart card.</span></span> <span data-ttu-id="e9230-128">これにより、[**SmartCardChallengeContext**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardChallengeContext) のインスタンスが生成されます。このインスタンスには、カードの [**Challenge**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardchallengecontext.challenge) 値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="e9230-128">This will generate an instance of [**SmartCardChallengeContext**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardChallengeContext), which contains the card's [**Challenge**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardchallengecontext.challenge) value.</span></span>

2.  <span data-ttu-id="e9230-129">次に、カードのチャレンジ値とサービスまたは管理ツールから提供された管理者キーを、前の例で定義した **ChallengeResponseAlgorithm** に渡します。</span><span class="sxs-lookup"><span data-stu-id="e9230-129">Next, pass the card's challenge value and the admin key provided by the service or management tool to the **ChallengeResponseAlgorithm** that we defined in the previous example.</span></span>

3.  <span data-ttu-id="e9230-130">[**VerifyResponseAsync** ](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardchallengecontext.verifyresponseasync)戻ります**true**認証が成功した場合。</span><span class="sxs-lookup"><span data-stu-id="e9230-130">[**VerifyResponseAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardchallengecontext.verifyresponseasync) will return **true** if authentication is successful.</span></span>

```cs
bool verifyResult = false;
SmartCard card = await rootPage.GetSmartCard();
SmartCardProvisioning provisioning =
    await SmartCardProvisioning.FromSmartCardAsync(card);

using (SmartCardChallengeContext context =
       await provisioning.GetChallengeContextAsync())
{
    IBuffer response = ChallengeResponseAlgorithm.CalculateResponse(
        context.Challenge,
        rootPage.AdminKey);

    verifyResult = await context.VerifyResponseAsync(response);
}
```

## <a name="change-or-reset-a-user-pin"></a><span data-ttu-id="e9230-131">ユーザー PIN の変更またはリセット</span><span class="sxs-lookup"><span data-stu-id="e9230-131">Change or reset a user PIN</span></span>


<span data-ttu-id="e9230-132">スマート カードに関連付けられている PIN を変更するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="e9230-132">To change the PIN associated with a smart card:</span></span>

1.  <span data-ttu-id="e9230-133">カードにアクセスし、関連付けられた [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) オブジェクトを生成します。</span><span class="sxs-lookup"><span data-stu-id="e9230-133">Access the card and generate the associated [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) object.</span></span>
2.  <span data-ttu-id="e9230-134">[  **RequestPinChangeAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestpinchangeasync) を呼び出して、この操作を完了するための UI をユーザーに表示します。</span><span class="sxs-lookup"><span data-stu-id="e9230-134">Call [**RequestPinChangeAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestpinchangeasync) to display a UI to the user to complete this operation.</span></span>
3.  <span data-ttu-id="e9230-135">PIN が正しく変更された場合は、呼び出しから **true** が返されます。</span><span class="sxs-lookup"><span data-stu-id="e9230-135">If the PIN was successfully changed the call will return **true**.</span></span>

```cs
SmartCardProvisioning provisioning =
    await SmartCardProvisioning.FromSmartCardAsync(card);

bool result = await provisioning.RequestPinChangeAsync();
```

<span data-ttu-id="e9230-136">PIN のリセットを要求するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="e9230-136">To request a PIN reset:</span></span>

1.  <span data-ttu-id="e9230-137">[  **RequestPinResetAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestpinresetasync) を呼び出して操作を開始します。</span><span class="sxs-lookup"><span data-stu-id="e9230-137">Call [**RequestPinResetAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestpinresetasync) to initiate the operation.</span></span> <span data-ttu-id="e9230-138">この呼び出しには、スマート カードと PIN のリセット要求を表す [**SmartCardPinResetHandler**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardpinresethandler) メソッドが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e9230-138">This call includes a [**SmartCardPinResetHandler**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardpinresethandler) method that represents the smart card and the pin reset request.</span></span>
2.  <span data-ttu-id="e9230-139">[**SmartCardPinResetHandler** ](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardpinresethandler)情報を提供する、 **ChallengeResponseAlgorithm**でラップされた、 [ **SmartCardPinResetDeferral** ](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardPinResetDeferral)を呼び出すと、カードのチャレンジの値と要求の認証にサービスや管理のツールによって提供される管理キーを比較するために使用します。</span><span class="sxs-lookup"><span data-stu-id="e9230-139">[**SmartCardPinResetHandler**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardpinresethandler) provides information that our **ChallengeResponseAlgorithm**, wrapped in a [**SmartCardPinResetDeferral**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardPinResetDeferral) call, uses to compare the card's challenge value and the admin key provided by the service or management tool to authenticate the request.</span></span>

3.  <span data-ttu-id="e9230-140">チャレンジが成功すると、[**RequestPinResetAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestpinresetasync) の呼び出しが完了し、PIN が正しくリセットされた場合は **true** が返されます。</span><span class="sxs-lookup"><span data-stu-id="e9230-140">If the challenge is successful, the [**RequestPinResetAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestpinresetasync) call is completed; returning **true** if the PIN was successfully reset.</span></span>

```cs
SmartCardProvisioning provisioning =
    await SmartCardProvisioning.FromSmartCardAsync(card);

bool result = await provisioning.RequestPinResetAsync(
    (pinResetSender, request) =>
    {
        SmartCardPinResetDeferral deferral =
            request.GetDeferral();

        try
        {
            IBuffer response =
                ChallengeResponseAlgorithm.CalculateResponse(
                    request.Challenge,
                    rootPage.AdminKey);
            request.SetResponse(response);
        }
        finally
        {
            deferral.Complete();
        }
    });
}
```

## <a name="remove-a-smart-card-or-virtual-smart-card"></a><span data-ttu-id="e9230-141">スマート カードまたは仮想スマート カードの取り外し</span><span class="sxs-lookup"><span data-stu-id="e9230-141">Remove a smart card or virtual smart card</span></span>


<span data-ttu-id="e9230-142">物理スマート カードが取り外されると、カードの削除時に [**CardRemoved**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.cardremoved) イベントが発生します。</span><span class="sxs-lookup"><span data-stu-id="e9230-142">When a physical smart card is removed a [**CardRemoved**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardreader.cardremoved) event will fire when the card is deleted.</span></span>

<span data-ttu-id="e9230-143">カード リーダーでこのイベントが発生したときのイベント ハンドラーとして、カードまたはリーダーが取り外されたときのアプリの動作を定義するメソッドを関連付けます。</span><span class="sxs-lookup"><span data-stu-id="e9230-143">Associate the firing of this event with the card reader with the method that defines your app's behavior on card or reader removal as an event handler.</span></span> <span data-ttu-id="e9230-144">この動作は、カードが取り外されたことをユーザーに通知するといった単純なものでかまいません。</span><span class="sxs-lookup"><span data-stu-id="e9230-144">This behavior can be something as simply as providing notification to the user that the card was removed.</span></span>

```cs
reader = card.Reader;
reader.CardRemoved += HandleCardRemoved;
```

<span data-ttu-id="e9230-145">仮想スマート カードの削除はプログラムによって行います。まずカードを取得し、次に [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) によって返されたオブジェクトから [**RequestVirtualSmartCardDeletionAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcarddeletionasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="e9230-145">The removal of a virtual smart card is handled programmatically by first retrieving the card and then calling [**RequestVirtualSmartCardDeletionAsync**](https://docs.microsoft.com/uwp/api/windows.devices.smartcards.smartcardprovisioning.requestvirtualsmartcarddeletionasync) from the [**SmartCardProvisioning**](https://docs.microsoft.com/uwp/api/Windows.Devices.SmartCards.SmartCardProvisioning) returned object.</span></span>

```cs
bool result = await SmartCardProvisioning
    .RequestVirtualSmartCardDeletionAsync(card);
```