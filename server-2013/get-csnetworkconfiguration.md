---
title: Get-CsNetworkConfiguration
TOCTitle: Get-CsNetworkConfiguration
ms:assetid: 08bc8eca-b244-4d5e-b089-1cc95605ba14
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398140(v=OCS.15)
ms:contentKeyID: 49293099
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft globale Einstellungen für Anrufsteuerung, erweiterte Notrufdienste (E9-1-1) und Medienumgehung ab. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

In diesem Beispiel werden die Netzwerkkonfigurationseinstellungen abgerufen. Diese Einstellungen sind nur auf der globalen Ebene definiert, d. h., es wird nur ein Element zurückgegeben.

    Get-CsNetworkConfiguration

## BEISPIEL 2

Es ist nur ein Satz von Einstellungen für die Medienumgehung vorhanden, der global angewendet wird. Diese werden als Teil der Gesamtnetzwerkkonfiguration gespeichert. Der Befehl ruft diese Konfiguration über das Cmdlet **Get-CsNetworkConfiguration** auf und ruft anschließend die Eigenschaft "MediaBypassSettings" der Konfiguration ab.

    (Get-CsNetworkConfiguration).MediaBypassSettings

## Detaillierte Beschreibung

Das Netzwerkkonfigurationsobjekt enthält alle globalen Einstellungen für die Medienumgehung und eine komplette Anrufsteuerungskonfiguration in einer Lync Server-Bereitstellung. Dazu zählt auch die Information, ob die Konfiguration aktiviert ist. Mit diesem Cmdlet können Sie diese Konfigurationen und Einstellungen abrufen. Abgesehen von "EnableBandwidthPolicyCheck" und "MediaBypassSettings" wird empfohlen, zum Abrufen der Anrufsteuerungs-Konfigurationseinstellungen für den Objekttyp spezifische Cmdlets zu verwenden. Es ist beispielsweise einfacher, Netzwerkregionen statt mit dem Cmdlet **Get-CsNetworkConfiguration** über das Cmdlet **Get-CsNetworkRegion** abzurufen und dann die Eigenschaft "NetworkRegions" dieser Konfiguration abzurufen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsNetworkConfiguration** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkConfiguration"}

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
<td><p>Da es immer nur eine Netzwerkkonfiguration gibt, ist dieser Parameter für dieses Cmdlet nicht erforderlich.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Immer &quot;Global&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Netzwerkkonfiguration aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit dem Cmdlet **Get-CsNetworkConfiguration** wird eine Instanz des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

