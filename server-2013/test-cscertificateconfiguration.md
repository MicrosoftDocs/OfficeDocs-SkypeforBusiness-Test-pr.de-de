---
title: Test-CsCertificateConfiguration
TOCTitle: Test-CsCertificateConfiguration
ms:assetid: 8086bdf7-d283-4666-9f6c-0d5a3a31b3a6
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398647(v=OCS.15)
ms:contentKeyID: 49294566
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsCertificateConfiguration

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den auf dem lokalen Computer verwendeten Lync Server-Zertifikaten zurück. Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Test-CsCertificateConfiguration [-Report <String>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 gibt Informationen zu Zertifikaten zurück, die gegenwärtig von Lync Server (auf dem lokalen Computer) verwendet werden.

    Test-CsCertificateConfiguration

## BEISPIEL 2

Der Befehl in Beispiel 2 ist eine Variante des Befehls in Beispiel 1. In diesem Fall wird jedoch der Parameter "Report" zur Angabe eines Dateipfads (C:\\Logs\\Certificates.xml) für die Ausgabedatei verwendet, die beim Ausführen des Cmdlets **Test-CsCertificateConfiguration** generiert wird.

    Test-CsCertificateConfiguration -Report "C:\Logs\Certificates.xml"

## Detaillierte Beschreibung

Das Cmdlet **Test-CsCertificateConfiguration** ist ein Beispiel für eine "synthetische Transaktion". Anhand synthetischer Transaktionen wird in Lync Server überprüft, ob Benutzer allgemeine Aufgaben wie z. B. das Anmelden beim System, das Austauschen von Chatnachrichten oder das Tätigen von Anrufen im Telefonfestnetz (Public Switched Telephone Network, PSTN) erfolgreich durchführen können. Diese Tests können manuell von einem Administrator oder automatisch von einer Anwendung wie Microsoft System Center Operations Manager (früher Microsoft Operations Manager) durchgeführt werden.

Das Cmdlet **Test-CsCertificateConfiguration** gibt Informationen zu den von Lync Server verwendeten Zertifikaten zurück. Das Cmdlet **Test-CsCertificateConfiguration** wird in erster Linie vom Zertifikat-Assistenten verwendet. Für Administratoren empfiehlt sich der Gebrauch des Cmdlets **Get-CsCertificate** zum Abrufen von Zertifikatinformationen.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsCertificateConfiguration"}

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
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht es Ihnen, einen Dateipfad für die bei der Ausführung des Cmdlets erstellte Protokolldatei anzugeben. Beispiel: -Report &quot;C:\Logs\Certificates.html&quot;. Ist die Datei bereits vorhanden, wird sie bei der Ausführung des Cmdlets überschrieben.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Test-CsCertificateConfiguration** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Mit dem Cmdlet **Test-CsCertificateConfiguration** werden Instanzen des Objekts "Microsoft.Rtc.Management.Deployment,CertificateExists" zurückgegeben.

## Siehe auch

#### Weitere Ressourcen

[Get-CsCertificate](get-cscertificate.md)

