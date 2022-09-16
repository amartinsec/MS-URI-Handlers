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


After finding all handlers, I ran strings.exe against my whole system to find any refernces to the above:
C:\Windows\*:

| Protocols  |  |  |  
| --- | --- | --- |
|acrobat://remove_history\>|ftp://ftp.info-zip.org/pub/infozip/src/}}}\sectd|ms-gamingoverlay://startuptips|
|acrobat://remove_history\>El|ftp://ftp.microsoft.com|ms-gamingoverlay://startuptips?%ls=%ls&ProcessId=%lu&WindowId=%ll|
|acrobat://remove_history\>Odstr|ftp://ftp.microsoft.com/pub|ms-gamingoverlay://startuptips?pid=%lu&WindowId=%llu|
|acrobat://remove_history\>Odstrani|ftp://ftp.microsoft.com/pub/*C|ms-get-started://collection/?id=windows-collection&tipsetid=use|
|acrobat://remove_history\>Poista|ftp://ftp.tlcsupport.com/Parsonstech1/Legal2001Updat|ms-get-started://redirect?id=apps_action|
|acrobat://remove_history\>Preflight-audittrail|ftp://localhost/samplefile.txt|ms-get-started://redirect?id=handwriting|
|acrobat://remove_history\>Preflight-Pr|iehistory://|ms-get-started://redirect?id=handwriting&p=ui&s=handwriting|
|acrobat://remove_history\>Remover|ierss://|ms-get-started://redirect?id=helpoffline|
|acrobat://remove_history\>Supprimer|launch=ms-actioncenter://|ms-get-started://redirect?id=my-people|
|acrobat://remove_history\>Usu|LDAP://|ms-get-started://redirect?id=new|
|acrobat://verify_fingerprint\>|LDAP://%ls/%ls|ms-get-started://redirect?id=touch_pen|
|acrobat://verify_fingerprint\>Check|LDAP://%s|msldap://|
|acrobat://verify_fingerprint\>Comprobar|LDAP://%s%s%s|msldap://CN=myStore,CN=Program|
|acrobat://verify_fingerprint\>Controlla|LDAP://%s%s%s%s%s|ms-paint://|
|acrobat://verify_fingerprint\>Fingerabdruck|LDAP://%s%sRootDSE|ms-phone://|
|acrobat://verify_fingerprint\>Kontroller|LDAP://%s,%s|ms-phone://phonelink?ocid=Winsettingshome|
|acrobat://verify_fingerprint\>Kontrollera|LDAP://%s/|ms-screensketch://edit?|
|acrobat://verify_fingerprint\>Preveri|LDAP://%s/%s|ms-screensketch://edit?source=inkworkspace&sharedAccessToken=|
|acrobat://verify_fingerprint\>Profil|LDAP://%s/%s,%s|ms-search://search?q=|
|acrobat://verify_fingerprint\>Skontrolova|LDAP://%sC:\Windows\\WinSxS\amd64_microsoft-hyper-v-v|ms-settings-location://|
|acrobat://verify_fingerprint\>Sprawd|LDAP://%ws|ms-windows-store://|
|acrobat://verify_fingerprint\>Tarkista|ldap://%ws/|ms-windows-store://assoc/?fileext=|
|acrobat://verify_fingerprint\>V|LDAP://%ws/%ws|ms-windows-store://assoc/?protocol=|
|acrobat://verify_fingerprint\>Verificar|LDAP://%ws/rootDSE|ms-windows-store://Assoc/?referrer=sharepicker&tags=|
|acrobat://verify_fingerprint\>Vingerafdruk|LDAP://,|ms-windows-store://assoc/?Tags=ContactPanel-ContactPanel&OCID=ems|
|acrobat://verify_fingerprint\>Zkontrolovat|ldap:///|ms-windows-store://collection/?CollectionId=Fonts&OCID=SettingsFo|
|acrobat://verify_fingerprint>Check|ldap:///%1!s!%2!s!?%3!s!,%4!s!,%5!s!,%6!s!,%7!s!?one?|ms-windows-store://collection/?CollectionId=LocalExperiencePacks&|
|acrobat2018://dc.acrobat.com/link/review?|ldap:///%s?userCertificate|ms-windows-store://collection/?CollectionId=securityapps|
|acrobat2018://dc.stage.acrobat.com/link/review?|ldap:///%s?userCertificate?base?objectCategory=user|ms-windows-store://collection/?CollectionId=WindowsInkCollection|
|acrobat2018://documentcloud.adobe.com/link/review?|ldap:///CN=%7%8,CN=%2,CN=CDP,CN=Public|ms-windows-store://collection/?CollectionId=WindowsStickers|
|acrobat2019://dc/launchTool?|ldap:///CN=%7,CN=AIA,CN=Public|ms-windows-store://collection/?CollectionId=WindowsThemes&OCID=OS|
|acrobat2020://dc/launchToolWithFiles?|ldap:///CN=%7,CN=Certification|ms-windows-store://DownloadsAndUpdates|
|browsertools://browsertools.debugger.js,n.QuotaExceededErrorMessage=QuotaExceededError|ldap:///CN=%7,CN=KRA,CN=Public|ms-windows-store://navigatetopage/?Id=Subscriptions|
|dlna-playsingle://|ldap:///CN=%ws,CN=%ws,CN=CDP|ms-windows-store://pdp/?PFN=|
|dlna-playsingle://%ls?sid=urn:upnp-org:serviceId:ContentDirector|ldap:///CN=%ws,CN=Certification|ms-windows-store://pdp/?PFN=%s|
|feed://|ldap:///CN=AIA,CN=Public|ms-windows-store://pdp/?PFN=Microsoft.3DBuilder_8wekyb3d8bbwe|
|feed://https://|ldap:///CN=Certification|ms-windows-store://pdp/?productId=%1&skuid=%2&catalogid=%3|
|feedback-hub://|ldap:///CN=KRA,CN=Public|ms-windows-store://pdp/?ProductId=9mspc6mp8fm4|
|feedback-hub://?ContextId=%s&PackageName=%s|ldap:///CN=NTAuthCertificates|ms-windows-store://pdp/?productid=9n0866fs04w8|
|feedback-hub://?contextid=104|ldap:///CN=NTAuthCertificates,CN=Public|ms-windows-store://pdp/?productid=9n0866fs04w8.ms-windows-store:/|
|feedback-hub://?contextid=114|ldap:///CN=Public|ms-windows-store://pdp/?productid=9nblggh10pg8>|
|feedback-hub://?contextid=115|LDAP://{0}/{1}|ms-windows-store://pdp/?ProductId=9nblggh4qghw|
|feedback-hub://?contextid=117|LDAP://<GUID=|ms-windows-store://pdp/?productid=9NFFX4SZZ23L|
|feedback-hub://?contextid=118|LDAP://<SID=|ms-windows-store://pdp/?productid=9NNRDVCB3J7W|
|feedback-hub://?contextid=119|ldap://acraiz.suscerte.gob.ve07|ms-windows-store://pdp/?productid=9NNRDVCB3J7W|
|feedback-hub://?contextid=127|ldap://admindir.admin.ch:389/cn=Swiss%20Government%20|ms-windows-store://pdp/?productid=9PJ0NKL8MCSJ|
|feedback-hub://?contextid=13|LDAP://CN=...,DC=...|ms-windows-store://pdp/?productid=9wzdncrdtbvb>|
|feedback-hub://?contextid=137|LDAP://CN={31B2F340-016D-11D2-945F-00C04FB984F9},CN=P|ms-windows-store://pdp/?ProductId=9wzdncrfhvqm|
|feedback-hub://?contextid=158|LDAP://CN=Certificate|ms-windows-store://pdp/?productid=BF712690PL0G|
|feedback-hub://?contextid=210|LDAP://CN=ComPartitions,CN=System,%s|ms-windows-store://pdp?pfn=%s|
|feedback-hub://?contextid=213|LDAP://cn=DisplaySpecifiers,%s|ms-windows-store://PDP?PFN=Microsoft.XboxApp_8wekyb3d8bbwe|
|feedback-hub://?contextid=215|LDAP://CN=Machine,|ms-windows-store://settings/|
|feedback-hub://?contextid=217|LDAP://CN=ms-FVE-KeyPackage,|ms-windows-store://Settings/?display=preferences|
|feedback-hub://?contextid=220|LDAP://CN=ms-FVE-RecoveryGuid,|ms-windows-store://signin|
|feedback-hub://?contextid=223|LDAP://CN=ms-FVE-RecoveryInformation,|ms-windows-store://signin|
|feedback-hub://?contextid=236|LDAP://CN=ms-FVE-RecoveryPassword,|ms-windows-store://switchwindows|
|feedback-hub://?contextid=239|LDAP://CN=ms-FVE-VolumeGuid,|mswindowsvideo://playurl//?url=|
|feedback-hub://?contextid=242|LDAP://CN=MyContainer,DC=MyDomain,DC=Company,DC=Com|ms-wpc://appblock?n=|
|feedback-hub://?contextid=275|LDAP://CN=Partitions,|ms-wpc://exeblock?n=|
|feedback-hub://?contextid=276|LDAP://CN=Policies,CN=System|ms-xgpueject://?AdapterName=%ws|
|feedback-hub://?contextid=330|LDAP://CN=User,|odopen://kfmWizard?launchSource=22&accounttype=personal|
|feedback-hub://?contextid=331|LDAP://DC=|odopen://launch?ScenarioID=13|
|feedback-hub://?contextid=335|ldap://directory.d-trust.net/CN=D-TRUST%20Root%20CA%2|odopen://launch?scenarioId=27&accounttype=personal|
|feedback-hub://?contextid=336|ldap://directory.d-trust.net/CN=D-TRUST%20Root%20Clas|siteoforigin:///|
|feedback-hub://?contextid=338|ldap://ldap.ca.posta.rs/cn=Posta%20CA%20Root,cn=AIA,c|tbauth://|
|feedback-hub://?contextid=341|ldap://ldap.e-szigno.hu/CN=Microsec%20e-Szigno%20Root|tel://|
|feedback-hub://?contextid=394|ldap://ldap.fpki.gov/cn=Federal%20Common%20Policy%20C|tftp://|
|feedback-hub://?contextid=454|LDAP://OU=..,DC=...|value=dlna-playsingle://|
|feedback-hub://?contextid=461|LDAP://RootDSE|vldap://directory.d-trust.net/CN=D-TRUST%20Root%20Clas|
|feedback-hub://?contextid=506|ldap://www.trustcenter.de/CN=TC%20TrustCenter%20Class|vstfs:///|
|feedback-hub://?contextid=516|lt?p=DefaultStartLayout1&amplaunch=ms-get-started://redirect%3Fid=placeholdertiles|vstfs:///Classification/TeamProject/|
|feedback-hub://?contextid=53|lt?p=DefaultStartLayout2&amplaunch=ms-get-started://redirect%3Fid=placeholdertiles|vstfs:///LabManagement/LabExecution/|
|feedback-hub://?contextid=534|mailto://|vstfs:///LabManagement/TeamProjectCollectionHostGroup/|
|feedback-hub://?contextid=535|mapi://|vstfs:///LabManagement/TeamProjectCollectionLibrarySha|
|feedback-hub://?contextid=547|mapi://{|vstfs:///LabManagement/TeamProjectHostGroup/|
|feedback-hub://?contextid=58|mms://|vstfs:///LabManagement/TeamProjectLibraryShare/|
|feedback-hub://?contextid=606|ms-contact-support://|windows.tbauth://|
|feedback-hub://?contextid=610|ms-contact-support://?SearchKey=Audio%20Issues|windowsdefender://|
|feedback-hub://?contextid=615|ms-contact-support://settings/|windowsdefender://account/|
|feedback-hub://?contextid=620|ms-cxh://AADPINRESETAUTH|windowsdefender://accountprotection/|
|feedback-hub://?contextid=630|ms-cxh://AADSSPR|windowsdefender://allowappthroughfolder/|
|feedback-hub://?contextid=64|ms-cxh://AADWEBAUTH|windowsdefender://appbrowser/|
|feedback-hub://?contextid=653|ms-cxh://FRX/AAD|windowsdefender://appguardsettings/|
|feedback-hub://?contextid=654|ms-cxh://FRX/INCLUSIVE|windowsdefender://coreisolation/|
|feedback-hub://?contextid=657|ms-cxh://FRX/INCLUSIVE?start=OobeProvisioningStatus|windowsdefender://coreisolationreboot/|
|feedback-hub://?contextid=658|ms-cxh://FRX/TEAMEDITION|windowsdefender://customscan|
|feedback-hub://?contextid=66|ms-cxh://FRXRDXINCLUSIVE|windowsdefender://devicesecurity/|
|feedback-hub://?contextid=67|ms-cxh://mosetmsalocal|windowsdefender://enableandupdate/|
|feedback-hub://?contextid=68|ms-cxh://MOSETMSALOCAL?ocid=winsettingshome|windowsdefender://enablertp/|
|feedback-hub://?contextid=684|ms-cxh://MOSETMSALOCAL?ocid=winsettingshomerewards|windowsdefender://exclusions/|
|feedback-hub://?contextid=685|ms-cxh://MSACFLPINRESET|windowsdefender://exploitprotection/|
|feedback-hub://?contextid=686|ms-cxh://MSACFLPINRESETSIGNIN|windowsdefender://family/|
|feedback-hub://?contextid=72|ms-cxh://MSACXSIGNINAUTHONLY|windowsdefender://freshstart/|
|feedback-hub://?contextid=738|ms-cxh://MSACXSIGNINPINADD|windowsdefender://fullhistory/|
|feedback-hub://?contextid=75|ms-cxh://MSACXSIGNINPINRESET|windowsdefender://fullscan/|
|feedback-hub://?contextid=755|ms-cxh://MSAPINRESET|windowsdefender://hardware/|
|feedback-hub://?contextid=756|ms-cxh://MSASSPR|windowsdefender://history|
|feedback-hub://?contextid=76|ms-cxh://NTH|windowsdefender://Network|
|feedback-hub://?contextid=79|ms-cxh://NTH/AADRECOVERY|windowsdefender://network/|
|feedback-hub://?contextid=861|ms-cxh://NTHAADNGCFIXME|windowsdefender://perfhealth/|
|feedback-hub://?contextid=874|ms-cxh://NTHAADNGCONLY|windowsdefender://protectedfolders/|
|feedback-hub://?contextid=886|ms-cxh://NTHAADNGCRESET|windowsdefender://providers/|
|feedback-hub://?contextid=920|ms-cxh://NTHAADNGCRESETDESTRUCTIVE|windowsdefender://quarantinehistory/|
|feedback-hub://?contextid=937|ms-cxh://NTHAADNGCRESETNONDESTRUCTIVE|windowsdefender://quickscan/|
|feedback-hub://?contextid=952|ms-cxh://NTHAADORMDM?ngc=enabled|windowsdefender://ransomwareprotection/|
|feedback-hub://?contextid=979|ms-cxh://NTHENTNGCFIXME|windowsdefender://reboot/|
|feedback-hub://?contextid=98|ms-cxh://NTHENTNGCONLY|windowsdefender://samples|
|feedback-hub://?contextid=99|ms-cxh://NTHENTNGCRESET|windowsdefender://securityprocessor/|
|feedback-hub://?tabid=2&categoryid=57|ms-cxh://NTHENTNGCRESETDESTRUCTIVE|windowsdefender://securityprocessortroubleshooting/|
|feedback-hub://?tabid=2&contextid=1010|ms-cxh://NTHENTORMDM|windowsdefender://settings/|
|feedback-hub://?tabid=2&contextid=1032|ms-cxh://NTHENTORMDM?ngc=enabled|windowsdefender://smartscreenpua/|
|feedback-hub://?tabid=2&contextid=1032&newFeedback=true|ms-cxh://NTHEXPEDITEDUPDATE%ws|windowsdefender://threat/|
|feedback-hub://?tabid=2&contextid=869|ms-cxh://NTHEXPEDITEDUPDATELITE%ws|windowsdefender://threatsettings/|
|feedback-hub://?tabid=2&contextid=938|ms-cxh://NTHNGCUPSELL|windowsdefender://update/|
|fldap://ldap.tmca.com.my:389/cn=arl1dp1,ou=ARL,ou=TM|ms-cxh://NTHPRIVACY|windowsdefender://updateandquickscan/|
|ftp://|ms-cxh://SCOOBE|windowsdefender://wdoscan/|
|ftp://%s/|ms-cxh://SCOOBE%ws|wldap://lcr1.certeurope.fr/cn=Certeurope%20Root%20CA%2|
|ftp://%s:%s@%s|ms-cxh://SCOOBE/NDUPMSA%ws|wldap://lcr2.certeurope.fr/cn=Certeurope%20Root%20CA%2|
|ftp://164.214.2.65/pub/gg/tr8350.2/changes.pdf|ms-cxh://SCOOBE/UPGRADE|xbox://|
|ftp://ftp.|ms-cxh-full://SCOOBE/?surface=settingsvaluebanner|xbox://launch?type=%s&xuid=%s|
|ftp://ftp.cs.berkeley.\hich\af40\dbch\af31505\loch\f|ms-gamebarservices:///|XBOX://LI|
|ftp://ftp.cs.berkeley.edu/pub/4bsd/README.Impt.Licen|ms-gamingoverlay://|xbox-tcui://|
|ftp://ftp.info-zip.org/pub/infozip/src/|ms-gamingoverlay://kglcheck|zldap://admindir.admin.ch:389/cn=Swiss%20Government%20|
|zldap://directory.d-trust.net/CN=D-TRUST%20Root%20Clas||||


## Links
  
https://docs.microsoft.com/en-us/windows/win32/search/-search-3x-wds-extidx-prot-implementing
  
https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml
