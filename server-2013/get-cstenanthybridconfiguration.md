---
title: Get-CsTenantHybridConfiguration
TOCTitle: Get-CsTenantHybridConfiguration
ms:assetid: 4b2e6781-8f46-4ba3-be76-3a95460e3132
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994034(v=OCS.15)
ms:contentKeyID: 52056359
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantHybridConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Werte für die Konfigurationseinstellungen zurück, mit denen Benutzer, deren Konten in Microsoft Lync Online verwaltet werden, auf lokale Enterprise-VoIP-Funktionen wie Medienumgehung, erweiterte Notfalldienste (Enhanced 9-1-1) und Parken von Anrufen zugreifen können. Ein Hybridszenario (auch als Szenario mit geteilter Domäne bezeichnet) ist eine Lync Server-Bereitstellung, in der einige Benutzer über lokale Konten und andere Benutzer über Konten in Lync Online verfügen.

Das Cmdlet "Get-CsTenantHybridConfiguration" kann nur mit Skype for Business Online verwendet werden.

## Syntax

    Get-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-LocalStore] [<CommonParameters>]Get-CsTenantHybridConfiguration [-Tenant <guid>] [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 gibt die Eigenschaftswerte für die globale Auflistung der Mandanten-Hybridkonfigurationseinstellungen zurück.

    Get-CsTenantHybridConfiguration -Identity "Global"

## Beispiel 2

In Beispiel 2 werden die Eigenschaftswerte für die benutzerdefinierten Hybridkonfigurationseinstellungen des Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" zurückgegeben.

    Get-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## Beispiel 3

In Beispiel 3 werden Hybridkonfigurationseinstellungen für alle verfügbaren Mandanten zurückgegeben. Dafür ruft der Befehl zunächst das Cmdlet **Get-CsTenant** auf, um eine Auflistung all dieser Mandanten zurückzugeben. Diese Auflistung wird dann an das Cmdlet **ForEach-Object** weitergeleitet, das jeden Mandanten in der Auflistung nimmt und nacheinander zwei Aufgaben durchführt. Erstens druckt das Cmdlet den Active Directory-Anzeigenamen für den Mandanten aus, um sicherzustellen, dass jede Auflistung von Einstellungen problemlos identifiziert werden kann. Danach führt das Cmdlet **ForEach-Object** das Cmdlet **Get-CsTenantHybridConfiguration** aus, um die Mandanten-Hybridkonfigurationseinstellungen für den jeweiligen Mandanten zurückzugeben.

    Get-CsTenant | ForEach-Object {$_.DisplayName; Get-CsTenantHybridConfiguration -Tenant $_.TenantId}

## Detaillierte Beschreibung

In einer Hybridbereitstellung oder einer Bereitstellung mit geteilter Domäne gibt es in einer Organisation einige Benutzer mit Konten in Lync Online und gleichzeitig andere mit Konten in der lokalen Version von Lync Server. Standardmäßig können Benutzer, deren Konten in Lync Online verwaltet werden, nicht auf die gesamte Palette der von Enterprise-VoIP gebotenen Funktionen zugreifen, weil die Lync Online-Server keinen direkten Zugriff auf die Lync Server-Bereitstellung und die Netzwerkkonfigurationsinformationen haben. Unter anderem können Lync Online-Benutzer nicht standardmäßig auf Funktionen wie die folgenden zugreifen:

  - "Enhanced 9-1-1", den Lync Server-Dienst für erweiterte Notfalldienst

  - "Anrufe parken", den Lync Server-Dienst, der es Benutzern ermöglicht, einen Anruf auf Telefon A in die Warteschleife zu setzen, während sie einen Anruf auf Telefon B annehmen

  - Medienumgehung, eine Funktion, die es ermöglicht, dass Anrufe in und aus dem öffentlichen Telefonnetz (PSTN) den Vermittlungsserver umgehen, was dazu beiträgt, den Transcodierungsaufwand und die Netzwerklatenz minimal zu halten.

  - Eingehende und ausgehende Anrufe über das PSTN während einer Konferenz, wodurch Benutzer in der Lage sind, mit einem PSTN-Telefon oder einem mobilen Gerät am Audioteil einer Konferenz teilzunehmen.

  - Die Reaktionsgruppenanwendung, die eine Möglichkeit bietet, Telefonanrufe automatisch an Entitäten wie einen Helpdesk oder den Kundensupport weiterzuleiten. Standardmäßig können Lync Server-Benutzer nicht als Reaktionsgruppen-Agents fungieren.

Um den Lync Online-Benutzer den Zugriff auf diese Enterprise-VoIP-Features zu ermöglichen, muss der Administrator in den Hybridkonfigurationseinstellungen die geeigneten Werte wie die internen und externen Webdienst-URLs und den vollständig qualifizierten Domänennamen des Zugriffs-Edgeservers der Organisation zuweisen. Mit diesen Werten, die nur mit dem Cmdlet **Set-CsTenantHybridConfiguration** konfiguriert werden können, erhalten die Lync Online-Server die Informationen, die notwendig sind, damit diese erweiterten Enterprise-VoIP-Features genutzt werden können.

Sie können Informationen zu den derzeit in Ihrer Organisation verwendeten Mandanten-Hybridkonfigurationseinstellungen mit dem Cmdlet **Get-CsTenantHybridConfiguration** zurückgeben.

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
<td><p>Ermöglicht die Verwendung von Platzhalterzeichen für die Rückgabe einer Auflistung von Mandanten-Hybridkonfigurationseinstellungen. Da Sie auf eine einzige globale Auflistung von Hybridkonfigurationseinstellungen beschränkt sind, muss der Parameter &quot;Filter&quot; nicht verwendet werden. Dennoch ist folgende Syntax für das Cmdlet <strong>Get-CsTenantHybridConfiguration</strong> gültig:</p>
<p>Get-CsTenantHybridConfiguration –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutige Identität der Mandanten-Hybridkonfigurationseinstellungen, die zurückgegeben werden sollen. Da Sie auf eine einzige globale Auflistung von Hybridkonfigurationseinstellungen beschränkt sind, ist die einzige Auflistung, die mit dem Parameter &quot;Identity&quot; geändert werden kann, die globale Auflistung:</p>
<p>-Identity global</p>
<p>Zum Ändern der Einstellungen für einen einzelnen Mandanten verwenden Sie den Parameter <strong>Tenant</strong> anstelle des Parameters <strong>Identity</strong> .</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Daten für die Mandantenhybridkonfiguration aus dem lokalen Replikat des zentralen Verwaltungsspeichers statt aus dem zentralen Verwaltungsspeicher selbst ab.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Mandantenkontos, dessen Hybridkonfigurationseinstellungen zurückgegeben werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Wenn Sie eine Remotesitzung von Windows PowerShell verwenden und nur eine Verbindung mit Skype for Business Online hergestellt haben, müssen Sie den Parameter <strong>Tenant</strong> nicht einfügen. Stattdessen wird die Mandanten-ID automatisch anhand Ihrer Verbindungsinformationen für Sie eingetragen. Der Parameter <strong>Tenant</strong> ist hauptsächlich zur Verwendung in einer Hybridbereitstellung vorgesehen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsTenantHybridConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Get-CsTenantHybridConfiguration** gibt Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration" zurück.

## Siehe auch

#### Weitere Ressourcen

[Set-CsTenantHybridConfiguration](set-cstenanthybridconfiguration.md)

