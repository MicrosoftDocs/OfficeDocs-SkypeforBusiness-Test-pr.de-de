---
title: Disable-CsPublicProvider
TOCTitle: Disable-CsPublicProvider
ms:assetid: df1338ea-fe6d-45da-a39c-86108bb54ef5
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398984(v=OCS.15)
ms:contentKeyID: 49295641
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsPublicProvider

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Deaktiviert einen für die Verwendung in Ihrer Organisation konfigurierten öffentlichen Anbieter. Ein öffentlicher Anbieter ist eine Organisation, die Instant Messaging-, Anwesenheits- und ähnliche Dienste für die breite Öffentlichkeit bietet. Lync Server umfasst drei öffentliche Anbieter, die zwar bereits konfiguriert, aber noch nicht aktiviert sind: Yahoo; AIM (AOL) und Messenger (MSN). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Disable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Disable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird der öffentliche Anbieter mit dem Identitätswert "Messenger" deaktiviert. Wenn MSN bereits deaktiviert ist, wird beim Ausführen dieses Befehls ein Fehler zurückgegeben.

    Disable-CsPublicProvider -Identity "Messenger"

## BEISPIEL 2

In Beispiel 2 werden alle derzeit aktivierten öffentlichen Anbieter deaktiviert. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller öffentlichen Anbieter zurückzugeben, die derzeit in der Organisation verwendet werden. Diese Auflistung wird an das Cmdlet **Where-Object** weitergeleitet, das nur die Anbieter herausfiltert, bei denen die Eigenschaft "Enabled" den Wert "True" aufweist. Diese Auflistung wird an das Cmdlet **Disable-CsPublicProvider** weitergeleitet, das jeden Anbieter in der Auflistung deaktiviert.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $True} | Disable-CsPublicProvider

## BEISPIEL 3

Der Befehl in Beispiel 3 deaktiviert alle öffentlichen Anbieter, die derzeit aktiviert sind und bei denen die Überprüfungsstufe auf "AlwaysVerifiable" gesetzt ist. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller öffentlichen Anbieter zurückzugeben, die derzeit in der Organisation verwendet werden. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Anbieter auswählt, die zwei Kriterien erfüllen: 1) Die Eigenschaft "VerificationLevel " weist den Wert "AlwaysVerifiable" auf, und 2) die Eigenschaft "Enabled" weist den Wert "True" auf. (Der Operator "-and" weist das Cmdlet **Where-Object** an, dass ein Objekt alle angegebenen Kriterien erfüllen muss, um ausgewählt zu werden.) Die gefilterte Auflistung wird dann an das Cmdlet **Disable-CsPublicProvider** weitergeleitet, das jeden Anbieter in der Auflistung deaktiviert.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable" -and $_.Enabled -eq $True} | Disable-CsPublicProvider

## Detaillierte Beschreibung

Ein Partnerverbund ist eine Möglichkeit, mit der zwei Organisationen eine Vertrauensstellung einrichten können, die die Kommunikation zwischen den beiden Gruppen erleichtert. Wenn ein Partnerverbund eingerichtet wurde, können Benutzer in beiden Organisationen einander Chatnachrichten senden, Anwesenheitsbenachrichtigungen abonnieren und mithilfe von SIP-Anwendungen wie Lync 2013 miteinander kommunizieren. Lync Server bietet drei Arten des Partnerverbunds: 1) direkter Partnerverbund zwischen Ihrer und einer anderen Organisation, 2) Partnerverbund zwischen Ihrer Organisation und einem öffentlichen Anbieter und 3) Partnerverbund zwischen Ihrer Organisation und einem externen Hostinganbieter.

Ein öffentlicher Anbieter ist eine Organisation, die SIP (Session Initiation Protocol)-Kommunikationsdienste für die breite Öffentlichkeit bereitstellt. Wenn Sie eine Partnerverbundbeziehung mit einem öffentlichen Anbieter einrichten, stellen Sie im Prinzip einen Partnerverbund mit allen Benutzern her, deren Konto von diesem Anbieter gehostet wird. Bei einem Partnerverbund mit Messenger (MSN) können Benutzer Chatnachrichten und Anwesenheitsinformationen mit allen anderen Benutzern austauschen, die über ein Instant Messaging-Konto für Messenger verfügen.

Um mit einem öffentlichen Anbieter im Partnerverbund zu arbeiten, müssen Sie einen neuen öffentlichen Anbieter erstellen und aktivieren. (Darüber hinaus muss der öffentliche Anbieter eine Partnerverbundbeziehung mit Ihnen einrichten.) Wenn Sie einen öffentlichen Anbieter erstellen, können Sie diese Partnerverbundbeziehung entweder aktivieren oder deaktivieren. Wird ein öffentlicher Anbieter aktiviert, können Benutzer in der Organisation Chatnachrichten und Anwesenheitsinformationen mit Personen austauschen, die über ein Konto bei dem öffentlichen Anbieter verfügen. Wird ein öffentlicher Anbieter deaktiviert, besteht so lange keine Möglichkeit mehr, mit Personen mit einem Konto bei dem öffentlichen Anbieter zu kommunizieren, bis der Anbieter wieder aktiviert wurde. Wenn Sie eine Beziehung mit einem Anbieter zeitweise unterbrechen müssen, verwenden Sie das Cmdlet **Disable-CsPublicProvider**. Ziehen Sie es vor, den Anbieter vollständig zu löschen, verwenden Sie das Cmdlet **Remove-CsPublicProvider**.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Disable-CsPublicProvider** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsPublicProvider"}

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
<td><p>Eindeutige ID für den zu deaktivierenden öffentlichen Anbieter. Als Identitätswert wird in der Regel der Name der Website verwendet, die die Dienste bereitstellt (z. B. Yahoo!, AOL, MSN).</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider-Objekt. Das Cmdlet **Disable-CsPublicProvider** akzeptiert weitergeleitete Instanzen des Objekts für öffentliche Anbieter.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider" deaktiviert.

## Siehe auch

#### Weitere Ressourcen

[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

