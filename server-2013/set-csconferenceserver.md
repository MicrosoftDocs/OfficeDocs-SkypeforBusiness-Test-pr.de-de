---
title: Set-CsConferenceServer
TOCTitle: Set-CsConferenceServer
ms:assetid: 90f9f1f1-0029-4f97-a8f4-719523cfad56
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398738(v=OCS.15)
ms:contentKeyID: 49294749
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceServer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert die Eigenschaften eines A/V-Konferenzservers (auch einfach Konferenzserver genannt). Der Konferenzserver stellt Audio- und Videofunktionen (A/V) für Ihre Konferenzen bereit. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsConferenceServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AppSharingSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-AudioVideoSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomPort <UInt16>] [-EdgeServer <String>] [-Force <SwitchParameter>] [-ImSipPort <UInt16>] [-MeetingPsomPort <UInt16>] [-PhoneSipPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Mit dem in Beispiel 1 gezeigten Befehl wird der Instant Messaging-SIP-Port für den Konferenzserver "ConferencingServer:atl-cs-001.litwareinc.com" geändert. In diesem Beispiel wird der Port in 5075 geändert.

    Set-CsConferenceServer -Identity "ConferencingServer:atl-cs-001.litwareinc.com" -ImSipPort 5075

## BEISPIEL 2

Beispiel 2 ist eine Variante des in Beispiel 1 gezeigten Befehls. In diesem Fall wird jedoch der Instant Messaging-SIP-Port für alle Konferenzserver in der Organisation geändert. Hierbei verwendet der Befehl zunächst das Cmdlet **Get-CsService** und den Parameter "ConferencingServer", um eine Auflistung aller derzeit verwendeten Konferenzserver zurückzugeben. Diese Auflistung wird anschließend an das Cmdlet **ForEach-Object** weitergeleitet, welches das Cmdlet **Set-CsConferenceServer** für jeden Server in der Auflistung ausführt, um die Eigenschaft "ImSipPort" auf 5075 festzulegen.

    Get-CsService -ConferencingServer | ForEach-Object {Set-CsConferenceServer -Identity $_.Identity -ImSipPort 5075}

## Detaillierte Beschreibung

Konferenzserver (auch bekannt als A/V-Konferenzserver) werden verwendet, um Audio- und Videofunktionen für Konferenzen bereitzustellen. Mit dem Cmdlet **Set-CsConferenceServer** können Sie die Eigenschaften dieser Server ändern; insbesondere können Sie festlegen, welche Ports z. B. für Audiodatenverkehr, Videodatenverkehr und die Anwendungsfreigabe verwendet werden. Außerdem können Sie das Cmdlet **Set-CsConferenceServer** für die Zuordnung eines bestimmten Servers zum Edgeserver oder zum Archivierungsserver verwenden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsConferenceServer** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Die Gesamtanzahl von Ports, die für die Anwendungsfreigabe zugewiesen sind. Die Ports, die tatsächlich geöffnet werden sollen, beginnen mit dem unter &quot;AppSharingPortStart&quot; festgelegten Wert. Von diesem Wert ausgehend wird die unter &quot;AppSharingPortCount&quot; festgelegte Anzahl von Ports geöffnet. Wenn für &quot;AppSharingPortStart&quot; z. B. der Wert 60000 und für &quot;AppSharingPortCount&quot; der Wert 100 festgelegt ist, werden die Ports 60000 bis 60099 für die Anwendungsfreigabe verwendet.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Der erste Port im für die Anwendungsfreigabe zugewiesenen Medienportbereich. Beispiel: –AppSharingPortStart 60000.</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingSipPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>SIP-Port für die Überwachung von Anforderungen zur Anwendungsfreigabe. Die für die Anwendungsfreigabe tatsächlich verwendeten Ports werden über &quot;AppSharingPortStart&quot; und &quot;AppSharingPortCount&quot; konfiguriert.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Gesamtanzahl von Ports, die für das Senden und Empfangen von Audiodaten genutzt werden. Die Ports, die tatsächlich geöffnet werden sollen, beginnen mit dem unter &quot;AudioPortStart&quot; festgelegten Wert. Von diesem Wert ausgehend wird die unter &quot;AudioPortCount&quot; festgelegte Anzahl von Ports geöffnet. Wenn &quot;AudioPortStart&quot; beispielsweise auf 60000 und &quot;AudioPortCount&quot; auf 100 festgelegt wurde, werden die Ports 60000 bis 60099 für den Audiodatenverkehr genutzt.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Der erste Port in dem für das Senden und Empfangen von Audiodaten zugewiesenen Medienportbereich. Beispiel: –AudioPortStart 60000.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioVideoSipPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>SIP-Port für die Überwachung auf eingehende Anforderungen für den Audio- und Videodienst. Die tatsächlich für den Audio- und Videodatenverkehr eingesetzten Ports werden über &quot;AudioPortCount&quot;, &quot;AudioPortStart&quot;, &quot;VideoPortCount&quot; und &quot;VideoPortStart&quot; konfiguriert.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Der vom PSOM-Protokoll (Persistent Shared Object Model) verwendete Datenport.</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Dienstidentifizierung des Edgeservers, der dem Konferenzserver zugeordnet werden soll. Beispiel: -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Dienstidentifizierung des zu ändernden Konferenzservers. Beispiel: -Identity &quot;ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Beachten Sie, dass Sie das Präfix &quot;ConferencingServer:&quot; auslassen können, wenn Sie einen Konferenzserver angeben. Beispiel: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ImSipPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port für den Instant Messaging-Datenverkehr.</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingPsomPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port für das PSOM-Protokoll (Persistent Shared Object Model), ein Microsoft-Protokoll für Konferenzen.</p></td>
</tr>
<tr class="even">
<td><p><em>PhoneSipPort</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port für Telefoniedatenverkehr.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Gesamtanzahl von Ports, die für das Senden und Empfangen von Videodaten genutzt werden. Die Ports, die tatsächlich geöffnet werden sollen, beginnen mit dem unter &quot;VideoPortStart&quot; festgelegten Wert. Von diesem Wert ausgehend wird die unter &quot;VideoPortCount&quot; festgelegte Anzahl von Ports geöffnet. Wenn &quot;VideoPortStart&quot; beispielsweise auf 60000 und &quot;VideoPortCount&quot; auf 100 festgelegt wird, werden die Ports 60000 bis 60099 für den Videodatenverkehr genutzt.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt16</p></td>
<td><p>Der erste Port in dem für das Senden und Empfangen von Videodaten zugewiesenen Portbereich. Beispiel: –VideoPortStart 60000.</p></td>
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

Keine. Das Cmdlet **Set-CsConferenceServer** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Set-CsConferenceServer** gibt keine Objekte oder Werte zurück. Stattdessen ändert das Cmdlet vorhandene Instanzen des Objekts "Microsoft.Rtc.Management.Xds.DisplayConferenceServer".

## Siehe auch

#### Weitere Ressourcen

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[Get-CsService](get-csservice.md)

