---
title: New-CsNetworkRegionLink
TOCTitle: New-CsNetworkRegionLink
ms:assetid: 61a6a7be-8078-4d59-a78a-2f241f6bf800
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398437(v=OCS.15)
ms:contentKeyID: 49294180
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegionLink

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt eine Verknüpfung zwischen zwei Regionen, die für die Anrufsteuerung konfiguriert wurden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsNetworkRegionLink -NetworkRegionLinkID <String> <COMMON PARAMETERS>

    New-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die neue Netzwerkregionenverbindung "NA\_EMEA" zum Verbinden der Regionen "NorthAmerica" und "EMEA" erstellt. Der Name der Regionenverbindung wird als Wert für den Parameter "Identity" festgelegt. (Dieser Wert wird automatisch als Wert des Parameters "NetworkRegionLinkID" zugewiesen.) Zum Erstellen der Verbindung müssen die beiden zu verbindenden Netzwerkregionen angegeben werden, in diesem Fall "NorthAmerica" und "EMEA". In diesem Beispiel wurde auch dem Parameter "BWPolicyProfile" ein Wert zugewiesen. Hierdurch werden die Bandbreiteneinschränkungen, die in diesem Bandbreitenrichtlinienprofil (LowBWLimits) definiert sind, den Verbindungen zwischen diesen Regionen zugewiesen. Wenn keine "BWPolicyProfileID" angegeben wird, gelten keine Bandbreiteneinschränkungen für Verbindungen zwischen diesen beiden Regionen. (Es kann dennoch Einschränkungen zwischen Standorten geben. Einzelheiten finden Sie im Hilfethema zum Cmdlet **New-CsNetworkSite**.)

    New-CsNetworkRegionLink -Identity NA_EMEA -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID LowBWLimits

## Detaillierte Beschreibung

Regionen in einem Netzwerk sind über eine physische WAN-Verbindung verbunden. Dieses Cmdlet definiert eine Verbindung zwischen zwei Regionen und legt die Bandbreiteneinschränkungen für Audio- und Videoverbindungen zwischen diesen Regionen fest.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsNetworkRegionLink** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegionLink"}

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
<td><p>Eine eindeutige ID für die neu erstellte Netzwerkregionenverbindung. Netzwerkregionenverbindungen werden ausschließlich global erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die den eindeutigen Namen zur Identifizierung dieser Verbindung darstellt.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Der Identitätswert (NetworkRegionID) der Region, die mit der durch den Parameter &quot;NetworkRegionID2&quot; identifizierten Region verbunden ist.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Der Identitätswert (NetworkRegionID) der Region, die mit der durch den Parameter &quot;NetworkRegionID1&quot; identifizierten Region verbunden ist.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkID</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Dieser Wert ist mit &quot;Identity&quot; identisch. Sie können nicht gleichzeitig den Identitätswert und den Parameter &quot;NetworkRegionLinkID&quot; angeben. Ein Wert, der für einen der beiden Parameter angegeben wird, gilt automatisch für beide.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Der Identitätswert des Bandbreitenrichtlinienprofils, das die Bandbreiteneinschränkungen für diese Verbindung definiert. Sie können eine Liste der verfügbaren Profile durch Aufrufen des Cmdlets <strong>Get-CsNetworkBandwidthPolicyProfile</strong> abrufen.</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit diesem Cmdlet wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType" erstellt.

## Siehe auch

#### Weitere Ressourcen

[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkSite](new-csnetworksite.md)

