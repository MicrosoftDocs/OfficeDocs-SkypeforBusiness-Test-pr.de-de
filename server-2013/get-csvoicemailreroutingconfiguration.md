---
title: Get-CsVoicemailReroutingConfiguration
TOCTitle: Get-CsVoicemailReroutingConfiguration
ms:assetid: 25e401eb-6a84-468f-b0eb-5b794f20b5bc
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425732(v=OCS.15)
ms:contentKeyID: 49293457
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicemailReroutingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ruft Einstellungen ab, mit denen Festnetztelefonnummern (Public Switched Telephone Network, PSTN) bereitgestellt werden, um auf Exchange UM-Funktionen wie Teilnehmerzugriff und automatischen Telefonzentralen zuzugreifen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicemailReroutingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

In diesem Beispiel werden alle Konfigurationseinstellungen für die Voicemailumleitung in dieser Bereitstellung von Lync Server abgerufen. Wenn es beispielsweise drei Zweigstellen gibt, in denen eine Survivable Branch Appliance bereitgestellt wurde, gibt dieser Befehl drei Konfigurationssätze für die Voicemailumleitung zurück.

    Get-CsVoicemailReroutingConfiguration

## BEISPIEL 2

In diesem Beispiel werden die Konfigurationseinstellungen für die Voicemailumleitung am Standort "BranchOffice\_Portland" abgerufen.

    Get-CsVoicemailReroutingConfiguration -Identity site:BranchOffice_Portland

## BEISPIEL 3

In diesem Beispiel werden alle Voicemailumleitungseinstellungen für alle Standorte abgerufen, deren Name mit "BranchOffice" beginnt (z. B. "BranchOffice\_Portland", "BranchOffice\_Sacramento").

    Get-CsVoicemailReroutingConfiguration -Filter *:BranchOffice*

## BEISPIEL 4

In diesem Beispiel werden alle Konfigurationseinstellungen für die Voicemailumleitung abgerufen, die nicht aktiviert wurden. Der Befehl ruft zunächst das Cmdlet **Get-CsVoicemailReroutingConfiguration** auf, das eine Auflistung aller Konfigurationseinstellungen für die Voicemailumleitung abruft. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** beschränkt diese Auflistung auf die Konfigurationseinstellungen, bei denen die Eigenschaft "Enabled" den Wert "False" aufweist (der Vergleichsoperator "-eq" steht für "equal to").

    Get-CsVoicemailReroutingConfiguration | Where-Object {$_.Enabled -eq $False}

## Detaillierte Beschreibung

Mit diesem Cmdlet werden Einstellungen abgerufen, die festlegen, wohin Anrufe bei der automatischen Telefonzentrale und Teilnehmerzugriffsanrufe geleitet werden, wenn in der Zweigstelle keine IP-Verbindung zwischen Lync Server und dem Exchange UM-Server im Datencenter verfügbar ist.

Die automatische Telefonzentrale und der Teilnehmerzugriff sind Funktionen von Exchange UM. Die automatische Telefonzentrale bietet Spracherkennung und Tonwahlverfahren (Dual-Tone Multifrequency, DTMF) für externe Anrufer zur Navigation im Telefonsystem eines Unternehmens, um auf diese Weise eine Verbindung mit der gewünschten Abteilung oder dem gewünschten Mitarbeiter herzustellen oder um im Modus zum Nachrichtenempfang Nachrichten für Benutzer anzunehmen. (Im Modus zum Nachrichtenempfang sollte die Sprachumleitung aktiviert werden.) Mit dem Teilnehmerzugriff können interne Benutzer über ein Telefon auf ihren Microsoft Outlook-Posteingang zugreifen. Über die mit diesen Einstellungen bereitgestellten Nummern können Anrufer Voicemailnachrichten für Enterprise-VoIP-Benutzer hinterlassen (Einstellung "AutoAttendantNumber"), die sie auch wieder abrufen können, selbst wenn an einem Remotestandort die IP-Verbindung von der Lync Server-Bereitstellung mit Exchange UM im Datencenter nicht verfügbar ist (Einstellung "SubscriberAccessNumber").

Durch Aufrufen dieses Cmdlets ohne Parameter werden alle Konfigurationseinstellungen für die Voicemailumleitung zurückgegeben.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsVoicemailReroutingConfiguration** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicemailReroutingConfiguration"}

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
<td><p>Mit dem Parameter &quot;Filter&quot; können Sie Konfigurationseinstellungen für einen bestimmten Standortsatz anhand eines Platzhalterabgleichs abrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die eindeutige ID der Konfiguration, die abgerufen werden soll. Der Identitätswert dieses Cmdlets lautet entweder &quot;Global&quot; oder &quot;Site:&lt;Standortname&gt;&quot;, wobei &lt;Standortname&gt; der Name des Standorts ist, für den die Einstellungen gelten.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Daten zur Voicemail-Umleitungskonfiguration aus dem lokalen Replikat des zentralen Verwaltungsspeicher ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Gibt mindestens ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration" zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)

