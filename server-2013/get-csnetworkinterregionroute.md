---
title: Get-CsNetworkInterRegionRoute
TOCTitle: Get-CsNetworkInterRegionRoute
ms:assetid: 31c38d92-1cef-40fe-bd04-26e5b373703e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425817(v=OCS.15)
ms:contentKeyID: 49293598
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterRegionRoute

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft Routen ab, die Netzwerkregionen in einer Anrufsteuerungskonfiguration miteinander verbinden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterRegionRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Mit Beispiel 1 wird die Route mit dem Identitätswert "NA\_APAC\_Route" abgerufen.

    Get-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## BEISPIEL 2

In Beispiel 2 werden mit dem Parameter "Filter" sämtliche Routen abgerufen, deren Identitätswert die Zeichenfolge "APAC" enthält.

    Get-CsNetworkInterRegionRoute -Filter *APAC*

## BEISPIEL 3

In diesem Beispiel werden alle Regionenrouten abgerufen, die die Netzwerkregionenverbindung "NA\_EMEA" verwenden. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsNetworkInterRegionRoute** auf. Durch das Aufrufen dieses Cmdlets ohne Parameter werden alle Routen abgerufen, die mit der Anrufsteuerungskonfiguration definiert wurden. Diese Auflistung von Routen wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** ruft sämtliche Elemente in der Auflistung ab, deren Liste "NetworkRegionLinks" den Wert "NA\_EMEA" enthält.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionLinks -eq "NA_EMEA"}

## BEISPIEL 4

In Beispiel 4 werden sämtliche Regionenrouten abgerufen, die die Region "NorthAmerica" enthalten. Der erste Teil dieses Befehls ist ein Aufruf des Cmdlets **Get-CsNetworkInterRegionRoute**. Wenn dieses Cmdlet ohne Parameter aufgerufen wird, werden alle Regionenrouten abgerufen. Diese Auflistung von Routen wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** schränkt die Auflistung auf solche Routen ein, die "NorthAmerica" als eine ihrer Regionen umfassen. Hierzu wird geprüft, ob "NetworkRegionID1" oder (-or) "NetworkRegionID2" den Wert "NorthAmerica" aufweist (der Vergleichsoperator "-eq" steht für "equal to").

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"}

## Detaillierte Beschreibung

Jede Region in einer Anrufsteuerungskonfiguration muss auf jede andere Region zugreifen können. Während die Regionenverbindungen Bandbreiteneinschränkungen für Verbindungen zwischen Regionen festlegen und auch die physischen Verbindungen darstellen, bestimmt eine Route, welchen Pfad die Verbindung von einer Region zur anderen nimmt. Dieses Cmdlet ruft Informationen zu diesen Routenzuordnungen ab.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsNetworkInterRegionRoute** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterRegionRoute"}

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
<td><p>Eine Zeichenfolge, mit der Routen basierend auf einer Übereinstimmung zwischen den Identitätswerten und der Platzhaltersuchzeichenfolge abgerufen werden können, die als Wert für diesen Parameter übergeben wird.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Die eindeutige ID für die Netzwerkregionsroute, die abgerufen werden soll. Netzwerkregionsrouten werden ausschließlich auf globaler Ebene erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, bei der es sich um einen eindeutigen Namen zur Identifizierung einer bestimmten Route handelt.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die regionenübergreifenden Netzwerkrouteninformationen aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit diesem Cmdlet werden ein oder mehrere Objekte vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)

