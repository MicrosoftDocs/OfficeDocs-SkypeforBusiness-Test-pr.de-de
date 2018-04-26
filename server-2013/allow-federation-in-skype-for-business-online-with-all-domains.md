---
title: Zulassen eines Verbunds mit allen Domänen
TOCTitle: Zulassen eines Verbunds mit allen Domänen
ms:assetid: d26f1057-a76c-447a-9efe-72efdce4c15e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362855(v=OCS.15)
ms:contentKeyID: 56269329
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zulassen eines Verbunds mit allen Domänen

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn es Ihren Benutzern gestattet sein soll, dass sie mit Benutzern aus jeder beliebigen Domäne kommunizieren können, müssen Sie zwei Schritte ausführen. Zunächst erstellen Sie mit dem Cmdlet [New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md) eine Instanz des **AllowAllKnownDomains**-Objekts:

    $x = New-CsEdgeAllowAllKnownDomains

Danach rufen Sie das Cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) auf, und legen Sie den Wert der Eigenschaft **AllowedDomains** auf die Variable fest (in diesem Beispiel **$x**), in der das **AllowAllKnownDomains**-Objekt enthalten ist:

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

