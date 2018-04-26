---
title: Get-CsPstnUsage
TOCTitle: Get-CsPstnUsage
ms:assetid: 9dc82b88-303b-4678-8298-0dbc769f6781
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412734(v=OCS.15)
ms:contentKeyID: 49294906
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPstnUsage

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen über die in Ihrer Organisation verwendeten Verwendungsdatensätze des Telefonfestnetzes (Public Switched Telephone Network, PSTN) zurück. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPstnUsage [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Mit diesem Befehl wird die Liste der globalen PSTN-Verwendungen zurückgegeben, die innerhalb der Organisation verfügbar sind.

    Get-CsPstnUsage

## BEISPIEL 2

Der Befehl in diesem Beispiel gibt eine Liste aller definierten PSTN-Verwendungen zurück. Dabei wird in der Ausgabe eine Verwendung pro Zeile angezeigt. Wenn das Cmdlet **Get-CsPstnUsage** allein aufgerufen wird, werden die Listen "Identity" und "Usage" zurückgegeben. Wenn die Liste "Usage" mehr als drei oder vier Einträge umfasst, wird die Liste in der Ausgabe wie im folgenden Beispiel abgekürzt:

Usage : {Internal, Local, Long Distance, International...}

Verwenden Sie den Befehl in diesem Beispiel, um lediglich eine Liste der Verwendungen anzuzeigen. Die Ausgabe entspricht in etwa folgendem Beispiel:

Internal

Local

Long Distance

International

Restricted

    (Get-CsPstnUsage).Usage

## BEISPIEL 3

Mit diesem Befehl werden alle PSTN-Verwendungen zurückgegeben, deren Namen die Zeichenfolge "tern" enthalten. Dieser Befehl gibt z. B. "Internal" und "International" zurück, nicht jedoch "Local" oder "Long Distance".

Im ersten Teil dieses Befehls wird das Cmdlet **Get-CsPstnUsage** in Klammern angegeben, sodass im ersten Schritt sämtliche PSTN-Verwendungen abgerufen werden. Die Eigenschaft ".Usage" gibt nur die Verwendungsinformationen für die PSTN-Verwendungen zurück, nicht jedoch den Identitätswert. Die Liste der Verwendungen wird dann an das Cmdlet **ForEach-Object** weitergeleitet, das die Verwendungszeichenfolgen nacheinander überprüft. Mit der If-Anweisung wird die aktuelle Verwendungszeichenfolge mit der Zeichenfolge "\*tern\*" verglichen (die Sternchen (\*) sind Platzhalterzeichen), und die ermittelten Übereinstimmungen für dieses Muster werden angezeigt.

    (Get-CsPstnUsage).Usage | ForEach-Object {if ($_ -like "*tern*") {$_}}

## Detaillierte Beschreibung

Bei PSTN-Verwendungen handelt es sich um Zeichenfolgenwerte, die für die Anrufautorisierung verwendet werden. Eine PSTN-Verwendung verknüpft eine VoIP-Richtlinie mit einer Route. Mit dem Cmdlet **Get-CsPstnUsage** wird die Liste aller in Ihrer Organisation verfügbaren PSTN-Verwendungen innerhalb einer Organisation abgerufen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Get-CsPstnUsage** lokal ausführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPstnUsage"}

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
<td><p>Mithilfe des Parameters &quot;Filter&quot; können nur PSTN-Verwendungen abgerufen werden, deren Identitätswert mit einer bestimmten Platzhalterzeichenfolge übereinstimmt. Da der einzige verfügbare Identitätswert für PSTN-Verwendungen jedoch &quot;Global&quot; ist, ist die Verwendung dieses Parameters mit diesem Cmdlet nicht sinnvoll.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die Ebene, auf der diese Einstellungen angewendet werden. Für PSTN-Verwendungen kann nur der Identitätswert &quot;Global&quot; angewendet werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die PSTN-Verwendungsinformationen aus dem lokalen Datenspeicher statt vom zentralen Verwaltungsspeicher ab.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit dem Cmdlet **Get-CsPstnUsage** werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PSTNUsages" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Set-CsPstnUsage](set-cspstnusage.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

