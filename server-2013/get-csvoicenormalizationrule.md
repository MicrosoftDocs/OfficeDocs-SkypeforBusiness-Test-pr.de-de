---
title: Get-CsVoiceNormalizationRule
TOCTitle: Get-CsVoiceNormalizationRule
ms:assetid: 59fe1370-1cec-4cf9-8f65-029a7c2454d1
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398393(v=OCS.15)
ms:contentKeyID: 49294098
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceNormalizationRule

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den in Ihrer Organisation verwendeten VoIP-Normalisierungsregeln zurück. VoIP-Normalisierungsregeln werden verwendet, um Wählanforderungen (z. B. das Wählen der Ziffer 0 für den Zugriff auf eine Amtsleitung) in das von Lync Server verwendete E.164-Telefonnummernformat zu konvertieren. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceNormalizationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

In diesem Beispiel werden alle für die Organisation definierten VoIP-Normalisierungsregeln abgerufen.

    Get-CsVoiceNormalizationRule

## BEISPIEL 2

In Beispiel 2 werden alle VoIP-Normalisierungsregeln abgerufen, die für sämtliche Standorte definiert sind.

    Get-CsVoiceNormalizationRule -Filter site*

## BEISPIEL 3

Beispiel 3 ruft alle VoIP-Normalisierungsregeln mit dem Buchstaben "s" irgendwo im Gültigkeitsbereich ab. Dieser Befehl gibt beispielsweise alle Regeln auf Standort- und Dienstebene sowie benutzerbezogene Regeln mit einem "s" im Gültigkeitsbereichsnamen zurück, z. B. "RedmondEastUsers".

    Get-CsVoiceNormalizationRule -Filter *s*

## BEISPIEL 4

Der in den Beispielen 2 und 3 verwendete Parameter "Filter" ermittelt lediglich Übereinstimmungen für den Gültigkeitsbereich der Identität. In diesem Beispiel werden Übereinstimmungen im Namen ermittelt, um alle Regeln zurückzugeben, deren Namen die Zeichenfolge "seattle" enthalten. Zu diesem Zweck wird zunächst das Cmdlet **Get-CsVoiceNormalizationRule** aufgerufen, um alle Normalisierungsregeln für die Organisation abzurufen. Anschließend wird die ermittelte Auflistung an das Cmdlet **Where-Object** weitergeleitet, um alle Elemente in der Auflistung zu ermitteln, deren Eigenschaft "Name" mit der Zeichenfolge "seattle" übereinstimmt.

    Get-CsVoiceNormalizationRule | Where-Object {$_.Name -match "seattle"}

## Detaillierte Beschreibung

Über dieses Cmdlet wird eine benannte VoIP-Normalisierungsregel oder eine Sammlung von VoIP-Normalisierungsregeln zurückgegeben. Diese Regeln sind ein erforderlicher Teil der Telefonautorisierung und Anrufweiterleitung. Sie definieren die Anforderungen für das Umwandeln (oder Übersetzen) von Nummern aus einem internen Lync Server-Format in ein Standardformat (E.164). Für das Definieren von zu übersetzenden Nummernmustern ist ein Verständnis regulärer Ausdrücke hilfreich.

Der Zugriff auf die Regeln, auf die mit diesem Cmdlet zugegriffen wird, kann auch über die Eigenschaft "NormalizationRules" erfolgen, die beim Aufruf des Cmdlets **Get-CsDialPlan** zurückgegeben wird.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Get-CsVoiceNormalizationRule** lokal ausführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceNormalizationRule"}

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
<td><p>Verwendet Platzhalterzeichenfolgen, um eine Auflistung von Normalisierungsregeln basierend auf der Identität zurückzugeben. Beachten Sie, dass der Filter nur auf den Abschnitt zum Gültigkeitsbereich der Identität, nicht jedoch auf den Namen angewendet wird. Der Filterwert &quot;*lob*&quot; gibt z. B. alle Regeln auf globaler Ebene (welche die Zeichenfolge &quot;lob&quot; enthalten), nicht jedoch Regeln mit der Identität &quot;site:Redmond/lobby&quot; zurück, wobei &quot;lob&quot; nur der Namensteil der Identität, nicht der Gültigkeitsbereich ist.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eine eindeutige ID für die Regel. Wenn für diesen Parameter ein Wert angegeben wird, muss er mit dem Format &quot;Gültigkeitsbereich/Name&quot; angegeben werden, z. B.: &quot;site:Redmond/Rule1&quot;. Dabei steht &quot;site:Redmond&quot; für den Gültigkeitsbereich und &quot;Rule1&quot; für den Namen.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die VoIP-Normalisierungsregel aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit dem Cmdlet **Get-CsVoiceNormalizationRule** werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Get-CsDialPlan](get-csdialplan.md)

