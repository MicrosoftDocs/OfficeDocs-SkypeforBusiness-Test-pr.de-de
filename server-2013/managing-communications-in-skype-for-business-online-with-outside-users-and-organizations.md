---
title: Verwalten der Kommunikation zwischen externen Benutzern und Organisationen
TOCTitle: Verwalten der Kommunikation zwischen externen Benutzern und Organisationen
ms:assetid: 8a64f0fe-1e79-47d8-835e-548d7ac0757e
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362813(v=OCS.15)
ms:contentKeyID: 56269309
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verwalten der Kommunikation zwischen externen Benutzern und Organisationen

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Die folgenden Cmdlets können für die Verwaltung des Partnerverbunds mit externen Domänen und öffentlichen Instant Messaging-Anbietern verwendet werden:


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
<td><p><a href="new-csedgeallowallknowndomains.md">New-CsEdgeAllowAllKnownDomains</a></p></td>
<td><p>Ermöglicht den Benutzern, mit allen Domänen außer denjenigen zu kommunizieren, die sich auf der Liste der blockierten Domänen befinden.</p>
<p>&quot;Partnerverbund&quot; ist eine Funktion, die es Benutzern ermöglicht, Chatnachrichten und Anwesenheitsinformationen mit Benutzern in anderen Domänen auszutauschen. Normalerweise verwenden Administratoren Listen mit zulässigen und blockierten Domänen, um die externen Domänen anzugeben, mit denen die Benutzer kommunizieren können.</p></td>
</tr>
<tr class="even">
<td><p><a href="new-csedgeallowlist.md">New-CsEdgeAllowList</a></p></td>
<td><p>Beschränkt die Benutzerkommunikation auf eine angegebene Auflistung von Domänen.</p>
<p>Die Benutzer dürfen nur mit Domänen kommunizieren, die sich in der Liste der zulässigen Domänen befinden.</p></td>
</tr>
<tr class="odd">
<td><p><a href="new-csedgedomainpattern.md">New-CsEdgeDomainPattern</a></p></td>
<td><p>Ändern die Listen der zulässigen und blockierten Domänen.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantfederationconfiguration.md">Get-CsTenantFederationConfiguration</a><br />
<a href="set-cstenantfederationconfiguration.md">Set-CsTenantFederationConfiguration</a></p></td>
<td><p>Aktiviert und deaktiviert den Partnerverbund mit anderen Domänen und mit öffentlichen Anbietern.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-cstenanthybridconfiguration.md">Get-CsTenantHybridConfiguration</a><br />
<a href="set-cstenanthybridconfiguration.md">Set-CsTenantHybridConfiguration</a></p></td>
<td><p>Weist die geeigneten Werte in den Hybridkonfigurationseinstellungen zu.</p>
<p>Bei einer Hybridbereitstellung oder einer Bereitstellung mit &quot;geteilten Domänen&quot; verfügen einige Benutzer in der Organisation über Konten, die in Skype for Business Online gehostet werden, während gleichzeitig andere Benutzer über Konten verfügen, die in Lync Server 2013 gehostet werden. Standardmäßig haben Benutzer mit Konten in Skype for Business Online keine Zugriff auf die vollständige Palette der von Enterprise-VoIP gebotenen Features. Damit auch die Skype for Business Online-Benutzer auf diese Enterprise-VoIP-Features zugreifen können, muss der Administrator in den Hybridkonfigurationseinstellungen die geeigneten Werte zuweisen. Diese Werte können nur mit den<strong>CsTenantHybridConfiguration</strong>-Cmdlets verwaltet werden.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantpublicprovider.md">Get-CsTenantPublicProvider</a><br />
<a href="set-cstenantpublicprovider.md">Set-CsTenantPublicProvider</a></p></td>
<td><p>Verwaltet den Partnerverbund mit öffentlichen Anbietern.</p>
<p>Öffentliche Anbieter sind Organisation, die SIP-Kommunikationsdienste für die breite Öffentlichkeit bereitstellen. Wenn Sie eine Partnerverbundbeziehung mit einem öffentlichen Anbieter einrichten, stellen Sie im Prinzip einen Partnerverbund mit allen Benutzern her, deren Konto von diesem Anbieter gehostet wird.</p></td>
</tr>
</tbody>
</table>


Sie können die Partnerverbundeinstellungen sowohl für Domänen im Partnerverbund als auch für öffentliche Anbieter auch im Skype for Business Online Admin Center verwalten:

![Lync Online Admin Center: Organisationseinstellungen](images/Dn362813.f860d03f-5906-49b0-bcc7-7634afe7005e(OCS.15).png "Lync Online Admin Center: Organisationseinstellungen")

## Siehe auch

#### Konzepte

[Die Lync Online-Cmdlets](the-skype-for-business-online-cmdlets.md)  
[Kurzübersicht: Verwenden von Windows PowerShell zum Ausführen von häufig anstehenden Lync Online-Verwaltungsaufgaben](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

