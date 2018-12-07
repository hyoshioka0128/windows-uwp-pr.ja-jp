---
title: リッチ プレゼンスのプログラミング
description: Xbox Live メンバーのオンライン プレゼンス状態を設定するコード例について説明します。
ms.assetid: 7e6e7b69-d7c3-42fa-bcc4-6d68947f6fdb
ms.date: 04/04/2017
ms.topic: article
keywords: xbox live, xbox, ゲーム, uwp, windows 10, xbox one, リッチ プレゼンス
ms.localizationpriority: medium
ms.openlocfilehash: 0a113dc140500c982ddf22e25308eaafeaed66d6
ms.sourcegitcommit: a3dc929858415b933943bba5aa7487ffa721899f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2018
ms.locfileid: "8780262"
---
# <a name="programming-rich-presence"></a><span data-ttu-id="1fdbc-104">リッチ プレゼンスのプログラミング</span><span class="sxs-lookup"><span data-stu-id="1fdbc-104">Programming Rich Presence</span></span>

<span data-ttu-id="1fdbc-105">リッチ プレゼンスは、プレイヤーの現在のアクティビティを他のプレイヤーに通知するための機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="1fdbc-105">Rich presence provides features for advertising a player's current activity to other players.</span></span> <span data-ttu-id="1fdbc-106">詳細については、「[リッチ プレゼンス文字列 - 概要](rich-presence-strings-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1fdbc-106">For more information, see [Rich Presence Strings: Overview](rich-presence-strings-overview.md).</span></span>

```cpp

XboxLiveContext^ xboxLiveContext = NULL;

// Set the XboxLiveContext for a user *once* otherwise you may encounter unpredictable behavior.
void OneTimeInit()
{
  // Get the XboxLiveContext.  This should only be done once per user after signing in.
  xboxLiveContext = ref new Microsoft::Xbox::Services::XboxLiveContext(User::Users->GetAt(0));
}

void Example_PresenceService_SetPresenceAsync()
{
    // The config ID below is an example.
    // The real ID to use is defined when you set up the game on Xbox Development Portal.
    String^ aServiceConfigurationId = "C1BA92A9-0000-0000-0000-000000000000";

    PresenceData^ presenceData = ref new PresenceData(
        aServiceConfigurationId,
        "mainMenuPresence"
        );

    IAsyncAction^ setPresenceAction = xboxLiveContext->PresenceService->SetPresenceAsync(
        xboxLiveContext->User->XboxLiveId,
        true, // isUserActive
        presenceData    // richPresenceData is optional
        );

    create_task( setPresenceAction )
    .then([] ()
    {
        LogComment( L"SetPresenceAsync Done" );
    })
    .wait();
}
```
