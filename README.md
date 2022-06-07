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

After digging through the registry, there a many URI's that aren't listed in the settings page. As of now, I'm not why MS pulls in some values to show while others are hidden in the reg. Searching the registry for 'URL:' will show you schemes registered to URI's. I have also found an IANA (link at the bottom) that has been helpful while digging into these schemes.

```
Powershell command to search here
```

In the registry, some URI associations will begin with a period such as '.zip'. These URI's will not work when typed in a web browser since they are missing the 'URL Protocol' registry entry, but will maintain their association if the Windows Search feature is used. 






## Links
https://docs.microsoft.com/en-us/windows/win32/search/-search-3x-wds-extidx-prot-implementing
https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml
