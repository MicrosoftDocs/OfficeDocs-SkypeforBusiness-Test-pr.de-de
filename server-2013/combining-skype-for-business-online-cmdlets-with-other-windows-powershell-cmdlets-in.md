---
title: Kombinieren von Lync Online-Cmdlets mit anderen Windows PowerShell-Cmdlets
TOCTitle: Kombinieren von Lync Online-Cmdlets mit anderen Windows PowerShell-Cmdlets
ms:assetid: 8bb8800a-f966-4570-8c8b-db87a91ad783
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362816(v=OCS.15)
ms:contentKeyID: 56269306
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Kombinieren von Lync Online-Cmdlets mit anderen Windows PowerShell-Cmdlets

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie die Verbindung zu Skype for Business Online über Windows PowerShell herstellen, stehen Ihnen etwa 40 Skype for Business Online-Cmdlets zur Verfügung. Sie sind bei der Verwaltung von Skype for Business Online jedoch nicht auf diese 40 Cmdlets beschränk. Neben den Skype for Business Online-Cmdlets können Sie auch alle anderen Windows PowerShell-Cmdlets verwenden, die auf Ihrem Computer installiert sind. (Bei der Installation von Windows PowerShell 3.0 werden zusätzlich Hunderte Windows PowerShell-Kern-Cmdlets installiert.) In Ihren Befehlen können Sie Skype for Business Online-Cmdlets und beliebige andere auf Ihre Computer befindliche Cmdlets nach Lust und Laune kombinieren.

Eine vollständige Einführung in Windows PowerShell 3.0 würde den Rahmen dieses Artikels zwar sprengen, dennoch finden Sie hier einige Beispiele, die zeigen, warum Sie die Cmdlets möglicherweise kombinieren möchten. Zunächst einmal enthält keines der Skype for Business Online-Cmdlets einen Druckbefehl, und einen solchen Befehl finden Sie auch nicht in der Windows PowerShell-Konsole. Wie können Sie also die Informationen drucken, die Sie mit einem Cmdlet abgerufen haben? Eine Möglichkeit besteht darin, die Informationen abzurufen und dann an das Cmdlet **Out-Printer** zu senden

    Get-CsTenant | Out-Printer

Da keine zusätzlichen Parameter angegeben wurden, werden alle vom Cmdlet **the Out-Printer** zurückgegebenen Informationen auf dem Standarddrucker gedruckt.

Ebenso umfasst keines der Skype for Business Online-Cmdlets einen Parameter, der es Ihnen ermöglicht, Daten in einer Datei zu speichern. Das ist jedoch kein Problem, denn dieser Befehl verwendet das Cmdlet **Out-File**, um die zurückgegebenen Informationen in der Textdatei "C:\\Logs\\Tenants.txt" zu speichern:

    Get-Tenant | Out-File -FilePath "C:\Logs\Tenants.txt"

Dieser Befehl hier verwendet das Cmdlet **Select-Object**, um die Daten einzuschränken, die zurückgegeben und auf dem Bildschirm angezeigt werden. In diesem Beispiel ruft das Cmdlet [Get-CsOnlineUser](get-csonlineuser.md) Informationen zu allen Ihren Skype for Business Online-Benutzern ab. Anschließend wird das Cmdlet **Select-Object** verwendet, um die angezeigten Daten auf den Wert **Identity** des Benutzers und auf die Archivierungsrichtlinie zu begrenzen:

    Get-CsOnlineUser | Select-Object Identity, ArchivingPolicy

Da auf Ihrem Computer Hunderte von Cmdlets zur Verfügung stehen, finden Sie es möglicherweise schwierig festzustellen, bei welche es sich um Skype for Business Online-Cmdlets handelt und bei welchen nicht. Wenn Sie eine Liste der Skype for Business Online-Cmdlets (und nur der Skype for Business Online-Cmdlets) zurückgeben möchten, müssen Sie zuerst den Namen des temporären Windows PowerShell-Moduls ermitteln, das alle Skype for Business Online-Cmdlets enthält. Geben Sie hierzu an der Windows PowerShell-Eingabeaufforderung den folgenden Befehl ein:

    Get-Module

Auf dem Bildschirm werden nun Informationen wie die folgenden angezeigt:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Das Modul mit dem Modultyp "Script" ist das Modul, das die Skype for Business Online-Cmdlets enthält. Um eine Liste dieser Cmdlets zurückzugeben, führen Sie das Cmdlet **Get-Command** aus und verwenden hierbei den Namen des Skriptmoduls als Modulnamen:

    Get-Command -Module tmp_5astd3uh.m5v

Möglicherweise gibt es mehrere Module mit dem Modultyp "Script". In dem Fall können Sie den folgenden Befehl ausführen, um herauszufinden, welches Modul das Cmdlet **Get-CsTenant** enthält:

    Get-Command Get-CsTenant

Das Module, das für das Cmdlet **Get-CsTenant** zurückgegeben wird, ist das Modul, das alle Skype for Business Online-Cmdlets enthält:

    CommandType     Name                                               ModuleName
    -----------     ----                                               ----------
    Function        Get-CsTenant                                       tmp_5astd3uh.m5v

## Siehe auch

#### Konzepte

[Einführung in Windows PowerShell und Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

