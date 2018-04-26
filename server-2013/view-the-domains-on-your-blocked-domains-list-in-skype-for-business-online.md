---
title: Anzeigen der Domänen in Ihrer Liste der blockierten Domänen
TOCTitle: Anzeigen der Domänen in Ihrer Liste der blockierten Domänen
ms:assetid: 67c65dbf-1a68-4c77-aabd-bed5001b4267
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362797(v=OCS.15)
ms:contentKeyID: 56269283
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Anzeigen der Domänen in Ihrer Liste der blockierten Domänen

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Rufen Sie zum Anzeigen aller Domänen in Ihrer Liste der blockierten Domänen das Cmdlet [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) auf, und leiten Sie die zurückgegebene Daten and das Cmdlet **Select-Object** weiter:

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty BlockedDomains

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

