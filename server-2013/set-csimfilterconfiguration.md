---
title: Set-CsImFilterConfiguration
TOCTitle: Set-CsImFilterConfiguration
ms:assetid: c2b08cc0-8261-4b8b-b2e9-5efa902ceb40
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412960(v=OCS.15)
ms:contentKeyID: 49295314
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsImFilterConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine vorhandene Konfiguration von Instant Messaging-Filtern. Einstellungen für diese Filter sollen verhindern, dass Benutzer Chatnachrichten senden, die (klickbare) Links enthalten. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsImFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in diesem Beispiel deaktiviert den URI-Filter für die Konfiguration von Chatnachrichtenfiltern mit dem Identitätswert "site:Redmond". Hierzu wird beim Aufrufen des Cmdlets **Set-CsImFilterConfiguration** mit dem Wert "$False" der Parameter "Enabled" verwendet.

    Set-CsImFilterConfiguration -Identity site:Redmond -Enabled $False

## BEISPIEL 2

In Beispiel 2 wird ein neues URI-Präfix (urn:) der Liste mit Präfixen hinzugefügt, die gemäß der Konfiguration für Chatnachrichtenfilter für "site:Redmond" nicht zulässig sind. Das Cmdlet **Get-CsImFilterConfiguration** wird zum Hinzufügen eines neuen Präfixes verwendet, um die Konfiguration für "site:Redmond" abzurufen. Das zurückgegebene Objekt, das diese Konfiguration repräsentiert, wird in der Variablen "$x" gespeichert. Nachdem die Einstellungen abgerufen wurden, wird die Add()-Methode in Zeile 2 aufgerufen, um "urn:" dem in der Eigenschaft "Prefixes" gespeicherten Satz von Präfixen hinzuzufügen. Dadurch wird der Wert der Objektreferenz "$x" geändert. Um die tatsächliche Konfiguration selbst zu ändern, ruft Zeile 3 das Cmdlet **Set-CsImFilterConfiguration** auf und übergibt "$x" als einzigen Parameterwert.

    $x = Get-CsImFilterConfiguration -Identity site:Redmond
    $x.Prefixes.Add("urn:")
    Set-CsImFilterConfiguration -Instance $x

## BEISPIEL 3

In Beispiel 3 wird dieselbe Maßnahme wie in Beispiel 2 durchgeführt, jedoch mit einer Zeile. In diesem Befehl wird der Parameter "Prefixes" des Cmdlets **Set-CsImFilterConfiguration** dazu verwendet, um "urn:" der Liste der Präfixe hinzuzufügen. Der Add-Listenmodifizierer wird verwendet, um diesen Wert zur Präfixliste hinzuzufügen.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="urn:"}

## BEISPIEL 4

In diesem Beispiel wird das Präfix "urn:" aus der Liste der Präfixe entfernt, die gemäß der Konfiguration für Chatnachrichtenfilter für "site:Redmond" nicht zulässig sind. Dieses Beispiel entspricht Beispiel 3. Es wird jedoch nicht der Add-Listenmodifizierer zum Hinzufügen des Präfixes zur Liste, sondern der Remove-Modifizierer wird zum Entfernen eines Präfixes aufgerufen.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{remove="urn:"}

## Detaillierte Beschreibung

Beim Senden von Chatnachrichten können Benutzer einen URI (Uniform Resource Identifier) im Nachrichtentext einbetten, um andere Gesprächsteilnehmer an eine bestimmte Website oder -freigabe zu verweisen. Lync Server kann so konfiguriert werden, dass Links mit bestimmten Präfixen blockiert werden oder nicht aktiv sind. (Anders ausgedrückt: Die Teilnehmer können nicht einfach auf den Link klicken, um zur Site zu gelangen, auf die der URI verweist. Sie müssen den Link stattdessen kopieren und manuell in einen Browser einfügen.)

Mit dem Cmdlet **Set-CsImFilterConfiguration** können Sie eine Liste von URI-Präfixen ändern, die gefiltert werden, sowie eine globale oder standortspezifische Filterung aktivieren oder deaktivieren. Mit diesem Cmdlet können Sie auch verschiedene Nachrichten mit Warnmeldungen für Benutzer aktualisieren.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsImFilterConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsImFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>Optional</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>Der Wert dieses Parameters bestimmt die Aktion, die ausgeführt wird, wenn eine Chatnachricht einen Link enthält:</p>
<p>Allow. Den Links wird ein Unterstrich vorangestellt, sodass sie nicht mehr aktiv sind. Darüber hinaus wird am Anfang jeder Chatnachricht mit einem Link eine Benachrichtigung eingefügt, wenn in der Eigenschaft &quot;AllowMessage&quot; eine Nachricht festgelegt wurde.</p>
<p>Block. Die Übermittlung von Nachrichten mit aktiven Links wird blockiert, und Lync Server gibt eine Fehlermeldung an den Sender aus.</p>
<p>Warn. Nachrichten mit aktiven Links werden an die Empfänger zusammen mit einer Warnmeldung übermittelt, die am Anfang dieser Nachrichten eingefügt wird. Diese Warnmeldung kann mithilfe der Eigenschaft &quot;WarnMessage&quot; festgelegt werden. Wenn &quot;Warn&quot; festgelegt und keine Warnmeldung mit &quot;WarnMessage&quot; eingegeben wurde, wird der Chatnachrichtenfilter deaktiviert, selbst wenn die Einstellungen für die Eigenschaft &quot;BlockFileExtension&quot; weiterhin berücksichtigt werden.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowMessage</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Wenn für diesen Parameter ein Wert festgelegt wurde, wird diese Zeichenfolge am Anfang jeder Nachricht mit einem Link eingefügt, wenn der Wert der Eigenschaft &quot;Action&quot; auf &quot;Allow&quot; festgelegt ist. Sie können mit dieser Nachricht Benutzer darüber informieren, dass das Klicken auf unbekannte Links eine potenzielle Gefahr darstellt, oder sie auf die entsprechenden Richtlinien oder Anforderungen Ihrer Organisation hinweisen.</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wenn dieser Parameter auf &quot;True&quot; festgelegt wurde, wird ein Link zu einer Datei blockiert, wobei der Dateipfad eine durch die Eigenschaft &quot;Extensions&quot; festgelegte Erweiterung enthält, die in der Klasse &quot;Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration&quot; definiert wurde. (Der Abruf erfolgt über das Cmdlet <strong>Get-CsFileTransferFilterConfiguration</strong>.) Darüber hinaus wird eine Fehlermeldung an den Sender zurückgegeben. Wenn dieser Parameter auf &quot;False&quot; festgelegt ist, werden Dateipfade und Erweiterung nicht geprüft.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Aktiviert oder deaktiviert diese Funktion. Wenn dieser Parameter auf &quot;True&quot; festgelegt wurde, werden Chatnachrichten nach Links durchsucht, und die Regeln in dieser Konfiguration werden angewendet. Wenn dieser Parameter auf &quot;False&quot; festgelegt wurde, werden Nachrichten nicht auf Links hin überprüft.</p>
<p>Standard: True</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Die eindeutige ID der Konfigurationseinstellungen für Chatnachrichtenfilter, die Sie ändern möchten. Dieser Wert ist entweder global oder lautet &quot;site:&lt;Standortname&gt;, wobei &lt;Standortname&gt; der Standort ist, auf den die Konfiguration angewendet wird, z. B. &quot;site:Redmond&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Der Wert dieses Parameters bestimmt, ob die Filterung für lokale Intranet-URIs durchgeführt wird, die in Chatnachrichten übergeben werden. Wenn dieser Parameter auf &quot;True&quot; festgelegt wurde, werden alle URIs ignoriert, die in der Intranetzone des lokalen Computers definiert wurden. (Der lokale Computer ist der Front-End-Server, auf dem der Chatnachrichtenfilter ausgeführt wird.) Wenn dieser Parameter auf &quot;False&quot; festgelegt ist, wird der angegebene Filter auf alle Links angewendet.</p>
<p>Standard: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>ImFilterConfiguration</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt individuelle Parameterwerte festzulegen. Dieses Cmdlet akzeptiert ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration&quot;, das durch Aufrufen von <strong>Get-CsImFilterConfiguration</strong> abgerufen werden kann.</p></td>
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
<td><p>Dieser Parameter enthält die Warnmeldung, die am Anfang jeder Chatnachricht mit Links eingefügt wird, wenn der Wert der Eigenschaft &quot;Action&quot; auf &quot;Warn&quot; festgelegt wurde. Diese Nachricht enthält in der Regel eine Benachrichtigung, dass das Klicken auf unbekannte Links eine potenzielle Gefahr darstellt, oder einen Hinweis auf die entsprechenden Richtlinien oder Anforderungen Ihrer Organisation.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration-Objekt. Akzeptiert eine weitergeleitete Eingabe von Konfigurationsobjekten für Chatnachrichtenfilter.

## Rückgabetypen

Das Cmdlet **Set-CsImFilterConfiguration** gibt keine Werte oder Objekte zurück. Stattdessen werden mit dem Cmdlet Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration" konfiguriert.

## Siehe auch

#### Weitere Ressourcen

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

