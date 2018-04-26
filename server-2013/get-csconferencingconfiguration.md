---
title: Get-CsConferencingConfiguration
TOCTitle: Get-CsConferencingConfiguration
ms:assetid: db4ab3bc-071c-4f73-a3a0-62dc8aed48a1
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398965(v=OCS.15)
ms:contentKeyID: 49295607
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den in Ihrer Organisation verwendeten Konferenzkonfigurationseinstellungen zurück. Mit Konferenzeinstellungen werden z. B. die maximal zulässige Größe für Konferenzinhalte und -handzettel, die Kulanzfrist für Inhalte (d. h. der Zeitraum, in dem Inhalte gespeichert werden, bevor sie gelöscht werden) und die URLs für interne und externe Downloads des unterstützten Clients festgelegt. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 werden Informationen zu allen derzeit in Ihrer Organisation verwendeten Konferenzkonfigurationseinstellungen zurückgegeben. Dazu wird das Cmdlet **Get-CsConferencingConfiguration** ohne Parameter aufgerufen.

    Get-CsConferencingConfiguration

## BEISPIEL 2

In Beispiel 2 werden nur Konfigurationsinformationen zu Konferenzen für den Standort "Redmond" (-Identity "site:Redmond) zurückgegeben. Da Identitätswerte eindeutig sein müssen, wird mit diesem Befehl immer nur maximal eine Auflistung von Konferenzkonfigurationseinstellungen zurückgegeben.

    Get-CsConferencingConfiguration -Identity site:Redmond

## BEISPIEL 3

Der Befehl in Beispiel 3 gibt Informationen zu allen Konferenzkonfigurationseinstellungen zurück, die auf Standortebene angewendet wurden. Hierzu wird das Cmdlet **Get-CsConferencingConfiguration** mit dem Parameter "Filter" aufgerufen. Mit dem Filterwert "site:\*" wird sichergestellt, dass nur die Einstellungen zurückgegeben werden, deren Identitätswert mit der Zeichenfolge "site:" beginnt.

    Get-CsConferencingConfiguration -Filter "site:*"

## BEISPIEL 4

In Beispiel 4 werden Informationen zu allen Konferenzkonfigurationseinstellungen zurückgegeben, bei denen die Organisation nicht auf "Litwareinc" festgelegt ist. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsConferencingConfiguration** ohne Parameter auf. Dadurch wird eine Auflistung aller in der Organisation verwendeten Konferenzkonfigurationseinstellungen zurückgegeben. Die resultierende Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Einstellungen herausfiltert, bei denen die Eigenschaft "Organization" nicht den Wert "Litwareinc" aufweist.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"}

## BEISPIEL 5

In Beispiel 5 werden Informationen nur für die Konferenzkonfigurationseinstellungen zurückgegeben, bei denen der maximale Inhaltsspeicher größer als 100 Megabyte ist. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsConferencingConfiguration** ohne Parameter auf, um eine Auflistung aller Konferenzkonfigurationseinstellungen zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Einstellungen herausfiltert, bei denen der Inhaltsspeicher größer als 100 Megabyte ist.

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMB -gt 100}

## Detaillierte Beschreibung

Bei der Verwaltung von Konferenzen werden zwei Cmdlet-Sätze verwendet. Wenn Sie festlegen möchten, welche Aufgaben Benutzer durchführen oder nicht durchführen können (z. B. Einladen anonymer Teilnehmer zu einer Konferenz, Berechtigung zum Freigeben von Anwendungen bzw. Dateiübertragungen innerhalb einer Konferenz), müssen Sie die **CsConferencingPolicy**-Cmdlets verwenden.

Administratoren verwalten nicht nur die Benutzeraktivitäten, sondern müssen auch den Lync Server Webkonferenzdienst verwalten. Administratoren müssen z. B. die maximale Größe des für eine einzelne Konferenz vorgesehenen Inhaltsspeichers und die Kulanzfrist festlegen können, nach deren Ablauf Konferenzinhalte automatisch gelöscht werden. Sie müssen außerdem die Ports festlegen können, die für Aktivitäten wie z. B. Anwendungsfreigabe und Dateiübertragung verwendet werden.

Diese Aktivitäten können mit den **CsConferencingConfiguration**-Cmdlets verwaltet werden. Mit diesen Cmdlets können Sie die Server selbst verwalten. Mit den **CsConferencingConfiguration**-Cmdlets (die global, auf Standort- und Dienstebene angewendet werden können) wird nicht festgelegt, ob ein Benutzer während einer Konferenz Anwendungen freigeben kann. Wenn die Anwendungsfreigabe zulässig ist, können Sie mit diesen Cmdlets jedoch angeben, welche Ports für diese Aktivität verwendet werden sollen. Ebenso können Sie mit den Cmdlets Speicherbeschränkungen und Ablaufzeiträume sowie Verweise auf interne und externe URLs angeben, über die Benutzer Hilfe und Ressourcen zur Konferenzfunktion erhalten.

Das Cmdlet **Get-CsConferencingConfiguration** bietet Administratoren die Möglichkeit, Informationen zu allen Konferenzkonfigurationseinstellungen zurückzugeben, die derzeit in Ihrer Organisation verwendet werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Get-CsConferencingConfiguration** lokal ausführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, beim Angeben des Identitätswerts der Konferenzkonfigurationseinstellungen Platzhalter zu verwenden. Verwenden Sie beispielsweise folgende Syntax, um alle auf Standortebene konfigurierten Einstellungen zurückzugeben: -Filter &quot;site:*&quot;. Verwenden Sie folgende Syntax, um alle auf Dienstebene konfigurierten Einstellungen zurückzugeben: -Filter &quot;service:*&quot;.</p>
<p>Beachten Sie, dass Sie die Parameter &quot;Identity&quot; und &quot;Filter&quot; nicht in demselben Befehl verwenden können.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutige ID für die abzurufende Auflistung von Konferenzkonfigurationseinstellungen. Verwenden Sie folgende Syntax, um die globalen Einstellungen abzurufen: -Identity global. Verwenden Sie eine Syntax wie die folgende, um auf Standortebene konfigurierte Einstellungen abzurufen: -Identity &quot;site:Redmond&quot;. Verwenden Sie eine Syntax wie die folgende, um auf Dienstebene konfigurierte Einstellungen abzurufen: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Bei Auslassung dieses Parameters werden mit dem Cmdlet <strong>Get-CsConferencingConfiguration</strong> alle derzeit in Ihrer Organisation verwendeten Konferenzkonfigurationseinstellungen zurückgegeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Konferenzkonfigurationsdaten aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsConferencingConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsConferencingConfiguration** werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

