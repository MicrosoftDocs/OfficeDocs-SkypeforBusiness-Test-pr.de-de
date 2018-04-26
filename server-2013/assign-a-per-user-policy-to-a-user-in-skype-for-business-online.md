---
title: Zuordnen einer benutzerbasierte Richtlinie zu einem Benutzer
TOCTitle: Zuordnen einer benutzerbasierte Richtlinie zu einem Benutzer
ms:assetid: 37e07da7-6391-4d6d-a428-c70272897039
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362779(v=OCS.15)
ms:contentKeyID: 56269265
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zuordnen einer benutzerbasierte Richtlinie zu einem Benutzer

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie einem Benutzer eine benutzerbasierte Richtlinie zuordnen möchten, müssen Sie zunächst das geeignete **Grant-Cs**-Cmdlet auswählen (z. B. das Cmdlet [Grant-CsVoicePolicy](grant-csvoicepolicy.md), wenn Sie eine benutzerbasierte VoIP-Richtlinie zuordnen möchten). Führen Sie das Cmdlet aus, und geben Sie unbedingt sowohl die Identität des Benutzers an, dem die Richtlinie zugeordnet werden soll, als auch den Namen der Richtlinie, die zugeordnet werden soll:

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

Wenn Sie allen Benutzern die gleiche Richtlinie zuordnen möchten, verwenden Sie diese Syntax:

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName "RedmondVoicePolicy"

Beachten Sie, dass es aufgrund von unterschiedlichen Lizenzvereinbarungen und je nach Land/Region unterschiedlichen Beschränkungen möglich sein kann, dass einem Benutzer bestimmte Konferenzrichtlinien, Richtlinien für den externen Zugriff oder Mobilitätsrichtlinien nicht zugeordnet werden können. Wenn Sie die benutzerbasierten Richtlinien überprüfen möchten, die einem gegebenen Benutzer (z. B. kenmyer@litwareinc.com) zugeordnet werden können, verwenden Sie je nach Bedarf einen der folgenden Befehle (sowie den Parameter **ApplicableTo**):

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

Die vorstehende Syntax gibt nur die benutzerbasierten Richtlinien zurück, die Ken Myer tatsächlich zugeordnet werden können.

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

