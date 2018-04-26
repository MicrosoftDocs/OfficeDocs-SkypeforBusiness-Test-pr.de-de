---
title: Import-CsCertificate
TOCTitle: Import-CsCertificate
ms:assetid: 87bdafce-f4b9-4c44-ad8f-86c2deb680a4
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398688(v=OCS.15)
ms:contentKeyID: 49294657
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsCertificate

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Importiert ein Zertifikat zur Verwendung mit Lync Server. Wenn ein Zertifikat nicht durch Verwendung des Cmdlets **Request-CsCertificate** erworben wird, muss dieses Zertifikat importiert werden, bevor es einer Lync Server-Serverrolle zugewiesen werden kann. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Import-CsCertificate -Identity <XdsIdentity> -Type <CertType[]> <COMMON PARAMETERS>

    Import-CsCertificate [-PrivateKeyExportable <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Path <String> [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Password <String>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 importiert das Zertifikat "C:\\Certificates\\WebServer.pfx". Nach der Ausführung des Befehls steht das Zertifikat für die Zuweisung zu einer Serverrolle zur Verfügung.

    Import-CsCertificate -Path "C:\Certificates\WebServer.pfx" -PrivateKeyExportable $True

## Detaillierte Beschreibung

Mit Zertifikaten können Server und Serverrollen in Lync Server ihre Identitätswerte überprüfen. Beispielsweise überprüft ein Edgeserver mithilfe von Zertifikaten, ob der Computer, mit dem er kommuniziert, tatsächlich ein Front-End-Server ist (und umgekehrt). Damit Lync Server vollständig implementiert werden kann, müssen Sie die den jeweiligen Serverrollen die entsprechenden Zertifikate zuweisen.

Um Zertifikate einer Lync Server-Rolle zuzuweisen, müssen diese Zertifikate in Lync Server bekannt gemacht werden. Mit dem Cmdlet **Request-CsCertificate** können Sie sowohl neue Online- als auch neue Offlinezertifikate anfordern. Wenn Sie eine Onlineanforderung stellen, wird das Zertifikat automatisch heruntergeladen und im lokalen Zertifikatspeicher abgelegt. Außerdem kann es sofort von Lync Server verwendet werden. Bei einer Offlineanforderung wird Ihnen eine Zertifikatdatei zugesandt. In diesem Fall können Sie das Zertifikat mit dem Cmdlet **Import-CsCertificate** importieren, um das Zertifikat für eine Zuweisung zu einer Lync Server-Serverrolle verfügbar zu machen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Sie müssen ein lokaler Administrator sein, um das Cmdlet **Import-CsCertificate** lokal ausführen zu können. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsCertificate"}

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
<td><p>Vollständiger Pfad zur Zertifikatdatei, die importiert werden soll. Beispiel: –Path &quot;C:\Certificates\WebServer.cer&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Typ des angeforderten Zertifikats. Zu den Zertifikatstypen gehören u. a. die folgenden:</p>
<p>* AccessEdgeExternal</p>
<p>* AudioVideoAuthentication</p>
<p>* DataEdgeExternal</p>
<p>* Default</p>
<p>* External</p>
<p>* Internal</p>
<p>* iPadAPNService</p>
<p></p>
<p>* iPhoneAPNService</p>
<p>* LogRetentionService</p>
<p>* MPNService</p>
<p>* OAuthTokenIssuer</p>
<p>* PICWebService</p>
<p>* ProvisionService</p>
<p>* SMPDNSWebService</p>
<p>* TenantAdmin</p>
<p>* UpgradeEngineService</p>
<p>* WebServicesExternal</p>
<p>* WebServicesInternal</p>
<p>* WsFedTokenTransfer</p>
<p>* XMPPServer</p></td>
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
<td><p>Der Zertifikatdatei zugeordnetes Kennwort.</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Wenn Sie diesen Parameter auf &quot;True&quot; festlegen, wird sichergestellt, dass der private Schlüssel des Zertifikats vom Konto &quot;Netzwerkdienst&quot; gelesen werden kann.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, einen Dateipfad für die bei der Ausführung des Cmdlets erstellte Protokolldatei anzugeben. Beispiel: -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Roll</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ermöglicht die Aktualisierung des angegebenen Zertifikats an dem Datum und zu der Uhrzeit, die mit dem Parameter &quot;EffectiveDate&quot; festgelegt werden. Hiermit können Sie einen Zeitpunkt angeben, zu dem das neue Zertifikat das primäre Zertifikat wird. Beachten Sie, dass der Befehlt scheitert, wenn Sie den Parameter &quot;Roll&quot; angeben, ohne den Parameter &quot;EffectiveDate&quot; einzuschließen.</p></td>
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

Keine. Das Cmdlet **Import-CsCertificate** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Keine.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCertificate](get-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

