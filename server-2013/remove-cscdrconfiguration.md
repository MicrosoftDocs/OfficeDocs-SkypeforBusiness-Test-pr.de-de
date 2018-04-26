---
title: Remove-CsCdrConfiguration
TOCTitle: Remove-CsCdrConfiguration
ms:assetid: 64352746-a03c-434a-9baf-4d9cd630e9da
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398451(v=OCS.15)
ms:contentKeyID: 49294210
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCdrConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt die angegebene Auflistung von Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen (KDS). Die KDS-Funktion ermöglicht das Nachverfolgen von Peer-zu-Peer-, VoIP- und Konferenzanrufen. Diese Nutzungsdaten umfassen Informationen wie z. B. Anrufer, Angerufener, Anrufzeitpunkt und Anrufdauer Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 werden mit dem Cmdlet **Remove-CsCdrConfiguration** die KDS-Einstellungen entfernt, die dem Standort "Redmond" zugewiesen sind. Die Verwendung des Parameters "Identity" stellt sicher, dass nur Einstellungen entfernt werden, die dem angegebenen Standort zugewiesen sind.

    Remove-CsCdrConfiguration -Identity site:Redmond

## BEISPIEL 2

Der Befehl in Beispiel 2 entfernt alle KDS-Einstellungen, die auf Standortebene zugewiesen wurden. Hierzu ruft der Befehl zunächst mit dem Cmdlet **Get-CsCdrConfiguration** und dem Parameter "Filter" die entsprechenden KDS-Einstellungen ab. Der Zeichenfolgenwert "site:\*" stellt sicher, dass nur solche Einstellungen zurückgegeben werden, deren Identitätswert mit der Zeichenfolge "site:" beginnt. Diese gefilterte Auflistung wird dann an das Cmdlet **Remove-CsCdrConfiguration** weitergeleitet, das alle Elemente in der Auflistung löscht.

    Get-CsCdrConfiguration -Filter site:* | Remove-CsCdrConfiguration

## BEISPIEL 3

In Beispiel 3 werden sämtliche KDS-Einstellungen gelöscht, deren Eigenschaft "KeepCallDetailForDays" einen kleineren Wert als 30 aufweist. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsCdrConfiguration** (ohne Parameter) auf, um eine Auflistung aller KDS-Einstellungen zurückzugeben, die derzeit in der Organisation verwendet werden. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Einstellungen herausfiltert, bei denen die Eigenschaft "KeepCallDetailForDays" einen kleineren Wert als 30 aufweist. Die gefilterte Auflistung wird dann an das Cmdlet **Remove-CsCdrConfiguration** weitergeleitet, um sämtliche Elemente in der Auflistung zu löschen.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30} | Remove-CsCdrConfiguration

## Detaillierte Beschreibung

Die KDS-Funktion bietet eine Möglichkeit, die Nutzung von Lync Server-Funktionen wie VoIP-Anrufe (Voice over IP-Protokoll), Chat, Dateiübertragungen, Audio-/Videokonferenzen (A/V) und Anwendungsfreigabesitzungen nachzuverfolgen. KDS (das nur verfügbar ist, wenn Sie den Überwachungsdienst bereitgestellt haben) zeichnet Verwendungsinformationen auf: Es protokolliert Informationen zu Anrufteilnehmern, Anrufdauer, eventuellen Dateiübertragungen usw., zeichnet jedoch nicht den Anruf selbst auf.

Die KDS-Funktion verfolgt auch Informationen zu Anruffehlern nach, so z. B. detaillierte Diagnosedaten für Peer-zu-Peer-Sitzungen und Konferenzanrufe.

Als Administrator können Sie festlegen, ob die KDS-Funktion in Ihrer Organisation verwendet wird. Wenn der Überwachungsdienst bereitgestellt wird, können Sie KDS einfach aktivieren oder deaktivieren. Sie können KDS außerdem entweder in der gesamten Organisation oder standortbezogen aktivieren oder deaktivieren. Sie können KDS z. B. am Standort "Redmond" aktivieren, aber am Standort "Paris" deaktivieren.

Standortbezogene Einstellungen, die Sie mit dem Cmdlet **New-CsCdrConfiguration** erstellen, können später mit dem Cmdlet **Remove-CsCdrConfiguration** entfernt werden. Beim Entfernen standortbezogener Einstellungen unterliegen die KDS-Einstellungen für den betroffenen Standort automatisch den globalen KDS-Konfigurationseinstellungen.

Sie können das Cmdlet **Remove-CsCdrConfiguration** auch für globale KDS-Einstellungen ausführen. Da die globalen Einstellungen jedoch nicht entfernt werden können, werden sie stattdessen auf ihre Standardwerte zurückgesetzt. Nehmen Sie beispielsweise an, Sie setzen den Wert für die Eigenschaft "KeepCallDetailForDays" in den globalen Einstellungen auf 90. Wenn Sie das Cmdlet **Remove-CsCdrConfiguration** für die globalen Einstellungen ausführen, wird diese Eigenschaft auf ihren Standardwert 60 zurückgesetzt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsCdrConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCdrConfiguration"}

## Parameter


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Erforderlich</th>
<th>Typ</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die eindeutige ID für die KDS-Konfigurationseinstellungen, die entfernt werden sollen. Verwenden Sie diese Syntax, um die globalen Einstellungen zu &quot;entfernen&quot;: -Identity global. (Wie bereits erwähnt, können Sie die globalen Einstellungen nicht wirklich entfernen. Sie können ausschließlich die Eigenschaften auf ihre Standardwerte zurücksetzen.) Verwenden Sie eine Syntax wie die folgende, um die Einstellungen auf Standortebene zu entfernen: -Identity site:Redmond. Sie können beim Angeben eines Identitätswerts keine Platzhalter verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. Das Cmdlet **Remove-CsCdrConfiguration** akzeptiert eine weitergeleitete Eingabe von KDS-Konfigurationsobjekten.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings" gelöscht.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

