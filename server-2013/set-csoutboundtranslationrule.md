---
title: Set-CsOutboundTranslationRule
TOCTitle: Set-CsOutboundTranslationRule
ms:assetid: fbf82146-7884-418c-8239-66c0ca0f2ba6
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg413073(v=OCS.15)
ms:contentKeyID: 49295995
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundTranslationRule

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine bestehende ausgehende Übersetzungsregel. Eine ausgehende Übersetzungsregel konvertiert Telefonnummern in das lokale Wählformat, um die Interaktion mit Nebenstellenanlagen (Private Branch Exchange, PBX) zu ermöglichen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die globale ausgehende Übersetzungsregel mit dem Identitätswert "site:Redmond/Prefix Redmond" geändert. Es enthält eine Beschreibung, die erläutert, dass diese Regel zur Übersetzung von Nummern im E.164-Format in eine siebenstellige Telefonnummer dient. Darüber hinaus wurden Muster- und Übersetzungswerte angegeben, die die bestehenden Werte dieser Eigenschaften ändern. Diese Werte übersetzen eine vom regulären Ausdruck im Muster angegebene Nummer im E.164-Format (in diesem Fall 12 Ziffern, die mit +1425 beginnen) durch Entfernen der ersten fünf Ziffern in eine siebenstellige Nummer. Die Nummer +14255551212 wird beispielsweise in 5551212 übersetzt.

    Set-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond" -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## BEISPIEL 2

In diesem Beispiel wird die Eigenschaft "Name" einer ausgehenden Übersetzungsregel geändert. Beachten Sie, dass damit der Identitätswert dieser Regel geändert wird. Der erste Befehl in diesem Beispiel ist ein Aufruf des Cmdlets **Get-CsOutboundTranslationRule**. Als Identitätswert wird "site:Redmond\\OBR1" angegeben. Diese gibt eine einzelne Übersetzungsregel, die Regel mit dem Identitätswert, zurück. Statt diese Regel anzuzeigen, wird diese der Variablen "$a" zugewiesen. In Zeile 2 dieses Beispiels wird die Zeichenfolge "Outbound Rule 1" der Eigenschaft "Name" der Variablen "$a" zugewiesen. Diese Variable enthält einen Verweis auf "site:Redmond/OBR1". In der letzten Zeile dieses Beispiels wird das Cmdlet **Set-CsOutboundTranslationRule** aufgerufen, das den Parameter "Instance" angibt und ihm die Variable "$a" übergibt. Wenn Sie nun das Cmdlet **Get-CsOutboundTranslationRule** mit dem Identitätswert "site:Redmond/OBR1" aufrufen, wird nichts zurückgegeben. Grund hierfür ist, dass dieser Identitätswert nicht mehr vorhanden ist. Er wurde von der gleichen Regel ersetzt, die allerdings den Identitätswert "site:Redmond/Outbound Rule 1" hat.

    $a = Get-CsOutboundTranslationRule -Identity "site:Redmond/OBR1"
    $a.Name = "Outbound Rule 1"
    Set-CsOutboundTranslationRule -Instance $a

## Detaillierte Beschreibung

Lync Server normalisiert Telefonnummern in das E.164-Format. Viele Nebenstellenanlagen können dieses Format allerdings nicht verarbeiten. Ausgehende Übersetzungsregeln übersetzen die Nummer in das lokale Wählformat, bevor sie diese an den Vermittlungsserver oder an das Gateway senden. Rufen Sie dieses Cmdlet auf, um eine bestehende ausgehende Übersetzungsregel zu ändern.

Jede ausgehende Übersetzungsregel ist einer Trunkkonfiguration zugeordnet. Die Verwendung dieses Cmdlets zum Ändern einer Regel hat daher Auswirkungen auf die entsprechende Trunkkonfiguration. Es ist möglich, jeder Konfiguration mehrere ausgehende Übersetzungsregeln zuzuordnen. Der Identitätswert jeder Regel besteht daher aus einem Gültigkeitsbereich und einem innerhalb des Gültigkeitsbereichs eindeutigen Namen (im Format "Gültigkeitsbereich/Name", z. B. "site:Redmond/OBR1"). Die Regel wird automatisch der Trunkkonfiguration im gleichen Gültigkeitsbereich zugeordnet. Zum Ändern der ausgehenden Übersetzungsregeln in einer Trunkkonfiguration wird das Cmdlet **Set-CsOutboundTranslationRule** empfohlen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsOutboundTranslationRule** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundTranslationRule"}

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
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Eine aussagekräftige Beschreibung der ausgehenden Übersetzungsregel. Anhand dieser Beschreibung können Administratoren den Zweck der Regel einwandfrei erkennen.</p></td>
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
<td><p>XdsIdentity</p></td>
<td><p>Die eindeutige ID für die ausgehende Übersetzungsregel, die geändert werden soll. Der Identitätswert besteht aus dem Gültigkeitsbereich, gefolgt von einem eindeutigen Namen in jedem Gültigkeitsbereich. Beispiel: site:Redmond/OutboundRule1.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>TranslationRule</p></td>
<td><p>Ein Objektverweis auf eine ausgehende Übersetzungsregel. Dieses Objekt muss vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule&quot; sein und kann durch Aufrufen des Cmdlets <strong>Get-CsOutboundTranslationRule</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Ein regulärer Ausdruck, der das Nummernmuster repräsentiert, für das die Übersetzung gilt.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Wenn eine Nummer dem Muster einer oder mehrerer ausgehender Übersetzungsregeln entspricht, werden die Regeln nach ihrer Priorität angewendet. Verwenden Sie diesen Parameter, um der Regel eine Priorität zuzuweisen.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Ein regulärer Ausdruck, der auf die mit dem Muster übereinstimmende Nummer angewendet wird, um diese auf das Ausgangsrouting vorzubereiten.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule-Objekt. Akzeptiert eine weitergeleitete Eingabe von Objekten für ausgehende Übersetzungsregeln.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

