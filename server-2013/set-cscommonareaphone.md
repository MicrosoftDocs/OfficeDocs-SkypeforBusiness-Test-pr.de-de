---
title: Set-CsCommonAreaPhone
TOCTitle: Set-CsCommonAreaPhone
ms:assetid: 765ab74c-33ca-4b17-ba15-edb2fe559ebb
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398579(v=OCS.15)
ms:contentKeyID: 49294432
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCommonAreaPhone

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert die Eigenschaftswerte eines Telefons im öffentlichen Bereich, das mit Lync Server verwaltet wird. Telefone in öffentlichen Bereichen sind Telefone in Eingangsbereichen von Gebäuden, Aufenthaltsräumen für Mitarbeiter oder in anderen Bereichen, in denen sie oftmals von vielen Menschen und für unterschiedliche Benutzer genutzt werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird der Active Directory-Anzeigename für das Telefon im öffentlichen Bereich mit der Telefonnummer 1-425-555-6710 geändert. Dazu wird zunächst das Cmdlet **Get-CsCommonAreaPhone** mit dem Parameter "Filter" aufgerufen. Der Filterwert "{LineUri -eq "tel:+14255556710"}" beschränkt die zurückgegebenen Daten auf das Telefon im öffentlichen Bereich, bei dem die Eigenschaft "LineUri" den Wert "tel:+14255556710" aufweist. Das zurückgegebene Objekt wird dann an das Cmdlet **Set-CsCommonAreaPhone** weitergeleitet, das den Wert der Eigenschaft "DisplayName" auf "Employee Lounge" festlegt.

    Get-CsCommonAreaPhone -Filter {LineUri -eq "tel:+14255556710"} | Set-CsCommonAreaPhone -DisplayName "Employee Lounge"

## BEISPIEL 2

Der Befehl in Beispiel 2 aktiviert alle Telefone in öffentlichen Bereichen, die derzeit für die Verwendung in der Organisation konfiguriert sind. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsCommonAreaPhone** ohne Parameter auf, um eine Auflistung aller Telefone in öffentlichen Bereichen zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Set-CsCommonAreaPhone** weitergeleitet, das für jedes Element in der Auflistung die Eigenschaft "Enabled" auf "True" festlegt.

    Get-CsCommonAreaPhone | Set-CsCommonAreaPhone -Enabled $True

## BEISPIEL 3

In Beispiel 3 wird allen Telefonen in öffentlichen Bereichen eine allgemeine Beschreibung hinzugefügt, bei denen der Eigenschaft "Description" kein Wert zugewiesen wurde. Dazu wird das Cmdlet **Get-CsCommonAreaPhone** mit dem Parameter "Filter" aufgerufen. Der Filterwert "{Description -eq $Null}" stellt sicher, dass nur Telefone in öffentlichen Bereichen zurückgegeben werden, deren Eigenschaft "Description" einen NULL-Wert aufweist. Die gefilterte Auflistung wird dann an das Cmdlet **Set-CsCommonAreaPhone** weitergeleitet, das für jedes Element in der Auflistung die allgemeine Beschreibung "Common area phone" zuweist.

    Get-CsCommonAreaPhone -Filter {Description -eq $Null} | Set-CsCommonAreaPhone -Description "Common area phone"

## Detaillierte Beschreibung

Telefone in öffentlichen Bereichen sind IP-Telefone, die keinem einzelnen Benutzer zugeordnet sind. Sie befinden sich nicht in einem Büro, sondern normalerweise in Eingangsbereichen, Cafeterias, Aufenthaltsräumen für Mitarbeiter, Besprechungszimmern und anderen Bereichen, in denen viele Menschen zusammenkommen. Die Verwaltung solcher Telefone stellt für Administratoren eine Herausforderung dar, da die Telefonnutzung in Lync Server normalerweise anhand verschiedener VoIP-Richtlinien und Wähleinstellungen verwaltet wird, die einzelnen Benutzern zugewiesen sind. Telefonen in öffentlichen Bereichen sind keine einzelnen Benutzer zugewiesen.

Eine Methode zur Bewältigung dieser Herausforderung besteht darin, Active Directory-Kontaktobjekte für alle Telefone in öffentlichen Bereichen zu erstellen. (Diese Kontaktobjekte können mit dem Cmdlet **New-CsCommonAreaPhone** erstellt werden.) Diesen Kontaktobjekten können dann genau wie Benutzerkonten Richtlinien und VoIP-Einstellungen zugewiesen werden. Auf diese Weise können Sie Telefone in öffentlichen Bereichen verwalten, auch wenn sie keinem einzelnen Benutzer zugeordnet sind. Wenn Benutzer beispielsweise nicht die Möglichkeit haben sollen, Anrufe von einem Telefon im öffentlichen Bereich aus weiterzuleiten oder zu parken, können Sie eine VoIP-Richtlinie erstellen, die die Weiterleitung und das Parken von Anrufen verhindert. Weisen Sie diese Richtlinie dann dem Telefon im öffentlichen Bereich zu. (Genauer gesagt, weisen Sie diese Richtlinie dem Kontaktobjekt zu, das für das Telefon im öffentlichen Bereich steht.) Mit dem folgenden Befehl wird allen Telefonen in öffentlichen Bereichen die VoIP-Richtlinie "CommonAreaPhoneVoicePolicy" zugewiesen:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

Mit dem Cmdlet **Set-CsCommonAreaPhone** können Sie die Eigenschaften der Kontaktobjekte ändern, die Telefonen in öffentlichen Bereichen zugeordnet sind. Sie können unter anderem den Active Directory-Anzeigenamen des Kontakts oder den Anschluss-URI (Uniform Resource Identifier) ändern, der dem Telefon zugeordnet ist. Sie können auch den Parameter "Enabled" verwenden, um das Konto für die Verwendung mit Lync Server zu aktivieren und zu deaktivieren.

Darüber hinaus können Sie mit den Cmdlets vom Typ "CsClientPolicy" das "Hotdesking" für Telefone für gemeinsame Bereiche konfigurieren. Bei einem sog. Hotdesk-Telefon können sich Benutzer über ihre Lync Server-Anmeldeinformationen beim Telefon anmelden. Dadurch erhalten die Benutzer u. a. einen einfachen Zugriff auf ihre Kontakte. Weitere Informationen finden Sie im Hilfethema zum Cmdlet [Set-CsClientPolicy](set-csclientpolicy.md).

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsCommonAreaPhone** lokal ausführen: RTCUniversalUserAdmins. Berechtigungen zum Ausführen dieses Cmdlets für bestimmte Standorte oder spezifische Active Directory-Organisationseinheiten (OUs) können mit dem Cmdlet **Grant-CsOUPermission** zugewiesen werden. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCommonAreaPhone"}

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
<td><p><em>Identity</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>UserIdParameter</p></td>
<td><p>Eindeutige ID des Telefons im öffentlichen Bereich. Telefone in öffentlichen Bereichen werden mit dem Distinguished Name des zugeordneten Kontaktobjekts in Active Directory identifiziert. Telefone in öffentlichen Bereichen verwenden standardmäßig eine GUID (Globally Unique Identifier) als allgemeinen Namen. Telefone weisen daher in der Regel etwa den folgenden Identitätswert auf: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Daher ist es möglicherweise einfacher, Telefone in öffentlichen Bereichen mit dem Cmdlet <strong>Get-CsCommonAreaPhone</strong> abzurufen und dann die zurückgegebenen Objekte an das Cmdlet <strong>Set-CsCommonAreaPhone</strong> weiterzuleiten.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Ermöglicht es Ihnen, das Active Directory-Beschreibungsattribut für ein Telefon im öffentlichen Bereich zu ändern. Dies bietet Ihnen die Möglichkeit, zusätzliche Informationen zum Telefon bereitzustellen. So können Sie beispielsweise Angaben darüber machen, wer bei Problemen mit dem Telefon kontaktiert werden soll.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Ermöglicht es Ihnen, den Active Directory-Anzeigenamen des Telefons im öffentlichen Bereich zu ändern.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die in Lync angezeigte Telefonnummer. Die Eigenschaft &quot;DisplayNumber&quot; kann nach Belieben formatiert werden, z. B. 1-800-555-1234, 1-(800)-555-1234 oder 1.800.555.1234. Beachten Sie bei der Wahl einer Anzeigenummer, dass diese Nummer nur dann auf dem Anzeigebildschirm des Telefons im öffentlichen Bereich angezeigt wird, wenn sie normalisiert werden kann. (Normalisierung ist das Verfahren zum Übersetzen von Nummernzeichenfolgen in ein standardmäßiges Telefonnummernformat.) Wenn für das Telefonnummernformat, das beim Konfigurieren der Anzeigenummer verwendet wird, keine Normalisierungsregel vorhanden ist, zeigt der Anzeigebildschirm des Telefons im öffentlichen Bereich den Wert der Eigenschaft &quot;LineUri&quot; anstelle des Werts der Eigenschaft &quot;DisplayNumber&quot; an.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Fqdn</p></td>
<td><p>Ermöglicht es Ihnen, zum Ändern von Kontaktinformationen eine Verbindung mit dem angegebenen Domänencontroller herzustellen. Zum Herstellen einer Verbindung mit einem bestimmten Domänencontroller nehmen Sie den Parameter &quot;DomainController&quot; auf und geben anschließend den Computernamen (z. B. &quot;atl-mcs-001&quot;) oder den vollqualifizierten Domänennamen (z. B. &quot;atl-mcs-001.litwareinc.com&quot;) an.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob das Kontaktobjekt für das Telefon im öffentlichen Bereich für Lync Server aktiviert wurde.</p>
<p>Wenn Sie einen Kontakt mithilfe des Parameters &quot;Enabled&quot; deaktivieren, werden die diesem Konto zugeordneten Informationen beibehalten (einschließlich der zugewiesenen Richtlinien sowie der Information, ob der Benutzer Enterprise-VoIP, die Remoteanrufsteuerung und/oder die Voicemailintegration nutzen darf). Wird das Konto zu einem späteren Zeitpunkt über den Parameter &quot;Enabled&quot; wieder aktiviert, werden die zugeordneten Kontoinformationen wiederhergestellt.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob das Kontaktobjekt für das Telefon im öffentlichen Bereich für Enterprise-VoIP aktiviert wurde, die von Microsoft angebotene VoIP-Lösung (Voice over Internet Protocol). Mit Enterprise-VoIP können Benutzer Anrufe über das Internet tätigen und müssen nicht länger das herkömmliche Telefonnetz nutzen.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Gibt an, ob die Chatsitzungen des Kontakts archiviert werden. Zulässige Werte:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Telefonnummer des Telefons im öffentlichen Bereich. Der Anschluss-URI (Uniform Resource Identifier) muss im E.164-Format angegeben werden und mit dem Präfix &quot;TEL:&quot; beginnen. Beispiel: TEL:+14255551297. Durchwahlnummern werden an das Ende des Anschluss-URI angehängt. Beispiel: TEL:+14255551297; ext=51297.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Gibt ein Objekt zurück, das das Telefon in einem öffentlichen Bereich darstellt.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Eindeutiger Bezeichner, mit dem das Telefon im öffentlichen Bereich mit SIP-Geräten wie Lync kommunizieren kann. Die SIP-Adresse muss mit dem Präfix &quot;sip&quot;: beginnen und eine gültige SIP-Domäne enthalten. Beispiel: sip:bldg14lobby@litwareinc.com.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact-Objekt.

## Rückgabetypen

Das Cmdlet **Set-CsCommonAreaPhone** gibt standardmäßig keine Objekte oder Werte zurück. Wenn Sie jedoch den Parameter "PassThru" einschließen, gibt das Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact" zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)

