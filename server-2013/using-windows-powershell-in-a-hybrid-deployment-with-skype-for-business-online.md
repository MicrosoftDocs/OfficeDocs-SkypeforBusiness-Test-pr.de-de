---
title: Verwenden von Windows PowerShell in einer Hybridbereitstellung
TOCTitle: Verwenden von Windows PowerShell in einer Hybridbereitstellung
ms:assetid: b19625d4-4b68-403c-a072-5296aa590556
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362835(v=OCS.15)
ms:contentKeyID: 56269332
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwenden von Windows PowerShell in einer Hybridbereitstellung

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

In einer Hybridbereitstellung verwaltet eine Organisation einige Benutzer in der lokalen Version von Lync Server 2013 und die weiteren Benutzer in Skype for Business Online. Sie können eine einzige Windows PowerShell-session verwenden, um gleichzeitig sowohl Ihre lokale Version von Lync Server als auch Ihren Skype for Business Online-Mandanten zu verwalten. Damit dies funktioniert, müssen zwei wesentliche Punkte klar sein:

1.  Herstellen einer gleichzeitigen Verbindung mit Lync Server und Skype for Business Online

2.  Verweisen auf die Skype for Business Online-Einstellungen aus dieser gleichzeitigen Verbindung

Das Herstellen einer gleichzeitigen Verbindung mit Lync Server und Skype for Business Online ist überraschend einfach. Beginnen Sie hiermit, indem Sie eine Verbindung mit Lync Server auf dieselbe Weise herstellen wie immer, entweder, indem Sie die Lync Server-Verwaltungsshell starten oder eine Remoteverbindung mit einem Front-End-Pool herstellen. Nachdem Sie erfolgreich eine Verbindung mit der lokalen Version von Lync Server hergestellt haben, können Sie eine Verbindung mit Skype for Business Online herstellen, indem Sie auf dieselbe Weise vorgehen, als würden Sie nur eine Verbindung mit Skype for Business Online herstellen. Damit diese Verbindung hergestellt werden kann, müssen Sie zunächst ein Windows PowerShell-Objekt mit Anmeldeinformationen erstellen, indem Sie Ihre Office 365-Anmeldeinformationen verwenden. Geben Sie dazu Folgendes an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE:

    $credential = Get-Credential

Nachdem Sie die EINGABETASTE gedrückt haben, wird das Dialogfeld **Bei Windows PowerShell anmelden** angezeigt:

![Windows PowerShell: Anmeldeinformationen](images/Dn362835.0f04e0a1-c9d6-4341-a0bb-ef721c4815fd(OCS.15).png "Windows PowerShell: Anmeldeinformationen")

Geben Sie in das Feld **Benutzername** Ihren Skype for Business Online-Namen ein. Geben Sie in das Feld **Kennwort** Ihr Skype for Business Online-Kennwort ein (das Kennwort wird maskiert und ist auf dem Bildschirm nicht zu sehen). Wenn Sie beispielsweise den Benutzernamen kenmyer@litwareinc.com und das Kennwort p@ssw0rd\! haben, sieht das Dialogfeld wie folgt aus:

![Windows PowerShell: Anmeldeinformationen](images/Dn362835.85977a0e-b14a-4aec-a45e-8548e9c9f691(OCS.15).png "Windows PowerShell: Anmeldeinformationen")

Damit das Objekt mit Anmeldeinformationen erstellt wird, klicken Sie auf **OK**. Nachdem Sie dieses Objekt erstellt haben, können Sie eine Verbindung mit Skype for Business Online herstellen, indem Sie den folgenden Befehl ausführen:

    $session = New-CsOnlineSession -Credential $credential

Achten Sie darauf, dass Sie den Befehl korrekt eingeben. Es spielt keine Rolle, welchen Namen Ihre Skype for Business Online-Domäne hat. Das Cmdlet **New-CsOnlineSession** stellt für Sie eine Verbindung mit Office 365 her und meldet Sie mit den bereitgestellten Anmeldeinformationen an. Nachdem Sie die Verbindung hergestellt haben und authentifiziert wurden, wird für Sie automatisch eine Umleitung zum richtigen URI vorgenommen.

Wenn die Verbindung erfolgreich hergestellt wurde, wird in der Windows PowerShell-Konsole eine Meldung angezeigt, die in etwa wie folgt aussieht:

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

Nachdem Sie erfolgreich eine Verbindung mit Skype for Business Online hergestellt haben, importieren Sie diese session, indem Sie einen Befehl ausführen, der in etwa wie folgt aussieht:

    Import-PSSession $session -AllowClobber


> [!TIP]
> Mit dem Parameter AllowClobber wird sichergestellt, dass alle Skype for Business Online-Cmdlets importiert werden, und zwar auch die Cmdlets, die dieselben Namen haben wie die normalen Lync Server-Cmdlets. Dies sind sehr viele Cmdlets, da die meisten Skype for Business Online-Cmdlets, so auch <A href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</A>, <A href="new-csexumcontact.md">New-CsExUmContact</A>, <A href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</A> usw., ein lokales Gegenstück haben. Die paarweise aufgeführten Cmdlets (beispielsweise das Lync Server-Cmdlet <STRONG>Get-CsMeetingConfiguration</STRONG> und das Skype for Business Online-Cmdlet <STRONG>Get-CsMeetingConfiguration</STRONG>) sind identisch: Es spielt keine Rolle, welches Cmdlet Sie verwenden. Der einzige Grund für die Verwendung des Parameters AllowClobber besteht darin, dass das Anzeigen von Warnmeldungen auf dem Bildschirm verhindert wird.



Sie sind jetzt soweit, dass Sie damit beginnen können, sowohl die lokale Version von Lync Server als auch Skype for Business Online zu verwalten. An diesem Punkt stellen Sie sich möglicherweise folgende wichtige Frage: Wie unterscheide ich zwischen Lync Server-Richtlinien und -Einstellungen sowie Skype for Business Online-Richtlinien und -Einstellungen? Nehmen Sie beispielsweise an, Sie möchten die globalen Konfigurationseinstellungen für Besprechungen ändern. Dazu führen Sie den folgenden Befehl aus:

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False

Dieser Befehl ändert die global Einstellungen. Aber welche globalen Einstellungen? Lync Server lokal? Skype for Business Online? Beide? Weder noch?

In diesem speziellen Fall werden die lokalen Einstellungen geändert. Woran ist dies zu erkennen? Daran, dass der Parameter **Tenant** nicht in dem Befehl angegeben ist. Wenn Sie gleichzeitig eine Verbindung mit Lync Server lokal und mit Skype for Business Online haben, werden Cmdlets, die für beide Plattformen ausgeführt werden können, für Lync Server ausgeführt, es sei denn, Sie haben etwas anderes angegeben. Die einzige Möglichkeit hierzu besteht darin, den Parameter **Tenant** einzufügen, wenn der Befehl ausgeführt wird. Beispielsweise werden mit dem folgenden Befehl die globalen Einstellungen für den Skype for Business Online-Mandanten aktualisiert, der die Mandanten-ID bf19b7db-6960-41e5-a139-2aa373474354 hat:

    Set-CsMeetingConfiguration -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AdmitAnonymousUsersByDefault $False

Der Parameter **Tenant** ist der Schlüssel. Der folgende Befehl gibt die globale externe Zugriffrichtlinie für die lokale Version von Lync Server zurück:

    Get-CsExternalAccessPolicy -Identity "global"

Und der folgende Befehl gibt die globale externe Zugriffrichtlinie für Ihren Skype for Business Online-Mandanten zurück:

    Get-CsExternalAccessPolicy -Identity "global" -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

Beachten Sie, dass es mehr als 700 lokale Cmdlets gibt. Allerdings hat der überwiegende Teil dieser Cmdlets keinen Tenant-Parameter, d. h., diese Cmdlets können nicht mit Skype for Business Online verwendet werden. Außerdem gibt es einige wenige Cmdlets, die einen Tenant-Parameter haben, aber noch nicht mit Skype for Business Online verwendet werden können. Wenn Sie die Namen von genau den Cmdlets abrufen möchten, die mit Skype for Business Online verwendet werden können, führen Sie folgenden Befehl an der Windows PowerShell-Eingabeaufforderung aus:

    Get-Module

Die auf dem Bildschirm angezeigten Informationen sehen in etwa wie folgt aus:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Das Modul, das den Modultyp **Script** hat, ist das Modul das die Skype for Business Online-Cmdlets enthält. Wenn Sie eine Liste mit den Namen dieser Cmdlets zurückgeben möchten, führen Sie das Cmdlet **Get-Command** aus, wobei Sie den Namen des **Script**-Moduls als Modulnamen angeben:

    Get-Command -Module tmp_5astd3uh.m5v

Windows PowerShell zeigt dann eine Liste mit den Namen aller Skype for Business Online-Cmdlets an.

**Behebung von Verbindungsproblemen in einer Hybridbereitstellung**

In einigen Fällen treffen Administratoren möglicherweise auf Probleme bei der Anmeldung bei Office 365, wenn sie ein lokales Konto (beispielsweise administrator@litwareinc.net) anstelle eines Office 365-Kontos (wie administrator@litwareinc.onmicrosoft.com) verwenden. Wenn die Verzeichnissynchronisierung korrekt funktioniert, sollten Sie sich mit beiden Konten anmelden können, was einer der Vorteile einer Hybridbereitstellung ist. Dennoch gab es Situationen, in denen sich ein Administrator nicht mit seinem lokalen Konto anmelden konnte. Normalerweise liegt das daran, dass die Autoermittlung den Anmeldeversuch auf die lokale Installation von Lync Server statt auf Office 365 verweist.

Es gibt jedoch eine einfache Problemumgehung: Wenn Sie das **New-CsOnlineSession**-cmdlet für die Anmeldung bei Office 365 verwenden, schließen Sie den OverrideAdminDomain-Parameter, gefolgt vom Domänennamen Office 365 ein. Wenn Sie sich beispielsweise bei Office 365 über das Konto administrator@litwareinc.net anmelden, schließen Sie den OverrideAdminDomain-Parameter, gefolgt vom Domänennamen litwareinc.onmicrosoft.com, ein:

    $session = New-CsOnlineSession -Credential $credential -OverrideAdminDomain "litwareinc.onmicrosoft.com"

Mit diesem Befehl wird der Anmeldeversuch direkt an die Office 365-Server und die litwareinc.onmicrosoft.com-Domäne geleitet.

