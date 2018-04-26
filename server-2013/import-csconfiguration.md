---
title: Import-CsConfiguration
TOCTitle: Import-CsConfiguration
ms:assetid: 9a9c27f2-313c-4327-aeed-c47852a831ec
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398800(v=OCS.15)
ms:contentKeyID: 49294868
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Importiert Ihre Lync Server-Topologie, -Richtlinien und -Konfigurationseinstellungen entweder in den zentralen Verwaltungsspeicher oder auf den lokalen Computer. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Import-CsConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    Import-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 dient zum Importieren der aktuellen Topologie, Konfigurationseinstellungen und Richtlinien aus der Datei "C:\\Config.zip" in den zentralen Verwaltungsspeicher.

    Import-CsConfiguration -FileName "C:\Config.zip"

## BEISPIEL 2

Beispiel 2 zeigt, wie Daten anfänglich auf einen Computer im Umkreisnetzwerk repliziert werden können. In diesem Beispiel wurden Konfigurationsdaten in die Datei "Config.zip" exportiert. Diese Datei wurde in den Ordner "C:\\" auf dem Computer im Umkreisnetzwerk kopiert. "Import-CsConfiguration" dient anschließend zum Importieren dieser Daten unter Angabe des Parameters "LocalStore", was bewirkt, dass die Daten auf den lokalen Computer und nicht in den zentralen Verwaltungsspeicher importiert werden.

    Import-CsConfiguration -FileName "C:\Config.zip" -LocalStore

## BEISPIEL 3

Die beiden Befehle in Beispiel 3 exportieren ohne Verwendung einer ZIP-Datei die aktuelle Topologie, die aktuellen Konfigurationseinstellungen und die aktuellen Richtlinien und importieren diese Daten anschließend auf den lokalen Computer. Hierzu verwendet der erste Befehl das Cmdlet **Export-CsConfiguration** und den Parameter "AsBytes", um die aktuelle Topologie, die aktuellen Konfigurationseinstellungen und die aktuellen Richtlinien als Bytearray zu exportieren. Dieses Bytearray wird in der Variablen "$x" gespeichert. Im zweiten Befehl werden das Cmdlet **Import-CsConfiguration** und der Parameter "ByteInput" verwendet, um die in "$x" gespeicherten Informationen zu importieren. Der Parameter "LocalStore" bewirkt, dass die Daten auf den lokalen Computer und nicht in den zentralen Verwaltungsspeicher importiert werden. Folglich werden die Daten aus dem zentralen Verwaltungsspeicher auf den lokalen Computer kopiert.

    $x = Export-CsConfiguration -AsBytes
    Import-CsConfiguration -ByteInput $x -LocalStore

## Detaillierte Beschreibung

Computer, auf denen Lync Server-Dienste oder -Serverrollen ausgeführt werden, müssen zum Ausführen der zugewiesenen Rolle über eine Kopie der aktuellen Topologie, aktuellen Konfigurationseinstellungen, aktuellen Richtlinien usw. verfügen. Lync Server ist dafür zuständig, dass diese Informationen an jeden Computer übermittelt werden, der diese benötigt.

Die Cmdlets "Import-CsConfiguration" und "Export-CsConfiguration" dienen während eines Upgrades des zentralen Verwaltungsspeichers zum Sichern und Wiederherstellen Ihrer Lync Server-Topologie, -Konfigurationseinstellungen und -Richtlinien. Das Cmdlet **Export-CsConfiguration** ermöglicht das Exportieren von Daten in eine ZIP-Datei. Mithilfe des Cmdlets **Import-CsConfiguration** können Sie diese ZIP-Datei anschließend lesen und die Topologie, Einstellungen und Richtlinien im zentralen Verwaltungsspeicher wiederherstellen. Anschließend dienen die Replikationsdienste von Lync Server zum Replizieren der wiederhergestellten Informationen auf Computern, auf denen Dienste ausgeführt werden.

Die Fähigkeit zum Exportieren und Importieren von Konfigurationsdaten kommt auch bei der Erstkonfiguration von Computern in Ihrem Umkreisnetzwerk zum Einsatz (beispielsweise beim Edgeserver). Bei der Konfiguration eines Computers im Umkreisnetzwerk müssen Sie zuerst mithilfe der CsConfiguration-Cmdlets eine manuelle Replikation durchführen. Sie müssen die Konfigurationsdaten mithilfe des Cmdlets **Export-CsConfiguration** exportieren und die ZIP-Datei auf den Computer im Umkreisnetzwerk kopieren. Anschließend können Sie das Cmdlet **Import-CsConfiguration** und den Parameter "LocalStore" verwenden, um die Daten zu importieren. Dieser Schritt muss nur einmal ausgeführt werden. Danach erfolgt die Replikation automatisch.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Import-CsConfiguration** lokal ausführen: RTCUniversalServerAdmins. Zum Ausführen dieses Cmdlets müssen Sie nicht nur der Gruppe "RTCUniversalServerAdmins" angehören, sondern auch entweder ein lokaler Administrator sein oder über lokale Konfigurations- und Replikationsberechtigungen verfügen. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsConfiguration"}

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
<td><p><em>ByteInput</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Liest Topologieinformationen von einem Bytearray, das in einer Variablen gespeichert ist. Dieses Bytearray wird mithilfe des Parameters &quot;ByteInput&quot; erstellt, wenn das Cmdlet <strong>Export-CsConfiguration</strong> aufgerufen wird.</p>
<p>Sie können die Parameter &quot;ByteInput&quot; und &quot;FileName&quot; nicht im selben Befehl verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Pfad zur ZIP-Datei, die von &quot;Export-CsConfiguration&quot; erstellt wurde. Beispiel: -FileName &quot;C:\Config.zip&quot;. Beachten Sie, dass Sie entweder den Parameter &quot;ByteInput&quot; oder &quot;FileName&quot; verwenden müssen. Es dürfen aber nicht beide Parameter verwendet werden, wenn das Cmdlet <strong>Import-CsConfiguration</strong> aufgerufen wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Umgeht Eingabeaufforderungen, die ansonsten angezeigt würden, sollte bei Ausführung des Befehls ein nicht schwerwiegender Fehler auftreten. Verwenden Sie diese Syntax, um den Parameter &quot;Force&quot; auf &quot;True&quot; festzulegen:</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Kopiert die Konfigurationsdaten nicht in den zentralen Verwaltungsspeicher, sondern auf den lokalen Computer.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Import-CsConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Import-CsConfiguration** gibt keine Werte oder Objekte zurück.

## Siehe auch

#### Weitere Ressourcen

[Export-CsConfiguration](export-csconfiguration.md)

