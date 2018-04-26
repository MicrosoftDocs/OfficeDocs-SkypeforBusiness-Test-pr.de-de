---
title: Set-CsCertificate
TOCTitle: Set-CsCertificate
ms:assetid: 6da0be05-b257-4258-9d6d-7ddf283f1038
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398518(v=OCS.15)
ms:contentKeyID: 49294334
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCertificate

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ermöglicht die Zuweisung von Zertifikaten zu Lync Server-Servern oder -Serverrollen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsCertificate -Reference <CertificateReference> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCertificate -Identity <XdsIdentity> -Path <String> -Type <CertType[]> [-Password <String>] <COMMON PARAMETERS>

    Set-CsCertificate -Thumbprint <String> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Über den Befehl in Beispiel 1 wird das Zertifikat mit dem Fingerabdruck "B142918E463981A76503828BB1278391B716280987B" der Rolle "WebServicesExternal" auf dem lokalen Computer zugewiesen.

    Set-CsCertificate -Type WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## BEISPIEL 2

In Beispiel 2 wird das Zertifikat mit dem Fingerabdruck "B142918E463981A76503828BB1278391B716280987B" drei verschiedenen Rollen auf dem lokalen Computer zugewiesen: "Default", "WebServicesInternal" und "WebServicesExternal".

    Set-CsCertificate -Type Default, WebServicesInternal, WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## Detaillierte Beschreibung

Mit Zertifikaten können Server und Serverrollen in Lync Server ihre Identitätswerte überprüfen. Beispielsweise überprüft ein Edgeserver mithilfe von Zertifikaten, ob der Computer, mit dem er kommuniziert, tatsächlich ein Front-End-Server ist (und umgekehrt). Für eine vollständige Implementierung von Lync Server müssen den Serverrollen die entsprechenden Zertifikate zugewiesen werden.

Mit dem Cmdlet **Set-CsCertificate** können Administratoren Servern oder Serverrollen Zertifikate zuweisen. Beachten Sie, dass nur Zertifikate zugewiesen werden können, die bereits für die Verwendung mit Lync Server konfiguriert wurden. Zur Ermittlung der für die Zuweisung verfügbaren Zertifikate verwenden Sie das Cmdlet **Get-CsCertificate**.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Sie müssen ein lokaler Administrator sein, um das Cmdlet **Set-CsCertificate** lokal ausführen zu können. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCertificate"}

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
<td><p>Bei Festlegung auf &quot;Global&quot; kann das Zertifikat dem globalen Gültigkeitsbereich zugewiesen werden. Globale Zertifikate werden automatisch kopiert und an die entsprechenden Computer verteilt.</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Vollständiger Pfad zur PFX-Zertifikatsdatei.</p></td>
</tr>
<tr class="odd">
<td><p><em>Reference</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertificateReference</p></td>
<td><p>Objektverweis auf ein für die Verwendung mit Lync Server konfiguriertes Zertifikat. Über den folgenden Befehl wird ein Objektverweis (die Variable &quot;$x&quot;) zurückgegeben, der ein Zertifikat mit dem Fingerabdruck &quot;B142918E463981A76503828BB1278391B716280987B&quot; darstellt:</p>
<p>$x = Get-CsCertificate | Where-Object {$_.Thumbprint –eq &quot;B142918E463981A76503828BB1278391B716280987B&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Eindeutige ID für das Zertifikat. Der Fingerabdruck eines Zertifikats kann wie folgt aussehen: B142918E463981A76503828BB1278391B716280987B.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Zugewiesener Zertifikatstyp. Zu den Zertifikatstypen gehören u. a. die folgenden:</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (nur Microsoft Lync Online 2010)</p>
<p>ProvisionService (nur Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Mit dieser Syntax wird beispielsweise das Standardzertifikat zugewiesen: -Type Default.</p>
<p>Sie können in einem einzelnen Befehl mehrere Typen angeben, indem Sie die Zertifikatstypen durch Kommata abtrennen:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>EffectiveDate</em></p></td>
<td><p>Optional</p></td>
<td><p>System.DateTime</p></td>
<td><p>Zeitpunkt (Datum und Uhrzeit), zu dem das Zertifikat zuerst verwendet werden kann. Verwenden Sie beispielsweise die folgende Syntax auf einem Server, für den &quot;Englisch (Vereinigte Staaten)&quot; in den Regions- und Spracheinstellungen eingestellt ist, um ein Zertifikat für die erste Verwendung am 31. Juli 2012 um 8:00 Uhr zu konfigurieren:</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Das Kennwort für das Zertifikat.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, ausführliche Informationen zu den Verfahren aufzuzeichnen, die vom Cmdlet <strong>Set-CsCertificate</strong> ausgeführt werden. Der Parameterwert sollte den vollständigen Pfad zur HTML-Datei enthalten, die generiert werden soll. Beispiel: -Report C:\Logs\Certificates.html. Wenn die angegebene Datei bereits vorhanden ist, wird sie automatisch mit den neuen Informationen überschrieben.</p></td>
</tr>
<tr class="odd">
<td><p><em>Roll</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ermöglicht die Aktualisierung des angegebenen Zertifikats an dem Datum und zu der Uhrzeit, die mit dem Parameter &quot;EffectiveDate&quot; festgelegt werden. Hiermit können Sie einen Zeitpunkt angeben, zu dem das neue Zertifikat das primäre Zertifikat wird. Beachten Sie, dass der Befehlt scheitert, wenn Sie den Parameter &quot;Roll&quot; angeben, ohne den Parameter &quot;EffectiveDate&quot; einzuschließen.</p></td>
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

Microsoft.Rtc.Management.Deployment.CertificateReference.

## Rückgabetypen

Das Cmdlet **Set-CsCertificate** gibt keine Werte oder Objekte zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)

