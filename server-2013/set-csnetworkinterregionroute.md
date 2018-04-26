---
title: Set-CsNetworkInterRegionRoute
TOCTitle: Set-CsNetworkInterRegionRoute
ms:assetid: 5d9da3c0-56fc-401d-baf3-ed6c0f50f53d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398410(v=OCS.15)
ms:contentKeyID: 49294140
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterRegionRoute

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine vorhandene Route, die Netzwerkregionen mit einer Anrufsteuerungskonfiguration verbindet. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterRegionRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-NetworkRegionLinkIDs <String>] [-NetworkRegionLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Dieses Beispiel ändert die Route "NA\_APAC\_Route", indem die Regionenverbindungen geändert werden, die entlang der Route durchquert werden. Für den Parameter "NetworkRegionLinkIDs" wird der Wert "NA\_SA,SA\_APAC" verwendet, der alle vorhandenen Verbindungen durch die beiden in dieser Zeichenfolge angegebenen Verbindungen ersetzt.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## BEISPIEL 2

Wie in Beispiel 1 werden in Beispiel 2 die Verbindungen innerhalb der Route "NA\_APAC\_Route" geändert. Doch anstatt mithilfe des Parameters "NetworkRegionLinkIDs" alle Verbindungen für diese Route zu ersetzen, wird hier der Parameter "NetworkRegionLinks" verwendet, um eine Verbindung der Liste der Verbindungen hinzuzufügen, die bereits für diese Route vorhanden sind. In diesem Fall wird die Verbindung "SA\_EMEA" der Route hinzugefügt. Die Syntax "@{add=\<Verbindung\>}" fügt der Liste der Verbindungen ein Element hinzu. Sie können auch die Syntax "@{replace=\<Verbindung\>}" verwenden, um alle vorhandenen Verbindungen mit denen durch "\<Verbindung\>" angegebenen Verbindungen zu ersetzen (was dem Verhalten von "NetworkRegionLinkIDs" im Wesentlichen entspricht). Über die Syntax "@{remove=\<Verbindung\>}" können Sie eine Verbindung aus der Liste entfernen.

    Set-CsNetworkInterRegionRoute -Identity NA_APAC_Route -NetworkRegionLinks @{add="SA_EMEA"}

## BEISPIEL 3

Im dritten Beispiel wird die Route "NA\_Route5" geändert. Dieses Beispiel ändert eine der Regionen, aus denen sich diese Route zusammensetzt. Der Parameter "NetworkRegionID2" dient zum Angeben der neuen Region. Anschließend wird der Parameter "NetworkRegionLinkIDs" verwendet, um eine neue Liste mit Links zum Verbinden der Regionen dieser Route zu erstellen.

    Set-CsNetworkInterRegionRoute -Identity NA_Route5 -NetworkRegionID2 SouthAmerica -NetworkRegionLinkIDs "NA_SA,SA_APAC"

## Detaillierte Beschreibung

Jede Region in einer Anrufsteuerungskonfiguration muss auf jede andere Region zugreifen können. Während die Regionenverbindungen Bandbreiteneinschränkungen für Verbindungen zwischen Regionen festlegen und auch die physischen Verbindungen darstellen, bestimmt eine Route, welchen Pfad die Verbindung von einer Region zur anderen nimmt. Dieses Cmdlet ändert diese Routenzuordnung.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsNetworkInterRegionRoute** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterRegionRoute"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Die eindeutige ID der Netzwerkregionsroute, die geändert werden soll. Netzwerkregionsrouten werden ausschließlich auf globaler Ebene erstellt, sodass mit dieser ID kein Gültigkeitsbereich festgelegt werden muss. Stattdessen ist eine Zeichenfolge enthalten, die den eindeutigen Namen zur Identifizierung dieser Route darstellt.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>InterNetworkRegionRouteType</p></td>
<td><p>Ein Objektverweis auf eine vorhandene Regionenroute. Dieses Objekt muss vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType&quot; sein, das durch Aufrufen von <strong>Get-CsNetworkInterRegionRoute</strong> abgerufen werden kann.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Identitätswert (NetworkRegionID) einer der beiden Regionen, die durch diese Route verbunden werden. Der an diesen Parameter übergebene Wert muss eine andere Region als der Wert des Parameters &quot;NetworkRegionID2&quot; angeben. (Dies soll verhindern, dass eine Region zu sich selbst geroutet wird.) Darüber hinaus muss die Kombination von &quot;NetworkRegionID1&quot; und &quot;NetworkRegionID2&quot; eindeutig sein (es darf beispielsweise nicht zwei Routen geben, die &quot;NorthAmerica&quot; und &quot;EMEA&quot; verbinden).</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Der Identitätswert (NetworkRegionID) einer der beiden Regionen, die durch diese Route verbunden werden. Der an diesen Parameter übergebene Wert muss eine andere Region als der Wert des Parameters &quot;NetworkRegionID1&quot; angeben. (Dies soll verhindern, dass eine Region zu sich selbst geroutet wird.) Darüber hinaus muss die Kombination von &quot;NetworkRegionID1&quot; und &quot;NetworkRegionID2&quot; eindeutig sein (es darf beispielsweise nicht zwei Routen geben, die &quot;NorthAmerica&quot; und &quot;EMEA&quot; verbinden).</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionLinkIDs</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Ermöglicht das Angeben aller Verbindungen für diese Route als Zeichenfolge mit durch Komma getrennten Werten. Die Werte sind die Identitätswerte (NetworkRegionLinkIDs) der Regionenverbindungen. Wenn Sie sowohl für &quot;NetworkRegionLinkIDs&quot; als auch für &quot;NetworkRegionLinks&quot; Werte eingeben, wird &quot;NetworkRegionLinkIDs&quot; ignoriert. Alle mithilfe dieses Parameters geänderten Verbindungen ersetzen alle in der Route vorhandenen Verbindungen.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Ein Listenobjekt mit den Identitätswerten (NetworkRegionLinkIDs) der Regionenverbindungen, die für diese Route gelten. Für dieses Cmdlet unterscheidet sich dieser Parameter von &quot;NetworkRegionLinkIDs&quot; dahingehend, dass Sie nicht nur die für diese Route vorhandenen Verbindungen ersetzen, sondern auch einzelne Verbindungen hinzufügen oder entfernen können.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType-Objekt. Akzeptiert eine weitergeleitete Eingabe von regionenübergreifenden Netzwerkroutenobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Es ändert ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType".

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

