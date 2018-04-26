---
title: Move-CsCommonAreaPhone
TOCTitle: Move-CsCommonAreaPhone
ms:assetid: af5f832c-1be9-4495-ba1a-c10ca50d7b29
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412837(v=OCS.15)
ms:contentKeyID: 49295098
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsCommonAreaPhone

 

_**Letztes Änderungsdatum des Themas:** 2015-04-02_

Verschiebt ein oder mehrere Telefone für öffentliche Bereichen in einen neuen Registrierungsstellenpool. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Move-CsCommonAreaPhone -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 verschiebt das Telefon für öffentliche Bereiche mit dem Identitätswert "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" in den Registrierungsstellenpool "atl-cs-001.litwareinc.com".

    Move-CsCommonAreaPhone -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## BEISPIEL 2

In Beispiel 2 wird das Telefon für öffentliche Bereiche mit dem Active Directory-Anzeigenamen "Building 31 Cafeteria" in den Registrierungsstellenpool "atl-cs-001.litwareinc.com" verschoben. Hierzu wird zunächst das Cmdlet **Get-CsCommonAreaPhone** ohne Parameter aufgerufen, um eine Auflistung aller derzeit in der Organisation verwendeten Telefone für öffentliche Bereiche zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Telefone herausfiltert, bei denen die Eigenschaft "DisplayName" den Wert "Building 31 Cafeteria" aufweist. Diese gefilterte Auflistung wird dann an das Cmdlet **Move-CsCommonAreaPhone** weitergeleitet, das jedes Telefon in der Auflistung in "atl-cs-001.litwareinc.com" verschiebt.

    Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -eq "Building 31 Cafeteria"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## BEISPIEL 3

In Beispiel 3 werden alle Telefone für öffentliche Bereichen, die sich derzeit im Registrierungsstellenpool "dublin-cs-001.litwareinc.com" befinden, in den Registrierungsstellenpool "atl-cs-001.litwareinc.com" verschoben. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsCommonAreaPhone** ohne Parameter auf. Damit wird eine Auflistung aller Telefone für öffentliche Bereiche zurückgegeben, die für die Verwendung in der Organisation konfiguriert wurden. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Telefone für öffentliche Bereiche herausfiltert, bei denen "RegistrarPool" den Wert "dublin-cs-001.litwareinc.com" aufweist. Diese Auflistung wird dann an das Cmdlet **Move-CsCommonAreaPhone** weitergeleitet, das jedes Telefon in der Auflistung in den neuen Registrierungsstellenpool "atl-cs-001.litwareinc.com" verschiebt.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## BEISPIEL 4

Beispiel 4 ist eine Variante des Befehls aus Beispiel 3. In diesem Fall werden die Telefone in öffentlichen Bereichen jedoch nicht in einen neuen Registrierungsstellenpool verschoben, sondern einer neuen benutzerbasierten VoIP-Richtlinie zugewiesen. Hierzu wird beim Aufrufen des Cmdlets **Move-CsCommonAreaPhone** der Parameter "PassThru" angegeben, damit Sie die Objekte für Telefone in öffentlichen Bereichen weiterleiten können. (**Move-CsCommonAreaPhone** leitet standardmäßig keine Objekte weiter.) Nachdem die Telefone verschoben wurden, werden die Telefonobjekte an das Cmdlet **Grant-CsVoicePolicy** weitergeleitet, das den einzelnen gerade verschobenen Telefonen die VoIP-Richtlinie "AtlantaVoicePolicy" zuweist.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com -PassThru | Grant-CsVoicePolicy -PolicyName AtlantaVoicePolicy

## Detaillierte Beschreibung

Telefone für öffentliche Bereiche sind IP-Telefone, die keinem einzelnen Benutzer zugeordnet sind. Sie befinden sich nicht in einem Büro, sondern normalerweise in Eingangsbereichen, Cafeterias, Aufenthaltsräumen für Mitarbeiter, Besprechungszimmern und anderen Bereichen, in denen viele Menschen zusammenkommen. Die Verwaltung solcher Telefone stellt für Administratoren eine Herausforderung dar, da die Telefonnutzung in Lync Server normalerweise anhand verschiedener VoIP-Richtlinien und Wähleinstellungen verwaltet wird, die einzelnen Benutzern zugewiesen sind. Telefonen für öffentliche Bereiche sind keine einzelnen Benutzer zugewiesen.

Eine Lösung besteht darin, Active Directory-Kontaktobjekte für alle Telefone in öffentlichen Bereichen zu erstellen. (Diese Kontaktobjekte können mit dem Cmdlet **New-CsCommonAreaPhone** erstellt werden.) Diesen Kontaktobjekten können dann genau wie Benutzerkonten Richtlinien und VoIP-Einstellungen zugewiesen werden. Auf diese Weise können Sie Telefone in öffentlichen Bereichen verwalten, auch wenn sie keinem einzelnen Benutzer zugeordnet sind. Wenn Benutzer beispielsweise nicht die Möglichkeit haben sollen, Anrufe von einem Telefon in einem öffentlichen Bereich aus weiterzuleiten oder zu parken, können Sie eine VoIP-Richtlinie erstellen, die die Weiterleitung und das Parken von Anrufen verhindert. Weisen Sie diese Richtlinie dann dem Telefon im öffentlichen Bereich zu. (Genauer gesagt, weisen Sie diese Richtlinie dem Kontaktobjekt zu, das für das Telefon im öffentlichen Bereich steht.)

Mit dem Cmdlet **Move-CsCommonAreaPhone** können Sie ein bestehendes Telefon in einem öffentlichen Bereich in einen neuen Registrierungsstellenpool verschieben.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Move-CsCommonAreaPhone** lokal ausführen: RTCUniversalUserAdmins. Berechtigungen zum Ausführen dieses Cmdlets für bestimmte Standorte oder spezifische Active Directory-Organisationseinheiten (OUs) können mit dem Cmdlet **Grant-CsOUPermission** zugewiesen werden. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsCommonAreaPhone"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Eindeutige ID des Telefons im öffentlichen Bereich. Telefone in öffentlichen Bereichen werden mit dem Distinguished Name des zugeordneten Kontaktobjekts in Active Directory identifiziert. Telefone in öffentlichen Bereichen verwenden standardmäßig eine GUID (Globally Unique Identifier) als allgemeinen Namen (Common Name, CN), deshalb verfügen Telefone in der Regel über einen Identitätswert wie den folgenden: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Der vollqualifizierte Domänenname (FQDN) des Registrierungsstellenpools, in den das Telefon für öffentliche Bereiche verschoben werden soll. Beispiel: atl-cs-001.litwareinc.com. Neben einem Registrierungsstellenpool kann als Ziel auch der FQDN eines Hostinganbieters angegeben werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Ermöglicht es Ihnen, zum Verschieben eines Telefons für öffentliche Bereiche eine Verbindung mit dem angegebenen Domänencontroller herzustellen. Zum Herstellen einer Verbindung mit einem bestimmten Domänencontroller nehmen Sie den Parameter &quot;DomainController&quot; auf und geben anschließend den Computernamen (z. B. &quot;atl-cs-001&quot;) oder den vollqualifizierten Domänennamen (z. B. &quot;atl-cs-001.litwareinc.com&quot;) an.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Wird dieser Parameter angegeben, wird das Telefon für öffentliche Bereiche verschoben, zugeordnete Daten (z. B. dem Gerät zugewiesene Richtlinien) werden jedoch gelöscht. Wenn dieser Parameter nicht angegeben wird, wird das Telefon mit den zugeordneten Daten verschoben.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Durch Angabe des Parameters wird der Computer angewiesen, alle Fehler zu ignorieren, die ggf. in der Back-End-Datenbank auftreten, und das Telefon für allgemeine Bereiche trotz dieser Fehler zu verschieben.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ermöglicht das Übergeben eines Benutzerobjekts für das Benutzerkonto, das verschoben wird. Das Cmdlet <strong>Move-CsCommonAreaPhone</strong> leitet standardmäßig keine Objekte weiter.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Dieser Parameter wird nur für Lync Online verwendet. Er sollte nicht mit einer lokalen Implementierung von Lync Server verwendet werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Zeichenfolge. Das Cmdlet **Move-CsCommonAreaPhone** akzeptiert einen weitergeleiteten Zeichenfolgenwert, der die Identität des Telefons in öffentlichen Bereichen repräsentiert.

## Rückgabetypen

Das Cmdlet **Move-CsCommonAreaPhone** gibt standardmäßig keine Objekte oder Werte zurück. Wenn Sie jedoch den Parameter "PassThru" verwenden, gibt das Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact" zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

