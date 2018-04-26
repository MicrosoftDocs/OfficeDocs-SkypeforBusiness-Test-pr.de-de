---
title: Test-CsPstnOutboundCall
TOCTitle: Test-CsPstnOutboundCall
ms:assetid: 12d940c3-8526-4c8f-8dc1-3fe65a3211bc
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398207(v=OCS.15)
ms:contentKeyID: 49293240
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnOutboundCall

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet, ob ein Benutzer einen Anruf an eine Telefonnummer im Telefonfestnetz (Public Switched Telephone Network, PSTN) tätigen kann. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsPstnOutboundCall -TargetPstnPhoneNumber <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall -TargetFqdn <String> -TargetPstnPhoneNumber <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel wird überprüft, ob ein vorab konfigurierter Testbenutzer sich beim Pool "atl-cs-001.litwareinc.com" anmelden und einen Telefonanruf über das PSTN-Gateway tätigen kann. Dieser Befehl funktioniert nur, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Ist dies der Fall, ermittelt der Befehl, ob der erste Testbenutzer sich beim System anmelden und ggf. einen Telefonanruf an ein Telefon im Telefonfestnetz tätigen kann.

Wurden keine Testbenutzer definiert, kann der Befehl nicht ausgeführt werden, da nicht ermittelt werden kann, welcher Benutzer beim Test verwendet werden sollen. Wenn Sie für einen Pool keine Testbenutzer definiert haben, müssen Sie den Parameter "UserSipAddress" sowie die entsprechenden Anmeldeinformationen des Benutzerkontos für den Test angeben. Mit dem Cmdlet **Test-CsPstnOutboundCall** werden die Überprüfungen dann mit dem angegebenen Benutzer durchgeführt.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" 

## BEISPIEL 2

Mit den Befehlen im zweiten Beispiel wird getestet, ob ein Testbenutzer ("litwareinc\\kenmyer") sich bei Lync Server anmelden und dann über das PSTN-Gateway einen Anruf tätigen kann. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Ken Myer" enthält. (Da der Anmeldename "litwareinc\\kenmyer" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Ken Myer" eingeben.) Das entstehende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert.

Anhand des Objekts mit Anmeldeinformationen ermittelt der zweite Befehl im Beispiel, ob der Testbenutzer sich bei Lync Server anmelden und dann einen Telefonanruf an die Zieltelefonnummer (+15551234567) durchführen kann. Hierzu wird das Cmdlet **Test-CsPstnOutboundCall** mit folgenden Parametern aufgerufen: "TargetFqdn" (der FQDN des Registrierungsstellenpools), "UserSipAddress" (die SIP-Adresse des Benutzers, der den Anruf tätigt), "UserCredential" (das Windows PowerShell-Objekt mit Anmeldeinformationen für den Testbenutzer) und "TargetPstnPhoneNumber" (die angerufene Telefonnummer).

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## BEISPIEL 3

Im dritten Beispiel wird gezeigt, wie das Cmdlet **Test-CsPstnOutboundCall** im Serverplattformmodus verwendet werden kann. In diesem Modus wird die SIP-Adresse des Benutzers angegeben, nicht jedoch die Anmeldeinformationen des Benutzers. Bei dieser Ausführungsart verwendet Lync Server Zertifikate für die Authentifizierung des Testbenutzers.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress sip:kenmyer@litwareinc.com -TargetPstnPhoneNumber "+15551234567"

## Detaillierte Beschreibung

Das Cmdlet **Test-CsPstnOutboundCall** ist ein Beispiel für eine synthetische Lync Server-Transaktion. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich ausführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit den zwei betreffenden Benutzerkonten (anstelle von zwei Testkonten) durchführen und versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

"Test-CsPstnOutboundCall" kann auch im Serverplattformmodus verwendet werden. In diesem Fall müssen Sie nur die SIP-Adresse eines Benutzers angeben. Lync Server verwendet dann Zertifikate zur Authentifizierung dieses Benutzers.

Beim Ausführen des Cmdlets **Test-CsPstnOutboundCall** versucht das Cmdlet zunächst, den Testbenutzer bei Lync Server anzumelden. Nach erfolgreicher Anmeldung versucht das Cmdlet, einen Telefonanruf über das PSTN-Gateway zu tätigen. Dieser Telefonanruf wird mithilfe der Wähleinstellungen, der VoIP-Richtlinie und anderer Richtlinien und Einstellungen durchgeführt, die dem Testkonto zugewiesen sind. Wenn der Anruf beantwortet wird, sendet das Cmdlet DTMF-Codes (Dual-Tone Multifrequency) über das Netzwerk, um die Medienkonnektivität zu überprüfen.

Im Rahmen der Tests wird mit dem Cmdlet **Test-CsPstnOutboundCall** ein tatsächlicher Telefonanruf durchgeführt: Das angerufene Telefon klingelt, und der Anruf muss für einen erfolgreichen Abschluss des Tests entgegengenommen werden. Dieser Anruf muss zudem manuell vom Administrator beendet werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnOutboundCall"}

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
<td><p>Vollqualifizierter Domänenname (FQDN) des zu testenden Pools.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die PSTN-Telefonnummer, die während des Tests angerufen werden soll. Die Zieltelefonnummer wird am besten im E.164-Format angegeben, d. h. die Nummer sieht in etwa wie folgt aus: &quot;+14255551298&quot;. Die Nummer beginnt mit einem Pluszeichen (+), gefolgt vom Länder-/Regionscode (1), der Ortskennzahl (425) und der Rufnummer (5551298). Verwenden Sie beim Festlegen von Telefonnummern keine Bindestriche, Klammern oder andere Zeichen.</p>
<p>Wenn Sie nicht das E.164-Format verwenden, werden die Wähleinstellungen des Testbenutzers an die Nummer angehängt. Lync Server verwendet in diesem Fall die Wähleinstellungen, um die Nummer in das E.164-Format zu normalisieren. Ist keine Normalisierung der Nummer möglich, kann der Anruf nicht durchgeführt werden, und der Test ist nicht erfolgreich.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das Konto, das getestet wird. Bei dem an &quot;UserCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der Variablen &quot;$x&quot;:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben.</p>
<p>Dieser Parameter ist nicht erforderlich, wenn der Befehl Testbenutzer verwendet, die mit den Cmdlets vom Typ &quot;CsHealthMonitoringConfiguration&quot; konfiguriert wurden. Der Parameter ist ebenfalls nicht erforderlich, wenn der Test im Serverplattformmodus ausgeführt wird. In diesem Fall versucht Lync Server, den Benutzer mithilfe von Zertifikaten zu authentifizieren.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Optional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Art der im Test verwendeten Authentifizierung. Zulässige Werte:</p>
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
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$Testausgabe&quot; zu speichern:</p>
<p>-OutVerboseVariable Testausgabe</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Der vom Registrierungsdienst verwendete SIP-Port. Dieser Parameter ist nicht erforderlich, wenn die Registrierung den Standardport 5061 verwendet.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>SIP-Adresse für das Benutzerkonto, das getestet wird. Beispiel: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;UserSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;UserCredential&quot; verweisen.</p>
<p>Dieser Parameter ist nicht erforderlich, wenn der Befehl Testbenutzer verwendet, die mit den CsHealthMonitoringConfiguration-Cmdlets konfiguriert wurden.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsPstnOutboundCall** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsPstnOutboundCall** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsPstnPeerToPeerCall](test-cspstnpeertopeercall.md)

