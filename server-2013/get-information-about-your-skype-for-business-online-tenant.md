---
title: Abrufen von Informationen über Ihren Lync Online-Mandanten
TOCTitle: Abrufen von Informationen über Ihren Lync Online-Mandanten
ms:assetid: 06467515-9114-45bb-8d09-26a915c3fc4d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362768(v=OCS.15)
ms:contentKeyID: 56269247
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abrufen von Informationen über Ihren Lync Online-Mandanten

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie Informationen über Ihren Skype for Business Online-Mandanten abrufen möchten, verwenden Sie das Cmdlet [Get-CsTenant](get-cstenant.md) ohne zusätzliche Parameter:

    Get-CsTenant

Wenn Sie nur den Mandatennamen und die ID abrufen möchten (der Wert des Parameters **TenantID** ist für die Ausführung von Cmdlets wie [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) und [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) erforderlich), verwenden Sie diesen Befehl:

    Get-CsTenant | Select-Object Name, TenantID

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

