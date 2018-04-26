---
title: Die maximale Anzahl von gleichzeitigen Shells für diesen Mandanten wurde überschritten
TOCTitle: Die maximale Anzahl von gleichzeitigen Shells für diesen Mandanten wurde überschritten
ms:assetid: a4c91ffa-fdcc-414c-b941-a0d36c906825
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362832(v=OCS.15)
ms:contentKeyID: 56269325
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Die maximale Anzahl von gleichzeitigen Shells für diesen Mandanten wurde überschritten

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Zwar darf jeder Administrator bis zu drei gleichzeitige Verbindungen mit einem Skype for Business Online-Mandanten haben, aber jeder Mandant darf maximal neun gleichzeitige Verbindungen haben. Nehmen Sie beispielsweise an, drei Administratoren haben jeweils drei aktive Sitzungen. Wenn ein vierter Administrator versucht, eine Verbindung herzustellen (wodurch sich insgesamt 10 gleichzeitige Verbindungen ergeben würden), schlägt dieser Versuch mit der folgenden Fehlermeldung fehl:

    New-PSSession : [admin.vdomain.com] Beim Verbinden mit dem Remoteserver "admin.vdomain.com" ist folgender Fehler aufgetreten: Die Anforderung kann vom WS-Verwaltungsdienst nicht verarbeitet werden. Die maximale Anzahl von gleichzeitigen Shells für diesen Mandanten wurde überschritten. Schließen Sie bestehende Shells, oder erhöhen Sie die Quote für diesen Mandanten. Weitere Informationen finden Sie im Hilfethema "about_Remote_Troubleshooting".

Dieses Problem lässt sich nur dadurch beheben, dass Sie mindestens eine der aktiven Verbindungen schließen. Wenn Sie eine Skype for Business Online-Sitzung abgeschlossen haben, empfiehlt es sich, diese Sitzung mit dem Cmdlet **Remove-PSSession** zu beenden. Damit kann dieses Problem verhindert werden.

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

