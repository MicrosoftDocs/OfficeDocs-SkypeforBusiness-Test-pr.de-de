---
title: Set-CsPstnUsage
TOCTitle: Set-CsPstnUsage
ms:assetid: ecba9ed6-4845-4035-933e-0c540d530b72
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399069(v=OCS.15)
ms:contentKeyID: 49295810
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnUsage

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert einen Satz von Zeichenfolgen, die die zulässigen Verwendungen des Telefonfestnetzes (Public Switched Telephone Network, PSTN) identifizieren. Mit diesem Cmdlet können der Liste von PSTN-Verwendungen weitere hinzugefügt sowie einzelne daraus entfernt werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPstnUsage [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Usage <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Über diesen Befehl wird die Zeichenfolge "International" zur aktuellen Liste der verfügbaren PSTN-Verwendungen hinzugefügt.

    Set-CsPstnUsage -Identity global -Usage @{add="International"}

## BEISPIEL 2

Über diesen Befehl wird die Zeichenfolge "Local" aus der Liste der verfügbaren PSTN-Verwendungen entfernt.

    Set-CsPstnUsage -Identity global -Usage @{remove="Local"}

## BEISPIEL 3

Mit dem Befehl in diesem Beispiel wird dieselbe Aktion wie mit dem Befehl in Beispiel 2 ausgeführt: Die PSTN-Verwendung "Local" wird entfernt. In diesem Beispiel wird der Befehl ohne Angabe des Parameters "Identity" gezeigt. Die einzige für das Cmdlet **Set-CsPstnUsage** verfügbare Identität lautet "Global". Beim Auslassen des Parameters "Identity" wird der Standardwert "Global" verwendet.

    Set-CsPstnUsage -Usage @{remove="Local"}

## BEISPIEL 4

Über diesen Befehl werden sämtliche Daten in der Verwendungsliste durch die Werte "International" und "Restricted" ersetzt. Alle zuvor vorhandenen Verwendungen werden entfernt.

    Set-CsPstnUsage -Usage @{replace="International","Restricted"}

## Detaillierte Beschreibung

Bei PSTN-Verwendungen handelt es sich um Zeichenfolgenwerte, die für die Anrufautorisierung verwendet werden. Eine PSTN-Verwendung verknüpft eine VoIP-Richtlinie mit einer Route. Das Cmdlet **Set-CsPstnUsage** wird zum Hinzufügen oder Entfernen von Telefonverwendungen zu bzw. aus der Verwendungsliste eingesetzt. Da diese Liste global ist, kann sie von Richtlinien und Routen innerhalb der Lync Server-Bereitstellung verwendet werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsPstnUsage** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnUsage"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die Ebene, auf der diese Einstellungen angewendet werden. Die Identität für dieses Cmdlet ist immer &quot;Global&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>PstnUsages</p></td>
<td><p>Ein Verweis auf das PSTN-Verwendungsobjekt. Dieses Objekt muss ein Objekt vom Typ &quot;PstnUsages&quot; sein und kann mithilfe des Cmdlets <strong>Get-CsPstnUsage</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Usage</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Umfasst eine Liste der zulässigen Verwendungszeichenfolgen. Für diese Einträge kann ein beliebiger Zeichenfolgenwert verwendet werden.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages-Objekt. Akzeptiert eine weitergeleitete Eingabe von PSTN-Verwendungsobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[Get-CsPstnUsage](get-cspstnusage.md)

