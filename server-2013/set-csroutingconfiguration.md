---
title: Set-CsRoutingConfiguration
TOCTitle: Set-CsRoutingConfiguration
ms:assetid: ab69c6e8-262a-4ecb-b1af-513383c494fe
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412811(v=OCS.15)
ms:contentKeyID: 49295055
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRoutingConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine Liste von VoIP-Routen. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Zum Ändern einer VoIP-Route innerhalb einer Routingkonfiguration sind mehrere Schritte erforderlich. In diesem Beispiel wird zunächst das Routingkonfigurationsobjekt abgerufen, indem das Cmdlet **Get-CsRoutingConfiguration** aufgerufen wird. Anschließend wird das abgerufene Objekt (es wird nur ein Objekt zurückgegeben) der Variablen "$a" zugewiesen.

In Zeile 2 des vorliegenden Beispiels werden die Inhalte der Eigenschaft "Route" aus der Variablen "$a" abgerufen, bei der es sich um eine Auflistung von VoIP-Routenobjekten handelt. Anschließend wird die Auflistung an das Cmdlet **Where-Object** übergeben, und die Auflistung wird nach allen VoIP-Routenobjekten durchsucht, deren Name mit der Zeichenfolge "LocalRoute" übereinstimmt. Dieses Objekt wird der Variablen "$b" zugewiesen.

Als Nächstes wird das VoIP-Routenobjekt "LocalRoute" geändert, indem der Eigenschaft "SuppressCallerId" der Wert "$False" zugewiesen wird. Durch eine Aktualisierung des Objekts wird das Objekt in der Variablen "$a" aktualisiert. Das Objekt befindet sich jedoch weiterhin nur im Arbeitsspeicher. Im letzten Schritt müssen die vorgenommenen Änderungen gespeichert werden, indem "$a" an den Parameter "Instance" des Cmdlets **Set-CsRoutingConfiguration** übergeben wird.

Hierbei handelt es sich nicht um die empfohlene Vorgehensweise zum Ändern einer Routingkonfiguration. Ändern Sie zum Bearbeiten einer Routingkonfiguration die einzelnen VoIP-Routen über das Cmdlet **Set-CsVoiceRoute**, wie nachfolgend gezeigt:

Set-CsVoiceRoute -Identity LocalRoute -SuppressCallerId $False

Diese eine Zeile führt dieselbe Aufgabe aus wie Beispiel 1.

    $a = Get-CsRoutingConfiguration
    $b = $a.Route | Where-Object {$_.Name -match "LocalRoute"}
    $b.SuppressCallerId = $False
    Set-CsRoutingConfiguration -Instance $a

## Detaillierte Beschreibung

VoIP-Routen umfassen Anweisungen, anhand derer Lync Server ermittelt, wie Anrufe von Enterprise-VoIP-Benutzern bei Telefonnummern im Telefonfestnetz (Public Switched Telephone Network, PSTN) oder in einer Nebenstellenanlage (Private Branch Exchange, PBX) weitergeleitet werden sollen. Mit diesem Cmdlet können Sie die Einstellungen einer beliebigen Route ändern, die in einer Lync Server-Bereitstellung definiert ist.

Die Verwendung dieses Cmdlets wird nicht empfohlen. Ändern Sie zum Bearbeiten der Routingkonfigurationen die einzelnen VoIP-Routen über das Cmdlet **Set-CsVoiceRoute**.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsRoutingConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRoutingConfiguration"}

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
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Wird dieser Wert auf &quot;True&quot; festgelegt, erfolgt die Verwaltung des VoIP-Routings unter Berücksichtigung des jeweiligen Standorts der Gesprächspartner. Der Standardwert lautet &quot;False&quot;.</p></td>
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
<td><p>XdsIdentity</p></td>
<td><p>Der Gültigkeitsbereich der Routingkonfiguration. Dieser muss &quot;Global&quot; lauten.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Ein Routingkonfigurationsobjekt (Microsoft.Rtc.Management.WritablConfig.Policy.Voice.PstnRoutingSettings). Ein Objekt dieses Typs kann durch den Aufruf des Cmdlets <strong>Get-CsRoutingConfiguration</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>Route</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste aller VoIP-Routen (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route-Objekte), die für die Lync Server-Bereitstellung definiert sind.</p>
<p>Sie sollten einzelne VoIP-Routenobjekte über das Cmdlet <strong>Set-CsVoiceRoute</strong> ändern. Dies ist die empfohlene Methode zum Ändern von Routen in dieser Liste.</p></td>
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

Microsoft.Rtc.WritableConfig.Management.Policy.Voice.PSTNRoutingSettings-Objekt. Akzeptiert eine weitergeleitete Eingabe von Routingkonfigurationsobjekten.

## Rückgabetypen

Das Cmdlet **Set-CsRoutingConfiguration** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

