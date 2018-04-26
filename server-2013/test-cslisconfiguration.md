---
title: Test-CsLisConfiguration
TOCTitle: Test-CsLisConfiguration
ms:assetid: 6983d42e-6b93-4365-b0f1-81031d6e251b
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398497(v=OCS.15)
ms:contentKeyID: 49294287
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet die LIS-Konfiguration (Location Information Server). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsLisConfiguration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BssId <String>] [-ChassisId <String>] [-Force <SwitchParameter>] [-Mac <String>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PortId <String>] [-PortIdSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-Subnet <String>]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die LIS-Konfiguration für den FQDN "atl-cs-001.litwareinc.com" getestet. Der Test ist erfolgreich, wenn bei Verwendung dieses vollqualifizierten Domänennamens mit den aktuellen Benutzeranmeldeinformationen eine Verbindung mit dem LIS-Webdienst hergestellt werden kann. Wenn ein übereinstimmender Standort für die Subnetz-IP-Adresse 192.168.0.0 ermittelt wird, wird diese Standortadresse zurückgegeben.

Damit dieser Befehl erfolgreich ausgeführt werden kann, muss eine Zustandsüberwachungskonfiguration mit Benutzern für synthetische Transaktionen vorhanden sein. Führen Sie das Cmdlet **Get-CsHealthMonitoringConfiguration** aus, um festzustellen, ob eine Zustandsüberwachungskonfiguration vorliegt. Führen Sie das Cmdlet **New-CsHealthMonitoringConfiguration** aus, um eine Zustandsüberwachungskonfiguration zu erstellen.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0

## BEISPIEL 2

Dieses Beispiel entspricht Beispiel 1, fügt jedoch den Parameter "UserSipAddress" hinzu. Verwenden Sie diesen Befehl, wenn keine Benutzer für synthetische Transaktionen eingerichtet wurden, der zur Ausführung des Befehls verwendete Computer jedoch ein Serverzertifikat besitzt.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com

## BEISPIEL 3

Über die erste Zeile in diesem Beispiel wird ein Windows PowerShell-Cmdlet aufgerufen, nämlich das Cmdlet **Get-Credential**, über das der Benutzer zur Eingabe einer Benutzer-ID und eines Kennworts aufgefordert wird. Diese Informationen werden in verschlüsselter Form in der Variablen "$cred" gespeichert.

Die zweite Zeile entspricht dem Befehl in Beispiel 2, fügt jedoch den Parameter "UserSipAddress" hinzu. Verwenden Sie diesen Befehl, wenn keine Benutzer für synthetische Transaktionen eingerichtet wurden und wenn der zur Ausführung des Befehls verwendete Computer kein Serverzertifikat besitzt.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com -UserCredential $cred

## BEISPIEL 4

Über die erste Zeile in diesem Beispiel wird das Cmdlet **Get-Credential** aufgerufen, über das der Benutzer zur Eingabe einer Benutzer-ID und eines Kennworts aufgefordert wird. Diese Informationen werden in verschlüsselter Form in der Variablen "$cred" gespeichert.

In Zeile 2 wird die LIS-Konfiguration getestet, indem der Webdienst-URI (https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc) basierend auf der SIP-Adresse des Remotebenutzers (sip:kmyer@litwareinc.com) aufgerufen wird und die in Zeile 1 abgerufenen Anmeldeinformationen an den Parameter "WebCredential" weitergeleitet werden. Der Test ist erfolgreich, wenn bei Verwendung dieses URI mit den bereitgestellten Benutzeranmeldeinformationen eine Verbindung mit dem LIS-Webdienst hergestellt werden kann. Wenn ein übereinstimmender Standort ermittelt wird, der die Subnetz-IP-Adresse 192.168.0.0, die MAC-Adresse "0A-23-00-00-00-AA" oder die Port-ID 4500 sowie für "ChassisId" den Wert "0A-23-00-00-00-AA" aufweist, wird diese Standortadresse zurückgegeben.

Verwenden Sie diesen Befehl, wenn der zur Ausführung des Befehls verwendete Computer kein Serverzertifikat besitzt.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -WebCredential $cred -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## BEISPIEL 5

Dieses Beispiel entspricht Beispiel 4, außer dass der Parameter "WebCredential" nicht verwendet wird (und somit das Cmdlet **Get-Credential** nicht aufgerufen wird). Verwenden Sie diesen Befehl, wenn der zur Ausführung des Befehls verwendete Computer ein Serverzertifikat besitzt.

    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## Detaillierte Beschreibung

Mit diesem Cmdlet wird ermittelt, ob der LIS-Webdienst (Location Information Server) basierend auf den in den angegebenen Parametern bereitgestellten Informationen kontaktiert werden kann. Wenn der Webdienst kontaktiert werden kann und ein Standort für die angegebenen Parameter ermittelt wird, wird der Test als erfolgreich betrachtet, und der Standort wird angezeigt. Auch wenn der Standort nicht gefunden wird und der Webdienst dennoch kontaktiert werden kann, gilt der Test als erfolgreich, es werden jedoch keine Standortinformationen zurückgegeben. Wenn Sie dieses Cmdlet ohne optionale Parameter aufrufen, wird der Test dennoch erfolgreich abgeschlossen, sofern der Webdienst kontaktiert werden kann. Auch in diesem Fall werden jedoch keine Standortinformationen zurückgegeben.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Test-CsLisConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsConfiguration"}

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
<td><p><em>TargetFqdn</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der vollqualifizierte Domänenname (mit dem Format &quot;server.litwareinc.com&quot;) des Servers, für den der Test ausgeführt werden soll.</p>
<p>Dieser Parameter ist erforderlich, wenn Sie den Parameter &quot;TargetUri&quot; nicht angeben. Wenn Sie &quot;TargetUri&quot; angeben, kann &quot;TargetFqdn&quot; nicht festgelegt werden.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der URI (Uniform Resource Identifier) des Standortinformationsdiensts. Sie können den URI des Standortinformationsdiensts über folgenden Befehl abrufen: Get-CsService –WebServer | Select-Object LIServiceInternalUri</p>
<p>Wenn für diesen Parameter ein Wert angegeben wird, ist der Parameter &quot;UserSipAddress&quot; ebenfalls erforderlich. Wenn der Computer, auf dem Sie den Befehl ausführen, kein Serverzertifikat besitzt, müssen Sie außerdem einen Wert für den Parameter &quot;WebCredential&quot; angeben.</p>
<p>Dieser Parameter ist nur dann nicht erforderlich, wenn Sie den Parameter &quot;TargetFqdn&quot; angeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Ein Objekt mit den Benutzeranmeldeinformationen für den Zugriff auf den Standortinformationsdienst. Dieses Objekt kann abgerufen werden, indem Sie das Cmdlet <strong>Get-Credential</strong> aufrufen und die entsprechenden Anmeldeinformationen angeben.</p>
<p>Dieser Parameter ist erforderlich, wenn die Parameter &quot;TargetFqdn&quot; und &quot;UserSipAddress&quot; angegeben werden und wenn der Computer, auf dem Sie das Cmdlet ausführen, kein Serverzertifikat besitzt.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Optional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Der Typ der beim Test zu verwendenden Authentifizierung. Zulässige Werte:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>BssId</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Basic Service Set Identifier (BSSID) eines Funkzugriffspunkts. Der Wert muss in der Form &quot;nn-nn-nn-nn-nn-nn&quot; vorliegen, z. B. &quot;12-34-56-78-90-ab&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>ChassisId</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die MAC-Adresse (Media Access Control) eines Netzwerkswitches. Der Wert muss in der Form &quot;nn-nn-nn-nn-nn-nn&quot; vorliegen, z. B. &quot;12-34-56-78-90-ab&quot;, oder in Form einer IP-Adresse.</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Dieser Parameter wird für LIS (Location Information Server) nicht unterstützt.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mac</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die MAC-Adresse des Portswitches. Der Wert muss in der Form &quot;nn-nn-nn-nn-nn-nn&quot; vorliegen, z. B. &quot;12-34-56-78-90-ab&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Diese Variable umfasst die beiden Methoden &quot;ToHTML&quot; und &quot;ToXML&quot;, mit deren Hilfe die Ausgabe entweder in einer HTML- oder XML-Datei gespeichert werden kann.</p>
<p>Verwenden Sie beispielsweise die folgende Syntax, um die Ausgabe in einer Protokollierungsvariablen mit dem Namen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Hinweis: Setzen Sie kein Dollarzeichen ($) vor den Variablennamen. Verwenden Sie einen ähnlichen Befehl wie den folgenden, um die in der Protokollierungsvariablen gespeicherten Informationen in einer HTML-Datei zu speichern:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Wählen Sie zum Speichern der in der Protokolliervariablen gespeicherten Informationen in einer XML-Datei einen Befehl wie den folgenden:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="even">
<td><p><em>PortId</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die ID des Ports, der dem zu testenden Standort zugeordnet ist. Bei diesem Wert kann es sich auch um eine MAC- oder IP-Adresse handeln.</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIdSubType</em></p></td>
<td><p>Optional</p></td>
<td><p>PortIDSubType</p></td>
<td><p>Der Untertyp des Ports. Dieser Wert kann als numerischer Wert oder als Zeichenfolge eingegeben werden, es muss sich jedoch um einen gültigen Untertyp handeln. Gültige Untertypen:</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Die Portnummer des Registrierungsdiensts.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnet</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die IP-Adresse eines Subnetzes. Dieser Wert wird als IPv4-Adresse (bei der Ziffern durch Punkte getrennt sind, z. B. 192.0.2.0) eingegeben.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse eines Remotebenutzers.</p>
<p>Wenn Sie für diesen Parameter einen Wert angeben, ist auch der Parameter &quot;TargetFqdn&quot; oder &quot;TargetUri&quot; erforderlich.</p>
<p>Dieser Parameter muss bei Verwendung des Parameters &quot;TargetFqdn&quot; nur dann angegeben werden, wenn Sie keine Benutzer für synthetische Transaktionen eingerichtet haben. Führen Sie das Cmdlet <strong>Get-CsHealthMonitoringConfiguration</strong> aus, um festzustellen, ob Benutzer für synthetische Transaktionen eingerichtet wurden.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Optional</p></td>
<td><p>PSCredential</p></td>
<td><p>Ein Objekt mit den Benutzeranmeldeinformationen für den Zugriff auf den Standortinformationsdienst. Dieses Objekt kann abgerufen werden, indem Sie das Cmdlet <strong>Get-Credential</strong> aufrufen und die entsprechenden Anmeldeinformationen angeben.</p>
<p>Dieser Parameter ist erforderlich, wenn die Parameter &quot;TargetUri&quot; und &quot;UserSipAddress&quot; angegeben werden und wenn der Computer, auf dem Sie den Befehl ausführen, kein Serverzertifikat besitzt.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit dem Cmdlet **Test-CsLisConfiguration** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)

