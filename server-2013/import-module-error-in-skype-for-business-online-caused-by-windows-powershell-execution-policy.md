---
title: Von der Windows PowerShell-Ausführungsrichtlinie verursachter Fehler des Importmoduls
TOCTitle: Von der Windows PowerShell-Ausführungsrichtlinie verursachter Fehler des Importmoduls
ms:assetid: 4bc093ca-fd30-44c9-a0a3-16f78698df2b
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362786(v=OCS.15)
ms:contentKeyID: 56269268
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Von der Windows PowerShell-Ausführungsrichtlinie verursachter Fehler des Importmoduls

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Die Windows PowerShell-Ausführungsrichtlinie hilft bei der Feststellung, welche Konfigurationsdateien in die Windows PowerShell-Konsole geladen und welche Skripts der Benutzer über die Konsole ausführen kann. Zumindest kann das Skype for Business Online-Connectormodul erst importiert werden, wenn die Ausführungsrichtlinie auf **RemoteSigned** festgelegt wurde. Andernfalls erhalten Sie bei dem Versuch, das Modul zu importieren, die folgende Fehlermeldung:

    Import-Module : Die Datei "C:\Program Files\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnectorStartup.psm1" kann nicht geladen werden, da die Ausführung von Skripts auf diesem System deaktiviert ist. Weitere Informationen finden Sie unter "about_Execution_Policies" (http://go.microsoft.com/fwlink/?LinkID=135170).

Zur Lösung dieses Problems starten Sie Windows PowerShell als Administrator und führen dann den folgenden Befehl aus:

    Set-ExecutionPolicy RemoteSigned

Details zur Ausführungsrichtlinie finden Sie im zugehörigen Hilfethema an [http://go.microsoft.com/fwlink/?LinkID=135170](http://go.microsoft.com/fwlink/?linkid=135170).

## Siehe auch

#### Konzepte

[Diagnostizieren und Beheben von Problemen mit Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

