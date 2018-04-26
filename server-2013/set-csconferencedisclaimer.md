---
title: Set-CsConferenceDisclaimer
TOCTitle: Set-CsConferenceDisclaimer
ms:assetid: 97afce6d-b031-466d-a170-3ca50d6df245
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398776(v=OCS.15)
ms:contentKeyID: 49294834
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceDisclaimer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert die Eigenschaftswerte der in Ihrer Organisation verwendeten Konferenzhaftungsausschlüsse. Der Konferenzhaftungssausschluss ist eine Meldung, die Benutzern angezeigt wird, die der Konferenz über einen Link beitreten (z. B. durch Einfügen eines Konferenzlinks in einen Browser wie Windows Internet Explorer). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferenceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Header <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 ändert sowohl die Eigenschaft "Header" als auch die Eigenschaft "Body" für den Konferenzhaftungsausschluss der Organisation. Da nur ein Haftungsausschluss verwendet werden kann, muss beim Ausführen von **Set-CsConferenceDisclaimer** kein Identitätswert angegeben werden.

    Set-CsConferenceDisclaimer -Header "Litwareinc.com Online Conference" -Body "Important note: Conferencing proceedings are recorded and archived."

## Detaillierte Beschreibung

Beim Konfigurieren der Konferenzeinstellungen können Administratoren einen rechtlichen Haftungsausschluss eingeben, der den Teilnehmern zum Zeitpunkt des Beitritts zu von Lync Server gehosteten Konferenzen angezeigt wird. In diesem Haftungsausschluss werden im Allgemeinen rechtliche Auflagen und Rechte an geistigem Eigentum für diese Konferenz erläutert. Benutzer können erst dann der Konferenz beitreten, wenn sie den in diesem Haftungsausschluss aufgeführten Bestimmungen zustimmen. Dieser Haftungsausschluss wird jedoch nur Benutzern angezeigt, die einer Konferenz über einen Link beitreten.

In Lync Server kann nur eine einzelne, globale Instanz des Konferenzhaftungsausschlusses vorliegen. Mit dem Cmdlet **Set-CsConferenceDisclaimer** können Sie den Konferenzhaftungsausschluss ändern, der in Ihrer Organisation verwendet wird.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsConferenceDisclaimer** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Inhalt des Konferenzhaftungsausschlusses.</p></td>
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
<td><p><em>Header</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Titel für den Konferenzhaftungsausschluss.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutiger Identitätswert des Konferenzhaftungsausschlusses. Da nur eine einzelne, globale Instanz des Konferenzhaftungsausschlusses vorliegen kann, müssen Sie beim Aufrufen des Cmdlets <strong>Set-CsConferenceDisclaimer</strong> keinen Identitätswert angeben. Sie können jedoch die folgende Syntax verwenden, um auf den globalen Haftungsausschluss zu verweisen: -Identity global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>ConferenceDisclaimer-Objekt</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer-Objekt. Das Cmdlet **Set-CsConferenceDisclaimer** akzeptiert eine weitergeleitete Eingabe von Konferenzhaftungsausschluss-Objekten.

## Rückgabetypen

Das Cmdlet **Set-CsConferenceDisclaimer** gibt keine Objekte oder Werte zurück. Stattdessen werden mit dem Cmdlet vorhandene Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer" geändert.

## Siehe auch

#### Weitere Ressourcen

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)

