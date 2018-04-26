---
title: Remove-CsCpsConfiguration
TOCTitle: Remove-CsCpsConfiguration
ms:assetid: 546343e1-a2e4-4bc0-bf6d-c8ae9bb3e690
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398358(v=OCS.15)
ms:contentKeyID: 49294024
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCpsConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt eine vorhandene Konfiguration des Diensts zum Parken von Anrufen. Die Funktion zum Parken von Anrufen ist ein Dienst, über den Benutzer eingehende Anrufe "parken" können. Beim Parken eines Anrufs wird der Anruf an eine Nummer in einem angegebenen Bereich (oder Orbit) übergeben und anschließend sofort in der Warteschleife platziert. Sämtliche Benutzer (nicht nur der Benutzer, der den Anruf ursprünglich entgegengenommen hat) können das Gespräch von einem beliebigen Telefon aus fortführen, indem sie einfach die richtige Nummer eingeben. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsCpsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel wird das Cmdlet **Remove-CsCpsConfiguration** verwendet, um die Konfiguration des Diensts zum Parken von Anrufen mit der Identität "site:Redmond1" zu löschen. Da Identitäten eindeutig sind, wird über diesen Befehl nur eine einzelne Konfiguration gelöscht.

    Remove-CsCpsConfiguration -Identity site:Redmond1

## BEISPIEL 2

In Beispiel 2 werden alle Konfigurationen für den Dienst zum Parken von Anrufen gelöscht, die auf Standortebene definiert wurden. Hierzu verwendet der Befehl zunächst das Cmdlet **Get-CsCpsConfiguration** und den Parameter "Filter", um alle Konfigurationen des Diensts zum Parken von Anrufen zurückzugeben, die auf Standortebene definiert wurden. Über den Platzhalter "site:\*" wird sichergestellt, dass ausschließlich Einstellungen zurückgegeben werden, deren Identitätswert mit der Zeichenfolge "site:" beginnt. Diese gefilterte Auflistung wird anschließend an das Cmdlet **Remove-CsCpsConfiguration** weitergeleitet, um sämtliche Elemente in der Auflistung zu löschen. Beachten Sie Folgendes: Wenn Sie Einstellungen des Diensts zum Parken von Anrufen von einem Standort entfernen, verwendet der Standort anschließend automatisch die auf globaler Ebene konfigurierten Einstellungen des Diensts zum Parken von Anrufen.

    Get-CsCpsConfiguration -Filter site:* | Remove-CsCpsConfiguration

## Detaillierte Beschreibung

Dieses Cmdlet wird zum Entfernen einer Konfiguration des Diensts zum Parken von Anrufen verwendet. Eine Konfiguration des Diensts für das Parken von Anrufen gibt an, wie mit einem geparkten Anruf verfahren wird. Wenn ein geparkter Anruf beispielsweise nach einem bestimmten Zeitraum nicht entgegengenommen wird, kann er automatisch an einen anderen Benutzer (z. B. an einen Administrator oder an eine Reaktionsgruppe) weitergeleitet werden. Um zu verhindern, dass Anrufe vergessen werden, können die Einstellungen so konfiguriert werden, dass das Telefon nach einem bestimmten Zeitraum erneut läutet. Darüber hinaus kann der Dienst für das Parken von Anrufen so konfiguriert werden, dass für den Anrufer eines geparkten Anrufs Wartemusik wiedergegeben wird.

Mit diesem Cmdlet können sämtliche Konfigurationen zum Parken von Anrufen entfernt werden, einschließlich der globalen Konfiguration. Bei der globalen Konfiguration wird diese jedoch nicht wirklich entfernt, sondern stattdessen auf die Standardwerte zurückgesetzt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsCpsConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCpsConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die eindeutige ID für die Konfiguration des Diensts zum Parken von Anrufen, die entfernt werden soll. Diese ID lautet entweder &quot;Global&quot; oder &quot;site:&lt;Standortname&gt;&quot;. Dabei steht &lt;Standortname&gt; für den Namen des Standorts, für den die Konfiguration gilt.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings-Objekt. Akzeptiert eine weitergeleitete Eingabe von Konfigurationsobjekten des Diensts zum Parken von Anrufen.

## Rückgabetypen

Entfernt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings".

## Siehe auch

#### Weitere Ressourcen

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

