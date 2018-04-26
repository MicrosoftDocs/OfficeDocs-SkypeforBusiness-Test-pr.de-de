---
title: New-CsEdgeDomainPattern
TOCTitle: New-CsEdgeDomainPattern
ms:assetid: 653bc148-c22b-4ad4-afdd-17aaeaa299d2
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994040(v=OCS.15)
ms:contentKeyID: 52056371
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeDomainPattern

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Dient zum Angeben einer Domäne, die dem für den Partnerverbund aktivierten oder deaktivierten Domänensatz hinzugefügt oder daraus entfernt wird. Sie müssen das Cmdlet **New-CsEdgeDomainPattern** verwenden, wenn Sie die Listen zulässiger oder blockierter Domänen ändern. Zeichenfolgenwerte (wie "fabrikam.com") können nicht direkt an die für die Verwaltung dieser Listen verwendeten Cmdlets übergeben werden.

Das Cmdlet **New-CsEdgeDomainPattern** kann nur mit Skype for Business Online verwendet werden.

## Syntax

    New-CsEdgeDomainPattern -Domain <String> [-Verbose]

## Beispiele

## Beispiel 1

Beispiel 1 zeigt, wie Sie eine einzige Domäne der Liste blockierter Domänen für einen bestimmten Mandanten zuweisen können. Dafür erstellt der erste Befehl im Beispiel ein Domänenobjekt für die Domäne "fabrikam.com". Dafür wird das Cmdlet **New-CsEdgeDomainPattern** aufgerufen und das daraus resultierende Domänenobjekt in einer Variable namens "$x" gespeichert. Der zweite Befehl verwendet dann das Cmdlet **Set-CsTenantFederationConfiguration** und den Parameter "BlockedDomains", um "fabrikam.com" als die einzige vom Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" blockierte Domäne zu konfigurieren.

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

## Detaillierte Beschreibung

Ein Verbund ist ein Dienst, über den Benutzer Chat- und Anwesenheitsinformationen mit Benutzern anderer Domänen austauschen können. Mit Skype for Business Online können Administratoren die Verbundkonfigurationseinstellungen verwenden, um Folgendes zu steuern:

  - Die Möglichkeit für Benutzer, mit Personen aus anderen Domänen kommunizieren zu können, sowie für die Benutzer festlegen, mit welchen Domänen Kommunikation erlaubt sein soll

  - Die Möglichkeit für Benutzer, mit Personen zu kommunizieren, die Konten bei öffentlichen Instant Messaging- und Anwesenheitsanbietern wie Windows Live, AOL oder Yahoo\! haben

Die Partnerverbundfunktion wird teilweise mithilfe der Liste der zulässigen Domänen bzw. der Liste der blockierten Domänen verwaltet. Die Liste der zulässigen Domänen gibt die Domänen an, mit denen die Benutzer kommunizieren dürfen, und die Liste der blockierten Domänen enthält die Domänen, mit denen die Benutzer nicht kommunizieren dürfen. Standardmäßig können Benutzer mit allen Domänen kommunizieren, die sich nicht in der Liste der blockierten Domänen befinden. Der Administrator kann diese Standardeinstellung jedoch ändern und die Kommunikation auf die Domänen beschränken, die sich in der Liste der zulässigen Domänen befinden.

In Skype for Business Online ist es nicht zulässig, die Liste der zulässigen oder blockierten Domänen direkt zu ändern. So können Sie beispielsweise nicht einen Befehl wie den folgenden verwenden, mit dem ein Zeichenfolgenwert, der für einen Domänennamen steht, an die Liste der blockierten Domänen übergeben wird:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains "fabrikam.com"

Stattdessen müssen Sie mit dem Cmdlet **New-CsEdgeDomainPattern** ein Domänenobjekt erstellen, dieses Objekt in einer Variable (in diesem Beispiel "$x") speichern und den Variablennamen dann an die Liste blockierter Domänen übergeben:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

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
<td><p><em>Domain</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>Vollqualifizierter Domänenname der Domäne, die zur Liste zulässiger Domänen hinzugefügt werden soll. Beispiel:</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>Beachten Sie, dass Sie beim Angeben eines Domänennamens keine Platzhalter verwenden können.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **New-CsEdgeDomainPattern** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **New-CsEdgeDomainPattern** erstellt neue Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DomainPattern".

## Siehe auch

#### Weitere Ressourcen

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

