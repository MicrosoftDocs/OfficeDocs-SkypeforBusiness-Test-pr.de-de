---
title: Zurückgeben von Informationen zu Ihren Audiokonferenzanbietern
TOCTitle: Zurückgeben von Informationen zu Ihren Audiokonferenzanbietern
ms:assetid: df9c8fc0-8bb6-4416-a5cc-aa9b1601a688
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362848(v=OCS.15)
ms:contentKeyID: 56269351
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zurückgeben von Informationen zu Ihren Audiokonferenzanbietern

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie Informationen zu den Audiokonferenzanbietern zurückgeben möchten, die einem Benutzer zugewiesen sind, verwenden Sie das Cmdlet [Get-CsUserAcp](get-csuseracp.md) mit der folgenden Syntax:

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

