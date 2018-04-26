---
title: Set-CsNetworkSite
TOCTitle: Set-CsNetworkSite
ms:assetid: 221a099c-72c4-4eb0-8812-6b2b7639a9ee
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398295(v=OCS.15)
ms:contentKeyID: 49293414
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSite

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert einen vorhandenen Netzwerkstandort, der für die Anrufsteuerung oder erweiterten Notfalldienste (E9-1-1) definiert wurde. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSite [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-LocationPolicy <String>] [-NetworkRegionID <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird der Netzwerkstandort "Vancouver" geändert. Der Name des zu ändernden Standorts wird als Wert für den Parameter "Identity" angegeben. Der Standort "Vancouver" wird in eine neue Region verschoben, sodass der Parameter "NetworkRegionID" geändert werden muss, in diesem Fall in die Region "Canada". Da zwar ein Wert für "NetworkRegionID", aber kein Wert für "BypassID" angegeben wurde, wird automatisch ein Wert für "BypassID" generiert. Eine zuvor vorhandene ID für die Umgehung wird überschrieben.

    Set-CsNetworkSite -Identity Vancouver -NetworkRegionID Canada

## BEISPIEL 2

In Beispiel 2 wird das dem Standort "Vancouver" zugeordnete Bandbreitenrichtlinienprofil geändert. Der Standortname wird als Wert für den Parameter "Identity" angegeben. Anschließend wird ein Wert für den Parameter "BWPolicyProfileID" festgelegt: LowBWLimits. Die mit diesem Profil verbundenen Richtlinien werden für diesen Standort verwendet.

    Set-CsNetworkSite -Identity Vancouver - BWPolicyProfileID LowBWLimits

## Detaillierte Beschreibung

Netzwerkstandorte sind Niederlassungen oder Standorte, die in jeder Region einer Anrufsteuerungs- oder E9-1-1-Bereitstellung konfiguriert sind. Mit diesem Cmdlet werden die Einstellungen eines bestehenden Standorts geändert. Dazu gehören Einstellungen wie die Region, der der Standort zugeordnet ist, die Beschreibung des Standorts und das zugeordnete Bandbreitenrichtlinienprofil.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsNetworkSite** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSite"}

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
<td><p>Der Identitätswert des Bandbreitenrichtlinienprofils, mit dem die Beschränkungen für diesen Standort definiert werden. Sie können eine Liste der verfügbaren Profile durch Aufrufen des Cmdlets <strong>Get-CsNetworkBandwidthPolicyProfile</strong> abrufen.</p>
<p>Wenn Sie für diesen Parameter einen Wert angeben, müssen Sie auch einen Wert für den Parameter &quot;NetworkRegionID&quot; angeben.</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Eine GUID (Globally Unique Identifier). Mit dieser GUID können Sie Netzwerkstandorte Medienumgehungseinstellungen in einer Netzwerkkonfiguration für Anrufsteuerung oder E9-1-1 zuordnen. (Verwenden Sie diesen Wert für &quot;BypassID&quot; beim Aufrufen des Cmdlets <strong>New-CsNetworkMediaBypassConfiguration</strong>.)</p>
<p>Wenn Sie für diesen Parameter einen Wert angeben, müssen Sie auch einen Wert für den Parameter &quot;NetworkRegionID&quot; angeben. Wenn Sie für diesen Parameter keinen Wert angeben, Sie jedoch einen Wert für &quot;NetworkRegionID&quot; festlegen, wird automatisch eine ID für die Umgehung generiert.</p>
<p>Wenn Sie einen Wert explizit angeben, muss dieser das Format einer GUID aufweisen (z. B. 3b24a047-dce6-48b2-9f20-9fbff17ed62a). Es wird empfohlen, einen Wert für &quot;NetworkRegionID&quot; anzugeben und eine automatisch Erstellung des Werts &quot;BypassID&quot; zuzulassen. Wenn Sie manuell einen Wert eingeben, wird eine Bestätigungsaufforderung eingeblendet, um zu bestätigen, dass Sie diesen Wert manuell festlegen möchten.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Eine Zeichenfolge, die den Standort beschreibt. Mit diesem Parameter können Sie eine aussagekräftigere Erläuterung des Zwecks und der Lage dieses Standorts bereitstellen als nur mit dem Identitätswert.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; wird das VoIP-Routing verwaltet, indem sowohl der Standort des Benutzers, der den Anruf tätigt, als auch der Standort des Empfängers berücksichtigt wird. Der Standardwert lautet &quot;False&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Eine eindeutige ID des Netzwerkstandorts, der geändert werden soll. Standorte werden nur global erstellt. Sie müssen daher keinen Gültigkeitsbereich festlegen. Es genügt, wenn Sie die Netzwerkstandort-ID angeben.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>DisplayNetworkSiteType</p></td>
<td><p>Ein Verweis auf ein Netzwerkstandortobjekt (ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType&quot;). Dieses Objekt kann durch Aufrufen des Cmdlets <strong>Get-CsNetworkSite</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationPolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Name der Standortrichtlinie, die diesem Standort zugeordnet ist. Mit der Standortrichtlinie werden dem Standort spezifische E9-1-1-Einstellungen zugewiesen. Zum Abrufen einer Liste mit Standortrichtlinien rufen Sie das Cmdlet <strong>Get-CsLocationPolicy</strong> auf.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Identitätswert der Netzwerkregion, die diesem Standort zugeordnet ist. Dieser Parameter muss einen Wert enthalten, wenn Sie eine &quot;BypassID&quot; angeben möchten (entweder per automatischer Generierung oder manuell) oder die Eigenschaft &quot;EnableBandwidthPolicyCheck&quot; der Netzwerkkonfiguration auf &quot;True&quot; festgelegt ist. Sie können die Netzwerkkonfigurationseinstellungen durch Aufrufen des Cmdlets <strong>Get-CsNetworkConfiguration</strong> abrufen.</p>
<p>Wenn für diesen Standort bereits eine ID für die Umgehung vorhanden ist und Sie keinen Wert für den Parameter &quot;BypassID&quot; festlegen, wird die vorhandene ID für die Umgehung durch eine automatisch generierte ID für die Umgehung überschrieben.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Benutzerbasierte VoIP-Routingrichtlinie, die dem Standort zugewiesen wird. Beispiel:</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>Beachten Sie, dass Sie eine benutzerbasierte Richtlinie angeben müssen. Globale Richtlinien bzw. Standortrichtlinien können einem Standort nicht mithilfe des Parameters &quot;VoiceRoutingPolicy&quot; zugewiesen werden.</p>
<p>Dieser Parameter wurde in der Lync Server 2013-Version vom Februar 2013 eingeführt.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Netzwerkstandortobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

