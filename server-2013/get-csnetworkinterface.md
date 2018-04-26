---
title: Get-CsNetworkInterface
TOCTitle: Get-CsNetworkInterface
ms:assetid: 06a5fedf-d87e-4469-9bd6-ad16c1f9a801
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398121(v=OCS.15)
ms:contentKeyID: 49293065
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterface

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Netzwerkschnittstellen zurück, die auf Computern mit Lync Server-Diensten oder -Serverrollen verwendet werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsNetworkInterface [-Identity <NetworkInterfaceIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterface [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ComputerFqdn <Fqdn>]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel werden Informationen zu allen in der Organisation konfigurierten Netzwerkschnittstellen zurückgegeben.

    Get-CsNetworkInterface

## BEISPIEL 2

Der Befehl in Beispiel 2 gibt Informationen zu einer einzelnen Netzwerkschnittstelle zurück: diese hat den Identitätswert "atl-cs-001.litwareinc.com.com/Primary/1"

    Get-CsNetworkInterface -Identity atl-cs-001.litwareinc.com/Primary/1

## BEISPIEL 3

In Beispiel 3 werden Informationen zu allen Netzwerkschnittstellen in der Domäne "litwareinc.com" zurückgegeben. Hierzu wird der Parameter "Filter" zusammen mit dem Filterwert "\*.litwareinc.com\*" verwendet. Dieser Filterwert beschränkt die zurückgegebenen Daten auf Schnittstellen, deren Identitätswert den Zeichenfolgenwert "litwareinc.com" enthält.

    Get-CsNetworkInterface -Filter "*.litwareinc.com*"

## BEISPIEL 4

In Beispiel 4 werden Informationen zu allen für die IP-Adresse 192.168.0.240 konfigurierten Netzwerkschnittstellen zurückgegeben. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsNetworkInterface** ohne Parameter auf. Damit wird eine Auflistung aller derzeit für die Verwendung in der Organisation konfigurierten Netzwerkschnittstellen zurückgegeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Schnittstellen herausfiltert, bei denen die Eigenschaft "IPAddress" den Wert 192.168.0.240 aufweist.

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -eq "192.168.0.240"}

## BEISPIEL 5

Der Befehl in Beispiel 5 ist eine Variante des Befehls aus Beispiel 4. In diesem Fall werden allerdings Informationen zu allen für das Subnetz "192.168.0.\*" konfigurierten Netzwerkschnittstellen zurückgegeben. Hierzu wird eine Auflistung aller Netzwerkschnittstellen abgerufen und diese Auflistung an das Cmdlet **Where-Object** weitergeleitet. Anschließend werden nur die Schnittstellen herausgefiltert, deren Eigenschaft "IPAddress" mit dem Zeichenfolgenwert 192.168.0. beginnt.

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -like "192.168.0.*"}

## BEISPIEL 6

Im sechsten Beispiel werden alle Netzwerkschnittstellen zurückgegeben, die für den externen Zugriff konfiguriert wurden. Dazu wird das Cmdlet **Get-CsNetworkInterface** zunächst ohne Parameter aufgerufen. Anschließend wird eine Auflistung mit allen derzeit verwendeten Netzwerkschnittstellen zurückgegeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Elemente auswählt, bei denen die Eigenschaft "Interface" den Wert "External" besitzt.

    Get-CsNetworkInterface | Where-Object {$_.Interface -eq "External"}

## Detaillierte Beschreibung

Damit Informationen von einem Computer an einen anderen übertragen werden können, benötigen die Computer Netzwerkschnittstellen, d. h. Verbindungen zwischen dem Computer und dem Netzwerk. Computer mit Lync Server-Diensten oder -Serverrollen müssen mindestens eine Netzwerkschnittstelle besitzen. Andernfalls können sie nicht mit anderen Computern kommunizieren. Diese Computer können allerdings auch über mehrere Netzwerkschnittstellen verfügen. Ein Edgeserver kann beispielsweise über eine Schnittstelle zum Herstellen einer Verbindung mit dem internen Netzwerk und über eine zweite Schnittstellen zum Herstellen einer Verbindung mit dem Internet verfügen. Das Cmdlet **Get-CsNetworkInterface** ermöglicht es Administratoren, Informationen zu den derzeit auf Computern mit Lync Server-Diensten oder -Serverrollen verwendeten Netzwerkschnittstellen zurückzugeben.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsNetworkInterface** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterface"}

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
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN des Computers, von dem Netzwerkschnittstelleninformationen zurückgegeben werden sollen. Verwenden Sie folgende Syntax, um Netzwerkschnittstelleninformationen ausschließlich für den Computer &quot;atl-cs-001.litwareinc.com&quot; zurückzugeben: -ComputerFqdn atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht die Verwendung von Platzhaltern beim Angeben der zurückzugebenden Netzwerkschnittstellen. Diese Syntax gibt beispielsweise Informationen zur Netzwerkschnittstelle &quot;Primary&quot; zurück, die auf allen Computern mit einem Lync Server-Dienst oder einer -Serverrolle verwendet wird. -Filter &quot;*/Primary/*&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.NetworkInterfaceIdentity</p></td>
<td><p>Eindeutige ID für die zurückzugebende Netzwerkschnittstelle. Eine Netzwerkschnittstellen-ID besteht aus drei Teilen:</p>
<p>Vollqualifizierter Domänenname (FQDN) des Computers (z. B. &quot;atl-cs-001.litwareinc.com&quot;).</p>
<p>Netzwerkschnittstellenbereich (&quot;Primary&quot;, &quot;Internal&quot;, &quot;External&quot;, &quot;PSTN&quot;). Der Bereich gibt an, für welche Art von Datenverkehr der Port verwendet wird.</p>
<p>Netzwerkschnittstellennummer für diesen spezifischen Bereich.</p>
<p>Beispiel: -Identity &quot;atl-cs-001.litwareinc.com/Primary/1&quot;.</p>
<p>Die Parameter &quot;Identity&quot;, &quot;ComputerFqdn&quot; und &quot;Filter&quot; müssen separat verwendet werden. Es ist beispielsweise nicht möglich, einen Befehl auszuführen, der sowohl &quot;ComputerFqdn&quot; als auch &quot;Identity&quot; verwendet. Darüber hinaus können Sie beim Angeben des Identitätswerts keine Platzhalterzeichen verwenden. Verwenden Sie hierzu den Parameter &quot;Filter&quot;.</p>
<p>Wenn weder &quot;Identity&quot;, &quot;ComputerFqdn&quot; noch &quot;Filter&quot; verwendet werden, gibt das Cmdlet <strong>Get-CsNetworkInterface</strong> Informationen zu allen Netzwerkschnittstellen zurück, die derzeit auf den Computern verwendet werden, auf denen ein Lync Server-Dienst oder eine -Serverrolle ausgeführt wird.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsNetworkInterface** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsNetworkInterface** wird eine Instanz des Objekts "Microsoft.Rtc.Management.Xds.DisplayNetworkInterface" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Get-CsComputer](get-cscomputer.md)

