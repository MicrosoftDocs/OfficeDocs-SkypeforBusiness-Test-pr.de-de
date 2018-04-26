---
title: Remove-CsPrivacyConfiguration
TOCTitle: Remove-CsPrivacyConfiguration
ms:assetid: 32052c51-953d-4278-9425-306245d297ed
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425821(v=OCS.15)
ms:contentKeyID: 49293604
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPrivacyConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt eine vorhandene Auflistung von Datenschutzkonfigurationseinstellungen. Datenschutzkonfigurationseinstellungen sind hilfreich, um zu bestimmen, wie viele Informationen Benutzer anderen Benutzern zur Verfügung stellen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsPrivacyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel werden die Datenschutzkonfigurationseinstellungen zurückgegeben, die dem Standort "Redmond" zugewiesen wurden. Wenn diese Einstellungen gelöscht werden, erben die Benutzer am Standort "Redmond" automatisch die globalen Datenschutzkonfigurationseinstellungen.

    Remove-CsPrivacyConfiguration -Identity site:Redmond

## BEISPIEL 2

In Beispiel 2 werden alle auf Standortebene zugewiesenen Datenschutzkonfigurationseinstellungen gelöscht. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPrivacyConfiguration** mit dem Parameter "Filter" auf. Der Filterwert "site:\*" stellt sicher, dass nur die Einstellungen zurückgegeben werden, deren Identitätswert mit der Zeichenfolge "site" beginnt. Die gefilterte Auflistung wird anschließend an das Cmdlet **Remove-CsPrivacyConfiguration** weitergeleitet, das sämtliche Elemente in der Auflistung löscht.

    Get-CsPrivacyConfiguration -Filter "site:*" | Remove-CsPrivacyConfiguration

## BEISPIEL 3

Der Befehl in Beispiel 3 löscht alle Datenschutzkonfigurationseinstellungen, bei denen der Datenschutzmodus deaktiviert wurde. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPrivacyConfiguration** ohne Parameter auf. Anschließend wird eine Auflistung aller in der Organisation verwendeten Datenschutzkonfigurationseinstellungen zurückgegeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Einstellungen herausfiltert, bei denen die Eigenschaft "EnablePrivacyMode" den Wert "False" aufweist. Diese gefilterte Auflistung wird dann an das Cmdlet **Remove-CsPrivacyConfiguration** weitergeleitet, das alle Elemente in der Auflistung löscht.

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Remove-CsPrivacyConfiguration

## Detaillierte Beschreibung

Benutzer können mit Lync Server eine Vielzahl von Anwesenheitsinformationen mit anderen Benutzern austauschen: Sie können ein Foto von sich veröffentlichen, ausführliche Standortinformationen bereitstellen und Anwesenheitsinformationen jeder Person in der Organisation (nicht nur Personen in ihrer Kontaktliste) zur Verfügung stellen.

Einige Benutzer begrüßen die Möglichkeit, ihren Kollegen diese Informationen zur Verfügung zu stellen, andere Benutzer hingegen möchten diese Daten nicht freigeben. (Viele Personen möchten z. B. nicht, dass die Anwesenheitsinformationen ihr Foto enthalten.) In der Regel können Benutzer steuern, welche Informationen freigegeben (oder nicht freigegeben) werden. Benutzer können z. B. ein Kontrollkästchen aktivieren oder deaktivieren, um zu steuern, ob ihre Standortinformationen für andere Benutzer freigegeben werden. Zusätzlich können Administratoren mit den Cmdlets für die Datenschutzkonfiguration Datenschutzeinstellungen für ihre Benutzer verwalten. In einigen Fällen können Administratoren Einstellungen aktivieren oder deaktivieren. Wenn beispielsweise die Eigenschaft "AutoInitiateContacts" auf "True" festgelegt wird, werden Teammitglieder automatisch den Kontaktlisten der einzelnen Benutzer hinzugefügt. Wenn die Eigenschaft auf "False" festgelegt wird, werden Teammitglieder nicht automatisch den Kontaktlisten der einzelnen Benutzer hinzugefügt.

In anderen Fällen können Administratoren die Standardwerte in Lync Server konfigurieren und Benutzern dennoch das Recht erteilen, diese Werte zu ändern. Die Standortdaten werden z. B. standardmäßig für Benutzer veröffentlicht, auch wenn Benutzer berechtigt sind, die Veröffentlichung des Standorts zu verhindern. Administratoren können dieses Verhalten ändern, indem sie die Eigenschaft "PublishLocationDataByDefault" auf "False" festlegen: In diesem Fall werden die Standortdaten standardmäßig nicht veröffentlicht, auch wenn Benutzer weiterhin berechtigt sind, diese Daten bei Bedarf zu veröffentlichen.

Datenschutzkonfigurationseinstellungen können global, auf Standortebene und auf Dienstebene (mit Ausnahme des Benutzerserverdiensts) angewendet werden. Mit dem Cmdlet **Remove-CsPrivacyConfiguration** haben Sie die Möglichkeit, Einstellungen zu löschen, die entweder auf Standort- oder Dienstebene konfiguriert wurden. Wenn Sie das Cmdlet beispielsweise für auf Standortebene konfigurierte Einstellungen ausführen, werden diese Einstellungen gelöscht, und für die Datenschutzeinstellungen der Benutzer an diesem Standort gilt die globale Auflistung. Das Cmdlet **Remove-CsPrivacyConfiguration** kann auch für die globale Auflistung ausgeführt werden, aber diese wird nicht gelöscht. Stattdessen werden alle Eigenschaften in dieser Auflistung auf die Standardwerte zurückgesetzt. Angenommen, Sie haben zuvor die Eigenschaft "EnablePrivacyMode" in "True" geändert. Wenn Sie jetzt die globale Auflistung "löschen", wird "EnablePrivacyMode" auf seinen Standardwert "False" zurückgesetzt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsPrivacyConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPrivacyConfiguration"}

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
<td><p>Die eindeutige ID für die Datenschutzkonfigurationseinstellungen, die entfernt werden sollen. Verwenden Sie eine Syntax wie die folgende, um die auf Standortebene konfigurierten Einstellungen zu entfernen: -Identity site:Redmond. Verwenden Sie eine Syntax wie die folgende, um Einstellungen auf Dienstebene zu entfernen: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>Das Cmdlet <strong>Remove-CsPrivacyConfiguration</strong> kann auch für die globale Auflistung von Einstellungen ausgeführt werden. In diesem Fall werden die globalen Einstellungen jedoch nicht gelöscht. Stattdessen werden alle Eigenschaften in dieser Auflistung auf die Standardwerte zurückgesetzt.</p></td>
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
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Skype for Business Online-Mandantenkontos, für das Datenschutzkonfigurationseinstellungen gelöscht werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Mithilfe des folgenden Befehls können Sie die Mandanten-ID für jeden Ihrer Mandanten zurückgeben:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration-Objekt. Das Cmdlet **Remove-CsPrivacyConfiguration** akzeptiert eine weitergeleitete Eingabe von Konfigurationsobjekten für den Datenschutz.

## Rückgabetypen

Keine. Mit dem Cmdlet **Remove-CsPrivacyConfiguration** werden stattdessen vorhandene Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration" gelöscht.

## Siehe auch

#### Weitere Ressourcen

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

