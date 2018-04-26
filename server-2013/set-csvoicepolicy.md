---
title: Set-CsVoicePolicy
TOCTitle: Set-CsVoicePolicy
ms:assetid: e6035b74-d760-4c48-aa0b-d09d129e0830
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399021(v=OCS.15)
ms:contentKeyID: 49295723
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicePolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine vorhandene VoIP-Richtlinie. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowCallForwarding <$true | $false>] [-AllowPSTNReRouting <$true | $false>] [-AllowSimulRing <$true | $false>] [-CallForwardingSimulRingUsageType <VoicePolicyUsage | InternalOnly | CustomUsage>] [-Confirm [<SwitchParameter>]] [-CustomCallForwardingSimulRingUsages <PSListModifier>] [-Description <String>] [-EnableBWPolicyOverride <$true | $false>] [-EnableCallPark <$true | $false>] [-EnableCallTransfer <$true | $false>] [-EnableDelegation <$true | $false>] [-EnableMaliciousCallTracing <$true | $false>] [-EnableTeamCall <$true | $false>] [-EnableVoicemailEscapeTimer <$true | $false>] [-Force <SwitchParameter>] [-Name <String>] [-PreventPSTNTollBypass <$true | $false>] [-PstnUsages <PSListModifier>] [-PSTNVoicemailEscapeTimer <Int64>] [-Tenant <Guid>] [-VoiceDeploymentMode <OnPrem | Online | OnlineBasic | OnPremOnlineHybrid>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die Eigenschaft "AllowSimulRing" für die benutzerbasierte Richtlinie "UserVoicePolicy2" auf "False" gesetzt, sodass das gleichzeitige Klingeln für die dieser Richtlinie zugewiesenen Benutzer nicht aktiviert werden kann. Über diese Funktion wird festgelegt, ob beim Klingeln des Bürotelefons eines Benutzers gleichzeitig auch ein zweites Telefon (z. B. ein Mobiltelefon) läuten soll. Über diesen Befehl wird zudem die Verwendung "Local" aus der Liste der Telefonverwendungen für diese Richtlinie entfernt. (Beachten Sie, dass der Parameter "Identity" nicht explizit angegeben wird. Der Parameter "Identity" ist ein Positionsparameter. Wenn Sie den Identitätswert in der Parameterliste zuerst angeben, muss daher nicht explizit angegeben werden, dass es sich um die Identität handelt.)

    Set-CsVoicePolicy UserVoicePolicy2 -AllowSimulRing $false -PstnUsages @{remove="Local"}

## BEISPIEL 2

In diesem Beispiel wird die VoIP-Richtlinie für den Standort "Redmond" so geändert, dass alle für die Organisation definierten PSTN-Verwendungen auf diese Richtlinie angewendet werden. In der ersten Zeile dieses Beispiels wird das Cmdlet **Get-CsPstnUsage** aufgerufen, um den globalen Satz an PSTN-Verwendungen für die Organisation abzurufen und in der Variablen "$a" zu speichern. In der zweiten Zeile wird das Cmdlet **Set-CsVoicePolicy** aufgerufen, um die VoIP-Richtlinie für den Standort "Redmond" zu ändern. Um die aktuelle Liste der Telefonverwendungen für die Richtlinie durch die Liste im globalen Satz mit PSTN-Verwendungen zu ersetzen, wird ein Wert an den Parameter "PstnUsages" übergeben. Beachten Sie die Syntax des ersetzten Werts: $a.Usage. Dies bezieht sich auf die Eigenschaft "Usage" der PSTN-Verwendungseinstellungen, welche die Liste der PSTN-Verwendungen enthält.

    $a = Get-CsPstnUsage
    Set-CsVoicePolicy -Identity site:Redmond -PstnUsages @{replace=$a.Usage}

## Detaillierte Beschreibung

Dieses Cmdlet ändert eine vorhandene VoIP-Richtlinie. VoIP-Richtlinien werden zum Verwalten von Enterprise-VoIP-bezogenen Funktionen verwendet, z. B. für das gleichzeitige Klingeln (die Möglichkeit, ein zweites Telefon läuten zu lassen, wenn jemand die Nummer Ihres Bürotelefons wählt) und die Anrufweiterleitung. Verwenden Sie dieses Cmdlet zum Ändern der Einstellungen, über die eine Vielzahl dieser Funktionen aktiviert oder deaktiviert wird.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsVoicePolicy** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicePolicy"}

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
<td><p><em>AllowCallForwarding</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Wenn dieser Parameter auf &quot;True&quot; festgelegt ist, können Benutzer, die dieser Richtlinie zugeordnet sind, Anrufe weiterleiten. Wird &quot;False&quot; festgelegt, ist keine Anrufweiterleitung möglich.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowPSTNReRouting</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Wenn dieser Parameter auf &quot;True&quot; festgelegt ist, werden Anrufe bei internen Nummern, die sich in einem anderen Pool befinden, über das Telefonfestnetz (Public Switched Telephone Network, PSTN) geleitet, wenn der Pool oder das WAN nicht verfügbar ist.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSimulRing</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gleichzeitiges Klingeln ist eine Funktion, mit der mehrere Telefone läuten können, wenn eine einzige Nummer gewählt wird. Bei Festlegung von &quot;True&quot; wird das gleichzeitige Klingeln aktiviert. Wenn dieser Parameter auf &quot;False&quot; festgelegt wird, kann das gleichzeitige Klingeln für die dieser Richtlinie zugewiesenen Benutzer nicht konfiguriert werden.</p></td>
</tr>
<tr class="even">
<td><p><em>CallForwardingSimulRingUsageType</em></p></td>
<td><p>Optional</p></td>
<td><p>CallForwardingSimulRingUsageType</p></td>
<td><p>Bietet Administratoren eine Möglichkeit zum Verwalten von Anrufweiterleitung und gleichzeitigem Klingeln. Zulässige Werte:</p>
<p>* VoicePolicyUsage – mit der Standardverwendung der VoIP-Richtlinie wird Anrufweiterleitung und gleichzeitiges Klingeln bei allen Anrufen verwaltet. Dies ist der Standardwert.</p>
<p>* InternalOnly – Anrufweiterleitung und gleichzeitiges Klingeln sind auf Anrufe zwischen Lync-Benutzern beschränkt.</p>
<p>* CustomUsage. Mit einer benutzerdefinierten Verwendung von PSTN wird Anrufweiterleitung und gleichzeitiges Klingeln verwaltet. Diese Verwendung muss mit dem Parameter &quot;CustomCallForwardingSimulRingUsages&quot; festgelegt werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomCallForwardingSimulRingUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Benutzerdefinierte Verwendung von PSTN zum Verwalten von Anrufweiterleitung und gleichzeitigem Klingeln. Verwenden Sie eine Syntax wie die folgende, um eine benutzerdefinierte Verwendung hinzuzufügen.</p>
<p>-CustomCallForwardingSimulRingUsages @{Add=&quot;RedmondPstnUsage&quot;}</p>
<p>Verwenden Sie diese Syntax, um eine benutzerdefinierte Verwendung zu entfernen:</p>
<p>-CustomCallForwardingSimulRingUsages @{Remove=&quot;RedmondPstnUsage&quot;}</p>
<p>Beachten Sie, dass die Verwendung vorhanden sein muss, ehe Sie mit dem Parameter &quot;CustomCallForwardingSimulRingUsages&quot; verwendet werden kann.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Eine Beschreibung der VoIP-Richtlinie.</p>
<p>Maximale Länge: 1040 Zeichen.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBWPolicyOverride</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Zum Einschränken der Bandbreite und Festlegen verschiedener anderer Eigenschaften für die Netzwerkkonfiguration können Richtlinien festgelegt werden. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, können diese Richtlinien außer Kraft gesetzt werden. Anders ausgedrückt: Wenn dieser Parameter auf &quot;True&quot; festgelegt ist, finden keine Bandbreitenprüfungen statt, und Anrufe werden unabhängig von den Anrufsteuerungseinstellungen durchgestellt.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCallPark</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Mit der Anwendung zum Parken von Anrufen können Anrufe bei einer bestimmten Nummer innerhalb eines Nummernbereichs geparkt werden, um zu einem späteren Zeitpunkt abgerufen zu werden. Wird dieser Parameter auf &quot;True&quot; festgelegt, wird diese Anwendung für Benutzer aktiviert, denen diese Richtlinie zugewiesen ist. Wenn dieser Parameter auf &quot;False&quot; festgelegt wird, können die dieser Richtlinie zugewiesenen Benutzer keine Anrufe parken, die über ihre Telefonnummer eingehen.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallTransfer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Bestimmt, ob Anrufe an eine andere Nummer weitergeleitet werden können. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, können Anrufe weitergeleitet werden. Bei Festlegung von &quot;False&quot; ist keine Weiterleitung möglich.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDelegation</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Mit der Anrufdelegierung kann ein Benutzer die Anrufe für einen anderen Benutzer entgegennehmen oder Anrufe im Namen des anderen Benutzers tätigen. Ein Vorgesetzter kann die Anrufdelegierung beispielsweise einrichten, damit bei eingehenden Anrufen sowohl das eigene als auch das Telefon eines Administrators läutet. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, können die dieser Richtlinie zugewiesenen Benutzer die Anrufdelegierung einrichten. Bei Festlegung von &quot;False&quot; wird die Anrufdelegierung deaktiviert.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMaliciousCallTracing</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Die Nachverfolgung bei Missbrauch durch Anrufer ist ein Standard, um Anrufe nachzuverfolgen, bei denen ein Benutzer eine Belästigung meldet. Diese Anrufe können auch dann nachverfolgt werden, wenn die Anruferkennung unterdrückt wird. Die Nachverfolgung ist nur durch autorisierte Stellen möglich, nicht durch den Benutzer. Wenn diese Eigenschaft auf &quot;True&quot; festgelegt wird, kann eine Nachverfolgung bei Missbrauch durch Anrufer aktiviert werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTeamCall</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Mit der Funktion für Teamanrufe kann ein Benutzer eine Gruppe von Benutzern bestimmen, deren Telefone beim Eingehen von Anrufen an die eigene Nummer läuten. Diese Funktion ist z. B. für Teams nützlich, in denen ein beliebiges Teammitglied eingehende Anrufe von Kunden annehmen kann. Bei Festlegung von &quot;True&quot; wird diese Funktion aktiviert.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableVoicemailEscapeTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; werden unbeantwortete Anrufe auf mobile Geräte an die Voicemail der Organisation statt die des Anbieters des mobilen Geräts umgeleitet. Wird ein Anruf &quot;zu schnell&quot; (d. h. vor Ablauf des für die Eigenschaft &quot;PSTNVoicemailEscapeTimer&quot; konfigurierten Werts) wird sichergestellt, dass das mobile Gerät nicht verfügbar ist, und der Anruf wird an die Voicemail der Organisation umgeleitet.</p>
<p>Der Standardwert lautet &quot;False&quot;.</p></td>
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
<td><p>XdsIdentity</p></td>
<td><p>Eine eindeutige ID zur Angabe des Gültigkeitsbereichs und in einigen Fällen des Namens der Richtlinie.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen. Dieses Objekt muss vom Typ &quot;VoicePolicy&quot; sein und kann mit dem Cmdlet <strong>Get-CsVoicePolicy</strong> abgerufen werden.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Ein Anzeigename zur Beschreibung dieser Richtlinie.</p></td>
</tr>
<tr class="odd">
<td><p><em>PreventPSTNTollBypass</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Für Anrufe im Telefonfestnetz (Public Switched Telephone Network, PSTN) fallen üblicherweise Gebühren an. Organisationen können diese Gebühren durch die Implementierung einer VoIP-Lösung (Voice over Internet Protocol) umgehen, bei der sich Zweigstellen über Netzwerkanrufe verbinden können. Wenn dieser Parameter auf &quot;True&quot; festgelegt wird, erfolgen Anrufe nicht über das Netzwerk (zur Umgehung der Gebühren), sondern gebührenpflichtig über das Telefonfestnetz.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste der für diese Richtlinie verfügbaren PSTN-Verwendungen. Die PSTN-Verwendung verknüpft eine VoIP-Richtlinie mit einer Telefonroute.</p>
<p>In diese Liste kann ein Zeichenfolgenwert gesetzt werden, sofern dieser Wert in der aktuellen globalen Liste von PSTN-Verwendungen vorhanden ist. (Doppelte Zeichenfolgen sind nicht zulässig, alle Einträge müssen eindeutig sein.) Die Liste der PSTN-Verwendungen kann mit dem Cmdlet <strong>Get-CsPstnUsage</strong> abgerufen werden.</p>
<p>Wenn Sie diesen Parameter zum Entfernen aller PSTN-Verwendungen aus der Richtlinie verwenden, denken Sie daran, dass Benutzer, denen diese Richtlinie zugewiesen wurde, keine ausgehenden PSTN-Anrufe tätigen können.</p></td>
</tr>
<tr class="odd">
<td><p><em>PSTNVoicemailEscapeTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Int64</p></td>
<td><p>Zeitraum (in Millisekunden), in dem bestimmt wird, ob ein Anruf &quot;zu schnell&quot; angenommen wurde. Wenn innerhalb dieses Zeitraums eine Antwort empfangen wird, nimmt Lync Server an, dass das mobile Gerät nicht verfügbar ist, und leitet den Anruf automatisch an die Voicemail der Organisation weiter. Wenn innerhalb des Zeitintervalls keine Antwort empfangen wird, wird der Anruf zugelassen.</p>
<p>Der Standardwert ist 1.500 Millisekunden.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>Guid</p></td>
<td><p>GUID (Globally Unique Identifier) des Skype for Business Online-Mandantenkontos, für das die VoIP-Richtlinie geändert werden soll. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
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

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy-Objekt. Akzeptiert eine weitergeleitete Eingabe von VoIP-Richtlinienobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Voice.VoicePolicy" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)

