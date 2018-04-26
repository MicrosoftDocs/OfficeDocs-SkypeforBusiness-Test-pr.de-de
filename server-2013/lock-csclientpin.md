---
title: Lock-CsClientPin
TOCTitle: Lock-CsClientPin
ms:assetid: 81a9895f-96e3-43c9-9dac-8129358e446a
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398650(v=OCS.15)
ms:contentKeyID: 49294580
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lock-CsClientPin

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ermöglicht es einem Administrator, einen Benutzer an der Verwendung der PIN-Authentifizierung zu hindern. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Lock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird das Cmdlet **Lock-CsClientPin** zum Sperren der PIN für den Benutzer "kenmyer@litwareinc.com" verwendet.

    Lock-CsClientPin -Identity "kenmyer@litwareinc.com"

## BEISPIEL 2

In Beispiel 2 wird das Cmdlet **Lock-CsClientPin** zum Sperren der PINs für alle Benutzer verwendet, denen zurzeit eine PIN zugewiesen ist. Hierzu wird mit dem Cmdlet **Get-CsUser** eine Auflistung aller Benutzer abgerufen, die für Lync Server aktiviert sind. Die Auflistung wird anschließend an das Cmdlet **Get-CsClientPinInfo** weitergeleitet. Dieses Cmdlet wird mit dem Cmdlet **Where-Object** eingesetzt, um eine Auflistung der Benutzer zurückzugeben, bei denen die Eigenschaft "IsPinSet" den Wert "True" aufweist. Die gefilterte Auflistung wird anschließend an das Cmdlet **Lock-CsClientPin** weitergeleitet, das die PIN für jeden Benutzer in der Auflistung sperrt.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $True} | Lock-CsClientPin

## BEISPIEL 3

In Beispiel 3 wird das Cmdlet **Lock-CsClientPin** zum Sperren der PINs für alle Benutzer verwendet, deren PINs abgelaufen sind. Hierzu wird zunächst das Cmdlet **Get-CsUser** aufgerufen, um eine Auflistung aller Benutzer zurückzugeben, die für Lync Server aktiviert sind. Anschließend wird die Auflistung an das Cmdlet **Get-CsClientPinInfo** weitergeleitet, das zusammen mit dem Cmdlet **Where-Object** die Auflistung auf Benutzer beschränkt, deren PINs abgelaufen sind. Um zu ermitteln, welche Benutzer-PINs abgelaufen sind, prüft das Cmdlet **Where-Object** auf Konten, bei denen die Eigenschaft "PinExpirationTime" (diese gibt das Datum des PIN-Ablaufs an) einen Wert aufweist, der vor dem aktuellen Datum liegt. (Das aktuelle Datum wird mit dem Cmdlet **Get-Date** abgerufen.) Wenn das Ablaufdatum (z. B. 1. September 2010) vor dem aktuellen Datum liegt (beispielsweise 2. September 2010), ist die PIN abgelaufen. Anschließend werden mit dem Cmdlet **Lock-CsClientPin** alle abgelaufenen PINs gesperrt.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.PinExpirationTime -lt (Get-Date)} | Lock-CsClientPin

## Detaillierte Beschreibung

Lync Server ermöglicht es den Benutzern, eine Verbindung mit dem System herzustellen oder per Telefon an Konferenzen über das Telefonfestnetz (Public Switched Telephone Network, PSTN) teilzunehmen. Üblicherweise ist für die Anmeldung beim System oder für den Beitritt zu einer Konferenz die Eingabe eines Benutzernamens oder Kennworts erforderlich. Die Eingabe eines Benutzernamens oder Kennworts kann jedoch zu einem Problem werden, wenn Sie ein Telefon verwenden, das keine alphanumerischen Tasten umfasst. Daher können Sie mit Lync Server den Benutzern ausschließlich aus Zahlen bestehende PINs zur Verfügung stellen. Benutzer können sich dann nach Aufforderung beim System anmelden oder einer Konferenz beitreten, indem sie anstelle eines Benutzernamens und Kennworts eine PIN eingeben.

Als Sicherheitsmaßnahme können Sie in Lync Server die PIN eines Benutzers sperren. Wenn eine PIN gesperrt ist, kann der Benutzer diese PIN nicht länger zur Verbindung mit dem System oder zur Teilnahme an einer Konferenz verwenden. (Dieser Benutzer kann jedoch weiterhin auf das System zugreifen und an Konferenzen teilnehmen, wenn eine Anwendung wie Lync 2013 verwendet und ein Benutzername sowie ein Kennwort angegeben wird.) Nachdem die PIN gesperrt wurde, ist eine Wiederherstellung der PIN (und der Zugriffsberechtigungen des Benutzers) nur möglich, indem ein Administrator die PIN entsperrt. Dies kann mit dem Cmdlet **Unlock-CsClientPin** durchgeführt werden.

Mit dem Cmdlet **Lock-CsClientPin** können Administratoren einen Benutzer temporär daran hindern, unter Verwendung der PIN-Authentifizierung auf das System zuzugreifen. PINs können auch durch das System gesperrt werden: Wenn ein Benutzer bei der Systemanmeldung wiederholt eine falsche PIN eingibt, wird die PIN automatisch gesperrt und kann nur durch einen Administrator wieder entsperrt werden.

Beachten Sie, dass die Firewallausnahmen für SQL Server Express standardmäßig nicht aktiviert sind, wenn Sie die Standard Edition von Lync Server installieren. Dies bedeutet, dass Sie das Cmdlet **Lock-CsClientPin** nicht über eine Remoteinstanz von Windows PowerShell ausführen können. Der Grund hierfür ist, dass der Befehl die Firewall nicht passieren kann und somit kein Zugriff auf die SQL Server Express-Datenbank möglich ist. (Sie können das Cmdlet jedoch weiterhin lokal auf dem Standard Edition-Server selbst ausführen.) Zur Remoteausführung des Cmdlets **Lock-CsClientPin** müssen Sie die Firewallausnahmen für SQL Server Express manuell aktivieren.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Lock-CsClientPin** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Lock-CsClientPin"}

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
<td><p>Identität des Benutzerkontos, dessen PIN gesperrt werden soll. Benutzeridentitäten können in den folgenden vier Formaten angegeben werden: als 1) SIP-Adresse des Benutzers, 2) UPN (Benutzerprinzipalname) des Benutzers, 3) Domänen- und Anmeldename des Benutzers (mit dem Format &quot;Domäne\Anmeldename&quot;, z. B. &quot;litwareinc\kenmyer&quot;) und 4) Active Directory-Anzeigename des Benutzers (z. B. &quot;Ken Myer&quot;). Sie können auch unter Verwendung des Active Directory-Distinguished Name (DN) des Benutzers auf Benutzeridentitäten verweisen.</p>
<p>Ferner können Sie das Sternchen (*) als Platzhalterzeichen verwenden, wenn Sie den Anzeigenamen als Benutzeridentität verwenden. Der Identitätswert &quot;* Smith&quot; gibt beispielsweise alle Benutzer zurück, deren Anzeigename auf den Zeichenfolgenwert &quot; Smith&quot; endet.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
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

Zeichenfolgenwert oder Microsoft.Rtc.Management.ADConnect.Schema.ADUser-Objekt. Das Cmdlet **Lock-CsClientPin** akzeptiert eine weitergeleitete Eingabe von Zeichenfolgenwerten, die den Identitätswert eines Benutzerkontos repräsentieren. Das Cmdlet akzeptiert auch eine weitergeleitete Eingabe von Benutzerobjekten.

## Rückgabetypen

Das Cmdlet **Lock-CsClientPin** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WriteableConfig.Voice.VoicePolicy" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

