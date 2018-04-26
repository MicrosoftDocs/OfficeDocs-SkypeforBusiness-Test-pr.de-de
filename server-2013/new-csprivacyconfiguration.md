---
title: New-CsPrivacyConfiguration
TOCTitle: New-CsPrivacyConfiguration
ms:assetid: 9b7f02d7-93a5-4fa5-a74c-3fe4baf8bbfc
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398807(v=OCS.15)
ms:contentKeyID: 49294877
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPrivacyConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt eine neue Auflistung von Datenschutzkonfigurationseinstellungen. Datenschutzkonfigurationseinstellungen sind hilfreich, um zu bestimmen, wie viele Informationen Benutzer anderen Benutzern zur Verfügung stellen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsPrivacyConfiguration -Identity <XdsIdentity> [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 erstellt eine neue Auflistung von Datenschutzkonfigurationseinstellungen, die auf den Standort "Redmond" (-Identity site:Redmond) angewendet wird. Mit den neuen Einstellungen wird der Datenschutzmodus aktiviert, indem der Parameter "EnablePrivacyMode" hinzugefügt und der Parameterwert auf "True" festgelegt wird. Beachten Sie, dass bei diesem Befehl ein Fehler auftritt, wenn der Standort "Redmond" bereits über eine Auflistung von Datenschutzeinstellungen verfügt.

    New-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $True

## BEISPIEL 2

In Beispiel 2 wird gezeigt, wie Sie den Parameter "InMemory" zum Erstellen einer neuen Auflistung von Datenschutzkonfigurationseinstellungen verwenden können, die zunächst nur im Arbeitsspeicher vorhanden sind. Dazu wird das Cmdlet **New-CsPrivacyConfiguration** mit den Parametern "Identity" und "InMemory" aufgerufen. Das resultierende Objekt wird in der Variablen "$x" gespeichert. Die Datenschutzeinstellungen sind zu diesem Zeitpunkt nur im Arbeitsspeicher vorhanden. Wenn Sie das Cmdlet **Get-CsPrivacyConfiguration** ausführen, wird für "site:Redmond" keine Auflistung angezeigt.

Beim zweiten Befehl wird der Wert der Eigenschaft "EnablePrivacyMode" auf "True" festgelegt. Der dritte Befehl verwendet schließlich das Cmdlet **Set-CsPrivacyConfiguration**, um die virtuelle Auflistung von Datenschutzeinstellungen in eine tatsächliche Auflistung von Einstellungen umzuwandeln, die auf den Standort "Redmond" angewendet wird. Das Aufrufen des Cmdlets **Set-CsPrivacyConfiguration** ist äußerst wichtig: Wenn dieses Cmdlet nicht aufgerufen wird, werden Ihre neuen Datenschutzeinstellungen nicht auf den Standort "Redmond" angewendet und gehen verloren, wenn Sie Ihre Windows PowerShell-Sitzung beenden oder die Variable "$x" löschen.

    $x = New-CsPrivacyConfiguration -Identity site:Redmond -InMemory
    $x.EnablePrivacyMode = $True
    Set-CsPrivacyConfiguration -Instance $x

## Detaillierte Beschreibung

Benutzer können mit Lync Server eine Vielzahl von Anwesenheitsinformationen mit anderen Benutzern austauschen: Sie können ein Foto von sich veröffentlichen, ausführliche Standortinformationen bereitstellen und Anwesenheitsinformationen jeder Person in der Organisation (nicht nur Personen in ihrer Kontaktliste) zur Verfügung stellen.

Einige Benutzer begrüßen die Möglichkeit, ihren Kollegen diese Informationen zur Verfügung zu stellen, andere Benutzer hingegen möchten diese Daten nicht freigeben. (Viele Personen möchten z. B. nicht, dass die Anwesenheitsinformationen ihr Foto enthalten.) In der Regel können Benutzer steuern, welche Informationen freigegeben (oder nicht freigegeben) werden. Benutzer können z. B. ein Kontrollkästchen aktivieren oder deaktivieren, um zu steuern, ob ihre Standortinformationen für andere Benutzer freigegeben werden. Zusätzlich können Administratoren mit den Cmdlets für die Datenschutzkonfiguration Datenschutzeinstellungen für ihre Benutzer verwalten. Administratoren können in einigen Fällen Einstellungen aktivieren oder deaktivieren. Wenn beispielsweise die Eigenschaft "AutoInitiateContacts" auf "True" festgelegt wird, werden Teammitglieder automatisch der Liste "Kontakte" der einzelnen Benutzer hinzugefügt. Wenn die Eigenschaft auf "False" festgelegt wird, werden Teammitglieder nicht automatisch der Liste "Kontakte" der einzelnen Benutzer hinzugefügt.

In anderen Fällen können Administratoren die Standardwerte in Lync konfigurieren und Benutzern dennoch das Recht erteilen, diese Werte zu ändern. Die Standortdaten werden z. B. standardmäßig für Benutzer veröffentlicht, auch wenn Benutzer berechtigt sind, die Veröffentlichung des Standorts zu verhindern. Administratoren können dieses Verhalten ändern, indem sie die Eigenschaft "PublishLocationDataByDefault" auf "False" festlegen: In diesem Fall werden die Standortdaten standardmäßig nicht veröffentlicht, auch wenn Benutzer weiterhin berechtigt sind, diese Daten bei Bedarf zu veröffentlichen.

Datenschutzkonfigurationseinstellungen können global, auf Standortebene und auf Dienstebene (mit Ausnahme des Benutzerserverdiensts) angewendet werden. Mit dem Cmdlet **New-CsPrivacyConfiguration** können Sie neue Datenschutzkonfigurationseinstellungen erstellen, die auf einen Standort oder Dienst angewendet werden sollen. (Neue Auflistungen können nicht global erstellt werden.) Beachten Sie, dass jeder einzelne Standort oder Dienst maximal eine Auflistung von Datenschutzkonfigurationseinstellungen aufweisen kann: Wenn Sie versuchen, eine neue Auflistung für den Standort "Redmond" zu erstellen, und es für den Standort "Redmond" bereits eine Auflistung von Datenschutzeinstellungen gibt, tritt beim Befehl ein Fehler auf.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsPrivacyConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPrivacyConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die eindeutige ID für die Datenschutzkonfigurationseinstellungen, die erstellt werden sollen. Verwenden Sie eine Syntax wie die folgende, um eine neue Auflistung von Einstellungen auf Standortebene zu erstellen: -Identity site:Redmond. Verwenden Sie eine Syntax wie die folgende, um neue Einstellungen auf Dienstebene zu erstellen: -Identity service:UserServer:atl-cs-001.litwareinc.com. Datenschutzeinstellungen können nur für den Benutzerserverdienst erstellt werden. Es wird eine Fehlermeldung angezeigt, wenn Sie versuchen, diese Einstellungen auf einen anderen Dienst anzuwenden.</p>
<p>Beachten Sie, dass bei Ihrem Befehl ein Fehler auftritt, wenn für den angegebenen Standort oder Dienst bereits Datenschutzkonfigurationseinstellungen vorhanden sind. Bei Ihrem Befehl tritt ebenfalls ein Fehler auf, wenn Sie versuchen, eine neue Auflistung globaler Einstellungen zu erstellen.</p></td>
</tr>
<tr class="even">
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Wenn &quot;True&quot; festgelegt ist, fügt Lync Ihren Vorgesetzten und Ihre direkt unterstellten Mitarbeiter automatisch Ihrer Liste &quot;Kontakte&quot; hinzu. Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Wenn &quot;True&quot; festgelegt ist, wird das Foto des Benutzers in Lync automatisch veröffentlicht. Wenn &quot;False&quot; festgelegt ist, wird das Foto des Benutzers nicht zur Verfügung gestellt, es sei denn, der Benutzer wählt explizit die Option &quot;Andere Benutzer können mein Foto sehen&quot; aus. Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Falls &quot;True&quot;, haben Benutzer die Möglichkeit, den erweiterten Datenschutzmodus zu aktivieren. Im erweiterten Datenschutzmodus können nur Personen in Ihrer Liste &quot;Kontakte&quot; Ihre Anwesenheitsinformationen anzeigen. Wenn &quot;False&quot; festgelegt ist, stehen Ihre Anwesenheitsinformationen jeder Person in der Organisation zur Verfügung. Der Standardwert lautet &quot;False&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Wenn &quot;True&quot; festgelegt ist, werden die Standortdaten in Lync automatisch veröffentlicht. Wenn &quot;False&quot; festgelegt ist, stehen die Standortdaten nicht zur Verfügung, es sei denn, der Benutzer wählt explizit die Option &quot;Eigenen Standort für Kontakte anzeigen&quot; aus. Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID (Globally Unique Identifier) des Skype for Business Online-Mandantenkontos, für das die neuen Datenschutzkonfigurationseinstellungen erstellt werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für jeden Mandanten zurückgeben, indem Sie folgenden Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Keine. Das Cmdlet **New-CsPrivacyConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **New-CsPrivacyConfiguration** werden neue Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration" erstellt.

## Siehe auch

#### Weitere Ressourcen

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

