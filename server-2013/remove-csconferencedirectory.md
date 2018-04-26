---
title: Remove-CsConferenceDirectory
TOCTitle: Remove-CsConferenceDirectory
ms:assetid: c2c62a14-f3f3-472f-bf91-1fcea9e45425
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412961(v=OCS.15)
ms:contentKeyID: 49295317
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDirectory

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt ein vorhandenes Konferenzverzeichnis. Konferenzverzeichnisse helfen den Benutzern von Einwahlkonferenzen beim Suchen nach Konferenzinformationen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 löscht das Konferenzverzeichnis mit dem Identitätswert 2.

    Remove-CsConferenceDirectory -Identity 2

## BEISPIEL 2

In Beispiel 2 werden alle für den Dienst "UserServer:atl-cs-001.litwareinc.com" gefundenen Konferenzverzeichnisse gelöscht. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsConferenceDirectory** ohne Parameter auf, um eine Auflistung aller Konferenzverzeichnisse zurückzugeben, die derzeit in Ihrer Organisation verwendet werden. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Verzeichnisse herausfiltert, die unter dem Dienst "UserServer:atl-cs-001.litwareinc.com" gehostet werden. Diese gefilterte Auflistung wird an das Cmdlet **Remove-CsConferenceDirectory** weitergeleitet und gelöscht.

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"} | Remove-CsConferenceDirectory

## Detaillierte Beschreibung

Wenn Sie einen Einwahlkonferenz-URI (Uniform Resource Identifier) erstellen, wird diesem URI eine eindeutige SIP-Adresse zugewiesen. SIP-Adressen lassen sich aber nicht problemlos auf nicht SIP-fähige Geräten übersetzen. Ein Gerät für das Telefonfestnetz (Public Switched Telephone Network, PSTN) kann eine SIP-Adresse beispielweise nicht interpretieren. Aus diesem Grund verwendet Lync Server Konferenzverzeichnisse, anhand derer diese Geräte Einwahlkonferenzen suchen und eine Verbindung mit diesen herstellen können. Hierzu wird ein SIP-Konferenzverzeichnis erstellt, das jedem Einwahlkonferenz-URI zugeordnet ist und statt durch einen SIP-URI durch einen Ganzzahlenwert identifiziert wird. Festnetztelefone und andere Geräte können diese Nummern (statt eines SIP-URI) dann beim Herstellen von Verbindungen mit Konferenzen verwenden. Die Verzeichnisnummer ist in der PSTN-Konferenz-ID enthalten, die Benutzer beim Herstellen einer Verbindung mit einer Einwahlkonferenz eingeben.

Konferenzverzeichnisse werden mit dem Cmdlet **New-CsConferenceDirectory** erstellt. Sie müssen möglicherweise gelegentlich ein oder mehrere dieser Verzeichnisse löschen, da Sie beispielsweise den Pool außer Betrieb setzen müssen, in dem die Verzeichnisse gehostet werden. Konferenzverzeichnisse können entfernt werden, indem das Cmdlet **Remove-CsConferenceDirectory** aufgerufen wird. Beachten Sie, dass Sie durch den Aufruf des Cmdlets **Move-CsConferenceDirectory** ein Verzeichnis aus einem Pool in einen anderen verschieben können.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsConferenceDirectory** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDirectory"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Numerischer Identitätswert des Konferenzverzeichnisses, das entfernt werden soll.</p></td>
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
<td><p>Entfernt das Konferenzverzeichnis, wenn vorhanden, selbst wenn der Pool derzeit nicht verfügbar ist, der das Verzeichnis hostet. Mit dem Cmdlet <strong>Remove-CsConferenceDirectory</strong> werden standardmäßig keine Verzeichnisse entfernt, wenn der entsprechende Pool nicht kontaktiert werden kann.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories-Objekt. Das Cmdlet **Remove-CsConferenceDirectory** akzeptiert eine weitergeleitete Eingabe von Konferenzverzeichnisobjekten.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet **Removes-CsConferenceDirectory** Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories" gelöscht.

## Siehe auch

#### Weitere Ressourcen

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)

