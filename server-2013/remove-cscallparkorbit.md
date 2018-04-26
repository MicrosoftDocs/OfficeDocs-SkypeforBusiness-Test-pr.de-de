---
title: Remove-CsCallParkOrbit
TOCTitle: Remove-CsCallParkOrbit
ms:assetid: b8e7c236-f8de-45bd-966b-60c815b37aed
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412901(v=OCS.15)
ms:contentKeyID: 49295205
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCallParkOrbit

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt einen bestimmten Orbitbereich für das Parken von Anrufen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird das Cmdlet **Remove-CsCallParkOrbit** verwendet, um den Orbitbereich "Redmond CPO 1" zum Parken von Anrufen zu löschen.

    Remove-CsCallParkOrbit -Identity "Redmond CPO 1"

## BEISPIEL 2

Der Befehl in diesem Beispiel entfernt alle Orbitbereiche für das Parken von Anrufen, die für eine Organisation definiert wurden. Der Befehl ruft zunächst das Cmdlet **Get-CsCallParkOrbit** ohne Parameter auf, um alle definierten Orbitbereiche für das Parken von Anrufen abzurufen. Anschließend wird die Auflistung aller Orbitbereiche für das Parken von Anrufen an das Cmdlet **Remove-CsCallParkOrbit** weitergeleitet, das jeden Orbit zum Parken von Anrufen entfernt.

    Get-CsCallParkOrbit | Remove-CsCallParkOrbit

## BEISPIEL 3

Mit diesem Befehl werden alle Orbitbereiche für das Parken von Anrufen entfernt, deren Identitätswert die Zeichenfolge "Redmond" enthält, z. B. "Redmond 501", "CP Redmond 1" und "ARedmond". Der Befehl ruft zunächst das Cmdlet **Get-CsCallParkOrbit** mit dem Parameter "Filter" auf, um alle Orbitbereiche für das Parken von Anrufen abzurufen, deren Identitätswert die Zeichenfolge "Redmond" enthält. Diese Auflistung wird an das Cmdlet **Remove-CsCallParkOrbit** weitergeleitet, das alle Inhalte in der Auflistung entfernt.

    Get-CsCallParkOrbit -Filter *Redmond* | Remove-CsCallParkOrbit

## Detaillierte Beschreibung

Mit dem Cmdlet **Remove-CsCallParkOrbit** wird der Orbitbereich für das Parken von Anrufen mit dem an den Parameter "Identity" übergegebenen Namen gelöscht. (Die Angabe dieses Parameters ist erforderlich.) Jeder Orbit für das Parken von Anrufen innerhalb einer Organisation muss über einen eindeutigen Nummernbereich verfügen. Das Entfernen eines Orbits für das Parken von Anrufen gibt den Bereich für diesen Orbit frei. Die freigegebenen Nummern können anschließend in einem neu definierten Orbit für das Parken von Anrufen verwendet werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsCallParkOrbit** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCallParkOrbit"}

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
<td><p>Der Name des Orbitbereichs zum Parken von Anrufen. Dieser Name wurde vom Administrator beim Definieren des Orbitbereichs für das Parken von Anrufen zugewiesen.</p></td>
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

Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit-Objekt. Akzeptiert eine weitergeleitete Eingabe von Orbitobjekten zum Parken von Anrufen.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit" entfernt.

## Siehe auch

#### Weitere Ressourcen

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

