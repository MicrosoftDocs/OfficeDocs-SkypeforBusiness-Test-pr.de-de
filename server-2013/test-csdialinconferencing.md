---
title: Test-CsDialInConferencing
TOCTitle: Test-CsDialInConferencing
ms:assetid: e4aedf4f-77ac-4c8b-9613-07f8ea12c041
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399013(v=OCS.15)
ms:contentKeyID: 49295704
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialInConferencing

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Das Cmdlet **Test-CsDialInConferencing** überprüft, ob ein Benutzer an einer Einwahlkonferenzsitzung teilnehmen kann. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsDialInConferencing -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetPstnPhoneNumber <String>] [-UserSipAddress <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetPstnPhoneNumber <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird überprüft, ob ein vorkonfigurierter Testbenutzer an Einwahlkonferenzen im Pool "atl-cs-001.litwareinc.com" teilnehmen kann. Dieser Befehl funktioniert nur, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Wenn dies der Fall ist, dann bestimmt der Befehl, ob der erste Testbenutzer sich bei Lync Server anmelden kann.

Wenn keine Testbenutzer definiert wurden, tritt beim Ausführen des Befehls ein Fehler auf, da nicht bekannt ist, welcher Benutzer angemeldet werden soll. Wenn Sie für einen Pool keinen Testbenutzer definiert haben, müssen Sie den Parameter "UserCredential" und die Anmeldeinformationen des Benutzers verwenden, die der Befehl für die Anmeldung verwenden soll.

    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com 

## BEISPIEL 2

Mit den Befehlen in Beispiel 2 wird überprüft, ob ein bestimmter Benutzer (litwareinc\\pilar) an Einwahlkonferenzen im Pool "atl-cs-001.litwareinc.com" teilnehmen kann. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Pilar Ackerman" enthält. (Da der Anmeldename "litwareinc\\pilar" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Pilar Ackerman" eingeben.) Das resultierende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert.

Mit dem zweiten Befehl wird anschließend geprüft, ob sich der Benutzer Pilar Ackerman beim Pool "atl-cs-001.litwareinc.com" anmelden und dann an einer Einwahlkonferenz teilnehmen kann. Hierzu wird das Cmdlet **Test-CsDialInConferencing** mit drei Parametern aufgerufen: "TargetFqdn" (der FQDN des Registrierungsstellenpools), "UserCredential" (das Windows PowerShell-Objekt mit den Anmeldeinformationen des Benutzers "Pilar Ackerman") und "UserSipAddress" (die mit den eingegebenen Anmeldeinformationen übereinstimmende SIP-Adresse).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $cred1

## Detaillierte Beschreibung

Das Cmdlet **Test-CsDialInConferencing** ist ein Beispiel für eine "synthetische Transaktion" in Lync Server. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie z. B. das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich durchführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit den zwei betreffenden Benutzerkonten (anstelle von zwei Testkonten) durchführen und versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

Das Cmdlet **Test-CsDialInConferencing** versucht, einen Testbenutzer beim System anzumelden. (Wenn Sie mit Testbenutzern arbeiten, verwendet das Cmdlet **Test-CsDialInConferencing** das erste Testkonto, das für diesen Pool konfiguriert wurde.) Ist die Anmeldung erfolgreich, probiert das Cmdlet dann mit den Anmeldeinformationen und Berechtigungen des Benutzers die verfügbaren Zugriffsnummern für Einwahlkonferenzen aus. Der Erfolg oder Misserfolg jedes Einwahlversuchs wird vermerkt, und dann wird der Testbenutzer von Lync Server abgemeldet.

Mit dem Cmdlet **Test-CsDialInConferencing** wird nur überprüft, ob die entsprechenden Verbindungen hergestellt werden können. Das Cmdlet tätigt keine echten Anrufe und erstellt keine Einwahlkonferenzen, an denen andere Benutzer teilnehmen können.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Test-CsDialInConferencing** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialInConferencing"}

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
<td><p>System.String</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) des zu testenden Pools.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das Benutzerkonto, das getestet wird. Bei dem an &quot;UserCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der Variablen &quot;$x&quot;:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben. Dieser Parameter ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung durchführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>Beim Ausführen des Tests verwendeter Authentifizierungstyp. Zulässige Werte:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Diese Variable umfasst die beiden Methoden &quot;ToHTML&quot; und &quot;ToXML&quot;, mit deren Hilfe die Ausgabe entweder in einer HTML- oder XML-Datei gespeichert werden kann.</p>
<p>Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in einer Protokollierungsvariablen mit dem Namen &quot;$Testausgabe&quot; zu speichern:</p>
<p>-OutLoggerVariable Testausgabe</p>
<p>Hinweis: Setzen Sie kein Dollarzeichen ($) vor den Variablennamen. Wählen Sie zum Speichern der in der Protokolliervariablen gespeicherten Informationen in einer HTML-Datei einen Befehl wie den folgenden:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\Testausgabe.html</p>
<p>Wählen Sie zum Speichern der in der Protokolliervariablen gespeicherten Informationen in einer XML-Datei einen Befehl wie den folgenden:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\Testausgabe.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$Testausgabe&quot; zu speichern:</p>
<p>-OutVerboseVariable Testausgabe</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>Der vom Registrierungsdienst verwendete SIP-Port. Dieser Parameter ist nicht erforderlich, wenn die Registrierung den Standardport 5061 verwendet.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Telefonnummer für ein Festnetztelefon, mit der überprüft wird, ob Benutzer des Telefonfestnetzes an einer Einwahlkonferenz teilnehmen können. Beispiel:</p>
<p>-TargetPstnPhoneNumber &quot;+12065551219&quot;</p>
<p>Beachten Sie, dass &quot;TargetPstnPhoneNumber&quot; nur aufgenommen werden sollte, wenn der Parameter &quot;VerifyConferenceJoinType&quot; verwendet wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>SIP-Adresse für das Benutzerkonto, das getestet wird. Beispiel: -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;UserSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;UserCredential&quot; verweisen. Dieser Parameter ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung durchführen.</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyConferenceJoin</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Bei Festlegung von &quot;True&quot; wird überprüft, ob Benutzer mit einem Festnetztelefon an der Einwahlkonferenz teilnehmen können. Bei diesem Test können Sie optional &quot;TargetPstnPhoneNumber&quot; verwenden. In diesem Fall muss &quot;TargetPstnPhoneNumber&quot; das für die Teilnahme an der Konferenz verwendete Festnetztelefon angeben. Wird &quot;TargetPstnPhoneNumber&quot; nicht aufgenommen, verwendet das Cmdlet <strong>Test-CsDialInConferencing</strong> Einwahltelefonnummern, die vorab der entsprechenden Region für die Einwahlkonferenz zugewiesen wurden.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsDialInConferencing** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsDialInConferencing** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsAVConference](test-csavconference.md)

