---
title: Set-CsNetworkSubnet
TOCTitle: Set-CsNetworkSubnet
ms:assetid: 9e85cdbb-b5fb-48d6-8f95-6e7cba9d9597
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412739(v=OCS.15)
ms:contentKeyID: 49294914
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSubnet

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert ein vorhandenes Netzwerksubnetz. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSubnet [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaskBits <Int32>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird das Subnetz mit dem Identitätswert (der Subnetz-ID) 172.11.15.0 geändert. Dieses Subnetz wurde mit einem neuen Wert für "MaskBits" (25) und mit einem neuen Wert für "NetworkSiteID" (Chicago) geändert.

    Set-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 25 -NetworkSiteID Chicago

## BEISPIEL 2

In Beispiel 2 werden alle Subnetze vom Standort "Vancouver" zum Standort "Chicago" verschoben. Hierzu wird das Cmdlet **Get-CsNetworkSubnet** aufgerufen. Dadurch wird eine Auflistung aller Subnetze abgerufen, die in der Lync Server-Bereitstellung definiert wurden. Diese Auflistung von Subnetzen wird dann an das Cmdlet **Where-Object** weitergeleitet. Mit dem Cmdlet **Where-Object** wird diese Auflistung auf die Subnetze beschränkt, deren Parameter "NetworkSiteID" den Wert "Vancouver" aufweist (der Vergleichsoperator "-eq" steht für "equal to"). Da die Auflistung jetzt nur die Subnetze enthält, die dem Standort "Vancouver" zugeordnet sind, wird die Auflistung an das Cmdlet **Set-CsNetworkSubnet** weitergeleitet. Es wird ein Parameter für das Cmdlet **Set-CsNetworkSubnet** bereitgestellt: NetworkSiteID. Indem der Wert "Chicago" an den Parameter übergeben wird, wird das Cmdlet **Set-CsNetworkSubnet** angewiesen, die Netzwerkstandort-ID für jedes Element in der Auflistung in "Chicago" zu ändern.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Set-CsNetworkSubnet -NetworkSiteID Chicago

## Detaillierte Beschreibung

Jedes Subnetz muss einem Netzwerkstandort zugeordnet sein, damit der geografische Standort und der zu diesem Subnetz gehörende Host ermittelt werden können. Sie können mit diesem Cmdlet den zugeordneten Netzwerkstandort, die Beschreibung des Subnetzes oder die Maskenbits für das Subnetz ändern.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsNetworkSubnet** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSubnet"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Eine Beschreibung des Subnetzes, das geändert werden soll.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Die eindeutige ID für das Subnetz, das geändert werden soll. Dieser Wert ist entweder eine IP-Adresse (z. B. 174.11.12.0) oder ein URL, der mit &quot;http:&quot; oder &quot;https:&quot; beginnt.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>SubnetType</p></td>
<td><p>Ein Verweis auf das Netzwerksubnetzobjekt, das geändert werden soll. Dieses Objekt muss ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType&quot; sein und kann durch Aufrufen des Cmdlets <strong>Get-CsNetworkSubnet</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Die auf das Subnetz anzuwendende Bitmaske.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die Standort-ID des Netzwerkstandorts, auf den dieses Subnetz angewendet werden soll. Sie können Standort-IDs für Ihre Bereitstellung abrufen, indem Sie das Cmdlet <strong>Get-CsNetworkSite</strong> aufrufen.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Netzwerksubnetzobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

