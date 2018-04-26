---
title: Test-CsGroupIM
TOCTitle: Test-CsGroupIM
ms:assetid: 1e73fd7a-5727-4688-8d4c-a3107c3985e9
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398273(v=OCS.15)
ms:contentKeyID: 49293372
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsGroupIM

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet die Fähigkeit zweier Benutzer, eine Chatkonferenz durchzuführen. Das Cmdlet **Test-CsGroupIM** ist eine "synthetische Transaktion", also eine Simulation gängiger Lync Server-Aktivitäten, die zur Integritäts- und Leistungsüberwachung verwendet werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsGroupIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsGroupIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsGroupIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel wird geprüft, ob ein vorkonfiguriertes Testbenutzerpaar sich beim Pool "atl-cs-001.litwareinc.com" anmelden und an einer Instant Messaging-Konferenz teilnehmen kann. Dieser Befehl funktioniert nur, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Sofern Testbenutzer konfiguriert wurden, wird mit dem Befehl geprüft, ob sich die beiden Benutzer beim System anmelden und an einer Instant Messaging-Konferenz teilnehmen können.

Wurden keine Testbenutzer definiert, kann der Befehl nicht ausgeführt werden, da nicht ermittelt werden kann, welche Benutzer beim Test verwendet werden sollen. Wenn Sie für einen Pool keine Testbenutzer definiert haben, müssen Sie die Parameter "SenderSipAddress" und "ReceiverSipAddress" sowie die entsprechenden Anmeldeinformationen der Benutzer für den Test angeben. Mit dem Cmdlet **Test-CsGroupIM** werden die Überprüfungen dann mit den beiden angegebenen Benutzern durchgeführt.

    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com

## BEISPIEL 2

Mit den Befehlen im zweiten Beispiel wird getestet, ob zwei Benutzer ("litwareinc\\pilar" und "litwareinc\\kenmyer") sich bei Lync Server anmelden und an einer Instant Messaging-Konferenz teilnehmen können. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Pilar Ackerman" enthält. (Da der Anmeldename "litwareinc\\pilar" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Pilar Ackerman" eingeben.) Das entstehende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert. Der zweite Befehl hat die gleiche Aufgabe, nur gibt dieser ein Objekt mit Anmeldeinformationen für das Konto "Ken Myer" zurück.

Anhand der beiden Objekte mit Anmeldeinformationen ermittelt der dritte Befehl im Beispiel, ob sich die beiden Benutzer bei Lync Server anmelden und dann an einer Instant Messaging-Konferenz teilnehmen können. Hierzu wird das Cmdlet **Test-CsGroupIM** mit folgenden Parametern aufgerufen: "TargetFqdn" (der FQDN des Registrierungsstellenpools), "SenderSipAddress" (die SIP-Adresse für den ersten Benutzer), "SenderCredential" (das PowerShell-Objekt mit den Anmeldeinformationen für den ersten Benutzer), "ReceiverSipAddress" (die SIP-Adresse des zweiten Benutzers) und "ReceiverCredential" (das PowerShell-Objekt mit den Anmeldeinformationen für den zweiten Benutzer).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Detaillierte Beschreibung

Das Cmdlet **Test-CsGroupIM** ist ein Beispiel für eine synthetische Lync Server-Transaktion. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich ausführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit den zwei betreffenden Benutzerkonten (anstelle von zwei Testkonten) durchführen und anschließend versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie die Anmeldeinformationen für jeden Benutzer angeben müssen.

Mit dem Cmdlet **Test-CsGroupIM** können Sie überprüfen, ob Benutzer in Ihrer Organisation Konferenzen durchführen können. Damit die Tests ordnungsgemäß mit dem Cmdlet **Test-CsGroupIM** ausgeführt werden können, sind zwei Benutzerkonten erforderlich. Wenn Sie Testbenutzer für die Zustandsüberwachung für den Pool eingerichtet haben, für den der Test durchgeführt werden soll, müssen Sie diese Konten nicht angeben. Vom Cmdlet **Test-CsGroupIM** werden automatisch die Testkonten verwendet, die dem Pool zugewiesen wurden. (Einzelheiten finden Sie im Hilfethema zum Cmdlet [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md).) Alternativ können Sie den Test auch mit anderen Konten als denjenigen durchführen, die der Registrierung zugewiesen wurden. So können Sie Tests selbst dann ausführen, wenn Sie keine Testbenutzer für den Pool konfiguriert haben. Sie können ferner testen, ob zwei spezifische Benutzer die Möglichkeit haben, eine Konferenz durchzuführen. Wenn Sie sich für diese Methode entscheiden, müssen Sie den Benutzernamen und das Kennwort für beide Benutzer bereitstellen.

Beim Ausführen des Cmdlets **Test-CsGroupIM** versucht das Cmdlet, beide Testbenutzer bei Lync Server anzumelden. Nach erfolgter Anmeldung erstellt das Cmdlet **Test-CsGroupIM** eine neue Konferenz unter dem Namen des ersten Testbenutzers. Anschließend wird der zweite Benutzer eingeladen, an der Konferenz teilzunehmen. Es werden einige Nachrichten ausgetauscht, woraufhin beide Benutzer vom System abgemeldet werden. Dies wird ohne Benutzereingriff und ohne Auswirkungen auf tatsächlich vorhandene Benutzer durchgeführt. Beispiel: Das Testkonto "sip:kenmyer@litwareinc.com" entspricht einem realen Benutzer mit einem tatsächlichen Lync Server-Konto. In diesem Fall wird der Test ohne Unterbrechungen für Ken Myer durchgeführt. Selbst wenn der Testbenutzer Ken Myer vom System abgemeldet wird, bleibt der reale Benutzer Ken Myer weiterhin angemeldet. Gleichermaßen erhält der reale Ken Myer keine Einladung zur Teilnahme an der Konferenz. Diese Einladung wird an das Testkonto gesendet und vom Testkonto angenommen.

Durch das Hinzufügen des Parameters "Verbose" erhalten Sie eine ausführliche Übersicht über alle Aktionen, die vom Cmdlet **Test-CsGroupIM** während des Tests durchgeführt wurden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsGroupIM"}

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
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse für das erste der beiden zu testenden Benutzerkonten. Beispiel: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Der Parameter &quot;ReceiverSipAddress&quot; muss auf das gleiche Benutzerkonto verweisen wie &quot;ReceiverCredential&quot;.</p>
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
<td><p>Die SIP-Adresse für das zweite der beiden zu testenden Benutzerkonten. Beispiel: -SenderSipAddres &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;SenderSipAddress&quot; muss auf das gleiche Benutzerkonto verweisen wie &quot;SenderCredential&quot;.</p>
<p>Die Angabe der SIP-Adresse ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Testet (sofern angegeben), ob der Join Launcher an einer AV-Konferenz teilnehmen kann. Der Join Launcher unterstützt Benutzer von Mobilgeräten (und damit Benutzer des Mobilitätsdiensts) bei der Teilnahme an Konferenzen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsGroupIM** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsGroupIM** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsIM](test-csim.md)

