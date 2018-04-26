---
title: Parameter im Vergleich zu Eigenschaften
TOCTitle: Parameter im Vergleich zu Eigenschaften
ms:assetid: 65348f95-f4d4-40cd-8869-f9d72643792d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362796(v=OCS.15)
ms:contentKeyID: 56269297
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Parameter im Vergleich zu Eigenschaften

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Bei der Durchsicht der Hilfethemen zu den Skype for Business Online-Cmdlets werden Sie feststellen, dass die Begriffe *Parameter* und *Eigenschaft* abwechselnd verwendet werden. Lassen Sie sich davon nicht verwirren: Obwohl es technisch gesehen einen Unterschied gibt, beziehen sich die Begriffe in Skype for Business Online im Wesentlichen auf das gleiche Konzept.

Im technischen Sinne werden Parameter verwendet, um ein Cmdlet auszuführen. Im folgenden Windows PowerShell-Befehl sind **EnableMicrosoftPushNotificationService** und **EnableApplePushNotificationService** Parameter des Cmdlets [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) cmdlet:

    Set-CsPushNotificationConfiguration -EnableMicrosoftPushNotificationService -EnableApplePushNotificationService $True

Eine Eigenschaft ist hingegen ein Attribut eines Skype for Business Online-Objekts (z. B. eine Auflistung von Konfigurationseinstellungen für Pushbenachrichtigungen). Einmal angenommen, Sie führen den folgenden Befehl aus:

    Set-CsPushNotificationConfiguration

Hiermit erhalten Sie eine Auflistung von Eigenschaften und der zugehörigen Werte, zu denen die folgenden Elemente gehören:

    EnableMicrosoftPushNotificationService : True
    EnableApplePushNotificationService     : True

Wie Sie hier sehen, tragen Eigenschaften und Parameter den gleichen Namen: Sie können den Parameter **EnableMicrosoftPushNotificationService** verwenden, um den Wert der Eigenschaft **EnableMicrosoftPushNotificationService** zu konfigurieren.

## Siehe auch

#### Konzepte

[Einführung in Windows PowerShell und Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

