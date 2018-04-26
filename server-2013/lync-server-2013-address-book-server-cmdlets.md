---
title: Cmdlets für Adressbuchserver
TOCTitle: Cmdlets für Adressbuchserver
ms:assetid: 33da45da-3c57-4d04-9679-f0e5a0cfd37e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg415643(v=OCS.15)
ms:contentKeyID: 49293628
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets für Adressbuchserver

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Adressbuchserver dienen als Mittler zwischen den Active Directory-Domänendiensten (AD DS) und Microsoft Lync Server 2013. Der Adressbuchserver stellt sicher, dass die in Lync Server 2013 gespeicherten Benutzerinformationen mit den in Active Directory gespeicherten Benutzerinformationen synchronisiert sind. Hierzu werden die Adressbuchdateien regelmäßig mit den in der Benutzerdatenbank gespeicherten Informationen synchronisiert. Lync Server wiederum umfasst verschiedene Cmdlets zur Verwaltung von Adressbuchservern.

## Cmdlets für Adressbuchserver

Sie können die Einstellungen für Adressbuchserver nicht in der Lync Server-Systemsteuerung verwalten. Das primäre Tool zum Verwalten dieser Einstellungen ist Windows PowerShell. In der folgenden Liste werden Cmdlets aufgeführt, die im Rahmen der Verwaltung von Adressbuchservern eingesetzt werden:

**Adressbuchserver**

  -   
    [Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

  -   
    [New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)

  -   
    [Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

  -   
    [Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

<!-- end list -->

  -   
    [Update-CsAddressBook](update-csaddressbook.md)

  -   
    [Debug-CsAddressBookReplication](debug-csaddressbookreplication.md)

<!-- end list -->

  -   
    [Test-CsAddressBookService](test-csaddressbookservice.md)

  -   
    [Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

## Siehe auch

#### Weitere Ressourcen

[Lync Server PowerShell-Blog](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x407)

