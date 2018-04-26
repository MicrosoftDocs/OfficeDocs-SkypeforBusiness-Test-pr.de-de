---
title: Remove-CsConfigurationStoreLocation
TOCTitle: Remove-CsConfigurationStoreLocation
ms:assetid: 141be225-c6e4-4377-913b-ba61528929d4
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398214(v=OCS.15)
ms:contentKeyID: 49293257
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConfigurationStoreLocation

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt den Active Directory-Dienstverbindungspunkt für den zentralen Verwaltungsspeicher. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsConfigurationStoreLocation [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 entfernt den Active Directory-Dienststeuerungspunkt für den zentralen Verwaltungsspeicher. Zur Wiederherstellung dieses Dienststeuerungspunkts (oder zum Erstellen eines neuen Dienststeuerungspunkts) müssen Sie das Cmdlet **Set-CsConfigurationStoreLocation** ausführen.

    Remove-CsConfigurationStoreLocation

## BEISPIEL 2

In Beispiel 2 wird der Active Directory-Dienststeuerungspunkt für den zentralen Verwaltungsspeicher entfernt. Zusätzlich zum Entfernen des Dienststeuerungspunkts werden mit diesem Befehl Informationen zum erfolgreichen (oder nicht erfolgreichen) Abschluss des Vorgangs in der Protokolldatei "C:\\Logs\\Store\_Location.html" aufgezeichnet. Zur Erstellung dieser Protokolldatei verwendet der Befehl den Parameter "Report", gefolgt vom Pfad der Protokolldatei, in der die Informationen gespeichert werden sollen. Ist die Datei bereits vorhanden, wird der Inhalt beim Ausführen des Befehls überschrieben. Wenn die Datei noch nicht vorhanden ist, wird Sie beim Ausführen des Befehls erstellt.

    Remove-CsConfigurationStoreLocation -Report C:\Logs\Store_Location.html

## Detaillierte Beschreibung

Active Directory-Domänendienste verwendet Dienststeuerungspunkte, mit denen Computer bestimmte Dienste ermitteln können. Wenn Sie beispielsweise Lync Server installieren, wird ein Dienststeuerungspunkt erstellt, der Standortinformationen für den zentralen Verwaltungsspeicher bereitstellt, die zum Verwalten von Lync Server dienen. Computer, die Zugriff auf die Datenbank benötigen, stellen eine Verbindung mit Active Directory her und nutzen die Informationen des Dienststeuerungspunkts bei der Suche nach dem richtigen Computer und der richtigen SQL Server-Instanz.

Wie bereits erwähnt, wird bei der Installation von Lync Server automatisch ein Dienststeuerungspunkt für den zentralen Verwaltungsspeicher erstellt. In der Regel sollte dieser Dienststeuerungspunkt nicht gelöscht werden, da Computer andernfalls nicht in der Lage sind, die Datenbank zu ermitteln. Gelegentlich (z. B. bei der Problembehandlung) muss jedoch der Dienststeuerungspunkt gelöscht werden. Hierzu verwenden Sie das Cmdlet **Remove-CsConfigurationStoreLocation**. Nachdem der Dienststeuerungspunkt gelöscht wurde, können Sie den Dienststeuerungspunkt mit dem Cmdlet **Set-CsConfigurationStoreLocation** wiederherstellen (oder einen neuen Dienststeuerungspunkt erstellen).

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsConfigurationStoreLocation** lokal ausführen: RTCUniversalServerAdmins.

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) eines Domänencontrollers, auf dem globale Einstellungen gespeichert sind. Wenn die globalen Einstellungen im Active Directory-Systemcontainer gespeichert sind, muss dieser Parameter auf den Stammdomänencontroller verweisen. Wenn die globalen Einstellungen im Konfigurationscontainer gespeichert sind, kann jeder Domänencontroller verwendet werden, und dieser Parameter kann ausgelassen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, einen Dateipfad für die bei der Ausführung des Cmdlets erstellte Protokolldatei anzugeben. Beispiel: -Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Remove-CsConfigurationStoreLocation** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Remove-CsConfigurationStoreLocation** gibt keine Objekte oder Werte zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

