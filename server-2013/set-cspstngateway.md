---
title: Set-CsPstnGateway
TOCTitle: Set-CsPstnGateway
ms:assetid: 5d61e7e5-dacb-4dd3-bdd5-b757d98181d3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398408(v=OCS.15)
ms:contentKeyID: 49294139
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnGateway

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert die Eigenschaften eines PSTN-Gateways (Public Switched Telephone Network, öffentliches Telefonfestnetz). PSTN-Gateways unterstützen das Weiterleiten von Anrufen zwischen Geräten im externen Telefonfestnetz und Geräten in Ihrem internen Enterprise-VoIP-Netzwerk. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsPstnGateway [-Identity <XdsGlobalRelativeIdentity>] [-AlternateByPassId <String>] [-Confirm [<SwitchParameter>]] [-Default <$true | $false>] [-Force <SwitchParameter>] [-GatewaySipClientTcpPort <UInt16>] [-GatewaySipClientTlsPort <UInt16>] [-MediationServer <String>] [-RepresentativeMediaIP <String>] [-Routable <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 konfiguriert das Gateway "PstnGateway:192.168.0.240" als Standardgateway. Das heißt, dass "PstnGateway:192.168.0.240" zum Verarbeiten von Anrufen von Office Communications Server 2007 R2 verwendet werden kann.

    Set-CsPstnGateway -Identity "PstnGateway:192.168.0.240" -Default $True

## BEISPIEL 2

Im zweiten Beispiel werden alle PSTN-Gateways in der Organisation konfiguriert, um sicherzustellen, dass alle diese Gateways für das Ausgangsrouting verwendet werden können. Hierzu verwendet der Befehl zunächst das Cmdlet **Get-CsService** und den Parameter "PstnGateway", um eine Auflistung aller derzeit verwendeten PSTN-Gateways zurückzugeben. Diese Auflistung wird anschließend an das Cmdlet **ForEach-Object** weitergeleitet. Das Cmdlet **ForEach-Object** führt das Cmdlet **Set-CsPstnGateway** für jedes Gateway in der Auflistung aus und setzt die Eigenschaft "Routable" jeweils auf "True".

    Get-CsService -PstnGateway | ForEach-Object {Set-CsPstnGateway -Identity $_.Identity -Routable $True}

## Detaillierte Beschreibung

PSTN-Gateways ermöglichen Enterprise VoIP-Benutzern, Personen im Telefonfestnetz anzurufen und Anrufe von diesen zu empfangen. Diese Gateways fungieren als Brücke zwischen dem Vermittlungsserver und dem Telefonfestnetz.

PSTN-Gateways sind normalerweise erforderlich, wenn Sie eine TDM-Nebenstellenanlage (Time Division Multiplex Private Branch Exchange) verwenden. In diesem Fall müssen Sie in der Regel sowohl ein PSTN-Gateway als auch einen Vermittlungsserver einsetzen, um Enterprise-VoIP-Anrufe an das Telefonfestnetz weiterzuleiten. Wenn Sie im Gegensatz dazu eine IP-Nebenstellenanlage verwenden, können Sie eine direkte SIP-Verbindung zwischen der Nebenstellenanlage und dem Vermittlungsserver herstellen und auf ein PSTN-Gateway verzichten.

Nachdem PSTN-Gateways installiert und konfiguriert wurden, können sie mit dem Cmdlet **Set-CsPstnGateway** verwaltet werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsPstnGateway** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnGateway"}

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
<td><p><em>AlternateByPassId</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>GUID (Globally Unique Identifier), die die alternative ID für die Umgehung darstellt. Diese ID wird automatisch von Lync Server generiert und dient zum Vermeiden von HCR (Hairpin Call Routing). Je nach Konfiguration Ihres Systems kann HCR den Vermittlungsserver automatisch umgehen, ohne dass Sie einzelne Subnetze definieren und allen Standorten und Regionen zuordnen müssen.</p>
<p>Hierzu müssen Sie in der Regel die Umgehung global aktivieren, um Netzwerkkonfigurationsstandorte und -regionen zu verwenden, und anschließend die Umgehung in der Trunkkonfiguration für Ihr PSTN-Gateway aktivieren.</p>
<p>HCR liegt vor, wenn ein aus dem Telefonfestnetz eingehender Anruf über die Anrufweiterleitung oder über das gleichzeitige Klingeln an das Netzwerk zurückgeleitet wird.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Default</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; verarbeitet dieses Gateway Anrufe, die von Office Communications Server 2007 R2 gesendet werden. In der Auflistung von Gateways, die von einem einzelnen Vermittlungsserver verwaltet werden, kann es nur ein Standardgateway geben.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Bestätigungsaufforderungen oder Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Cmdlets auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>GatewaySipClientTcpPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Überwachter Port für die Kommunikation mit Vermittlungsservern über TCP (Transmission Control Protocol). Der Standardwert lautet 5066.</p></td>
</tr>
<tr class="even">
<td><p><em>GatewaySipClientTlsPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Überwachter Port für die Kommunikation mit Vermittlungsservern über das TLS-Protokoll (Transport Layer Security). Der Standardwert lautet 5067.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Dienstidentität des zu ändernden PSTN-Gateways. Beispiel: -Identity &quot;PstnGateway:192.168.0.240&quot;.</p>
<p>Beachten Sie, dass Sie das Präfix &quot;PstnGatewayServer:&quot; beim Angeben eines PSTN-Gateways auch auslassen können. Beispiel: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Dienstidentität des Vermittlungsservers, der dem PSTN-Gateway zugeordnet werden soll. Beispiel: -MediationServer &quot;MediationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>RepresentativeMediaIP</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>IP-Adresse des dem Gateway zugeordneten Medienprozessors, vorausgesetzt, der Prozessorstandort unterscheidet sich von der Signaladresse. Sowohl Medienumgehung als auch Anrufsteuerung basieren auf dem Standort des Gatewaymedienprozessors. Standardmäßig stimmt dieser mit der Signaladresse überein. Wenn sich die beiden Standorte unterscheiden (wenn der Medienprozessor sich beispielsweise an einem Remotestandort und der Signalpeer sich am zentralen Standort befindet), muss &quot;RepresentativeMediaIP&quot; mit der IP-Adresse des Medienprozessors konfiguriert werden.</p>
<p>Wenn Sie mehrere Medienprozessoren mit jeweils einer eigenen IP-Adresse an demselben Standort bereitgestellt haben, können Sie eine dieser IP-Adressen bei der Konfiguration der Eigenschaft &quot;RepresentativeMediaIP&quot; verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>Routable</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; kann das Gateway beim Ausgangsrouting verwendet werden.</p></td>
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

Keine. Das Cmdlet **Get-CsPstnGateway** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Set-CsPstnGateway** werden keine Objekte oder Werte zurückgegeben. Stattdessen ändert das Cmdlet vorhandene Instanzen des Objekts "Microsoft.Rtc.Management.Xds.DisplayPstnGateway".

## Siehe auch

#### Weitere Ressourcen

[Get-CsService](get-csservice.md)

