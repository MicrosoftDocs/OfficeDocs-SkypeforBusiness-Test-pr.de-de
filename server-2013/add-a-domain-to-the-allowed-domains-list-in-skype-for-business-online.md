---
title: 'Lync Online: Hinzufügen einer Domäne zur Liste der zulässigen Domänen'
TOCTitle: Hinzufügen einer Domäne zur Liste der zulässigen Domänen
ms:assetid: 7b7f76c8-3047-40be-a938-8ac2868a6bc8
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362818(v=OCS.15)
ms:contentKeyID: 56269298
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Hinzufügen einer Domäne zur Liste der zulässigen Domänen in Lync Online

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Das Hinzufügen der ersten Domäne zur Liste zulässiger Domänen ist ein dreistufiger Vorgang. Zunächst verwenden Sie das Cmdlet [New-CsEdgeDomainPattern](new-csedgedomainpattern.md), um ein Domänenobjekt für die hinzuzufügende Domäne zu erstellen:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

Anschließend erstellen Sie mit dem Cmdlet [New-CsEdgeAllowList](new-csedgeallowlist.md) eine neue Liste zulässiger Domänen, die das Domänenobjekt enthält:

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x

Schließlich verwenden Sie das Cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md), um die neue Liste zulässiger Domänen in Skype for Business Online zu schreiben:

    Set-CsTenantFederationConfiguration -AllowedDomains $newAllowList

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

