---
title: Anzeigen der Domänen in Ihrer Liste der zulässigen Domänen
TOCTitle: Anzeigen der Domänen in Ihrer Liste der zulässigen Domänen
ms:assetid: 13bceaba-5c4f-431f-864f-9e374cafa986
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362772(v=OCS.15)
ms:contentKeyID: 56269251
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Anzeigen der Domänen in Ihrer Liste der zulässigen Domänen

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Verwenden Sie zum Anzeigen aller Domänen in Ihrer Liste der zulässigen Domänen das Cmdlet [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) und die folgende Syntax:

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty AllowedDomains | Select-Object AllowedDomain

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

