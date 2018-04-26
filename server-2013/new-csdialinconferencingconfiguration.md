---
title: New-CsDialInConferencingConfiguration
TOCTitle: New-CsDialInConferencingConfiguration
ms:assetid: ac0b6e22-3883-4884-aa94-18f4029c7f1e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412816(v=OCS.15)
ms:contentKeyID: 49295065
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt eine neue Auflistung von Konfigurationseinstellungen für Einwahlkonferenzen. Diese Einstellungen legen fest, wie Lync Server reagiert, wenn Benutzer einer Einwahlkonferenz beitreten oder diese verlassen. Insbesondere werden Informationen dahingehend zurückgegeben, ob Teilnehmer beim Beitritt zu einer Konferenz ihren Namen aufzeichnen müssen und wie (bzw. ob) das System mitteilt, dass jemand einer Besprechung beigetreten ist oder diese verlassen hat. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 erstellt eine neue Auflistung von Konfigurationseinstellungen für Einwahlkonferenzen, die für den Standort "Redmond" gelten. Darüber hinaus wird der optionale Parameter "EnableNameRecording" hinzugefügt, um die Eigenschaft "EnableNameRecording" auf "False" festzulegen.

    New-CSDialInConferencingConfiguration -Identity site:Redmond -EnableNameRecording $False

## BEISPIEL 2

In Beispiel 2 wird der Parameter "InMemory" verwendet, um eine neue Auflistung von Konfigurationseinstellungen für Einwahlkonferenzen zu erstellen, die anfänglich nur im Arbeitsspeicher vorhanden ist. Hierzu wird im Beispiel zunächst das Cmdlet **New-CSDialInConferencingConfiguration** mit dem Parameter "InMemory" aufgerufen, um eine virtuelle Einstellungsauflistung zu erstellen, die in der Variablen "$x" gespeichert wird. (Dieser Auflistung wird der Identitätswert "site:Redmond" zugewiesen.) Nach Erstellen der virtuellen Auflistung wird in Zeile 2 der Wert der Eigenschaft "EnableNameRecording" geändert. In Zeile 3 in diesem Beispiel wird schließlich das Cmdlet **Set-CSDialInConferencingConfiguration** aufgerufen, um die in "$x" gespeicherten virtuellen Konfigurationseinstellungen in eine tatsächliche Einstellungsauflistung umzuwandeln, die auf den Standort "Redmond" angewendet wird.

    $x = New-CSDialInConferencingConfiguration -Identity site:Redmond -InMemory
    $x.EnableNameRecording = $False
    Set-CSDialInConferencingConfiguration -Instance $x

## Detaillierte Beschreibung

Wenn Benutzer einer Einwahlkonferenz beitreten (oder diese verlassen), kann Lync Server auf verschiedene Weise reagieren. Teilnehmer können beispielsweise aufgefordert werden, ihren Namen aufzuzeichnen, bevor sie an der Konferenz teilnehmen können. Administratoren können auch bestimmen, ob Lync Server mitteilen soll, dass Einwahlteilnehmer eine Konferenz verlassen haben oder ihr beigetreten sind.

Die entsprechenden Konferenzverhalten werden mithilfe von Konfigurationseinstellungen für Einwahlkonferenzen verwaltet, die auf globaler oder Standortebene konfiguriert werden können. (Einstellungen auf Standortebene haben Vorrang vor globalen Einstellungen.) Wenn Sie Lync Server erstmals installieren, stehen Ihnen nur die Konfigurationseinstellungen für Einwahlkonferenzen auf globaler Ebene zur Verfügung. Sie können mit dem Cmdlet **New-CSDialInConferencingConfiguration** jedoch neue Einstellungen auf Standortebene erstellen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsDialInConferencingConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingConfiguration"}

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
<td><p>XdsIdentity</p></td>
<td><p>Gibt den Identitätswert der zu erstellenden Konfigurationseinstellungen für Einwahlkonferenzen an. Da diese Einstellungen nur auf Standortebene erstellt werden können, verwenden Sie eine Syntax wie die folgende, bei der auf &quot;site:&quot; der Name des Standorts folgt: -Identity site:Redmond.</p>
<p>Pro Standort kann es nur einen Satz von Konfigurationseinstellungen für Einwahlkonferenzen geben. Beim Beispielbefehl tritt ein Fehler auf, wenn es bereits eine Auflistung von Einstellungen mit dem Identitätswert &quot;site:Redmond&quot; gibt.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableNameRecording</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Bestimmt, ob Benutzer aufgefordert werden, ihren Namen aufzuzeichnen, bevor sie der Konferenz beitreten. Bei Festlegung auf &quot;True&quot; ($True) wird die Namensaufzeichnung angefordert, bei Festlegung auf &quot;False&quot; ($False) wird sie umgangen. Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; werden Ansagen wiedergegeben, wenn ein Teilnehmer einer Konferenz beitritt oder sie verlässt. Bei Festlegung auf &quot;False&quot; (Standardwert) werden beim Beitreten und Verlassen keine Ansagen wiedergegeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>Optional</p></td>
<td><p>EntryExitAnnouncementsType</p></td>
<td><p>Gibt die Aktion an, die das System ausführt, wenn ein Teilnehmer der Konferenz beitritt oder sie verlässt. Gültige Werte:</p>
<p>UseNames. Der Name der Person wird angesagt, sobald sie einer Konferenz beitritt oder sie verlässt (z. B. &quot;Ken Myer verlässt die Konferenz&quot;).</p>
<p>ToneOnly. Ein Ton wird wiedergegeben, wenn ein Teilnehmer einer Konferenz beitritt oder sie verlässt.</p>
<p>Der Standardwert lautet &quot;UseNames&quot;. Beachten Sie, dass Ansagen nur wiedergegeben werden, wenn die Eigenschaft &quot;EntryExitAnnouncementsEnabledByDefault&quot; auf &quot;True&quot; festgelegt ist.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **New-CsDialInConferencingConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Erstellt neue Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration".

## Siehe auch

#### Weitere Ressourcen

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

