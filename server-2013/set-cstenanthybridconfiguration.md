---
title: Set-CsTenantHybridConfiguration
TOCTitle: Set-CsTenantHybridConfiguration
ms:assetid: 805ac9ee-df40-40e1-baaa-adffb6bd8cf6
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994046(v=OCS.15)
ms:contentKeyID: 52056372
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantHybridConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Wird in einem Hybridszenario verwendet, um Benutzern, deren Konten in Microsoft Lync Online gehostet werden, den Zugriff auf lokale Enterprise-VoIP-Features wie Medienumgehung, erweiterte Notfalldienste (Enhanced 9-1-1, E9-1-1-) und Parken von Anrufen zu ermöglichen. Ein Hybridszenario (auch als Szenario mit geteilter Domäne bezeichnet) ist eine Lync Server-Bereitstellung, in der einige Benutzer über lokale Konten und andere Benutzer über Konten in Lync Online verfügen.

Dieses Cmdlet kann nur in Verbindung mit Skype for Business Online verwendet werden.

## Syntax

    Set-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-PeerDestination <string>] [-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]Set-CsTenantHybridConfiguration [-Tenant <guid>] [-PeerDestination <string>][-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Instance <psobject>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 legt die interne Dienst-URL für die globale Auflistung der Hybridkonfigurationseinstellungen des Mandanten fest. Schließen Sie zum Konfigurieren einer globalen Einstellung den Parameter **Identity** mit dem Parameterwert "global" ein.

    Set-CsTenantHybridConfiguration -Identity "global" - HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Beispiel 2

In Beispiel 2 wird die interne Dienst-URL für einen bestimmten Mandanten konfiguriert. In diesem Beispiel hat der Mandant die Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354". Wenn ein Eigenschaftswert explizit einem einzelnen Mandanten zugewiesen wird, gelten für den Mandanten die individuellen Hybridkonfigurationseinstellungen des Mandanten und nicht die globalen Einstellungen.

    Set-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## Beispiel 3

Mit dem in Beispiel 3 gezeigten Befehl wird die interne Dienst-URL für alle Mandanten Ihrer Organisation konfiguriert. Hierfür verwendet der Befehl erst das Cmdlet **Get-CsTenant**, um ein Auflistung aller verfügbaren Mandanten zurückzugeben. Diese Auflistung wird dann an das Cmdlet **ForEach-Object** weitergeleitet. Im nächsten Schritt führt das Cmdlet **ForEach-Object** das Cmdlet **Set-CsTenantHybridConfiguration** für jeden Mandanten in der Auflistung aus und legt die interne Dienst-URL für jeden der Mandanten auf "https://internal.litwareinc.com" fest.

    Get-CsTenant | ForEach-Object {Set-CsTenantHybridConfiguration -Tenant $_.TenantID -HybridConfigServiceInternalUrl "https://internal.litwareinc.com"}

## Detaillierte Beschreibung

In einer Hybridbereitstellung oder einer Bereitstellung mit geteilten Domänen gibt es in einer Organisation einige Benutzer mit Konten in Lync Online und gleichzeitig andere mit Konten in Lync Server. Standardmäßig können Benutzer, deren Konten in Lync Online gehostet werden, nicht auf die gesamte Palette der von Enterprise-VoIP gebotenen Funktionen zugreifen, weil die Lync Online-Server keinen direkten Zugriff auf die lokale Lync Server-Bereitstellung und die Netzwerkkonfigurationsinformationen haben. Unter anderem können Lync Online-Benutzer nicht standardmäßig auf Features wie die folgenden zugreifen:

  - "Enhanced 9-1-1", den Lync Server-Dienst für erweiterte Notfalldienst

  - "Anrufe parken", den Lync Server-Dienst, der es Benutzern ermöglicht, einen Anruf auf Telefon A in die Warteschleife zu setzen, während sie einen Anruf auf Telefon B annehmen

  - Medienumgehung, eine Funktion, die es ermöglicht, dass Anrufe in und aus dem öffentlichen Telefonnetz (PSTN) den Vermittlungsserver umgehen, was dazu beiträgt, den Transcodierungsaufwand und die Netzwerklatenz minimal zu halten.

  - Eingehende und ausgehende Anrufe über das PSTN während einer Konferenz, wodurch Benutzer in der Lage sind, mit einem PSTN-Telefon oder einem mobilen Gerät am Audioteil einer Konferenz teilzunehmen.

  - Die Reaktionsgruppenanwendung, die eine Möglichkeit bietet, Telefonanrufe automatisch an Entitäten wie einen Helpdesk oder den Kundensupport weiterzuleiten. Standardmäßig können Lync Online-Benutzer nicht als Reaktionsgruppen-Agents fungieren.

Um den Lync Online-Benutzer den Zugriff auf diese Enterprise-VoIP-Features zu ermöglichen, muss der Administrator in den Hybridkonfigurationseinstellungen die geeigneten Werte wie die internen und externen Webdienst-URLs und den vollständig qualifizierten Domänennamen des Zugriffs-Edgeservers der Organisation zuweisen. Mit diesen Werten, die nur mit dem Cmdlet **Set-CsTenantHybridConfiguration** konfiguriert werden können, erhalten die Lync Online-Server die Informationen, die notwendig sind, damit diese erweiterten Enterprise-VoIP-Features genutzt werden können.

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
<td><p></p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>HybridConfigServiceExternalUrl</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Externe Webdienst-URL</p></td>
</tr>
<tr class="even">
<td><p><em>HybridConfigServiceInternalUrl</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Interne Webdienst-URL</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutige Identität der Hybridkonfigurationseinstellungen des Mandanten, die geändert werden sollen. Da Sie auf eine einzige, globale Auflistung von Hybridkonfigurationseinstellungen beschränkt sind, ist die einzige Auflistung, die mit dem Parameter <strong>Identity</strong> geändert werden kann, die globale Auflistung:</p>
<p>-Identity global</p>
<p>Zum Ändern der Einstellungen für einen einzelnen Mandanten verwenden Sie den Parameter <strong>Tenant</strong> anstelle des Parameters <strong>Identity</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen.</p></td>
</tr>
<tr class="odd">
<td><p><em>PeerDestination</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Vollständig qualifizierter Domänenname des lokalen Zugriffs-Edgeservers.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Mandantenkontos, dessen Hybridkonfigurationseinstellungen geändert werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Wenn Sie Windows PowerShell in einer Remotesitzung verwenden und nur mit Skype for Business Online verbunden sind, müssen Sie den Parameter <strong>Tenant</strong> nicht angeben. Stattdessen wird die Mandanten-ID automatisch basierend auf Ihren Verbindungsinformationen eingegeben. Der Parameter <strong>Tenant</strong> wird in erster Linie in Hybridbereitstellungen verwendet.</p></td>
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

Keine. Das Cmdlet **Set-CsTenantHybridConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet **Set-CsTenantHybridConfiguration** vorhandene Instanzen des Objekts **Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration** geändert.

## Siehe auch

#### Weitere Ressourcen

[Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

