---
title: Get-CsConferenceDisclaimer
TOCTitle: Get-CsConferenceDisclaimer
ms:assetid: 2382aaef-9c5e-43f8-99de-6c880134db7d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425714(v=OCS.15)
ms:contentKeyID: 49293430
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDisclaimer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu dem in Ihrer Organisation verwendeten Konferenzhaftungsausschluss zurück. Der Konferenzhaftungssausschluss ist eine Meldung, die Benutzern angezeigt wird, die der Konferenz über einen Link beitreten (z. B. Benutzer, die einen Konferenzlink in einen Browser wie Windows Internet Explorer einfügen). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 gibt Informationen zu allen Konferenzhaftungsausschlüssen zurück, die für die Verwendung in Ihrer Organisation konfiguriert sind. Da nur ein einziger Haftungsausschluss (auf globaler Ebene) konfiguriert werden kann, müssen Sie beim Ausführen dieses Befehls keinen Identitätswert angeben.

    Get-CSConferenceDisclaimer

## Detaillierte Beschreibung

Beim Konfigurieren der Konferenzeinstellungen können Administratoren einen rechtlichen Haftungsausschluss eingeben, der den Teilnehmern zum Zeitpunkt des Beitritts zu von Lync Server gehosteten Konferenzen angezeigt wird. In diesem Haftungsausschluss werden im Allgemeinen rechtliche Auflagen und Rechte an geistigem Eigentum für diese Konferenz erläutert, und Benutzer können erst dann der Konferenz beitreten, wenn sie den in diesem Haftungsausschluss aufgeführten Bestimmungen zustimmen. Dieser Haftungsausschluss wird nur Benutzern angezeigt, die einer Konferenz über einen Link beitreten.

Mit dem Cmdlet **Get-CsConferenceDisclaimer** können Sie den Text und den Header des Haftungsausschlusses Ihrer Organisation anzeigen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsConferenceDisclaimer** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDisclaimer"}

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
<td><p>Ermöglicht es Ihnen, beim Verweis auf einen Konferenzhaftungsausschluss Platzhalterwerte zu verwenden. Da nur eine einzelne, globale Instanz des Konferenzhaftungsausschlusses vorliegen kann, besteht kein Grund zur Verwendung des Parameters &quot;Filter&quot;. Sie können jedoch die folgende Syntax verwenden, um auf den globalen Haftungsausschluss zu verweisen: -Filter &quot;g*&quot;. Mit dieser Syntax werden alle Konferenzhaftungsausschlüsse zurückgegeben, deren Identitätswert mit dem Buchstaben &quot;g&quot; beginnt.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutiger Identitätswert des Konferenzhaftungsausschlusses. Da nur eine einzelne, globale Instanz des Konferenzhaftungsausschlusses vorliegen kann, müssen Sie beim Aufrufen des Cmdlets <strong>Get-CsConferenceDisclaimer</strong> keinen Identitätswert angeben. Sie können jedoch die folgende Syntax verwenden, um auf den globalen Haftungsausschluss zu verweisen: -Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Daten zum Konferenzhaftungsausschluss aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit dem Cmdlet **Get-CsConferenceDisclaimer** werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

