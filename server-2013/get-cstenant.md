---
title: Get-CsTenant
TOCTitle: Get-CsTenant
ms:assetid: 7b642117-5ca7-4a5b-bca7-16b0ae694ae2
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994044(v=OCS.15)
ms:contentKeyID: 52056389
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenant

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den Skype for Business Online-Mandanten zurück, die zur Verwendung in Ihrer Organisation konfiguriert wurden. Mandanten stellen Gruppen von Onlinebenutzern dar. In vielen Fällen benötigen Sie möglicherweise nur einen einzigen Mandanten. Wenn jedoch verschiedene Benutzergruppen unterschiedliche Verwaltungsanforderungen haben, unterstützt Skype for Business Online das Einrichten mehrerer Mandanten für eine Organisation.

Get-CsTenant kann nur mit Skype for Business Online verwendet werden.

## Syntax

    Get-CsTenant [[-Identity] <OUIdParameter>] [-Filter <String>] [-ResultSize <Unlimited`1>] [-Verbose]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 gibt Informationen zu allen Mandanten zurück, die zur Verwendung in Ihrer Organisation konfiguriert wurden.

    Get-CsTenant

## Beispiel 2

In Beispiel 2 werden Informationen zu einem einzigen Mandanten zurückgegeben, dem Mandanten mit der Identität "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsTenant -Identity "bf19b7db-6960-41e5-a139-2aa373474354"

## Beispiel 3

Der vorstehende Befehl zeigt eine alternative Methode zum Zurückgeben von Informationen zu einem einzigen Mandanten. In diesem Beispiel werden dafür der Parameter "Filter" und der Filterwert "{DisplayName –eq "Fabrikam"}" eingeschlossen. Mit dieser Syntax werden nur Informationen für den Mandanten mit dem Anzeigenamen "Fabrikam" zurückgegeben.

    Get-CsTenant -Filter {DisplayName -eq "Fabrikam"}

## Beispiel 4

Der Befehl in Beispiel 4 gibt Informationen zu allen Mandanten zurück, bei denen die Eigenschaft "ServiceInstance" den Wert "LitwareincCommunicationsOnline/San Antonio" hat. Dafür schließt der Befehl den Parameter "Filter" und den Filterwert "{ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}" ein. Dieser Filterwert schränkt die zurückgegebenen Daten auf Mandanten ein, deren Eigenschaft "ServiceInstance" gleich (-eq) "LitwareincCommunicationsOnline/San Antonio" ist.

    Get-CsTenant -Filter {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}

## Beispiel 5

In Beispiel 5 werden Informationen zu allen Mandanten zurückgegeben, deren Anzeigename für das Land oder die Region dem Wert "Australia" entspricht. Dafür werden der Parameter "Filter" und der Filterwert "{CountryOrRegionDisplayName -eq "Australia"}" verwendet.

    Get-CsTenant -Filter {CountryOrRegionDisplayName -eq "Australia"}

## Detaillierte Beschreibung

In Skype for Business Online stellen Mandanten Gruppen von Benutzern dar, deren Konten in dem Dienst verwaltet werden. Viele Organisationen benötigen nur einen einzigen Mandanten für alle Benutzerkonten. Aber die Skype for Business Online-Verwaltung wird oft Mandant für Mandant durchgeführt, was bedeutet, dass alle Benutzer im selben Mandanten über dieselbe VoIP-Richtlinie, dieselben Partnerverbundkonfigurationseinstellungen usw. verfügen. Wenn Sie einige Benutzer auf eine andere Weise als andere Benutzer verwalten müssen, sollten Sie die Verwendung mehrerer Mandanten in Betracht ziehen, die dann jeweils über eine eigene Auflistung von Richtlinien und Einstellungen verfügen.

Unabhängig von der Anzahl Ihrer Mandanten können Sie Informationen zu diesen Mandanten mit dem Cmdlet **Get-CsTenant** zurückgeben.

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
<td><p>Ermöglicht Ihnen, Daten mithilfe von Active Directory-Attributen zurückzugeben, ohne den vollständigen Active Directory Distinguished Name angeben zu müssen. Verwenden Sie beispielsweise zum Abrufen eines Mandanten mithilfe des Anzeigenamens für den Mandanten eine Syntax wie die folgende:</p>
<p>Get-CsTenant –Filter {DisplayName –eq &quot;FabrikamTenant&quot;}</p>
<p>Verwenden Sie die folgende Syntax, um alle Mandanten zurückzugeben, die eine Fabrikam-Domäne verwenden:</p>
<p>Get-CsTenant –Filter {Domains –like &quot;*fabrikam*&quot;}</p>
<p>Der Parameter &quot;-Filter&quot; verwendet dieselbe Windows PowerShell-Filterungssyntax wie das Cmdlet &quot;Where-Object&quot;.</p>
<p>Sie können die Parameter &quot;Identity&quot; und &quot;Filter&quot; nicht in demselben Befehl verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Active Directory Distinguished Name des Mandanten. Beispiel:</p>
<p>-Identity &quot;OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=litwareinc,dc=com&quot;</p>
<p>Wenn Sie weder den Parameter &quot;Identity&quot; noch den Parameter &quot;Filter&quot; einschließen, gibt das Cmdlet <strong>Get-CsTenant</strong> Informationen zu allen Mandanten zurück.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited`1</p></td>
<td><p>Ermöglicht es Ihnen, die Anzahl der vom Cmdlet zurückgegebenen Datensätze einzuschränken. Um beispielsweise sieben Mandanten (unabhängig von der Gesamtzahl der Mandanten in der Gesamtstruktur) zurückzugeben, verwenden Sie den Parameter &quot;ResultSize&quot; und legen den Parameterwert auf 7 fest. Beachten Sie, dass nicht garantiert werden kann, welche sieben Benutzer zurückgegeben werden.</p>
<p>Für die Ergebnisgröße kann ein ganzzahliger Wert zwischen einschließlich 0 und 2147483647 festgelegt werden. Bei Festlegung von 0 wird der Befehl ausgeführt, es werden jedoch keine Daten zurückgegeben. Wenn Sie &quot;ResultSize&quot; auf 7 festlegen, jedoch lediglich über drei Mandanten in Ihrer Gesamtstruktur verfügen, werden diese drei Mandanten zurückgegeben und der Befehl wird anschließend ohne Ausgabe eines Fehlers abgeschlossen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Das Cmdlet **Get-CsTenant** akzeptiert weitergeleitete Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.TenantObject" sowie Zeichenfolgenwerte, die die Identität eines Skype for Business Online-Mandanten darstellen (z. B. "OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=vdomain,dc=com").

## Rückgabetypen

Das Cmdlet **Get-CsTenant** gibt Instanzen des Objekts "Microsoft.Rtc.Management.ADConnect.Schema.TenantObject" zurück.

## Siehe auch

#### Weitere Ressourcen

[Get-CsOnlineUser](get-csonlineuser.md)

