---
title: Get-CsNetworkInterSitePolicy
TOCTitle: Get-CsNetworkInterSitePolicy
ms:assetid: a4a64048-f8d7-483a-9565-0c6f3b0937b7
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412769(v=OCS.15)
ms:contentKeyID: 49294973
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterSitePolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft eine oder mehrere standortübergreifende Netzwerkrichtlinien ab, die die Bandbreiteneinschränkungen zwischen Standorten definieren, die in einer Anrufsteuerungskonfiguration direkt verbunden sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterSitePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Mit dem Aufruf des Cmdlets **Get-CsNetworkInterSitePolicy** ohne Parameter werden alle Netzwerkstandortrichtlinien abgerufen, die zwischen zwei direkt miteinander verbundenen Netzwerkstandorten definiert sind.

    Get-CsNetworkInterSitePolicy

## BEISPIEL 2

In diesem Beispiel wird die Netzwerkstandortrichtlinie mit dem Identitätswert "Reno\_Portland" abgerufen.

    Get-CsNetworkInterSitePolicy -Identity Reno_Portland

## BEISPIEL 3

In Beispiel 3 werden alle Netzwerkstandortrichtlinien abgerufen, die die Zeichenfolge "Reno" an einer beliebigen Stelle im Identitätswert aufweisen. Die Platzhalterzeichen (\*) im Wert, die an den Parameter "Filter" übergeben werden, bedeuten "jedes beliebige Zeichen oder jede beliebige Zeichenfolge". Anders ausgedrückt: Die Zeichenfolge "Reno" stimmt mit den Identitätswerten überein, die mit einem oder mehreren beliebigen Zeichen, gefolgt von der Zeichenfolge "Reno" und gefolgt mit einem oder mehreren beliebigen Zeichen beginnen.

    Get-CsNetworkInterSitePolicy -Filter *Reno*

## BEISPIEL 4

In diesem Beispiel werden alle Netzwerkstandortrichtlinien abgerufen, die kein zugeordnetes Bandbreitenrichtlinienprofil haben. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsNetworkInterSitePolicy** auf. Anschließend wird eine Auflistung aller Netzwerkstandortrichtlinien abgerufen (siehe Beispiel 1). Diese Auflistung wird anschließend an das Cmdlet **Where-Object** weitergeleitet. Mit dem Cmdlet **Where-Object** wird die Auflistung auf die Standortrichtlinien beschränkt, denen kein Bandbreitenrichtlinienprofil zugeordnet ist. Zu diesem Zweck wird verglichen, ob die Eigenschaft "BWPolicyProfileID" für jede Standortrichtlinie einen Nullwert ($null) aufweist (der Vergleichsoperator "-eq" steht für "equal to").

    Get-CsNetworkInterSitePolicy | Where-Object {$_.BWPolicyProfileID -eq $null}

## Detaillierte Beschreibung

Wenn Netzwerkstandorte eine direkte Verbindung teilen, können Bandbreiteneinschränkungen für Audio- und Videoverbindungen zwischen diesen zwei Standorten definiert werden. Mit diesem Cmdlet werden eine oder mehrere Netzwerkstandortrichtlinien abgerufen, die die Einstellungen zur Bandbreiteneinschränkung den direkt verbundenen Standorten zuordnen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Get-CsNetworkInterSitePolicy** lokal ausführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterSitePolicy"}

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
<td><p>Eine Zeichenfolge mit Platzhalterzeichen, mit der Richtlinien mit Identitätswerten durchsucht werden, die mit der Platzhalterzeichenfolge übereinstimmen.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Die eindeutige ID der Netzwerkstandortrichtlinie, die abgerufen werden soll. Netzwerkstandortrichtlinien werden ausschließlich global erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die den eindeutigen Namen zur Identifizierung dieser Richtlinie darstellt.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die standortübergreifenden Netzwerkrichtlinieninformationen aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Ruft ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType" ab.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)

