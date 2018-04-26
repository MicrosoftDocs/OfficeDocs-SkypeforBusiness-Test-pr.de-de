---
title: Get-CsCertificate
TOCTitle: Get-CsCertificate
ms:assetid: 15b8f019-1d00-4389-9abe-18deb8cbf2ea
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398227(v=OCS.15)
ms:contentKeyID: 49293280
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCertificate

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu Zertifikaten auf den lokalen Computern zurück, die für die Verwendung in Lync Server konfiguriert sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsCertificate [-Identity <XdsIdentity>] [-Report <String>] [-Type <CertType[]>]

## Beispiele

## BEISPIEL 1

Der Befehl im ersten Beispiel gibt Informationen zu den Zertifikaten zurück, die derzeit Lync Server-Komponenten zugewiesen sind. Hierzu wird das Cmdlet **Get-CsCertificate** ohne zusätzliche Parameter aufgerufen.

    Get-CsCertificate

## BEISPIEL 2

Im zweiten Beispiel werden alle Lync Server-Zertifikate abgerufen, die für interne Webdienste genutzt werden. Hierzu wird der Parameter "Type" zusammen mit dem Parameterwert "WebServicesInternal" verwendet.

    Get-CsCertificate -Type WebServicesInternal

## BEISPIEL 3

Im dritten Beispiel werden alle Lync Server-Zertifikate zurückgegeben, die vor dem 1. September 2012 ablaufen. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsCertificate** auf, um eine Auflistung aller derzeit verwendeten Lync Server-Zertifikate zurückzugeben. Diese Auflistung wird anschließend an das Cmdlet **Where-Object** weitergeleitet, das nur die Zertifikate auswählt, die vor dem 1. September 2012 ablaufen. In diesem Beispiel wird für Datums- und Uhrzeitwerte das US-Format (9/1/2011) verwendet. Datumswerte müssen in einem Format angegeben werden, das mit den jeweiligen Regions- und Spracheinstellungen kompatibel ist.

    Get-CsCertificate | Where-Object {$_.NotAfter -lt "9/1/2012"}

## BEISPIEL 4

In Beispiel 4 werden Informationen zu allen von der Zertifizierungsstelle MyCa ausgestellten Lync Server-Zertifikaten zurückgegeben. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsCertificate** ohne Parameter auf, um eine Auflistung aller derzeit verwendeten Zertifikate zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das alle Zertifikate herausfiltert, bei denen die Eigenschaft "Issuer" den Wert "Cn=MyCa" aufweist (der Vergleichsoperator "-eq" steht für "equal to").

    Get-CsCertificate | Where-Object {$_.Issuer -eq "Cn=MyCa"}

## BEISPIEL 5

Der Befehl in Beispiel 5 gibt alle Lync Server-Zertifikate zurück, bei denen die Eigenschaft "Subject" auf "CN=atl-cs-001.litwareinc.com" festgelegt wurde. Hierzu wird das Cmdlet **Get-CsCertificate** ausgeführt, um eine Auflistung aller Lync Server-Zertifikate zurückzugeben, die dann an das Cmdlet **Where-Object** weitergeleitet wird. Das Cmdlet **Where-Object** wählt daraufhin nur die Zertifikate aus, bei denen die Eigenschaft "Subject" den Wert "CN=atl-cs-001.litwareinc.com" aufweist.

    Get-CsCertificate | Where-Object {$_.Subject -eq "CN=atl-cs-001.litwareinc.com"}

## Detaillierte Beschreibung

Mit Zertifikaten können Server und Serverrollen in Lync Server ihre Identitätswerte überprüfen. Beispielsweise überprüft ein Edgeserver mithilfe von Zertifikaten, ob der Computer, mit dem er kommuniziert, tatsächlich ein Front-End-Server ist (und umgekehrt). Damit Lync Server vollständig implementiert werden kann, müssen Sie die den jeweiligen Serverrollen die entsprechenden Zertifikate zuweisen.

Mit dem Cmdlet **Get-CsCertificate** können Sie ausführliche Informationen zu den Zertifikaten abrufen, die für die Verwendung in Lync Server konfiguriert sind. Beachten Sie, dass mit dem Cmdlet nur Informationen zu Lync Server-Zertifikaten zurückgegeben werden. Wenn ein Zertifikat nicht für die Verwendung in Lync Server konfiguriert wurde (mit dem Cmdlet **Set-CsCertificate**), wird das Zertifikat beim Ausführen des Cmdlets **Get-CsCertificate** nicht zurückgegeben.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsCertificate** lokal auszuführen: RTCUniversalServerAdmins.

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
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Ermöglicht das Abrufen von auf globaler Ebene konfigurierten Zertifikaten. (Globale Zertifikate werden kopiert und an die entsprechenden Computer verteilt.) Mit der folgenden Syntax können Sie Informationen zu den globalen Zertifikaten zurückgeben:</p>
<p>Get-CsCertificate –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, ausführliche Informationen zu den mit dem Cmdlet <strong>Get-CsCertificate</strong> ausgeführten Vorgängen aufzuzeichnen. Als Parameterwert wird der vollständige Pfad der zu generierenden HTML-Datei verwendet. Beispiel: -Report C:\Logs\Certificates.html. Wenn die angegebene Datei bereits vorhanden ist, wird sie automatisch mit den neuen Informationen überschrieben.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Typ des angeforderten Zertifikats. Zu den Zertifikatstypen gehören u. a. die folgenden:</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>Extern</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (nur Microsoft Lync Online 2010)</p>
<p>ProvisionService (nur Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Mit der folgenden Syntax werden beispielsweise Informationen zum Dateispeicher zurückgegeben: -Type Default.</p>
<p>Sie können in einem einzelnen Befehl mehrere Typen angeben, indem Sie die Zertifikatstypen durch Kommata abtrennen:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsCertificate** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsCertificate** werden Instanzen des Objekts "Microsoft.Rtc.Management.Deployment.CertificateReference" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

