---
title: 'Lync Online: Hinzufügen einer Domäne zur Liste der blockierten Domänen'
TOCTitle: Hinzufügen einer Domäne zur Liste der blockierten Domänen
ms:assetid: ea6ebeea-3031-4c42-9a2c-88eaab790636
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362853(v=OCS.15)
ms:contentKeyID: 56269354
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Hinzufügen einer Domäne zur Liste der blockierten Domänen in Lync Online

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Zum Hinzufügen einer Domäne zur Liste der blockierten Domänen verwenden Sie eine Syntax ähnlich der folgenden:

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -BlockedDomains @{Add=$x}

Wie Sie hier sehen, besteht der Befehl aus zwei Schritten. Zuerst verwenden Sie das Cmdlet [New-CsEdgeDomainPattern](new-csedgedomainpattern.md), um ein Domänenobjekt zu erstellen, das für die Domäne steht, die der Liste der blockierten Domänen hinzugefügt werden soll. Anschließend verwenden Sie das Cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) und die Methode **Add** , um diese Domäne der Liste hinzuzufügen (in diesem Beispiel wird die Domäne in der Variablen **$x** gespeichert).

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

