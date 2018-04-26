---
title: Get-CsComputer
TOCTitle: Get-CsComputer
ms:assetid: 493931a9-1670-4a76-abba-7d3c7723d2e1
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425959(v=OCS.15)
ms:contentKeyID: 49293901
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsComputer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Computern zurück, die in Ihrer Lync Server-Infrastruktur Dienstrollen innehaben. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel dient das Cmdlet **Get-CsComputer** zum Zurückgeben von Informationen zu allen Computern mit Dienstrollen in Ihrer Lync Server-Infrastruktur.

    Get-CsComputer

## BEISPIEL 2

Der Befehl in Beispiel 2 verwendet den Parameter "Filter", um nur die Computer mit Dienstrollen zurückzugeben, die zur Domäne "litwareinc.com" gehören. Die Platzhalterzeichenfolge "\*.litwareinc.com" beschränkt die zurückgegebenen Informationen auf Computer mit einem vollqualifizierten Domänennamen, der auf ".litwareinc.com" endet.

    Get-CsComputer -Filter "*.litwareinc.com"

## BEISPIEL 3

Im dritten Beispiel dient der Parameter "-Identity" zum Begrenzen der zurückgegebenen Daten auf den einen Computer, dessen vollqualifizierter Domänenname "atl-cs-001.litwareinc.com" lautet.

    Get-CsComputer -Identity "atl-cs-001.litwareinc.com"

## BEISPIEL 4

In Beispiel 4 dient der Parameter "Pool" zum Zurückgeben von Informationen zu allen Computern im Pool "atl-cs-001.litwareinc.com".

    Get-CsComputer -Pool "atl-cs-001.litwareinc.com"

## Detaillierte Beschreibung

Das Cmdlet **Get-CsComputer** bietet eine Möglichkeit zur schnellen Ermittlung von Computern, auf denen Lync Server-Dienste oder -Serverrollen ausgeführt werden. Beim Aufrufen ohne Parameter gibt das Cmdlet **Get-CsComputer** eine Auflistung aller Computer mit Lync Server-Diensten oder Serverrollen zurück. Diese Auflistung enthält die Identität, den Poolnamen und den vollqualifizierten Domänennamen der einzelnen Computer. Sie können auch optionale Parameter wie "Identity", "Filter" oder "Pool" angeben, um die zurückgegebenen Daten auf einen einzelnen Computer oder eine Computergruppe zu begrenzen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsComputer** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p>Ermöglicht die Verwendung von Platzhalterzeichen beim Angeben der Identität zurückzugebender Computer. Dieser Befehl gibt beispielsweise Informationen zu allen Computern zurück, deren Identitätswert mit dem Zeichenfolgenwert &quot;atl-&quot; beginnt: -Filter &quot;atl-*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Vollqualifizierter Domänenname des Computers, der zurückgegeben werden soll. Beispiel: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Wenn dieser Parameter nicht angegeben ist, werden alle Computer mit Lync Server zurückgegeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>Local</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ist dieser Parameter angegeben, werden nur Informationen für den lokalen Computer zurückgegeben.</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Vollqualifizierter Domänenname eines Lync Server-Pools. Bei Verwendung dieses Parameters werden Informationen zu allen Computern im angegebenen Pool zurückgegeben.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsComputer** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsComputer** werden Instanzen des Objekts "Microsoft.Rtc.Management.Deploy.Internal.Machine" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

