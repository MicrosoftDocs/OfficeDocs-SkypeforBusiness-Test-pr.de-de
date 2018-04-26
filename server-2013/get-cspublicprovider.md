---
title: Get-CsPublicProvider
TOCTitle: Get-CsPublicProvider
ms:assetid: c122505d-7209-4dcb-a888-5c73f58fa68a
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg412945(v=OCS.15)
ms:contentKeyID: 49295294
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPublicProvider

 

_**Letztes Änderungsdatum des Themas:** 2015-03-09_

Gibt Informationen zu den öffentlichen Anbietern zurück, die für die Verwendung in Ihrer Organisation konfiguriert sind. Ein öffentlicher Anbieter ist eine Organisation, die Instant Messaging-, Anwesenheits- und ähnliche Dienste für die breite Öffentlichkeit bietet. Lync Server umfasst drei öffentliche Anbieter, die zwar bereits konfiguriert, aber noch nicht aktiviert sind: Yahoo\!, AIM (AOL) und Messenger (MSN). Dieses Cmdlet wurde in Lync Server 2010 eingeführt.

## Syntax

    Get-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPublicProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Beispiele

## BEISPIEL 1

Der Befehl in Beispiel 1 gibt eine Auflistung aller öffentlichen Anbieter zurück, die für die Verwendung in der Organisation konfiguriert wurden. Beim Aufrufen des Cmdlets **Get-CsPublicProvider** ohne zusätzliche Parameter wird immer eine vollständige Auflistung der öffentlichen Anbieter zurückgegeben.

    Get-CsPublicProvider

## BEISPIEL 2

In Beispiel 2 werden alle öffentlichen Anbieter zurückgegeben, die den Identitätswert "Messenger" aufweisen. Da die Identitätswerte von öffentlichen Anbietern (und von Hostinganbietern) eindeutig sein müssen, gibt dieser Befehl immer nur ein Element zurück.

    Get-CsPublicProvider -Identity "Messenger"

## BEISPIEL 3

In Beispiel 3 werden alle öffentlichen Anbieter zurückgegeben, deren Identitätswert mit dem Buchstaben "W" beginnt. Dazu werden der Parameter "Filter" und der Filterwert "W\*" verwendet.

    Get-CsPublicProvider -Filter W*

## BEISPIEL 4

Der Befehl in Beispiel 4 gibt eine Auflistung aller derzeit deaktivierten öffentlichen Anbieter zurück. Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller öffentlichen Anbieter zurückzugeben, die für die Verwendung in der Organisation konfiguriert sind. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das nur die Anbieter auswählt, bei denen die Eigenschaft "Enabled" den Wert "False" aufweist.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False}

## BEISPIEL 5

In Beispiel 5 werden alle öffentlichen Anbieter zurückgegeben, bei denen die Eigenschaft "VerificationLevel" entweder auf "AlwaysUnverifiable" oder "UseSourceVerification" festgelegt ist. (Überprüfungsstufen können immer auf "AlwaysUnverifiable", "UseSourceVerification" oder "AlwaysVerifiable" festgelegt werden.) Hierzu ruft der Befehl zunächst das Cmdlet **Get-CsPublicProvider** auf, um eine Auflistung aller öffentlichen Anbieter zurückzugeben, die für die Verwendung in der Organisation konfiguriert sind. Diese Auflistung wird dann an das Cmdlet **Where-Object** weitergeleitet, das die Anbieter herausfiltert, bei denen die Eigenschaft "VerificationLevel" nicht den Wert "AlwaysVerifiable" aufweist. Auswirkung: Es werden nur Anbieter herausgefiltert, bei denen die Eigenschaft "VerificationLevel" entweder auf "AlwaysUnverifiable" oder "UseSourceVerification" festgelegt ist.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"}

## Detaillierte Beschreibung

Ein Partnerverbund ist eine Möglichkeit, mit der zwei Organisationen eine Vertrauensstellung einrichten können, die die Kommunikation zwischen den beiden Gruppen erleichtert. Wenn ein Partnerverbund eingerichtet wurde, können Benutzer in beiden Organisationen einander Chatnachrichten senden, Anwesenheitsbenachrichtigungen abonnieren und mithilfe von SIP-Anwendungen wie Lync 2013 miteinander kommunizieren. Lync Server bietet drei Arten des Partnerverbunds: 1) direkter Partnerverbund zwischen Ihrer und einer anderen Organisation, 2) Partnerverbund zwischen Ihrer Organisation und einem öffentlichen Anbieter und 3) Partnerverbund zwischen Ihrer Organisation und einem externen Hostinganbieter.

Ein öffentlicher Anbieter ist eine Organisation, die SIP-Kommunikationsdienste für die breite Öffentlichkeit bietet. Wenn Sie eine Partnerverbundbeziehung mit einem öffentlichen Anbieter einrichten, stellen Sie im Prinzip einen Partnerverbund mit allen Benutzern her, deren Konto von diesem Anbieter gehostet wird. Bei einem Partnerverbund mit Messenger können Benutzer Chatnachrichten und Anwesenheitsinformationen mit allen anderen Benutzern austauschen, die über ein Instant Messaging-Konto für Messenger verfügen.

Um mit einem öffentlichen Anbieter im Partnerverbund zu arbeiten, müssen Sie einen neuen öffentlichen Anbieter erstellen und aktivieren. (Darüber hinaus muss der öffentliche Anbieter eine Partnerverbundbeziehung mit Ihnen einrichten.) Mit dem Cmdlet **Get-CsPublicProvider** können Sie Informationen zu allen öffentlichen Anbietern zurückzugeben, die für die Verwendung in Ihrer Organisation konfiguriert sind.

Dieses Cmdlet kann von folgenden Benutzern ausgeführt werden: Standardmäßig sind Mitglieder der folgenden Gruppen autorisiert, das Cmdlet **Get-CsPublicProvider** lokal auszuführen: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Geben Sie den folgenden Befehl an der Windows PowerShell-Eingabeaufforderung ein, um eine Liste aller rollenbasierten Zugriffssteuerungsrollen zurückzugeben, die diesem Cmdlet zugewiesen wurden (einschließlich der benutzerdefinierten rollenbasierten Zugriffssteuerungsrollen, die Sie selbst erstellt haben):

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPublicProvider"}

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
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Ermöglicht die Verwendung von Platzhalterwerten zur Rückgabe eines oder mehrerer öffentlicher Anbieter. Verwenden Sie folgende Syntax, um beispielsweise eine Auflistung aller öffentlichen Anbieter zurückzugeben, deren Identitätswert mit dem Buchstaben &quot;Y&quot; beginnt: -Filter &quot;Y*&quot;. Verwenden Sie folgende Syntax, um eine Auflistung aller öffentlichen Anbieter zurückzugeben, deren Identitätswert die Zeichenfolge &quot;Windows&quot; enthält: -Filter &quot;*Windows*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Eindeutige ID für den öffentlichen Anbieter, der zurückgegeben wird. Als Identitätswert wird in der Regel der Name der Website verwendet, die die Dienste bereitstellt (z. B. Yahoo!, AOL, MSN).</p>
<p>Sie können beim Angeben des Identitätswerts keine Platzhalter verwenden. Verwenden Sie für die Platzhaltersuche zum Zurückgeben eines oder mehrerer öffentlicher Anbieter stattdessen den Parameter &quot;Filter&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Ruft die Daten zum öffentlichen Anbieter aus dem lokalen Replikat des zentralen Verwaltungsspeichers ab, statt die Daten aus dem zentralen Verwaltungsspeicher selbst abzurufen.</p></td>
</tr>
</tbody>
</table>


## Eingabetypen

Keine. Das Cmdlet **Get-CsPublicProvider** akzeptiert keine weitergeleitete Eingabe.

## Rückgabetypen

Gibt Instanzen des Objekts "Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider" zurück.

## Siehe auch

#### Weitere Ressourcen

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

