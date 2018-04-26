---
title: Verwalten von Exchange Unified Messaging und gehosteten Voicemails
TOCTitle: Verwalten von Exchange Unified Messaging und gehosteten Voicemails
ms:assetid: 844bf8d5-e093-4dcd-abcf-48dc70e8c73c
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362822(v=OCS.15)
ms:contentKeyID: 56269294
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwalten von Exchange Unified Messaging und gehosteten Voicemails

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Die folgenden Cmdlets können für die Verwaltung der Exchange-UM-Einstellungen (Unified Messaging) und der Richtlinien für gehostete Voicemail verwendet werden:


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
<td><p><a href="get-csexumcontact.md">Get-CsExUmContact</a></p>
<p><a href="new-csexumcontact.md">New-CsExUmContact</a></p>
<p><a href="remove-csexumcontact.md">Remove-CsExUmContact</a></p>
<p><a href="set-csexumcontact.md">Set-CsExUmContact</a></p></td>
<td><p>Erstellt und verwaltet die Kontaktobjekte, die für die Dienste &quot;Automatische Telefonzentrale&quot; und &quot;Abonnentenzugriff&quot; verwendet werden, wenn Exchange UM als gehosteter Dienst ausgeführt wird.</p>
<p>Skype for Business Online arbeitet mit Exchange UM, um diverse VoIP-bezogenen Features wie &quot;Automatische Telefonzentrale&quot; und &quot;Abonnentenzugriff&quot; bereitzustellen. Die automatische Telefonzentrale bietet einen Anrufbeantworter und ermöglicht die automatische Weiterleitung von Anrufen an die zuständigen Personen . Über den Abonnentenzugriff können Benutzer die Verbindung zu Exchange UM herstellen und E-Mails, Sprachnachrichten, Kontakte und Kalenderinformationen abrufen.</p>
<p>Wenn Exchange UM als gehosteter Dienst bereitgestellt wird, müssen die Kontaktobjekte für die Dienste &quot;Automatische Telefonzentrale&quot; und &quot;Abonnentenzugriff&quot; mit Windows PowerShell erstellt werden. Diese Objekte werden mit den <strong>CsExUmContact</strong>-Cmdlets erstellt und verwaltet.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cshostedvoicemailpolicy.md">Get-CsHostedVoicemailPolicy</a></p>
<p><a href="grant-cshostedvoicemailpolicy.md">Grant-CsHostedVoicemailPolicy</a></p></td>
<td><p>Verwaltet die in der Organisation verwendeten Richtlinien für gehostete Voicemails. Mit Richtlinien für gehostete Voicemails wird festgelegt, wie nicht angenommene Anrufe an den Exchange UM-Dienst weitergeleitet werden. Diese Richtlinien gelten nur für Benutzer, die in Exchange UM für gehostete Voicemails aktiviert wurden. Wenn Sie überprüfen möchten, ob ein Benutzer für gehostete Voicemails aktiviert wurde, geben Sie an der Windows PowerShell-Eingabeaufforderung einen Befehl wie den folgenden ein:</p>
<pre><code>Get-CsOnlineUser -Identity &quot;kenmyer@litwareinc.com&quot; | Select-Object HostedVoiceMail</code></pre></td>
</tr>
</tbody>
</table>


Sie können die Exchange UM-Einstellungen und die Richtlinien für gehostete Voicemails nicht im Skype for Business Online Admin Center verwalten.

## Siehe auch

#### Konzepte

[Die Lync Online-Cmdlets](the-skype-for-business-online-cmdlets.md)  
[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

