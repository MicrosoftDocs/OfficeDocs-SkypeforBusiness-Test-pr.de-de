---
title: Set-CsNetworkInterSitePolicy
TOCTitle: Set-CsNetworkInterSitePolicy
ms:assetid: 973979bc-db2c-47a6-909e-5949a927f51c
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398772(v=OCS.15)
ms:contentKeyID: 49294821
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterSitePolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine vorhandene standortübergreifende Netzwerkrichtlinie zur Definition von Bandbreiteneinschränkungen zwischen Standorten, die in einer Anrufsteuerungskonfiguration direkt verbunden sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterSitePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkSiteID1 <String>] [-NetworkSiteID2 <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die Netzwerkstandortrichtlinie mit dem Identitätswert "Reno\_Portland" geändert. Hierbei wird der Parameter "BWPolicyProfileID" verwendet, um das dieser Netzwerkstandortrichtlinie zugeordnete Bandbreitenrichtlinienprofil in "HighBWLimits" zu ändern.

    Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

## Detaillierte Beschreibung

Wenn Netzwerkstandorte eine direkte Verbindung teilen, können Bandbreiteneinschränkungen für Audio- und Videoverbindungen zwischen diesen zwei Standorten definiert werden. Mit diesem Cmdlet wird eine standortübergreifende Netzwerkrichtlinie geändert, die zwei direkt verbundenen Standorten eine Richtlinie zur Bandbreiteneinschränkung zuordnet.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsNetworkInterSitePolicy** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterSitePolicy"}

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
<td><p>String</p></td>
<td><p>Der Identitätswert des Bandbreitenrichtlinienprofils, das die Beschränkungen für diese Standortrichtlinie bestimmt. Sie können eine Liste der verfügbaren Profile durch Aufrufen des Cmdlets <strong>Get-CsNetworkBandwidthPolicyProfile</strong> abrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>.SwitchParameter</p></td>
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
<td><p>Die eindeutige ID der Netzwerkstandortrichtlinie, die geändert werden soll. Netzwerkstandortrichtlinien werden ausschließlich global erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge mit einem eindeutigen Namen zur Identifizierung der Standortrichtlinie enthalten.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>InterNetworkSitePolicyType</p></td>
<td><p>Ein Objektverweis auf eine Standortrichtlinie, die im Arbeitsspeicher geändert wurde. Dieses Objekt muss vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType&quot; sein und kann durch Aufrufen des Cmdlets <strong>Get-CsNetworkInterSitePolicy</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID1</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Der Identitätswert (NetworkSiteID) eines der beiden Standorte, denen diese Richtlinie zugeordnet ist. Die Kombination aus &quot;NetworkSiteID1&quot; und &quot;NetworkSiteID2&quot; muss eindeutig sein (Sie können beispielsweise nicht zwei Standortrichtlinien definieren, die &quot;Reno&quot; und &quot;Portland&quot; verbinden).</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID2</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Der Identitätswert (NetworkSiteID) eines der beiden Standorte, denen diese Richtlinie zugeordnet ist. Die Kombination aus &quot;NetworkSiteID1&quot; und &quot;NetworkSiteID2&quot; muss eindeutig sein (Sie können beispielsweise nicht zwei Standortrichtlinien definieren, die &quot;Reno&quot; und &quot;Portland&quot; verbinden).</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType-Objekt. Akzeptiert eine weitergeleitete Eingabe von standortübergreifenden Netzwerkrichtlinienobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Es ändert ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType".

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

