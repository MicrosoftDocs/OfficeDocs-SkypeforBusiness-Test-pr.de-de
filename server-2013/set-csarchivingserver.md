---
title: Set-CsArchivingServer
TOCTitle: Set-CsArchivingServer
ms:assetid: d4e51c14-34a6-4134-bb71-87bc2f11092d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398923(v=OCS.15)
ms:contentKeyID: 49295523
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsArchivingServer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Enables you to specify a new database location for one or more Archivierungsserver. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsArchivingServer [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingDatabase <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

The command shown in Example 1 changes the location of the Archivierungsdatenbank for the ArchivingServer:atl-cs-001.litwareinc.com Archivierungsserver . In this example, the new database is located at ArchivingDatabase:atl-sql-001.litwareinc.com.

    Set-CsArchivingServer -Identity "ArchivingServer:atl-cs-001.litwareinc.com" -ArchivingDatabase "ArchivingDatabase:atl-sql-001.litwareinc.com"

## Detailed Description

Archivierungsserver provide a way for you to save complete transcripts of the instant messaging (IM) sessions that take place in your organization. In some organizations, it can be useful to have copies of these IM sessions. In other organizations, where records must be kept of all electronic communications, it can be mandatory to have copies of these IM sessions.

Archivierungsserver records the transcript of each IM session (as well as information about when the session took place, and who participated in the session) in a SQL Server database. The location of this database must be specified when you install Archivierungsserver; in most cases, you will not need to change the location of that database. However, if a hardware failure or other problem should occur, you can point Archivierungsserver to a new database by using the **Set-CsArchivingServer** cmdlet.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Set-CsArchivingServer** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsArchivingServer"}

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
<td><p><em>ArchivingDatabase</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Service location where the new Archivierungsdatenbank is located. For example: -ArchivingDatabase ArchivingDatabase:atl-sql-001.litwareinc.com. Make sure you use the service location and not the SQL Server path when specifying the database location.</p></td>
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
<td><p>Suppresses the display of any non-fatal error message that might occur when running the command.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Service location of the Archivierungsserver instance to be modified. For example: -Identity ArchivingServer:atl-cs-001.litwareinc.com. You can retrieve the service location for all your Archiving servers by running this command:</p>
<p>Get-CsService –ArchivingServer | Select-Object Identity</p>
<p>Note that you can leave off the prefix &quot;ArchivingServer:&quot; when specifying an Archiving server. For example: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Input Types

None. The **Set-CsArchivingServer** cmdlet does not accept pipelined input.

## Return Types

The **Set-CsArchivingServer** cmdlet does not return any objects or values. Instead, the cmdlet modifies instances of the Microsoft.Rtc.Management.Xds.DisplayArchivingServer object.

## Siehe auch

#### Weitere Ressourcen

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)

