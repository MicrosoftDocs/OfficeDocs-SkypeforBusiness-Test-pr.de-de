---
title: Set-CsCdrConfiguration
TOCTitle: Set-CsCdrConfiguration
ms:assetid: 977f0d3e-796b-43a3-bc0c-82ea91741c52
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398774(v=OCS.15)
ms:contentKeyID: 49294831
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCdrConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine vorhandene Auflistung von Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen (KDS). Die KDS-Funktion ermöglicht das Nachverfolgen von Peer-zu-Peer-, VoIP- und Konferenzanrufen. Diese Nutzungsdaten umfassen Informationen wie z. B. Anrufer, Angerufener, Anrufzeitpunkt und Anrufdauer. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCdrConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird die Tageszeit für den Löschvorgang alter Datensätze festgelegt. In diesem Fall ist die Uhrzeit auf 23 (23:00 Uhr) festgelegt. Mit dem Parameter "Identity" wird sichergestellt, dass diese Änderungen nur an den KDS-Einstellungen mit dem Identitätswert "site:Redmond" vorgenommen werden.

    Set-CsCdrConfiguration -Identity site:Redmond -PurgeHourOfDay 23 

## BEISPIEL 2

Beispiel 2 ist eine Variante des in Beispiel 1 gezeigten Befehls. In diesem Fall wird die Eigenschaft "PurgeHourOfDay" für jede Auflistung von KDS-Konfigurationseinstellungen geändert, die derzeit in der Organisation verwendet werden. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsCdrConfiguration** ohne Parameter auf, um eine Auflistung aller derzeit verwendeten KDS-Einstellungen zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Set-CsCdrConfiguration** weitergeleitet, das den Wert der Eigenschaft "PurgeHourOfDay" für jedes Element in der Auflistung in 23 (23:00 Uhr) ändert.

    Get-CsCdrConfiguration | Set-CsCdrConfiguration -PurgeHourOfDay 23 

## BEISPIEL 3

Beispiel 3 zeigt eine weitere Variante des Befehls aus Beispiel 1. In diesem Beispiel wird die Eigenschaft "PurgeHourOfDay" für alle KDS-Einstellungen geändert, die auf Standortebene konfiguriert wurden. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsCdrConfiguration** mit dem Parameter "Filter" auf. Der Filterwert "site:\*" stellt sicher, dass nur KDS-Einstellungen mit einem Identitätswert herausgefiltert werden, der mit dem Zeichenfolgenwert "site:" beginnt. Die gefilterte Auflistung wird dann an das Cmdlet **Set-CsCdrConfiguration** weitergeleitet, das die Eigenschaft "PurgeHourOfDay" der einzelnen Elemente der Auflistung ändert.

    Get-CsCdrConfiguration -Filter "site:*"| Set-CsCdrConfiguration -PurgeHourOfDay 23

## Detaillierte Beschreibung

Die KDS-Funktion bietet eine Möglichkeit, die Nutzung von Lync Server-Funktionen wie VoIP-Anrufe (Voice over Internet Protocol), Chatnachrichten (Instant Messaging), Dateiübertragungen, Audio-/Videokonferenzen (A/V) und Anwendungsfreigabesitzungen nachzuverfolgen. KDS (das nur verfügbar ist, wenn Sie den Überwachungsdienst bereitgestellt haben) zeichnet Verwendungsinformationen auf: Hierbei werden z. B. Anrufer, Angerufener, Anrufdauer und Informationen dazu aufgezeichnet, ob Dateien übertragen wurden. Die KDS-Funktion zeichnet den eigentlichen Anruf jedoch nicht auf.

Die KDS-Funktion verfolgt auch Informationen zu Anruffehlern nach, so z. B. detaillierte Diagnosedaten für Peer-zu-Peer-Sitzungen und Konferenzanrufe.

Als Administrator können Sie bestimmen, ob KDS in Ihrer Organisation zum Einsatz kommen soll. Sofern der Überwachungsdienst bereitgestellt wurde, kann KDS einfach aktiviert oder deaktiviert werden. Außerdem können Sie diese Entscheidung global (in diesem Fall ist KDS in der gesamten Organisation entweder aktiviert oder deaktiviert) oder auf Standortbasis treffen. Beispielsweise können Sie KDS am Standort Redmond, jedoch nicht am Standort Paris verwenden.

Administratoren können außerdem die KDS-Datenbank verwalten. Sie können beispielsweise die Anzahl von Tagen angeben, für die KDS-Einträge beibehalten werden, bevor sie aus der Datenbank gelöscht werden. Änderungen wie diese können mit dem Cmdlet **Set-CsCdrConfiguration** durchgeführt werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsCdrConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCdrConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCDR</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Zeigt an, ob KDS aktiviert ist. Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Gibt an, ob KDS-Datensätze regelmäßig aus der KDS-Datenbank gelöscht werden. Wenn dieser Parameter auf &quot;True&quot; festgelegt ist (Standardeinstellung), werden Einträge nach dem Zeitraum gelöscht, der in den Eigenschaften &quot;KeepCallDetailForDays&quot; (KDS-Datensätze) und &quot;KeepErrorReportForDays&quot; (KDS-Fehler) angegeben ist. Bei Festlegung des Parameters auf &quot;False&quot; werden KDS-Einträge nie gelöscht.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutige ID, die der Auflistung von KDS-Konfigurationseinstellungen zugewiesen ist. Verwenden Sie folgende Syntax, um auf die globalen Einstellungen zu verweisen: -Identity global. Verwenden Sie eine Syntax wie die folgende, um auf eine Auflistung zu verweisen, die auf Standortebene konfiguriert ist: -Identity site:Redmond. Beachten Sie, dass beim Angeben eines Identitätswerts keine Platzhalterzeichen verwendet werden können.</p>
<p>Bei Auslassung dieses Parameters werden mit dem Cmdlet <strong>Set-CsCdrConfiguration</strong> die globalen Einstellungen geändert.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>CdrSettings-Objekt</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Gibt die Anzahl von Tagen an, die KDS-Datensätze in der KDS-Datenbank gespeichert werden. Einträge, die älter sind als angegeben, werden automatisch gelöscht. (Beachten Sie, dass der Löschvorgang nur stattfindet, wenn die Eigenschaft &quot;EnablePurging&quot; auf &quot;True&quot; festgelegt wurde.)</p>
<p>Sie können diese Eigenschaft auf einen beliebigen ganzzahligen Wert zwischen 1 und 2562 (etwa 7 Jahre) festlegen. Der Standardwert lautet 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Gibt die Anzahl von Tagen an, für die KDS-Fehlerberichte beibehalten werden. Berichte, die älter sind als angegeben, werden automatisch gelöscht. KDS-Fehlerberichte sind Diagnoseberichte, die von Clientanwendungen wie z. B. Lync 2013 hochgeladen werden.</p>
<p>Sie können diese Eigenschaft auf einen beliebigen ganzzahligen Wert zwischen 1 und 2562 (etwa 7 Jahre) festlegen. Der Standardwert lautet 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Gibt die lokale Uhrzeit an, zu der abgelaufene Einträge aus der KDS-Datenbank gelöscht werden. Die Tageszeit wird im 24-Stunden-Format angegeben, wobei 0 für Mitternacht und 23 für 23:00 Uhr steht. Beachten Sie, dass Sie nur die Stunde angeben können; das heißt, dass Sie den Löschvorgang auf 4:00 Uhr, jedoch nicht auf 4:30 Uhr oder 4:15 Uhr festlegen können. Der Standardwert lautet 2 (2:00 Uhr morgens). Es wird empfohlen, den Löschvorgang außerhalb der Geschäftszeiten durchzuführen.</p>
<p>Das Leeren der Datenbank erfolgt nur, wenn &quot;EnablePurging&quot; auf &quot;True&quot; festgelegt wurde.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. Das Cmdlet **Set-CsCdrConfiguration** akzeptiert eine weitergeleitete Eingabe von Konfigurationsobjekten für Kommunikationsdatensätze (KDS).

## Rückgabetypen

Das Cmdlet **Set-CsCdrConfiguration** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CDRSettings" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

