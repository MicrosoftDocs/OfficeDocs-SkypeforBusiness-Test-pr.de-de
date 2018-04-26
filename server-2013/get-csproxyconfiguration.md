---
title: Get-CsProxyConfiguration
TOCTitle: Get-CsProxyConfiguration
ms:assetid: e4836619-026f-4df0-adbd-aa5216e36368
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399011(v=OCS.15)
ms:contentKeyID: 49295702
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsProxyConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den derzeit in Ihrer Organisation verwendeten Konfigurationseinstellungen für Proxyserver zurück. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsProxyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 gibt eine Auflistung aller Proxykonfigurationseinstellungen zurück, die derzeit in der Organisation verwendet werden. Dazu wird das Cmdlet **Get-CsProxyConfiguration** ohne Parameter aufgerufen.

    Get-CsProxyConfiguration

## BEISPIEL 2

In Beispiel 2 werden die Proxykonfigurationseinstellungen mit dem Identitätswert "service:EdgeServer:atl-edge-001.litwareinc.com" zurückgegeben. Da Identitätswerte eindeutig sein müssen, gibt dieser Befehl immer nur eine Auflistung von Einstellungen zurück.

    Get-CsProxyConfiguration -Identity "service:EdgeServer:atl-cs-001.litwareinc.com"

## BEISPIEL 3

In Beispiel 3 werden Informationen zu allen Proxyeinstellungen zurückgegeben, die auf Dienstebene konfiguriert wurden. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsProxyConfiguration** mit dem Parameter "Filter" auf. Der Filterwert "service:\*" stellt sicher, dass nur Einstellungen mit einem Identitätswert herausgefiltert werden, der mit dem Zeichenfolgewert "service:" beginnt.

    Get-CsProxyConfiguration -Filter "service:*"

## BEISPIEL 4

In Beispiel 4 werden Informationen zu Proxykonfigurationseinstellungen zurückgegeben, die keine Clientzertifikate als Authentifizierungsmechanismus zulassen. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsProxyConfiguration** auf, um eine Auflistung aller derzeit verwendeten Proxykonfigurationseinstellungen zurückzugeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Einstellungen herausfiltert, bei denen die Eigenschaft "UseCertificateForClientToProxyAuth" den Wert "False" aufweist.

    Get-CsProxyConfiguration | Where-Object {$_.UseCertificateForClientToProxyAuth -eq $False}

## BEISPIEL 5

In Beispiel 5 werden alle Proxykonfigurationseinstellungen zurückgegeben, bei denen die maximale Textgröße für Clientnachrichten höchstens 5000 Kilobyte beträgt. Dazu ruft der Befehl zunächst das Cmdlet **Get-CsProxyConfiguration** ohne Parameter auf. Dadurch wird eine Auflistung aller derzeit verwendeten Proxykonfigurationseinstellungen zurückgegeben. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Einstellungen herausfiltert, bei denen die Eigenschaft "MaxClientMessageBodySizeKb" einen geringeren Wert als 5000 aufweist.

    Get-CsProxyConfiguration | Where-Object {$_.MaxClientMessageBodySizeKb -lt 5000}

## Detaillierte Beschreibung

Lync Server ermöglicht die Verwaltung von Proxyservern mithilfe entsprechender Konfigurationseinstellungen. Diese Einstellungen, die sowohl auf globaler Ebene als auch auf Dienstebene angewendet werden können (wenn auch nur für den Edgeserver und den Registrierungsdienst), ermöglichen u. a. die Steuerung von Authentifizierungsprotokollen, die von Clientendpunkten verwendet werden können, und die Entscheidung, ob die Daten eingehender und ausgehender Proxyserververbindungen komprimiert werden. Während der Installation von Lync Server wird automatisch eine globale Auflistung von Konfigurationseinstellungen für Proxyserver erstellt. Wie erwähnt, können Sie auch zusätzliche Auflistungen auf Dienstebene erstellen.

Mit dem Cmdlet **Get-CsProxyConfiguration** können Sie Informationen zu allen Konfigurationseinstellungen für Proxyserver abrufen, die derzeit in Ihrer Organisation verwendet werden.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Get-CsProxyConfiguration** lokal ausführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsProxyConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht die Verwendung von Platzhalterzeichen beim Angeben der zurückzugebenden Proxykonfigurationseinstellungen. Verwenden Sie beispielsweise folgende Syntax, um alle auf Dienstebene konfigurierten Einstellungen zurückzugeben: -Filter &quot;service:*&quot;.</p>
<p>Sie können die Parameter &quot;Filter&quot; und &quot;Identity&quot; nicht im gleichen Befehl verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Eindeutige ID für die zurückzugebenden Konfigurationseinstellungen für Proxyserver. Verwenden Sie folgende Syntax, um die globalen Einstellungen zurückzugeben: -Identity global. Verwenden Sie eine Syntax wie die folgende, um die auf Dienstebene konfigurierten Einstellungen zurückzugeben: -Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;. Beachten Sie, dass beim Angeben eines Identitätswerts keine Platzhalterzeichen verwendet werden können. Wenn Sie Platzhalter einsetzen möchten (oder müssen), verwenden Sie den Parameter &quot;-Filter&quot;.</p>
<p>Wenn dieser Parameter nicht angegeben ist, gibt das Cmdlet <strong>Get-CsProxyConfiguration</strong> eine Auflistung aller Proxyservereinstellungen zurück, die derzeit in Ihrer Organisation verwendet werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Proxykonfigurationsdaten aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsProxyConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Get-CsProxyConfiguration** werden Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

