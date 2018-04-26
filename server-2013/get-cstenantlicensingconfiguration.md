---
title: Get-CsTenantLicensingConfiguration
TOCTitle: Get-CsTenantLicensingConfiguration
ms:assetid: 0df23143-f1aa-4850-b0f7-750422762925
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362770(v=OCS.15)
ms:contentKeyID: 56269252
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantLicensingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt an, ob Lizenzinformationen für den angegebenen Mandaten im Lync-Admin Center verfügbar sind.

Dieses Cmdlet kann nur in Verbindung mit Lync Online verwendet werden.

## Syntax

    Get-CsTenantLicensingConfiguration [-Filter] <Object>] [-Identity] <Object>] [-Tenant] <Object>] [-LocalStore]

## Detaillierte Beschreibung

Das Cmdlet **Get-CsTenantLicensingConfiguration** gibt an, ob Lizenzinformationen für den angegebenen Mandaten im Lync-Admin Center verfügbar sind. Das Cmdlet gibt Informationen wie die folgenden zurück:

Identity : Global  
Status : Enabled

Wenn **Status** gleich **Enabled** ist, sind im Lync-Admin Center Lizenzinformationen verfügbar. Andernfalls sind im Lync-Admin Center keine Lizenzinformationen verfügbar.

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
<td><p><strong>Filter</strong></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht die Verwendung von Platzhalterzeichen, um eine Auflistung der Konfigurationseinstellungen für die Mandantenlizenzen zurückzugeben. Da jeder Mandant auf eine einzige, globale Auflistung von Lizenzkonfigurationseinstellungen beschränkt ist, ist die Verwendung des Parameters <strong>Filter</strong> nicht erforderlich.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Gibt die Auflistung der Konfigurationseinstellungen der Mandantenlizenz an, die zurückgegeben werden soll. Da jeder Mandant auf eine einzige, globale Auflistung von Lizenzeinstellungen beschränkt ist, muss dieser Parameter beim Aufruf des Cmdlets <strong>Get-CsTenantLicensingConfiguration</strong> nicht angegeben werden.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalStore</strong></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Konfigurationsdaten der Mandantenlizenz aus dem lokalen Replikat des zentralen Verwaltungsspeichers statt aus dem zentralen Verwaltungsspeicher selbst ab.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tenant</strong></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Mandantenkontos, dessen Lizenzeinstellungen zurückgegeben werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Das Cmdlet **Get-CsTenantLicensingConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Get-CsTenantLicensingConfiguration** gibt Instanzen des Objekts **Deserialized.Microsoft.Rtc.Management.WritableConfig.Settings.TenantConfiguration.TenantLicensingConfiguration** zurück.

## Beispiel

Mit dem Befehl in Beispiel 1 werden Lizenzkonfigurationsinformationen für den aktuellen Mandanten zurückgegeben:

    Get-CsTenantLicensingConfiguration

