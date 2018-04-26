---
title: Get-CsTenantFederationConfiguration
TOCTitle: Get-CsTenantFederationConfiguration
ms:assetid: e5f836d0-6066-4c23-9594-6e3f1cbd39ef
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994072(v=OCS.15)
ms:contentKeyID: 52056480
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantFederationConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Partnerverbundkonfigurationseinstellungen für Ihre Microsoft Lync Online-Mandanten zurück. Partnerverbundkonfigurationseinstellungen werden verwendet, um zu bestimmen, mit welchen Domänen (wenn überhaupt) Ihre Benutzer kommunizieren können.

Das Cmdlet **Get-CsTenantFederationConfiguration** kann nur mit Skype for Business Online verwendet werden.

## Syntax

    Get-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-LocalStore] [-Verbose] Get-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-Filter <String>] [-LocalStore] [-Verbose]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 gibt Partnerverbundkonfigurationsinformationen für den Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" zurück. Mandanten-IDs können mit einem Befehl wie dem folgenden abgerufen werden:

Get-CsTenant | Select-Object TenantID

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Der Parameter "Tenant" ist optional. Sie können das Cmdlet "Get-CsTenantFederationConfiguration" auch mit der folgenden Syntax aufrufen:

    Get-CsTenantFederationConfiguration

## Beispiel 2

In Beispiel 2 werden Informationen für alle Domänen zurückgegeben, die in der Liste der zulässigen Partnerverbünde für den Mandanten "bf19b7db-6960-41e5-a139-2aa373474354" gefunden werden. (Die zulässige Liste stellt alle Domänen dar, mit denen der Mandant einen Partnerverbund herstellen kann.) Dafür ruft der Befehl zunächst das Cmdlet **Get-CsTenantFederationConfiguration** auf, um Partnerverbundinformationen für den angegebenen Mandanten zurückzugeben. Diese Informationen werden dann an das Cmdlet **Select-Object** weitergeleitet, das "ExpandProperty" verwendet, um die Eigenschaft "AllowedList" zu "erweitern". Das Erweitern einer Eigenschaft bedeutet einfach, dass alle in dieser Eigenschaft gespeicherten Informationen in einem einfach zu lesenden Format auf dem Bildschirm angezeigt werden.

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty AllowedList

## Beispiel 3

Der vorstehende Befehl gibt die Partnerverbundkonfiguration für alle derzeit in der Organisation verwendeten Mandanten zurück. Zum Ausführen dieser Aufgabe ruft der Befehl zunächst das Cmdlet **Get-CsTenant** ohne Parameter auf. Damit wird eine Auflistung aller verfügbaren Mandanten zurückgegeben. Diese Auflistung wird dann an das Cmdlet **ForEach-Object** weitergeleitet. "ForEach-Object" nimmt jeden Mandanten in der Auflistung und ruft das Cmdlet **Get-CsTenantFederationConfiguration** auf. Dabei wird der Eigenschaftswert "TenantID" (zurückgegeben vom Cmdlet **Get-CsTenant**) verwendet, um die Mandanten-ID darzustellen.

    Get-CsTenant | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId}

## Beispiel 4

In Beispiel 4 werden Partnerverbundinformationen nur für die Mandanten zurückgegeben, die keinen Partnerverbund mit öffentlichen Benutzern zulassen. Dafür ruft der Befehl zunächst das Cmdlet **Get-CsTenant** ohne Parameter auf, um eine Auflistung aller Mandanten zurückzugeben, die für die Verwendung in der Organisation konfiguriert sind. Diese Auflistung wird dann an das Cmdlet **ForEach-Object** weitergeleitet, das jeden Mandanten in der Auflistung nimmt und dann das Cmdlet **Get-CsTenantFederationConfiguration** verwendet, um Konfigurationsinformationen für den Partnerverbund zurückzugeben. Der gesamte Satz mit Konfigurationseinstellungen für den Partnerverbund wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Mandanten heraussucht, bei denen die Eigenschaft "AllowPublicUsers" gleich (-eq) "$False" ist.

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Get-CsTenantFederationConfiguration -Tenant $_.TenantId} | Where-Object {$_.AllowPublicUsers -eq $False}

## Detaillierte Beschreibung

Ein Verbund ist ein Dienst, über den Benutzer Chat- und Anwesenheitsinformationen mit Benutzern anderer Domänen austauschen können. Mit Lync Online können Administratoren die Verbundkonfigurationseinstellungen verwenden, um Folgendes zu steuern:

  - Die Möglichkeit für Benutzer, mit Personen aus anderen Domänen kommunizieren zu können, sowie für die Benutzer festlegen, mit welchen Domänen Kommunikation erlaubt sein soll

  - Die Möglichkeit für Benutzer, mit Personen zu kommunizieren, die Konten bei öffentlichen Instant Messaging- und Anwesenheitsanbietern wie Windows Live, AOL oder Yahoo\! haben

Mit dem Cmdlet **Get-CsTenantFederationConfiguration** können Administratoren Partnerverbundinformationen für ihre Lync Online-Mandanten zurückgeben. Dieses Cmdlet kann auch verwendet werden, um die zulässigen und blockierten Listen zu prüfen, die verwendet werden, um Domänen anzugeben, mit denen Benutzer kommunizieren können. Administratoren müssen jedoch das Cmdlet **Get-CsTenantPublicProvider** verwenden, um zu sehen, mit welchen öffentlichen Chat- und Anwesenheitsanbietern Benutzer kommunizieren können.

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
<td><p>Ermöglicht die Verwendung von Platzhalterzeichen für die Rückgabe einer Auflistung von Konfigurationseinstellungen für den Mandantenpartnerverbund. Da Sie auf eine einzige globale Auflistung von Partnerverbundkonfigurationseinstellungen beschränkt sind, muss der Parameter &quot;Filter&quot; nicht verwendet werden. Dennoch ist folgende Syntax für das Cmdlet <strong>Get-CsTenantFederationConfiguration</strong> gültig:</p>
<p>Get-CsTenantFederationConfiguration –Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Filter &quot;g*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Gibt die Auflistung der zurückzugebenden Partnerverbundkonfigurationseinstellungen eines Mandaten an. Da es für jeden Mandanten nur eine einzige globale Sammlung von Verbundeinstellungen geben kann, ist nicht erforderlich, diesen Parameter einzufügen, wenn das Cmdlet <strong>Get-CsTenantFederationConfiguration</strong> aufgerufen wird. Wenn Sie den Parameter &quot;Identity&quot; verwenden, müssen Sie auch den Parameter &quot;Tenant&quot; einfügen. Beispiel:</p>
<p>Get-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Konfigurationsdaten für den Mandantenpartnerverbund aus dem lokalen Replikat des zentralen Verwaltungsspeichers statt aus dem zentralen Verwaltungsspeicher selbst ab.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Mandantenkontos, dessen Partnerverbundeinstellungen zurückgegeben werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Wenn Sie eine Remotesitzung von Windows PowerShell verwenden und nur eine Verbindung mit Skype for Business Online hergestellt haben, müssen Sie den Parameter <strong>Tenant</strong> nicht einfügen. Stattdessen wird die Mandanten-ID automatisch anhand Ihrer Verbindungsinformationen für Sie eingetragen. Der Parameter <strong>Tenant</strong> ist hauptsächlich zur Verwendung in einer Hybridbereitstellung vorgesehen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsTenantFederationConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Get-CsTenantFederationConfiguration** gibt Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings" zurück.

## Siehe auch

#### Weitere Ressourcen

[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

