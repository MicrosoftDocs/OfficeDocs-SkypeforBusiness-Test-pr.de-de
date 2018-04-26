---
title: Get-CsCommonAreaPhone
TOCTitle: Get-CsCommonAreaPhone
ms:assetid: bfb7927b-49a7-4637-a9ff-fd68897efb45
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412934(v=OCS.15)
ms:contentKeyID: 49295273
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCommonAreaPhone

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu Telefonen in öffentlichen Bereichen zurück, die mit Lync Server verwaltet werden. Telefone in öffentlichen Bereichen sind Telefone in Eingangsbereichen von Gebäuden, Aufenthaltsräumen für Mitarbeiter oder in anderen Bereichen, in denen sie oftmals von vielen Menschen und zu unterschiedlichen Zwecke genutzt werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsCommonAreaPhone [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 gibt Informationen zu allen Telefonen in öffentlichen Bereichen zurück, die für die Verwendung in der Organisation konfiguriert wurden. Hierzu wird das Cmdlet **Get-CsCommonAreaPhone** ohne Parameter aufgerufen.

    Get-CsCommonAreaPhone

## BEISPIEL 2

In Beispiel 2 wird das Telefon für öffentliche Bereiche mit dem Active Directory-Anzeigenamen "Building 14 Lobby" zurückgegeben. Hierzu wird der Parameter "Filter" und der Filterwert "{DisplayName -eq "Building 14 Lobby"}" aufgerufen. Dieser Filterwert beschränkt die zurückgegebenen Objekte auf Telefone in öffentlichen Bereichen, bei denen die Eigenschaft "DisplayName" den Wert "Building 14 Lobby" aufweist.

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"}

## BEISPIEL 3

In Beispiel 3 werden alle Telefone in öffentlichen Bereichen zurückgegeben, deren Active Directory-Anzeigename mit den Zeichen "Building 14" beginnt. Hierzu wird das Cmdlet **Get-CsCommonAreaPhone** mit dem Parameter "Filter" und dem Filterwert "{DisplayName -like "Building 14\*"}" aufgerufen. Der Filterwert verwendet den Operator "-like" und die Platzhalterzeichenfolge "Building 14\*", um die zurückgegebenen Daten auf die Telefone zu beschränken, bei denen die Eigenschaft "DisplayName" mit "Building 14" beginnt. (Beispiel: "Building 14 Lobby", "Building 14 Cafeteria" usw.)

    Get-CsCommonAreaPhone  -Filter {DisplayName -like "Building 14*"}

## BEISPIEL 4

In Beispiel 4 wird ein einziges Telefon im öffentlichen Bereich zurückgegeben: das Telefon, bei dem die Eigenschaft "LineUri" den Wert "tel:+14255551234" aufweist. Da die Eigenschaft "LineUri" eindeutig sein muss, gibt dieser Befehl immer nur ein Element zurück.

    Get-CsCommonAreaPhone  -Filter {LineUri -eq "tel:+14255551234"}

## BEISPIEL 5

Der Befehl in Beispiel 5 gibt Informationen zu allen Telefonen in öffentlichen Bereichen zurück, denen keine Wähleinstellungen zugewiesen wurden. Hierzu wird der Parameter "Filter" und der Filterwert "{DialPlan -eq $Null}" verwendet, um die zurückgegebenen Daten auf die Telefone zu beschränken, bei denen die Eigenschaft "DialPlan" einen Nullwert aufweist. Wenn einem Telefon in einem öffentlichen Bereich nicht explizit ein Wählplan zugewiesen wurde, wird automatisch der globale Wählplan oder, sofern verfügbar, der dem Standort zugewiesene Wählplan verwendet.

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null}

## BEISPIEL 6

In Beispiel 6 wird eine Auflistung aller Telefone in öffentlichen Bereichen zurückgegeben, die ein Kontaktobjekt in der OU "Telecommunications" in Active Directory-Domänendienste besitzen. Dazu wird das Cmdlet **Get-CsCommonAreaPhone** mit dem Parameter "OU" aufgerufen. Der Parameterwert beschränkt die zurückgegebenen Objekte auf die Telefone, die Kontaktobjekte in der Organisationseinheit mit dem Distinguished Name "ou=Telecommunications,dc=litwareinc,dc=com" besitzen.

    Get-CsCommonAreaPhone -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## Detaillierte Beschreibung

Telefone in öffentlichen Bereichen sind IP-Telefone, die keinem einzelnen Benutzer zugeordnet sind. Sie befinden sich nicht in einem Büro, sondern normalerweise in Eingangsbereichen, Cafeterias, Aufenthaltsräumen für Mitarbeiter, Besprechungszimmern und anderen Bereichen, in denen viele Menschen zusammenkommen. Die Verwaltung solcher Telefone stellt für Administratoren eine Herausforderung dar, da die Telefonnutzung in Lync Server normalerweise anhand verschiedener VoIP-Richtlinien und Wähleinstellungen verwaltet wird, die einzelnen Benutzern zugewiesen sind. Telefonen in öffentlichen Bereichen sind keine einzelnen Benutzer zugewiesen.

Eine Lösung besteht darin, Active Directory-Kontaktobjekte für alle Telefone in öffentlichen Bereichen zu erstellen. (Diese Kontaktobjekte können mit dem Cmdlet **New-CsCommonAreaPhone** erstellt werden.) Diesen Kontaktobjekten können dann genau wie Benutzerkonten Richtlinien und VoIP-Einstellungen zugewiesen werden. Auf diese Weise können Sie Telefone in öffentlichen Bereichen verwalten, auch wenn sie keinem einzelnen Benutzer zugeordnet sind. Wenn Benutzer beispielsweise nicht die Möglichkeit haben sollen, Anrufe von einem Telefon in einem öffentlichen Bereich aus weiterzuleiten oder zu parken, können Sie eine VoIP-Richtlinie erstellen, die die Weiterleitung und das Parken von Anrufen verhindert. Weisen Sie diese Richtlinie dann dem Telefon im öffentlichen Bereich zu. (Genauer gesagt, weisen Sie diese Richtlinie dem Kontaktobjekt zu, das für das Telefon im öffentlichen Bereich steht.) Mit dem folgenden Befehl wird z. B. allen Telefonen in öffentlichen Bereichen die VoIP-Richtlinie "CommonAreaPhoneVoicePolicy" zugewiesen:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

Mit dem Cmdlet **Get-CsCommonAreaPhone** können Sie Informationen zu Telefonen in öffentlichen Bereichen abrufen, die für die Verwendung in Ihrer Organisation konfiguriert sind. Wenn Sie das Cmdlet **Get-CsCommonAreaPhone** ohne Parameter aufrufen, gibt das Cmdlet Informationen zu allen Ihren Telefonen in öffentlichen Bereichen zurück. Mit optionalen Parametern haben Sie verschiedene Möglichkeiten, Informationen zu filtern. Sie können beispielsweise alle Telefone in öffentlichen Bereichen, die Kontaktobjekte in einer angegebenen Organisationseinheit haben, oder alle Kontaktobjekte zurückgeben, die sich in einem bestimmten Gebäude befinden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsCommonAreaPhone** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Berechtigungen zum Ausführen dieses Cmdlets für bestimmte Standorte oder spezifische Active Directory-OUs können mit dem Cmdlet **Grant-CsOUPermission** zugewiesen werden. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCommonAreaPhone"}

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
<td><p><em>Credential</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Ermöglicht die Ausführung des Cmdlets <strong>Get-CsCommonAreaPhone</strong> mit anderen Anmeldeinformationen. Dies kann notwendig sein, wenn das für die Anmeldung bei Windows verwendete Konto nicht über die erforderlichen Berechtigungen verfügt, um mit Kontaktobjekten zu arbeiten.</p>
<p>Zur Verwendung des Parameters &quot;Credential&quot; muss zunächst über das Cmdlet <strong>Get-Credential</strong> ein PSCredential-Objekt erstellt werden. Einzelheiten finden Sie im Hilfethema zum Cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Ermöglicht es Ihnen, zum Abrufen von Kontaktinformationen eine Verbindung mit dem angegebenen Domänencontroller herzustellen. Um eine Verbindung mit einem bestimmten Domänencontroller herzustellen, fügen Sie den Parameter &quot;DomainController&quot; ein, gefolgt vom vollqualifizierten Domänennamen (FQDN) des Computers (z. B. &quot;atl-cs-001.litwareinc.com&quot;).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht die Einschränkung der zurückgegebenen Daten, indem diese nach Lync Server-spezifischen Attributen gefiltert werden. Die zurückgegebenen Daten können z. B. auf Kontaktobjekte der Telefone in öffentlichen Bereichen beschränkt werden, die einer bestimmten VoIP-Richtlinie zugewiesen sind, oder auf Kontakte, denen keine spezifische VoIP-Richtlinie zugewiesen wurde.</p>
<p>Der Parameter &quot;Filter&quot; verwendet dieselbe Windows PowerShell-Filtersyntax wie das Cmdlet <strong>Where-Object</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Eindeutige ID des Telefons im öffentlichen Bereich. Telefone in öffentlichen Bereichen werden mit dem Distinguished Name (DN) des zugeordneten Kontaktobjekts in Active Directory identifiziert. Telefone in öffentlichen Bereichen verwenden standardmäßig eine GUID (Globally Unique Identifier) als allgemeinen Namen (Common Name, CN), deshalb verfügen Telefone in der Regel über einen Identitätswert wie den folgenden: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, die zurückgegebenen Daten durch das Filtern allgemeiner Active Directory-Attribute einzuschränken (d. h. Attribute, die nicht Lync Server-spezifisch sind). Beispielsweise können Sie die zurückgegebenen Daten auf Kontaktobjekte beschränken, die einer bestimmten Abteilung zugewiesen sind oder sich in einem bestimmten Gebäude befinden.</p>
<p>Der Parameter &quot;LdapFilter&quot; verwendet beim Erstellen von Filtern die LDAP-Abfragesprache. Im folgenden Beispiel wird ein Filter gezeigt, der nur Kontaktobjekte zurückgibt, die Telefone in öffentlichen Gebäuden in der Stadt &quot;Redmond&quot; repräsentieren:</p>
<p>-LDAPFilter &quot;l=Redmond&quot;</p>
<p>Im vorstehenden Filter repräsentiert &quot;l&quot; (ein klein geschriebenes L) das Attribut der Active Directory-Domänendienste (&quot;l&quot; steht für &quot;locality&quot;, Deutsch: Ort), &quot;=&quot; ist der Vergleichsoperator (equal to) und &quot;Redmond&quot; der Filterwert.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Ermöglicht es Ihnen, Kontaktobjekte aus einer bestimmten Active Directory-Organisationseinheit (Organizational Unit, OU) zurückzugeben. Der Parameter &quot;OU&quot; gibt Daten aus der angegebenen OU und allen untergeordneten OUs zurück. Wenn die OU &quot;Finance&quot; z. B. über zwei untergeordnete OUs verfügt – &quot;AccountsPayable&quot; und &quot;AccountsReceivable&quot; – werden alle Informationen zu Telefonen in öffentlichen Bereichen aus diesen OUs zurückgegeben.</p>
<p>Verwenden Sie beim Angeben einer Organisationseinheit den Distinguished Name des Containers. Beispiel: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Ermöglicht es Ihnen, die Anzahl von zurückgegebenen Datensätzen einzuschränken. Um beispielsweise sieben Telefone in öffentlichen Bereichen zurückzugeben (unabhängig von der Anzahl von Telefonen in öffentlichen Bereichen in der Gesamtstruktur), verwenden Sie den Parameter &quot;ResultSize&quot;, und setzen Sie seinen Wert auf 7. Beachten Sie, dass nicht garantiert werden kann, welche sieben Telefone zurückgegeben werden. Wenn Sie &quot;ResultSize&quot; auf 7 setzen, jedoch lediglich über drei Telefone in öffentlichen Bereichen in Ihrer Gesamtstruktur verfügen, werden diese drei Telefone zurückgegeben, und der Befehl wird anschließend ohne Fehler abgeschlossen.</p>
<p>Für die Ergebnisgröße kann ein ganzzahliger Wert zwischen einschließlich 0 und 2147483647 festgelegt werden. Bei Festlegung von 0 wird der Befehl ausgeführt, es werden jedoch keine Daten zurückgegeben.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Zeichenfolge. Das Cmdlet **Get-CsCommonAreaPhone** akzeptiert einen weitergeleiteten Zeichenfolgenwert, der die Identität des Telefons in öffentlichen Bereichen repräsentiert.

## Rückgabetypen

Mit dem Cmdlet **Get-CsCommonAreaPhone** werden Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

