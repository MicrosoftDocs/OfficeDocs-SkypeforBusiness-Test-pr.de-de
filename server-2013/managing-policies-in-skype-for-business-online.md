---
title: Verwalten von Richtlinien
TOCTitle: Verwalten von Richtlinien
ms:assetid: 91372888-a96e-44db-a0dc-d08facbfce87
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362826(v=OCS.15)
ms:contentKeyID: 56269317
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwalten von Richtlinien

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Mit den folgenden Cmdlets werden Skype for Business Online-Richtlinien verwaltet. Mit Richtlinien werden die Skype for Business Online-Features festgelegt, die für die Benutzer und für die Organisation an solche zur Verfügung stehen.


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
<td><p><a href="get-csclientpolicy.md">Get-CsClientPolicy</a><br />
<a href="grant-csclientpolicy.md">Grant-CsClientPolicy</a></p></td>
<td><p>Mit Clientrichtlinien werden die Lync-Clientfeatures festgelegt, die für Benutzer zur Verfügung stehen. So können Sie für einige Benutzer beispielsweise die Möglichkeit eröffnen, Dateien an andere Benutzer zu übertragen, für andere hingegen nicht.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csconferencingpolicy.md">Get-CsConferencingPolicy</a><br />
<a href="grant-csconferencingpolicy.md">Grant-CsConferencingPolicy</a></p></td>
<td><p>Konferenzrichtlinien legen die in einer Konferenz zur Verfügung stehenden Funktionen fest. Hierzu gehört alles, also beispielsweise die Verfügbarkeit von IP-Audio und -Video für die Konferenz oder die zulässige Höchstanzahl von Teilnehmern einer Besprechung.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csexternalaccesspolicy.md">Get-CsExternalAccessPolicy</a><br />
<a href="grant-csexternalaccesspolicy.md">Grant-CsExternalAccessPolicy</a></p></td>
<td><p>Richtlinien für den externen Zugriff werden verwendet, um festzulegen, ob Ihre Benutzer mit Benutzern aus Partnerverbunddomänen kommunizieren dürfen und/oder ob sie mit Benutzern kommunizieren dürfen, die Konten bei öffentlichen Instant Messaging-Anbietern wie Windows Live oder AOL unterhalten.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csvoicepolicy.md">Get-CsVoicePolicy</a><br />
<a href="grant-csvoicepolicy.md">Grant-CsVoicePolicy</a><br />
<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a></p></td>
<td><p>VoIP-Richtlinien werden zum Verwalten von Enterprise-VoIP-Funktionen verwendet, z. B. für das gleichzeitige Klingeln (die Möglichkeit, ein zweites Telefon läuten zu lassen, wenn jemand die Nummer Ihres Bürotelefons wählt) und die Anrufweiterleitung.</p></td>
</tr>
</tbody>
</table>


Sie können ausgewählte Einstellungen für Konferenzrichtlinien auch über das Skype for Business Online Admin Center verwalten:

![Lync Admin Center: Eigenschaften für allgemeine Optionen](images/Dn362826.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Lync Admin Center: Eigenschaften für allgemeine Optionen")

Sie können die Richtlinien für den externen Zugriff ebenfalls über das Skype for Business Online Admin Center verwalten:

![Admin Center: Optionen für externe Kommunikation](images/Dn362826.e5cfb159-b096-463e-b1ef-2b42eb29168a(OCS.15).png "Admin Center: Optionen für externe Kommunikation")

## Siehe auch

#### Konzepte

[Die Lync Online-Cmdlets](the-skype-for-business-online-cmdlets.md)  
[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

