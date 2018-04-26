---
title: Set-CsClientVersionConfiguration
TOCTitle: Set-CsClientVersionConfiguration
ms:assetid: 7cd2e86f-2d31-4db2-9d0f-f1418fd4aba2
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398623(v=OCS.15)
ms:contentKeyID: 49294525
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert die angegebene Auflistung von Konfigurationseinstellungen für Clientversionen. Konfigurationseinstellungen für die Clientversion legen fest, ob Lync Server die Versionsnummer der einzelnen Clientanwendungen prüft, die sich beim System anmelden. Wenn die Clientversionsfilterung aktiviert ist, hängt der Zugriff der jeweiligen Clientanwendung auf das System von den Einstellungen ab, die in der entsprechenden Clientversionsrichtlinie konfiguriert sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird das Cmdlet **Set-CsClientVersionConfiguration** zum Ändern der Auflistung von Einstellungen mit der Identität "site:Redmond" verwendet. In diesem Fall wird der Parameter "Enabled" auf "False" festgelegt, um die Konfigurationseinstellungen für Clientversionen zu deaktivieren.

    Set-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## BEISPIEL 2

In Beispiel 2 wird die Eigenschaft "DefaultUrl" für alle gegenwärtig in der Organisation verwendeten Konfigurationseinstellungen für Clientversionen geändert. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsClientVersionConfiguration** ohne zusätzliche Parameter auf, um sämtliche Konfigurationseinstellungen für Clientversionen zurückzugeben. Diese Informationen werden an das Cmdlet **Set-CsClientVersionConfiguration** weitergeleitet, das den Wert von "DefaultUrl" für jede Konfigurationsauflistung auf "https://litwareinc.com/csclients" setzt.

    Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration -DefaultURL "https://litwareinc.com/csclients"

## BEISPIEL 3

In Beispiel 3 werden alle Konfigurationseinstellungen für Clientversionen geändert, deren Eigenschaft "DefaultAction" gegenwärtig auf "Block" festgelegt ist. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsClientVersionConfiguration** auf, um eine Auflistung aller derzeit verwendeten Konfigurationseinstellungen für Clientversionen zurückzugeben. Diese Informationen werden an das Cmdlet **Where-Object** weitergeleitet, das die Einträge herausfiltert, bei denen die Eigenschaft "DefaultAction" den Wert "Block" aufweist. Diese gefilterte Auflistung wiederum wird an das Cmdlet **Set-CsClientVersionConfiguration** weitergeleitet, das für jedes Element in der Auflistung zwei Aktionen ausführt: 1) Festlegen von "DefaultAction" auf "BlockWithUrl" und 2) Festlegen von "DefaultUrl" auf "https://litwareinc.com/csclients".

    Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block"} | Set-CsClientVersionConfiguration -DefaultAction "BlockWithUrl" -DefaultURL "https://litwareinc.com/csclients"

## Detaillierte Beschreibung

Lync Server räumt Administratoren einen beträchtlichen Spielraum in Bezug auf die Angabe der Clientsoftware (und ebenso auf die Versionsnummer der jeweiligen Software) ein, mit der Benutzer sich beim System anmelden können. Beispielsweise gibt es keinen technischen Grund dafür, dass Benutzer sich über Lync Server bei Lync anmelden müssen. Es gelten keine technischen Einschränkungen, die einen Benutzer an der Anmeldung über Microsoft Office Communicator 2007 R2 hindern.

Auf der anderen Seite könnte es jedoch nicht technische Gründe dafür geben, dass Benutzer sich nicht über Office Communicator 2007 R2 anmelden sollten. Beispielsweise unterstützt Office Communicator 2007 R2 nicht alle Funktionen und Möglichkeiten von Lync. Demzufolge verwenden Benutzer, die sich über Office Communicator 2007 R2 anmelden, die Anwendung anders als Benutzer, die sich über Lync anmelden. Dieser Umstand kann sowohl für Ihre Benutzer zu Schwierigkeiten führen als auch für das Helpdeskpersonal, das Support für eine Reihe verschiedener Clientanwendungen leisten muss.

Wenn dies für Ihre Organisation ein Problem darstellen könnte, können Sie die Clientversionsfilterung einsetzen und angeben, welche Clientanwendungen für die Anmeldung bei Lync Server verwendet werden können. Bei der Installation von Lync Server wird ein globaler Satz mit Konfigurationseinstellungen für Clientversionen installiert und aktiviert. Anhand dieser Einstellungen wird festgelegt, ob die Clientversionsfilterung aktiviert wird. Zusätzlich zu den globalen Einstellungen können Konfigurationseinstellungen für Clientversionen auch auf Standortebene angewendet werden. In diesen Fällen haben die standortbasierten Einstellungen Vorrang vor den globalen Einstellungen.

Mit dem Cmdlet **Set-CsClientVersionConfiguration** können Sie eine vorhandene Auflistung von Konfigurationseinstellungen für Clientversionen ändern.

Beachten Sie, dass die Clientversionskonfiguration keine Sicherheitsfunktion darstellt. Die Technologie verlässt sich auf die Selbstauskunft der Clientanwendungen und versucht nicht sicherzustellen, dass es sich bei einer Anwendung tatsächlich um die Anwendung und die Versionsnummer handelt, die sie vorgibt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsClientVersionConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionConfiguration"}

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
<td><p><em>DefaultAction</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Gibt die auszuführende Aktion beim Versuch eines Benutzers an, sich über eine Clientanwendung anzumelden, deren Versionsnummer nicht in der entsprechenden Clientversionsrichtlinie ermittelt werden kann. &quot;DefaultAction&quot; muss auf einen der folgenden Werte festgelegt werden:</p>
<p>Allow. Die Clientanwendung kann sich anmelden.</p>
<p>AllowWithUrl. Die Clientanwendung kann sich anmelden. Zusätzlich wird dem Benutzer ein Meldungsfenster angezeigt, in dem die URL einer Webseite aufgeführt ist, von der der Benutzer eine genehmigte Clientanwendung herunterladen kann. Die URL für diese Webseite sollte als Wert für die Eigenschaft &quot;DefaultUrl&quot; angegeben werden.</p>
<p>Block. Die Clientanwendung kann sich nicht anmelden.</p>
<p>BlockWithUrl. Die Clientanwendung kann sich nicht anmelden. Allerdings enthält das Meldungsfenster &quot;Access denied&quot;, das dem Benutzer angezeigt wird, die URL einer Webseite, von der der Benutzer eine genehmigte Clientanwendung herunterladen kann. Die URL für diese Webseite sollte als Wert für die Eigenschaft &quot;DefaultUrl&quot; angegeben werden.</p>
<p>Diese Eigenschaft wird ignoriert, wenn die Eigenschaft &quot;Enabled&quot; auf &quot;False&quot; festgelegt ist. Wenn die Eigenschaft &quot;Enabled&quot; auf &quot;False&quot; gesetzt wird, werden keine Clientversionsfilter angewendet.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultURL</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Gibt die URL der Webseite an, von der Benutzer eine genehmigte Clientanwendung herunterladen können. Wird dieser Wert angegeben und &quot;DefaultAction&quot; auf &quot;BlockWithURL&quot; gesetzt, erscheint diese URL im Meldungsfenster &quot;Access denied&quot;, das jedes Mal angezeigt wird, wenn der Benutzer versucht, sich über eine nicht unterstützte Anwendung anzumelden.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Gibt an, ob die Clientversionsfilterung aktiviert ist. Wenn die Eigenschaft &quot;Enabled&quot; auf &quot;True&quot; festgelegt ist, überprüft der Server die Versionsnummer jeder Clientanwendung, die zum Anmelden verwendet wird. Der Zugriff wird anschließend basierend auf der entsprechenden Clientversionsrichtlinie zugelassen oder verweigert. Weist die Eigenschaft &quot;Enabled&quot; den Wert &quot;False&quot; auf, kann sich jede anmeldefähige Clientanwendung anmelden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Die eindeutige ID der Konfigurationseinstellungen für Clientversionen, die geändert werden sollen. Verwenden Sie eine Syntax wie die folgende, um die globalen Einstellungen zu ändern: -Identity global. Verwenden Sie eine Syntax wie die folgende, um die auf Standortebene zugewiesenen Einstellungen zu ändern: &quot;site:Redmond&quot;.</p>
<p>Wenn dieser Parameter nicht enthalten ist, werden mit dem Cmdlet <strong>Set-CsClientVersionConfiguration</strong> automatisch die globalen Einstellungen konfiguriert.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>ClientVersionPolicy-Objekt</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration-Objekt. Das Cmdlet **Set-CsClientVersionConfiguration** akzeptiert weitergeleitete Instanzen des Konfigurationsobjekts für Clientversionen.

## Rückgabetypen

Das Cmdlet **Set-CsClientVersionConfiguration** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)

