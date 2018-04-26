---
title: Einführung in Windows PowerShell und Lync Online
TOCTitle: Einführung in Windows PowerShell und Lync Online
ms:assetid: 4b4cf534-c950-4d6c-abd9-d3d0e6f53bb7
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362785(v=OCS.15)
ms:contentKeyID: 56269269
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Einführung in Windows PowerShell und Lync Online

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Windows PowerShell ist eine Befehlsshell und eine Skriptsprache und kann verwendet werden, um Skype for Business Online zu verwalten. Anstelle des grafisch orientierten Skype for Business Online Admin Centers können Sie alternativ auch dieses Produkt nutzen, um Skype for Business Online mithilfe von Befehlszeilenbefehlen wie dem folgenden zu verwalten:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Neben der Ausführung von einfachen Befehlen wie im vorstehenden Beispiel (der Informationen über den Benutzer mit dem UPN "kenmyer@litwareinc.com" zurückgibt), können Benutzer, die mit Windows PowerShell bereits vertraut sind, diese Befehle auch zu Skripts zusammenfassen. Mit diesen Skripts können Prozesse automatisiert und/oder sich wiederholende Aufgaben ausgeführt werden.

Generell gilt, dass Sie für jede Aufgabe, die Sie im Skype for Business Online Admin Center erledigen können, auch Windows PowerShell verwenden können. So können Sie im Admin Center beispielsweise Mobiltelefonbenachrichtigungen, so genannte *Pushbenachrichtigungen*, verwalten. Mit Pushbenachrichtigungen können Sie Benachrichtigungen zu Ereignissen (z. B. dem Empfang von neuen Chatnachrichten oder neuen Sprachnachrichten) an mobile Geräte wie iPhones und Windows Phones senden. Diese Benachrichtigungen können auf dem mobilen Gerät auch dann empfangen werden, wenn die Lync-Anwendung auf dem Gerät gerade im Hintergrund ausgeführt wird.

Wie werden Pushbenachrichtigungen verwaltet? Eine Möglichkeit besteht darin, das Skype for Business Online Admin Center zu verwenden, in dem Sie Pushbenachrichtigungen aktivieren oder deaktivieren können, indem Sie auf der Registerkarte **Organization** die geeignete Option auswählen:

![LyncOnlinePowerShell\_Push\_Notifications](images/Dn362785.0a6ec1f5-1999-427f-880b-0587c98d7670(OCS.15).png "LyncOnlinePowerShell_Push_Notifications")

Sie können Pushbenachrichtigungen aber auch über eine Windows PowerShell-Remotesitzung mit dem Cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) aktivieren oder deaktivieren. Mit dem folgenden Befehl werden Pushbenachrichtigungen beispielsweise für iPhones und Windows Phones deaktiviert:

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Wie Sie sehen, entsprechen die Parameter (d. h. **EnableApplePushNotificationService** und **EnableMicrosoftPushNotificationService**), die in Verbindung mit dem Cmdlet **Set-CsPushNotificationConfiguration** verwendet werden, den im Skype for Business Online Admin Center verfügbaren Optionen:

![Verbindung zwischen Lync-Optionen/PS-Cmdlet](images/Dn362785.f20086fd-3b51-4bbf-8d81-e643d9bf3a2e(OCS.15).png "Verbindung zwischen Lync-Optionen/PS-Cmdlet")

Unter dem Strich können Sie entweder das Admin Center oder ein Windows PowerShell-Cmdlet und die geeigneten Parameter verwenden, um Pushbenachrichtigungen zu verwalten. Beide Vorgehensweisen funktionieren, und beide Vorgehensweisen funktionieren gleich gut.


> [!TIP]
> Die Definitionen von bestimmten Windows PowerShell-Begriffen, wie <EM>Cmdlet</EM>, <EM>Parameter</EM>, <EM>Parameterwert</EM> und <EM>Argument</EM> finden Sie unter <A href="windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md">Windows PowerShell-Cmdlets, -Parameter und Parameterwerte</A>.



Damit stellt sich eine offensichtliche Frage: Wenn das Skype for Business Online Admin Center und Windows PowerShell exakt die gleichen Funktionen bieten, warum sollte ich dann das eine dem anderen vorziehen? Was das betrifft, warum sollten Sie sich jemals die Mühe machen, Befehle in Windows PowerShell einzugeben, wenn es doch so einfach ist, einfach die entsprechenden Kontrollkästchen im Admin Center zu aktivieren oder zu deaktivieren?

In einem so einfachen Fall wie im vorstehenden Beispiel ist es einfach eine Frage der persönlichen Vorliebe, welche Vorgehensweise Sie verwenden: Einige Personen bevorzugen eine grafische Benutzeroberfläche, andere arbeiten lieber mit einem Befehlszeilentool wie Windows PowerShell. In einige Fällen bietet Windows PowerShell jedoch die effizienteste oder gar die einzige Möglichkeit, eine Verwaltungsaufgabe zu erledigen. So können Sie im Skype for Business Online Admin Center beispielsweise Besprechungseinladungen anpassen:

![Lync Admin Center: Einstellungen für Besprechungseinladung](images/Dn362785.3fb00c33-0bd4-46dd-beb1-8f71e24cf630(OCS.15).png "Lync Admin Center: Einstellungen für Besprechungseinladung")

Dieselben Anpassungen können Sie auch mit dem Cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) vornehmen. Allerdings bietet das Cmdlet **Set-CsMeetingConfiguration** zusätzliche Optionen, die im Skype for Business Online Admin Center nicht verfügbar sind. Ein Beispiel: Wenn eine Person in Ihrer Organisation an einer Besprechung teilnimmt, wird diese Person standardmäßig und automatisch als Besprechungsreferent konfiguriert. Diese Einstellung kann mit dem Skype for Business Online Admin Center nicht geändert werden. Dies ist nur mit Windows PowerShell und dem Cmdlet **Set-CsMeetingConfiguration** möglich. Genauer gesagt, legt dieser Befehl die Eigenschaft **DesignateAsPresenter** auf **None** fest, was bedeutet, dass nur der Besprechungsorganisator als Referent konfiguriert wird, wenn er der Besprechung beitritt:

    Set-CsMeetingConfiguration -DesignateAsPresenter "Everyone"

Weitere Einzelheiten zur Nutzung von Windows PowerShell finden Sie unter den folgenden Themen:

  - [Windows PowerShell-Cmdlets, -Parameter und Parameterwerte](windows-powershell-cmdlets-parameters-and-parameter-values-in-skype-for-business-online.md)

  - [Arbeiten mit Parametern](working-with-parameters-in-skype-for-business-online.md)

  - [Obligatorische und optionale Parameter](mandatory-and-optional-parameters-in-skype-for-business-online.md)

  - [Parameter im Vergleich zu Eigenschaften](parameters-vs-properties-in-skype-for-business-online.md)

  - [Kombinieren von Lync Online-Cmdlets mit anderen Windows PowerShell-Cmdlets](combining-skype-for-business-online-cmdlets-with-other-windows-powershell-cmdlets-in.md)

  - [Weitere Hilfe für das Arbeiten mit Windows PowerShell](more-help-for-using-windows-powershell-in-skype-for-business-online.md)

