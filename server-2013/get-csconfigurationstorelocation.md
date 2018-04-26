---
title: Get-CsConfigurationStoreLocation
TOCTitle: Get-CsConfigurationStoreLocation
ms:assetid: abfda147-02fa-46a5-a988-d83daf4cc455
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412814(v=OCS.15)
ms:contentKeyID: 49295061
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConfigurationStoreLocation

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt den Standort des Active Directory-Dienstverbindungspunkts für den zentralen Verwaltungsspeicher zurück. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsConfigurationStoreLocation [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 gibt den SQL Server-Pfad zum Computer (oder Pool) zurück, der den zentralen Verwaltungsspeicher hostet.

    Get-CsConfigurationStoreLocation

## BEISPIEL 2

Beispiel 2 ist eine Variante des Befehls aus Beispiel 1. In diesem Fall wird jedoch der Parameter "Report" zur Angabe eines Dateipfads für den Bericht verwendet, der beim Ausführen des Cmdlets **Get-CsConfigurationStoreLocation** generiert wird.

    Get-CsConfigurationStoreLocation -Report "C:\Logs\ConfigurationStore.html"

## Detaillierte Beschreibung

Active Directory-Domänendienste verwendet Dienstverbindungspunkte, mit denen Computer bestimmte Dienste ermitteln können. Wenn Sie beispielsweise Lync Server installieren, wird ein Dienstverbindungspunkt erstellt, der Standortinformationen für den zentralen Verwaltungsspeicher bereitstellt, die zum Verwalten von Lync Server-Daten dienen. Computer, die Zugriff auf die Datenbank benötigen, stellen eine Verbindung mit Active Directory her und nutzen die Informationen des Dienstverbindungspunkts bei der Suche nach dem richtigen Computer und der richtigen SQL Server-Instanz.

Mit dem Cmdlet **Get-CsConfigurationStoreLocation** wird der SQL Server-Pfad (z. B. "atl-sql-001.litwareinc.com/rtc) zum Computer zurückgegeben, auf dem Sie den zentralen Verwaltungsspeicher ausführen.

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
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsConfigurationStoreLocation** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Zeichenfolge. Das Cmdlet **Get-CsConfigurationStoreLocation** gibt den Standort des Konfigurationsspeichers zurück.

## Siehe auch

#### Weitere Ressourcen

[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

