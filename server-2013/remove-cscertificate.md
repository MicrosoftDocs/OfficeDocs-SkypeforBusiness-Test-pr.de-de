---
title: Remove-CsCertificate
TOCTitle: Remove-CsCertificate
ms:assetid: b7a83a58-9d3f-458a-867e-44466c9817dc
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412895(v=OCS.15)
ms:contentKeyID: 49295182
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCertificate

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt ein Zertifikat, das zuvor für die Verwendung durch Lync Server als verfügbar markiert wurde. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsCertificate -Type <CertType[]> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsIdentity>] [-Previous <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 löscht alle für Lync Server verfügbaren WebServicesExternal-Zertifikate. Wenn eines dieser Zertifikate derzeit verwendet wird, werden Sie vom Cmdlet **Remove-CsCertificate** aufgefordert, den Löschvorgang des Zertifikats zu bestätigen. Sie müssen diesen Vorgang bestätigen, bevor der Befehl ausgeführt werden kann. Verwenden Sie den Parameter "Force", um die Bestätigungsmeldung zu umgehen:

Remove-CsCertificate –Type WebServicesExternal -Force

    Remove-CsCertificate -Type WebServicesExternal

## Detaillierte Beschreibung

Mit Zertifikaten können Server und Serverrollen in Lync Server ihre Identitätswerte überprüfen. Beispielsweise überprüft ein Edgeserver mithilfe von Zertifikaten, ob der Computer, mit dem er kommuniziert, tatsächlich ein Front-End-Server ist (und umgekehrt). Für eine vollständige Implementierung von Lync Server müssen den Serverrollen die entsprechenden Zertifikate zugewiesen werden.

Das Cmdlet **Remove-CsCertificate** bietet die Möglichkeit, Zertifikate zu entfernen, die derzeit von Lync Server verwendet werden. Mit dem Cmdlet **Remove-CsCertificate** wird das Zertifikat nicht wirklich gelöscht; es wird vielmehr als für die Verwendung durch Lync Server nicht mehr verfügbar markiert, jegliche Zertifikatsbindungen werden entfernt, und alle Zugriffsberechtigungen auf das Zertifikat werden widerrufen (vorausgesetzt, dass kein anderer Dienst das Zertifikat verwendet). Wenn Sie das Cmdlet **Get-CsCertificate** ausführen, wird das Zertifikat unter anderem nicht mehr angezeigt.

Um das Zertifikat wieder mit Lync Server zu verwenden, müssen Sie das Zertifikat mithilfe des Cmdlets **Set-CsCertificate** erneut Lync Server zuweisen.

Wenn Sie ein Zertifikat entfernen möchten, das derzeit verwendet wird, werden Sie beim Ausführen des Cmdlets **Remove-CsCertificate** gefragt, ob Sie das Zertifikat wirklich entfernen möchten. Das Zertifikat kann erst nach Bestätigung dieser Meldung entfernt werden. Ergänzen Sie den Befehl um den Parameter "Force", um die Anzeige einer solchen Meldung zu umgehen und ein Zertifikat auch dann zu löschen, wenn es derzeit verwendet wird.

Remove-CsCertificate –Type WebServicesExternal -Force

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Sie müssen ein lokaler Administrator und Mitglied der Domäne sein, um das Cmdlet **Remove-CsCertificate** lokal auszuführen. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCertificate"}

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
<td><p><em>Type</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Typ des zu löschenden Zertifikats. Zu den Zertifikatstypen gehören u. a. die folgenden:</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>PICWebService (nur Microsoft Lync Online 2010)</p>
<p>ProvisionService (nur Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Mit dieser Syntax wird beispielsweise das Standardzertifikat &quot;Default&quot; gelöscht: -Type Default.</p>
<p>Sie können mit einem einzelnen Befehl mehrere Typen löschen, indem Sie die Zertifikatstypen durch Kommata voneinander trennen:</p>
<p>-Type Internal,External,Default</p></td>
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
<td><p>Umgeht den Aufruf der Bestätigungsmeldung, die normalerweise angezeigt wird, wenn Sie versuchen, ein Zertifikat zu löschen, das derzeit in Gebrauch ist.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Bei Festlegung auf &quot;Global&quot; wird das Zertifikat aus dem globalen Bereich entfernt. Wenn kein Wert festgelegt ist, werden Zertifikate vom lokalen Computer entfernt.</p></td>
</tr>
<tr class="odd">
<td><p><em>Previous</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Wenn dieser Parameter angegeben ist, entfernt er statt des aktuell zugeordneten Zertifikats das zuvor zugeordnete Zertifikat.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, ausführliche Informationen zu den Verfahren aufzuzeichnen, die vom Cmdlet <strong>Remove-CsCertificate</strong> ausgeführt werden. Der Parameterwert sollte den vollständigen Pfad zur HTML-Datei enthalten, die generiert werden soll. Beispiel: -Report C:\Logs\Certificates.html. Wenn die angegebene Datei bereits vorhanden ist, wird sie automatisch mit den neuen Informationen überschrieben.</p></td>
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

Keine. Das Cmdlet **Remove-CsCertificate** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Keine. Mit dem Cmdlet **Remove-CsCertificate** werden stattdessen Instanzen des Objekts "Microsoft.Rtc.Management.Deployment.CertificateReference" gelöscht.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

