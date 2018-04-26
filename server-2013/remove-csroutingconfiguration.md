---
title: Remove-CsRoutingConfiguration
TOCTitle: Remove-CsRoutingConfiguration
ms:assetid: 80239fed-89ef-4ccc-be9b-d9149182d0c3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398643(v=OCS.15)
ms:contentKeyID: 49294562
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRoutingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Resets the routing configuration to its default settings. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

This example resets the Global (and only) routing configuration to the default settings. This action deletes all defined voice routes, so we added the Confirm parameter in order to receive a prompt asking whether we really want to perform this action before the removal takes place.

    Remove-CsRoutingConfiguration -Identity Global -Confirm

## Detailed Description

Voice routes contain instructions that tell Lync Server how to route calls from Enterprise Voice users to phone numbers on the public switched telephone network (PSTN) or a private branch exchange (PBX). This cmdlet removes the global (and only) routing configuration, which is a container for all voice routes defined for a Lync Server deployment. "Removing" the routing configuration doesn’t actually remove it; the Global (and only) instance is still there. However, it does set the list of voice routes to the default settings.

WARNING: Removing the routing configuration (in other words, setting the list of voice routes to the default) deletes all defined voice routes for a Lync Server deployment and replaces them with a single route with default settings.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Remove-CsRoutingConfiguration** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRoutingConfiguration"}

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
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>The scope of the routing configuration to remove. This value must be Global.</p></td>
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
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Input Types

Microsoft.Rtc.Management.Policy.Voice.PSTNRoutingSettings object. Accepts pipelined input of a routing configuration object.

## Return Types

This cmdlet removes (resets) an object of type Microsoft.Rtc.Management.Policy.Voice.PSTNRoutingSettings.

## Siehe auch

#### Weitere Ressourcen

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Set-CsRoutingConfiguration](set-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

