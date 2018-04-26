---
title: New-CsVoiceRegex
TOCTitle: New-CsVoiceRegex
ms:assetid: a1a498b7-8353-40bd-9c02-424c95743ec3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412751(v=OCS.15)
ms:contentKeyID: 49294944
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRegex

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt ein Muster für reguläre Ausdrücke und eine Übersetzung von Telefonnummern in verschiedene Formate. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsVoiceRegex -AtLeastLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    New-CsVoiceRegex -ExactLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird ein neues Muster für reguläre Ausdrücke und eine neue Übersetzung erstellt. Dieser Ausdruck enthält ein Muster, das genau 7 Zeichen (-ExactLength 7) lang sein muss. Die ersten drei Zeichen der übereinstimmenden Nummer (-DigitsToStrip 3) werden entfernt. Der durch diesen regulären Ausdruck erstellte Wert "Pattern" lautet ^\\d{3}(\\d{4})$, wohingegen der Wert "Translation" auf "$1" festgelegt ist. Die Nummer 5551212 stimmt z. B. mit diesem Muster überein, und die Übersetzung würde 1212 lauten: die 7-stellige Nummer ohne die ersten 3 Ziffern.

    $regex = New-CsVoiceRegex -ExactLength 7 -DigitsToStrip 3

## BEISPIEL 2

In diesem Beispiel werden auch ein neues Muster für reguläre Ausdrücke und eine neue Übersetzung erstellt. Es werden jedoch diese Werte verwendet, um eine neue VoIP-Normalisierungsregel zu erstellen. In der ersten Zeile wird das Cmdlet **New-CsVoiceRegEx**aufgerufen, um einen regulären Ausdruck zu erstellen, bei dem die übereinstimmende Zahl mindestens 7 Zeichen (-AtLeastLength 7) lang sein und mit einer 1 (-StartsWith "1") beginnen muss. Das Ergebnis dieses Befehls wird der Variablen "$regex" zugewiesen.

In der zweiten Zeile wird das Cmdlet **New-CsVoiceNormalizationRule** aufgerufen. Die neue Regel erhält einen eindeutigen Namen, in diesem Fall "globale/interne Regel". Als Muster der Normalisierungsregel wird das Muster zugewiesen, das durch Aufrufen des Cmdlets **New-CsVoiceRegex** erstellt wurde: -Pattern $regex.Pattern. Dies wird auch für den Wert "Translation" durchgeführt, indem der Wert "Translation" zugewiesen wird. Dieser Wert wurde durch den Aufruf des Cmdlets **New-CsVoiceRegex** erstellt: -Translation $regex.Translation.

Hinweis: Der in diesem Beispiel erstellte Wert "Pattern" lautet ^(1\\d{5}\\d+)$. Dieser Wert kann als Nummer entziffert werden, die mit 1 (1) beginnt, gefolgt von fünf Ziffern (\\d{5}) und einer beliebigen Anzahl von Ziffern (\\d+). Dies ergibt eine Nummer mit mindestens 7 Ziffern (1 plus 5 plus 1 oder mehr Ziffern), die wie gewünscht mit 1 beginnen.

    $regex = New-CsVoiceRegex -AtLeastLength 7 -StartsWith "1"
    New-CsVoiceNormalizationRule "global/internal rule" -Pattern $regex.Pattern -Translation $regex.Translation

## Detaillierte Beschreibung

Reguläre Ausdrücke werden für die Entsprechung von Zeichenmustern verwendet. In Lync Server werden reguläre Ausdrücke verwendet, um Telefonnummern in verschiedene Formate und aus verschiedenen Formaten zu konvertieren, einschließlich gewählter Nummern, des E.164-Formats sowie der Formate für Nebenstellenanlagen (Private Branch Exchange, PBX) und Telefonfestnetze (Public Switched Telephone Network, PSTN). Das Definieren dieser Konvertierungsregeln kann verwirrend sein, wenn Sie die Syntax- und Formatregeln zum Arbeiten mit regulären Ausdrücken nicht kennen. Das Cmdlet **New-CsVoiceRegex** stellt Parameter bereit, mit denen Sie bestimmte Kriterien festlegen können, und generiert den regulären Ausdruck für Sie.

Verwenden Sie dieses Cmdlet, um reguläre Ausdrücke zu generieren, die für die Werte "Pattern" und "Translation" für Normalisierungsregeln (Cmdlet **New-CsVoiceNormalizationRule**) und ausgehende Übersetzungsregeln (Cmdlet **New-CsOutboundTranslationRule**) sowie für den Wert "NumberPattern" für VoIP-Routen (Cmdlet **New-CsVoiceRoute**) verwendet werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsVoiceRegex** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRegex"}

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
<td><p><em>AtLeastLength</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Int32</p></td>
<td><p>Die Mindestlänge, die für die Zeichenfolge (Telefonnummer) erforderlich ist, die mit dem Ausdruck übereinstimmt. Wenn Sie z. B. eine sich nur auf Zahlen auswirkende Normalisierungsregel definieren, die mindestens 7 Ziffern (oder Zeichen) lang sein muss, legen Sie den Wert 7 für diesen Parameter fest.</p>
<p>Sie müssen entweder für diesen Parameter oder für den Parameter &quot;ExactLength&quot; einen Wert eingeben. Sie können nicht für beide Parameter einen Wert eingeben.</p></td>
</tr>
<tr class="even">
<td><p><em>ExactLength</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.Int32</p></td>
<td><p>Die Länge der Zeichenfolge (Telefonnummer), die mit dem regulären Ausdruck übereinstimmen muss. Wenn sich beispielsweise eine Normalisierungsregel nur auf Zahlen mit 10 Ziffern auswirken soll, legen Sie den Wert 10 für diesen Parameter fest.</p>
<p>Sie müssen entweder für diesen Parameter oder für den Parameter &quot;AtLeastLength&quot; einen Wert eingeben. Sie können nicht für beide Parameter einen Wert eingeben.</p></td>
</tr>
<tr class="odd">
<td><p><em>DigitsToPrepend</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Eine Zeichenfolge, mit der die Zeichen oder Zahlen festgelegt werden, die der Telefonnummer vorangestellt werden. Der in diesen Parameter eingegebene Wert wirkt sich auf den Wert &quot;Translation&quot; aus, indem Zeichen der Nummer vorangestellt werden, die mit dem Muster für reguläre Ausdrücke übereinstimmt. Wenn z. B. die mit dem Muster übereinstimmende Nummer 5551212 und der Wert &quot;DigitsToPrepend&quot; 425 lautet, lautet die übersetzte Nummer 4255551212 (vorausgesetzt, es wurden keine weiteren Übersetzungen angewendet).</p></td>
</tr>
<tr class="even">
<td><p><em>DigitsToStrip</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>Die Anzahl der Zeichen, die von der Zeichenfolge (Telefonnummer) entfernt werden. Wenn z. B. die Nummer 2065551212 eingegeben wird und der Wert &quot;DigitsToStrip&quot; 3 lautet, wird die Nummer in 5551212 übersetzt.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartsWith</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Das erste Zeichen der Zeichenfolge (Telefonnummer). Die Zeichenfolge stimmt nicht mit dem regulären Ausdruck überein, es sein denn, sie beginnt mit der Zeichenfolge, die im Parameter &quot;StartsWith&quot; festgelegt wurde. Wenn z. B. der Wert +1 für &quot;StartsWith&quot; festgelegt wurde, stimmen nur die Zahlen diesem Muster überein, die mit +1 beginnen, und nur diese Zahlen werden übersetzt. Beachten Sie, dass die Anzahl von Zeichen in der Zeichenfolge &quot;StartsWith&quot; in der Gesamtanzahl von &quot;ExactLength&quot; und &quot;AtLeastLength&quot; enthalten ist. Wenn Sie z. B. für &quot;ExactLength&quot; den Wert 10 und für die Zeichenfolge &quot;StartWith&quot; den Wert +1 festgelegt haben, ist eine übereinstimmende Telefonnummer 8 Zeichen lang. Dieser Nummer ist +1 vorangestellt, und sie ist insgesamt 10 Zeichen lang.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Erstellt ein Objekt vom Typ "Microsoft.Rtc.Management.Voice.OcsVoiceRegex".

## Siehe auch

#### Weitere Ressourcen

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)

