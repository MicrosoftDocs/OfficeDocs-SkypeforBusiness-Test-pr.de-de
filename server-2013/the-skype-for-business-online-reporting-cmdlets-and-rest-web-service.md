---
title: 'Lync Online: Die Lync Online-Berichterstellungs-Cmdlets und der REST-Webdienst'
TOCTitle: Die Lync Online-Berichterstellungs-Cmdlets und der REST-Webdienst
ms:assetid: cadd73a7-c08a-4102-b73a-ccb3ad4987bf
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362845(v=OCS.15)
ms:contentKeyID: 56269331
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Die Lync Online-Berichterstellungs-Cmdlets und der REST-Webdienst

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Im Zusammenhang mit den Berichterstellungsfeatures bietet Skype for Business Online Zugriff auf fünf Windows PowerShell-Cmdlets, mit denen entsprechende Berichte erstellt und die außerdem von Administratoren verwendet werden können, um angepasste Berichtsdaten zurückzugeben. Skype for Business Online beinhaltet außerdem den REST-Webdienst (Representational State Transfer), der von Entwicklern dazu verwendet werden kann, angepasste Berichtsinformationen abzurufen.

Folgende Berichtscmdlets sind für Administratoren verfügbar:

  - **Get-CsActiveUserReport**: stellt Informationen zur Anzahl der aktiven Benutzer bereit (dies sind Benutzer, die sich bei Skype for Business Online angemeldet und an mindestens einer Konferenz- oder Peer-to-Peer-Kommunikationssitzung teilgenommen haben)

  - **Get-CsAVConferenceTimeReport**: stellt Informationen zu den Zeitdauern (in Minuten) bereit, die Benutzer in Audio-/Videokonferenzen verbracht haben

  - **Get-CsConferenceReport**: stellt Informationen zur Anzahl und zu den Typen der Konferenzen bereit, an denen Benutzer teilgenommen haben

  - **Get-CsP2PAVTimeReport**: stellt Informationen zu den Zeitdauern (in Minuten) bereit, die Benutzer in Per-to-Peer-Sitzungen verbracht haben, die Audio-/Videodatenströme umfasst haben

  - **Get-CsP2PSessionReport**: stellt Informationen zur Anzahl und zu den Typen der Per-to-Peer-Sitzungen bereit, an denen Benutzer teilgenommen haben

Zumeist sollten Administratoren die Berichte verwenden, die im Office 365 Admin Center verfügbar sind: Diese Berichte werden nicht nur automatisch erstellt, sondern stellen auch grafische Darstellungen der Daten bereit. Üblicherweise lassen sich diese grafischen Darstellungen einfacher interpretieren als die reinen Zahlenwerte, die von den Berichterstellungs-Cmdlets zurückgegeben werden. Administratoren, die mit Windows PowerShell vertraut sind, können die Berichterstellungs-Cmdlets aber zur Rückgabe von Daten verwenden, die nicht ohne Weiteres aus den Lync Online-Berichten verfügbar sind. Beispielsweise geben die Berichterstellungs-Cmdlets Informationen zu den Sitzungsdauern (die jeweilige Zeitspanne in Minuten, die eine Sitzung gedauert hat) zurück. Sitzungsdauern sind nicht verfügbar, wenn die Lync Online-Berichte verwendet werden. Ähnlich werden in der täglichen Ansicht der Lync Online-Berichte nur Informationen für die vorangegangenen 7 Tage angezeigt. Wenn Sie die täglichen Gesamtzahlen für einen anderen Tag (beispielsweise ein Datum, das drei Wochen zurückliegt) anzeigen möchten, können Sie dazu die Berichterstellungs-Cmdlets verwenden.

Administratoren interessieren sich möglicherweise auch für den Artikel [Verwenden von Excel zum Abrufen von Office 365-Berichterstellungsdaten](http://msdn.microsoft.com/de-de/library/dn781442.aspx), in dem erläutert wird, wie die OData-Datenabfragefunktion in Microsoft Excel zur Erstellung eines benutzerdefinierten Office 365-Berichts verwendet wird, Mit benutzerdefinierten Berichten können Sie vorgeben, welche (und wie viele) Daten vom Office 365-Berichterstellungsdienst zurückgegeben werden. Mit benutzerdefinierten Berichten können Sie beispielsweise auch angeben, wie die Daten gruppiert und sortiert werden sollen, und Zugriff auf Informationen bereitstellen, die in den Office 365 Admin Center-Berichten nicht verfügbar sind.

Administratoren mit Entwicklungserfahrung können den REST-Webdienst verwenden, um Informationen abzurufen, die nicht im Skype for Business Online Admin Center angezeigt werden. Der REST-Dienst ist insofern mit dem SOAP-Dienst vergleichbar, als jede Technologie eine Möglichkeit bietet, XML-Daten zwischen einem Client und einem Server auszutauschen. Der REST-Dienst hat aber mindestens zwei Vorteile gegenüber dem SOAP-Dienst. Der erste besteht darin, dass REST ein standardisiertes Format für XML-Datenübertragungen verwendet, das als ATOM-Veröffentlichungsformat bezeichnet wird. Im Gegensatz dazu wird im SOAP-Dienst ein Nicht-Standardformat verwendet, wenn Daten übertragen werden. Außerdem können mit REST Daten über Netzwerke hinweg übertragen werden, von denen alle HTTP-Verben außer GET and POST blockiert werden.

## Siehe auch

#### Weitere Ressourcen

[Lync Online-Berichte](https://technet.microsoft.com/de-de/library/dn362827\(v=ocs.15\))  
[Der Office 365-Berichterstattungswebdienst](http://msdn.microsoft.com/de-de/library/office/jj984325.aspx)  
[Informationen zum Office 365-Berichterstattungswebdienst](http://msdn.microsoft.com/de-de/library/office/jj984321.aspx)  
[Cmdlets für die Berichterstellung in Exchange Online](http://technet.microsoft.com/de-de/library/jj200780\(v=exchg.150\).aspx)  
[Verwenden von Excel zum Abrufen von Office 365-Berichterstellungsdaten](http://msdn.microsoft.com/de-de/library/dn781442.aspx)

