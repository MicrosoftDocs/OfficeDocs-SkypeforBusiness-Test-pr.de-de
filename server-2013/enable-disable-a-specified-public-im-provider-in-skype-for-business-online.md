---
title: Aktivieren/Deaktivieren eines bestimmten Anbieters von öffentlichen Instant Messaging-Diensten
TOCTitle: Aktivieren/Deaktivieren eines bestimmten Anbieters von öffentlichen Instant Messaging-Diensten
ms:assetid: 9d3e2607-01c0-4ae9-accc-39f03ce253bb
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362825(v=OCS.15)
ms:contentKeyID: 56269316
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aktivieren/Deaktivieren eines bestimmten Anbieters von öffentlichen Instant Messaging-Diensten

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Mit Skype for Business Online können Sie den Partnerverbund mit Benutzer von einem oder mehreren der folgenden Anbieter von öffentlichen Instant Messaging-Diensten einrichten:

  - Windows Live-Netzwerk der Internetdienste

  - Yahoo\!

  - AOL

Um den Partnerverbund mit einem oder mehreren dieser Anbieter zuzulassen, verwenden Sie das Cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) und legen den Wert der Eigenschaft **Provider** auf einen oder mehrere der folgenden Werte fest:

  - Windows Live

  - Yahoo\!

  - AOL

Mit diesem Befehl wird beispielsweise der Partnerverbund mit Windows Live und AOL eingerichtet:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Beachten Sie, dass Sie jedes Mal alle relevanten Anbieter in den Befehl einschließen müssen, wenn Sie einen Anbieter hinzufügen oder entfernen möchten. Mit dem folgenden Befehl können Sie beispielsweise Yahoo\! hinzufügen:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo"

Dieser Befehl sorgt dafür, dass Yahoo\! der einzige Partnerverbundanbieter ist, da im Befehl nur dieser Anbieter angegeben wurde. Wenn Sie den Partnerverbund mit allen drei Anbietern von öffentlichen Instant Messaging-Diensten einrichten möchten, müssen Sie auch alle drei Anbieter einschließen:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo", "AOL","WindowsLive"

Beachten Sie zudem, dass Sie beim Aufruf des Cmdlets **Set-CsTenantPublicProvider** den Parameter **Tenant** einschließen müssen. Andernfalls werden Sie aufgefordert, die Mandanten-ID einzugeben. Sie können die Mandanten-ID Ihres Skype for Business Online-Mandanten mit dem folgenden Befehl abrufen:

    Get-CsTenant | Select-Object TenantID

Alternativ können Sie auch diesen Befehl verwenden, um die Mandanten-ID in einer Variablen zu speichern:

    $tenantID = (Get-CsTenant | Select-Object TenantID)

Anschließend können Sie die Variable (in diesem Beispiel **$tenantID**) beim Aufruf von **Set-CsTenantPublicProvider** verwenden:

    Set-CsTenantPublicProvider -Tenant $tenantID -Provider "Yahoo", "AOL","WindowsLive"

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

