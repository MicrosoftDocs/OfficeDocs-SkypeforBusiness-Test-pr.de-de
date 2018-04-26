---
title: Fehler des Importmoduls aufgrund einer ungeeigneten Version von Windows PowerShell
TOCTitle: Fehler des Importmoduls aufgrund einer ungeeigneten Version von Windows PowerShell
ms:assetid: 6c209f41-2b97-4dda-b0b7-e5b582d3e6b6
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362802(v=OCS.15)
ms:contentKeyID: 56269279
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Fehler des Importmoduls aufgrund einer ungeeigneten Version von Windows PowerShell

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Das Skype for Business Online-Connectormodul kann nur unter Windows PowerShell 3.0 ausgeführt werden. Wenn Sie versuchen, das Modul unter einer älteren Version von Windows PowerShell zu importieren, schlägt der Importvorgang fehl, und es wird eine Fehlermeldung wie die folgende angezeigt:

    Import-Module : Die Version der geladenen PowerShell ist "2.0". Zum Ausführen des Moduls "D:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnector.psd1" ist mindestens Version 3.0 von PowerShell erforderlich. Überprüfen Sie die Installation von PowerShell, und wiederholen Sie den Vorgang.

Die einzige Möglichkeit zum Beheben des Problems besteht darin, Windows PowerShell 3.0 zu installieren. Die Anwendung steht im Microsoft Download Center an <http://www.microsoft.com/en-us/download/details.aspx?id=29939> zum Abruf bereit.

## Siehe auch

#### Konzepte

[Diagnostizieren und Beheben von Problemen mit Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

