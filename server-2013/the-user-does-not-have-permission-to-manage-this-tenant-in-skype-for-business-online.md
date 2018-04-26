---
title: Der Benutzer verfügt nicht über die Berechtigung zum Verwalten dieses Mandanten
TOCTitle: Der Benutzer verfügt nicht über die Berechtigung zum Verwalten dieses Mandanten
ms:assetid: 714ccf81-9451-4585-b62d-979f2a606315
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362812(v=OCS.15)
ms:contentKeyID: 56269304
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Der Benutzer verfügt nicht über die Berechtigung zum Verwalten dieses Mandanten

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Sie können nur eine Windows PowerShell-Remoteverbindung zu Skype for Business Online herstellen, wenn Sie ein Mitglied der Gruppe der Mandantenadministratoren sind. Andernfalls schlägt der Verbindungsversuch fehl, und Sie erhalten die folgende Fehlermeldung:

    New-PSSession : [admin.vdomain.com] Beim Verarbeiten von Daten vom Remoteserver "admin.vdomain.com" ist folgender Fehler aufgetreten: Der Benutzer "user@foo.com" verfügt nicht über die Berechtigung zum Verwalten dieses Mandanten. Berechtigungen können gewährt werden, indem der Benutzer der entsprechenden RBAC-Rolle zugewiesen wird. Weitere Informationen finden Sie unter dem Thema "about_Remote_Troubleshooting Help".

Wenn Sie glauben, dass Sie ein Mitglied der Gruppe der Mandantenadministratoren sind oder ein Mitglied dieser Gruppe sein sollten, müssen Sie Kontakt zum Office 365-Support aufnehmen.

## Siehe auch

#### Konzepte

[Diagnostizieren und Beheben von Problemen mit Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

