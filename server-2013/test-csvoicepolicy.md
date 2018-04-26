---
title: Test-CsVoicePolicy
TOCTitle: Test-CsVoicePolicy
ms:assetid: 4d631e36-3a9d-4ca2-913f-8c9f4e93183d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398310(v=OCS.15)
ms:contentKeyID: 49293951
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoicePolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Testet eine Telefonnummer für eine VoIP-Richtlinie und bestimmt, welche VoIP-Route für die Richtlinie dieser Nummer verwendet werden soll. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsVoicePolicy -TargetNumber <PhoneNumber> -VoicePolicy <VoicePolicy> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird ein VoIP-Richtlinientest für die VoIP-Richtlinie mit der Identität "site:Redmond" ausgeführt. Zunächst wird das Cmdlet **Get-CsVoicePolicy** ausgeführt, um die Richtlinie mit dem Identitätswert "site:Redmond" abzurufen. Das Richtlinienobjekt wird dann an das Cmdlet **Test-CsVoicePolicy** weitergeleitet, das die Richtlinie für die Telefonnummer +14255559999 testet. Die Ausgabe ist die erste VoIP-Route (basierend auf der Eigenschaft "Priority" der Route), die ein Nummernmuster aufweist, das dem Wert von "TargetNumber" entspricht, und eine Telefonverwendung hat, die einer Telefonverwendung in der Richtlinie entspricht. Wenn keine übereinstimmende Route gefunden wird (z. B., wenn das Nummernmuster einer elfstelligen Nummer entspricht und Sie eine siebenstellige Nummer angeben), wird ein NULL-Wert zurückgegeben.

    Get-CsVoicePolicy -Identity site:Redmond | Test-CsVoicePolicy -TargetNumber "+14255559999"

## BEISPIEL 2

Beispiel 2 ist mit Beispiel 1 identisch. Der einzige Unterschied ist, dass die Ergebnisse der Get-Operation nicht direkt an das Cmdlet **Test-CsVoicePolicy** weitergeleitet werden. Stattdessen wird das Objekt zunächst in der Variablen "$a" gespeichert und anschließend zur Verwendung als Wert für den Parameter "VoicePolicy" übergeben, der als Richtlinie verwendet wird, für die der Test ausgeführt wird.

    $a = Get-CsVoicePolicy -Identity site:Redmond
    Test-CsVoicePolicy -TargetNumber "+14255559999" -VoicePolicy $a

## BEISPIEL 3

In diesem Beispiel wird ein VoIP-Richtlinientest für sämtliche VoIP-Richtlinien ausgeführt, die innerhalb der Lync Server-Bereitstellung definiert sind. Zunächst wird das Cmdlet **Get-CsVoicePolicy** ohne Parameter ausgeführt, um alle VoIP-Richtlinien abzurufen. Die zurückgegebene Auflistung von Richtlinien wird anschließend an das Cmdlet **Test-CsVoicePolicy** weitergeleitet, das jede Richtlinie in der Auflistung basierend auf der angegebenen Zieltelefonnummer (+12065559999) und den Telefonverwendungen auf eine übereinstimmende Route überprüft. Die Ausgabe enthält eine Liste übereinstimmender Routen und die übereinstimmenden Telefonverwendungen.

    Get-CsVoicePolicy | Test-CsVoicePolicy -TargetNumber "+12065559999"

## Detaillierte Beschreibung

VoIP-Richtlinien sind an VoIP-Routen über die Verwendung eines Telefonfestnetzes (Public Switched Telephone Network, PSTN) gebunden. Ein Anruf eines Benutzers, dem eine bestimmte VoIP-Richtlinie zugewiesen wurde, kann nur über eine Route übertragen werden, deren PSTN-Verwendung einer Verwendung in der Richtlinie entspricht und deren Nummernmuster der gewählten Nummer entspricht. Rufen Sie das Cmdlet **Test-CsVoicePolicy** auf, um zu bestimmen, welche Route (falls vorhanden) zum Weiterleiten eines Anrufs von einem Benutzer mit einer bestimmten VoIP-Richtlinie verwendet wird und welche Telefonverwendung die Richtlinie an die Route bindet.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Test-CsVoicePolicy** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoicePolicy"}

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
<td><p><em>TargetNumber</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>PhoneNumber</p></td>
<td><p>Die für den Test verwendete Telefonnummer. Diese Nummer muss im E.164-Format vorliegen (z. B. +14255551212).</p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Ein Verweis auf ein VoIP-Richtlinienobjekt, für das der Test ausgeführt wird. VoIP-Richtlinienobjekte können mit dem Cmdlet <strong>Get-CsVoicePolicy</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Bestätigungsaufforderungen oder Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Cmdlets auftreten können.</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>Optional</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Die für den Test verwendeten Routeneinstellungen. Die Routeneinstellungen können über einen Aufruf des Cmdlets <strong>Get-CsRoutingConfiguration</strong> abgerufen werden.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy-Objekt. Akzeptiert eine weitergeleitete Eingabe von VoIP-Richtlinienobjekten.

## Rückgabetypen

Gibt ein Objekt vom Typ "Microsoft.Rtc.Management.Voice.VoicePolicyTestResult" zurück.

## Siehe auch

#### Weitere Ressourcen

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)

