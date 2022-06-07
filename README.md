# MS-URI-Handlers
*<sub>Note: The information below was tested from my personal computer. Values may be different from your own computer</sub>*

For the past year, I've been spending some time investigating how URI protocols are treated and potential vectors of abuse. With CVE-2021-40444 and the most recent CVE-2022-30190 (Follina), it still seems that there is research that needs to be done around these schemes. Most of these schemes are either undocumented or have minimal documentation on how they interact with the OS.

It's easy to see what apps are associated with protocols. A simple Windows search of 'Choose a default app for each protocol' will take you to the settings page where these associations are listed. After looking at this list, I noticed it was missing URI's that I knew were associated with my OS such as the Outlooks 'feed:' URI.

After digging through the registry, there a many URI's that aren't listed in the settings page. As of now, I'm not why MS pulls in some values to show while others are hidden in the reg. Searching the registry for 'URL:' will show you schemes registered to URI's. I have also found this IANA page that has been helpful while digging into these schemes.
