---
title: Set-CsUnassignedNumber
TOCTitle: Set-CsUnassignedNumber
ms:assetid: e7f52423-58d1-410a-9071-731bde45d3d4
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399033(v=OCS.15)
ms:contentKeyID: 49295747
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUnassignedNumber

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert einen vorhandenen Bereich von nicht zugewiesenen Nummern sowie die Routingregeln, die auf diese Nummern angewendet werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird ein Bereich nicht zugewiesener Nummern mit dem Namen "UNSet1" geändert. Zuerst wird der Wert "UNSet1" an den Parameter "Identity" übergeben. Dabei handelt es sich um den Namen des Bereichs nicht zugewiesener Nummern, der geändert werden soll. Mit den Parametern "NumberRangeStart" (+14255551000) und "NumberRangeEnd" (+14255551900) wird dann der Bereich nicht zugewiesener Nummern geändert, auf den die festgelegte Ansage oder die automatische Telefonzentrale angewendet wird.

    Set-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## BEISPIEL 2

In diesem Beispiel wird die Ansage aller Einstellungen für den Bereich nicht zugewiesener Nummern geändert, bei denen der Name einer Ansage die Zeichenfolge "Welcome" enthält. Zunächst wird das Cmdlet **Get-CsUnassignedNumber** aufgerufen, um alle Einstellungen für nicht zugewiesene Nummern abzurufen. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Auflistung auf die Einstellungen beschränkt, bei denen die Eigenschaft "AnnouncementName" die Zeichenfolge "Welcome" enthält (der Vergleichsoperator "-match" steht für "matches"). Anschließend werden diese Einstellungen an das Cmdlet **Set-CsUnassignedNumber** weitergeleitet, wobei mit dem Parameter "AnnouncementService" die Anwendungsserver-ID des Ansagediensts (ApplicationServer:redmond.litwareinc.com) und mit dem Parameter "AnnouncementName" der Name der neuen Ansage (Help Desk Announcement) geändert wird. Beachten Sie, dass Sie nach wie vor neben dem Namen auch die Dienst-ID angeben müssen, auch wenn sich nur der Name ändert, die Dienst-ID aber gleich bleibt.

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Set-CsUnassignedNumber -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Help Desk Announcement"

## Detaillierte Beschreibung

Nicht zugewiesene Nummern sind Telefonnummern, die einer Organisation, aber keinen bestimmten Benutzern oder Telefonen zugewiesen sind. Lync Server kann so eingerichtet werden, dass Anrufe an bestimmte Ziele weitergeleitet werden, wenn eine nicht zugewiesene Nummer angerufen wird. Mit diesem Cmdlet werden die Einstellungen geändert, die dieses Routing definieren.

Um einige der Einstellungen für dieses Cmdlet zu ändern, müssen Sie entweder Ansagen für Ihr System definieren oder eine automatische Exchange UM-Telefonzentrale einrichten. Um zu ermitteln, ob Ansagen definiert wurden, rufen Sie das Cmdlet **Get-CsAnnouncement** auf. Verwenden Sie das Cmdlet **New-CsAnnouncement**, um eine neue Ansage zu erstellen. Zum Überprüfen der Einstellungen für eine automatische Exchange UM-Telefonzentrale verwenden Sie das Cmdlet **Get-CsExUmContact**.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsUnassignedNumber** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>String</p></td>
<td><p>Der Name der Ansage, die zur Verarbeitung von Anrufen bei Nummern in diesem Bereich verwendet wird.</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>String</p></td>
<td><p>Der vollqualifizierte Domänenname (Fully Qualified Domain Name, FQDN) oder die Dienst-ID des Ansageservers.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>String</p></td>
<td><p>Die Telefonnummer der automatischen Exchange UM-Telefonzentrale, an die Anrufe für Nummern in diesem Bereich weitergeleitet werden. Der Kontakt für die automatische Exchange UM-Telefonzentrale muss bereits eingerichtet sein, um diesem Parameter einen Wert zuweisen zu können.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
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
<td><p>Der eindeutige Name für den Bereich nicht zugewiesener Nummern, der geändert wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>DisplayAnnouncementVacantNumberRange</p></td>
<td><p>Ein Verweis auf ein Objekt, das Einstellungen für nicht zugewiesene Nummern enthält. Dieses Objekt muss ein Objekt vom Typ &quot;Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange&quot; sein und kann mit dem Cmdlet <strong>Get-CsUnassignedNumber</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die letzte Nummer im Bereich der nicht zugewiesenen Nummern. Der Wert muss größer oder gleich dem Wert von &quot;NumberRangeStart&quot; sein. Zur Festlegung eines Bereichs mit nur einer Nummer verwenden Sie für &quot;NumberRangeStart&quot; und &quot;NumberRangeEnd&quot; denselben Wert.</p>
<p>Der Wert muss mit dem regulären Ausdruck &quot;(tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?&quot; übereinstimmen. Dies bedeutet, dass die Nummer mit der Zeichenfolge &quot;tel:&quot; (wenn Sie diese Zeichenfolge nicht angeben, wird sie automatisch hinzugefügt) sowie einem Pluszeichen (+) und einer Zahl zwischen 1 und 9 beginnen kann. Die Telefonnummer kann bis zu 17 Zeichen umfassen, gefolgt von einer Durchwahl im Format &quot;;ext=&quot; plus der Durchwahlnummer.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die erste Nummer im Bereich der nicht zugewiesenen Nummern. Der Wert muss kleiner oder gleich dem Wert von &quot;NumberRangeEnd&quot; sein.</p>
<p>Der Wert muss mit dem regulären Ausdruck &quot;(tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?&quot; übereinstimmen. Dies bedeutet, dass die Nummer mit der Zeichenfolge &quot;tel:&quot; (wenn Sie diese Zeichenfolge nicht angeben, wird sie automatisch hinzugefügt) sowie einem Pluszeichen (+) und einer Zahl zwischen 1 und 9 beginnen kann. Die Telefonnummer kann bis zu 17 Zeichen umfassen, gefolgt von einer Durchwahl im Format &quot;;ext=&quot; plus der Durchwahlnummer.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Bereiche nicht zugewiesener Nummern können sich überschneiden. Wenn eine Nummer in mehr als einen Bereich fällt, wird der Bereich mit der höheren Priorität verwendet.</p></td>
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

Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange-Objekt. Akzeptiert eine weitergeleitete Eingabe von Objekten für nicht zugewiesene Nummern.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

