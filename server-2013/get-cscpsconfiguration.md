---
title: Get-CsCpsConfiguration
TOCTitle: Get-CsCpsConfiguration
ms:assetid: d81ee8fe-d02b-4f60-a4d5-6aa84f65d156
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398948(v=OCS.15)
ms:contentKeyID: 49295570
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCpsConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zum Dienst für das Parken von Anrufen zurück. Die Funktion zum Parken von Anrufen ist ein Dienst, über den Benutzer eingehende Anrufe "parken" können. Beim Parken eines Anrufs wird der Anruf an eine Nummer in einem angegebenen Bereich (oder Orbit) übergeben und anschließend sofort in der Warteschleife platziert. Sämtliche Benutzer (nicht nur der Benutzer, der den Anruf ursprünglich entgegengenommen hat) können das Gespräch von einem beliebigen Telefon im System aus fortführen, indem sie die richtige Nummer eingeben. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCpsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird eine Auflistung aller Konfigurationen für den Dienst zum Parken von Anrufen abgerufen, die für Ihre Organisation definiert wurden.

    Get-CsCpsConfiguration

## BEISPIEL 2

In Beispiel 2 werden nur die Konfigurationen für den Dienst zum Parken von Anrufen mit dem Identitätswert "site:Redmond1" abgerufen.

    Get-CsCpsConfiguration -Identity site:Redmond1

## BEISPIEL 3

In Beispiel 3 werden mithilfe des Parameters "Filter" alle Konfigurationen für den Dienst zum Parken von Anrufen zurückgegeben, die auf Standortebene konfiguriert wurden. Die Platzhalterzeichenfolge "site:\*" weist das Cmdlet **Get-CsCpsConfiguration** an, nur die Einstellungen zurückzugeben, deren Identitätswert mit der Zeichenfolge "site:" beginnt.

    Get-CsCpsConfiguration -Filter site:*

## BEISPIEL 4

Wie in Beispiel 3 wird der Parameter "Filter" verwendet, um einen Teilsatz aller definierten Konfigurationen für den Dienst zum Parken von Anrufen abzurufen. In diesem Fall wird nach der Zeichenfolge ":re\*" gefiltert, wodurch alle Konfigurationen für den Dienst zum Parken von Anrufen zurückgegeben werden, deren Namen mit den Buchstaben "re" beginnen, z. B. "Redmond1", "Redmond2" und "RemoteComputer".

    Get-CsCpsConfiguration -Filter *:re*

## BEISPIEL 5

In Beispiel 5 werden alle Einstellungen des Diensts zum Parken von Anrufen zurückgegeben, bei denen für einen geparkten Anruf keine Wartemusik wiedergegeben wird. Zu diesem Zweck verwendet der Befehl zunächst das Cmdlet **Get-CsCpsConfiguration** zum Abrufen aller Einstellungen des Diensts für das Parken von Anrufen in Ihrer Organisation. Diese Informationen werden anschließend an das Cmdlet **Where-Object** weitergeleitet, das wiederum einen Filter anwendet, um die zurückgegebenen Daten auf diejenigen Elemente zu beschränken, deren Eigenschaft "EnableMusicOnHold" auf "False" festgelegt ist (der Vergleichsoperator "-eq" steht für "equal to").

    Get-CsCpsConfiguration | Where-Object {$_.EnableMusicOnHold -eq $False}

## Detaillierte Beschreibung

Dieses Cmdlet wird verwendet, um mindestens eine Konfiguration des Diensts für das Parken von Anrufen abzurufen. Eine Konfiguration des Diensts für das Parken von Anrufen gibt an, wie mit einem geparkten Anruf verfahren wird. Wenn ein geparkter Anruf beispielsweise nach einem bestimmten Zeitraum nicht beantwortet wird, kann er automatisch an einen anderen Benutzer, z. B. an einen Administrator, oder an eine Reaktionsgruppe weitergeleitet werden. Um zu verhindern, dass Anrufe vergessen werden, können die Einstellungen auch so konfiguriert werden, dass das Telefon nach einem bestimmten Zeitraum erneut läutet. Darüber hinaus kann der Dienst für das Parken von Anrufen so konfiguriert werden, dass für den Anrufer eines geparkten Anrufs Wartemusik wiedergegeben wird.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsCpsConfiguration** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCpsConfiguration"}

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
<td><p>Ermöglicht das Ausführen einer Platzhalterzeichensuche, um nur diejenigen Konfigurationen abzurufen, deren Identitätswerte mit der Platzhalterzeichenfolge übereinstimmen.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die eindeutige ID für die Konfiguration des Diensts zum Parken von Anrufen, die abgerufen werden soll. Diese ID lautet entweder &quot;Global&quot; oder &quot;site:&lt;Standortname&gt;&quot;. Dabei steht &lt;Standortname&gt; für den Namen des Standorts, für den die Konfiguration gilt.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Informationen zum Dienst für das Parken von Anrufen aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Gibt mindestens ein Objekt vom Typ Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

