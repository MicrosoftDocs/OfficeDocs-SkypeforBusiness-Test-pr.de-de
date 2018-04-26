---
title: Set-CsVoicemailReroutingConfiguration
TOCTitle: Set-CsVoicemailReroutingConfiguration
ms:assetid: c16a0d47-318b-46e4-991c-e4842403dbe3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412948(v=OCS.15)
ms:contentKeyID: 49295297
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicemailReroutingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert Einstellungen, mit denen Festnetznummern (Public Switched Telephone Network, PSTN) bereitgestellt werden, um auf Exchange UM-Funktionen wie den Teilnehmerzugriff und die automatische Telefonzentrale zuzugreifen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicemailReroutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel werden die Konfigurationseinstellungen für die Voicemailumleitung für den Standort "Redmond1" aktiviert.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True

## BEISPIEL 2

Die auf den Standort "Redmond1" zugewiesenen Einstellungen für die Voicemailumleitung werden in diesem Beispiel geändert, und die Telefonnummer für den Teilnehmerzugriff wird auf +14255551213 festgelegt.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## Detaillierte Beschreibung

Mit diesem Cmdlet können Sie Einstellungen ändern, die festlegen, wohin Anrufe an die automatische Telefonzentrale und Teilnehmerzugriffsanrufe geleitet werden, wenn keine IP-Verbindung mit einem Exchange UM-Server verfügbar ist.

Die automatische Telefonzentrale und der Teilnehmerzugriff sind Funktionen von Exchange UM. Die automatische Telefonzentrale bietet Spracherkennung und Tonwahlverfahren (Dual-Tone Multifrequency, DTMF) für externe Anrufer zur Navigation im Telefonsystem eines Unternehmens, um auf diese Weise eine Verbindung mit der gewünschten Abteilung oder mit dem gewünschten Mitarbeiter herzustellen oder um im Modus zum Nachrichtenempfang Nachrichten für Benutzer anzunehmen. (Im Modus zum Nachrichtenempfang sollte die Sprachumleitung aktiviert werden.) Mit dem Teilnehmerzugriff können interne Benutzer über ein Telefon auf ihren Microsoft Outlook-Posteingang zugreifen. Über die mit diesen Einstellungen bereitgestellten Nummern können Anrufer Voicemailnachrichten für Enterprise-VoIP-Benutzer hinterlassen (Einstellung "AutoAttendantNumber"), die sie auch wieder abrufen können, selbst wenn an einem Remotestandort die IP-Verbindung von der Lync Server-Bereitstellung mit Exchange UM im Datencenter nicht verfügbar ist (Einstellung "SubscriberAccessNumber").

Beachten Sie, dass diese Einstellungen erst dann verfügbar sind, wenn die Eigenschaft "Enabled" auf "True" festgelegt wurde.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsVoicemailReroutingConfiguration** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicemailReroutingConfiguration"}

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
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Telefonnummer der automatischen Telefonzentrale, an die Versuche, Voicemails zu hinterlassen, weitergeleitet werden sollen.</p>
<p>Die für diesen Parameter bereitgestellte Nummer muss ein Anschluss-URI eines vorhandenen Kontaktobjekts sein.</p>
<p>Der Wert muss eine Nummer sein, die mit einer Zahl von 1 bis 9 beginnt, der optional ein Pluszeichen (+) vorangestellt werden kann, gefolgt von einer beliebigen Anzahl von Ziffern.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob Zugriffsversuche auf Voicemails über PSTN weitergeleitet werden sollen, wenn keine IP-Verbindung vorhanden ist.</p></td>
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
<td><p>Die eindeutige ID der Konfiguration, die geändert werden soll. Der Identitätswert dieses Cmdlets lautet entweder &quot;Global&quot; oder &quot;Site:&lt;Standortname&gt;&quot;, wobei &lt;Standortname&gt; der Name des Standorts ist, für den die Einstellungen gelten.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>VoicemailReroutingConfiguration</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen.</p>
<p>Dieses Objekt muss vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration&quot; sein, das durch Aufrufen des Cmdlets <strong>Get-CsVoicemailReroutingConfiguration</strong> abgerufen werden kann.</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Teilnehmerzugriffsnummer, an die die Versuche zum Abrufen von Voicemail weitergeleitet werden sollen.</p>
<p>Die für diesen Parameter bereitgestellte Nummer muss ein Anschluss-URI eines vorhandenen Kontaktobjekts sein.</p>
<p>Der Wert muss eine Nummer sein, die mit einer Zahl von 1 bis 9 beginnt, der optional ein Pluszeichen (+) vorangestellt werden kann, gefolgt von einer beliebigen Anzahl von Ziffern.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration-Objekt. Akzeptiert eine weitergeleitete Eingabe von Konfigurationsobjekten für die Voicemailumleitung.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

