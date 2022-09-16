# MS-URI-Handlers
*<sub>Note: The information below was tested from my personal computer. Results will be different from your own</sub>*

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

After digging through the registry, there a many URI's that aren't listed in the settings page. As of now, I'm not sure why MS pulls in some values to show while others are hidden in the reg. Searching the registry for 'URL:' will show you schemes registered to URI's. I have also found an IANA (link at the bottom) that has been helpful while looking into these schemes.

```
gci -ea SilentlyContinue -recurse HKLM:\ | get-itemproperty | where { $_  -match 'URL:' }
```

Note: Any scheme with a "." in it will not resolve if entered directly into the web browser and is treated as http. 

Ex:
```microsoft.windows.camera://``` entered into the address bar of a web browser will get interpreted as --> http://microsoft.windows.camera//

Entering it in the run bar, opens the camera as expected. To bypass the browser not interpreting correctly, the schemes can be included on the page itself:
```<a href="microsoft.windows.camera://">microsoft.windows.camera</a></li>``` will properly interpret the scheme when clicked.


Protocols:
| Protocols  |  |  |  
| --- | --- | --- |
|AAM://|microsoft-edge-holographic://|ms-word://|
|accnc://|microsoftmusic://|ms-wpc://|
|acrobat://|microsoftvideo://|ms-wpdrmv://|
|acrobat2018://|mk://|ms-xbet-survey://|
|acrobat2019://|MMS://|ms-xbl-3d8b930f://|
|acrobat2020://|ms-aad-brokerplugin://|ms-xgpueject://|
|acrobat2021.oauth2://|ms-access://|NordVPN.Notification://|
|adbps://|ms-actioncenter://|NordVPN://|
|adcnc://|ms-appinstaller://|nxm://|
|adobe.genuine.invoker://|ms-apprep://|oculus://|
|appinstaller.oauth2://|ms-availablenetworks://|odopen://|
|armodelviewing://|ms-calculator://|OneIndex16://|
|auphd://|ms-clock://|OneNote.URL.16://|
|battlenet://|ms-contact-support://|onenote://|
|bingmaps://|ms-cortana2://|onenote-cmd://|
|bingweather://|ms-cxh://|OneNoteDesktop.URL.16 bingweather://|
|bittorrent://|ms-cxh-full://|OneNoteDesktop://|
|Blizzard.URI.Battlenet://|ms-default-location://|openvpn-connect://|
|Blizzard.URI.Blizzard://|ms-device-enrollment://|origin://|
|Blizzard.URI.Heroes://|ms-drive-to://|origin2://|
|Blizzard.URI.SC2://|ms-excel://|Outlook.URL.feed.15://|
|blizzard://|ms-eyecontrolspeech://|Outlook.URL.mailto.15://|
|calculator://|ms-gamebar://|Outlook.URL.stssync.15://|
|callto://|ms-gamebarservices://|Outlook.URL.webcal.15://|
|citrixonline://|ms-gamingoverlay://|outlookaccounts://|
|citrixonline551://|ms-getoffice://|outlookcal://|
|com.epicgames.eos://|ms-get-started://|outlookmail://|
|com.epicgames.launcher://|ms-holographicfirstrun://|paintdotnet://|
|com.microsoft.3dviewer://|msi-dc://|rdcnc://|
|conf://|ms-inputapp://|read://|
|discord-://|ms-insights://|receiver://|
|discord-://|ms-ipmessaging://|res://|
|discord-://|ms-meetnowflyout://|rlogin://|
|discord-://|ms-mmsys://|rtkuwp://|
|discord-://|ms-msdt://|search://|
|DLNA-PLAYSINGLE://|ms-msime-imepad://|search-ms://|
|eadm://|ms-msime-imjpdct://|sgnl://|
|ealink://|msnweather://|signalcaptcha://|
|exodus://|ms-officeapp://|sip://|
|Explorer.AssocActionId.BurnSelection://|ms-officecmd://|sips://|
|Explorer.AssocActionId.EraseDisc://|ms-oobenetwork://|skype://|
|Explorer.AssocActionId.ZipSelection://|ms-paint://|skypecast15://|
|Explorer.AssocProtocol.search-ms://|ms-pchealthcheck://|skype-meetnow://|
|Explorer.BurnSelection://|ms-penworkspace://|skypewin://|
|Explorer.EraseDisc://|ms-people://|slack://|
|Explorer.ZipSelection://|ms-perception-simulation://|spotify://|
|feed://|ms-phone://|steamlink://|
|feedback-hub://|ms-photos://|steamtours://|
|feeds://|ms-powerpoint://|stssync://|
|FirefoxURL-://|ms-print-addprinter://|tbauth://|
|FirefoxURL-://|ms-print-printjobs://|tel://|
|ftp://|ms-publisher://|telnet://|
|GeForceExperience://|ms-quick-assist://|tg://|
|git-client://|ms-rdx-document://|tn3270://|
|gotomeeting://|ms-retaildemo-launchbioenrollment://|uplay://|
|gotomeeting18962://|ms-retaildemo-launchstart://|viscosity://|
|gotomeeting19228://|ms-screenclip://|viscosityserial://|
|gotomeeting19598://|ms-screensketch://|vm://|
|gotomeeting19796://|ms-search://|vmrc://|
|gotomeeting19932://|ms-settings://|vms://|
|gotomeeting19950://|ms-settings-airplanemode://|vmware-rvm://|
|gotoopener://|ms-settings-bluetooth://|vrmonitor://|
|gotoopener551://|ms-settings-cellular://|vsls://|
|grvopen://|ms-settings-connectabledevices://|vstfs://|
|heroes://|ms-settings-displays-topology://|vsweb://|
|http://|ms-settings-emailandaccounts://|webcal://|
|https://|ms-settings-language://|webcals://|
|iehistory://|ms-settings-location://|whatsapp://|
|ierss://|ms-settings-lock://|windows.tbauth://|
|im://|ms-settings-mobilehotspot://|windowsdefender://|
|insiderhub://|ms-settings-notifications://|windows-feedback iehistory://|
|jnlp://|ms-settings-power://|WMP11.AssocProtocol.DLNA-PLAYSINGLE://|
|jnlps://|ms-settings-privacy://|WMP11.AssocProtocol.MMS://|
|launchacrobat://|ms-settings-proximity://|wpa://|
|launchreader://|ms-settings-screenrotation://|xbls://|
|LDAP://|ms-settings-wifi://|xbox://|
|link2ea://|ms-settings-workplace://|xbox-arena://|
|Lync15://|mssharepointclient://|xbox-captures://|
|Lync15classic://|ms-sttoverlay://|xbox-friendfinder://|
|ma-chan://|ms-taskswitcher://|xbox-gamehub://|
|ma-filelink://|msteams://|xboxgames://|
|Magnet://|ms-teams://|xbox-lfg://|
|mailto://|ms-unistore-email://|xboxliveapp-1297287741://|
|mapi://|ms-virtualtouchpad://|xboxmusi://|
|mapi16://|ms-voip-call://|xbox-network://|
|microsoft.windows.camera.multipicker://|ms-voip-video://|xbox-profile://|
|microsoft.windows.camera.picker://|ms-walk-to://|xbox-settings://|
|microsoft.windows.camera://|ms-wcrv://|xbox-store://|
|microsoft.windows.camera://|mswindowsmusic://|xbox-tcui://|
|microsoft.windows.photos.crop://|ms-windows-search://|zoommtg://|
|microsoft.windows.photos.picker://|ms-windows-store://|ZoomPbx.im://|
|microsoft.windows.photos.videoedit://|ms-windows-store2://|ZoomPbx.zoomphonecall://|
|Microsoft.Workfolders://|ms-windows-store-deskext://|ZoomPhoneCall://|
|microsoft-edge://|mswindowsvideo://|zunemicrosoft.windows.photos.videoedit://|

## Links
  
https://docs.microsoft.com/en-us/windows/win32/search/-search-3x-wds-extidx-prot-implementing
  
https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml
