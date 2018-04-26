---
title: Get-CsCdrConfiguration
TOCTitle: Get-CsCdrConfiguration
ms:assetid: 4af8ffa2-63d3-4873-8dac-5afede090d4f
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398298(v=OCS.15)
ms:contentKeyID: 49293924
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCdrConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen (KDS) zurück. Die KDS-Funktion ermöglicht das Nachverfolgen von Peer-zu-Peer-, VoIP- und Konferenzanrufen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCdrConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Bei diesem Beispiel gibt das Cmdlet **Get-CsCdrConfiguration** eine Auflistung aller Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen zurück, die für die Verwendung in Ihrer Organisation konfiguriert sind.

    Get-CsCdrConfiguration

## BEISPIEL 2

In Beispiel 2 wird der Parameter "Identity" verwendet, um eine einzelne Auflistung von KDS-Einstellungen zurückzugeben: die Einstellungen mit dem Identitätswert "site:Redmond".

    Get-CsCdrConfiguration -Identity site:Redmond

## BEISPIEL 3

In Beispiel 3 werden mithilfe des Parameters "Filter" alle Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen zurückgegeben, die auf Standortebene konfiguriert wurden. Der Filterwert "site:\*" gibt alle Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen zurück, deren Identitätswert mit dem Zeichenfolgenwert "site:" beginnt. Laut Definition sind dies Einstellungen, die auf Standortebene konfiguriert wurden.

    Get-CsCdrConfiguration -Filter site:*

## BEISPIEL 4

Im vierten Beispiel wird eine Auflistung mit allen Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen zurückgegeben, bei denen der Wert der Eigenschaft "KeepCallDetailForDays" kleiner als 30 Tage ist. Zu diesem Zweck verwendet der Befehl zunächst das Cmdlet **Get-CsCdrConfiguration**, um eine Auflistung aller in der Organisation konfigurierten Einstellungen für die Aufzeichnung von Kommunikationsdatensätzen zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Einstellungen herausfiltert, bei denen die Eigenschaft "KeepCallDetailForDays" einen geringeren Wert als 30 aufweist.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30}

## Detaillierte Beschreibung

Die KDS-Funktion bietet eine Möglichkeit, die Nutzung von Lync Server-Funktionen wie VoIP-Anrufe, Chatnachrichten, Dateiübertragungen, Audio-/Videokonferenzen und Anwendungsfreigabesitzungen nachzuverfolgen. KDS (das nur verfügbar ist, wenn Sie den Überwachungsdienst bereitgestellt haben) zeichnet Verwendungsinformationen auf: Hierbei werden z. B. Anrufer, Angerufener, Anrufdauer und Informationen dazu aufgezeichnet, ob Dateien übertragen wurden. (Die KDS-Funktion zeichnet den eigentlichen Anruf jedoch nicht auf.)

Die KDS-Funktion verfolgt auch Informationen zu Anruffehlern nach, so z. B. detaillierte Diagnosedaten für Peer-zu-Peer-Sitzungen und Konferenzanrufe.

Als Administrator können Sie bestimmen, ob KDS in Ihrer Organisation zum Einsatz kommen soll. Sofern der Überwachungsdienst bereitgestellt wurde, kann KDS aktiviert oder deaktiviert werden. Sie können KDS außerdem entweder in der gesamten Organisation oder standortbezogen aktivieren oder deaktivieren. Sie können KDS z. B. am Standort "Redmond" aktivieren, aber am Standort "Paris" deaktivieren.

Das Cmdlet **Get-CsCdrConfiguration** bietet eine Möglichkeit der Rückgabe detaillierter Informationen dazu, wie die Aufzeichnung von Kommunikationsdatensätzen (KDS) in Ihrer Organisation verwendet wird.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsCdrConfiguration** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCdrConfiguration"}

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
<td><p>Ermöglicht die Verwendung von Platzhalterzeichen, um eine Auflistung von KDS-Konfigurationseinstellungen zurückzugeben. Verwenden Sie beispielsweise folgende Syntax, um eine Auflistung aller auf der Standortebene konfigurierten Einstellungen zurückzugeben. -Filter site:*. Verwenden Sie folgende Syntax, um eine Auflistung aller Einstellungen zurückzugeben, deren Identitätswert den Zeichenfolgenwert &quot;Western&quot; aufweist: -Filter *Western*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Gibt die eindeutige ID für die Auflistung der zurückzugebenden KDS-Konfigurationseinstellungen an. Verwenden Sie folgende Syntax, um auf die globalen Einstellungen zu verweisen: -Identity global. Verwenden Sie eine Syntax wie die folgende, um auf eine Auflistung zu verweisen, die auf Standortebene konfiguriert ist: -Identity site:Redmond. Beachten Sie, dass beim Angeben eines Identitätswerts keine Platzhalterzeichen verwendet werden können. Wenn Platzhalter nötig sind, verwenden Sie stattdessen den Parameter &quot;Filter&quot;.</p>
<p>Wenn dieser Parameter nicht angegeben ist, gibt das Cmdlet <strong>Get-CsCdrConfiguration</strong> eine Auflistung aller in der Organisation verwendeten KDS-Konfigurationseinstellungen zurück.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die KDS-Konfigurationsdaten aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsCdrConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsCdrConfiguration** werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

