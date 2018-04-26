---
title: Export-CsConfiguration
TOCTitle: Export-CsConfiguration
ms:assetid: 7da7e133-e405-466c-a852-06a4fb678c59
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398627(v=OCS.15)
ms:contentKeyID: 49294532
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Exportiert Ihre Lync Server-Topologie, -Richtlinien und -Konfigurationseinstellungen in eine Datei. Unter anderem kann diese Datei nach einem Upgrade, einem Hardwareausfall oder einem anderen Problem, das zu Datenverlust geführt hat, zum Wiederherstellen dieser Informationen im zentralen Verwaltungsspeicher verwendet werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Export-CsConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    Export-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 exportiert Lync Server-Daten aus dem zentralen Verwaltungsspeicher in eine Datei namens "C:\\Config.zip".

    Export-CsConfiguration -FileName "C:\Config.zip"

## Detaillierte Beschreibung

Computer, auf denen Lync Server-Dienste oder -Serverrollen ausgeführt werden, benötigen eine Kopie der aktuellen Topologie, der aktuellen Konfigurationseinstellungen und der aktuellen Richtlinien, damit sie die ihnen zugewiesene Rolle erfüllen können. Lync Server ist dafür zuständig sicherzustellen, dass diese Informationen an jeden entsprechenden Computer weitergeleitet werden.

Die Cmdlets **Export-CsConfiguration** und **Import-CsConfiguration** werden zum Sichern und Wiederherstellen der Lync Server-Topologie, der Konfigurationseinstellungen und der Richtlinien während eines Upgrades des zentralen Verwaltungsspeichers eingesetzt. Das Cmdlet **Export-CsConfiguration** ermöglicht Ihnen das Exportieren von Daten in eine ZIP-Datei. Anschließend können Sie mit dem Cmdlet **Import-CsConfiguration** die ZIP-Datei lesen und die Topologie, die Konfigurationseinstellungen und die Richtlinien im zentralen Verwaltungsspeicher wiederherstellen. Danach replizieren die Replikationsdienste von Lync Server die wiederhergestellten Informationen auf anderen Computern, auf denen die Lync Server-Dienste ausgeführt werden.

Die Möglichkeit zum Exportieren und Importieren von Konfigurationsdaten wird auch bei der Anfangskonfiguration von Computern (z. B. Edgeservern) in Ihrem Umkreisnetzwerk genutzt. Bei der Konfiguration eines Computers im Umkreisnetzwerk müssen Sie zunächst eine manuelle Replikation mit den "CsConfiguration"-Cmdlets durchführen: Sie müssen die Konfigurationsdaten mit dem Cmdlet **Export-CsConfiguration** exportieren und die ZIP-Datei anschließend auf den Computer im Umkreisnetzwerk kopieren. Anschließend können Sie die Daten mit dem Cmdlet **Import-CsConfiguration** und dem Parameter "LocalStore" importieren. Dies ist nur einmal erforderlich; danach wird die Replikation automatisch durchgeführt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Export-CsConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsConfiguration"}

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
<td><p><em>FileName</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Pfad zur ZIP-Datei, die beim Ausführen des Cmdlets <strong>Export-CsConfiguration</strong> erstellt werden soll. Beispiel: -FileName &quot;C:\Config.zip&quot;. Beachten Sie, dass Sie entweder den Parameter &quot;FileName&quot; oder den Parameter &quot;AsBytes&quot; verwenden müssen. Es dürfen nicht beide Parameter beim Aufrufen des Cmdlets <strong>Export-CsConfiguration</strong> eingesetzt werden.</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Gibt Topologieinformationen als Bytearray zurück. Die zurückgegebenen Daten müssen anschließend in einer Variablen gespeichert werden, um vom Cmdlet <strong>Import-CsConfiguration</strong> verwendet werden zu können. Die Parameter &quot;AsBytes&quot; und &quot;FileName&quot; können nicht innerhalb desselben Befehls verwendet werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können. Verwenden Sie diese Syntax, um den Parameter &quot;Force&quot; auf &quot;True&quot; einzustellen:</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Konfigurationsdaten vom lokalen Computer und nicht aus dem zentralen Verwaltungsspeicher selbst ab.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Export-CsConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Wenn das Cmdlet **Export-CsConfiguration** zusammen mit dem Parameter "AsBytes" aufgerufen wird, werden Konfigurationsinformationen in Form eines Bytearrays zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Import-CsConfiguration](import-csconfiguration.md)

