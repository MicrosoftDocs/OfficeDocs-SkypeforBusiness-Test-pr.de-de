---
title: Remove-CsPublicProvider
TOCTitle: Remove-CsPublicProvider
ms:assetid: b9eec2f4-cf36-41b7-8023-67790cc8d4cd
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412906(v=OCS.15)
ms:contentKeyID: 49295211
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPublicProvider

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt einen für die Verwendung in Ihrer Organisation konfigurierten öffentlichen Anbieter. Ein öffentlicher Anbieter ist eine Organisation, die Instant Messaging- , Anwesenheits- und ähnliche Dienste für die breite Öffentlichkeit bietet. Lync Server umfasst drei öffentliche Anbieter, die zwar bereits konfiguriert, aber noch nicht aktiviert sind: Yahoo\!, AIM (AOL) und Messenger (MSN). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird der öffentliche Anbieter mit dem Identitätswert "Messenger" gelöscht. Nach Abschluss dieses Befehls wird "Messenger" nicht mehr in der Liste der konfigurierten öffentlichen Anbieter angezeigt. Zu diesem Zeitpunkt kann ein neuer Partnerverbund mit Messenger nur hergestellt werden, wenn der Anbieter neu erstellt wird.

    Remove-CsPublicProvider -Identity "Messenger"

## BEISPIEL 2

In Beispiel 2 werden alle für die Verwendung in der Organisation konfigurierten öffentlichen Anbieter gelöscht. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller derzeit zur Verwendung konfigurierten öffentlichen Anbieter zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Remove-CsPublicProvider** weitergeleitet, das jeden Anbieter in der Auflistung löscht.

    Get-CsPublicProvider | Remove-CsPublicProvider

## BEISPIEL 3

In Beispiel 3 werden alle öffentlichen Anbieter, die derzeit deaktiviert sind, aus dem Satz konfigurierter öffentlicher Anbieter entfernt. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller derzeit für die Verwendung konfigurierten öffentlichen Anbieter zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Anbieter auswählt, bei denen die Eigenschaft "Enabled" den Wert "False" aufweist. Diese gefilterte Auflistung wird dann an das Cmdlet **Remove-CsPublicProvider** weitergeleitet, das alle Elemente in der Auflistung löscht.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsPublicProvider

## Detaillierte Beschreibung

Ein Partnerverbund ist eine Möglichkeit, mit der zwei Organisationen eine Vertrauensstellung einrichten können, die die Kommunikation zwischen den beiden Gruppen erleichtert. Wenn ein Partnerverbund eingerichtet wurde, können Benutzer in beiden Organisationen einander Chatnachrichten senden, Anwesenheitsbenachrichtigungen abonnieren und mithilfe von SIP-Anwendungen wie Lync 2013 miteinander kommunizieren. Lync Server bietet drei Arten des Partnerverbunds: 1) direkter Partnerverbund zwischen Ihrer und einer anderen Organisation, 2) Partnerverbund zwischen Ihrer Organisation und einem öffentlichen Anbieter und 3) Partnerverbund zwischen Ihrer Organisation und einem externen Hostinganbieter.

Ein öffentlicher Anbieter ist eine Organisation, die SIP-Kommunikationsdienste für die breite Öffentlichkeit bietet. Wenn Sie eine Partnerverbundbeziehung mit einem öffentlichen Anbieter einrichten, stellen Sie im Prinzip einen Partnerverbund mit allen Benutzern her, deren Konto von diesem Anbieter gehostet wird. Bei einem Partnerverbund mit Messenger können Benutzer Chatnachrichten und Anwesenheitsinformationen mit allen anderen Benutzern austauschen, die über ein Instant Messaging-Konto für Messenger verfügen.

Um mit einem öffentlichen Anbieter im Partnerverbund zu arbeiten, müssen Sie einen neuen öffentlichen Anbieter erstellen und aktivieren. (Darüber hinaus muss der öffentliche Anbieter eine Partnerverbundbeziehung mit Ihnen einrichten.) Wenn Sie sich zu einem späteren Zeitpunkt dazu entschließen, diese Beziehung zu beenden, können Sie den öffentlichen Anbieter mit dem Cmdlet **Remove-CsPublicProvider** löschen. Wenn Sie einen öffentlichen Anbieter löschen, wird der Anbieter von Ihrer Verbundpartnerliste gelöscht. Ab diesem Moment kann die Beziehung nur wieder hergestellt werden, indem der Anbieter neu erstellt wird. Wenn Sie eine Beziehung zeitweise aufheben möchten, verwenden Sie stattdessen das Cmdlet **Disable-CsPublicProvider**. Ein deaktivierter öffentlicher Anbieter wird nicht von der Liste der Verbundpartner gelöscht, sondern nur als deaktiviert markiert, und die Kommunikation zwischen Ihrer Organisation und diesem Anbieter wird ausgesetzt. Wenn Sie die Beziehung wiederherstellen möchten, können Sie den Anbieter mit dem Cmdlet **Enable-CsPublicProvider** wieder neu aktivieren.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Remove-CsPublicProvider** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPublicProvider"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Eindeutige ID für den zu entfernenden öffentlichen Anbieter. Als Identitätswert wird in der Regel der Name der Website verwendet, die die Dienste bereitstellt (z. B. Yahoo!, AOL, MSN).</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider-Objekt. Das Cmdlet **Remove-CsPublicProvider** akzeptiert weitergeleitete Instanzen des Objekts für öffentliche Anbieter.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider" gelöscht.

## Siehe auch

#### Weitere Ressourcen

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

