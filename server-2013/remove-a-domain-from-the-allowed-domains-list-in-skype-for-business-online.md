---
title: Entfernen einer Domäne aus der Liste der zulässigen Domänen
TOCTitle: Entfernen einer Domäne aus der Liste der zulässigen Domänen
ms:assetid: 04948582-363b-49bd-8305-166c4c1d0dd9
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362766(v=OCS.15)
ms:contentKeyID: 56269246
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Entfernen einer Domäne aus der Liste der zulässigen Domänen

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Zum Entfernen einer Domäne aus der Liste der zulässigen Domänen ist eine Reihe von Schritten erforderlich. Zuerst müssen Sie einen Befehl wie den folgenden verwenden, um eine Aufstellung aller aktuell in der Liste befindlichen Domänen abzurufen:

    $x = (Get-CsTenantFederationConfiguration).AllowedDomains

Als Nächstes führen Sie diesen Befehl aus, um diese Domänen zu überprüfen:

``` 
$x
```

Notieren Sie sich die Nummer der Position der zu entfernenden Domäne. Wenn es sich hierbei um die erste Domäne in der Liste handelt, hat sie den Indexwert 0. Wenn es sich um die zweite Domäne in der Liste handelt, hat sie den Indexwert 1 usw.

Nachdem Sie die Indexnummer in Erfahrung gebracht haben, verwenden Sie einen Befehl wie den folgenden, um die spezifische Domäne zu entfernen. (Achten Sie darauf, die richtige Indexnummer zu verwenden\!) Mit dem folgenden Befehl wird die erste Domäne in der Liste (Indexnummer 0) entfernt:

    $x.AllowedDomain.RemoveAt(0)

Rufen Sie abschließend das Cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) auf, um Ihre Änderungen in Skype for Business Online zu speichern:

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

