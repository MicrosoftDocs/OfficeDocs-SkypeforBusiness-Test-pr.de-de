---
title: Set-CsVoiceConfiguration
TOCTitle: Set-CsVoiceConfiguration
ms:assetid: dbab35ac-9a55-41d2-a726-9a26b2ff8e85
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398967(v=OCS.15)
ms:contentKeyID: 49295612
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine Liste von VoIP-Testkonfigurationen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-VoiceTestConfigurations <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Zum Ändern einer VoIP-Testkonfiguration innerhalb einer VoIP-Konfiguration sind mehrere Schritte erforderlich. In diesem Beispiel wird zunächst das VoIP-Konfigurationsobjekt abgerufen, indem das Cmdlet **Get-CsVoiceConfiguration** aufgerufen wird. Anschließend wird das abgerufene Objekt (es wird nur ein Objekt zurückgegeben) der Variablen "$a" zugewiesen.

In Zeile 2 des Beispiels werden die Inhalte der Eigenschaft "VoiceTestConfigurations", bei der es sich um eine Auflistung von VoIP-Testkonfigurationsobjekten handelt, aus der Variablen "$a" abgerufen. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Auflistung nach dem VoIP-Testkonfigurationsobjekt mit dem Namen "TestConfig2" durchsucht. Dieses Objekt wird der Variablen "$b" zugewiesen.

Anschließend wird das VoIP-Testkonfigurationsobjekt "TestConfig2" geändert, indem wir den Eigenschaften "DialedNumber" und "ExpectedTranslatedNumber" neue Werte zuweisen. Durch eine Aktualisierung des Objekts wird das Objekt in der Variablen "$a" aktualisiert. Das Objekt befindet sich jedoch weiterhin nur im Arbeitsspeicher. Im letzten Schritt müssen die vorgenommenen Änderungen gespeichert werden, indem "$a" an den Parameter "Instance" des Cmdlets**Set-CsVoiceConfiguration** übergeben wird.

Hierbei handelt es sich nicht um die empfohlene Vorgehensweise zum Ändern einer VoIP-Konfiguration. Ändern Sie zum Bearbeiten einer VoIP-Konfiguration einfach die einzelnen VoIP-Testkonfigurationen mit dem Cmdlet **Set-CsVoiceTestConfiguration**, wie nachfolgend gezeigt:

Set-CsVoiceTestConfiguration -Identity TestConfig2 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

Diese eine Zeile führt dieselbe Aufgabe aus wie Beispiel 1.

    $a = Get-CsVoiceConfiguration
    $b = $a.VoiceTestConfigurations | Where-Object {$_.Name -eq "TestConfig2"}
    $b.DialedNumber = "5551212"
    $b.ExpectedTranslatedNumber = "+5551212"
    Set-CsVoiceConfiguration -Instance $a

## Detaillierte Beschreibung

VoIP-Testkonfigurationen werden dazu verwendet, eine bestimmte VoIP-Richtlinie, -Route und einen bestimmten Wählplan für eine Telefonnummer zu testen. Dieses Cmdlet kann verwendet werden, um VoIP-Testkonfigurationen aus einer Liste mit allen VoIP-Testkonfigurationen für eine Lync Server-Bereitstellung zu ändern.

Mit diesem Cmdlet wird ein Objekt vom Typ "VoiceConfiguration" geändert. Dieses Objekt ist lediglich ein Containerobjekt für VoIP-Testkonfigurationen. Daher wird die Verwendung dieses Cmdlets nicht empfohlen. Ändern Sie zum Bearbeiten der VoIP-Konfigurationen die einzelnen VoIP-Testkonfigurationen über das Cmdlet **Set-CsVoiceTestConfiguration**.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsVoiceConfiguration** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Der Gültigkeitsbereich dieses Objekts. Der einzige zulässige Wert für diesen Parameter lautet &quot;Global&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>VoiceConfiguration</p></td>
<td><p>Ein Verweis auf ein VoIP-Konfigurationsobjekt (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration). Objekte von diesem Typ können mit dem Cmdlet <strong>Get-CsVoiceConfiguration</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceTestConfigurations</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste aller VoIP-Testkonfigurationen (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration-Objekte), die für die Lync Server-Bereitstellung definiert sind.</p>
<p>Sie sollten einzelne VoIP-Testkonfigurationsobjekte über das Cmdlet <strong>Set-CsVoiceTestConfiguration</strong> ändern. Dies ist die empfohlene Methode zum Ändern von Konfigurationen in dieser Liste.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration-Objekt. Das Cmdlet **Set-CsVoiceConfiguration** akzeptiert eine weitergeleitete Eingabe von VoIP-Konfigurationsobjekten.

## Rückgabetypen

Das Cmdlet **Set-CsVoiceConfiguration** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

