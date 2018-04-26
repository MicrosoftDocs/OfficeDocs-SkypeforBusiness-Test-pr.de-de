---
title: Arbeiten mit Parametern
TOCTitle: Arbeiten mit Parametern
ms:assetid: 29ebda0f-ae5f-4512-ad59-240c3605b240
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362778(v=OCS.15)
ms:contentKeyID: 56269259
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Arbeiten mit Parametern

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Bei Verwendung des Parameters **Identity** stellen Sie möglicherweise fest, dass der Parameterwert "kenmyer@litwareinc.com" in Anführungsstriche eingeschlossen ist:

    -Identity "kenmyer@litwareinc.com"

Eine der Fragen, die Personen, die mit Windows PowerShell noch nicht vertraut sind, unweigerlich stellen, ist: Wann muss ich Anführungszeichen verwenden und darf ich keine Anführungszeichen verwenden? Auf diese Frage gibt es zwar keine einfachen Antwort, es gibt jedoch einige allgemeine Regeln, die befolgt werden sollten:

  - Anführungszeichen werden normalerweise nicht benötigt, wenn es sich bei dem Parameterwert um eine Zahl handelt. Wenn Sie beispielsweise die Anzahl der Benutzer einschränken möchten, die von dem Cmdlet [Get-CsOnlineUser](get-csonlineuser.md) zurückgegeben werden, verwenden Sie diese Syntax:
    
        -ResultSize 100
    
    Tatsächlich sollten Sie Zahlen niemals in Anführungszeichen setzen. Andernfalls könnte Windows PowerShell Schwierigkeiten haben, den Wert als Zahl zu interpretieren.
    
    Ebenso sollten Sie sicherstellen, dass Ihre Zahlen keine Kommas enthalten. Wenn Sie den Ergebnisumfang mit dem im Englischen als Tausendertrennzeichen verwendeten Komma auf 10,000 festlegen wollten, wäre die folgende Syntax falsch:
    
        -ResultSize 10,000
    
    Diese Syntax führt zu einer Fehlermeldung, da das Komma in Windows PowerShell verwendet wird, um Argumentwerte zu trennen. In diesem Fall geht Windows PowerShell davon aus, dass Sie zwei unterschiedliche Parameterwerte übergeben: 10 und 000. Da Sie den Ergebnisumfang jedoch nicht auf 10 und auf 0 beschränken können, tritt ein Fehler auf. Verwenden Sie stattdessen diese Syntax ohne Komma:
    
        -ResultSize 10000

  - Anführungszeichen werden normalerweise auch nicht benötigt, wenn es sich bei dem Parameterwert um ein Datum handelt:
    
        -StartDate 6/1/2013
    
    Dies gilt jedoch nur, wenn das Datum ohne Zeitangabe verwendet wird. Wenn Sie eine Zeitangabe einschließen (d. h., wenn Sie ein Leerzeichen zwischen Datum und Uhrzeit einfügen), muss der Parameterwert in Anführungszeichen eingeschlossen werden:
    
        -StartDate "6/1/2013 10:00AM"
    
    Denken Sie daran, dass der vorstehende Befehl für Computer formatiert ist, auf denen die Einstellungen für "Region und Sprache" auf "US English" festgelegt sind. Wenn Sie nicht mit "US English" arbeiten, sollten Sie Datumsangaben und Uhrzeiten gemäß den Einstellungen Ihres Computers formatieren. Um die von Windows PowerShell verwendeten Regions- und Spracheinstellungen zu überprüfen, geben Sie an der Eingabeaufforderung von Windows PowerShell den folgenden Befehl ein:
    
        Get-Host | Select-Object CurrentUICulture

  - Zeichenfolgenwerte (wie die Namen von Personen) setzen normalerweise keine Anführungszeichen voraus. Wichtige Ausnahmen sind Fälle, in denen der Zeichenfolgenwert eingeschränkte Zeichen wie Leerzeichen, Kommas oder andere Satzzeichen enthält. Die folgende Syntax funktioniert beispielsweise, weil die Identität des Benutzers keines der eingeschränkten Zeichen enthält:
    
        -Identity "kenmyer@litwareinc.com"
    
    Dieser Befehl schlägt jedoch fehl, weil die Identität ein Leerzeichen enthält:
    
        -Identity Ken Myer
    
    Der vorstehende Befehl schlägt fehl, da Windows PowerShell Leerzeichen zum Trennen einzelner Parameter verwendet. Dies bedeutet wiederum, dass Windows PowerShell davon ausgeht, dass "Ken" für den Parameter **Identity** steht und "Myer" ein vollkommen neuer Parameter ist. Dementsprechend wird die folgende Fehlermeldung ausgegeben:
    
        Get-CsOnlineUser : Es wurde kein Positionsparameter gefunden, der das Argument 'Myer' akzeptiert.
    
    Wenn Sie einen Parameterwert verwenden möchten, der ein Leerzeichen (oder ein Komma oder ein anderes eingeschränktes Zeichen) enthält, schließen Sie diesen Wert in Anführungszeichen ein:
    
        -Identity "Ken Myer"
    
    In den meisten Fällen können Sie in Windows PowerShell auch Hochkommas anstelle von Anführungszeichen verwenden. So beispielsweise ist auch die nachstehende Syntax in Windows PowerShell gültig:
    
        -Identity 'Ken Myer'
    
    Sie müssen jedoch am Anfang und am Ende der Zeichenfolge die gleiche Art Anführungszeichen verwenden. Die folgende ist keine gültige Windows PowerShell-Syntax:
    
        -Identity "Ken Myer'
    
    Wenn Sie versuchen, diesen Befehl auszuführen, wird in der Windows PowerShell-Konsole Folgendes angezeigt:
    
    ``` 
    >>
    ```
    
    Mit dem Der Doppelpfeil werden Sie aufgefordert, Ihren Befehl abzuschließen: Da Sie mit Anführungszeichen begonnen haben, erwartet Windows PowerShell, dass Sie den Wert auch mit Anführungszeichen abschließen. Wenn Sie die Eingabeaufforderung "\>\>" erhalten, drücken Sie STRG+C, um den Befehl abzubrechen, und versuchen Sie es erneut.

  - Anführungszeichen sollten nicht in Verbindung mit Booleschen Werten (Wahr/Falsch) verwendet werden. Beachten Sie außerdem, dass Sie die Windows PowerShell-Variablen **$True** und **$False** zur Angabe von Wahr/Falsch-Werten verwenden müssen. Ein Beispiel:
    
        -EnterpriseVoiceEnabled $True

Darüber hinaus gibt es auch bestimmte Windows PowerShell-Parameter, die als *Switch-Parameter* bezeichnet werden und keine Parameterwerte akzeptieren:

    -WhatIf

In Verbindung mit Switch-Parametern sind nicht nur keine Parameterwerte erforderlich, deren Angabe führt sogar zu einer Fehlermelden. Einmal angenommen, Sie versuchen, den folgenden Befehl auszuführen:

    -WhatIf $True

Diese Befehl würde mit einer Fehlermeldung ähnlich der folgenden fehlschlagen:

    Set-CsUserAcp : Es wurde kein Positionsparameter gefunden, der das Argument 'True' akzeptiert.

Ihre Fähigkeit zur Verwaltung von Skype for Business Online mithilfe von Windows PowerShell setzt zwingend voraus, dass Sie wissen, welche Cmdlets zur Verfügung stehen, und Sie müssen den *Datentyp* eines jeden Parameters kennen (d. h., ob der Parameter einen Datumswert, einen Zeichenfolgenwert, eine Zahl usw. akzeptiert). Diese Informationen (sowie zahlreiche Beispiele für die Verwendung der Cmdlets) finden Sie in den Hilfethemen zu den Skype for Business Online-Cmdlets. Hier sehen Sie beispielsweise die Parameter, die Sie in Verbindung mit dem Cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) verwenden können:

![Parameter für ein spezielles PowerShell-Cmdlet](images/Dn362778.ead7add1-eec3-4fa4-8bbe-9aa72bb7a1ae(OCS.15).png "Parameter für ein spezielles PowerShell-Cmdlet")

Wie Sie sehen, enthält die Parametertabelle eine Beschreibung des Cmdlets und es wird angegeben, ob der Parameter erforderlich (obligatorisch) oder optional ist. Darüber hinaus wird der Datentyp eines jeden Parameters aufgelistet. Beachten Sie, dass es sich bei dem in der Tabelle aufgeführten Datentyp um den offiziellen, von .NET Framework verwendeten Datentyp handelt. Dies bedeutet, dass der Datentyp als **System.Management.Automation.SwitchParameter** anstatt nur als Switch-Parameter angegeben wird. Hier ein schneller Überblick über die Datentypen, die am häufigsten in Verbindung mit den Skype for Business Online-Cmdlets verwendet werden:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Ein Zeichenfolgenwert, der für die Identität eines Benutzers steht. Hierbei handelt es sich normalerweise um die UPN- oder SIP-Adresse des Benutzers:</p>
<pre><code>-Identity &quot;kenmyer@litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Ein FQDN ist ein vollständig qualifizierter Domänenname. Ein Beispiel:</p>
<pre><code>-Fqdn &quot;atl-lync-001.litwareinc.com&quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Boolean</p></td>
<td><p>Ein Boolescher Wert ist ein Wahr/Falsch-Wert. Denken Sie daran, dass Sie die Windows PowerShell-Variables <strong>$True</strong> und <strong>$False</strong> für die Angabe von Booleschen Werten verwenden müssen:</p>
<pre><code>-Enabled $True -EnterpriseVoiceEnabled $False</code></pre></td>
</tr>
<tr class="even">
<td><p>System.Guid</p></td>
<td><p>GUID ist die Abkürzung für <em>Globally Unique Identifier</em>. Hierbei handelt es sich um einen eindeutigen Bezeichner der in Skype for Business Online jedem Skype for Business Online-Mandanten zugewiesen wird. Ein Beispiel:</p>
<pre><code>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</code></pre>
<p>Mit folgendem Befehl kann der GUID abgerufen werden, der Ihren Skype for Business Online-Mandanten zugewiesen wurde:</p>
<pre><code>Get-CsTenant | Select-Object TenantId</code></pre></td>
</tr>
<tr class="odd">
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Switch-Parameter werden so genannt, weil sie entweder ein- oder ausgeschaltet werden können. Wenn der Parameter vorhanden ist, steht der Schalter sozusagen auf &quot;Ein&quot;, wenn der Parameter nicht vorhanden ist, steht der Schalter auf &quot;Aus&quot;. Wenn Sie beispielsweise den Parameter <strong>Confirm</strong> verwenden möchte, um vor der Ausführung eines Befehls eine Bestätigung anzufordern, schließen Sie den Parameter <strong>Confirm</strong> (ohne einen Parameterwert) in den Befehl ein. Ein Beispiel:</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot; -Confirm</code></pre>
<p>Wenn Sie keine Bestätigung benötigen, schließen Sie den Parameter <strong>Confirm</strong> nicht ein:</p>
<pre><code>Remove-CsUserAcp -Identity &quot;Ken Myer&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>System.String</p></td>
<td><p>Ein Zeichenfolgenwert ist ein alphanumerischer Wert, d. h., er kann (im Allgemeinen) jedes Zeichen enthalten, das über die Tastatur eingegeben werden kann. Ein Beispiel:</p>
<pre><code>-Password &quot;abc123%&amp;*&quot;</code></pre>
<p>Es empfiehlt sich, Zeichenfolgenwerte in Anführungszeichen einzuschließen. Dies ist nicht immer notwendig, jedoch erforderlich, wenn Ihre Zeichenfolgenwert ein Leerzeichen oder ein Komma enthält oder wenn es sich um ein reserviertes Windows PowerShell-Schlüsselwort handelt. (Ein Schlüsselwort ist ein Befehl oder ein anderes Element, das Teil der Windows PowerShell-Programmiersprache als solcher ist. So sind <strong>If</strong> und <strong>End</strong> jeweils Windows PowerShell-Schlüsselwörter. Geben Sie für weitere Informationen den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein:</p>
<p>Get-Help about_Reserved_Words</p></td>
</tr>
</tbody>
</table>


## Siehe auch

#### Konzepte

[Einführung in Windows PowerShell und Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

