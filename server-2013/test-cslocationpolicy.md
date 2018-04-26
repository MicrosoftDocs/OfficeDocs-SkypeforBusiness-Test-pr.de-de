---
title: Test-CsLocationPolicy
TOCTitle: Test-CsLocationPolicy
ms:assetid: 49f7d148-d46d-4bcc-af9d-6a3a0fdde8ee
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425962(v=OCS.15)
ms:contentKeyID: 49293910
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLocationPolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Führt einen Test zum Bestimmen der Standortrichtlinie aus, die basierend auf den in den Parameterwerten angegebenen Kriterien verwendet wird. Die Standortrichtlinie enthält die Einstellungen, die bestimmen, ob und wie die erweiterten Notfalldienste (E9-1-1) zum Tragen kommen. Mit E9-1-1 können Notrufoperatoren den geografischen Standort des Anrufers ermitteln. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsLocationPolicy -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Subnet <String>]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die Standortrichtlinie des aktuellen Benutzers (bzw. aktuell konfigurierten Benutzers) bestimmt. "TargetFqdn" ist erforderlich.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com 

## BEISPIEL 2

Die erste Zeile in Beispiel 2 ist ein Aufruf des Windows PowerShell-Cmdlets **Get-Credential**. Dieses Cmdlet ruft die Benutzeranmeldeinformationen ab und gibt diese als sicheres Objekt zurück. Der einzige Parameter, der für dieses Cmdlet angegeben wird, ist die Benutzer-ID. Bei Ausführung dieses Cmdlets wird ein Dialogfeld geöffnet, das mit der Benutzer-ID vorab ausgefüllt wird und ein Textfeld aufweist, das die Eingabe des Benutzerkennworts ermöglicht. Diese Benutzeranmeldeinformationen werden in der Variablen "$cred" gespeichert.

In Zeile 2 wird das Cmdlet **Test-CsLocationPolicy** aufgerufen. Wie in Beispiel 1 muss "TargetFqdn" angegeben werden. Doch in diesem Beispiel wird nicht der vorkonfigurierte Benutzer verwendet, sondern der Test für einen Benutzer mit der SIP-Adresse "kenmyer@litwareinc.com" ausgeführt. Dieser Wert (mit dem Präfix "sip:") wird an den Parameter "UserSipAddress", und die (in der Variablen "$cred") gespeicherten Anmeldeinformationen werden an den Parameter "UserCredential" übergeben.

    $cred = Get-Credential "litwareinc\kenmyer"
    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred -UserSipAddress "sip:kenmyer@litwareinc.com"

## BEISPIEL 3

Dieses Beispiel ähnelt Beispiel 2, doch es werden keine Benutzeranmeldeinformationen angegeben. Wenn das Cmdlet **Test-CsLocationPolicy** ohne Angabe von Benutzeranmeldeinformationen aufgerufen wird, dient das Serverzertifikat des Computers, auf dem das Cmdlet ausgeführt wird, zum Authentifizieren und Ermitteln der Standortrichtlinie des Benutzers. Wenn der Computer kein Serverzertifikat hat, müssen Sie Anmeldeinformationen angeben (siehe Beispiel 2). Um zu ermitteln, ob es ein Serverzertifikat für den Computer gibt, rufen Sie das Cmdlet **Get-CsCertificate** auf.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com"

## BEISPIEL 4

In diesem Beispiel wird die Standortrichtlinie des Subnetzes mit der ID 172.15.11.0 bestimmt. Wenn dem Subnetz keine Standortrichtlinie zugewiesen ist, wird die Standortrichtlinie für den aktuell konfigurierten Benutzer abgerufen.

Hinweis: Eine Standortrichtlinie wird für ein Subnetz festgelegt, indem der Parameter "LocationPolicy" des Cmdlets **Set-CsNetworkSite** auf die Standortrichtlinien-ID festgelegt wird und anschließend der Parameter "NetworkSiteId" des Cmdlets **Set-CsNetworkSubnet** auf die ID dieses Standorts festgelegt wird. Beispiel:

Set-CsNetworkSite Portland –LocationPolicy Reno

Set-CsNetworkSubnet 175.15.11.0 –NetworkSiteID Portland

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -Subnet 172.15.11.0

## Detaillierte Beschreibung

Mit der Standortrichtlinie werden Einstellungen im Zusammenhang mit der E9-1-1-Funktion und dem Clientstandort zugewiesen. Die Standortrichtlinie ermittelt, ob E9-1-1 für einen Benutzer aktiviert ist, und legt ggf. das Verhalten eines Notrufs fest. Sie können mit der Standortrichtlinie beispielsweise definieren, welche Nummer als Notrufnummer betrachtet wird, ob die Abteilung für Unternehmenssicherheit automatisch benachrichtigt werden soll, und wie der Anruf weitergeleitet werden soll. Dieses Cmdlet gibt Informationen zur Standortrichtlinie zurück, die genutzt werden, wenn ein bestimmter Client in einem bestimmten Pool, Subnetz oder einen bestimmten Switch oder Funkzugriffspunkt einen Anruf tätigt.

Wenn im Aufruf dieses Cmdlets kein Benutzer angegeben ist, wird der gegenwärtig konfigurierte Benutzer getestet. Rufen Sie das Cmdlet **Get-CsHealthMonitoringConfiguration** auf, um den aktuell konfigurierten Benutzer zu bestimmen. Rufen Sie das Cmdlet **Set-CsHealthMonitoringConfiguration** auf, um den konfigurierten Benutzer festzulegen.

Wenn eine Standortrichtlinie für den Benutzer oder das Subnetz gefunden wurde, hat der Test Erfolg. Zu den standardmäßig zurückgegebenen Informationen gehört der Name der Standortrichtlinie (falls eine benutzerbasierte Richtlinie zugewiesen ist) und ob der Benutzer oder das Subnetz für E9-1-1 aktiviert ist. Fügen Sie den allgemeinen Windows PowerShell-Parameter "Verbose" hinzu, um zusätzliche Informationen zum Test abzurufen.

Sie können Standortrichtlinien für Benutzer oder Netzwerksubnetze testen. Wenn Sie den Test für ein Subnetz ausführen (indem Sie einen Wert für den Parameter "Subnet" angeben), versucht das Cmdlet, die Standortrichtlinie für dieses Subnetz aufzulösen. Wenn dem Subnetz keine Standortrichtlinie zugewiesen ist, wird die Standortrichtlinie für den konfigurierten Benutzer abgerufen. Wenn die Subnetzrichtlinie erfolgreich abgerufen wird, enthält die Ausgabe den mit "subnet-tagid" beginnenden Wert "LocationPolicyTagID". Wenn keine Standortrichtlinie für das Subnetz gefunden wurde, beginnt die "LocationPolicyTagID" mit "user-tagid".

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Test-CsLocationPolicy** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLocationPolicy"}

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
<td><p>Der vollqualifizierte Domänenname (FQDN) des Pools, in dem sich der angegebene Benutzer bzw. das Subnetz befindet. (Ist kein Benutzer angegeben, wird der vorkonfigurierte oder aktuelle Benutzer angenommen.)</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Ein Objekt mit Benutzer-ID und Kennwort des Benutzerkontos, dessen Standortrichtlinie getestet wird. Ein Objekt mit Anmeldeinformationen kann abgerufen werden, indem das Cmdlet <strong>Get-Credential</strong> aufgerufen wird, die entsprechenden Informationen eingegeben werden und die Ausgabe in einer Variablen gespeichert wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Optional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Art der im Test verwendeten Authentifizierung. Zulässige Werte:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Diese Variable umfasst die beiden Methoden &quot;ToHTML&quot; und &quot;ToXML&quot;, mit deren Hilfe die Ausgabe entweder in einer HTML- oder in einer XML-Datei gespeichert werden kann.</p>
<p>Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in einer Protokollierungsvariablen mit dem Namen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Hinweis: Stellen Sie dem Variablennamen kein Dollarzeichen ($) voran. Falls Sie die Informationen aus der Protokolliervariablen in einer HTML-Datei speichern möchten, verwenden Sie einen Befehl wie den folgenden:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Falls Sie die Informationen aus der Protokolliervariablen in einer XML-Datei speichern möchten, verwenden Sie einen Befehl wie den folgenden:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$Testausgabe&quot; zu speichern:</p>
<p>-OutVerboseVariable Testausgabe</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Die Portnummer des Registrierungsdiensts.</p></td>
</tr>
<tr class="even">
<td><p><em>Subnet</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die ID (IP-Adresse) des Netzwerksubnetzes, für das Sie die Standortrichtlinie testen möchten.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse des Benutzers, dessen Standortrichtlinie Sie testen möchten. Diese muss das Format &quot;sip:&lt;Benutzer-ID&gt;&quot; haben, z. B. sip:kenmyer@litwareinc.com.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Das Cmdlet **Test-CsLocationPolicy** gibt eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

