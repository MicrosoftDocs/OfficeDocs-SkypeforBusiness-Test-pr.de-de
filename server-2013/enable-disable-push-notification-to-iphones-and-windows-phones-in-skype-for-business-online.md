---
title: Aktivieren/Deaktivieren von Pushbenachrichtigungen an iPhones und Windows Phones
TOCTitle: Aktivieren/Deaktivieren von Pushbenachrichtigungen an iPhones und Windows Phones
ms:assetid: 64482dcb-6354-4fb5-a2e4-1564b3d0e047
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362792(v=OCS.15)
ms:contentKeyID: 56269296
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aktivieren/Deaktivieren von Pushbenachrichtigungen an iPhones und Windows Phones

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Um Pushbenachrichtigungen zu deaktivieren, die an iPhones oder Windows Phones gesendet werden, verwenden Sie das Cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) und legen die Werte der Eigenschaften **EnableApplePushNotificationService** und **EnableMicrosoftPushNotificationService** auf **False** ($False) fest:

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Die Einstellungen für iPhones und Windows Phones können unabhängig voneinander festgelegt werden. Mit dem folgenden Befehl werden Pushbenachrichtigungen beispielsweise für iPhones deaktiviert und für Windows Phones aktiviert:

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $True

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

