---
title: Test-CsPstnPeerToPeerCall
TOCTitle: Test-CsPstnPeerToPeerCall
ms:assetid: 839cf83f-b667-4cbe-b1ab-28f54a8a9d0b
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398662(v=OCS.15)
ms:contentKeyID: 49294607
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnPeerToPeerCall

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet die Fähigkeit zweier Benutzer, einen Peer-zu-Peer-Anruf über das PSTN-Gateway (Public Switched Telephone Network) zu tätigen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsPstnPeerToPeerCall -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird geprüft, ob sich ein vorkonfiguriertes Testbenutzerpaar beim Pool "atl-cs-001.litwareinc.com" anmelden kann. Nachdem sich die Testbenutzer angemeldet haben, wird mit dem Cmdlet **Test-CsPstnPeerToPeerCall** geprüft, ob die beiden Benutzer einen Peer-zu-Peer-Anruf über das PSTN-Gateway tätigen können. Dieser Befehl ist nur erfolgreich, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Ist dies der Fall, ermittelt der Befehl, ob sich der erste Testbenutzer beim System anmelden kann, und prüft anschließend, ob dieser Benutzer den zweiten für den Pool definierten Benutzer anrufen kann.

Wurden keine Testbenutzer definiert, kann der Befehl nicht ausgeführt werden, da nicht ermittelt werden kann, welcher Benutzer beim Test verwendet werden sollen. Wenn Sie keine Testbenutzer für einen Pool definiert haben und nicht den Serverplattformmodus verwenden, müssen Sie die Parameter "SenderSipAddress" und "ReceiverSipAddress" sowie die entsprechenden Anmeldeinformationen für die Benutzer angeben, die als Testkonten dienen. Mit dem Cmdlet **Test-CsPstnPeerToPeerCall** werden die Überprüfungen dann anhand der beiden angegebenen Benutzer durchgeführt.

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com 

## BEISPIEL 2

Mit den Befehlen in Beispiel 2 wird getestet, ob sich ein Benutzerpaar ("litwareinc\\pilar" und "litwareinc\\kenmyer") bei Lync Server anmelden und einen Peer-zu-Peer-Anruf über das PSTN-Gateway durchführen kann. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Pilar Ackerman" enthält. (Da der Anmeldename "litwareinc\\pilar" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Pilar Ackerman" eingeben.) Das resultierende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert. Der zweite Befehl hat die gleiche Aufgabe, nur gibt dieser ein Objekt mit Anmeldeinformationen für das Konto "Ken Myer" zurück.

Anhand der beiden Objekte mit Anmeldeinformationen wird mit dem dritten Befehl im Beispiel ermittelt, ob sich die beiden Benutzer bei Lync Server anmelden und einen Peer-zu-Peer-Anruf über das PSTN-Gateway durchführen können. Hierzu wird das Cmdlet **Test-CsPstnPeerToPeerCall** mit den folgenden Parametern aufgerufen: "TargetFqdn" (FQDN des Registrierungsstellenpools), "SenderSipAddress" (SIP-Adresse für den ersten Testbenutzer), "SenderCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für denselben Benutzer), "-ReceiverSipAddress" (SIP-Adresse für den anderen Testbenutzer) und "ReceiverCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für den anderen Benutzer).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## BEISPIEL 3

In Beispiel 3 wird gezeigt, wie das Cmdlet "Test-CsPstnPeerToPeerCall" im Serverplattformmodus verwendet werden kann. In diesem Modus werden die SIP-Adressen der Testbenutzer angegeben, die Anmeldeinformationen der Benutzer werden jedoch nicht eingeschlossen. Bei dieser Ausführung verwendet Lync Server Zertifikate für die Authentifizierung der beiden Testbenutzer.

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" 

## Detaillierte Beschreibung

Das Cmdlet **Test-CsPstnPeerToPeerCall** ist ein Beispiel für eine "synthetische Transaktion" in Lync Server. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie z. B. das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich durchführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die Cmdlets vom Typ **CsHealthMonitoringConfiguration**, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit den zwei betreffenden Benutzerkonten (anstelle von zwei Testkonten) durchführen und versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

Das Cmdlet **Test-CsPstnPeerToPeerCall** kann auch im Serverplattformmodus verwendet werden. In diesem Fall müssen Sie nur die SIP-Adresse der Benutzer angeben, und Lync Server verwendet Zertifikate zur Authentifizierung dieser Benutzer.

Wenn Sie das Cmdlet **Test-CsPstnPeerToPeerCall** aufrufen, wird zunächst versucht, die zwei Testbenutzer bei Lync Server anzumelden. Sind diese Anmeldungen erfolgreich, initiiert das Cmdlet einen Anruf von Benutzer 1 bei Benutzer 2, wobei der Anruf über das PSTN-Gateway erfolgt. Das Cmdlet **Test-CsPstnPeerToPeerCall** tätigt diesen Anruf unter Verwendung der Wähleinstellungen, VoIP-Richtlinie und weiteren Richtlinien sowie Konfigurationseinstellungen, die für den Testbenutzer festgelegt wurden. Verläuft der Test wie geplant, überprüft das Cmdlet, ob Benutzer 2 den Anruf beantworten konnte. Anschließend werden beide Testkonten vom System abgemeldet.

Das Cmdlet **Test-CsPstnPeerToPeerCall** tätigt einen tatsächlichen Telefonanruf, der bestätigt, dass eine Verbindung hergestellt werden kann. Außerdem werden DTMF-Codes (Mehrfrequenzverfahren) über das Netzwerk übertragen, um festzustellen, ob Medien über die Verbindung gesendet werden können. Allerdings wird der Anruf vom Cmdlet selbst angenommen, und es nicht erforderlich, den Anruf manuell zu beenden. (Es muss also niemand den Anruf entgegennehmen und anschließend auflegen.)

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnPeerToPeerCall"}

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das erste der beiden zu testenden Benutzerkonten. Bei dem an &quot;ReceiverCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\pilar&quot; zurück und speichert dieses Objekt in der Variablen &quot;$y&quot;:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben.</p>
<p>Die Angabe der Empfängeranmeldeinformationen ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen oder wenn Sie den Serverplattformmodus verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das zweite der beiden zu testenden Benutzerkonten. Bei dem an &quot;SenderCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der Variablen &quot;$x&quot;:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben.</p>
<p>Die Angabe der Senderanmeldeinformationen ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen oder wenn Sie den Serverplattformmodus verwenden.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>String</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) des zu testenden Pools.</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Diese Variable umfasst die beiden Methoden &quot;ToHTML&quot; und &quot;ToXML&quot;, mit deren Hilfe die Ausgabe entweder in einer HTML- oder XML-Datei gespeichert werden kann.</p>
<p>Verwenden Sie beispielsweise die folgende Syntax, um die Ausgabe in einer Protokollierungsvariablen mit dem Namen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Hinweis: Setzen Sie kein Dollarzeichen ($) vor den Variablennamen. Verwenden Sie einen ähnlichen Befehl wie den folgenden, um die in der Protokollierungsvariablen gespeicherten Informationen in einer HTML-Datei zu speichern:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Verwenden Sie einen ähnlichen Befehl wie den folgenden, um die in der Protokollierungsvariablen gespeicherten Informationen in einer XML-Datei zu speichern:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die SIP-Adresse für das erste der beiden zu testenden Benutzerkonten. Beispiel: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Der Parameter &quot;ReceiverSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;ReceiverCredential&quot; verweisen.</p>
<p>Die Angabe der SIP-Adresse ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Der vom Registrierungsdienst verwendete SIP-Port. Dieser Parameter ist nicht erforderlich, wenn die Registrierung den Standardport 5061 verwendet.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die SIP-Adresse für das zweite der beiden zu testenden Benutzerkonten. Beispiel: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;SenderSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;SenderCredential&quot; verweisen.</p>
<p>Die Angabe der SIP-Adresse ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsPstnPeerToPeerCall** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsPstnPeerToPeerCall** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsPstnOutboundCall](test-cspstnoutboundcall.md)

