---
title: Test-CsPresence
TOCTitle: Test-CsPresence
ms:assetid: 09a5faf6-4e80-4a3b-ac84-aec9778ee9b5
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398148(v=OCS.15)
ms:contentKeyID: 49293115
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPresence

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet, ob sich ein Benutzer bei Lync Server anmelden, Anwesenheitsinformationen veröffentlichen und die von einem zweiten Benutzer veröffentlichten Anwesenheitsinformationen abonnieren kann. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsPresence -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-PublisherSipAddress <String>] [-RegistrarPort <Int32>] [-SubscriberSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPresence -PublisherCredential <PSCredential> -PublisherSipAddress <String> -SubscriberCredential <PSCredential> -SubscriberSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPresence [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-SubscriberSipAddress <String>]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel wird geprüft, ob sich ein vorkonfiguriertes Testbenutzerpaar am Pool "atl-cs-001.litwareinc.com" anmelden kann. Nachdem sich die Testbenutzer angemeldet haben, wird mit dem Cmdlet **Test-CsPresence** geprüft, ob die beiden Benutzer Anwesenheitsinformationen austauschen können. Dieser Befehl funktioniert nur, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Ist dies der Fall, ermittelt der Befehl, ob sich der erste Testbenutzer am System anmelden kann, und prüft anschließend, ob dieser Benutzer Anwesenheitsinformationen mit dem zweiten für den Pool definierten Testbenutzer austauschen kann.

Wurde keine Registrierung definiert, tritt beim Ausführen des Befehls ein Fehler auf, da der Befehl nicht ermitteln kann, welche Benutzer beim Test verwendet werden sollen. Wenn Sie für einen Pool keine Testbenutzer definiert haben, müssen Sie die Parameter "SubscriberSipAddress" und "PublisherSipAddress" sowie die entsprechenden Anmeldeinformationen der Benutzer angeben, die als Abonnent und Herausgeber der Anwesenheitsinformationen fungieren. Mit dem Cmdlet **Test-CsPresence** werden die Überprüfungen dann anhand der beiden angegebenen Benutzer durchgeführt.

    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com 

## BEISPIEL 2

Die Befehle in Beispiel 2 testen, ob sich ein Benutzerpaar ("litwareinc\\pilar" und "litwareinc\\kenmyer") bei Lync Server anmelden und Anwesenheitsinformationen austauschen kann. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Pilar Ackerman" enthält. (Da der Anmeldename "litwareinc\\pilar" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Pilar Ackerman" eingeben.) Das entstehende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert. Der zweite Befehl hat die gleiche Aufgabe, nur gibt dieser ein Objekt mit Anmeldeinformationen für das Konto "Ken Myer" zurück.

Anhand der beiden Objekte mit Anmeldeinformationen ermittelt der dritte Befehl im Beispiel, ob sich die beiden Benutzer bei Lync Server anmelden und Anwesenheitsinformationen austauschen können. Hierzu wird das Cmdlet **Test-CsPresence** mit den folgenden Parametern aufgerufen: "TargetFqdn" (FQDN des Registrierungsstellenpools); "SubscriberSipAddress" (SIP-Adresse für einen Testbenutzer); "SubscriberCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für diesen Benutzer); "PublisherSipAddress" (SIP-Adresse für den anderen Testbenutzer) und "PublisherCredential" (Windows PowerShell-Objekt mit den Anmeldeinformationen für den anderen Benutzer).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com -SubscriberSipAddress "sip:pilar@litwareinc.com" -SubscriberCredential $cred1 -PublisherSipAddress "sip:kenmyer@litwareinc.com" -PublisherCredential $cred2

## Detaillierte Beschreibung

Das Cmdlet **Test-CsPresence** ist ein Beispiel für eine synthetische Lync Server-Transaktion. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich ausführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern. Administratoren können mithilfe dieser für einen Pool konfigurierten Benutzerkonten eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer keine Chatnachrichten austauschen können, kann ein Administrator zum Diagnostizieren und Behandeln des Problems eine synthetische Transaktion unter Verwendung der beiden fraglichen Benutzerkonten ausführen (anstatt mithilfe eines Testkontopaars). Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

Mit dem Cmdlet **Test-CsPresence** wird ermittelt, ob sich ein Testbenutzerpaar bei Lync Server anmelden und Anwesenheitsinformationen austauschen kann. Hierzu meldet das Cmdlet die beiden Benutzer zunächst am System an. Wenn beide erfolgreich angemeldet werden können, fordert der erste Testbenutzer Anwesenheitsinformationen vom zweiten Benutzer an. Der zweite Benutzer veröffentlicht diese Informationen, und mit dem Cmdlet **Test-CsPresence** wird geprüft, ob die Informationen erfolgreich an den ersten Benutzer übermittelt wurden. Nach dem Austausch von Anwesenheitsinformationen werden beide Testbenutzer von Lync Server abgemeldet.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPresence"}

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
<td><p><em>PublisherCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das erste der beiden zu testenden Benutzerkonten. Bei dem an &quot;PublisherCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der Variablen &quot;$x&quot;:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben.</p>
<p>Die Anmeldeinformationen zum Herausgeber sind nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das zweite der beiden zu testenden Benutzerkonten. Bei dem an &quot;SubscriberCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\pilar&quot; zurück und speichert dieses Objekt in der Variablen &quot;$y&quot;:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben.</p>
<p>Die Abonnentenanmeldeinformationen sind nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
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
<td><p><em>PublisherSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse für das erste der beiden zu testenden Benutzerkonten. Beispiel: -PublisherSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;PublisherSipAddress&quot; muss auf das gleiche Benutzerkonto verweisen wie &quot;PublisherCredential&quot;.</p>
<p>Die Angabe der SIP-Adresse ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Der vom Registrierungsdienst verwendete SIP-Port. Dieser Parameter ist nicht erforderlich, wenn die Registrierung den Standardport 5061 verwendet.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse für das zweite der beiden zu testenden Benutzerkonten. Beispiel: -SubscriberSipAddress &quot;sip:pilar@litwareinc.com&quot;. Der Parameter &quot;SubscriberSipAddress&quot; muss auf das gleiche Benutzerkonto verweisen wie &quot;SubscriberCredential&quot;.</p>
<p>Die Angabe der SIP-Adresse ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsPresence** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsPresence** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsRegistration](test-csregistration.md)

