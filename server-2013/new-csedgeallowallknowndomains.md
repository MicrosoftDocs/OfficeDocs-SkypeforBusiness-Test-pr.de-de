---
title: New-CsEdgeAllowAllKnownDomains
TOCTitle: New-CsEdgeAllowAllKnownDomains
ms:assetid: f9416909-c328-41b3-9215-7ebd091b0ca0
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994088(v=OCS.15)
ms:contentKeyID: 52056507
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowAllKnownDomains

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Ermöglicht den Microsoft Lync Online-Partnerverbund mit allen Domänen außer denen, die in der Liste blockierter Domänen vorhanden sind.

Dieses Cmdlet kann nur in Verbindung mit Skype for Business Online verwendet werden.

## Syntax

    New-CsEdgeAllowAllKnownDomains [-Verbose]

## Beispiele

## Beispiel 1

Die zwei Befehle in Beispiel 1 konfigurieren die Partnerverbundeinstellungen für den Mandanten mit der Identität "bf19b7db-6960-41e5-a139-2aa373474354" so, dass alle bekannten Domänen zulässig sind. Dafür verwendet der erste Befehl im Beispiel das Cmdlet **New-CsEdgeAllowAllKnownDomains**, um eine Instanz des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains" zu erstellen. Diese Instanz wird in einer Variable namens "$x" gespeichert. Im zweiten Befehl wird das Cmdlet **Set-CsTenantFederationConfiguration** zusammen mit dem Parameter "AllowedDomains" aufgerufen. Mit "$x" als Parameterwert werden die Partnerverbundeinstellungen so konfiguriert, dass alle bekannten Domänen zulässig sind.

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

## Beispiel 2

Beispiel 2 zeigt, wie Sie alle Mandanten so konfigurieren können, dass eine Kommunikation mit allen Domänen zulässig ist, die nicht ausdrücklich in der Liste blockierter Domänen aufgeführt sind. Dafür verwendet der erste Befehl im Beispiel das Cmdlet **New-CsEdgeAllowAllKnownDomains**, um eine Instanz des Objekts "AllowAllKnownDomains" zu erstellen, ein Objekt, das in einer Variable namens "$x" gespeichert ist.

Der zweite Befehl im Beispiel verwendet dann das Cmdlet **Get-CsTenant**, um eine Auflistung aller verfügbaren Mandanten zurückzugeben. Diese Auflistung wird dann an das Cmdlet **ForEach-Object** weitergeleitet. Das Cmdlet **ForEach-Object** wiederum führt das Cmdlet **Set-CsTenantFederationConfiguration** für jeden Mandanten in der Auflistung aus und konfiguriert die Eigenschaft "AllowedDomains" so, dass alle bekannten Domänen zulässig sind.

    $x = New-CsEdgeAllowAllKnownDomains
    Get-CsTenant | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantID -AllowedDomains $x}

## Detaillierte Beschreibung

Ein Verbund ist ein Dienst, über den Benutzer Chat- und Anwesenheitsinformationen mit Benutzern anderer Domänen austauschen können. Mit Lync Online können Administratoren die Verbundkonfigurationseinstellungen verwenden, um Folgendes zu steuern:

  - Die Möglichkeit für Benutzer, mit Personen aus anderen Domänen kommunizieren zu können, sowie für die Benutzer festlegen, mit welchen Domänen Kommunikation erlaubt sein soll

  - Die Möglichkeit für Benutzer, mit Personen zu kommunizieren, die Konten bei öffentlichen Instant Messaging- und Anwesenheitsanbietern wie Windows Live, AOL oder Yahoo\! haben

Die Partnerverbundfunktion wird teilweise mithilfe der Liste der zulässigen Domänen bzw. der Liste der blockierten Domänen verwaltet. Die Liste der zulässigen Domänen gibt die Domänen an, mit denen die Benutzer kommunizieren dürfen, und die Liste der blockierten Domänen enthält die Domänen, mit denen die Benutzer nicht kommunizieren dürfen. Standardmäßig können Benutzer mit allen Domänen kommunizieren, die sich nicht in der Liste der blockierten Domänen befinden. Der Administrator kann diese Standardeinstellung jedoch ändern und die Kommunikation auf die Domänen beschränken, die sich in der Liste der zulässigen Domänen befinden.

In Lync Online ist es nicht zulässig, die Liste der zulässigen oder blockierten Domänen direkt zu ändern. So können Sie beispielsweise nicht einen Befehl wie den folgenden verwenden, mit dem ein Zeichenfolgenwert, der für einen Domänennamen steht, an die Liste der zulässigen Domänen übergeben wird:

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

Stattdessen müssen Sie entweder das Cmdlet **New-CsEdgeAllowAllKnownDomains** oder das Cmdlet **New-CsEdgeAllowList** verwenden, um ein Domänenobjekt zu erstellen und dieses Domänenobjekt dann an das Cmdlet **Set-CsTenantFederationConfiguration**zu übergeben. Das Cmdlet **New-CsEdgeAllowAllKnownDomains** wird verwendet, wenn Sie zulassen möchten, dass die Benutzer mit allen Domänen außer denjenigen kommunizieren können, die explizit in der Liste der blockierten Domänen aufgeführt sind. Das Cmdlet N**ew-CsEdgeAllowList** wird verwendet, wenn Sie die Benutzerkommunikation auf eine bestimmte Auflistung von Domänen beschränken möchten. In diesem Fall dürfen die Benutzer nur mit Domänen kommunizieren, die sich in der Liste der zulässigen Domänen befinden.

Verwenden Sie einen Befehlssatz wie den folgenden, um den Partnerverbund mit allen bekannten Domänen zu konfigurieren:

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

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
<td><p>Dieses Cmdlet stellt nur gängige Windows PowerShell-Parameter bereit.</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **New-CsEdgeAllowAllKnownDomains** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **New-CsEdgeAllowAllKnownDomains** erstellt neue Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains".

## Siehe auch

#### Weitere Ressourcen

[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

