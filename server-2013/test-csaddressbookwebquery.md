---
title: Test-CsAddressBookWebQuery
TOCTitle: Test-CsAddressBookWebQuery
ms:assetid: 9753dcba-83b3-437b-98f0-2806305a5bbb
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398773(v=OCS.15)
ms:contentKeyID: 49294827
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookWebQuery

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet, ob ein Benutzer unter Verwendung des Adressbuch-Webabfragediensts nach Informationen im Adressbuch suchen und diese Informationen zurückgeben kann. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsAddressBookWebQuery -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookWebQuery -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TargetSipAddress <String>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird der Adressbuch-Webabfragedienst für den Pool "atl-cs-001.litwareinc.com" getestet, indem nach dem Kontakt mit der SIP-Adresse "sip:kenmyer@litwareinc.com" gesucht wird. Dieser Befehl ist nur erfolgreich, wenn für den Pool "atl-cs-001.litwareinc.com" Testbenutzer definiert wurden. Trifft dies zu, wird der Befehl mit den Anmeldeinformationen des ersten Testbenutzers für diesen Pool ausgeführt.

Wurden keine Testbenutzer definiert, tritt bei der Befehlsausführung ein Fehler auf. Wenn Sie keine Testbenutzer für einen Pool definiert haben, müssen Sie den Parameter "UserSipAddress" und die Anmeldeinformationen des Benutzers verwenden, in dessen Namen der Befehl ausgeführt werden soll.

    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com  -TargetSipAddress "sip:kenmyer@litwareinc.com"

## BEISPIEL 2

Die in Beispiel 2 gezeigten Befehle testen ebenfalls die Verfügbarkeit des Adressbuch-Webabfragediensts. In diesem Fall werden die Befehle jedoch unter Verwendung der Anmeldeinformationen für den Benutzer "Ken Myer" (litwareinc\\kenmyer) ausgeführt. Hierzu verwendet der erste Befehl das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Ken Myer" enthält. (Da der Anmeldename "litwareinc\\kenmyer" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Ken Myer" eingeben.) Das resultierende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert.

Im zweiten Befehl wird das Cmdlet **Test-CsAddressBookWebQuery** dazu verwendet, den Adressbuch-Webabfragedienst für den Pool "atl-cs-001.litwareinc.com" zu testen. Zur Ausführung dieses Befehls mit den Anmeldeinformationen des Benutzers Ken Myer wird der Parameter "UserCredential" eingeschlossen, zusammen mit dem Parameterwert "$cred1". Der Befehl verwendet außerdem "TargetSipAddress", um anzugeben, dass das Cmdlet das Adressbuch nach dem Kontakt mit der SIP-Adresse "sip:kenmyer@litwareinc.com" durchsuchen soll.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## BEISPIEL 3

Beispiel 3 zeigt, wie der Adressbuch-Webabfragedienst für "atl-cs-001.litwareinc.com" getestet werden kann. Zu diesem Zweck wird das Cmdlet **Test-CsAddressBookWebQuery** mit drei Parametern aufgerufen: "TargetUri" gibt den URI des Adressbuch-Webabfragediensts an, "UserSipAddress" enthält die Windows PowerShell-SIP-Adresse des im Test verwendeten Benutzerkontos und "TargetSipAddress" enthält die SIP-Adresse des gesuchten Benutzerkontos.

    Test-CsAddressBookWebQuery -TargetUri https://atl-cs-001.litwareinc.com/groupexpansion -UserSipAddress "sip:packerman@litwareinc.com" -TargetSipAddress "sip:kenmyer@litwareinc.com"

## Detaillierte Beschreibung

Das Cmdlet **Test-CsAddressBookWebQuery** ist ein Beispiel für eine "synthetische Transaktion". Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie z. B. das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich durchführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit diesen zwei Benutzerkonten (anstelle von zwei Testkonten) durchführen und versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

Mit dem Cmdlet **Test-CsAddressBookWebQuery** können Administratoren prüfen, ob Benutzer den Adressbuch-Webabfragedienst verwenden können, um nach einem bestimmten Kontakt zu suchen. Wenn Sie das Cmdlet **Test-CsAddressBookWebQuery** ausführen, stellt es zur Authentifizierung zunächst eine Verbindung mit dem Webticketdienst her. Ist die Authentifizierung erfolgreich, stellt das Cmdlet eine Verbindung mit dem Adressbuch-Webabfragedienst her und sucht nach dem angegebenen Kontakt. Wird der Kontakt gefunden, versucht das Cmdlet, diese Informationen an den lokalen Computer zurückzugeben. Der Test wird nur dann als erfolgreich betrachtet, wenn alle Schritte durchgeführt werden können.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookWebQuery"}

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
<td><p>Vollqualifizierter Domänenname (FQDN) des Registrierungsstellenpools, in dem sich der zu testende Adressbuch-Webabfragedienst befindet. Beispiel: -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Beachten Sie, dass die Parameter &quot;TargetUri&quot; und &quot;TargetFqdn&quot; nicht im gleichen Befehl verwendet werden können.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>String</p></td>
<td><p>Der URI (Uniform Resource Identifier) des Adressbuch-Webabfragediensts. Beispiel: -TargetUri &quot;https://atl-cs-001.litwareinc.com/groupexpansion&quot;.</p>
<p>Beachten Sie, dass die Parameter &quot;TargetUri&quot; und &quot;TargetFqdn&quot; nicht im gleichen Befehl verwendet werden können.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das Benutzerkonto, das im Test verwendet werden soll. Bei dem an &quot;UserCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Beispiel: Dieser Code gibt ein Anmeldeinformationsobjekt für den Benutzer &quot;itwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der folgenden Variablen:</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Sie müssen beim Ausführen dieses Befehls das Benutzerkennwort angeben.</p></td>
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
<td><p><em>External</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Ermöglicht Ihnen zu überprüfen, ob externe Benutzer den Adressbuch-Webabfragedienst verwenden können.</p></td>
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
<td><p><em>TargetSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>SIP-Adresse des Kontakts, der durch den Adressbuch-Webabfragedienst zurückgegeben werden soll. Beispiel: -TargetSipAddress &quot;sip:kenmyer@litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>SIP-Adresse des Benutzers, der im Test verwendet wird. Wenn dieser Parameter ausgelassen wird, führt das Cmdlet <strong>Test-CsAddressBookWebQuery</strong> die Überprüfungen anhand der Konfigurationseinstellungen für die Integrationsüberwachung für den getesteten Pool durch.</p></td>
</tr>
<tr class="even">
<td><p><em>WebCredential</em></p></td>
<td><p>Optional</p></td>
<td><p>PSCredential</p></td>
<td><p>Ein Objekt mit den Benutzeranmeldeinformationen für den Zugriff auf den Standortinformationsdienst. Dieses Objekt kann abgerufen werden, indem Sie das Cmdlet <strong>Get-Credential</strong> aufrufen und die entsprechenden Anmeldeinformationen angeben.</p>
<p>Dieser Parameter ist erforderlich, wenn die Parameter &quot;TargetUri&quot; und &quot;UserSipAddress&quot; angegeben werden und wenn der Computer, auf dem Sie den Befehl ausführen, kein Serverzertifikat besitzt.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsAddressBookWebQuery** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsAddressBookWebQuery** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Update-CsAddressBook](update-csaddressbook.md)

