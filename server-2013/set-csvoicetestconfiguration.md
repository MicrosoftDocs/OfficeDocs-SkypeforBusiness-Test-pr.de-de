---
title: Set-CsVoiceTestConfiguration
TOCTitle: Set-CsVoiceTestConfiguration
ms:assetid: 7b95fc95-ec0e-4bb3-aed1-e8b72e305999
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398614(v=OCS.15)
ms:contentKeyID: 49294508
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceTestConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert ein Testszenario, das zum Testen von Routen und Regeln für bestimmte Telefonnummern verwendet werden kann. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceTestConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die gewählte Nummer der VoIP-Testkonfiguration für "TestConfig1" auf 14255551212 festgelegt. Für diese Nummer wird die VoIP-Richtlinie und -Route getestet, um das erwartete Normalisierungsverhalten zu überprüfen. Gleichzeitig soll sichergestellt werden, dass die richtigen Routen und Wähleinstellungen verwendet werden.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 14255551212

## BEISPIEL 2

In diesem Beispiel werden die Einstellungen für die VoIP-Testkonfiguration "TestConfig1" geändert. Der Befehl legt als "TargetDialplan " die Wähleinstellungen für "site:Redmond1" fest. Da das Ändern der Wähleinstellungen eine Änderung der Normalisierungsregeln zur Folge haben könnte, wurde auch der Wert von "ExpectedTranslationNumber" geändert, um das erwartete Verhalten der Normalisierungsregeln für diese Wähleinstellungen widerzuspiegeln.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -TargetDialplan site:Redmond1 -ExpectedTranslatedNumber "+912065551212"

## Detaillierte Beschreibung

Vor der Implementierung von VoIP-Routen und -Richtlinien ist es sinnvoll, diese Einstellungen für verschiedene Telefonnummern zu testen, um die erwartete Funktionsweise sicherzustellen. Zu diesem Zweck können mit diesem Cmdlet Testszenarien geändert werden.

Über das Cmdlet **Set-CsVoiceTestConfiguration** werden VoIP-Route, Verwendung, Wählplan und VoIP-Richtlinie geändert, die für eine angegebene Telefonnummer getestet werden sollen. All diese Informationen können über andere Cmdlets festgelegt und abgerufen werden (siehe Parameterbeschreibungen für dieses Thema).

Die mit diesem Cmdlet geänderten Konfigurationen werden mithilfe des Cmdlets **Test-CsVoiceTestConfiguration** getestet.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsVoiceTestConfiguration** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceTestConfiguration"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die Telefonnummer, die zum Testen der Richtlinien, Verwendungen usw. verwendet werden soll.</p>
<p>Dieser Wert kann maximal 512 Zeichen umfassen.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Der Name der erwarteten VoIP-Route während des Konfigurationstests. Wenn basierend auf dem Zielwählplan und der VoIP-Richtlinie eine andere Route verwendet wird, kann der Test nicht erfolgreich abgeschlossen werden. Die verfügbaren VoIP-Routen können über das Cmdlet <strong>Get-CsVoiceRoute</strong> abgerufen werden.</p>
<p>Dieser Wert kann maximal 256 Zeichen umfassen.</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die Telefonnummer im erwarteten Format nach der Übersetzung. Dabei handelt es sich um den Wert des Parameters &quot;DialedNumber&quot; nach der Normalisierung. Wenn Sie das Cmdlet <strong>Test-CsVoiceTestConfiguration</strong> ausführen und das Ergebnis von &quot;DialedNumber&quot; nicht mit dem Wert in &quot;ExpectedTranslatedNumber&quot; übereinstimmt, gilt der Test als nicht erfolgreich.</p>
<p>Dieser Wert kann maximal 512 Zeichen umfassen.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Der Name der erwarteten PSTN-Verwendung während des Konfigurationstests. Wenn basierend auf dem Zielwählplan und der VoIP-Richtlinie eine andere PSTN-Verwendung eingesetzt wird, kann der Test nicht erfolgreich abgeschlossen werden. Die verfügbaren Telefonverwendungen können über das Cmdlet <strong>Get-CsPstnUsage</strong> abgerufen werden.</p>
<p>Dieser Wert kann maximal 256 Zeichen umfassen.</p></td>
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
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Eine Zeichenfolge zur eindeutigen Kennzeichnung des Testszenarios, das geändert werden soll.</p>
<p>Da dieses Objekt nur mit dem globalen Gültigkeitsbereich erstellt werden kann, umfasst der Wert dieses Parameters keinen Gültigkeitsbereich. Aus diesem Grund ist nur ein Name erforderlich.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>TestConfiguration</p></td>
<td><p>Ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration&quot;, das eine vorhandene VoIP-Testkonfiguration mit den Änderungen umfasst, die Sie an der Konfiguration vornehmen möchten. Objekte von diesem Typ können mit dem Cmdlet <strong>Get-CsVoiceTestConfiguraton</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetDialplan</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Der Identitätswert der Wähleinstellungen, die für diesen Test verwendet werden sollen. Wähleinstellungen können über das Cmdlet <strong>Get-CsDialPlan</strong> abgerufen werden.</p>
<p>Dieser Wert kann maximal 40 Zeichen umfassen.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Der Identitätswert der VoIP-Richtlinie, für die dieser Test ausgeführt werden soll. VoIP-Richtlinien können über das Cmdlet <strong>Get-CsVoicePolicy</strong> abgerufen werden.</p>
<p>Dieser Wert kann maximal 40 Zeichen umfassen.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration-Objekt. Akzeptiert eine weitergeleitete Eingabe von VoIP-Testkonfigurationsobjekten.

## Rückgabetypen

Dieses Cmdlet gibt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration" zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

