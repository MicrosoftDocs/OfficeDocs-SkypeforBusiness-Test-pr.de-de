---
title: Test-CsRegistration
TOCTitle: Test-CsRegistration
ms:assetid: 9e38cb36-c97a-43f2-97fe-64759f663be2
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412737(v=OCS.15)
ms:contentKeyID: 49294910
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsRegistration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet, ob der Benutzer sich bei Lync Server anmelden kann. Das Cmdlet **Test-CsRegistration** ist eine "synthetische Transaktion", d. h. eine Simulation gängiger Lync Server-Aktivitäten, die zur Zustands- und Leistungsüberwachung verwendet werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsRegistration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsRegistration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsRegistration [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird der Registrierungsstellendienst für den Pool "atl-cs-001.litwareinc.com" getestet. Dieser Befehl funktioniert nur, wenn Testbenutzer für den Pool "atl-cs-001.litwareinc.com" definiert wurden. Wenn dies der Fall ist, wird anschließend mit dem Befehl festgestellt, ob sich der erste Testbenutzer bei Lync Server anmelden kann.

Wenn keine Testbenutzer definiert wurden, tritt beim Befehl ein Fehler auf, da nicht bekannt ist, welcher Benutzer angemeldet werden soll. Wenn Sie keine Testbenutzer für einen Pool definiert haben, müssen Sie den Parameter "UserSipAddress" und die Anmeldeinformationen des Benutzers verwenden, die der Befehl für die Anmeldung verwenden soll.

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com 

## BEISPIEL 2

Mit dem Befehl in Beispiel 2 wird getestet, ob sich ein bestimmter Benutzer (litwareinc\\pilar) bei Lync Server anmelden kann. Hierzu verwendet der erste Befehl im Beispiel das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Pilar Ackerman" enthält. (Da der Anmeldename "litwareinc\\pilar" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Pilar Ackerman" eingeben.) Das resultierende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert.

Der zweite Befehl prüft anschließend, ob sich dieser Benutzer beim Pool "atl-cs-001.litwareinc.com" anmelden kann. Dazu werden mit dem Befehl zunächst das Cmdlet **Test-CsRegistration** und drei Parameter aufgerufen: "TargetFqdn" (der vollqualifizierte Domänenname des Registrierungsstellenpools), "UserCredential" (das Windows PowerShell-Objekt mit den Anmeldeinformationen des Benutzers "Pilar Ackerman") und "UserSipAddress" (die mit den eingegebenen Anmeldeinformationen übereinstimmende SIP-Adresse).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:pilar@litwareinc.com"

## Detaillierte Beschreibung

Das Cmdlet **Test-CsRegistration** ist ein Beispiel für eine "synthetische Transaktion" in Lync Server. Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie z. B. das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich durchführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die CsHealthMonitoringConfiguration-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit den zwei betreffenden Benutzerkonten (anstelle von zwei Testkonten) durchführen und versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

Mit dem Cmdlet **Test-CsRegistration** können Sie überprüfen, ob Benutzer in Ihrer Organisation sich bei Lync Server anmelden können. Für das Cmdlet **Test-CsRegistration** ist ein Testkonto erforderlich, um diese Überprüfung durchführen zu können. Wenn Sie Testbenutzer für den Pool eingerichtet haben, für den der Test durchgeführt werden soll, müssen Sie kein Konto angeben. Das Cmdlet **Test-CsRegistration** verwendet automatisch die ersten Testkonten, die dem Pool zugewiesen wurden. (Einzelheiten finden Sie im Hilfethema zum Cmdlet [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md).) Sie können den Test alternativ mit einem Konto durchführen, das dem Pool nicht zugewiesen wurde. So können Sie Tests selbst dann ausführen, wenn Sie keine Testbenutzer konfiguriert haben. Sie können außerdem überprüfen, ob ein bestimmter Benutzer sich bei Lync Server anmelden kann. (Wenn Sie sich für diese Methode entscheiden, müssen Sie den Benutzernamen und das Kennwort für das Konto bereitstellen, das getestet werden soll.)

Wenn das Cmdlet **Test-CsRegistration** ausgeführt wird, versucht das Cmdlet, den Testbenutzer bei Lync Server anzumelden. Bei Erfolg wird dieser Testbenutzer anschließend vom System getrennt. Dies wird ohne Benutzereingriff und ohne Auswirkungen auf tatsächlich vorhandene Benutzer durchgeführt. Beispiel: Das Testkonto "sip:kenmyer@litwareinc.com" entspricht einem realen Benutzer mit einem tatsächlichen Lync Server-Konto. In diesem Fall wird der Test ohne Unterbrechungen für Ken Myer durchgeführt. Wenn sich das Testkonto "Ken Myer" vom System abmeldet, bleibt die Person "Ken Myer" weiterhin angemeldet.

Durch Hinzufügen des Parameters "Verbose" erhalten Sie eine ausführliche Übersicht über alle Aktionen, die vom Cmdlet **Test-CsRegistration** während des Tests durchgeführt wurden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsRegistration"}

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
<td><p>String</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) des zu testenden Pools.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das Konto, das getestet wird. Der Wert, der an &quot;UserCredential&quot; übergeben wird, muss ein Objektverweis sein, der durch die Verwendung des Cmdlets <strong>Get-Credential</strong> abgerufen wurde. Beispiel: Dieser Code gibt ein Anmeldeinformationsobjekt für den Benutzer &quot;itwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der folgenden Variablen:</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben. Dieser Parameter ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Optional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Der Typ der beim Test zu verwendenden Authentifizierung. Zulässige Werte:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Falls angegeben, wird nach Ausführung des Cmdlets die detaillierte Ausgabe in der angegebenen Variablen gespeichert. Geben Sie beispielsweise die folgende Syntax an, um die Ausgabe in der Variablen &quot;$TestOutput&quot; zu speichern:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Setzen Sie kein Dollarzeichen ($) vor den Variablennamen.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Der vom Registrierungsdienst verwendete SIP-Port. Dieser Parameter ist nicht erforderlich, wenn die Registrierung den Standardport 5061 verwendet.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>SIP-Adresse für das Benutzerkonto, das getestet wird. Beispiel: -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Der Parameter &quot;UserSipAddress&quot; muss auf dasselbe Benutzerkonto wie &quot;UserCredential&quot; verweisen. Dieser Parameter ist nicht erforderlich, wenn Sie den Test mit den Konfigurationseinstellungen für die Zustandsüberwachung des Pools ausführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsRegistration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsRegistration** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

