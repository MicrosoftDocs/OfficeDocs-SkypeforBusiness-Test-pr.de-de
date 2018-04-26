---
title: New-CsTrunkConfiguration
TOCTitle: New-CsTrunkConfiguration
ms:assetid: f3958f86-3313-4929-9f9d-f796a2669aea
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg413021(v=OCS.15)
ms:contentKeyID: 49295886
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrunkConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt eine neue Trunkkonfiguration, mit der die Einstellungen für eine Trunkpeerentität wie z. B. ein PSTN-Gateway, eine IP-Nebenstellenanlage oder einen SBC (Session Border Controller) des Dienstanbieters definiert werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsTrunkConfiguration -Identity <XdsIdentity> [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-InMemory <SwitchParameter>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird eine neue Trunkkonfiguration mit dem Identitätswert "site:Redmond" erstellt. Die übrigen Eigenschaften für diese neue Konfiguration werden mit Standardwerten aufgefüllt.

    New-CsTrunkConfiguration -Identity site:Redmond

## BEISPIEL 2

In diesem Beispiel wird eine neue Trunkkonfiguration mit dem Identitätswert "site:Redmond" erstellt und die Medienumgehung aktiviert. Die Medienumgehung wird aktiviert, indem dem Parameter "EnableBypass" der Wert "$True" zugewiesen wird. Die übrigen Eigenschaften für diese neue Konfiguration werden mit Standardwerten aufgefüllt.

    New-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## BEISPIEL 3

In diesem Beispiel wird eine neue Trunkkonfiguration mit dem Identitätswert "site:Redmond" erstellt und dem Trunk anschließend eine neue ausgehende Übersetzung zugewiesen. In der ersten Zeile des Beispiels wird das Cmdlet **New-CsTrunkConfiguration** aufgerufen, um die neue Trunkkonfiguration mit Standardeinstellungen zu erstellen. In der zweiten Zeile wird das Cmdlet **New-CsOutboundTranslationRule** aufgerufen. Beachten Sie den zugewiesenen Identitätswert: site:Redmond/OTR1. Der erste Teil des Identitätswerts (site:Redmond) definiert den Geltungsbereich, auf den die Regel angewendet wird. Dieser Geltungsbereich entspricht dem Identitätswert der neuen Trunkkonfiguration, was bedeutet, dass diese Regel automatisch auf diese Konfiguration angewendet wird. Dem Geltungsbereich folgen ein Schrägstrich (/) und eine Zeichenfolge, bei der es sich lediglich um einen eindeutigen Namen für diese Regel handelt. (Pro Geltungsbereich können mehrere Regeln vorliegen.) Anschließend werden Werte an die Parameter "Pattern" und "Translation" übergeben, die diese Regel definieren.

    New-CsTrunkConfiguration -Identity site:Redmond
    New-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Pattern '^\+(\d{8})$' -Translation '9$1'

## Detaillierte Beschreibung

Verwenden Sie dieses Cmdlet, um eine neue Trunkkonfiguration für PSTN-Gatewayentitäten zu erstellen. Jede Konfiguration umfasst spezifische Einstellungen für eine Trunkpeerentität, wie z. B. ein PSTN-Gateway, eine IP-Nebenstellenanlage oder einen SBC (Session Border Controller) des Dienstanbieters. Diese Einstellungen konfigurieren beispielsweise, ob die Medienumgehung auf diesem Trunk aktiviert ist, ob unter bestimmten Bedingungen RTCP-Pakete (Real-Time Transport Control Protocol) gesendet werden und ob die sichere SRTP-Verschlüsselung (Secure Real-Time Transport Protocol) erforderlich ist.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsTrunkConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrunkConfiguration"}

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
<td><p>Eine eindeutige ID, die den Gültigkeitsbereich der Trunkkonfiguration enthält. Trunkkonfigurationen können auf Standortebene bzw. für einen PSTN-Gatewaydienst auf Dienstebene erstellt werden. (Eine globale Konfiguration ist standardmäßig vorhanden und kann nicht entfernt oder neu erstellt werden.) Beispiel: &quot;site:Redmond&quot; (für den Standort) oder &quot;PstnGateway:Redmond.litwareinc.com&quot; (für den Dienst).</p></td>
</tr>
<tr class="even">
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Der Wert dieses Parameters bestimmt, ob ein bekannter Medienendpunkt vorhanden ist. (Ein Beispiel für einen bekannten Medienendpunkt ist ein PSTN-Gateway, bei dem der Medienendpunkt die gleiche IP-Adresse hat wie der Signaldatenverkehr-Endpunkt.) Legen Sie diesen Wert auf &quot;False&quot; fest, wenn der Trunk über keinen bekannten Medienendpunkt verfügt.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Eine Zeichenfolge, mit der der Zweck der Trunkkonfiguration beschrieben wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob das 3PCC-Protokoll verwendet werden kann, um weitergeleitete Anrufe zuzulassen, um die gehostete Website zu umgehen. 3PCC wird auch als &quot;Drittpartei-Anrufsteuerung&quot; bezeichnet und tritt auf, wenn ein Drittanbieters zur Verbindung eines Anruferpaares verwendet wird (z. B. wenn ein Operator einen Anruf von Person A an Person B tätigt). Die REFER-Methode ist eine Standard-SIP-Methode, die angibt, dass der Empfänger mit den vom Absender bereitgestellten Informationen einen Drittanbieter kontaktieren soll. Der Standardwert lautet &quot;False&quot; ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableBypass</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Der Wert dieses Parameters bestimmt, ob die Medienumgehung für diesen Trunk aktiviert ist. Legen Sie diesen Wert auf &quot;True&quot; fest, um die Umgehung zu aktivieren. Beachten Sie, dass zur ordnungsgemäßen Funktion der Medienumgehung bestimmte Funktionen von PSTN-Gateways, SBCs (Session Border Controller) und Nebenstellenanlagen unterstützt werden müssen:</p>
<p>- Die Möglichkeit, gegabelte Antworten auf Einladungen zu empfangen.</p>
<p>- Lync Server-Clients und der Medienendpunkt müssen direkt und ohne einen Vermittlungsserver miteinander kommunizieren können.</p>
<p>- Das Gatewaysubnetz muss für den gleichen Standort wie das Subnetz des Clients definiert sein; ist dies nicht der Fall, dürfen die Standorte nicht durch WAN-Verbindungen mit beschränkter Bandbreite voneinander getrennt sein.</p>
<p>Die Medienumgehung kann nur unter den folgenden Umständen aktiviert werden:</p>
<p>- Der Parameter &quot;ConcentratedTopology&quot; ist auf &quot;True&quot; festgelegt</p>
<p>- Der Parameter &quot;EnableReferSupport&quot; ist auf &quot;False&quot; festgelegt, und die Werte für &quot;RTCPActiveCalls&quot; und &quot;RTCPCallsOnHold&quot; lauten &quot;False&quot;, oder &quot;EnableReferSupport&quot; ist auf &quot;True&quot; festgelegt</p>
<p>Beachten Sie Folgendes: Wenn &quot;EnableBypass&quot; auf &quot;True&quot; und &quot;EnableReferSupport&quot; auf &quot;False&quot; festgelegt wird, wird für nachfolgend weitergeleitete Anrufe mit Medienumgehung keine Medienumgehung durchgeführt.</p>
<p>Die Medienumgehung funktioniert nur dann für einen bestimmten Trunk, wenn sie sowohl global als auch für den betreffenden Trunk aktiviert wurde. Verwenden Sie das Cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>, um die Medienumgehung auf globaler Ebene zu aktivieren.</p>
<p>Standard: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; werden ausgehende Anrufe an den nächsten verfügbaren Trunk weitergeleitet, wenn Sie vom Gateway nicht innerhalb von 10 Sekunden angenommen werden. Wenn keine zusätzlichen Trunks vorhanden sind, wird der Anruf automatisch verworfen. In einer Organisation mit langsamen Netzwerken und Gateway-Antworten führt dies u. U. dazu, dass Anrufe unnötigerweise verworfen werden.</p>
<p>Der Standardwert lautet &quot;True&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Wird als Wert &quot;True&quot; festgelegt, wird das standortbasierte VoIP-Routing für Anrufe aktiviert, die über SIP-Trunks geleitet werden, die von der angegebenen Auflistung der SIP-Trunk-Konfigurationseinstellungen verwaltet werden. Beim standortbasierten VoIP-Routing werden bei der Anrufweiterleitung der Standort des Benutzers, der den Anruf tätigt, und der Standort des Benutzers, der den Anruf entgegennimmt, berücksichtigt. Wird für diese Eigenschaft &quot;True&quot; (Standardwert: False) festgelegt, müssen Sie auch die NetworkSiteId-Eigenschaft angeben.</p>
<p>Dieser Parameter wurde in der Lync Server 2013-Version von Februar 2013 eingeführt.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Definiert, ob der Dienstanbieter ein Mobilfunkbetreiber ist.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob die SIP-Trunks Online-VoIP unterstützen. Bei Online-VoIP haben Benutzer ein lokales Lync Server-Konto, ihre Voicemail wird jedoch von Office 365 gehostet. Der Standardwert lautet &quot;False&quot; ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Definiert, ob Notrufe mit PIDF-LO (Presence Information Data Format Location Object) über das definierte Gateway weitergeleitet werden. Legen Sie diesen Parameter auf &quot;True&quot; fest, wenn Notrufe an einen zertifizierten Anbieter für die Notrufunterstützung weitergeleitet werden sollen. (Der Standort wird mit dem Anruf übertragen.)</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Definiert, ob dieser Trunk Übergabeanforderungen vom Vermittlungsserver empfangen kann.</p>
<p>Die Medienumgehung kann nur unter den folgenden Umständen aktiviert werden:</p>
<p>- Der Parameter &quot;ConcentratedTopology&quot; ist auf &quot;True&quot; festgelegt</p>
<p>- Der Parameter &quot;EnableReferSupport&quot; ist auf &quot;False&quot; festgelegt, und die Werte für &quot;RTCPActiveCalls&quot; und &quot;RTCPCallsOnHold&quot; lauten &quot;False&quot;, oder &quot;EnableReferSupport&quot; ist auf &quot;True&quot; festgelegt</p>
<p>Beachten Sie Folgendes: Wenn &quot;EnableBypass&quot; auf &quot;True&quot; und &quot;EnableReferSupport&quot; auf &quot;False&quot; festgelegt wird, wird für nachfolgend weitergeleitete Anrufe mit Medienumgehung keine Medienumgehung durchgeführt.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob die SIP-Trunks RTP-Verriegelung unterstützen. RTP-Verriegelung ist eine Technologie, die RTP/RTCP-Konnektivität durch ein NAT (Network Address Translator)-Gerät oder eine Firewall ermöglicht. Der Standardwert lautet &quot;False&quot; ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob der Sitzungszeitgeber aktiviert ist. Mithilfe von Sitzungszeitgebern können Sie ermitteln, ob eine bestimmte Sitzung noch immer aktiv ist.</p>
<p>Beachten Sie, dass selbst bei einer Festlegung dieses Parameters auf &quot;False&quot; Sitzungszeitgeber gelten können, wenn für die Remotesitzung Sitzungszeitgeber aktiviert sind. In einem solchen Fall antwortet der Vermittlungsserver auf Prüfpakete von Sitzungszeitgebern der Remoteentität.</p>
<p>Standard: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Wenn dieser Parameter auf &quot;True&quot; festgelegt ist, verstärken das PSTN-Gateway, die IP-Nebenstellenanlage oder der SBC (Session Border Controller) des Dienstanbieters das Audiosignal im VoIP-Datenstrom, der an den Vermittlungsserver oder Lync Server-Clients gesendet wird. Ist dieser Wert auf &quot;False&quot; gesetzt, erfolgt die Verstärkung des Audiosignals entweder beim Vermittlungsserver (für Anrufe ohne Umgehung) oder in Lync Server-Clients (für Anrufe mit Umgehung).</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob Informationen zum Anrufverlauf durch den Trunk weitergeleitet werden. Der Standardwert lautet &quot;False&quot; ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Gibt an, ob der P-Asserted-Identity (PAI)-Header zusammen mit dem Anruf weitergeleitet wird. Der PAI-Header bietet eine Möglichkeit zum Überprüfen der Identität des Anrufers. Der Standardwert lautet &quot;False&quot; ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Optional</p></td>
<td><p>UInt32</p></td>
<td><p>Die maximale Anzahl von gegabelten Antworten, die ein PSTN-Gateway, eine IP-Nebenstellenanlage oder ein SBC (Session Border Controller) des Dienstanbieters auf an den Vermittlungsserver gesendete Einladungen empfangen kann.</p>
<p>Standard: 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Standort-ID des der neuen Auflistung der Trunkkonfigurationseinstellungen zugeordneten Netzwerkstandorts. Wird für die EnableLocationRestriction-Eigenschaft &quot;True&quot; festgelegt, wird das standortbasierte VoIP-Routing über diesen Trunk mithilfe der für den angegebenen Standort konfigurierten Einstellungen verwaltet. Netzwerkstandort-IDs können mit dem folgenden Befehl abgerufen werden:</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p>
<p>Dieser Parameter wurde in der Lync Server 2013-Version von Februar 2013 eingeführt.</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Dem Trunk zugewiesene Auflistung von ausgehenden Übersetzungsregeln für Telefonnummern. Führen Sie diesen Befehl aus, um Informationen zu den verfügbaren Regeln abzurufen:</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung von Regeln für die Telefonnummernübersetzung für Anrufe, die per Ausgangsrouting verarbeitet werden (d. h., sie werden an Nebenstellenanlagen oder PSTN-Ziele geleitet).</p>
<p>Wenngleich diese Liste und die Regeln direkt mit diesem Cmdlet erstellt werden können, sollten die ausgehenden Übersetzungsregeln mit dem Cmdlet <strong>New-CsOutboundTranslationRule</strong> erstellt werden. Dieses Cmdlet erstellt die Regel und weist sie der Trunkkonfiguration mit dem entsprechenden Geltungsbereich zu.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Dem Trunk zugewiesene Auflistung von PSTN-Verwendungen. Verwenden Sie diesen Befehl, um Informationen zu den verfügbaren Verwendungen abzurufen:</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Wenn Sie diesen Parameter auf &quot;True&quot; festlegen, entfernt der Vermittlungsserver vorangestellte Pluszeichen (+) aus den URIs (Unified Resource Identifier), bevor sie an den Dienstanbieter gesendet werden.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Dieser Parameter legt fest, ob für aktive Anrufe RTCP-Pakete vom PSTN-Gateway, der IP-Nebenstellenanlage oder dem SBC (Session Border Controller) des Dienstanbieters gesendet werden. Ein aktiver Anruf ist in diesem Kontext ein Anruf, bei dem Mediendaten in mindestens eine Richtung übertragen werden dürfen. Wenn &quot;RTCPActiveCalls&quot; auf &quot;True&quot; festgelegt ist, können der Vermittlungsserver oder Lync Server-Client einen Anruf beenden, wenn für mehr als 30 Sekunden keine RTCP-Pakete empfangen werden.</p>
<p>Beachten Sie, dass durch die Deaktivierung der Überprüfung auf empfangene RTCP-Pakete für aktive Anrufe in Lync Server-Elementen eine wichtige Sicherheitsprüfung entfällt, um verworfene Peers zu ermitteln. Eine Deaktivierung sollte nur erfolgen, wenn dies erforderlich ist.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Dieser Parameter legt fest, ob für Anrufe, die in der Warteschleife platziert wurden und für die erwartungsgemäß keine Medienpakete übermittelt werden, weiterhin RTCP-Pakete über den Trunk gesendet werden. Wenn Wartemusik für den Lync Server-Client oder den Trunk aktiviert ist, wird der Anruf als aktiv eingestuft, und diese Eigenschaft wird ignoriert. Verwenden Sie unter diesen Umständen den Parameter &quot;RTCPActiveCalls&quot;.</p>
<p>Beachten Sie, dass durch die Deaktivierung der Überprüfung auf empfangene RTCP-Pakete für aktive Anrufe in Lync Server-Elementen eine wichtige Sicherheitsprüfung entfällt, um verworfene Peers zu ermitteln. Eine Deaktivierung sollte nur erfolgen, wenn dies erforderlich ist.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste der Übersetzungsregeln für SIP-Antwortcodes, die den von einem PSTN-Gateway, einer IP-Nebenstellenanlage oder einem SBC (Session Border Controller) des Dienstanbieters empfangenen Antwortcodes entsprechen. Diese Regeln ermöglichen Administratoren das Zuordnen von SIP-Antwortcodes mit Werten zwischen 400 und 699, die über einen Trunk empfangen wurden, zu neuen, geeigneteren Werten für Lync Server.</p>
<p>Sie können diese Liste und zugehörige Regeln direkt mit diesem Cmdlet erstellen. Es wird jedoch empfohlen, die Übersetzungsregeln für SIP-Antwortcodes mit dem Cmdlet <strong>New-CsSipResponseCodeTranslationRule</strong> zu erstellen. Dieses Cmdlet erstellt die Regel und weist sie der Trunkkonfiguration mit dem übereinstimmenden Bereich zu.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Optional</p></td>
<td><p>SRTPMode</p></td>
<td><p>Der Wert dieses Parameters legt die Unterstützungsebene für SRTP zum Schutz von Mediendaten fest, die zwischen dem Vermittlungsserver und dem PSTN-Gateway, der IP-Nebenstellenanlage oder dem SBC (Session Border Controller) des Dienstanbieters übertragen werden. Bei der Medienumgehung muss dieser Wert mit der Einstellung &quot;EncryptionLevel&quot; in der Medienkonfiguration kompatibel sein. Die Medienkonfiguration wird mit den Cmdlets <strong>New-CsMediaConfiguration</strong> und <strong>Set-CsMediaConfiguration</strong> festgelegt.</p>
<p>Gültige Werte:</p>
<p>- Required: Die SRTP-Verschlüsselung muss verwendet werden.</p>
<p>- Optional: SRTP wird verwendet, wenn es vom Gateway unterstützt wird.</p>
<p>- NotSupported: Die SRTP-Verschlüsselung wird nicht unterstützt und daher auch nicht verwendet.</p>
<p>Hinweis: &quot;SRTPMode&quot; wird nur verwendet, wenn das Gateway zur Verwendung von TLS (Transport Layer Security) konfiguriert ist. Wenn das Gateway mit dem Transportprotokoll TCP (Transmission Control Protocol) konfiguriert ist, wird &quot;SRTPMode&quot; intern auf &quot;NotSupported&quot; festgelegt.</p>
<p>Standard: Required</p></td>
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

Keine.

## Rückgabetypen

Erstellt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration".

## Siehe auch

#### Weitere Ressourcen

[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)

