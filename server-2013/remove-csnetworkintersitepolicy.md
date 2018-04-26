---
title: Remove-CsNetworkInterSitePolicy
TOCTitle: Remove-CsNetworkInterSitePolicy
ms:assetid: daf1afc8-cce4-4192-8ba4-05d26817198e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398963(v=OCS.15)
ms:contentKeyID: 49295604
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterSitePolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt eine standortübergreifende Netzwerkrichtlinie zur Definition von Bandbreiteneinschränkungen zwischen Standorten, die in einer Anrufsteuerungskonfiguration direkt verbunden sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsNetworkInterSitePolicy -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die Netzwerkstandortrichtlinie mit dem Identitätswert "Reno\_Portland" entfernt.

    Remove-CsNetworkInterSitePolicy -Identity Reno_Portland

## BEISPIEL 2

In Beispiel 2 werden alle Netzwerkstandortrichtlinien entfernt, die innerhalb der Anrufsteuerungskonfiguration definiert sind. Dazu wird zunächst mit dem Cmdlet **Get-CsNetworkInterSitePolicy** eine Auflistung aller Netzwerkstandortrichtlinien abgerufen. Diese Auflistung wird dann an das Cmdlet **Remove-CsNetworkInterSitePolicy** weitergeleitet, das alle Elemente in der Auflistung entfernt.

    Get-CsNetworkInterSitePolicy | Remove-CsNetworkInterSitePolicy

## Detaillierte Beschreibung

Wenn Netzwerkstandorte eine direkte Verbindung teilen, können Bandbreiteneinschränkungen für Audio- und Videoverbindungen zwischen diesen zwei Standorten definiert werden. Mit diesem Cmdlet wird eine Netzwerkstandortrichtlinie entfernt, die zwei direkt verbundenen Standorten eine Richtlinie zur Bandbreiteneinschränkung zuordnet.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsNetworkInterSitePolicy** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterSitePolicy"}

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
<td><p>Die eindeutige ID der Netzwerkstandortrichtlinie, die entfernt werden soll. Netzwerkstandortrichtlinien werden ausschließlich global erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die der eindeutige Name zur Identifizierung dieser Standortrichtlinie ist.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType-Objekt. Akzeptiert eine weitergeleitete Eingabe von standortübergreifenden Netzwerkobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType" entfernt.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

