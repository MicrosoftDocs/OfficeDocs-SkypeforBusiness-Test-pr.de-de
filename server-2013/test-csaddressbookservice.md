---
title: Test-CsAddressBookService
TOCTitle: Test-CsAddressBookService
ms:assetid: 8398c9ea-eaab-4a4d-9e09-473ea2b27e22
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398661(v=OCS.15)
ms:contentKeyID: 49294603
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookService

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet die Fähigkeit eines Benutzers, auf den Server mit dem Adressbuch-Downloadwebdienst zuzugreifen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsAddressBookService -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird der Adressbuch-Downloadwebdienst für den Pool "atl-cs-001.litwareinc.com" getestet. Dieser Befehl testet den Adressbuch-Downloadwebdienst mithilfe von Testbenutzern, die für den Pool "atl-cs-001.litwareinc.com" vorkonfiguriert wurden.

    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com 

## BEISPIEL 2

Die in Beispiel 2 gezeigten Befehle testen ebenfalls die Verfügbarkeit des Servers mit dem Adressbuch-Downloadwebdienst. In diesem Fall werden die Befehle jedoch unter Verwendung der Anmeldeinformationen für den Benutzer "Ken Myer" (litwareinc\\kenmyer) ausgeführt. Hierzu verwendet der erste Befehl das Cmdlet **Get-Credential**, um ein Windows PowerShell-Objekt mit Anmeldeinformationen zu erstellen, das den Namen und das Kennwort des Benutzers "Ken Myer" enthält. (Da der Anmeldename "litwareinc\\kenmyer" als Parameter angegeben ist, muss der Administrator im Dialogfeld "Bei Windows PowerShell anmelden" lediglich das Kennwort für das Konto "Ken Myer" eingeben.) Das resultierende Objekt mit Anmeldeinformationen wird dann in der Variablen "$cred1" gespeichert.

Im zweiten Befehl wird das Cmdlet **Test-CsAddressBookService** dazu verwendet, den Adressbuch-Downloadwebdienst für den Pool "atl-cs-001.litwareinc.com" zu testen. Zur Ausführung dieses Befehls mit den Anmeldeinformationen des Benutzers Ken Myer wird der Parameter "UserCredential" eingeschlossen, zusammen mit dem Parameterwert "$cred1". Zusätzlich muss Kens SIP-Adresse über den Parameter "UserSipAddress" bereitgestellt werden.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com"

## BEISPIEL 3

Beispiel 3 zeigt, wie der Adressbuch-Downloadwebdienst für "atl-cs-001.litwareinc.com" getestet werden kann. Zu diesem Zweck wird das Cmdlet **Test-CsAddressBookService** mit zwei Parametern aufgerufen: "TargetUri" gibt den URI des Adressbuch-Downloadwebdiensts an, und "UserSipAddress" enthält die Windows PowerShell-SIP-Adresse für das im Test verwendete Benutzerkonto.

``` 


Test-CsAddressBookService -TargetUri https://atl-cs-001.litwareinc.com/abs/handler -UserSipAddress "sip:kenmyer@litwareinc.com"
```

## Detaillierte Beschreibung

Das Cmdlet **Test-CsAddressBookService** ist ein Beispiel für eine "synthetische Transaktion". Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie z. B. das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich durchführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Synthetische Transaktionen werden in der Regel auf zwei unterschiedliche Arten ausgeführt. Viele Administratoren verwenden die **CsHealthMonitoringConfiguration**-Cmdlets, um für jeden Registrierungsstellenpool Testbenutzer einzurichten. Bei diesen Testbenutzern handelt es sich um ein Benutzerpaar, das für synthetische Transaktionen vorkonfiguriert wurde. (Dies sind in der Regel Testkonten und keine Konten von tatsächlich vorhandenen Benutzern.) Administratoren können mithilfe von Testbenutzern, die für einen Pool konfiguriert wurden, eine synthetische Transaktion für diesen Pool durchführen, ohne die Identitätswerte (und die Anmeldeinformationen) der für den Test verwendeten Benutzerkonten anzugeben.

Administratoren können eine synthetische Transaktion allerdings auch mit tatsächlichen Benutzerkonten ausführen. Wenn zwei Benutzer beispielsweise Chatnachrichten austauschen, kann ein Administrator eine synthetische Transaktion mit diesen zwei Benutzerkonten (anstelle von zwei Testkonten) durchführen und versuchen, das Problem zu diagnostizieren und zu beheben. Denken Sie beim Ausführen einer synthetischen Transaktion mit tatsächlichen Benutzerkonten daran, dass Sie den Anmeldenamen und das Kennwort jedes Benutzers angeben müssen.

Mit dem Cmdlet **Test-CsAddressBookService** kann überprüft werden, ob ein Benutzer eine Verbindung mit dem Adressbuch-Downloadwebdienst herstellen kann. Wenn Sie das Cmdlet **Test-CsAddressBookService** ausführen, stellt es eine Verbindung mit dem Adressbuch-Downloadwebdienst im angegebenen Pool her und fordert den Speicherort der Adressbuchdateien an. Wenn der Adressbuch-Downloadwebdienst den Speicherort zurückgibt, wird der Test als erfolgreich betrachtet. Wenn die Anforderung abgelehnt wird, wird der Test als nicht erfolgreich betrachtet.

Es gibt zwei Möglichkeiten, den Adressbuch-Downloadwebdienst zu testen: Entweder testen Sie den Dienst selbst, oder Sie testen den zugeordneten Webdienst.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Test-CsAddressBookService** auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookService"}

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
<td><p>Vollqualifizierter Domänenname (FQDN) des Registrierungsstellenpools, in dem sich der zu testende Adressbuch-Downloadwebdienst befindet. Beispiel: -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Sie können die Parameter &quot;TargetUri&quot; und &quot;TargetFqdn&quot; nicht in demselben Befehl verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>String</p></td>
<td><p>Der URI (Uniform Resource Identifier) des Adressbuch-Webabfragediensts. Beispiel: -TargetUri &quot;https://atl-cs-001.litwareinc.com/abs/handler&quot;.</p>
<p>Sie können die Parameter &quot;TargetUri&quot; und &quot;TargetFqdn&quot; nicht in demselben Befehl verwenden.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PSCredential</p></td>
<td><p>Objekt mit Anmeldeinformationen für das Benutzerkonto, das im Test verwendet werden soll. Bei dem an &quot;UserCredential&quot; übergebenen Wert muss es sich um einen Objektverweis handeln, der mit dem Cmdlet <strong>Get-Credential</strong> abgerufen wurde. Der folgende Code gibt beispielsweise ein Objekt mit Anmeldeinformationen für den Benutzer &quot;litwareinc\kenmyer&quot; zurück und speichert dieses Objekt in der Variablen &quot;$x&quot;:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
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
<td><p>Ermöglicht Ihnen zu überprüfen, ob externe Benutzer den Adressbuch-Downloadwebdienst verwenden können.</p></td>
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
<td><p>SIP-Adresse des Benutzers, der im Test verwendet wird. Wenn dieser Parameter nicht angegeben ist, führt <strong>Test-CsAddressBookService</strong> die Prüfungen unter Verwendung des Kontos für den angemeldeten Benutzer durch.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Optional</p></td>
<td><p>PSCredential</p></td>
<td><p>Ein Objekt mit den Benutzeranmeldeinformationen für den Zugriff auf den Standortinformationsdienst. Dieses Objekt kann abgerufen werden, indem Sie das Cmdlet <strong>Get-Credential</strong> aufrufen und die entsprechenden Anmeldeinformationen angeben.</p>
<p>Dieser Parameter ist erforderlich, wenn die Parameter &quot;TargetUri&quot; und &quot;UserSipAddress&quot; angegeben werden und wenn der Computer, auf dem Sie den Befehl ausführen, kein Serverzertifikat besitzt.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsAddressBookService** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsAddressBookService** wird eine Instanz des Objekts "Microsoft.Rtc.SyntheticTransactions.TaskOutput" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)  
[Update-CsAddressBook](update-csaddressbook.md)

