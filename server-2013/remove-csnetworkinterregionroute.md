---
title: Remove-CsNetworkInterRegionRoute
TOCTitle: Remove-CsNetworkInterRegionRoute
ms:assetid: 91948c03-2bcb-4e25-b0b6-23827e85bbb3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398743(v=OCS.15)
ms:contentKeyID: 49294756
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterRegionRoute

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt eine Route, die Netzwerkregionen mit einer Anrufsteuerungskonfiguration verbindet. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird die Route mit dem Identitätswert "NA\_APAC\_Route" entfernt.

    Remove-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## BEISPIEL 2

In Beispiel 2 werden sämtliche Regionenrouten entfernt, die die Region "NorthAmerica" enthalten. Der erste Teil dieses Befehls ist ein Aufruf des Cmdlets **Get-CsNetworkInterRegionRoute**. Wenn dieses Cmdlet ohne Parameter aufgerufen wird, werden alle Regionenrouten abgerufen. Diese Auflistung von Routen wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** schränkt die Auflistung auf solche Routen ein, die "NorthAmerica" als eine ihrer Regionen umfassen. Hierzu wird geprüft, ob "NetworkRegionID1" oder (-or) "NetworkRegionID2" den Wert "NorthAmerica" aufweist (der Vergleichsoperator "-eq" steht für "equal to"). Nachdem die Auflistung auf lediglich die Routen beschränkt wurde, welche die Region "NorthAmerica" enthalten, wird die Auflistung an das Cmdlet **Remove-CsNetworkInterRegionRoute** weitergeleitet, das jede dieser Routen entfernt.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"} | Remove-CsNetworkInterRegionRoute

## Detaillierte Beschreibung

Jede Region in einer Anrufsteuerungskonfiguration muss auf jede andere Region zugreifen können. Während die Regionenverbindungen Bandbreiteneinschränkungen für Verbindungen zwischen Regionen festlegen und auch die physischen Verbindungen darstellen, bestimmt eine Route, welchen Pfad die Verbindung von einer Region zur anderen nimmt. Dieses Cmdlet entfernt eine dieser Routenzuordnungen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsNetworkInterRegionRoute** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterRegionRoute"}

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
<td><p>Die eindeutige ID für die Netzwerkregionsroute, die entfernt werden soll. Netzwerkregionsrouten werden ausschließlich auf globaler Ebene erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die den eindeutigen Namen zur Identifizierung dieser Route darstellt.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType-Objekt. Akzeptiert eine weitergeleitete Eingabe von regionenübergreifenden Netzwerkroutenobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType" entfernt.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

