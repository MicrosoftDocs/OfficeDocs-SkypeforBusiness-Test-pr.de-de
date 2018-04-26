---
title: Remove-CsClientVersionConfiguration
TOCTitle: Remove-CsClientVersionConfiguration
ms:assetid: 42065d1d-a0ef-4fa4-826b-d65b14b343c9
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425925(v=OCS.15)
ms:contentKeyID: 49293815
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Entfernt die angegebene Auflistung von Konfigurationseinstellungen für Clientversionen. Konfigurationseinstellungen für die Clientversion legen fest, ob Lync Server die Versionsnummer der einzelnen Clientanwendungen prüft, die sich beim System anmelden. Wenn die Clientversionsfilterung aktiviert ist, hängt der Zugriff der jeweiligen Clientanwendung auf das System von den Einstellungen ab, die in der entsprechenden Clientversionsrichtlinie konfiguriert sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Remove-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 löscht die Konfigurationseinstellungen für Clientversionen mit dem Identitätswert "site:Redmond".

    Remove-CsClientVersionConfiguration -Identity site:Redmond

## BEISPIEL 2

In Beispiel 2 werden alle Konfigurationseinstellungen für Clientversionen gelöscht, die auf Standortebene zugewiesen wurden. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsClientVersionConfiguration** mit dem Parameter "Filter" auf. Mit dem Filterwert "site:\*" wird sichergestellt, dass nur die Konfigurationseinstellungen für Clientversionen ausgewählt werden, deren Identitätswert mit dem Zeichenfolgenwert "site:" beginnt. Diese gefilterte Auflistung wird dann an das Cmdlet **Remove-CsClientVersionConfiguration** weitergeleitet, um sämtliche Elemente in der Auflistung zu löschen.

    Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## BEISPIEL 3

Im dritten Beispiel werden alle Konfigurationseinstellungen für Clientversionen gelöscht, die derzeit deaktiviert sind. Hierzu gibt der Befehl zunächst mit dem Cmdlet **Get-CsClientVersionConfiguration** eine Auflistung aller derzeit in der Organisation verwendeten Konfigurationseinstellungen für Clientversionen zurück. Nachdem die Daten zurückgegeben wurden, wird die Auflistung an das Cmdlet **Where-Object** weitergeleitet, das die Einstellungen herausfiltert, bei denen die Eigenschaft "Enabled" den Wert "False" besitzt. Die gefilterte Auflistung wird dann an das Cmdlet **Remove-CsClientVersionConfiguration** weitergeleitet, das jedes Element in der Auflistung löscht.

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionConfiguration

## Detaillierte Beschreibung

Lync Server räumt Administratoren einen beträchtlichen Spielraum in Bezug auf die Angabe der Clientsoftware (und ebenso auf die Versionsnummer der jeweiligen Software) ein, mit der Benutzer sich beim System anmelden können. Beispielsweise gibt es keinen technischen Grund dafür, dass Benutzer sich über Lync Server bei Lync anmelden müssen. Es gelten keine technischen Einschränkungen, die einen Benutzer an der Anmeldung über Microsoft Office Communicator 2007 R2 hindern.

Es kann jedoch andere Gründe dafür geben, dass Benutzer sich nicht über Office Communicator 2007 R2 anmelden sollten. Beispielsweise unterstützt Office Communicator 2007 R2 nicht alle Funktionen und Möglichkeiten von Lync. Demzufolge verwenden Benutzer, die sich über Office Communicator 2007 R2 anmelden, die Anwendung anders als Benutzer, die sich über Lync anmelden. Dieser Umstand kann sowohl für Ihre Benutzer zu Schwierigkeiten führen als auch für das Helpdeskpersonal, das Support für eine Reihe verschiedener Clientanwendungen leisten muss.

Wenn dies für Ihre Organisation ein Problem darstellen könnte, können Sie die Clientversionsfilterung einsetzen und angeben, welche Clientanwendungen für die Anmeldung bei Lync Server verwendet werden können. Bei der Installation von Lync Server wird ein globaler Satz mit Konfigurationseinstellungen für Clientversionen installiert und aktiviert. Zusätzlich zu den globalen Einstellungen können Konfigurationseinstellungen für die Clientversion auch auf Standortebene angewendet werden.

Sämtliche der erstellten standortbasierten Einstellungen können später mit dem Cmdlet **Remove-CsClientVersionConfiguration** wieder gelöscht werden. Beachten Sie, dass Sie das Cmdlet **Remove-CsClientVersionConfiguration** auch für die globalen Einstellungen ausführen können. In diesem Fall werden die globalen Einstellungen nicht entfernt. Stattdessen werden die globalen Eigenschaften auf ihre Standardwerte zurückgesetzt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Remove-CsClientVersionConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutige ID der Auflistung von zu entfernenden Konfigurationseinstellungen für Clientversionen. Verwenden Sie folgende Syntax, um die globale Auflistung zu entfernen: -Identity global. (Beachten Sie, dass die globalen Einstellungen nicht wirklich entfernt werden. Stattdessen werden die globalen Eigenschaften auf ihre Standardwerte zurückgesetzt.) Verwenden Sie eine Syntax wie die folgende, um eine Standortauflistung zu entfernen: -Identity site:Redmond. Beachten Sie, dass beim Angeben des Identitätswerts keine Platzhalterzeichen verwendet werden können.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration-Objekt. Das Cmdlet **Remove-CsClientVersionConfiguration** akzeptiert weitergeleitete Instanzen des Konfigurationsobjekts für die Clientversion.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration" gelöscht.

## Siehe auch

#### Weitere Ressourcen

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

