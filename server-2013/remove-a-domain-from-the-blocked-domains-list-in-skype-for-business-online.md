---
title: Entfernen einer Domäne aus der Liste blockierter Domänen
TOCTitle: Entfernen einer Domäne aus der Liste blockierter Domänen
ms:assetid: a11ea475-bb8b-44be-a5a5-4abb2fed42b8
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362830(v=OCS.15)
ms:contentKeyID: 56269319
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Entfernen einer Domäne aus der Liste blockierter Domänen

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Zum Entfernen einer Domäne aus der Liste blockierter Domänen sind zwei Schritte erforderlich. Zunächst müssen Sie das Cmdlet [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) verwenden, um ein Domänenobjekt für die zu entfernende Domäne zu erstellen:

    $x = New-CsEdgeDomainPattern "fabrikam.com"

Nachdem Sie dieses Objekt erstellt haben, verwenden Sie den folgenden Befehl, um die Domäne (in diesem Beispiel ist die Domäne in der Variablen **$x** gespeichert) aus der Liste blockierter Domänen zu entfernen:

    Set-CsTenantFederationConfiguration -BlockedDomains @{Remove=$x}

Wenn Sie alle Domänen aus der Liste blockierter Domänen entfernen möchten, legen Sie den Wert der Eigenschaft **BlockedDomains** auf den Nullwert ($Null) fest:

    Set-CsTenantFederationConfiguration -BlockedDomains $Null

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

