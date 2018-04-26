---
title: Get-CsNetworkBandwidthPolicyProfile
TOCTitle: Get-CsNetworkBandwidthPolicyProfile
ms:assetid: 31784852-0cf4-4114-bf92-5eef6f346c47
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425815(v=OCS.15)
ms:contentKeyID: 49293595
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkBandwidthPolicyProfile

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft Richtlinienprofile für die Netzwerkbandbreite auf. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkBandwidthPolicyProfile [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Wenn das Cmdlet **Get-CsNetworkBandwidthPolicyProfile** ohne Parameter aufgerufen wird, werden alle Bandbreitenrichtlinienprofile abgerufen, die innerhalb der Lync Server-Bereitstellung definiert sind.

    Get-CsNetworkBandwidthPolicyProfile

## BEISPIEL 2

In diesem Beispiel wird das Bandbreitenrichtlinienprofil mit dem Identitätswert "LowBWProfile" abgerufen. Da Identitätswerte eindeutig sein müssen, wird maximal ein Profil zurückgegeben.

    Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## BEISPIEL 3

In diesem Beispiel werden mit dem Parameter "Filter" ein oder mehrere Profile angegeben, die mithilfe einer Platzhaltersuchzeichenfolge abgerufen werden sollen. Es wird die Zeichenfolge "\*50MB\*" verwendet, die alle Bandbreitenrichtlinienprofile mit einem Identitätswert mit der Zeichenfolge 50MB abruft. Dies ruft beispielsweise Profile mit dem Identitätswert "BW profile for 50MB links", "50MB audio limit" und "video limits of 50MB" ab.

    Get-CsNetworkBandwidthPolicyProfile -Filter *50MB*

## Detaillierte Beschreibung

Im Rahmen der Anrufsteuerung wird eine Bandbreitenrichtlinie dazu verwendet, Bandbreiteneinschränkungen für bestimmte Modalitäten zu definieren. (In Lync Server können Bandbreiteneinschränkungen nur für Audio und Video zugewiesen werden.) Dieses Cmdlet ruft Containerprofile für diese Richtlinien ab.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsNetworkBandwidthPolicyProfile** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Eine Zeichenfolge mit Platzhalterzeichen, mit der Bandbreitenrichtlinienprofile abgerufen werden, deren Identitätswert mit dem Platzhaltermuster übereinstimmt.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Ein Zeichenfolgenwert zur eindeutigen Kennzeichnung des abzurufenden Bandbreitenrichtlinienprofils. Durch Angabe eines Identitätswerts wird maximal ein Profil abgerufen.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft das Richtlinienprofil für die Netzwerkbandbreite aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Gibt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType" zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

