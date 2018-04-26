---
title: New-CsVoicePolicy
TOCTitle: New-CsVoicePolicy
ms:assetid: 3852de89-a604-437a-9fdf-3597b88ce13d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425856(v=OCS.15)
ms:contentKeyID: 49293687
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicePolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt eine neue VoIP-Richtlinie. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsVoicePolicy -Identity <XdsIdentity> [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die neue benutzerbasierte VoIP-Richtlinie mit der Identität "UserVoicePolicy1" unter Verwendung der Standardeinstellungen erstellt.

    New-CsVoicePolicy -Identity UserVoicePolicy1

## BEISPIEL 2

In diesem Beispiel wird die neue benutzerbasierte VoIP-Richtlinie mit dem Identitätswert "UserVoicePolicy2" erstellt. Zudem wird die Eigenschaft "AllowSimulRing" auf "False" festgelegt, sodass die Funktion für gleichzeitiges Klingeln bei den dieser Richtlinie zugewiesenen Benutzern nicht aktiviert ist. Über diese Funktion wird festgelegt, ob beim Klingeln des Bürotelefons eines Benutzers gleichzeitig auch ein zweites Telefon (z. B. ein Mobiltelefon) läuten soll. Mit diesem Befehl wird außerdem "Local" zu der Liste von PSTN-Verwendungen hinzugefügt, wodurch diese VoIP-Richtlinie einer VoIP-Route zugeordnet wird, die ebenfalls die PSTN-Verwendung "Local" verwendet. (Beachten Sie, dass der Parameter "Identity" nicht explizit angegeben wird. Der Parameter "Identity" ist ein Positionsparameter. Wenn Sie den Identitätswert in der Parameterliste zuerst angeben, muss daher nicht explizit angegeben werden, dass es sich um die Identität handelt.)

    New-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{add = "Local"}

## BEISPIEL 3

In diesem Beispiel wird eine neue VoIP-Richtlinie für den Standort "Redmond" erstellt. Zudem werden alle für die Organisation definierten PSTN-Verwendungen auf diese Richtlinie angewendet. In der ersten Zeile dieses Beispiels wird das Cmdlet **Get-CsPstnUsage** aufgerufen, um den globalen Satz mit PSTN-Verwendungen für die Organisation abzurufen und in der Variablen "$a" zu speichern. In der zweiten Zeile wird das Cmdlet **New-CsVoicePolicy** aufgerufen, um die neue VoIP-Richtlinie für den Standort "Redmond" zu erstellen. An den Parameter "PstnUsages" wird ein Wert übergeben, um dieser Richtlinie die im globalen Satz von PSTN-Verwendungen enthaltene Liste hinzuzufügen. Beachten Sie die Syntax des add-Werts: $a.Usage. Dies bezieht sich auf die Eigenschaft "Usage" der PSTN-Verwendungseinstellungen, welche die Liste der PSTN-Verwendungen enthält.

    $a = Get-CsPstnUsage
    New-CsVoicePolicy site:Redmond -PstnUsages @{add = $a.Usage}

## Detaillierte Beschreibung

Mit diesem Cmdlet wird eine neue VoIP-Richtlinie erstellt. VoIP-Richtlinien werden zum Verwalten von Enterprise-VoIP-bezogenen Funktionen verwendet, z. B. für das gleichzeitige Klingeln (die Möglichkeit, ein zweites Telefon läuten zu lassen, wenn jemand die Nummer Ihres Bürotelefons wählt) und die Anrufweiterleitung. Die mit diesem Cmdlet erstellte Richtlinie bestimmt, ob eine Vielzahl dieser Funktionen aktiviert oder deaktiviert ist.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsVoicePolicy** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicePolicy"}

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
<td><p>XdsIdentity</p></td>
<td><p>Eine eindeutige ID zur Angabe des Bereichs oder des Namens der Richtlinie. Zulässige Werte für dieses Cmdlet sind &quot;site:&lt;Standortname&gt;&quot; (wobei &lt;Standortname&gt; der Name des Lync Server-Standorts ist, für den die Richtlinie gilt – beispielsweise &quot;site:Redmond&quot;) und eine Zeichenfolge zum Angeben einer benutzerbasierten Richtlinie (beispielsweise &quot;RedmondVoicePolicy&quot;). Standardmäßig ist eine globale Richtlinie vorhanden.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wird dieser Parameter auf &quot;True&quot; festgelegt, ist keine Anrufweiterleitung möglich. Wird &quot;False&quot; festgelegt, ist keine Anrufweiterleitung möglich.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wenn dieser Parameter auf &quot;True&quot; festgelegt ist, werden Anrufe bei internen Nummern, die sich in einem anderen Pool befinden, über das Telefonfestnetz (Public Switched Telephone Network, PSTN) geleitet, wenn der Pool oder das WAN nicht verfügbar ist.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gleichzeitiges Klingeln ist eine Funktion, mit der mehrere Telefone läuten können, wenn eine einzige Nummer gewählt wird. Bei Festlegung von &quot;True&quot; wird diese Funktion aktiviert. Wenn dieser Parameter auf &quot;False&quot; festgelegt wird, kann das gleichzeitige Klingeln für die dieser Richtlinie zugewiesenen Benutzer nicht konfiguriert werden.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Optional</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Ermöglicht Administratoren die Verwaltung von Anrufweiterleitung und gleichzeitigem Klingeln. Zulässige Werte:</p>
<p>* VoicePolicyUsage – Die VoIP-Richtlinie wird standardmäßig zum Verwalten von Anrufweiterleitung und gleichzeitigem Klingeln für alle Anrufe verwendet. Dies ist der Standardwert.</p>
<p>* InternalOnly – Anrufweiterleitung und gleichzeitiges Klingeln sind auf Anrufe zwischen Lync-Benutzern beschränkt.</p>
<p>* CustomUsage – Für die Verwaltung von Anrufweiterleitung und gleichzeitigem Klingeln wird eine benutzerdefinierte Nutzung des Telefonfestnetzes (Public Switched Telephone Network, PSTN) verwendet. Diese Nutzung muss mithilfe des Parameters &quot;CustomCallForwardingSimulRingUsages&quot; angegeben werden.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Benutzerdefinierte Nutzung des Telefonfestnetzes (Public Switched Telephone Network, PSTN) für die Verwaltung von Anrufweiterleitung und gleichzeitigem Klingeln. Verwenden Sie eine Syntax nach folgendem Muster, um einer VoIP-Richtlinie eine benutzerdefinierte Nutzung hinzuzufügen:</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Verwenden Sie folgende Syntax, um eine benutzerdefinierte Nutzung zu entfernen:</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Beachten Sie, dass die Nutzung vorhanden sein muss, damit sie mit dem Parameter &quot;CustomCallForwardingSimulRingUsages&quot; verwendet werden kann.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Eine Beschreibung der VoIP-Richtlinie.</p>
<p>Maximale Länge: 1040 Zeichen.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Sie können Richtlinien zur Verwaltung der Netzwerkkonfiguration, wie beispielsweise zur Beschränkung der Bandbreite, festlegen. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, können diese Richtlinien außer Kraft gesetzt werden. Anders ausgedrückt: Wenn dieser Parameter auf &quot;True&quot; festgelegt ist, finden keine Bandbreitenprüfungen statt und Anrufe werden unabhängig von den Anrufsteuerungseinstellungen durchgestellt.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Mit der Anwendung zum Parken von Anrufen können Anrufe bei einer bestimmten Nummer innerhalb eines Nummernbereichs geparkt werden, um zu einem späteren Zeitpunkt abgerufen zu werden. Bei Festlegung von &quot;True&quot; wird die Anwendung aktiviert. Wenn dieser Parameter auf &quot;False&quot; festgelegt wird, können die dieser Richtlinie zugewiesenen Benutzer keine Anrufe parken, die über ihre Telefonnummer eingehen.</p>
<p>Standard: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Bestimmt, ob Anrufe an eine andere Nummer weitergeleitet werden können. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, können Anrufe weitergeleitet werden. Bei Festlegung von &quot;False&quot; ist keine Weiterleitung möglich.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Mit der Anrufdelegierung kann ein Benutzer die Anrufe für einen anderen Benutzer entgegennehmen oder Anrufe im Namen des anderen Benutzers tätigen. Ein Vorgesetzter kann beispielsweise die Anrufdelegierung einrichten, damit bei eingehenden Anrufen sowohl das eigene als auch das Telefon eines Administrators läutet. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, können die dieser Richtlinie zugewiesenen Benutzer die Anrufdelegierung einrichten. Bei Festlegung von &quot;False&quot; wird die Anrufdelegierung deaktiviert.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Die Nachverfolgung bei Missbrauch durch Anrufer ist ein Standard, um Anrufe nachzuverfolgen, bei denen ein Benutzer eine Belästigung meldet. Diese Anrufe können auch dann nachverfolgt werden, wenn die Anruferkennung unterdrückt wird. Die Nachverfolgung ist nur durch autorisierte Stellen möglich, nicht durch den Benutzer. Wenn diese Eigenschaft auf &quot;True&quot; festgelegt wird, kann eine Nachverfolgung bei Missbrauch durch Anrufer aktiviert werden.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Mit der Funktion für Teamanrufe kann ein Benutzer eine Gruppe von Benutzern bestimmen, deren Telefone beim Eingehen von Anrufen an die eigene Nummer läuten. Diese Funktion ist z. B. für Teams nützlich, in denen ein beliebiges Teammitglied eingehende Anrufe von Kunden annehmen kann. Bei Festlegung von &quot;True&quot; wird diese Funktion aktiviert.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Ist dieser Wert auf &quot;True&quot; festgelegt, werden nicht entgegengenommene Anrufe bei einem Mobilgerät an die Voicemail der Organisation (und nicht an die Voicemail des Geräteanbieters) weitergeleitet. Wird ein Anruf &quot;zu früh&quot; (also vor Ablauf des für die Eigenschaft &quot;PSTNVoicemailEscapeTimer&quot; konfigurierten Werts) entgegengenommen, wird angenommen, dass das Mobilgerät nicht verfügbar ist, und der Anruf wird an die Voicemail der Organisation weitergeleitet.</p>
<p>Der Standardwert ist &quot;False&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Ein Anzeigename zur Beschreibung dieser Richtlinie.</p>
<p>Standard: DefaultPolicy</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Für Anrufe im Telefonfestnetz (Public Switched Telephone Network, PSTN) fallen üblicherweise Gebühren an. Organisationen können diese Gebühren durch die Implementierung einer VoIP-Lösung (Voice over Internet Protocol) umgehen, bei der sich Zweigstellen über Netzwerkanrufe verbinden können. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, erfolgen Anrufe nicht über das Netzwerk (zur Umgehung der Gebühren), sondern gebührenpflichtig über das Telefonfestnetz.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste der für diese Richtlinie verfügbaren PSTN-Verwendungen. Die PSTN-Verwendung verknüpft eine VoIP-Richtlinie mit einer Telefonroute.</p>
<p>In diese Liste kann ein Zeichenfolgenwert gesetzt werden, sofern dieser Wert in der aktuellen globalen Liste von PSTN-Verwendungen vorhanden ist. (Doppelte Zeichenfolgen sind nicht zulässig, alle Einträge müssen eindeutig sein.) Die Liste der PSTN-Verwendungen kann mit dem Cmdlet <strong>Get-CsPstnUsage</strong> abgerufen werden.</p>
<p>Diese Liste ist standardmäßig leer. Wenn Sie keinen Wert für diesen Parameter bereitstellen, wird eine Warnmeldung angezeigt, dass Benutzer, denen diese Richtlinie zugewiesen wurde, keine ausgehenden PSTN-Anrufe tätigen können.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Int64</p></td>
<td><p>Zeitwert (in Millisekunden), mit dessen Hilfe ermittelt wird, ob ein Anruf &quot;zu früh&quot; entgegengenommen wurde. Erfolgt die Entgegennahme eines Anrufs innerhalb dieses Zeitraums, wird von Lync Server davon ausgegangen, dass das Mobilgerät nicht verfügbar ist, und der Anruf wird automatisch an die Voicemail der Organisation weitergeleitet. Wird der Anruf nicht vor Ablauf dieses Zeitraums entgegengenommen, wird der Anruf normal weitergegeben. Der Standardwert ist 1500 Millisekunden.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>GUID</p></td>
<td><p>GUID (Globally Unique Identifier) des Skype for Business Online-Mandantenkontos, für das die neue VoIP-Richtlinie erstellt wird. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für alle Mandanten mit diesem Befehl zurückgeben:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceDeploymentMode</em></p></td>
<td><p>Optional</p></td>
<td><p>VoiceDeploymentMode</p></td>
<td><p>Zulässige Werte:</p>
<p>* OnPrem</p>
<p>* Online</p>
<p>* OnlineBasic</p>
<p>* OnPremOnlineHybrid</p>
<p>Der Standardwert ist &quot;OnPrem&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Mit diesem Cmdlet wird eine Instanz des Objekts "Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy" erstellt.

## Siehe auch

#### Weitere Ressourcen

[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

