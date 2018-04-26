---
title: Get-CsAudioConferencingProvider
TOCTitle: Get-CsAudioConferencingProvider
ms:assetid: 4632e9d0-aa87-459f-ad7e-27125c11da5b
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994030(v=OCS.15)
ms:contentKeyID: 52056324
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioConferencingProvider

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Audiokonferenzanbietern zurück, die zur Verwendung in der Organisation freigegeben sind. Audiokonferenzanbieter sind Drittanbieter, die Organisationen Konferenzdienste bereitstellen.

Das Cmdlet **Get-CsAudioConferencingProvider** kann nur mit Microsoft Lync Online verwendet werden.

## Syntax

    Get-CsAudioConferencingProvider [[-Identity] <XdsGlobalRelativeIdentity>] [-LocalStore][<CommonParameters>]Get-CsAudioConferencingProvider [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 gibt Informationen zu allen Audiokonferenzanbietern zurück, die zur Verwendung in Ihrer Organisation zur Verfügung stehen.

    Get-CsAudioConferencingProvider

## Beispiel 2

In Beispiel 2 werden Informationen für einen einzigen Audiokonferenzanbieter zurückgegeben, den Anbieter mit der Identität "Fabrikam Telecom".

    Get-CsAudioConferencingProvider -Identity "Fabrikam Telecom"

## Beispiel 3

Beispiel 3 zeigt, wie Platzhalterwerte (und der Parameter "Filter") verwendet werden können, um Informationen zu Audiokonferenzanbietern zurückzugeben. In diesem Beispiel gibt der Filterwert "\*Fabrikam\*" alle Audiokonferenzanbieter zurück, deren Identität den Zeichenfolgenwert "Fabrikam" an einer beliebigen Stelle enthält.

    Get-CsAudioConferencingProvider -Filter "*Fabrikam*"

## Detaillierte Beschreibung

Bei einem Audiokonferenzanbieter handelt es sich um ein Drittanbieterunternehmen, das Konferenzdienste für Organisationen bereitstellt. Audiokonferenzanbieter bieten u. a. die Möglichkeit für Benutzer, von außerhalb eines Standorts und ohne Verbindung mit dem Unternehmensnetzwerk oder dem Internet am Audioteil einer Konferenz oder Besprechung teilzunehmen. Audiokonferenzanbieter stellen oft hochwertige Dienstleistungen wie Simultanübersetzung, Transkription und operatorgestützte Livekonferenzen bereit.

Nachdem eine Organisation einen Vertrag mit einem Audiokonferenzanbieter abgeschlossen hat, können Benutzer mit dem Cmdlet **Set-CsUserAcp** dem Anbieter zugewiesen werden. Administratoren können Informationen zu den verfügbaren Audiokonferenzanbietern mit dem Cmdlet **Get-CsAudioConferencingProvider** abrufen.

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
<td><p>Ermöglicht die Verwendung von Platzhalterzeichen beim Angeben der zurückzugebenden Audiokonferenzanbieter. Mit der folgenden Syntax werden beispielsweise alle Audiokonferenzanbieter zurückgegeben, deren Identität den Zeichenfolgenwert &quot;fabrikam&quot; an einer beliebigen Stelle enthält:</p>
<p>-Filter &quot;*fabrikam*&quot;</p>
<p>Beachten Sie, dass Sie die Parameter &quot;Identity&quot; und &quot;Filter&quot; nicht im selben Befehl verwenden können.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Eindeutige ID für den zurückzugebenden Audiokonferenzanbieter. Beispiel:</p>
<p>-Identity &quot;Fabrikam Telecom&quot;</p>
<p>Ist weder der Parameter &quot;Identity&quot; noch der Parameter &quot;Filter&quot; im Befehl enthalten, gibt das Cmdlet <strong>Get-CsAudioConferencingProvider</strong> Informationen zu allen verfügbaren Anbietern zurück.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Konfigurationsdaten für Audiokonferenzanbieter aus dem lokalen Replikat des zentralen Verwaltungsspeichers statt aus dem zentralen Verwaltungsspeicher selbst ab.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsAudioConferencingProvider** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Get-CsAudioConferencingProvider** gibt Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.AudioConferencingProvider.AudioConferencingProvider\#Decorated" zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

