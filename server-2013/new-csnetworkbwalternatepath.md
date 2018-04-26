---
title: New-CsNetworkBWAlternatePath
TOCTitle: New-CsNetworkBWAlternatePath
ms:assetid: 9017378e-4583-42bc-9572-aa8e9571cfe3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398732(v=OCS.15)
ms:contentKeyID: 49294738
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWAlternatePath

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt neue Einstellungen, mit denen für Verbindungen mit Bandbreiteneinschränkungen definiert wird, ob Audio- und Videodaten an alternative Pfade über das Internet geroutet werden können. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsNetworkBWAlternatePath -AlternatePath <$true | $false> -BWPolicyModality <Audio | Video>

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird ein neuer alternativer Pfad bei Vorhandensein von Netzwerkbandbreiteneinschränkungen erstellt, und diese Einstellungen werden einer neu erstellten Region zugewiesen. In der ersten Zeile des Beispiels wird das Cmdlet **New-CsNetworkBWAlternatePath** aufgerufen, um einen neuen alternativen Pfad zu erstellen. Ein alternativer Pfad weist nur zwei Eigenschaften auf: "BWPolicyModality", die entweder auf "Audio" oder "Video" (in diesem Beispiel "Audio") festgelegt werden muss, sowie "AlternatePath", die entweder auf "True" oder "False" (in diesem Beispiel "True") festgelegt werden muss. Die Ausgabe dieses Cmdlets, ein Verweis auf das soeben erstellte Objekt für den alternativen Pfad, wird der Variablen "$a" zugewiesen.

In Zeile 2 dieses Beispiels wird dieser neu erstellte alternative Pfad dazu verwendet, eine neue Netzwerkregion zu erstellen. Hierzu wird das Cmdlet **New-CsNetworkRegion** aufgerufen und "NorthAmerica" als Identitätswert übergeben. Dem erforderlichen Parameter "CentralSite" wird ein Wert zugewiesen (in diesem Beispiel lautet der Name des zentralen Standorts für diese Region "Redmond-NA-MLS"). Anschließend wird die Variable "$a" mit dem soeben erstellten Objekt für den alternativen Pfad an den Parameter "BWAlternatePaths" übergeben.

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $true
    New-CsNetworkRegion -Identity NorthAmerica -CentralSite Redmond-NA-MLS -BWAlternatePaths $a

## Detaillierte Beschreibung

Innerhalb einer Anrufsteuerungskonfiguration in Lync Server gibt es zwei Modalitäten: Audio und Video. Für jede dieser Modalitäten können Bandbreiteneinschränkungen festgelegt werden. Wenn Bandbreiteneinschränkungen das Tätigen eines Anrufs verhindern, kann der Anruf möglicherweise unter Verwendung eines alternativen Pfads über das Internet erfolgen. Mit diesem Cmdlet können Sie Einstellungen festlegen, die definieren, ob ein Anruf basierend auf der Modalität an einen alternativen Pfad über das Internet geroutet werden kann. Die Einstellungen werden pro Region innerhalb der Anrufsteuerungskonfiguration angewendet.

Dieses Cmdlet führt keine sofortige Speicherung der neu erstellten Einstellungen durch. Stattdessen werden die Einstellungen im Arbeitsspeicher erstellt. Um diese Einstellungen auf eine Region innerhalb des Netzwerks anzuwenden, müssen Sie die Ausgabe des Cmdlets einer Variablen zuweisen und anschließend die Variable als Wert für den Parameter "BWAlternatePaths" für das Cmdlet **New-CsNetworkRegion** oder für das Cmdlet **Set-CsNetworkRegion** verwenden. Beachten Sie, dass Sie diese Einstellungen mithilfe der Parameter "AudioAlternatePath" und "VideoAlternatePath" der Cmdlets **New-CsNetworkRegion** und **Set-CsNetworkRegion** auch direkt festlegen können, ohne das Cmdlet **New-CsNetworkBWAlternatePath** zum Erstellen eines neuen Objekts aufrufen zu müssen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsNetworkBWAlternatePath** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWAlternatePath"}

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
<td><p><em>AlternatePath</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Boolean</p></td>
<td><p>Legen Sie den Parameter auf &quot;True&quot; fest, um für Anrufe mit der im Wert des Parameters &quot;BWPolicyModality&quot; (Audio oder Video) festgelegten Modalität eine Weiterleitung an einen alternativen Pfad zuzulassen, wenn im primären Pfad nicht genügend Bandbreite vorhanden ist.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>BWPolicyModality</p></td>
<td><p>Die Modalität, für welche die Einstellung eines alternativen Pfads gilt.</p>
<p>Gültige Werte: audio, video</p>
<p>Vollständiger Datentyp: Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Erstellt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType".

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

