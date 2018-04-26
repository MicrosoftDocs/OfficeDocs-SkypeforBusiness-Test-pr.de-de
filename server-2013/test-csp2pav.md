---
title: Test-CsP2PAV
TOCTitle: Test-CsP2PAV
ms:assetid: acb01fb7-4685-4f38-a724-8c2ae8e0219a
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412821(v=OCS.15)
ms:contentKeyID: 49295070
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsP2PAV

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet, ob ein Benutzerpaar einen Peer-zu-Peer-Audioanruf/-Videoanruf (A/V) durchführen kann. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsP2PAV -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsP2PAV -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsP2PAV [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird geprüft, ob sich ein vorkonfiguriertes Testbenutzerpaar beim Pool "atl-cs-001.litwareinc.com" anmelden und dann am Peer-zu-Peer-Audio-/Videoanruf teilnehmen kann. Dieser Befehl ist nur erfolgreich, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Ist dies der Fall, ermittelt der Befehl, ob sich diese beiden Benutzer beim System anmelden und ggf. einen Audio-/Videoanruf durchführen können.

Wurden keine Testbenutzer definiert, kann der Befehl nicht ausgeführt werden, da nicht ermittelt werden kann, welche Benutzer für den Test verwendet werden sollen. Wenn Sie für einen Pool keine Testbenutzer definiert haben, müssen Sie die Parameter "SenderSipAddress" und "ReceiverSipAddress" sowie die entsprechenden Anmeldeinformationen der Benutzer angeben, die Chatnachrichten austauschen. Mit dem Cmdlet **Test-CsP2PAV** werden die Überprüfungen dann anhand der beiden angegebenen Benutzer durchgeführt.

    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com 

## BEISPIEL 2

Mit den Befehlen in Beispiel 2 wird getestet, ob sich ein Benutzerpaar ("litwareinc\\pilar" und "litwareinc\\kenmyer") bei Lync Server anmelden und einen Peer-zu-Peer-Audio-/Videoanruf durchführen kann. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Pilar Ackerman" enthält. (Da der Anmeldename "litwareinc\\pilar" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Pilar Ackerman" eingeben.) Das resultierende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert. Der zweite Befehl hat die gleiche Aufgabe, nur gibt dieser ein Objekt mit Anmeldeinformationen für das Konto "Ken Myer" zurück.

Anhand der beiden Objekte mit Anmeldeinformationen wird mit dem dritten Befehl im Beispiel ermittelt, ob sich die beiden Benutzer bei Lync Server anmelden und einen Peer-zu-Peer-Audio-/Videoanruf durchführen können. Hierzu wird das Cmdlet **Test-CsP2PAV** mit den folgenden Parametern aufgerufen: "TargetFqdn" (FQDN des Registrierungsstellenpools), "SenderSipAddress" (SIP-Adresse für den ersten Testbenutzer), "SenderCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für diesen Benutzer), "ReceiverSipAddress " (SIP-Adresse für den anderen Testbenutzer) und "ReceiverCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für den anderen Benutzer).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Detaillierte Beschreibung

Das Cmdlet **Test-CsP2PAV** ist ein Beispiel für eine "synthetische Transaktion" in Lync Server. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie z. B. das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich durchführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit den zwei betreffenden Benutzerkonten (anstelle von zwei Testkonten) durchführen und versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

Mit dem Cmdlet **Test-CsP2PAV** wird bestimmt, ob zwei Testbenutzer an einer Peer-zu-Peer-Audiounterhaltung/-Videounterhaltung (A/V) teilnehmen können. Mit dem Cmdlet werden zum Testen dieses Szenarios zunächst die zwei Benutzer bei Lync Server angemeldet. Unter der Voraussetzung, dass die zwei Anmeldungen erfolgreich sind, lädt der erste Benutzer den zweiten Benutzer zu einem A/V-Anruf ein. Der zweite Benutzer akzeptiert den Anruf, und die Verbindung der beiden Benutzer wird getestet. Der Anruf wird dann beendet, und die Testbenutzer werden vom System abgemeldet.

Mit dem Cmdlet **Test-CsP2PAV** wird kein tatsächlicher A/V-Anruf durchgeführt, und es werden keine Multimediainformationen zwischen den Testbenutzern ausgetauscht. Mit dem Cmdlet wird stattdessen einfach überprüft, ob die entsprechenden Verbindungen hergestellt werden und die zwei Benutzer einen solchen Anruf durchführen können.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsP2PAV"}

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
<td><p>Zeichenfolge</p></td>
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
<td><p>Zeichenfolge</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
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
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse für das zweite der beiden zu testenden Benutzerkonten. Beispiel: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;SenderSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;SenderCredential&quot; verweisen.</p>
<p>Die Angabe der SIP-Adresse ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsP2PAV** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsP2PAV** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsAVConference](test-csavconference.md)

