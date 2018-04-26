---
title: Get-CsNetworkRegionLink
TOCTitle: Get-CsNetworkRegionLink
ms:assetid: dc5cb988-13e2-4af4-8b36-0aaa58ebf1c5
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398972(v=OCS.15)
ms:contentKeyID: 49295619
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegionLink

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft eine oder mehrere Verbindungen zwischen Netzwerkregionen ab, die für die Anrufsteuerung konfiguriert wurden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegionLink [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 werden alle in einer Lync Server-Bereitstellung definierten Netzwerkregionenverbindungen abgerufen.

    Get-CsNetworkRegionLink

## BEISPIEL 2

In Beispiel 2 werden Informationen zu (maximal) einer Netzwerkregionenverbindung mit der Identität "NA\_EMEA" abgerufen.

    Get-CsNetworkRegionLink -Identity NA_EMEA

## BEISPIEL 3

In diesem Beispiel werden mit dem Parameter "Filter" sämtliche Netzwerkregionenverbindungen abgerufen, deren Name (Identity) die Zeichenfolge "EMEA" enthält. Beachten Sie, dass vor und hinter der Zeichenfolge "EMEA" jeweils ein Sternchen (\*) steht. Somit können der Zeichenfolge ein oder mehrere Zeichen vorangestellt oder angehängt werden. In der Zeichenfolge "EMEA" muss lediglich an irgendeiner Stelle die Identität enthalten sein. Dadurch werden Regionen mit Namen wie "NA\_EMEA", "EMEA\_APAC" und "EMEA2\_SA" abgerufen.

    Get-CsNetworkRegionLink -Filter *EMEA*

## BEISPIEL 4

In diesem Beispiel werden alle Netzwerkregionenverbindungen abgerufen, die "EMEA" als eine der beiden verbundenen Regionen enthalten. In dem Beispiel wird zunächst das Cmdlet **Get-CsNetworkRegionLink** ohne Parameter aufgerufen, um alle Regionenverbindungen abzurufen. Diese Auflistung von Verbindungen wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Mit dem Cmdlet **Where-Object** werden nacheinander die Werte der Eigenschaften "NetworkRegionID1" und "NetworkRegionID2" jedes Mitglieds der Aufzählung überprüft. Wenn eine dieser Eigenschaften (also entweder "NetworkRegionID1" oder (-or) "NetworkRegionID2") den Wert "EMEA" aufweist (der Vergleichsoperator (-eq) steht für "equal to"), soll dieses Element in der Auflistung beibehalten und angezeigt werden.

    Get-CsNetworkRegionLink | Where-Object {$_.NetworkRegionID1 -eq "EMEA" -or $_.NetworkRegionID2 -eq "EMEA"}

## Detaillierte Beschreibung

Regionen in einem Netzwerk sind über eine physische WAN-Verbindung verbunden. Dieses Cmdlet ruft eine oder mehrere Regionenverbindungen ab, die in den Netzwerkkonfigurationseinstellungen für eine Lync Server-Bereitstellung definiert sind.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsNetworkRegionLink** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegionLink"}

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
<td><p>Nimmt eine Platzhalterzeichenfolge zum Abrufen von Netzwerkverbindungen an, deren Identitätswert mit der Platzhalterzeichenfolge übereinstimmt.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Eine eindeutige ID der Netzwerkregionenverbindung, die abgerufen werden soll. Netzwerkregionenverbindungen werden ausschließlich global erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die den eindeutigen Namen zur Identifizierung dieser Verbindung darstellt. (Beachten Sie, dass dieser Wert mit &quot;NetworkRegionLinkID&quot; identisch ist.)</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Informationen zu Netzwerkregionenverbindungen aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Gibt ein oder mehrere Objekte vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType" zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)

