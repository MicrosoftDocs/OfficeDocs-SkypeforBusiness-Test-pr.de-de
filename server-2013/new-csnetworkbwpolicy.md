---
title: New-CsNetworkBWPolicy
TOCTitle: New-CsNetworkBWPolicy
ms:assetid: bbc91bd1-453c-4ae6-bb77-3b6be9429ed0
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412916(v=OCS.15)
ms:contentKeyID: 49295226
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWPolicy

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt im Arbeitsspeicher eine Bandbreitenrichtlinie, die auf das Bandbreitenrichtlinienprofil angewendet werden kann. Diese Richtlinie gilt in Lync Server entweder für die Audio- oder Videobandbreite. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsNetworkBWPolicy -BWLimit <UInt32> -BWPolicyModality <Audio | Video> -BWSessionLimit <UInt32>

## Beispiele

## BEISPIEL 1

In diesem Beispiel wird eine neue Bandbreitenrichtlinie erstellt und der Variablen "$bwp" zugewiesen. Alle Parameter für das Cmdlet **New-CsNetworkBWPolicy** sind erforderlich. In diesem Beispiel wurde ein Gesamtbandbreitenlimit (BWLimit) von 2000 KBit/s und ein Bandbreitensitzungslimit (BWSessionLimit) von 300 KBit/s festgelegt, und diese Grenzwerte wurden auf Videositzungen (-BWPolicyModality video) angewendet.

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video

## BEISPIEL 2

Beispiel 2 ist eine Erweiterung von Beispiel 1, indem einem Richtlinienprofil eine neue Bandbreitenrichtlinie zugewiesen wird. Der Befehl in Zeile 1 ist mit Beispiel 1 identisch: Es werden Videobandbreiteneinschränkungen erstellt. In Zeile 2 wird dann das Cmdlet **New-CsNetworkBandwidthPolicyProfile** aufgerufen, um diese Richtlinie einem neuen Profil hinzuzufügen. Das neue Profil erhält den Identitätswert "LowBWLimit". Anschließend wird der Parameter "BWPolicy" verwendet, der den Wert "$bwp" erhält. Dieser Wert ist die Variable, die die neue Bandbreitenrichtlinie enthält, die in Zeile 1 erstellt wurde.

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video
    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bwp

## Detaillierte Beschreibung

Mit diesem Cmdlet wird eine neue Bandbreitenrichtlinie erstellt. Eine Bandbreitenrichtlinie wird verwendet, um Bandbreiteneinschränkungen für bestimmte Modalitäten zu definieren. (In Lync Server können Bandbreiteneinschränkungen nur für Audio und Video zugewiesen werden.) Die Bandbreitenrichtlinie wird nur im Arbeitsspeicher erstellt. Die Ausgabe muss daher einer Variablen zugewiesen und dann dem Parameter "BWPolicy" des Cmdlets **New-CsNetworkBandwidthPolicyProfile** oder **Set-CsNetworkBandwidthPolicyProfile** übergeben werden. Bandbreitenrichtlinien werden auf Richtlinienprofile angewendet, die mehrere Richtlinien für ein Profil speichern und Teil der globalen Netzwerkkonfiguration für die Anrufsteuerung sind.

Es wird zudem empfohlen, Audio- und Videorichtlinien auch direkt dem Bandbreitenrichtlinienprofil zuzuweisen, indem das Cmdlet **New-CsNetworkBandwidthPolicyProfile** oder **Set-CsNetworkBandwidthPolicyProfile** aufgerufen wird und Werte für die Parameter "AudioBWLimit", "AudioBWSessionLimit", "VideoBWLimit" und "VideoBWSessionLimit" festgelegt werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsNetworkBWPolicy** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWPolicy"}

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
<td><p><em>BWLimit</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.UInt32</p></td>
<td><p>Die maximale Gesamtbandbreite (KBit/s) für alle gleichzeitigen Sitzungen des im Parameter &quot;BWPolicyModality&quot; festgelegten Typs.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
<td><p>Legt fest, welcher Bandbreitentyp beschränkt wird.</p>
<p>Gültige Werte: Audio, Video</p></td>
</tr>
<tr class="odd">
<td><p><em>BWSessionLimit</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.UInt32</p></td>
<td><p>Die maximale, für eine einzige Sitzung zulässige Bandbreite (KBit/s) des im Parameter &quot;BWPolicyModality&quot; festgelegten Typs.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Erstellt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType".

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

