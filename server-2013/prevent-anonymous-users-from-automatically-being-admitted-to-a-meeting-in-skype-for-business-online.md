---
title: Verhindern, dass anonyme Benutzer automatisch zu einer Besprechung zugelassen werden
TOCTitle: Verhindern, dass anonyme Benutzer automatisch zu einer Besprechung zugelassen werden
ms:assetid: 23f120d2-4c39-4509-aa1f-4d186a525075
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362775(v=OCS.15)
ms:contentKeyID: 56269257
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verhindern, dass anonyme Benutzer automatisch zu einer Besprechung zugelassen werden

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Um zu verhindern, dass anonyme Benutzer automatisch zu einer Onlinebesprechung zugelassen werden, verwenden Sie das Cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) und legen die Eigenschaft **AdmitAnonymousUsersByDefault** auf **False** ($False) fest:

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

Wenn Sie diese Option aktivieren möchten, legen Sie die Eigenschaft **AdmitAnonymousUsersByDefault** wieder auf **True** ($True) fest:

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $True

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

