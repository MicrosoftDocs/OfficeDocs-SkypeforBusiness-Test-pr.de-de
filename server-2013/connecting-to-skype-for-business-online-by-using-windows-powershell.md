---
title: Herstellen der Verbindung zu Lync Online mit Windows PowerShell
TOCTitle: Herstellen der Verbindung zu Lync Online mit Windows PowerShell
ms:assetid: 6167dad9-9628-4fdb-bed1-bdb3f7108e64
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362795(v=OCS.15)
ms:contentKeyID: 56269277
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Herstellen der Verbindung zu Lync Online mit Windows PowerShell

 

_**Letztes Änderungsdatum des Themas:** 2017-03-03_

Nachdem Sie die erforderliche Software installiert haben, können Sie damit beginnen, Skype for Business Online mit Windows PowerShell zu verwalten. Hierzu öffnen Sie zunächst eine Standardinstanz von Windows PowerShell. Es ist weder erforderlich, eine spezielle Instanz von Windows PowerShell zu öffnen (wie beispielsweise Lync Server-Verwaltungsshell), noch müssen Sie eine Systemsteuerungs-App oder einen anderen speziellen Anwendungstyp öffnen, denn die Verwaltung von Skype for Business Online erfolgt mit einer Remotesitzung von Windows PowerShell. Dies bedeutet:

1.  Sie verwenden eine reguläre Sitzung von Windows PowerShell, um die Verbindung zu Skype for Business Online herzustellen. Bei einer Remoteverbindung arbeiten Sie auf dem lokalen Computer und verwenden Ihre lokale Kopie von Windows PowerShell, verwalten jedoch Objekte, die sich auf einem Remotesystem befinden (d. h. Skype for Business Online).

2.  Alle Cmdlets, Skripts und andere Elemente, die für die Verwaltung von Skype for Business Online notwendig sind, werden auf Ihren Computer heruntergeladen. Diese Elemente befinden sich im Arbeitsspeicher und stehen – wichtig zu wissen\! – nur während der Remotesitzung mit Skype for Business Online zur Verfügung. Wenn Sie eine Remoteverbindung zu Skype for Business Online herstellen, werden die Skype for Business Online-Cmdlets wie [Get-CsTenant](get-cstenant.md) in den Arbeitsspeicher Ihres Computers kopiert. Während der Remotesitzung können Sie diese Cmdlets ausführen, sie stehen jedoch nur in dieser Remotesitzung zur Verfügung. So können Sie beispielsweise eine zweite Sitzung von Windows PowerShell starten, ohne in dieser Sitzung jedoch die Verbindung zu Skype for Business Online herzustellen. Wenn Sie nun versuchen, in dieser Sitzung das Cmdlet **Get-CsTenant** auszuführen, wird die folgende Fehlermeldung ausgegeben:
    
        Get-CsTenant : The term 'Get-CsTenant' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
    
    Auch eine Suche auf der Festplatte nach dem Cmdlet **Get-CsTenant** (oder einem beliebigen anderen Skype for Business Online-Cmdlet) verläuft ergebnislos, da tatsächlich nichts auf Ihrer Festplatte gespeichert wird, wenn Sie eine Remotesitzung einrichten.

3.  Wenn Sie die Remotesitzung schließen, werden die heruntergeladenen Elemente aus dem Arbeitsspeicher des Computers gelöscht. Sie können beispielsweise eine Windows PowerShell-Remotesitzung mit dem Cmdlet **Get-CsTenant** starten und die Sitzung dann schließen. Wenn Sie Windows PowerShell nun erneut starten, ist das Cmdlet **Get-CsTenant** nicht mehr verfügbar. Wenn Sie erneut auf das Cmdlet **Get-CsTenant** zugreifen möchten, müssen Sie eine neue Verbindung zu Skype for Business Online herstellen.


> [!TIP]
> Wenn Sie mit einer Hybridbereitstellung arbeiten, sollten Sie die im Artikel <A href="using-windows-powershell-in-a-hybrid-deployment-with-skype-for-business-online.md">Verwenden von Windows PowerShell in einer Hybridbereitstellung</A> beschriebenen Verfahren befolgen.



Um eine Remoteverbindung zu Skype for Business Online herzustellen, starten Sie zunächst eine neue Sitzung mit Windows PowerShell auf Ihrem lokalen Computer. Wenn Sie mit Windows 7, Windows Server 2008 R2, Windows Server 2012 oder Windows Server 2012 R2 arbeiten, gehen Sie folgendermaßen vor:

  - Klicken Sie auf **Start** \> **Alle Programme** \> **Zubehör**, klicken Sie auf **Windows PowerShell**, und klicken Sie dann auf **Windows PowerShell**.

Wenn Sie Windows 8 oder 8.1 verwenden, gehen Sie stattdessen wie folgt vor:

  - Zeigen Sie die Charmsleiste an, klicken Sie auf **Suchen**, und klicken Sie dann auf **Windows PowerShell**. Sie können auf jedem Computer unter Windows 8 oder 8.1 (mit oder ohne Touchscreen) schnell auf die Charmsleiste zugreifen, indem Sie die WINDOWS-TASTE gedrückt halten, während Sie die Taste C drücken.

Wenn die Windows PowerShell-Konsole angezeigt wird, müssen Sie ein Windows PowerShell-Objekt mit Anmeldeinformationen erstellen. Das Objekt mit Anmeldeinformationen wird verwendet, um Ihren Benutzernamen und Ihr Kennwort sicher an Skype for Business Online zu übermitteln. Zum Erstellen eines Objekts mit Anmeldeinformationen geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein und drücken dann die EINGABETASTE:

    $credential = Get-Credential


> [!TIP]
> In diesem Beispiel werden Ihr Benutzername und das Kennwort in der Variablen <STRONG>$credential</STRONG> gespeichert. Sie können der Variablen einen beliebigen Namen zuweisen, solange dieser Name den Namensregeln für Variablen von Windows PowerShell entspricht. Sie müssen jedoch irgendeine Art von Variable verwenden, um den Benutzernamen und das Kennwort zu speichern. Andernfalls verschwindet das Objekt mit Anmeldeinformationen, das Sie erstellen, unmittelbar nach seiner Erstellung.



Nachdem Sie die EINGABETASTE gedrückt haben, sollte das Windows PowerShell-Dialogfeld für die Eingabe von Anmeldeinformationen angezeigt werden:

![Windows PowerShell: Anmeldeinformationen](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Windows PowerShell: Anmeldeinformationen")

Geben Sie im Feld **Benutzername** Ihren Skype for Business Online-Benutzernamen ein. Geben Sie im Feld **Kennwort** Ihr Skype for Business Online-Kennwort ein (das Kennwort wird maskiert und auf dem Bildschirm nicht angezeigt). Wenn Ihr Benutzername beispielsweise "kenmyer@litwareinc.com" und Ihr Kennwort "p@ssw0rd\!" lautet, sieht das Dialogfeld wie folgt aus:

![Windows PowerShell: Anmeldeinformationen](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Windows PowerShell: Anmeldeinformationen")

Zum Erstellen des **Credentials**-Objekts klicken Sie auf **OK**. Wenn Sie überprüfen möchten, ob dieses Objekt erstellt wurde, geben Sie einfach den Variablennam3en an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie die EINGABETASTE:

    $credential

Windows PowerShell reagiert, indem eine Anzeige wie die folgende ausgegeben wird:

    UserName                            Password
    --------                            --------
    kenmyer@litwareinc.com              System.Security.SecureString


> [!TIP]
> Denken Sie daran, dass das Cmdlet <STRONG>Get-Credential</STRONG> alle Anmeldeinformationen akzeptiert, die Sie eingeben, und nicht versucht zu überprüfen, ob Sie einen gültigen Benutzernamen bzw. ein gültige Kennwort eingegeben haben. Diese Überprüfung erfolgt erst bei dem Versuch, sich bei Skype for Business Online anzumelden.



Nachdem Sie das **credentials**-Objekt erstellt haben, können Sie eine neue Windows PowerShell-Remotesitzung erstellen, mit der eine Verbindung zu Skype for Business Online hergestellt wird. Geben Sie hierfür den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie die EINGABETASTE:

    $session = New-CsOnlineSession -Credential $credential


> [!TIP]
> <STRONG>$session</STRONG> ist eine Variable, die zur Aufnahme von Informationen verwendet wird, in diesem Fall von Informationen über die Verbindung mit Skype for Business Online. Auch dieser Variablen können Sie einen beliebigen Namen zuweisen, solange dieser den Windows PowerShell-Richtlinien für die Variablenbenennung entspricht (so darf der Name beispielsweise keine Leerzeichen oder Satzzeichen enthalten).



Geben Sie den Befehl unbedingt genau wie hier gezeigt ein (möglicherweise mit Ausnahme des Variablennamens). Der Name Ihrer Skype for Business Online-Domäne ist hierbei nicht wichtig. Unabhängig vom Domänennamen stellt das Cmdlet **New-CsOnlineSession** die Verbindung zu Office 365 her und meldet Sie mit den von Ihnen angegebenen Anmeldeinformationen an. Nachdem die Verbindung hergestellt und Sie authentifiziert wurden, werden Sie automatisch basierend auf den angegebenen Anmeldeinformationen an den richtigen URI weitergeleitet.

Wenn die Verbindung erfolgreich hergestellt werden konnte, werden in der Windows PowerShell-Konsole Meldungen wie die folgenden angezeigt:

    VERBOSE: Determining domain to admin
    VERBOSE: AdminDomain = litwareinc.com
    VERBOSE: Discovering PowerShell endpoint URI
    VERBOSE: TargetUri = https://webdir0d.litwareinc.com/OcsPowerShellLiveId
    VERBOSE: Requesting authentication token
    VERBOSE: Success
    VERBOSE: Initializing remote session
    VERBOSE: Success
    Id Name       ComputerName    State        ConfigurationName     Availability -- ----       ------------    -----        -----------------     ------------
    2 Session2    litwarein...    Opened       Microsoft.PowerShell  Available

Sind Sie nun bereit, mit der Verwaltung von Skype for Business Online mit Windows PowerShell zu beginnen? Noch nicht ganz. Das Cmdlet **New-CsOnlineSession** stellt die Verbindung zu Skype for Business Online her und erstellt eine neue Sitzung für Sie. Nun müssen Sie diese neue Sitzung jedoch in die Windows PowerShell-Konsole importieren. Führen Sie hierzu den folgenden Befehl aus:

    Import-PSSession $session

Wenn Sie die EINGABETASTE drücken, wird in der Windows PowerShell-Konsole eine Fortschrittsanzeige wie die folgende angezeigt:

    Creating implicit remoting module . . .
         Getting command information from remote session . . . 16 commands  
              received
         [oooooooooooooooo
         00:00:33 remaining

Das ist der Punkt, an dem Windows PowerShell Cmdlets und andere Elemente herunterlädt, die für die Verwaltung von Skype for Business Online erforderlich sind. Nach Abschluss des Downloads werden in der Windows PowerShell-Konsole Informationen wie die folgenden angezeigt:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enable-Cs ...}

Nun sind Sie bereit, um mit der Verwaltung von Skype for Business Online mit Windows PowerShell zu beginnen. Um zu überprüfen, dass der Download erfolgreich abgeschlossen wurde, und um die Skype for Business Online-Cmdlets anzuzeigen, die nun zur Verfügung stehen, müssen Sie zunächst den Namen des temporären Windows PowerShell-Moduls ermitteln, das alle Skype for Business Online-Cmdlets enthält. Geben Sie hierzu an der Windows PowerShell-Eingabeaufforderung den folgenden Befehl ein:

    Get-Module

Auf dem Bildschirm werden nun Informationen wie die folgenden angezeigt:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Das Modul mit dem Modultyp "Script" ist das Modul, das die Skype for Business Online-Cmdlets enthält. Um eine Liste dieser Cmdlets zurückzugeben, führen Sie das Cmdlet **Get-Command** aus und verwenden hierbei den Namen des Skriptmoduls als Modulnamen:

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell sollte nun eine Liste aller Skype for Business Online-Cmdlets anzeigen.

Nachdem Sie alle Verwaltungsaufgaben erledigt haben, sollten Sie immer den folgenden Befehl ausführen, bevor Sie die Windows PowerShell-Konsole schließen:

    Remove-PSSession $session

Das Cmdlet **Remove-PSSession** trennt die Verbindung zu Skype for Business Online und schließt die Remotesitzung. Wenn Sie nun versuchen, die Sitzung erneut zu importieren (mit dem Cmdlet **Import-PSSession**), wird folgende Fehlermeldung ausgegeben:

    Import-PSSession : State of runspace is not valid for this operation.

Diese Meldung bedeutet ganz einfach, dass Sie eine neue Sitzung erstellen müssen, um erneut eine Verbindung zu Skype for Business Online herstellen zu können.

Wenn Sie vergessen, die Sitzung zu entfernen, bevor Sie die Windows PowerShell-Konsole schließen (der wenn die Konsole unerwartet geschlossen wird), ist das auch nicht weiter dramatisch. Nach 15 Minuten Inaktivität trennt die Sitzung die Verbindung automatisch und selbsttätig. Standardmäßig darf jeder Skype for Business Online-Administrator jedoch nur drei simultane Verbindungen zu Skype for Business Online unterhalten. Wenn Sie die Windows PowerShell-Konsole schließen, ohne die Sitzung zu entfernen, zählt diese geschlossene Sitzung weiterhin als eine Verbindung, auch wenn diese im Moment nicht genutzt wird. (Und sie zählt weiterhin als eine Verbindung, bis das Zeitlimit überschritten wurde.) So könnte es beispielsweise vorkommen, dass Sie die Windows PowerShell-Konsole drei Mal öffnen und schließen, jedes Mal, ohne die Skype for Business Online-Sitzung zu entfernen. Würden Sie Windows PowerShell nun öffnen und versuchen, eine vierte Verbindung herzustellen, bleibt der Befehl hängen, und es wird keine Verbindung hergestellt.


> [!TIP]
> Wenn Windows PowerShell bei dem Versuch, eine Verbindung herzustellen, hängen bleibt, drücken Sie STRG+C, um den hängengebliebenen Befehl zu beenden.



Während einzelne Administratoren nur mit jeweils drei simultanen Verbindungen zu einem Skype for Business Online-Mandanten arbeiten können, verfügt die Organisation als solche über insgesamt neun simultane Verbindungen. Dies bedeutet, dass drei Administratoren über jeweils drei simultane Verbindungen oder neun Administratoren über jeweils eine Verbindung zu Skype for Business Online verfügen können usw. Um es jedoch noch einmal zu betonen: Kein einzelner Administrator kann mehr als drei aktive Sitzungen unterhalten.

## Siehe auch

#### Konzepte

[Konfigurieren eines Computers für Lync Online-Verwaltung](configuring-your-computer-for-skype-for-business-online-management.md)

