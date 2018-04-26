---
title: Test-CsDialPlan
TOCTitle: Test-CsDialPlan
ms:assetid: e6618394-82c5-4bc2-85cc-97ac4686a1aa
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399024(v=OCS.15)
ms:contentKeyID: 49295730
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialPlan

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet einen Wählplan (ehemals als Standortprofil bezeichnet) für eine Telefonnummer und gibt die Normalisierungsregel, die auf diese Nummer angewendet wird, sowie die übersetzte Nummer nach dem Anwenden der Normalisierungsregel zurück. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsDialPlan -DialedNumber <PhoneNumber> -Dialplan <LocationProfile>

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird ein Test für die Wähleinstellungen mit der Identität "site:Redmond" ausgeführt. Zunächst wird das Cmdlet **Get-CsDialPlan** ausgeführt, um die Wähleinstellungen mit der Identität "site:Redmond" abzurufen. Dieses Wähleinstellungsobjekt wird anschließend an das Cmdlet **Test-CsDialPlan** weitergeleitet, das die Wähleinstellungen für die Telefonnummer "14255559999" testet. Die Ausgabe entspricht "DialedNumber", nachdem eine VoIP-Normalisierungsregel mit einem übereinstimmenden Muster angewendet wurde. Wenn innerhalb des Standorts mehrere Normalisierungsregeln ein übereinstimmendes Muster aufweisen, wird die Regel mit dem geringsten Prioritätswert angewendet. Wenn keine Regeln mit einem übereinstimmenden Muster für den Wert "DialedNumber" vorhanden sind (wenn die Normalisierungsregel z. B. mit dem Muster für eine elfstellige Nummer übereinstimmt und Sie eine siebenstellige Nummer angeben), wird kein Wert zurückgegeben.

Die Ausgabe dieses Befehls umfasst eine Telefonnummer und eine Normalisierungsregel. Da die Normalisierungsregel über diverse Eigenschaften verfügt, wird diese Ausgabe standardmäßig mit Auslassungspunkten (...) abgeschnitten. Um alle Eigenschaften und Werte der zurückgegebenen VoIP-Normalisierungsregel anzuzeigen, wird die Ausgabe vor der Anzeige auf dem Bildschirm an das Cmdlet **Format-List** weitergeleitet. Über dieses Cmdlet werden die Telefonnummer und die Normalisierungsregel in separaten Zeilen angezeigt, und auf die Eigenschaften und Werte der Normalisierungsregel wird ein Zeilenumbruch angewendet.

    Get-CsDialPlan -Identity site:Redmond | Test-CsDialPlan -DialedNumber 14255559999 | Format-List

## BEISPIEL 2

Beispiel 2 ist mit Beispiel 1 identisch. Der einzige Unterschied ist, dass die Ergebnisse der Get-Operation nicht direkt an das Cmdlet **Test-CsDialPlan** weitergeleitet werden. Stattdessen wird das Objekt zunächst in der Variablen "$a" gespeichert und anschließend als Wert an den Parameter "DialPlan" übergeben, der als Wählplan verwendet wird, für den der Test ausgeführt wird.

Wie in Beispiel 1 wird die Ausgabe auch in diesem Befehl anschließend an das Cmdlet **Format-List** weitergeleitet, um umfangreichere Informationen zur VoIP-Normalisierungsregel anzuzeigen als in der standardmäßigen Darstellung.

    $a = Get-CsDialPlan -Identity site:Redmond
    Test-CsDialPlan -DialedNumber 14255559999 -Dialplan $a | Format-List

## BEISPIEL 3

In diesem Beispiel wird ein Test für sämtliche Wahlpläne ausgeführt, die innerhalb der Lync Server-Bereitstellung definiert sind. Zunächst wird das Cmdlet **Get-CsDialPlan** ohne Parameter ausgeführt, um alle Wahlpläne abzurufen. Die zurückgegebene Sammlung von Wahlplänen wird anschließend an das Cmdlet **Test-CsDialPlan** weitergeleitet. Dieses Cmdlet testet die einzelnen Wahlpläne für die Telefonnummer "2065559999". Als Ausgabe wird eine Liste mit übersetzten Nummern mit der jeweils angewendeten VoIP-Normalisierungsregel (eine Regel pro Wählplan) angezeigt. Wenn keine VoIP-Normalisierungsregeln innerhalb eines Wählplans für den Wert von "DialedNumber" für einen bestimmten Wählplan gelten (wenn die Normalisierungsregel z. B. mit dem Muster für eine elfstellige Nummer übereinstimmt und Sie eine siebenstellige Nummer angeben), wird in der Liste für diesen Wählplan eine leere Zeile angezeigt.

In der Ausgabe wird die vollständige Anzeige der angewendeten VoIP-Normalisierungsregel standardmäßig abgeschnitten. In Beispiel 1 und 2 wurde die Ausgabe vollständig angezeigt, da die Testergebnisse an das Cmdlet **Format-List** weitergeleitet wurden. In diesem Beispiel wird die Ausgabe an das Cmdlet **Format-Table** mit dem Parameter "Wrap" weitergeleitet. Dadurch wird jeder Eintrag im Tabellenformat angezeigt (eine Spalte für die übersetzte Nummer und eine Spalte für die angewendete VoIP-Normalisierungsregel). Da jedoch ein Zeilenumbruch auf die Ausgabe angewendet wird, wird die Normalisierungsregel innerhalb der Spalte umgebrochen.

    Get-CsDialPlan | Test-CsDialPlan -DialedNumber 2065559999 | Format-Table -Wrap

## Detaillierte Beschreibung

Über dieses Cmdlet können die Ergebnisse beim Anwenden eines Wählplans auf eine bestimmte Telefonnummer angezeigt werden. Wähleinstellungen bieten die erforderlichen Informationen für Enterprise-VoIP-Benutzer, um Anrufe tätigen zu können. Diese Informationen umfassen u. a., wie Normalisierungsregeln angewendet werden. Basierend auf einer gewählten Nummer und einem Wählplan prüft dieses Cmdlet, welche Normalisierungsregel innerhalb der Wähleinstellungen angewendet wird und wie die übersetzte Nummer lautet.

Dieses Cmdlet kann verwendet werden, um Probleme bei der Nummernübersetzung zu behandeln oder die Anwendung von Regeln für bestimmte Nummern zu überprüfen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Test-CsDialPlan** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialPlan"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PhoneNumber</p></td>
<td><p>Die Telefonnummer, für welche die im Parameter &quot;Dialplan&quot; angegebenen Wähleinstellungen getestet werden sollen.</p>
<p>Vollständiger Datentyp: Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>LocationProfile</p></td>
<td><p>Ein Objekt mit einer Referenz zu den Wähleinstellungen, die für die im Parameter &quot;DialedNumber&quot; angegebene Nummer getestet werden sollen.</p>
<p>Vollständiger Datentyp: Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile-Objekt. Akzeptiert eine weitergeleitete Eingabe von Wähleinstellungsobjekten.

## Rückgabetypen

Gibt ein Objekt vom Typ Microsoft.Rtc.Management.Voice.LocationProfileTestResult zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)

