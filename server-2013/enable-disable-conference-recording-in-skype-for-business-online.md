---
title: Aktivieren/Deaktivieren von Konferenzaufzeichnung
TOCTitle: Aktivieren/Deaktivieren von Konferenzaufzeichnung
ms:assetid: f6c5afab-081c-495c-97f7-135dcc2f6085
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362857(v=OCS.15)
ms:contentKeyID: 56269355
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aktivieren/Deaktivieren von Konferenzaufzeichnung

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie nicht möchten, dass Benutzer die Möglichkeit haben, Onlinekonferenzen aufzuzeichnen, legen Sie mit dem Cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) den Wert des Parameters **AllowConferenceRecording** auf **False** ($False) fest:

    Set-CsMeetingConfiguration -AllowConferenceRecording $False

Wenn Sie die Möglichkeit zum Aufzeichnen von Onlinekonferenzen wiederherstellen möchten, legen Sie den Wert des Parameters **AllowConferenceRecording** auf **True** ($True) fest:

    Set-CsMeetingConfiguration -AllowConferenceRecording $True

## Siehe auch

#### Konzepte

[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

