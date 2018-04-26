---
title: Update-CsTenantMeetingUrl
TOCTitle: Update-CsTenantMeetingUrl
ms:assetid: 9aed3ede-bbd3-405a-997f-f7553e66aecd
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn424754(v=OCS.15)
ms:contentKeyID: 59373611
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsTenantMeetingUrl

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Aktualisiert die Besprechungs-URL für den angegebenen Skype for Business Online-Mandanten. Die aktualisierte URL verwendet ein einfacheres, eher dem Standard entsprechendes Format, wodurch es für Kunden einfacher wird, Besprechungen zu finden und die Verbindung hierzu herzustellen.

Diese Cmdlet ist nur für die Verwendung mit Skype for Business Online vorgesehen.

## Syntax

    Update-CsTenantMeetingUrl [-Tenant] <guid> [-Force] [-WhatIf] [-Confirm]

## Beispiele

## Beispiel 1

Mit dem Befehl im ersten Beispiel wird die Besprechungs-URL des Mandanten mit der Mandanten-ID "38aad667-af54-4397-aaa7-e94c79ec2308" aktualisiert. (Beachten Sie, dass Sie die Mandanten-ID angeben müssen, damit dieser Befehl ausgeführt werden kann.) Nachdem Sie die EINGABETASTE gedrückt haben, um den Befehl auszuführen, werden Sie aufgefordert zu bestätigen, dass Sie die Besprechungs-URL aktualisieren möchten. Sie müssen in der Bestätigung auf **Ja** klicken, damit **Update-CsTenantMeetingUrl** die Änderungen in Ihren Skype for Business Online-Konfigurationseinstellungen vornimmt.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308"

## Beispiel 2

Mit dem Befehl im zweiten Beispiel wird ebenfalls die Besprechungs-URL des Mandanten mit der Mandanten-ID "38aad667-af54-4397-aaa7-e94c79ec2308" aktualisiert. In diesem Fall wird jedoch der Parameter **Force** verwendet. Damit wird die Bestätigungsaufforderung umgangen, die normalerweise angezeigt wird, wenn Sie **Update-CsTenantMeetingUrl** ausführen. In diesem Fall wird der Befehl sofort nach dem Drücken der EINGABETASTE ausgeführt, und Ihre Skype for Business Online-Konfigurationseinstellungen werden geändert.

    Update-CsTenantMeetingUrl -Tenant "38aad667-af54-4397-aaa7-e94c79ec2308" -Force

## Detaillierte Beschreibung

Mit dem Cmdlet **Update-CsTenantMeetingUrl** wird die Skype for Business Online-Besprechungs-URL auf ein einfacheres und eher dem Standard entsprechendes Format aktualisiert. Damit erübrigen sich Probleme, die gelegentlich mit der ursprünglichen Besprechungs-URL aufgetreten sind. Nehmen wir beispielsweise an, eine Organisation richtet eine Office 365-Domäne mit dem Namen "contoso.onmicrosoft.com" ein. In diesem Fall ergeben sich Besprechungs-URLs wie die folgenden:

https://meet.lync.com/onmicrosoft/contoso/user1/45GZFH99

Nehmen wir nun weiter an, dass es in der Organisation einige Änderungen gibt und dass entschieden wird, die anstelle der URL "onmicrosoft.com" nun die "Vanity"-URL "litwareinc.com" zu verwenden. Die E-Mail-Adressen der Benutzer in der Organisation werden dahingehend geändert, dass die Domäne "litwareinc.com" verwendet wird, in den Besprechungs-URLs wird jedoch weiterhin der alte Domänenname verwendet:

https://meet.lync.com/contoso/user1/45GZFH99

Um dieses Probleme zu beheben, sollte der Administrator des Cmdlet **Update-CsTenantMeetingUrl** verwendet. Hiermit wird die alte Besprechungs-URL durch die neue ersetzt, in der nun die "Vanity"-URL verwendet wird:

https://meet.lync.com/litwareinc.com/user1/37JYLP71

Diese Änderung kann nur mit dem Cmdlet **Update-CsTenantMeetingUrl** durchgeführt werden.

Wenn Sie das Cmdlet Update-CsTenantMeetingUrl ausführen, wird der Skype for Business Online-Mandant nach einer kurzen Synchronisierungsverzögerung auf die neue URL umgestellt. Hierdurch ergeben sich bei neuen Besprechungen, die die Benutzer ansetzen, keine Problem. Bei Besprechungen, die zuvor geplant wurden, gibt es jedoch Probleme, die diese mit der alten, nun nicht mehr funktionierenden Besprechungs-URL angesetzt wurden. Die einzige Möglichkeit zur Lösung dieses Problems besteht darin, die Benutzer zu veranlassen, diese Besprechungen erneut anzusetzen.

Aufgrund der Tatsache, dass dies in einigen Organisationen potenziell zu Problemen führt (besonders in Organisationen, in denen bereits zahlreiche Besprechungen geplant sind), gibt das Cmdlet **Update-CsTenantMeetingUrl** standardmäßig eine Warnung aus, bevor die Besprechungs-URL tatsächlich aktualisiert wird:

WARNUNG: Diese Änderung kann für die Benutzer dieses Mandanten die Lauffähigkeit der Anwendung beeinträchtigen. Die Konfiguration der Besprechungs-URL wird aktualisiert\! Alte Besprechungs-URLs funktionieren dann nicht mehr. Diese Änderung kann nicht rückgängig gemacht werden.  
Möchten Sie den Vorgang wirklich fortsetzen?  
\[J\] Ja \[A\] Ja, alle \[N\] Nein \[L\] Alle beibehalten \[H\] Anhalten \[?\] Hilfe (Standardwert ist "J"):

Sie müssen auf **Ja** oder **Ja, alle** klicken, damit der Befehl ausgeführt wird. Wenn Sie auf **Nein** klicken, wird der Befehl abgebrochen, und die Besprechungs-URL wird nicht aktualisiert. Denken Sie daran, dass eine einmal geänderte Besprechungs-URL nicht wieder auf die ursprüngliche URL zurückgesetzt werden kann. Mit der Ausführung des Befehls wird die Besprechungs-URL geändert, und alle zuvor geplanten Besprechungen müssen erneut geplant werden. Dies bedeutet zudem, dass Sie den Befehl nur einmal pro Mandant ausführen müssen. Es ist nicht notwendig, die Befehl regelmäßig auszuführen und die Besprechungs-URL erneut zu aktualisieren.

Wenn Sie es vorziehen, den Befehl ohne Bestätigungsaufforderung auszuführen, können Sie den Parameter **Force** einschließen. In diesem Fall wird **Update-CsTenantMeetingUrl** ausgeführt, ohne dass Sie zur Bestätigung aufgefordert werden:

WARNUNG: Diese Änderung kann für die Benutzer dieses Mandanten die Lauffähigkeit der Anwendung beeinträchtigen. Die Konfiguration der Besprechungs-URL wird aktualisiert\!

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
<td><p><strong>Mandant</strong></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Mandantenkontos, dessen Partnerverbundeinstellungen zurückgegeben werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Wenn Sie den Parameter <strong>Tenant</strong> nicht eingeben, fordert das Cmdlet <strong>Update-CsMeetingUrl</strong> Sie zur Eingabe dieses Parameters auf, bevor Sie fortfahren können.</p></td>
</tr>
<tr class="even">
<td><p><strong>Confirm</strong></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p>
<p>Beachten Sie, dass bei der Ausführung von <strong>Update-CsMeetingUrl</strong> standardmäßig eine Bestätigungsaufforderung angezeigt wird, bevor irgendwelche Aktualisierungen erfolgen. Dies bedeutet, dass Sie den Parameter <strong>Confirm</strong> nicht einschließen müssen, um eine Bestätigungsaufforderung zu erhalten.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Force</strong></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige der Bestätigungsaufforderung, die ansonsten angezeigt würde, bevor mit <strong>Update-CsMeetingUrl</strong> eine Aktualisierung erfolgt.</p></td>
</tr>
<tr class="even">
<td><p><strong>WhatIf</strong></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. **Update-CsMeetingUrl** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Keine.

## Siehe auch

#### Weitere Ressourcen

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

