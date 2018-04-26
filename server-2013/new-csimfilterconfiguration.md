---
title: New-CsImFilterConfiguration
TOCTitle: New-CsImFilterConfiguration
ms:assetid: 1964cbf9-d7f1-4b4e-99d1-951ac42d82fe
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398244(v=OCS.15)
ms:contentKeyID: 49293319
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsImFilterConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt eine neue Chatnachrichten-Filterkonfiguration. Chatnachrichtenfilter sollen verhindern, dass Benutzer Chatnachrichten senden, die aktive Links enthalten. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsImFilterConfiguration -Identity <XdsIdentity> [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-InMemory <SwitchParameter>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Im ersten Beispiel wird mit dem Cmdlet **New-CsImFilterConfiguration** eine neue Chatnachrichten-Filterkonfiguration mit der Identität "site:Redmond" erstellt. (Da keine zusätzlichen Parameter angegeben wurden, werden diese Einstellungen mit den Standardwerten erstellt.)

    New-CsImFilterConfiguration -Identity site:Redmond

## BEISPIEL 2

In diesem Befehl wird mit dem Cmdlet **New-CsImFilterConfiguration** eine neue Chatnachrichten-Filterkonfiguration mit dem Identitätswert "site:Redmond" erstellt. Da der Parameter "Prefixes" angegeben wurde, enthält die neue Konfiguration alle Standardwerte, darunter auch die zu filternden Standardpräfixe, sowie zwei zusätzliche URI-Präfixe: "rtsp:" und "urn:". Mithilfe des Add-Listenmodifizierers werden diese Präfixe der Standardliste hinzugefügt.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="rtsp:","urn:"}

## BEISPIEL 3

In diesem Befehl wird mit dem Cmdlet **New-CsFileTransferFilterConfiguration** eine neue Chatnachrichten-Filterkonfiguration mit dem Identitätswert "site:Redmond" erstellt. Dieses Beispiel ähnelt Beispiel 2, mit Ausnahme des Replace-Listenmodifizierers, der hier statt des Add-Listenmodifizierers verwendet wurde. Das bedeutet, dass alle Standard-URI-Präfixe durch diese beiden Präfixe ersetzt werden ("rtsp:" und "urn:"). Es werden nur URIs mit den Präfixen "rtsp:" oder "urn:" aus Chatnachrichten für den Standort "Redmond" herausgefiltert.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{replace="rtsp:","urn:"}

## Detaillierte Beschreibung

Beim Senden von Chatnachrichten können Benutzer einen URI (Uniform Resource Identifier) im Nachrichtentext einbetten, um andere Gesprächsteilnehmer an eine bestimmte Website oder Freigabe zu verweisen. Lync Server kann so konfiguriert werden, dass Links mit bestimmten Präfixen blockiert werden oder nicht aktiv sind. (Anders ausgedrückt: Die Teilnehmer können nicht einfach auf den Link klicken, um zu der Site zu gelangen, auf die der URI verweist. Sie müssen den Link stattdessen kopieren und manuell in einen Browser einfügen.)

Mit dem Cmdlet **New-CsImFilterConfiguration** können Sie, neben einer vollständigen Aktivierung oder Deaktivierung der Filterung, eine Liste der zu filternden URI-Präfixe für einen bestimmten Standort definieren. Durch den Aufruf des Cmdlets **New-CsImFilterConfiguration** nur mit einem angegebenen Identitätswert wird eine neue Konfiguration mit diesem Identitätswert erstellt, wobei die Liste mit Präfixen für diesen Standort Standardpräfixe enthält, die gefiltert werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsImFilterConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsImFilterConfiguration"}

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
<td><p>Eine eindeutige ID, mit der der Gültigkeitsbereich der Chatnachrichtenfilterkonfiguration festgelegt wird. Globale Einstellungen sind standardmäßig vorhanden und können nicht mit dem Cmdlet <strong>New-CsImFilterConfiguration</strong> neu erstellt werden. Sie können jedoch Einstellungen auf Standortebene erstellen, indem Sie den Identitätswert &quot;site:&lt;Standortname&gt;&quot; festlegen, wobei &lt;Standortname&lt; für den Namen des Standorts steht, auf den die Einstellungen angewendet werden (z. B. &quot;site:Redmond&quot;).</p>
<p>Vollständiger Datentyp: Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>Optional</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>Der Wert dieses Parameters bestimmt die Aktion, die ausgeführt wird, wenn eine Chatnachricht einen Link enthält:</p>
<p>Allow. Den Links wird ein Unterstrich vorangestellt, sodass sie nicht mehr aktiv sind. Wenn in der Eigenschaft &quot;AllowMessage&quot; eine Nachricht festgelegt wurde, wird diese Nachricht am Anfang jeder Chatnachricht mit einem Link eingefügt.</p>
<p>Block. Die Übermittlung von Nachrichten mit aktiven Links wird blockiert, und Lync Server gibt eine Fehlermeldung an den Absender aus.</p>
<p>Warn. Nachrichten mit aktiven Links werden an die Empfänger zusammen mit einer Warnmeldung übermittelt, die am Anfang dieser Nachrichten eingefügt wird. Diese Warnmeldung kann mithilfe der Eigenschaft &quot;WarnMessage&quot; festgelegt werden. Wenn &quot;Warn&quot; festgelegt und keine Warnmeldung mit &quot;WarnMessage&quot; eingegeben wurde, wird der Chatnachrichtenfilter deaktiviert, selbst wenn die Einstellungen für die Eigenschaft &quot;BlockFileExtension&quot; weiterhin berücksichtigt werden.</p>
<p>Standard: &quot;Allow&quot;, es sei denn eine Nachricht enthält mehr als 1.000 URLs, in diesem Fall lautet die Standardeinstellung &quot;Block&quot;.</p>
<p>Vollständiger Datentyp: Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.UrlFilterAction</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMessage</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Wenn für diesen Parameter ein Wert festgelegt wurde, wird diese Zeichenfolge am Anfang jeder Nachricht mit einem Link eingefügt, wenn der Wert der Eigenschaft &quot;Action&quot; auf &quot;Allow&quot; festgelegt ist. Sie können mit dieser Nachricht Benutzer darüber informieren, dass das Klicken auf unbekannte Links eine potenzielle Gefahr darstellt, oder sie auf die entsprechenden Richtlinien oder Anforderungen Ihrer Organisation hinweisen.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wenn dieser Parameter auf &quot;True&quot; festgelegt wurde, wird ein Link zu einer Datei blockiert, wobei der Dateipfad eine durch die Eigenschaft &quot;Extensions&quot; festgelegte Erweiterung enthält, die in der anwendbaren Filterkonfiguration für Dateiübertragungen definiert wurde (der Abruf erfolgt über das Cmdlet <strong>Get-CsFileTransferFilterConfiguration</strong>). Darüber hinaus wird eine Fehlermeldung an den Absender zurückgegeben. Wenn dieser Parameter auf &quot;False&quot; festgelegt wurde, findet keine zusätzliche Prüfung der Dateierweiterungen statt.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Aktiviert oder deaktiviert diese Funktion. Wenn dieser Parameter auf &quot;True&quot; festgelegt wurde, werden Chatnachrichten nach Links durchsucht, und die Regeln in dieser Konfiguration werden angewendet. Wenn dieser Parameter auf &quot;False&quot; festgelegt wurde, werden Nachrichten nicht auf Links hin überprüft.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Der Wert dieses Parameters bestimmt, ob die Filterung für lokale Intranet-URIs durchgeführt wird, die in Chatnachrichten übergeben werden. Wenn dieser Parameter auf &quot;True&quot; festgelegt wurde, werden alle URIs ignoriert, die in der Intranetzone des lokalen Computers definiert wurden. (Der lokale Computer ist der Front-End-Server, auf dem die Chatnachrichten-Filteranwendung ausgeführt wird.) Wenn dieser Parameter auf &quot;False&quot; festgelegt ist, wird der angegebene Filter auf alle Links angewendet.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Die Liste mit URI-Präfixen, die herausgefiltert werden. Alle Links in einer Chatnachricht mit einem Präfix, das einem der Präfixe in dieser Liste entspricht, werden gemäß den festgelegten Einstellungen gefiltert.</p>
<p>Standard: callto:, file:, ftp., ftp:, gopher:, href, http:, https:, ldap:, mailto:, news:, nntp:, sip:, sips:, tel:, telnet:, www*.</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Dieser Parameter enthält die Warnmeldung, die am Anfang jeder Chatnachricht mit Links eingefügt wird, wenn der Wert der Eigenschaft &quot;Action&quot; auf &quot;Warn&quot; festgelegt wurde. Diese Nachricht weist in der Regel darauf hin, dass das Klicken auf unbekannte Links eine potenzielle Gefahr darstellt, oder verweist auf die entsprechenden Richtlinien oder Anforderungen Ihrer Organisation.</p></td>
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

Erstellt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration".

## Siehe auch

#### Weitere Ressourcen

[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

