---
title: Remove-CsNetworkRegion
TOCTitle: Remove-CsNetworkRegion
ms:assetid: 661dce40-f601-4181-b8f1-3277a76d5df4
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398466(v=OCS.15)
ms:contentKeyID: 49294236
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegion

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt eine bestehende Netzwerkregion. Netzwerkregionen stellen Netzwerkhubs oder Backbones in einem Unternehmensnetzwerk dar. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Beispiel 1 entfernt die Netzwerkregion mit dem Identitätswert "NorthAmerica". Da Identitätswerte eindeutig sind, entfernt dieser Befehl nur eine Netzwerkregion.

    Remove-CsNetworkRegion -Identity NorthAmerica

## BEISPIEL 2

Dieses Beispiel entfernt alle Netzwerkregionen, die "Redmond" (zentraler Standort) zugeordnet sind. Der Befehl ruft zunächst das Cmdlet **Get-CsNetworkRegion** ohne Parameter auf, um eine Auflistung aller Netzwerkregionen abzurufen, die für die Lync Server-Bereitstellung definiert sind. Diese Auflistung wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** filtert diese Auflistung, um nur die Netzwerkregionen zurückzugeben, bei denen der Wert "CentralSite" dem Wert "site:Redmond" entspricht (der Vergleichsoperator "-eq" steht für "equal to"). Diese gefilterte Auflistung wird dann an das Cmdlet **Remove-CsNetworkRegion** weitergeleitet, das jedes Element in der Auflistung entfernt.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"} | Remove-CsNetworkRegion

## BEISPIEL 3

Dieses Beispiel entfernt die Netzwerkregion mit dem Identitätswert "NorthAmerica". Eine Region kann jedoch nicht entfernt werden, wenn sie einem Standort zugeordnet ist. Deshalb entfernt dieses Beispiel zunächst alle Zuordnungen zwischen der Region "NorthAmerica" und einem Standort.

Der Befehl im Beispiel ruft zunächst das Cmdlet **Get-CsNetworkSite** ohne Parameter auf, um eine Auflistung aller Netzwerkstandorte abzurufen, die für die Lync Server-Bereitstellung definiert sind. Diese Auflistung wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** filtert diese Auflistung, um nur die Netzwerkstandorte zurückzugeben, bei denen der Wert von "NetworkRegionID" dem Wert "NorthAmerica" entspricht (der Vergleichsoperator "-eq" steht für "equal to"). Diese neue Auflistung wird dann an das Cmdlet **Set-CsNetworkSite** weitergeleitet. Für jeden Standort, dessen Parameter "NetworkRegionID" den Wert "NorthAmerica" aufweist, wird "NetworkRegionID" auf "Null" ($null) festgelegt. Dadurch wird der Verweis auf die Region für diesen Standort entfernt. Ein Standort darf jedoch keine "BypassID" haben, wenn diese keinem Standort zugeordnet ist. Deshalb muss zusätzlich zum Entfernen des Verweises auf die Region durch Festlegen von "NetworkRegionID" auf "Null" auch die Umgehungszuordnung entfernt werden, indem "BypassID" auf "Null" festgelegt wird.

Nach Abschluss von Zeile 1 sind Standorte, die der Region "NorthAmerica" zugeordnet waren, nicht mehr an eine Region oder Umgehungseinstellungen gebunden. An dieser Stelle wird Zeile 2 aufgerufen, die die Netzwerkregion entfernt.

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"} | Set-CsNetworkSite -NetworkRegionID $null -BypassID $null
    Remove-CsNetworkRegion -Identity "NorthAmerica"

## Detaillierte Beschreibung

Eine Netzwerkregion verbindet verschiedene Teile eines Netzwerks, das sich über verschiedene geografische Bereiche erstreckt. Jede Netzwerkregion muss einem zentraler Standort zugeordnet sein. Als zentraler Standort bezeichnet man den Datencenterstandort, an dem der Bandbreitenrichtliniendienst ausgeführt wird. Verwenden Sie dieses Cmdlet zum Entfernen einer Netzwerkregion.

Beachten Sie, dass eine Netzwerkregion nicht entfernt werden kann, wenn sie einem Netzwerkstandort zugeordnet ist (d. h. die "NetworkRegionID" eines Standorts dem Identitätswert der Region entspricht). Wenn Sie versuchen, eine einem Standort zugeordnete Region zu entfernen, wird eine Fehlermeldung ausgegeben.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Remove-CsNetworkRegion** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegion"}

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
<td><p>Die eindeutige ID der Netzwerkregion, die entfernt werden soll. Der Identitätswert liegt als Zeichenfolge vor, die diese Region eindeutig identifiziert.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Netzwerkregionsobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType" entfernt.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

