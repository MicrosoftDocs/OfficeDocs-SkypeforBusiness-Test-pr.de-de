---
title: Set-CsVoiceRoute
TOCTitle: Set-CsVoiceRoute
ms:assetid: b786aec0-946e-4ce5-812e-25e5d8cfa4d5
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412893(v=OCS.15)
ms:contentKeyID: 49295180
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoute

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine VoIP-Route. VoIP-Routen umfassen Anweisungen, anhand derer Lync Server ermittelt, wie Anrufe von Enterprise-VoIP-Benutzern bei Telefonnummern im Telefonfestnetz (Public Switched Telephone Network, PSTN) oder in einer Nebenstellenanlage (Private Branch Exchange, PBX) weitergeleitet werden sollen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Mit diesem Befehl wird die Beschreibung der VoIP-Route "Route1" auf "Test Route" festgelegt.

    Set-CsVoiceRoute -Identity Route1 -Description "Test Route"

## BEISPIEL 2

In diesem Beispiel wird die VoIP-Route mit dem Identitätswert "Route1" geändert, um die PSTN-Verwendung "Long Distance" zur Liste der Verwendungen für diese VoIP-Route hinzuzufügen. "Long Distance" muss sich in der Liste der globalen PSTN-Verwendungen befinden (die mit dem Aufruf des Cmdlets **Get-CsPstnUsage** abgerufen werden kann).

    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"}

## BEISPIEL 3

In diesem Beispiel wird die VoIP-Route "Route1" geändert, um die Liste der PSTN-Verwendungen für diese Route mit allen vorhandenen Verwendungen für die Organisation aufzufüllen. Mit dem ersten Befehl in diesem Beispiel wird die Liste der globalen PSTN-Verwendungen abgerufen. Beachten Sie, dass der Aufruf des Cmdlets **Get-CsPstnUsage** in Klammern aufgeführt wird. Dies bedeutet, dass zuerst ein Objekt mit den PSTN-Verwendungsinformationen abgerufen wird. (Da nur eine globale PSTN-Verwendung vorhanden ist, wird nur ein Objekt abgerufen.) Mit dem Befehl wird dann die Eigenschaft "Usage" dieses Objekts abgerufen. Diese Eigenschaft, die eine Liste der PSTN-Verwendungen enthält, wird der Variablen "$x" zugewiesen. In der zweiten Zeile dieses Beispiels wird das Cmdlet **Set-CsVoiceRoute** aufgerufen, um die VoIP-Route mit dem Identitätswert "Route1" zu ändern. Beachten Sie den Wert, der an den Parameter "PstnUsages" übergeben wird: @{replace=$x}. Dieser Wert ersetzt alle Einträge in der Liste "PstnUsages" für diese Route durch die Inhalte der Variablen "$x", die die PSTN-Verwendungen enthält, die in Zeile 1 abgerufen wurden.

    $x = (Get-CsPstnUsage).Usage
    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{replace=$x}

## BEISPIEL 4

Mit diesem Befehlssatz wird die Eigenschaft "Name" der VoIP-Route mit dem Identitätswert "Route1" zu "RouteA" geändert. Durch die Änderung der Eigenschaft "Name" wird automatisch auch die Eigenschaft "Identity" geändert, in diesem Fall zu "RouteA".

In der ersten Zeile wird das Cmdlet **Get-CsVoiceRoute** aufgerufen, um die VoIP-Route mit dem Identitätswert "Route1" abzurufen. Das zurückgegebene Objekt wird in der Variablen "$x" gespeichert. Als Nächstes wird der Eigenschaft "Name" dieses Objekts der Zeichenfolgenwert "RouteA" zugewiesen. Schließlich wird das Objekt (in Variable "$x") an den Parameter "Instance" des Cmdlets **Set-CsVoiceRoute** übergeben, um die Änderung durchzuführen.

    $x = Get-CsVoiceRoute -Identity Route1
    $x.Name = "RouteA"
    Set-CsVoiceRoute -Instance $x

## BEISPIEL 5

In diesem Beispiel wird die VoIP-Route "Route1" geändert, und die Liste der PSTN-Gateways (PstnGatewayList) wird mit der Serverrolle des Gateways mit dem Identitätswert "PstnGateway:192.168.0.100" aufgefüllt. In der ersten Zeile des Befehls wird das Cmdlet **Get-CsVoiceRoute** aufgerufen, um die VoIP-Route abzurufen, die geändert werden soll, in diesem Fall "Route1". Als Nächstes wird die Add-Methode für die Eigenschaft "PstnGatewayList" von "Route1" aufgerufen. Dann wird die Add-Methode an die Identität des Diensts übergeben, der hinzugefügt werden soll. Abschließend wird das Cmdlet **Set-CsVoiceRoute** aufgerufen, und der Parameter "Instance" wird an die Variable "$y" übergeben, sodass "Route1" (gespeichert in "$y") mit dem neu hinzugefügten PSTN-Gateway aktualisiert wird.

    $y = Get-CsVoiceRoute -Identity Route1
    $y.PstnGatewayList.Add("PstnGateway:192.168.0.100")
    Set-CsVoiceRoute -Instance $y

## Detaillierte Beschreibung

Verwenden Sie dieses Cmdlet, um eine vorhandene VoIP-Route zu ändern. VoIP-Routen werden VoIP-Richtlinien über die Verwendung eines Telefonfestnetzes (Public Switched Telephone Network, PSTN) zugeordnet. Eine VoIP-Route umfasst einen regulären Ausdruck, der festlegt, welche Telefonnummern über eine vorgegebene VoIP-Route weitergeleitet werden: alle Telefonnummern, die mit dem regulären Ausdruck übereinstimmen, werden über diese Route weitergeleitet.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsVoiceRoute** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoute"}

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
<td><p><em>AlternateCallerId</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Wenn der Parameter &quot;SuppressCallerId&quot; auf &quot;True&quot; festgelegt ist, wird den Empfängern anstelle der tatsächlichen Nummer des Anrufers der Wert des Parameters &quot;AlternateCallerId&quot; angezeigt. Diese Nummer muss eine gültige Nummer sein, die für eine Abteilung innerhalb der Organisation steht, z. B. die Support- oder Personalabteilung.</p>
<p>Wenn der Parameter &quot;SuppressCallerId&quot; auf &quot;False&quot; festgelegt ist, wird der Parameter &quot;AlternateCallerId&quot; ignoriert.</p>
<p>Dieser Wert muss mit dem regulären Ausdruck &quot;(\+)?[1-9]\d*(;ext=[1-9]\d*)?&quot; übereinstimmen. Anders ausgedrückt, der Wert kann mit einem Pluszeichen (+) beginnen, dies ist jedoch nicht erforderlich. Der Wert muss sich aus einer beliebigen Anzahl von Ziffern zusammensetzen, ggf. gefolgt von einer Durchwahlnummer, die mit &quot;;ext=&quot; beginnt, gefolgt von einer beliebigen Anzahl von Ziffern. (Beachten Sie, dass die Zeichenfolge bei Angabe einer Durchwahlnummer in doppelte Anführungszeichen gesetzt werden muss.)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Eine Beschreibung des Zwecks der Telefonroute.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Die eindeutige Identität der VoIP-Route. (Wenn der Routenname ein Leerzeichen wie z. B. in &quot;Test Route&quot; enthält, muss die gesamte Zeichenfolge in Klammern eingeschlossen werden.)</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>Route</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen. Dieses Objekt muss ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route&quot; sein und kann durch Aufrufen des Cmdlets <strong>Get-CsVoiceRoute</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberPattern</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ein regulärer Ausdruck, der die Telefonnummern angibt, auf die diese Route angewendet wird. Nummern, die diesem Muster entsprechen, werden gemäß der weiteren Routingeinstellungen weitergeleitet. Beispielsweise gibt das standardmäßige Nummernmuster &quot;[0-9]{10}&quot; eine zehnstellige Nummer an, die beliebige Ziffern zwischen 0 und 9 enthält.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>Eine Nummer kann in mehrere VoIP-Routen aufgelöst werden. Die Priorität bestimmt die Reihenfolge, in der die Routen angewendet werden, wenn mehr als eine Route möglich ist.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Einem Vermittlungsserver können mehrere Gateways zugeordnet werden. Dieser Parameter enthält eine Liste der Gateways, die dieser VoIP-Route zugeordnet sind. Bei den Mitgliedern dieser Liste muss es sich um die Dienstidentität des PSTN-Gateways oder Vermittlungsservers handeln. Der Wert kann nur auf einen Vermittlungsserver verweisen, wenn der Vermittlungsserver für Microsoft Office Communications Server 2007 oder Microsoft Office Communications Server 2007 R2 konfiguriert ist. Für Lync Server muss ein PSTN-Gateway verwendet werden. Die Dienstidentität ist eine Zeichenfolge im Format &quot;ServiceRole:FQDN&quot;, wobei &quot;ServiceRole&quot; der Name der Dienstrolle (PSTNGateway) und &quot;FQDN&quot; der vollqualifizierte Domänenname (FQDN, Fully Qualified Domain Name) des Pools oder die IP-Adresse des Servers ist. Beispiel: PSTNGateway:redmondpool.litwareinc.com. Dienstidentitäten können abgerufen werden, indem der Befehl &quot;Get-CsService | Select-Object Identity&quot; aufgerufen wird.</p>
<p>Wenn Sie eine VoIP-Route ändern und die Liste &quot;PstnGatewayList&quot; leer bleibt oder durch Ihre Änderung alle Elemente in der Liste entfernt werden, wird eine Warnmeldung angezeigt, dass Benutzer keine PSTN-Anrufe mehr tätigen können.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Eine Liste der PSTN-Verwendungen (z. B. &quot;Local&quot; oder &quot;Long Distance&quot;), die auf diese VoIP-Route angewendet werden können. Die PSTN-Verwendung muss vorhanden sein. (PSTN-Verwendungen können mit dem Cmdlet <strong>Get-CsPstnUsage</strong> abgerufen werden.)</p>
<p>Wenn Sie eine VoIP-Route ändern und die Liste &quot;PstnUsages&quot; leer bleibt oder durch Ihre Änderung alle PSTN-Verwendungen in der Liste entfernt werden, wird eine Warnmeldung angezeigt, dass Benutzer keine PSTN-Anrufe mehr tätigen können.</p></td>
</tr>
<tr class="odd">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Legt fest, ob bei ausgehenden Anrufen eine Anrufer-ID offengelegt wird. Ist dieser Parameter auf &quot;True&quot; festgelegt, wird die Anrufer-ID unterdrückt. Anstelle der tatsächlichen ID wird der Wert des Parameters &quot;AlternateCallerId&quot; angezeigt. Wenn &quot;SuppressCallerId&quot; auf &quot;True&quot; festgelegt ist, muss für &quot;AlternateCallerId&quot; ein Wert angegeben werden.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Objekt "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route". Das Cmdlet **Set-CsVoiceRoute** akzeptiert eine weitergeleitete Eingabe von VoIP-Routenobjekten.

## Rückgabetypen

Das Cmdlet **Set-CsVoiceRoute** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)

