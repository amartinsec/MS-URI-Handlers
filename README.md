# MS-URI-Handlers
*<sub>Note: The information below was tested from my personal computer. Values may be different from your own computer</sub>*

## Primer
Anytime you make a request in the browser, add an external link to a document, etc. Windows first checks what protocol is speified. The most common are web requests that use HTTP and HTTPS such as:
```
https://github.com
```
Here, we have the protocol as HTTPS (hypertext transfer protocol secure) to transfer data over a network. This is just one of many protocols that Windows recognizies out of the box. Anytime a program is installed, it may make a registry entry to register the protocol handler. Typing 
```
calculator:
```
in a web browser (with Windows OS) will have a popup asking if you would like to open calc.exe. The same applies if you have ever clicked on an email address and the web browser oepns an email client. Here, the URI handler is 
```
mailto:exampleuser@exampledomain.com
```


## URI's

For the past year, I've been spending some time investigating how URI protocols are treated and potential vectors of abuse. With CVE-2021-40444 and the most recent CVE-2022-30190 (Follina), it still seems that there is research that needs to be done around these schemes. Most of these schemes are either undocumented or have minimal documentation on how they interact with the OS.

It's easy to see what apps are associated with protocols. A simple Windows search of 'Choose a default app for each protocol' will take you to the settings page where these associations are listed. After looking at this list, I noticed it was missing URI's that I knew were associated with my OS such as the Outlooks 'feed:' URI.

After digging through the registry, there a many URI's that aren't listed in the settings page. As of now, I'm not sure why MS pulls in some values to show while others are hidden in the reg. Searching the registry for 'URL:' will show you schemes registered to URI's. I have also found an IANA (link at the bottom) that has been helpful while digging into these schemes.

```
Powershell command to search here
```

In the registry, some URI associations will begin with a period such as '.zip'. These URI's will not work when typed in a web browser since they are missing the 'URL Protocol' registry entry, but will maintain their association if the Windows Search feature is used. 

Protocols on my computer:
| Protocols  |  |  |  |  |  | 
| --- | --- | --- | --- | --- | --- |
|AAM|Microsoft.Workfolders|msnweather|AAM|Microsoft.Workfolders|msnweather|
|accnc|microsoftmusic|mssharepointclient|accnc|microsoftmusic|mssharepointclient|
|acrobat|microsoftvideo|msteams|acrobat|microsoftvideo|msteams|
|acrobat2018|mk|mswindowsmusic|acrobat2018|mk|mswindowsmusic|
|acrobat2019|MMS|mswindowsvideo	|acrobat2019|MMS|mswindowsvideo|
|acrobat2020|ms-aad-brokerplugin|NordVPN|acrobat2020|ms-aad-brokerplugin|NordVPN|
|acrobat2021.oauth2|ms-access|NordVPN.Notification	|acrobat2021.oauth2|ms-access|NordVPN.Notification|
|adbps|ms-actioncenter|nxm|adbps|ms-actioncenter|nxm|
|adcnc|ms-appinstaller|oculus|adcnc|ms-appinstaller|oculus|
|adobe.genuine.invoker|ms-apprep|odopen	|adobe.genuine.invoker|ms-apprep|odopen|
|appinstaller.oauth2|ms-availablenetworks|OneIndex16	|appinstaller.oauth2|ms-availablenetworks|OneIndex16|
|armodelviewing|ms-calculator|onenote|armodelviewing|ms-calculator|onenote|
|auphd|ms-clock|onenote-cmd|auphd|ms-clock|onenote-cmd|
|battlenet|ms-contact-support|OneNote.URL.16	|battlenet|ms-contact-support|OneNote.URL.16|
|bingmaps|ms-cortana2|OneNoteDesktop|bingmaps|ms-cortana2|OneNoteDesktop|
|bingweather|ms-cxh|OneNoteDesktop.URL.16	bingweather|ms-cxh|OneNoteDesktop.URL.16|
|bittorrent|ms-cxh-full|openvpn-connect|bittorrent|ms-cxh-full|openvpn-connect|
|blizzard|ms-default-location|origin|blizzard|ms-default-location|origin|
|Blizzard.URI.Battlenet|ms-device-enrollment|origin2|Blizzard.URI.Battlenet|ms-device-enrollment|origin2|
|Blizzard.URI.Blizzard|ms-drive-to|Outlook.URL.feed.15|Blizzard.URI.Blizzard|ms-drive-to|Outlook.URL.feed.15|
|Blizzard.URI.Heroes|ms-excel|Outlook.URL.mailto.15|Blizzard.URI.Heroes|ms-excel|Outlook.URL.mailto.15|
|Blizzard.URI.SC2|ms-eyecontrolspeech|Outlook.URL.stssync.15|Blizzard.URI.SC2|ms-eyecontrolspeech|Outlook.URL.stssync.15|
|calculator|ms-gamebar|Outlook.URL.webcal.15|calculator|ms-gamebar|Outlook.URL.webcal.15|
|callto|ms-gamebarservices|outlookaccounts|callto|ms-gamebarservices|outlookaccounts|
|citrixonline|ms-gamingoverlay|outlookcal|citrixonline|ms-gamingoverlay|outlookcal|
|citrixonline551|ms-get-started|outlookmail|citrixonline551|ms-get-started|outlookmail|
|com.epicgames.eos|ms-getoffice|paintdotnet|com.epicgames.eos|ms-getoffice|paintdotnet|
|com.epicgames.launcher|ms-holographicfirstrun|rdcnc	|com.epicgames.launcher|ms-holographicfirstrun|rdcnc|
|com.microsoft.3dviewer|ms-inputapp|read|com.microsoft.3dviewer|ms-inputapp|read|
|conf|ms-insights|receiver|conf|ms-insights|receiver|
|discord-349947310375043074|ms-ipmessaging|res|discord-349947310375043074|ms-ipmessaging|res|
|discord-361968954954219521|ms-meetnowflyout|rlogin|discord-361968954954219521|ms-meetnowflyout|rlogin|
|discord-464045794530557953|ms-mmsys|rtkuwp|discord-464045794530557953|ms-mmsys|rtkuwp|
|discord-531450167799447552|ms-msdt|search|discord-531450167799447552|ms-msdt|search|
|discord-550022696642281486|ms-msime-imepad|search-ms|discord-550022696642281486|ms-msime-imepad|search-ms|
|DLNA-PLAYSINGLE|ms-msime-imjpdct|sgnl|DLNA-PLAYSINGLE|ms-msime-imjpdct|sgnl|
|eadm|ms-officeapp|signalcaptcha|eadm|ms-officeapp|signalcaptcha|
|ealink|ms-officecmd|sip|ealink|ms-officecmd|sip|
|exodus|ms-oobenetwork|sips|exodus|ms-oobenetwork|sips|
|Explorer.AssocActionId.BurnSelection|ms-paint|skype|Explorer.AssocActionId.BurnSelection|ms-paint|skype|
|Explorer.AssocActionId.EraseDisc|ms-pchealthcheck|skype-meetnow|Explorer.AssocActionId.EraseDisc|ms-pchealthcheck|skype-meetnow|
|Explorer.AssocActionId.ZipSelection|ms-penworkspace|skypecast15|Explorer.AssocActionId.ZipSelection|ms-penworkspace|skypecast15|
|Explorer.AssocProtocol.search-ms|ms-people|skypewin|Explorer.AssocProtocol.search-ms|ms-people|skypewin|
|Explorer.BurnSelection|ms-perception-simulation|slack|Explorer.BurnSelection|ms-perception-simulation|slack|
|Explorer.EraseDisc|ms-phone|spotify|Explorer.EraseDisc|ms-phone|spotify|
|Explorer.ZipSelection|ms-photos|starcraft|Explorer.ZipSelection|ms-photos|starcraft|
|feed|ms-powerpoint|steam	|feed|ms-powerpoint|steam|
|feedback-hub|ms-print-addprinter|steamlink|feedback-hub|ms-print-addprinter|steamlink|
|feeds|ms-print-printjobs|steamtours|feeds|ms-print-printjobs|steamtours|
|file|ms-publisher|stssync|file|ms-publisher|stssync|
|FirefoxURL-308046B0AF4A39CB|ms-quick-assist|tbauth	|FirefoxURL-308046B0AF4A39CB|ms-quick-assist|tbauth|
|FirefoxURL-CA9422711AE1A81C|ms-rdx-document|tel	|FirefoxURL-CA9422711AE1A81C|ms-rdx-document|tel|
|ftp|ms-retaildemo-launchbioenrollment|telnet	|ftp|ms-retaildemo-launchbioenrollment|telnet|
|GeForceExperience|ms-retaildemo-launchstart|tg	|GeForceExperience|ms-retaildemo-launchstart|tg|
|git-client|ms-screenclip|tn3270|git-client|ms-screenclip|tn3270|
|gotomeeting|ms-screensketch|uplay|gotomeeting|ms-screensketch|uplay|
|gotomeeting18962|ms-search|viscosity	|gotomeeting18962|ms-search|viscosity|
|gotomeeting19228|ms-settings|viscosityserial|gotomeeting19228|ms-settings|viscosityserial|
|gotomeeting19598|ms-settings-airplanemode|vm|gotomeeting19598|ms-settings-airplanemode|vm|
|gotomeeting19796|ms-settings-bluetooth|vmrc|gotomeeting19796|ms-settings-bluetooth|vmrc|
|gotomeeting19932|ms-settings-cellular|vms|gotomeeting19932|ms-settings-cellular|vms|
|gotomeeting19950|ms-settings-connectabledevices|vmware-rvm	|gotomeeting19950|ms-settings-connectabledevices|vmware-rvm|
|gotoopener|ms-settings-displays-topology|vrmonitor|gotoopener|ms-settings-displays-topology|vrmonitor|
|gotoopener551|ms-settings-emailandaccounts|vsls|gotoopener551|ms-settings-emailandaccounts|vsls|
|grvopen|ms-settings-language|vstfs|grvopen|ms-settings-language|vstfs|
|heroes|ms-settings-location|vsweb|heroes|ms-settings-location|vsweb|
|http|ms-settings-lock|webcal	|http|ms-settings-lock|webcal|
|https|ms-settings-mobilehotspot|webcals|https|ms-settings-mobilehotspot|webcals|
|IE.HTTP|ms-settings-notifications|whatsapp	|IE.HTTP|ms-settings-notifications|whatsapp|
|iehistory|ms-settings-power|windows-feedback	iehistory|ms-settings-power|windows-feedback|
|ierss|ms-settings-privacy|windows.tbauth|ierss|ms-settings-privacy|windows.tbauth|
|im|ms-settings-proximity|windowsdefender|im|ms-settings-proximity|windowsdefender|
|insiderhub|ms-settings-screenrotation|WMP11.AssocProtocol.DLNA-PLAYSINGLE|insiderhub|ms-settings-screenrotation|WMP11.AssocProtocol.DLNA-PLAYSINGLE|
|jnlp|ms-settings-wifi|WMP11.AssocProtocol.MMS|jnlp|ms-settings-wifi|WMP11.AssocProtocol.MMS|
|jnlps|ms-settings-workplace|wpa|jnlps|ms-settings-workplace|wpa|
|launchacrobat|ms-sttoverlay|xbls|launchacrobat|ms-sttoverlay|xbls|
|launchreader|ms-taskswitcher|xbox|launchreader|ms-taskswitcher|xbox|
|LDAP|ms-teams|xbox-arena	|LDAP|ms-teams|xbox-arena|
|link2ea|ms-unistore-email|xbox-captures|link2ea|ms-unistore-email|xbox-captures|
|Lync15|ms-virtualtouchpad|xbox-friendfinder|Lync15|ms-virtualtouchpad|xbox-friendfinder|
|Lync15classic|ms-voip-call|xbox-gamehub|Lync15classic|ms-voip-call|xbox-gamehub|
|ma-chan|ms-voip-video|xbox-lfg|ma-chan|ms-voip-video|xbox-lfg|
|ma-filelink|ms-walk-to|xbox-network|ma-filelink|ms-walk-to|xbox-network|
|Magnet|ms-wcrv|xbox-profile|Magnet|ms-wcrv|xbox-profile|
|mailto|ms-windows-search|xbox-settings|mailto|ms-windows-search|xbox-settings|
|mapi|ms-windows-store|xbox-store|mapi|ms-windows-store|xbox-store|
|mapi16|ms-windows-store-deskext|xbox-tcui|mapi16|ms-windows-store-deskext|xbox-tcui|
|microsoft-edge|ms-windows-store2|xboxgames|microsoft-edge|ms-windows-store2|xboxgames|
|microsoft-edge-holographic|ms-word|xboxliveapp-1297287741	|microsoft-edge-holographic|ms-word|xboxliveapp-1297287741|
|microsoft.windows.camera|ms-wpc|xboxmusi	|microsoft.windows.camera|ms-wpc|xboxmusic|
|microsoft.windows.camera.multipicker|ms-wpdrmv|zoommtg|microsoft.windows.camera.multipicker|ms-wpdrmv|zoommtg|
|microsoft.windows.camera.picker|ms-xbet-survey|ZoomPbx.im|microsoft.windows.camera.picker|ms-xbet-survey|ZoomPbx.im|
|microsoft.windows.photos.crop|ms-xbl-3d8b930f|ZoomPbx.zoomphonecall|microsoft.windows.photos.crop|ms-xbl-3d8b930f|ZoomPbx.zoomphonecall|
|microsoft.windows.photos.picker|ms-xgpueject|ZoomPhoneCall|microsoft.windows.photos.picker|ms-xgpueject|ZoomPhoneCall|
|microsoft.windows.photos.videoedit|msi-dc|zunemicrosoft.windows.photos.videoedit|msi-dc|zune|



## Links
https://docs.microsoft.com/en-us/windows/win32/search/-search-3x-wds-extidx-prot-implementing
https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml
