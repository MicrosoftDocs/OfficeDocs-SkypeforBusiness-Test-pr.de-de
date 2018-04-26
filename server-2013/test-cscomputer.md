---
title: Test-CsComputer
TOCTitle: Test-CsComputer
ms:assetid: 0b33d951-510d-445c-9b01-c6431fda6d47
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398162(v=OCS.15)
ms:contentKeyID: 49293135
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsComputer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Das Cmdlet **Test-CsComputer** überprüft den Status der auf dem lokalen Computer ausgeführten Lync Server-Dienste. Das Cmdlet überprüft ferner, ob die richtigen Lync Server Active Directory-Gruppen den geeigneten lokalen Gruppen auf dem Computer hinzugefügt und die notwendigen Firewallports des Computers geöffnet wurden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsComputer [-Report <String>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 überprüft den Dienstaktivierungsstatus für den lokalen Computer. Der Parameter "Verbose" ist im Befehl enthalten, um sicherzustellen, dass ausführliche Informationen zum Erfolg (oder Misserfolg) des Vorgangs auf dem Bildschirm angezeigt werden.

    Test-CsComputer -Verbose

## BEISPIEL 2

Im zweiten Beispiel wird ebenfalls der Dienstaktivierungsstatus des lokalen Computers überprüft. Darüber hinaus schreibt dieser Befehl ausführliche Informationen zum Aktivierungsstatus in die Datei "C:\\Logs\\Computer.html". Dieses Protokoll wird generiert, wenn Sie den Parameter "Report" verwenden, gefolgt vom vollständigen Pfad zur Protokolldatei, in der die Informationen erfasst werden sollen.

    Test-CsComputer -Verbose -Report C:\Logs\Computer.html

## Detaillierte Beschreibung

Das Cmdlet **Test-CsComputer** ist ein Beispiel für eine synthetische Lync Server-Transaktion. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich ausführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Das Cmdlet **Test-CsComputer**, das nur auf dem lokalen Computer ausgeführt werden kann, überprüft den Status aller Lync Server-Dienste auf diesem Computer. Es prüft außerdem, ob die richtigen Firewallports auf dem Computer geöffnet wurden, und ermittelt, ob die bei der Installation von Lync Server erstellten Active Directory-Gruppen den geeigneten lokalen Gruppen hinzugefügt wurden. Das Cmdlet **Test-CsComputer** überprüft beispielsweise, ob die Active Directory-Gruppe "RTCUniversalUserAdmins" der lokalen Gruppe "Administratoren" hinzugefügt wurde.

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
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, einen Dateipfad für die bei der Ausführung des Cmdlets erstellte Protokolldatei anzugeben. Beispiel: -Report &quot;C:\Logs\Computer.html&quot;. Ist die Datei bereits vorhanden, wird sie bei der Ausführung des Cmdlets überschrieben.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsComputer** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsComputer** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)

