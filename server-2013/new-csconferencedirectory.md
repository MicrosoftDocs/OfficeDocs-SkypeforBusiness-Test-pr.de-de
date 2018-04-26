---
title: New-CsConferenceDirectory
TOCTitle: New-CsConferenceDirectory
ms:assetid: fd5a4369-10cd-4337-94df-51bcaee4fde9
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg413080(v=OCS.15)
ms:contentKeyID: 49296008
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferenceDirectory

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt ein neues Konferenzverzeichnis für die Verwendung in Ihrer Organisation. Konferenzverzeichnisse helfen den Benutzern von Einwahlkonferenzen beim Suchen nach Konferenzinformationen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsConferenceDirectory -HomePool <String> -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Erstellt ein neues Konferenzverzeichnis mit dem Identitätswert 42. Dieses Verzeichnis wird im Pool "atl-cs-001.litwareinc.com" gehostet.

    New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## Detaillierte Beschreibung

Wenn Sie einen Einwahlkonferenz-URI (Uniform Resource Identifier) erstellen, wird diesem URI eine eindeutige SIP-Adresse zugewiesen. SIP-Adressen lassen sich aber nicht problemlos auf nicht SIP-fähige Geräten übersetzen. Ein Gerät für das Telefonfestnetz (Public Switched Telephone Network, PSTN) kann eine SIP-Adresse beispielweise nicht interpretieren. Aus diesem Grund verwendet Lync Server Konferenzverzeichnisse, anhand derer diese Geräte Einwahlkonferenzen suchen und eine Verbindung mit diesen herstellen können. Hierzu wird ein SIP-Konferenzverzeichnis erstellt, das jedem Einwahlkonferenz-URI zugeordnet ist und statt durch einen SIP-URI durch einen Ganzzahlenwert identifiziert wird. Festnetztelefone und andere Geräte können diese Nummern (statt eines SIP-URI) dann beim Herstellen von Verbindungen zu Konferenzen verwenden. Die Verzeichnisnummer ist in der PSTN-Konferenz-ID enthalten, die Benutzer beim Herstellen einer Verbindung mit einer Einwahlkonferenz eingeben.

Das Cmdlet **New-CsConferenceDirectory** dient zum Erstellen neuer Konferenzverzeichnisse.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsConferenceDirectory** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferenceDirectory"}

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
<td><p><em>HomePool</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Vollqualifizierter Domänennamen (FQDN) des Registrierungsstellenpools , der das neue Konferenzverzeichnis hostet. Beispiel: -Identity atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Eindeutige numerische ID des neuen Konferenzverzeichnisses. Identitäten können einen beliebigen Ganzzahlenwert zwischen 0 und 9999 (einschließlich) aufweisen, müssen aber eindeutig sein. (Es kann beispielsweise nicht zwei Verzeichnisse mit dem Identitätswert 575 geben.) Sie müssen beim Erstellen neuer Verzeichnisse keine numerische Reihenfolge beachten, sondern können beispielsweise ein Verzeichnis mit dem Identitätswert 999, gefolgt von einem Verzeichnis mit dem Identitätswert 2, gefolgt von einem Verzeichnis mit dem Identitätswert 438 usw. erstellen.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
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

Keine. Das Cmdlet **New-CsConferenceDirectory** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Erstellt neue Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories".

## Siehe auch

#### Weitere Ressourcen

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

