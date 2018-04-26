---
title: Remove-CsNetworkRegionLink
TOCTitle: Remove-CsNetworkRegionLink
ms:assetid: f26cde90-e789-44a7-a304-695c85e64403
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg413012(v=OCS.15)
ms:contentKeyID: 49295873
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegionLink

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt eine Verbindung zwischen zwei Regionen, die für die Anrufsteuerung konfiguriert wurden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel wird die Netzwerkregionenverbindung mit dem Identitätswert "NA\_EMEA" entfernt.

    Remove-CsNetworkRegionLink -Identity NA_EMEA

## BEISPIEL 2

In Beispiel 2 werden alle Netzwerkregionenverbindungen entfernt, die das Bandbreitenrichtlinienprofil namens "HighBWLimits" verwenden. Das erste im Beispiel aufgerufene Cmdlet ist das Cmdlet **Get-CsNetworkRegionLink** (ohne Parameter), das alle Regionenverbindungen abruft. Diese Auflistung von Verbindungen wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** durchläuft die einzelnen Elemente in der Auflistung und prüft den Wert der Eigenschaft "BWPolicyProfileID". Wenn diese Eigenschaft gleich "HighBWLimits" ist (der Vergleichsoperator -eq steht für "equal to"), wird das jeweilige Element an das Cmdlet **Remove-CsNetworkRegionLink** weitergeleitet, welches die Verbindung entfernt.

    Get-CsNetworkRegionLink | Where-Object {$_.BWPolicyProfileID -eq "HighBWLimits"} | Remove-CsNetworkRegionLink

## Detaillierte Beschreibung

Regionen in einem Netzwerk sind über eine physische WAN-Verbindung verbunden. Dieses Cmdlet hat keinerlei Auswirkungen auf physische Verbindungen, entfernt jedoch die Verbindung aus der Anrufsteuerungskonfiguration.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsNetworkRegionLink** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegionLink"}

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
<td><p>Die eindeutige ID der Netzwerkregionenverbindung, die entfernt werden soll. Netzwerkregionenverbindungen werden ausschließlich global erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die den eindeutigen Namen zur Identifizierung dieser Verbindung darstellt.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Objekten für Netzwerkregionenverbindungen.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType" entfernt.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)

