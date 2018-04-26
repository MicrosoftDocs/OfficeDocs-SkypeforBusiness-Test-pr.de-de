---
title: Fehler beim Herstellen der Verbindung zum Live ID-Server
TOCTitle: Fehler beim Herstellen der Verbindung zum Live ID-Server
ms:assetid: 701af721-dd6a-4f48-96f9-94e89c644201
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362811(v=OCS.15)
ms:contentKeyID: 56269300
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Fehler beim Herstellen der Verbindung zum Live ID-Server

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

In der Regel gibt es drei Gründe, warum ein Verbindungsversuch mit der folgenden Fehlermeldung fehlschlägt:

    Get-CsWebTicket : Fehler beim Herstellen einer Verbindung mit Live ID-Servern. Stellen Sie sicher, dass der Proxy aktiviert ist und der Computer eine Netzwerkverbindung mit Live ID-Servern herstellen kann.

Diese Fehlermeldung bedeutet oft, dass der Microsoft Online Services-Anmelde-Assistent nicht ausgeführt wird. Sie können den Status des Diensts überprüfen, indem Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung eingeben:

    Get-Service "msoidsvc"

Wenn der Dienst nicht ausgeführt wird, starten Sie ihn mit diesem Befehl:

    Start-Service "msoidsvc"

Wenn der Dienst ausgeführt wird, gibt es möglicherweise Probleme mit der Netzwerkverbindung zwischen Ihrem Computer und dem Microsoft Live ID-Authentifizierungsserver. Um diese zu überprüfen, öffnen Sie Internet Explorer, und navigieren Sie zu <https://login.microsoftonline.com/.> Versuchen Sie, sich von dort aus bei Office 365 anzumelden. Wenn der Versuch fehlschlägt, liegen wahrscheinlich Probleme mit der Netzwerkverbindung vor.

In seltenen Fällen ist es möglich, dass der Verbindungs-URI für den Microsoft Live ID-Authentifizierungsserver mit einem falschen Wert konfiguriert wurde. Wenn Sie bereits festgestellt haben, dass der Anmelde-Assistent ausgeführt wird und dass keine Probleme mit der Netzwerkverbindung vorliegen, könnte dies das Problem sein. Kontaktieren Sie in diesem Fall den Office 365-Support.

## Siehe auch

#### Konzepte

[Diagnostizieren und Beheben von Problemen mit Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

