---
title: Zuweisen eines Audiokonferenzanbieters zu einem Benutzer
TOCTitle: Zuweisen eines Audiokonferenzanbieters zu einem Benutzer
ms:assetid: 60db6896-9c5c-4d64-ab7e-10d91748587c
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362791(v=OCS.15)
ms:contentKeyID: 56269276
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zuweisen eines Audiokonferenzanbieters zu einem Benutzer

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Das Cmdlet [Set-CsUserAcp](set-csuseracp.md) bietet eine Möglichkeit, einem Benutzer einen Audiokonferenzanbieter zuzuweisen:

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "12065551219" -TollFreeNumbers "18005550712" -ParticipantPasscode "p@ssw0rd" -Domain "sip.contoso.com" -Name "Contoso ACP"

Diese Zuweisung wird erst wirksam, nachdem Sie einen Vertrag mit dem angegebenen Anbieter geschlossen haben.

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

