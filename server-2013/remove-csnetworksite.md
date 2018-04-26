---
title: Remove-CsNetworkSite
TOCTitle: Remove-CsNetworkSite
ms:assetid: 07b543a6-3aa0-4fce-85f9-9ddc75d7b14f
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398135(v=OCS.15)
ms:contentKeyID: 49293082
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSite

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt einen Netzwerkstandort, der für die Anrufsteuerung oder für erweiterte Notrufdienste (E9-1-1) definiert wurde. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird der Standort mit dem Identitätswert "Vancouver" aus der Anrufsteuerungs- oder E9-1-1-Konfiguration entfernt.

    Remove-CsNetworkSite -Identity Vancouver

## BEISPIEL 2

In Beispiel 2 werden alle Netzwerke, die das Bandbreitenrichtlinienprofil "LowBWProfile" verwenden, aus der Anrufsteuerungs- oder E9-1-1-Konfiguration entfernt. Hierbei wird zunächst das Cmdlet **Get-CsNetworkSite** aufgerufen, um alle Netzwerkstandorte abzurufen. Diese Auflistung von Standorten wird an das Cmdlet **Where-Object** weitergeleitet, das sie auf lediglich die Standorte beschränkt, deren "BWPolicyProfileID" den Wert "LowBWProfile" aufweist (der Vergleichsoperator "-eq" steht für "equal to"). Diese neue Auflistung wird dann an das Cmdlet **Remove-CsNetworkSite** weitergeleitet, um alle diese Standorte zu entfernen.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Remove-CsNetworkSite

## Detaillierte Beschreibung

Netzwerkstandorte sind Niederlassungen oder Standorte, die in jeder Region einer Anrufsteuerungs- oder E9-1-1-Bereitstellung konfiguriert sind. Mit diesem Cmdlet wird ein Standort aus der Anrufsteuerungs- oder E9-1-1-Konfiguration entfernt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Remove-CsNetworkSite** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSite"}

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
<td><p>Die eindeutige ID des Netzwerkstandorts, der entfernt werden soll. Standorte werden nur global erstellt. Sie müssen daher keinen Gültigkeitsbereich festlegen. Es genügt, wenn Sie die Standort-ID angeben.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Netzwerkstandortobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType" entfernt.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkSite](new-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

