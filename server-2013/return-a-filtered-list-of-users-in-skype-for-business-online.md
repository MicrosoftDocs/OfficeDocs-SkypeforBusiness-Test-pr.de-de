---
title: Zurückgeben einer gefilterten Benutzerliste
TOCTitle: Zurückgeben einer gefilterten Benutzerliste
ms:assetid: f2c4d13b-8601-4192-8b94-e9a57969da11
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362858(v=OCS.15)
ms:contentKeyID: 56269345
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zurückgeben einer gefilterten Benutzerliste

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie das Cmdlet [Get-CsOnlineUser](get-csonlineuser.md) mit dem Parameter **LdapFilter** oder **Filter** verwenden, können Sie mühelos Informationen zu einer bestimmten Gruppe von Benutzern zurückgeben. Beispielsweise gibt der folgende Befehl alle Benutzer zurück, die in der Finanzabteilung arbeiten:

    Get-CsOnlineUser -LdapFilter "department=Finance"

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

