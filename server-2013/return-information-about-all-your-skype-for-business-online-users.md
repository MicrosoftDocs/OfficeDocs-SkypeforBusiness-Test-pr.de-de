---
title: Abrufen von Informationen zu allen Lync Online-Benutzern
TOCTitle: Abrufen von Informationen zu allen Lync Online-Benutzern
ms:assetid: 0b59fadf-67e6-48ea-86f1-2efef500ebdf
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362769(v=OCS.15)
ms:contentKeyID: 56269248
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abrufen von Informationen zu allen Lync Online-Benutzern

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie Informationen zu allen Benutzern abrufen möchten, die für Skype for Business Online aktiviert wurden, verwenden Sie das Cmdlet [Get-CsOnlineUser](get-csonlineuser.md) ohne zusätzliche Parameter:

    Get-CsOnlineUser

Wenn Sie Informationen zu einem einzigen, zufällig ausgewählten Benutzer abrufen möchten (um dieses Konto beispielsweise zu Testzwecken zu verwenden), rufen Sie das Cmdlet **Get-CsOnlineUser** auf, und legen Sie den Parameter **ResultSize** auf 1 fest:

    Get-CsOnlineUser -ResultSize 1

Damit gibt das Cmdlet **Get-CsOnlineUser** Informationen nur zu einem Benutzer zurück, ganz gleich, wie viele Benutzer in der Organisation vorhanden sind. Wenn Sie Informationen zu fünf Benutzern zurückgeben möchten, legen Sie den Wert des Parameters **ResultSize** auf 5 fest:

    Get-CsOnlineUser -ResultSize 5

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

