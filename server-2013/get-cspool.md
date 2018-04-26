---
title: Get-CsPool
TOCTitle: Get-CsPool
ms:assetid: e0911c68-9a0a-461a-88d6-c610c6cd996c
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398992(v=OCS.15)
ms:contentKeyID: 49295664
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPool

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Pools zurück, die in Ihrer Bereitstellung von Lync Server verwendet werden. Bei einem Pool handelt es sich um eine Auflistung von Computern, die sich alle an demselben Standort befinden und auf denen dieselben Lync Server-Dienste ausgeführt werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Site <String>]

## Beispiele

## BEISPIEL 1

In Beispiel 1 werden alle Pools in Ihrer Bereitstellung von Lync Server zurückgegeben.

    Get-CsPool

## BEISPIEL 2

In Beispiel 2 werden ausführliche Informationen zu den Computern in den einzelnen Pools zurückgegeben. Hierzu wird das Cmdlet **Get-CsPool** aufgerufen. Die zurückgegebenen Daten werden dann an das Cmdlet **Select-Object** weitergeleitet. Der Parameter "ExpandProperty" wird verwendet, um den Wert der Eigenschaft "Computers" zu erweitern. Die Eigenschaft "Computers" ist ein Array von Objekten, die die einzelnen Computer im Pool darstellen. Wenn Sie die Eigenschaft "Computers" erweitern, erhalten Sie ausführliche Informationen zu den einzelnen Computern.

    Get-CsPool | Select-Object -ExpandProperty Computers

## BEISPIEL 3

In Beispiel 3 dient der Parameter "Identity" zum Einschränken der zurückgegebenen Daten auf den einen Pool mit dem Identitätswert "atl-cs-001.litwareinc.com".

    Get-CsPool -Identity atl-cs-001.litwareinc.com

## BEISPIEL 4

In Beispiel 4 werden alle Pools am Standort Redmond zurückgegeben. Dazu verwendet der Befehl den Parameter "Site". Der Parameterwert "Redmond" beschränkt die zurückgegebenen Daten auf Pools, bei denen die Eigenschaft "Site" den Wert "Redmond" aufweist.

    Get-CsPool -Site "Redmond"

## BEISPIEL 5

Der Befehl in Beispiel 5 gibt eine Auflistung aller Pools zurück, in denen keine Lync Server-Dienste installiert sind. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPool** ohne Parameter auf. Dadurch wird eine Auflistung aller derzeit in der Organisation verwendeten Pools zurückgegeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Pools herausfiltert, bei denen die Eigenschaft "Services.Count" den Wert 0 aufweist, d. h., es sind keine Lync Server-Dienste für diesen Pool konfiguriert.

    Get-CsPool | Where-Object {$_.Services.Count -eq 0}

## Detaillierte Beschreibung

In Lync Server besteht ein Pool aus einem oder mehreren Computer am gleichen Standort, auf denen dieselben Dienste ausgeführt werden. Wenn Sie beispielsweise einen Server am Standort "Redmond" haben, auf dem der Vermittlungsserver ausgeführt wird, hätten Sie einen Vermittlungsserver-Pool, der aus diesem einen Computer besteht. Wenn Sie zwei Computer am Standort "Redmond" haben, auf denen der Vermittlungsserver ausgeführt wird, hätten Sie einen Vermittlungsserver-Pool, der aus zwei Computern besteht. Die Anzahl der Pools in Ihrer Organisation hängt von der Anzahl Ihrer Server und den verschiedenen darauf ausgeführten Diensten ab.

Mit dem Cmdlet **Get-CsPool** können Informationen zu allen Pools in Ihrer Organisation abgerufen werden, einschließlich Informationen zu den Diensten, die in jedem dieser Pools ausgeführt werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsPool** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPool"}

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
<td><p>Ermöglicht es Ihnen, beim Angeben der Identität des/der zurückzugebenden Pools Platzhalter zu verwenden. Beispielsweise werden mit folgender Syntax alle Pools zurückgegeben, deren Identität mit dem Zeichenfolgenwert &quot;.fabrikam.com&quot; endet: -Filter &quot;*.fabrikam.com&quot;.</p>
<p>Beachten Sie, dass Sie die Parameter &quot;Identity&quot; und &quot;Filter&quot; nicht im gleichen Befehl verwenden können.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) des Pools, der zurückgegeben werden soll. Beispiel: -Identity atl-cs-001.litwareinc.com.</p>
<p>Wenn dieser Parameter nicht angegeben ist, werden alle Pools in Ihrer Organisation zurückgegeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>Site</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Gibt alle Pools am angegebenen Standort zurück. Der betreffende Standort sollte mit &quot;DisplayName&quot; des Standorts (z. B. &quot;Redmond&quot;) statt mit dem Standortidentitätswert (z. B. &quot;site:Redmond&quot;) referenziert werden. Beispiel: -Site &quot;Redmond&quot;. Durch Ausführen dieses Befehls können Sie die Anzeigenamen für Ihre Standorte abrufen:</p>
<p>Get-CsSite | Select-Object Identity, DisplayName</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsPool** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsPool** werden Instanzen des Objekts "Microsoft.Rtc.Management.Deploy.Internal.Cluster " zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Get-CsSite](get-cssite.md)  
[Get-CsTopology](get-cstopology.md)

