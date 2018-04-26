---
title: Get-CsNetworkRegion
TOCTitle: Get-CsNetworkRegion
ms:assetid: 5c9eef10-16c1-45f7-ae7b-2bee0965b421
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398406(v=OCS.15)
ms:contentKeyID: 49294132
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegion

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft eine oder mehrere Netzwerkregionen ab. Netzwerkregionen repräsentieren Netzwerkhubs oder Backbones in einem Unternehmensnetzwerk. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Beispiel 1 ruft alle für die Organisation definierten Netzwerkregionen ab.

    Get-CsNetworkRegion

## BEISPIEL 2

Beispiel 2 ruft die Netzwerkregionen mit dem Identitätswert "NorthAmerica" ab. Da Identitätswerte eindeutig sind, ruft dieser Befehl maximal eine Netzwerkregion ab.

    Get-CsNetworkRegion -Identity NorthAmerica

## BEISPIEL 3

Dieses Beispiel ruft alle Netzwerkregionen mit Identitätswerten ab, die auf "America" enden. Dazu würden z. B. Regionen mit den Identitätswerten "NorthAmerica", "SouthAmerica" und "CentralAmerica" zählen.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## BEISPIEL 4

Dieses Beispiel ruft alle Netzwerkregionen ab, die "Redmond" (zentraler Standort) zugeordnet sind. Der Befehl ruft zunächst das Cmdlet **Get-CsNetworkRegion** ohne Parameter auf, um eine Auflistung aller Netzwerkregionen abzurufen, die für die Lync Server-Bereitstellung definiert sind. Diese Auflistung wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** filtert diese Auflistung, um nur die Netzwerkregionen zurückzugeben, bei denen der Wert "CentralSite" dem Wert "site:Redmond" entspricht (der Vergleichsoperator "-eq" steht für "equal to").

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## Detaillierte Beschreibung

Eine Netzwerkregion verbindet verschiedene Teile eines Netzwerks, das sich über verschiedene geografische Bereiche erstreckt. Jede Netzwerkregion muss einem zentralen Standort zugeordnet sein. Mit diesem Cmdlet können Sie Informationen über eine oder mehrere Netzwerkregionen abrufen, einschließlich des zugeordneten zentraler Standorts und Einstellungen, die festlegen, ob für Audio- und Videoverbindungen alternative Pfade zulässig sind, und die die Standorte innerhalb der Region mit einer Konfiguration zur Medienumgehung in Bezug setzen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsNetworkRegion** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegion"}

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
<td><p>Dieser Parameter ermöglicht eine Platzhaltersuche nach dem Identitätswert aller für die Organisation konfigurierten Netzwerkregionen. Mit dem Platzhalterzeichen kann nach einer beliebigen Komponente des Identitätswerts gefiltert werden.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Eine eindeutige ID der Netzwerkregion, die abgerufen werden soll. Der Identitätswert liegt als Zeichenfolge vor, die diese Region eindeutig identifiziert. (&quot;Identity&quot; ist mit &quot;NetworkRegionID&quot; identisch.)</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Netzwerkregionsinformationen aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Gibt ein oder mehrere Objekte vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType" zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

