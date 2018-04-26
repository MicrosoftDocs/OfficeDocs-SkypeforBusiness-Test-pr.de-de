---
title: Obligatorische und optionale Parameter
TOCTitle: Obligatorische und optionale Parameter
ms:assetid: e766362f-e2e9-4598-a595-fdf5eedd9ad6
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362851(v=OCS.15)
ms:contentKeyID: 56269348
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Obligatorische und optionale Parameter

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Windows PowerShell-Parameter gehören zu einer von zwei Kategorien: obligatorisch oder optional. Ein *obligatorischer Parameter* ist ein Parameter, der angegeben werden muss, wenn Sie den Befehl ausführen. Beispielsweise wird das Cmdlet [Remove-CsUserAcp](remove-csuseracp.md) dazu verwendet, die Zuweisung eines Audiokonferenzanbieters aufzuheben, der zuvor einem Benutzer zugewiesen wurde. Wenn Sie das Cmdlet **the Remove-CsUserAcp** ausführen, müssen Sie den Parameter **Identity** einfügen. Mit diesem Parameter wird dem Cmdlet angegeben, für welchen Benutzer der Audiokonferenzanbieter entfernt werden muss. Wie Sie vermutlich erwarten, ergibt ein Ausführen dieses Befehls ohne Parameter keinen wirklichen Sinn:

    Remove-CsUserAcp

In einem solchen Fall "weiß" das Cmdlet nicht, für welchen Benutzer dessen Audiokonferenzanbieter entfernt werden soll. Daher müssen Sie die Identität des Benutzer angeben:

    Remove-CsUserAcp -Identity "Ken Myer"

Normalerweise werden Sie von Windows PowerShell zu einer Eingabe aufgefordert, wenn Sie einen Befehl ausführen möchten und einen obligatorischen Parameter nicht angegeben haben. Beispielsweise könnten Sie folgenden Befehl eingeben und dann die EINGABETASTE drücken:

    Remove-CsUserAcp

Windows PowerShell führt diesen unvollständigen Befehl nicht aus. Stattdessen werden Sie aufgefordert, den fehlenden obligatorischen Parameter einzugeben:

    Cmdlet Remove-CsUserAcp an der Befehlspipelineposition 1
    Geben Sie Werte für die folgenden Parameter an:
    Identity:

Wenn Sie einen gültigen Wert für den Parameter **Identity** eingeben und die EINGABETASTE drücken, führt Windows PowerShell das Cmdlet **Remove-CsUserAcp** aus und entfernt den Audiokonferenzanbieter. Wenn Sie Ihre Meinung ändern und entscheiden, dass der Befehl doch nicht ausgeführt werden soll, drücken Sie STRG+C, um den Befehl abzubrechen.

Dies ist kein absolut sicheres System, sodass Windows PowerShell nicht immer in der Lage ist, Sie zur Eingabe der jeweils erforderlichen Parameter aufzufordern. Beispielsweise sind einige Cmdlets so konzipiert, dass entweder Parameter A oder Parameter B (aber nicht beide) obligatorisch ist. Möglicherweise werden Sie von Windows PowerShell zur Eingabe von Parameter A und B aufgefordert, der Befehl schlägt dann aber fehl, weil Parameter A und Parameter B nicht im selben Befehl verwendet werden dürfen. Daher empfiehlt es sich, alle erforderlichen Parameter vor dem Ausführen des Befehls einzufügen, statt sich darauf zu verlassen, dass Windows PowerShell zur Eingabe der benötigten Informationen auffordert.

Außerdem ist zu beachten, dass das Formatieren eines Parameterwerts gelegentlich ein nicht sehr intuitiver Vorgang ist. Wenn Sie beispielsweise einen Parameterwert einfügen, der ein Leerzeichen enthält, müssen Sie den Wert in doppelte Anführungszeichen setzen:

    -Identity "Ken Myer"

Anführungszeichen müssen Sie allerdings nur verwenden, wenn Sie den Parameter und dessen Wert als Teil des auszuführenden Befehls eingeben. Wenn Sie versuchen, das Cmdlet **Remove-CsUserAcp** auszuführen, aber versehentlich den Parameter **Identity** nicht angeben, werden Sie von Windows PowerShell zur Eingabe der Benutzeridentität aufgefordert:

    Cmdlet Remove-CsUserAcp an der Befehlspipelineposition 1
    Geben Sie Werte für die folgenden Parameter an:
    Identity:

Nun geben Sie **Ken Myer** in doppelten Anführungszeichen als Wert für den Parameter **Identity** ein:

    Cmdlet Remove-CsUserAcp an der Befehlspipelineposition 1
    Geben Sie Werte für die folgenden Parameter an:
    Identity: "Ken Myer"

Daraufhin schlägt der Befehl mit der folgenden Fehlermeldung fehl:

    Remove-CsUserAcp : Das Verwaltungsobjekt für die Identität ""Ken Myer"" wurde nicht gefunden.

In diesem Fall wurde nach einem Benutzer gesucht, der die Identität "Ken Myer" hat, wobei die doppelten Anführungszeichen als Teile des Parameters **Identity** interpretiert wurden. Wenn Sie zur Eingabe eines Parameterwerts aufgefordert werden, dürfen Sie keine doppelten Anführungszeichen einfügen:

    Cmdlet Remove-CsUserAcp an der Befehlspipelineposition 1
    Geben Sie Werte für die folgenden Parameter an:
    Identity: Ken Myer

Im Vergleich ist ein *optionaler Parameter* genau das, was die Bezeichnung besagt: Der Parameter muss nicht eingegeben werden, damit das Cmdlet ausgeführt werden kann. Beispielsweise hat das Cmdlet **Remove-CsUserAcp** den optionalen Parameter **Name**. Ist der Parameter **Name** in dem Befehl angegeben, wird nur der angegebene Audiokonferenzanbieter entfernt. Der folgende Befehl entfernt den Audiokonferenzanbieter, der den Namen **Fabrikam ACP** hat, entfernt aber keinen anderen der Audiokonferenzanbieter, die Ken Myer zugewiesen sind:

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

Wenn Sie diesen optionalen Parameter nicht angeben, wird der Befehl trotzdem ausgeführt. In diesem Fall löscht **Remove-CsUserAcp** aber alle Audiokonferenzanbieter, die Ken Myer zugewiesen sind:

    Remove-CsUserAcp -Identity "Ken Myer"

## Siehe auch

#### Konzepte

[Einführung in Windows PowerShell und Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

