---
title: New-CsClientVersionConfiguration
TOCTitle: New-CsClientVersionConfiguration
ms:assetid: e7aac850-9e29-4d18-8929-74a89e9355cd
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399029(v=OCS.15)
ms:contentKeyID: 49295744
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt eine neue Auflistung von Konfigurationseinstellungen für Clientversionen. Konfigurationseinstellungen für die Clientversion legen fest, ob Lync Server die Versionsnummer der einzelnen Clientanwendungen prüft, die sich beim System anmelden. Wenn die Clientversionsfilterung aktiviert ist, hängt der Zugriff der jeweiligen Clientanwendung auf das System von den Einstellungen ab, die in der entsprechenden Clientversionsrichtlinie konfiguriert sind. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 erstellt eine neue Auflistung von Konfigurationseinstellungen für Clientversionen für den Standort Redmond. In diesem Befehl wird der Parameter "Enabled" auf "False" festgelegt, d. h., Clientfilter werden für den Standort "Redmond" deaktiviert.

    New-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## BEISPIEL 2

Beispiel 2 zeigt, wie Sie eine neue Auflistung von Konfigurationseinstellungen für Clientversionen im Arbeitsspeicher erstellen und ändern können und diese virtuellen Einstellungen dann in eine tatsächliche Auflistung von Einstellungen für den Standort Redmond umwandeln. Dazu verwendet der erste Befehl das Cmdlet **New-CsClientVersionConfiguration** und den Parameter "InMemory", um eine Auflistung von Einstellungen mit dem Identitätswert "site:Redmond" zu erstellen, die nur im Arbeitsspeicher vorhanden ist. Diese Auflistung wird in der Variablen "$x" gespeichert und ist nur im Arbeitsspeicher vorhanden. Wenn Sie die Windows PowerShell-Sitzung beenden oder die Variable "$x" löschen, gehen diese Konfigurationseinstellungen für Clientversionen verloren und werden niemals auf den Standort "Redmond" angewendet.

In Befehl 2 wird der Wert der Eigenschaft "DefaultAction" für die virtuellen Einstellungen auf "Block" festgelegt. In Befehl 3 werden die virtuellen Einstellungen dann mit dem Cmdlet **Set-CsClientVersionConfiguration** in eine tatsächliche Auflistung von Konfigurationseinstellungen für Clientversionen umgewandelt, die auf den Standort "Redmond" angewendet werden.

    $x = New-CsClientVersionConfiguration -Identity site:Redmond -InMemory
    $x.DefaultAction = "Block" 
    Set-CsClientVersionConfiguration -Instance $x

## Detaillierte Beschreibung

Lync Server räumt Administratoren einen beträchtlichen Spielraum in Bezug auf die Angabe der Clientsoftware (und ebenso auf die Versionsnummer der jeweiligen Software) ein, mit der Benutzer sich beim System anmelden können. Beispielsweise gibt es keinen technischen Grund dafür, dass Benutzer sich über Lync Server bei Lync anmelden müssen. Es gelten keine technischen Einschränkungen, die einen Benutzer an der Anmeldung über Microsoft Office Communicator 2007 R2 hindern.

Es kann jedoch nicht technische Gründe dafür geben, dass Benutzer sich nicht über Office Communicator 2007 R2 anmelden sollten. Beispielsweise unterstützt Office Communicator 2007 R2 nicht alle Funktionen und Möglichkeiten von Lync. Demzufolge verwenden Benutzer, die sich über Office Communicator 2007 R2 anmelden, die Anwendung anders als Benutzer, die sich über Lync anmelden. Dieser Umstand kann sowohl für Ihre Benutzer zu Schwierigkeiten führen als auch für das Helpdeskpersonal, das Support für eine Reihe verschiedener Clientanwendungen leisten muss.

Wenn dies für Ihre Organisation ein Problem darstellen könnte, können Sie die Clientversionsfilterung einsetzen und angeben, welche Clientanwendungen für die Anmeldung bei Lync Server verwendet werden können. Bei der Installation von Lync Server wird ein globaler Satz mit Konfigurationseinstellungen für Clientversionen installiert und aktiviert. Anhand dieser Einstellungen wird festgelegt, ob die Clientversionsfilterung aktiviert wird.

Neben den globalen Einstellungen können Sie mit dem Cmdlet **New-CsClientVersionConfiguration** Konfigurationseinstellungen für Clientversionen auf Standortebene erstellen. Auf Standortebene angewendete Konfigurationseinstellungen für Clientversionen haben Vorrang vor den globalen Einstellungen. Nehmen Sie beispielsweise an, Sie haben Clientversionsfilter auf globaler Ebene aktiviert und erstellen dann eine separate Auflistung von Einstellungen für den Standort Redmond, bei der Clientversionsfilter deaktiviert sind. In diesem Fall sind Clientversionsfilter für alle Benutzer deaktiviert, die über ein Konto am Standort Redmond verfügen.

Beachten Sie jedoch, dass für anonyme Benutzer nur globale Einstellungen gelten, denn anonyme Benutzer sind keinem Standort zugeordnet.

Beachten Sie, dass die Clientversionskonfiguration keine Sicherheitsfunktion darstellt. Die Technologie verlässt sich auf die Selbstauskunft der Clientanwendungen und versucht nicht sicherzustellen, dass es sich bei einer Anwendung tatsächlich um die Anwendung und die Versionsnummer handelt, die sie vorgibt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsClientVersionConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionConfiguration"}

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
<td><p>Stellt die eindeutige ID dar, die der neuen Auflistung von Konfigurationseinstellungen für Clientversionen zugewiesen werden soll. Da Sie neue Auflistungen nur auf Standortebene erstellen können, weist der Identitätswert immer das Präfix &quot;site:&quot; auf, gefolgt vom Standortnamen, z. B. &quot;site:Redmond&quot;. Beachten Sie, dass bei dem vorstehenden Befehl ein Fehler auftritt, wenn bereits eine Auflistung von Einstellungen mit dem Identitätswert &quot;site:Redmond&quot; vorhanden ist.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Gibt die auszuführende Aktion beim Versuch eines Benutzers an, sich über eine Clientanwendung anzumelden, deren Versionsnummer nicht in der entsprechenden Clientversionsrichtlinie ermittelt werden kann. &quot;DefaultAction&quot; muss auf einen der folgenden Werte festgelegt werden:</p>
<p>Allow. Die Clientanwendung kann sich anmelden.</p>
<p>AllowWithUrl. Die Clientanwendung kann sich anmelden. Darüber hinaus wird eine Meldung angezeigt, die die URL einer Webseite enthält, von der der Benutzer eine genehmigte Clientanwendung herunterladen kann. Die URL für diese Webseite sollte als Wert für die Eigenschaft &quot;DefaultUrl&quot; angegeben werden.</p>
<p>Block. Die Clientanwendung kann sich nicht anmelden.</p>
<p>BlockWithUrl. Die Clientanwendung kann sich nicht anmelden. Allerdings enthält das Meldungsfenster &quot;Access denied&quot;, das dem Benutzer angezeigt wird, die URL einer Webseite, von der der Benutzer eine genehmigte Clientanwendung herunterladen kann. Die URL für diese Webseite sollte als Wert für die Eigenschaft &quot;DefaultUrl&quot; angegeben werden.</p>
<p>Diese Eigenschaft wird ignoriert, wenn die Eigenschaft &quot;Enabled&quot; auf &quot;False&quot; festgelegt ist. Wenn die Eigenschaft &quot;Enabled&quot; auf &quot;False&quot; festgelegt wird, werden keine Clientversionsfilter angewendet.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultURL</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Gibt die URL der Webseite an, von der Benutzer eine genehmigte Clientanwendung herunterladen können. Wird dieser Wert angegeben und &quot;DefaultAction&quot; auf &quot;BlockWithUrl&quot; festgelegt, wird diese URL im Meldungsfenster &quot;Access denied&quot; angezeigt, das jedes Mal geöffnet wird, wenn der Benutzer versucht, sich über eine nicht unterstützte Anwendung anzumelden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Gibt an, ob die Clientversionsfilterung aktiviert ist. Wenn die Eigenschaft &quot;Enabled&quot; den Wert &quot;True&quot; aufweist, überprüft der Server die Versionsnummer jeder Clientanwendung, die einen Anmeldeversuch unternimmt. Auf der Grundlage der entsprechenden Clientversionsrichtlinie erlaubt oder verweigert der Server dann den Zugriff. Weist die Eigenschaft &quot;Enabled&quot; den Wert &quot;False&quot; auf, kann sich jede anmeldefähige Clientanwendung anmelden.</p>
<p>Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
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

Keine. Das Cmdlet **New-CsClientVersionConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Erstellt neue Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration".

## Siehe auch

#### Weitere Ressourcen

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

