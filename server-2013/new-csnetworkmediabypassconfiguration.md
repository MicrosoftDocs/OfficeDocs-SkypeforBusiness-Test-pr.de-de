---
title: New-CsNetworkMediaBypassConfiguration
TOCTitle: New-CsNetworkMediaBypassConfiguration
ms:assetid: 24055ae5-7fc8-4ca5-9e65-ac3a1f17b405
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg425718(v=OCS.15)
ms:contentKeyID: 49293436
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkMediaBypassConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Erstellt neue globale Einstellungen für die Medienumgehung. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    New-CsNetworkMediaBypassConfiguration [-AlwaysBypass <$true | $false>] [-BypassID <String>] [-Enabled <$true | $false>] [-EnableDefaultBypassID <$true | $false>] [-EnabledForAudioVideoConferences <$true | $false>] [-ExternalBypassMode <Off | ICE | Any>] [-InternalBypassMode <Off | ICE | Any>]

## Beispiele

## BEISPIEL 1

Die Befehle in diesem Beispiel aktivieren die Medienumgehung und konfigurieren sie derart, dass immer eine Umgehung versucht wird. Die erste Zeile in diesem Beispiel besteht aus einem Aufruf des Cmdlets **New-CsNetworkMediaBypassConfiguration**. An dieses Cmdlet werden zwei Parameter übergeben: "AlwaysBypass" und "Enabled", wobei beide auf "True" ($true) festgelegt werden. Wenn Sie "Enabled" auf "True" festlegen, wird die Medienumgehung aktiviert. Durch das Festlegen von "AlwaysBypass" auf "True" wird sichergestellt, dass die Medienumgehung für alle Anrufe versucht wird. (Beachten Sie, dass durch das Festlegen dieser beiden Parameter automatisch ein Wert für die Eigenschaft "BypassID" generiert wird.) Mit dem Cmdlet **New-CsNetworkMediaBypassConfiguration** wird das Objekt nur im Arbeitsspeicher erstellt, woraufhin das Objekt der Variablen "$a" zugewiesen wird.

Die Medienumgehungskonfiguration wird in den Netzwerkkonfigurationseinstellungen gespeichert. Daher werden in Zeile 2 des Beispiels Änderungen an der Medienumgehungskonfiguration in der Netzwerkkonfiguration gespeichert, indem das Cmdlet **Set-CsNetworkConfiguration** aufgerufen wird. Hierbei wird das Konfigurationsobjekt für die Medienumgehung ($a), das in Zeile 1 erstellt wurde, an den Parameter "MediaBypassSettings" übergeben.

    $a = New-CsNetworkMediaBypassConfiguration -AlwaysBypass $true -Enabled $true
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## BEISPIEL 2

In Lync Server gibt es kein Cmdlet **Set-CsNetworkMediaBypassConfiguration**. Wenn Sie daher die vorhandenen Einstellungen ändern möchten, müssen Sie entweder eine neue Konfiguration erstellen (siehe Beispiel 1), die die vorhandene Konfiguration ersetzt, oder Sie müssen die Einstellungen ändern, indem Sie die vorhandenen Einstellungen abrufen, diese ändern und die Änderungen anschließend mit dem Cmdlet **Set-CsNetworkConfiguration** speichern. Dieses Beispiel zeigt, wie Sie die Option zum stetigen Umgehen mithilfe der letzten Option deaktivieren können.

Der Befehl in der ersten Zeile im Beispiel ruft die vorhandenen Medienumgehungseinstellungen ab. Hierzu wird das Cmdlet **Get-CsNetworkConfiguration** aufgerufen. Der Aufruf dieses Cmdlets wird in Klammern angegeben, um sicherzustellen, dass das Cmdlet vollständig ausgeführt wurde, bevor ein anderer Teil des Befehls ausgeführt wird. Mit dem Cmdlet **Get-CsNetworkConfiguration** werden alle Einstellungen für eine gesamte Netzwerkkonfiguration abgerufen. Da nur die Medienumgehungseinstellungen betrachtet werden sollen, wird die Eigenschaft "MediaBypassSettings" angegeben, um nur diese Einstellungen abzurufen. Diese Einstellungen werden der Variablen "$a" zugewiesen.

In Zeile 2 werden die in der Variablen "$a" gespeicherten Einstellungen geändert, indem der Eigenschaft "AlwaysBypass" der Wert "False" ($false) zugewiesen wird. In Zeile 3 wird das Cmdlet **Set-CsNetworkConfiguration** aufgerufen, wobei die Variable "$a" an den Parameter "MediaBypassSettings" übergeben wird, wodurch die an der Eigenschaft "AllowBypass" vorgenommenen Änderungen gespeichert werden.

    $a = (Get-CsNetworkConfiguration).MediaBypassSettings
    $a.AlwaysBypass = $false
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## Detaillierte Beschreibung

Mit diesem Cmdlet werden globale Einstellungen für die Medienumgehung von Audioverbindungen erstellt.

Anders als die meisten Cmdlets vom Typ "New" in Lync Server wird bei diesem Cmdlet die neue Konfiguration nicht unmittelbar gespeichert; vielmehr werden die Einstellungen nur im Arbeitsspeicher erstellt. Das mit diesem Cmdlet erstellte Objekt muss in einer Variablen gespeichert und dann der Eigenschaft "MediaBypassSettings" der Netzwerkkonfiguration zugewiesen werden. (Ausführliche Informationen finden Sie in den Beispielen weiter unten in diesem Thema.)

Die mit diesem Cmdlet erstellten Einstellungen können nur durch Zugriff auf die Eigenschaft "MediaBypassSettings" der globalen Netzwerkkonfiguration abgerufen werden. Führen Sie diesen Befehl aus, um diese Einstellungen abzurufen: (Get-CsNetworkConfiguration).MediaBypassSettings.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **New-CsNetworkMediaBypassConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkMediaBypassConfiguration"}

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
<td><p><em>AlwaysBypass</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Wenn Sie diesen Parameter auf &quot;True&quot; festlegen, werden für alle Anrufe Medienumgehungen versucht.</p>
<p>Legen Sie diesen Wert nur auf &quot;True&quot; fest, wenn die Anrufsteuerung deaktiviert wurde. Dieser Parameter sollte ausschließlich für Bereitstellungen auf &quot;True&quot; festgelegt werden, für die Folgendes gilt:</p>
<p>- Es besteht keine Notwendigkeit zur Bandbreitensteuerung.</p>
<p>- Es ist keine fein abgestimmte Konfiguration erforderlich, mit der die Anforderung einer Medienumgehung erkannt wird.</p>
<p>- Zwischen Gateways und Clients ist vollständige Konnektivität gegeben.</p>
<p>Wenn der Parameter &quot;Enabled&quot; auf &quot;True&quot; gesetzt wird und &quot;AlwaysBypass&quot; auf &quot;False&quot;, nutzt die Umgehungslogik Konfigurationsstandorte und -regionen, um zu ermitteln, wann eine Umgehung möglich ist.</p>
<p>Wenn Sie &quot;AlwaysBypass&quot; auf &quot;True&quot; festlegen, aber für den Parameter &quot;Enable&quot; nicht &quot;True&quot; festlegen, wird eine Warnung ausgegeben: Die Einstellung &quot;AlwaysBypass&quot; wird ignoriert, wenn &quot;Enabled&quot; auf &quot;False&quot; festgelegt wurde.</p>
<p>Wenn Sie &quot;AlwaysBypass&quot; und &quot;Enabled&quot; auf &quot;True&quot; festlegen, wird automatisch eine ID für die Umgehung generiert, die in der Eigenschaft &quot;BypassID&quot; gespeichert wird.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Optional</p></td>
<td><p>Zeichenfolge</p></td>
<td><p>Die ID für die Medienumgehung. Wenn der Parameter &quot;AlwaysBypass&quot; auf &quot;True&quot; festgelegt wird und für diesen Parameter ein Wert angegeben wird, wird diese ID für die Medienumgehung allen Subnetzen zugeordnet. Wenn &quot;AlwaysBypass&quot; auf &quot;False&quot; festgelegt wird, wird der Wert von &quot;BypassID&quot; allen Subnetzen zugeordnet, die nicht in den Standorten und Regionen der Netzwerkkonfiguration gefunden werden.</p>
<p>Diese ID muss im Format einer GUID vorliegen, z. B. 96f14dea-5170-429a-b92b-f1cb909c4bb6. Üblicherweise muss dieser Parameter jedoch weder festgelegt noch geändert werden. Dieser Wert wird automatisch generiert, wenn &quot;Enabled&quot; auf &quot;True&quot; festgelegt wurde und eine der folgenden Bedingungen gilt: 1) &quot;AlwaysBypass&quot; ist auf &quot;True&quot; festgelegt, oder 2) der Parameter &quot;EnableDefaultBypassID&quot; ist auf &quot;True&quot; festgelegt.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Legen Sie diesen Parameter auf &quot;True&quot; fest, um die Medienumgehung zu aktivieren. Umgehungsentscheidungen werden basierend auf dem Wert der Einstellung &quot;AlwaysBypass&quot; folgendermaßen getroffen:</p>
<p>- Wenn &quot;AlwaysBypass&quot; auf &quot;True&quot; festgelegt ist, wird eine Umgehung für alle Anrufe versucht.</p>
<p>- Ist &quot;AlwaysBypass&quot; auf &quot;False&quot; festgelegt, wird anhand der Standorte und Regionen in der Netzwerkkonfiguration ermittelt, ob eine Umgehung möglich ist.</p>
<p>Standard: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDefaultBypassID</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Dieser Wert findet nur Anwendung, wenn &quot;AlwaysBypass&quot; auf &quot;False&quot; festgelegt ist.</p>
<p>Wenn Sie diesen Wert auf &quot;True&quot; festlegen, wird automatisch eine Standard-ID für die Umgehung generiert. Dieser automatisch generierte Wert wird in der Eigenschaft &quot;BypassID&quot; gespeichert.</p>
<p>Dieser Parameter ist nützlich, wenn ein gut verbundener Hauptdienst vorliegt, dessen Remotestandorte Verbindungen mit eingeschränkter Bandbreite aufweisen. Der Administrator muss lediglich anhand von Standorten und Regionen in der Netzwerkkonfiguration die den Remotestandorten zugeordneten Subnetze konfigurieren. Keines der dem Hauptdienst zugeordneten Subnetze muss definiert werden, und zwischen diesen Subnetzen wird automatisch eine Umgehung versucht.</p>
<p>Standard: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnabledForAudioVideoConferences</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolescher Wert</p></td>
<td><p>Gibt an, ob die Medienumgehung für Audio-/Videokonferenzen verwendet werden soll. Der Standardwert ist &quot;False&quot; ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalBypassMode</em></p></td>
<td><p>Optional</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>Für die zukünftige Verwendung reserviert. Eine externe Medienumgehung wird in Lync Server nicht unterstützt.</p>
<p>Standard: Off</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalBypassMode</em></p></td>
<td><p>Optional</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>Der Wert dieses Parameters steuert, wann Clients, die von innerhalb des Organisationsnetzwerks eine Verbindung herstellen, eine Medienumgehung versuchen können. Wenn &quot;Enabled&quot; auf &quot;True&quot; festgelegt ist, wird dieser Wert automatisch in &quot;Any&quot; geändert. Andere Werte für diesen Parameter sind für eine zukünftige Verwendung reserviert.</p>
<p>Standard: Off</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine.

## Rückgabetypen

Erstellt einen Objektverweis vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.MediaBypassSettingsType".

## Siehe auch

#### Weitere Ressourcen

[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)

