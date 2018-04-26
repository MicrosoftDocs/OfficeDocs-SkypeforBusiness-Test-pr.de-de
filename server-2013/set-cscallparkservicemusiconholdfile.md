---
title: Set-CsCallParkServiceMusicOnHoldFile
TOCTitle: Set-CsCallParkServiceMusicOnHoldFile
ms:assetid: af5e7573-4bfd-47b1-a92b-83b06a537158
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412836(v=OCS.15)
ms:contentKeyID: 49295096
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkServiceMusicOnHoldFile

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert die Audiodatei, die für Anrufer mit geparkten Anrufen wiedergegeben wird. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsCallParkServiceMusicOnHoldFile -Content <Byte[]> -Service <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird die Datei "SoothingMusic.wma" als Audiodatei festgelegt, die für Anrufer wiedergegeben wird, deren Anrufe geparkt werden. Die erste Zeile dieses Befehls enthält einen Aufruf des integrierten Cmdlets **Get-Content**. Die Inhalte einer Datei werden eingelesen und in diesem Fall der Variablen "$a" zugewiesen. Der Wert 0 wird dem Parameter "ReadCount" übergeben, sodass mit dem Cmdlet **Get-Content** der Inhalt der gesamten Datei in einem Schritt (und nicht zeilenweise, was bei einer Audiodatei nicht möglich ist) eingelesen wird. Der Parameter "Encoding" wird auf "byte" festgelegt. Auf diese Weise wird das Cmdlet **Get-Content** darüber informiert, dass es sich bei den in die Variable "$a" einzulesenden Inhalten nicht um eine Audiodatei im WMA-Format, sondern um ein Bytearray handelt.

In Zeile 2 des vorliegenden Beispiels erfolgt die eigentliche Zuweisung der Audiodatei. Hierzu wird das Cmdlet **Set-CsCallParkServiceMusicOnHoldFile** aufgerufen und die ID des Diensts angegeben, in dem der Dienst für das Parken von Anrufen ausgeführt wird. Anschließend werden die Inhalte der Audiodatei, die in die Variable "$a" eingelesen wurden, an den Parameter "Content" übergeben. (Denken Sie daran, dass die Inhalte im Byteformat vorliegen müssen.)

    $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
    Set-CsCallParkServiceMusicOnHoldFile -Service ApplicationServer:pool0.litwareinc.com -Content $a

## Detaillierte Beschreibung

Die Funktion zum Parken von Anrufen ist ein Dienst, über den Benutzer eingehende Anrufe "parken" können. Beim Parken eines Anrufs wird der Anruf an eine Nummer in einem angegebenen Bereich übergeben und anschließend sofort in der Warteschleife platziert. Basierend auf den Konfigurationseinstellungen für den Dienst zum Parken von Anrufen kann für den Anrufer eines geparkten Anrufs Wartemusik wiedergegeben werden. Verwenden Sie dieses Cmdlet, um die Audiodatei (Wartemusik) zu ändern, die der Anrufer in Warteschleife hört.

Die Wartemusik wird nur wiedergegeben, wenn die Eigenschaft "EnableMusicOnHold" des Diensts für das Parken von Anrufen auf "True" festgelegt wurde. Sie können diese Eigenschaft überprüfen, indem Sie das Cmdlet **Get-CsCpsConfiguration** aufrufen. Sie können die Eigenschaft entweder festlegen, wenn die Konfiguration der Anwendung zum Parken von Anrufen mit dem Cmdlet **New-CsCpsConfiguration** erstellt wird, oder indem Sie eine bereits vorhandene Konfiguration mit dem Cmdlet **Set-CsCpsConfiguration** aufrufen. Diese Eigenschaft ist standardmäßig auf "True" festgelegt.

Lync Server umfasst eine Standarddatei für Wartemusik, die für Anrufer geparkter Anrufe wiedergegeben werden kann. Wenn Sie keine Audiodatei zuweisen, wird die Standarddatei verwendet.

Audiodateien müssen im folgenden Format vorliegen: Windows Media Audio 9, 44 kHz, 16 Bit, Mono, CBR oder 32 KBit/s.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsCallParkServiceMusicOnHoldFile** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkServiceMusicOnHoldFile"}

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
<td><p><em>Content</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Die Inhalte der Audiodatei im Byteformat.</p>
<p>Verwenden Sie das Cmdlet <strong>Get-Content</strong>, um die Inhalte der Audiodatei im Byteformat abzurufen. (Ausführliche Informationen finden Sie in den Beispielen weiter unten in diesem Thema.)</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Die ID des Diensts, unter dem sich der Dienst für das Parken von Anrufen befindet. Beispiel: ApplicationServer:pool0.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Byte\[\]. Akzeptiert die weitergeleitete Eingabe eines Bytearrays mit der Wartemusikdatei.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)

