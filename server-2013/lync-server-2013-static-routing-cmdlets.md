---
title: Cmdlets für das statische Routing
TOCTitle: Cmdlets für das statische Routing
ms:assetid: 71d5e0cd-8412-4383-818a-95b851a4da4b
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg416492(v=OCS.15)
ms:contentKeyID: 49294376
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets für das statische Routing

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Mithilfe von statischen Routen können Administratoren festlegen, über welche Netzwerkrouten SIP-Nachrichten geleitet werden. Wenn der Server eine Nachricht empfängt, überprüft er die Nachrichtenadresse und leitet die Nachricht dann an den als nächsten Hop von einem Administrator festgelegten Server weiter. Die ordnungsgemäße Konfiguration der statischen Routen stellt eine zeitgerechte und akkurate Zustellung der Nachrichten sicher, und dies bei minimalem Serveroverhead.

## Cmdlets für das statische Routing

Sofern Sie vom Microsoft-Support keine anderen Anweisungen erhalten haben, sollten statische Routen für Microsoft Lync Server 2013 mit dem Cmdlet [New-CsStaticRoute](new-csstaticroute.md) erstellt werden. Nach dem Erstellen einer Route können Sie die Cmdlets vom Typ "CsStaticRoutingConfiguration" dazu verwenden, diese Route zu einer Auflistung von statischen Routen hinzuzufügen.

**Statisches Routing**

  -   
    [Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)

  -   
    [New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)

  -   
    [Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

  -   
    [Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

  -   
    [New-CsStaticRoute](new-csstaticroute.md)

  -   
    [Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)

  -   
    [New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)

  -   
    [Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

  -   
    [Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

  -   
    [New-CsSipProxyCustom](new-cssipproxycustom.md)

  -   
    [New-CsSipProxyRealm](new-cssipproxyrealm.md)

  -   
    [New-CsSipProxyTCP](new-cssipproxytcp.md)

  -   
    [New-CsSipProxyTLS](new-cssipproxytls.md)

  -   
    [New-CsSipProxyTransport](new-cssipproxytransport.md)

  -   
    [New-CsSipProxyUseDefault](new-cssipproxyusedefault.md)

  -   
    [New-CsSipProxyUseDefaultCert](new-cssipproxyusedefaultcert.md)

  -   
    [New-CsIssuedCertId](new-csissuedcertid.md)

## Siehe auch

#### Weitere Ressourcen

[Lync Server PowerShell-Blog](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x407)

