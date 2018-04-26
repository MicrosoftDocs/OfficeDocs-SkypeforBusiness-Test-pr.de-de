---
title: New-CsCdrConfiguration
TOCTitle: New-CsCdrConfiguration
ms:assetid: e5890ac3-7a6c-4609-a866-84c39b76d3a9
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399018(v=OCS.15)
ms:contentKeyID: 49295717
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCdrConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt einen neuen Satz von Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen (KDS). Die KDS-Funktion ermöglicht das Nachverfolgen von Peer-zu-Peer-, VoIP- und Konferenzanrufen. Diese Nutzungsdaten umfassen Informationen wie z. B. Anrufer, Angerufener, Anrufzeitpunkt und Anrufdauer. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 verwendet das Cmdlet **New-CsCdrConfiguration** zum Erstellen einer neuen Gruppe von KDS-Einstellungen mit dem Identitätswert "site:Redmond". Zusätzlich zum Identitätswert "site:Redmond" ist die Eigenschaft "EnableCDR" in den neuen Einstellungen auf "False" festgelegt. Da Standorteinstellungen Vorrang vor globalen Einstellungen haben, bedeutet dies, dass KDS für den Standort "Redmond" nicht verwendet wird – unabhängig davon, ob KDS auf globaler Ebene aktiviert wurde oder nicht.

    New-CsCdrConfiguration -Identity site:Redmond -EnableCDR $False

## BEISPIEL 2

In Beispiel 2 wird gezeigt, wie Sie mit dem Parameter "InMemory" eine neue Auflistung von KDS-Konfigurationseinstellungen erstellen können, die zunächst nur im Arbeitsspeicher vorhanden sind. Dazu werden im ersten Beispiel zunächst das Cmdlet **New-CsCdrConfiguration** und der Parameter "InMemory" verwendet, um eine virtuelle Auflistung von Einstellungen mit dem Identitätswert "site:Redmond" zu erstellen. Diese virtuelle Auflistung wird in der Variablen "$x" gespeichert. Würde die Auflistung nicht in einer Variablen gespeichert, würde sie nach dem Erstellen sofort verloren gehen.

Nachdem die virtuelle Auflistung erstellt wurde, wird mit dem Befehl in Zeile 2 der Wert für die Eigenschaft "EnableCDR" auf "False" ($False) festgelegt. In Zeile 3 wird die virtuelle Auflistung "$x" dann mit dem Cmdlet **Set-CsCdrConfiguration** in eine tatsächliche Auflistung von KDS-Konfigurationseinstellungen umgewandelt, die auf den Standort "Redmond" angewendet werden. Würde das Cmdlet **Set-CsCdrConfiguration** nicht aufgerufen, würde die virtuelle Auflistung verloren gehen, sobald Sie die Windows PowerShell-Sitzung beenden oder die Variable "$x" löschen.

    $x = New-CsCdrConfiguration -Identity site:Redmond -InMemory
    $x.EnableCDR = $False
    Set-CsCdrConfiguration -Instance $x

## Detaillierte Beschreibung

Die KDS-Funktion bietet eine Möglichkeit, die Nutzung von Lync Server-Funktionen wie Voice-over-IP-Anrufe (VoIP), Instant Messaging (Chatnachrichten), Dateiübertragungen, Audio-/Videokonferenzen (A/V) und Anwendungsfreigabesitzungen nachzuverfolgen. KDS (das nur verfügbar ist, wenn Sie den Überwachungsdienst bereitgestellt haben) zeichnet Verwendungsinformationen auf: Hierbei werden z. B. Anrufer, Angerufener, Anrufdauer und Informationen dazu aufgezeichnet, ob Dateien übertragen wurden. (Die KDS-Funktion zeichnet jedoch nicht den Anruf selbst auf.)

Die KDS-Funktion protokolliert auch alle Informationen zu Anruffehlern: ausführliche Diagnosedaten für Peer-zu-Peer-Sitzungen und Konferenzanrufe.

Als Administrator können Sie bestimmen, ob KDS in Ihrer Organisation zum Einsatz kommen soll. Wenn der Überwachungsdienst bereitgestellt wurde, kann KDS mühelos aktiviert oder deaktiviert werden. Sie können KDS außerdem entweder in der gesamten Organisation oder standortbezogen aktivieren oder deaktivieren. Sie können KDS z. B. am Standort "Redmond" aktivieren, aber am Standort "Paris" deaktivieren.

Mit dem Cmdlet **New-CsCdrConfiguration** können Sie Auflistungen neuer KDS-Einstellungen auf Standortebene erstellen. (Neue Einstellungen können nicht global erstellt werden.) Beachten Sie, dass jeder Standort nur eine Auflistung von KDS-Einstellungen hosten kann. Somit können Sie keine neue Auflistung für den Standort Redmond erstellen, wenn für den Standort bereits KDS-Konfigurationseinstellungen vorhanden sind. Sollten Sie dies versuchen, tritt bei dem Ausführen des Befehls ein Fehler auf.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsCdrConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCdrConfiguration"}

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
<td><p>Repräsentiert die eindeutige ID, die einer neuen Auflistung von KDS-Konfigurationseinstellungen zugewiesen werden soll. Da Sie neue Auflistungen nur auf Standortebene erstellen können, weist der Identitätswert immer das Präfix &quot;site:&quot; auf, gefolgt vom Standortnamen, z. B. &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCDR</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Gibt an, ob KDS aktiviert ist. Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Gibt an, ob Kommunikationsdatensätze (KDS) regelmäßig aus der KDS-Datenbank gelöscht werden oder nicht. Wenn dieser Parameter auf &quot;True&quot; festgelegt ist (Standardeinstellung), werden Einträge nach der über die Eigenschaften &quot;KeepCallDetailForDays&quot; (Kommunikationsdatensätze) und &quot;KeepErrorReportForDays&quot; (KDS-Fehler) angegebenen Zeitdauer gelöscht. Bei Festlegung des Parameters auf &quot;False&quot; werden KDS-Einträge nie gelöscht.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Gibt die Anzahl von Tagen an, die Kommunikationsdatensätze (KDS) in der KDS-Datenbank gespeichert werden. Einträge, die älter sind als angegeben, werden automatisch gelöscht. (Beachten Sie, dass der Löschvorgang nur stattfindet, wenn die Eigenschaft &quot;EnablePurging&quot; auf &quot;True&quot; festgelegt wurde.)</p>
<p>&quot;KeepCallDetailForDays&quot; kann auf einen beliebigen ganzzahligen Wert zwischen 1 und 2562 Tage (ungefähr 7 Jahre) festgelegt werden. Der Standardwert lautet 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Gibt die Anzahl von Tagen an, die KDS-Fehlerberichte aufbewahrte werden. Berichte, die älter sind als angegeben, werden automatisch gelöscht. Fehlerberichte zu Kommunikationsdatensätzen sind Diagnoseberichte, die von Clientanwendungen wie z. B. Lync 2013 hochgeladen werden.</p>
<p>Sie können diese Eigenschaft auf einen beliebigen ganzzahligen Wert zwischen 1 und 2562 (etwa 7 Jahre) festlegen. Der Standardwert lautet 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Gibt die lokale Uhrzeit an, zu der abgelaufene Einträge aus der KDS-Datenbank gelöscht werden. Die Uhrzeit wird im 24-Stunden-Format angegeben, wobei Mitternacht (12:00 AM) durch 0 und 11:00 PM durch 23 dargestellt wird. Beachten Sie, dass Sie den Löschvorgang nur zur vollen Stunde ausführen können, d. h., Sie können den Löschvorgang für 4:00 Uhr planen, nicht jedoch für 4:30 oder 4:15 Uhr. Der Standardwert lautet 2 (2:00 Uhr). Es wird empfohlen, den Löschvorgang außerhalb der Geschäftszeiten durchzuführen.</p>
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

Keine. Das Cmdlet **New-CsCdrConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Erstellt Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings".

## Siehe auch

#### Weitere Ressourcen

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

