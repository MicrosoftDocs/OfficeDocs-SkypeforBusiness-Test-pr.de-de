---
title: Remove-CsNetworkBandwidthPolicyProfile
TOCTitle: Remove-CsNetworkBandwidthPolicyProfile
ms:assetid: 7b1f3c8d-486c-4a7e-aa40-57893f249f66
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398609(v=OCS.15)
ms:contentKeyID: 49294502
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkBandwidthPolicyProfile

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt ein Bandbreitenrichtlinienprofil. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird das Bandbreitenrichtlinienprofil mit der Identität "LowBWProfile" entfernt. Da Identitäten eindeutig sein müssen, wird maximal ein Profil entfernt.

    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## BEISPIEL 2

In Beispiel 2 werden alle Verweise auf das Bandbreitenrichtlinienprofil mit der Identität "LowBWProfile" aus allen Standorten entfernt, denen das Profil zugeordnet wurde. Anschließend wird das Profil entfernt. In der ersten Zeile wird zunächst das Cmdlet **Get-CsNetworkSite** aufgerufen, um alle für die Anrufsteuerung konfigurierten Standorte abzurufen. Diese Auflistung von Standorten wird anschließend an das Cmdlet **Where-Object** weitergeleitet, das sie auf lediglich die Standorte beschränkt, deren "BWPolicyProfileID" den Wert "LowBWProfile" aufweist (der Vergleichsoperator "-eq" steht für "equal to"). Diese eingeschränkte Auflistung, die nur Standorte mit dem Wert "LowBWProfile" für den Parameter "BWPolicyProfileID" enthält, wird an das Cmdlet **Set-CSNetworkSite** weitergeleitet, das den Wert von "BWPolicyProfileID" für jeden aufgeführten Standort in einen Nullwert ($null) ändert. Über diese Schritte wurden sämtliche Standorte ermittelt, bei denen der Parameter "BWPolicyProfileID" den Wert "LowBWProfile" aufweist. Dieser Wert wurde dann auf "Null" gesetzt. Anschließend sind keine Standorte mehr vorhanden, die das Profil "LowBWProfile" verwenden. Jetzt wird das Cmdlet **Remove-CsNetworkBandwidthPolicyProfile** für das Profil "LowBWProfile" aufgerufen, um das nicht mehr verwendete Profil zu entfernen.

Um sicherzustellen, dass das Profil in der Netzwerkkonfiguration nicht mehr verwendet wird, führen Sie dieselben Schritte in Zeile 1 für standortübergreifende Richtlinien und Netzwerkregionenverbindungen durch.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Set-CsNetworkSite -BWPolicyProfileID $null
    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## Detaillierte Beschreibung

Im Rahmen der Anrufsteuerung wird eine Bandbreitenrichtlinie dazu verwendet, Bandbreiteneinschränkungen für bestimmte Modalitäten zu definieren. (In Lync Server können Bandbreiteneinschränkungen nur für Audio und Video zugewiesen werden.) Dieses Cmdlet entfernt ein Containerprofil für diese Richtlinien.

WICHTIG: Wenn einem Standort (über das Cmdlet **New-CsNetworkSite** oder das Cmdlet **Set-CsNetworkSite**), einer standortübergreifenden Richtlinie (über das Cmdlet **New-CsNetworkInterSitePolicy** oder das Cmdlet **Set-CsNetworkInterSitePolicy**) oder einer Netzwerkregionenverbindung (über das Cmdlet **New-CsNetworkRegionLink** oder das Cmdlet **Set-CsNetworkRegionLink**) ein Profil zugewiesen wurde, kann dieses nicht entfernt werden. Beim Versuch, das Profil über einen Aufruf des Cmdlets **Remove-CsNetworkBandwidthPolicyProfile** zu entfernen, wird ein Fehler zurückgegeben. Zum Entfernen des Profils muss dieses zunächst aus allen Standorten, standortübergreifenden Richtlinien und Netzwerkregionenverbindungen entfernt werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Remove-CsNetworkBandwidthPolicyProfile** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Ein Zeichenfolgenwert zur eindeutigen Kennzeichnung des zu entfernenden Bandbreitenrichtlinienprofils. Beim Angeben einer Identität wird maximal ein Profil entfernt.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Objekten für ein Netzwerkbandbreiten-Richtlinienprofil.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Es entfernt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType".

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

