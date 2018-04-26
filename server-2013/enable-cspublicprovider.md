---
title: Enable-CsPublicProvider
TOCTitle: Enable-CsPublicProvider
ms:assetid: 98370dfd-9a53-41a8-a1f3-bb7a516c3c5e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398780(v=OCS.15)
ms:contentKeyID: 49294838
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsPublicProvider

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Aktiviert einen für die Verwendung in Ihrer Organisation konfigurierten öffentlichen Anbieter. Ein öffentlicher Anbieter ist eine Organisation, die Chat-, Anwesenheits- und ähnliche Dienste für die breite Öffentlichkeit bietet. Lync Server umfasst drei öffentliche Anbieter, die zwar bereits konfiguriert, aber noch nicht aktiviert sind: Yahoo\!, AIM (AOL) und Messenger (MSN). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Enable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 aktiviert den öffentlichen Anbieter mit dem Identitätswert "Messenger". Dieser Befehl gibt einen Fehler zurück, wenn Messenger (MSN) bereits aktiviert ist.

    Enable-CsPublicProvider -Identity "Messenger"

## BEISPIEL 2

In Beispiel 2 werden alle öffentlichen Anbieter aktiviert, die derzeit deaktiviert sind. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller öffentlichen Anbieter zurückzugeben, die für die Verwendung in der Organisation konfiguriert sind. Diese Auflistung wird an das Cmdlet **Where-Object** weitergeleitet, das die Anbieter herausfiltert, deren Eigenschaft "Enabled" den Wert "False" aufweist. Die gefilterte Auflistung wird dann an das Cmdlet **Enable-CsPublicProvider** weitergeleitet, das jeden Anbieter in der Auflistung aktiviert.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsPublicProvider

## BEISPIEL 3

In Beispiel 3 werden alle noch nicht aktivierten öffentlichen Anbieter aktiviert, vorausgesetzt, dass deren Überprüfungsstufe auf "AlwaysVerifiable" festgelegt ist. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller öffentlichen Anbieter zurückzugeben, die aktuell in der Organisation verwendet werden. Diese Auflistung wird an das Cmdlet **Where-Object** weitergeleitet, das nur die Anbieter herausfiltert, die die folgenden zwei Kriterien erfüllen: 1) die Eigenschaft "VerificationLevel" lautet "AlwaysVerifiable" und 2) die Eigenschaft "Enabled" lautet "False". (Der Operator "and" weist das Cmdlet **Where-Object** an, dass ein Objekt alle angegebenen Kriterien erfüllen muss, um ausgewählt zu werden.) Die gefilterte Auflistung wird dann an das Cmdlet **Enable-CsPublicProvider** weitergeleitet, das jeden Anbieter in der Auflistung aktiviert.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysVerifiable" -and $_.Enabled -eq $False} | Enable-CsPublicProvider

## Detaillierte Beschreibung

Ein Partnerverbund ist eine Möglichkeit, mit der zwei Organisationen eine Vertrauensstellung einrichten können, die die Kommunikation zwischen den beiden Gruppen erleichtert. Wenn ein Partnerverbund eingerichtet wurde, können Benutzer in beiden Organisationen einander Chatnachrichten senden, Anwesenheitsbenachrichtigungen abonnieren und mithilfe von SIP-Anwendungen wie Lync 2013 miteinander kommunizieren. Lync Server bietet drei Arten des Partnerverbunds: 1) direkter Partnerverbund zwischen Ihrer und einer anderen Organisation, 2) Partnerverbund zwischen Ihrer Organisation und einem öffentlichen Anbieter und 3) Partnerverbund zwischen Ihrer Organisation und einem externen Hostinganbieter.

Ein öffentlicher Anbieter ist eine Organisation, die SIP-Kommunikationsdienste für die breite Öffentlichkeit bereitstellt. Wenn Sie eine Partnerverbundbeziehung mit einem öffentlichen Anbieter einrichten, stellen Sie im Prinzip einen Partnerverbund mit allen Benutzern her, deren Konto von diesem Anbieter gehostet wird. Bei einem Partnerverbund mit Messenger (MSN) können Benutzer Chatnachrichten und Anwesenheitsinformationen mit allen anderen Benutzern austauschen, die über ein Chatkonto für MSN Messenger verfügen.

Um mit einem öffentlichen Anbieter im Partnerverbund zu arbeiten, müssen Sie einen neuen öffentlichen Anbieter erstellen und aktivieren. (Darüber hinaus muss der öffentliche Anbieter eine Partnerverbundbeziehung mit Ihnen einrichten.) Öffentliche Anbieter können bei ihrer Erstellung oder zu einem späteren Zeitpunkt mit dem Cmdlet **Enable-CsPublicProvider** aktiviert werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Enable-CsPublicProvider** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsPublicProvider"}

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
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
<td><p>Eindeutige ID für den zu aktivierenden öffentlichen Anbieter. Als Identitätswert wird in der Regel der Name der Website verwendet, die die Dienste bereitstellt (z. B. Yahoo!, AOL, MSN usw.).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>DisplayPublicProvider-Objekt</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider-Objekt. Das Cmdlet **Enable-CsPublicProvider** akzeptiert weitergeleitete Instanzen des Objekts für öffentliche Anbieter.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider" aktiviert.

## Siehe auch

#### Weitere Ressourcen

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

