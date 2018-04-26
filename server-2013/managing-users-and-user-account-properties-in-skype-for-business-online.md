---
title: Verwalten von Benutzern und Benutzerkontoeigenschaften
TOCTitle: Verwalten von Benutzern und Benutzerkontoeigenschaften
ms:assetid: 5d13ab15-0e12-4bd0-a970-f130de980404
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362790(v=OCS.15)
ms:contentKeyID: 56269278
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwalten von Benutzern und Benutzerkontoeigenschaften

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Mit den folgenden Cmdlets werden die Skype for Business Online-Benutzerkonten verwaltet.


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
<td><p><a href="get-csonlineuser.md">Get-CsOnlineUser</a></p></td>
<td><p>Gibt Informationen über die Benutzer zurück, deren Konten unter Ihrem Skype for Business Online-Mandanten gehostet werden.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csuseracp.md">Get-CsUserAcp</a><br />
<a href="remove-csuseracp.md">Remove-CsUserAcp</a><br />
<a href="set-csuseracp.md">Set-CsUserAcp</a></p></td>
<td><p>Ermöglicht das Zuweisen, Ändern oder Aufheben der Zuweisung eines Audiokonferenzanbieters für einzelne Benutzer.</p>
<p>Ein Audiokonferenzanbieter ist ein Drittanbieterunternehmen, das Organisation mit Konferenzdiensten einschließlich hochwertiger Dienste wie Simultandolmetschen, Transkription und operatorgestützte Livekonferenzen ausstattet.</p>
<p>Dieses Cmdlet gibt keine Informationen zu den Audiokonferenzanbietern zurück, die den Benutzern zugewiesen werden können. Führen Sie für solche Informationen stattdessen diesen Befehl aus:</p>
<pre><code>Get-CsAudioConferencingProvider</code></pre></td>
</tr>
</tbody>
</table>



> [!WARNING]
> Das Set-CsUser-Cmdlet gehört ebenfalls zu der Reihe der Cmdlets, die für Skype for Business Online-Administratoren zur Verfügung stehen, kann derzeit jedoch nicht für die Verwaltung von Skype for Business Online verwendet werden. Einzige Ausnahme ist das Festlegen des Parameters AudioVideoDisabled. Wenn Sie versuchen, das Cmdlet mit einem anderen Parameter auszuführen, schlägt es mit einer Fehlermeldung ähnlich der folgenden fehl:<BR>"Die SIP-Adresse ("SipAddress") konnte nicht festgelegt werden". Dieser Parameter ist in PowerShell für Remotemandanten eingeschränkt."



Audiokonferenzanbieter können Benutzerkonten auch im Skype for Business Online Admin Center zugewiesen werden bzw. die Zuweisung kann auch hier aufgehoben werden:

![Lync Admin Center: Eigenschaften von Einwahlkonferenzen](images/Dn362790.0c61f0c2-8aef-4020-a0a8-02580d43092a(OCS.15).png "Lync Admin Center: Eigenschaften von Einwahlkonferenzen")

## Siehe auch

#### Konzepte

[Die Lync Online-Cmdlets](the-skype-for-business-online-cmdlets.md)  
[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

