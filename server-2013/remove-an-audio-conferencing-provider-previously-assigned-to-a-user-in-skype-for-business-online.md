---
title: Entfernen eines Audiokonferenzanbieters, der einem Benutzer zuvor zugewiesen wurde
TOCTitle: Entfernen eines Audiokonferenzanbieters, der einem Benutzer zuvor zugewiesen wurde
ms:assetid: 85d59e6c-d646-4908-9767-adb48763f6de
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362808(v=OCS.15)
ms:contentKeyID: 56269302
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Entfernen eines Audiokonferenzanbieters, der einem Benutzer zuvor zugewiesen wurde

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Führen Sie zum Entfernen aller Audiokonferenzanbieter, die einem Benutzer zugewiesen wurden, das Cmdlet [Remove-CsUserAcp](remove-csuseracp.md) ohne Parameter aus (mit Ausnahme des Parameters **Identity**, der den jeweiligen Benutzer angibt):

    Remove-CsUserAcp -Identity "Ken Myer"

Wenn einem Benutzer mehrere Audiokonferenzanbieter zugewiesen wurden, können Sie einen einzelnen Anbieter entfernen, indem Sie den Parameter **Name** gefolgt vom Namen des zu entfernenden Anbieters verwenden:

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Contoso ACP"

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

