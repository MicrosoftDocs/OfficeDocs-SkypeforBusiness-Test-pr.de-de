---
title: Aufheben der Zuweisung einer benutzerbasierten Richtlinie für einen Benutzer
TOCTitle: Aufheben der Zuweisung einer benutzerbasierten Richtlinie für einen Benutzer
ms:assetid: bdba1d22-28e4-4203-a109-a3fb408783d3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362840(v=OCS.15)
ms:contentKeyID: 56269336
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aufheben der Zuweisung einer benutzerbasierten Richtlinie für einen Benutzer

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie die Zuweisung einer benutzerbasierten Richtlinie für einen Benutzer aufheben möchten, führen Sie das entsprechende **Grant-Cs**-Cmdlet erneut aus (beispielsweise das Cmdlet [Grant-CsVoicePolicy](grant-csvoicepolicy.md), um die Zuweisung einer VoIP-Richtlinie aufzuheben), und legen Sie den Parameter **PolicyName** auf den Nullwert ($Null) fest:

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

Wenn Sie die Zuweisung von VoIP-Richtlinien für alle Benutzer aufheben möchten, verwenden Sie den folgenden Befehl:

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName $Null

Wenn die Zuweisung einer Richtlinie für einen Benutzer aufgehoben wurde, wird dieser Benutzer danach gemäß der globalen Richtlinie verwaltet.

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

