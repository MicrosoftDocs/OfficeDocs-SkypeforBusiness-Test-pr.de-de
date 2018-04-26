---
title: Zurückgeben einer Liste benutzerbasierter Richtlinien
TOCTitle: Zurückgeben einer Liste benutzerbasierter Richtlinien
ms:assetid: e95a2755-3501-40cc-a704-5ecd01839d76
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362856(v=OCS.15)
ms:contentKeyID: 56269352
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zurückgeben einer Liste benutzerbasierter Richtlinien

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie eine Liste der verfügbaren benutzerbasierten Richtlinien zurückgeben möchten, wählen Sie zunächst das geeignete **Get-Cs**-Cmdlet aus (beispielsweise das Cmdlet [Get-CsVoicePolicy](get-csvoicepolicy.md), wenn Sie die benutzerbasierten VoIP-Richtlinien zurückgeben möchten). Anschließend verwenden Sie die folgende Syntax, um die Identität (Identity) für jede benutzerbasierte Richtlinie zurückzugeben:

    Get-CsVoicePolicy -Filter "tag:*" | Select-Object Identity

Wegen unterschiedlicher Lizenzverträge und unterschiedlicher Länder-/Regionsbeschränkungen ist es vielleicht nicht möglich, einem bestimmten Benutzer bestimmte Konferenzrichtlinien, Richtlinien für den externen Zugriff und Mobilitätsrichtlinien zuzuweisen. Wenn Sie überprüfen möchten, welche benutzerbasierten Richtlinien einem bestimmten Benutzer (beispielsweise kenmyer@litwareinc.com) tatsächlich zugewiesen werden können, verwenden Sie je nach Verwendungsfall einen der folgenden Befehle (und den Parameter **ApplicableTo**):

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

Dieser Befehl gibt nur die benutzerbasierten Richtlinien zurück, die Ken Myer tatsächlich zugewiesen werden können.

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

