---
title: Die maximale Anzahl von gleichzeitigen Shells für diesen Benutzer wurde überschritten
TOCTitle: Die maximale Anzahl von gleichzeitigen Shells für diesen Benutzer wurde überschritten
ms:assetid: b309efe8-a214-41ea-a345-93e6a36e0cb1
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362837(v=OCS.15)
ms:contentKeyID: 56269338
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Die maximale Anzahl von gleichzeitigen Shells für diesen Benutzer wurde überschritten

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Für jeden Administrator darf es bis zu drei gleichzeitige Remoteverbindungen mit Skype for Business Online geben. Wenn Sie drei aktive Remoteverbindungen mit Windows PowerShell haben, wird für jeden Versuch, eine vierte gleichzeitige Verbindung herzustellen, die folgende Fehlermeldung angezeigt:

    New-PSSession : [admin.vdomain.com] Beim Verbinden mit dem Remoteserver "admin.vdomain.com" ist folgender Fehler aufgetreten: Die Anforderung kann vom WS-Verwaltungsdienst nicht verarbeitet werden. Die maximale Anzahl von gleichzeitigen Shells für diesen Benutzer wurde überschritten. Schließen Sie bestehende Shells, oder erhöhen Sie die Quote für diesen Benutzer. Weitere Informationen finden Sie im Hilfethema "about_Remote_Troubleshooting".

Dieses Problem lässt sich nur dadurch beheben, dass Sie mindestens eine der aktiven Verbindungen schließen. Wenn Sie eine Skype for Business Online-Sitzung abgeschlossen haben, empfiehlt es sich, die Sitzung mit dem Cmdlet **Remove-PSSession** zu beenden. Damit kann dieses Problem verhindert werden.

## Siehe auch

#### Konzepte

[Diagnostizieren und Beheben von Problemen mit Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

