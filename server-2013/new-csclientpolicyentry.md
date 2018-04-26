---
title: New-CsClientPolicyEntry
TOCTitle: New-CsClientPolicyEntry
ms:assetid: e975d048-4911-4ae6-9446-2a6363726a4a
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399046(v=OCS.15)
ms:contentKeyID: 49295772
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicyEntry

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Fügt Lync Server-Clientrichtlinien neue Optionen hinzu. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsClientPolicyEntry -Name <String> -Value <String>

## Beispiele

## BEISPIEL 1

Die Befehle in Beispiel 1 zeigen, wie der globalen Clientrichtlinie ein neuer Richtlinieneintrag hinzugefügt werden kann. In dem Beispiel wird Lync eine neue Feedbackoption hinzugefügt. Dieses Beispiel dient ausschließlich zu Demonstrationszwecken. Sie sollten nicht erwarten, dass Sie diese Befehle ausführen und Ihrer Version von Lync eine ähnliche Feedbackoption hinzufügen können.

Um den neuen Richtlinieneintrag hinzuzufügen, wird mit dem ersten Befehl im Beispiel mit dem Cmdlet **New-CsClientPolicyEntry** ein Eintrag mit dem Namen "OnlineFeedbackURL" und dem Wert "http://www.litwareinc.com/feedback" erstellt. Das resultierende Richtlinieneintragsobjekt wird in der Variablen "$x" gespeichert.

Im zweiten Befehl wird mit dem Cmdlet **Get-CsClientPolicy** ein Objektverweis ($y) auf die globale Clientrichtlinie erstellt. Nachdem der Objektverweis erstellt wurde, wird der neue Richtlinieneintrag mit der Add-Methode der Eigenschaft "PolicyEntry" hinzugefügt. Falls "PolicyEntry" bereits einen oder mehrere Einträge hat, wird der neue Wert einfach an das Ende dieser Auflistung angehängt.

Anschließend schreibt der letzte Befehl die Änderungen mit dem Cmdlet **Set-CsClientPolicy** in die eigentliche globale Richtlinie. Wenn Sie das Cmdlet **Set-CsClientPolicy** nicht aufrufen, sind die Änderungen nur im Arbeitsspeicher vorhanden und gehen verloren, sobald Sie Windows PowerShell beenden oder die Variable "$x" löschen.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    
    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.Add($x)
    
    Set-CsClientPolicy -Instance $y

## BEISPIEL 2

Beispiel 2 ist eine Variante der Befehle in Beispiel 1. In diesem Fall werden jedoch alle Einträge, die derzeit in der Eigenschaft "PolicyEntry" der globalen Richtlinie vorhanden sind, durch den neuen Richtlinieneintrag ersetzt. Hierzu wird mit dem ersten Befehl im Beispiel ein neuer Richtlinieneintrag erstellt, der in der Variablen "$x" gespeichert wird. Der zweite Befehl legt dann den Wert der Eigenschaft "PolicyEntry" mit dem Cmdlet **Set-CsClientPolicy** auf "$x" fest. Nachdem der Befehl ausgeführt wurde, ist der neue Eintrag der einzige Eintrag in der Eigenschaft "PolicyEntry". Alle Elemente, die sich vor dem Aufrufen des Cmdlets **Set-CsClientPolicy** in dieser Eigenschaft befanden, wurden durch den neuen Eintrag ersetzt.

    $x = New-CsClientPolicyEntry -Name "OnlineFeedbackURL" -Value "http://www.litwareinc.com/feedback"
    Set-CsClientPolicy -Identity global -PolicyEntry $x

## BEISPIEL 3

Beispiel 3 zeigt, wie Sie einen Clientrichtlinieneintrag aus der globalen Richtlinie entfernen können. Hierzu wird mit dem ersten Befehl im Beispiel die globale Clientrichtlinie abgerufen, und diese Informationen werden in der Variablen "$y" gespeichert.

Sobald die globale Richtlinie abgerufen wurde, verwendet der zweite Befehl im Beispiel die RemoveAt()-Methode, um den ersten Richtlinieneintrag in dieser Richtlinie zu löschen. Der zu entfernende Richtlinieneintrag wird durch eine Indexnummer gekennzeichnet: Der erste Richtlinieneintrag weist die Indexnummer 0 auf, der zweite Eintrag hat die Indexnummer 1 usw. Eine Syntax der folgenden Art gibt an, dass der erste Richtlinieneintrag entfernt wird: RemoveAt(0).

Sobald der Richtlinieneintrag aus der arbeitsspeicherinternen Instanz der globalen Richtlinie entfernt wurde, wird das Cmdlet **Set-CsClientPolicy** aufgerufen, um diese Änderungen in die tatsächliche Instanz der globalen Clientrichtlinie zu schreiben.

    $y = Get-CsClientPolicy -Identity global
    $y.PolicyEntry.RemoveAt(0)
    
    Set-CsClientPolicy -Instance $y 

## BEISPIEL 4

Der Befehl in Beispiel 4 entfernt alle Clientrichtlinieneinträge, die für die globale Richtlinie konfiguriert wurden. Hierzu wird der Parameter "PolicyEntry" verwendet, dessen Parameterwert auf Null ($Null) festgelegt wird.

    Set-CsClientPolicy -Identity global -PolicyEntry $Null

## Detaillierte Beschreibung

Clientrichtlinien dienen für Lync Server als primärer Mechanismus zum Verwalten von Clientsoftware wie Lync. Beim Erstellen oder Konfigurieren einer Clientrichtlinie stehen Ihnen zahlreiche Optionen zur Verfügung. Sie können beispielsweise angeben, ob Fotos in Lync verwendet werden sollen, ob Emoticons in Chatnachrichten zulässig sind und ob Lync automatisch Aufzeichnungen von Instant Messaging-Sitzungen speichert. Diese Optionen decken viele der clientbezogenen Einstellungen ab, die von Administratoren verwaltet werden müssen.

Einige der zu verwaltenden Clienteinstellungen können jedoch fehlen. Um die Verwaltung noch flexibler und umfassender zu gestalten, ist in Clientrichtlinien eine Eigenschaft namens "PolicyEntry" enthalten. Diese mehrwertige Eigenschaft ermöglicht es Administratoren, neue Verwaltungsoptionen hinzuzufügen, die in Clientrichtlinien nicht explizit aufgerufen werden. Vor der Veröffentlichung von Lync Server war es Beta-Testern beispielsweise möglich, Lync eine Feedbackoption hinzuzufügen. Diese Option wurde als neuer Richtlinieneintrag hinzugefügt und mit dem Cmdlet **New-CsClientPolicyEntry** erstellt.

Beachten Sie, dass Sie nicht willkürlich neue Richtlinieneinträge erstellen können, um Lync oder andere Clientanwendungen zu verwalten. Stattdessen müssen Sie auf eine offizielle Benachrichtigung von Microsoft hinsichtlich der Namen und Werte warten, die zum Erstellen neuer Clientrichtlinieneinträge verwendet werden können.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsClientPolicyEntry** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientPolicyEntry"}

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
<td><p><em>Name</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Namen für den neuen Richtlinieneintrag. Beispiel: -Name &quot;OnlineFeedbackURL&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Value</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Wert, der dem neuen Richtlinieneintrag zugewiesen werden soll. Beispiel: -Value http://www.litwareinc.com/feedback.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **New-CsClientPolicyEntry** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **New-CsClientPolicyEntry** werden neue Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Policy.Client.PolicyEntryType" erstellt.

## Siehe auch

#### Weitere Ressourcen

[New-CsClientPolicy](new-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

