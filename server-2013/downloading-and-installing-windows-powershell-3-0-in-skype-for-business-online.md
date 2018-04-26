---
title: 'Lync Online: Herunterladen und Installieren von Windows PowerShell 3.0'
TOCTitle: Herunterladen und Installieren von Windows PowerShell 3.0
ms:assetid: 39ae065d-02d7-4ce3-9e6f-6ad550a1777e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362783(v=OCS.15)
ms:contentKeyID: 56269262
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Herunterladen und Installieren von Windows PowerShell 3.0 in Lync Online

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Wenn Sie mit Windows Server 2012, Windows Server 2012 R2, Windows 8, oder Windows 8.1 arbeiten, sollten Sie bereits über Windows PowerShell 3.0 verfügen, da die Anwendung zusammen mit diesen Betriebssystemen installiert wird.

Wenn Sie Windows 7 oder Windows Server 2008 R2 verwenden, kann es ebenfalls sein, dass Windows PowerShell 3.0 bereits installiert ist. Es ist aber auch möglich, dass Sie noch mit Version 2.0 arbeiten, der Version, die seinerzeit mit den Betriebssystemen ausgeliefert wurde. Gehen Sie auf dem Computer mit Windows 7 oder Windows Server 2008 R2 wie folgt vor, um herauszufinden, welche Version von Windows PowerShell Sie verwenden, :

1.  Klicken Sie auf **Start** \> **Alle Programme** \> **Zubehör**, klicken Sie auf **Windows PowerShell**, und klicken Sie dann auf **Windows PowerShell**.

2.  Geben Sie in der Windows PowerShell-Konsole den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:
    
        Get-Host | Select-Object Version

3.  Nun werden im Konsolenfenster Informationen wie die folgenden angezeigt:
    
        Version
        -------
        3.0

Wenn als Versionsnummer 3.0 zurückgegeben wird, arbeiten Sie mit Windows PowerShell 3.0. Wenn als Versionsnummer nicht 3.0 zurückgegeben wird, müssen Sie Windows PowerShell 3.0 installieren. Sie können Windows Management Framework 3.0 mit Windows PowerShell 3.0 aus dem [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=34595) herunterladen.

Nachdem Sie sich vergewissert haben, dass Windows PowerShell 3.0 installiert ist, müssen Sie prüfen, ob Windows PowerShell für die Ausführung von Remoteskripts konfiguriert ist. Starten Sie hierfür Windows PowerShell als Administrator. Gehen Sie unter Windows 7, Windows Server 2008 R2, Windows Server 2012 oder Windows Server 2012 R2 wie folgt vor:

1.  Klicken Sie auf **Start** \> **All Programs** \> **Accessories**, klicken Sie auf **Windows PowerShell**, klicken Sie mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

2.  Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**, um zu bestätigen, dass Sie Windows PowerShell mit Administratorrechten ausführen möchten.

Wenn Sie Windows 8 verwenden, gehen Sie stattdessen wie folgt vor:

1.  Zeigen Sie die Charmsleiste an, klicken Sie auf **Suchen**, und klicken Sie dann mit der rechten Maustaste auf **Windows PowerShell**. Sie können auf jedem Computer unter Windows 8 (mit oder ohne Touchscreen) schnell auf die Charmsleiste zugreifen, indem Sie die WINDOWS-TASTE gedrückt halten, während Sie die Taste C drücken.

2.  Klicken Sie in der Toolsleiste unten im Bildschirm auf **Als Administrator ausführen**.

3.  Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**, um zu bestätigen, dass Sie Windows PowerShell mit Administratorrechten ausführen möchten.

Nachdem Windows PowerShell ausgeführt wird, müssen Sie die Ausführungsrichtlinie so ändern, dass Remoteskripts ausgeführt werden können. Geben Sie in der Windows PowerShell-Konsole den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

    Set-ExecutionPolicy RemoteSigned -Force


> [!TIP]
> Wenn Sie den vorstehenden Befehl ausgeführt haben, wird ggf. die folgende Fehlermeldung angezeigt:<BR>Set-ExecutionPolicy : Zugriff auf den Registrierungsschlüssel 'HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.PowerShell' wurde verweigert.<BR>Diese Fehlermeldung wird normalerweise ausgegeben, wenn Sie Windows PowerShell nicht mit Administratorrechten ausführen. Schließen Sie die Windows PowerShell-Sitzung, und starten Sie eine neue Sitzung als Administrator.



Wenn Sie überprüfen möchten, ob die Ausführungsrichtlinie ordnungsgemäß konfiguriert wurde, geben Sie Folgendes an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie die EINGABETASTE:

    Get-ExecutionPolicy

Wenn der folgende Wert zurückgegeben wird, wurde alles ordnungsgemäß konfiguriert:

    RemoteSigned

Wenn Sie Windows PowerShell 3.0 aktuell noch nicht installiert haben, müssen Sie auch Windows Management Framework 3.0 aus dem Microsoft Download Center herunterladen und installieren. Hierbei handelt es sich um ein Installationspaket, das Windows PowerShell 3.0 und Windows Remote Management (WinRM) 3.0 enthält. Dieses Installationspaket ist möglicherweise erforderlich, wenn Sie mit Windows 7 arbeiten und noch kein Update auf Windows PowerShell 3.0 durchgeführt haben. Wenn Sie Windows Server 2012, Windows Server 2012 R2, Windows 8 oder Windows 8.1 verwenden, sollte die Installation von Windows PowerShell 3.0 nicht erforderlich sein. Windows PowerShell 3.0 wird gemeinsam mit diesen Betriebssystemen installiert.

Vor der Installation von Windows Management Framework 3.0:

  - Vergewissern Sie sich, dass Sie die korrekte Version des Installationspakets heruntergeladen haben. Wenn Sie die 64-Bit-Version von Windows 7 verwenden, laden Sie die Datei "Windows6.1-KB2506143-x64.msu" herunter. Für die 32-Bit-Version von Windows 7 laden Sie die Datei "Windows6.1-KB2506143-x86.msu" herunter.

  - Wenn auf Ihrem Computer Windows 7 ausgeführt wird, vergewissern Sie sich, dass Sie Windows 7 Service Pack 1 installiert haben.

Wenn Sie nicht sicher sind, welche Windows-Version ausgeführt wird oder ob Windows 7 Service Pack 1 installiert ist, klicken Sie auf **Start**, klicken Sie mit der rechten Maustaste auf **Computer**, und klicken Sie dann auf **Eigenschaften**. Die folgenden Informationen werden im Dialogfeld **System** angezeigt:

![Systemdialogfeld mit Einstellungen](images/Dn362783.30bff2e8-2862-4dd7-828f-43732f4b9314(OCS.15).png "Systemdialogfeld mit Einstellungen")

Führen Sie die folgenden Schritte aus, um Windows Management Framework 3.0 zu installieren:

1.  Doppelklicken Sie auf die MSU-Installationsdatei (entweder **Windows6.1-KB2506143-x64.msu** oder **Windows6.1-KB2506143-x86.msu**).

2.  Klicken Sie im Assistenten zum Herunterladen und Installieren von Updates auf der Seite **Lesen Sie bitte die Lizenzbedingungen (1 von 1)** auf **Annehmen**.

3.  Klicken Sie nach Abschluss der Installation auf **Neu starten**, um den Computer neu zu starten.

Vergewissern Sie sich nach dem Neustart des Computers, dass Windows PowerShell gestartet und die Anwendung mit Administratorrechten ausgeführt werden kann. Gehen Sie hierfür folgendermaßen vor:

1.  Klicken Sie auf **Start** \> **All Programs** \> **Accessories**, klicken Sie auf **Windows PowerShell**, klicken Sie mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

2.  Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**, um zu bestätigen, dass Sie Windows PowerShell mit Administratorrechten ausführen möchten.

Wenn die Windows PowerShell-Konsole angezeigt wird, sollten Sie sich vergewissern, dass der Dienst WinRM ausgeführt wird und ordnungsgemäß konfiguriert wurde. Um zu überprüfen, ob der Dienst ausgeführt wird, geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie die EINGABETASTE:

    Get-Service winrm

Auf dem Bildschirm werden nun Informationen zum Dienst WinRM angezeigt:

    Status   Name               DisplayName
    ------   ----               -----------
    Running  winrm              Windows Remote Management (WS-Manag...

Wenn der Dienststatus nicht gleich "Wird ausgeführt" ist, starten Sie WinRM, indem Sie den folgenden Befehl eingeben und dann die EINGABETASTE drücken:

    Start-Service winrm

Nachdem der Dienst gestartet wurde, führen Sie den folgenden Befehl aus, um sich zu vergewissern, dass WinRM mit der Standardauthentifizierung arbeitet:

    winrm set winrm/config/client/auth '@{Basic="True"}'

Auf dem Bildschirm werden nun Informationen wie die folgenden angezeigt:

    Auth
        Basic = true
        Digest = true
        Kerberos = true
        Negotiate = true
        Certificate = true
        CredSSP = false

Wenn die Standardauthentifizierung verwendet wird, können Sie Windows PowerShell verwenden, um die Verbindung zu Skype for Business Online herzustellen.

