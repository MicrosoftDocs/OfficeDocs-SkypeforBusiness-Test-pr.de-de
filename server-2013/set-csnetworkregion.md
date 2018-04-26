---
title: Set-CsNetworkRegion
TOCTitle: Set-CsNetworkRegion
ms:assetid: ffa1774b-ac60-4392-ad55-07bb887bf945
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg413089(v=OCS.15)
ms:contentKeyID: 49296026
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegion

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine bestehende Netzwerkregion. Netzwerkregionen repräsentieren Netzwerkhubs oder Backbones in einem Unternehmensnetzwerk. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-CentralSite <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die Netzwerkregion "NorthAmerica" geändert. Der Parameter "Description" erhält den Wert "North American Region". Wenn für die Region "NorthAmerica" ein Wert für "Description" vorhanden ist, überschreibt dieser Befehl ihn mit diesem Wert. Wenn kein Wert für "Description" festgelegt wurde, wird mit diesem Befehl ein Wert festgelegt.

    Set-CsNetworkRegion -Identity NorthAmerica -Description "North American Region"

## BEISPIEL 2

In diesem Beispiel wird die Netzwerkregion "EMEA" geändert und dieser eine neue alternative Pfadeinstellung für Video zugewiesen. Hierzu wird das Cmdlet **Set-CsNetworkRegion** aufgerufen und "EMEA" als Identitätswert übergeben. Anschließend wird der Parameter "VideoAlternatePath" angegeben und der Wert "$False" übergeben. Die Einstellung "False" für "VideoAlternatePath" gibt an, dass der Videoanruf bei unzureichender Bandbreite nicht an einen alternativen Pfad weitergeleitet, sondern stattdessen einfach nicht getätigt wird.

    Set-CsNetworkRegion -Identity EMEA -VideoAlternatePath $False

## BEISPIEL 3

In Beispiel 3 wird der Netzwerkregion "Asia" der gleiche Satz an alternativen Pfadeinstellungen wie der Region "NorthAmerica" zugewiesen. Die erste Zeile in diesem Beispiel ruft eine Instanz der Netzwerkregion "NorthAmerica" ab und weißt sie der Variablen "$a" zu. Die zweite Zeile ruft zunächst den Inhalt der Eigenschaft "BWAlternatePaths" und die (in der Variablen "$a" gespeicherten) Region "NorthAmerica" ab: "$a.BWAlternatePaths". Hierbei handelt es sich um eine Auflistung aller alternativer Pfadeinstellungen in der Region "NorthAmerica".

Als Nächstes wird diese Einstellungsauflistung an die foreach-Funktion weitergeleitet. "Foreach" durchläuft die Auflistung Element für Element und führt dabei die Aktionen in den folgenden geschweiften Klammern aus. In diesem Fall wird das Cmdlet **Set-CsNetworkRegion** mit der Identität "Asia" aufgerufen, um die Eigenschaften der Region "Asia" festzulegen. Der nächste Parameter ist "BWAlternatePaths". Sie übergeben den Wert "@{add=$\_}" an diesen Parameter. Die Variable "$\_" repräsentiert das aktuelle Element in der Auflistung, in diesem Fall den aktuellen alternativen Pfad. Der Teil "@{add=}" des Werts fügt dieses Element der Auflistung von "BWAlternatePaths" für die Region "Asia" hinzu.

    $a = Get-CsNetworkRegion -Identity NorthAmerica
    $a.BWAlternatePaths | foreach {Set-CsNetworkRegion -Identity Asia -BWAlternatePaths @{add=$_}}

## Detaillierte Beschreibung

Eine Netzwerkregion verbindet verschiedene Teile eines Netzwerks, das sich über verschiedene geografische Bereiche erstreckt. Jede Netzwerkregion muss einem zentraler Standort zugeordnet sein. Der zentrale Standort ist der Datencenterstandort, an dem der Bandbreitenrichtliniendienst für die Anrufsteuerung ausgeführt wird. Mit diesem Cmdlet können Sie eine vorhandene Netzwerkregion ändern – einschließlich der Einstellungen, die festlegen, ob für Audio- und Videoverbindungen alternative Pfade zulässig sind, und die die Standorte innerhalb der Region mit einer Konfiguration zur Medienumgehung in Bezug setzen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsNetworkRegion** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegion\\b"}

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
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Dieser Parameter bestimmt, ob Audioanrufe über einen alternativen Pfad weitergeleitet werden, wenn der primäre Pfad keine angemessene Bandbreite bietet.</p>
<p>Dieser Parameter füllt die Eigenschaft &quot;BWAlternatePaths&quot; auf. Der für diesen Parameter bereitgestellte Wert wird in der Eigenschaft &quot;AlternatePath&quot; für das alternative Pfadelement gespeichert, wobei &quot;BWPolicyModality&quot; den Wert &quot;Audio&quot; aufweist.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWAlternatePaths&quot; angeben.</p>
<p>Falls Ihre Anrufe auch Internetanrufe umfassen, muss der Wert unabhängig von den Bandbreiteneinstellungen &quot;True&quot; sein.</p></td>
</tr>
<tr class="even">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste von Objekten mit Informationen darüber, ob alternative Verbindungspfade zulässig sind, wenn eine Medienanforderung nicht entlang des bevorzugten Pfads abgeschlossen werden kann (z. B. wenn die Grenzwerte für diesen Pfad überschritten wurde). Alternative Pfadobjekte müssen vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType&quot; sein. Sie können Objekte diesen Typs durch Aufrufen des Cmdlets <strong>New-CsNetworkBWAlternatePath</strong> erstellen.</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Eine GUID (Globally Unique Identifier). Mit dieser GUID können Sie Netzwerkregionen Medienumgehungseinstellungen in einer Netzwerkkonfiguration für Anrufsteuerung oder 9-1-1 (erweitert) (E9-1-1) zuordnen. (Verwenden Sie diesen Wert für &quot;BypassID&quot; beim Aufruf des Cmdlets <strong>New-CsNetworkMediaBypassConfiguration</strong>.)</p>
<p>Dieser Parameter kann (durch Aufrufen des Cmdlets <strong>New-CsNetworkRegion</strong>) automatisch beim Erstellen der Region generiert werden. Von einer Änderung dieses Werts wird abgeraten. Wenn Sie dennoch einen Wert angeben, muss dieser die Form einer GUID aufweisen (z. B. &quot;3b24a047-dce6-48b2-9f20-9fbff17ed62a&quot;). Daraufhin wird eine Meldung eingeblendet, in der Sie bestätigen müssen, dass Sie diesen Wert manuell festlegen möchten.</p></td>
</tr>
<tr class="even">
<td><p><em>CentralSite</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Gibt den zentraler Standort an, an dem der Bandbreitenrichtliniendienst ausgeführt wird. Dieser Dienst muss aktiviert sein, damit Sie die Anrufsteuerung verwenden können. Dieser Dienst wird auf dem Front-End-Server oder dem Standard Edition-Server ausgeführt.</p></td>
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
<td><p>String</p></td>
<td><p>Eine Zeichenfolge, die die Region beschreibt. Mit diesem Parameter können Sie eine aussagekräftigere Erläuterung des Zwecks dieser Region bereitstellen als nur mit dem Identitätswert.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Eine eindeutige ID für die Netzwerkregion, die geändert werden soll. Der Identitätswert liegt als Zeichenfolge vor, die diese Region eindeutig identifiziert.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>PSObject</p></td>
<td><p>Ein Verweis auf das Netzwerkregionsobjekt. Dieses Objekt muss vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType&quot; sein und kann durch Aufrufen des Cmdlets <strong>Get-CsNetworkRegion</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Dieser Parameter bestimmt, ob Videoanrufe über einen alternativen Pfad weitergeleitet werden, wenn der primäre Pfad keine angemessene Bandbreite bietet.</p>
<p>Dieser Parameter füllt die Eigenschaft &quot;BWAlternatePaths&quot; auf. Der für diesen Parameter bereitgestellte Wert wird in der Eigenschaft &quot;AlternatePath&quot; für das alternative Pfadelement gespeichert, wobei &quot;BWPolicyModality&quot; den Wert &quot;Video&quot; aufweist.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWAlternatePaths&quot; angeben.</p>
<p>Falls Ihre Anrufe auch Internetanrufe umfassen, muss der Wert unabhängig von den Bandbreiteneinstellungen &quot;True&quot; sein.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Netzwerkregionsobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

