---
title: Set-CsCpsConfiguration
TOCTitle: Set-CsCpsConfiguration
ms:assetid: 9c2c0ad1-12f8-47b6-a7ec-60d91c9685bf
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412721(v=OCS.15)
ms:contentKeyID: 49294885
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCpsConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ändert eine vorhandene Auflistung von Einstellungen für den Dienst für das Parken von Anrufen. Die Funktion zum Parken von Anrufen ist ein Dienst, über den Benutzer eingehende Anrufe "parken" können. Beim Parken eines Anrufs wird der Anruf an eine Nummer in einem angegebenen Bereich (oder Orbit) übergeben und anschließend sofort in der Warteschleife platziert. Sämtliche Benutzer (nicht nur der Benutzer, der den Anruf ursprünglich entgegengenommen hat) können das Gespräch von einem beliebigen Telefon aus fortführen, indem sie einfach die richtige Nummer eingeben. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Set-CsCpsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCpsConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallPickupTimeoutThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-EnableMusicOnHold <$true | $false>] [-Force <SwitchParameter>] [-MaxCallPickupAttempts <Int32>] [-OnTimeoutURI <String>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 ändert die Konfiguration des Dienstes zum Parken von Anrufen mit dem Identitätswert "site:Redmond1", indem die Anzahl der Rückrufe, die für einen geparkten Anruf beim antwortenden Telefon erfolgen, auf 2 festgelegt wird. Hierzu wird der Parameter "MaxCallPickupAttempts" verwendet und auf den Wert 2 festgelegt.

    Set-CsCpsConfiguration -Identity site:Redmond1 -MaxCallPickupAttempts 2

## BEISPIEL 2

Beispiel 2 ist eine Variante des Befehls aus Beispiel 1. In diesem Fall wird jedoch für alle Konfigurationen (nicht nur für eine Konfiguration) des Diensts für das Parken von Anrufen die Eigenschaft "MaxCallPickupAttempts" auf den Wert 2 festgelegt. Hierzu wird mit dem Cmdlet **Get-CsCpsConfiguration** eine Auflistung aller Einstellungen des Diensts für das Parken von Anrufen abgerufen, die in der Organisation verwendet werden. Diese Auflistung wird dann an das Cmdlet **Set-CsCpsConfiguration** weitergeleitet, das für jedes Element in der Auflistung die Eigenschaft "MaxCallPickupAttempts" auf den Wert 2 festgelegt.

    Get-CsCpsConfiguration | Set-CsCpsConfiguration -MaxCallPickupAttempts 2

## BEISPIEL 3

In diesem Beispiel wird die Konfiguration der Anwendung für das Parken von Anrufen für den Standort "Redmond1" geändert, indem der Zeitraum bis zum Rückruf für einen geparkten Anruf (enthalten in der Eigenschaft "CallPickupTimeoutThreshold") auf 45 Sekunden festgelegt wird.

    Set-CsCpsConfiguration -Identity site:Redmond1 -CallPickupTimeoutThreshold 00:00:45

## Detaillierte Beschreibung

Dieses Cmdlet wird zum Ändern einer vorhandenen Konfiguration des Diensts für das Parken von Anrufen verwendet. Eine Konfiguration des Diensts für das Parken von Anrufen gibt an, wie mit einem geparkten Anruf verfahren wird. Wenn ein geparkter Anruf beispielsweise nach einem bestimmten Zeitraum nicht beantwortet wird, kann er automatisch an einen anderen Benutzer, z. B. an einen Administrator, oder an eine Reaktionsgruppe weitergeleitet werden. Um zu verhindern, dass Anrufe vergessen werden, können die Einstellungen so konfiguriert werden, dass das Telefon nach einem bestimmten Zeitraum erneut läutet. Darüber hinaus kann der Dienst für das Parken von Anrufen so konfiguriert werden, dass für den Anrufer eines geparkten Anrufs Wartemusik wiedergegeben wird.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig dürfen Mitglieder der folgenden Gruppen das Cmdlet **Set-CsCpsConfiguration** lokal ausführen: RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCpsConfiguration"}

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
<td><p><em>CallPickupTimeoutThreshold</em></p></td>
<td><p>Optional</p></td>
<td><p>TimeSpan</p></td>
<td><p>Die Zeitspanne, die nach dem Parken eines Anrufs verstreicht, bis das Telefon zurückgerufen wird, an dem der Anruf entgegengenommen wurde.</p>
<p>Dieser Wert muss im Format &quot;hh:mm:ss&quot; (hh = Stunden, mm = Minuten, ss = Sekunden) eingegeben werden.</p>
<p>Mindestwert: 10 Sekunden (00:00:10); Höchstwert: 10 Minuten (00:10:00)</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMusicOnHold</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Legt fest, ob der Anrufer eines geparkten Anrufs Wartemusik hört.</p>
<p>Lync Server umfasst eine Standarddatei für Wartemusik. Sie können diese Datei (und damit die Musik, die der Anrufer während der Wartezeit hört) über das Cmdlet <strong>Set-CsCallParkServiceMusicOnHoldFile</strong> ändern.</p></td>
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
<td><p>XdsIdentity</p></td>
<td><p>Eine eindeutige ID für die Konfiguration, die geändert werden soll. Der Identitätswert gibt den Bereich an, auf den die Konfiguration angewendet wird. Eine Konfiguration kann entweder global oder auf einen bestimmten Standort angewendet werden (im Format &quot;site:&lt;Standortname&gt;&quot;, z. B. &quot;site:Redmond&quot;).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>CallParkServiceSettings</p></td>
<td><p>Ein Objektverweis auf ein Konfigurationsobjekt des Diensts für das Parken von Anwendungen vom Typ &quot;Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings&quot;. Dieses Objekt kann durch Aufrufen des Cmdlets <strong>Get-CsCpsConfiguration</strong> abgerufen werden. Das Objekt kann anschließend geändert und die Änderungen können gespeichert werden, indem das Objekt in diesem Parameter wieder an das Cmdlet <strong>Set-CsCpsConfiguration</strong> übergeben wird.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxCallPickupAttempts</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>Die Anzahl der Rückrufe, die für einen geparkten Anruf beim antwortenden Telefon erfolgen, bevor der Anruf an den Fallback-URI weitergeleitet wird. Der Fallback-URI wird mit dem Parameter &quot;OnTimeoutURI&quot; festgelegt.</p>
<p>Mindestwert: 1; Höchstwert: 10</p></td>
</tr>
<tr class="even">
<td><p><em>OnTimeoutURI</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Die SIP-Adresse des Benutzers oder der Reaktionsgruppe, an die nicht beantwortete geparkte Anrufe weitergeleitet werden. Der geparkte Anruf wird weitergeleitet, nachdem die Anzahl der über den Parameter &quot;MaxCallPickupAttempts&quot; definierten Rückrufe erreicht wurde. Wenn dieser Parameter auf &quot;Null&quot; festgelegt ist, wird &quot;OnTimeoutURI&quot; ignoriert und der geparkte Anruf nach erfolglosen Rückrufversuchen getrennt.</p>
<p>Bei den Werten muss es sich um SIP-URI handeln, beginnend mit &quot;sip:&quot;. Beispiel: sip:rgs1@litwareinc.com.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings-Objekt. Akzeptiert eine weitergeleitete Eingabe von Konfigurationsobjekten für den Dienst zum Parken von Anrufen.

## Rückgabetypen

Ändert ein Objekt vom Typ "Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings".

## Siehe auch

#### Weitere Ressourcen

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

