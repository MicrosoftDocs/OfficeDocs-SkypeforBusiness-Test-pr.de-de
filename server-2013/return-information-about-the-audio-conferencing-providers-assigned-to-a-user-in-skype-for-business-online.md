---
title: Abrufen von Informationen über den einem Benutzer zugewiesenen Audiokonferenzanbieter
TOCTitle: Abrufen von Informationen über den einem Benutzer zugewiesenen Audiokonferenzanbieter
ms:assetid: 7fae822f-9f6c-4381-95c5-879661027925
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362814(v=OCS.15)
ms:contentKeyID: 56269284
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abrufen von Informationen über den einem Benutzer zugewiesenen Audiokonferenzanbieter

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Zum Abrufen von Informationen zu den Audiokonferenzanbietern, die einem Benutzer zugewiesen wurden, verwenden Sie das Cmdlet [Get-CsUserAcp](get-csuseracp.md) und die folgende Syntax:

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

