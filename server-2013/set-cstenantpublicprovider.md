---
title: Set-CsTenantPublicProvider
TOCTitle: Set-CsTenantPublicProvider
ms:assetid: 8341d801-bfa1-4c5b-9b80-5d503deebaf7
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994047(v=OCS.15)
ms:contentKeyID: 52056393
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantPublicProvider

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Aktiviert und deaktiviert die Kommunikation mit den Drittanbieter-Chat- und -Anwesenheitsanbietern Windows Live, AOL und Yahoo. Bei Aktivierung können Microsoft Lync Online-Benutzer Chatnachrichten und Anwesenheitsinformationen mit Benutzern austauschen, die über Konten beim angegebenen öffentlichen Anbieter verfügen.

Das Cmdlet **Set-CsTenantPublicProvider** kann nur mit Skype for Business Online verwendet werden.

## Syntax

    Set-CsTenantPublicProvider -Tenant <String> [-Provider <String[]>] [-Verbose] [-WhatIf] [-Confirm]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 aktiviert den Partnerverbund mit Windows Live für den Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354". Da Windows Live der einzige angegebene Anbieter ist, werden die Anbieter AOL und Yahoo nach Ausführung des Befehls deaktiviert.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

## Beispiel 2

In Beispiel 2 werden zwei öffentliche Anbieter aktiviert: Windows Live und AOL. Das bedeutet, dass nur der öffentliche Anbieter Yahoo für den angegebenen Mandanten deaktiviert wird.

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive","AOL"

## Beispiel 3

Beispiel 3 zeigt, wie Sie alle öffentlichen Anbieter für einen bestimmten Mandanten deaktivieren können. Dafür legen Sie die Eigenschaft "Provider" auf eine leere Zeichenfolge fest ("").

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

## Beispiel 4

Der Befehl in Beispiel 4 deaktiviert alle öffentlichen Anbieter für Ihre sämtlichen Lync Online-Mandanten. Zum Ausführen dieser Aufgabe verwendet der Befehl zunächst das Cmdlet **Get-CsTenant**, um eine Auflistung aller Mandanten zurückzugeben. Diese Auflistung wird dann an das Cmdlet **ForEach-Object** weitergeleitet, das jeden Mandanten in der Auflistung nimmt, das Cmdlet **Set-CsTenantPublicProvider** erneut für diese Mandanten aufruft und alle öffentlichen Anbieter deaktiviert. Die letzte Aufgabe wird ausgeführt, indem die Eigenschaft "Provider" auf eine leere Zeichenfolge festgelegt wird ("").

    Get-CsTenant | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider ""}

## Detaillierte Beschreibung

Öffentliche Anbieter sind Organisationen, die SIP-Kommunikationsdienste für die breite Öffentlichkeit bieten. Wenn Sie eine Partnerverbundbeziehung mit einem öffentlichen Anbieter einrichten, stellen Sie im Prinzip einen Partnerverbund mit allen Benutzern her, deren Konto von diesem Anbieter gehostet wird. Bei einem Partnerverbund mit Windows Live können Benutzer beispielsweise Chatnachrichten und Anwesenheitsinformationen mit allen anderen Benutzern austauschen, die über ein Windows Live-Chatkonto verfügen.

Mit Lync Online können Administratoren einen Partnerverbund mit einem oder mehreren der folgenden öffentlichen Chat- und Anwesenheitsanbieter konfigurieren:

  - Windows Live

  - AOL

  - Yahoo\!

Mit dem Cmdlet **Set-CsTenantPublicProvider** kann der Partnerverbund mit jedem dieser öffentlichen Anbieter aktiviert oder deaktiviert werden. Denken Sie bei der Verwendung dieses Cmdlets daran, dass Sie bei jeder Ausführung des Cmdlets **Set-CsTenantPublicProvider** alle Anbieter angeben müssen, die aktiviert werden sollten. Nehmen wir beispielsweise an, dass alle drei Anbieter deaktiviert sind und Sie den folgenden Befehl ausführen:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

Erwartungsgemäß wird damit Windows Live aktiviert, während AOL und Yahoo deaktiviert bleiben.

Nehmen wir jetzt an, Sie führen anschließend den folgenden Befehl aus:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL"

Dieser Befehl aktiviert AOL. Er deaktiviert jedoch gleichzeitig Windows Live, da Windows Live nicht als Teil des an den Parameter "Provider" übergebenen Parameterwerts angegeben wurde. Wenn Sie AOL aktivieren möchten und auch Windows Live aktiviert bleiben soll, müssen Sie beim Aufrufen von "Set-CsTenantPublicProvider" sowohl AOL als auch Windows Live angeben:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Zum Deaktivieren des Partnerverbunds für alle drei Anbieter legen Sie die Eigenschaft "Provider" auf eine leere Zeichenfolge fest (""):

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider ""

Beachten Sie, dass das reine Aktivieren des Status eines öffentlichen Anbieters nicht bedeutet, dass Benutzer Chatnachrichten und Anwesenheitsinformationen mit Benutzern austauschen können, die über ein Konto bei diesem Anbieter verfügen. Neben der Aktivierung des Partnerverbunds mit dem Anbieter selbst müssen Administratoren auch die Eigenschaft "AllowPublicUsers" der Konfigurationseinstellungen für den Partnerverbund auf "True" festlegen. Wenn diese Eigenschaft auf "False" festgelegt ist, ist keine Kommunikation mit den öffentlichen Anbietern zulässig, unabhängig von den Konfigurationseinstellungen für öffentliche Anbieter.

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
<td><p><em>Tenant</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Mandantenkontos, dessen Einstellungen für öffentliche Anbieter geändert werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie den folgenden Befehl ausführen:</p>
<pre><code>Get-CsTenant | Select-Object DisplayName, TenantID</code></pre>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String[]</p></td>
<td><p>Gibt die öffentlichen Anbieter an, mit denen Benutzer kommunizieren dürfen. Gültige Werte:</p>
<p>* AOL</p>
<p>* WindowsLive</p>
<p>* Yahoo</p>
<p>Beachten Sie, dass bei der Konfiguration öffentlicher Anbieter jeder im Parameterwert &quot;Provider&quot; enthaltene Anbieter zur Verwendung aktiviert und jeder nicht im Parameterwert enthaltene Anbieter deaktiviert wird. Mit der folgenden Syntax wird beispielweise nur Yahoo aktiviert, während Windows Live und AOL deaktiviert werden:</p>
<p>-Provider &quot;AOL&quot;</p>
<p>Sie können mehrere Anbieter aktivieren, indem Sie die Anbieternamen durch Kommas trennen:</p>
<p>-Provider &quot;AOL&quot;,&quot;WindowsLive&quot;</p></td>
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

Das Cmdlet **Set-CsTenantPublicProvider** akzeptiert weitergeleitete Instanzen des Objekts "Microsoft.Rtc.Management.Hosted.TenantPICStatus".

## Rückgabetypen

Keine. Stattdessen ändert das Cmdlet **Set-CsTenantPublicProvider** vorhandene Instanzen des Objekts "Microsoft.Rtc.Management.Hosted.TenantPICStatus".

## Siehe auch

#### Weitere Ressourcen

[Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

