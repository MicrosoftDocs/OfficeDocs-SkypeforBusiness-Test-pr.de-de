---
title: New-CsNetworkBandwidthPolicyProfile
TOCTitle: New-CsNetworkBandwidthPolicyProfile
ms:assetid: 84940891-37a6-45fc-972d-05b95aa71ba9
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398675(v=OCS.15)
ms:contentKeyID: 49294620
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBandwidthPolicyProfile

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt ein neues Bandbreitenrichtlinienprofil. Dieses Cmdlet kann auch zum Festlegen der Bandbreitenrichtlinien innerhalb des Profils verwendet werden. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

In Beispiel 1 wird ein neues Bandbreitenrichtlinienprofil namens "LowBWLimits" erstellt. Diesem neuen Profil werden zwei Richtlinien zugewiesen, eine Audio- und eine Videorichtlinie (die einzig möglichen Richtlinientypen in Lync Server). Die Audiorichtlinie wird dem Profil hinzugefügt, indem dem Parameter "AudioBWLimit" ein Limit von (in diesem Fall) 2.000 KBit/s für alle Audioverbindungen und dem Parameter "AudioBWSessionLimit" ein Limit von 200 KBit/s für einzelne Audiositzungen zugewiesen wird. Ebenso werden Limits für Videositzungen erstellt, hierbei unter Verwendung der Parameter "VideoBWLimit" und "VideoBWSessionLimit".

    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimits -AudioBWLimit 2000 -AudioBWSessionLimit 200 -VideoBWLimit 1400 -VideoBWSessionLimit 500

## Detaillierte Beschreibung

Im Rahmen der Anrufsteuerung wird eine Bandbreitenrichtlinie dazu verwendet, Bandbreiteneinschränkungen für bestimmte Modalitäten zu definieren. (In Lync Server können Bandbreiteneinschränkungen nur für Audio und Video zugewiesen werden.) Dieses Cmdlet erstellt ein Containerprofil für diese Richtlinien. Sie definieren die einzelnen Richtlinien innerhalb des Containers, indem Sie beim Aufruf dieses Cmdlets die Beschränkungen für die Audio- und Videobandbreite angeben.

Bandbreitenrichtlinienprofile werden durch das Aufrufen der Cmdlets **New-CsNetworkSite** oder **Set-CsNetworkSite** auf Netzwerkstandorte angewendet.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **New-CsNetworkBandwidthPolicyProfile** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Ein Zeichenfolgenwert, der die Richtlinie eindeutig identifiziert. Alle Bandbreitenrichtlinienprofile werden auf globaler Ebene erstellt. Der Gültigkeitsbereich ist daher impliziert, und es muss beim Erstellen eines neuen Bandbreitenrichtlinienprofils nur ein eindeutiger Name angegeben werden. Beachten Sie, dass mit diesem Wert auch die Eigenschaft &quot;BWPolicyProfileID&quot; des Profils aufgefüllt wird.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Die maximale Bandbreite, die für alle Audioverbindungen zugewiesen wird. Wenn eine einzelne Audiositzung das Audiobandbreitenlimit überschreitet, kann diese Sitzung nicht gestartet werden.</p>
<p>Ausgedrückt in KBit/s. Der Wert 1000 steht beispielsweise für 1.000 KBit/s.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;AudioBWSessionLimit&quot;, jedoch nicht für &quot;AudioBWLimit&quot; angeben, wird &quot;AudioBWLimit&quot; standardmäßig auf 0 festgelegt.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Die maximale Bandbreite, die pro Audiositzung zugewiesen wird. Ausgedrückt in KBit/s. Der Wert muss bei 40 oder höher liegen.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;AudioBWLimit&quot;, jedoch nicht für &quot;AudioBWSessionLimit&quot; angeben, wird &quot;AudioBWSessionLimit&quot; standardmäßig auf 175 festgelegt.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Eine Liste der Objekte, die Bandbreitenrichtlinienprofile enthalten. Jedes Objekt in der Liste umfasst eine Bandbreitenmodalität (Audio oder Video), eine Bandbreiteneinschränkung sowie eine Bandbreitensitzungseinschränkung.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für die Parameter &quot;AudioBWLimit&quot;, &quot;AudioBWSessionLimit&quot;, &quot;VideoBWLimit&quot; oder &quot;VideoBWSessionLimit&quot; angeben.</p>
<p>Objekte in der Liste können mit dem Cmdlet <strong>New-CsNetworkBWPolicy</strong> erstellt werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Eine Beschreibung des Bandbreitenrichtlinienprofils. Sie können diesen Parameter beispielsweise verwenden, um die erwartete Verwendung des Profils zu erläutern.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt alle Bestätigungsaufforderungen, die andernfalls vor der Durchführung von Änderungen angezeigt würden.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Erstellt einen Objektverweis ohne einen Commit für das Objekt auszuführen und die Änderungen dadurch dauerhaft zu speichern. Wenn Sie die Ausgabe des mit diesem Parameter aufgerufenen Cmdlet einer Variablen zuweisen, können Sie die Eigenschaften des Objektverweises ändern und anschließend einen Commit für diese Änderungen ausführen, indem Sie das entsprechende Cmdlet vom Typ &quot;Set-&quot; aufrufen.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Die maximale Bandbreite, die für alle Videoverbindungen zugewiesen wird. Wenn eine einzelne Videositzung das Videobandbreitenlimit überschreitet, kann diese Sitzung nicht gestartet werden.</p>
<p>Ausgedrückt in KBit/s. Der Wert 1000 steht beispielsweise für 1.000 KBit/s.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;VideoBWSessionLimit&quot;, jedoch nicht für &quot;VideoBWLimit&quot; angeben, wird &quot;VideoBWLimit&quot; standardmäßig auf 0 festgelegt.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Die maximale Bandbreite, die pro Videositzung zugewiesen wird. Ausgedrückt in KBit/s. Der Wert muss bei 100 oder höher liegen.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;VideoBWLimit&quot;, jedoch nicht für &quot;VideoBWSessionLimit&quot; angeben, wird &quot;VideoBWSessionLimit&quot; standardmäßig auf 700 festgelegt.</p></td>
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

Keine.

## Rückgabetypen

Erstellt ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType".

## Siehe auch

#### Weitere Ressourcen

[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

