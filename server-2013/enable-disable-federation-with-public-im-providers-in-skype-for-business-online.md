---
title: Aktivieren/Deaktivieren des Partnerverbunds mit öffentlichen Instand Messaging-Anbietern
TOCTitle: Aktivieren/Deaktivieren des Partnerverbunds mit öffentlichen Instand Messaging-Anbietern
ms:assetid: 8609682c-97d3-48e6-a243-d84c1f9c8419
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362809(v=OCS.15)
ms:contentKeyID: 56269303
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aktivieren/Deaktivieren des Partnerverbunds mit öffentlichen Instand Messaging-Anbietern

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie dafür sorgen möchten, dass Ihre Benutzer mit Benutzern kommunizieren können, die über Konten bei öffentlichen Instant Messaging-Anbietern verfügen, verwenden Sie das Cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) und legen die Eigenschaft **AllowPublicUsers** auf **True** ($True) fest:

    Set-CsTenantFederationConfiguration -AllowPublicUsers $True

Anschließend müssen Sie mit dem Cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) die öffentlichen Instant Messaging-Anbieter angeben, mit denen die Kommunikation zulässig sein soll.

Zum Deaktivieren des Partnerverbunds mit öffentlichen IM-Anbietern legen Sie die Eigenschaft **AllowPublicUsers** wieder auf **False** ($False) fest:

    Set-CsTenantFederationConfiguration -AllowPublicUsers $False

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

