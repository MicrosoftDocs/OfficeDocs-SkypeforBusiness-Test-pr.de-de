---
title: Remove-CsNetworkSubnet
TOCTitle: Remove-CsNetworkSubnet
ms:assetid: 251ddb5c-4837-4810-b46f-d276f9535653
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425726(v=OCS.15)
ms:contentKeyID: 49293447
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSubnet

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt ein vorhandenes Netzwerksubnetz. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird das Subnetz mit dem Identitätswert (d. h. der Subnetz-ID) "172.11.15.0" entfernt.

    Remove-CsNetworkSubnet -Identity 172.11.15.0

## BEISPIEL 2

In Beispiel 2 werden alle Subnetze entfernt, die dem Standort "Vancouver" zugeordnet sind. Hierzu wird das Cmdlet **Get-CsNetworkSubnet** aufgerufen. Dadurch wird eine Auflistung aller Subnetze abgerufen, die in der Lync Server-Bereitstellung definiert wurden. Diese Auflistung von Subnetzen wird dann an das Cmdlet **Where-Object** weitergeleitet. Mit dem Cmdlet **Where-Object** wird diese Auflistung auf die Subnetze beschränkt, deren Parameter "NetworkSiteID" den Wert "Vancouver" besitzt (der Vergleichsoperator "-eq" steht für "equal to"). Da die Auflistung jetzt nur die Subnetze enthält, die dem Standort "Vancouver" zugeordnet sind, wird die Auflistung an das Cmdlet **Remove-CsNetworkSubnet** weitergeleitet, das jedes Element in der Auflistung entfernt.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Remove-CsNetworkSubnet

## Detaillierte Beschreibung

Jedes Subnetz muss einem Netzwerkstandort zugeordnet sein, damit der geografische Standort und der zu diesem Subnetz gehörende Host ermittelt werden können. Verwenden Sie dieses Cmdlet, um ein Netzwerksubnetz zu entfernen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Remove-CsNetworkSubnet** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSubnet"}

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
<td><p>Die eindeutige ID des Subnetzes, das entfernt werden soll. Dieser Wert ist eine IP-Adresse (z. B. 174.11.12.0).</p></td>
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
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Netzwerksubnetzobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType" entfernt.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

