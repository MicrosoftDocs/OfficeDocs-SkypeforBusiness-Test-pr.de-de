---
title: Set-CsAnalogDevice
TOCTitle: Set-CsAnalogDevice
ms:assetid: b05e729e-cdef-4c78-8ce7-b183c3208a93
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412843(v=OCS.15)
ms:contentKeyID: 49295108
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnalogDevice

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert ein vorhandenes Gerät in der Auflistung von Analoggeräten, die mit Lync Server verwaltet werden können. Ein Analoggerät ist ein Telefon oder ein anderes Gerät, das mit dem Telefonfestnetz (PSTN, Public Switched Telephone Network) verbunden ist. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsAnalogDevice -Identity <UserIdParameter> [-AnalogFax <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-Gateway <Fqdn>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird der Wert der Eigenschaft "LineUri" für das Analoggerät mit dem Identitätswert "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" geändert.

    Set-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -LineUri "TEL:+14255551298"

## BEISPIEL 2

Der Befehl in Beispiel 2 ändert das Gateway für jedes Analoggerät, das derzeit das Gateway 192.168.0.240 verwendet. Hierzu ruft der Befehl das Cmdlet **Get-CsAnalogDevice** zusammen mit dem Parameter "Filter" auf. Der Filterwert "{Gateway -eq "192.168.0.240"}" stellt sicher, dass nur Geräte zurückgegeben werden, bei denen die Eigenschaft "Gateway" den Wert "192.168.0.240" aufweist (der Vergleichsoperator "-eq" steht für "equal to"). Diese gefilterte Auflistung wird dann an das Cmdlet **Set-CsAnalogDevice** weitergeleitet, das für jedes Element der Auflistung den Wert der Eigenschaft "Gateway" in "192.168.1.100" ändert.

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"} | Set-CsAnalogDevice -Gateway "192.168.1.100"

## Detaillierte Beschreibung

Zu den Analoggeräten gehören Telefone, Faxgeräte, Modems und TTY/TTD-Geräte (Telekommunikationsgeräte für Hörgeschädigte), die mit dem Telefonfestnetz (Public Switched Telephone Network, PSTN) verbunden sind. Im Gegensatz zu Geräten, die Enterprise-VoIP (d. h. die Voice over IP-Implementierung von Microsoft) nutzen, werden bei analogen Geräten Informationen nicht als digitale Pakete übertragen. Stattdessen werden Informationen mithilfe eines Dauersignals übertragen. Dieses Signal wird gemeinhin als analoges Signal bezeichnet, daher der Begriff "analoge Geräte".

Damit Administratoren analoge Geräte verwalten können, ermöglicht Lync Server das Zuordnen analoger Geräte zu Active Directory-Kontaktobjekten. Nachdem ein Gerät einem Kontaktobjekt zugeordnet wurde, können Sie das analoge Gerät verwalten, indem Sie dem Kontakt Richtlinien und Wähleinstellungen zuweisen.

Mit dem Cmdlet **Set-CsAnalogDevice** können Sie die Eigenschaften der Kontaktobjekte ändern, die den Analoggeräten zugeordnet sind. Sie können beispielsweise den Active Directory-Anzeigenamen des Kontakts oder den Anschluss-URI (Uniform Resource Identifier) ändern, der dem Telefon zugeordnet ist.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsAnalogDevice** lokal ausführen: RTCUniversalUserAdmins. Berechtigungen zum Ausführen dieses Cmdlets für bestimmte Standorte oder spezifische Active Directory-Organisationseinheiten (OUs) können mit dem Cmdlet **Grant-CsOUPermission** zugewiesen werden. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnalogDevice"}

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
<td><p>Eindeutige ID für das zu ändernde Analoggerät. Analoge Geräte werden mithilfe des Active Directory-DN (Distinguished Name) des zugeordneten Kontaktobjekts identifiziert. Analoge Geräte verwenden standardmäßig eine GUID (Globally Unique Identifier) als allgemeinen Namen (Common Name, CN), deshalb verfügen Geräte in der Regel über einen Identitätswert wie den folgenden: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Daher ist es für Sie u. U. einfacher, analoge Geräte mit dem Cmdlet <strong>Get-CsAnalogDevice</strong> zu ändern, um die analogen Geräteobjekte zurückzugeben und an das Cmdlet <strong>Set-CsAnalogDevice</strong> weiterzuleiten.</p></td>
</tr>
<tr class="even">
<td><p><em>AnalogFax</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wenn das Analoggerät ein Faxgerät ist, ist dieser Parameter auf &quot;True&quot; ($True) festgelegt. Wenn das Analoggerät kein Faxgerät ist, ist dieser Parameter auf &quot;False&quot; ($False) festgelegt.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Konfiguriert den Active Directory-Anzeigenamen des Analoggeräts.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die in Lync angezeigte Telefonnummer. Die Eigenschaft &quot;DisplayNumber&quot; kann auf gewünschte Weise formatiert werden, z. B. 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Fqdn</p></td>
<td><p>Ermöglicht es Ihnen, zum Ändern von Kontaktinformationen eine Verbindung mit dem angegebenen Domänencontroller herzustellen. Zum Herstellen einer Verbindung mit einem bestimmten Domänencontroller verwenden Sie den Parameter &quot;DomainController&quot; und geben anschließend den Computernamen (z. B. &quot;atl-mcs-001&quot;) oder den vollqualifizierten Domänennamen (FQDN) (z. B. &quot;atl-mcs-001.litwareinc.com&quot;) an.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; ($True) kann das analoge Gerät mit Lync verwendet werden.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob das Kontaktobjekt für das Analoggerät für Enterprise-VoIP (d. h. die VoIP-Lösung von Microsoft) aktiviert wurde. Mit Enterprise-VoIP können Benutzer Anrufe über das Internet tätigen und müssen nicht länger das herkömmliche Telefonnetz nutzen.</p></td>
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
<td><p><em>Gateway</em></p></td>
<td><p>Optional</p></td>
<td><p>Fqdn</p></td>
<td><p>Die IP-Adresse des PSTN-Gateways, das vom Analoggerät verwendet wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Rufnummer des Analoggeräts. Der Anschluss-URI muss im E.164-Format angegeben werden und mit dem Präfix &quot;TEL:&quot; beginnen. Beispiel: TEL:+14255551297. Durchwahlnummern werden an das Ende des Anschluss-URI angehängt. Beispiel: TEL:+14255551297;ext=51297.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Gibt ein Objekt zurück, das das Telefon in einem öffentlichen Bereich darstellt.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Eindeutige ID, die eine Kommunikation zwischen dem Analoggerät und SIP-Geräten wie Lync 2013 ermöglicht. Die SIP-Adresse muss mit dem Präfix &quot;sip:&quot; beginnen. Beispiel: &quot;sip:bldg14lobby@litwareinc.com&quot;.</p></td>
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

Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact-Objekt. Das Cmdlet **Set-CsAnalogDevice** akzeptiert weitergeleitete Instanzen des Analoggeräteobjekts.

## Rückgabetypen

Das Cmdlet **Set-CsAnalogDevice** gibt standardmäßig keine Objekte oder Werte zurück. Wenn Sie jedoch den Parameter "PassThru" verwenden, gibt das Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact" zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)

