---
title: "\"new-csaddressbookconfiguration\" für die Adressbuchverwaltung"
TOCTitle: "\"new-csaddressbookconfiguration\" für die Adressbuchverwaltung"
ms:assetid: a58ddc8c-ae04-4141-b69e-e45374a67d72
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg429718(v=OCS.15)
ms:contentKeyID: 49294982
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# \"new-csaddressbookconfiguration\" für die Adressbuchverwaltung

 

_**Letztes Änderungsdatum des Themas:** 2012-11-01_

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet "new-csaddressbookconfiguration" lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "new-csaddressbookconfiguration"}

Das Cmdlet "new-csaddressbookconfiguration" erstellt eine neue Konfiguration zum Verwalten des Adressbuchverhaltens. Mit diesem Cmdlet können Sie beispielsweise definieren, ob der Adressbuchdienst Clientdownloaddateien erstellt, wie und ob Normalisierungsregeln verwendet werden, wie lange Delta- und komprimierte Deltadateien beibehalten werden, wie groß Deltadateien werden dürfen, bevor eine neue vollständige Datei erstellt wird, zu welcher Uhrzeit die vollständige Adressbuchdatei erstellt wird, und welche internen Einstellungen für die Synchronisierung von Informationen in der Benutzerdatenbank gelten.

Beispiel:

    new-csaddressbookconfiguration -Identity site:Redmond -KeepDuration 15 -SynchronizePollingInterval 00:10:00

Eine detaillierte Beschreibung des vollständigen Befehls finden Sie im folgenden Abschnitt der Referenz zu den Windows PowerShell-RTCCmdlets von Lync Server.

## Siehe auch

#### Weitere Ressourcen

[new-csaddressbookconfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAddressBookConfiguration)

