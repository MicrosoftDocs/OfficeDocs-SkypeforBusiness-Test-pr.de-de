---
title: Set-CsExUmContact
TOCTitle: Set-CsExUmContact
ms:assetid: c0fe0fdc-6fea-4334-8645-24ffd494db07
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412944(v=OCS.15)
ms:contentKeyID: 49295292
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExUmContact

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert ein vorhandenes Kontaktobjekt für eine automatische Telefonzentrale oder den Teilnehmerzugriff für den gehosteten Exchange Unified Messaging (UM)-Dienst. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsExUmContact -Identity <UserIdParameter> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die Eigenschaft "AutoAttendant" des Exchange UM-Kontakts mit der SIP-Adresse "exumsa4@fabrikam.com" auf "True" festgelegt. Zunächst wird das Cmdlet **Get-CsExUmContact** aufgerufen, um das Kontaktobjekt abzurufen. (Alternativ kann auch der Active Directory-Anzeigename, der Benutzerprinzipalname (User Principal Name, UPN) oder der Anmeldename des Kontakts verwendet werden.) Dieser Befehl ruft den einen Kontakt mit der angegebenen Identität ab. Dieser Kontakt wird anschließend an das Cmdlet **Set-CsExUmContact** übergeben, und der Parameter "AutoAttendant" wird auf "True" festgelegt.

    Get-CsExUmContact -Identity sip:exumsa4@fabrikam.com | Set-CsExUmContact -AutoAttendant $True

## BEISPIEL 2

Dieses Beispiel ist mit Beispiel 1 identisch, der Kontakt wird jedoch nicht über einen Aufruf des Cmdlets **Get-CsExUmContact** und Übergabe des Objekts an das Cmdlet **Set-CsExUmContact** abgerufen. Stattdessen wird an das Cmdlet **Set-CsExUmContact** die Identität des Kontakts übergeben, der geändert werden soll. Beachten Sie das Format für den Identitätswert: Es muss sich in diesen Fall um den vollständigen Distinguished Name (DN) des Kontaktobjekts handeln, der eine automatisch generierte GUID enthält. (Diese wird bei der Erstellung des Kontakts generiert.) Anschließend wird der Parameter "AutoAttendant" des Kontakts auf "True" festgelegt.

    Set-CsExUmContact -Identity "CN={1bf6208d-2847-45d0-828f-636f14da858b},OU=ExUmContacts,DC=litwareinc,DC=com" -AutoAttendant $True

## Detaillierte Beschreibung

Lync Server wird mit Exchange UM eingesetzt, um verschiedene VoIP-bezogene Funktionen wie automatische Telefonzentralen oder den Teilnehmerzugriff bereitzustellen. Wenn Exchange UM nicht als lokaler, sondern als gehosteter Dienst bereitgestellt wird, müssen zum Verwenden einer automatischen Telefonzentrale und des Teilnehmerzugriffs Kontaktobjekte mit Windows PowerShell erstellt werden. Diese Objekte werden durch Aufruf des Cmdlets **New-CsExUmContact** erstellt und können später mithilfe des Cmdlets **Set-CsExUmContact** geändert werden.

Die einfachste Methode zur Verwendung dieses Cmdlets besteht darin, zunächst mit dem Cmdlet **Get-CsExUmContact** eine Instanz des Kontaktobjekts abzurufen, das Sie ändern möchten. Leiten Sie die Ausgabe des Cmdlet-Befehls **Get-CsExUmContact** an das Cmdlet **Set-CsExUmContact** weiter, und weisen Sie Parameterwerte für die Eigenschaften zu, die Sie ändern möchten. (Ausführliche Informationen finden Sie in den Beispielen weiter unten in diesem Thema.) Alternativ können Sie das Cmdlet **Set-CsExUmContact** aufrufen und ihm die Identität des Kontaktobjekts übergeben, das geändert werden soll.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsExUmContact** lokal auszuführen: RTCUniversalUserAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExUmContact"}

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
<td><p>Die eindeutige ID für das Kontaktobjekt, das geändert werden soll. Kontaktidentitäten können in den folgenden vier Formaten angegeben werden: als 1) SIP-Adresse des Kontakts, 2) Benutzerprinzipalname (User Principal Name, UPN) des Kontakts, 3) Domänen- und Anmeldename des Kontakts (mit dem Format &quot;Domäne\Anmeldename&quot;, z. B. &quot;litwareinc\exum1&quot;) und 4) Active Directory-Anzeigename des Kontakts (z. B. &quot;Team Auto Attendant&quot;).</p>
<p>Vollständiger Datentyp: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendant</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Legen Sie den Parameter auf &quot;True&quot; fest, wenn es sich bei dem Kontaktobjekt um eine automatische Telefonzentrale handelt. Dieser Parameter ist standardmäßig auf &quot;False&quot; festgelegt.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Eine Beschreibung dieses Kontakts. Anhand der Beschreibung können Administratoren den Typ des Kontakts (automatische Telefonzentrale oder Teilnehmerzugriff), den Standort, den Anbieter sowie andere Informationen ermitteln, die Aufschluss über den Zweck der einzelnen Exchange UM-Kontakte geben.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die Telefonnummer des Kontakts. Die Anzeigenummern für jeden Kontakt müssen eindeutig sein. (Es ist nicht zulässig, dass zwei Exchange UM-Kontakte über dieselbe Anzeigenummer verfügen.) Eine Änderung dieses Werts führt auch zu einer Änderung der Eigenschaft &quot;LineURI&quot;.</p>
<p>Dieser Wert kann mit einem Pluszeichen (+) beginnen und eine beliebige Anzahl von Ziffern umfassen. Die erste Ziffer darf keine Null sein.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>FQDN</p></td>
<td><p>Ermöglicht die Angabe eines Domänencontrollers. Wenn kein Domänencontroller angegeben ist, wird der erste verfügbare Domänencontroller verwendet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob der Kontakt für Lync Server aktiviert ist. Durch das Festlegen dieses Parameters auf &quot;False&quot; wird der Kontakt deaktiviert, wodurch die diesem Kontakt zugeordnete automatische Telefonzentrale bzw. der Teilnehmerzugriff nicht mehr funktioniert.</p>
<p>Wenn Sie ein Konto über den Parameter &quot;Enabled&quot; deaktivieren, werden die diesem Konto zugeordneten Informationen (einschließlich der zugewiesenen gehosteten Voicemailrichtlinien) beibehalten. Wird das Konto zu einem späteren Zeitpunkt über den Parameter &quot;Enable&quot; erneut aktiviert, werden die zugeordneten Kontoinformationen wiederhergestellt.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob der Kontakt für Enterprise-VoIP aktiviert ist. Ist dieser Wert auf &quot;False&quot; gesetzt, stehen die Funktionen für die automatische Telefonzentrale und der Teilnehmerzugriff für diesen Kontakt nicht länger zur Verfügung.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Gibt an, wo die Chatnachrichtensitzungen des Kontakts archiviert werden. Zulässige Werte:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Gibt die Ergebnisse des Befehls zurück. Standardmäßig wird von diesem Cmdlet keine Ausgabe generiert.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die SIP-Adresse des Kontakts. Dabei muss es sich um eine neue Adresse handeln, die noch nicht als Benutzer oder Kontakt in Active Directory-Domänendienste vorhanden ist.</p>
<p>Eine Änderung dieses Werts wirkt sich auch auf die in der Eigenschaft &quot;OtherIpPhone&quot; gespeicherte SIP-Adresse aus.</p>
<p>Die SIP-Adresse kann in den <strong>Get-CsExUmContact</strong>-Cmdlet-Befehlen als Identitätswert verwendet werden, um spezifische Kontakte abzurufen. Wenn Sie dieses Cmdlet aufrufen, wird die neue SIP-Adresse verwendet; Abfragen unter Verwendung der alten SIP-Adresse geben kein Objekt zurück.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact-Objekt. Akzeptiert eine weitergeleitete Eingabe von Exchange UM-Kontaktobjekten.

## Rückgabetypen

Mit diesem Cmdlet wird ein Objekt vom Typ "Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact" geändert. Bei Verwendung mit dem Parameter "PassThru" wird auch ein Objekt dieses Typs zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

