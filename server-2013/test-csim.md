---
title: Test-CsIM
TOCTitle: Test-CsIM
ms:assetid: 2fdab54c-5ec4-4db5-b29c-a3efaae68f66
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425802(v=OCS.15)
ms:contentKeyID: 49293570
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsIM

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet, ob zwei Benutzer Chatnachrichten austauschen können. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-EmailHost <String>] [-Force <SwitchParameter>] [-IsSsl <$true | $false>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Password <String>] [-Port <UInt16>] [-TestLegalIntercept <SwitchParameter>] [-Username <String>] [-WaitSeconds <Int16>]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel wird geprüft, ob sich ein vorkonfiguriertes Testbenutzerpaar am Pool "atl-cs-001.litwareinc.com" anmelden und dann Chatnachrichten austauschen kann. Dieser Befehl funktioniert nur, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Ist dies der Fall, ermittelt der Befehl, ob sich diese beiden Benutzer am System anmelden und ggf. Chatnachrichten austauschen können.

Wurden keine Testbenutzer definiert, kann der Befehl nicht ausgeführt werden, da nicht ermittelt werden kann, welcher Benutzer beim Test verwendet werden sollen. Wenn Sie für einen Pool keine Registrierung definiert haben, müssen Sie die Parameter "SenderSipAddress" und "ReceiverSipAddress" sowie die entsprechenden Anmeldeinformationen der Benutzer angeben, die an der Chatnachrichtensitzung teilnehmen. Das Cmdlet **Test-CsIM** führt die Überprüfungen dann anhand der beiden angegebenen Benutzer durch.

    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com

## BEISPIEL 2

Die Befehle in Beispiel 2 testen, ob sich ein Benutzerpaar ("litwareinc\\pilar" und "litwareinc\\kenmyer") bei Lync Server anmelden und Chatnachrichten austauschen kann. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Pilar Ackerman" enthält. (Da der Anmeldename "litwareinc\\pilar" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Pilar Ackerman" eingeben.) Das entstehende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert. Der zweite Befehl hat die gleiche Aufgabe, nur gibt dieser ein Objekt mit Anmeldeinformationen für das Konto "Ken Myer" zurück.

Anhand der beiden Objekte mit Anmeldeinformationen ermittelt der dritte Befehl im Beispiel, ob sich die beiden Benutzer bei Lync Server anmelden und Chatnachrichten austauschen können. Zu diesem Zweck wird das Cmdlet **Test-CsIM** mit den folgenden Parametern aufgerufen: "TargetFqdn" (FQDN des Registrierungsstellenpools); "SenderSipAddress" (SIP-Adresse für den ersten Testbenutzer); "SenderCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für diesen Benutzer); "-ReceiverSipAddress " (SIP-Adresse für den anderen Testbenutzer) und "ReceiverCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für den anderen Benutzer).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Detaillierte Beschreibung

Das Cmdlet **Test-CsIM** ist ein Beispiel für eine synthetische Lync Server-Transaktion. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich ausführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer keine Chatnachrichten austauschen können, kann ein Administrator eine synthetische Transaktion anhand der beiden fraglichen Benutzerkonten durchführen (statt anhand eines Testkontopaars), um das Problem zu ermitteln und zu lösen. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie die Anmeldeinformationen für jeden Benutzer angeben müssen.

Das Cmdlet **Test-CsIM** versucht zunächst, zwei Testbenutzer bei Lync Server anzumelden. Wenn die zwei Anmeldungen erfolgreich waren, initiiert das Cmdlet daraufhin eine Chatnachrichtensitzung (Instant Messaging) zwischen den beiden Testbenutzern. (Benutzer 1 lädt Benutzer 2 zu einer Chatnachrichtensitzung ein, und Benutzer 2 nimmt die Einladung an.) Nachdem geprüft wurde, ob Nachrichten zwischen den beiden Benutzern ausgetauscht werden können, beendet das Cmdlet **Test-CsIM** die Chatnachrichtensitzung und meldet beide Benutzer vom System ab.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsIM"}

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
<p>Die Angabe der Empfängeranmeldeinformationen ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das zweite der beiden zu testenden Benutzerkonten. Bei dem an &quot;SenderCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der Variablen &quot;$x&quot;:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben.</p>
<p>Die Angabe der Senderanmeldeinformationen ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) des zu testenden Pools.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Optional</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>Art der im Test verwendeten Authentifizierung. Zulässige Werte:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>EmailHost</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>E-Mail-Host für den Benutzer, der zum Testen von Legal Intercept verwendet wird. Beispiel:</p>
<p>-EmailHost &quot;litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>IsSsl</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Mit &quot;True&quot; wird angegeben, dass der Test unter Verwendung des SSL-Protokolls (Secure Socket Layer-Protokoll) ausgeführt wird.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Diese Variable umfasst die beiden Methoden &quot;ToHTML&quot; und &quot;ToXML&quot;, mit deren Hilfe die Ausgabe entweder in einer HTML- oder in einer XML-Datei gespeichert werden kann.</p>
<p>Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in einer Protokollierungsvariablen mit dem Namen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Hinweis: Stellen Sie dem Variablennamen kein Dollarzeichen ($) voran. Falls Sie die Informationen aus der Protokolliervariablen in einer HTML-Datei speichern möchten, verwenden Sie einen Befehl wie den folgenden:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Falls Sie die Informationen aus der Protokolliervariablen in einer XML-Datei speichern möchten, verwenden Sie einen Befehl wie den folgenden:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$Testausgabe&quot; zu speichern:</p>
<p>-OutVerboseVariable Testausgabe</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="even">
<td><p><em>Password</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Kennwort für den Benutzer, der zum Testen von Legal Intercept verwendet wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>Optional</p></td>
<td><p>UInt16</p></td>
<td><p>Für Legal Intercept verwendeter Port.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse für das erste der beiden zu testenden Benutzerkonten. Beispiel: -ReceiverSipAddress &quot;sip:jhaas@litwareinc.com&quot;. Der Parameter &quot;ReceiverSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;ReceiverCredential&quot; verweisen.</p>
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
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse für das zweite der beiden zu testenden Benutzerkonten. Beispiel: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;SenderSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;SenderCredential&quot; verweisen.</p>
<p>Die Angabe der SIP-Adresse ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestLegalIntercept</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Mit dieser Option wird &quot;Test-CsIM&quot; angewiesen, den Legal Intercept-Dienst für den angegebenen Benutzer zu testen.</p></td>
</tr>
<tr class="even">
<td><p><em>Username</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Benutzername des Benutzers, der zum Testen von Legal Intercept verwendet wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitSeconds</em></p></td>
<td><p>Optional</p></td>
<td><p>Int16</p></td>
<td><p>Gibt an, wie lange vom System auf eine Reaktion des Legal Intercept-Diensts gewartet werden soll (in Sekunden).</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsIM** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsIM** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsGroupIM](test-csgroupim.md)

