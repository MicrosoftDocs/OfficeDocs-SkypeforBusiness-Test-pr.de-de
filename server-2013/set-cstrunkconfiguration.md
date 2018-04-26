---
title: Set-CsTrunkConfiguration
TOCTitle: Set-CsTrunkConfiguration
ms:assetid: 18152388-68de-4a6b-b5a1-248534ecde72
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398238(v=OCS.15)
ms:contentKeyID: 49293308
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrunkConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-02-27_

Ändert eine vorhandene Trunkkonfiguration, mit der die Einstellungen für eine Trunkpeerentität – beispielsweise für ein PSTN-Gateway, für eine IP-Nebenstellenanlage oder für einen SBC (Session Border Controller) – des Dienstanbieters definiert werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTrunkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird eine Trunkkonfiguration mit dem Identitätswert "site:Redmond" geändert, um die Medienumgehung zu aktivieren. Die Medienumgehung wird aktiviert, indem dem Parameter "EnableBypass" der Wert "$True" zugewiesen wird. Die verbleibenden Eigenschaften für diese Konfiguration behalten ihre jeweiligen Werte.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

## BEISPIEL 2

In diesem Beispiel wird eine ausgehende Übersetzungsregel geändert, die für die Trunkkonfiguration mit dem Identitätswert "site:Redmond" definiert wurde. Beachten Sie, dass für diese Änderung das Cmdlet **Set-CsTrunkConfiguration** nicht wirklich aufgerufen wird. Änderungen, die mit dem Cmdlet **Set-CsOutboundTranslationRule** vorgenommen werden, werden automatisch in die Trunkkonfiguration aufgenommen, deren Identitätswert mit dem Bereich des Identitätswerts der ausgehenden Übersetzungsregel übereinstimmt.

    Set-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Translation '$1'

## BEISPIEL 3

In Beispiel 3 wird "SRTPMode" für alle auf Standortebene definierten Trunkkonfigurationen auf den Wert "Optional" festgelegt. Mit dem Befehl wird zunächst das Cmdlet **Get-CsTrunkConfiguration** mit dem Parameter "Filter" aufgerufen, um alle Trunkkonfigurationen abzurufen, deren Identitätswert mit "site:" beginnt, d. h. alle Trunkkonfigurationen, die auf Standortebene definiert sind. Diese Auflistung von Konfigurationen wird dann an das Cmdlet **Set-CsTrunkConfiguration** weitergeleitet, das die Eigenschaft "SRTPMode" der einzelnen Elemente auf "Optional" festlegt.

    Get-CsTrunkConfiguration -Filter site:* | Set-CsTrunkConfiguration -SRTPMode "Optional"

## BEISPIEL 4

In Beispiel 4 wird eine Trunkkonfiguration mit dem Identitätswert "site:Redmond" geändert, um die PIDF-LO-Unterstützung zu aktivieren. Der Standardwert für den Parameter "EnablePIDFLOSupport" lautet "False". In diesem Beispiel wurde der Wert auf "True" festgelegt, um die Standortübertragung für Notrufe zu aktivieren. Sie müssen "EnablePIDFLOSupport" auf "True" festlegen, damit Standortinformationen von der Ausgangsroutinganwendung an den Trunk gesendet werden.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnablePIDFLOSupport $True

## Detaillierte Beschreibung

Verwenden Sie dieses Cmdlet, um eine Trunkkonfiguration für PSTN-Gatewayentitäten zu ändern. Jede Konfiguration umfasst spezifische Einstellungen für eine Trunkpeerentität, wie z. B. ein PSTN-Gateway, eine IP-Nebenstellenanlage oder einen SBC (Session Border Controller) des Dienstanbieters. Diese Einstellungen konfigurieren beispielsweise, ob die Medienumgehung auf diesem Trunk aktiviert ist, ob unter bestimmten Bedingungen RTCP-Pakete (Real-Time Transport Control Protocol) gesendet werden und ob die sichere SRTP-Verschlüsselung (Secure Real-Time Transport Protocol) erforderlich ist.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsTrunkConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrunkConfiguration"}

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
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Der Wert dieses Parameters bestimmt, ob ein bekannter Medienendpunkt vorhanden ist. (Ein Beispiel für einen bekannten Medienendpunkt ist ein PSTN-Gateway, bei dem der Medienendpunkt die gleiche IP-Adresse hat wie der Signaldatenverkehr-Endpunkt.) Legen Sie diesen Wert auf &quot;False&quot; fest, wenn der Trunk nicht über einen bekannten Medienendpunkt verfügt.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Eine Zeichenfolge, mit der der Zweck der Trunkkonfiguration beschrieben wird.</p></td>
</tr>
<tr class="even">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob das 3pcc-Protokoll verwendet werden kann, um zuzulassen, dass weitergeleitete Anrufe den gehosteten Standort umgehen. 3pcc wird auch als Drittsteuerung bezeichnet und wird verwendet, wenn ein Anruferpaar von einem Dritten verbunden wird (beispielsweise von einem Telefonisten, der dafür sorgt, dass ein Gespräch zwischen Person A und Person B zustande kommt). Die REFER-Methode ist eine standardmäßige SIP-Methode, mit der angegeben wird, dass der Empfänger unter Verwendung der Informationen, die er vom Absender erhalten hat, einen Dritten kontaktieren soll. Der Standardwert ist &quot;False&quot; ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBypass</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Der Wert dieses Parameters bestimmt, ob die Medienumgehung für diesen Trunk aktiviert ist. Legen Sie diesen Wert auf &quot;True&quot; fest, um die Umgehung zu aktivieren. Beachten Sie, dass zur ordnungsgemäßen Funktion der Medienumgehung bestimmte Funktionen von PSTN-Gateways, SBCs (Session Border Controller) und Nebenstellenanlagen unterstützt werden müssen:</p>
<p>- Die Fähigkeit, gegabelte Antworten auf Einladungen zu empfangen.</p>
<p>- Lync Server-Clients und der Medienendpunkt müssen direkt und ohne einen Vermittlungsserver miteinander kommunizieren können.</p>
<p>- Das Gatewaysubnetz muss für den gleichen Standort wie das Subnetz des Clients definiert sein; ist dies nicht der Fall, dürfen die Standorte nicht durch WAN-Verbindungen mit beschränkter Bandbreite voneinander getrennt sein.</p>
<p>Die Medienumgehung kann nur unter den folgenden Umständen aktiviert werden:</p>
<p>- Der Parameter &quot;ConcentratedTopology&quot; ist auf &quot;True&quot; festgelegt.</p>
<p>- Der Parameter &quot;EnableReferSupport&quot; ist auf &quot;False&quot; festgelegt, und die Werte für &quot;RTCPActiveCalls&quot; und &quot;RTCPCallsOnHold&quot; lauten &quot;False&quot;, oder &quot;EnableReferSupport&quot; ist auf &quot;True&quot; festgelegt.</p>
<p>Beachten Sie Folgendes: Wenn &quot;EnableBypass&quot; auf &quot;True&quot; und &quot;EnableReferSupport&quot; auf &quot;False&quot; festgelegt wird, wird für nachfolgend weitergeleitete Anrufe mit Medienumgehung keine Medienumgehung durchgeführt.</p>
<p>Die Medienumgehung funktioniert nur dann für einen bestimmten Trunk, wenn sie sowohl global als auch für den betreffenden Trunk aktiviert wurde. Verwenden Sie das Cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>, um die Medienumgehung auf globaler Ebene zu aktivieren.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; werden ausgehende Anrufe, die nicht innerhalb von 10 Sekunden vom Gateway beantwortet werden, an den nächsten verfügbaren Trunk weitergeleitet. Sind keine zusätzlichen Trunks vorhanden, wird der Anruf automatisch abgebrochen. In einer Organisation mit langsamen Netzwerken und Gatewayreaktionen kann dies dazu führen, dass Anrufe unnötigerweise abgebrochen werden.</p>
<p>Der Standardwert ist &quot;True&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Bei Festlegung auf &quot;True&quot; wird das standortbasierte VoIP-Routing für Anrufe aktiviert, die über die SIP-Trunks verlaufen, für die die Verwaltung durch die angegebene Auflistung von SIP-Trunkkonfigurationseinstellungen erfolgt. Beim standortbasierten VoIP-Routing wird sowohl der Standort des Anrufers als auch der Standort des Empfängers berücksichtigt, wenn Anrufe weitergeleitet werden. Wenn diese Eigenschaft auf &quot;True&quot; festgelegt ist (der Standardwert ist &quot;False&quot;), sollte auch die Eigenschaft &quot;NetworkSiteId&quot; festgelegt werden.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Definiert, ob der Dienstanbieter ein Mobilfunkbetreiber ist.</p>
<p>Standard: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob die SIP-Trunks Online-VoIP unterstützen. Bei Online-VoIP verfügen die Benutzer über ein lokales Lync Server-Konto, die Voicemail wird jedoch von Skype for Business Online gehostet. Der Standardwert ist &quot;False&quot; ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Definiert, ob Notrufe mit PIDF-LO (Presence Information Data Format Location Object) über das definierte Gateway weitergeleitet werden. Legen Sie diesen Parameter auf &quot;True&quot; fest, wenn Notrufe an einen zertifizierten Anbieter für die Notrufunterstützung weitergeleitet werden sollen. (Der Standort wird mit dem Anruf übertragen.)</p>
<p>Standard: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Definiert, ob dieser Trunk Übergabeanforderungen vom Vermittlungsserver empfangen kann.</p>
<p>Die Medienumgehung kann nur unter den folgenden Umständen aktiviert werden:</p>
<p>- Der Parameter &quot;ConcentratedTopology&quot; ist auf &quot;True&quot; festgelegt.</p>
<p>- Der Parameter &quot;EnableReferSupport&quot; ist auf &quot;False&quot; festgelegt, und die Werte für &quot;RTCPActiveCalls&quot; und &quot;RTCPCallsOnHold&quot; lauten &quot;False&quot;, oder &quot;EnableReferSupport&quot; ist auf &quot;True&quot; festgelegt.</p>
<p>Beachten Sie Folgendes: Wenn &quot;EnableBypass&quot; auf &quot;True&quot; und &quot;EnableReferSupport&quot; auf &quot;False&quot; festgelegt wird, wird für nachfolgend weitergeleitete Anrufe mit Medienumgehung keine Medienumgehung durchgeführt.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob die SIP-Trunks die RTP-Verriegelung unterstützen. Bei der RTP-Verriegelung handelt es sich um eine Technologie, mit der RTP-/RTCP-Verbindungen über ein Gerät zur Netzwerkadressenübersetzung (Network Address Translation, NAT) oder über eine Firewall ermöglicht werden. Der Standardwert ist &quot;False&quot; ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob der Sitzungszeitgeber aktiviert ist. Mithilfe von Sitzungszeitgebern können Sie ermitteln, ob eine bestimmte Sitzung noch immer aktiv ist.</p>
<p>Beachten Sie, dass selbst bei einer Festlegung dieses Parameters auf &quot;False&quot; Sitzungszeitgeber gelten können, wenn für die Remoteverbindung Sitzungszeitgeber aktiviert sind. In einem solchen Fall antwortet der Vermittlungsserver auf Prüfpakete von Sitzungszeitgebern der Remoteentität.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wenn dieser Parameter auf &quot;True&quot; festgelegt ist, verstärken das PSTN-Gateway, die IP-Nebenstellenanlage oder der SBC (Session Border Controller) des Dienstanbieters das Audiosignal im VoIP-Datenstrom, der an den Vermittlungsserver oder an Lync Server-Clients gesendet wird. Ist dieser Wert auf &quot;False&quot; festgelegt, erfolgt die Verstärkung des Audiosignals entweder auf dem Vermittlungsserver (für Anrufe ohne Umgehung) oder in Lync Server-Clients (für Anrufe mit Umgehung).</p>
<p>Standard: False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob Anruflisteninformationen über den Trunk weitergeleitet werden. Der Standardwert ist &quot;False&quot; ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob der PAI-Header (P-Asserted-Identity Header) zusammen mit dem Anruf weitergeleitet wird. Mit dem PAI-Header lässt sich die Identität des Anrufers überprüfen. Der Standardwert ist &quot;False&quot; ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Eine eindeutige ID, die den Gültigkeitsbereich der Trunkkonfiguration enthält. Trunkkonfigurationen können auf globaler oder auf Standortebene bzw. für einen PSTN-Gatewaydienst auf Dienstebene vorhanden sein. Beispiel: &quot;site:Redmond&quot; (für den Standort) oder &quot;PstnGateway:Redmond.litwareinc.com&quot; (für den Dienst).</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>TrunkConfiguration</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen.</p>
<p>Dieser Parameter erfordert ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration&quot;, das mit dem Cmdlet <strong>Get-CsTrunkConfiguration</strong> abgerufen werden kann.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Optional</p></td>
<td><p>UInt32</p></td>
<td><p>Die maximale Anzahl von gegabelten Antworten, die ein PSTN-Gateway, eine IP-Nebenstellenanlage oder ein SBC (Session Border Controller) des Dienstanbieters auf Einladungen empfangen kann, die an den Vermittlungsserver gesendet werden.</p>
<p>Standard: 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die Website-ID des Netzwerkstandorts, der der Auflistung der Trunkkonfigurationseinstellungen zugeordnet ist. Wenn die Eigenschaft &quot;EnableLocationRestriction&quot; auf &quot;True&quot; festgelegt ist, wird das standortbasierte VoIP-Routing über diesen Trunk verwaltet, indem die für den angegebenen Standort konfigurierten Einstellungen verwendet werden. IDs von Netzwerkstandorten können mit dem folgenden Befehl abgerufen werden:</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Auflistung ausgehender Rufnummernübersetzungsregeln, die dem Trunk zugewiesen sind. Mit dem folgenden Befehl können Sie Informationen zu den verfügbaren Regeln abrufen:</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Auflistung von Regeln für die Telefonnummernübersetzung für Anrufe, die per Ausgangsrouting verarbeitet werden (d. h., sie werden an Nebenstellenanlagen oder PSTN-Ziele geleitet).</p>
<p>Diese Liste und diese Regeln können mit diesem Cmdlet direkt geändert werden. Es wird jedoch empfohlen, ausgehende Übersetzungsregeln mit dem Cmdlet <strong>Set-CsOutboundTranslationRule</strong> zu ändern. Mit dem Cmdlet <strong>Set-CsOutboundTranslationRule</strong> wird die Regel geändert, und diese Änderungen werden automatisch in die Trunkkonfiguration aufgenommen. Rufen Sie das Cmdlet <strong>New-CsOutboundTranslationRule</strong> auf, um die Trunkkonfiguration durch Hinzufügen einer neuen ausgehenden Übersetzungsregel zu ändern. Die neue Regel wird der Trunkkonfiguration mit entsprechendem Gültigkeitsbereich hinzugefügt.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Auflistung von PSTN-Verwendungen, die dem Trunk zugewiesen sind. Mit dem folgenden Befehl können Sie Informationen zu den verfügbaren Verwendungen abrufen:</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wenn Sie diesen Parameter auf &quot;True&quot; festlegen, entfernt der Vermittlungsserver vorangestellte Pluszeichen (+) aus den URIs (Unified Resources Identifier), bevor sie an den Dienstanbieter gesendet werden.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Dieser Parameter legt fest, ob für aktive Anrufe RTCP-Pakete vom PSTN-Gateway, von der IP-Nebenstellenanlage oder vom SBC (Session Border Controller) des Dienstanbieters gesendet werden. Ein aktiver Anruf ist in diesem Kontext ein Anruf, bei dem Mediendaten in mindestens eine Richtung übertragen werden dürfen. Wenn &quot;RTCPActiveCalls&quot; auf &quot;True&quot; festgelegt ist, können der Vermittlungsserver oder Lync Server-Client einen Anruf beenden, wenn für mehr als 30 Sekunden keine RTCP-Pakete empfangen werden.</p>
<p>Beachten Sie, dass durch die Deaktivierung der Überprüfung auf empfangene RTCP-Pakete für aktive Anrufe in Lync Server-Elementen eine wichtige Sicherheitsprüfung entfällt, um verworfene Peers zu ermitteln. Eine Deaktivierung sollte nur erfolgen, wenn dies erforderlich ist.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Dieser Parameter legt fest, ob für Anrufe, die in der Warteschleife platziert wurden und für die erwartungsgemäß keine Medienpakete übermittelt werden, weiterhin RTCP-Pakete über den Trunk gesendet werden. Wenn Wartemusik für den Lync Server-Client oder den Trunk aktiviert ist, wird der Anruf als aktiv eingestuft, und diese Eigenschaft wird ignoriert. Verwenden Sie unter diesen Umständen den Parameter &quot;RTCPActiveCalls&quot;.</p>
<p>Beachten Sie, dass durch die Deaktivierung der Überprüfung auf empfangene RTCP-Pakete für aktive Anrufe in Lync Server-Elementen eine wichtige Sicherheitsprüfung entfällt, um verworfene Peers zu ermitteln. Eine Deaktivierung sollte nur erfolgen, wenn dies erforderlich ist.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste der Übersetzungsregeln für SIP-Antwortcodes, die für die von einem PSTN-Gateway, einer IP-Nebenstellenanlage oder einem SBC (Session Border Controller) des Dienstanbieters empfangenen Antwortcodes gelten. Diese Regeln ermöglichen Administratoren das Zuordnen von SIP-Antwortcodes mit Werten zwischen 400 und 699, die über einen Trunk empfangen wurden, zu neuen, geeigneteren Werten für Lync Server.</p>
<p>Sie können diese Liste und zugehörige Regeln direkt mit diesem Cmdlet erstellen. Es wird jedoch empfohlen, die Übersetzungsregeln für SIP-Antwortcodes mit dem Cmdlet <strong>New-CsSipResponseCodeTranslationRule</strong> zu erstellen. Dieses Cmdlet erstellt die Regel und weist sie der Trunkkonfiguration mit dem übereinstimmenden Bereich zu.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Optional</p></td>
<td><p>SRTPMode</p></td>
<td><p>Der Wert dieses Parameters legt den Umfang der Unterstützung für SRTP zum Schutz von Mediendaten fest, die zwischen dem Vermittlungsserver und dem PSTN-Gateway, der IP-Nebenstellenanlage oder dem SBC (Session Border Controller) des Dienstanbieters übertragen werden. Bei der Medienumgehung muss dieser Wert mit der Einstellung &quot;EncryptionLevel&quot; in der Medienkonfiguration kompatibel sein. Die Medienkonfiguration wird mit dem Cmdlet <strong>New-CsMediaConfiguration</strong> und dem Cmdlet <strong>Set-CsMediaConfiguration</strong> festgelegt.</p>
<p>Gültige Werte:</p>
<p>- Required: Die SRTP-Verschlüsselung muss verwendet werden.</p>
<p>- Optional: SRTP wird verwendet, wenn der Dienstanbieter dieses Protokoll unterstützt.</p>
<p>- NotSupported: Die SRTP-Verschlüsselung wird nicht unterstützt und daher auch nicht verwendet.</p>
<p>Hinweis: &quot;SRTPMode&quot; wird nur verwendet, wenn das Gateway für die Verwendung von TLS (Transport Layer Security) konfiguriert ist. Wenn das Gateway mit dem Transportprotokoll TCP (Transmission Control Protocol) konfiguriert ist, wird &quot;SRTPMode&quot; intern auf &quot;NotSupported&quot; festgelegt.</p>
<p>Standard: Required</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration-Objekt. Akzeptiert eine weitergeleitete Eingabe von Trunkkonfigurationsobjekten.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Mit ihm wird ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration" geändert.

## Siehe auch

#### Weitere Ressourcen

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)

