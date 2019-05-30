---
description: メールの作成ダイアログを起動して、ユーザーがメール メッセージを送信できるようにする方法について説明します。 ダイアログを表示する前に、メールの各フィールドにデータを設定することができます。 メッセージは、ユーザーが送信ボタンをタップするまで送信されません。
title: メールの送信
ms.assetid: 74511E90-9438-430E-B2DE-24E196A111E5
keywords: 連絡先, メール, 送信
ms.date: 10/11/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 524e1f12c3da0d9d06e73d84e08e2d54efde9a7e
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66361216"
---
# <a name="send-email"></a><span data-ttu-id="09c5e-106">メールの送信</span><span class="sxs-lookup"><span data-stu-id="09c5e-106">Send email</span></span>

<span data-ttu-id="09c5e-107">メールの作成ダイアログを起動して、ユーザーがメール メッセージを送信できるようにする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="09c5e-107">Shows how to launch the compose email dialog to allow the user to send an email message.</span></span> <span data-ttu-id="09c5e-108">ダイアログを表示する前に、メールの各フィールドにデータを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="09c5e-108">You can pre-populate the fields of the email with data before showing the dialog.</span></span> <span data-ttu-id="09c5e-109">メッセージは、ユーザーが送信ボタンをタップするまで送信されません。</span><span class="sxs-lookup"><span data-stu-id="09c5e-109">The message will not be sent until the user taps the send button.</span></span>

<span data-ttu-id="09c5e-110">**この記事では**</span><span class="sxs-lookup"><span data-stu-id="09c5e-110">**In this article**</span></span>

-   [<span data-ttu-id="09c5e-111">電子メールの作成 ダイアログを起動します。</span><span class="sxs-lookup"><span data-stu-id="09c5e-111">Launch the compose email dialog</span></span>](#launch-the-compose-email-dialog)
-   [<span data-ttu-id="09c5e-112">概要と次の手順</span><span class="sxs-lookup"><span data-stu-id="09c5e-112">Summary and next steps</span></span>](#summary-and-next-steps)
-   [<span data-ttu-id="09c5e-113">関連トピック</span><span class="sxs-lookup"><span data-stu-id="09c5e-113">Related topics</span></span>](#related-topics)

## <a name="launch-the-compose-email-dialog"></a><span data-ttu-id="09c5e-114">メールの作成ダイアログの起動</span><span class="sxs-lookup"><span data-stu-id="09c5e-114">Launch the compose email dialog</span></span>

<span data-ttu-id="09c5e-115">新しい [**EmailMessage**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Email.EmailMessage) オブジェクトを作成し、メールの作成ダイアログに事前に入力するデータを設定します。</span><span class="sxs-lookup"><span data-stu-id="09c5e-115">Create a new [**EmailMessage**](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Email.EmailMessage) object and set the data that you want to be pre-populated in the compose email dialog.</span></span> <span data-ttu-id="09c5e-116">ダイアログを表示するには、[**ShowComposeNewEmailAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.email.emailmanager.showcomposenewemailasync) を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="09c5e-116">Call [**ShowComposeNewEmailAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.email.emailmanager.showcomposenewemailasync) to show the dialog.</span></span>

``` cs
private async Task ComposeEmail(Windows.ApplicationModel.Contacts.Contact recipient,
    string subject, string messageBody)
{
    var emailMessage = new Windows.ApplicationModel.Email.EmailMessage();
    emailMessage.Body = messageBody;

    var email = recipient.Emails.FirstOrDefault<Windows.ApplicationModel.Contacts.ContactEmail>();
    if (email != null)
    {
        var emailRecipient = new Windows.ApplicationModel.Email.EmailRecipient(email.Address);
        emailMessage.To.Add(emailRecipient);
        emailMessage.Subject = subject;
    }

    await Windows.ApplicationModel.Email.EmailManager.ShowComposeNewEmailAsync(emailMessage);
}
```

>[!NOTE]
> <span data-ttu-id="09c5e-117">添付ファイルを使用して電子メールに追加する、 [EmailAttachment](https://docs.microsoft.com/uwp/api/windows.applicationmodel.email.emailattachment)クラスは、メール アプリでのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="09c5e-117">Attachments that you add to an email by using the [EmailAttachment](https://docs.microsoft.com/uwp/api/windows.applicationmodel.email.emailattachment) class will appear only in the Mail app.</span></span> <span data-ttu-id="09c5e-118">ユーザーがその既定のプログラムとして構成されているその他のメール プログラムを使用している場合、添付ファイルなし、compose ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="09c5e-118">If users have any other mail program configured as their default mail program, the compose window will appear without the attachment.</span></span> <span data-ttu-id="09c5e-119">これは既知の問題です。</span><span class="sxs-lookup"><span data-stu-id="09c5e-119">This is a known issue.</span></span>

## <a name="summary-and-next-steps"></a><span data-ttu-id="09c5e-120">要約と次のステップ</span><span class="sxs-lookup"><span data-stu-id="09c5e-120">Summary and next steps</span></span>

<span data-ttu-id="09c5e-121">このトピックでは、メールの作成ダイアログの起動方法を示しました。</span><span class="sxs-lookup"><span data-stu-id="09c5e-121">This topic has shown you how to launch the compose email dialog.</span></span> <span data-ttu-id="09c5e-122">メール メッセージの受信者として使う連絡先を選ぶ方法については、「[連絡先の選択](selecting-contacts.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="09c5e-122">For information on selecting contacts to use as recipients for an email message, see [Select contacts](selecting-contacts.md).</span></span> <span data-ttu-id="09c5e-123">電子メールの添付ファイルとして使用するファイルの選択については、「[**PickSingleFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="09c5e-123">See [**PickSingleFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync) to select a file to use as an email attachment.</span></span>

## <a name="related-topics"></a><span data-ttu-id="09c5e-124">関連トピック</span><span class="sxs-lookup"><span data-stu-id="09c5e-124">Related topics</span></span>

* [<span data-ttu-id="09c5e-125">連絡先を選択</span><span class="sxs-lookup"><span data-stu-id="09c5e-125">Selecting contacts</span></span>](selecting-contacts.md)
* <span data-ttu-id="09c5e-126">[ファイル ピッカーを呼び出した後、Windows Phone アプリを継続する方法](https://docs.microsoft.com/previous-versions/windows/apps/dn614994(v=win.10))</span><span class="sxs-lookup"><span data-stu-id="09c5e-126">[How to continue your Windows Phone app after calling a file picker](https://docs.microsoft.com/previous-versions/windows/apps/dn614994(v=win.10))</span></span>
 

 
