---
title: Updating a user's Presence via WinRT
description: Code example for setting a user's online presence status.
kindex: Updating a user's Presence via WinRT
kindex: rich presence
ms.topic: article
ms.assetid: 7e6e7b69-d7c3-42fa-bcc4-6d68947f6fdb
ms.localizationpriority: medium
ms.date: 04/04/2017
---

# Updating a user's Presence via WinRT

Xbox Live Rich Presence provides features for advertising a player's current activity to other players.

For more information, see [Rich Presence overview](../live-presence-overview.md).

This code example sets a user's online presence status:

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
