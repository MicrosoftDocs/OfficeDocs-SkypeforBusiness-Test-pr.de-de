---
title: Get-CsTenantPublicProvider
TOCTitle: Get-CsTenantPublicProvider
ms:assetid: 0d949ec2-206d-4979-a3be-a5578ae93ed3
ms:mtpsurl: https://technet.microsoft.com/de-de/library/JJ994016(v=OCS.15)
ms:contentKeyID: 52056285
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenantPublicProvider

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zurück, die darauf hinweisen, ob Microsoft Lync Online-Benutzer mit Personen kommunizieren dürfen, die über Konten bei den Drittanbieter-Chat- und -Anwesenheitsanbietern Windows Live, AOL und Yahoo verfügen.

Dieses Cmdlet kann nur in Verbindung mit Skype for Business Online verwendet werden.

## Syntax

    Get-CsTenantPublicProvider -Tenant <String> [-Verbose]

## Beispiele

## Beispiel 1

Der Befehl in Beispiel 1 gibt Informationen zum öffentlichen Anbieter für den Mandanten mit der Mandanten-ID "bf19b7db-6960-41e5-a139-2aa373474354" zurück.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Der Parameter "Tenant" ist optional. Sie können das Cmdlet "Get-CsTenantPublicProvider" auch mit der folgenden Syntax aufrufen:

    Get-CsTenantPublicProvider

## Beispiel 2

Der vorstehende Befehl gibt ausführliche Informationen zum Status aller öffentlichen Anbieter zurück, die dem Mandanten "bf19b7db-6960-41e5-a139-2aa373474354" zugeordnet sind. Dafür verwendet der Befehl zunächst das Cmdlet **Get-CsTenantPublicProvider**, um Informationen zu öffentlichen Anbietern für den angegebenen Mandanten zurückzugeben. Diese Informationen werden dann an das Cmdlet **Select-Object** weitergeleitet, das den Parameter "ExpandProperty" verwendet, um den Wert der Eigenschaft "DomainPICStatus" zu "erweitern". Das Erweitern einer Eigenschaft bedeutet einfach, dass alle in dieser Eigenschaft gespeicherten Werte in einem einfach zu lesenden Format auf dem Bildschirm angezeigt werden.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Ein solcher Befehl würde in einer hybriden Bereitstellung von Lync Server 2013 verwendet werden.

## Beispiel 3

Der Befehl in Beispiel 3 ist eine Variante des Befehls in Beispiel 2. In Beispiel 3 werden die durch die "Erweiterung" der Eigenschaft "DomainPICStatus" zurückgegebenen Informationen zu öffentlichen Anbietern jedoch wiederum an das Cmdlet **Where-Object** weitergeleitet. Das Cmdlet **Where-Object** sucht dann nur die Anbieter heraus, deren Eigenschaft "Status" auf "Enabled" festgelegt ist. Im Endeffekt werden damit nur die öffentlichen Anbieter angezeigt, die zur Verwendung aktiviert sind.

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus | Where-Object {$_.Status -eq "Enabled"}

## Detaillierte Beschreibung

Öffentliche Anbieter sind Organisationen, die SIP-Kommunikationsdienste für die breite Öffentlichkeit bieten. Wenn Sie eine Partnerverbundbeziehung mit einem öffentlichen Anbieter einrichten, stellen Sie im Prinzip einen Partnerverbund mit allen Benutzern her, deren Konto von diesem Anbieter gehostet wird. Bei einem Partnerverbund mit Windows Live können Benutzer beispielsweise Chatnachrichten und Anwesenheitsinformationen mit allen anderen Benutzern austauschen, die über ein Windows Live-Chatkonto verfügen.

Mit Lync Online können Administratoren einen Partnerverbund mit einem oder mehreren der folgenden öffentlichen Chat- und Anwesenheitsanbieter konfigurieren:

  - Windows Live

  - AOL

  - Yahoo\!

Administratoren können mit dem Cmdlet **Get-CsTenantPublicProvider** bestimmen, welche dieser Anbieter (wenn überhaupt) für einen Partnerverbund aktiviert wurden. Wenn Sie das Cmdlet **Get-CsTenantPublicProvider** aufrufen, erhalten Sie Informationen wie die folgenden zurück:

    PublicProviderSet     DomainPicStatus
    ------------------    ------------------------
    True                  {Microsoft.Rtc.Management.Hosted.DomainPICStatus}

Die Eigenschaft "PublicProviderSet" gibt an, ob ein Partnerverbund für einen oder mehrere öffentliche Anbieter aktiviert wurde. Wenn "PublicProviderSet" auf "True" festgelegt ist, wurde ein Partnerverbund mit mindestens einem Anbieter aktiviert. Bei Festlegung auf "False" wurde der Partnerverbund für alle drei öffentlichen Anbieter (Windows Live, AOL und Yahoo) deaktiviert. Verwenden Sie den folgenden Befehl, um den tatsächlichen Status jedes Anbieters zu bestimmen:

    Get-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" | Select-Object -ExpandProperty DomainPICStatus

Beachten Sie, dass das reine Aktivieren des Status eines öffentlichen Anbieters nicht bedeutet, dass Benutzer Chatnachrichten und Anwesenheitsinformationen mit Benutzern austauschen können, die über ein Konto bei diesem Anbieter verfügen. Neben der Aktivierung des Partnerverbunds mit dem Anbieter selbst müssen Administratoren auch die Eigenschaft "AllowPublicUsers" der Konfigurationseinstellungen für den Partnerverbund auf "True" festlegen. Wenn diese Eigenschaft auf "False" festgelegt ist, ist keine Kommunikation mit den öffentlichen Anbietern zulässig, unabhängig von den Konfigurationseinstellungen für öffentliche Anbieter.

Weitere Informationen finden Sie in dem Hilfethema zum **Set-CsTenantFederationConfiguration**-Cmdlet.

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
<td><p><em>Tenant</em></p></td>
<td><p>Erforderlich</p></td>
<td><p>System.String</p></td>
<td><p>GUID des Mandantenkontos, dessen Einstellungen für öffentliche Anbieter zurückgegeben werden. Beispiel:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Sie können die Mandanten-ID für all Ihre Mandanten zurückgeben, indem Sie diesen Befehl ausführen:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Wenn Sie eine Remotesitzung von Windows PowerShell verwenden und nur eine Verbindung mit Skype for Business Online hergestellt haben, müssen Sie den Parameter <strong>Tenant</strong> nicht einfügen. Stattdessen wird die Mandanten-ID automatisch anhand Ihrer Verbindungsinformationen für Sie eingetragen. Der Parameter <strong>Tenant</strong> ist hauptsächlich zur Verwendung in einer Hybridbereitstellung vorgesehen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsTenantPublicProvider** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Das Cmdlet **Get-CsTenantPublicProvider** gibt Instanzen des Objekts "Microsoft.Rtc.Management.Hosted.TenantPICStatus" zurück.

## Siehe auch

#### Weitere Ressourcen

[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md)

