---
title: Möglichkeit zur Herstellung der Verbindung zu einem deaktivierten Mandanten
TOCTitle: Möglichkeit zur Herstellung der Verbindung zu einem deaktivierten Mandanten
ms:assetid: 7365d31b-173e-4339-b0a3-98ab73a9558f
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362820(v=OCS.15)
ms:contentKeyID: 56269287
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Möglichkeit zur Herstellung der Verbindung zu einem deaktivierten Mandanten

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Damit Sie Windows PowerShell zum Verwalten von Skype for Business Online verwenden können, muss die Eigenschaft **EnableRemotePowerShellAccess** in der Windows PowerShell-Mandantenrichtlinie auf "True" festgelegt sein. Andernfalls schlägt die Verbindung fehl, und Sie erhalten die folgende Fehlermeldung:

    New-PSSession : [admin.vdomain.com] Beim Verarbeiten von Daten vom Remoteserver "admin.vdomain.com" ist folgender Fehler aufgetreten: Die Möglichkeit zum Herstellen der Verbindung zu diesem Mandanten mit einer PowerShell-Remotesitzung wurde deaktiviert. Bitte kontaktieren Sie die Lync-Hilfe, um die Powershell-Richtlinie für diesen Mandanten prüfen zu lassen. Weitere Informationen finden Sie im Artikel "about_Remote_Troubleshooting Help".

Wenn diese Fehlermeldung angezeigt wird, müssen Sie Kontakt zum Office 365-Support aufnehmen und den Windows PowerShell-Remotezugriff aktivieren lassen.

## Siehe auch

#### Konzepte

[Diagnostizieren und Beheben von Problemen mit Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

