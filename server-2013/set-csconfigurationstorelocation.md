---
title: Set-CsConfigurationStoreLocation
TOCTitle: Set-CsConfigurationStoreLocation
ms:assetid: 1c69a872-8e78-4c78-ba27-f20f04dce59f
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398258(v=OCS.15)
ms:contentKeyID: 49293349
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConfigurationStoreLocation

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Legt den Active Directory-Dienstverbindungspunkt für den zentralen Verwaltungsspeicher fest. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsConfigurationStoreLocation -SqlServerFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-MirrorSqlInstanceName <String>] [-MirrorSqlServerFqdn <Fqdn>] [-Report <String>] [-SkipLookup <SwitchParameter>] [-SqlInstanceName <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 legt den Active Directory-Dienststeuerungspunkt für den zentralen Verwaltungsspeicher von Lync Server fest. In diesem Beispiel verweist der Dienststeuerungspunkt auf den Computer "atl-sql-001.litwareinc.com" und die SQL Server-Instanz "Rtc".

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc

## BEISPIEL 2

Der in Beispiel 2 gezeigte Befehl ist eine Variante des Befehls aus Beispiel 1. Dieser Befehl legt ebenfalls den Active Directory-Dienststeuerungspunkt für den zentralen Verwaltungsspeicher von Lync Server fest. Darüber hinaus werden Informationen zum erfolgreichen (oder nicht erfolgreichen) Abschlusses dieses Vorgangs in der Datei "C:\\Store\_Location.html" protokolliert. Dieses Protokoll wird generiert, wenn Sie den Parameter "Report" verwenden, gefolgt vom vollständigen Pfad zur Protokolldatei, in der die Informationen aufgezeichnet werden sollen.

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc -Report C:\Logs\Store_Location.html

## Detaillierte Beschreibung

Active Directory-Domänendienste verwendet Dienststeuerungspunkte, mit denen Computer bestimmte Dienste ermitteln können. Wenn Sie beispielsweise Lync Server installieren, wird ein Dienststeuerungspunkt erstellt, der Standortinformationen für den zentralen Verwaltungsspeicher bereitstellt, die zum Verwalten von Lync Server dienen. Computer, die Zugriff auf die Datenbank benötigen, stellen eine Verbindung mit Active Directory her und nutzen die Informationen des Dienststeuerungspunkts bei der Suche nach dem richtigen Computer und der richtigen SQL Server-Instanz.

Wie bereits erwähnt, wird bei der Installation von Lync Server automatisch ein Dienststeuerungspunkt für den zentralen Verwaltungsspeicher erstellt. Wenn Sie diese Datenbank auf einen anderen Computer oder eine andere SQL Server-Instanz verschieben möchten, müssen Sie den entsprechenden Dienststeuerungspunkt aktualisieren. Dazu können Sie das Cmdlet **Set-CsConfigurationStoreLocation** verwenden. Wenn Sie es ausführen, wird Active Directory mit dem Cmdlet **Set-CsConfigurationStoreLocation** nach dem mit dem Parameter "SqlServer" festgelegten Computer durchsucht. Das Cmdlet legt als Speicherort dann den vollqualifizierten Domänennamen (FQDN) dieses Computers fest.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsConfigurationStoreLocation** lokal ausführen: RTCUniversalServerAdmins.

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
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) des Computers, auf dem zentralen Verwaltungsspeicher installiert wurde. Beispiel: -SqlServer atl-sql-001.litwareinc.com.</p></td>
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
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN eines Domänencontrollers, auf dem die globalen Einstellungen gespeichert sind. Wenn die globalen Einstellungen im Active Directory-Systemcontainer gespeichert sind, muss dieser Parameter auf den Stammdomänencontroller verweisen. Wenn die globalen Einstellungen im Konfigurationscontainer gespeichert sind, kann jeder Domänencontroller verwendet werden, und dieser Parameter kann ausgelassen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorSqlInstanceName</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Name der SQL Server-Instanz mit den Tabellen und Daten der Lync Server-Spiegeldatenbank. Beispiel: -SqlInstanceName &quot;rtc&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorSqlServerFqdn</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Vollqualifizierter Domänenname (Fully Qualified Domain Name, FQDN) des Computers, auf dem die zentralen Verwaltungsspeicher-Spiegeldatenbank installiert wurde. Beispiel: -SqlServer atl-mirror-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, einen Dateipfad für die bei der Ausführung des Cmdlets erstellte Protokolldatei anzugeben. Beispiel: -Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipLookup</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Wenn dieser Parameter angegeben wurde, wird mit dem Cmdlet <strong>Set-CsConfigurationStoreLocation</strong> nicht überprüft, ob der angegebene Computer und die festgelegte SQL Server-Instanz verfügbar sind. Stattdessen wird der Dienststeuerungspunkt geändert.</p>
<p>Wenn dieser Parameter nicht angegeben wurde, müssen sowohl der angegebene Computer als auch die festgelegte SQL Server-Instanz verfügbar sein, bevor der Dienststeuerungspunkt geändert wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Name der SQL Server-Instanz mit den Lync Server-Tabellen und -Daten. Beispiel: -SqlInstanceName &quot;rtc&quot;.</p></td>
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

Keine. Das Cmdlet **Set-CsConfigurationStoreLocation** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Set-CsConfigurationStoreLocation** gibt keine Objekte oder Werte zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

