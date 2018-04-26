---
title: Verwalten von Lync Online-Besprechungen und -Konferenzen
TOCTitle: Verwalten von Lync Online-Besprechungen und -Konferenzen
ms:assetid: a4d0c070-4df2-47df-a1e2-6ce62600a287
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362833(v=OCS.15)
ms:contentKeyID: 56269326
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwalten von Lync Online-Besprechungen und -Konferenzen

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Mit den folgenden Cmdlets können Besprechungs- und Konferenzeinstellungen verwaltet werden:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-csmeetingroom.md">Disable-CsMeetingRoom</a><br />
<a href="enable-csmeetingroom.md">Enable-CsMeetingRoom</a><br />
<a href="get-csmeetingroom.md">Get-CsMeetingRoom</a><br />
<a href="set-csmeetingroom.md">Set-CsMeetingRoom</a></p></td>
<td><p>Verwaltet Endgeräte für Besprechungsräume.</p>
<p>In Skype for Business Online sind Besprechungsräume eigenständige Computergeräte, die in Konferenzräumen installiert sind und erweiterte Besprechungsfunktionen bieten. Damit Sie diese neuen Endgeräte verwalten können, müssen Sie u. a. ein Exchange-Ressourcenpostfachkonto für das Gerät erstellen und aktivieren und dieses Ressourcenkonto dann für Skype for Business Online aktivieren.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csaudioconferencingprovider.md">Get-CsAudioConferencingProvider</a></p></td>
<td><p>Gibt Informationen zu den Audiokonferenzanbietern zurück, mit denen Ihre Organisation Verträge abgeschlossen hat.</p>
<p>Ein Audiokonferenzanbieter ist ein Drittanbieterunternehmen, das Konferenzdienste für Organisationen bereitstellt. Dazu gehören hochwertige Dienstleistungen wie Simultanübersetzung, Transkription und operatorgestützte Livekonferenzen.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a><br />
<a href="set-csmeetingconfiguration.md">Set-CsMeetingConfiguration</a></p></td>
<td><p>Steuert, welche Arten von Besprechungen Benutzer erstellen können, und legt fest, wie anonyme Benutzer und Benutzer von Einwahlkonferenzen in Besprechungen behandelt werden.</p>
<p>Besprechungen (auch als Konferenzen bezeichnet) sind ein integraler Bestandteil von Skype for Business Online. Mit diesen Cmdlets können Sie Besprechungen beispielsweise so konfigurieren, dass Einwählbenutzer nicht automatisch für die Besprechung zugelassen, sondern in den Wartebereich für die Konferenz weitergeleitet werden. Diese Einwählbenutzer verbleiben im Wartebereich, bis ein Referent sie für die Besprechung zulässt.</p></td>
</tr>
</tbody>
</table>


Eine kleine Teilmenge der Eigenschaften einer Besprechungskonfiguration können Sie auch mit dem Skype for Business Online Admin Center verwalten:

![Lync Admin Center: Eigenschaften für allgemeine Optionen](images/Dn362826.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Lync Admin Center: Eigenschaften für allgemeine Optionen")

## Siehe auch

#### Konzepte

[Die Lync Online-Cmdlets](the-skype-for-business-online-cmdlets.md)  
[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

