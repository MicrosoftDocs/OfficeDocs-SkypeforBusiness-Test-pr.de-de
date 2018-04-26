---
title: Remove-CsConferenceDisclaimer
TOCTitle: Remove-CsConferenceDisclaimer
ms:assetid: 196252a1-2526-4944-9064-01d1846f3266
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398243(v=OCS.15)
ms:contentKeyID: 49293322
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDisclaimer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Löscht den Text aus dem Header und aus dem Hauptteil des in Ihrer Organisation verwendeten Konferenzhaftungsausschlusses. Der Konferenzhaftungssausschluss ist eine Meldung, die Benutzern angezeigt wird, die der Konferenz über einen Link beitreten (z. B. Benutzer, die einen Konferenzlink in einen Browser wie Windows Internet Explorer einfügen). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsConferenceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel werden die Eigenschaftswerte des globalen Haftungsausschlusses zurückgesetzt. Das bedeutet, dass sowohl für den Header als auch für den Text des Haftungsausschlusses Nullwerte festgelegt werden: Der Haftungsausschluss ist also leer.

    Remove-CsConferenceDisclaimer -Identity global

## Detaillierte Beschreibung

Beim Konfigurieren der Konferenzeinstellungen können Administratoren einen rechtlichen Haftungsausschluss eingeben, der den Teilnehmern zum Zeitpunkt des Beitritts zu von Lync Server gehosteten Konferenzen angezeigt wird. In diesem Haftungsausschluss werden im Allgemeinen rechtliche Auflagen und Rechte an geistigem Eigentum für diese Konferenz erläutert. Benutzer können erst dann der Konferenz beitreten, wenn sie den in diesem Haftungsausschluss aufgeführten Bestimmungen zustimmen. Dieser Haftungsausschluss wird nur Benutzern angezeigt, die einer Konferenz über einen Link beitreten.

In Lync Server kann nur eine einzelne, globale Instanz des Konferenzhaftungsausschlusses vorliegen. Mit dem Cmdlet **Remove-CsConferenceDisclaimer** können Sie den Konferenzhaftungsausschluss zurücksetzen: Durch das Ausführen dieses Cmdlets werden sowohl für den Header als auch für den Text des Haftungsausschlusses Nullwerte festgelegt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsConferenceDisclaimer** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDisclaimer"}

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
<td><p>Eindeutiger Identitätswert des zu entfernenden Konferenzhaftungsausschlusses. Auch wenn nur eine einzige globale Instanz des Konferenzhaftungsausschlusses vorliegen darf, müssen Sie dennoch beim Aufrufen des Cmdlets <strong>Remove-CsConferenceDisclaimer</strong> den Parameter &quot;Identity&quot; angeben.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer-Objekt. Das Cmdlet **Remove-CsConferenceDisclaimer** akzeptiert eine weitergeleitete Eingabe von Konferenzhaftungsausschluss-Objekten.

## Rückgabetypen

Keine. Mit dem Cmdlet **Remove-CsConferenceDisclaimer** werden bestehende Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer" auf ihre Standardeigenschaftswerte zurückgesetzt.

## Siehe auch

#### Weitere Ressourcen

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

