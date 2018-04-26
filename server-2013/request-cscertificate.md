---
title: Request-CsCertificate
TOCTitle: Request-CsCertificate
ms:assetid: 24e8ba6f-6023-4c03-a594-5b40784fd16a
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425723(v=OCS.15)
ms:contentKeyID: 49293443
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Request-CsCertificate

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ermöglicht die Anforderung von Zertifikaten für die Verwendung mit Servern mit Lync Server und Serverrollen. Ermöglicht es zudem, den Status von vorhandenen Zertifikatsanforderungen zu prüfen und ggf. eine oder alle dieser Anforderungen abzubrechen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Request-CsCertificate -New <SwitchParameter> -Type <CertType[]> [-AllSipDomain <SwitchParameter>] [-CA <String>] [-CaAccount <String>] [-CaPassword <String>] [-City <String>] [-ClientEKU <$true | $false>] [-ComputerFqdn <Fqdn>] [-Country <String>] [-DomainName <String>] [-FriendlyName <String>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-KeyAlg <RSA | ECDH_P256 | ECDH_P384 | ECDH_P521>] [-KeySize <Int32>] [-Organization <String>] [-OU <String>] [-Output <String>] [-PrivateKeyExportable <$true | $false>] [-State <String>] [-Template <String>] <COMMON PARAMETERS>

    Request-CsCertificate -List <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Retrieve <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    Request-CsCertificate -Clear <SwitchParameter> [-RequestId <Int32>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Mit dem in Beispiel 1 gezeigten Befehl wird eine neue Zertifikatsanforderung erstellt: Es wird Kontakt zur Zertifizierungsstelle "atl-ca-001.litwareinc.com\\myca" aufgenommen und ein neues Zertifikat "WebServicesExternal" angefordert.

    Request-CsCertificate -New -Type WebServicesExternal -CA "atl-ca-001.litwareinc.com\myca"

## BEISPIEL 2

Im zweiten Beispiel werden alle ausstehenden Zertifikatanforderungen aufgeführt, die mit dem Cmdlet **Request-CsCertificate** erstellt wurden.

    Request-CsCertificate -List

## BEISPIEL 3

In Beispiel 3 wird mit dem Parameter "Output" eine Offlinezertifikatsanforderung erstellt.

    Request-CsCertificate -New -Type WebServicesExternal -Output C:\Certificates\WebServicesExternal.cer

## BEISPIEL 4

Das vierte Beispiel ist ein detaillierteres (realistischeres) Beispiel zur Verwendung des Cmdlets "Request-CsCertificate". In diesem Beispiel wird ein Zertifikat zur Verwendung mit der Standard Edition von Lync Server angefordert.

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Standard Edition Certficate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-cs-001.litwareinc.com,atl-ext.litwareinc.com"

## BEISPIEL 5

In Beispiel 5 wird ein Poolzertifikat zur Verwendung mit der Enterprise Edition von Lync Server angefordert.

    Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -ComputerFqdn "atl-cs-001.litwareinc.com" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Enterprise Edition Pool Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "pool1.litwareinc.com,pool1int.litwareinc.com,pool1ext.litwareinc.com"

## BEISPIEL 6

Im sechsten Beispiel wird gezeigt, wie Sie ein Zertifikat für den internen Edgeserver anfordern können.

    Request-CsCertificate -New -Type Internal -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "Internal Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com, ap.litwareinc.com"

## BEISPIEL 7

Beispiel 7 ist eine Variante des Befehls aus Beispiel 6. In diesem Fall wird die Anforderung jedoch für den externen Edgeserver erstellt.

    Request-CsCertificate -New -Type AccessEdgeExternal,DataEdgeExternal,AudioVideoAuthentication -ComputerFqdn "atl-edge-001" -CA "atl-ca-001.litwareinc.com\myca" -FriendlyName "External Edge Certificate" -Template jcila -PrivateKeyExportable $True -DomainName "atl-edge-001.litwareinc.com,ap.litwareinc.com,dp.litwareinc.com,atl-edge-001"

## Detaillierte Beschreibung

Mit Zertifikaten können Server und Serverrollen in Lync Server ihre Identitätswerte überprüfen. Beispielsweise überprüft ein Edgeserver mithilfe von Zertifikaten, ob der Computer, mit dem er kommuniziert, tatsächlich ein Front-End-Server ist (und umgekehrt). Für eine vollständige Implementierung von Lync Server müssen den Serverrollen die entsprechenden Zertifikate zugewiesen werden.

Sie können Zertifikate für Lync Server zum einen durch den Aufruf des Cmdlets **Request-CsCertificate** anfordern. Zur Anforderung von Zertifikaten für die Verwendung mit Lync Server können auch andere Windows-Standardtools verwendet werden. Ein wesentlicher Vorteil des Cmdlets **Request-CsCertificate** besteht jedoch darin, dass das Cmdlet vor der Kontaktaufnahme mit der Zertifizierungsstelle Ihre Topologie analysiert. Anhand dieser Analyse fordert das Cmdlet **Request-CsCertificate** automatisch ein Zertifikat mit den Feldern für den Antragstellernamen und den alternativen Antragstellernamen an.

Das Cmdlet **Request-CsCertificate** wurde speziell für die Anforderung von Zertifikaten zur Verwendung mit Lync Server konzipiert. Es dient nicht als allgemeines Zertifikatverwaltungstool.

Mit diesem Cmdlet können Sie nicht nur neue Zertifikate anfordern, sondern auch ausstehende Zertifikatsanforderungen überprüfen, vorausgesetzt, die Zertifikate wurden mit dem Cmdlet **Request-CsCertificate** angefordert. Mit dem Cmdlet **Request-CsCertificate** können Sie auch ausstehende Zertifikatsanforderungen löschen, sofern diese Zertifikate mit dem Cmdlet angefordert wurden.

Eine Zertifikatsanforderung kann zu einer Fehlermeldung führen, wenn abgelehnte Anforderungen vorliegen. Derzeit unterstützt das Cmdlet **Request-CsCertificate** nur diese Anforderungstypen: "Issued", "Denied" und "Pending". Wenn es aufgrund einer abgelehnten Anforderung zu Problemen kommt, verwenden Sie einen Befehl wie den folgenden, um die abgelehnte Anforderung zu löschen (hierbei entspricht 224 der Anforderungs-ID der abgelehnten Zertifikatsanforderung):

Request-CsCertificate –Clear –RequestID 224

Nach Ausführung dieses Befehls sollten Sie Zertifikate anfordern können.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Sie müssen Mitglied der lokalen Administratorengruppe sein und über Rechte für die angegebene Zertifizierungsstelle verfügen, um das Cmdlet **Request-CsCertificate** lokal ausführen zu können. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Request-CsCertificate"}

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
<td><p><em>Clear</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Sofern angegeben, werden alle ausstehenden Zertifikatsanforderungen gelöscht, die mit dem Cmdlet <strong>Request-CsCertificate</strong> erstellt wurden.</p></td>
</tr>
<tr class="even">
<td><p><em>List</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Sofern angegeben, werden alle ausstehenden Zertifikatsanforderungen aufgelistet, die mit dem Cmdlet <strong>Request-CsCertificate</strong> erstellt wurden.</p></td>
</tr>
<tr class="odd">
<td><p><em>New</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Gibt an, dass Sie ein neues Zertifikat anfordern möchten.</p></td>
</tr>
<tr class="even">
<td><p><em>Retrieve</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Sofern angegeben, werden alle ausstehenden Zertifikatsanforderungen abgerufen, die mit dem Cmdlet <strong>Request-CsCertificate</strong> erstellt wurden. Es wird versucht, den Vorgang abzuschließen und das angeforderte Zertifikat zu importieren.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Typ des angeforderten Zertifikats. Zu den Zertifikatstypen gehören u. a. die folgenden:</p>
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
<p>Mit dieser Syntax wird beispielsweise ein neues Standardzertifikat angefordert: -Type Default.</p>
<p>Sie können in einem einzelnen Befehl mehrere Typen angeben, indem Sie die Zertifikatstypen durch Kommata abtrennen:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>AllSipDomain</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Sofern angegeben, werden alle Ihre SIP-Domänen automatisch dem Feld &quot;Alternative Antragstellernamen&quot; der Zertifikate hinzugefügt. Falls nicht angegeben, wird standardmäßig nur die primäre SIP-Domäne hinzugefügt. Mithilfe des Parameters &quot;DomainName&quot; können allerdings weitere Domänen angegeben werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>CA</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Der vollqualifizierte Domänenname (FQDN), der auf die Zertifizierungsstelle verweist. Beispiel: -CA &quot;atl-ca-001.litwareinc.com\myca&quot;. Geben Sie an der Windows PowerShell-Eingabeaufforderung Folgendes ein, und drücken Sie die Eingabetaste, um eine Liste der bekannten Zertifizierungsstellen abzurufen:</p>
<p>certutil</p>
<p>Die von &quot;Certutil&quot; zurückgegebene Eigenschaft &quot;Config&quot; gibt die Adresse einer Zertifizierungsstelle an.</p></td>
</tr>
<tr class="even">
<td><p><em>CaAccount</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Kontoname des Benutzers, der das neue Zertifikat anfordert, im Format &quot;Domänenname\Benutzername&quot;. Beispiel: -CaAccount &quot;litwareinc\kenmyer&quot;. Wenn dieser Wert nicht angegeben wird, verwendet das Cmdlet <strong>Request-CsCertificate</strong> bei der Anforderung des neuen Zertifikats die Anmeldeinformationen des angemeldeten Benutzers.</p></td>
</tr>
<tr class="odd">
<td><p><em>CaPassword</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Kennwort für den Benutzer, der das neue Zertifikat anfordert (festgelegt durch den Parameter &quot;CaAccount&quot;).</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ort, an dem das Zertifikat bereitgestellt wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientEKU</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Legen Sie diesen Parameter auf &quot;True&quot; fest, wenn das Zertifikat zur Clientauthentifizierung verwendet werden soll. Diese Form der Authentifizierung ist erforderlich, wenn Ihre Benutzer Chatnachrichten mit AOL-Kontobenutzern austauschen können sollen. Der EKU-Teil des Parameternamens steht für &quot;Extended Key Usage&quot; (erweiterte Schlüsselverwendung). In diesem Feld werden die gültigen Verwendungszwecke für das Zertifikat aufgeführt.</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN des Computers, für den das Zertifikat angefordert wird. Sofern angegeben, zwingt dieser Parameter das Cmdlet <strong>Request-CsCertificate</strong>, eine Verbindung mit dem zentralen Verwaltungsspeicher herzustellen, um den angegebenen Computer zu suchen. Sie sollten beim Anfordern eines Zertifikats immer den Computernamen angeben, selbst wenn Sie ein Poolzertifikat anfordern. Das Cmdlet <strong>Request-CsCertificate</strong> fügt den Poolnamen automatisch dem Antragstellernamen für alle Zertifikate hinzu, die mit diesem Cmdlet abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Land/Region, in dem/der das Zertifikat bereitgestellt wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainName</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Durch Trennzeichen getrennte Liste von vollqualifizierten Domänennamen, die dem Feld für den alternativen Antragstellernamen des Zertifikats hinzugefügt werden sollen. Beispiel:</p>
<p>-DomainName &quot;atl-cs-001.litwareinc.com, atl-cs-002.litwareinc.com,atl-cs-003.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>FriendlyName</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Vom Benutzer zugewiesener Name, mit dem das Zertifikat leichter identifiziert werden kann.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) eines globalen Katalogservers in Ihrer Domäne. Dieser Parameter ist nicht erforderlich, wenn Sie das Cmdlet <strong>Request-CsCertificate</strong> auf einem Computer mit einem Konto in der Domäne ausführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN eines Domänencontrollers, auf dem die globalen Einstellungen gespeichert wurden. Wenn die globalen Einstellungen im Systemcontainer von Active Directory-Domänendienste gespeichert wurden, muss dieser Parameter auf den Stammdomänencontroller verweisen. Wenn die globalen Einstellungen im Konfigurationscontainer gespeichert sind, kann jeder Domänencontroller verwendet werden, und dieser Parameter kann ausgelassen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>KeyAlg</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.X509Certificates.KeyAlgorithmIdentifier</p></td>
<td><p>Gibt die Art des Kryptografiealgorithmus an, der beim Generieren der öffentlichen und privaten Schlüssel für das neue Zertifikat verwendet wird. Gültige Schlüsselalgorithmen:</p>
<p>RSA</p>
<p>ECDH_P256</p>
<p>ECDH_P384</p>
<p>ECDH_P521</p></td>
</tr>
<tr class="odd">
<td><p><em>KeySize</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>Gibt die Größe des privaten Schlüssels (in Bit) an, der vom Zertifikat verwendet wird. Größere Schlüssel sind sicherer, führen bei der Entschlüsselung jedoch zu mehr Verarbeitungsaufwand.</p>
<p>Gültige Schlüsselgrößen sind 1024, 2048 und 4096. Beispiel: -KeySize 2048.</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Name der Organisation, die das neue Zertifikat anfordert. Beispiel: -Organization &quot;Litwareinc&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Active Directory-Organisationseinheit für den Computer, dem das neue Zertifikat zugewiesen wird.</p></td>
</tr>
<tr class="even">
<td><p><em>Output</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Der Pfad zur Zertifikatsdatei. Wenn Sie eine Offlinezertifikatsanforderung erstellen möchten, verwenden Sie den Parameter &quot;Output&quot;, und geben Sie einen Dateipfad für die Zertifikatsanforderung an. Beispiel: -Output C:\Certificates\NewCertificate.pfx. Mit diesem Befehl wird eine Zertifikatsanforderungsdatei erstellt, die anschließend per E-Mail zur Verarbeitung an eine Zertifizierungsstelle gesendet werden kann.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Legen Sie diesen Parameter auf &quot;True&quot; fest, wenn der private Schlüssel des Zertifikats exportiert werden darf. Wenn ein privater Schlüssel exportierbar ist, kann das Zertifikat kopiert und auf mehreren Computern verwendet werden.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, einen Dateipfad für die bei der Ausführung des Cmdlets erstellte Protokolldatei anzugeben. Beispiel: -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RequestId</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>Einer Zertifikatsanforderung zugeordnete ID. Mit dem Parameter &quot;RequestID&quot; können Sie ein einzelnes Zertifikat auflisten, abrufen oder löschen.</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>US-Bundesstaat, in dem das Zertifikat bereitgestellt wird. Beispiel: -State WA.</p></td>
</tr>
<tr class="odd">
<td><p><em>Template</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Gibt die Zertifikatsvorlage an, die beim Generieren des neuen Zertifikats verwendet werden soll. Beispiel: -Template &quot;WebServer&quot;. Die angeforderte Vorlage muss in der Zertifizierungsstelle installiert sein. Beachten Sie, dass es sich bei dem eingegebenen Wert um den Namen der Vorlage, nicht um den Anzeigenamen der Vorlage, handeln muss.</p></td>
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

Keine. Das Cmdlet **Request-CsCertificate** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Keine. Mit dem Cmdlet **Request-CsCertificate** können stattdessen Instanzen des Objekts "Microsoft.Rtc.Management.Deployment.CertificateReference" verwaltet werden.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

