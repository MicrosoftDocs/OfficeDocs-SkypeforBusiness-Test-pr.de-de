---
title: Get-CsVoiceRoute
TOCTitle: Get-CsVoiceRoute
ms:assetid: 422abb2d-bff3-4b9a-b18c-d8202b01f69b
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425926(v=OCS.15)
ms:contentKeyID: 49293817
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoute

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den VoIP-Routen zurück, die zur Verwendung in einer Organisation konfiguriert sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Ruft die Eigenschaften für alle VoIP-Routen ab, die innerhalb der Organisation definiert sind.

    Get-CsVoiceRoute

## BEISPIEL 2

Ruft die Eigenschaften für die VoIP-Route "Route1" ab.

    Get-CsVoiceRoute -Identity Route1

## BEISPIEL 3

Mit diesem Befehl werden VoIP-Routeneinstellungen angezeigt, bei denen der Identitätswert die Zeichenfolge "test" (an beliebiger Stelle innerhalb des Werts) enthält. Um nur Identitätswerte zu ermitteln, bei denen die Zeichenfolge "test" am Ende des Werts steht, verwenden Sie den Wert "\*test". Wenn Sie nur Identitätswerte ermitteln möchten, bei denen die Zeichenfolge "test" am Anfang des Identitätswerts steht, geben Sie den Wert "test\*" an.

    Get-CsVoiceRoute -Filter *test*

## BEISPIEL 4

Mit diesem Befehl werden alle VoIP-Routen abgerufen, denen keine PSTN-Gateways zugewiesen wurden. Zunächst werden über das Cmdlet **Get-CsVoiceRoute** alle VoIP-Routen abgerufen. Diese VoIP-Routen werden dann an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** schränkt die Ergebnisse der Get-Operation ein. In diesem Fall werden alle VoIP-Routen durchlaufen (dies wird durch "$\_" angezeigt), und die Eigenschaft "Count" von "PstnGatewayList" wird überprüft. Wenn der Wert "Count" von PSTN-Gateways 0 lautet, ist die Liste leer, und es wurden keine Gateways für die Route definiert.

    Get-CsVoiceRoute | Where-Object {$_.PstnGatewayList.Count -eq 0}

## Detaillierte Beschreibung

Verwenden Sie dieses Cmdlet, um vorhandene VoIP-Routen abzurufen. VoIP-Routen umfassen Anweisungen, anhand derer Lync Server ermittelt, wie Anrufe von Enterprise-VoIP-Benutzern bei Telefonnummern im Telefonfestnetz (Public Switched Telephone Network, PSTN) oder in einer Nebenstellenanlage (Private Branch Exchange, PBX) weitergeleitet werden sollen.

Dieses Cmdlet kann zum Abrufen von VoIP-Routeninformationen verwendet werden. Dazu zählt beispielsweise, welchen PSTN-Gateways die Route (gegebenenfalls) zugeordnet ist, welche PSTN-Verwendungen der Route zugeordnet sind, das Muster (in Form eines regulären Ausdrucks) zur Angabe der Telefonnummern, für welche die Route gilt, sowie Anruferkennungseinstellungen. Die PSTN-Verwendung ordnet die VoIP-Route einer VoIP-Richtlinie zu.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsVoiceRoute** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoute"}

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
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Dieser Parameter filtert die Ergebnisse der Get-Operation basierend auf dem an diesen Parameter übergebenen Platzhalterwert.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Eine Zeichenfolge zur eindeutigen Kennzeichnung der VoIP-Route. Wenn kein Identitätswert angegeben wird, werden alle VoIP-Routen der Organisation zurückgegeben.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die VoIP-Route aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit diesem Cmdlet werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)

