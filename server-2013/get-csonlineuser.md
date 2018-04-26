---
title: Get-CsOnlineUser
TOCTitle: Get-CsOnlineUser
ms:assetid: 2bfafd70-a7d9-4308-a353-5ecf44249b53
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994026(v=OCS.15)
ms:contentKeyID: 52056318
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOnlineUser

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu Benutzern zurück, deren Konten in Microsoft Lync Online verwaltet werden. Dieses Cmdlet kann nur mit Skype for Business Online verwendet werden.

## Syntax

    Get-CsOnlineUser [[-Identity] <UserIdParameter>] [-Filter <String>] [-LdapFilter <String>] [-OnOfficeCommunicationServer] [-OnLyncServer] [-UnAssignedUser] [-OU <OUIdParameter>] [-DomainController <Fqdn>] [-Credential <PSCredential>] [-ResultSize <Unlimited`1>] [-Verbose]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 gibt Informationen zu allen Benutzern zurück, die als Onlinebenutzer konfiguriert sind.

    Get-CsOnlineUser

## Beispiel 2

In Beispiel 2 werden Informationen zu einem einzigen Onlinebenutzer zurückgegeben, dem Benutzer mit der SIP-Adresse "sip:kenmyer@litwareinc.com".

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

## Beispiel 3

Der Befehl in Beispiel 3 gibt Informationen zu allen Onlinebenutzern zurück, die für Lync Online aktiviert wurden, derzeit aber keinem Registrierungsstellenpool zugewiesen sind.

    Get-CsOnlineUser -UnassignedUser

## Beispiel 4

In Beispiel 4 wird der Parameter "Filter" verwendet, um die zurückgegebenen Daten auf Onlinebenutzer einzuschränken, denen die benutzerbasierte Archivierungsrichtlinie "RedmondArchiving" zugewiesen wurde. Dafür wird der Filterwert "{ArchivingPolicy -eq "RedmondArchiving"}" verwendet. Mit dieser Syntax werden die zurückgegebenen Daten auf die Benutzer beschränkt, bei denen die Eigenschaft "ArchivingPolicy" gleich (-eq) "RedmondArchiving" ist.

    Get-CsOnlineUser -Filter {ArchivingPolicy -eq "RedmondArchiving"}

## Beispiel 5

In Beispiel 5 werden Informationen nur zu Benutzerkonten zurückgegeben, die so konfiguriert wurden, dass das Konto nicht in Microsoft Exchange-Adresslisten angezeigt wird. (Das heißt, das Active Directory-Attribut "msExchHideFromAddressLists" ist auf "True" festgelegt.) Zum Ausführen dieser Aufgabe wird der Parameter "Filter" zusammen mit dem Filterwert "{HideFromAddressLists -eq $True}" eingeschlossen.

    Get-CsOnlineUser -Filter {HideFromAddressLists -eq $True}

## Beispiel 6

Der Befehl in Beispiel 6 gibt Informationen zu allen Onlinebenutzern zurück, die dem Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" zugewiesen sind. Dafür enthält der Befehl den Parameter "Filter" zusammen mit dem Filterwert "{TenantId –eq "bf19b7db-6960-41e5-a139-2aa373474354"}". Dieser Filter schränkt die zurückgegebenen Daten auf Onlinebenutzer ein, die dem Mandanten "bf19b7db-6960-41e5-a139-2aa373474354" zugewiesen sind.

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

## Detaillierte Beschreibung

Das Cmdlet **Get-CsOnlineUser** gibt Informationen zu Benutzern zurück, deren Konten in Microsoft Lync Online verwaltet werden. Zu den zurückgegebenen Informationen zählen Active Directory-Standardkontoinformationen (wie die Abteilung, in der der Benutzer arbeitet, seine Adresse und Telefonnummer usw.) sowie Lync Server-spezifische Informationen: Das Cmdlet **Get-CsOnlineUser** gibt Informationen beispielsweise dazu zurück, ob der Benutzer für Enterprise-VoIP aktiviert wurde und welche benutzerbasierten Richtlinien (wenn überhaupt) dem Benutzer zugewiesen wurden.

Beachten Sie, dass das Cmdlet **Get-CsOnlineUser** keinen TenantId-Parameter umfasst, was bedeutet, dass Sie keinen Befehl wie den folgenden verwenden können, um die zurückgegebenen Daten auf Benutzer einzuschränken, die über Konten bei einem spezifischen Lync Online-Mandanten verfügen:

    Get-CsOnlineUser -TenantId "bf19b7db-6960-41e5-a139-2aa373474354"

Wenn jedoch mehrere Lync Online-Mandanten vorhanden sind, können Sie Benutzer von einem bestimmten Mandanten über den Parameter "Filter" und einen Befehl wie den folgenden zurückgeben:

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

Dieser Befehl schränkt die zurückgegebenen Daten auf Benutzerkonten ein, die zu dem Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" gehören. Wenn Sie Ihre Mandanten-IDs nicht kennen, können Sie diese Informationen über den folgenden Befehl zurückgeben:

    Get-CsTenant

Wenn Sie eine Hybridbereitstellung oder eine Bereitstellung mit "geteilter Domäne" (d. h. eine Bereitstellung, in der die Konten einiger Benutzer in Lync Online und die Konten anderer Benutzer in einer lokalen Versionen von Lync Server verwaltet werden), denken Sie daran, dass das Cmdlet **Get-CsOnlineUser** nur Informationen für Lync Online-Benutzer zurückgibt. Das Cmdlet [Get-CsUser](get-csuser.md) gibt jedoch Informationen für Lync Online-Benutzer und lokale Lync Server-Benutzer zurück. Wenn Sie Lync Online-Benutzer aus den vom Cmdlet **Get-CsUser** zurückgegebenen Daten ausschließen möchten, verwenden Sie den folgenden Befehl:

    Get-CsUser -Filter {TenantId -eq "00000000-0000-0000-0000-000000000000"}

Per Definition haben Benutzer, die in der lokalen Version von Lync Server verwaltet werden, für "TenantId" immer den Wert "00000000-0000-0000-0000-000000000000". Benutzer, die in Lync Online verwaltet werden, haben einen Wert für "TenantId", der einem anderen Wert als "00000000-0000-0000-0000-000000000000" entspricht.

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
<td><p>Ermöglicht die Ausführung des Cmdlets <strong>Get-CsOnlineUser</strong> mit anderen Anmeldeinformationen. Dies kann notwendig sein, wenn das für die Anmeldung an Windows verwendete Konto nicht über die erforderlichen Berechtigungen verfügt, um mit Benutzerobjekten zu arbeiten.</p>
<p>Zur Verwendung des Parameters &quot;Credential&quot; muss zunächst über das Cmdlet <strong>Get-Credential</strong> ein PSCredential-Objekt erstellt werden. Einzelheiten finden Sie im Hilfethema zum Cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Ermöglicht es Ihnen, zum Abrufen von Benutzerinformationen eine Verbindung mit dem angegebenen Domänencontroller herzustellen. Um eine Verbindung mit einem bestimmten Domänencontroller herzustellen, fügen Sie den Parameter &quot;DomainController&quot; ein, gefolgt vom vollqualifizierten Domänennamen (z. B. &quot;atl-cs-001.litwareinc.com&quot;).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht die Einschränkung der zurückgegebenen Daten, indem diese nach Lync Server-spezifischen Attributen gefiltert werden. Die zurückgegebenen Daten können z. B. auf Benutzer beschränkt werden, denen eine bestimmte VoIP-Richtlinie zugewiesen ist, oder Benutzer, denen keine spezifische VoIP-Richtlinie zugewiesen wurde.</p>
<p>Der Parameter &quot;Filter&quot; verwendet dieselbe Windows PowerShell-Filterungssyntax wie das Cmdlet &quot;Where-Object&quot;. Beispielsweise sieht ein Filter, der nur für Enterprise-VoIP aktivierte Benutzer zurückgibt, wie nachstehend gezeigt aus. &quot;EnterpriseVoiceEnabled&quot; stellt das Active Directory-Attribut dar, &quot;-eq&quot; den Vergleichsoperator &quot;equal to&quot; und &quot;$True&quot; (eine integrierte Windows PowerShell-Variable) den Filterwert:</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Gibt den Identitätswert des Benutzerkontos an, das abgerufen werden soll. Benutzeridentitäten können in den folgenden vier Formaten angegeben werden: als 1) SIP-Adresse des Benutzers, 2) UPN (Benutzerprinzipalname) des Benutzers, 3) Domänen- und Anmeldename des Benutzers (mit dem Format &quot;Domäne\Anmeldename&quot;, z. B. &quot;litwareinc\kenmyer&quot;) und 4) Active Directory-Anzeigename des Benutzers (z. B. &quot;Ken Myer&quot;). Sie können auch unter Verwendung des Active Directory-Distinguished Name (DN) des Benutzers auf ein Benutzerkonto verweisen.</p>
<p>Sie können das Sternchen (*) als Platzhalterzeichen nutzen, wenn Sie den Anzeigenamen als Benutzeridentität verwenden. Der Identitätswert &quot;* Smith&quot; gibt beispielsweise alle Benutzer zurück, deren Anzeigename auf den Zeichenfolgenwert &quot; Smith&quot; endet.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, die zurückgegebenen Daten durch das Filtern allgemeiner Active Directory-Attribute einzuschränken (d. h. Attribute, die nicht Lync Server-spezifisch sind). Beispielsweise können die zurückgegebenen Daten auf Benutzer beschränkt werden, die in einer bestimmten Abteilung arbeiten, oder auf Benutzer mit einem bestimmten Vorgesetzten oder einer bestimmten Position.</p>
<p>Der Parameter &quot;LdapFilter&quot; verwendet beim Erstellen von Filtern die LDAP-Abfragesprache. Im folgenden Beispiel wird ein Filter gezeigt, der nur Benutzer zurückgibt, die in Redmond arbeiten: &quot;l=Redmond&quot;. Dabei ist &quot;l&quot; (klein geschriebenes &quot;L&quot;) das Active Directory-Attribut (&quot;l&quot; steht für &quot;locality&quot;, Deutsch: Ort), &quot;=&quot; ist der Vergleichsoperator (equal to) und &quot;Redmond&quot; der Filterwert.</p></td>
</tr>
<tr class="even">
<td><p><em>OnLyncServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Gibt eine Auflistung mit Benutzern zurück, die Lync Server angehören. Benutzer mit Konten in früheren Versionen der Software werden bei diesem Parameter nicht zurückgegeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>OnOfficeCommunicationServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Gibt eine Auflistung von Benutzern zurück, die sich auf einer früheren Version von Lync Server befinden (z. B. Microsoft Office Communications Server 2007 R2). Benutzer mit Konten in der aktuellen Version der Software werden bei diesem Parameter nicht zurückgegeben.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Ermöglicht es Ihnen, Informationen zu Benutzerkonten in einer spezifischen Organisationseinheit (Organizational Unit, OU) oder in einem spezifischen Container zurückzugeben. Der Parameter &quot;OU&quot; gibt Daten aus der angegebenen OU und allen untergeordneten OUs zurück. Wenn die OU &quot;Finance&quot; z. B. über zwei untergeordnete OUs verfügt – &quot;AccountsPayable&quot; und &quot;AccountsReceivable&quot; – werden alle Benutzer aus diesen drei OUs zurückgegeben.</p>
<p>Verwenden Sie beim Angeben einer Organisationseinheit den Distinguished Name (DN) des Containers, z. B.: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;. Verwenden Sie die folgende Syntax, um Benutzerkonten aus dem Container &quot;Users&quot; zurückzugeben:</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Ermöglicht es Ihnen, die Anzahl der vom Cmdlet zurückgegebenen Datensätze einzuschränken. Um beispielsweise sieben Benutzer (unabhängig von der Gesamtzahl der Benutzer in der Gesamtstruktur) zurückzugeben, verwenden Sie den Parameter &quot;ResultSize&quot; und legen Sie den Parameterwert auf 7 fest. Beachten Sie, dass nicht garantiert werden kann, welche sieben Benutzer zurückgegeben werden.</p>
<p>Für die Ergebnisgröße kann ein ganzzahliger Wert zwischen einschließlich 0 und 2147483647 festgelegt werden. Bei Festlegung von 0 wird der Befehl ausgeführt, es werden jedoch keine Daten zurückgegeben. Wenn Sie &quot;ResultSize&quot; auf 7 festlegen, jedoch nur drei Benutzer in Ihrer Gesamtstruktur vorhanden sind, werden diese drei Benutzer zurückgegeben und der Befehl wird anschließend ohne Fehler abgeschlossen.</p></td>
</tr>
<tr class="even">
<td><p><em>UnassignedUser</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ermöglicht die Rückgabe einer Auflistung aller Benutzer, die für Lync Online aktiviert wurden, aber derzeit keinem Registrierungsstellenpool zugewiesen sind. Benutzer dürfen sich nur anmelden, wenn sie einem Registrierungsstellenpool zugewiesen sind.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Das Cmdlet **Get-CsOnlineUser** akzeptiert weitergeleitete Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.OCSADUser" sowie Zeichenfolgenwerte, die eine gültige Benutzerkontoidentität darstellen (z. B. "sip:kenmyer@litwareinc.com").

## Rückgabetypen

Das Cmdlet **Get-CsOnlineUser** gibt Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.ADOCOnlineUser" zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsUser](get-csuser.md)

