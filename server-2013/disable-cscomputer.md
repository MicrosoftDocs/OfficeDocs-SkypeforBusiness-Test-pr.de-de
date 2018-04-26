---
title: Disable-CsComputer
TOCTitle: Disable-CsComputer
ms:assetid: e64128f1-2b53-4569-bf37-90cbbba01b36
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg399023(v=OCS.15)
ms:contentKeyID: 49295728
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsComputer

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Deaktiviert Dienste oder Serverrollen, die von einem Computer entfernt wurden, auf dem Lync Server ausgeführt wird. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Disable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Scorch <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 deaktiviert den lokalen Computer.

    Disable-CsComputer 

## BEISPIEL 2

Der Befehl in Beispiel 2 deaktiviert ebenfalls den lokalen Computer. Mit diesem Befehl wird jedoch nicht nur der Computer deaktiviert, es werden auch Informationen zum Erfolg (oder Misserfolg) dieses Vorgangs in der Datei "C:\\Logs\\Disable.html" gespeichert. Diese Protokolldatei wird durch Hinzufügen des Parameters "Report", gefolgt von dem Pfad zu der Protokolldatei zum Aufzeichnen der Informationen generiert.

    Disable-CsComputer -Report C:\Logs\Disable.html

## Detaillierte Beschreibung

Durch Entfernen eines Diensts oder einer Serverrolle von einem Computer wird die Lync Server-Topologie nicht automatisch aktualisiert. Stattdessen muss der betreffende Dienst bzw. die betreffende Rolle deaktiviert werden, bevor eine vollständige Aktualisierung der Änderungen in der Topologie erfolgen kann. Administratoren können mit dem Cmdlet **Disable-CsComputer** beliebige Dienste oder Serverrollen deaktivieren, die von dem lokalen Computer entfernt wurden.

Sofern Sie nicht den Parameter "Scorch" verwenden, wird die Lync Server-Software vom Cmdlet **Disable-CsComputer** nicht deinstalliert. Stattdessen wird der Computer daran gehindert, in seiner zuvor zugewiesenen Rolle zu funktionieren.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Sie müssen ein lokaler Administrator und Mitglied der Domäne sein, um das Cmdlet **Disable-CsComputer** lokal auszuführen.

## Parameter


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Erforderlich</th>
<th>Typ</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Fordert Sie vor der Ausführung des Befehls zum Bestätigen auf.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Unterdrückt die Anzeige von Meldungen bei nicht schwerwiegenden Fehlern, die beim Ausführen des Befehls auftreten können.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Vollqualifizierter Domänenname (FQDN) eines globalen Katalogservers in Ihrer Domäne. Dieser Parameter ist nicht erforderlich, wenn das Cmdlet <strong>Disable-CsComputer</strong> auf einem Computer ausgeführt wird, für den ein Konto in der Domäne vorhanden ist.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN eines Domänencontrollers, auf dem die globalen Einstellungen gespeichert sind. Wenn die globalen Einstellungen im Systemcontainer von Active Directory-Domänendienste gespeichert sind, muss dieser Parameter auf den Stammdomänencontroller verweisen. Wenn die globalen Einstellungen im Konfigurationscontainer gespeichert sind, kann jeder Domänencontroller verwendet werden, und dieser Parameter kann ausgelassen werden.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, einen Dateipfad für die bei der Ausführung des Cmdlets erstellte Protokolldatei anzugeben. Beispiel: -Report &quot;C:\Logs\DisableComputer.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Scorch</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Deinstalliert alle Lync Server-Dienste und Serverrollen für den lokalen Computer.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Beschreibt die Auswirkungen einer Ausführung des Befehls, ohne den Befehl tatsächlich auszuführen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Disable-CsComputer** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Keine. Mit dem Cmdlet **Disable-CsComputer** werden Instanzen des Objekts "Microsoft.Rtc.Management.Deploy.Internal.Machine" deaktiviert.

## Siehe auch

#### Weitere Ressourcen

[Enable-CsComputer](enable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

