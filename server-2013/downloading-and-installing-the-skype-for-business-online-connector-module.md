---
title: Herunterladen und Installieren des Lync Online-Connector-Moduls
TOCTitle: Herunterladen und Installieren des Lync Online-Connector-Moduls
ms:assetid: a0c87219-b642-4201-85d4-a85c2163d1eb
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362829(v=OCS.15)
ms:contentKeyID: 56269323
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Herunterladen und Installieren des Lync Online-Connector-Moduls

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Das Skype for Business Online-Connector-Modul beinhaltet das Cmdlet **New-CsOnlineSession**, mit dem Sie eine Windows PowerShell-Remotesitzung erstellen können, für die eine Verbindung mit Skype for Business Online hergestellt wird. Dieses Modul, das nur auf 64-Bit-Computern unterstützt wird (weitere Informationen hierzu finden Sie unter [Konfigurieren eines Computers für Lync Online-Verwaltung](configuring-your-computer-for-skype-for-business-online-management.md)), kann aus dem Microsoft Download Center unter [http://go.microsoft.com/fwlink/?LinkId=294688](http://go.microsoft.com/fwlink/?linkid=294688) heruntergeladen werden. Laden Sie die Datei **LyncOnlinePowershell.exe** herunter, und führen Sie dann die folgenden Schritte aus:

1.  Doppelklicken Sie auf die Datei **LyncOnlinePowershell.exe**.

2.  Wählen Sie im Skype for Business Online Tenant PowerShell Setup-Assistenten auf der Seite **Microsoft Software License Terms** die Option **I accept the terms in the License Agreement** aus, und klicken Sie dann auf **Install**. Wenn das Dialogfeld **User Account Control** angezeigt wird, klicken Sie auf **Yes**, um die Installation fortzusetzen.

3.  Klicken Sie auf der Seite **Completed the Microsoft Lync Online, Tenant PowerShell Setup** auf **Finish**.

Das Setupprogramm kopiert das Skype for Business Online-Connector-Modul (und das Cmdlet **New-CsOnlineSession**) auf Ihren lokalen Computer. Damit Sie auf das Modul zugreifen können, starten Sie eine Windows PowerShell-Sitzung mit den Anmeldeinformationen eines Administrators, und führen Sie dann den folgenden Befehl aus:

    Import-Module LyncOnlineConnector

Wenn Sie diesen Befehl nicht jedes Mal eingeben möchten, wenn Sie Windows PowerShell starten, fügen Sie den Befehl zu Ihrem Windows PowerShell-Profil hinzu. Geben Sie dazu den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE:

    notepad.exe $profile

Wenn der Editor angezeigt wird, fügen Sie die folgende Zeile unter den Befehlen hinzu, die sich bereits im Profil befinden (wenn zutreffend:

    Import-Module LyncOnlineConnector

Speichern Sie die Datei. Wenn Sie Windows PowerShell das nächste Mal starten, wird das Skype for Business Online-Connector-Modul automatisch importiert. Sie erhalten eine Fehlermeldung, und das Modul wird nicht geladen, wenn Sie Windows PowerShell nicht mit Administratorrechten ausführen.

Zusätzlich zu dem Skype for Business Online-Connector-Modul installiert **LyncOnlinePowershell.exe** zwei weitere Komponenten: .NET Framework 4.5 und das Microsoft Visual C++ 2012 Redistributable (x64) Package (Version 11.0.50727). .NET Framework 4.5 stellt die Infrastruktur bereit, mit der .NET-Anwendungen erstellt und ausgeführt werden können, einschließlich Windows PowerShell. Das Visual C++ Redistributable Package installiert Visual C++-Laufzeitkomponenten für Computers, auf denen Microsoft Visual Studio 2012 nicht installiert ist.

## Siehe auch

#### Konzepte

[Konfigurieren eines Computers für Lync Online-Verwaltung](configuring-your-computer-for-skype-for-business-online-management.md)

