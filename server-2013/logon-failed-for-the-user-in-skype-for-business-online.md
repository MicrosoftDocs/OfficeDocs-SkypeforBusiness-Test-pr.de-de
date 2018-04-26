---
title: Fehler bei der Anmeldung des Benutzers
TOCTitle: Fehler bei der Anmeldung des Benutzers
ms:assetid: 006020cd-34d0-4a78-b5b4-e382d95ef04d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn329053(v=OCS.15)
ms:contentKeyID: 56269243
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Fehler bei der Anmeldung des Benutzers

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Bei dem Versuch, eine Remoteverbindung zu Skype for Business Online herzustellen, müssen Sie den Benutzernamen und das Kennwort eines gültigen Skype for Business Online-Benutzerkontos angeben. Andernfalls schlägt die Anmeldung mit einer Fehlermeldung ähnlich der folgenden fehl:

    Get-CsWebTicket : Fehler bei der Anmeldung des Benutzers 'kenmyer@litwareinc.com'. Bitte erstellen Sie ein neues "PSCredential"-Objekt, und vergewissern Sie sich, dass Sie den richtigen Benutzernamen bzw. das richtige Kennwort verwenden.

Wenn Sie davon ausgehen, dass Sie ein gültiges Benutzerkonto verwenden und über das richtige Kennwort verfügen, versuchen Sie erneut, sich anzumelden. Wenn die Anmeldung erneut fehlschlägt, versuchen Sie, sich mit denselben Anmeldeinformationen bei <https://login.microsoftonline.com/> anzumelden. Wenn Sie sich hier ebenfalls nicht anmelden können, kontaktieren Sie den Office 365-Support.

## Siehe auch

#### Konzepte

[Diagnostizieren und Beheben von Problemen mit Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

