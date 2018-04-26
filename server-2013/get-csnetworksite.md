---
title: Get-CsNetworkSite
TOCTitle: Get-CsNetworkSite
ms:assetid: 9627869d-101f-4668-bee2-01fce1d84cbd
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398766(v=OCS.15)
ms:contentKeyID: 49294813
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSite

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft einen oder mehrere Netzwerkstandorte ab, die für die Anrufsteuerung oder für erweiterte Notrufdienste (E9-1-1) definiert wurden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Durch den Aufruf des Cmdlets **Get-CsNetworkSite** ohne Parameter werden alle Netzwerkstandorte zurückgegeben, die innerhalb der Lync Server-Bereitstellung für Anrufsteuerung oder E9-1-1 konfiguriert sind.

    Get-CsNetworkSite

## BEISPIEL 2

Mit diesem Befehl wird der Standort mit dem Identitätswert "Redmond" (per Definition auch der Wert für "NetworkSiteID") abgerufen.

    Get-CsNetworkSite -Identity Redmond

## BEISPIEL 3

Der Befehl in Beispiel 3 ruft das Cmdlet **Get-CsNetworkSite** mit dem Parameter "Filter" auf. Der Wert für den Parameter "Filter" lautet "NA\*", d. h. mit diesem Befehl werden alle Standorte abgerufen, deren Identitätswert mit der Zeichenfolge "NA" beginnt, gefolgt von einer beliebigen Anzahl von Zeichen. Es werden beispielsweise Standorte wie "NARedmond", "NAVancouver" und "NAChicago" zurückgegeben.

    Get-CsNetworkSite -Filter NA*

## BEISPIEL 4

In Beispiel 4 werden die beiden Cmdlets **Get-CsNetworkSite** und **Where-Object** zum Abrufen aller Standorte verwendet, die Bestandteil der Region "NorthAmerica" sind. Der Befehl ruft zunächst das Cmdlet **Get-CsNetworkSite** ohne Parameter auf, um alle Netzwerkstandorte abzurufen. Diese Auflistung von Standorten wird anschließend an das Cmdlet **Where-Object** weitergeleitet, das die Auflistung filtert und nur die Standorte in der Auflistung auswählt, bei denen die Eigenschaft "NetworkRegionID" den Wert "NorthAmerica" aufweist (der Vergleichsoperator "-eq" steht für "equal to").

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"}

## Detaillierte Beschreibung

Netzwerkstandorte sind Niederlassungen oder Standorte, die in jeder Region einer Anrufsteuerungs- oder E9-1-1-Bereitstellung konfiguriert sind. Dieses Cmdlet ruft die Einstellungen für einen oder mehrere vorhandene Standorte ab.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Get-CsNetworkSite** lokal ausführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSite"}

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
<td><p>Eine Platzhalterzeichenfolge zum Abrufen mehrerer Standorte, indem der Identitätswert des Standorts mit dem Filterwert abgeglichen wird.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Die eindeutige ID des Netzwerkstandorts, der abgerufen werden soll. Standorte werden nur global erstellt. Sie müssen daher keinen Gültigkeitsbereich festlegen. Stattdessen müssen Sie nur die Standort-ID angeben. (Dieser Wert entspricht dem Wert von &quot;NetworkSiteID&quot; für den Netzwerkstandort.)</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Netzwerkstandortinformationen aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Ruft ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType" ab.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

