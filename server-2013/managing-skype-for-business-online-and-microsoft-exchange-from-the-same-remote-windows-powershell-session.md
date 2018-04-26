---
title: Verwalten von Lync Online und Microsoft Exchange mit derselben Windows PowerShell-Remotesitzung
TOCTitle: Verwalten von Lync Online und Microsoft Exchange mit derselben Windows PowerShell-Remotesitzung
ms:assetid: 4eb4b5f0-f407-46bd-a2ac-a7ccbc387d51
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362787(v=OCS.15)
ms:contentKeyID: 56269271
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwalten von Lync Online und Microsoft Exchange mit derselben Windows PowerShell-Remotesitzung

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie Office 365 abonnieren, erhalten Sie nicht nur Zugriff auf Skype for Business Online, sondern auch auf Exchange Online. Sie können Skype for Business Online über eine Windows PowerShell-Remotesitzung verwalten. Mit einer Windows PowerShell-Remotesitzung können Sie auch Exchange verwalten. Skype for Business Online und Exchange Online nutzen jedoch weder den gleichen URI, noch wird die gleiche Verbindungsmethode verwendet. Dies lässt den Schluss zu, dass Sie für die Verwaltung von Skype for Business Online und Exchange zwei getrennte Sitzungen verwenden müssen. Oder gibt es eine Möglichkeit, beide Produkte mit einer einzigen Windows PowerShell-Remotesitzung zu verwalten?

Ja, die gibt es, und Sie können nicht nur beide Produkte mit der gleichen Instanz von Windows PowerShell verwalten, sondern die Einrichtung dieser dualen Verwaltungssitzung ist auch noch denkbar einfach. Im ersten Schritt starten Sie Windows PowerShell und stellen die Verbindung zu Skype for Business Online in der gleichen Weise her wie immer: Sie erstellen ein **Credentials**-Objekt und dann eine neue Sitzung, mit der Sie Verbindung zu Skype for Business Online herstellen:

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $lyncSession = New-CsOnlineSession -Credential $credential

Im nächsten Schritt gehen Sie ebenso vor, um die Verbindung zu Exchange Online herzustellen. Hierfür müssen Sie kein neues **Credentials**-Objekt erstellen, sondern können mit dem gleichen Objekt (**$credential**) fortfahren, das Sie für die Anmeldung bei Skype for Business Online verwendet haben:

    $exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection

Sie sollten bei der Herstellung der Verbindung zu Exchange Online immer den URI https://outlook.office365.com/powershell-liveid/ verwenden und zwar ungeachtet des Office 365-URI. Nachdem Sie authentifiziert worden sind, werden Sie automatisch an den richtigen URI weitergeleitet. Aus diesem Grund ist es besonders wichtig, den Parameter AllowRedirection einzuschließen. Wenn Sie diesen Parameter auslassen, werden Sie zwar authentifiziert, jedoch schlägt die Umleitung fehl und die Verbindung zu Exchange Online kann nicht hergestellt werden:

    New-PSSession : [ps.outlook.com] The WinRM service cannot process the request because the request needs to be sent to a different machine. Use the redirect information to send the request to a new machine.  Redirect location reported: https://pod51043psh.outlook.com/powershell-liveid?PSVersion=3.0 . To automatically connect to the redirected URI, verify  MaximumConnectionRedirectionCount" property of session preference variable "PSSessionOption" and use "AllowRedirection" parameter on the cmdlet.

Nun sollten auf Ihrem Computer zwei separate Remotesitzungen ausgeführt werden. Sie überprüfen dies, indem Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung eingeben:

    Get-PSSession

Nun werden Informationen wie die folgenden auf dem Bildschirm angezeigt:

    Id Name      ComputerName  State   ConfigurationName     Availability
    -- ----      ------------  -----   -----------------     ------------
     1 Session1  pod510w43...  Opened  Microsoft.PowerShell     Available
     2 Session2  up02921vd...  Opened  Microsoft.Exchange       Available

Damit verfügen Sie über zwei Remotesitzungen, die in die lokale Windows PowerShell-Sitzung importiert werden können. Hierzu führen Sie die beiden folgenden Befehle aus:

    Import-PSSession $lyncSession
    Import-PSSession $exchangeSession

Ab diesem Punkt stehen Ihnen die sowohl die Skype for Business Online- als auch die Exchange Online-Cmdlets zur Verfügung. Sie überprüfen dies, indem Sie den folgenden Befehl eingeben und sich vergewissern, dass Benutzerinformationen zurückgegeben werden:

    Get-CsOnlineUser -ResultSize 1

Führen Sie dann den folgenden Exchange-Befehl aus, und vergewissern Sie sich, dass Postfachinformationen zurückgegeben werden:

    Get-Mailbox -ResultSize 1

Wenn Sie die Verwaltungssitzung beenden, achten Sie darauf, beide Remotesitzungen zu schließen:

    Remove-PSSession $lyncSession
    Remove-PSSession $exchangeSession

## Siehe auch

#### Konzepte

[Konfigurieren eines Computers für Lync Online-Verwaltung](configuring-your-computer-for-skype-for-business-online-management.md)

