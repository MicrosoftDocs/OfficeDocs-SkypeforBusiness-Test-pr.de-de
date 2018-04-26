---
title: Automatisches Herstellen der Verbindung zu Lync Online bei jedem Start von Windows PowerShell
TOCTitle: Automatisches Herstellen der Verbindung zu Lync Online bei jedem Start von Windows PowerShell
ms:assetid: 68f76c36-5dd6-48ea-b19a-d65593199e4c
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362799(v=OCS.15)
ms:contentKeyID: 56269286
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Automatisches Herstellen der Verbindung zu Lync Online bei jedem Start von Windows PowerShell

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie sich nicht alle Befehle merken können, die für die Herstellung der Verbindung zu Skype for Business Online erforderlich sind, können Sie die Oberfläche so konfigurieren, dass Sie lediglich auf eine Verknüpfung doppelklicken und Ihr Skype for Business Online-Kennwort eingeben müssen, um im Handumdrehen mit Skype for Business Online verbunden zu werden.

Starten Sie hierzu im ersten Schritt den Windows Editor (oder einen beliebigen anderen Texteditor), und fügen Sie dann die folgenden Befehle ein, wobei Sie statt "kenmyer@litwareinc.com" Ihren Skype for Business Online-Kontonamen eingeben:

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $session = New-CsOnlineSession -Credential $credential 
    Import-PSSession $session

Speichern Sie die Datei mit der Erweiterung "PS1" (z. B. "C:\\Skripts\\LyncOnline.ps1").

Führen Sie nach dem Speichern der Datei die folgenden Schritte durch, um eine Verknüpfung auf dem Desktop zu erstellen, mit der Windows PowerShell gestartet und das Skript beim Start ausgeführt wird:

1.  Klicken Sie mit der rechten Maustaste auf den Desktop, klicken Sie auf **Neu**, und klicken Sie dann auf **Verknüpfung**.

2.  Geben Sie im Assistenten zum Erstellen von Verknüpfungen Folgendes in das Feld **Geben Sie den Speicherort des Elements ein** ein, und klicken Sie dann auf **Weiter** (denken Sie daran, den Pfad zu der Skriptdatei anzugeben, die Sie soeben erstellt haben):
    
        powershell.exe -noexit C:\Scripts\LyncOnline.ps1

3.  Geben Sie im Feld **Geben Sie den Namen für die Verknüpfung ein** einen Namen für die Verknüpfung ein (z. B. **Skype for Business Online**), und klicken Sie dann auf **Fertig stellen**.

4.  Wenn Sie das nächste Mal Windows PowerShell verwenden möchten, um Skype for Business Online zu verwalten, doppelklicken Sie einfach auf die neue Verknüpfung, und geben Sie Ihr Kennwort ein. Das Skript sorgt dafür, dass die Verbindung hergestellt und eine neue Remotesitzung eingerichtet wird.

Diese neue Sitzung wird normalerweise nicht in der Variablen $session gespeichert. Sie erhält stattdessen in der Regel die Sitzungs-ID 1. Dies hat keinerlei Auswirkungen auf Ihre Sitzung, zumindest nicht bis zum Schließen der Sitzung. Hierbei müssen Sie nämlich auf die Sitzungs-ID verweisen, wenn Sie das Cmdlet **Remove-PSSession** aufrufen:

    Remove-PSSession 1

Sie können die Ihrer Skype for Business Online-Sitzung zugewiesene ID überprüfen, indem Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung eingeben:

    Get-PSSession

## Siehe auch

#### Konzepte

[Konfigurieren eines Computers für Lync Online-Verwaltung](configuring-your-computer-for-skype-for-business-online-management.md)

