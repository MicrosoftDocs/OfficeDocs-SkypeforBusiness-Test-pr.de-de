---
title: Set-CsNetworkRegionLink
TOCTitle: Set-CsNetworkRegionLink
ms:assetid: b3d5d203-2aa7-4a54-93d4-30bcda391d68
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412867(v=OCS.15)
ms:contentKeyID: 49295143
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegionLink

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine Verbindung zwischen zwei Netzwerkregionen, die für die Anrufsteuerung konfiguriert wurden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegionLink [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird das Bandbreitenrichtlinienprofil der Netzwerkregionenverbindung "NA\_EMEA" zum Profil "HighBWLimits" geändert. Der Name der Netzwerkregionenverbindung, die geändert werden soll, wird als Wert des Parameters "Identity" festgelegt. Anschließend wird dem Parameter "BWPolicyProfile" der Wert "HighBWLimits" zugewiesen. Dadurch werden die Bandbreiteneinschränkungen, die in diesem Bandbreitenrichtlinienprofil (HighBWLimits) definiert sind, den Verbindungen zwischen diesen Regionen zugewiesen.

    Set-CsNetworkRegionLink -Identity NA_EMEA -BWPolicyProfileID HighBWLimits

## Detaillierte Beschreibung

Regionen in einem Netzwerk sind über eine physische WAN-Verbindung verbunden. Mit diesem Cmdlet wird eine Verbindung zwischen zwei Regionen geändert, sodass Sie die verbundenen Regionen sowie die Bandbreiteneinschränkung bei Audio- und Videoverbindungen zwischen diesen Regionen ändern können.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsNetworkRegionLink** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegionLink"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Identitätswert des Bandbreitenrichtlinienprofils, das die Einschränkungen für diese Verbindung definiert. Sie können eine Liste der verfügbaren Profile durch Aufrufen des Cmdlets <strong>Get-CsNetworkBandwidthPolicyProfile</strong> abrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
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
<td><p>Die eindeutige ID für die Netzwerkregionenverbindung, die geändert werden soll. Netzwerkregionenverbindungen werden ausschließlich global erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die den eindeutigen Namen zur Identifizierung dieser Verbindung darstellt.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>NetworkRegionLinkType</p></td>
<td><p>Ein Objektverweis auf die Netzwerkregionenverbindung. Dieses Objekt muss ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType&quot; sein, das durch Aufrufen des Cmdlets <strong>Get-CsNetworkRegionLink</strong> abgerufen werden kann.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Identitätswert (NetworkRegionID) der Region, die mit der durch die Eigenschaft &quot;NetworkRegionID2&quot; identifizierten Region verbunden ist.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Identitätswert (NetworkRegionID) der Region, die mit der durch die Eigenschaft &quot;NetworkRegionID1&quot; identifizierten Region verbunden ist.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Objekten für die Netzwerkregionenverbindung.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

