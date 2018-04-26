---
title: Set-CsTenantFederationConfiguration
TOCTitle: Set-CsTenantFederationConfiguration
ms:assetid: e13c2f55-7a68-4174-a0da-5eec8c65f64c
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994080(v=OCS.15)
ms:contentKeyID: 52056474
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantFederationConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Verwaltet Verbundkonfigurationseinstellungen für Ihre Microsoft Lync Online-Mandanten. Anhand dieser Einstellungen wird entschieden, mit welchen Domänen Ihre Benutzer kommunizieren dürfen.

Das Cmdlet **Set-CsTenantFederationConfiguration** kann nur mit Skype for Business Online verwendet werden.

## Syntax

    Set-CsTenantFederationConfiguration [[-Identity] <XdsIdentity>] [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Force] [-Verbose] [-WhatIf] [-Confirm]Set-CsTenantFederationConfiguration [-Tenant <Nullable`1>] [-AllowedDomains <IAllowedDomainsChoice>] [-BlockedDomains <PSListModifier>] [-AllowFederatedUsers] [-AllowPublicUsers] [-SharedSipAddressSpace] [-Instance <PSObject>] [-Force] [-Verbose] [-WhatIf] [-Confirm]

## Beispiele

## Beispiel 1

Der im Beispiel 1 gezeigte Befehl deaktiviert die Kommunikation mit öffentlichen Anbietern für den Mandanten, der die Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" hat.

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowPublicUsers $False

Der Parameter **Tenant** ist optional. Wenn Sie diesen Parameter nicht angeben, fügt Windows PowerShell die richtige Mandanten-ID automatisch auf Basis Ihrer Verbindung ein.

## Beispiel 2

Im Beispiel 2 wird gezeigt, wie Sie die Kommunikation mit allen öffentlichen Anbietern für alle Mandanten in Ihrer Organisation deaktivieren können. Dazu wird im Befehl zunächst das Cmdlet **Get-CsTenant** aufgerufen, das eine Sammlung aller verfügbaren Mandanten zurückgibt. Diese Sammlung wird dann an das Cmdlet **Select-Object** weitergeleitet, in dem für jedes Element der Sammlung nur die Eigenschaft **TenantId** ausgelesen wird. Diese Sammlung der Mandanten-IDs wird nun an das Cmdlet **ForEach-Object** weitergeleitet. Das Cmdlet F**orEach-Object** übernimmt dann jede Mandanten-ID und führt das Cmdlet **Set-CsTenantFederationConfiguration** für die jeweilige ID aus, wobei die Eigenschaft **AllowPublicUsers** für jeden Mandanten auf **False** ($False) festgelegt wird.

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantId -AllowPublicUsers $False}

## Beispiel 3

Im Beispiel 3 wird die Domäne **fabrikam.com** für den Mandanten mit der Mandanten -ID "bf19b7db-6960-41e5-a139-2aa373474354" als einzige Domäne in der Liste der blockierten Domänen zugewiesen. Dazu wird im ersten Befehl des Beispiels das Cmdlet **New-CsEdgeDomainPattern** verwendet, um ein neues Domänenobjekt für **fabrikam.com** zu erstellen. Dieses Domänenobjekt wird in der Variablen **$x** gespeichert.

Im zweiten Befehl des Beispiels wird dann mit dem Cmdlet **Set-CsTenantFederationConfiguration** die Liste der blockierten Domänen aktualisiert. Durch Verwenden der Methode **Replace** wird sichergestellt, dass die vorhandene Liste der blockierten Domänen durch die neue Liste ersetzt wird: eine Liste, die nur die Domäne **fabrikam.com** enthält.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Replace=$x}

## Beispiel 4

Die im Beispiel 4 aufgeführten Befehle entfernen **fabrikam.com** aus der Liste der blockierten Domänen für den Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354". Dazu wird im ersten Befehl des Beispiels das Cmdlet **New-CsEdgeDomainPattern** verwendet, um ein Domänenobjekt für **fabrikam.com** zu erstellen. Dieses Domänenobjekt wird dann in der Variablen **$x** gespeichert.

Im zweiten Befehl des Beispiels werden das Cmdlet **Set-CsTenantFederationConfiguration** und die Methode **Remove** verwendet, um **fabrikam.com** für den angegebenen Mandanten aus der Liste der blockierten Domänen zu entfernen.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Remove=$x}

## Beispiel 5

Die im Beispiel 5 aufgeführten Befehle fügen die Domäne **fabrikam.com** zur Liste der blockierten Domänen für den Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" hinzu. Um eine neue blockierte Domäne hinzuzufügen, wird im ersten Befehl des Beispiels das Cmdlet **New-CsEdgeDomainPattern** verwendet, um ein Domänenobjekt für **fabrikam.com** zu erstellen. Dieses Objekt wird dann in der Variablen **$x** gespeichert.

Nachdem das Domänenobjekt erstellt wurde, werden im zweiten Befehl das Cmdlet **Set-CsTenantFederationConfiguration** und die Methode **Add** verwendet, um **fabrikam.com** zu den Domänen hinzuzufügen, die sich bereits in der Liste der blockierten Domänen befinden.

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant bf19b7db-6960-41e5-a139-2aa373474354 -BlockedDomains @{Add=$x}

## Beispiel 6

Im Beispiel 6 wird gezeigt, wie Sie alle Domänen entfernen können, die einem Mandanten in der Liste der blockierten Domänen zugewiesen sind. Dazu fügen Sie einfach den Parameter **BlockedDomains** ein, und legen Sie den Parameterwert auf den Nullwert ($Null) fest. Nach dem Ausführen dieses Befehls enthält die Liste der blockierten Domänen keine Domänen mehr für den Mandanten, der die Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" hat.

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $Null

## Detaillierte Beschreibung

Ein Verbund ist ein Dienst, über den Benutzer Chat- und Anwesenheitsinformationen mit Benutzern anderer Domänen austauschen können. Mit Lync Online können Administratoren die Verbundkonfigurationseinstellungen verwenden, um Folgendes zu steuern:

  -   
    Die Möglichkeit für Benutzer, mit Personen aus anderen Domänen kommunizieren zu können, sowie für die Benutzer festlegen, mit welchen Domänen Kommunikation erlaubt sein soll

  -   
    Die Möglichkeit für Benutzer, mit Personen zu kommunizieren, die Konten bei öffentlichen Instant Messaging- und Anwesenheitsanbietern wie Windows Live, AOL oder Yahoo\! haben

Administratoren können mit dem Cmdlet **Set-CsTenantFederationConfiguration** einen Verbund mit anderen Domänen sowie einen Verbund mit öffentlichen Anbietern aktivieren und deaktivieren. Außerdem können mit diesem Cmdlet explizit die Domänen festgelegt werden, mit denen Benutzer kommunizieren bzw. nicht kommunizieren dürfen. Administratoren müssen aber das Cmdlet **Set-CsTenantPublicProvider** verwenden, wenn Sie die öffentlichen Instant Messaging- und Anwesenheitsanbieter angeben möchten, mit denen Benutzer kommunizieren bzw. nicht kommunizieren dürfen.

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
<td><p><em>AllowedDomains</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.IAllowedDomainsChoice</p></td>
<td><p>Domänenobjekte (die mit dem Cmdlet <strong>New-CsEdgeAllowList</strong> oder dem Cmdlet <strong>New-CsEdgeAllowAllKnownDomains</strong> erstellt wurden), die den Domänen entsprechen, mit denen Benutzer kommunizieren dürfen. Wenn das Cmdlet <strong>New-CsEdgeAllowAllKnownDomains</strong> verwendet wird, können Benutzer mit jeder Domäne kommunizieren, die nicht in der Liste der blockierten Domänen enthalten ist. Wenn das Cmdlet <strong>New-CsEdgeAllowList</strong> verwendet wird, können Benutzer nur mit Domänen kommunizieren, die der Liste der zulässigen Domänen hinzugefügt wurden.</p>
<p>Es ist zu beachten, dass Zeichenfolgenwerte nicht direkt an den Parameter <strong>AllowedDomains</strong> übergeben werden können. Stattdessen müssen Sie mit dem Cmdlet <strong>New-CsEdgeAllowList</strong> oder <strong>New-CsEdgeAllowAllKnownDomains</strong> einen Objektverweis erstellen und dann die Objektverweisvariable als Parameterwert verwenden.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowFederatedUsers</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Ist dieser Parameter auf <strong>True</strong> festgelegt (der Standardwert), ist es Benutzern möglicherweise erlaubt, mit Benutzern aus anderen Domänen zu kommunizieren. Ist dieser Parameter auf <strong>False</strong> festgelegt, können Benutzer nicht mit Benutzern aus anderen Domänen kommunizieren, und zwar unabhängig davon, welche Werte den Eigenschaften <strong>AllowedDomains</strong> und <strong>BlockedDomains</strong> zugewiesen sind.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPublicUsers</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Ist dieser Parameter auf <strong>True</strong> festgelegt (der Standardwert), ist es Benutzern möglicherweise erlaubt, mit Benutzern zu kommunizieren, die Konten bei öffentlichen Instant Messaging- und Anwesenheitsanbietern wie Windows Live, Yahoo! und AOL haben. Die Sammlung der öffentlichen Anbieter, mit denen Benutzer tatsächlich kommunizieren können, wird mit dem Cmdlet <strong>Set-CsTenantPublicProvider</strong> verwaltet.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockedDomains</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Wenn die Eigenschaft <strong>AllowedDomains</strong> auf <strong>AllowAllKnownDomains</strong> festgelegt ist, dürfen Benutzer mit Benutzern aus allen Domänen mit Ausnahme der Domänen kommunizieren, die in der Liste der blockierten Domänen enthalten sind. Ist die Eigenschaft <strong>AllowedDomains</strong> nicht auf <strong>AllowAllKnownDomains</strong> festgelegt, wird die Liste der blockierten Domänen ignoriert, und Benutzer können mit den Domänen kommunizieren, die explizit der Liste der zulässigen Domänen hinzugefügt wurden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie zu einer Bestätigung auf, bevor der Befehl ausgeführt wird.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Gibt die Sammlung der zu ändernden Verbundkonfigurationseinstellungen eines Mandaten an. Da es für jeden Mandanten nur eine einzige globale Sammlung von Verbundeinstellungen geben kann, ist nicht erforderlich, diesen Parameter einzufügen, wenn das Cmdlet <strong>Set-CsTenantFederationConfiguration</strong> aufgerufen wird. Wenn Sie den Parameter <strong>Identity</strong> verwenden, müssen Sie auch den Parameter <strong>Tenant</strong> einfügen. Beispiel:</p>
<p>Set-CsTenantFederationConfiguration -Tenant &quot;bf19b7db-6960-41e5-a139-2aa373474354&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Ermöglicht Ihnen, einen Verweis auf ein Objekt an das Cmdlet zu übergeben, statt einzelne Parameterwerte festzulegen.</p></td>
</tr>
<tr class="odd">
<td><p><em>SharedSipAddressSpace</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>Ist dieser Parameter auf <strong>True</strong> festgelegt, gibt er an, dass für Benutzer, die in Lync Online verwaltet werden, dieselbe SIP-Domäne verwendet wird wie für Benutzer, die in der lokalen Version von Lync Server verwaltet werden. Der Standardwert ist <strong>False</strong>, d. h., die beiden Benutzergruppen haben unterschiedliche SIP-Domänen.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Guid</p></td>
<td><p>GUID des Mandantenkontos, dessen Verbundeinstellungen geändert werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Wenn Sie eine Remotesitzung von Windows PowerShell verwenden und nur eine Verbindung mit Skype for Business Online hergestellt haben, müssen Sie den Parameter <strong>Tenant</strong> nicht einfügen. Stattdessen wird die Mandanten-ID automatisch anhand Ihrer Verbindungsinformationen für Sie eingetragen. Der Parameter <strong>Tenant</strong> ist hauptsächlich zur Verwendung in einer Hybridbereitstellung vorgesehen.</p></td>
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

Das Cmdlet **Set-CsTenantFederationConfiguration** akzeptiert weitergeleitete Instanzen des Objekts **Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings**.

## Rückgabetypen

Keine. Stattdessen werden mit dem Cmdlet **Set-CsTenantFederationConfiguration** vorhandene Instanzen des Objekts **Microsoft.Rtc.Management.WritableConfig.Settings.Edge.TenantFederationSettings** geändert.

## Siehe auch

#### Weitere Ressourcen

[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

