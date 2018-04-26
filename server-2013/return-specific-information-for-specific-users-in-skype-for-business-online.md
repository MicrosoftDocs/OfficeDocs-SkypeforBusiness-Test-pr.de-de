---
title: Zurückgeben von bestimmten Informationen zu bestimmten Benutzern
TOCTitle: Zurückgeben von bestimmten Informationen zu bestimmten Benutzern
ms:assetid: bbee85bd-d8a7-4b28-90d7-45c43eee48f6
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362838(v=OCS.15)
ms:contentKeyID: 56269341
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zurückgeben von bestimmten Informationen zu bestimmten Benutzern

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Standardmäßig gibt das Cmdlet [Get-CsOnlineUser](get-csonlineuser.md) eine große Menge von Informationen für jedes Skype for Business Online-Benutzerkonto zurück. Wenn Sie nur eine Teilmenge dieser Informationen benötigen, geben Sie die zurückgegebenen Daten an das Cmdlet **Select-Object** weiter. Im folgenden Befehl werden beispielsweise alle Daten für den Benutzer Ken Myer zurückgegeben und die auf dem Bildschirm angezeigten Informationen mit dem Cmdlet **Select-Object** auf Kens Active Directory-Domänendienste-Anzeigenamen und Wählplan beschränkt:

    Get-CsOnlineUser -Identity "Ken Myer" | Select-Object DisplayName, DialPlan

Der folgende Befehl gibt die Anzeigenamen und Wählpläne für alle Benutzer zurück.

    Get-CsOnlineUser | Select-Object DisplayName, DialPlan

Wenn Sie die Eigenschaften eines Skype for Business Online-Benutzerkontos abrufen möchten, verwenden Sie den folgenden Befehl:

    Get-CsOnlineUser | Get-Member

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

