---
title: New-CsEdgeAllowList
TOCTitle: New-CsEdgeAllowList
ms:assetid: 21a6d546-9e03-485c-b7ec-9deb778f2b01
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994023(v=OCS.15)
ms:contentKeyID: 52056304
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowList

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ermöglicht Administratoren, die Domänen anzugeben, mit denen die Benutzer kommunizieren dürfen. Das Cmdlet **New-CsEdgeAllowList**, das nur in Microsoft Lync Online verwendet werden kann, muss zusammen mit dem Cmdlet **New-CsEdgeDomainPattern** und dem Cmdlet **Set-CsTenantFederationConfiguration** verwendet werden.

## Syntax

    New-CsEdgeAllowList [-AllowedDomain <PSListModifier>] [-Verbose]

## Beispiele

## Beispiel 1

Mit den in Beispiel 1 gezeigten Befehlen wird die Domäne "fabrikam.com" der Liste der zulässigen Domänen für den Mandanten mit der Mandaten-ID "bf19b7db-6960-41e5-a139-2aa373474354" zugeordnet. Hierfür wird im ersten Befehl in diesem Beispiel des Cmdlet **New-CsEdgeDomainPattern** verwendet, um ein Domänenobjekt für "fabrikam.com" zu erstellen. Dieses Objekt wird in einer Variablen namens **$x** gespeichert. Nachdem das Domänenobjekt erstellt wurde, wird das Cmdlet **New-CsEdgeAllowList** verwendet, um eine neue Liste der zulässigen Domänen zu erstellen, die nur die Domäne "fabrikam.com" enthält.

Sobald diese Liste der zulässigen Domänen erstellt wurde, kann mit dem letzten Befehl im Beispiel das Cmdlet **Set-CsTenantFederationConfiguration** aufgerufen werden, um "fabrikam.com" als die einzige Domäne in der Liste der zulässigen Domänen für den angegebenen Mandanten zu konfigurieren.

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Beachten Sie, dass der Parameter **Tenant** nur in einer Hybridbereitstellung erforderlich ist. Wenn Sie nur mit Skype for Business Online verbunden sind, kann der Parameter **Tenant** ausgelassen werden.

## Beispiel 2

In Beispiel 2 wird gezeigt, wie Sie einer Liste der zulässigen Domänen mehrere Domänen hinzufügen können. Dafür wird das Cmdlet **New-CsEdgeDomainPattern** mehrere Male aufgerufen (einmal für jede Domäne, die der Liste hinzugefügt werden soll), und die resultierenden Domänenobjekte werden in unterschiedlichen Variablen gespeichert. Jede dieser Variablen kann dann der Liste der zulässigen Domänen hinzugefügt werden, die mit dem Cmdlet **New-CsEdgeAllowList** erstellt wird, indem einfach der Parameter **AllowedDomain** verwendet wird und die Variablennamen durch Kommas getrennt werden:

$newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y

    $x = New-CsEdgeDomainPattern -Domain "contoso.com"
    $y = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Beispiel 3

In Beispiel 3 werden alle Domänen aus der Liste der zulässigen Domänen entfernt. Hierzu wird im ersten Befehl im Beispiel das Cmdlet **New-CsEdgeAllowList** verwendet, um eine leere Liste der zulässigen Domänen zu erstellen. Dies wird erreicht, indem die Eigenschaft **AllowedDomain** auf einen Nullwert ($Null) festgelegt wird. Der resultierende Objektverweis ($newAllowList) wird dann zusammen mit dem Cmdlet **Set-CsTenantFederationConfiguration** verwendet, um alle Domänen aus der Liste der zulässigen Domänen für den Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" zu entfernen.

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $Null
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Detaillierte Beschreibung

"Partnerverbund" ist eine Funktion, die es Benutzern ermöglicht, Chatnachrichten und Anwesenheitsinformationen mit Benutzern in anderen Domänen auszutauschen. In Lync Online können Administratoren die Einstellungen für die Verbundkonfiguration verwenden, um Folgendes zu steuern:

  - Ob Benutzer mit Personen aus anderen Domänen kommunizieren können und, wenn ja, mit welchen Domänen diese Kommunikation stattfinden darf.

  - Ob Benutzer mit Personen kommunizieren können, die über Konten bei öffentlichen Instant Messaging- und Anwesenheitsinformationsanbietern wie Windows Live, AOL und Yahoo\! verfügen.

Die Partnerverbundfunktion wird teilweise mithilfe der Liste der zulässigen Domänen bzw. der Liste der blockierten Domänen verwaltet. Die Liste der zulässigen Domänen gibt die Domänen an, mit denen die Benutzer kommunizieren dürfen, und die Liste der blockierten Domänen enthält die Domänen, mit denen die Benutzer nicht kommunizieren dürfen. Standardmäßig können Benutzer mit allen Domänen kommunizieren, die sich nicht in der Liste der blockierten Domänen befinden. Der Administrator kann diese Standardeinstellung jedoch ändern und die Kommunikation auf die Domänen beschränken, die sich in der Liste der zulässigen Domänen befinden.

In Lync Online ist es nicht zulässig, die Liste der zulässigen oder blockierten Domänen direkt zu ändern. So können Sie beispielsweise nicht einen Befehl wie den folgenden verwenden, mit dem ein Zeichenfolgenwert, der für einen Domänennamen steht, an die Liste der zulässigen Domänen übergeben wird:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

Stattdessen müssen Sie entweder das Cmdlet **New-CsEdgeAllowAllKnownDomains** oder das Cmdlet **New-CsEdgeAllowList** verwenden, um ein Domänenobjekt zu erstellen und dieses Domänenobjekt dann an das Cmdlet **Set-CsTenantFederationConfiguration** übergeben. Das Cmdlet **New-CsEdgeAllowAllKnownDomains** wird verwendet, wenn Sie zulassen möchten, dass die Benutzer mit allen Domänen außer denjenigen kommunizieren können, die explizit in der Liste der blockierten Domänen aufgeführt sind. Das Cmdlet **New-CsEdgeAllowList** wird verwendet, wenn Sie die Benutzerkommunikation auf eine bestimmte Auflistung von Domänen beschränken möchten. In diesem Fall dürfen die Benutzer nur mit Domänen kommunizieren, die sich in der Liste der zulässigen Domänen befinden.

Wenn Sie der Liste der zulässigen Domänen eine einzelne Domäne ("fabrikam.com") hinzufügen möchten, müssen Sie eine Befehlsreihe wie die folgende verwenden:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Nachdem diese Befehlsreihe ausgeführt wurde, können die Benutzer nur noch mit den Benutzern der Domäne "fabrikam.com" kommunizieren.

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
<td><p><em>AllowedDomain</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Objektverweis auf die neuen Domäne (oder Reihe von Domänen), die der Liste der zulässigen Domänen hinzugefügt werden soll. Verweise auf Domänenobjekte müssen mit dem Cmdlet <strong>New-CsEdgeDomainPattern</strong> erstellt werden. Es können mehrere Domänenobjekte hinzugefügt werden, indem die Objektverweise durch Kommas getrennt werden. Ein Beispiel:</p>
<p>-AllowedDomain $x,$y</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **New-CsEdgeAllowList** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **New-CsEdgeAllowList** werden neue Instanzen des Objekts **Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowList** erstellt.

## Siehe auch

#### Weitere Ressourcen

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

