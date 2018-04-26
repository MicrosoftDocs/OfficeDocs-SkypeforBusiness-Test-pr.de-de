---
title: Remove-CsConferencingConfiguration
TOCTitle: Remove-CsConferencingConfiguration
ms:assetid: a3dff4b0-100b-46fa-9078-d3b0d4914d87
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412767(v=OCS.15)
ms:contentKeyID: 49294966
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt die angegebene Auflistung von Konferenzkonfigurationseinstellungen. Mit Konferenzeinstellungen werden z. B. die maximal zugelassene Größe für Konferenzinhalte und -handzettel, die Kulanzfrist für Inhalte und die URLs für interne und externe Downloads des unterstützten Clients festgelegt. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 werden die Konfigurationseinstellungen für Konferenzen gelöscht, die auf den Standort "Redmond" angewendet wurden. Wenn solche Standorteinstellungen gelöscht werden, erben die Benutzer dieses Standorts automatisch die Einstellungen, die sich in den globalen Konfigurationseinstellungen für Konferenzen befinden.

    Remove-CsConferencingConfiguration -Identity site:Redmond

## BEISPIEL 2

Mit diesem Befehl werden in Beispiel 2 alle Konfigurationseinstellungen für Konferenzen gelöscht, die auf Standortebene angewendet wurden. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsConferencingConfiguration** mit dem Parameter "Filter" auf. Der Filterwert "site:" stellt sicher, dass nur Einstellungen zurückgegeben werden, deren Identitätswert mit der Zeichenfolge "site:" beginnt. Diese gefilterte Auflistung wird dann an das Cmdlet **Remove-CsConferencingConfiguration** weitergeleitet, das jedes Element in der Auflistung löscht.

    Get-CsConferencingConfiguration -Filter site:* | Remove-CsConferencingConfiguration

## BEISPIEL 3

In Beispiel 3 werden alle Konfigurationseinstellungen für Konferenzen gelöscht, bei denen die Organisation nicht auf "Litwareinc" festgelegt ist. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsConferencingConfiguration** ohne Parameter auf. Anschließend wird eine Auflistung aller in der Organisation verwendeten Konfigurationseinstellungen für Konferenzen zurückgegeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Einstellungen herausfiltert, bei denen die Eigenschaft "Organization" nicht den Wert "Litwareinc" aufweist. Anschließend wird die gefilterte Auflistung an **Remove-CsConferencingConfiguration** weitergeleitet, um sämtliche Einstellungen in der Auflistung zu löschen.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"} | Remove-CsConferencingConfiguration

## Detaillierte Beschreibung

Bei der Verwaltung von Konferenzen werden zwei Cmdlet-Sätze verwendet. Wenn Sie festlegen möchten, welche Aufgaben Benutzer durchführen oder nicht durchführen können (z. B. Einladen anonymer Teilnehmer zu einer Konferenz, Berechtigung zum Freigeben von Anwendungen bzw. Dateiübertragungen innerhalb einer Konferenz usw.), müssen Sie die **CsConferencingPolicy**-Cmdlets verwenden.

Zusätzlich zu Benutzeraktivitäten müssen Administratoren den Webkonferenzdienst verwalten. Administratoren müssen z. B. die maximale Größe des für eine einzelne Konferenz vorgesehenen Inhaltsspeichers und die Kulanzfrist festlegen können, nach deren Ablauf Konferenzinhalte automatisch gelöscht werden. Sie müssen außerdem die Ports festlegen können, die für Aktivitäten wie z. B. Anwendungsfreigabe und Dateiübertragung verwendet werden.

Diese Aktivitäten können mit den **CsConferencingConfiguration**-Cmdlets verwaltet werden. Mit diesen Cmdlets können Sie die Server selbst verwalten. Mit den **CsConferencingConfiguration**-Cmdlets (die global, auf Standort- und Dienstebene angewendet werden können) wird nicht festgelegt, ob ein Benutzer während einer Konferenz Anwendungen freigeben kann. Wenn die Anwendungsfreigabe zulässig ist, können Sie mit diesen Cmdlets jedoch angeben, welche Ports für diese Aktivität verwendet werden sollen. Ebenso können Sie mit den Cmdlets Speicherbeschränkungen und Ablaufzeiträume sowie Verweise auf interne und externe URLs angeben, über die Benutzer Hilfe und Ressourcen zur Konferenzfunktion erhalten.

Das Cmdlet **Remove-CsConferencingConfiguration** bietet die Möglichkeit, alle benutzerdefinierten Auflistungen von Konfigurationseinstellungen für Konferenzen zu löschen, die für die Verwendung in Ihrer Organisation erstellt wurden. Wenn Sie eine Auflistung von Einstellungen löschen, gilt für alle Server, die von diesen Einstellungen zuvor betroffen waren, die nächste Auflistung in der Hierarchie (Dienst-, Standortebene). Wenn die gelöschten Einstellungen auf Dienstebene angewendet wurden, werden die Server von den Standorteinstellungen verwaltet. Wenn keine Einstellungen auf Standortebene vorhanden sind, werden die Server von den globalen Einstellungen verwaltet. Wenn Sie Einstellungen auf Standortebene löschen, werden die Server, die zuvor mit den Standorteinstellungen verwaltet wurden, mit den globalen Einstellungen verwaltet.

Beachten Sie, dass Sie das Cmdlet **Remove-CsConferencingConfiguration** auch für globale Einstellungen ausführen können. In diesem Fall werden die globalen Einstellungen jedoch nicht entfernt, da in Lync Server keine globalen Einstellungen entfernt werden dürfen. Stattdessen werden alle Eigenschaften in der globalen Auflistung auf die Standardwerte zurückgesetzt. Wenn Sie beispielsweise zuvor den Maximalwert für die Inhaltsspeicherung in 200 Megabyte geändert haben, wird diese Eigenschaft auf den Standardwert von 100 Megabyte zurückgesetzt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsConferencingConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingConfiguration"}

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
<td><p>Die eindeutige ID der Auflistung von Konfigurationseinstellungen für Konferenzen, die entfernt werden soll. Verwenden Sie eine Syntax wie die folgende, um die auf Standortebene konfigurierten Einstellungen zu entfernen: -Identity &quot;site:Redmond&quot;. Verwenden Sie eine Syntax wie die folgende, um die auf Dienstebene konfigurierten Einstellungen zu entfernen: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Das Cmdlet <strong>Remove-CsConferencingConfiguration</strong> kann auch für die globalen Einstellungen ausgeführt werden. In diesem Fall werden die Einstellungen jedoch nicht entfernt. Stattdessen werden alle Eigenschaften einfach auf ihre Standardwerte zurückgesetzt.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings-Objekt. Das Cmdlet **Remove-CsConferencingConfiguration** akzeptiert weitergeleitete Instanzen des Konfigurationsobjekts für Einwahlkonferenzen.

## Rückgabetypen

Keine. Mit dem Cmdlet **Remove-CsConferencingConfiguration** werden stattdessen vorhandene Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings" gelöscht.

## Siehe auch

#### Weitere Ressourcen

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

