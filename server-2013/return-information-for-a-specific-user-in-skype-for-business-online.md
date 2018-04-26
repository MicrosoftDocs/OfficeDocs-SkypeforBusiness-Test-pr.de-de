---
title: Abrufen von Informationen zu einem bestimmten Benutzer
TOCTitle: Abrufen von Informationen zu einem bestimmten Benutzer
ms:assetid: 6c8c2190-8e62-4f92-bbe9-4f692bd7ebf5
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362803(v=OCS.15)
ms:contentKeyID: 56269295
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abrufen von Informationen zu einem bestimmten Benutzer

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Beim Aufruf des Cmdlets [Get-CsOnlineUser](get-csonlineuser.md) gibt es mehrere Möglichkeiten, um auf ein bestimmtes Benutzerkonto zu verweisen. Sie können den Anzeigenamen des Benutzers in den Active Directory-Domänendiensten verwenden:

    Get-CsOnlineUser -Identity "Ken Myer"

Sie können die SIP-Adresse des Benutzers verwenden:

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

Sie können den Benutzerprinzipalnamen (User Principal Name, UPN) des Benutzers verwenden:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

