---
title: Set-CsNetworkBandwidthPolicyProfile
TOCTitle: Set-CsNetworkBandwidthPolicyProfile
ms:assetid: 519916b9-d5a0-476e-a516-9b8a3058daf2
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398338(v=OCS.15)
ms:contentKeyID: 49293995
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkBandwidthPolicyProfile

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert ein vorhandenes Richtlinienprofil für die Netzwerkbandbreite. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkBandwidthPolicyProfile [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Dieses Beispiel ändert die Beschreibung des Bandbreitenrichtlinienprofils mit dem Identitätswert "LowBWProfile". Hierzu wird das Cmdlet **Set-CsNetworkBandwidthPolicyProfile** mit zwei Parametern aufgerufen: "Identity" zum Angeben des Namens des zu ändernden Profils und "Description" zum Angeben der neuen Profilbeschreibung.

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -Description "Policy for links of less than 10MB"

## BEISPIEL 2

Beispiel 2 ändert den allgemeinen Grenzwert und den Sitzungsgrenzwert für Videoübertragungen des Bandbreitenrichtlinienprofils mit der Identität "LowBWLimit". Nach Angabe des Identitätswerts des zu ändernden Profils wird als Nächstes mithilfe des Parameters "VideoBWLimit" der allgemeine Videogrenzwert auf 2500 festgelegt. Anschließend wird mithilfe des Parameters "VideoBWSessionLimit" der Grenzwert für einzelne Sitzungen auf 300 festgelegt. Dieser Befehl fügt entweder ein Videoprofil hinzu oder aktualisiert ein vorhandenes Videoprofil für das Bandbreitenrichtlinienprofil "LowBWLimit". Vorhandene Audioprofile sind nicht betroffen.

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -VideoBWLimit 2500 -VideoBWSessionLimit 300

## BEISPIEL 3

In diesem Beispiel wird eine neue Bandbreitenrichtlinie erstellt und dem Bandbreitenrichtlinienprofil mit dem Identitätswert "LowBWLimit" zugewiesen. Die erste Zeile in diesem Beispiel enthält einen Aufruf des Cmdlets **New-CsNetworkBWPolicy**. Dieses Cmdlet erstellt ein neues Profil, in diesem Fall ein Videoprofil (-BWPolicyModality video) mit dem Grenzwert 5000 KBit/s (-BWLimit 5000) und dem Sitzungsgrenzwert 200 KBit/s (-BWSessionLimit 200). Dieses neue Profilobjekt wird in der Variablen "$bp" gespeichert. Die nächste Zeile dieses Beispiels ruft das Cmdlet **Set-CsNetworkBandwidthPolicyProfile** zum Ändern des Profils "LowBWLimit" (-Identity LowBWLimit) auf. Der Parameter "BWPolicy" wird mit dem Wert von "$bp" verwendet. Dadurch werden alle vorhandenen Richtlinien dieses Profils durch die neu erstellte, in der Variablen "$bp" gespeicherte Richtlinie ersetzt.

    $bp = New-CsNetworkBWPolicy -BWLimit 5000 -BWSessionLimit 200 -BWPolicyModality video
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bp

## BEISPIEL 4

Beispiel 4 fügt eine neue Bandbreitenrichtlinie für Audio den im Profil "LowBWProfile" vorhandenen Richtlinien hinzu. In der ersten Zeile wird das Cmdlet **Get-CsNetworkBandwidthPolicyProfile** aufgerufen, um das Profil mit dem Identitätswert "LowBWProfile" abzurufen. Dieses Profil wird in der Variablen "$a" gespeichert. In der nächsten Zeile wird das Cmdlet **New-CsNetworkBWPolicy** aufgerufen, um eine neue Bandbreitenrichtlinie zu erstellen. Diese Richtlinie ist eine Audiorichtlinie (-BWPolicyModality audio) mit dem Grenzwert 2000 KBit/s (-BWLimit 2000) und dem Sitzungsgrenzwert 300 KBit/s (-BWSessionLimit 300). Die neue Richtlinie wird in der Variablen "$ap" gespeichert.

In der dritten Zeile wird dem in der ersten Zeile abgerufenen (und in der Variablen "$a" gespeicherten) Profil die neue Audiorichtline hinzugefügt (und in "$ap" gespeichert). Hierzu wird die Methode "Add" der Eigenschaft "BWPolicy" des Profils aufgerufen, um einen Wert für "$ap" zu übergeben. Dieser kann so gelesen werden, dass die neue Richtlinie, die in "$ap" gespeichert ist, der Richtlinie "BWPolicy" des Profils "LowBWProfile" (das in "$a" gespeichert ist) hinzugefügt wird.

Schließlich wird das Cmdlet **Set-CsNetworkBandwidthPolicyProfile** zum Aktualisieren des Profils "LowBWProfile" aufgerufen. Mit dem Parameter "Instance" wird ein Wert von "$a" übergeben, der das geänderte Profil enthält.

    $a = Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile
    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    $a.BWPolicy.Add($ap)
    Set-CsNetworkBandwidthPolicyProfile -Instance $a

## BEISPIEL 5

Beispiel 5 entspricht Beispiel 4 dahingehend, dass der vorhandenen Richtlinienliste für das Profil "LowBWProfile" eine neue Audiorichtlinie hinzugefügt wird. Diese Methode erfordert weniger Befehlszeilen, ist aber ggf. nicht so übersichtlich. Sie wurde hier nur hinzugefügt, um zu veranschaulichen, dass es zum Erledigen derselben Aufgaben mehrere Möglichkeiten gibt.

In Zeile 1 wird eine neue Bandbreitenrichtlinie für Audio erstellt, die ein Bandbreitenlimit (2000) und ein Sitzungslimit (300) festlegt und das neue Objekt in der Variablen "$ap" speichert. Als Nächstes wird das Cmdlet **Set-CsNetworkBandwidthPolicyProfile** aufgerufen, um das Profil mit dem Identitätswert "LowBWProfile" zu ändern. Mithilfe des Parameters "BWPolicy" wird die Liste der Richtlinien im Profil geändert. Beachten Sie den Wert, der an diesen Parameter übergeben wird: @{add=$ap}. Dies ist in Windows PowerShell eine Möglichkeit, ein Element einer Liste hinzuzufügen. Sie beginnen mit dem Zeichen "@", auf das geschweifte Klammern "{}" folgen. In diesen geschweiften Klammern geben Sie die Aktion an, die auf die Liste angewendet werden soll, in diesem Fall eine Hinzufügung zur Liste. (Sie können Elemente auch entfernen oder ersetzen.) Dann folgt die Aktion "(add)" mit einem Gleichheitszeichen, gefolgt vom Objekt, das der Liste hinzugefügt werden soll, in diesem Fall die neue in der Variablen "$ap" gespeicherte Richtlinie.

    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -BWPolicy @{add=$ap}

## Detaillierte Beschreibung

Im Rahmen der Anrufsteuerung wird eine Bandbreitenrichtlinie dazu verwendet, Bandbreiteneinschränkungen für bestimmte Modalitäten zu definieren. (In Lync Server können Bandbreiteneinschränkungen nur für Audio und Video zugewiesen werden.) Dieses Cmdlet ändert ein Containerprofil für diese Richtlinien.

WICHTIG: Wenn ein Profil mehrere Richtlinien enthält (z. B. eine Audio- und eine Videorichtlinie), werden beim Ändern des Profils mithilfe der Eigenschaften "AudioBWLimit", "AudioBWSessionLimit", "VideoBWLimit" oder "VideoBWSessionLimit" alle im Profil vorhandenen Richtlinien entfernt und durch neue Werte ersetzt. Wenn das Profil eine Richtlinie zum Einschränken von Video enthielt und Sie nur den Parameter "AudioBWLimit" festgelegt haben, wird die Videorichtlinie entfernt und eine Audiorichtlinie erstellt.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Set-CsNetworkBandwidthPolicyProfile** lokal auszuführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die maximale Bandbreite, die für alle Audioverbindungen zugewiesen wird. Wenn eine einzelne Audiositzung das Audiobandbreitenlimit überschreitet, kann diese Sitzung nicht gestartet werden.</p>
<p>Ausgedrückt in KBit/s. Der Wert 1000 steht beispielsweise für 1.000 KBit/s.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;AudioBWSessionLimit&quot;, jedoch nicht für &quot;AudioBWLimit&quot; angeben, wird &quot;AudioBWLimit&quot; standardmäßig auf 0 festgelegt.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die maximale Bandbreite, die pro Audiositzung zugewiesen wird. Ausgedrückt in KBit/s. Der Wert muss bei 40 oder höher liegen.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;AudioBWLimit&quot;, jedoch nicht für &quot;AudioBWSessionLimit&quot; angeben, wird &quot;AudioBWSessionLimit&quot; standardmäßig auf 175 festgelegt.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicy</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Eine Liste der Objekte, die Bandbreitenrichtlinienprofile enthalten. Jedes Objekt in der Liste umfasst eine Bandbreitenmodalität (Audio oder Video), eine Bandbreiteneinschränkung sowie eine Bandbreitensitzungseinschränkung.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für die Parameter &quot;AudioBWLimit&quot;, &quot;AudioBWSessionLimit&quot;, &quot;VideoBWLimit&quot; oder &quot;VideoBWSessionLimit&quot; angeben.</p>
<p>Objekte in der Liste müssen vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType&quot; sein. Objekte dieses Typs können durch das Aufrufen des Cmdlets <strong>New-CsNetworkBWPolicy</strong> erstellt werden; die resultierende Richtlinie kann dann dem Profil hinzugefügt werden, indem Sie sie als Parameterwert zuweisen.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Eine Beschreibung des Bandbreitenrichtlinienprofils. Sie können diesen Parameter beispielsweise verwenden, um die erwartete Verwendung des Profils zu erläutern.</p></td>
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
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Der Zeichenfolgenwert zur eindeutigen Kennzeichnung des zu ändernden Bandbreitenrichtlinienprofils. Dieser Wert entspricht der Eigenschaft &quot;BWPolicyProfileID&quot; des Profils und kann durch Ändern des Werts dieser Eigenschaft geändert werden. Dies ist vergleichbar mit einem Kopieren-und-Einfügen-Vorgang: alle Eigenschaften des Profils bleiben unverändert, nur der Name ändert sich. Dieser Wert kann jedoch nicht geändert werden, wenn das Profil einem Netzwerkstandort zugewiesen ist.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>BWPolicyProfileType</p></td>
<td><p>Ein Verweis auf ein Objekt eines Bandbreitenrichtlinienprofils (ein Objekt vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType&quot;) mit den Einstellungen, die Sie zum Ändern des Profils verwenden möchten. Dieses Objekt kann durch Aufrufen des Cmdlets <strong>Get-CsNetworkBandwidthPolicyProfile</strong> abgerufen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die maximale Bandbreite, die für alle Videoverbindungen zugewiesen wird. Wenn eine einzelne Videositzung das Videobandbreitenlimit überschreitet, kann diese Sitzung nicht gestartet werden.</p>
<p>Ausgedrückt in KBit/s. Der Wert 1000 steht beispielsweise für 1.000 KBit/s.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;VideoBWSessionLimit&quot;, jedoch nicht für &quot;VideoBWLimit&quot; angeben, wird &quot;VideoBWLimit&quot; standardmäßig auf 0 festgelegt.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die maximale Bandbreite, die pro Videositzung zugewiesen wird. Ausgedrückt in KBit/s. Der Wert muss bei 100 oder höher liegen.</p>
<p>Wenn Sie einen Wert für diesen Parameter bereitstellen, können Sie keinen Wert für den Parameter &quot;BWPolicy&quot; angeben.</p>
<p>Standard: Wenn Sie einen Wert für den Parameter &quot;VideoBWLimit&quot;, jedoch nicht für &quot;VideoBWSessionLimit&quot; angeben, wird &quot;VideoBWSessionLimit&quot; standardmäßig auf 700 festgelegt.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType-Objekt. Akzeptiert eine weitergeleitete Eingabe von Objekten für ein Netzwerkbandbreiten-Richtlinienprofil.

## Rückgabetypen

Dieses Cmdlet gibt keinen Wert zurück. Es ändert ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType".

## Siehe auch

#### Weitere Ressourcen

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

