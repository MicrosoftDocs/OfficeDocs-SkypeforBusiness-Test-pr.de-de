---
title: Set-CsNetworkConfiguration
TOCTitle: Set-CsNetworkConfiguration
ms:assetid: d54dc154-c092-4be9-8656-f7fec3fbd835
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398927(v=OCS.15)
ms:contentKeyID: 49295529
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert die Einstellungen für eine Netzwerkkonfiguration. Dieses Cmdlet wird meistens zum Aktivieren oder Deaktivieren der Anrufsteuerung verwendet. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfiles <PSListModifier>] [-Confirm [<SwitchParameter>]] [-EnableBandwidthPolicyCheck <$true | $false>] [-Force <SwitchParameter>] [-InterNetworkRegionRoutes <PSListModifier>] [-InterNetworkSitePolicies <PSListModifier>] [-MediaBypassSettings <MediaBypassSettingsType>] [-NetworkRegionLinks <PSListModifier>] [-NetworkRegions <PSListModifier>] [-NetworkSites <PSListModifier>] [-Subnets <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Mit dem Befehl in diesem Beispiel wird die gesamte Anrufsteuerungskonfiguration überprüft und die Anrufsteuerung dann (je nach Ihren Reaktionen auf zurückgegebene Warnungen) aktiviert. Wenn die Anrufsteuerung bereits aktiviert ist (d. h. die Eigenschaft "EnableBandwidthPolicyCheck" weist den Wert "True" auf) und Sie diesen Befehl ausführen, wird lediglich die Überprüfung ausgeführt.

    Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck $True

## Detaillierte Beschreibung

Das Netzwerkkonfigurationsobjekt enthält alle Einstellungen für eine gesamte Anrufsteuerungskonfiguration innerhalb einer Lync Server-Bereitstellung sowie Medienumgehungseinstellungen. Sie können mit diesem Cmdlet einen beliebigen Teil der Anrufsteuerungskonfiguration ändern und müssen es verwenden, wenn die Medienumgehungseinstellungen geändert werden sollen. Zum Ändern der meisten Anrufsteuerungskonfigurationseinstellungen wird jedoch empfohlen, objekttypspezifische Cmdlets zu verwenden. Um beispielsweise mit Netzwerkregionen zu arbeiten, verwenden Sie die Cmdlets, die mit dem Substantiv "CsNetworkRegion" enden, statt den Parameter "NetworkRegions" dieses Cmdlets zu ändern.

Der Zweck dieses Cmdlets besteht in erster Linie darin, die Anrufsteuerung zu aktivieren (und zu deaktivieren) und Medienumgehungseinstellungen anzuwenden. Nachdem Sie die verschiedenen Komponenten eingerichtet haben, die für Ihre Konfiguration erforderlich sind (z. B. Regionen, Standorte und Subnetze), müssen Sie die Konfiguration aktivieren. Ansonsten funktioniert sie nicht. Setzen Sie dazu einfach den Parameter "EnableBandwidthPolicyCheck" auf "True". Beachten Sie jedoch, dass die Anrufsteuerung durch Ausführen dieses Cmdlets, bei dem "EnableBandwidthPolicyCheck" auf "True" festgelegt ist, nicht sofort aktiviert wird. Bevor sie aktiviert werden kann, wird eine Reihe von Überprüfungen ausgeführt, um sicherzustellen, dass das Setup richtig konfiguriert ist. Bei jedem Fehler bzw. jeder Diskrepanz im Setup wird eine Warnung angezeigt, mit der Sie gefragt werden, ob Sie die Aktivierung der Anrufsteuerung trotz des Problems fortsetzen möchten. Falls Sie sich zum Fortfahren entschließen (durch Drücken der Eingabetaste oder der Taste "Y"), wird die Überprüfung fortgesetzt. Tritt ein weiteres Problem auf, werden Sie erneut gefragt.

Wenn Sie die gesamte Überprüfung durchlaufen und den Vorgang bei jeder Warnung fortsetzen, wird "EnableBandwidthPolicyCheck" auf "True" festgelegt und die Anrufsteuerung aktiviert. Sie wird jedoch wahrscheinlich nicht erwartungsgemäß funktionieren, bevor die Probleme behoben wurden. Sollten Sie sich während der Überprüfung an einem beliebigen Punkt entschließen, den Vorgang anzuhalten (durch Eingabe von "N" bei einer Warnung), wird die Überprüfung beendet, und "EnableBandwidthPolicyCheck" bleibt auf "False" gesetzt (Standardeinstellung).

Wenn für "EnableBandwidthPolicyCheck" bereits "True" festgelegt wurde, können Sie das Cmdlet **Set-CsNetworkConfiguration** aufrufen und den Wert "True" an den Parameter "EnableBandwidthPolicyCheck" übergeben, um die Überprüfung auszuführen, ohne Einstellungen zu ändern. Ist "EnableBandwidthPolicyCheck" auf "True" festgelegt, wird die Überprüfung außerdem jedes Mal ausgeführt, wenn Sie das Cmdlet **Set-CsNetworkConfiguration** aufrufen, um Änderungen vorzunehmen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsNetworkConfiguration** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkConfiguration"}

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
<td><p><em>BWPolicyProfiles</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung aller Bandbreitenrichtlinienprofile, die Standorten, standortübergreifenden Richtlinien und Netzwerkregionenverbindungen zugewiesen werden können. Jedes Bandbreitenrichtlinienprofil enthält Bandbreiteneinschränkungen (allgemeine Einschränkungen und Sitzungseinschränkungen) für Audio- und/oder Videoverbindungen. Eine vollständige Liste der Bandbreitenrichtlinienprofile können Sie mit dem Cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong> abrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBandwidthPolicyCheck</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Wenn Sie diesen Parameter auf &quot;True&quot; festlegen, wird die gesamte Anrufsteuerungskonfiguration überprüft. Wenn alle Überprüfungen erfolgreich sind oder Sie alle Warnungen ignorieren, wird die Anrufsteuerung aktiviert. Ist eine Überprüfung nicht erfolgreich, können Sie sie beenden. Der Wert von &quot;EnableBandwidthPolicyCheck&quot; wird dann nicht geändert. Vor dem Ausführen der Überprüfung müssen zwischen jedem Netzwerkregionenpaar Regionenrouten definiert werden.</p>
<p>Wenn Sie diesen Wert auf &quot;False&quot; festlegen, wird die Anrufsteuerung deaktiviert.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Dieser Parameter hat keinen Wert. Wenn Sie diesen Parameter angeben, werden alle Änderungen an der Konfiguration, einschließlich ihrer Aktivierung, ohne Warnungen oder Überprüfungen vorgenommen.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Dieser Wert ist immer &quot;Global&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>NetworkConfigurationSettings</p></td>
<td><p>Ein Verweis auf ein Netzwerkkonfigurationsobjekt. Dieses Objekt muss ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings&quot; sein und kann über das Cmdlet <strong>Get-CsNetworkConfiguration</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>InterNetworkRegionRoutes</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung aller Netzwerkregionsrouten, die innerhalb der Anrufsteuerungskonfiguration definiert sind. Sie können alle Mitglieder dieser Auflistung mit dem Cmdlet <strong>Get-CsNetworkInterRegionRoute</strong> abrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkSitePolicies</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung von standortübergreifenden Netzwerkrichtlinien, die innerhalb der Anrufsteuerungskonfiguration definiert sind. Sie können alle Mitglieder dieser Auflistung mit dem Cmdlet <strong>Get-CsNetworkInterSitePolicy</strong> abrufen.</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaBypassSettings</em></p></td>
<td><p>Optional</p></td>
<td><p>MediaBypassSettingsType</p></td>
<td><p>Ein Verweis auf ein Objekt, das die globalen Medienumgehungseinstellungen für die Anrufsteuerungskonfiguration definiert. Wenn Sie diesen Wert festlegen, werden alle vorhandenen Medienumgehungseinstellungen überschrieben. Sie erhalten diesen Objektverweis, indem Sie das Cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong> aufrufen und die neuen Konfigurationseinstellungen einer Variablen zuweisen. Übergeben Sie dieses Variable an den Parameter &quot;MediaBypassSettings&quot;, um die globalen Medienumgehungseinstellungen zu ändern.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung von Netzwerkregionenverbindungen, die innerhalb der Anrufsteuerungskonfiguration definiert sind. Mit jeder Netzwerkregionenverbindung wird eine Verbindung zwischen zwei Regionen und beliebigen zwischen diesen Regionen anzuwendenden Bandbreiteneinschränkungen definiert. Sie können alle Mitglieder dieser Auflistung mit dem Cmdlet <strong>Get-CsNetworkRegionLink</strong> abrufen.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegions</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung von Netzwerkregionen (von denen jede einen Hub oder Backbone innerhalb des Netzwerks darstellt), die innerhalb der Anrufsteuerungskonfiguration definiert sind. Sie können alle Mitglieder dieser Auflistung mit dem Cmdlet <strong>Get-CsNetworkRegion</strong> abrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSites</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung von Netzwerkstandorten (von denen jeder ein Büro oder einen Standort innerhalb des Netzwerks darstellt), die innerhalb der Anrufsteuerungskonfiguration definiert sind. Sie können alle Mitglieder dieser Auflistung mit dem Cmdlet <strong>Get-CsNetworkSite</strong> abrufen.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnets</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung von Netzwerksubnetzen (von denen jedes einen Endpunkt einem Standort zuordnet), die innerhalb der Anrufsteuerungskonfiguration definiert sind. Sie können alle Mitglieder dieser Auflistung mit dem Cmdlet <strong>Get-CsNetworkSubnet</strong> abrufen.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings-Objekt. Akzeptiert eine weitergeleitete Eingabe von Netzwerkkonfigurationsobjekten.

## Rückgabetypen

Das Cmdlet **Set-CsNetworkConfiguration** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings" geändert.

## Siehe auch

#### Weitere Ressourcen

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)

