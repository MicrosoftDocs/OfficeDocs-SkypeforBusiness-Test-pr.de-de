---
title: Set-CsVoiceNormalizationRule
TOCTitle: Set-CsVoiceNormalizationRule
ms:assetid: 68850abb-4ac7-4ae1-bb6e-d991385f92a4
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398491(v=OCS.15)
ms:contentKeyID: 49294272
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceNormalizationRule

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine VoIP-Normalisierungsregel. VoIP-Normalisierungsregeln werden verwendet, um eine Wählanforderung (z. B. das Wählen der Ziffer 9 für den Zugriff auf eine Amtsleitung) in das von Lync Server verwendete E.164-Telefonnummernformat zu konvertieren. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceNormalizationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird "Add a prefix to all numbers on site Redmond" als Beschreibung der Regel "Prefix Redmond" für den Standort "Redmond" festgelegt.

    Set-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond" -Description "Add a prefix to all numbers on site Redmond"

## BEISPIEL 2

In diesem Beispiel wird die VoIP-Normalisierungsregel mit der Identität "global/SeattleFourDigit" geändert. Eine neue Beschreibung wird angegeben, in der die Änderungen an der Regel vermerkt sind. Darüber hinaus wird die Regel um einen "Translation"-Wert erweitert. Durch diesen Wert werden Nummern, die mit dem vorhandenen Muster dieser Regel übereinstimmen, um das Präfix "+1206556" ergänzt. Wenn das vorhandene Muster z. B. bei vierstelligen Nummern zu einer Übereinstimmung führt und die Ziffern "1234" eingegeben werden, wird diese Durchwahl in die Nummer "+12065561234" übersetzt.

    Set-CsVoiceNormalizationRule -Identity global/SeattleFourDigit -Description "Translate an internal four-digit extension" -Translation '+1206556$1'

## BEISPIEL 3

In Beispiel 3 wird der Name der Normalisierungsregel geändert. Beachten Sie, dass durch die Namensänderung auch der Abschnitt für den Namen in der Identität geändert wird. Da das Cmdlet **Set-CsVoiceNormalizationRule** nicht über einen Parameter "Name" verfügt, rufen wir zum Ändern des Namens zunächst das Cmdlet **Get-CsVoiceNormalizationRule** auf, um die Regel mit der Identität "global/RedmondFourDigit" abzurufen und das zurückgegebene Objekt der Variablen "$a" zuzuweisen. Anschließend weisen wir der Eigenschaft "Name" des Objekts die Zeichenfolge "RedmondRule" zu. Dann übergeben wir die Variable an den Parameter "Instance" des Cmdlets **Set-CsVoiceNormalizationRule**, um die Änderung dauerhaft zu speichern.

    $a = Get-CsVoiceNormalizationRule -Identity global/RedmondFourDigit
    $a.name = "RedmondRule"
    Set-CsVoiceNormalizationRule -Instance $a

## Detaillierte Beschreibung

Dieses Cmdlet ändert eine benannte VoIP-Normalisierungsregel. Diese Regeln sind ein erforderlicher Teil der Telefonautorisierung und Anrufweiterleitung. Sie definieren die Anforderungen für das Konvertieren (oder Übersetzen) von Nummern aus einem internen Lync Server-Format in ein Standardformat (E.164). Für das Definieren von zu übersetzenden Nummernmustern ist ein Verständnis regulärer Ausdrücke hilfreich.

Die mit diesem Cmdlet geänderten Regeln sind Teil der Wähleinstellungen. Der Zugriff kann nicht nur über das Cmdlet **Get-CsVoiceNormalizationRule**, sondern auch über die Eigenschaft "NormalizationRules" erfolgen, die bei einem Aufruf des Cmdlets **Get-CsDialPlan** zurückgegeben wird.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsVoiceNormalizationRule** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceNormalizationRule"}

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
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Eine benutzerfreundliche Beschreibung der Normalisierungsregel.</p>
<p>Maximale Länge der Zeichenfolge: 512 Zeichen.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eine eindeutige ID für die Regel. Die angegebene Identität muss den Gültigkeitsbereich umfassen, auf den ein Schrägstrich und anschließend der Name folgt. Beispiel: site:Redmond/Rule1. Dabei steht &quot;site:Redmond&quot; für den Gültigkeitsbereich und &quot;Rule1&quot; für den Namen.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>NormalizationRule</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen. Dieses Objekt muss vom Typ &quot;NormalizationRule&quot; sein und kann mithilfe des Cmdlets <strong>Get-CsVoiceNormalizationRule</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>IsInternalExtension</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Bei Festlegung von &quot;True&quot; ist das Ergebnis beim Anwenden dieser Regel eine interne Nummer des Unternehmens. Wenn Sie &quot;False&quot; festlegen, ist das Ergebnis eine externe Nummer. Dieser Wert wird ignoriert, wenn der Wert der Eigenschaft &quot;OptimizeDeviceDialing&quot; der zugeordneten Wähleinstellungen auf &quot;False&quot; festgelegt ist.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ein regulärer Ausdruck, mit dem die gewählte Nummer übereinstimmen muss, damit diese Regel angewendet wird.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>Die Reihenfolge, in der Regeln angewendet werden. Eine Telefonnummer kann mit mehreren Regeln übereinstimmen. Dieser Parameter legt die Reihenfolge fest, in der die Regeln mit der Telefonnummer abgeglichen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Das Muster für reguläre Ausdrücke, das zur Konvertierung in das E.164-Format auf die Nummer angewendet wird.</p>
<p></p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule-Objekt. Das Cmdlet **Set-CsVoiceNormalizationRule** akzeptiert eine weitergeleitete Eingabe von VoIP-Normalisierungsregelobjekten.

## Rückgabetypen

Das Cmdlet **Set-CsVoiceNormalizationRule** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

