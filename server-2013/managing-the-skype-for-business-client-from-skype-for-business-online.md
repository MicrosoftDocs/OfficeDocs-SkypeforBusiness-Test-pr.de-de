---
title: Verwalten des Lync-Clients
TOCTitle: Verwalten des Lync-Clients
ms:assetid: d1ccc7b6-99ff-4ffd-bd29-9088fb8fe837
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362847(v=OCS.15)
ms:contentKeyID: 56269334
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwalten des Lync-Clients

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Mit den folgenden Cmdlets kann der Lync-Client verwaltet werden:


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
<td><p><a href="get-csimfilterconfiguration.md">Get-CsImFilterConfiguration</a></p></td>
<td><p>Ruft Informationen zu den in Ihrer Organisation verwendeten URI-Einschränkungen ab.</p>
<p>Beim Senden von Chatnachrichten können Benutzer einen URI im Nachrichtentext einbetten, über den andere Gesprächsteilnehmer an eine bestimmte Website oder Freigabe verwiesen werden. Skype for Business Online kann so konfiguriert werden, dass Links mit bestimmten Präfixen blockiert werden oder nicht aktiv sind. Dadurch ist sichergestellt, dass Teilnehmer nicht durch Klicken auf den Link zu der Site gelangen können, auf die der URI verweist. Stattdessen müssen Sie den Link kopieren und manuell in einem Browser einfügen.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cspresencepolicy.md">Get-CsPresencePolicy</a></p></td>
<td><p>Gibt Informationen zu zwei wichtigen Aspekten von Anwesenheitsabonnements zurück: Abonnentenaufforderungen und Kategorieabonnements.</p>
<p>Wenn Sie zur Kontaktliste einer anderen Person hinzugefügt werden, werden Sie standardmäßig mithilfe einer Popupbenachrichtigung darüber informiert. Jede Benachrichtigung gilt als eine Abonnentenaufforderung, bis Sie das angezeigte Popupfenster verwerfen.</p>
<p>Ein Kategorieabonnement entspricht einer Anforderung für eine spezielle Informationskategorie, z. B. eine Anwendung, die Kalenderdaten anfordert.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csprivacyconfiguration.md">Get-CsPrivacyConfiguration</a><br />
<a href="set-csprivacyconfiguration.md">Set-CsPrivacyConfiguration</a></p></td>
<td><p>Konfiguriert Standarddatenschutzwerte in Skype for Business Online, bietet Benutzern aber weiterhin die Möglichkeit, diese Werte zu ändern.</p>
<p>Benutzer können mit Skype for Business Online eine Vielzahl von Anwesenheitsinformationen für andere Benutzer freigeben. Benutzer können Fotos von sich veröffentlichen, ausführliche Standortinformationen bereitstellen und festlegen, dass Anwesenheitsinformationen automatisch für jede Person in der Organisation verfügbar sind (statt nur für Personen in ihren Kontaktlisten). Mit <strong>CsPrivacyConfiguration</strong>-Cmdlets können Administratoren Standarddatenschutzwerte in Skype for Business Online konfigurieren, wobei Benutzer allerdings weiterhin die Möglichkeit haben, diese Werte zu ändern.</p></td>
</tr>
</tbody>
</table>


Eine Teilmenge der Einstellungen der Datenschutzkonfiguration können Sie auch mit dem Skype for Business Online Admin Center verwalten:

![Lync Admin Center: Anwesenheitseinstellungen für privaten Modus](images/Dn362847.eb206b74-844d-4a7b-b1b3-0cfcb6e3614b(OCS.15).png "Lync Admin Center: Anwesenheitseinstellungen für privaten Modus")

## Siehe auch

#### Konzepte

[Die Lync Online-Cmdlets](the-skype-for-business-online-cmdlets.md)  
[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

