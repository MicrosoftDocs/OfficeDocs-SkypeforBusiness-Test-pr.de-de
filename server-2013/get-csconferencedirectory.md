---
title: Get-CsConferenceDirectory
TOCTitle: Get-CsConferenceDirectory
ms:assetid: 2b7927ab-c6b3-42ce-9c27-9825cd47fd77
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425771(v=OCS.15)
ms:contentKeyID: 49293529
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDirectory

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Konferenzverzeichnissen zurück, die für die Verwendung in Ihrer Organisation konfiguriert sind. Konferenzverzeichnisse helfen den Benutzern von Einwahlkonferenzen beim Suchen nach Konferenzinformationen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsConferenceDirectory [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDirectory [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 gibt Informationen zu allen Konferenzverzeichnissen zurück, die für die Verwendung in Ihrer Organisation konfiguriert sind.

    Get-CsConferenceDirectory

## BEISPIEL 2

In Beispiel 2 werden Informationen zum Konferenzverzeichnis mit dem Identitätswert "2" zurückgegeben. Da Identitätswerte eindeutig sein müssen, wird mit diesem Befehl niemals mehr als ein Konferenzverzeichnis zurückgegeben.

    Get-CsConferenceDirectory -Identity 2

## BEISPIEL 3

Im dritten Beispiel werden alle Konferenzverzeichnisse zurückgegeben, die sich im Dienst "UserServer:atl-cs-001.litwareinc.com" befinden. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsConferenceDirectory** ohne Parameter auf, um eine Auflistung aller in der Organisation verwendeten Konferenzverzeichnisse zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Verzeichnisse herausfiltert, bei denen "ServiceID" den Zeichenfolgenwert "UserServer:atl-cs-001.litwareinc.com" besitzt.

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"}

## Detaillierte Beschreibung

Wenn Sie einen Einwahlkonferenz-URI (Uniform Resource Identifier) erstellen, wird diesem URI eine eindeutige SIP-Adresse zugewiesen. SIP-Adressen lassen sich aber nicht problemlos auf nicht SIP-fähige Geräten übersetzen. Ein Gerät für das Telefonfestnetz (Public Switched Telephone Network, PSTN) kann eine SIP-Adresse beispielweise nicht interpretieren. Aus diesem Grund verwendet Lync Server Konferenzverzeichnisse, anhand derer diese Geräte Einwahlkonferenzen suchen und eine Verbindung mit diesen herstellen können. Hierzu wird ein SIP-Konferenzverzeichnis erstellt, das jedem Einwahlkonferenz-URI zugeordnet ist und statt durch einen SIP-URI durch einen Ganzzahlenwert identifiziert wird. Festnetztelefone und andere Geräte können diese Nummern (statt eines SIP-URI) dann beim Herstellen von Verbindungen zu Konferenzen verwenden. Die Verzeichnisnummer ist in der PSTN-Konferenz-ID enthalten, die Benutzer beim Herstellen einer Verbindung mit einer Einwahlkonferenz eingeben.

Mit dem Cmdlet **Get-CsConferenceDirectory** können Sie Informationen zu allen Konferenzverzeichnissen zurückgeben, die für die Verwendung in Ihrer Organisation konfiguriert sind.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsConferenceDirectory** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDirectory"}

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
<td><p>Ermöglicht es Ihnen, Platzhalter beim Festlegen der Identitätswerte des Konferenzverzeichnisses (oder der Konferenzverzeichnisse) zu verwenden, die zurückgegeben werden sollen. Da Verzeichnisidentitätswerte numerisch sind, hat dieser Parameter u. U. einen sehr kleinen Wert. Diese Syntax gibt jedoch alle Konferenzverzeichnisse zurück, die einen Identitätswert aufweisen, der mit 3 beginnt: -Filter &quot;3*&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Numerische ID (beispielsweise 7) des zurückzugebenden Konferenzverzeichnisses. Wenn dieser Parameter ausgelassen wird, werden mit dem Cmdlet <strong>Get-CsConferenceDirectory</strong> alle derzeit in Ihrer Organisation verwendeten Konferenzverzeichnisse zurückgegeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Daten zum Konferenzverzeichnis aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsConferenceDirectory** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsConferenceDirectory** werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

